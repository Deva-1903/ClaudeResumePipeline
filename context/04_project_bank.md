# Project Bank

> Structured project facts. Pull from here only when the bullet bank or factbase is not enough.

---

## AgenticSearch — Provenance-First Entity Discovery

### What it is
Multi-stage agentic web-discovery service that turns open-ended topic queries into structured entity tables with cell-level provenance.

### Verified technologies
Python, FastAPI, Brave Search API, OpenAI, Groq, SQLite.

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
- Not deployed to production users.
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
From-scratch implementation of generative models and benchmarking of deep architectures on CIFAR-10 in JAX/PyTorch.

### Verified technologies
JAX, PyTorch, NumPy.

### Strong resume angles
- Applied Scientist / Research
- ML Engineer (modeling rigor)

### Verified implementation details
- RealNVP normalizing flows from scratch in JAX.
- DDPM diffusion models from scratch in JAX (custom forward/reverse processes, training loops, likelihood + sample-quality diagnostics).
- 8 deep architectures (CNN / ResNet variants, regularized models) benchmarked on CIFAR-10 with custom optimizers.
- Reverse-mode automatic differentiation over matrix-valued operations from scratch.

### Possible resume bullets
- Implemented RealNVP normalizing flows and DDPM diffusion models from scratch in JAX, including custom forward/reverse processes, training loops, and likelihood + sample-quality diagnostics on image benchmarks.
- Built and benchmarked 8 deep architectures (CNN / ResNet variants, regularized models) on CIFAR-10 with custom optimizers, isolating the effect of regularization and depth on generalization.
- Implemented reverse-mode automatic differentiation over matrix-valued operations from scratch to validate gradient correctness against framework autodiff.

### Do not claim
- No specific FID / NLL / accuracy numbers.

---

## KG2RAG-Enhanced — Multi-Hop QA on HotpotQA (CS 685)

### What it is
Multi-view retrieval extension to KG2RAG with token-budgeted evidence selection.

### Verified technologies
Python, Ollama, sentence-transformers, llama-index, spaCy, PyTorch.

### Strong resume angles
- Applied Scientist (retrieval research)
- AI Engineer (RAG sophistication)
- ML Engineer

### Verified implementation details
- Sub-question generation; per-view passage retrieval; fusion via Reciprocal Rank Fusion (RRF), cross-encoder reranking, and Maximal Marginal Relevance (MMR).
- 0–1 knapsack token-budget evidence selection (value = relevance × coverage).
- Ollama + LLaMA-3 inference pipeline; 100–500-question batch experiments with token and latency logging.

### Possible resume bullets
- Extended KG2RAG with multi-view seed retrieval on HotpotQA: generated sub-questions, retrieved passages per view, and fused results via Reciprocal Rank Fusion (RRF), cross-encoder reranking, and MMR.
- Replaced heuristic top-M selection with a 0–1 knapsack token-budget formulation (value = relevance × coverage); integrated it into an Ollama + LLaMA-3 pipeline and ran 100–500-question batch experiments with token and latency logging.
- Built the multi-view retrieval component of a team KG-guided RAG pipeline, decomposing complex questions into single-hop sub-questions and fusing per-view retrieval to improve evidence coverage.

### Do not claim
- No specific accuracy delta vs the KG2RAG baseline.

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
Optimization of a naive Spark ETL pipeline on the NYC TLC taxi dataset using Databricks.

### Verified technologies
Apache Spark / PySpark, Databricks, SQL, Python.

### Strong resume angles
- SRE / Systems / data platform
- ML Engineer (data engineering side)
- SDE / Backend (data platform context)

### Verified implementation details
- Broadcast-join tuning, caching, partitioning, adaptive Spark settings, column pruning, precomputed fields.
- Spark UI metrics and stage-level timings to compare naive vs optimized runs.
- Documented a repeatable optimization workflow.

### Possible resume bullets
- Optimized a naive Spark ETL pipeline on the NYC TLC taxi dataset by tuning broadcast joins, caching, partitioning, and adaptive Spark settings to reduce shuffle volume and wall-clock runtime.
- Profiled stage-level timings via Spark UI to localize shuffle and skew bottlenecks; iteratively applied column pruning and precomputed fields to cut unnecessary data movement.
- Documented a repeatable optimization workflow over the same dataset to compare naive vs tuned runs and to make Spark configuration trade-offs reviewable.

### Do not claim
- No specific runtime / latency / cluster-cost reduction percentages.

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
Backend Engineer role on Wysa's UK Clinical team, building multi-tenant NHS eTriage systems and a full-stack ML annotation platform.

