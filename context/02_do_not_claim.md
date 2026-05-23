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
- Do not list the US-client inventory management system (LinkedIn-sourced freelance sub-project) as a standalone project — no confirmed public repo; freelance-experience color only.
- Do not list the Expense-Tracker app as a resume project until its public repo and code are confirmed (currently a portfolio repo).
- Do not present the Teenofes internship (Mar–Jul 2022) as more than an undergraduate-era SDE internship; it is LinkedIn-sourced and unverified — surface only for Java/JSP/Servlet/Flutter-relevant JDs.
- Do not fold the MOOC/HackerRank certs or the Bhumi/VELS/census volunteering into resume content by default — weak signal; they live in the brain dump's Appendix D only.
- Do not list Cloudflare Workers / Durable Objects / D1 / WorkflowEntrypoint as production experience. They are scoped to the cf ai research scout personal project.
- Do not claim Sonare hackathon placement or any specific accuracy/latency numbers — not stated.
- refusal-decay findings are now documented and usable (graded full marks, COMPSCI 602): 0.92→0.32 refusal at k=3, monotone late-layer projection shift, 0/300 intervention null with controls, 87.5% classifier-agreement spot-check. But: it is a course research project, NOT a publication; and do not generalize the causal-null beyond the tested single-position interventions, the single model (Llama-3.1-8B-Instruct), or the prefilling attack family.
- Do not claim "8 architectures" for CS 689 — direct evidence (HW4) shows 5 base architectures; use "5 architectures across 3 optimizers." Do not assert "RealNVP" specifically — the HW5 flow is a coupling-layer normalizing flow; say "normalizing flow with coupling layers" unless RealNVP is confirmed. Do not put CS 689 quantitative results (CIFAR-10 accuracy, FID/NLL, Penn Treebank log-likelihood) or a final grade on a resume — unconfirmed. The HW6 transformer/LM work was read from the spec, not a submitted file.

## Tooling realism

- Do not claim expertise in tools only mentioned casually. Use "Working knowledge" framing or omit.
- Do not claim production usage of: Kafka, RabbitMQ, GraphQL, Terraform, Jenkins, AWS Lambda, Prefect, vLLM, TRL, MCP, SLURM (these appeared on older resumes but are not backed by deep verified usage).
- Do not claim Spark or Databricks production usage outside the NYC TLC personal project.
- Go is listed in older resumes but production usage is not verified — keep as a language exposure, not a project deliverable.

## Scope realism

- Do not promote project work to "deployed", "in production", or "served users" unless stated in `01_verified_claims.md`.
- Do not promote a coursework lab to research output. Use phrasing like "course project" or "coursework" when relevant.
- Do not promote Wysa POC duties to people-management or staff-level leadership.

## Trust the brain dump and context files

Claims that appear in `raw/brain_dump_original.md`, `context/01_verified_claims.md`, `context/03_skills.md`, `context/04_project_bank.md`, `context/05_bullet_bank.md`, or `context/00_resume_factbase.md` are **usable factual material**. Do not weaken or hedge them just because they are quantified. Specifically usable as-is:

- 8+ UK clients, 10,000+ monthly triage submissions, $340K+ revenue contribution at Wysa.
- 100+ hours/month manual-work reduction and 60% labeling throughput improvement on the Wysa annotation platform.
- 20+ VAPT findings remediated.
- 20+ RESTful APIs at Cario.
- 90%+ payments through portal and 70% manual-workload reduction on the freelance gym platform.
- 150+ automated tests on AgenticSearch.
- 30+ students tutored at Sayur.
- 5 neural architectures (perceptron, deep MLP, ReLU MLP, VGG-style CNN, ResNet) across 3 optimizers on CIFAR-10 (CS 689, HW4 — graded 87/100).
- 100–500 question batch experiments (KG2RAG-Enhanced).

Interview-prep notes (still usable on the resume — just be ready to defend the framing):

- Wysa client count: 8+ is the default. Earlier resumes used 6+; reconcile in interview if asked.
- $340K+ revenue: time window not stated publicly; phrase as "contributed to $340K+ in revenue" without claiming a window.

## Claims that cannot be invented (not in the truth source)

The following do NOT appear with measured numbers in the brain dump or context. Do not invent metrics for them:

- KG2RAG-Enhanced supporting-fact recall delta vs the baseline (qualitative only).
- AgenticSearch broad-query robustness, extraction precision/recall (no external numbers).
- AutoEval discriminative-power deltas (no specific numbers).
- Spark ETL specific runtime / cost / cluster-resource reduction percentages.
- Sonare on-device latency, accuracy, or hackathon placement.
- CI/CD ML Pipeline POC "30% deployment-time reduction" — appeared on a single archived resume; do not surface (project also has no public repo).

If a JD asks for a quantitative outcome on one of the above, either omit it or rephrase truthfully (e.g., "designed for X" / "reduced shuffle volume and runtime" without a percentage).
