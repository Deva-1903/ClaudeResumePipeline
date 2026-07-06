# Master Question List + Glossary

One-stop sheet: every question you might face (answers are in `interview_followup_drill.md` and `interview_prep.md`), followed by plain-language refreshers for every term you might need. Read the glossary once; skim the questions before the call.

---

## The 3 scenarios he sent (the openers)

1. **Two public websites** — one for a scientific community/conference that collects data from members, one for the lab. How would you build each? How long would each take? What admin workflows, accessibility practices, and maintenance plan?
2. **CCR platform** — researchers upload a corpus, define/select constructs, run CCR-style analysis, inspect results, export. What architecture: frontend, backend, database, NLP pipeline, deployment, user workflow?
3. **Grad student + messy dataset** — new construct, messy text data, wants a reliable LLM-based NLP analysis. What questions do you ask? What reproducible pipeline do you build?

## Expected follow-ups — Scenario 1 (websites)

- Why a static site? What if our admin can't use Git?
- What does accessibility mean *concretely*? What's WCAG?
- Your estimate is X weeks — what if it takes longer? What are your assumptions?
- Who maintains this after you graduate?
- Where would you host it? What does it cost?
- How do you secure the member data collected? Anything legal/institutional (IRB, university policy)?
- How do you stop spam signups / fake form submissions?
- WordPress vs custom vs static — walk me through the trade-off.

## Expected follow-ups — Scenario 2 (CCR platform)

- Why FastAPI and not Django or Flask?
- Why React and not something simpler (Streamlit/Gradio)?
- Why SQLite — isn't that a toy database? When would you switch?
- Why host the embedding model yourself instead of calling the OpenAI API?
- What happens with a million documents? What breaks first?
- How do you know your implementation is *correct*?
- How would you handle reverse-scored items? *(most likely depth-charge)*
- A dissatisfied text can score high on satisfaction — isn't the method broken? *(relatedness vs stance)*
- Whole documents or sentence-by-sentence scoring? What about long texts?
- Which embedding model would you use and why? What about non-English corpora?
- How do users define a *new* construct? What can go wrong?
- What about data privacy / IRB if researchers upload sensitive text?
- How do multiple users share it? What's missing before the lab can rely on it?
- You built this in a day — how? *(the AI-assisted development question)*
- What would you build first if hired?

## Expected follow-ups — Scenario 3 (grad-student pipeline)

- What's the FIRST question you'd ask the student?
- Which LLM would you use? Why? What settings?
- How do you make LLM labeling reliable enough to publish with?
- How large a validation subset? How do you measure agreement?
- What if the human annotators disagree with *each other*?
- The IRB says no external APIs — now what?
- When would you NOT use an LLM at all?
- What does "reproducible" concretely mean in your pipeline?
- How do you clean the messy data without destroying signal? What do you log?

## Cross-cutting / behavioral

- Tell me about yourself. / Why this role? (20-second versions in `interview_prep.md`)
- You have 20 hrs/week and three projects — how do you prioritize?
- What don't you know? What would you need help with?
- When can you start? How many hours can you sustain?
- Tell me about a production issue you handled. (Wysa stories)
- Have you worked with researchers / non-engineers before? (Wysa AI team annotation platform)
- Questions for me? (Ask: most urgent project first month? work with you or PhD students day-to-day? existing lab infrastructure/hosting?)

---

# Glossary — refreshers in plain language

## Psychology & measurement

**Construct** — a psychological property you can't observe directly and must measure indirectly: individualism, life satisfaction, moral concern. The whole game is measuring these validly.

**Psychometrics** — the science of measuring psychological constructs: designing scales, proving they're reliable (consistent) and valid (measure what they claim).

