# Verified Claims

> Source of truth for resume content. Anything not in this file should not appear on a resume unless it can be cross-checked in `raw/brain_dump_original.md`. Items marked **Needs verification** must NOT be used as resume claims.

---

## Education

### University of Massachusetts Amherst
- Master of Science in Computer Science.
- September 2025 – May 2027 (Expected).
- Amherst, MA.
- Coursework taken or in progress: CS 689 Advanced Machine Learning; CS 685 Advanced Natural Language Processing; CS 651 Optimization in Computer Science; CS 532 Systems for Data Science; CS 690PF Performance Engineering.

### Vels Institute of Science, Technology and Advanced Studies (VISTAS)
- Bachelor of Engineering in Computer Science and Engineering.
- August 2019 – May 2023.
- Chennai, India.

## Wysa Backend Experience

- Title: Backend Engineer.
- Dates: July 2023 – July 2025.
- Location: Bengaluru, India.
- Stack: Node.js, Express, MongoDB, React, REST APIs, integration tests. Sails.js also appears as a Wysa-era skill tag (LinkedIn-sourced) — verify depth before featuring.
- Team: UK Clinical tech team. eTriage = self-referral and triage flow used by NHS Talking Therapies clients; integrated with Mayden's iaptus platform.

Verified facts:
- Engineered multi-tenant NHS eTriage backend serving 8+ UK clinical clients.
- Processed 10,000+ monthly triage submissions through the eTriage stack.
- Contributed to $340K+ in revenue (per published resumes).
- Remediated 20+ Vulnerability Assessment and Penetration Testing (VAPT) findings.
- Hardened authentication and rate limiting; added integration tests for regression protection.
- Architected a full-stack ML training-data annotation platform (React, Node.js, MongoDB) replacing spreadsheet-based labeling workflows; reduced manual annotation work by 100+ hours/month and improved labeling throughput by 60%.
- Monitored production logs during feature releases and client integrations; investigated and shipped fixes for tenant-specific incidents.
- Acted as primary technical point of contact for the eTriage backend; ran knowledge transfer for new developers on the team.

## Cario Growth Services Backend Internship

- Title: Backend Developer Intern.
- Dates: November 2022 – May 2023.
- Location: Chennai, India.
- Stack: Node.js, Fastify, PostgreSQL, TypeScript. Sequelize ORM also used with PostgreSQL for data migration and CRUD (LinkedIn-sourced detail).

Verified facts:
- Designed and implemented 20+ RESTful APIs in Node.js + Fastify backed by PostgreSQL with input validation, clear contracts, and backward-compatible changes used in production by the frontend team.
- Migrated core codebase from JavaScript to TypeScript across multiple repositories.
- Integrated LLM-powered context-aware replies into a chat product (prompt iteration, response-quality heuristics).

## Open Source / Freelance Work

- Dates: July 2022 – August 2023.
- Remote.

Verified facts:
- Built a gym management platform on the MERN stack (with Redux) with Stripe payments and cron-based email automation; 90%+ of payments moved through the portal; 70% reduction in client manual workload. Live site: https://www.underdogsfitness.in/ (LinkedIn-sourced).
- Selected for GirlScript Summer of Code (GSSoC) 2023.
- Contributed features to open-source projects including Linkfree, Freehit, and ProjectsHut.

Candidate (LinkedIn-sourced, verify before resume use):
- Built an inventory management system for a US client (React, Node.js, Express, MongoDB) with a third-party photo-processing API integration. Distinct freelance deliverable in the same Jul 2022 – Aug 2023 window; no confirmed public repo, so not resume-eligible as a standalone project — usable only as freelance-experience color and as evidence of a second (US) international client.

## AgenticSearch (Provenance-First Entity Discovery)

- Repo: https://github.com/Deva-1903/ciir_agentic_search
- Live demo: https://agentic-search-negglszkwa-uc.a.run.app (hosted demo on Google Cloud Run; resume-safe to show as a live link, but not a production product, no usage metrics).
- Stack: Python, FastAPI, Brave Search API, OpenAI, Groq, SQLite.

Verified facts:
- Multi-stage agentic web-discovery pipeline: typed retrieval planning, web search, page rerank, evidence-regime classification, deterministic entity extraction with LLM fallback, output verification.
- Returns cell-level provenance for every extracted value (value, snippet, source URL/title, confidence).
- Hardened with 150+ automated tests; provider routing/fallback across LLM backends; pipeline instrumentation; reviewer-facing trust UI.

