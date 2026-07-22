# Hugging Face Trending Models Digest 2026-07-23

> Source: [Hugging Face Hub](https://huggingface.co/) | 30 models | Generated: 2026-07-22 23:09 UTC

---

# 🤗 Hugging Face Trending Models Digest — 2026-07-23

## Today's Highlights

This week's trending models reveal a clear **shift toward ultra-lightweight and compressed architectures**, led by **zai-org/GLM-5.2** (4,334 likes) and **google/gemma-4-31B-it** (3,327 likes, 12M+ downloads). **Uncensored and vision-capable variants** of the Qwen 3.6 family dominate the fine-tune space, with **HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive** (2,998 likes, 2M downloads) and **empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF** (2,416 likes, 2.1M downloads) signaling intense community interest in edge-deployable, reasoning-focused models. The **prism-ml** team's **Bonsai** series demonstrates the viability of 1-bit and 2-bit quantization at 27B scale, while **Microsoft's Mage-Flow** and **NVIDIA's Cosmos3-Edge** mark enterprise entries into image generation and video understanding, respectively.

---

## Trending Models

### 🧠 Language Models (LLMs, Chat Models, Instruction-Tuned)

- **[zai-org/GLM-5.2](https://huggingface.co/zai-org/GLM-5.2)** — Author: zai-org | Likes: 4,334 | Downloads: 545,109  
  A 52B MoE conversational model with advanced DSA (Dynamic Sparse Attention), trending as the week's top-ranked text-generation model.

- **[google/gemma-4-31B-it](https://huggingface.co/google/gemma-4-31B-it)** — Author: google | Likes: 3,327 | Downloads: 12,113,203  
  Google's latest instruction-tuned 31B multimodal model, leading total downloads and signaling continued enterprise investment in mid-scale open-weight LLMs.

- **[moonshotai/Kimi-K2.7-Code](https://huggingface.co/moonshotai/Kimi-K2.7-Code)** — Author: moonshotai | Likes: 1,222 | Downloads: 722,058  
  A code-specialized 2.7B model with compressed tensors, reflecting growing demand for small, efficient coding assistants.

- **[poolside/Laguna-S-2.1](https://huggingface.co/poolside/Laguna-S-2.1)** — Author: poolside | Likes: 381 | Downloads: 3,056  
  A new 2.1B general-purpose text-generation model from poolside, spawning multiple quantization variants (GGUF, NVFP4) in the same week.

- **[Nanbeige/Nanbeige4.2-3B](https://huggingface.co/Nanbeige/Nanbeige4.2-3B)** — Author: Nanbeige | Likes: 223 | Downloads: 0  
  3B language model from Nanbeige, minimally trending with zero downloads—likely a fresh upload awaiting adoption.

- **[upstage/Solar-Open2-250B](https://huggingface.co/upstage/Solar-Open2-250B)** — Author: upstage | Likes: 203 | Downloads: 0  
  A massive 250B open-weight model from Upstage, signaling ambition in the large-scale open-source LLM space.

### 🎨 Multimodal & Generation (Image, Video, Audio, Text-to-X)

- **[baidu/Unlimited-OCR](https://huggingface.co/baidu/Unlimited-OCR)** — Author: baidu | Likes: 2,700 | Downloads: 2,237,351  
  A powerful OCR model supporting unlimited-length image-to-text conversion, trending for its production-grade document understanding capabilities.

- **[HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)** — Author: HauhauCS | Likes: 2,998 | Downloads: 1,997,690  
  An uncensored, vision-capable MoE variant of Qwen 3.6 with aggressive reasoning tuning, among the most downloaded models this week.

- **[empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF](https://huggingface.co/empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF)** — Author: empero-ai | Likes: 2,416 | Downloads: 2,133,420  
  A GGUF-quantized 9B vision-language reasoning model, popular for its "Mythos" Claude-distilled thinking capabilities.

- **[thinkingmachines/Inkling](https://huggingface.co/thinkingmachines/Inkling)** — Author: thinkingmachines | Likes: 1,445 | Downloads: 16,441  
  A multimodal conversational model early in its lifecycle, quickly spawning GGUF variants (unsloth/inkling-GGUF).

- **[ATH-MaaS/OvisOCR2](https://huggingface.co/ATH-MaaS/OvisOCR2)** — Author: ATH-MaaS | Likes: 249 | Downloads: 17,162  
  A Qwen 3.5-based OCR model specialized for vision document understanding, competing with baidu's Unlimited-OCR.

- **[bottlecapai/ThinkingCap-Qwen3.6-27B](https://huggingface.co/bottlecapai/ThinkingCap-Qwen3.6-27B)** — Author: bottlecapai | Likes: 510 | Downloads: 12,002  
  A 27B multimodal reasoning model built on Qwen 3.6, targeting step-by-step thinking tasks.

- **[microsoft/Mage-Flow](https://huggingface.co/microsoft/Mage-Flow)** — Author: microsoft | Likes: 115 | Downloads: 0  
  Microsoft's new text-to-image generation model, still fresh but representing enterprise expansion into diffusion-based image editing.

- **[OpenMOSS-Team/MOSS-Transcribe-Diarize](https://huggingface.co/OpenMOSS-Team/MOSS-Transcribe-Diarize)** — Author: OpenMOSS-Team | Likes: 308 | Downloads: 92,265  
  An audio-text-to-text model combining transcription and speaker diarization, trending for speech-to-text applications.

- **[nvidia/nemotron-3.5-asr-streaming-0.6b](https://huggingface.co/nvidia/nemotron-3.5-asr-streaming-0.6b)** — Author: nvidia | Likes: 914 | Downloads: 590,230  
  NVIDIA's 0.6B streaming ASR model, trending for on-device real-time speech recognition.

- **[nvidia/Cosmos3-Edge](https://huggingface.co/nvidia/Cosmos3-Edge)** — Author: nvidia | Likes: 87 | Downloads: 6,623  
  An edge-optimized video understanding model built on Cosmos architecture, showing NVIDIA's edge AI push.

### 🔧 Specialized Models (Code, Math, Medical, Embeddings)

- **[nvidia/Nemotron-3-Embed-1B-BF16](https://huggingface.co/nvidia/Nemotron-3-Embed-1B-BF16)** — Author: nvidia | Likes: 102 | Downloads: 93,021  
  A 1B sentence-embedding model leveraging Ministral3 architecture, trending for RAG and retrieval applications.

- **[conradlocke/krea2-identity-edit](https://huggingface.co/conradlocke/krea2-identity-edit)** — Author: conradlocke | Likes: 493 | Downloads: 0  
  A LoRA adapter for identity-preserving image editing built on Krea-2-Raw, notable for its ComfyUI compatibility.

- **[Motif-Technologies/Motif-3-Beta](https://huggingface.co/Motif-Technologies/Motif-3-Beta)** — Author: Motif-Technologies | Likes: 154 | Downloads: 125  
  A feature-extraction model from Motif Technologies, likely targeting embedding and search use cases.

### 🤖 Robotics & Vision-Language-Action Models

- **[openbmb/MiniCPM-RobotManip](https://huggingface.co/openbmb/MiniCPM-RobotManip)** — Author: openbmb | Likes: 154 | Downloads: 58  
  A vision-language-action model for robot manipulation tasks, representing the growing robotics-AI crossover.

- **[openbmb/MiniCPM-RobotTrack](https://huggingface.co/openbmb/MiniCPM-RobotTrack)** — Author: openbmb | Likes: 114 | Downloads: 72  
  A companion model for object tracking in robotic systems, paired with MiniCPM-RobotManip in the robotics pipeline.

### 📦 Fine-tunes & Quantizations (Community Fine-tunes, GGUF, AWQ)

- **[prism-ml/Ternary-Bonsai-27B-gguf](https://huggingface.co/prism-ml/Ternary-Bonsai-27B-gguf)** — Author: prism-ml | Likes: 937 | Downloads: 432,196  
  A 2-bit ternary GGUF quantization of a 27B model, demonstrating extreme compression viable for edge deployment.

- **[prism-ml/Bonsai-27B-gguf](https://huggingface.co/prism-ml/Bonsai-27B-gguf)** — Author: prism-ml | Likes: 593 | Downloads: 1,404,962  
  1-bit GGUF quantization of a 27B model, among the most downloaded GGUF models this week for its unprecedented compression ratio.

- **[prism-ml/Bonsai-27B-mlx-1bit](https://huggingface.co/prism-ml/Bonsai-27B-mlx-1bit)** — Author: prism-ml | Likes: 165 | Downloads: 25,273  
  The Apple Silicon (MLX) port of the 1-bit Bonsai-27B, showing cross-platform quantization demand.

- **[DavidAU/Qwen3.6-27B-Fable-Fusion-711-Uncensored-Heretic-NM-DAU-NEO-MAX-MTP-GGUF](https://huggingface.co/DavidAU/Qwen3.6-27B-Fable-Fusion-711-Uncensored-Heretic-NM-DAU-NEO-MAX-MTP-GGUF)** — Author: DavidAU | Likes: 317 | Downloads: 62,842  
  An extensively fine-tuned and uncensored GGUF variant of Qwen 3.6 with aggressive naming conventions, trending in the "heretic" fine-tune subculture.

- **[GnLOLot/MiniCPM5-1B-Claude-Opus-Fable5-V2-Thinking-GGUF](https://huggingface.co/GnLOLot/MiniCPM5-1B-Claude-Opus-Fable5-V2-Thinking-GGUF)** — Author: GnLOLot | Likes: 153 | Downloads: 51,746  
  A thinking-focused GGUF fine-tune of MiniCPM5 distilled from Claude Opus, demonstrating tiny-model reasoning.

- **[unsloth/Laguna-S-2.1-GGUF](https://huggingface.co/unsloth/Laguna-S-2.1-GGUF)** — Author: unsloth | Likes: 104 | Downloads: 0  
  Unsloth's GGUF variant of poolside's Laguna-S-2.1, ready for vLLM and community deployment.

- **[poolside/Laguna-S-2.1-GGUF](https://huggingface.co/poolside/Laguna-S-2.1-GGUF)** — Author: poolside | Likes: 90 | Downloads: 289  
  Official GGUF release of Laguna-S-2.1, region-locked to US endpoints.

- **[poolside/Laguna-S-2.1-NVFP4](https://huggingface.co/poolside/Laguna-S-2.1-NVFP4)** — Author: poolside | Likes: 88 | Downloads: 1,953  
  NVIDIA FP4 quantization of Laguna-S-2.1, targeting Hopper-generation GPU inference efficiency.

- **[unsloth/inkling-GGUF](https://huggingface.co/unsloth/inkling-GGUF)** — Author: unsloth | Likes: 120 | Downloads: 7,377  
  GGUF quantization of the Inkling multimodal model from thinkingmachines, adding MoE and audio-text-to-text support.

---

## Ecosystem Signal

The **Qwen 3.6 family** has become the dominant fine-tuning substrate this week, powering 5 of the 30 trending models (HauhauCS, DavidAU, bottlecapai, ATH-MaaS, and prism-ml's MLX variant). This reflects Qwen's strong multimodal capabilities and permissive license attracting community experimentation.

**Ultra-low-bit quantization** (1-bit, 2-bit, ternary) is the week's most significant infrastructure trend. **prism-ml's Bonsai series** demonstrates that 27B models can run on edge devices while retaining useful conversational capability, with collective downloads exceeding 1.8M across three quantization formats. This aligns with the broader industry push toward on-device AI.

**Uncensored fine-tunes** continue to be a major community driver—HauhauCS's model alone has 2M downloads. These models typically blend aggressive reasoning with minimal safety filtering, appealing to power users and roleplay communities.

On the **enterprise side**, Google's Gemma-4, NVIDIA's Nemotron/NGC pipeline, and Microsoft's Mage-Flow show that major AI labs are prioritizing **mid-scale (3B–35B) multimodal models** over 70B+ flagships, betting on distillation and quantization to bridge the capability-efficiency gap. **Poolside's Laguna-S-2.1** release with simultaneous GGUF, NVFP4, and Unsloth support suggests a new best practice: launching models with deployment infrastructure ready from day one.

The **robotics category** (MiniCPM-RobotManip/MiniCPM-RobotTrack) and **streaming ASR** (nvidia/nemotron-3.5-asr-streaming) are emerging as niche growth areas, while OCR remains a consistent high-download category driven by baidu's dominance.

---

## Worth Exploring

1. **[prism-ml/Bonsai-27B-gguf](https://huggingface.co/prism-ml/Bonsai-27B-gguf)** — The 1-bit 27B model is the most significant compression milestone this week, showing what's possible at extreme quantization levels. Essential for anyone exploring edge deployment of large models.

2. **[google/gemma-4-31B-it](https://huggingface.co/google/gemma-4-31B-it)** — With 12M+ downloads, this is the week's most adopted model. It represents Google's latest multimodal instruction-tuned offering at a competitive scale—worth studying for its architectural choices and safety tuning.

3. **[openbmb/MiniCPM-RobotManip](https://huggingface.co/openbmb/MiniCPM-RobotManip)** — As one of the few robotics-specific models on the trending leaderboard, it marks an important frontier where VLMs meet physical action. Worth exploring for anyone interested in embodied AI and vision-language-action pipelines.

---
*This digest is auto-generated by [agents-radar](https://github.com/kky-wollu/agents-radar).*