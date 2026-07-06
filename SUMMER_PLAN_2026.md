# Summer 2026 Plan — June 10 → Sept 15

Goal: Fall 2026 internship (big tech preferred) + be fully interview-ready when 2027 new-grad postings open in August. Target: $130–150K base FT. Budget: 8–10 hrs/day, ~14 weeks.

## The one decision (so you stop being confused)

**Depth bet: LLM post-training + inference, with agents as the applied layer.**

Why this and not the others:

- Your own skill-gap data (113 JD keywords tracked) clusters here: RL (9 JDs), CUDA (5), distributed training (4), fine-tuned LLM (2), vLLM (2), LoRA/QLoRA (2), TensorRT-LLM, SGLang, Triton, RL post-training. One coherent stack covers ~25 of your tracked gaps.
- Correction (Deva, 2026-06-10): the CS689 work (autodiff, transformers, generative models) and AutoEval were vibe-coded — little deep understanding; AgenticSearch understood at layer level only. So Phase 1 assumes learning ML for real from near-zero, and every phase includes "re-own a resume project" defense-doc tasks, since interviewers will probe these claims. Detailed week-by-week version: `SUMMER_CHECKLIST_2026.md`.
- Your PhD-student research idea (character persona models) IS a post-training project: fine-tuning + evals. Research and depth bet are the same work.
- It's what the market is hiring for in 2026 (NVIDIA, Cohere, Workato-AI-Lab-type roles all asked for exactly this).

**Explicitly NOT doing this summer** (these gaps are noise from scattershot applications, not signal): Go, Rust, Angular, mobile/React Native, SLAM/robotics, crypto/DeFi, Terraform/Ansible depth, AWS certifications. If an interview needs Terraform basics, learn it that week, not now.

## Answers to your open questions

**Karpathy videos?** Yes — they are the spine of Phase 1–2, not a side activity. Order: Zero to Hero (micrograd → makemore → GPT from scratch) → nanoGPT → nanochat (his full-stack ChatGPT-clone repo: tokenizer, pretraining, SFT, RL, inference, serving — exactly your depth bet). Rule: 70% typing code yourself, 30% watching. You already built autodiff from scratch, so micrograd will be fast review — the payoff starts at makemore.

**Certifications (AWS etc.)?** No. Big-tech SDE/ML loops give zero credit for certs — they test coding, design, ML depth, and projects. Every cert hour is a stolen flagship-project hour. Certs matter for IT/cloud-consulting roles you aren't targeting.

**"Foundations shaky, so should I even start the research project?"** Start it. The persona project requires exactly the foundations Phase 1 builds — they run in parallel and the project gives the revision purpose. Waiting for "ready" is how it stays untouched for another 2 months.

**What ML interviews look like** (so you know what "ready" means):

