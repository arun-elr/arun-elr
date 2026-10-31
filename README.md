<h1 align="center">Hi, I'm Arunkumar Eli</h1>

<p align="center">
  <strong>Real-time inference @ Meta Superintelligence Labs</strong> · San Francisco<br>
  Real-time multimodal inference: CUDA graphs, batching and KV cache under memory pressure, and the RL and robotics stacks that run on them
</p>

---

### About me

I work on real-time inference at Meta Superintelligence Labs, which I joined through the WaveForms AI acquisition. I built the real-time inference stack behind full-duplex voice in Muse Realtime Voice ([Bringing Your Muse to Life](https://research.meta.ai/blog/bringing-your-muse-to-life)).

Before that:

- **WaveForms AI:** distributed training infrastructure for 1,000+ GPUs across data centers.
- **Kumo** (acquired by NVIDIA): platform, cloud and security for Graph ML, on-prem and SaaS.
- **Founding teams** at Armorblox (acquired by Cisco), Grainite (acquired by MongoDB) and Lacework: infrastructure, security and compliance.

In open source I work on inference engines end to end: CUDA-graph capture and piecewise replay, continuous and dynamic batching, paged KV-cache admission and eviction under memory pressure, zero-copy tensor transport between workers over shared-memory arenas and Mooncake RDMA, tensor-parallel lockstep execution, and control-plane hardening.

### M\*, the multimodal inference engine

Core contributor to [M\*](https://github.com/mstar-project/mstar).

- **Performance:** 2.3x faster streaming Wan VAE decode ([#425](https://github.com/mstar-project/mstar/pull/425)) and 1.74x on Wan 2.2 with the same decoder ([#437](https://github.com/mstar-project/mstar/pull/437)); Qwen3-Omni streams audio after 12 frames instead of 25 ([#443](https://github.com/mstar-project/mstar/pull/443)); faster first audio for VoxCPM2 and Qwen3-TTS through CUDA-graph capture ([#659](https://github.com/mstar-project/mstar/pull/659), [#661](https://github.com/mstar-project/mstar/pull/661)); no per-step host sync in the denoise loops of Cosmos3, Wan 2.2 and OmniVoice ([#453](https://github.com/mstar-project/mstar/pull/453)).
- **Batching and KV cache under memory pressure:** a refused admit unwinds exactly what it reserved ([#561](https://github.com/mstar-project/mstar/pull/561)), the engine recovers without stranding requests ([#560](https://github.com/mstar-project/mstar/pull/560)), and a refused batch retries smaller when nothing can be evicted ([#651](https://github.com/mstar-project/mstar/pull/651)). A full `/dev/shm`, a late message or one failed request no longer takes down the server or the batch ([#546](https://github.com/mstar-project/mstar/pull/546), [#557](https://github.com/mstar-project/mstar/pull/557), [#559](https://github.com/mstar-project/mstar/pull/559)).
- **Voice:** Fish Audio S2-Pro ([#492](https://github.com/mstar-project/mstar/pull/492)) and Fun-CosyVoice3 ([#495](https://github.com/mstar-project/mstar/pull/495)) voice cloning, Meta Omnilingual ASR in 1,600+ languages ([#515](https://github.com/mstar-project/mstar/pull/515)), server and semantic turn detection for `/v1/realtime` ([#669](https://github.com/mstar-project/mstar/pull/669), [#672](https://github.com/mstar-project/mstar/pull/672)), AudioSeal watermarking ([#469](https://github.com/mstar-project/mstar/pull/469)).
- **World models:** LingBot-World-V2 camera-controlled image-to-world ([#455](https://github.com/mstar-project/mstar/pull/455)) and Cosmos3-Edge streamed-rollout fixes ([#622](https://github.com/mstar-project/mstar/pull/622)).
- **Security:** removed pickle from the control-plane wire, closing an unauthenticated RCE ([#407](https://github.com/mstar-project/mstar/pull/407)); optional API key on every route ([#626](https://github.com/mstar-project/mstar/pull/626)); models load without running checkpoint repo code ([#654](https://github.com/mstar-project/mstar/pull/654)); about 20 more hardening and denial-of-service fixes (request size and media limits, file permissions, upload cleanup, CVE floors).
- **Observability and evals:** Prometheus metrics across the API server, conductor, workers and transport with a Grafana dashboard ([#736](https://github.com/mstar-project/mstar/pull/736) to [#755](https://github.com/mstar-project/mstar/pull/755)); an eval framework ([#502](https://github.com/mstar-project/mstar/pull/502)) with a Full-Duplex-Bench suite ([#520](https://github.com/mstar-project/mstar/pull/520)); a base vs PR regression matrix across GPUs, transports, stress and perceptual quality ([#571](https://github.com/mstar-project/mstar/pull/571)).

### Robot learning, RL and inference engines

- **[LeRobot](https://github.com/huggingface/lerobot):** pi0.5 denoise: read-only prefix cache and opt-in CUDA graph, 154 to 56 ms per chunk on one H200 at the same LIBERO success rate ([#5148](https://github.com/huggingface/lerobot/issues/5148), [#5152](https://github.com/huggingface/lerobot/pull/5152), [#5153](https://github.com/huggingface/lerobot/pull/5153))
- **[TorchRL](https://github.com/pytorch/rl):** GSPO loss for LLM post-training ([#4653](https://github.com/pytorch/rl/pull/4653)); LeRobot policy loading fix ([#4651](https://github.com/pytorch/rl/pull/4651))
- **[RLinf](https://github.com/RLinf/RLinf):** Robotics test reliability ([#1750](https://github.com/RLinf/RLinf/pull/1750)); ALOHA env and LeRobot ACT eval ([#1786](https://github.com/RLinf/RLinf/pull/1786)); eval against running action servers ([#1751](https://github.com/RLinf/RLinf/pull/1751))
- **[M\*](https://github.com/mstar-project/mstar):** Pause, drain and hot weight reload for RL rollouts ([#845](https://github.com/mstar-project/mstar/pull/845))
- **[vLLM-Omni](https://github.com/vllm-project/vllm-omni):** Copy-on-write KV session fork for AR-diffusion ([#4909](https://github.com/vllm-project/vllm-omni/pull/4909)); action-conditioned robot world model ([#4904](https://github.com/vllm-project/vllm-omni/pull/4904))
- **[vLLM](https://github.com/vllm-project/vllm):** Priority scheduling: preempt for higher-priority requests at max_num_seqs ([#45561](https://github.com/vllm-project/vllm/pull/45561))
- **[Mooncake](https://github.com/kvcache-ai/Mooncake):** Check every task in `transfer_check_status` ([#4913](https://github.com/kvcache-ai/Mooncake/pull/4913))

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
