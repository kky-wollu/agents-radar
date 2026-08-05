# Hugging Face Trending Models Digest 2026-08-06

> Source: [Hugging Face Hub](https://huggingface.co/) | 30 models | Generated: 2026-08-05 23:05 UTC

---

# 🤖 Hugging Face Trending Models Digest — 2026-08-06

---

## 1. Today's Highlights

The Hugging Face ecosystem is buzzing with **frontier-scale releases**: Moonshot AI's **Kimi-K3** (10.1K likes, 1.1M downloads) leads the pack as a massive multimodal compressed-tensor model, while **GLM-5.2** from Zhipu AI continues its strong run with 2.2M downloads. DeepSeek keeps the momentum with **DeepSeek-V4-Flash** and a dated "0731" variant, both topping 400K+ downloads as the open-weight conversation model of choice for the week. On the media side, **MiniMax-H3** is making waves in image-text-to-video generation, quickly spawning ComfyUI integrations, GGUF quantizations, and spinoff fine-tunes. The community is also heavily engaged in **Qwen3.5/3.6 MoE fine-tunes** (uncensored/Heretic variants) and **GGUF quantizations** from unsloth and independent creators, with download counts in the millions for some entries — a clear sign that local deployment and customization remain top priorities.

---

## 2. Trending Models by Category

### 🧠 Language Models (LLMs, chat models, instruction-tuned)

| Model | Author | Likes | Downloads | Why it's trending |
|-------|--------|-------|-----------|-------------------|
| [DeepSeek-V4-Flash-0731](https://huggingface.co/deepseek-ai/DeepSeek-V4-Flash-0731) | deepseek-ai | 2,483 | 433K | The latest Flash variant of DeepSeek V4, optimized for conversational speed and efficiency |
| [Kimi-K3](https://huggingface.co/moonshotai/Kimi-K3) | moonshotai | 10,118 | 1.13M | A massive multimodal MoE with compressed-tensor support — the week's biggest release by likes |
| [GLM-5.2](https://huggingface.co/zai-org/GLM-5.2) | zai-org | 4,848 | 2.23M | Zhipu's flagship MoE with "DSA" sparse attention; enterprise-grade conversational AI |
| [DeepSeek-V4-Flash](https://huggingface.co/deepseek-ai/DeepSeek-V4-Flash) | deepseek-ai | 2,030 | 2.74M | The main release of DeepSeek V4 Flash — highest weekly downloads on the list |
| [LiquidAI/LFM2.5-2.6B](https://huggingface.co/LiquidAI/LFM2.5-2.6B) | LiquidAI | 278 | 47K | Liquid AI's liquid-neural-network foundation model, compact and efficient for edge deployment |
| [Ling-3.0-flash](https://huggingface.co/inclusionAI/Ling-3.0-flash) | inclusionAI | 155 | 25 | New hybrid-architecture flash model from inclusionAI, still early in adoption |
| [K-EXAONE-2.0-750B-A37B](https://huggingface.co/LGAI-EXAONE/K-EXAONE-2.0-750B-A37B) | LGAI-EXAONE | 129 | 325 | LG's massive 750B MoE with 37B active parameters, targeting Korean+multilingual use cases |
| [Shieldstral-1.0-3B](https://huggingface.co/mistralai/Shieldstral-1.0-3B) | mistralai | 129 | 166 | Mistral's compact safety/guardrail model built on Mistral 3 — small but critical |

---

### 🎨 Multimodal & Generation (image, video, audio, text-to-X)

| Model | Author | Likes | Downloads | Why it's trending |
|-------|--------|-------|-----------|-------------------|
| [MiniMax-H3](https://huggingface.co/MiniMaxAI/MiniMax-H3) | MiniMaxAI | 2,480 | 10.8K | The week's breakout video-gen model — image-text-to-video via diffusers, extremely hot |
| [Unlimited-OCR](https://huggingface.co/baidu/Unlimited-OCR) | baidu | 3,905 | 2.70M | Baidu's all-in-one OCR model with feature-extraction — enormous download velocity |
| [Mage-VL](https://huggingface.co/microsoft/Mage-VL) | microsoft | 274 | 436K | Microsoft's multimodal vision-language model, rapidly adopted since release |
| [Inkling-Small](https://huggingface.co/thinkingmachines/Inkling-Small) | thinkingmachines | 308 | 15.5K | A compact conversational image-text-to-text model, gaining attention |
| [Audio8-TTS-Preview-0.6b](https://huggingface.co/Audio8/Audio8-TTS-Preview-0.6b) | Audio8 | 273 | 11.3K | New ArkTTS-based text-to-speech preview — one of the first credible open TTS releases this week |
| [Kroma](https://huggingface.co/lodestones/Kroma) | lodestones | 190 | 0 | A Krea2-based LoRA for text-to-image (ComfyUI-ready); early but promising |
| [Inflect-Micro-v2](https://huggingface.co/owensong/Inflect-Micro-v2) | owensong | 417 | 2.1K | CPU-friendly, local TTS for edge-AI — great community reception |
| [NVIDIA-NemotronLabs-VoiceChat-11B](https://huggingface.co/nvidia/NVIDIA-NemotronLabs-VoiceChat-11B) | nvidia | 123 | 80 | NVIDIA's 11B voice-chat model (speech-to-speech), backed by multiple arXiv papers |

---

### 🔧 Specialized Models (code, math, medical, embeddings)

| Model | Author | Likes | Downloads | Why it's trending |
|-------|--------|-------|-----------|-------------------|
| [KAT-Coder-V2.5-Dev](https://huggingface.co/Kwaipilot/KAT-Coder-V2.5-Dev) | Kwaipilot | 493 | 15.4K | Qwen3.5-MoE-based code generation model — strong developer adoption |
| [XYZ-Aquila-mini](https://huggingface.co/XYZAILab/XYZ-Aquila-mini) | XYZAILab | 416 | 1.3K | Compact Qwen3.6-based multimodal agent, optimized for efficiency |
| [XYZ-Aquila-pro](https://huggingface.co/XYZAILab/XYZ-Aquila-pro) | XYZAILab | 366 | 1.4K | Pro sibling of Aquila-mini with agentic-search capabilities built in |

---

### 📦 Fine-tunes & Quantizations (community fine-tunes, GGUF, AWQ)

| Model | Author | Likes | Downloads | Why it's trending |
|-------|--------|-------|-----------|-------------------|
| [Qwen3.6-27B-Fable-Fusion-711-Uncensored-Heretic-NM-DAU-NEO-MAX-MTP-GGUF](https://huggingface.co/DavidAU/Qwen3.6-27B-Fable-Fusion-711-Uncensored-Heretic-NM-DAU-NEO-MAX-MTP-GGUF) | DavidAU | 1,584 | 1.63M | Massive community follow — uncensored Qwen3.6 fine-tune with MTP GGUF, one of the most downloaded |
| [DeepSeek-V4-Flash-0731-GGUF](https://huggingface.co/unsloth/DeepSeek-V4-Flash-0731-GGUF) | unsloth | 500 | 112K | Official unsloth GGUF quantization of the latest DeepSeek Flash |
| [Kimi-K3-GGUF](https://huggingface.co/unsloth/Kimi-K3-GGUF) | unsloth | 316 | 170K | GGUF quant of Kimi-K3, enabling local deployment of the week's hottest model |
| [MiniMax-H3_GGUFs](https://huggingface.co/realrebelai/MiniMax-H3_GGUFs) | realrebelai | 133 | 40K | Community quantization of MiniMax-H3 for ComfyUI workflows |
| [Qwen3.6-35B-A3B-Escha-W2](https://huggingface.co/EschaLabs/Qwen3.6-35B-A3B-Escha-W2) | EschaLabs | 209 | 3K | Specialized Qwen3.6 MoE weight-2 quantization; experimental |
| [Qwen3.6-35B-A3B-Uncensored-Genesis-Hermes-V7-GGUF](https://huggingface.co/LuffyTheFox/Qwen3.6-35B-A3B-Uncensored-Genesis-Hermes-V7-GGUF) | LuffyTheFox | 384 | 309K | Hermes-style uncensored Qwen3.6 MoE fine-tune — 300K+ downloads in days |
| [Qwen3.5-9B-The-Defiant-Fable-Uncensored-Heretic-NEO-IMATRIX-MAX-MTP-GGUF](https://huggingface.co/DavidAU/Qwen3.5-9B-The-Defiant-Fable-Uncensored-Heretic-NEO-IMATRIX-MAX-MTP-GGUF) | DavidAU | 280 | 323K | Another one of DavidAU's uncensored MTP/Imatrix GGUF variants — extremely popular |
| [Comfy-Org/MiniMax-H3](https://huggingface.co/Comfy-Org/MiniMax-H3) | Comfy-Org | 748 | 2 | Official ComfyUI integration repo for MiniMax-H3 — key for workflows |
| [Qwen3-VL-32B-Ultra-Heretic-H3-ComfyUI-INT8-ConvRot](https://huggingface.co/ethanfel/Qwen3-VL-32B-Ultra-Heretic-H3-ComfyUI-INT8-ConvRot) | ethanfel | 279 | 0 | INT8 ComfyUI-optimized Qwen3-VL fine-tune — early but niche-cool |
| [Qwythos-27B-v1](https://huggingface.co/empero-ai/Qwythos-27B-v1) | empero-ai | 144 | 2.2K | Qwen3.5-based image-text-to-text fine-tune for roleplay/chat |

---

## 3. Ecosystem Signal

**Qwen is the de facto community base.** Nearly half of all trending fine-tunes and quantizations are Qwen3.5/3.6 derivatives (MoE, uncensored, GGUF) — DavidAU and LuffyTheFox are turning out massive download counts, signaling Qwen has overtaken Llama as the go-to open-weight foundation for community work.

**Uncensored and "Heretic" models are a persistent, large-scale subculture** — these variants regularly pull 300K–1.6M downloads, proving a dedicated (and sizable) user base for unrestricted generation, even as major labs focus on alignment.

**Chinese labs are dominating open-weight releases** — DeepSeek, Kimi, GLM, Baidu, MiniMax, and Qwen collectively represent ~80% of this week's most-liked models. Open-weight competition is now firmly an East-Asia-led race, with US labs (OpenAI, Anthropic, Google) notably absent from trending — except via NVIDIA and Microsoft entries.

**Quantization is now a first-class release path** — GGUF is no longer a community afterthought; unsloth and Comfy-Org are releasing quantized/integrated versions within days of base models, treating them as official artifacts. **Uncensored + MTP + Imatrix** is the emerging "power-user trifecta" for efficient local inference.

**Multimodal is exploding** — video-gen (MiniMax-H3), OCR (Baidu), voice chat (NVIDIA), TTS (Audio8, Inflect), and vision-language (Mage-VL, Inkling) all trended simultaneously, suggesting that text-only LLMs are no longer the frontier of public excitement.

---

## 4. Worth Exploring

**1. [Kimi-K3](https://huggingface.co/moonshotai/Kimi-K3)** — The week's highest-liked model with 1.1M downloads, featuring compressed-tensor multimodal MoE. It represents the new frontier of efficient massive models, and its GGUF variant makes it locally runnable — worth studying for anyone tracking the intersection of scale and deployment.

**2. [MiniMax-H3](https://huggingface.co/MiniMaxAI/MiniMax-H3)** — The viral video-generation model of the week with an official ComfyUI integration. Understanding its diffusers-based architecture and community ecosystem (including the GGUF port) gives a clear read on where video-gen is heading for open-weight platforms.

**3. [Unlimited-OCR](https://huggingface.co/baidu/Unlimited-OCR)** — With 2.7M downloads in its first week, it's the fastest-growing specialized utility model on the list. OCR is a high-value commercial niche, and Baidu's entry signals that Chinese labs are targeting practical, commoditized AI services — not just chat.

---
*This digest is auto-generated by [agents-radar](https://github.com/kky-wollu/agents-radar).*