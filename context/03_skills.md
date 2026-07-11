# Skills

> Strength labels:
> - **Strong** — used in production work, in a graded course project, or in a public personal project with real code.
> - **Working knowledge** — used in coursework or in a project but not deeply.
> - **Basics** — surface-level familiarity, resume-safe to list as "basics" when JD-relevant; no production ownership claim.
> - **Exposure** — listed on prior resumes but not deeply applied; safe to mention only when JD-relevant.

If a JD asks for a skill not on this list, either omit it or surface adjacent skills truthfully.

## Languages

- Python — Strong (AgenticSearch, AutoEval, KG2RAG, CS 689, CS 685, Spark ETL).
- JavaScript — Strong (Wysa, Cario, freelance MERN).
- TypeScript — Strong (Wysa, Cario JS→TS migration, cf ai research scout).
- C++ — Working knowledge (CS 690PF performance work — coursework reference only; not surfaced as a standalone project).
- SQL — Working knowledge (PostgreSQL, MongoDB aggregation, SQLite).
- Java — Exposure (listed on older resumes; coursework-level; also Teenofes internship — JSP/Servlet, LinkedIn-sourced, surface only for Java/legacy-stack JDs).
- Go — Exposure (listed on older resumes; not verified in production).
- Bash — Working knowledge.
- HTML/CSS — Exposure.
- Tailwind CSS — Working knowledge (personal and freelance projects; user-confirmed 2026-06-08).

## Backend

- Node.js, Express — Strong (Wysa, Cario, freelance).
- React — Strong (Wysa annotation platform, Underdogs MERN, Sonare).
- **Next.js — Strong** (six public personal projects with real code: SpotiPlay, weekflow, AutoReferral, umass-meal-planner (web), TasteGraph, Habit-Tracker; Next.js 14–16; user-confirmed 2026-07-03). **Always list Next.js in the Skills row (user directive 2026-07-03).**
- FastAPI — Strong (AgenticSearch, Sonare).
- Fastify — Working knowledge (Cario).
- REST APIs — Strong.
- Async services / queues — Strong (Sonare local pipeline; AgenticSearch service).
- API design, authentication, rate limiting, audit logging — Strong (Wysa eTriage hardening).
- Multi-tenant architecture — Strong (Wysa eTriage).
- **SMART on FHIR (OAuth2/PKCE launch, callback, token flow)** — Working knowledge (TherAlign, current role — in progress).
- **FHIR R4 (Patient / Medication / Observation resources)** — Working knowledge (TherAlign, current role — in progress).
- **CDS Hooks** — Basics (TherAlign, current role — target composer/sidecar integration; learning).
- GraphQL — Exposure.
- Sails.js — Exposure (Wysa-era skill tag, LinkedIn-sourced; depth unverified, list only when JD-relevant).
- Sequelize (ORM) — Exposure (Cario, used with PostgreSQL for migration/CRUD; LinkedIn-sourced).
- Redux — Exposure (freelance MERN / gym platform; LinkedIn-sourced).
- Flutter — Exposure (Teenofes internship frontend widgets; LinkedIn-sourced).

## ML / AI

