# Follow-up Drill — where the interview is actually decided

He sent the same 3 scenarios to every candidate. Everyone arrives with a decent surface answer, so he differentiates by **drilling follow-ups until the "why" runs out**. Your advantage: you built the thing, so your whys come from decisions you actually made. Format below: likely follow-up → strong answer → trap to avoid.

**The universal answer pattern:** *choice → rejected alternative → reason tied to THIS lab's constraints → upgrade trigger.* "I chose X. I considered Y. For a small Python-first lab with sensitive data and student turnover, X wins because Z. I'd switch to Y when [trigger]."

---

## Q1 follow-ups — the two websites

**"Why a static site? Our admin can't use Git."**
→ "Then that changes my answer — that's exactly the requirement that flips it. Static-plus-Git is for a lab where content changes rarely and editors are technical. If non-technical staff edit weekly, I'd use a headless CMS (content in a friendly editor, site still fast and static) or WordPress as the pragmatic default. The right architecture depends on who maintains it, which is why my first step is a requirements conversation, not code."
✗ Trap: defending static dogmatically. He may be testing whether you adapt to users.

**"What does accessibility actually mean here — concretely?"**
→ "WCAG 2.1 AA as the standard — which UMass also expects for public university sites. Concretely: semantic HTML so screen readers can navigate; every form input labeled; keyboard-only operation works; color contrast ratios checked; alt text on images; captions if there's video. Process-wise: automated audit (Lighthouse/axe) plus one manual keyboard-and-screen-reader pass before launch, and re-check when templates change."
✗ Trap: just saying "WCAG compliance" with no concrete item — that's the answer everyone else gives.

**"Your estimate is 4–6 weeks. What if it takes longer?"**
→ "The estimate carries assumptions I'd state up front: requirements settled, content provided, ~15–20 hrs/week. The honest control is scope sequencing: auth + forms + data export ship first, polish ships iteratively. If week 2 shows drift, you hear it in week 2, not week 5. At Wysa I was the primary contact for a clinical backend — surfacing slippage early is the job."
✗ Trap: "it won't" — PIs have heard that from every student ever.

**"Who maintains this after you graduate?"**
→ "I design for my own replaceability: everything in a lab-owned GitHub org (not my personal account), README with setup-from-zero instructions, documented admin workflows, managed hosting so there's no server to patch. At Wysa I onboarded my backend's second developer to on-call readiness in ~6 weeks with structured docs — same playbook."
✗ Trap: not having thought about it. For a lab that cycles students, this may be his top hidden criterion.

**"How do you handle the member data we collect? Anything legal to think about?"**
→ "Three layers: technical (HTTPS, hashed passwords, role-based access, exports limited to admins), policy (only collect what's needed, retention window defined), and institutional (if it touches human-subjects research, the IRB protocol dictates storage and consent language; university data-classification rules may require campus hosting). I'd ask what the IRB status is before building the schema."
✗ Trap: pure tech answer. Mentioning IRB unprompted is a lab-culture signal.

---

## Q2 follow-ups — CCR platform (he will drill deepest here; you have the most ammo)

**"Why FastAPI and not Django? / not Flask?"**
→ "The product is an API around an ML pipeline — FastAPI gives async, typed request validation with Pydantic, and auto-generated API docs. Django's win is its admin panel and batteries for CRUD-heavy apps — that's why I'd pick Django for the *community site* in your first question, but here the admin surface is small and the ML integration is the core. Flask can do it but you hand-assemble what FastAPI includes. Different question, different tool — I'd happily defend the opposite choice for the other project."
✗ Trap: bashing Django. Show the boundary where your choice loses.

**"Why not just use the OpenAI embeddings API instead of hosting a model?"**
→ "Three research-specific reasons. Reproducibility: API models get deprecated or silently updated — a paper's numbers must be regenerable years later; pinned local weights guarantee that. Privacy: corpora may be IRB-covered; text shouldn't leave infrastructure you control. Validity: published CCR uses sentence-transformers — using the same model family keeps results comparable to the literature. Cost is the bonus: embedding is free per-run locally. The API is a documented fallback for non-sensitive data at scales beyond local compute."
✗ Trap: only saying "cost". The reproducibility argument is the one a methods researcher respects most.