**Validated scale / self-report measure** — a fixed set of questionnaire items (e.g., SWLS's 5 items) that research has shown reliably measures a construct. The items are the field's distilled expert knowledge — CCR's key input.

**SWLS** — Satisfaction with Life Scale (Diener et al., 1985). 5 items ("I am satisfied with my life."). Your demo's default example.

**MFQ / Moral Foundations Questionnaire** — Graham, Haidt et al.'s instrument measuring moral foundations: Care, Fairness, Loyalty, Authority, Sanctity. Atari co-authored the MFQ-2 revision — know that Care and Fairness are two of your seeded constructs.

**Individualism / Collectivism** — cultural orientation: self-reliance and independence vs. interdependence and group priority. Triandis & Gelfand's scale distinguishes horizontal (equality-flavored) and vertical (hierarchy-flavored) variants; you seeded the horizontal ones.

**Reverse-scored item** — a scale item worded in the opposite direction ("I rarely feel close to others" on a connectedness scale). In questionnaires you flip the number. In CCR you *can't just flip* — embeddings capture topic more than direction, so the reversed item still sits near the forward items in vector space. Open methods problem; say so.

**Face validity** — "does it pass the smell test": do the top-scoring texts *look* like the construct to a human? Your results screen shows top/bottom texts precisely for this check.

**Convergent validity** — the measure correlates with other measures it theoretically should correlate with.

**Ground truth / gold labels** — human-provided correct answers used to evaluate an automated method.

**Inter-annotator agreement** — how much two+ human labelers agree; the ceiling for any automated method (if humans agree only 75%, don't demand 95% from a model). Measured with **Cohen's kappa** (2 raters) or **Krippendorff's alpha** (any number of raters, missing data OK) — both correct for chance agreement.

**IRB** — Institutional Review Board: the university committee approving human-subjects research. Governs what data can be collected, where stored, whether it may leave campus infrastructure. Why "just call the OpenAI API" can be a hard no.

**Historical psychology** — measuring psychological constructs in historical texts (Atari's EMNLP paper: traditionalism/collectivism in classical Chinese). You can't survey the dead — hence text analysis.

## NLP & ML

**Embedding** — a list of numbers (a vector) representing a piece of text, produced by a neural model, where similar meanings land close together. "Meaning becomes geometry."

**Sentence-transformers / SBERT** — model family + Python library producing one vector per sentence/passage, tuned so cosine similarity between vectors is meaningful. What CCR and your platform use.

**all-MiniLM-L6-v2** — the default sentence-transformers model: small (~90 MB), fast, 384-dimensional vectors, ~256-token window. The CCR reference model. **all-mpnet-base-v2** = bigger/better/slower; **paraphrase-multilingual-MiniLM** = 50+ languages.

**Cosine similarity** — measures the angle between two vectors: 1 = same direction (similar meaning), 0 = unrelated. With L2-normalized vectors it's just the dot product. The single arithmetic operation at CCR's heart.

**L2 normalization** — scaling a vector to length 1 so only direction matters, making dot product = cosine similarity.

**Loading** — CCR's term for one text's cosine similarity to one scale item. The mean loading across a construct's items = the text's **CCR score**.

**CCR in one sentence** — embed the validated scale items and the texts with the same sentence-embedding model; each text's similarity to the items is its loading on the construct.

**Token / token window (max sequence length)** — models read text as tokens (~¾ of a word each) and only the first N (256 for MiniLM). Longer texts are silently truncated — your platform warns about this. Fix: segment long docs, score segments, aggregate.

**Relatedness vs stance** — THE limitation to name: similarity says "this text is about the same topic as the items," not "this text endorses them." A lament about a terrible life scores high on satisfaction similarity. Mitigation: face-validity views + human-validated subsets.

**Dictionary methods (LIWC-style)** — count words from a hand-built list ("fair", "harm"). Fast, transparent, but context-blind. The pre-embedding baseline CCR outperforms.

**Zero-shot** — using a model on a task with no task-specific training. CCR is zero-shot: no labeled examples needed, only the scale items.

**Temperature** — LLM randomness dial. 0 = (near-)deterministic output — what you want for labeling reliability.

**Fine-tuning / contrastive learning** — further training a model on domain data. The EMNLP paper fine-tuned models for classical Chinese with a contrastive objective (pulling related pairs together in vector space). Know the term; don't claim depth.

**RAG** — retrieval-augmented generation: retrieve relevant documents, then have an LLM answer using them. Your KG2RAG project; not part of CCR but likely small-talk fodder.

## Engineering

**FastAPI** — modern Python web framework for APIs: async, typed validation (Pydantic), auto-generated docs. Your backend.

**Pydantic** — Python library defining data shapes; FastAPI uses it to validate every request automatically.

**REST API** — web endpoints (GET/POST...) exchanging JSON — the contract between your React frontend and Python backend.

**SPA (single-page app)** — the browser loads one page (your React build) and JavaScript renders everything, calling the API for data.

**Vite / React build** — React source compiles to static JS/CSS files; your FastAPI serves them, so one process serves both app and API.

**SQLite** — a full SQL database in a single file, no server process. Perfect single-node; limit = concurrent writers. **WAL mode** = write-ahead logging, letting reads proceed during writes.

**PostgreSQL** — the standard client-server SQL database: concurrent writers, backups, managed hosting. The named upgrade from SQLite.

**Object storage (S3/GCS)** — cloud service storing files ("objects") durably and cheaply. The named upgrade from local-disk file storage.

**Worker queue / background jobs** — long tasks (embedding 100k texts) run outside the web request so the browser never waits. Yours: a single worker thread, job state in the DB. **Celery + Redis** = the industrial version: parallel workers, retries, scheduling.

**Orphaned job recovery** — on startup, mark jobs left "running" by a crashed/restarted process as failed with an explanation, so nothing hangs forever in the UI.

**Docker / container** — packages app + dependencies + (here) the ML models into one image that runs identically anywhere. How you deploy to HF Spaces.

**Ephemeral storage** — disk that vanishes when the container restarts. Your demo's documented trade-off; fixed by Postgres + object storage.

**Hugging Face Spaces** — free hosting for ML demos via Docker; where your demo lives, and where the original CCR tool also lives.

**Cold start** — delay when a scaled-to-zero service boots for the first request. Why you warm the Space before 9 AM.

**CORS** — browser rule about which origins may call an API. Non-issue in prod for you (same origin); enabled for the dev server.

**JWT / auth** — signed tokens proving who a user is; part of the named production path (accounts, roles).

**CI / GitHub Actions** — automation running your tests on every push. Roadmap mention.

**Golden-file / parity test** — run your implementation and the reference implementation (`ccr_wrapper`) on identical input; assert identical output. Your correctness answer's centerpiece.

**Deterministic fake embedder** — your test trick: a hash-based stand-in for the ML model so all 17 tests run in ~1 s with no torch. Real model verified separately.

**Reproducibility record** — what your platform stores per run: model name/version, item-wording hash, package versions, timestamps, row counts. The answer to "which model produced Table 2?"

**WCAG 2.1 AA** — the web accessibility standard (semantic HTML, keyboard navigation, contrast, labeled forms, alt text). "AA" is the level universities require for public sites.

**Headless CMS** — content editing UI for non-technical staff that feeds a fast static site — the middle option between "editors use Git" and "run WordPress."

**Presigned URL** — a temporary link letting a browser upload directly to object storage, bypassing your server — the prod path for big files.

**CSV formula injection** — a cell starting with `=` executes when opened in Excel; exports must escape it. Niche, but naming it signals security literacy.

---

## The one-line cheat card

CCR = *embed validated scale items + your texts with the same model; cosine similarity = loading; mean loading = score.* Limitation = *relatedness ≠ stance* → validate with humans. Platform = *the workflow around the method: projects, library, async jobs, face-validity views, exports, reproducibility records.* Production path = *Postgres + S3 + Celery + auth, each with a trigger.* You = *the person who builds that layer, and knows where engineering ends and psychometrics begins.*
