# Summer 2026 — Week-by-Week Learn & Build Checklist

Companion to `SUMMER_PLAN_2026.md` (strategy). This is the tracking doc — check boxes, move things between weeks freely, but don't add new topics without removing something.

**Honest starting point (your words):** CS689 work and AutoEval were vibe-coded — ~0 deep understanding. AgenticSearch understood at layer level. So Phase 1 assumes you're learning ML for real for the first time, and every phase includes "re-own a resume project" tasks — because interviewers WILL probe your resume and right now you can't defend it.

**CUDA is Week 9.** It's deliberately late: kernels make no sense until you've trained and served models yourself.

**On IoT/hardware for RL:** skip hardware — it adds shipping/wiring/debug time that teaches no ML. Sims (gymnasium) give the same RL learning with better visuals to post. The one fun hardware-ish project that IS on-bet: running a quantized LLM on a Raspberry Pi/old laptop (it's an inference/quantization project — see fun-build menu).

---

## Recurring every week (not repeated below)

- [ ] DSA daily ~2h (topic per week listed below), log count
- [ ] Applications via `/lean-apply` ~45m/day, never pauses
- [ ] 1 post on X + LinkedIn (the week's build IS the content)
- [ ] Daily one-line log: what shipped

---

## WEEK 0 — Jun 10–14 (this week)

- [ ] TherAlign final round prep + interview (top priority)
- [ ] Message PhD student: "restarting persona-model idea, meeting in 2 weeks with proposal"
- [ ] Word Break II cold, then family: LC 139, 140, 131, 93, 39, 40, 79
- [ ] Set up: gymnasium + PyTorch env, W&B account, daily log file
- [ ] Skim `SUMMER_PLAN_2026.md` rules section once more

## PHASE 1 — ML FOUNDATIONS FOR REAL (Weeks 1–4)

### Week 1 — Jun 15–21 · Backprop until it's boring

Learn:
- [ ] Karpathy Zero to Hero #1: micrograd (code along, every line typed)
- [ ] 3B1B Essence of Calculus eps 1–4 (chain rule intuition only)
- [ ] Derive by hand on paper: gradient of MSE through a 2-layer net; gradient of softmax+cross-entropy
- [ ] Concepts to be able to explain out loud: loss function, gradient descent, learning rate, train/val/test split, overfitting

Build:
- [ ] Extend your micrograd: add tanh/relu/exp ops + train a tiny MLP on a toy 2D dataset, plot decision boundary
- [ ] Deep-ML sheet Week-1 rows (linear algebra, NumPy fluency)

DSA (topic: arrays/strings/hashing + finish DP-backtracking family):
- [ ] 8 problems cold; redo Word Break II from blank file

Re-own resume:
- [ ] Write 1-page "defense doc": CS689 HW3 autodiff — what a computation graph is, what topological-sort backprop does, why. (You claimed it; now own it. micrograd IS this homework.)

Post idea: "I rebuilt backprop from scratch — 3 things that finally clicked"

### Week 2 — Jun 22–28 · From neurons to language models

Learn:
- [ ] Zero to Hero #2–4: makemore bigram → MLP → activations/BatchNorm
- [ ] Probability basics: random variables, expectation, conditional prob, MLE (StatQuest or Blitzstein lectures — pick one, 2–3 hrs max)
- [ ] Explain out loud: why cross-entropy = MLE, what an embedding is, vanishing gradients, why BatchNorm

Build:
- [ ] makemore trained on a dataset YOU pick (Indian first names? Pokémon? startup names) — sample outputs
- [ ] Deep-ML Week-2 rows (probability/statistics)

DSA (topic: two pointers + sliding window):
- [ ] 8 problems cold

Re-own resume:
- [ ] Defense doc: AgenticSearch — diagram every layer, explain extraction/verification/provenance flow without looking at code

Post idea: the generated-names sampler with funniest outputs + what BatchNorm actually does

### Week 3 — Jun 29–Jul 5 · Attention and GPT

Learn:
- [ ] Zero to Hero #5–6: WaveNet, "Let's build GPT from scratch"
- [ ] Attention math on paper: write Q,K,V; compute one attention head by hand for a 3-token example
- [ ] Explain out loud: self-attention, multi-head, positional encoding, causal masking, why transformers beat RNNs

Build:
- [ ] Train nanoGPT-style mini-GPT on a fun corpus (your own X/WhatsApp export, Shakespeare, anime subs) — share samples
- [ ] Deep-ML Week-3 rows

DSA (topic: trees + BFS/DFS):
- [ ] 8 problems cold

Re-own resume:
- [ ] Defense doc: AutoEval — read your own repo top to bottom, write what it evaluates, how, and what "anti-Goodharting" means there. If you can't reconstruct it, rewrite the resume bullet to what you CAN defend (truth hierarchy applies)

Post idea: "I trained GPT on <corpus> — here's what it learned"

### Week 4 — Jul 6–12 · Tokenizers, optimizers, classical ML + research proposal

Learn:
- [ ] Zero to Hero tokenizer video (BPE)
- [ ] Optimizers: implement SGD, momentum, Adam from scratch; compare on same net (this re-owns CS689 HW4)
- [ ] Classical ML for interviews: logistic regression, k-means, decision trees — concept + from-scratch NumPy implementation of first two
- [ ] Regularization: L2, dropout, early stopping — when/why
- [ ] Read 5–6 persona/character-model papers (Character-LLM, RoleBench, persona-consistency evals) — notes per paper

Build:
- [ ] BPE tokenizer from scratch on your corpus
- [ ] Deep-ML Week-4 rows
- [ ] 1-page experiment proposal → send to PhD student, book meeting

DSA (topic: graphs + heaps):
- [ ] 8 problems cold

**Phase 1 exit check:** can you whiteboard-explain backprop, attention, BPE, Adam, overfitting? Can you implement logistic regression cold in 20 min? If no → repeat the weak week before moving on; push everything right.

## PHASE 2 — POST-TRAINING DEPTH + FLAGSHIP (Weeks 5–9)

### Week 5 — Jul 13–19 · Fine-tuning for real

Learn:
- [ ] HuggingFace ecosystem hands-on: datasets, transformers, Trainer loop (their LLM course chapters, code-along)
- [ ] What SFT actually is; chat templates; instruction datasets
- [ ] LoRA paper §1–3 + concept: why low-rank adapters work

Build:
- [ ] Full fine-tune Qwen2.5-0.5B on a small instruction dataset (Colab/Lightning/cloud GPU)
- [ ] Same task with LoRA → compare loss curves + GPU memory in W&B; this chart is the post

DSA (topic: DP round 2 — 1D/2D classics):
- [ ] 6 problems cold

Post idea: "Full fine-tune vs LoRA on a 0.5B model — actual numbers"

### Week 6 — Jul 20–26 · Flagship part 1: persona SFT + eval harness

Build (flagship is the main block all week):
- [ ] Persona dataset: pick a character, build/curate dialogue data (synthetic generation + filtering is fine — document it)
- [ ] QLoRA fine-tune a 1.5–3B model into the persona
- [ ] Persona-consistency eval harness: held-out probes, LLM-as-judge + simple metrics — design it yourself first, then compare with papers (this re-owns the AutoEval idea for real)
- [ ] Meet PhD student with proposal + first results

Learn:
- [ ] Eval metrics: win-rate, judge bias, contamination — why evals are hard

DSA (topic: intervals + greedy):
- [ ] 6 problems cold

Post idea: first persona-bot conversation screenshots + eval design

### Week 7 — Jul 27–Aug 2 · Preference tuning + RL (the fun week)

Learn:
- [ ] RLHF overview: reward models, PPO concept (no math grind), then why DPO skips RL
- [ ] DPO paper §1–4
- [ ] RL basics via doing (below), not theory

Build:
- [ ] DPO pass on persona model with TRL (preference pairs: in-character vs out-of-character) → measure eval delta
- [ ] FUN: PPO on CartPole then LunarLander with gymnasium + stable-baselines3, record gifs — this is your RL portfolio piece, no IoT needed
- [ ] Stretch fun: PPO agent plays Snake/Flappy Bird (custom env) — extremely postable

DSA (topic: binary search + variants):
- [ ] 6 problems cold

Post idea: LunarLander landing gif thread — "I taught a neural net to land a rocket this week"

### Week 8 — Aug 3–9 · Inference & serving

Learn:
- [ ] vLLM: PagedAttention idea, continuous batching — read docs + one blog deep-dive
- [ ] Quantization: GGUF/AWQ/4-bit — what's actually lost

Build:
- [ ] Serve persona model on vLLM; benchmark throughput/latency vs naive transformers generate; quantized vs not — table of numbers
- [ ] Simple chat UI demo (you have full-stack skills; keep it to 1 day)
- [ ] FUN option: quantized small model running on a Raspberry Pi / old laptop ("local LLM" post)

DSA (topic: linked lists + stacks):
- [ ] 6 problems cold; start 1 timed mock set (2 mediums / 35 min)

Re-own resume:
- [ ] Defense doc: KG2RAG + Spark ETL (one page each — these get probed in ML interviews)

Post idea: benchmark table + demo video of persona bot

### Week 9 — Aug 10–16 · CUDA/Triton week + full-stack view + resume refresh

Learn/Build (GPU):
- [ ] srush/GPU-Puzzles (all) — CUDA mental model
- [ ] Triton-Puzzles + write 2 kernels: softmax, fused bias+activation; benchmark vs PyTorch
- [ ] Read FlashAttention blog-level explanation — connect to Week 3 attention math
- [ ] Read nanochat repo end-to-end (tokenizer→pretrain→SFT→RL→inference) — the full-stack map; run scaled-down if budget allows

Ship:
- [ ] Flagship write-up: blog-style README, figures, numbers — pin on GitHub, feature on LinkedIn
- [ ] 1 OSS PR opened (TRL/vLLM/nanochat — docs/good-first-issue fine)
- [ ] **Resume refresh:** `/refresh-factbase` + `/refresh-base-resumes` — LoRA/DPO/vLLM/Triton now project-backed claims, not Exposure

DSA: 6 problems + 1 timed set

Post idea: "my Triton softmax vs PyTorch" benchmark chart

**Phase 2 exit check:** fine-tuned + DPO'd model with eval numbers, served + benchmarked, public write-up, RL gifs posted, resume refreshed. Can you explain LoRA, DPO, PagedAttention, and your own eval harness out loud?

## PHASE 3 — INTERVIEW SEASON (Weeks 10–14) · postings open, rolling — apply same-day

### Week 10 — Aug 17–23 · Application blitz + system design start

- [ ] Morning ritual: check SimplifyJobs New-Grad + intern repos, apply same-day via `/lean-apply`
- [ ] System design: Alex Xu Vol 1 chapters 1–7 + 2 designs on paper (URL shortener, rate limiter)
- [ ] ML breadth drills start: 20 questions self-quizzed from your tracker's Track 2 sheet
- [ ] DSA: 6 problems + 2 timed sets
- [ ] Behavioral: rewrite top 8 STAR stories (Amazon LP post-mortem: what failed last time)

### Week 11 — Aug 24–30 · Mocks begin

- [ ] 2 mock coding interviews (Pramp/peers)
- [ ] 2 ML system design cases from your tracker (recsys, search ranking) — 45 min each, written
- [ ] System design: caching, queues, sharding + 2 more designs
- [ ] DSA: 6 + 2 timed sets · ML breadth: 20 more questions
- [ ] Research block resumes if PhD project is live (8–10h/wk fixed)

### Week 12 — Aug 31–Sep 6

- [ ] 2–3 mocks (1 ML-focused: implement k-means/attention from scratch under time)
- [ ] 2 ML system design cases (fraud, ads CTR)
- [ ] Behavioral: 2 stories per Amazon LP, all written
- [ ] DSA: 6 + 2 timed sets · applications daily

### Week 13 — Sep 7–13

- [ ] Full loop simulation: coding + design + behavioral in one day
- [ ] Weak-area triage: whatever mocks exposed, drill only that
- [ ] 2 ML system design cases · DSA timed sets only now

### Week 14 — Sep 14–20

- [ ] Second full loop simulation
- [ ] 50+ Fall/new-grad applications cumulative — audit the tracker
- [ ] Post: summer recap thread (everything built, with links) — this is the "reach out to me" artifact

---

## Fun-build menu (pick max 1 per phase, only if week's core is done)

- [ ] Mini-GPT trained on your own chat history (W3 fits)
- [ ] PPO Snake/Flappy Bird with gameplay gifs (W7 fits)
- [ ] Quantized LLM on Raspberry Pi — "ChatGPT in my pocket" (W8 fits)
- [ ] Attention-visualizer web toy (post-W3 anytime)
- [ ] Triton kernel benchmark thread (W9 fits)
- [ ] Persona bot public demo link (W8–9)

## RESEARCH TRACK ADD-ON (added 2026-06-10 — targeting RE/AS-intern roles too)

Adds ~1.5–2h/day from Week 5. What it buys: replication skill, a paper-shaped project, and advisor setup — the things entry-level Research Engineer / Applied Scientist screens actually test. Publications come winter/spring, not September.

- [ ] **W4:** Pick 1 persona/eval paper to replicate (core experiment only); add to proposal
- [ ] **W5:** Math spine starts — 45 min/day probability + linear algebra (Math for ML / Blitzstein), every week through W14
- [ ] **W5:** Read Suryaansh's ICLR paper (LLM-judge bias) + 30-min chat — directly adjacent to your eval harness
- [ ] **W5–6:** Replication part 1 — reproduce the paper's main table/figure
- [ ] **W6:** Eval harness gets baselines + ablations (paper-shaped, not demo-shaped)
- [ ] **W7:** Finish replication → publish 1-page replication report (this is a post AND a credential)
- [ ] **W8:** Related-work section drafted for flagship write-up
- [ ] **W9:** Flagship write-up ships paper-shaped (baselines, ablations, related work, limitations)
- [ ] **W10:** Application targets expand: RE/AS-intern postings + check residency-style programs (Amazon AS, NVIDIA, Cohere, AI2, HF)
- [ ] **W11:** Build + rehearse a 10-min research talk on the flagship (slides)
- [ ] **W12:** Fall setup: enroll RL course (Bruno Castro Da Silva), fix PhD-project weekly block, identify 2nd prof (AI-alignment / AI-for-SE)
- [ ] **W14:** Workshop-target shortlist + winter submission timeline with PhD student

## MARKET-CHECK ADDITIONS (added 2026-06-10 — from auditing all 66 applied JDs + current postings)

Verdict: plan already covers ~80% of what JDs ask. Four surgical additions, no new tracks:

- [ ] **W8 (stretch):** C++ refresh — redo 5 already-solved LC problems in C++ (C++ in 29% of JDs, 64% of SRE-family; you have CS690PF base, just rusty syntax)
- [ ] **W8 (stretch):** LoRA fine-tune a small VLM (Qwen2-VL-2B) — image persona/captioning, 2–3 days cap (multimodal in 23% of JDs, plan had zero)
- [ ] **W9 (core):** Write 2 kernels in raw CUDA C++ (vector add, tiled matmul) alongside Triton — makes "CUDA" a truthful project-level claim for NVIDIA-class roles
- [ ] **W10 (core):** SQL brush-up half-day — joins, window functions (SQL in 30% of JDs)

Explicitly REJECTED after the audit: Go (20% of JDs but SDE-generalist noise — Python carries those interviews), Java depth, Terraform/Ansible (6%), Kafka depth (5%), mobile, Angular. Language-chasing is how summers die.

**Round 2 — internet-wide scan (big-tech minimums, AS/lab postings, AI-engineer + inference market):**

- [ ] **W6 (core):** Eval harness ships with versioned eval set + numerical score + regression gate — eval literacy is the #1 "actually built with LLMs" hiring signal in 2026
- [ ] **W8 (core):** Inference mechanics deep-dive — KV cache, continuous batching, speculative decoding (what NVIDIA LLM-performance new-grad JDs probe)
- [ ] **W8 (core, 1-day cap):** Wrap persona bot as an MCP server — MCP is on the 2026 AI-engineer checklist; you have Exposure only
- [ ] **W9 (stretch, 1-day cap):** Tracing + cost/token dashboard on persona bot — production observability + cost optimization are screened for

Round-2 findings that need no new tasks: Amazon AS-intern is MS-eligible with publications only *preferred* (research track already fits); big-tech SDE intern minimums are just one language + DSA (covered); your Wysa production background + AgenticSearch provider-routing already cover the "production reliability / cost routing" checklist items — defense docs make them defendable.

## Adjustment rules

1. Slipping? Cut from the bottom: fun-builds first, then CUDA depth, then system-design count, then replication scope. Never cut DSA, applications, or flagship.
2. Each phase exit check is a gate — failing it means repeat, not skip.
3. If TherAlign converts: work replaces depth blocks; DSA + applications + 1 post/wk survive.
4. Anything vibe-coded from now on doesn't count. If Claude wrote it, you re-explain it in the defense doc or it's not "learned."
