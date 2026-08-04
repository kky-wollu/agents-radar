# Hugging Face Trending Models Digest 2026-08-05

> Source: [Hugging Face Hub](https://huggingface.co/) | 30 models | Generated: 2026-08-04 23:06 UTC

---

# 🤖 Hugging Face Trending Models Digest — 2026-08-05

## 1. Today's Highlights

This week's Hugging Face trending list is dominated by **massive open-weight MoE releases** — most notably **DeepSeek-V4-Flash** (2.7M downloads, 2K likes), **Kimi-K3** (1.1M downloads, 10K likes — the highest-liked model on the list), and **GLM-5.2** (2.2M downloads, 4.8K likes). The **Qwen3.6/3.5** family continues to be the most active base for community fine-tunes, with multiple uncensored and "Heretic" variants racking up significant download counts. In video, **MiniMax-H3** is the breakout release of the week, spawning immediate ComfyUI integrations and GGUF quantizations, signaling strong community enthusiasm for open video generation. Quantization continues to be a major driver of adoption, with GGUF variants appearing for nearly every major release within hours.

---

## 2. Trending Models by Category

### 🧠 Language Models (LLMs, chat, instruction-tuned)

| Model | Author | Likes / Downloads | Why It's Trending |
|-------|--------|-------------------|-------------------|
| [**DeepSeek-V4-Flash-0731**](https://huggingface.co/deepseek-ai/DeepSeek-V4-Flash-0731) | deepseek-ai | 2,288 / 433K | Latest Flash variant of DeepSeek's flagship V4 series — compact, fast, and highly capable. |
| [**DeepSeek-V4-Flash**](https://huggingface.co/deepseek-ai/DeepSeek-V4-Flash) | deepseek-ai | 2,011 / 2.7M | The non-dated release of DeepSeek V4 Flash; massive download count reflects production adoption. |
| [**Kimi-K3**](https://huggingface.co/moonshotai/Kimi-K3) | moonshotai | 10,005 / 1.1M | **Most-liked model this week** — Moonshot's K3 with compressed-tensors support signals a new generation of efficient multimodal LLMs. |
| [**GLM-5.2**](https://huggingface.co/zai-org/GLM-5.2) | zai-org | 4,819 / 2.2M | Zhipu AI's GLM-5.2 MoE with DSA (dynamic sparse attention) — a leading open-weight competitor to GPT-class models. |
| [**LiquidAI/LFM2.5-2.6B**](https://huggingface.co/LiquidAI/LFM2.5-2.6B) | LiquidAI | 137 / 47K | Liquid's 2.6B liquid foundation model — compact, state-space inspired architecture for edge deployment. |
| [**Nanbeige4.2-3B**](https://huggingface.co/Nanbeige/Nanbeige4.2-3B) | Nanbeige | 664 / 37K | Compact 3B Chinese-first LLM; strong performance per parameter. |
| [**poolside/Laguna-S-2.1**](https://huggingface.co/poolside/Laguna-S-2.1) | poolside | 920 / 82K | Poolside's software-focused LLM — code-heavy model with strong general reasoning. |
| [**LGAI-EXAONE/K-EXAONE-2.0-750B-A37B**](https://huggingface.co/LGAI-EXAONE/K-EXAONE-2.0-750B-A37B) | LGAI-EXAONE | 116 / 325 | Massive 750B MoE with 37B active — LG's flagship Korean+multilingual model; early release, low downloads. |

### 🎨 Multimodal & Generation (image, video, audio, text-to-X)

| Model | Author | Likes / Downloads | Why It's Trending |
|-------|--------|-------------------|-------------------|
| [**MiniMax-H3**](https://huggingface.co/MiniMaxAI/MiniMax-H3) | MiniMaxAI | 1,984 / 0 | **Breakout video generation model** — text-to-video + image-to-video; the "H3" successor to Hailuo. Zero downloads (API/studio-first), but massive community enthusiasm. |
| [**baidu/Unlimited-OCR**](https://huggingface.co/baidu/Unlimited-OCR) | baidu | 3,880 / 2.7M | Baidu's OCR model — highest download count on the list; likely near-universal OCR coverage beyond traditional limits. |
| [**microsoft/Mage-VL**](https://huggingface.co/microsoft/Mage-VL) | microsoft | 254 / 435K | Microsoft's multimodal vision-language model — likely a strong VL baseline for enterprise. |
| [**Audio8-TTS-Preview-0.6b**](https://huggingface.co/Audio8/Audio8-TTS-Preview-0.6b) | Audio8 | 246 / 11K | New TTS model with arktts architecture — preview release, early community traction. |
| [**owensong/Inflect-Micro-v2**](https://huggingface.co/owensong/Inflect-Micro-v2) | owensong | 409 / 2K | CPU-friendly, edge-optimized TTS — the "small and local" voice synthesis answer. |
| [**lodestones/Kroma**](https://huggingface.co/lodestones/Kroma) | lodestones | 174 / 0 | LoRA for Krea2 (text-to-image) — community style adapter, ComfyUI-ready. |

### 🔧 Specialized Models (code, OCR, agentic)

| Model | Author | Likes / Downloads | Why It's Trending |
|-------|--------|-------------------|-------------------|
| [**KAT-Coder-V2.5-Dev**](https://huggingface.co/Kwaipilot/KAT-Coder-V2.5-Dev) | Kwaipilot | 471 / 15K | Qwen3.5-MoE-based code model with multimodal input; strong dev-focused release. |
| [**XYZ-Aquila-pro**](https://huggingface.co/XYZAILab/XYZ-Aquila-pro) | XYZAILab | 358 / 1.3K | Agentic-search focused variant of Qwen3.5-MoE — positions for web/data agent workloads. |
| [**XYZ-Aquila-mini**](https://huggingface.co/XYZAILab/XYZ-Aquila-mini) | XYZAILab | 404 / 1.3K | Smaller sibling of Aquila-pro; same family, efficient inference. |
| [**poolside/Laguna-S-2.1**](https://huggingface.co/poolside/Laguna-S-2.1) | poolside | 920 / 82K | Also categorized here — explicitly "for software" positioning. |

### 📦 Fine-tunes & Quantizations (GGUF, community fine-tunes)

| Model | Author | Likes / Downloads | Why It's Trending |
|-------|--------|-------------------|-------------------|
| [**DavidAU/Qwen3.6-27B-Fable-Fusion-711-Uncensored-Heretic-NM-DAU-NEO-MAX-MTP-GGUF**](https://huggingface.co/DavidAU/Qwen3.6-27B-Fable-Fusion-711-Uncensored-Heretic-NM-DAU-NEO-MAX-MTP-GGUF) | DavidAU | 1,510 / 1.6M | Community favorite — uncensored Qwen3.6 fine-tune with MTP support; 1.6M downloads. |
| [**unsloth/DeepSeek-V4-Flash-0731-GGUF**](https://huggingface.co/unsloth/DeepSeek-V4-Flash-0731-GGUF) | unsloth | 466 / 111K | Official Unsloth quantization of DeepSeek V4 Flash — fast local inference. |
| [**unsloth/Kimi-K3-GGUF**](https://huggingface.co/unsloth/Kimi-K3-GGUF) | unsloth | 304 / 170K | Unsloth's GGUF of Kimi-K3 — makes the hottest model locally runnable. |
| [**HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive**](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive) | HauhauCS | 3,296 / 1.9M | Huge traction — an "aggressive" uncensored fine-tune with vision support; 1.9M downloads. |
| [**DavidAU/Qwen3.5-9B-The-Defiant-Fable-Uncensored-Heretic-NEO-IMATRIX-MAX-MTP-GGUF**](https://huggingface.co/DavidAU/Qwen3.5-9B-The-Defiant-Fable-Uncensored-Heretic-NEO-IMATRIX-MAX-MTP-GGUF) | DavidAU | 265 / 323K | Same DavidAU recipe, 9B scale — the "everyone can run it" uncensored GGUF. |
| [**LuffyTheFox/Qwen3.6-35B-A3B-Uncensored-Genesis-Hermes-V6-GGUF**](https://huggingface.co/LuffyTheFox/Qwen3.6-35B-A3B-Uncensored-Genesis-Hermes-V6-GGUF) | LuffyTheFox | 363 / 308K | Hermes-style uncensored Qwen3.6 MoE in GGUF — 300K+ downloads. |
| [**EschaLabs/Qwen3.6-35B-A3B-Escha-W2**](https://huggingface.co/EschaLabs/Qwen3.6-35B-A3B-Escha-W2) | EschaLabs | 191 / 3K | 2-bit (W2) quantization of Qwen3.6-35B MoE — extreme compression experiment. |
| [**nota-ai/Solar-Open2-250B-Nota-NVFP4**](https://huggingface.co/nota-ai/Solar-Open2-250B-Nota-NVFP4) | nota-ai | 174 / 69K | NVFP4 fp4 quantization of Solar Open2 250B — vLLM-ready, pushes frontier efficiency. |
| [**Comfy-Org/MiniMax-H3**](https://huggingface.co/Comfy-Org/MiniMax-H3) | Comfy-Org | 592 / 2 | Official ComfyUI integration weights for MiniMax-H3. |
| [**ethanfel/Qwen3-VL-32B-Ultra-Heretic-MiniMax-H3-ComfyUI-INT8-ConvRot**](https://huggingface.co/ethanfel/Qwen3-VL-32B-Ultra-Heretic-MiniMax-H3-ComfyUI-INT8-ConvRot) | ethanfel | 186 / 0 | ComfyUI + MiniMax hybrid — combines Qwen3-VL and H3 conventions into one INT8 model. |
| [**realrebelai/MiniMax-H3_GGUFs**](https://huggingface.co/realrebelai/MiniMax-H3_GGUFs) | realrebelai | 102 / 40K | Community GGUF of MiniMax-H3 — enables local video gen. |
| [**empero-ai/Qwythos-27B-v1**](https://huggingface.co/empero-ai/Qwythos-27B-v1) | empero-ai | 133 / 2.2K | Qwen3.5-based fine-tune with vision — early signals of community adoption. |
| [**thinkingmachines/Inkling-Small**](https://huggingface.co/thinkingmachines/Inkling-Small) | thinkingmachines | 282 / 15.5K | Small multimodal chat model — efficient vision+language for narrow tasks. |

---

## 3. Ecosystem Signal

**MoE is the dominant paradigm.** Every frontier release this week — DeepSeek-V4, GLM-5.2, Kimi-K3, Solar Open2, K-EXAONE-2.0 — is Mixture-of-Experts. The **Qwen3.6/3.5 generation** is now the primary base for community experimentation, with uncensored fine-tunes, Heretic variants, and MTP (multi-token prediction) GGUFs proliferating. The **"uncensored + GGUF"** pairing is the single strongest community pattern: unmodified weights rarely generate this kind of volume. Quantization is accelerating in **two directions**: extreme compression (Escha W2, NVFP4) and accessibility (Unsloth's rapid-fire GGUF releases). **Video generation broke through**: MiniMax-H3 is the first video model in months to generate immediate ComfyUI + GGUF ecosystem adoption, signaling that open-weights video has reached mainstream interest. Open-weight dominance continues — no proprietary-only model made the top 30.

---

## 4. Worth Exploring

1. **Kimi-K3** (moonshotai) — With 10K likes in week one, it's the most community-validated release of the month. Its `compressed-tensors` tag suggests a new approach to efficient multimodal inference. Worth studying as a likely reference architecture for 2026–2027.

2. **MiniMax-H3 + Comfy-Org + GGUF trio** — The full early-adoption lifecycle (release → ComfyUI → quantization) happened in under a week. Studying this cluster reveals how the community operationalizes a new video model — and H3's architecture likely sets the bar for open video generation.

3. **DavidAU's Qwen3.6-27B-Fable-Fusion-711-Uncensored-Heretic-NM-DAU-NEO-MAX-MTP-GGUF** — 1.6M downloads with zero marketing, purely via search/discovery and word of mouth. If you want to understand what the "long tail" of HF actually runs locally, trace this model's recipe: MTP, NEO imatrix, GGUF, uncensored, and Qwen3.6 base. It's the clearest signal of what everyday users want from open weights.

---
*This digest is auto-generated by [agents-radar](https://github.com/kky-wollu/agents-radar).*