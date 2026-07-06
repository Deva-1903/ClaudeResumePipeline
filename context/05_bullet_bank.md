# Bullet Bank

> Paste-ready bullets, organized by role family. Tags in `[brackets]` indicate which projects/roles a bullet maps to. Pick the smallest set that covers the JD; tighten metrics only if they appear verbatim in `01_verified_claims.md`.

---

## SDE / Backend Bullets

### Wysa
- [Wysa] [Backend] [SDE] Engineered multi-tenant NHS eTriage backend (Node.js, MongoDB) for **8+ UK clients**, processing **10,000+ monthly triage submissions** and integrated with Mayden's iaptus platform via REST APIs and aggregation queries; contributed to **$340K+** in revenue.
- [Wysa] [Backend] [SDE] Architected a full-stack data annotation platform (React, Node.js, MongoDB) used daily by the AI team; replaced spreadsheet workflows with secure role-based REST APIs, cutting manual operations by **100+ hours/month** and improving labeling throughput by **60%**.
- [Wysa] [Backend] [Security] Owned backend security and reliability across the eTriage stack: hardened authentication and rate limiting, added integration tests, and remediated **20+ VAPT findings** to protect sensitive clinical data against regressions.
- [Wysa] [Backend] [Security] Implemented **AWS KMS envelope encryption** for PII / clinical data on the multi-tenant eTriage stack and enforced a **90-day data-retention policy** per NHS / client agreement.
- [Wysa] [Leadership] Acted as primary technical POC for the eTriage backend; designed and shipped auth, rate limiting, and audit logging features and ran knowledge transfer for new developers on the UK Clinical team — onboarded a second eTriage dev to on-call readiness in ~6 weeks via structured KT.
- [Wysa] [AI Eng] [Tooling] Participated in a Copilot productivity pilot, routing tech-debt PRs, code migrations, and security-finding triage through AI-assisted workflows; maintained a versioned `.github/copilot-instructions.md` conventions file to keep AI-generated code aligned with team patterns.

### Cario
- [Cario] [Backend] [SDE] Designed and implemented **20+ RESTful APIs** in Node.js + Fastify backed by PostgreSQL with input validation, clear contracts, and backward-compatible changes used in production by the frontend team.
- [Cario] [SDE] Migrated core codebase from JavaScript to TypeScript across multiple repositories, improving type safety and long-term maintainability.
- [Cario] [AI Engineer] Integrated LLM-powered context-aware replies into a chat product, iterating on prompt design and response-quality heuristics for a real customer-facing experience.
- [Cario] [AI Engineer] [Frugality] Shipped an open-source LLM auto-commenting feature for the Piechips social app in production — **4-bit quantized Llama-7B via llama.cpp on a single VM** with per-character persona prompts, async queued generation, per-character rate limits, short-circuit caching, and a deterministic content-safety filter — built end-to-end with no ML mentor on the team.

### AgenticSearch (backend angle)
- [AgenticSearch] [Backend] [SDE] Built a Python/FastAPI service for an agentic web-discovery pipeline with provider routing across OpenAI/Groq, pipeline instrumentation, and a reviewer-facing trust UI.
- [AgenticSearch] [Backend] Hardened the service with **150+ automated tests** and provider fallback to keep extraction predictable across LLM backends.

### Sonare (backend angle)
- [Sonare] [Backend] Engineered a FastAPI backend and Electron/React frontend that run fully offline; designed async APIs and queues to keep the UI responsive while handling local video and audio streams.

---

## SRE / Systems Bullets

### Wysa reliability framing
- [Wysa] [SRE] Owned backend reliability and security for multi-tenant NHS eTriage systems (Node.js, MongoDB) serving **8+ UK clients** and processing **10,000+ monthly triage submissions** integrated with Mayden's iaptus platform.
- [Wysa] [SRE] Monitored production logs during feature releases and client integrations, investigated incident bugs, and shipped fixes for tenant-specific and integration issues; improved operational stability through authentication hardening, rate limiting, and audit logging.
- [Wysa] [SRE] [Security] Remediated **20+ VAPT findings** and added integration tests to protect sensitive clinical workflows against regressions; enforced secure-by-default patterns across tenant isolation and backend access paths.

### Spark / data systems
- [Spark] [SRE] [Performance] Cut end-to-end Spark ETL runtime **~25%** (17 to 19 min down to 14.3 min) on a **~1.4B-row** NYC TLC dataset by replacing shuffle joins with broadcast joins (minutes to ~0.05s), enabling AQE and skew-join handling, and tuning shuffle partitions, schema-aware reads, and year/month partitioning with Snappy compression.
- [Spark] [SRE] [Performance] Reduced analytics tail-latency ratio (P99/P50) from **2.14x to 1.74x** (~19%) via partition pruning, column pruning, filter pushdown, pre-computed derived columns, and adaptive skew-join configuration.
- [Spark] [SRE] [Performance] Optimized a Spark ETL pipeline on the NYC TLC taxi dataset with broadcast-join tuning, caching, partitioning, adaptive Spark settings, column pruning, and precomputed fields to reduce shuffle volume and wall-clock runtime.
- [Spark] [SRE] [Performance] Used Spark UI metrics and stage-level timings to localize shuffle and skew bottlenecks and to document a repeatable optimization workflow for downstream analytics jobs.

