# TherAlign Health — Interview Prep
**Round:** Non-Technical Interview (behavioral + "how would you solve X")
**When:** Tue June 9, 2026, 2:00–3:00 PM ET
**Interviewer:** Dachuan Chen, PharmD — Clinical Lead, CEO & Co-Founder (the *clinical* founder)
**Other co-founder:** Eric Swidler — CTO / technical co-founder (Staff Software Engineer @ Panorama Education); a later round may be with him
**Traction signal:** TherAlign won **1st Place @ MIT Hacking Medicine** (good to know / reference warmly)
**Role:** Founding Software Engineer Intern (summer, remote)
**Referred by:** Vishnu Bheem Reddy (your MS CS batchmate, was the founding SWE intern Jan–Apr 2026)

---

## 0. Glossary — decode the jargon first

**The healthcare / domain terms (these matter most with a clinical founder):**

- **Prior Authorization (PA)** — when a doctor prescribes a drug, the insurer often requires approval *before* they'll pay for it. The doctor submits paperwork, the insurer reviews, and it can take days and get denied. This delay/denial is the core pain TherAlign is killing. "Stop Waiting" = stop waiting on PA.
- **Formulary** — the list of drugs a specific insurance plan covers (and at what tier/cost). A drug "on formulary" is covered; "off formulary" usually needs PA or isn't covered. TherAlign checks this so the doctor picks something already covered.
- **Payer** — the insurance company (the one who pays). Each payer has its own formulary and PA rules.
- **Step therapy** — when a payer makes you try a cheaper drug first before approving a pricier one. Another source of PA friction.
- **Comparative efficacy** — evidence on which of several drugs actually works better for a condition. TherAlign uses this so the covered alternative it suggests is also clinically sound.
- **Clinical Decision Support (CDS)** — software that gives clinicians recommendations at the point of care (here: "this covered alternative is appropriate and likely to be approved"). TherAlign *is* a CDS tool.
- **PHI / HIPAA** — PHI = Protected Health Information (a patient's identifiable health data). HIPAA = the US law governing how you must protect it. Why your Wysa security/audit-logging experience matters.

**The EHR / integration terms:**

- **EHR (Electronic Health Record)** — the software system where clinicians store patient charts, write prescriptions, etc. The doctor lives in the EHR all day.
- **Epic (Epic Systems)** — the largest EHR vendor in the US; a huge share of hospitals run on it. "Integrating with Epic" = making TherAlign work inside the system doctors already use, so they don't switch apps. TherAlign is building this (per Eric's letter).
- **FHIR** (say "fire," *Fast Healthcare Interoperability Resources*) — the standard data format/API for exchanging health data between systems. Think "the REST API standard for healthcare." It's how TherAlign reads a patient's meds/conditions from the EHR.
- **SMART on FHIR** — a standard that lets a third-party app (like TherAlign) securely launch *inside* an EHR and access its FHIR data with the right permissions. It's "FHIR + a login/permission layer for apps."
- **OAuth2 / PKCE** — the secure login/authorization protocol behind SMART on FHIR. OAuth2 = the standard way an app gets permission to access data on a user's behalf without seeing their password. PKCE = an extra security step in that flow for apps that can't keep a secret safe. (You already know OAuth-style auth from your backend work.)
- **Mock FHIR server** — a fake EHR that returns FHIR data for local testing, so you can build without a real hospital connection.

**The drug-data / AI terms:**

- **RxNorm** — a standardized US naming system for drugs (maintained by the NIH). It maps all the brand/generic names of a medication to one normalized concept, so software can reason about drugs reliably instead of matching messy text.
- **PubMed** — the free NIH database of medical research literature. TherAlign pulls evidence from it to back recommendations. ("Evidence extraction from medical literature" = mining PubMed — your AgenticSearch wheelhouse.)
- **Gemini** — Google's large language model (their version of GPT). TherAlign uses it for "structured output" = forcing the LLM to return clean, validated fields (e.g., a JSON of {drug, reason, evidence}) rather than free-form text.
- **Provenance (in AI)** — keeping a traceable record of *where each piece of an AI output came from* (which source, which rule). Critical for trust in clinical AI — you built "cell-level provenance" in AgenticSearch.
- **Rule-based fallback** — when the AI is uncertain or unavailable, fall back to hard-coded, deterministic logic instead of guessing. A safety net.
- **RAG (Retrieval-Augmented Generation)** — give an LLM real retrieved documents (e.g., PubMed abstracts, formulary rules) to ground its answer, instead of relying on what it memorized. Reduces hallucination — central to trustworthy clinical AI.

