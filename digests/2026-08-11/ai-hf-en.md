# Hugging Face Trending Models Digest 2026-08-11

> Source: [Hugging Face Hub](https://huggingface.co/) | 30 models | Generated: 2026-08-10 22:42 UTC

---

# 🤖 Hugging Face Trending Models Digest — 2026-08-11

---

## 1. 🔥 Today's Highlights

This week's trending chart is dominated by **MiniMax-H3**, a powerful new image-text-to-video model that has spawned an entire ecosystem of derivatives—from ComfyUI ports (6M+ downloads) to LoRA adapters, GGUF quantizations, and NSFW fine-tunes. Meanwhile, **moonshotai/Kimi-K3** (10.4K likes) and **baidu/Unlimited-OCR** (4K likes) represent strong momentum for Chinese labs in multimodal LLMs and OCR respectively. On the language model front, **DeepSeek-V4-Flash-0731** continues its reign with ~1M downloads, while **meta-models/Muse-Glimmer-30B** debuts as a promising new multimodal entry from Meta's model family. The **"Heretic"** fine-tune trend—uncensored variants built on Qwen3-VL and MiniMax-H3 stacks—reveals a persistent community appetite for unrestricted models. Notably, several models show **zero downloads despite high likes**, suggesting a speculative "collecting" dynamic around newly released artifacts.

---

## 2. 📊 Trending Models by Category

### 🧠 Language Models

| Model | Author | Likes | Downloads | Why It's Trending |
|-------|--------|-------|-----------|-------------------|
| [DeepSeek-V4-Flash-0731](https://huggingface.co/deepseek-ai/DeepSeek-V4-Flash-0731) | deepseek-ai | 3,047 | 954,441 | Flagship Flash-tier LLM from DeepSeek, with massive adoption and a GGUF derivative already available. |
| [Kimi-K3](https://huggingface.co/moonshotai/Kimi-K3) | moonshotai | 10,468 | 1,510,032 | Moonshot's compact multimodal LLM (compressed-tensors) — the week's most-liked model. |
| [LFM2.5-2.6B](https://huggingface.co/LiquidAI/LFM2.5-2.6B) | LiquidAI | 488 | 89,680 | Liquid's efficient 2.6B liquid foundation model, with official GGUF release. |
| [maple-preview](https://huggingface.co/deepgrove/maple-preview) | deepgrove | 309 | 1,344 | MoE-based causal LM preview from deepgrove, early-stage but generating buzz. |
| [Ling-3.0-flash](https://huggingface.co/inclusionAI/Ling-3.0-flash) | inclusionAI | 287 | 5,261 | Flash-tier conversational model with hybrid architecture (bailing_hybrid). |
| [Mach-1-Additive-35B](https://huggingface.co/SyzygyResearch/Mach-1-Additive-35B) | SyzygyResearch | 114 | 2,129 | Ternary/additive 35B MoE built on Qwen3.5-MoE — experimental but intriguing. |

### 🎨 Multimodal & Generation

| Model | Author | Likes | Downloads | Why It's Trending |
|-------|--------|-------|-----------|-------------------|
| [MiniMax-H3](https://huggingface.co/MiniMaxAI/MiniMax-H3) | MiniMaxAI | 3,420 | 47,468 | The week's breakout image-text-to-video model from MiniMax; base for dozens of derivatives. |
| [FLUX.1-dev](https://huggingface.co/black-forest-labs/FLUX.1-dev) | black-forest-labs | 14,076 | 480,762 | Still the most-liked text-to-image model on the Hub; evergreen popularity. |
| [Muse-Glimmer-30B](https://huggingface.co/meta-models/Muse-Glimmer-30B) | meta-models | 671 | 0 | Meta's new 30B image-text-to-text model — early buzz, no downloads yet (fresh release). |
| [Unlimited-OCR](https://huggingface.co/baidu/Unlimited-OCR) | baidu | 4,001 | 2,921,751 | Baidu's OCR powerhouse; massive download count and strong community adoption. |
| [NVIDIA-NemotronLabs-VoiceChat-11B](https://huggingface.co/nvidia/NVIDIA-NemotronLabs-VoiceChat-11B) | nvidia | 295 | 597 | NVIDIA's voice-chat model, backed by multiple arxiv papers. |
| [BigBang-v1](https://huggingface.co/endless-frontier/BigBang-v1) | endless-frontier | 150 | 617 | Qwen3.5-MoE-based multimodal conversational model. |

### 🔧 Specialized Models

| Model | Author | Likes | Downloads | Why It's Trending |
|-------|--------|-------|-----------|-------------------|
| [Shieldstral-1.0-3B](https://huggingface.co/mistralai/Shieldstral-1.0-3B) | mistralai | 221 | 6,343 | Mistral's 3B safety guardrail model, vLLM-compatible. |

### 📦 Fine-tunes & Quantizations

| Model | Author | Likes | Downloads | Why It's Trending |
|-------|--------|-------|-----------|-------------------|
| [Comfy-Org/MiniMax-H3](https://huggingface.co/Comfy-Org/MiniMax-H3) | Comfy-Org | 1,142 | 6,009,639 | The de facto ComfyUI port of MiniMax-H3 — staggering download numbers. |
| [DavidAU/Qwen3.6-27B-Fable-Fusion-711...](https://huggingface.co/DavidAU/Qwen3.6-27B-Fable-Fusion-711-Uncensored-Heretic-NM-DAU-NEO-MAX-MTP-GGUF) | DavidAU | 1,857 | 2,439,083 | Monster GGUF merged fine-tune; "uncensored heretic" niche is exploding. |
| [unsloth/DeepSeek-V4-Flash-0731-GGUF](https://huggingface.co/unsloth/DeepSeek-V4-Flash-0731-GGUF) | unsloth | 636 | 199,167 | Official unsloth-quantized DeepSeek V4 Flash. |
| [larryvrh/MiniMax-H3-Turbo-Lora](https://huggingface.co/larryvrh/MiniMax-H3-Turbo-Lora) | larryvrh | 596 | 0 | LoRA for MiniMax-H3 Turbo — text-to-video + text-to-audio. |
| [realrebelai/MiniMax-H3_GGUFs](https://huggingface.co/realrebelai/MiniMax-H3_GGUFs) | realrebelai | 192 | 174,862 | Community GGUF quantizations of MiniMax-H3. |
| [Abiray/Minimax-H3-nvfp4-INT4-INT8-Convrot](https://huggingface.co/Abiray/Minimax-H3-nvfp4-INT4-INT8-Convrot) | Abiray | 162 | 530,052 | Quantized/video-to-video variant of MiniMax-H3; high downloads. |
| [SexGod1979/PinkCherry_MiniMax-H3](https://huggingface.co/SexGod1979/PinkCherry_MiniMax-H3) | SexGod1979 | 248 | 0 | Uncensored fine-tune of MiniMax-H3; trending in the "heretic" niche. |

---

## 3. 🌐 Ecosystem Signal

**MiniMax-H3 is the clear breakout star** — not just as a model, but as an ecosystem. The combination of a strong base model + ComfyUI port + LoRAs + GGUFs + uncensored fine-tunes demonstrates how quickly a single release can spawn a full derivative stack (6M+ downloads on the Comfy port alone). This pattern mirrors the FLUX.1-dev playbook and signals that **video generation is becoming as community-extensible as image generation**.

**Chinese labs continue to dominate the charts**: Moonshot (Kimi-K3), MiniMax (H3), DeepSeek (V4-Flash), and Baidu (Unlimited-OCR) hold top positions. Their open-weight releases are increasingly the default choice for both commercial and community use, rivaling (and in some cases surpassing) Western labs' adoption rates.

**The "Heretic/Uncensored" trend is now a full sub-ecosystem**: Qwen3-VL + MiniMax-H3 + LoRA merges with names like "Ultra-Heretic" and "PinkCherry" show sustained demand for unrestricted models, with dedicated GGUF/INT8/NVFP4 quantizations. This raises ongoing questions about alignment vs. openness.

**Quantization remains a critical distribution layer**: Almost every top model now ships with an official or community GGUF variant (unsloth, LiquidAI, realrebelai). Zero-download models with high likes suggest speculative collection of newly-released checkpoints, particularly for Meta and MiniMax artifacts.

---

## 4. 💎 Worth Exploring

1. **[Kimi-K3](https://huggingface.co/moonshotai/Kimi-K3)** — The week's most-liked model (10.4K) with 1.5M downloads. Its use of **compressed-tensors** and a compact multimodal design makes it a benchmark-worthy study in efficient vision-language modeling. If your stack needs a fast, capable VL model, this is the one to try.

2. **[MiniMax-H3](https://huggingface.co/MiniMaxAI/MiniMax-H3) + [Comfy-Org port](https://huggingface.co/Comfy-Org/MiniMax-H3)** — The hottest video-generation model of the week. With 6M downloads on the ComfyUI port, it's the most practical path to state-of-the-art text/image-to-video in a local pipeline. Watch the [Turbo-LoRA](https://huggingface.co/larryvrh/MiniMax-H3-Turbo-Lora) for speed optimizations.

3. **[Muse-Glimmer-30B](https://huggingface.co/meta-models/Muse-Glimmer-30B)** — Zero downloads yet, but 671 likes in its debut week. As Meta's newest image-text-to-text model (and already with GGUF variants from unsloth and meta-models), this is a **high-upside watchlist item** — early testers will define the community's verdict.

---
*This digest is auto-generated by [agents-radar](https://github.com/kky-wollu/agents-radar).*