### CS 690PF Performance Engineering (public repo `github.com/Deva-1903/cs690pf`; graded coursework, resume-eligible)
- [CS690PF] [Systems] [Performance] [SDE] Optimized C++ matrix multiplication from a naive baseline through cache-aware tiling, manual **AVX/SIMD** vectorization, register-aware micro-kernels, and **OpenMP** multithreading, profiling L1/L3/TLB misses with **perf** and inspecting generated assembly.
- [CS690PF] [Systems] [Performance] Built an 8-stage C++ matmul optimization pipeline (loop reorder, unroll, blocking, AVX SIMD, cache-aware tiling with hardware-tuned Kc/Mc/Nc + Mr/Nr micro-kernels, register-aware YMM kernels, OpenMP), profiling each stage with `perf` on Linux.
- [CS690PF] [Systems] [Research] Reproduced results from three performance-engineering papers (Coz causal profiling on SQLite, Hoard vs. `ptmalloc2`/`jemalloc`/`mimalloc` false-sharing, Mytkowicz measurement bias), building allocators from source without root and using `perf c2c`, Cachegrind, and TMA to explain discrepancies.

### Coursework / performance
- [CS 690PF] [Systems] Coursework in Performance Engineering covering profiling, cache-aware design, vectorization concepts, and multithreading on Linux.

### Sonare (systems angle)
- [Sonare] [Systems] Designed an offline pipeline with async queues and local-only inference (MediaPipe + whisper.cpp + local TTS), keeping the UI responsive without external network dependencies.

### cf ai research scout (edge / durable systems)
- [cf-ai-research-scout] [Systems] Designed durable workflow boundaries via WorkflowEntrypoint and Durable Objects so multi-step agent tasks survive process restarts and tool failures, with conversation state persisted in D1.

---

## ML Engineer Bullets

### CS 689 (Advanced ML)
- [CS 689] [MLE] [Research] Implemented a **matrix-based reverse-mode automatic differentiation engine from scratch in NumPy** — computation graphs, topological-sort backpropagation, and operators including matmul, linear solve, and log-determinant — **validated against JAX** to machine precision.
- [CS 689] [MLE] Trained and benchmarked **5 neural architectures** (perceptron, deep MLP, ReLU MLP, VGG-style CNN, ResNet) on **CIFAR-10** across **3 optimizers** with learning-rate tuning, documenting train/test-error curves.
- [CS 689] [MLE] [Research] Implemented generative models from scratch in JAX — a **normalizing flow with coupling layers** and a **DDPM diffusion model** — deriving the ELBO and closed-form Gaussian-KL objectives via variational inference.

### KG2RAG-Enhanced
- [KG2RAG] [MLE] [AI Eng] [IR] Built the multi-view retrieval component of a team KG-guided RAG pipeline for HotpotQA, query-side decomposition into single-hop sub-questions, per-view dense retrieval, and RRF fusion + cross-encoder reranking + MMR, lifting supporting-fact recall **+2.68%** (54.53 to 57.21) over the KG²RAG baseline on a **4,905-question** evaluation.
- [KG2RAG] [MLE] [AI Eng] [IR] Extended KG2RAG with multi-view seed retrieval on HotpotQA: generated sub-questions, retrieved passages per view, and fused via Reciprocal Rank Fusion (RRF), cross-encoder reranking, and MMR.
- [KG2RAG] [MLE] [AI Eng] [team-framed] In a team KG-guided RAG pipeline, replaced heuristic top-M selection with a 0–1 knapsack token-budget formulation (value = relevance × coverage) and ran 4,905-question and controlled N=1,000 batch experiments with token and latency logging on an Ollama + LLaMA-3 pipeline.

### AgenticSearch (ML angle)
- [AgenticSearch] [MLE] [AI Eng] Built a multi-stage agentic web-discovery pipeline that plans typed retrieval, reranks pages, classifies evidence regimes, extracts entities with deterministic parsers before LLM fallback, verifies outputs, and returns cell-level provenance.

### Wysa (ML data infra angle)
- [Wysa] [MLE] Architected a full-stack ML training-data annotation platform (React, Node.js, MongoDB) used daily by the AI team; cut manual annotation work by **100+ hours/month** and improved labeling throughput by **60%**.

---

## AI Engineer Bullets

