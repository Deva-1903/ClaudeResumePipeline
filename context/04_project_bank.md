# Project Bank

> Structured project facts. Pull from here only when the bullet bank or factbase is not enough.

---

## AgenticSearch — Provenance-First Entity Discovery

### What it is
Multi-stage agentic web-discovery service that turns open-ended topic queries into structured entity tables with cell-level provenance.

### Verified technologies
Python, FastAPI, Brave Search API, OpenAI, Groq, SQLite. Repo: https://github.com/Deva-1903/ciir_agentic_search. Live demo: https://agentic-search-negglszkwa-uc.a.run.app (Google Cloud Run).

### Strong resume angles
- AI Engineer / LLM Engineer
- ML Engineer (retrieval, evaluation rigor)
- Applied Scientist (research-style provenance and evaluation)
- SDE / Backend (FastAPI service, instrumentation, 150+ tests)

### Verified implementation details
- Typed retrieval planning and per-page rerank.
- Evidence-regime classification.
- Deterministic entity extraction with LLM fallback.
- Output verification step before returning results.
- Cell-level provenance: extracted value, snippet, source URL/title, confidence.
- Provider routing/fallback across OpenAI and Groq backends.
- Pipeline instrumentation and reviewer-facing trust UI.
- 150+ automated tests.

### Possible resume bullets
- Built a multi-stage agentic web-discovery service that converts open-ended topic queries into structured entity tables using typed retrieval planning, page rerank, deterministic extraction with LLM fallback, output verification, and cell-level provenance.
- Returned per-cell provenance (value, source URL/title, snippet, confidence) so every generated table cell is traceable to a verifiable source.
- Hardened the service with 150+ automated tests, provider routing/fallback across OpenAI and Groq, pipeline instrumentation, and a reviewer-facing trust UI for inspecting extraction quality and ranking transparency.
- Designed evidence-regime classification and deterministic-then-LLM extraction order to keep extraction predictable on broad, ambiguous topic queries.

### Do not claim
- No external benchmark numbers (precision/recall, ranking quality).
- A live demo is hosted (DigitalOcean App Platform) and is resume-safe to link, but it is a demo deployment, do not claim production users, adoption, traffic, or SLA.
- No claim of broad-query robustness numbers.

---

## AutoEval — Retrieval Evaluation Improvement Agent

### What it is
Agent that iteratively improves a retrieval evaluation suite by proposing new queries and labels, scoring them against multiple reference systems, and accepting only updates that improve discriminative power.

### Verified technologies
Python, IR evaluation tooling, Git automation.

### Strong resume angles
- AI Engineer (agentic systems with eval rigor)
- Applied Scientist (evaluation methodology)
- ML Engineer (eval pipelines, MLOps adjacency)

### Verified implementation details
- Discriminative-power objective with a holdout-heavy fitness function.
- Anti-Goodharting guardrails: schema checks, duplicate rejection, read-only holdout protection.
- Git-backed accepted updates with report cards for auditability.

### Possible resume bullets
- Built an evaluation-improvement agent that proposes queries and labels, scores them against multiple retrieval systems, and accepts only updates that improve discriminative power on a holdout-heavy fitness objective.
- Added anti-Goodharting guardrails — schema checks, duplicate rejection, and read-only holdout protection — and committed accepted updates back to Git with report cards for an auditable, reproducible eval workflow.

### Do not claim
- No specific deltas in discriminative power.
- No external dataset benchmark numbers.

---

## Generative Models & Deep Learning Coursework (CS 689 Advanced ML)

### What it is
PhD-level Advanced ML (Prof. Justin Domke, Fall 2025): a derive-then-implement course spanning from-scratch automatic differentiation, optimization/convergence theory, deep nets on CIFAR-10, generative models, and transformer language modeling. Strongest direct-evidence artifacts are the HW3 autodiff engine and the graded HW4 (87/100).

### Verified technologies
Python, NumPy, JAX (incl. vmap), PyTorch.

### Strong resume angles
- Applied Scientist / Research
- ML Engineer (modeling rigor)

### Verified implementation details
- Matrix-based reverse-mode automatic differentiation engine from scratch in NumPy (computation graph, topological-sort backprop, operators incl. matmul/solve/logdet/logsumexp), validated against JAX to machine precision; applied to multivariate-Gaussian likelihood and gradients (HW3).
- Derived and empirically verified linear-regression asymptotics (parameter and risk error) across N ∈ {10, 100, 1000, 10000} (HW3).
- Derived gradient-descent and SGD convergence behavior on PSD/PD objectives (HW4).
- Trained and benchmarked 5 neural architectures (perceptron, deep MLP, ReLU MLP, VGG-style CNN, ResNet) on CIFAR-10 across 3 optimizers with learning-rate tuning (HW4, graded 87/100).
- Normalizing flow with coupling layers and a DDPM diffusion model from scratch in JAX; ELBO via variational inference, closed-form Gaussian KL (HW5).

