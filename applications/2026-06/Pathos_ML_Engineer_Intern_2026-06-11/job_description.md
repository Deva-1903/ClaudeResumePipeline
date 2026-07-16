# Pathos — Machine Learning Engineer (Intern)

NYC HQ, hybrid (up to 3 days/week onsite).

Pathos is building a next-generation biotech with AI at the core, the largest foundation model in oncology, paired with proprietary AI systems, deep oncology expertise, and 200+ petabytes of multimodal data linked to patient outcomes. Small teams of 2-4 experts each command hundreds of AI agents. Everyone builds, everyone ships.

## About the role
Hiring Machine Learning Engineer Interns to work alongside senior researchers and engineers on high-impact projects spanning:
- Hyper-scale training & inference infrastructure
- Pre-training & post-training of multi-modal foundational models
- Knowledge Graph (KG) & Retrieval Augmented Generation (RAG)
- Evaluation of reasoning capabilities (logic, metric design, dataset curation)

## What You Will Do (depending on strengths / team needs)
- Use Nsight to profile post-training pipeline; identify what dominates wall-clock (rollout GEMM vs KV cache I/O vs weight reloading vs reward compute).
- Design an NCCL-based weight broadcast path streaming LoRA/base weights into inference engine GPU memory.
- Improve hyper-scale training throughput (sharding granularity, mixed-precision, communication overlap, gradient bucketing).
- Mixture-of-Experts training: tensor/expert/data parallel groups on H200 with InfiniBand; token vs sequence routing.
- Training stability and load balancing (aux-loss, capacity factor, drop/pad, router z-loss, expert dropout).
- SFT and RL on a pre-trained MoE (router freezing, gradient flow).
- Prefill/decode disaggregation serving; KV cache transfer over NVLink/InfiniBand; scheduling.

## Qualifications (you do not need to meet every item)
### Minimum
- Strong programming ability in Python.
- Solid ML/DL fundamentals (coursework, research, internships, or substantial projects).
- Experience with PyTorch and modern training workflows.
- Comfort in ambiguous problem spaces with a bias toward execution.
### Preferred
- Distributed systems (multi-node training, large-scale data loaders, cluster scheduling).
- Performance optimization (profiling, kernel efficiency, GPU utilization, throughput/latency).
- Research experience (papers, preprints, open-source, or significant independent work).
- Exposure to biomedical, clinical, or multimodal datasets (helpful, not required).

## What We Offer
- Thousand-scale GPU infrastructure; full-cycle multimodal foundation model training (pre to post).
- Opportunities to publish at NeurIPS, ACL, ICML. Strong candidates considered for full-time. New/recent grads encouraged.