### AgenticSearch
- [AgenticSearch] [AI Eng] Built a multi-stage agentic web-discovery service that converts open-ended topic queries into structured entity tables using typed retrieval planning, page rerank, deterministic extraction with LLM fallback, output verification, and **cell-level provenance** for every result.
- [AgenticSearch] [AI Eng] Hardened the service with **150+ automated tests**, provider routing/fallback across OpenAI and Groq, pipeline instrumentation, and a reviewer-facing trust UI.

### AutoEval
- [AutoEval] [AI Eng] [Eval] Built an evaluation-improvement agent that proposes queries and labels, scores them against multiple retrieval systems, and accepts only updates that improve discriminative power on a holdout-heavy fitness objective.
- [AutoEval] [AI Eng] [Eval] Added anti-Goodharting guardrails — schema checks, duplicate rejection, read-only holdout protection — and committed accepted updates back to Git with report cards for an auditable, reproducible eval workflow.

### KG2RAG-Enhanced
- [KG2RAG] [AI Eng] [RAG] Built the multi-view retrieval component of a team KG-guided RAG pipeline for HotpotQA, decomposing complex questions into single-hop sub-questions and fusing per-view retrieval with RRF, cross-encoder reranking, and MMR, lifting supporting-fact recall **+2.68%** (54.53 to 57.21) over the KG²RAG baseline on a 4,905-question evaluation.

### cf ai research scout
- [cf-ai-research-scout] [AI Eng] Built an edge-native AI research assistant on Cloudflare Workers: agent fetches web sources, generates multi-step research digests, and streams responses to the client over WebSocket in real time.
- [cf-ai-research-scout] [AI Eng] Used Workers AI for embeddings and streaming inference and prototyped end-to-end stateful agent behavior (AIChatAgent + Durable Objects + WorkflowEntrypoint + D1) without an external database.

### Cario (LLM in production)
- [Cario] [AI Eng] Integrated LLMs into a chat product to generate context-aware replies from conversation history and user input; iterated on prompt design and response-quality heuristics for a real customer-facing experience.

---

## Applied Scientist / Research Bullets

### CS 689
- [CS 689] [Research] Implemented a matrix-based reverse-mode automatic differentiation engine from scratch in NumPy and validated it against JAX to machine precision; applied it to multivariate-Gaussian likelihood and gradients.
- [CS 689] [Research] Implemented generative models from first principles in JAX — a normalizing flow with coupling layers and a DDPM diffusion model — deriving the ELBO and Gaussian-KL objectives via variational inference.
- [CS 689] [Research] Derived convergence guarantees for gradient descent and SGD on PSD/PD objectives and analyzed estimator asymptotics (parameter and risk error) with empirical verification across sample sizes.
- [CS 689] [Research] [needs verification] Trained self-attention / transformer language models on Penn Treebank and analyzed scaling behavior (test log-likelihood vs. training FLOPs) over context length, hidden dimension, and attention-head count. (HW6 — confirm submission before use.)

### KG2RAG-Enhanced
- [KG2RAG] [Research] Led the multi-view seed retrieval in a team KG-guided RAG pipeline on HotpotQA (query-side decomposition, per-view retrieval, RRF fusion + cross-encoder reranking + MMR), lifting supporting-fact recall **+2.68%** (54.53 to 57.21) over the KG²RAG baseline on a 4,905-question evaluation with 95% binomial CIs.

### ngvi-curvature-variance (CS 651, team project, all bullets team-framed)
- [ngvi] [Research] [MLE] Built a PyTorch black-box variational-inference testbed comparing Adam, closed-form natural-gradient (NGVI), and EMA Diagonal-Fisher optimizers across mean-field and low-rank-plus-diagonal Gaussian families on Neal's Funnel and the Eight Schools model.
- [ngvi] [Research] Showed NGVI's ELBO gain over Adam grows with posterior ill-conditioning (κ from 180 to 2566 maps to +0.28 to +2.32 nats) and that closed-form NGVI beats an EMA Diagonal-Fisher method in wall-clock on every scenario despite O(D^3) Fisher-inversion cost.
- [ngvi] [Research] Instrumented ELBO, Hessian condition number, and gradient variance jointly to separate curvature from Monte-Carlo-noise bottlenecks, showing antithetic sampling cut gradient variance ~10x yet could not rescue Adam from ill-conditioned plateaus.

### AutoEval
- [AutoEval] [Research] Designed an evaluation-improvement agent with a holdout-heavy fitness objective and anti-Goodharting guardrails (schema checks, duplicate rejection, read-only holdout protection) for reproducible retrieval evaluation.