## AutoEval (Retrieval Evaluation Improvement Agent)

- Repo: https://github.com/Deva-1903/AutoEval
- Stack: Python, IR evaluation tooling, Git automation.

Verified facts:
- Agent iteratively improves a retrieval evaluation suite by proposing new queries and labels, scoring against multiple reference systems, and accepting only updates that improve discriminative power on a holdout-heavy fitness objective.
- Anti-Goodharting guardrails: schema checks, duplicate rejection, read-only holdout protection, Git-backed accepted updates with report cards.

## Generative Models & Deep Learning Coursework (CS 689)

- Repo: https://github.com/Deva-1903/UMASS_CICS_689
- Affiliation: UMass Amherst CS 689 Advanced Machine Learning (PhD-level), Prof. Justin Domke, Fall 2025 (first MS CS semester).
- Stack: Python, NumPy, JAX (incl. vmap), PyTorch.

Verified facts (direct code/results or graded submission in the course folder):
- Built a matrix-based reverse-mode automatic differentiation engine from scratch in NumPy — computation-graph nodes with forward/backward rules for add/sub/mul/inner/matmul/solve/logdet/exp/log/logsumexp, topological-sort backpropagation, and a grad operator — validated against JAX to machine precision and applied to multivariate-Gaussian log-likelihood and gradients (HW3, direct code + results).
- Derived linear-regression asymptotics (asymptotic parameter error and risk error) and verified them empirically across N ∈ {10, 100, 1000, 10000} (HW3).
- Derived convergence behavior of gradient descent and SGD on PSD and PD objectives (HW4).
- Trained and benchmarked 5 neural architectures (single-layer perceptron, deep MLP, ReLU MLP, VGG-style CNN, ResNet) on CIFAR-10 across 3 optimizers with learning-rate tuning, documenting train/test-error curves (HW4, graded 87/100).
- Implemented generative models from scratch in JAX: a normalizing flow with coupling layers (trained by negative log-likelihood) and a DDPM diffusion model, deriving the ELBO via variational inference and using the closed-form Gaussian KL (HW5).
- Group final-project proposal (scored 100/100) comparing a BERT / language-model approach against traditional ML on a free-text-feature task.

## KG2RAG-Enhanced (Multi-Hop QA on HotpotQA)

- Repo: https://github.com/Deva-1903/KG2RAG-685-NLP
- Affiliation: UMass Amherst CS 685 Advanced NLP (team project; HotpotQA distractor setting).
- Stack: Python, Ollama + LLaMA-3 8B, sentence-transformers (cross-encoder), llama-index, spaCy, networkx, NumPy/Pandas, PyTorch.

Verified facts:
- Extended KG2RAG with query-side multi-view seed retrieval: sub-question generation, per-view passage retrieval, fusion via Reciprocal Rank Fusion (RRF), cross-encoder reranking, and Maximal Marginal Relevance (MMR). (Deva-led component.)
- 0–1 knapsack token-budget evidence selection (value = relevance × coverage; exact DP + greedy approximation). (Teammate-led — see team-framing note below.)
- Knowledge graphs built over 28,492 unique entities (26,788 used in experiments) across 7,405 questions; evaluated on a 4,905-question subset plus controlled N=1,000 runs, with token/latency logging and 95% binomial confidence intervals.

Verified results (vs KG²RAG baseline, N=4,905):
- Supporting-fact (SP) recall +2.68% (54.53 → 57.21) — headline gain, validates the multi-view retrieval Deva led.
- Answer F1 +0.49 (39.33 → 39.82); SP F1 +0.20 (22.35 → 22.54); EM +0.08 (29.83 → 29.91, CIs overlap, not significant); avg context 298.7 → 335.8 tokens.
- Controlled N=1,000 run: EM +4.2% (43.4 → 47.6, "Precision Shift").

Team-framing (per the final report): Deva led multi-view retrieval (query-side decomposition, per-view retrieval, RRF fusion), core integration, experimental setup, and retrieval/hop-coverage evaluation. The knapsack token-budget selection was teammate Sharvi's and KG construction/reasoning teammate Aditi's, frame those team-wide, not as Deva's solo work.

## Spark ETL Performance Optimization

