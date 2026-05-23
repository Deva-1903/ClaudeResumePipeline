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

## Backend

- Node.js, Express — Strong (Wysa, Cario, freelance).
- FastAPI — Strong (AgenticSearch, Sonare).
- Fastify — Working knowledge (Cario).
- REST APIs — Strong.
- Async services / queues — Strong (Sonare local pipeline; AgenticSearch service).
- API design, authentication, rate limiting, audit logging — Strong (Wysa eTriage hardening).
- Multi-tenant architecture — Strong (Wysa eTriage).
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
- PEFT (LoRA / QLoRA), TRL, vLLM, Weights & Biases — Exposure (listed on older resumes; not deeply used).

## LLM / Agentic Systems

- LLM-driven extraction and verification pipelines — Strong (AgenticSearch).
- Provider routing/fallback across LLM backends — Strong (AgenticSearch).
- LLM evaluation / anti-Goodharting design — Working knowledge (AutoEval).
- Prompt iteration and response-quality heuristics — Working knowledge (Cario chat product).
- OpenAI APIs — Strong (AgenticSearch).
- Groq APIs — Working knowledge (AgenticSearch).
- Ollama — Working knowledge (KG2RAG inference pipeline).
- MCP (Model Context Protocol) — Exposure (listed; not surfaced in projects).

## Retrieval / Search

- Multi-view retrieval, sub-question decomposition — Working knowledge (KG2RAG).
- Reciprocal Rank Fusion (RRF), cross-encoder reranking, MMR — Working knowledge (KG2RAG).
- 0–1 knapsack token-budget evidence selection — Working knowledge (KG2RAG).
- Brave Search API integration, web scraping — Working knowledge (AgenticSearch).
- Cell-level provenance and trust UIs — Working knowledge (AgenticSearch).
- FAISS — Exposure.
- llama-index, spaCy — Working knowledge (KG2RAG).

## Systems / Performance

- Spark / PySpark ETL optimization (broadcast joins, partitioning, caching, column pruning) — Working knowledge (NYC TLC project).
- Spark UI, stage-level timing analysis — Working knowledge.
- Linux profiling and reproducible benchmarking — Working knowledge (CS 690PF coursework).
- Performance methodology (memory hierarchy, cache awareness, vectorization concepts) — Working knowledge (CS 690PF coursework — not surfaced as a project).
- Distributed systems concepts — Working knowledge (coursework + Spark project).

## Cloud / DevOps

- Docker — Working knowledge.
- Git, GitHub Actions — Strong.
- CI/CD — Working knowledge.
- Cloudflare Workers / Workers AI / Durable Objects / D1 — Working knowledge (cf ai research scout personal project — do not claim production use).
- AWS, GCP, Azure — resume-safe to list plain in the Skills row Cloud / DevOps category (always-on per `07_resume_style_rules.md`); no deep production ownership. Confirmed by user 2026-05-09. Bullets must not claim production cloud work.
- Kubernetes — Exposure.
- DigitalOcean App Platform — Exposure.

## Databases

- MongoDB — Strong (Wysa).
- PostgreSQL — Strong (Cario).
- Redis — Working knowledge.
- SQLite — Working knowledge (AgenticSearch).
- Databricks — Working knowledge (Spark ETL project).
- MySQL — Exposure.

## Tools

- Claude / Claude Code, GitHub Copilot, Cursor, ChatGPT / OpenAI Codex — daily AI-assisted development across UMass coursework and projects (surface when a JD calls out AI-assisted dev tooling).
- pytest / integration testing — Strong (Wysa, AgenticSearch 150+ tests).
- GTest, CMake — Exposure (autograd engine work — not currently resume-eligible).
- Linux `perf`, OpenMP, AVX intrinsics — Working knowledge (CS 690PF coursework reference only; private repos).

## Coursework-Relevant Skills

- CS 689 Advanced Machine Learning (Prof. Justin Domke, Fall 2025) — from-scratch reverse-mode autodiff, optimization & convergence theory, deep nets on CIFAR-10, generative models (flows & DDPM), transformer language modeling.
- CS 685 Advanced Natural Language Processing — retrieval, RAG, evaluation.
- CS 651 Optimization in Computer Science.
- CS 532 Systems for Data Science — distributed data systems concepts.
- CS 690PF Performance Engineering — profiling, cache-aware design, vectorization, multithreading, causal profiling, allocator design.

## Domain Knowledge

- Multi-tenant SaaS architecture (NHS / clinical context).
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
