# Interview Prep — Culture and Morality Lab, Dr. Mohammad Atari

**When:** Thursday, July 2, 9:20–9:30 AM (Zoom link + Google invite sent)
**Format:** 10 minutes, non-technical. He shared 3 questions in advance — he's testing communication, realistic estimation, and whether you can be handed ambiguous technical work and run with it.

**The one rule for a 10-minute slot:** answer headline-first, then 2–3 supporting points, then stop. Aim 60–90 seconds per answer. Never monologue past 2 minutes — he may only get through 1–2 of the 3 questions.

---

## 30-second context on him and the lab

- Mohammad Atari, Assistant Professor, Psychological & Brain Sciences, UMass. Runs the Culture and Morality Lab (CAM-L): culture, morality, language, AI — studied with NLP methods.
- Three research lines: cultural/historical variation in psychology, pluralistic morality, and **developing NLP methods for social psych** (this hire supports line 3).
- **CCR is his own method** (with Ali Omrani). Know it cold — see Q2.
- He was previously at Harvard (historical psychology) and USC before UMass.

## Your 20-second opener (if asked "tell me about yourself")

"I'm an MS CS student here, graduating May 2027. Before grad school I spent two years as a backend engineer at Wysa, a mental-health AI company, where I owned an NHS data-collection backend and built an annotation platform for the AI team — so research-adjacent web infrastructure is exactly what I've done professionally. My coursework and projects are NLP-focused: RAG pipelines, sentence-transformers, LLM APIs. This role is the intersection of both."

---

## Q1 — Two public websites: conference/community site (with member data collection) + lab site

**Headline answer:** "They're two different classes of site, so I'd build them differently. The lab site is mostly static content — keep it simple and nearly maintenance-free. The community site collects data from members, so it needs a real backend, auth, and an admin panel."

**Lab site**
- Static site (Next.js static export, Hugo, or similar), content in Markdown so lab members can edit without touching code; hosted on GitHub Pages/Vercel under a lab GitHub org — free, fast, no server to patch.
- Sections: people, publications, projects, news, join-us. Publications can auto-pull from BibTeX.
- **Estimate: ~1–2 weeks at part-time hours** for a polished v1, assuming content (bios, pubs) is provided.

**Conference/community site**
- React (or server-rendered Next.js) front-end + Python backend (FastAPI/Django) + PostgreSQL. Member accounts, registration/submission forms, payments only if needed.
- **Estimate: ~4–6 weeks part-time for an MVP** (auth, member profiles, data-collection forms, admin dashboard, CSV export), then iterate. I'd give a firmer number after 30 minutes of requirements: what data, from whom, roughly how many members.

