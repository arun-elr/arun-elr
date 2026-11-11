<h1 align="center">Hi, I'm Arunkumar Eli</h1>

<p align="center">
  <strong>Real-time inference @ Meta Superintelligence Labs</strong> · San Francisco<br>
  Distributed Inference / Training | RL | Robotics
</p>

---

### About me

I work on real-time inference at Meta Superintelligence Labs, which I joined through the WaveForms AI acquisition. I built the real-time inference stack behind full-duplex voice in Muse Realtime Voice ([Bringing Your Muse to Life](https://research.meta.ai/blog/bringing-your-muse-to-life)).

Before that:

- **WaveForms AI:** distributed training infrastructure for 1,000+ GPUs across data centers.
- **Kumo** (acquired by NVIDIA): platform, cloud and security for Graph ML, on-prem and SaaS.
- **Founding teams** at Grainite (acquired by MongoDB) and Lacework: infrastructure, security and compliance.

In open source I work on inference engines end to end: CUDA-graph capture and piecewise replay, continuous and dynamic batching, paged KV-cache admission and eviction under memory pressure, zero-copy tensor transport between workers over shared-memory arenas and Mooncake RDMA, tensor-parallel lockstep execution, and control-plane hardening.

### Latest OSS contributions

**Agent infrastructure and reliability**

- **TorchRL** — agent state stays correct after a tool call: `IncrementalTokenizer`'s prompt tokens kept in sync with tool results ([#4674](https://github.com/pytorch/rl/pull/4674))
- **AgentENV** — agent gateway reliability: close slow and idle HTTP client connections ([#455](https://github.com/kvcache-ai/AgentENV/pull/455))
- **verl** — keep the prompt out of an empty tool-agent-loop response ([#8479](https://github.com/verl-project/verl/pull/8479))
- **M\*** — LiveKit voice agent over one session: STT, LLM and TTS ([#476](https://github.com/mstar-project/mstar/pull/476))

**Secure distributed infrastructure**

- **M\*** — removed unsafe pickle serialization from the control plane, closing an unauthenticated RCE ([#407](https://github.com/mstar-project/mstar/pull/407))
- **M\*** — secure model loading, without executing checkpoint repository code ([#654](https://github.com/mstar-project/mstar/pull/654))
- **M\*** — API authentication across serving endpoints ([#626](https://github.com/mstar-project/mstar/pull/626))
- **M\*** — refuse a socket or upload directory as a runtime directory ([#617](https://github.com/mstar-project/mstar/pull/617)); allowlisted remote media fetch ([#645](https://github.com/mstar-project/mstar/pull/645)); worker and decoder error text kept out of client responses ([#646](https://github.com/mstar-project/mstar/pull/646))

**Model evaluation and observability**

- **M\*** — unified evaluation framework: one runner, a results schema, and TTS, ASR and full-duplex suites ([#502](https://github.com/mstar-project/mstar/pull/502))
- **M\*** — LLM-based evaluation with measured judge agreement, on a Full-Duplex-Bench v1.5 suite ([#520](https://github.com/mstar-project/mstar/pull/520))
- **M\*** — Prometheus inference metrics across the API server, conductor, workers and transport, with a Grafana dashboard ([#736](https://github.com/mstar-project/mstar/pull/736) to [#755](https://github.com/mstar-project/mstar/pull/755))
- **M\*** — base vs PR regression matrix across GPUs, transports, stress and perceptual quality ([#571](https://github.com/mstar-project/mstar/pull/571))

**Inference and reinforcement learning**

- **M\*** — GPU batching and memory-pressure recovery: a refused admit unwinds exactly what it reserved ([#561](https://github.com/mstar-project/mstar/pull/561)), the engine recovers without stranding requests ([#560](https://github.com/mstar-project/mstar/pull/560)), and a refused batch retries smaller when nothing can be evicted ([#651](https://github.com/mstar-project/mstar/pull/651))
- **vLLM-Omni** — copy-on-write KV-cache session forking for AR-diffusion ([#4909](https://github.com/vllm-project/vllm-omni/pull/4909))
- **M\*** — hot weight reload for RL rollouts: pause and drain across ranks ([#845](https://github.com/mstar-project/mstar/pull/845)), with the weight version stamped on every output ([#942](https://github.com/mstar-project/mstar/pull/942))
- **TorchRL** — GSPO reinforcement learning loss for LLM post-training ([#4653](https://github.com/pytorch/rl/pull/4653))
- **vLLM** — priority scheduling: preempt running requests for higher-priority ones at `max_num_seqs` ([#45561](https://github.com/vllm-project/vllm/pull/45561))
- **RLinf** — prefetch embodied micro-batches to the device during the update loop ([#1788](https://github.com/RLinf/RLinf/pull/1788))

**Inference performance**

- **M\*** — 2.3x faster streaming Wan VAE decode ([#425](https://github.com/mstar-project/mstar/pull/425)) and 1.74x on Wan 2.2 with the same decoder ([#437](https://github.com/mstar-project/mstar/pull/437)); Qwen3-Omni streams audio after 12 frames instead of 25 ([#443](https://github.com/mstar-project/mstar/pull/443)); faster first audio for VoxCPM2 and Qwen3-TTS through CUDA-graph capture ([#659](https://github.com/mstar-project/mstar/pull/659), [#661](https://github.com/mstar-project/mstar/pull/661)); no per-step host sync in the denoise loops of Cosmos3, Wan 2.2 and OmniVoice ([#453](https://github.com/mstar-project/mstar/pull/453))
- **Mooncake** — check every task in `transfer_check_status` ([#4913](https://github.com/kvcache-ai/Mooncake/pull/4913))

**Robot learning and embodied RL**

- **LeRobot** — pi0.5 denoise: read-only prefix cache and opt-in CUDA graph, 154 to 56 ms per chunk on one H200 at the same LIBERO success rate ([#5152](https://github.com/huggingface/lerobot/pull/5152), [#5153](https://github.com/huggingface/lerobot/pull/5153)); the same for pi0 ([#5188](https://github.com/huggingface/lerobot/pull/5188)) and GR00T N1.7 ([#5186](https://github.com/huggingface/lerobot/pull/5186)); ACT with SDPA attention and a channels-last backbone ([#5190](https://github.com/huggingface/lerobot/pull/5190))
- **RLinf** — gym-aloha env and LeRobot ACT eval ([#1786](https://github.com/RLinf/RLinf/pull/1786)); eval against running action servers ([#1751](https://github.com/RLinf/RLinf/pull/1751))

**Biology and chemistry**

- **OpenFold-3** — opt-in CUDA graph for the diffusion denoising step ([#500](https://github.com/aqlaboratory/openfold-3/pull/500))
- **scientific-agent-skills** — retrosynthesis skill for AiZynthFinder route planning ([#361](https://github.com/K-Dense-AI/scientific-agent-skills/pull/361))

**Training infrastructure**

- **Megatron-LM** — log only the configured MoE load-balancing losses ([#8809](https://github.com/NVIDIA/Megatron-LM/pull/8809))
- **DeepSpeed** — report `train_loss` to monitors again ([#8971](https://github.com/deepspeedai/DeepSpeed/pull/8971))
- **torchtitan** — skip the pipeline-parallel loss-visibility hint when `LOG_RANK` is unset ([#5724](https://github.com/pytorch/torchtitan/pull/5724))
- **Liger-Kernel** — GRPO: keep the Triton gradient when `delta < 1 + epsilon_high` ([#1583](https://github.com/linkedin/Liger-Kernel/pull/1583)); mask the LUSPO loss elementwise to match TRL ([#1582](https://github.com/linkedin/Liger-Kernel/pull/1582))

### Tech

<p align="center">
  <img src="https://img.shields.io/badge/PyTorch-EE4C2C?style=for-the-badge&logo=pytorch&logoColor=white"/>
  <img src="https://img.shields.io/badge/CUDA-76B900?style=for-the-badge&logo=nvidia&logoColor=white"/>
  <img src="https://img.shields.io/badge/vLLM-30A2FF?style=for-the-badge&logoColor=white"/>
  <img src="https://img.shields.io/badge/Ray-028CF0?style=for-the-badge&logo=ray&logoColor=white"/>
  <img src="https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white"/>
  <img src="https://img.shields.io/badge/Rust-000000?style=for-the-badge&logo=rust&logoColor=white"/>
  <img src="https://img.shields.io/badge/Kubernetes-326CE5?style=for-the-badge&logo=kubernetes&logoColor=white"/>
  <img src="https://img.shields.io/badge/Prometheus-E6522C?style=for-the-badge&logo=prometheus&logoColor=white"/>
</p>

---

### Portfolio

**[retrolm.xyz](https://retrolm.xyz)** — small fine-tuned models for single-step retrosynthesis, and the stack that serves them.

On 500 held-out USPTO-50K reactions, a 1.7B with test-time augmentation reaches 56.0% top-1 and 93.0% top-10, against 53.6% and 85.2% for Claude Opus 5.5 at medium reasoning: top-10 significantly ahead (p < 0.0001), top-1 not a significant difference (p = 0.30). A 0.6B answers in 0.21 s at $0.07 per 1,000 molecules, 23 to 90 times faster per request and 110 to 900 times cheaper than the frontier models it is measured against. Given the same training data at inference, where the LLMs may search all 40,008 training reactions while answering, the 1.7B is still ahead on top-10 (92.8% against 90.0%) at about 23 times lower cost. Evaluation is exact-match on the same reactions for every model, with training-overlap checks.

The playground serves those weights on Kubernetes: a FastAPI gateway streaming one-step proposals over SSE from vLLM and SGLang, Redis for caching, rate limits and the route queue, and a planner worker running Retro* search over a 23M-compound building-block stock, streaming every expansion back to the page. The published benchmark is open; running models live is invite-only.
