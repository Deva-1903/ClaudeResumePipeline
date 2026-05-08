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
- Stack: Node.js, Express, MongoDB, React, REST APIs, integration tests.
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
- Stack: Node.js, Fastify, PostgreSQL, TypeScript.

Verified facts:
- Designed and implemented 20+ RESTful APIs in Node.js + Fastify backed by PostgreSQL with input validation, clear contracts, and backward-compatible changes used in production by the frontend team.
- Migrated core codebase from JavaScript to TypeScript across multiple repositories.
- Integrated LLM-powered context-aware replies into a chat product (prompt iteration, response-quality heuristics).

## Open Source / Freelance Work

- Dates: July 2022 – August 2023.
- Remote.

Verified facts:
- Built a gym management platform on the MERN stack with Stripe payments and cron-based email automation; 90%+ of payments moved through the portal; 70% reduction in client manual workload.
- Selected for GirlScript Summer of Code (GSSoC) 2023.
- Contributed features to open-source projects including Linkfree, Freehit, and ProjectsHut.

## AgenticSearch (Provenance-First Entity Discovery)

- Repo: https://github.com/Deva-1903/ciir_agentic_search
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
- Stack: JAX, PyTorch, NumPy.

Verified facts:
- Implemented RealNVP normalizing flows from scratch in JAX (custom forward/reverse processes, training loops, likelihood + sample-quality diagnostics).
- Implemented DDPM diffusion models from scratch in JAX.
- Built and benchmarked 8 deep architectures (CNN / ResNet variants, regularized models) on CIFAR-10 with custom optimizers.
- Implemented reverse-mode automatic differentiation over matrix-valued operations from scratch.

## KG2RAG-Enhanced (Multi-Hop QA on HotpotQA)

- Repo: https://github.com/Deva-1903/KG2RAG-685-NLP
- Affiliation: UMass Amherst CS 685 Advanced NLP.
- Stack: Python, Ollama, sentence-transformers, llama-index, spaCy, PyTorch.

Verified facts:
- Extended KG2RAG with multi-view seed retrieval: sub-question generation, per-view passage retrieval, fusion via Reciprocal Rank Fusion (RRF), cross-encoder reranking, and Maximal Marginal Relevance (MMR).
- Replaced heuristic top-M selection with a 0–1 knapsack token-budget evidence selection (value = relevance × coverage).
- Ran 100–500-question batch experiments with token and latency logging using an Ollama + LLaMA-3 inference pipeline.

## Spark ETL Performance Optimization

- Repo: https://github.com/Deva-1903/Spark-ETL-Optimization
- Stack: Apache Spark / PySpark, Databricks, SQL, Python.

Verified facts:
- Optimized a Spark ETL pipeline on the NYC TLC taxi dataset using broadcast-join tuning, caching, partitioning, adaptive Spark settings, column pruning, and precomputed fields.
- Used Spark UI metrics and stage-level timings to compare naive vs. optimized runs and document a repeatable optimization workflow.
- Reduced shuffle volume and wall-clock runtime; lowered cluster resource usage (qualitative — no specific percentage verified).

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
- Affiliation: UMass empirical CS project (informal/independent — confirm before listing as coursework).

Verified facts (per existing context files):
- Studies refusal behavior in safety-aligned LLMs under prefilling attacks.
- Uses Llama-3.1-8B-Instruct and Llama-3.2-3B-Instruct.
- Uses AdvBench harmful prompts and Alpaca benign prompts.
- Worked with refusal direction analysis, prefilling, tracing, and patching/intervention experiments.

Status: not yet on a public resume. Surface only when a JD warrants it (alignment / interpretability / safety roles) and only with conservative phrasing.

## Publication

- Title: "Alzheimer's Disease Classification using Transfer Learning."
- Venue: IEEE CONIT 2023 (3rd International Conference on Intelligent Technologies).
- Repo: https://github.com/Deva-1903/Alzheimer-s-Disease-Classification-
- First-author capstone work; deep transfer learning on neuroimaging data.

## Other Projects (resume-eligible repos)

- ngvi-curvature-variance — ML/optimization research. Repo: https://github.com/Deva-1903/ngvi-curvature-variance. **Bullets need verification before resume use.**
- autoresearch-karpathy — auto-research agent workflow experiment. Repo: https://github.com/Deva-1903/autoresearch-karpathy. **Bullets need verification before resume use.**

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
- refusal-decay quantitative findings (refusal-recovery curves, attack success rates) — not yet documented in a publishable form.

If a JD asks for any of these and they are not verified here, either omit the claim or use adjacent truthful experience.
