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
- CS 690PF (Cache/SIMD-Aware Matrix Multiplication + Performance Engineering Reproduction Study) is now **resume-eligible** via the PUBLIC consolidated repo `https://github.com/Deva-1903/cs690pf` (verified public 2026-07-02). List it as a standalone linked project using THIS repo; do NOT link the per-assignment GitHub Classroom repos (`690pf-assignment-0`, `assignment-1-Deva-1903`, `assignment2-Deva-1903`, `project-Deva-1903-690pf`) — those remain private. Keep it framed as graded coursework, not production: do not claim production/HFT deployment or a specific unverified speedup number (the stage-by-stage best speedups, final block sizes, and thread sweet-spot are still "Needs Review" in the brain dump).
- Do not list the LLM Inference Service, Distributed Training Simulator, CI/CD Pipeline for ML Models, or the Last.fm recommendation system on a resume — no public repos.
- Do not list the US-client inventory management system (LinkedIn-sourced freelance sub-project) as a standalone project — no confirmed public repo; freelance-experience color only.
- Do not list the Expense-Tracker app as a resume project until its public repo and code are confirmed (currently a portfolio repo).
- Do not present the Teenofes internship (Mar–Jul 2022) as more than an undergraduate-era SDE internship; it is LinkedIn-sourced and unverified — surface only for Java/JSP/Servlet/Flutter-relevant JDs.
- Do not fold the MOOC/HackerRank certs or the Bhumi/VELS/census volunteering into resume content by default — weak signal; they live in the brain dump's Appendix D only.
- Do not list Cloudflare Workers / Durable Objects / D1 / WorkflowEntrypoint as production experience. They are scoped to the cf ai research scout personal project.
- Do not claim Sonare hackathon placement or any specific accuracy/latency numbers — not stated.
- refusal-decay findings are now documented and usable (graded full marks, COMPSCI 602): 0.92→0.32 refusal at k=3, monotone late-layer projection shift, 0/300 intervention null with controls, 87.5% classifier-agreement spot-check. But: it is a course research project, NOT a publication; and do not generalize the causal-null beyond the tested single-position interventions, the single model (Llama-3.1-8B-Instruct), or the prefilling attack family.
- Do not claim "8 architectures" for CS 689 — direct evidence (HW4) shows 5 base architectures; use "5 architectures across 3 optimizers." Do not assert "RealNVP" specifically — the HW5 flow is a coupling-layer normalizing flow; say "normalizing flow with coupling layers" unless RealNVP is confirmed. Do not put CS 689 quantitative results (CIFAR-10 accuracy, FID/NLL, Penn Treebank log-likelihood) or a final grade on a resume — unconfirmed. The HW6 transformer/LM work was read from the spec, not a submitted file.
- KG2RAG-Enhanced is a team project: Deva led multi-view retrieval; the 0–1 knapsack token-budget selection (teammate Sharvi) and KG construction/reasoning (teammate Aditi) were teammate-led. Do not present the knapsack or KG-construction work as Deva's solo contribution; frame the pipeline team-wide and lead with Deva's multi-view retrieval and the +2.68% SP recall it drove.
- ngvi-curvature-variance is a 3-person CS 651 team project with no per-author contribution breakdown. Keep bullets team-framed; do not claim solo ownership of a component. Do not state the κ→ELBO-gain relationship as a proven scaling law (n=3, D≲10; the fit line is visual-only).
- **CAM Lab (Lab Assistant, current):** platform is PRE-LAUNCH as of 2026-07-11 — do not claim launched, in production, deployed for lab use, or any user/adoption numbers. Do not claim Supabase/Google sign-in (designed, not integrated), Postgres migration, or run-limit/retention enforcement (decided, not implemented). Do not put the ~1e-5 reproduction-parity number on a resume (design target, unverified on real weights). Do not link the lab GitHub repo anywhere (unpushed, redistribution-rights question open) — the PRE-HIRE demo repo/live link (Deva-1903/ccr-platform) remains the only linkable artifact. Official title is "Lab Assistant"; do not inflate to Research Assistant/Engineer as a title (describing the work as research-platform engineering is fine). The 99 constructs are EXISTING published scales imported into the library — do not phrase as creating/validating scales; wordings are not verbatim-verified. No publication, authorship, or research-contribution claims from this role.

## Tooling realism

- Do not claim expertise in tools only mentioned casually. Use "Working knowledge" framing or omit.
- Do not claim production usage of: RabbitMQ, GraphQL, Terraform, Jenkins, AWS Lambda, Prefect, vLLM, TRL, MCP, SLURM (these appeared on older resumes but are not backed by deep verified usage).
- UPDATE (user-confirmed 2026-06-10): **Kubernetes, Apache Kafka, and DynamoDB** are now resume-safe at **working-knowledge / project level** (built/used in personal projects). List plainly in Skills. Still do NOT claim production-scale or production-ownership of these. See `03_skills.md`.
- Do not claim Spark production usage outside the NYC TLC personal project. Do NOT list Databricks for the Spark ETL project at all — that repo runs locally via spark-submit and Databricks is not evidenced; only claim Databricks if separately true.
- Go is listed in older resumes but production usage is not verified — keep as a language exposure, not a project deliverable.

