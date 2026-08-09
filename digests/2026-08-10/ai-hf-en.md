# Hugging Face Trending Models Digest 2026-08-10

> Source: [Hugging Face Hub](https://huggingface.co/) | 30 models | Generated: 2026-08-09 22:35 UTC

---

# 🤗 Hugging Face Trending Models Digest — 2026-08-10

## 1. Today's Highlights

This week's trending list is dominated by **MiniMax-H3**, a powerful image-text-to-video model that has spawned an extensive ecosystem of community adaptations — from ComfyUI integrations and GGUF quantizations to LoRA fine-tunes and Turbo variants, with over 5.6M combined downloads across its derivatives. Meanwhile, the **DeepSeek-V4-Flash-0731** continues its strong run with nearly 870K downloads, supported by an official GGUF release from Unsloth. Major releases include **Kimi-K3** from Moonshot AI (10.4K likes, the second most-liked model this week), **GLM-5.2** from Z.ai (4.9K likes, 2.5M downloads), and **FLUX.1-dev** retaining its position as the all-time most-liked model with 14K likes. Notable trends include the proliferation of "uncensored" fine-tunes (DavidAU, ethanfel, LuffyTheFox), a surge in voice/audio models (NVIDIA NemotronLabs VoiceChat, Audio8-TTS), and the continued growth of Mixture-of-Experts architectures in production models like Ling-3.0-flash, maple-preview, and the Qwen3.5-MoE based coding and multimodal models.

## 2. Trending Models by Category

### 🧠 Language Models (LLMs, chat models, instruction-tuned)

- **[DeepSeek-V4-Flash-0731](https://huggingface.co/deepseek-ai/DeepSeek-V4-Flash-0731)** — deepseek-ai | 2,939 likes | 868,576 downloads
  - DeepSeek's latest Flash-tier conversational model, trending due to its exceptional performance-to-compute ratio and strong community adoption.

- **[Kimi-K3](https://huggingface.co/moonshotai/Kimi-K3)** — moonshotai | 10,395 likes | 1,456,459 downloads
  - Moonshot AI's flagship compressed multimodal LLM (image-text-to-text) with feature-extraction capabilities; the second most-liked model this week.

- **[GLM-5.2](https://huggingface.co/zai-org/GLM-5.2)** — zai-org | 4,913 likes | 2,488,397 downloads
  - Z.ai's latest GLM iteration with DSA (Dynamic Sparse Attention) MoE architecture; one of the most downloaded models this week.

- **[LiquidAI/LFM2.5-2.6B](https://huggingface.co/LiquidAI/LFM2.5-2.6B)** — LiquidAI | 448 likes | 85,651 downloads
  - Liquid AI's efficient 2.6B liquid foundation model, trending for its small-footprint, high-performance design.

- **[deepgrove/maple-preview](https://huggingface.co/deepgrove/maple-preview)** — deepgrove | 287 likes | 1,089 downloads
  - Preview release of a new Mixture-of-Experts causal LM, generating interest for its novel architecture and early access status.

- **[inclusionAI/Ling-3.0-flash](https://huggingface.co/inclusionAI/Ling-3.0-flash)** — inclusionAI | 244 likes | 4,747 downloads
  - Flash-tier conversational model using Bailing hybrid architecture with custom code; trending for its efficient design and strong chat performance.

- **[mistralai/Shieldstral-1.0-3B](https://huggingface.co/mistralai/Shieldstral-1.0-3B)** — mistralai | 211 likes | 5,651 downloads
  - Mistral's compact 3B safety/guardrail model built on Mistral-3, trending as safety becomes a priority in open-weight deployments.

### 🎨 Multimodal & Generation (image, video, audio, text-to-X)

- **[MiniMaxAI/MiniMax-H3](https://huggingface.co/MiniMaxAI/MiniMax-H3)** — MiniMaxAI | 3,236 likes | 35,295 downloads
  - The week's breakout model: a state-of-the-art image-text-to-video diffusion model with exceptional motion quality and prompt adherence.

- **[baidu/Unlimited-OCR](https://huggingface.co/baidu/Unlimited-OCR)** — baidu | 3,985 likes | 2,889,062 downloads
  - Baidu's OCR-capable multimodal model; trending due to its impressive accuracy across languages and document types, with 2.9M downloads.

- **[black-forest-labs/FLUX.1-dev](https://huggingface.co/black-forest-labs/FLUX.1-dev)** — black-forest-labs | 14,057 likes | 487,171 downloads
  - The most-liked model on Hugging Face; FLUX.1-dev remains the benchmark open-weight text-to-image generator.

- **[nvidia/NVIDIA-NemotronLabs-VoiceChat-11B](https://huggingface.co/nvidia/NVIDIA-NemotronLabs-VoiceChat-11B)** — nvidia | 260 likes | 543 downloads
  - NVIDIA's 11B voice chat model enabling natural spoken dialogue; newly released and rapidly gaining attention.

- **[Audio8/Audio8-TTS-Preview-0.6b](https://huggingface.co/Audio8/Audio8-TTS-Preview-0.6b)** — Audio8 | 332 likes | 13,132 downloads
  - Compact 0.6B text-to-speech model with ArkTTS architecture; trending for its surprisingly natural voice synthesis at small scale.

- **[microsoft/Mage-VL](https://huggingface.co/microsoft/Mage-VL)** — microsoft | 323 likes | 461,150 downloads
  - Microsoft's multimodal vision-language model; trending for its strong general-purpose image understanding capabilities.

### 🔧 Specialized Models (code, math, medical, embeddings)

- **[Kwaipilot/KAT-Coder-V2.5-Dev](https://huggingface.co/Kwaipilot/KAT-Coder-V2.5-Dev)** — Kwaipilot | 552 likes | 18,574 downloads
  - Qwen3.5-MoE based code model with image-text-to-text multimodal capabilities; trending in the developer community for its coding performance.

### 📦 Fine-tunes & Quantizations (community fine-tunes, GGUF, AWQ)

- **[Comfy-Org/MiniMax-H3](https://huggingface.co/Comfy-Org/MiniMax-H3)** — Comfy-Org | 1,069 likes | 4,947,943 downloads
  - The official ComfyUI single-file version of MiniMax-H3; the most downloaded MiniMax variant, essential for ComfyUI users.

- **[unsloth/DeepSeek-V4-Flash-0731-GGUF](https://huggingface.co/unsloth/DeepSeek-V4-Flash-0731-GGUF)** — unsloth | 627 likes | 188,761 downloads
  - Unsloth's optimized GGUF quantization of DeepSeek-V4-Flash, enabling efficient local deployment of the model.

- **[DavidAU/Qwen3.6-27B-Fable-Fusion-711-Uncensored-Heretic-NM-DAU-NEO-MAX-MTP-GGUF](https://huggingface.co/DavidAU/Qwen3.6-27B-Fable-Fusion-711-Uncensored-Heretic-NM-DAU-NEO-MAX-MTP-GGUF)** — DavidAU | 1,804 likes | 2,390,692 downloads
  - A heavily fine-tuned "uncensored" Qwen3.6-27B variant in GGUF format; one of the most downloaded community fine-tunes this week.

- **[LuffyTheFox/Qwen3.6-35B-A3B-Uncensored-Genesis-Hermes-V7-GGUF](https://huggingface.co/LuffyTheFox/Qwen3.6-35B-A3B-Uncensored-Genesis-Hermes-V7-GGUF)** — LuffyTheFox | 454 likes | 396,282 downloads
  - A MoE-based Qwen3.6-35B-A3B uncensored fine-tune with Hermes-style training, in GGUF format; strong community following.

- **[realrebelai/MiniMax-H3_GGUFs](https://huggingface.co/realrebelai/MiniMax-H3_GGUFs)** — realrebelai | 187 likes | 160,747 downloads
  - Community GGUF quantizations of MiniMax-H3, bringing the video model to more accessible hardware.

- **[lightx2v/Minimax-h3-Turbo](https://huggingface.co/lightx2v/Minimax-h3-Turbo)** — lightx2v | 233 likes | 6,117 downloads
  - Turbo-speed version of MiniMax-H3 supporting multiple video generation modes (t2v, i2v, r2v); trending for its speed.

- **[larryvrh/MiniMax-H3-Turbo-Lora](https://huggingface.co/larryvrh/MiniMax-H3-Turbo-Lora)** — larryvrh | 543 likes | 0 downloads
  - LoRA adapters for MiniMax-H3-Turbo enabling style control and customization for text-to-video generation.

- **[Abiray/Minimax-H3-nvfp4-INT4-INT8-Convrot](https://huggingface.co/Abiray/Minimax-H3-nvfp4-INT4-INT8-Convrot)** — Abiray | 155 likes | 511,473 downloads
  - Mixed-precision (NVFP4/INT4/INT8) quantization of MiniMax-H3; one of the most downloaded quantized video models.

- **[LiquidAI/LFM2.5-2.6B-GGUF](https://huggingface.co/LiquidAI/LFM2.5-2.6B-GGUF)** — LiquidAI | 173 likes | 68,468 downloads
  - Official GGUF version of LFM2.5-2.6B for llama.cpp; enables local deployment of liquid models.

- **[ethanfel/Qwen3-VL-32B-Ultra-Heretic-H3-ComfyUI-INT8-ConvRot](https://huggingface.co/ethanfel/Qwen3-VL-32B-Ultra-Heretic-H3-ComfyUI-INT8-ConvRot)** — ethanfel | 418 likes | 0 downloads
  - ComfyUI-integrated Qwen3-VL-32B with MiniMax-H3 style modifications; a niche but notable community experiment.

- **[Kijai/MiniMax-H3_comfy](https://huggingface.co/Kijai/MiniMax-H3_comfy)** — Kijai | 233 likes | 0 downloads
  - Kijai's ComfyUI implementation of MiniMax-H3, a key integration for video generation workflows.

- **[sakamakismile/Qwen3-VL-32B-Heretic-MiniMax-H3-NVFP4](https://huggingface.co/sakamakismile/Qwen3-VL-32B-Heretic-MiniMax-H3-NVFP4)** — sakamakismile | 142 likes | 0 downloads
  - NVFP4-quantized text-encoder variant combining Qwen3-VL with MiniMax-H3; a community cross-pollination experiment.

- **[SexGod1979/PinkCherry_MiniMax-H3](https://huggingface.co/SexGod1979/PinkCherry_MiniMax-H3)** — SexGod1979 | 229 likes | 0 downloads
  - Apache-2.0 licensed MiniMax-H3 variant with transformers pipeline support; part of the broader H3 ecosystem.

- **[Kijai/MiniMax-H3-experimental](https://huggingface.co/Kijai/MiniMax-H3-experimental)** — Kijai | 168 likes | 0 downloads
  - Experimental version of MiniMax-H3 from Kijai, exploring edge features and optimizations.

- **[drbaph/MiniMax-H3-Turbo-Lora-ComfyUI](https://huggingface.co/drbaph/MiniMax-H3-Turbo-Lora-ComfyUI)** — drbaph | 231 likes | 0 downloads
  - Pruned ComfyUI-ready LoRA for MiniMax-H3-Turbo, streamlining customization workflows.

- **[endless-frontier/BigBang-v1](https://huggingface.co/endless-frontier/BigBang-v1)** — endless-frontier | 116 likes | 482 downloads
  - Qwen3.5-MoE based multimodal conversational model; a newer entry attracting early adopters.

## 3. Ecosystem Signal

Several clear trends define this week's ecosystem. **MiniMax-H3** has created a dominant **single-model ecosystem** rivaling FLUX in its breadth: official release, ComfyUI integration, Turbo variants, LoRA adapters, GGUF quantizations, mixed-precision versions, and even cross-pollinated modifications with Qwen3-VL text encoders. This demonstrates the open-weight community's acceleration in building infrastructure around vision generators.

**Open-weight momentum continues to surge** with DeepSeek-V4, Kimi-K3, and GLM-5.2 all showing production-grade performance while maintaining permissive licenses. The **MoE architecture** is clearly winning: GLM-5.2 (DSA-MoE), Qwen3.5-MoE variants, maple-preview, and LFM2.5 all leverage mixture-of-experts to scale capability efficiently.

**Quantization and accessibility** remain critical: Unsloth's GGUF of DeepSeek-V4 has 188K downloads, while MixedNLP and community quantizers (INT8, NVFP4) are making video generation deployable on consumer hardware. The "**uncensored**" fine-tune segment (DavidAU, LuffyTheFox, ethanfel) continues trending strongly despite moderation debates.

**Multimodal convergence** is accelerating — models increasingly handle image-text-to-text, image-to-video, voice chat, and TTS simultaneously, suggesting a future of unified interfaces rather than specialty models.

## 4. Worth Exploring

1. **[MiniMaxAI/MiniMax-H3](https://huggingface.co/MiniMaxAI/MiniMax-H3)** — The breakout video generation model of the week. Its extensive ecosystem (ComfyUI, GGUF, LoRA, Turbo) makes it the single best model to study for understanding how one model can spawn a full product ecosystem, and for anyone working on text/video generation pipelines.

2. **[Kimi-K3](https://huggingface.co/moonshotai/Kimi-K3)** — With 10.4K likes, this compressed multimodal LLM (compressed-tensors tag) suggests Moonshot is solving efficiency in a novel way. Its compressed-tensors approach could be the future of serving large models. Worth studying for advanced model compression techniques.

3. **[nvidia/NVIDIA-NemotronLabs-VoiceChat-11B](https://huggingface.co/nvidia/NVIDIA-NemotronLabs-VoiceChat-11B)** — Just released, with only 543 downloads — this is an early-insight opportunity. NVIDIA's voice chat model paired with its heavy arXiv citations (three papers) suggests serious research behind a compact 11B voice solution. Getting in early on such models typically pays off as the ecosystem matures.

---
*This digest is auto-generated by [agents-radar](https://github.com/kky-wollu/agents-radar).*