### Possible resume bullets
- Implemented a matrix-based reverse-mode automatic-differentiation engine from scratch in NumPy — computation graphs, topological-sort backpropagation, and operators including matmul, linear solve, and log-determinant — validated against JAX to machine precision.
- Trained and benchmarked 5 neural architectures (perceptron, deep MLP, ReLU MLP, VGG-style CNN, ResNet) on CIFAR-10 across 3 optimizers with learning-rate tuning, documenting train/test-error curves.
- Implemented generative models from first principles — a normalizing flow with coupling layers and a DDPM diffusion model — deriving the ELBO and closed-form Gaussian-KL objectives via variational inference (JAX).
- Derived convergence guarantees for gradient descent and SGD on PSD/PD objectives and analyzed estimator asymptotics (parameter and risk error) with empirical verification.

### Do not claim
- No specific FID / NLL / CIFAR-10 accuracy / Penn Treebank log-likelihood numbers, and no final grade — none verified.
- Do not say "8 architectures" — direct evidence shows 5; do not assert "RealNVP" specifically — it is a coupling-layer flow.
- Transformer / self-attention LM on Penn Treebank (HW6) was read from the spec, not a submitted file — verify before listing.

---

## KG2RAG-Enhanced — Multi-Hop QA on HotpotQA (CS 685)

### What it is
Query-side multi-view retrieval extension to KG2RAG for multi-hop QA on HotpotQA (distractor setting). CS 685 Advanced NLP team project. Deva led the multi-view retrieval component; the knapsack token-budget selection was led by teammate Sharvi and KG construction/reasoning by teammate Aditi.

### Verified technologies
Python, Ollama + LLaMA-3 8B, sentence-transformers (cross-encoder), llama-index, spaCy, networkx, NumPy/Pandas, PyTorch.

### Strong resume angles
- Applied Scientist (retrieval research)
- AI Engineer (RAG sophistication)
- ML Engineer

### Verified implementation details
- Sub-question generation; per-view passage retrieval; fusion via Reciprocal Rank Fusion (RRF), cross-encoder reranking, and Maximal Marginal Relevance (MMR). (Deva-led.)
- 0–1 knapsack token-budget evidence selection (value = relevance × coverage; exact DP + greedy approximation). (Teammate-led.)
- Ollama + LLaMA-3 inference pipeline; knowledge graphs over 28,492 unique entities (26,788 used) across 7,405 questions.
- Evaluated on a 4,905-question large-scale subset plus controlled N=1,000 runs, with token/latency logging and 95% binomial confidence intervals.

### Verified results (vs KG²RAG baseline)
- N=4,905: supporting-fact (SP) recall +2.68% (54.53 → 57.21) — headline gain, validates the multi-view retrieval Deva led; Answer F1 +0.49 (39.33 → 39.82); EM +0.08 (29.83 → 29.91, CIs overlap, not significant); SP F1 +0.20 (22.35 → 22.54); avg context 298.7 → 335.8 tokens.
- Controlled N=1,000 run: EM +4.2% (43.4 → 47.6).
- Lead resume bullets with the +2.68% SP recall figure.

### Possible resume bullets
- Built the multi-view retrieval component of a team KG-guided RAG pipeline for HotpotQA, query-side decomposition into single-hop sub-questions, per-view dense retrieval, and RRF fusion + cross-encoder reranking + MMR, lifting supporting-fact recall +2.68% (54.53 → 57.21) over the KG²RAG baseline on a 4,905-question evaluation.
- Extended KG2RAG with multi-view seed retrieval: generated sub-questions, retrieved passages per view, and fused results via RRF, cross-encoder reranking, and MMR.
- (team-framed) In a team KG-guided RAG pipeline, replaced heuristic top-M selection with a 0–1 knapsack token-budget formulation (value = relevance × coverage) and ran 4,905-question plus controlled N=1,000 batch experiments with token and latency logging.

### Do not claim
- The 0–1 knapsack token-budget selection (teammate Sharvi) and KG construction/reasoning (teammate Aditi) were teammate-led — keep team-framed; do not present as Deva's solo work. Deva's solo-creditable contribution is multi-view retrieval (sub-question decomposition, per-view retrieval, RRF fusion) plus integration and evaluation.
- EM and SP-F1 gains overlap confidence intervals and are not statistically significant; lead with the +2.68% SP recall. Do not present the N=1,000 +4.2% EM as the main-eval result.

---

## Sonare — Offline Sign ↔ Speech Cross-Platform Desktop App

### What it is
Privacy-preserving offline sign-to-speech and speech-to-sign desktop application built at the Qualcomm Edge AI Hackathon 2025.

### Verified technologies
React, Electron, FastAPI, MediaPipe, whisper.cpp.

### Strong resume angles
- SDE / Backend (FastAPI + Electron integration)
- ML Engineer (edge / on-device ML)
- SRE-leaning (async pipeline, offline robustness)

### Verified implementation details
- MediaPipe hand tracking; gesture classification with temporal stabilization.
- whisper.cpp on-device ASR; local TTS.
- Async APIs and queues for video/audio streams.
- Cross-platform Electron + React UI; FastAPI backend running fully offline with no external network dependencies.

