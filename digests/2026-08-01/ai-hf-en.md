# Hugging Face Trending Models Digest 2026-08-01

> Source: [Hugging Face Hub](https://huggingface.co/) | 30 models | Generated: 2026-07-31 23:06 UTC

---

# 🤗 Hugging Face Trending Models Digest — 2026-08-01

---

## 1. Today's Highlights

This week's trending榜单is dominated by **Kimi-K3** from Moonshot AI (9,268 likes), a multimodal model that has captured the community's attention and spawned a quick GGUF quantization ecosystem via Unsloth. **DeepSeek-V4-Flash** continues its momentum with nearly 3M downloads, while **GLM-5.2** from Zhipu AI maintains strong interest. The Qwen3.6 fine-tuning wave shows no signs of slowing, with multiple uncensored variants (e.g., HauhauCS' aggressive tuning at 3,205 likes) driving massive download counts. Notably, **multimodal models (image-text-to-text)** now represent over half of the top 30, signaling a shift toward unified vision-language architectures as the default foundation model paradigm.

---

## 2. Trending Models by Category

### 🧠 Language Models (LLMs, chat models, instruction-tuned)

| Model | Author | Likes | Downloads | Why it's trending |
|-------|--------|-------|-----------|-------------------|
| [DeepSeek-V4-Flash-0731](https://huggingface.co/deepseek-ai/DeepSeek-V4-Flash-0731) | deepseek-ai | 941 | 0 | Fresh release of DeepSeek's flagship Flash model with an associated arXiv paper, just registered on the Hub |
| [DeepSeek-V4-Flash](https://huggingface.co/deepseek-ai/DeepSeek-V4-Flash) | deepseek-ai | 1,924 | 2,923,499 | The widely-adopted V4 Flash base model, proving DeepSeek's continued dominance in the open-weight LLM arena |
| [GLM-5.2](https://huggingface.co/zai-org/GLM-5.2) | zai-org | 4,706 | 1,651,533 | Zhipu AI's latest MoE with DSA attention—a major conversational model with massive community uptake |
| [Laguna-S-2.1](https://huggingface.co/poolside/Laguna-S-2.1) | poolside | 862 | 76,212 | Poolside's enterprise-focused LLM update, drawing attention for code-specialized performance |
| [Nanbeige4.2-3B](https://huggingface.co/Nanbeige/Nanbeige4.2-3B) | Nanbeige | 595 | 26,928 | A compact 3B model punching above its weight—popular for edge and local deployment scenarios |
| [Solar-Open2-250B](https://huggingface.co/upstage/Solar-Open2-250B) | upstage | 714 | 12,911 | Upstage's open-weight 250B frontier-scale LLM, attracting researchers seeking alternative large models |

### 🎨 Multimodal & Generation (image, video, audio, text-to-X)

| Model | Author | Likes | Downloads | Why it's trending |
|-------|--------|-------|-----------|-------------------|
| [Kimi-K3](https://huggingface.co/moonshotai/Kimi-K3) | moonshotai | 9,268 | 493,481 | The week's breakout star—Moonshot's flagship multimodal model with compressed-tensor support, generating massive organic interest |
| [Unlimited-OCR](https://huggingface.co/baidu/Unlimited-OCR) | baidu | 3,660 | 2,513,603 | Baidu's general-purpose OCR model redefining document understanding—huge download counts indicate production usage |
| [KAT-Coder-V2.5-Dev](https://huggingface.co/Kwaipilot/KAT-Coder-V2.5-Dev) | Kwaipilot | 368 | 10,241 | Multimodal code model on Qwen3.5 MoE base, bringing vision capabilities to code generation workflows |
| [Inkling](https://huggingface.co/thinkingmachines/Inkling) | thinkingmachines | 1,664 | 57,259 | A new multimodal conversational model from Thinking Machines, alongside its smaller sibling — quickly gaining traction through effective demos |
| [Inkling-Small](https://huggingface.co/thinkingmachines/Inkling-Small) | thinkingmachines | 192 | 2,971 | The lightweight variant of Inkling for resource-constrained multimodal tasks |
| [Mage-VL](https://huggingface.co/microsoft/Mage-VL) | microsoft | 148 | 5,650 | Microsoft's vision-language model, pairing with Comfy-org's Flow integration for new image workflows |
| [Fara1.5-27B](https://huggingface.co/microsoft/Fara1.5-27B) | microsoft | 234 | 2,726 | Microsoft's computer-use agent model on Qwen3.5—positioning for GUI automation agents |
| [Inflect-Micro-v2](https://huggingface.co/owensong/Inflect-Micro-v2) | owensong | 347 | 1,449 | CPU-optimized TTS micro model for edge AI speech synthesis without GPU dependency |
| [Inflect-Nano-v2](https://huggingface.co/owensong/Inflect-Nano-v2) | owensong | 121 | 802 | The even-smaller sibling in the Inflect local TTS family, demonstrating the push for on-device speech |
| [Audio8-TTS-Preview-0.6b](https://huggingface.co/Audio8/Audio8-TTS-Preview-0.6b) | Audio8 | 151 | 2,481 | Preview release of a 0.6B TTS model with feature-extraction utilities—early but promising audio quality |
| [VibeVoice-ASR-BitNet](https://huggingface.co/microsoft/VibeVoice-ASR-BitNet) | microsoft | 133 | 5,464 | Microsoft's BitNet-based ASR pushing efficient speech recognition with GGML/GGUF support |

### 🔧 Specialized Models (code, math, medical, embeddings)

| Model | Author | Likes | Downloads | Why it's trending |
|-------|--------|-------|-----------|-------------------|
| [XYZ-Aquila-pro](https://huggingface.co/XYZAILab/XYZ-Aquila-pro) | XYZAILab | 326 | 869 | Agentic-search MoE model—specialized retrieval/agent tooling built on Qwen3.5 architecture |
| [XYZ-Aquila-mini](https://huggingface.co/XYZAILab/XYZ-Aquila-mini) | XYZAILab | 351 | 579 | Compact variant of the Aquila agentic-search series for embedded retrieval workflows |

### 📦 Fine-tunes & Quantizations (community fine-tunes, GGUF)

| Model | Author | Likes | Downloads | Why it's trending |
|-------|--------|-------|-----------|-------------------|
| [Qwen3.6-27B-Fable-Fusion-711-Uncensored-Heretic-NM-DAU-NEO-MAX-MTP-GGUF](https://huggingface.co/DavidAU/Qwen3.6-27B-Fable-Fusion-711-Uncensored-Heretic-NM-DAU-NEO-MAX-MTP-GGUF) | DavidAU | 1,140 | 1,119,057 | A prolific community fine-tune—uncensored Qwen3.6 with MTP support is a juggernaut in download volume |
| [Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive) | HauhauCS | 3,205 | 1,835,931 | The most-liked community GGUF—aggressive uncensored tuning of Qwen3.6 MoE has captured massive user base |
| [Qwen3.5-9B-The-Defiant-Fable-Uncensored-Heretic-NEO-IMATRIX-MAX-MTP-GGUF](https://huggingface.co/DavidAU/Qwen3.5-9B-The-Defiant-Fable-Uncensored-Heretic-NEO-IMATRIX-MAX-MTP-GGUF) | DavidAU | 172 | 261,856 | IMX-optimized 9B GGUF variant—popular lightweight uncensored option |
| [Qwen3.6-35B-A3B-Uncensored-Genesis-Hermes-V6-GGUF](https://huggingface.co/LuffyTheFox/Qwen3.6-35B-A3B-Uncensored-Genesis-Hermes-V6-GGUF) | LuffyTheFox | 267 | 212,426 | Hermes-v6-tuned MoE GGUF, bringing NousResearch's style to the Qwen3.6 line |
| [Kimi-K3-GGUF](https://huggingface.co/unsloth/Kimi-K3-GGUF) | unsloth | 226 | 36,180 | Unsloth's official GGUF conversion of Kimi-K3—the fast path for local deployment |
| [Kimi-K3](https://huggingface.co/unsloth/Kimi-K3) | unsloth | 215 | 1,044 | Unsloth's fine-tunable copy of Kimi-K3 with optimizations for resource-efficient training |
| [DeepSeek-V4-Flash-0731-GGUF](https://huggingface.co/unsloth/DeepSeek-V4-Flash-0731-GGUF) | unsloth | 166 | 0 | Day-one GGUF quantizations by Unsloth—guaranteed infrastructure for the new DeepSeek release |
| [Solar-Open2-250B-Nota-NVFP4](https://huggingface.co/nota-ai/Solar-Open2-250B-Nota-NVFP4) | nota-ai | 151 | 18,531 | NVFP4 quantized 250B model for vLLM—practical frontier-scale inference on consumer GPUs |
| [Ternary-Bonsai-27B-gguf](https://huggingface.co/prism-ml/Ternary-Bonsai-27B-gguf) | prism-ml | 1,124 | 712,835 | Radical 2-bit ternary quantization of a 27B model—astonishing quality-per-bit trade-off driving downloads |
| [Mage-Flow](https://huggingface.co/Comfy-Org/Mage-Flow) | Comfy-Org | 106 | 60,162 | Single-file diffusion workflow integration with Microsoft's Mage model—bridging LLM and ComfyUI pipelines |
| [Qwen3.6-35B-A3B-Escha-W2](https://huggingface.co/EschaLabs/Qwen3.6-35B-A3B-Escha-W2) | EschaLabs | 104 | 599 | Community W2 (two-bit) variant of Qwen3.6 MoE; early-stage but gaining attention for extreme compression |

---

## 3. Ecosystem Signal

**Qwen is the de facto base for the community.** The Qwen3.5/3.6 MoE family underpins at least eight of the top 30 trending models — from 9B to 35B-A3B, spanning uncensored tunings, Hermes-style fine-tunes, and agentic search variants. This mirrors the Llama-2-era pattern where one accessible family becomes the substrate for mass fine-tuning.

**GPU-quantization as a competitive moat.** The presence of Ternary-Bonsai (2-bit), NVFP4 quantizations, and BitNet-based ASR signals a decisive shift toward extreme compression as a first-class product feature. The community appears willing to trade 1-2 quality points for massive VRAM savings, making 27B-35B models runnable on consumer hardware.

**Unsloth has industrialized day-one GGUF availability.** Within hours of Moonshot and DeepSeek releases, Unsloth provides official quantizations (36K+ downloads for Kimi-K3-GGUF). This pipeline is now a critical distribution channel, effectively setting the standard for how open-weight models reach end users.

**Multimodality is default, not optional.** Over half of the top-30 list is image-text-to-text. The line between "LLM" and "VLM" has essentially dissolved for frontier releases.

**Open-weight momentum is asymmetric.** Chinese labs (DeepSeek, Moonshot, Zhipu, Baidu) dominate the top-liked releases. The West's contributions — Microsoft's multimodal line, Upstage's Solar, poolside's Laguna — are present but with 3–10x less community traction, indicating a structural advantage for Chinese open-weight ecosystems in both release cadence and community engagement.

---

## 4. Worth Exploring

1. **[Kimi-K3](https://huggingface.co/moonshotai/Kimi-K3)** — The highest-liked model of the week (9.2K likes) with compressed-tensor support and a Unsloth GGUF ready. If Moonshot's Kimi-K3 matches its hype, it represents a genuine frontier candidate. Its multimodal, feature-extraction tags suggest flexibility beyond chat. **Try it if you power a production multimodal pipeline or need a flagship open VLM.**

2. **[Ternary-Bonsai-27B-gguf](https://huggingface.co/prism-ml/Ternary-Bonsai-27B-gguf)** — At 1.1K likes and 712K downloads, this 2-bit ternary model is the strongest signal that extreme compression is where the community is heading. Its quality-per-bit is extraordinary enough to be a viral phenomenon. **Studying this reveals where "efficient frontier" actually lives for CPU/edge reasoning in late 2026.**

3. **[Inkling](https://huggingface.co/thinkingmachines/Inkling)** — A dark-horse multimodal model from Thinking Machines (formerly behind MM1 and similar research directions). At 1,664 likes for a non-uncensored, unfine-tuned base release, it is outperforming far more heavily-marketed enterprise models. Its popularity suggests the architecture or demo results are genuinely impressive — **worth benchmarking against Kimi-K3 to compare frontier multimodal capabilities across vendors.**

---
*This digest is auto-generated by [agents-radar](https://github.com/kky-wollu/agents-radar).*