- PyTorch — Strong (CS 689, Alzheimer's classification, refusal-decay project).
- JAX — Working knowledge (CS 689 — coupling-layer normalizing flow and DDPM from scratch; used as the reference to validate the from-scratch NumPy autodiff engine).
- Hugging Face Transformers — Working knowledge (CS 685, refusal-decay).
- sentence-transformers — Working knowledge (KG2RAG).
- TensorFlow — Exposure (older projects).
- NumPy — Strong (CS 689 HW3: built a matrix-based reverse-mode autodiff engine from scratch).
- pandas, scikit-learn — Working knowledge.
- Automatic differentiation / reverse-mode backprop — Strong (CS 689 HW3: computation graph, topological-sort backprop, operators incl. matmul/solve/logdet/logsumexp; validated against JAX).
- Optimization — gradient descent / SGD convergence analysis, learning-rate tuning, SGD vs. Adam — Working knowledge (CS 689 HW4).
- Variational inference, natural-gradient methods (NGVI), Fisher information, reparameterization trick, antithetic variance reduction — Working knowledge (CS 651 ngvi-curvature-variance; team project).
- PEFT (LoRA / QLoRA), TRL, vLLM, Weights & Biases — Exposure (listed on older resumes; not deeply used).

## LLM / Agentic Systems

- LLM-driven extraction and verification pipelines — Strong (AgenticSearch).
- Provider routing/fallback across LLM backends — Strong (AgenticSearch).
- LLM evaluation / anti-Goodharting design — Working knowledge (AutoEval).
- Prompt iteration and response-quality heuristics — Working knowledge (Cario chat product).
- OpenAI APIs — Strong (AgenticSearch).
- Groq APIs — Working knowledge (AgenticSearch).
- **Google Gemini API (structured output)** — Working knowledge (TherAlign, current role — constrained to synthesis with deterministic backend control + provenance).
- Ollama — Working knowledge (KG2RAG inference pipeline).
- MCP (Model Context Protocol) — Exposure (listed; not surfaced in projects).

## Retrieval / Search

- Multi-view retrieval, sub-question decomposition — Working knowledge (KG2RAG).
- Reciprocal Rank Fusion (RRF), cross-encoder reranking, MMR — Working knowledge (KG2RAG).
- 0–1 knapsack token-budget evidence selection — Working knowledge (KG2RAG).
- Brave Search API integration, web scraping — Working knowledge (AgenticSearch).
- Cell-level provenance and trust UIs — Working knowledge (AgenticSearch; also TherAlign transparency pane — current role).
- **RxNorm drug normalization; PubMed / clinical-guideline (AHA/ACC) evidence retrieval** — Working knowledge (TherAlign, current role).
- FAISS — Exposure.
- llama-index, spaCy, networkx (knowledge-graph construction) — Working knowledge (KG2RAG).

## Systems / Performance

- Spark / PySpark ETL optimization (broadcast joins, AQE, shuffle-partition tuning, skew-join handling, partitioning, column pruning) — Working knowledge (NYC TLC project, ~1.4B rows; ~25% ETL runtime cut, tail-latency 2.14x to 1.74x).
- Spark UI, stage-level timing analysis — Working knowledge.
- Linux profiling and reproducible benchmarking — Working knowledge (CS 690PF coursework).
- Performance methodology (memory hierarchy, cache-aware tiling/blocking, SIMD vectorization, register-aware micro-kernels, OpenMP multithreading, `perf`/`perf c2c`/Cachegrind/TMA profiling, causal profiling, allocator false-sharing, measurement bias) — Working knowledge (CS 690PF coursework; hands-on C++ matmul optimization pipeline + Coz/Hoard/Mytkowicz reproduction). **Public repo `https://github.com/Deva-1903/cs690pf` (as of 2026-07-02) — now resume-eligible as a standalone project, strongest systems-C++ signal.**
- Low-level / systems C++ (AVX SIMD via `__m256` intrinsics, cache blocking, OpenMP, assembly/register inspection) — Working knowledge (CS 690PF matmul optimization; also llama.cpp quantized-inference work at Cario).
- Distributed systems concepts — Working knowledge (coursework + Spark project).

## Cloud / DevOps

- Docker — Working knowledge.
- Git, GitHub Actions — Strong.
- CI/CD — Working knowledge.
- **Git webhook auto-deploy** — Working knowledge (Underdogs Fitness: GitHub webhook → DigitalOcean droplet on push).
- Cloudflare Workers / Workers AI / Durable Objects / D1 — Working knowledge (cf ai research scout personal project — do not claim production use).
- AWS — Working knowledge for SDKs and managed services (**AWS KMS** used in production at Wysa for at-rest PII / clinical-data encryption; SQS for delayed messaging; resume-safe to list plain in Skills, but production ownership claim limited to KMS use).
- **AWS KMS** — Working knowledge / Strong (Wysa production — envelope-encryption pattern for PII/clinical data; 90-day data-retention policy).
- **AWS S3** — Working knowledge (Wysa production — asset/file storage, including multi-region S3 *buckets*; user-confirmed 2026-06-08). NOTE: this is multi-region bucket usage, NOT a multi-region app deployment — do not claim multi-region architecture/replication/region-aware routing.
- GCP, Azure — resume-safe to list plain in the Skills row Cloud / DevOps category (always-on per `07_resume_style_rules.md`); no deep production ownership. Confirmed by user 2026-05-09.
- **DigitalOcean droplet** — Working knowledge (Underdogs Fitness backend host).
- **Vercel** — Working knowledge (Underdogs Fitness frontend host).
- **Firebase Storage** — Working knowledge (Underdogs Fitness image storage).
- **Firebase Cloud Functions** — Working knowledge (TherAlign, current role — serverless backend for the medication-alternatives API).
- **Google Cloud Run** — Working knowledge (TherAlign, current role — mock FHIR service container).
- **MongoDB Atlas** — Working knowledge (Underdogs Fitness DB host).
- **Kubernetes** — Working knowledge (personal/side projects; user-confirmed 2026-06-10, project-level not production). Resume-safe to list plainly.
- **Apache Kafka** — Working knowledge (personal/side projects; user-confirmed 2026-06-10, project-level). Resume-safe to list plainly; do not claim production-scale streaming.
- **DynamoDB** — Working knowledge (personal/side projects; user-confirmed 2026-06-10, project-level). Resume-safe to list plainly.
- **Hadoop / MapReduce** — Working knowledge (user-confirmed 2026-06-11; understands the model and has touched it, no substantial project). Resume-safe to list plainly in a data/distributed Skills category; do not claim a production Hadoop job or a specific cluster-scale result.
- **Load balancing** — Working knowledge (user-confirmed 2026-06-11; understands the patterns and has worked near it, did not own the LB config). Resume-safe to list plainly as a distributed-systems concept/skill; do not claim having configured/operated a production load balancer.

## Databases

- MongoDB — Strong (Wysa).
- PostgreSQL — Strong (Cario).
- Redis — Working knowledge.
- SQLite — Working knowledge (AgenticSearch).
- Databricks — Exposure only (listed on older resumes; the Spark ETL repo runs local spark-submit, NOT Databricks — do not claim Databricks for that project).
- MySQL — Exposure.

## Tools

- Claude / Claude Code, GitHub Copilot, Cursor, ChatGPT / OpenAI Codex — daily AI-assisted development across UMass coursework and projects. **GitHub Copilot** specifically: used in a measured Wysa productivity pilot for tech-debt PRs, code migration, and security-finding triage; maintained `.github/copilot-instructions.md` conventions file to keep AI-generated code aligned with codebase patterns.
- pytest / integration testing — Strong (Wysa, AgenticSearch 150+ tests).
- **LambdaTest** — Working knowledge (Wysa cross-browser / cross-device testing).
- **Agile / Scrum** — Strong (Wysa: sprint planning, daily stand-ups, retrospectives across 2 years).
- **llama.cpp** — Working knowledge (Cario chip auto-commenting: 4-bit quantized Llama-7B inference on a single VM).
- GTest, CMake — Exposure (autograd engine work — not currently resume-eligible).
- Linux `perf` (`perf stat`/`perf record`/`perf c2c`), OpenMP, AVX/SIMD intrinsics (`__m256`), Cachegrind, TMA, `lmbench`, building tools from source without root (jemalloc/mimalloc/Hoard) — Working knowledge (CS 690PF coursework; public repo `github.com/Deva-1903/cs690pf`, resume-eligible).

## Coursework-Relevant Skills

- CS 689 Advanced Machine Learning (Prof. Justin Domke, Fall 2025) — from-scratch reverse-mode autodiff, optimization & convergence theory, deep nets on CIFAR-10, generative models (flows & DDPM), transformer language modeling.
- CS 685 Advanced Natural Language Processing — retrieval, RAG, evaluation.
- CS 651 Optimization in Computer Science.
- CS 532 Systems for Data Science — distributed data systems concepts.
- CS 690PF Performance Engineering — profiling, cache-aware design, vectorization, multithreading, causal profiling, allocator design.

## Domain Knowledge

- Multi-tenant SaaS architecture (NHS / clinical context).
- **Healthtech / clinical decision support (CDS), prior-authorization prevention, Real-Time Prescription Benefit (RTPB), formulary/coverage, EHR interoperability (Epic / SMART on FHIR)** — TherAlign, current role.
- Mental-health and clinical NLP (Wysa product domain).
- Information Retrieval / RAG / multi-hop QA.
- Edge / on-device ML (Sonare).
- Generative models — normalizing flows (coupling layers), DDPM diffusion, variational inference / ELBO (CS 689).
- Transformers / self-attention and neural language modeling (CS 689 — confirm HW6 submission).
- Statistical learning theory — estimator asymptotics, convergence analysis (CS 689).
- Medical imaging / transfer learning (Alzheimer's classification).

## Soft Skills (resume-safe)

- Cross-functional collaboration with clinical and product teams (Wysa).
- Production debugging and on-call mindset (Wysa).
- Knowledge transfer / mentoring (Wysa KT, Sayur tutoring).
- Technical writing (IEEE publication).