### Possible resume bullets
- Built a cross-platform desktop application integrating camera, microphone, UI, and backend services into an on-device pipeline using MediaPipe hand tracking, gesture classification, whisper.cpp ASR, and local TTS — end-to-end product designed and shipped at the Qualcomm Edge AI Hackathon 2025.
- Engineered the FastAPI backend and Electron/React frontend to run fully offline with no external network dependencies; designed async APIs and queues to keep the UI responsive while handling video and audio streams locally.
- Designed the system to preserve privacy by keeping all video, audio, and ML inference on-device.

### Do not claim
- No latency, accuracy, or hackathon placement numbers.

---

## Spark ETL Performance Optimization (NYC TLC Trip Data)

### What it is
Profile-and-optimize study of a naive Spark ETL + analytics pipeline over the NYC TLC trip dataset (~1.4B records, 2011–2024, ~30GB), benchmarking a naive baseline against an optimized build plus an analytics query workload. Runs locally via spark-submit (not Databricks).

### Verified technologies
Python, Apache Spark / PySpark (local spark-submit, 16GB driver/executor on a 24GB machine), Spark UI, uv package manager, SQL.

### Strong resume angles
- SRE / Systems / data platform
- ML Engineer (data engineering side)
- SDE / Backend (data platform context)

### Verified implementation details
- Explicit schemas + schema-era batch reading (3 batches) + column pruning on read (8 cols).
- Adaptive Query Execution (AQE), shuffle-partition tuning (200), 256MB max / 128MB advisory partition sizing.
- Broadcast joins for ~265-zone lookup tables; year/month partitioning + Snappy compression + repartition(50) on write.
- Skew-join handling (skewJoin + localShuffleReader); filter pushdown and pre-computed derived columns in analytics; a 6-rule data-quality filter.
- Parallel data downloader (ThreadPoolExecutor + connection pooling + exponential backoff); DAG analysis; Spark UI metrics; repeatable optimization playbook.

### Verified results (measured, from repo docs)
- Total ETL 17–19 min → 14.3 min (~25%); write step 1050–1150s → 850s (~25%).
- Broadcast joins eliminate shuffle (minutes → ~0.05s).
- Tail-latency ratio (P99/P50) 2.14x → 1.74x (~19%).
- Data-quality filter retains 95.26% of records (4.74% dropped).
- Lead resume bullets with the ~25% ETL runtime cut and the 2.14x → 1.74x tail-latency improvement.

### Possible resume bullets
- Cut end-to-end Spark ETL runtime ~25% (17–19 min → 14.3 min) on a ~1.4B-row NYC TLC dataset by replacing shuffle joins with broadcast joins (minutes → ~0.05s), enabling AQE and skew-join handling, and tuning shuffle partitions, schema-aware reads, and year/month partitioning with Snappy compression.
- Reduced analytics tail-latency ratio (P99/P50) from 2.14x to 1.74x (~19%) via partition pruning, column pruning, filter pushdown, pre-computed derived columns, and adaptive skew-join configuration.
- Profiled stage-level timings via Spark UI to localize shuffle and skew bottlenecks and documented a repeatable optimization playbook comparing naive vs tuned runs.

### Do not claim
- Not Databricks — the repo runs locally via spark-submit; do not list Databricks as a tool for this project.
- Estimated-only figures (analytics queries ~30–50% faster, column pruning 20–30% less I/O, partitioning 30–50% faster time-based queries) are marked "Est." in the repo guide — do not state as measured.

---

## cf ai research scout — Cloudflare-Native AI Research Assistant

### What it is
Edge-native AI research assistant prototyped end-to-end on Cloudflare Workers.

### Verified technologies
TypeScript, Cloudflare Workers AI, AIChatAgent, Durable Objects, WorkflowEntrypoint, D1, WebSockets.

### Strong resume angles
- AI Engineer (LLM systems on edge)
- SRE / Systems (edge / serverless / durable workflows)

### Verified implementation details
- Stateful WebSocket chat via AIChatAgent + Durable Objects.
- Durable multi-step digest generation via WorkflowEntrypoint.
- D1 storage; Workers AI for embeddings and streaming inference.
- Tasks survive process restarts and individual tool failures; agent state persists server-side without an external database.

### Possible resume bullets
- Built an edge-native AI research assistant on Cloudflare Workers: agent fetches web sources, generates multi-step research digests, and streams responses to the client over WebSocket in real time.
- Designed durable workflow boundaries via WorkflowEntrypoint and Durable Objects so multi-step research tasks survive process restarts and individual tool failures, with conversation state persisted in D1.
- Used Workers AI for embeddings and streaming inference, prototyping an end-to-end stateful agent without an external database.

### Do not claim
- No production deployment, no usage metrics, no SLA claims.

---

## Wysa Backend Experience (production)

### What it is
Backend Engineer role on Wysa. Started in Platforms pod (~6 months under manager Tirth Bal — VAPT remediation, B2B app platform tasks), then moved to UK Clinical tech team (manager: Dhaval Kriplani; EM: Paul Sebatien "Sebi"; PM: Sarah; senior dev partner: Tapas). Owned multi-tenant NHS eTriage backend and built a full-stack ML annotation platform.

