# Bullet Bank

> Paste-ready bullets, organized by role family. Tags in `[brackets]` indicate which projects/roles a bullet maps to. Pick the smallest set that covers the JD; tighten metrics only if they appear verbatim in `01_verified_claims.md`.

---

## SDE / Backend Bullets

### Wysa
- [Wysa] [Backend] [SDE] Engineered multi-tenant NHS eTriage backend (Node.js, MongoDB) for **8+ UK clients**, processing **10,000+ monthly triage submissions** and integrated with Mayden's iaptus platform via REST APIs and aggregation queries; contributed to **$340K+** in revenue.
- [Wysa] [Backend] [SDE] Architected a full-stack data annotation platform (React, Node.js, MongoDB) used daily by the AI team; replaced spreadsheet workflows with secure role-based REST APIs, cutting manual operations by **100+ hours/month** and improving labeling throughput by **60%**.
- [Wysa] [Backend] [Security] Owned backend security and reliability across the eTriage stack: hardened authentication and rate limiting, added integration tests, and remediated **20+ VAPT findings** to protect sensitive clinical data against regressions.
- [Wysa] [Leadership] Acted as primary technical POC for the eTriage backend; designed and shipped auth, rate limiting, and audit logging features and ran knowledge transfer for new developers on the UK Clinical team.

### Cario
- [Cario] [Backend] [SDE] Designed and implemented **20+ RESTful APIs** in Node.js + Fastify backed by PostgreSQL with input validation, clear contracts, and backward-compatible changes used in production by the frontend team.
- [Cario] [SDE] Migrated core codebase from JavaScript to TypeScript across multiple repositories, improving type safety and long-term maintainability.
- [Cario] [AI Engineer] Integrated LLM-powered context-aware replies into a chat product, iterating on prompt design and response-quality heuristics for a real customer-facing experience.

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
- [Spark] [SRE] [Performance] Optimized a Spark ETL pipeline on the NYC TLC taxi dataset with broadcast-join tuning, caching, partitioning, adaptive Spark settings, column pruning, and precomputed fields to reduce shuffle volume and wall-clock runtime.
- [Spark] [SRE] [Performance] Used Spark UI metrics and stage-level timings to localize shuffle and skew bottlenecks and to document a repeatable optimization workflow for downstream analytics jobs.

### Coursework / performance
- [CS 690PF] [Systems] Coursework in Performance Engineering covering profiling, cache-aware design, vectorization concepts, and multithreading on Linux.

### Sonare (systems angle)
- [Sonare] [Systems] Designed an offline pipeline with async queues and local-only inference (MediaPipe + whisper.cpp + local TTS), keeping the UI responsive without external network dependencies.

### cf ai research scout (edge / durable systems)
- [cf-ai-research-scout] [Systems] Designed durable workflow boundaries via WorkflowEntrypoint and Durable Objects so multi-step agent tasks survive process restarts and tool failures, with conversation state persisted in D1.

---

## ML Engineer Bullets

### CS 689 Generative Models
- [CS 689] [MLE] [Research] Implemented **RealNVP normalizing flows** and **DDPM diffusion models** from scratch in JAX, including custom forward/reverse processes, training loops, and likelihood + sample-quality diagnostics on image benchmarks.
- [CS 689] [MLE] Built and benchmarked **8 deep architectures** (CNN / ResNet variants, regularized models) on CIFAR-10 with custom optimizers; implemented reverse-mode automatic differentiation over matrix-valued operations from scratch.

### KG2RAG-Enhanced
- [KG2RAG] [MLE] [AI Eng] [IR] Extended KG2RAG with multi-view seed retrieval on HotpotQA: generated sub-questions, retrieved passages per view, and fused via Reciprocal Rank Fusion (RRF), cross-encoder reranking, and MMR.
- [KG2RAG] [MLE] [AI Eng] Replaced heuristic top-M selection with a 0–1 knapsack token-budget formulation (value = relevance × coverage); integrated it into an Ollama + LLaMA-3 pipeline and ran 100–500-question batch experiments with token and latency logging.

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
- [KG2RAG] [AI Eng] [RAG] Built the multi-view retrieval component of a KG-guided RAG pipeline for HotpotQA, decomposing complex questions into single-hop sub-questions and fusing per-view retrieval with RRF, cross-encoder reranking, and MMR.