## Scope realism

- Do not promote project work to "deployed", "in production", or "served users" unless stated in `01_verified_claims.md`.
- Do not promote a coursework lab to research output. Use phrasing like "course project" or "coursework" when relevant.
- Do not promote Wysa POC duties to people-management or staff-level leadership.

## Tailoring stability (metric referents and scope descriptors)

Tailoring may reframe vocabulary and emphasis across JDs. It may NOT change what claims appear, what they are attributed to, or how broad they are. The rules below are how the truth boundary stays leak-proof across versions.

### Metric referent lock

Every quantified claim has ONE attributed cause, decided once from the truth source. Do not re-point a metric at a different outcome to flatter a JD. You may reorder, omit, or de-emphasize a metric; you may not change what it caused.

Anchored referents (use these — do not paraphrase to a different cause):

- `100+ hours/month` — manual annotation / operations work removed by the **Wysa annotation platform**. NOT "model-training iteration", "research velocity", or "AI-team productivity".
- `60%` — **labeling throughput** improvement on the Wysa annotation platform. NOT engineering velocity or general "throughput".
- `$340K+` — revenue contribution at Wysa (no time window claimed).
- `8+ UK clients` — UK clinical clients of the NHS eTriage backend at Wysa.
- `10,000+ monthly submissions` — NHS eTriage submissions at Wysa.
- `20+ VAPT` — vulnerabilities remediated at Wysa.
- `20+ RESTful APIs` — designed at Cario.
- `150+ tests` — automated tests on **AgenticSearch**.
- `+2.68% SP recall (54.53 → 57.21)` — KG2RAG-Enhanced vs the KG²RAG baseline on a 4,905-question HotpotQA eval.
- `~25% ETL runtime cut (17–19 min → 14.3 min)` — NYC TLC Spark ETL.
- `2.14x → 1.74x tail-latency ratio` — NYC TLC Spark analytics tail latency.
- `5 architectures × 3 optimizers on CIFAR-10` — CS 689 HW4.

If the JD seems to want a different framing for one of these metrics, choose a different bullet — do NOT re-attribute the metric to fit.

### JD-independent scope and ownership descriptors

Scope, ownership, and audience phrases are either true of the work or not. They are decided once from the truth source, not toggled per JD.

- **Ownership verbs** (`Owned`, `Led`, `Drove`, `Primary technical point of contact`) — include only if the truth source already supports them for that experience. You may reorder or emphasize, but you may NOT *add* one for a JD that rewards ownership and *drop* it for a JD that doesn't.
- **Scope words** (`production`, `production-facing`, `multi-tenant`, `distributed`, `real-time`, `large-scale`) — same rule. The Wysa eTriage backend is multi-tenant in every version or none.
- **Audience claims** (`used daily by the AI team`, `consumed by clinical reviewers`, `for downstream production models`) — same rule. If the AI team used it daily, that's stable across all resumes; if not, do not surface it on the AI/ML versions to flatter the JD.

The overfitting tell to catch in your own draft: a scope/ownership/audience phrase that appears on the AI/ML version but vanishes on the SDE/SRE version of the same job. If it's true, it belongs everywhere; if it isn't, it belongs nowhere.

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
- KG2RAG-Enhanced: supporting-fact recall +2.68% (54.53 → 57.21) over the KG²RAG baseline on a 4,905-question evaluation (KGs over 28,492 entities); EM +4.2% on the controlled N=1,000 run. Lead with the +2.68% SP recall; keep knapsack/KG-construction team-framed.
- Spark ETL: ~25% total ETL runtime cut (17–19 min → 14.3 min) and tail-latency ratio 2.14x → 1.74x (~19%) on the ~1.4B-row NYC TLC dataset; broadcast joins minutes → ~0.05s.
- ngvi-curvature-variance (CS 651): NGVI ELBO gain over Adam grows with curvature (κ≈180 → 2566 maps to +0.28 → +2.32 nats); antithetic sampling cut gradient variance ~10×. Keep team-framed.

Interview-prep notes (still usable on the resume — just be ready to defend the framing):

- Wysa client count: 8+ is the default. Earlier resumes used 6+; reconcile in interview if asked.
- $340K+ revenue: time window not stated publicly; phrase as "contributed to $340K+ in revenue" without claiming a window.

## Claims that cannot be invented (not in the truth source)

The following do NOT appear with measured numbers in the brain dump or context. Do not invent metrics for them:

- AgenticSearch broad-query robustness, extraction precision/recall (no external numbers).
- AutoEval discriminative-power deltas (no specific numbers).
- Sonare on-device latency, accuracy, or hackathon placement.
- KG2RAG-Enhanced and Spark ETL recall/runtime numbers are now MEASURED and resolved (see "usable as-is" list above), no longer invent-prohibited. Spark's "Est."-marked analytics figures (30–50% faster, 20–30% less I/O) remain off-limits as measured claims.
- CI/CD ML Pipeline POC "30% deployment-time reduction" — appeared on a single archived resume; do not surface (project also has no public repo).

If a JD asks for a quantitative outcome on one of the above, either omit it or rephrase truthfully (e.g., "designed for X" / "reduced shuffle volume and runtime" without a percentage).
