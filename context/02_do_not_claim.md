# Do Not Claim

Hard guardrails. Never put any of the following on a resume unless explicitly verified in `01_verified_claims.md` first.

## Never invent

- Production scale numbers (users, RPS, QPS, dataset size).
- Active user counts.
- Revenue or business impact figures beyond the verified Wysa $340K+ contribution.
- Kubernetes ownership in production.
- Cloud production ownership (AWS / GCP / Azure account-level work, infra-as-code in production, on-call rotations on cloud infra).
- Large-scale model training (multi-node GPU training runs on real production data).
- Model serving at scale (vLLM/TGI/Triton in production with measured latency numbers).
- Publications beyond the verified IEEE CONIT 2023 Alzheimer's paper.
- Accepted or under-review papers at any venue.
- Internships or jobs not actually held.
- Open-source adoption metrics (stars, forks, downloads, dependents).
- Benchmarks or speedups without measured evidence in `01_verified_claims.md`.
- Security or compliance ownership beyond the verified Wysa VAPT/auth hardening work.
- Leadership titles not actually held (tech lead, manager, staff engineer).
- Product adoption beyond what the verified facts state.

## Project-specific limits

- Do not list the Scalar-Tensor Autograd Engine until the repo has real implementation.
- Do not list the Cache- and SIMD-Aware Matrix Multiplication or Performance Engineering Reproduction Study (CS 690PF) as standalone projects — private GitHub Classroom repos. Coursework name is OK.
- Do not list the LLM Inference Service, Distributed Training Simulator, CI/CD Pipeline for ML Models, or the Last.fm recommendation system on a resume — no public repos.
- Do not list Cloudflare Workers / Durable Objects / D1 / WorkflowEntrypoint as production experience. They are scoped to the cf ai research scout personal project.
- Do not claim Sonare hackathon placement or any specific accuracy/latency numbers — not stated.
- Do not claim quantitative refusal-decay findings until methodology and results are documented.

## Tooling realism

- Do not claim expertise in tools only mentioned casually. Use "Working knowledge" framing or omit.
- Do not claim production usage of: Kafka, RabbitMQ, GraphQL, Terraform, Jenkins, AWS Lambda, Prefect, vLLM, TRL, MCP, SLURM (these appeared on older resumes but are not backed by deep verified usage).
- Do not claim Spark or Databricks production usage outside the NYC TLC personal project.
- Go is listed in older resumes but production usage is not verified — keep as a language exposure, not a project deliverable.

## Scope realism

- Do not promote project work to "deployed", "in production", or "served users" unless stated in `01_verified_claims.md`.
- Do not promote a coursework lab to research output. Use phrasing like "course project" or "coursework" when relevant.
- Do not promote Wysa POC duties to people-management or staff-level leadership.

## Risky Claims Requiring Verification

These show up in the brain dump or earlier resumes and are tempting to reuse, but each needs verification before use:

- "6+ UK clients" vs "8+ UK clients" at Wysa — both have been published; default to 8+ but be ready to defend.
- "$340K+ revenue" — exact time window unspecified.
- "primary data labeling platform for model training" framing — appeared once in an archived resume; use the safer phrasing in `01_verified_claims.md`.
- KG2RAG "improved supporting-fact recall over the baseline" — qualitative only; no number.
- AgenticSearch broad-query robustness, extraction precision/recall — no external numbers.
- AutoEval discriminative-power deltas — no specific numbers.
- Spark ETL specific runtime/cost reduction percentages — none stated.
- Sonare on-device latency and accuracy — none stated.
- CI/CD ML Pipeline POC "30% deployment-time reduction" — appeared on a single old resume only; reuse with caution.

If a claim is needed for a JD and is in this list, either omit it or rephrase truthfully (e.g., "designed for X" instead of "achieved Y%").