### Refusal Decay (strongest for alignment / interpretability / safety / applied-science roles; graded full marks, COMPSCI 602)
- [refusal-decay] [Research] Ran a mechanistic-interpretability study (final project, COMPSCI 602 at UMass Amherst, graded full marks) of how prefilling attacks weaken refusal in Llama-3.1-8B-Instruct, extracting the residual-stream "refusal direction" via difference-in-means on a held-out prompt set (AdvBench harmful + Alpaca benign).
- [refusal-decay] [Research] Found the late-layer refusal-direction signal shifts negative under attack with a monotone-by-depth gradient and predicts per-prompt refusal vs. compliance, as behavioral refusal dropped from 0.92 to 0.32 at prefill length k=3.
- [refusal-decay] [Research] Designed two causal interventions (cross-condition activation patching and additive direction injection via PyTorch forward hooks) with multi-seed random/orthogonal controls and a benign positive control; reported a clean null (0/300 prompts recovered at late layers) with bootstrap 95% CIs and McNemar's test, showing the signal is a readout rather than the causal lever at the tested sites.
- [refusal-decay] [Research] Validated heuristic refusal labels with an independent secondary-classifier spot-check (87.5% agreement) and documented internal/external threats to validity across a structured multi-report research arc.

### Publication
- [Publication] *"Alzheimer's Disease Classification using Transfer Learning,"* IEEE CONIT 2023 — applied deep transfer learning on neuroimaging data for medical image classification.

---

## Project Bullets (Sonare and others)

### Sonare
- [Sonare] [Edge ML] [Backend] Built a cross-platform desktop application integrating camera, microphone, UI, and backend services into an on-device pipeline using MediaPipe hand tracking, gesture classification, whisper.cpp ASR, and local TTS — designed and shipped under hackathon time pressure at the Qualcomm Edge AI Hackathon 2025.
- [Sonare] [Backend] Engineered a FastAPI backend and Electron/React frontend to run fully offline with no external network dependencies; designed async APIs and queues to keep the UI responsive while handling local video and audio streams.

### Spark ETL
- [Spark] [Performance] [Data] Cut end-to-end Spark ETL runtime **~25%** (17 to 19 min down to 14.3 min) on a **~1.4B-row** NYC TLC dataset via broadcast joins, AQE, skew-join handling, shuffle-partition tuning, schema-aware reads, and year/month partitioning with Snappy compression; profiled stage timings via Spark UI.
- [Spark] [Performance] [Data] Optimized a Spark ETL pipeline on the NYC TLC taxi dataset by tuning broadcast joins, caching, partitioning, and adaptive Spark settings; profiled stage-level timings via Spark UI to localize shuffle and skew bottlenecks.

### Underdogs Fitness (solo freelance, production)
- [Underdogs] [Full-Stack] [SDE] Built and deployed **Underdogs Fitness** (https://www.underdogsfitness.in/), a production gym management platform on the MERN stack (MongoDB Atlas, Express, React + Redux, Node.js) solo end-to-end in ~1.5 months — auth, membership management, attendance tracking, **Stripe + manual-cash hybrid payments with a partial-payment ledger**, and cron-based renewal automation; live in production 3+ years.
- [Underdogs] [Full-Stack] [SDE] Designed for multi-branch from day 1 (every entity scoped by `branchId`, JWT-claim-based auth, frontend branch context provider); when the client expanded to a 2nd branch a year later, onboarded it as a configuration change with **zero schema migration**.
- [Underdogs] [DevOps] Set up **git-webhook auto-deploy** (GitHub webhook → DigitalOcean droplet on push) with Vercel for the frontend and Firebase Storage for media; moved **90%+** of payments through the portal and cut the client's manual workload **~70%** via cron-driven automation.

---

## Skills / Tools Phrases

- "Languages: Python, JavaScript, TypeScript, Java, C++, SQL, Bash."
- "Backend: Node.js, Express, FastAPI, REST APIs, async services, integration testing."
- "ML / AI: PyTorch, JAX, Hugging Face Transformers, sentence-transformers, RAG, LLM agents."
- "Retrieval / Search: RRF, cross-encoder reranking, MMR, knapsack token budgeting, Brave Search, scraping, provenance."
- "Systems / Performance: Linux profiling, Spark / PySpark, Spark UI, distributed data processing."
- "Cloud / DevOps: Docker, Git, GitHub Actions, CI/CD, AWS (KMS, SQS), DigitalOcean, Vercel, Firebase Storage, Cloudflare Workers (personal project)."
- "Databases: MongoDB (Atlas), PostgreSQL, Redis, SQLite."
- "AI-assisted dev: Claude / Claude Code, GitHub Copilot, Cursor, ChatGPT / OpenAI Codex."
- "Testing / QA: pytest, integration testing, LambdaTest (cross-browser)."

---

## Extracurriculars (paste-ready)

- Selected for **GirlScript Summer of Code (GSSoC) 2023**; contributed to multiple open-source projects (Linkfree, Freehit, ProjectsHut).
- Tutored **30+ underprivileged students** in programming at Sayur, a non-profit in South Tamil Nadu.
