# Resume Factbase

> Read this file FIRST during JD tailoring. It is a routing index, not the full source. Pull deeper detail from the numbered files below only when needed.

---

## Identity

- Name: Deva Anand
- Email: devaanand@umass.edu
- Phone: (413) 315-1715
- Web: devaanand.com
- LinkedIn: linkedin.com/in/devaaa
- GitHub: github.com/Deva-1903

## Current Status

- MS in Computer Science, University of Massachusetts Amherst (Sept 2025 – May 2027 expected).
- Prior: B.E. Computer Science and Engineering, Vels Institute of Science, Technology and Advanced Studies (VISTAS), Chennai (Aug 2019 – May 2023).
- Prior full-time role: Backend Engineer at Wysa (Jul 2023 – Jul 2025), Bengaluru, India.
- Open to internship and new-grad-style roles for 2026.

## Target Roles

Five role families. Each maps to one base resume in `base_resumes/`.

1. SDE / Backend Engineer
2. SRE / Systems / Infrastructure / Platform
3. ML Engineer / ML Systems
4. AI Engineer / LLM Engineer / Agentic AI
5. Applied Scientist / Research Engineer / Research Intern

## Core Positioning

- Backend engineer with two years of production Node.js / MongoDB experience in regulated multi-tenant healthcare (NHS), now in an MS focused on ML systems, AI/LLM systems, retrieval, and performance engineering.
- Strongest signal blends: production backend ownership + research-grade project rigor (provenance, evaluation, from-scratch ML).
- Comfortable across the stack: REST APIs, integration tests, security hardening, retrieval pipelines, agentic systems, low-level performance work.

## Strongest Evidence

- Wysa: multi-tenant NHS eTriage (8+ UK clients, 10,000+ monthly submissions, $340K+ revenue contribution, 20+ VAPT remediations) and a full-stack ML training-data annotation platform (100+ hrs/month saved, 60% throughput uplift).
- AgenticSearch: provenance-first agentic web discovery; 150+ automated tests; OpenAI/Groq/Brave; reviewer-facing trust UI.
- CS 689 (Adv ML, Prof. Domke, Fall 2025): matrix-based reverse-mode autodiff engine from scratch in NumPy (validated against JAX); 5 architectures on CIFAR-10 across 3 optimizers (HW4, graded 87/100); normalizing-flow + DDPM generative models in JAX; GD/SGD convergence theory.
- Sonare: offline sign↔speech cross-platform desktop app (Electron/React/FastAPI/MediaPipe/whisper.cpp), Qualcomm Edge AI Hackathon 2025.
- Spark ETL Performance Optimization on NYC TLC (Databricks; partitioning, broadcast joins, caching, column pruning, Spark UI analysis).
- IEEE CONIT 2023 publication: "Alzheimer's Disease Classification using Transfer Learning."

## Role Families

### SDE / Backend
Strongest evidence: Wysa eTriage backend, Wysa annotation platform, Cario REST APIs, Sonare backend, AgenticSearch service.

### SRE / Systems
Strongest evidence: Wysa reliability/security ownership, Spark ETL performance optimization, CS 690PF Performance Engineering coursework, Sonare async/queue design.

### ML Engineer
Strongest evidence: CS 689 generative models from scratch, AgenticSearch pipeline, KG2RAG-Enhanced retrieval, Wysa annotation platform (data infra), Spark ETL.

### AI Engineer
Strongest evidence: AgenticSearch (planning, retrieval, extraction, provenance), AutoEval, KG2RAG-Enhanced (RRF + cross-encoder + MMR + knapsack), Cario LLM chat integration, cf ai research scout.

### Applied Scientist / Research
Strongest evidence: CS 689 generative models, KG2RAG-Enhanced, AutoEval, IEEE CONIT 2023 publication, refusal-decay (LLM safety).

## Most Reusable Projects

| Project | Roles it serves best |
|---|---|
| AgenticSearch | AI Engineer, ML Engineer, Applied Scientist, SDE/Backend |
| AutoEval | AI Engineer, Applied Scientist, ML Engineer |
| CS 689 Advanced ML (autodiff, flows/DDPM, CIFAR-10) | Applied Scientist, ML Engineer |
| KG2RAG-Enhanced | Applied Scientist, AI Engineer, ML Engineer |
| Sonare | SDE/Backend, ML Engineer (edge), SRE (async/offline) |
| Spark ETL Optimization | SRE/Systems, ML Engineer (data), SDE/Backend |
| cf ai research scout | AI Engineer, SRE/Systems (edge/serverless) |
| Alzheimer's Classification | Applied Scientist, ML Engineer |
| refusal-decay | Applied Scientist / Research (alignment, interpretability, safety), ML Engineer |

## Resume Strategy

- Always start from the closest base resume in `base_resumes/`.
- Reorder skills, projects, and bullets — do not invent new content.
- Keep one page. Cut weaker bullets first. Never inflate metrics.
- If JD requires unsupported tooling, prefer adjacent truthful framing over stretching a claim.

## Files to Read Next

When tailoring a JD, default reading order:

1. `context/07_resume_style_rules.md` — formatting and constraints.
2. `context/06_role_targeting.md` — pick base resume and emphasis.
3. `context/01_verified_claims.md` — truth source.
4. `context/02_do_not_claim.md` — guardrails.
5. `context/03_skills.md` — skills bank.
6. `context/05_bullet_bank.md` — paste-ready bullets.
7. `context/04_project_bank.md` — only if you need full project detail or alternate phrasings.

Do NOT default to reading:

- `raw/brain_dump_original.md` — only when a specific fact is missing here.
- Old `applications/` folders — only when explicitly asked.
- Previous tailored resumes — unless explicitly chosen as a base.
- `context/08_motivation_bank.md` — NOT for resume tailoring; see below.

## Free-text application answers (separate from resume tailoring)

For free-text application boxes ("Why are you interested?", "Anything else?", "Why are you looking?"), use `context/08_motivation_bank.md` — reusable, company-agnostic voice fragments, assembled with one per-JD hook. It is bound by the truth hierarchy but is NOT a resume source; do not read it during `/lean-apply`.