**"Why SQLite? That's not a real database."**
→ "It's the right-sized database for the current write load — single node, few writers, zero ops. The schema is deliberately Postgres-portable and the swap is a connection string plus a migration, not a rewrite. The trigger is concurrent multi-user writes. Starting with Postgres on day one means running a database server before there's a second user — infrastructure before need."
✗ Trap: getting defensive. Name the limit before he does; it converts a gotcha into a design decision.

**"What happens with a million documents?"**
→ "Three bottlenecks in order: embedding time (move workers to a GPU box — MiniLM embeds ~1M short texts in hours on one GPU), memory (stream batches instead of holding the matrix; store per-item results incrementally), and the queue (single worker → Celery with parallel workers). The architecture doesn't change — job state already lives in the DB, so scaling is swapping the executor. For this lab's realistic corpora — tens of thousands to low hundreds of thousands — current design handles it on CPU."
✗ Trap: hand-waving 'it scales'. Name the first thing that breaks — that's what proves you've thought about it.

**"How do you know your implementation is correct?"**
→ "Two levels. Engineering: 17 automated tests, including the full pipeline against a deterministic fake embedder. Method: the plan is a golden-file parity test — run the same corpus + items through the reference `ccr_wrapper` and through my pipeline, assert the similarity matrices match. If my numbers ever diverge from the published implementation, that's a bug by definition — the lab's existing results are the spec."
✗ Trap: mentioning only unit tests. Parity-with-the-reference-implementation is the research-grade answer, and almost nobody else will say it.