- Repo: https://github.com/Deva-1903/Spark-ETL-Optimization
- Stack: Python, Apache Spark / PySpark (local spark-submit, 16GB driver/executor on a 24GB machine), Spark UI, uv, SQL. NOT Databricks (the repo runs locally via spark-submit).
- Dataset: NYC TLC trip data, ~1.4B records, 2011–2024, ~30GB.

Verified facts:
- Optimized a naive Spark ETL + analytics pipeline with broadcast joins (~265-zone lookups), Adaptive Query Execution (AQE), shuffle-partition tuning (200), schema-aware 3-batch reads with column pruning (8 cols), year/month partitioning + Snappy compression, skew-join handling (skewJoin + localShuffleReader), filter pushdown, and pre-computed derived columns; plus a 6-rule data-quality filter and a parallel data downloader.
- Used Spark UI metrics and stage-level timings to compare naive vs. optimized runs and document a repeatable optimization playbook.

Verified results (measured, from repo docs):
- Total ETL 17–19 min → 14.3 min (~25%); write step 1050–1150s → 850s (~25%).
- Broadcast joins eliminate shuffle (minutes → ~0.05s).
- Tail-latency ratio (P99/P50) 2.14x → 1.74x (~19%).
- Data-quality filter retains 95.26% of records (4.74% dropped).
- Estimated-only (do NOT state as measured; marked "Est." in repo): analytics queries ~30–50% faster, column pruning 20–30% less I/O, partitioning 30–50% faster time-based queries.

## Sonare (Offline Sign ↔ Speech Cross-Platform App)

- Repo: https://github.com/Deva-1903/Qualcomm-Sep25-Team-Sonare
- Affiliation: Qualcomm Edge AI Hackathon 2025.
- Stack: React, Electron, FastAPI, MediaPipe, whisper.cpp.

Verified facts:
- Built a cross-platform desktop application with on-device pipeline: MediaPipe hand tracking, gesture classification, whisper.cpp ASR, local TTS.
- Engineered FastAPI backend and Electron/React frontend to run fully offline with no external network dependencies.
- Designed async APIs and queues to keep the UI responsive while handling local video and audio streams.

## cf ai research scout (Cloudflare-Native AI Research Assistant)

- Repo: https://github.com/Deva-1903/cf_ai_research_scout
- Stack: TypeScript, Cloudflare Workers AI, AIChatAgent, Durable Objects, WorkflowEntrypoint, D1, WebSockets.

Verified facts:
- Edge-native AI research assistant built end-to-end on Cloudflare Workers; agent fetches web sources and generates multi-step research digests, streaming responses to the client over WebSocket.
- Stateful WebSocket chat via AIChatAgent + Durable Objects; durable multi-step workflow via WorkflowEntrypoint; D1 storage; Workers AI for embeddings and streaming inference.
- Multi-step research tasks survive process restarts and individual tool failures; agent state persists server-side without an external database.

## Refusal Decay / LLM Safety Research

- Repo: https://github.com/Deva-1903/refusal-decay
- Affiliation: **COMPSCI 602 (Research Methods in CS), UMass Amherst, Spring 2026 — final research project, graded full marks** (Report 7: 100/100; final paper: full marks), instructor Prof. David Jensen.

Verified facts:
- Mechanistic-interpretability study of how prefilling attacks weaken refusal behavior in safety-aligned LLMs.
- Primary model Llama-3.1-8B-Instruct (32 layers); Llama-3.2-3B used for smoke tests only. AdvBench harmful prompts + Alpaca benign controls.
- Refusal direction extracted via difference-in-means on a held-out, disjoint 50+50 prompt set; residual-stream projection traced per layer/token position; causal interventions (cross-condition activation patching + additive direction injection) via PyTorch forward hooks.

