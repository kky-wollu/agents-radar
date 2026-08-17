# Hugging Face Trending Models Digest 2026-08-18

> Source: [Hugging Face Hub](https://huggingface.co/) | 30 models | Generated: 2026-08-17 22:28 UTC

---

# 🤗 Hugging Face Trending Models Digest
**2026-08-18**

---

## 1. Today's Highlights

This week's Hugging Face trending list is dominated by **Qwen3.8-27B** and **MiniMax-H3** — two major releases showing that open-weight frontier models now span multiple modalities (image-text-to-text and video generation respectively). The **Kimi-K3** model from Moonshot AI has leapfrogged to the top with 10.8K likes, signaling massive community interest in compressed/feature-extraction capable architectures. Notably, **DeepSeek-V4** family shows strong adoption with both a "Pro" and "Flash" variant trending, suggesting a diversified deployment strategy (premium + lightweight). The community has been highly active with **GGUF and FP8 quantizations** of Qwen3.8-27B and Muse-Glimmer-30B, making these models accessible for local/edge inference. Finally, the rise of **video generation models** (MiniMax-H3 and derivatives like Turbo and LoRA variants) indicates a shift toward multimodal content creation as a mainstream use case.

---

## 2. Trending Models by Category

### 🧠 Language Models (LLMs, chat, instruction-tuned)

| Model | Author | Likes | Downloads |
|---|---|---|---|
| [Qwen/Qwen3.8-27B](https://huggingface.co/Qwen/Qwen3.8-27B) | Qwen | 10,692 | 415,039 |
| [deepseek-ai/DeepSeek-V4-Flash-0731](https://huggingface.co/deepseek-ai/DeepSeek-V4-Flash-0731) | deepseek-ai | 3,496 | 1,978,298 |
| [deepseek-ai/DeepSeek-V4-Pro-0813](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro-0813) | deepseek-ai | 572 | 25,006 |
| [Qwen/Qwen3.8-2.4T-A95B](https://huggingface.co/Qwen/Qwen3.8-2.4T-A95B) | Qwen | 1,040 | 9,465 |
| [Qwen/Qwen3.8-2.4T-A95B-FP8](https://huggingface.co/Qwen/Qwen3.8-2.4T-A95B-FP8) | Qwen | 219 | 12,295 |
| [nvidia/NVIDIA-Nemotron-3.5-Lightning-30B-A3B-NVFP4](https://huggingface.co/nvidia/NVIDIA-Nemotron-3.5-Lightning-30B-A3B-NVFP4) | nvidia | 307 | 231,271 |
| [nvidia/NVIDIA-Nemotron-3.5-Lightning-30B-A3B-BF16](https://huggingface.co/nvidia/NVIDIA-Nemotron-3.5-Lightning-30B-A3B-BF16) | nvidia | 169 | 69,833 |
| [LiquidAI/LFM2.5-2.6B](https://huggingface.co/LiquidAI/LFM2.5-2.6B) | LiquidAI | 653 | 147,270 |

- **Qwen3.8-27B**: Flagship multimodal LLM from Qwen (image+text-to-text) with massive 10.7K likes — the #2 most-liked model, indicating it's one of the most anticipated open releases of 2026, offering frontier-level capabilities under a permissive license.
- **DeepSeek-V4-Flash-0731**: Lightweight, fast variant of the DeepSeek V4 family with 3.5K likes and ~2M downloads — trending for delivering high-performance inference at scale, the "Flash" brand signals speed/efficiency focus.
- **DeepSeek-V4-Pro-0813**: Higher-tier sibling model from DeepSeek — trending as the premium option for users needing maximum quality from the V4 suite.
- **Qwen3.8-2.4T-A95B**: Massive 2.4T-parameter MoE model (95B active) — trending as the "frontier-scale" open-weight Mixture-of-Experts model demonstrating what's possible in open research.
- **Qwen3.8-2.4T-A95B-FP8**: FP8 quantized version of the MoE giant for reduced memory footprint.
- **NVIDIA-Nemotron-3.5-Lightning-30B-A3B-NVFP4**: NVIDIA's efficient 30B MoE model (3B active) in 4-bit NVFP4 — trending for enterprise-grade deployment with exceptional cost-efficiency.
- **NVIDIA-Nemotron-3.5-Lightning-30B-A3B-BF16**: BF16 version of the same architecture for maximum fidelity when hardware allows.
- **LiquidAI/LFM2.5-2.6B**: Small but capable 2.6B model from Liquid AI — trending for proving that smaller models can punch far above their weight class (653 likes from efficiency-focused developers).

---

### 🎨 Multimodal & Generation (image, video, audio, text-to-X)

| Model | Author | Likes | Downloads |
|---|---|---|---|
| [meta-models/Muse-Glimmer-30B](https://huggingface.co/meta-models/Muse-Glimmer-30B) | meta-models | 1,660 | 334,099 |
| [moonshotai/Kimi-K3](https://huggingface.co/moonshotai/Kimi-K3) | moonshotai | 10,800 | 2,163,953 |
| [MiniMaxAI/MiniMax-H3](https://huggingface.co/MiniMaxAI/MiniMax-H3) | MiniMaxAI | 4,086 | 2,403,238 |
| [Lightricks/LTX-2.5](https://huggingface.co/Lightricks/LTX-2.5) | Lightricks | 1,101 | 465,529 |
| [MiniMaxAI/MiniMax-Music3](https://huggingface.co/MiniMaxAI/MiniMax-Music3) | MiniMaxAI | 900 | 10,375 |
| [lightx2v/Minimax-h3-Turbo](https://huggingface.co/lightx2v/Minimax-h3-Turbo) | lightx2v | 583 | 264,351 |
| [Gazingstars123/Anima-2.9B](https://huggingface.co/Gazingstars123/Anima-2.9B) | Gazingstars123 | 233 | 23,202 |
| [inclusionAI/Ling-3.0-tiny](https://huggingface.co/inclusionAI/Ling-3.0-tiny) | inclusionAI | 301 | 6,266 |
| [LiquidAI/LFM2.5-VL-3B](https://huggingface.co/LiquidAI/LFM2.5-VL-3B) | LiquidAI | 162 | 6,816 |
| [fal/MiniMax-H3-Realism-People-LoRA](https://huggingface.co/fal/MiniMax-H3-Realism-People-LoRA) | fal | 243 | 18,562 |
| [larryvrh/MiniMax-H3-Turbo-Lora](https://huggingface.co/larryvrh/MiniMax-H3-Turbo-Lora) | larryvrh | 786 | 0 |

- **moonshotai/Kimi-K3**: Leading this category with 10.8K likes — a multimodal "image-text-to-text" model marketed with feature-extraction and compressed-tensors capabilities, indicating a novel architecture focus.
- **MiniMaxAI/MiniMax-H3**: One of the biggest video generation releases of the quarter (4K likes, 2.4M downloads), demonstrating high-quality text/image-to-video with strong prompt control, and spawning an entire ecosystem of LoRAs and derivatives.
- **meta-models/Muse-Glimmer-30B**: Multimodal 30B model from Meta (image-text-to-text) — trending with 1.66K likes as an accessible multimodal model for open-weights community.
- **Lightricks/LTX-2.5**: Image-to-video diffusion model for cinematic generation — trending due to professional-grade output quality.
- **MiniMaxAI/MiniMax-Music3**: Text-to-music generation model — trending for music industry applications.
- **lightx2v/Minimax-h3-Turbo**: Optimized Turbo version of MiniMax-H3 with faster inference.
- **Gazingstars123/Anima-2.9B**: Compact 2.9B text-to-image diffusion model for ComfyUI.
- **inclusionAI/Ling-3.0-tiny**: Hybrid-architecture tiny model with MIT license (region: US) — trending for permissive commercial use.
- **LiquidAI/LFM2.5-VL-3B**: Vision-language 3B model proving efficient multimodal performance.
- **fal/MiniMax-H3-Realism-People-LoRA**: Specialized LoRA for adding photorealistic people to MiniMax-H3 generations.
- **larryvrh/MiniMax-H3-Turbo-Lora**: Community Turbo LoRA with audio-video coupling (786 likes, 0 downloads — newly published).

---

### 🔧 Specialized Models

| Model | Author | Likes | Downloads |
|---|---|---|---|
| [Qwen/Qwen3.8-27B-FP8](https://huggingface.co/Qwen/Qwen3.8-27B-FP8) | Qwen | 526 | 495,646 |

- **Qwen3.8-27B-FP8**: Official 8-bit quantized variant for memory-constrained deployments — trending as the standard choice when hardware cannot fit the full BF16 model while still needing solid quality.

---

### 📦 Fine-tunes & Quantizations

| Model | Author | Likes | Downloads |
|---|---|---|---|
| [unsloth/Qwen3.8-27B-GGUF](https://huggingface.co/unsloth/Qwen3.8-27B-GGUF) | unsloth | 1,622 | 2,727,609 |
| [Comfy-Org/MiniMax-H3](https://huggingface.co/Comfy-Org/MiniMax-H3) | Comfy-Org | 1,402 | 14,015,769 |
| [DavidAU/Qwen3.6-27B-Fable-Fusion-711-Uncensored-Heretic-NM-DAU-NEO-MAX-MTP-GGUF](https://huggingface.co/DavidAU/Qwen3.6-27B-Fable-Fusion-711-Uncensored-Heretic-NM-DAU-NEO-MAX-MTP-GGUF) | DavidAU | 2,117 | 3,033,928 |
| [unsloth/Muse-Glimmer-30B-GGUF](https://huggingface.co/unsloth/Muse-Glimmer-30B-GGUF) | unsloth | 470 | 755,125 |
| [unsloth/Qwen3.8-27B-NVFP4](https://huggingface.co/unsloth/Qwen3.8-27B-NVFP4) | unsloth | 236 | 378,177 |
| [JonathanColetti/Qwen3.8-27B-Uncensored-GGUF](https://huggingface.co/JonathanColetti/Qwen3.8-27B-Uncensored-GGUF) | JonathanColetti | 295 | 357,701 |
| [orcarouter/Qwen3.8-27B-Uncensored-FP8](https://huggingface.co/orcarouter/Qwen3.8-27B-Uncensored-FP8) | orcarouter | 428 | 15,812 |
| [Comfy-Org/MiniMax-Music-3](https://huggingface.co/Comfy-Org/MiniMax-Music-3) | Comfy-Org | 166 | 256,988 |
| [froggeric/Qwen-Fixed-Chat-Templates](https://huggingface.co/froggeric/Qwen-Fixed-Chat-Templates) | froggeric | 1,206 | 0 |

- **unsloth/Qwen3.8-27B-GGUF**: The go-to GGUF quantization for local/CPU inference — the 2.7M downloads confirm it as THE edge-deployment standard for Qwen3.8.
- **Comfy-Org/MiniMax-H3**: ComfyUI-packaged single-file version — a staggering **14M downloads** proves user demand for "ready-to-run" video models through Comfy's node interface.
- **DavidAU/Qwen3.6-27B-Fable-Fusion-...**: An extremely fine-tuned, uncensored GGUF variant capturing 3M downloads — trending for the community's appetite for heavily modified, niche fine-tunes.
- **unsloth/Muse-Glimmer-30B-GGUF**: GGUF for Meta's multimodal model — 755K downloads showing demand for local multimodal inference.
- **unsloth/Qwen3.8-27B-NVFP4**: NVIDIA-optimized 4-bit format for enterprise GPUs.
- **JonathanColetti/Qwen3.8-27B-Uncensored-GGUF**: Uncensored GGUF variant removing alignment restrictions.
- **orcarouter/Qwen3.8-27B-Uncensored-FP8**: FP8 abliterated version for those wanting "rawer" output on NVIDIA hardware.
- **Comfy-Org/MiniMax-Music-3**: Comfy-single-file for music generation.
- **froggeric/Qwen-Fixed-Chat-Templates**: Highly useful (1.2K likes!) MLX/Jinja chat-template fix for Qwen3.5 — trending as a must-have quality-of-life download (0 downloads, likely newly released this week).

---

## 3. Ecosystem Signal

The current HF landscape shows **three dominant families** — Qwen3.8, MiniMax-H3, and Kimi-K3 — each anchoring its own ecosystem. Multi-modality is now the norm: image-text-to-text and text/image-to-video are the default "major release" formats, not novelty features. Open-weight developments are clearly leading, with all top-10 models being openly downloadable (Qwen, DeepSeek, Meta, MiniMax, Moonshot), significantly outpacing proprietary-only counterparts.

Quantization has become industrialized: every major release now ships with official or partner (unsloth/Comfy-Org) GGUF, FP8, or NVFP4 variants within 48 hours, dramatically lowering hardware barriers. The massive download numbers for Comfy-Org variants (14M) reinforce that **ease-of-use infrastructure** is as important as model quality. Meanwhile, niche fine-tunes (uncensored variants, creative blends like the "Fable-Fusion" model) show a highly engaged community pushing creative boundaries even if they deviate from "safety" norms. The presence of small models (2.6B–3B from LiquidAI, Gazingstars, inclusionAI) signals a parallel trend toward efficient, task-specific "small language/vision models" that can run on consumer hardware — a deliberate counterweight to the frontier-scale approach.

---

## 4. Worth Exploring

**1. [Qwen/Qwen3.8-27B](https://huggingface.co/Qwen/Qwen3.8-27B)** — The centerpiece of the current ecosystem. As the 2nd most-liked model on the platform, it represents the current state-of-the-art in open multimodal LLMs. Trying it, along with the **unsloth GGUF** version, provides the clearest picture of where open-weight research is heading in 2026.

**2. [MiniMaxAI/MiniMax-H3](https://huggingface.co/MiniMaxAI/MiniMax-H3) + [Comfy-Org/MiniMax-H3](https://huggingface.co/Comfy-Org/MiniMax-H3)** — The video generation release everybody is using (4K likes, 14M downloads on the Comfy variant). It's an excellent study in how a platform can successfully bridge state-of-the-art video generation into mainstream user workflows.

**3. [moonshotai/Kimi-K3](https://huggingface.co/moonshotai/Kimi-K3)** — Despite having the highest like count (10.8K), this model is arguably the least well-understood on this list. Its unique combination of image-text-to-text, feature-extraction, and compressed-tensors tags suggests an architectural novelty worth studying closely — potentially foreshadowing the next generation of memory and compute-efficient multimodal models.

---
*This digest is auto-generated by [agents-radar](https://github.com/kky-wollu/agents-radar).*