**The infra terms:**

- **GCP (Google Cloud Platform)** — Google's cloud (their AWS). TherAlign runs on it.
- **Firebase** — Google's app-development platform on top of GCP (hosting, database, auth, serverless functions). TherAlign's backend.
- **Serverless / Cloud Functions / Cloud Run** — running code without managing servers; the cloud spins it up on demand and scales automatically. Vishnu deployed serverless backend services on GCP. Cloud Run = serverless containers; Cloud Functions = serverless single functions.
- **Secret Manager** — a GCP service for safely storing API keys/credentials (not in code).

---

## 1. What TherAlign does (say it in one breath)

> TherAlign is an AI clinical-decision-support tool that helps providers prescribe medications that are both clinically right *and* covered by the patient's insurance — so prescriptions don't get stuck in prior-authorization delays and denials. Tagline: **"Stop Waiting. Start Prescribing."**

The problem they're attacking:
- Prior authorization (PA) is a massive pain — physicians do ~40+ PAs/week, most say they don't have time, and patients wait or abandon treatment. The AMA has publicly warned PA is harming patients (TherAlign posts about this).
- TherAlign's angle is **prevention**: surface a clinically-appropriate, *already-covered* option at the point of prescribing, instead of fighting the denial afterward.

The product (what Vishnu built, what you'd extend) — confirmed by both founders' recommendation letters:
- A **provider-facing medication review app** that launches inside the EHR via **SMART on FHIR** (OAuth2/PKCE), pulls patient + medication data over FHIR, shows a medication-review table with alternatives.
- **Epic Systems integration** — they're building interoperability with Epic, the most widely used EHR in the US (Eric's letter calls this out specifically).
- **AI/ML models that predict medication efficacy and prior-authorization approval likelihood** — so a provider sees not just "is it covered" but "how likely is this to get approved and to work."
- **Evidence extraction from medical literature** (PubMed) to back recommendations with comparative-efficacy insight — *this is your exact wheelhouse.*
- Backend = **serverless on Google Cloud / Firebase**, using **RxNorm** (drug normalization), **rule-based fallbacks**, and **Gemini structured output**. Strong emphasis on **documentation** (Eric praised Vishnu's architecture/infra/deployment docs).
- Stage: **very early / fast-moving startup** — prototype for investor, clinical, and product demos. **1st place at MIT Hacking Medicine**, present at **Web Summit Lisbon 2025**. Founding-engineer-intern = own real surface area, ramp fast, lots of ambiguity.

**Why this matters for the interview:** Dachuan is a *pharmacist and clinician*, not an engineer. This round tests whether you (a) genuinely get the healthcare problem, (b) can explain technical work to a non-technical clinical founder, (c) are a reliable self-starter who can own ambiguous work remotely, and (d) actually want to be here. Lead with clarity and impact, not jargon.

---

## ⭐ Most important: what Dachuan literally said he values

In his recommendation for Vishnu, Dachuan spelled out exactly what he screens for. **Mirror these traits in how you show up** — they matter more than any single answer:

- **Curiosity & coachability** — "willing to ask questions, take feedback, keep improving his understanding of both the technology and the healthcare problem." → So *ask thoughtful clinical questions*, react to his points with genuine interest, and don't act like you have it all figured out.
- **Learning the clinical context, not just coding** — he valued that Vishnu worked to understand *clinical logic, the product vision, and the patient problem*. → Show you want to understand *why* a prescription gets denied and what it does to a patient, not just the API.
- **Comfort with ambiguity** — "joined at an early, fast-moving stage… work through ambiguity as we shaped the technical direction." → Lean into your Sonare/AgenticSearch stories where the spec wasn't handed to you.
- **Growing fast with meaningful responsibility** — he rewards ownership. → Your annotation-tool story (saw it, built it, owned it) is perfect.

Eric (CTO) separately valued: **broad scope, fast learning, genuine ownership, and thorough documentation.** If technical depth comes up, emphasize that you document and hand off cleanly (you wrote runbooks/tests at Wysa).

> Net: be the curious, coachable, ownership-driven person who's clearly excited to learn the clinical side. That's the archetype that already succeeded here.

---

## 2. Your single strongest pitch (your "why me")

You're not a generic SWE intern — you're unusually on-target:

1. **You've built real clinical backends.** At Wysa you engineered a multi-tenant **NHS clinical backend** for 8+ UK clients, integrated with an external clinical platform (Mayden's iaptus) via REST — i.e., you've already done secure healthcare-system integration, which is exactly the muscle SMART-on-FHIR/EHR work needs.
2. **You've built trustworthy, grounded AI — not black boxes.** AgenticSearch and cf-ai-research-scout are literally *evidence-retrieval + structured extraction with verification, provenance, and rule-based fallback.* That is the same architecture TherAlign uses (RxNorm + PubMed + Gemini structured output + rule-based fallback). The founders had Vishnu do **"evidence extraction from medical literature"** — that *is* what your two AI projects do. In a clinical setting, "grounded AI you can trust" is the whole game, and it's your specialty. **This is your single most uncanny match — make sure it lands.**
3. **You understand sensitive-data stakes.** You owned backend security for clinical data — auth hardening, audit logging, remediating 20+ VAPT findings. You won't be cavalier with PHI.
4. **You ship fast and end-to-end.** Sonare (full desktop app shipped under hackathon pressure), 20+ APIs at Cario, a data-annotation tool that cut 100+ hrs/month. Founding-intern energy.
5. **You care about healthcare, demonstrably.** IEEE-published Alzheimer's classification work + an NHS mental-health backend. This isn't a random application.