Verified quantitative findings (from the project's own results):
- Refusal rate 0.92 → 0.32 at prefill k=3 (0.36 at k=10); benign 0.00.
- Late-layer refusal-direction projection shifts negative, monotone-by-depth (Δ 0.76 / 1.63 / 3.23 / 4.08 at layers 16/20/24/27); holds under held-out direction.
- Prompt-level association: refusers vs compliers gap +0.93 / +1.39 / +1.85 at layers 20/24/27.
- Clean causal null: cross-condition patching and additive injection both fail to restore refusal at late layers (0/300), indistinguishable from random/orthogonal controls; benign positive control yields 0 false-refusals.
- Reported with bootstrap 95% CIs + McNemar's test; refusal labels validated by a secondary-classifier spot-check (87.5% agreement).

Status: resume-eligible. Strongest for alignment / interpretability / safety / applied-science roles. Frame as a graded course research project, never as a publication. Do not generalize the causal-null beyond the tested single-position intervention sites or to "safety alignment" globally.

## ngvi-curvature-variance (Natural-Gradient VI Study, CS 651)

- Repo: https://github.com/Deva-1903/ngvi-curvature-variance (public, MIT, resume-eligible).
- Affiliation: UMass Amherst CS 651 (Optimization in Computer Science) final project, Spring 2026. 3-person team (Deva Anand, Jeet Sharma, Rishab Sharma); no per-author breakdown in the report, so keep bullets team-framed.
- Stack: Python, PyTorch (CUDA 12.6), NumPy, matplotlib, PyYAML.

Verified facts:
- Controlled, matched-compute study of when natural-gradient variational inference (NGVI) beats a Euclidean (Adam) baseline on ill-conditioned posteriors; black-box VI with the reparameterization trick.
- Two variational families: Mean-Field Gaussian and Low-Rank-plus-Diagonal (LRD) Gaussian. Three optimizers: Adam, closed-form NGVI (diagonal Fisher), and an EMA-smoothed Diagonal-Fisher quasi-natural method. Antithetic sampling for variance reduction.
- Instrumented ELBO, Hessian condition number κ, and gradient variance per trajectory; benchmarks Neal's Funnel and Eight Schools (centered CP + non-centered NCP).

Verified results (n=3 scenarios):
- NGVI's final-ELBO gain over Adam grows with curvature κ: κ≈180 → +0.28 nats, κ≈535 → +0.50, κ≈2566 → +2.32.
- Closed-form NGVI beats the EMA Diagonal-Fisher method in wall-clock on every LRD scenario despite higher per-step cost; NGVI needs ~3–9× fewer iterations but Adam often reaches threshold in less wall-clock time.
- Antithetic sampling cut gradient variance ~10× but did not lift Adam off ill-conditioned plateaus (ill-conditioning, not noise, is the binding constraint).

Status: resume-eligible (team-framed). Caveats: only 3 scenarios and low-dimensional (D≲10); the κ→ELBO-gain trend is suggestive (visual fit, n=3), not a proven scaling law. Do not claim solo ownership of a component.

## Publication

- Title: "Alzheimer's Disease Classification using Transfer Learning."
- Venue: IEEE CONIT 2023 (3rd International Conference on Intelligent Technologies).
- Repo: https://github.com/Deva-1903/Alzheimer-s-Disease-Classification-
- First-author capstone work; deep transfer learning on neuroimaging data.

## Other Projects (resume-eligible repos)

- ngvi-curvature-variance — now a fully verified CS 651 entry above (promoted 2026-05-23); no longer needs-verification.
- autoresearch-karpathy — auto-research agent workflow experiment. Repo: https://github.com/Deva-1903/autoresearch-karpathy. **Bullets need verification before resume use.**

## Teenofes Software Development Internship (LinkedIn-sourced — verify before resume use)

- Title: Software Development Engineer (Internship).
- Dates: March 2022 – July 2022 (5 months).
- Location: Chennai, India (on-site).
- Stack: Java, JSP, Servlet, SQL; Flutter (frontend widgets).

Candidate facts (LinkedIn description; not yet surfaced on any resume):
- Collaborated with a team of five to build a hospital management system covering information and data flow across healthcare workflows.
- Researched, developed, and shipped product prototypes; built reusable, SEO-friendly frontend widgets in Flutter.
- Predates Cario; an undergraduate-era internship. Cario is the stronger backend signal, so this is normally omitted — keep for JDs that call out Java/JSP/Servlet/Flutter or where chronology comes up in interviews.

## Published Technical Artifacts (LinkedIn-sourced — verify before resume use)

- Medium write-up "Measuring Memory Access Patterns (Sequential vs Strided vs Random)" (~early 2026): a benchmark built for CS 690PF comparing sequential vs strided vs random array access, reporting ~14x slowdown for random access at 128 MB. Self-authored public artifact (the CS 690PF coursework repo is private, but this write-up is its own resume-safe technical-writing data point when a JD values communication).
- Personal-finance / expense-tracker open-source app (~early 2026): low-friction expense logger with natural-language input ("chipotle $14") auto-categorized via an LLM. Stack: React + Vite, Python + FastAPI, Supabase / PostgreSQL, ChatGPT default LLM (swappable to Llama via Groq/Ollama); income tracking, monthly budgets, recurring expenses. Repo `Expense-Tracker` is currently a portfolio repo — confirm repo state before listing as a resume project (see `04_project_bank.md`).

## Volunteer / Extracurricular

- Tutored 30+ underprivileged students in programming at Sayur, a non-profit in South Tamil Nadu.
- GirlScript Summer of Code (GSSoC) 2023 selection; OSS contributions to Linkfree, Freehit, ProjectsHut.

---

## Needs Verification

These claims appear in the brain dump or older resumes but are not safe to use as default resume content:

- Wysa client count of 6+ vs 8+ — pick 8+ for new applications by default; reconcile in interview.
- $340K+ revenue figure — exact time window (one-time / annual / per-client) is not stated.
- Specific clinical interop standards at Wysa (HL7/FHIR) — not confirmed.
- LLM Inference Service quantitative impact (p95 latency, throughput numbers) — no public repo; exclude from resume.
- Distributed Training Simulator quantitative impact — no public repo; exclude from resume.
- Cache- and SIMD-Aware Matrix Multiplication and Performance Engineering Reproduction Study (CS 690PF) — private GitHub Classroom repos; cannot list as projects until a public mirror exists. Coursework reference is fine.
- Scalar-Tensor Autograd Engine (`cpp-autodiff-engine`) — repo currently empty; do not list until populated.
- CI/CD Pipeline for ML Models — no public repo.
- Scalable Recommendation System (Last.fm) — no public repo.
- Gym Management Platform — no public repo (allowed under freelance experience entry only).
- GPA at UMass and at VISTAS — not on any current resume.
- Hackathon placement for Sonare — not stated.
- refusal-decay: do not claim it is a publication/preprint/peer-reviewed (it is a graded course project); do not generalize the causal-null result beyond the tested single-position interventions, beyond Llama-3.1-8B-Instruct, or beyond the prefilling attack family. The documented quantitative findings (0.92→0.32 refusal, monotone late-layer Δ, 0/300 intervention null, 87.5% classifier agreement) ARE usable.
- CS 689 "8 deep architectures on CIFAR-10" — older resumes say 8, but HW4 directly evidences 5 base architectures (perceptron, deep MLP, ReLU MLP, VGG-style CNN, ResNet). Default to 5; 8 may count regularized/optimizer variants — confirm before using.
- CS 689 "RealNVP" specifically — HW5 is a coupling-layer normalizing flow; use "normalizing flow with coupling layers" unless confirmed to be RealNVP.
- CS 689 transformer / self-attention language modeling on Penn Treebank, with scaling analysis (test log-likelihood vs. training FLOPs) over context length / hidden dim / attention heads (HW6) — read from the assignment spec, not confirmed against a submitted file. Verify before resume use.
- CS 689 quantitative results — HW4 CIFAR-10 test accuracy, HW5 sample quality / FID / NLL, HW6 best test log-likelihood, and the final letter grade are not confirmed. HW1 and HW5 completion were read from specs rather than submitted files.
- Teenofes SDE internship (Mar–Jul 2022; Java/JSP/Servlet/SQL/Flutter; hospital management system) — LinkedIn-sourced, never on a resume. Verify scope before featuring; safe only for Java/legacy-stack JDs or interview chronology.
- US-client inventory management system (freelance; React/Node/Express/MongoDB + photo-processing API) — LinkedIn-sourced, no confirmed public repo; not resume-eligible as a standalone project.
- Sequelize ORM (Cario) and Sails.js (Wysa era) — LinkedIn-sourced skill tags; list only when JD-relevant and verify depth first.
- Expense-tracker app (React+Vite / FastAPI / Supabase / LLM) — confirm repo state and content before listing as a resume project.
- MOOC / HackerRank certifications (Udemy, Coursera, HackerRank) and additional volunteering roles (Bhumi organ-donation ambassador, VELS student member, CSC census enumerator) — present in the brain dump's LinkedIn sync but intentionally NOT folded into this factbase (weak resume signal); pull directly from `raw/brain_dump_original.md` Appendix D if ever needed.

If a JD asks for any of these and they are not verified here, either omit the claim or use adjacent truthful experience.