### Verified technologies
Node.js, Express, MongoDB, React, REST APIs, integration tests, **AWS KMS** (at-rest encryption for PII / clinical data), **AWS SQS** (delayed message scheduling for reminder cadences), **LambdaTest** (cross-browser/device testing). Agile/Scrum: sprint planning, daily stand-ups, retrospectives.

### Strong resume angles
- SDE / Backend (multi-tenant production work)
- SRE / Systems (reliability, security, on-call mindset)
- ML Engineer / AI Engineer (annotation platform fed downstream NLP/clinical models)
- Security / Cloud-adjacent (KMS envelope encryption, 90-day data retention compliance)

### Verified implementation details
- 8+ UK clinical clients; 10,000+ monthly triage submissions; $340K+ in revenue (per resume language).
- 20+ VAPT findings remediated; authentication and rate limiting hardened; integration tests added for regression protection.
- **AWS KMS** used for at-rest encryption of PII / clinical data; **90-day data retention** policy per NHS / client agreement.
- Integrated with Mayden's iaptus platform via REST APIs and aggregation queries; eTriage pipeline spans 3 repos (main chatbot, sigma SQS reminders, eTriage submission).
- Architected a full-stack ML training-data annotation platform replacing spreadsheet-based labeling.
- Reduced manual annotation work by 100+ hours/month; improved labeling throughput by 60%.
- Primary technical POC for the eTriage backend; ran knowledge transfer for new developers (onboarded second eTriage dev to on-call readiness in ~6 weeks via structured KT).
- Authored architecture documentation, sequence diagrams, per-repo READMEs, and post-incident analysis log for the eTriage stack (no prior documentation existed).
- **Copilot productivity pilot (final 6 months):** Selected by COO Shubhankar Sarda for a measured experiment routing tech-debt PRs, code migrations, and security-finding triage through participating devs. Maintained `.github/copilot-instructions.md` conventions file to align AI-generated code with codebase patterns.

### Possible resume bullets
- Engineered multi-tenant NHS eTriage backend (Node.js, MongoDB) for 8+ UK clients, processing 10,000+ monthly triage submissions and integrated with Mayden's iaptus platform via REST APIs; contributed to $340K+ in revenue.
- Owned backend security and reliability across the eTriage stack: monitored production logs during feature releases and client integrations, shipped tenant-specific incident fixes, hardened authentication and rate limiting, and remediated 20+ VAPT findings.
- Implemented AWS KMS envelope encryption for PII / clinical data and enforced a 90-day retention policy per NHS / client agreement across the eTriage stack.
- Architected a full-stack ML training-data annotation platform (React, Node.js, MongoDB) used daily by the AI team; replaced spreadsheet workflows with secure role-based REST APIs, cutting manual operations by 100+ hours/month and improving labeling throughput by 60%.
- Acted as primary technical POC for the eTriage backend; designed and shipped auth, rate limiting, and audit logging features and ran knowledge transfer for new developers on the UK Clinical team — onboarded a second eTriage dev to on-call readiness in ~6 weeks via structured KT.
- Participated in a Copilot productivity pilot, routing tech-debt PRs, code migrations, and security-finding triage through AI-assisted workflows; maintained a versioned `.github/copilot-instructions.md` conventions file to keep AI-generated code aligned with team patterns.

### Do not claim
- Specific clinical interop standards (HL7/FHIR) — not confirmed.
- People-management or staff-level leadership.
- Wysa app scale numbers (1M+ downloads, ~1k concurrent users) — user-confirmed verbally but not currently on any resume; cross-check public source before resume use.
- "10+ active UK clients" — resume default remains 8+; the higher number is for interview color only.

---

## Cario Backend Internship (production)