**"How would you handle reverse-scored items?"** *(methods depth-charge — he may ask precisely because it's awkward for CCR)*
→ "Honestly, this is a place where I'd want the lab's methods judgment, and here's the issue as I understand it: cosine similarity measures semantic relatedness, so a reverse-scored item ('I rarely rely on others' vs. reversed) and its forward twin sit close in embedding space — you can't just multiply by −1 like questionnaire scoring. Options I'd put on the table: keep loadings per-item and let the researcher handle direction analytically; exclude reversed items and document it; or validate empirically which treatment tracks human labels best on a annotated subset. I'd implement whichever the lab's validation supports."
✗ Trap: bluffing a formula. Naming the problem precisely + deferring the *methods* call to evidence is the strongest available move — it shows you know where engineering ends and psychometrics begins.

**"Your top-scoring text for satisfaction could be someone lamenting their dissatisfaction. Isn't that broken?"**
→ "It's the method's real limitation and I saw it in my own demo — similarity captures 'about the same thing' more than 'endorses it'. That's why the results screen shows highest AND lowest scoring texts as a face-validity step, and why I'd validate any new construct-corpus pair against a human-annotated subset before anyone publishes with it. CCR's own literature frames it as complement to, not replacement for, validation."
✗ Trap: defending the tool. Agreeing precisely, with the mitigation already built, is the senior answer.

**"Should texts be scored as whole documents or sentence by sentence?"**
→ "It's a real design choice that changes results: transformer models have a token window (~256 for MiniLM), so long documents get truncated — my platform flags likely-truncated texts. For long documents I'd segment (sentence or paragraph), score segments, and aggregate — but mean vs. max aggregation is itself a methods decision. I'd expose it as an option and validate which matches human judgment for the construct at hand."
✗ Trap: not knowing the token window exists. This is a favorite probing question for embedding pipelines.

**"You built this in a day? How?"** *(the AI question, direct or implied)*
→ "AI-assisted development, heavily and deliberately — it's how I work. I ran a COO-sponsored Copilot adoption pilot at my last company, so I have practiced workflows. The design decisions — local models for reproducibility, worker queue with state in the DB, parity testing against your reference implementation — are mine, and I can defend every one; the AI accelerated the typing, not the thinking. For a lab studying AI and language, I'd hope that's a feature."
✗ Trap: hedging or hiding it. He studies AI; evasiveness costs more than the admission.

---

## Q3 follow-ups — grad student, messy data, LLM pipeline

**"What's the FIRST question you'd ask the student?"**
→ "'How would you know if the analysis is right?' — i.e., what's the ground truth. It sets everything: if we can get human annotations, we can validate any method; if we can't, we're limited to methods with published validity evidence. Second question: 'Is there a validated scale for this construct or a close cousin?' — because that decides whether CCR is available or we're building an annotation codebook first."
✗ Trap: starting with tech ("which LLM?"). Measurement first, tools second.

**"How do you make LLM labeling reliable enough for research?"**
→ "Treat the LLM as an annotator whose reliability you measure, not an oracle. Concretely: pinned model version, temperature 0, versioned prompts, schema-validated outputs; run a stratified subset several times to measure self-consistency; and — decisive — measure agreement against human gold labels (a few hundred stratified items, inter-annotator agreement first so we know the human ceiling). If the LLM's agreement with humans matches human-human agreement, it can scale the labeling; if not, we know exactly what we have. And cheap baselines first — embedding similarity, dictionaries — so we know the LLM is adding anything."
✗ Trap: prompt-engineering talk without measurement. 'Agreement statistics' is the phrase that lands in a psych lab.

**"The student can't send data to OpenAI — IRB. Now what?"**
→ "Local models — I've shipped exactly this: at Cario I ran quantized Llama on a single VM in production with no GPU budget. Today: a strong open model via llama.cpp/Ollama on lab hardware, same pipeline otherwise — pinned weights, versioned prompts, agreement validation. Local is often better for research anyway: reproducible forever and free at the margin."
✗ Trap: treating it as a blocker. This is your best 'I've literally done this' moment.

**"What does 'reproducible' concretely mean in your pipeline?"**
→ "One command regenerates every number from raw data: config-driven runs (data paths, model versions, prompts, seeds all in versioned config), immutable raw data with all cleaning as logged code, pinned dependencies, outputs written with the config hash that produced them. Test: a new lab member reruns the paper's analysis without asking anyone anything. My platform already does the small version — every run stores model version + item hash."
✗ Trap: saying "I use Git" and stopping.

---

## Cross-cutting follow-ups

**"You have 20 hrs/week and three projects. How do you prioritize?"**
→ "I don't guess — I ask you to rank outcomes, then I sequence for earliest usable value and flag conflicts immediately. My default bias: unblock others first (if a PhD student waits on my platform, that's the multiplier), then deadline-driven work, then infrastructure."

**"What DON'T you know?"**
→ "Psychometrics depth — validity theory, scale construction, the measurement literature. I know the engineering around the methods, and I know when to defer: my construct library ships with a verify-against-the-original-publication warning precisely because item wording is a methods call, not an engineering call. I'd lean on the lab for measurement theory and pick it up fast."
✗ Trap: a fake weakness. This one is true, relevant, and shows you know the boundary.

**"Why do you want this role?" (10-second version)**
→ "This is the work I already choose to do — I built research infrastructure at Wysa that an AI team used daily, and I built your CCR platform question because it was fun. Getting paid to do that inside a lab whose methods I find interesting, while doing my MS here, is exactly the fit."

---

## The three sentences that beat other candidates (if you say nothing else)

1. **Parity:** "The lab's existing `ccr_wrapper` results are my spec — my pipeline should reproduce them exactly, and I'd test that."
2. **Stance:** "Cosine similarity measures relatedness more than stance — I saw it in my own demo, which is why validation against human labels stays in the loop."
3. **Boundaries:** "That's a methods decision, not an engineering decision — I'd implement whichever option your validation supports."

Each one draws the line between tool-builder and scientist — and shows you respect which side he lives on.