### cf ai research scout
- [cf-ai-research-scout] [AI Eng] Built an edge-native AI research assistant on Cloudflare Workers: agent fetches web sources, generates multi-step research digests, and streams responses to the client over WebSocket in real time.
- [cf-ai-research-scout] [AI Eng] Used Workers AI for embeddings and streaming inference and prototyped end-to-end stateful agent behavior (AIChatAgent + Durable Objects + WorkflowEntrypoint + D1) without an external database.

### Cario (LLM in production)
- [Cario] [AI Eng] Integrated LLMs into a chat product to generate context-aware replies from conversation history and user input; iterated on prompt design and response-quality heuristics for a real customer-facing experience.

---

## Applied Scientist / Research Bullets

### CS 689
- [CS 689] [Research] Implemented RealNVP normalizing flows and DDPM diffusion models from scratch in JAX, including custom forward/reverse processes and likelihood + sample-quality diagnostics.
- [CS 689] [Research] Built and benchmarked 8 deep architectures on CIFAR-10 with custom optimizers; implemented reverse-mode autodiff over matrix-valued operations from scratch to validate gradient correctness against framework autodiff.

### KG2RAG-Enhanced
- [KG2RAG] [Research] Extended KG2RAG with multi-view seed retrieval and a 0–1 knapsack token-budget evidence selection on HotpotQA, fusing per-view retrieval via RRF, cross-encoder reranking, and MMR.

### AutoEval
- [AutoEval] [Research] Designed an evaluation-improvement agent with a holdout-heavy fitness objective and anti-Goodharting guardrails (schema checks, duplicate rejection, read-only holdout protection) for reproducible retrieval evaluation.

### Refusal Decay (use only when alignment/safety is the role)
- [refusal-decay] [Research] Investigated positional decay of refusal-direction signals in safety-aligned LLMs (Llama-3.1-8B-Instruct, Llama-3.2-3B-Instruct) under prefilling attacks using AdvBench and Alpaca prompts.
- [refusal-decay] [Research] Built experiment scripts for generation, tracing, and intervention analysis to study how refusal behavior changes across layers and prefilling lengths.

### Publication
- [Publication] *"Alzheimer's Disease Classification using Transfer Learning,"* IEEE CONIT 2023 — applied deep transfer learning on neuroimaging data for medical image classification.

---

## Project Bullets (Sonare and others)

### Sonare
- [Sonare] [Edge ML] [Backend] Built a cross-platform desktop application integrating camera, microphone, UI, and backend services into an on-device pipeline using MediaPipe hand tracking, gesture classification, whisper.cpp ASR, and local TTS — designed and shipped under hackathon time pressure at the Qualcomm Edge AI Hackathon 2025.
- [Sonare] [Backend] Engineered a FastAPI backend and Electron/React frontend to run fully offline with no external network dependencies; designed async APIs and queues to keep the UI responsive while handling local video and audio streams.

### Spark ETL
- [Spark] [Performance] [Data] Optimized a Spark ETL pipeline on the NYC TLC taxi dataset by tuning broadcast joins, caching, partitioning, and adaptive Spark settings; profiled stage-level timings via Spark UI to localize shuffle and skew bottlenecks.

---

## Skills / Tools Phrases

- "Languages: Python, JavaScript, TypeScript, Java, C++, SQL, Bash."
- "Backend: Node.js, Express, FastAPI, REST APIs, async services, integration testing."
- "ML / AI: PyTorch, JAX, Hugging Face Transformers, sentence-transformers, RAG, LLM agents."
- "Retrieval / Search: RRF, cross-encoder reranking, MMR, knapsack token budgeting, Brave Search, scraping, provenance."
- "Systems / Performance: Linux profiling, Spark / PySpark, Databricks, Spark UI."
- "Cloud / DevOps: Docker, Git, GitHub Actions, CI/CD, Cloudflare Workers (personal project)."
- "Databases: MongoDB, PostgreSQL, Redis, SQLite."
- "AI-assisted dev: Claude / Claude Code, GitHub Copilot, Cursor, ChatGPT / OpenAI Codex."

---

## Extracurriculars (paste-ready)

- Selected for **GirlScript Summer of Code (GSSoC) 2023**; contributed to multiple open-source projects (Linkfree, Freehit, ProjectsHut).
- Tutored **30+ underprivileged students** in programming at Sayur, a non-profit in South Tamil Nadu.
