# Role Targeting

> Tells future Claude sessions how to choose a base resume and which evidence to lead with for each role family.

---

## SDE / Backend

Base resume: `base_resumes/sde_backend.tex`

Prioritize:
- Wysa eTriage backend (multi-tenant scale + integration story).
- Wysa annotation platform (full-stack delivery + measurable internal impact).
- Cario REST APIs and JS→TS migration.
- AgenticSearch backend (FastAPI service with tests and instrumentation).
- Sonare backend (FastAPI + async + offline).
- Spark ETL when JD touches data systems or performance.

Avoid overemphasizing:
- Pure research bullets unless JD mentions ML/AI.
- Cloudflare-specific framing unless JD mentions edge/serverless.

Default skills order:
Languages → Backend / Web → Databases → AI/ML → Cloud / DevOps.

---

## SRE / Systems / Infrastructure / Platform

Base resume: `base_resumes/sre_systems.tex`

Prioritize:
- Wysa reliability and security framing (incidents, hardening, integration tests, VAPT).
- Spark ETL performance optimization.
- CS 690PF Performance Engineering coursework (as coursework, not as project).
- Sonare async pipeline / offline robustness.
- cf ai research scout durable workflows when JD is edge/serverless-leaning.

Avoid overemphasizing:
- Generative-model research bullets.
- Pure NLP/IR bullets unless JD mentions search infra.

Default skills order:
Languages → Systems / Performance → Backend → Cloud / DevOps → Databases.

---

## ML Engineer

Base resume: `base_resumes/ml_engineer.tex`

Prioritize:
- CS 689 generative models from scratch (JAX, RealNVP, DDPM, CIFAR-10).
- AgenticSearch (multi-stage pipeline with deterministic/LLM extraction and provenance).
- KG2RAG-Enhanced (RRF, cross-encoder reranking, MMR, knapsack).
- Wysa annotation platform (data infra for downstream ML).
- Spark ETL when JD touches data pipelines.

Avoid overemphasizing:
- Wysa eTriage scale/revenue framing — keep one bullet, not three.
- Cloudflare framing unless JD calls for edge/serverless ML.

Default skills order:
Languages → ML / AI → Retrieval / Search → Systems / Performance → Backend → Databases.

---

## AI Engineer / LLM Engineer / Agentic AI

Base resume: `base_resumes/ai_engineer.tex`

Prioritize:
- AgenticSearch (typed retrieval planning, deterministic + LLM extraction, provenance, evaluation harness).
- AutoEval (eval rigor, anti-Goodharting guardrails).
- KG2RAG-Enhanced (RAG sophistication: RRF + cross-encoder + MMR + knapsack).
- cf ai research scout (LLM systems on edge with durable workflows).
- Cario LLM-powered chat integration (real customer-facing LLM use).

Avoid overemphasizing:
- Spark ETL unless JD ties data eng to LLM systems.
- Wysa eTriage scale/revenue framing — one bullet only.

Default skills order:
Languages → LLM / Agentic Systems → Retrieval / Search → ML / AI → Backend → Cloud / DevOps.

---

## Applied Scientist / Research Engineer / Research Intern

Base resume: `base_resumes/applied_scientist.tex`

Prioritize:
- CS 689 generative models (RealNVP, DDPM from scratch in JAX).
- KG2RAG-Enhanced (research-style retrieval method).
- AutoEval (evaluation methodology).
- IEEE CONIT 2023 publication.
- refusal-decay only when alignment / safety / interpretability is the role focus.

Avoid overemphasizing:
- Wysa product/scale framing — keep it brief; lead with research and methodology.
- Cario business-flavored bullets.

Default skills order:
Languages → ML / AI → Retrieval / Search → LLM / Agentic Systems → Systems / Performance.

---

## Ambiguous Role Rules

Many JDs straddle categories. Use these heuristics:

- "Software Engineer, AI Infrastructure" → AI Engineer if pipeline/agent emphasis; SRE/Systems if reliability/scaling emphasis.
- "Backend Engineer, ML Platform" → SDE/Backend if API and platform backend dominate; ML Engineer if model lifecycle dominates.
- "Applied Scientist Intern" / "Research Intern" → Applied Scientist.
- "LLM Agent Engineer" / "GenAI Engineer" → AI Engineer.
- "Software Engineer, Search" / "Search and Ranking" → AI Engineer if LLM/agentic; ML Engineer if classical IR.
- "Performance Engineer" / "Compiler" / "Database internals" → SRE/Systems (lean on Spark and CS 690PF coursework).
- "Edge AI" / "On-device ML" → ML Engineer or AI Engineer; lean on Sonare and cf ai research scout.
- "Full-Stack Engineer" → SDE/Backend (Wysa annotation platform + Cario JS→TS).

When in doubt, pick the resume that best matches what the JD will be evaluated on, not the resume that best matches the title. The strongest verified evidence wins over keyword density.
