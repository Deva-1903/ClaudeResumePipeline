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

Candidate evidence (verify first; off by default):
- Teenofes internship (Java/JSP/Servlet/Flutter) only when a JD is Java/legacy-stack heavy — see `01_verified_claims.md`.

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
- CS 689 (from-scratch reverse-mode autodiff in NumPy validated against JAX; normalizing-flow + DDPM generative models in JAX; 5 architectures on CIFAR-10 across 3 optimizers).
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
- CS 689 (from-scratch autodiff validated against JAX; normalizing-flow + DDPM generative models; GD/SGD convergence theory and estimator asymptotics).
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

## Global JD Framing Rules

For every JD, before bullet selection, extract:

1. **Role family** — SDE/Backend, SRE/Systems, ML Engineer, AI Engineer, Applied Scientist, Data Engineering, Security.
2. **Employer priority themes** — ownership, quality, ambiguity, fast-paced execution, simple solutions to complex problems, debugging / research mindset, infrastructure/platform scale, product thinking, AI-assisted development, security and reliability.
3. **Technical keywords** — APIs, distributed systems, pipelines, databases, ML models, data products, infrastructure, security, plus any company-stack keywords. Only include in the resume when the truth source supports it.
4. **Behavioral / culture signals** — constant learner, takes ownership, enjoys research, quality-focused, resilient in ambiguity, uses AI tools effectively.

Then tailor by:
- Reordering sections or bullets to emphasize the JD's priorities.
- Rewriting bullet phrasing to echo the JD's language while preserving truth.
- Reordering skills so the JD-relevant tools appear first.
- Choosing projects that match the team's likely placement.
- Cutting bullets that are strong generally but weak for this specific JD.
- Making the resume feel written for this company/role — without inserting the company name unless it is natural.

### Bullet rewriting examples (truth preserved)

If JD emphasizes "ownership":
- Generic: "Worked on backend APIs for assessment flows."
- Tailored: "Owned backend workflows for assessment and referral logic across production-facing Node.js services."

If JD emphasizes "quality":
- Generic: "Added tests and fixed bugs."
- Tailored: "Added integration tests, validation paths, and regression protection around backend workflows handling sensitive clinical data."

If JD emphasizes "simple solutions to complex problems":
- Generic: "Built agentic search system with LLM extraction."
- Tailored: "Designed a staged pipeline for open-ended entity discovery — schema planning, retrieval, extraction, deduplication, provenance — instead of a single opaque LLM call."

If JD emphasizes "research / figuring out how pieces work":
- Generic: "Optimized Spark ETL pipeline."
- Tailored: "Used Spark UI stage metrics to reason through shuffle, skew, and runtime bottlenecks, then documented repeatable fixes across naive and tuned ETL runs."

If JD emphasizes "AI tools":
- Generic: "Used AI tools."
- Tailored: "Used Claude Code, Cursor, and LLM APIs as engineering accelerators while keeping final system behavior grounded in tests, provenance, and deterministic validation."

If JD emphasizes "commerce / product / platform":
- Generic: "Built REST APIs."
- Tailored: "Built backend APIs and data workflows with clear contracts, validation, and production-facing reliability concerns suitable for product/platform teams."

## Broad SDE Internship Strategy (Shopify-like)

For broad engineering internships whose JD spans Software Engineering + Data + Applied ML + Infra + Security and emphasizes ownership, quality, ambiguity, AI agents/tools, and research/debugging:

- Default base: `base_resumes/sde_backend.tex` unless the JD is clearly ML/research/infrastructure-specific.
- Project priority order:
  1. Wysa backend experience (production scale + ownership signal).
  2. AgenticSearch (agentic systems + tests + provenance).
  3. Spark ETL / performance work (data + debugging mindset).
  4. Sonare — only if space allows or hacking/product-building is emphasized.
  5. Refusal Decay — only if ML / LLM safety / research is strongly relevant.
- Resume language should emphasize: ownership, quality, production backend systems, simple solutions to complex problems, debugging / research mindset, AI-assisted engineering, data/infrastructure/product readiness.
- Do not over-focus on pure ML research for broad SDE internships unless the JD explicitly asks for ML research.

### Multi-track JD handling

When a JD lists multiple tracks (e.g., "Software, Data, Applied ML, Infra, Security"):
- Pick the **primary** track that best matches Deva's strongest evidence and the JD's evaluation criteria — usually SDE/Backend.
- Treat secondary tracks as **angles** within the primary resume: surface 1–2 bullets that touch the secondary track without restructuring the resume.
- Do not split focus across tracks. One resume, one primary framing.

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
