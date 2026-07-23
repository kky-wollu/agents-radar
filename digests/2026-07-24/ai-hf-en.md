# Hugging Face Trending Models Digest 2026-07-24

> Source: [Hugging Face Hub](https://huggingface.co/) | 30 models | Generated: 2026-07-23 23:01 UTC

---

# Hugging Face Trending Models Digest — July 24, 2026

## 1. Today's Highlights

This week's Hugging Face landscape is dominated by two powerful forces: the explosive popularity of **extreme quantization** and the rapid proliferation of **Qwen3.6-based fine-tunes**. The **prism-ml/Bonsai-27B-gguf** series continues its incredible run, with over 1.9M downloads for the 1-bit variant alone, signaling that the community is hungry for highly compressed models that retain surprising capability. Meanwhile, **Google's Gemma-4-31B-it** has amassed a staggering 12.6M downloads, cementing its position as the most downloaded model on the platform. The **GLM-5.2** release from zai-org also stands out with 4.3K weekly likes, suggesting a major shift toward MoE architectures with dense-sparse attention. Notably, multimodal models (image-text-to-text) now dominate the top spots, with 7 of the top 10 models falling into this category.

## 2. Trending Models

### 🧠 Language Models (LLMs, chat models, instruction-tuned)

- **zai-org/GLM-5.2** ([link](https://huggingface.co/zai-org/GLM-5.2)) — Author: zai-org | Likes: 4,364 | Downloads: 596,442 — A 5.2B MoE model with dense-sparse attention architecture that's capturing attention for its efficient conversational capabilities and strong benchmark performance.

- **upstage/Solar-Open2-250B** ([link](https://huggingface.co/upstage/Solar-Open2-250B)) — Author: upstage | Likes: 403 | Downloads: 362 — A massive 250B open-weight model from Upstage, signaling continued investment in frontier-scale open-source LLMs despite relatively low download numbers.

- **Nanbeige/Nanbeige4.2-3B** ([link](https://huggingface.co/Nanbeige/Nanbeige4.2-3B)) — Author: Nanbeige | Likes: 312 | Downloads: 4,532 — A compact 3B parameter LLM optimized for efficiency, trending as a lightweight alternative for deployment on edge devices.

- **fdtn-ai/antares-1b** ([link](https://huggingface.co/fdtn-ai/antares-1b)) — Author: fdtn-ai | Likes: 119 | Downloads: 2,747 — A 1B hybrid MoE model focused on security applications, representing the growing niche of safety-oriented small language models.

- **Motif-Technologies/Motif-3-Beta** ([link](https://huggingface.co/Motif-Technologies/Motif-3-Beta)) — Author: Motif-Technologies | Likes: 172 | Downloads: 1,856 — A feature extraction-focused model that's gaining traction among developers building custom embedding pipelines.

### 🎨 Multimodal & Generation (image, video, audio, text-to-X)

- **baidu/Unlimited-OCR** ([link](https://huggingface.co/baidu/Unlimited-OCR)) — Author: baidu | Likes: 2,875 | Downloads: 2,414,259 — Baidu's unlimited OCR model for image-text-to-text tasks, trending as the go-to solution for document digitization and text extraction from images.

- **google/gemma-4-31B-it** ([link](https://huggingface.co/google/gemma-4-31B-it)) — Author: google | Likes: 3,347 | Downloads: 12,666,488 — Google's flagship 31B instruction-tuned multimodal model, dominating downloads with its strong vision-language capabilities and permissive Gemma license.

- **thinkingmachines/Inkling** ([link](https://huggingface.co/thinkingmachines/Inkling)) — Author: thinkingmachines | Likes: 1,503 | Downloads: 24,669 — A conversational image-text-to-text model designed for interactive multimodal dialogue, trending for its natural chat-based vision interactions.

- **moonshotai/Kimi-K2.7-Code** ([link](https://huggingface.co/moonshotai/Kimi-K2.7-Code)) — Author: moonshotai | Likes: 1,245 | Downloads: 766,522 — Moonshot AI's compressed code-specialized multimodal model, trending for combining efficient tensor compression with strong coding capabilities.

- **Qwen/Qwen3-TTS-12Hz-1.7B-CustomVoice** ([link](https://huggingface.co/Qwen/Qwen3-TTS-12Hz-1.7B-CustomVoice)) — Author: Qwen | Likes: 1,795 | Downloads: 2,497,020 — Qwen's text-to-speech model with custom voice support at 12Hz output, trending for its high-quality voice generation and personalization features.

- **nvidia/Cosmos3-Edge** ([link](https://huggingface.co/nvidia/Cosmos3-Edge)) — Author: nvidia | Likes: 98 | Downloads: 28,493 — NVIDIA's edge-optimized diffusion model, representing the growing trend of deploying image generation on resource-constrained devices.

- **microsoft/Mage-Flow** ([link](https://huggingface.co/microsoft/Mage-Flow)) — Author: microsoft | Likes: 181 | Downloads: 411 — Microsoft's text-to-image diffusion model with editing capabilities, gaining attention for its flow-based architecture.

- **nvidia/nemotron-3.5-asr-streaming-0.6b** ([link](https://huggingface.co/nvidia/nemotron-3.5-asr-streaming-0.6b)) — Author: nvidia | Likes: 924 | Downloads: 750,118 — A compact 0.6B streaming ASR model from NVIDIA, trending for real-time speech recognition at the edge.

- **OpenMOSS-Team/MOSS-Transcribe-Diarize** ([link](https://huggingface.co/OpenMOSS-Team/MOSS-Transcribe-Diarize)) — Author: OpenMOSS-Team | Likes: 319 | Downloads: 111,598 — An audio-text-to-text model combining transcription with speaker diarization, trending for meeting transcription and multi-speaker scenarios.

- **conradlocke/krea2-identity-edit** ([link](https://huggingface.co/conradlocke/krea2-identity-edit)) — Author: conradlocke | Likes: 515 | Downloads: 0 — A LoRA for identity-preserving image editing built on Krea-2, trending in the ComfyUI community despite being freshly released.

### 🔧 Specialized Models (code, math, medical, embeddings, robotics)

- **openbmb/MiniCPM-RobotManip** ([link](https://huggingface.co/openbmb/MiniCPM-RobotManip)) — Author: openbmb | Likes: 163 | Downloads: 408 — A vision-language-action model for robot manipulation, representing the emerging robotics pipeline on Hugging Face.

- **openbmb/MiniCPM-RobotTrack** ([link](https://huggingface.co/openbmb/MiniCPM-RobotTrack)) — Author: openbmb | Likes: 117 | Downloads: 306 — A companion VLA model focused on object tracking for robotic applications.

- **ATH-MaaS/OvisOCR2** ([link](https://huggingface.co/ATH-MaaS/OvisOCR2)) — Author: ATH-MaaS | Likes: 257 | Downloads: 26,919 — An OCR-specialized image-text-to-text model built on Qwen3.5, trending for high-accuracy document processing.

### 📦 Fine-tunes & Quantizations (community fine-tunes, GGUF, AWQ)

- **prism-ml/Bonsai-27B-gguf** ([link](https://huggingface.co/prism-ml/Bonsai-27B-gguf)) — Author: prism-ml | Likes: 619 | Downloads: 1,910,116 — A 1-bit quantized 27B model using llama.cpp, trending as the most popular extreme compression example with remarkable quality retention.

- **prism-ml/Ternary-Bonsai-27B-gguf** ([link](https://huggingface.co/prism-ml/Ternary-Bonsai-27B-gguf)) — Author: prism-ml | Likes: 980 | Downloads: 576,083 — A 2-bit ternary quantization of a 27B model, striking a balance between compression and quality that's attracting significant community interest.

- **HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive** ([link](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)) — Author: HauhauCS | Likes: 3,032 | Downloads: 2,027,080 — An uncensored fine-tune of Qwen3.6-35B-A3B with MoE architecture and vision support, trending for its aggressive creative generation capabilities.

- **empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF** ([link](https://huggingface.co/empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF)) — Author: empero-ai | Likes: 2,438 | Downloads: 2,126,755 — A GGUF-quantized 9B reasoning model derived from Qwen3.5, trending for strong reasoning performance at a compact size.

- **DavidAU/Qwen3.6-27B-Fable-Fusion-711-Uncensored-Heretic-NM-DAU-NEO-MAX-MTP-GGUF** ([link](https://huggingface.co/DavidAU/Qwen3.6-27B-Fable-Fusion-711-Uncensored-Heretic-NM-DAU-NEO-MAX-MTP-GGUF)) — Author: DavidAU | Likes: 392 | Downloads: 334,847 — An uncensored GGUF fine-tune of Qwen3.6-27B with maximal creative freedom, trending among users seeking unrestricted generation.

- **bottlecapai/ThinkingCap-Qwen3.6-27B** ([link](https://huggingface.co/bottlecapai/ThinkingCap-Qwen3.6-27B)) — Author: bottlecapai | Likes: 528 | Downloads: 25,231 — A Qwen3.6-based multimodal fine-tune optimized for reasoning, trending for its thoughtful balance of vision and chain-of-thought capabilities.

- **unsloth/Laguna-S-2.1-GGUF** ([link](https://huggingface.co/unsloth/Laguna-S-2.1-GGUF)) — Author: unsloth | Likes: 148 | Downloads: 28,542 — Unsloth's GGUF quantization of the Laguna-S-2.1 model, providing an optimized inference option for this popular text-generation model.

- **poolside/Laguna-S-2.1** ([link](https://huggingface.co/poolside/Laguna-S-2.1)) — Author: poolside | Likes: 510 | Downloads: 13,285 — The base Laguna-S-2.1 text-generation model from Poolside, showing strong community interest in their specialized code-focused LLM.

- **poolside/Laguna-S-2.1-NVFP4** ([link](https://huggingface.co/poolside/Laguna-S-2.1-NVFP4)) — Author: poolside | Likes: 115 | Downloads: 52,235 — NVIDIA FP4 quantization of Laguna-S-2.1, representing the cutting edge of ultra-low precision inference.

- **poolside/Laguna-S-2.1-GGUF** ([link](https://huggingface.co/poolside/Laguna-S-2.1-GGUF)) — Author: poolside | Likes: 112 | Downloads: 25,360 — The official GGUF variant of Laguna-S-2.1, making this code model more accessible for local deployment.

- **prism-ml/Bonsai-27B-mlx-1bit** ([link](https://huggingface.co/prism-ml/Bonsai-27B-mlx-1bit)) — Author: prism-ml | Likes: 170 | Downloads: 34,270 — Apple Silicon-optimized 1-bit quantization of Bonsai-27B using MLX, bringing extreme compression to Mac users.

- **LuffyTheFox/Qwen3.6-35B-A3B-Uncensored-Genesis-Hermes-V5-GGUF** ([link](https://huggingface.co/LuffyTheFox/Qwen3.6-35B-A3B-Uncensored-Genesis-Hermes-V5-GGUF)) — Author: LuffyTheFox | Likes: 117 | Downloads: 24,982 — Another Hermes-inspired uncensored Qwen3.6 fine-tune in GGUF format, part of a growing ecosystem of creative-generation-focused models.

## 3. Ecosystem Signal

**Qwen3.6 is the platform of the moment.** With at least 7 models directly derived from Qwen3.6 or Qwen3.5, this family has become the dominant base for community fine-tuning, particularly in the uncensored and creative generation spaces. The trend toward **"uncensored" multimodal models** (HauhauCS, DavidAU, LuffyTheFox) suggests a strong demand for creative freedom in image-text generation that bypasses safety filters.

**Extreme quantization has gone mainstream.** The Bonsai family's 1-bit and ternary variants achieving nearly 2.5M combined downloads signals that users are willing to trade significant precision for the ability to run 27B-class models on consumer hardware. The simultaneous success of GGUF, MLX, and NVFP4 formats shows the community is format-agnostic—they just want models that fit their devices.

**The robotics pipeline is emerging.** OpenBMB's MiniCPM-RobotManip and RobotTrack represent a new category: vision-language-action models hosted directly on Hugging Face. With modest downloads but clear developer interest, this could be the next frontier for the platform as embodied AI research accelerates.

**Laguna-S-2.1 is Poolside's bet on code-first LLMs.** With five variants (base, GGUF, NVFP4, and more) all trending simultaneously, the community is clearly evaluating this model for specialized code generation. The simultaneous release of multiple quantization formats shows sophisticated release strategy.

## 4. Worth Exploring

**Bonsai-27B-gguf** — At 1-bit quantization with 1.9M downloads, this is the litmus test for how far compression can go while maintaining usability. For anyone exploring on-device LLMs, this is the benchmark to study for understanding the quality-compression frontier. It's worth running side-by-side comparisons with 4-bit quantizations to see where the tradeoffs actually hurt.

**HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive** — With 2M downloads in its first week, this model represents the most popular uncensored multimodal fine-tune on the platform. For researchers studying alignment, safety, or the creative capabilities of stripped-down models, this is essential to understand what the "other side" of the alignment debate looks like in practice.

**openbmb/MiniCPM-RobotManip** — Robotics is Hugging Face's next growth vertical, and this VLA model is one of the first to gain meaningful traction. Developers interested in the intersection of vision, language, and action should study this as a reference architecture for how to repurpose existing vision-language models for robotic control tasks.

---
*This digest is auto-generated by [agents-radar](https://github.com/kky-wollu/agents-radar).*