**The honest gap + how to frame it:** You haven't personally written SMART on FHIR / RxNorm code yet (that was Vishnu's build). Don't hide it. Frame: *"I've done secure REST integration with external clinical systems and I go deep on auth — FHIR is a standard I'd ramp on quickly, and the grounded-AI/evidence side is already exactly what I've built."* Confidence + learnability, not bluffing.

---

## 3. Behavioral questions — your STAR stories

Use **STAR** (Situation, Task, Action, Result). Keep each answer ~60–90 seconds. All of these are pulled straight from your real experience.

**"Tell me about yourself."** (Almost certain opener.)
> MS CS at UMass Amherst, two years as a backend engineer at Wysa building NHS clinical systems for 8+ UK clients, plus a track record of building grounded, evidence-based AI tools (AgenticSearch, cf-ai-research-scout). I like working where backend, AI, and a real-world problem meet — and healthcare is where I keep coming back, from an NHS triage backend to a published medical-imaging paper. TherAlign sits right at that intersection, which is why Vishnu's referral genuinely excited me.

**"Tell me about a time you took ownership of something / a founding-type story."**
- S/T: At Wysa the AI team was labeling training data in spreadsheets — slow, error-prone, no access control.
- A: I designed and built a full-stack data-annotation tool (React/Node/MongoDB) with secure role-based REST APIs, replacing the spreadsheet workflow. I scoped it, built it, and got it adopted as a daily tool.
- R: Cut manual ops by 100+ hours/month and improved labeling throughput by 60%.
- *Why it lands:* shows you spot a problem and own it end-to-end — exactly founding-engineer behavior.

**"Tell me about working under ambiguity / time pressure."**
- Sonare (Qualcomm Edge AI Hackathon): built a full offline sign↔speech desktop app — camera, mic, MediaPipe hand tracking, whisper.cpp ASR, local TTS, Electron/React frontend + FastAPI backend — shipped end-to-end under hackathon time pressure with async queues keeping the UI responsive.
- *Why it lands:* startups live here. You can ship a working thing fast without a spec handed to you.

