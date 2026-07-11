# Project Ideas & Portfolio Roadmap

_Purpose: one place to track every portfolio project idea so nothing gets lost. Each project is mapped to the **recurring application gaps it closes** (counts = how many past applications flagged that gap, from `tracking/skill_gaps.jsonl`). Priority = gap-count payoff × how finishable it is._

_Last updated: 2026-07-10_

---

## Decisions log

- **2026-07-10 — "Train an LLM from scratch" is NOT a portfolio project.** It closes zero recurring resume gaps (pretraining appears nowhere in the gap data). The real payoff it advertises — interview confidence on transformer internals — is captured far more cheaply by a one-weekend nanoGPT rep (see Active #3). Energy goes to finishing align-ops + the LangGraph project and **writing them up**, not starting a third build. Reconsider only if, mid-align-ops, the attention/GRPO math doesn't click — then do the nanoGPT rep first.

---

## Active builds (in priority order)

### 1. align-ops — LLM Post-Training + Serving Ops  ⭐ marquee
Base LLM → **SFT (QLoRA) → DPO → GRPO** → eval win-rate → serve (vLLM + FastAPI + Redis + batching) → monitor (Prometheus/Grafana) → Docker → K8s on cloud GPU → CI. Full blueprint: `align-ops-PROJECT-SPEC.md` (7 phases, ~$20–60 GPU).

**Gaps it closes:**
- Reinforcement Learning — **13** (DPO + GRPO)
- Fine-tuned LLM / production training — **9** (SFT/QLoRA)
- Distributed training — **6** (accelerate + FSDP)
- Observability (Grafana/Prometheus) — **3 / 2**
- vLLM — **2**
- LoRA/QLoRA — **2**
- MLflow — **1**
- Jenkins — **6** (optional `Jenkinsfile` alongside GitHub Actions)
- Vector databases — **4** (if a retrieval/cache layer is added)

**This single project covers your #1, #2, and #4 recurring gaps.** Highest ROI on the board.

- **Status:** blueprint written, not yet built.
- **Next action:** build through **Phase 5** minimum (SFT→DPO→GRPO→eval). One number — "DPO wins X% vs base on N prompts" — is the payoff.
- **Done when:** repo reproduces SFT→DPO→GRPO from configs, shows an eval win-rate vs base, `docker compose up` shows live serving metrics in Grafana, + two build-in-public articles (dev phase, prod phase).

### 2. LangGraph agentic system — orchestration + ops
End-to-end multi-agent app with LangGraph: orchestration, memory, guardrails, security, evals, observability, benchmarks, cloud deployment, scalability.

**Gaps it closes:**
- LangGraph — **2**
- LangChain — **3**
- Agent frameworks (LangChain/LangGraph) — **1**
- Multi-agent systems / collaboration — **1 + 1**
- Observability — **3** (shared theme with align-ops)
- MCP servers (building) — **1** (if an MCP tool server is included)
- Self-evolving / agent ontology — **1 each** (stretch)

- **Status:** planned.
- **Next action:** scope the concrete agent task first (don't start with the framework). Pick a real workflow, then wire orchestration/memory/guardrails/evals around it.
- **Done when:** a deployed multi-agent pipeline with guardrails + an eval harness + an observability board, plus a write-up.

### 3. nanoGPT weekend rep — interview muscle (throwaway, $0)
~150-line from-scratch transformer: implement attention, a training loop, a tokenizer, and sampling **from memory, no HF Trainer**, on a tiny char dataset (CPU / free T4).

- **Not a portfolio project** — notes only, no polish, no article.
- **Payoff:** answer attention / positional-encoding / KV-cache / sampling / "how does training actually work" questions cold. Also de-risks align-ops (the GRPO advantage math lands faster once you've hand-rolled a training loop).
- **Status:** not started. **Do this first if align-ops internals feel shaky.**

---

## Backlog — candidate projects for the biggest STILL-UNCOVERED gaps

The two active AI projects cover the ML/agent/serving gaps. These are the largest gaps **no current project touches** — each could become a future build if you want breadth beyond AI/ML.

### A. Systems / DevOps / cloud-infra project
Covers the biggest non-AI cluster: **Go (7)**, **Terraform (5)**, **Jenkins (6, or fold into align-ops)**, Ansible (3), Infrastructure-as-Code (1), gRPC (1), Real-time systems (3).
- Idea: a Go backend service (client-server, gRPC) provisioned with Terraform, CI via Jenkins, deployed to cloud. Directly attacks the Go gap, which is your #1 *language* gap and shows up constantly in SDE/SRE JDs.

### B. GPU / CUDA project
Covers **CUDA (8)** — your #3 overall gap and completely uncovered — plus Triton (2), high-performance inference / GPU kernels (1), TensorRT (1).
- Idea: a hand-written CUDA kernel (or Triton kernel) for an op you already understand (matmul/attention), benchmarked vs a baseline. Pairs naturally with your existing `cs690pf` cache/SIMD work (CPU→GPU story). High signal for ML-systems/inference roles.

### C. Mobile app
Covers **Mobile development (7)** + React Native (3) + Swift (1) — entirely uncovered.
- Idea: a small React Native app (reuses your React skill) shipping one real feature. Only worth it if you're targeting roles that ask for mobile; otherwise skip.

### D. Data-viz / BI dashboard
Covers Data visualization / D3 (2), BI tools (3), Tableau (1) — small but recurring, and flagged on a real application (BillionToOne).
- Idea: could be satisfied cheaply as the **Next.js dashboard on align-ops** (chat + live Grafana panels) — kills two birds (Next.js skill + data-viz gap) without a separate project.

### Enterprise-language gaps (no project needed — exposure, not portfolio)
C# (6) / .NET (4) / Spring Boot (3) / Java-production (2) / Angular (4): these are stack-familiarity gaps. A dedicated project is low-ROI; better closed by a focused tutorial/small service if a specific target role demands it. Don't build a portfolio piece just for these.

---

## Gap coverage summary

| Rank | Gap | Count | Covered by |
|---|---|---|---|
| 1 | Reinforcement Learning | 13 | align-ops ✅ |
| 2 | Fine-tuned LLM (prod training) | 9 | align-ops ✅ |
| 3 | CUDA | 8 | Backlog B (uncovered) |
| 4 | Go | 7 | Backlog A (uncovered) |
| 5 | Mobile development | 7 | Backlog C (uncovered) |
| 6 | Embedded / firmware | 6 | — (out of scope) |
| 7 | Distributed training | 6 | align-ops ✅ |
| 8 | Jenkins | 6 | align-ops (optional) / Backlog A |
| 9 | Rust | 6 | Backlog A (uncovered) |
| 10 | Vector databases | 4 | align-ops (if added) / LangGraph |

**Takeaway:** align-ops alone closes 3 of your top-8 gaps. After it + the LangGraph project ship (with write-ups), the highest-value *uncovered* territory is **CUDA (8)** and **Go (7)** — those are the natural third and fourth projects if you want to broaden past AI/ML.