1. DSA coding — same as SDE, usually slightly lighter.
2. ML breadth Q&A — bias/variance, regularization, attention math, loss functions, eval metrics. (CS689 revision + Deep-ML sheet covers this.)
3. ML coding — implement attention / k-means / logistic regression from scratch in NumPy. (Your autodiff work + the Deep-ML list is literally this.)
4. ML system design — "design a recommendation system / search ranking." (Your tracker's ML System Design sheet has the case list.)
5. Behavioral — STAR stories; redo Amazon LP bank with lessons learned.

---

## Research track (added 2026-06-10)

Deva wants research roles (Research Engineer / Applied Scientist) in scope for Fall + FT. Honest framing: publications can't appear by September, but **replication skill + a paper-shaped project + advisor relationships** can — and that's what RE/AS-intern screens actually test at the entry level. Additions (~1.5–2h/day, total now ~10h):

- **Math spine (W5–14):** 45 min/day probability + linear algebra done properly (Math for ML book / Blitzstein), not just interview-level.
- **Paper replication (W4–7):** pick one persona/eval paper, reproduce its core experiment, publish a 1-page replication report. This is THE research-craft credential the summer can produce.
- **Paper-shaped flagship:** the persona eval harness gets baselines, ablations, and a related-work section — workshop-paper shaped by Week 9.
- **Suryaansh's ICLR paper** (LLM-judge bias) is directly adjacent to the eval harness — read it, talk to him (W5).
- **Phase 3 additions:** apply to RE/AS-intern + residency-style postings, build a 10-min research talk from the flagship, set up Fall (RL course with Bruno Castro Da Silva, fixed PhD-project block, identify a second prof in AI-alignment / AI-for-SE).
- **Winter/Spring:** workshop submission from the persona/eval work. That's the realistic first publication rung.

Cut order updates: fun builds → CUDA depth → system-design count → replication scope. DSA, applications, flagship stay sacred.

## Phase 0 — This week (June 10–14)

| Priority | Task |
|---|---|
| 1 | **TherAlign final technical round.** A summer role beats everything on this plan — real experience + resume line + income. Prep from `TherAlign_Interview_Prep_2026-06-09.md`. Their stack gaps from your tracker: Next.js, Firebase, SMART on FHIR — review at app level. |
| 2 | **Message the PhD student.** One concrete line: "I want to restart the persona-model idea — I'm spending the summer on LLM post-training; can we meet in 2 weeks once I've read the key papers and have an experiment proposal?" Sets a deadline. |
| 3 | **Word Break II post-mortem.** Solve it cold, then the pattern family: 139, 140, 131, 93, 39/40, 79. DP + backtracking is your first DSA block. |
| 4 | Set up daily log (one line per day in this repo: what shipped). |

## Phase 1 — Foundations, hands-on (June 10 → July 5, 4 weeks)

| Block | Daily | What |
|---|---|---|
| DSA | 2h | NeetCode 150, DP + backtracking first, then graphs, then the rest. Cold solves, 25-min timebox, then study solution. ~8/wk minimum. |
| Karpathy | 2.5h | Zero to Hero series, code-along. Finish through "GPT from scratch" + tokenizer video by July 5. |
| ML breadth | 1h | Deep-ML sheet (your existing xlsx, weeks 1–4, 8–12 items/wk) alternating with CS689 selective revision: optimization/SGD/Adam (HW4), transformers (HW6/Lecture 10+), generative models. Skip the rest of 689. |
| Research | 1h | Read persona/character-model papers (Character-LLM, RoleBench, persona-consistency evals — collect 6–8). End of phase: 1-page experiment proposal → meeting with PhD student. |
| Applications | 45m | Keep `/lean-apply` cadence on Fall postings. |
| Posting | 2–3h/wk | 1 post/wk on X + LinkedIn: build-in-public on the Karpathy work ("built GPT from scratch, here's what surprised me"), with code/figures. |

**Exit criteria:** GPT-from-scratch built and understood; 35+ DSA problems; Deep-ML weeks 1–4 done; experiment proposal sent; 4 posts published; TherAlign decision known.

## Phase 2 — Depth bet + flagship project (July 6 → Aug 9, 5 weeks)

| Block | Daily | What |
|---|---|---|
| Flagship | 4h | See below. |
| DSA | 1.5h | Maintain ~6/wk, mediums, mixed patterns. |
| System design | 1h | Alternate days: classic SD (Alex Xu Vol 1 / HelloInterview) and ML system design (your tracker's case list: recsys, search ranking, fraud). |
| Applications | 45m | Continue. Early postings start late July. |
| Posting | 1–2/wk | Project milestones with artifacts: eval charts, throughput benchmarks, kernel speedups. |

**Flagship: persona-model post-training pipeline** (research project = portfolio project):

1. Week 1: nanochat — read the whole repo, run scaled-down; understand tokenizer → pretrain → SFT → RL → inference end to end.
2. Weeks 2–3: SFT + LoRA/QLoRA an open-weight model (Qwen/Llama small) on persona data; build a persona-consistency eval harness (your AutoEval experience applies directly); then a DPO pass. Use TRL + W&B — moves them from "Exposure" to "Strong."
3. Week 4: Serve it with vLLM; measure throughput/latency/batching; compare quantized vs not. Small CUDA/Triton dose: srush GPU-Puzzles + Triton-Puzzles, write 2–3 kernels (softmax, fused ops). Goal: conversant, not kernel engineer.
4. Week 5: Write-up (blog-style README with figures), demo, share with PhD student as the research baseline. Ship 1–2 small OSS PRs along the way (vLLM/TRL/nanochat — docs or good-first-issue is a fine start).

**Exit criteria:** fine-tuned + DPO'd model with eval harness, served on vLLM with numbers; public write-up; 1+ merged/open PR; 30 more DSA problems; 8 system-design cases done.

## Phase 3 — Application season + interview mode (Aug 10 → Sept 15, 5 weeks)

Postings for Fall internships and 2027 new-grad open Aug–Oct and are **rolling** — applying day-of matters more than anything else in this phase.

- **Resume refresh first** (Aug 10–12): run `/refresh-factbase` + `/refresh-base-resumes` with summer work (flagship, TherAlign if it happened, research). CUDA/vLLM/LoRA/DPO move into Skills as project-backed claims.
- **Apply daily** via `/lean-apply` — monitor SimplifyJobs New-Grad + intern repos every morning; same-day applications.
- **Interview drills take over the depth-work hours:** 2–3 mock interviews/wk (peers/Pramp), ML breadth question drills, 2 ML system design cases/wk, behavioral bank redo (Amazon LP lessons — 2 stories per LP).
- DSA: 1.5h/day, now including 2 timed mock sessions/wk (2 mediums in 35 min).
- Research: if the PhD project landed, it gets a fixed 8–10h/wk block and continues into Fall — it's your differentiator for Applied Scientist roles.
- Posting: continue 1/wk; pin flagship on GitHub profile + LinkedIn featured.

**Exit criteria:** 50+ Fall/new-grad applications in; 10+ mocks done; can do a full ML system design case in 45 min; behavioral bank complete.

---

## Default day (Phases 1–2)

```
Morning   2.0h  DSA cold solves (hardest thing first)
          2.5h  Depth work (Karpathy / flagship)
Afternoon 1.5h  Depth work continued
          1.0h  ML breadth (Deep-ML / CS689 / papers)
Evening   0.75h Applications (/lean-apply)
          0.75h Posting, networking, outreach, daily log
= ~8.5h core; flex up to 10h goes to depth work, never to more passive video.
```

## Rules

1. One depth bet. No new niche until the flagship ships.
2. Build > watch. Nothing counts as "learned" without code you wrote.
3. Everything ships publicly — a thing that isn't posted/pushed doesn't exist for recruiters.
4. Applications never pause. Rolling deadlines reward speed, not perfection.
5. If TherAlign converts to a summer role, compress depth blocks (work hours replace them) but keep DSA + applications daily — the plan flexes, the priorities don't.
6. Track weekly: DSA count, depth milestone, posts, applications. If two weeks slip, cut scope (drop CUDA dose first, then system design depth) — never cut DSA or applications.