**"Tell me about high-stakes / sensitive work."**
- Owned backend security for sensitive NHS clinical data: hardened auth, rate limiting, audit logging, added regression integration tests, monitored production logs during releases/client integrations, remediated 20+ VAPT findings.
- *Why it lands:* signals you'll handle PHI responsibly — a clinician founder cares a lot about this.

**"Tell me about a hard technical problem / debugging."**
- cf-ai-research-scout: I designed durable workflow boundaries so multi-step AI research tasks survive process restarts and tool failures, with agent state persisted server-side — no external DB. Building reliability into an inherently flaky (LLM + external-API) pipeline.
- Or: monitoring production logs during NHS client integrations and remediating issues live.

**"A time you made a mistake / something failed."**
- Pick a real one and keep it honest: a bug caught in production logs during a release, or an early AgenticSearch version that over-trusted the LLM and you added the verification/provenance layer in response. Structure: what happened → what you did immediately → what you changed so it can't recur. *(Founders love the "and here's the system I built so it never happens again" ending.)*

**"Working with non-technical people / explaining technical things."**
- The annotation tool was used daily by the AI/labeling team (non-backend folks) — you designed it around *their* workflow, not yours. And at Wysa you supported clinical client integrations. You translate between technical and non-technical naturally. *(This is the meta-skill Dachuan is testing in this very call.)*

**"Why TherAlign / why healthcare / why this role?"**
> Three reasons. One, the problem is real and I've felt the healthcare-systems pain from the build side — prior auth is exactly the kind of friction that hurts patients and providers, and prevention is a smart wedge. Two, the technical fit is uncanny: I've built grounded, evidence-first AI with provenance and verification, which is precisely what a clinical recommendation tool needs to be trustworthy. Three, it's a founding-engineer seat where I can own real surface area, and Vishnu's experience here gave me a candid, positive read on the team.

---

## 4. "How would you solve X" — problem-solving scenarios

Dachuan will likely give you a product/clinical scenario and watch *how you think and communicate*, not whether you know an API. Think out loud, structure your answer, ask clarifying questions first, and tie back to patient/provider value.

**"How would you build a feature that suggests a covered, clinically-appropriate alternative to a prescribed drug?"**
> First I'd clarify the inputs we trust: patient's plan/formulary, the prescribed drug, diagnosis/indication. Then: (1) normalize the drug with **RxNorm** so we're reasoning on concepts, not free text; (2) pull candidate alternatives in the same therapeutic class; (3) check each against the patient's **formulary/coverage and PA rules**; (4) rank by clinical appropriateness using **PubMed/guideline evidence**; (5) use the LLM (**Gemini structured output**) to assemble it into a structured, explainable recommendation — but with a **rule-based fallback** and a **verification step**, never a raw LLM guess. The clinician sees the alternative *with its evidence and coverage reason*, and makes the call. I've built almost exactly this shape of pipeline (retrieval → structured extraction → verification → provenance) in AgenticSearch.

**"What if the AI recommends something wrong or unsafe?"** (Trust/safety — your sweet spot.)
> The core principle: never present LLM output as ground truth. I'd design for it — (1) **provenance** so every recommendation traces to its source (which guideline, which formulary rule); (2) a **verification/validation layer** and **rule-based guardrails** that can veto unsafe combos (e.g., contraindications, allergies); (3) **clinician-in-the-loop** — we suggest, they decide, nothing is auto-prescribed; (4) show **confidence and evidence** so a provider can judge; (5) **log everything** so we can reproduce and fix any bad case. In a clinical product, being able to say *why* the system said something matters as much as the recommendation.

**"How do you get busy providers to actually trust and use it?"**
> Fit it into their existing flow — that's why SMART on FHIR launching inside the EHR is right; don't make them log into another tool. Be transparent (show the coverage reason and evidence, not a black box), be fast, and start narrow where we're confident rather than boiling the ocean. Trust is earned by being right on a small surface first.

