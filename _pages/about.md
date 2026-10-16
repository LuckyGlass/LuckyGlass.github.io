---
layout: about
title: About
permalink: /
subtitle: <a href="https://sai.pku.edu.cn/znxyenglish">School of Intelligence Science and Technology</a>. Peking University.

profile:
  align: right
  image: prof_pic.jpg
  image_circular: true # crops the image to make it circular
  more_info: >
    <p>Peking University</p>
    <p>Beijing, China</p>
    <p class="profile-social">
      <a class="ps-icon" href="mailto:ysmao_lumen@outlook.com" aria-label="Email"><i class="fa-solid fa-envelope"></i></a>
      <span class="ps-sep">|</span>
      <a href="mailto:ysmao_lumen@outlook.com">ysmao_lumen@outlook.com</a>
    </p>
    <p class="profile-social">
      <a class="ps-icon" href="https://github.com/LuckyGlass" aria-label="GitHub" target="_blank" rel="noopener noreferrer"><i class="fa-brands fa-github"></i></a>
      <span class="ps-sep">|</span>
      <a href="https://github.com/LuckyGlass" target="_blank" rel="noopener noreferrer">github.com/LuckyGlass</a>
    </p>

selected_papers: false # includes a list of papers marked as "selected={true}"
social: false # includes social icons at the bottom of the page

announcements:
  enabled: true # includes a list of news items
  scrollable: true # adds a vertical scroll bar if there are more than 3 news items
  limit: 5 # leave blank to include all the news in the `_news` folder

latest_posts:
  enabled: true # includes a list of blog posts
  scrollable: true # adds a vertical scroll bar if there are more than 3 new posts items
  limit: 3 # leave blank to include all the blog posts
---

Yansheng Mao is a Ph.D. student in the School of Intelligence Science and Technology at Peking University, advised by [Muhan Zhang](https://muhanzhang.github.io/) in [Μμ Lab](https://mulabpku.com/). He studies large language models, especially training infrastructure.

He received his bachelor's degree from the School of Electronics Engineering and Computer Science at Peking University in 2026, where he was a member of the Zhi Class, a special class for excellent students majoring in artificial intelligence, and was awarded the Zhi Class scholarship in 2024 and 2025.

Since its founding in 2026, he has also been a member of the founding team of Norizon (无涯智远), an early-stage AI startup in Beijing, where he is responsible for the company's training infrastructure and is the primary author of all of its training frameworks.

## Research Interests

<div class="about-interests">
  <div class="about-interest-card">
    <h3>Training Infrastructure</h3>
    <p>
      I work on the systems side of large model training: training frameworks, the parallelism strategies
      (data, tensor, sequence, context, and expert parallelism) that scale training across GPU clusters, and
      the high-performance kernels underneath them. At Norizon, I design and build these systems for the
      company's model training — see <a href="#training-frameworks-at-norizon">Training Frameworks</a> below.
    </p>
  </div>

  <div class="about-interest-card">
    <h3>Recursive Self-Improvement (RSI)</h3>
    <p>
      Models that keep learning after deployment, internalizing verified experience into parameters as reusable
      capabilities (in-parameter learning), with improved capability in turn accelerating further learning. I'm
      interested in making this loop near real time — e.g., hypernetworks that generate weight updates in a
      single forward pass — and in sustaining long-term growth without forgetting or interference.
    </p>
  </div>
</div>

## Training Frameworks at Norizon

I am the primary author of Norizon's training frameworks. Three generations so far: a PyTorch/FSDP2
stack, a Megatron-Core rewrite, and a from-scratch PyTorch-native framework, the last two built solo.

<details markdown="1" class="framework-item">
  <summary>
    <strong>Gen 1 · PyTorch/FSDP2 trainer</strong> (2026.05 – 2026.10) — Ulysses sequence parallelism ·
    Muon/AdamW optimization.
  </summary>

  My role: top contributor; designed and owned the tensor-parallel and sequence-parallel integration.

  - Distributed trainer on PyTorch FSDP2 with HSDP (replicate × shard) meshes; multi-node training runs at 64-process scale.
  - Ulysses-style sequence parallelism for attention, reimplemented on native torch collectives and composed with FSDP sharding.
  - Custom tensor-parallel support for non-standard parameter groups, layered on HuggingFace accelerate.
  - Mixed-optimizer training (Muon + AdamW) with per-parameter routing; bf16 autocast with fp32 master weights.
  - Distributed checkpointing on `torch.distributed.checkpoint` with per-rank RNG state for exact resume.
  - TB-scale multi-machine offline data pipeline with staged rollout/rollback and tokenizer-consistency verification.
  - Kernel stack: FlashAttention-2, flash-linear-attention, Liger Kernel, and `torch.compile`.
</details>

<details markdown="1" class="framework-item">
  <summary>
    <strong>Gen 2 · Megatron-Core rewrite</strong> (2026.08 – 2026.09) — dense & MoE up to ~35B · TP/SP/DP/EP ·
    Triton/DeepGEMM grouped kernels · built solo.
  </summary>

  - Rewrote the training stack natively on Megatron-Core + Transformer Engine; imports HuggingFace checkpoints (dense and MoE) via Megatron-Bridge.
  - TP/SP/DP plus MoE expert parallelism, with auxiliary modules parallelized at their own tensor-parallel degree, independent of the backbone.
  - Custom Triton packed grouped-projection kernels — a single launch each for forward, input-gradient, and weight-gradient — plus DeepGEMM grouped BF16 GEMM.
  - Deterministic fault tolerance: coordinated replay that restores full RNG state and the data-iterator position for exact step reproduction; fully resumable distributed checkpoints.
  - Cross-framework checkpoint conversion between Megatron distributed checkpoints and safetensors.
  - Numerics discipline: tensor-parallel-invariance gates with measured bf16 drift bounds and fp32 gates at the 1e-8 level; FLOP-accurate MFU profiling and GPU telemetry.
  - Multi-node training of dense models up to ~27B and MoE models up to ~35B parameters.
</details>

<details markdown="1" class="framework-item">
  <summary>
    <strong>Gen 3 · From-scratch PyTorch-native framework</strong> (2026.09 – present) — context parallelism ·
    packed varlen training (~66% peak-memory cut) · Triton grouped GEMM · CPU-offloaded activation
    checkpointing · built solo in four weeks.
  </summary>

  - Clean-room rewrite (~9k lines of framework code plus ~18k lines of tests), developed with an agent-assisted, PR-based workflow.
  - Context parallelism over hybrid full-attention + linear-attention kernels (ring-flash-attention), with CP-aware reductions composed with FSDP gradient reduction; validated by whole-model numerical grids of hundreds of randomized trials per configuration.
  - Packed/varlen training with sequence metadata routed through every length-sensitive operator — ~66% peak-memory reduction at high-padding workloads at batched step time, backed by custom Triton grouped-GEMM kernels.
  - FSDP2/HSDP engineering: meta-device construction, rank-local streaming weight materialization from safetensors, and tied-weight ownership rules.
  - Activation checkpointing with CPU offloading (BF16) and backward prefetch; per-layer `torch.compile`.
  - Spec-driven kernel hot-swap (eager ↔ FlashAttention ↔ Liger) via operation-UID slots; single-step profiler with Chrome traces and FLOPs meta-accounting.
</details>
