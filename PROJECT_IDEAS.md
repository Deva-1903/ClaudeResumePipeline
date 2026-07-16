# Project Ideas & Portfolio Roadmap

_Purpose: one place to track every portfolio project idea so nothing gets lost. Each project is mapped to the **recurring application gaps it closes** (counts = how many past applications flagged that gap, from `tracking/skill_gaps.jsonl`). Priority = gap-count payoff × how finishable it is._

_Last updated: 2026-07-13_

---

## Decisions log

- **2026-07-13 — Rank 1 of the inference track SHIPPED + promoted to the project bank.** Quantized GEMM (INT8→INT4) NEON kernels built and measured on M4 Pro: fp32 3 GFLOP/s → int8 4×4-tiled 394 GFLOP/s (132×, ~2.5× over clang auto-vec), int4 W4A8 weights 6.4× smaller. Public repo: https://github.com/Deva-1903/neon-quantized-gemm. Now a real entry in `context/04_project_bank.md`. Two deviations from the original scope, both logged in the bank's "Do not claim": built on **ARM NEON, not AVX** (dev machine is Apple Silicon; concepts map to AVX-512-VNNI), and accuracy validated via **SNR on synthetic data — perplexity on a real model is still TODO** (do that in Rank 2 when a real GGUF tensor is loaded).
- **2026-07-13 — Added the "Inference Engineering × Low-Latency C++ track" (ranked 5-project build order).** Grew out of HRT (low-latency C++) and inference-serving JDs. Expands old Backlog B (GPU/CUDA) into a full arc: INT8/INT4 SIMD GEMM → mini C++ inference engine → CUDA kernel → continuous batching → OSS PR. Builds on `cs690pf` + align-ops; closes CUDA (8) + C++ systems (5) + vLLM/Triton. Kept out of `context/04_project_bank.md` on purpose — it's aspirational, not resume-eligible until built + measured.
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
- **Expanded into a full ranked track below — see "Inference Engineering × Low-Latency C++ track." This item is Rank 3 of that track.**

### C. Mobile app
Covers **Mobile development (7)** + React Native (3) + Swift (1) — entirely uncovered.
- Idea: a small React Native app (reuses your React skill) shipping one real feature. Only worth it if you're targeting roles that ask for mobile; otherwise skip.

### D. Data-viz / BI dashboard
Covers Data visualization / D3 (2), BI tools (3), Tableau (1) — small but recurring, and flagged on a real application (BillionToOne).
- Idea: could be satisfied cheaply as the **Next.js dashboard on align-ops** (chat + live Grafana panels) — kills two birds (Next.js skill + data-viz gap) without a separate project.

### Enterprise-language gaps (no project needed — exposure, not portfolio)
C# (6) / .NET (4) / Spring Boot (3) / Java-production (2) / Angular (4): these are stack-familiarity gaps. A dedicated project is low-ROI; better closed by a focused tutorial/small service if a specific target role demands it. Don't build a portfolio piece just for these.

---

## Inference Engineering × Low-Latency C++ track (ranked build order)

_The highest-fit lane for turning coursework-level C++ into production ML-systems C++/CUDA. Converts what you already have — `cs690pf` AVX/SIMD matmul + `perf`, and `llama.cpp` exposure from Cario — into an "I built and benchmarked an inference runtime" story. This is the intersection where your ML background is an **asset**, not neutral (NVIDIA, model-serving startups, frontier-lab inference teams), and it also clears HFT-style low-latency-C++ bars._