**"You're one of very few engineers and limited time — how do you prioritize?"**
> Work backward from the nearest concrete milestone — for you that's the investor/clinical/product demo. I'd ask you directly: what's the one workflow that has to be flawless for the demo to land? Build that path end-to-end first, stub the rest, and avoid gold-plating things no one will see yet. Then harden once the core is validated.

**"How would you predict whether a prior auth will get approved (or whether a drug will work)?"** (Eric's letter says they build these models.)
> I'd be honest about the data reality first: early on you rarely have enough labeled approval/denial data to train a heavy model, so I'd start simple and explainable — encode the known **payer/formulary rules and PA criteria** as features, combine with drug/diagnosis signals, and use a transparent model (or even a well-structured rules + scoring approach) so a clinician can see *why* a likelihood is high or low. As real approval/denial outcomes accumulate, learn from them to refine. For efficacy, ground it in **comparative-efficacy evidence from the literature** rather than letting a model freelance. The theme: explainable and evidence-backed beats a black-box score in a clinical product.

**"How would you ramp on FHIR / Epic / our stack quickly?"**
> Read Vishnu's code and docs/runbooks first (Eric mentioned the docs are solid), get the app running locally against the mock FHIR server, then make one small end-to-end change to learn the full path before taking on a feature. FHIR and Epic integration are well-documented standards and I've done secure external clinical-system integration before (Mayden's iaptus at Wysa), so I'd expect to be productive quickly — and I'd document as I go, since that clearly matters to the team.

**"What would you improve about our product?"** (Have *one* thoughtful, humble idea ready.)
> Frame as a question/hypothesis, not a critique: e.g., "I'd want to understand how you're measuring whether a suggested alternative actually avoided a PA — closing that feedback loop seems like it'd both improve the model and be a powerful metric for investors." Shows product thinking without presuming you know their business better than they do.

---

## 5. Questions to ask Dachuan (pick 3–4)

Ending strong matters. Mix clinical, product, and "is this a good fit" questions:

- "What does a great outcome for this intern look like by the end of the summer?"
- "What's the most important thing you're trying to prove or ship next — a clinical pilot, an investor milestone, a specific workflow?"
- "Who's the first user you're designing for — what kind of provider and setting?"
- "How do you and Eric split the clinical and technical sides, and how would I work with each of you?"
- "How do you think about AI safety and trust when the output is a clinical recommendation?" *(signals you get the stakes)*
- "What's the path from this prototype to something used in a real clinic — what are the regulatory or workflow hurdles you're thinking about?"
- "What did Vishnu work on that you'd want the next person to push further?" *(you know it was Epic integration, the prediction models, and evidence extraction — you can be specific)*
- "Congrats on the MIT Hacking Medicine win — how has that shaped what you're focused on now?" *(warm, shows you did homework)*
- "How are you thinking about the efficacy / PA-approval prediction models as more real outcome data comes in?"

*(Avoid leading with comp/logistics in this round — save for later.)*

---

## 6. Logistics & delivery tips

- It's titled **Non-Technical** — expect conversation, motivation, and reasoning, **not** live coding. Be warm and personable; this is partly a "do I want to work with this person every day" check.
- **Talk to the clinician, not the compiler.** When you explain AgenticSearch/Wysa, lead with the *problem and the patient/user impact*, then the tech. Drop the acronym soup.
- **Reference Vishnu naturally** — he vouched for you and did this exact role; it's social proof. ("Vishnu gave me a great sense of the team and the problem.")
- Have your resume open; be ready to walk any line. Every number on it (8+ clients, 10,000+ submissions, $340K+, 100+ hrs/month, 60%, 20+ VAPT) is fair game — own them.
- Show genuine enthusiasm for the *prior-auth problem* specifically. Founders fund themselves on belief; they want to see you share it.
- Keep answers tight (~60–90s), then check in: "Want me to go deeper on any of that?"
- It's a 1-hr remote call — test your camera/mic a few minutes early, quiet background, good light.

**One-line close if asked "anything else":**
> I've built secure clinical backends and grounded, evidence-first AI — the two halves of what TherAlign is. I'd love to help get the prototype to the point where providers trust it enough to change what they prescribe.
