# Hugging Face Trending Models Digest 2026-07-28

> Source: [Hugging Face Hub](https://huggingface.co/) | 30 models | Generated: 2026-07-27 23:08 UTC

---

# 🤗 Hugging Face Trending Models Digest — 2026-07-28

## 1. Today's Highlights

This week's Hugging Face trending board is dominated by **massive multimodal MoE models** from leading labs, with moonshotai's **Kimi-K3** (5,965 likes) and Qwen's **Qwen3.6-35B-A3B** (2,546 likes, 6.2M downloads) capturing the community's attention. A striking trend is the surge of **"uncensored" fine-tunes** and **aggressive quantization** (down to 1-bit and 2-bit)—the Bonsai and Ternary-Bonsai GGUF variants by prism-ml are among the most downloaded models this week. The ecosystem is also seeing strong momentum in **vision-language models adapted for OCR** (Baidu's Unlimited-OCR, ATH-MaaS/OvisOCR2) and **speech synthesis optimized for edge/CPU** (owensong's Inflect series). Notably, poolside's **Laguna-S-2.1** spawns a full family of quantized and FP4 variants, signaling enterprise-ready deployment patterns.

---

## 2. Trending Models by Category

### 🧠 Language Models (LLMs, chat models, instruction-tuned)

- **[moonshotai/Kimi-K3](https://huggingface.co/moonshotai/Kimi-K3)** — moonshotai | 5,965 ❤️ | 2,850 ⬇️  
  The week's top trending model: a flagship multimodal LLM leveraging compressed-tensors and image-text-to-text capabilities, driving massive community interest.

- **[upstage/Solar-Open2-250B](https://huggingface.co/upstage/Solar-Open2-250B)** — upstage | 628 ❤️ | 3,761 ⬇️  
  A 250B-parameter open-weight text-generation model from Upstage, positioned as a competitive alternative to proprietary frontier LLMs.

- **[Nanbeige/Nanbeige4.2-3B](https://huggingface.co/Nanbeige/Nanbeige4.2-3B)** — Nanbeige | 491 ❤️ | 16,518 ⬇️  
  A compact 3B-parameter LLM gaining attention for efficient inference and strong performance in resource-constrained settings.

- **[Motif-Technologies/Motif-3-Beta](https://huggingface.co/Motif-Technologies/Motif-3-Beta)** — Motif-Technologies | 199 ❤️ | 2,532 ⬇️  
  A new beta release from Motif Technologies featuring feature-extraction capabilities, signaling a push into enterprise NLP tooling.

- **[fdtn-ai/antares-1b](https://huggingface.co/fdtn-ai/antares-1b)** — fdtn-ai | 207 ❤️ | 6,421 ⬇️  
  A 1B-parameter security-focused model built on GraniteMoEHybrid architecture, targeting safety-critical AI applications.

### 🎨 Multimodal & Generation (image, video, audio, text-to-X)

- **[baidu/Unlimited-OCR](https://huggingface.co/baidu/Unlimited-OCR)** — baidu | 3,326 ❤️ | 2,645,773 ⬇️  
  A high-download OCR model from Baidu using image-text-to-text pipeline—dominating the OCR niche with practical utility.

- **[microsoft/Mage-Flow](https://microsoft.com/Mage-Flow)** — microsoft | 384 ❤️ | 1,691 ⬇️  
  Microsoft's text-to-image diffusion model for advanced image generation and editing.

- **[thinkingmachines/Inkling](https://huggingface.co/thinkingmachines/Inkling)** — thinkingmachines | 1,602 ❤️ | 36,196 ⬇️  
  A conversational multimodal model combining image understanding with dialogue—strong community engagement.

- **[microsoft/Fara1.5-27B](https://huggingface.co/microsoft/Fara1.5-27B)** — microsoft | 130 ❤️ | 1,406 ⬇️  
  A 27B-parameter vision-language model focused on computer-use tasks, powered by Qwen3.5 architecture.

- **[baseten/GLM-5.2-Vision-NVFP4](https://huggingface.co/baseten/GLM-5.2-Vision-NVFP4)** — baseten | 124 ❤️ | 2,276 ⬇️  
  An NVFP4-quantized vision-language variant of GLM-5.2, optimized for efficient multimodal deployment.

- **[nvidia/Cosmos3-Edge](https://huggingface.co/nvidia/Cosmos3-Edge)** — nvidia | 132 ❤️ | 33,127 ⬇️  
  NVIDIA's latest Cosmos diffusion model for edge-optimized image/video generation.

- **[owensong/Inflect-Micro-v2](https://huggingface.co/owensong/Inflect-Micro-v2)** — owensong | 221 ❤️ | 483 ⬇️  
  A compact text-to-speech model optimized for CPU and edge-AI deployment, representing the growing local TTS movement.

- **[owensong/Inflect-Nano-v2](https://huggingface.co/owensong/Inflect-Nano-v2)** — owensong | 91 ❤️ | 349 ⬇️  
  Even smaller sibling of Inflect-Micro-v2, pushing the frontier of edge speech synthesis.

- **[microsoft/Mage-Flow-Edit-Turbo](https://huggingface.co/microsoft/Mage-Flow-Edit-Turbo)** — microsoft | 100 ❤️ | 1,115 ⬇️  
  An accelerated variant of Mage-Flow specialized for instruction-based image editing.

- **[conradlocke/krea2-identity-edit](https://huggingface.co/conradlocke/krea2-identity-edit)** — conradlocke | 554 ❤️ | 0 ⬇️  
  A LoRA for identity-consistent image editing built on Krea-2-Raw, popular in the ComfyUI community.

### 🔧 Specialized Models (code, math, medical, embeddings)

- **[Kwaipilot/KAT-Coder-V2.5-Dev](https://huggingface.co/Kwaipilot/KAT-Coder-V2.5-Dev)** — Kwaipilot | 240 ❤️ | 5,312 ⬇️  
  A code-focused MoE model (based on Qwen3.5) with image-text-to-text pipeline, targeting developer workflows.

- **[ATH-MaaS/OvisOCR2](https://huggingface.co/ATH-MaaS/OvisOCR2)** — ATH-MaaS | 327 ❤️ | 42,152 ⬇️  
  A specialized OCR model built on Qwen3.5, competing with Baidu's offering in the document intelligence space.

### 📦 Fine-tunes & Quantizations (community fine-tunes, GGUF, AWQ)

- **[DavidAU/Qwen3.6-27B-Fable-Fusion-711-Uncensored-Heretic-NM-DAU-NEO-MAX-MTP-GGUF](https://huggingface.co/DavidAU/Qwen3.6-27B-Fable-Fusion-711-Uncensored-Heretic-NM-DAU-NEO-MAX-MTP-GGUF)** — DavidAU | 742 ❤️ | 634,146 ⬇️  
  An extreme "uncensored" Qwen3.6 fine-tune in GGUF format, typical of the highly customized community releases trending this week.

- **[HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)** — HauhauCS | 3,132 ❤️ | 1,894,395 ⬇️  
  The most popular uncensored Qwen3.6 MoE variant with aggressive tuning—1.9M downloads signals massive demand for unrestricted models.

- **[prism-ml/Ternary-Bonsai-27B-gguf](https://huggingface.co/prism-ml/Ternary-Bonsai-27B-gguf)** — prism-ml | 1,068 ❤️ | 648,938 ⬇️  
  A pioneering 2-bit ternary quantization of a 27B model, achieving extreme compression while retaining conversational quality.

- **[prism-ml/Bonsai-27B-gguf](https://huggingface.co/prism-ml/Bonsai-27B-gguf)** — prism-ml | 657 ❤️ | 2,257,928 ⬇️  
  The 1-bit quantization variant (2.3M downloads)—the most downloaded model this week, demonstrating insatiable demand for ultra-small LLMs.

- **[poolside/Laguna-S-2.1-GGUF](https://huggingface.co/poolside/Laguna-S-2.1-GGUF)** — poolside | 154 ❤️ | 85,554 ⬇️  
  Official GGUF quant of Laguna-S-2.1 from poolside, supporting llama.cpp and vLLM deployment.

- **[poolside/Laguna-S-2.1-NVFP4](https://huggingface.co/poolside/Laguna-S-2.1-NVFP4)** — poolside | 148 ❤️ | 158,308 ⬇️  
  NVIDIA FP4 quantized variant of Laguna-S-2.1, optimized for Blackwell-class GPUs.

- **[unsloth/Laguna-S-2.1-GGUF](https://huggingface.co/unsloth/Laguna-S-2.1-GGUF)** — unsloth | 217 ❤️ | 117,456 ⬇️  
  Community GGUF of Laguna-S-2.1 via Unsloth, highlighting the popularity of the Laguna family.

- **[LuffyTheFox/Qwen3.6-35B-A3B-Uncensored-Genesis-Hermes-V5-GGUF](https://huggingface.co/LuffyTheFox/Qwen3.6-35B-A3B-Uncensored-Genesis-Hermes-V5-GGUF)** — LuffyTheFox | 187 ❤️ | 83,658 ⬇️  
  Another uncensored Qwen3.6 GGUF, this time blending Hermes-style training—showing diversification of the uncensored fine-tune ecosystem.

- **[empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF](https://huggingface.co/empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF)** — empero-ai | 2,487 ❤️ | 1,336,263 ⬇️  
  A Qwen3.5-based 9B reasoning model with Claude-Mythos training, drawing 1.3M downloads—strong in the "reasoning" niche.

---

## 3. Ecosystem Signal

**Qwen3.6 MoE family dominates.** The base model ([Qwen3.6-35B-A3B](https://huggingface.co/Qwen/Qwen3.6-35B-A3B)) and its uncensored GGUF offspring occupy four of the top 10 trending slots, collectively exceeding 10M downloads. The community is enthusiastically pushing the "uncensored" boundary, with fine-tuners like HauhauCS and DavidAU creating aggressive, unaltered variants that clearly meet demand from users seeking maximal creative freedom—a trend that mirrors the open-source "wild west" ethos.

**Ultra-low-bit quantization becomes mainstream.** Prism-ml's Bonsai models (1-bit and 2-bit ternary) demonstrate that extreme compression (sub-2-bit) is no longer experimental—it's deployment-ready. With 2.3M downloads for the 1-bit Bonsai, users are clearly willing to trade quality for extreme memory efficiency (e.g., running a 27B model in under 8GB VRAM).

**Laguna-S-2.1 as a deployment exemplar.** Poolside's Laguna model shows an ideal open-weight release pattern: base model + official GGUF + NVIDIA FP4 quant + community Unsloth GGUF + vLLM compatibility tags. This multiplies reach across enterprise, edge, and llama.cpp users.

**Edge and CPU inference grows.** Owenson's Inflect series (Micro/Nano TTS) and the proliferation of GGUF models for llama.cpp all point to a sustained shift from cloud-only to local-first AI deployment.

---

## 4. Worth Exploring

1. **[prism-ml/Ternary-Bonsai-27B-gguf](https://huggingface.co/prism-ml/Ternary-Bonsai-27B-gguf)** — For researchers studying model compression: this 2-bit ternary quantization pushes the boundary of "how far can we shrink an LLM?" while maintaining conversational coherence. It's a live case study in extreme quantization trade-offs.

2. **[Qwen/Qwen3.6-35B-A3B](https://huggingface.co/Qwen/Qwen3.6-35B-A3B)** — As the base model powering half the trending list, this MoE vision-language model is essential for understanding the current architecture of choice for both multilingual and multimodal tasks. Its 6.2M downloads and widespread fine-tuning adoption make it a foundational checkpoint.

3. **[baidu/Unlimited-OCR](https://huggingface.co/baidu/Unlimited-OCR)** — With nearly 2.6M downloads and minimal marketing, this model is a sleeper hit for practical document intelligence. It represents a growing category of production-ready, domain-specific vision models that solve real-world problems rather than chasing benchmarks.

---
*This digest is auto-generated by [agents-radar](https://github.com/kky-wollu/agents-radar).*