### Verified technologies
Node.js, Express, MongoDB, React, REST APIs, integration tests.

### Strong resume angles
- SDE / Backend (multi-tenant production work)
- SRE / Systems (reliability, security, on-call mindset)
- ML Engineer / AI Engineer (annotation platform fed downstream NLP/clinical models)

### Verified implementation details
- 8+ UK clinical clients; 10,000+ monthly triage submissions; $340K+ in revenue (per resume language).
- 20+ VAPT findings remediated; authentication and rate limiting hardened; integration tests added for regression protection.
- Integrated with Mayden's iaptus platform via REST APIs and aggregation queries.
- Architected a full-stack ML training-data annotation platform replacing spreadsheet-based labeling.
- Reduced manual annotation work by 100+ hours/month; improved labeling throughput by 60%.
- Primary technical POC for the eTriage backend; ran knowledge transfer for new developers.

### Possible resume bullets
- Engineered multi-tenant NHS eTriage backend (Node.js, MongoDB) for 8+ UK clients, processing 10,000+ monthly triage submissions and integrated with Mayden's iaptus platform via REST APIs; contributed to $340K+ in revenue.
- Owned backend security and reliability across the eTriage stack: monitored production logs during feature releases and client integrations, shipped tenant-specific incident fixes, hardened authentication and rate limiting, and remediated 20+ VAPT findings.
- Architected a full-stack ML training-data annotation platform (React, Node.js, MongoDB) used daily by the AI team; replaced spreadsheet workflows with secure role-based REST APIs, cutting manual operations by 100+ hours/month and improving labeling throughput by 60%.
- Acted as primary technical POC for the eTriage backend; designed and shipped auth, rate limiting, and audit logging features and ran knowledge transfer for new developers on the UK Clinical team.

### Do not claim
- Specific clinical interop standards (HL7/FHIR) — not confirmed.
- People-management or staff-level leadership.
- Cloud infrastructure ownership.

---

## Cario Backend Internship (production)

### What it is
Backend Developer Internship at Cario Growth Services — Node.js/Fastify APIs over PostgreSQL plus an LLM-powered chat integration.

### Verified technologies
Node.js, Fastify, PostgreSQL, TypeScript.

### Strong resume angles
- SDE / Backend (API design)
- AI Engineer (LLM-powered chat integration as a small but real production data point)

### Verified implementation details
- 20+ RESTful APIs in Node.js + Fastify backed by PostgreSQL; input validation, clear contracts, backward-compatible changes used by the frontend team.
- Migrated core codebase from JavaScript to TypeScript across multiple repositories.
- Integrated LLMs into a chat product to generate context-aware replies from conversation history and user input; iterated on prompt design and response-quality heuristics.

### Possible resume bullets
- Designed and implemented 20+ RESTful APIs in Node.js + Fastify backed by PostgreSQL with input validation, clear contracts, and backward-compatible changes used in production by the frontend team.
- Migrated core codebase from JavaScript to TypeScript across multiple repositories, improving type safety and long-term maintainability.
- Integrated LLM-powered context-aware replies into a chat product, iterating on prompt design, evaluation, and response-quality heuristics for a real customer-facing experience.

### Do not claim
- No metrics on prompt-quality improvements, latency, or coverage.

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

## Refusal Decay (LLM Safety / Interpretability) — surface only when JD warrants it

### What it is
Empirical study of refusal-direction behavior in safety-aligned LLMs under prefilling attacks.

### Verified technologies
Python, PyTorch, Hugging Face Transformers (per existing context); Llama-3.1-8B-Instruct, Llama-3.2-3B-Instruct; AdvBench; Alpaca.

### Strong resume angles
- Applied Scientist / Research (alignment, interpretability, safety)

### Verified implementation details
- Prefilling attack experiments; refusal-direction analysis; tracing; patching/intervention experiments.

### Possible resume bullets (use sparingly; phrase conservatively)
- Investigated positional decay of refusal-direction signals in safety-aligned LLMs (Llama-3.1-8B-Instruct, Llama-3.2-3B-Instruct) under prefilling attacks using AdvBench and Alpaca prompts.
- Built experiment scripts for generation, tracing, and intervention analysis to study how refusal behavior changes across layers and prefilling lengths.

### Do not claim
- No quantitative findings (refusal-recovery curves, attack success rates, etc.) until documented.
- No claim of formal coursework affiliation unless confirmed.