**Gaps it closes:** CUDA — **8** (#3 overall, uncovered); C++ systems-level — **5**; Triton — **2**; vLLM — **2**; high-perf inference / GPU kernels — **1**; TensorRT — **1**; networking (partially, via the alt track) — **3**.

**Discipline (applies to every item):** report **tail percentiles, not means** (p50/p99/p999), pin threads, isolate CPUs, account for measurement bias (cite your CS 690PF Mytkowicz reproduction). Every resume-eligible claim needs a **measured** number you can defend in an interview: tokens/sec, TTFT, inter-token latency, kernel latency vs a baseline, GPU/CPU + memory-bandwidth utilization.

> **Not resume-eligible until built.** None of these has a repo or measured metric yet, so none may go on a resume or into `/lean-apply`. When one ships with a public repo + confirmed numbers, promote it to a real entry in `context/04_project_bank.md` (that's the file `/lean-apply` reads) — not here.

Do them in this order; each reuses the previous, so the arc compounds into one coherent system rather than five disconnected repos.

### Rank 1 — Quantized GEMM kernel (INT8 → INT4) with SIMD ✅ SHIPPED (2026-07-13)
- **What:** full INT8 matmul with dequant + GGUF-*style* INT4 block quant, hand-vectorized. Built on **ARM NEON `sdot`** (Apple M4), not AVX — concepts map to AVX-512-VNNI 1:1.
- **Repo:** https://github.com/Deva-1903/neon-quantized-gemm (public). **Now in `context/04_project_bank.md`.**
- **Measured (512³, M4 Pro, p50):** fp32 naive 3 → int8 4×4 register-tiled **394 GFLOP/s (132×, ~2.5× over compiler auto-vec)**; int4 W4A8 weights **6.4× smaller** than fp32; all kernels bit-exact vs scalar reference; p50/p99/p999 harness.
- **Still open (do not claim yet):** accuracy is SNR on **synthetic** data (45 dB int8 / 23 dB int4) — **no perplexity on a real model**; single-threaded only; NEON not AVX. Fold the perplexity metric in during Rank 2 (real GGUF weights).

### Rank 2 — From-scratch CPU inference engine (mini `llama.cpp` / `llm.c`)
- **What:** load a small model (GPT-2 / TinyLlama, GGUF), implement matmul (reuse Rank 1), attention, RMSNorm, RoPE, KV cache, sampling — pure C++, no framework.
- **Why second:** consumes the Rank 1 kernel and produces end-to-end numbers; this is the flagship repo of the track.
- **Metrics:** tokens/sec, TTFT, memory footprint; publish a naive → SIMD → multithreaded → cache-blocked latency ladder.

### Rank 3 — One CUDA kernel (mini flash-attention OR INT8 GEMM on GPU)  ← was Backlog B
- **What:** a tiled attention kernel with online softmax, or a fused RMSNorm+matmul, or an INT8 GEMM on GPU.
- **Why third:** opens GPU/CUDA (your #3 gap, and the actual inference-runtime job); best attempted once Rank 2 has taught you the ops.
- **Metrics:** kernel latency vs cuBLAS / PyTorch-eager, memory-bandwidth utilization via Nsight Compute (a roofline chart). Even one well-benchmarked kernel is standout signal.

### Rank 4 — Continuous batching + paged KV-cache serving layer (the vLLM core, in C++)
- **What:** a request scheduler that batches decode steps across concurrent requests, with a paged KV allocator + backpressure.
- **Why fourth:** the systems/serving layer — builds on Rank 2's engine + Rank 3's kernels, and is **align-ops one layer deeper** (you did the Python/vLLM orchestration above this; now build the engine underneath).
- **Metrics:** throughput-vs-latency curve, p99 inter-token latency under load, GPU util, batch efficiency vs one-request-at-a-time.

### Rank 5 (ongoing / last) — Real OSS contribution to `llama.cpp` / `vLLM`, or a runtime plugin
- **What:** merge an op/optimization into `llama.cpp` or `vLLM`, or write a TensorRT plugin / ONNX Runtime custom op / torch C++ extension / speculative-decoding path.
- **Why last:** best once Ranks 1–4 give you the vocabulary to navigate a large production C++/CUDA codebase. Strongest "look at code, figure out how it works, make it better" signal — with a merged PR to show — which also directly answers HFT-style firms.
- **Metrics:** merged-PR link, tokens/sec uplift, (spec-decode) acceptance rate.

**Reference material:** Karpathy `llm.c`; `llama.cpp` / `ggml` source; FlashAttention paper; vLLM PagedAttention paper; Carl Cook "When a Microsecond Is an Eternity."

**Adjacent alt track (pure low-latency C++, no ML — only if targeting pure HFT over inference):** ITCH/PCAP binary feed parser → in-memory limit-order book / matching engine → lock-free SPSC/MPSC ring buffer → kernel-bypass networking (io_uring / DPDK / ef_vi). Same measure-the-tail discipline; closes the networking (3) gap the inference track doesn't. Lower fit than the inference track given your ML background.

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
