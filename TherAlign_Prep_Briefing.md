# TherAlign — Pre-Meeting Briefing (from the docs Dachuan shared)

Everything below is pulled from the onboarding deck, Vishnu's handoff doc, and the interface mocks. Skim this and you'll walk in genuinely up to speed.

---

## TL;DR — the one-paragraph version (say this if asked "what do we do?")
TherAlign **prevents prior authorization instead of automating it.** Everyone else files the PA paperwork faster; TherAlign helps the clinician **write a covered script in the first place** — checking coverage as the prescription is typed, and (the differentiator) backing the covered alternative with **real-world evidence that it's clinically equivalent**, so the prescriber can trust the switch. No PA is ever triggered, and the prescriber always decides.

**The tagline framing:** *"Prevention, not automation."* / *"Write the covered script first."*

---

## 1. The problem (know these 4 numbers)
Prior authorization (PA) is a tax on every prescriber's week:
- **13 hrs/week** of physician + staff time per provider (on ~39 PAs filed) — *AMA 2024*
- **40%** of physicians employ staff whose *only* job is PA — *AMA 2024*
- **$90B+/year** spent nationally on PA administration — *CAQH 2024*
- **82%** of physicians report patients **abandoning therapy** because of PA — *AMA 2024*
- (Bonus: 19% report a PA-driven hospitalization — the harm isn't just admin cost.)

## 2. Why the status quo fails
- **PA automation (ePA)** just files the same paperwork faster — peer-reviewed evidence shows it speeds the *payer's* decision, **not the provider's workload**. A faster "no" is still a no.
- **Real-Time Prescription Benefit (RTPB)** — the coverage rails — is already built into ~every EHR (Epic, athenahealth, Cerner; 80%+ of prescribers). But it **sits idle**: only ~6–30% routine use, and just a **28% switch rate even when a PA-free alternative is shown.**
- **The insight / the wedge:** raw coverage data doesn't change a prescription — *a covered alternative a clinician can trust does.* That trust layer (real-world evidence) is what's missing, and what TherAlign adds.

## 3. How it works — 5 steps, in the seconds before signing
1. **Checked as you type** — coverage verified autofill-style in the composer. **Green = covered, done. Red = not covered.**
2. **Guideline preselection** — reads the diagnosis, locates the patient in the treatment algorithm, preselects guideline-recommended alternatives.
3. **Live benefit check** — each candidate run against the patient's *actual* pharmacy benefit via **RTPB aggregators** (Surescripts, DrFirst, CenterX).
4. **⭐ Efficacy engine (THE differentiator)** — runs a real-time **active-comparator, new-user study** on real-world EHR data — a **target-trial emulation for this patient**, not a static equivalence list.
5. **Covered switch, inline** — a covered, clinically-equivalent alternative surfaces in the workflow. **Switch & sign → therapy starts today.**

## 4. The interface (two cases)
- **Covered:** TherAlign's entire footprint is a **green dot** + copay inline. Zero added clicks.
- **Not covered:** a **red flag inline** in the med field; clicking it opens the **TherAlign card in the Epic sidecar** (the same slot ambient-AI tools like **Abridge** use in Epic today). Card shows the recommended covered alternative, copay vs retail, "no PA expected," evidence/stability tags, and a ranked list.
- **Transparency pane:** click the ⓘ and it shows **cohort, inclusion/exclusion criteria, study design, and confidence intervals** — *never a black box.* The prescriber always decides.

## 5. The tech / plumbing (this is your world)
- **CDS Hooks** (order-select) raises the flag → **SMART on FHIR** panel renders the interface → **RTPB via licensed aggregators.**
- **Epic (Hyperspace) is the first target**; the design is **EHR-agnostic** (athenahealth included).
- **Repos (multi-repo prototype, per Vishnu's handoff):**
  - `epic-app` — Next.js SMART-on-FHIR **frontend** + **mock FHIR server** (deployed on Cloud Run). Owns SMART launch/callback/token flow, patient dashboard, medication table, evidence dialog.
  - `theralign-backend` — **Firebase Functions** (`generateMedicationAlternatives`): RxNorm lookup, indication inference, **PubMed** evidence, **AHA/ACC guideline fallback**, formulary/tier/PA logic, **Gemini** synthesis.
  - `theralign-health` (marketing site), `fhir-tutorial` (learning), `theralign` (Diana's offline Python/Synthea pipeline).
- **Critical architecture boundary:** **Gemini only formats/synthesizes.** The **backend deterministically controls** candidate eligibility, guideline labels, and PA results. The **frontend only displays** the backend response — it must not invent alternatives, evidence, or PA. *(This is exactly your grounded-AI / provenance wheelhouse — lean into it.)*
- **Live demo:** `gemini.theralignhealth.com` — GCP project `theralign-health`, region `us-central1`. Backend endpoint is POST-only.

## 6. Where the build stands (likely what you'll work on)
- **Working now:** an end-to-end demo exists, but it renders on the **encounter summary page** — *not where the prescribing decision actually happens.*
- **Moving to:** relocate the experience to **where the prescription composer lives** — inline flag in the med field + full card in the **Epic sidecar.** → **This is the stated next step, so it's probably your first big area.**
- **Design rule:** EHR-agnostic; Epic first via CDS Hooks + SMART on FHIR.

## 7. Open work & risks (good to reference — shows you read closely)
1. **Real-world evidence** (Diana's Synthea/MIMIC-IV pipeline) is the **main unfinished path**. The demo currently uses **PubMed + AHA/ACC fallback**, not a validated real-world-outcomes model.
2. Diana's Python pipeline is **offline/batch**, architecturally different from the **real-time Node/Firebase backend** — someone has to decide integrate vs translate vs keep separate.
3. **Observation support** (BP, eGFR, creatinine, etc.) needs real-EHR validation beyond the mock.
4. PubMed evidence is **thin for many drugs** (backend is intentionally conservative → shows "Insufficient PubMed evidence").
5. Mock FHIR server deploy is **manual**; demo is **investor/internal only, NOT clinical use.**

## 8. Team & traction
- **Dachuan Chen** (PharmD) — CEO / Clinical Lead (your interviewer/manager).
- **Diana** (PhD) — real-world evidence / data science (the Synthea pipeline).
- **Eric Swidler** — CTO / tech lead.
- Founded **Mar 2025** → **1st place MIT Hacking Medicine GrandHack** → Web Summit ALPHA → MIT Beyond Hack finalist → **now in binding-LOI talks with a 100+ provider, PE-backed dermatology group in the SE US.**

## 9. The business case (one-liner)
**$3.20 returned per $1 of subscription** — $200/provider/month; ~**$1.58M net annual value** for a 300-prescriber system; **zero-risk pilot** (1–2 sites, no IT project, $0 pilot fee).

---

## 10. Smart questions to ask in the meeting
- "Is my first focus **relocating the experience from the encounter page to the prescription composer + Epic sidecar**?"
- "Do we have an **Epic sandbox** yet, or are we still developing against the mock FHIR server?"
- "How do you want to handle **Diana's real-world-evidence pipeline** vs the current PubMed/guideline fallback — is integrating that on the near-term roadmap?"
- "What's the target and timeline for the **dermatology-group pilot**? What has to be true in the product for it?"
- "Where do you most want an extra set of hands first — frontend/composer, the backend alternatives logic, or evidence?"

## 11. Talking points that show you "get it" (leverage your background)
- **"Prevention, not automation"** — repeat their framing; it signals you understood the wedge.
- **Trust & transparency** — "The transparency pane and the 'Gemini synthesizes, backend controls' boundary is exactly the grounded, provenance-first AI I've built (AgenticSearch) — I care a lot about not shipping a black box in a clinical setting." *This is your single strongest connection.*
- **The efficacy engine** = target-trial emulation / active-comparator new-user design — nod that you understand why that's harder and more trustworthy than a static equivalence list.
- Your **secure clinical backend** experience (Wysa/NHS, auth, audit logging) maps to the PHI/HIPAA + reliability needs here.

**Golden rule for the meeting** (their own words): *"Questions? Ask early, ask often."* Curiosity and coachability are exactly what they value — so ask.