**Admin workflows**
- Role-based access (admin / member); admin dashboard to manage members, review submissions, edit content without code, export data as CSV; email notifications for key events. (You've built exactly this: Underdogs Fitness admin panel; Wysa annotation platform with role-based REST APIs.)

**Accessibility**
- WCAG 2.1 AA as the target (also a university expectation for public sites): semantic HTML, keyboard navigability, contrast, alt text, properly labeled forms; audit with Lighthouse/axe + a screen-reader pass before launch.

**Maintenance plan**
- Everything in Git under a lab-owned org; documented README + handoff docs so it outlives any one student (you did exactly this KT at Wysa).
- Managed hosting + automated DB backups; dependency updates on a schedule; uptime monitoring; staging environment before production changes.
- Static lab site ≈ near-zero maintenance; dynamic site ≈ a few hours/month.

**Proof points to drop:** Underdogs Fitness — solo-built production platform, live 3+ years, second branch added with zero schema migration. eTriage backend — 10,000+ monthly form submissions in a clinical setting.

---

## Q2 — CCR platform architecture (his method — the centerpiece question)

**First, show you understand CCR (1 sentence):** "CCR measures a psychological construct in text by embedding validated questionnaire items and the text with a transformer model like SBERT, then taking cosine similarity — the text's 'loading' on the construct. So the platform is: upload corpus → pick or define a construct → run embeddings + similarity → inspect → export."

**User workflow**
1. Researcher signs in, creates a project, uploads corpus (CSV/XLSX — matching the existing `ccr_wrapper` input format).
2. Selects a construct from a library of validated scales, or defines custom items.
3. Picks an embedding model (default `all-MiniLM-L6-v2`, dropdown of alternatives, incl. multilingual — relevant to the lab's cross-cultural work).
4. Runs the job with a progress indicator; large corpora run async, email/notify when done.
5. Results dashboard: per-item and aggregated similarity scores, distributions, top-/bottom-scoring texts for face-validity checks.
6. Export CSV (input columns + appended similarity columns, same shape as the current R/Python packages, so it's a drop-in for existing users).

**Architecture**
- **Frontend:** React — upload wizard, project dashboard, results visualizations.
- **Backend:** FastAPI — auth, projects, REST endpoints; wraps the existing `pyccr` logic rather than reimplementing it.
- **Database:** PostgreSQL for users/projects/constructs/job metadata; object storage (S3/GCS) for corpora; results as files + summary rows in the DB.
- **NLP pipeline:** background worker queue (Celery + Redis, or lighter) because embedding 100k documents can take minutes — never block a web request. sentence-transformers with batching; cache questionnaire-item embeddings (small, reused constantly); GPU optional, CPU fine for MiniLM-class models.
- **Deployment:** Dockerized; a university VM or Cloud Run to start (I deploy AgenticSearch, a FastAPI service, on Cloud Run today). HTTPS, upload-size quotas, and a data-retention/delete option since corpora may be sensitive.
- **Reproducibility built in:** every job logs model name/version, preprocessing settings, timestamp — so a result in a paper can be regenerated.

**Estimate:** "A working MVP — upload, run CCR, view, export — in roughly 4–6 weeks at part-time hours. Construct library, visualizations, multi-user polish is a semester-long arc of iterations with lab feedback."

**Proof points:** AgenticSearch (FastAPI + LLM pipeline + 150+ tests, deployed on Cloud Run); Wysa annotation platform (React + Node data platform used daily by an AI team); KG2RAG (sentence-transformers, rerankers).

---

## Q3 — Grad student, new construct, messy text data → reliable LLM/NLP analysis

**Headline:** "Half of this job is asking the right questions before writing code — measurement validity first, then engineering reliability."

**Questions I'd ask them**
1. **Construct:** How is it defined theoretically? Are there validated scale items or a close cousin of a validated scale? (If yes → CCR is the natural first method.)
2. **Unit of analysis:** tweet, paragraph, document, person? What population and language(s)?
3. **The data's mess:** source, size, known problems — duplicates, spam/bots, encoding, mixed languages, PII?
4. **Research question:** continuous measurement, classification, or exploration? What stats do they want to run downstream?
5. **Ground truth:** can we get human annotations on a subset? Who annotates, and with what codebook?
6. **Constraints:** IRB/privacy — can text go to an external LLM API at all, or do we need local models (I've run quantized Llama locally in production)? API budget? Timeline?

**The reproducible pipeline I'd build**
1. **Data audit + cleaning script** — versioned, documented, deterministic: dedupe, language filter, normalization; raw data kept immutable, every transform logged. Never clean by hand.
2. **Operationalize the construct** — with the student: scale items (→ CCR/embeddings) and/or an annotation codebook with examples and edge cases.
3. **Baselines before LLMs** — embedding-similarity (CCR-style) and/or dictionary methods first; then LLM labeling with a structured prompt and a fixed output schema. Cheap baselines tell you whether the LLM is adding anything.
4. **Validation loop** — human-annotate a stratified subset (a few hundred items), measure inter-annotator agreement, then score each method against the human gold labels. Spot-check disagreements together.
5. **LLM reliability engineering** — pinned model version, temperature 0, versioned prompts, schema-validated outputs with retries, response caching (cost + reproducibility), repeated runs on a sample to measure label stability.
6. **Reproducibility as default** — everything config-driven in Git, pinned dependencies, one command to regenerate results end-to-end; a README a future lab member can follow.

**Proof points:** built the annotation platform an AI team used daily (you know labeling workflows from the infrastructure side); AgenticSearch's deterministic-extraction-first, LLM-fallback design with cell-level provenance is exactly this "make LLM outputs auditable" philosophy.

---

## Prototype: CCR Platform (BUILT — in `Coding Stuff/ccr-platform/`)

A working CCR platform exists at `../../ccr-platform/` (relative to this repo): FastAPI + SQLite + React dashboard, seeded construct library (SWLS, MFQ Care/Fairness, Individualism/Collectivism), async jobs with progress, results dashboard (histogram, per-item loadings, top/bottom texts), CSV export matching `ccr_wrapper` output shape, reproducibility metadata per run, 14 passing tests.

**Tonight (~10 min):**
1. `cd "…/Coding Stuff/ccr-platform" && ./run.sh` → open http://127.0.0.1:8000
2. `python scripts/verify_install.py` (inside `backend/.venv`) — real-model end-to-end check (~90 MB model downloads once).
3. Do one full demo run: new project → upload `sample_data/sample_corpus.csv` → *Satisfaction with Life* → Run → open results → Export CSV. **Take screenshots** (fallback if live demo misbehaves).
4. Optional: push to GitHub (`.gitignore` is set; `backend/data/` stays local) so you have a sendable link.

**90-second demo script (offer AFTER answering Q2 verbally):**
> "I actually built a working version of this to make sure my estimate was honest — may I share my screen for a minute?"
1. Upload corpus → point at column selection ("CSV or Excel, same input shape as your `ccr_wrapper`").
2. Pick SWLS → "seeded library of validated scales, with references; custom constructs supported; wordings flagged for verification against the original publications."
3. Run → results: histogram, per-item loadings ("face-validity check — which items drive the signal"), top/bottom texts.
4. Close on the footer: "every run logs model version, item hash, package versions — a result in a paper stays regenerable." Then STOP.

**Two things to say about it (senior-signal):**
- **Value-add over existing tools:** the R/Python packages and single-run web tool do one-off analyses; this adds persistent projects, construct library, async jobs, dashboards, exports, reproducibility records.
- **Known method nuance (say it before he asks):** cosine similarity captures construct *relatedness* more than stance — a text lamenting dissatisfaction sits near SWLS items in embedding space. Reverse-scored items need care; new construct+corpus combos should be validated against a human-annotated subset. Naming your demo's limitation unprompted is worth more than the demo itself.

**If asked "how long did this take?"** — honest answer: "The core method is simple — the work was the platform around it. A day with AI-assisted development for this MVP; the production version with auth, Celery, Postgres is the 4–6 week estimate I gave." (Ties into his likely interest in AI-assisted research engineering.)

---

## Design decisions — what I'd pick, why, and why not the alternatives

The interview-grade pattern: name the choice, name the rejected option, give the reason in terms of *this lab's* constraints (small team, Python-first, sensitive data, must survive student turnover, minimal budget).

**Lab site: static site generator vs WordPress vs custom app**
- **Pick static** (Next.js export / Hugo, Markdown content, GitHub Pages/Vercel): near-zero maintenance and security surface, free hosting, content versioned in Git.
- **Not WordPress:** constant plugin/security patching, PHP hosting to manage — a liability once you graduate. It only wins if non-technical staff must edit via WYSIWYG weekly; if so, say you'd revisit (or use a headless CMS).
- **Not a custom app:** a backend serving content that never changes is maintenance for nothing.

**Community-site backend: Django vs FastAPI vs Node/Express**
- **Pick Django** for the member/data-collection site: auth, ORM, forms, and — decisive here — the **auto-generated admin panel**, which covers most "admin workflows" for free.
- **FastAPI** loses here (you hand-build auth + admin) but **wins for the CCR platform**, where the product is an API around an ML pipeline and async matters. Two different jobs, two different tools — saying this distinction out loud is the strongest version of the answer.
- **Not Node** (despite your 2 years of production Node): the lab is Python-first. The next maintainer is a psych PhD student who knows Python, not Express. Choosing handoff-ability over personal comfort is exactly what a PI wants to hear.

**Database: PostgreSQL vs MongoDB vs SQLite**
- **Pick Postgres:** members/submissions/roles are relational with integrity constraints; researchers want tabular exports; the JD literally says SQL.
- **Not Mongo** (despite Wysa experience): schema flexibility isn't needed, joins are; flexible schemas rot without a team enforcing conventions.
- **SQLite is the MVP exception:** fine single-node with few writers (AgenticSearch uses it); migrate to Postgres when concurrent writes/multi-user arrive. Start small deliberately, name the upgrade trigger.

**Long-running jobs: synchronous vs FastAPI BackgroundTasks vs Celery+Redis**
- **Never synchronous:** embedding 100k docs in a request handler = timeouts and a frozen UI.
- **Pick BackgroundTasks for the MVP:** zero extra infrastructure. Known cost: jobs die on process restart, no retries or progress persistence.
- **Upgrade to Celery+Redis when it hurts** (long jobs, multiple users, need retries/progress). Deferring infrastructure until justified is the right size for a lab — say the trigger, not just the choice.

**Embeddings: local sentence-transformers vs OpenAI/API embeddings**
- **Pick local:** free per-run, reproducible (pinned weights — API models get deprecated mid-paper, a real research risk), data never leaves the machine (IRB-friendly), and it's what published CCR uses (`all-MiniLM-L6-v2`).
- **API as a documented fallback** for scale or bigger models when data isn't sensitive. This one matters most to a researcher: reproducibility + privacy beat convenience.

**Deployment: university VM vs Cloud Run vs Vercel/Pages**
- **Static frontends → Vercel/GitHub Pages** (free, no ops).
- **CCR platform → depends on data sensitivity:** university VM keeps data on campus (IRB) and is free, but you patch the box; Cloud Run is containerized, scale-to-zero cheap, no server management (you run AgenticSearch there) but data leaves campus and cold starts. Ask him about data-sensitivity requirements before committing — asking that question IS the answer.

**Platform frontend: Streamlit/Gradio vs React SPA**
- **Pick Streamlit for the internal-tool MVP:** days-not-weeks, pure Python (any lab member can edit it), perfect while the workflow is still evolving.
- **Graduate to React** when it goes public-facing or needs real UX (accounts, dashboards, the community site). Prototype in the cheap tool, invest in the expensive one only once the workflow is validated.

---

## Questions to ask him (pick 1–2, time permitting)

- "What's the most urgent project — is there something you'd want live in the first month?"
- "Would I work mostly with you directly or embedded with PhD students day-to-day?"
- "Does the lab have existing hosting/infrastructure at UMass, or would I be setting that up too?"

## Logistics checklist

- Confirm availability: start ASAP, up to 20 hrs/week through summer, open to continuing into fall/spring.
- Test Zoom, camera, mic beforehand; join 2–3 min early; have your CV and this doc open.
- Time estimates: always attach assumptions ("at ~15–20 hrs/week, assuming requirements are settled") — realistic beats optimistic with a PI.
- He said non-technical — so no whiteboarding; deliver answers as a calm, structured plan. The subtext of all three questions: *"Can I hand this person a vague project and trust what comes back?"* Every answer should end in something shippable with a date.