### What it is
Backend Developer Internship at Cario Growth Services — Node.js/Fastify APIs over PostgreSQL plus an LLM-powered chat integration on **Piechips** (https://piechips.com/), a mobile social app where "chips" are AI characters that post and comment on each other's content. ~10-person startup; reported directly to CEO **Mohan Venkadesan**.

### Verified technologies
Node.js, Fastify, PostgreSQL, TypeScript, Sequelize (ORM). **llama.cpp + Llama-7B (4-bit quantized)** on a single VM for chip auto-commenting inference.

### Strong resume angles
- SDE / Backend (API design)
- AI Engineer (LLM-powered chat integration + open-source LLM auto-comment shipped in production)
- Self-direction / ambiguity (built ML capability with no ML mentor on the team)

### Verified implementation details
- 20+ RESTful APIs in Node.js + Fastify backed by PostgreSQL; input validation, clear contracts, backward-compatible changes used by the frontend team.
- Migrated core codebase from JavaScript to TypeScript across multiple repositories.
- Integrated LLMs into a chat product to generate context-aware replies from conversation history and user input; iterated on prompt design and response-quality heuristics.
- **Open-source LLM auto-commenting feature for Piechips:** Shipped an auto-commenting system where each AI "chip" character generates in-character comments on other chips' posts. Built end-to-end with no ML mentor on the team; designed under tight resource constraints (single VM, no GPU budget) using 4-bit quantized Llama-7B via llama.cpp; per-chip persona prompts (no fine-tuning per chip); async queued generation with per-chip rate limits, short-circuit caching for similar recent posts, and a deterministic content-safety filter before publish.
- Worked closely with 2 frontend app developers on API design.

### Possible resume bullets
- Designed and implemented 20+ RESTful APIs in Node.js + Fastify backed by PostgreSQL with input validation, clear contracts, and backward-compatible changes used in production by the frontend team.
- Migrated core codebase from JavaScript to TypeScript across multiple repositories, improving type safety and long-term maintainability.
- Integrated LLM-powered context-aware replies into a chat product, iterating on prompt design, evaluation, and response-quality heuristics for a real customer-facing experience.
- Shipped an open-source LLM auto-commenting feature in production (4-bit quantized Llama-7B via llama.cpp on a single VM): per-chip persona prompts, async queued generation, per-character rate limits, short-circuit caching, and a content-safety filter — built end-to-end with no ML mentor on the team.

### Do not claim
- No metrics on prompt-quality improvements, latency, or coverage.
- No ML-engineer title or formal ML role; the ML scope was self-directed under CEO sponsorship.

---

## Alzheimer's Disease Classification (Publication, Undergrad Capstone)

### What it is
First-author deep transfer-learning study on neuroimaging data; published at IEEE CONIT 2023.

### Verified technologies
Python, PyTorch, transfer learning.

### Strong resume angles
- Applied Scientist / Research
- ML Engineer

### Verified implementation details
- Backbone-architecture experiments; training-setup variations.
- Comparison vs standard metrics with robustness checks.

### Possible resume bullets
- "Alzheimer's Disease Classification using Transfer Learning," IEEE CONIT 2023 — applied deep transfer learning on neuroimaging data for medical image classification.

### Do not claim
- No specific accuracy / AUC / dataset-size numbers beyond what the paper itself reports.

---

## Refusal Decay (LLM Safety / Mechanistic Interpretability) — strongest for research/safety roles

### What it is
Mechanistic-interpretability study of how prefilling attacks weaken refusal behavior in a safety-aligned LLM, and whether intervening on the internal "refusal direction" can recover refusal. Final research project for **COMPSCI 602 (Research Methods in Computer Science), UMass Amherst, Spring 2026** — graded full marks (Report 7: 100/100; final paper: full marks) by Prof. David Jensen. Public repo + 8 staged reports.

### Verified technologies
Python, PyTorch (forward hooks for activation capture/editing), Hugging Face Transformers; Llama-3.1-8B-Instruct (primary, 32 layers; Llama-3.2-3B for smoke tests); AdvBench (harmful prompts); Alpaca (benign controls). Repo: https://github.com/Deva-1903/refusal-decay

### Strong resume angles
- Applied Scientist / Research (alignment, interpretability, safety, experimental rigor)
- ML Engineer (interpretability tooling, evaluation/statistics)

### Verified implementation details
- Extracted the refusal direction by difference-in-means (Arditi et al. method) on a **held-out, disjoint** 50 harmful + 50 benign prompt set, so the direction is not fit on the prompts it is evaluated on.
- Traced the residual-stream refusal-direction projection per layer and generated-token position under prefilling at k ∈ {0, 3, 10}, layers {16, 20, 24, 27}.
- Two causal interventions via PyTorch forward hooks: cross-condition activation patching (clean k=0 source into attacked k=3 forward pass) and additive direction injection (add α·direction at a generated-token position).
- Controls: benign positive control (false-refusal test), multi-seed random and orthogonal direction baselines (5 seeds each), held-out direction extraction.
- Statistics: bootstrap 95% confidence intervals and McNemar's exact test on per-prompt intervention outcomes; secondary-classifier spot-check (87.5% agreement) to validate the phrase-list refusal labels.

### Verified quantitative findings
- Prefilling at k=3 dropped refusal rate from **0.92 to 0.32** on harmful prompts (0.36 at k=10); benign refusal stayed at 0.00.
- The late-layer refusal-direction projection shifted strongly negative under attack with a **monotone-by-depth gradient** (Δ = 0.76, 1.63, 3.23, 4.08 at layers 16/20/24/27); robust under the held-out direction.
- Prompt-level association: within attacked prompts, those that still refused had less-negative late-layer projection than those that complied (gaps +0.93, +1.39, +1.85 at layers 20/24/27).
- Clean negative causal result: neither cross-condition patching nor additive direction injection restored refusal at the late layers (**0 of 300** prompts), statistically indistinguishable from random/orthogonal controls — evidence the late-layer signal is a predictive readout, not the causal lever at the tested intervention sites.

### Possible resume bullets
- Ran a mechanistic-interpretability study (graded full marks, COMPSCI 602, UMass Amherst) of how prefilling attacks weaken refusal in Llama-3.1-8B-Instruct, measuring the residual-stream "refusal direction" extracted by difference-in-means on a held-out prompt set.
- Showed the late-layer refusal-direction signal shifts negative under attack with a monotone-by-depth gradient and predicts per-prompt refusal vs. compliance, while behavioral refusal dropped from 0.92 to 0.32 at prefill length k=3.
- Designed and ran two causal interventions (cross-condition activation patching and additive direction injection via PyTorch forward hooks) with multi-seed random/orthogonal controls and a benign positive control; reported a clean null result with bootstrap 95% CIs and McNemar's test, showing the late-layer signal is a readout rather than the causal lever at the tested sites.
- Validated heuristic refusal labels with an independent secondary-classifier spot-check (87.5% agreement) and documented internal/external threats to validity across an 8-report research arc.

### Do not claim
- Not a publication — it is a graded course research project. Do not call it a paper, preprint, or peer-reviewed work (the only verified publication is the IEEE CONIT 2023 Alzheimer's paper).
- Single model (Llama-3.1-8B-Instruct) and single attack family (prefilling) — do not generalize the causal-null claim beyond the tested intervention sites or to "safety alignment" globally.
- No multi-node/large-scale training; all inference-only on a single GPU.

---

## ngvi-curvature-variance — "When Do Natural Gradients Help?" (CS 651 Optimization)

### What it is
Controlled, matched-compute study of *when* natural-gradient variational inference (NGVI) beats a Euclidean (Adam) baseline on ill-conditioned posteriors. UMass CS 651 (Optimization in Computer Science) final project, Spring 2026; public MIT repo (resume-eligible). 3-person team (Deva Anand, Jeet Sharma, Rishab Sharma); the report has no per-author contribution breakdown, so keep bullets team-framed.

### Verified technologies
Python, PyTorch (CUDA 12.6), NumPy, matplotlib, PyYAML (config-driven experiments). Repo: https://github.com/Deva-1903/ngvi-curvature-variance

### Strong resume angles
- Applied Scientist / Research (optimization, Bayesian deep learning, experimental rigor)
- ML Engineer (optimization methods, variance reduction)

### Verified implementation details
- Black-box variational inference with the reparameterization trick.
- Two variational families: Mean-Field Gaussian and Low-Rank-plus-Diagonal (LRD) Gaussian (Σ = diag(e^2s) + VVᵀ).
- Three optimizers: Adam (Euclidean), closed-form NGVI (diagonal Fisher), and an EMA-smoothed Diagonal-Fisher quasi-natural method.
- Antithetic sampling for Monte-Carlo variance reduction; curvature and variance treated as separate axes.
- Instrumented ELBO, Hessian condition number κ, and gradient variance on every trajectory.
- Benchmarks: Neal's Funnel and Eight Schools (centered CP + non-centered NCP).

### Verified results (n=3 scenarios)
- NGVI's final-ELBO gain over Adam grows with curvature κ: κ≈180 → +0.28 nats, κ≈535 → +0.50, κ≈2566 → +2.32.
- Closed-form NGVI beats the EMA Diagonal-Fisher quasi-natural method in wall-clock on every LRD scenario despite higher per-step cost.
- Adam and NGVI are complementary: NGVI needs ~3–9× fewer iterations, but Adam often reaches threshold in less wall-clock time (per-step Fisher-inversion cost).
- Antithetic sampling cut gradient variance ~10× but did not lift Adam off ill-conditioned plateaus — ill-conditioning, not noise, is the binding constraint.

### Possible resume bullets
- Built a PyTorch black-box variational-inference testbed comparing Adam, closed-form natural-gradient (NGVI), and EMA Diagonal-Fisher optimizers across mean-field and low-rank-plus-diagonal Gaussian families on Neal's Funnel and the Eight Schools model.
- Showed NGVI's ELBO gain over Adam grows with posterior ill-conditioning (κ≈180 → 2566 maps to +0.28 → +2.32 nats) and that closed-form NGVI beats an EMA Diagonal-Fisher method in wall-clock on every scenario despite O(D³) Fisher-inversion cost.
- Instrumented ELBO, Hessian condition number, and gradient variance jointly to separate curvature from Monte-Carlo-noise bottlenecks, showing antithetic sampling cut gradient variance ~10× yet could not rescue Adam from ill-conditioned plateaus.

### Do not claim
- Team project with no per-author breakdown — keep bullets team-framed; do not claim solo ownership of a specific component.
- Only 3 scenarios and low-dimensional (D≲10); the κ→ELBO-gain trend is "suggestive," a visual fit at n=3, not a proven scaling law.
- §4.4/Fig. 4 attribute the κ-trend to the mean-field family while the Conclusion says LRD — cite the family carefully if pressed.

---

## Underdogs Fitness — Gym Management Platform (production, freelance solo)

### What it is
End-to-end gym website + management platform built solo as a freelance project (May–June 2023) for Underdogs Fitness, a newly-opened gym in India. Still in production 3+ years later; extended to a 2nd branch in 2025 as a config change with zero schema migration. **Promoted to resume-eligible standalone project 2026-06-08** (repos confirmed public).

### Verified technologies
**MERN stack:** MongoDB Atlas, Express, React + Redux, Node.js. **Hosts:** DigitalOcean droplet (backend), Vercel (frontend), MongoDB Atlas (DB), Firebase Storage (images). **Auth:** JWT with `branchId` claim. **Payments:** Stripe (online) + admin manual cash entry with partial-payment ledger (offline). **Automation:** Cron-based email notifications for renewals/payments. **Deploy:** git-webhook auto-deploy (GitHub webhook → DO droplet on push).

### Repos (public, resume-eligible)
- Backend: https://github.com/Deva-1903/backend_underdogs
- Frontend: https://github.com/Deva-1903/frontend_underdogs
- Live: https://www.underdogsfitness.in/

### Strong resume angles
- SDE / Full-Stack (solo end-to-end delivery)
- SDE / Backend (multi-tenant-style branch design; payments + ledger)
- Demonstrates ambiguity tolerance + calculated-risk delivery (sole dev, 3 unknowns time-boxed at 2 days each: payment integration, DigitalOcean deployment, Firebase image storage — with explicit fallbacks)
- Demonstrates long-term design (multi-branch first-class entity from day 1)

### Verified implementation details
- Member onboarding + authentication; membership tier + renewal management.
- Attendance tracking; subscription updates; admin controls; coach/staff management.
- **Payments:** Stripe checkout for online payment + admin manual cash entry with a partial-payment ledger tracking full/partial paid state per member.
- **Cron-based email automation** for payment events and renewal reminders.
- **Multi-branch architecture from day 1:** every member, attendance, payment, and coach row carries a `branchId` FK; auth scoped by `branchId` JWT claim; frontend uses a branchContext provider.
- **Extension to 2nd branch (2025):** Onboarded as a configuration change — insert one `branches` row, assign admins, done. **Zero schema migration.**
- **Image storage:** Firebase Storage SDK upload returns public URL stored against the entity.
- **Auto-deploy pipeline:** git push → GitHub webhook → DigitalOcean droplet pulls + restarts service.

### Quantified outcomes (delivery window)
- 90%+ of payments moved through the portal vs prior manual collection.
- 70% reduction in client manual workload via cron-driven automation.
- Sole-dev solo delivery in ~1.5–2 months across May–June 2023.

### Longevity outcome (post-delivery)
- Still in production 3+ years later (2026); extended to 2nd branch in 2025 with no schema migration; the owner explicitly cited the plug-and-play multi-branch design.

### Possible resume bullets
- Built and deployed **Underdogs Fitness** (https://www.underdogsfitness.in/), a production gym management platform (MERN: MongoDB Atlas, Express, React + Redux, Node.js) solo end-to-end in ~1.5 months — auth, membership management, attendance tracking, Stripe + manual-cash payment processing with a partial-payment ledger, and cron-based renewal automation; live 3+ years.
- Designed for multi-branch from day 1 (every entity scoped by `branchId`, JWT-claim-based auth, frontend branch context); when the client extended to a 2nd branch a year later, onboarded it as a configuration change with **zero schema migration**.
- Set up CI/CD via git-webhook auto-deploy (GitHub webhook → DigitalOcean droplet on push) with Vercel for the frontend and Firebase Storage for media; moved 90%+ of payments through the portal and cut the client's manual workload ~70%.

### Do not claim
- No quantified user count (membership numbers belong to the gym).
- Not a multi-tenant SaaS — it is a single-customer, multi-branch system.
- Stripe + cash hybrid is the design; do not claim Stripe-only or cash-only.

---

## MERN Inventory Management System (US-client freelance) — confirmed, no public repo

### What it is
Inventory management system built for a US client during the Jul 2022 – Aug 2023 freelance window. **User-confirmed 2026-06-08** as a real paid client engagement (was previously LinkedIn-sourced / "needs verify"). Distinct freelance deliverable from the gym platform; evidence of a second (US, international) client.

### Verified technologies
MERN stack (MongoDB, Express, React, Node.js).

### Status / do not claim
- **No public repo** — not resume-eligible as a standalone project (per Build Guide §5.6).
- Surface only as freelance-experience color under the Open Source / Freelance entry, and as evidence of a second international client.
- No quantified outcome numbers known.

---

## CCR Platform — Psychological Text Analysis Web Platform (deployed demo)

### What it is
Full-stack web platform for CCR (Contextualized Construct Representations; Atari, Omrani et al.) psychological text analysis: upload a corpus, select/define a validated construct, run analysis with locally-hosted sentence embeddings, inspect per-item loadings and distributions, export results with a reproducibility record. Built solo in ~1 day (AI-assisted, July 2026) while interviewing with the Culture and Morality Lab (UMass PBS); sent to the PI as a working demo ahead of the interview.

**OUTCOME: hired off this demo.** The lab work continues as EMPLOYMENT (Lab Assistant, July 2026 – present) with its own claims — see `01_verified_claims.md` "Culture and Morality Lab (CAM Lab) Experience". This entry stays scoped to the pre-hire demo. On resumes, prefer the employment entry; use this demo as a PROJECT only when the resume does not carry the CAM Lab experience entry (avoid double-counting the same system twice on one page).

### Verified technologies
Python, FastAPI, Pydantic, SQLAlchemy, SQLite (WAL), pandas, NumPy, sentence-transformers (all-MiniLM-L6-v2 / all-mpnet-base-v2 / multilingual MiniLM), React 18 + Vite, Docker, Hugging Face Spaces. Repo: https://github.com/Deva-1903/ccr-platform. Live: https://devaanand-ccr-platform.hf.space

### Strong resume angles
- AI Engineer / NLP tooling (embedding pipeline, model-serving trade-offs)
- SDE / Full-Stack (single-deployable FastAPI + React, job queue, ingestion hardening)
- Research infrastructure / computational social science roles (reproducibility record, face-validity views, validated-scale library)

### Verified implementation details
- CCR engine: same-model embedding of scale items + texts, L2-normalized, cosine similarity = per-item loadings, mean = score; item-embedding cache; pluggable EmbeddingBackend with deterministic fake for tests.
- Tolerant ingestion: encoding fallback (utf-8-sig → latin-1, user-facing note), delimiter sniffing, ragged-row skip, row/size caps, text-column suggestion heuristic, parse-info recorded per corpus.
- Job system: single-worker queue with DB-persisted state and progress polling; orphaned-job recovery on startup; documented Celery/Postgres/S3 upgrade triggers.
- Data-quality warnings (duplicates, dropped empties, token-window truncation) surfaced in results; per-run reproducibility record (model version, SHA-256 item hash, package versions, timestamps).
- Seeded construct library with citations (SWLS; MFQ Care/Fairness; Triandis & Gelfand Individualism/Collectivism) + verify-before-research-use caveats.
- 17 automated tests (engine + full API flow) running without torch via the fake backend; Docker image bakes all 3 models to eliminate runtime download stalls; deployed on HF Spaces free tier.

### Possible resume bullets
- Built and deployed a full-stack platform for CCR psychological text analysis (FastAPI, React, sentence-transformers, SQLite, Docker): corpus upload → validated-construct selection → embedding + cosine-similarity scoring → per-item loadings, distributions, and CSV export with a per-run reproducibility record (model version, item hash, package versions).
- Hardened ingestion for real-world research data — encoding fallback, delimiter sniffing, row/size caps, and researcher-facing data-quality warnings (duplicates, empty rows, token-window truncation) — and ran analyses on a DB-backed worker queue with orphaned-job recovery.
- Designed a pluggable embedding backend with a deterministic fake for CI, enabling 17 end-to-end tests to run in ~1s without ML dependencies; baked all offered models into the Docker image to eliminate cold-start downloads on Hugging Face Spaces.

### Do not claim
- No production users or adoption metrics — demo deployment (ephemeral storage, no auth). UPDATE 2026-07-11: now HIRED, so the demo may be framed as "built during the interview process for the lab that then hired me" and the hire itself is claimable; the demo still is not "the lab's platform" (that is the employment work in `01_verified_claims.md`).
- No benchmark/accuracy numbers; scale item wordings not verbatim-verified against original publications.
- Do not present as a publication or research contribution — it is an engineering implementation of a published method.

---

## Candidate Projects (LinkedIn-sourced — confirm before resume use)

> These are not yet resume-eligible defaults. They come from the brain dump's LinkedIn sync. Verify repo state and scope before surfacing on any resume.

### Expense Tracker — Natural-Language LLM Expense Logger

**What it is.** Open-source personal-finance app: log an expense in natural language ("chipotle $14") and an LLM auto-categorizes it. Adds income tracking, monthly budgets with progress bars, and recurring expenses.

**Verified technologies.** React + Vite (frontend), Python + FastAPI (backend), Supabase / PostgreSQL (DB), ChatGPT as default LLM (swappable to Llama via Groq/Ollama). Deployable on Vercel / Render / Supabase free tiers.

**Strong resume angles.** AI Engineer (LLM-feature angle: NL expense parsing), Full-Stack / SDE.

**Status / do not claim.** Repo `Expense-Tracker` is currently a portfolio repo, not a vetted resume project — confirm it has real, public code before listing (Build Guide §5.6). No usage or accuracy metrics.

### Inventory Management System (US-client freelance sub-project)

**MOVED:** Promoted to a confirmed entry above ("MERN Inventory Management System (US-client freelance) — confirmed, no public repo"). Confirmed by user 2026-06-08 as a real paid engagement. Remains not-standalone-resume-eligible due to no public repo; surface only as freelance-experience color.

### Memory-Access-Patterns Benchmark (Medium write-up)

**What it is.** A small CS 690PF benchmark comparing sequential vs strided vs random array access (reports ~14x slowdown for random access at 128 MB), published as a self-authored Medium write-up.

**Status.** The CS 690PF coursework repo is private, but the published write-up is its own artifact — resume-safe as a technical-writing / communication data point when a JD values it. Not a standalone code project.
