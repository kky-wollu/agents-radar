# Hugging Face Trending Models Digest 2026-08-15

> Source: [Hugging Face Hub](https://huggingface.co/) | 30 models | Generated: 2026-08-14 22:28 UTC

---

# Hugging Face Trending Models Digest — 2026-08-15

---

## 1. Today's Highlights

The spotlight this week is on two frontier-scale releases: **Qwen3.8** (now offering a 27B dense and a massive 2.4T MoE with 95B active parameters) and **Meta's Muse-Glimmer-30B**, a multimodal conversation model that is seeing heavy adoption via community GGUF quantizations. The **MiniMax-H3** video generation family continues to dominate ecosystem activity, with a Turbo variant, community LoRAs, and ComfyUI integrations spreading across the board. NVIDIA counters with a fast, compact **Nemotron-3.5 Lightning 30B-A3B** in both NVFP4 and BF16, while DeepSeek's V4 lineup shows a clear split between a widely-adopted Flash model and a more recent Pro checkpoint. Notably, **Kimi-K3** from Moonshot leads in weekly likes with 10.6K, suggesting compressed-tensor multimodal models are capturing significant developer attention.

---

## 2. Trending Models by Category

### 🧠 Language Models (LLMs, chat models, instruction-tuned)

| Model | Author | Likes | Downloads |
|---|---|---|---|
| [Qwen3.8-2.4T-A95B](https://huggingface.co/Qwen/Qwen3.8-2.4T-A95B) | Qwen | 909 | 3,832 |
| [DeepSeek-V4-Flash-0731](https://huggingface.co/deepseek-ai/DeepSeek-V4-Flash-0731) | deepseek-ai | 3,378 | 1.6M |
| [DeepSeek-V4-Pro-0813](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro-0813) | deepseek-ai | 429 | 245 |
| [NVIDIA-Nemotron-3.5-Lightning-30B-A3B-NVFP4](https://huggingface.co/nvidia/NVIDIA-Nemotron-3.5-Lightning-30B-A3B-NVFP4) | nvidia | 257 | 119,572 |
| [NVIDIA-Nemotron-3.5-Lightning-30B-A3B-BF16](https://huggingface.co/nvidia/NVIDIA-Nemotron-3.5-Lightning-30B-A3B-BF16) | nvidia | 141 | 34,137 |
| [LiquidAI/LFM2.5-2.6B](https://huggingface.co/LiquidAI/LFM2.5-2.6B) | LiquidAI | 614 | 124,172 |

- **Qwen3.8-2.4T-A95B**: Qwen's MoE flagship with 2.4T total parameters and 95B active, setting a new bar for open-weight scale.
- **DeepSeek-V4-Flash-0731**: The widely-adopted Lightning-style model in the V4 line with 1.6M downloads and strong community momentum.
- **DeepSeek-V4-Pro-0813**: The higher-capability Pro variant, just released and in early rollout.
- **NVIDIA Nemotron-Lightning variants (BF16 & NVFP4)**: A 30B-A3B hybrid that delivers top-tier performance with low inference cost, available in both dense and 4-bit quantized formats.
- **LFM2.5-2.6B**: Liquid's compact, efficient model gaining traction as an edge-friendly LLM.

### 🎨 Multimodal & Generation (image, video, audio, text-to-X)

| Model | Author | Likes | Downloads |
|---|---|---|---|
| [Qwen3.8-27B](https://huggingface.co/Qwen/Qwen3.8-27B) | Qwen | 8,869 | 2 |
| [Muse-Glimmer-30B](https://huggingface.co/meta-models/Muse-Glimmer-30B) | meta-models | 1,507 | 165K |
| [MiniMax-H3](https://huggingface.co/MiniMaxAI/MiniMax-H3) | MiniMaxAI | 3,916 | 1.99M |
| [LTX-2.5](https://huggingface.co/Lightricks/LTX-2.5) | Lightricks | 847 | 208K |
| [MiniMax-Music3](https://huggingface.co/MiniMaxAI/MiniMax-Music3) | MiniMaxAI | 645 | 63 |
| [Minimax-h3-Turbo](https://huggingface.co/lightx2v/Minimax-h3-Turbo) | lightx2v | 493 | 150K |
| [MiniMax-H3 (Comfy-Org)](https://huggingface.co/Comfy-Org/MiniMax-H3) | Comfy-Org | 1,316 | 11.77M |
| [Anima-2.9B](https://huggingface.co/Gazingstars123/Anima-2.9B) | Gazingstars123 | 158 | 10K |
| [Kimi-K3](https://huggingface.co/moonshotai/Kimi-K3) | moonshotai | 10,666 | 1.97M |

- **Qwen3.8-27B**: Qwen's 27B vision-language model — the most-liked release this week, signaling strong appetite for capable open multimodal chat models.
- **Muse-Glimmer-30B**: Meta's new multimodal conversation model with 30B parameters, seeing immediate and heavy community adoption.
- **MiniMax-H3**: The dominant open text/image-to-video model, with a massive 1.9M downloads on main and 11.7M via the ComfyUI single-file distribution.
- **LTX-2.5**: Lightricks' next-gen image-to-video model with multi-format inputs, building on the success of LTX-Video.
- **MiniMax-Music3**: A new text-to-music model from MiniMax, early but showing promise.
- **Minimax-h3-Turbo**: Accelerated inference variant of MiniMax-H3 with faster generation, very strong early adoption.
- **Kimi-K3**: Moonshot's compressed-tensor multimodal model — top likes this week, indicating strong user interest in efficient high-quality MLLMs.

### 🔧 Specialized Models (code, math, medical, embeddings)

*No dedicated specialized models (e.g., code-specific, embedding) appeared in this week's top-30 trending list.*

### 📦 Fine-tunes & Quantizations (community fine-tunes, GGUF, AWQ)

| Model | Author | Likes | Downloads |
|---|---|---|---|
| [Qwen3.8-27B-GGUF](https://huggingface.co/unsloth/Qwen3.8-27B-GGUF) | unsloth | 734 | 0 |
| [Muse-Glimmer-30B-GGUF](https://huggingface.co/unsloth/Muse-Glimmer-30B-GGUF) | unsloth | 414 | 597K |
| [Muse-Glimmer-30B-GGUF](https://huggingface.co/meta-models/Muse-Glimmer-30B-GGUF) | meta-models | 268 | 228K |
| [Qwen3.8-27B-FP8](https://huggingface.co/Qwen/Qwen3.8-27B-FP8) | Qwen | 282 | 0 |
| [Qwen3.8-2.4T-A95B-FP8](https://huggingface.co/Qwen/Qwen3.8-2.4T-A95B-FP8) | Qwen | 183 | 9,334 |
| [Qwen3.6-27B-Fable-Fusion-711-Uncensored-Heretic-NM-DAU-NEO-MAX-MTP-GGUF](https://huggingface.co/DavidAU/Qwen3.6-27B-Fable-Fusion-711-Uncensored-Heretic-NM-DAU-NEO-MAX-MTP-GGUF) | DavidAU | 2,014 | 2.89M |
| [MiniMax-H3-Turbo-Lora](https://huggingface.co/larryvrh/MiniMax-H3-Turbo-Lora) | larryvrh | 741 | 0 |
| [MiniMax-H3-Realism-People-LoRA](https://huggingface.co/fal/MiniMax-H3-Realism-People-LoRA) | fal | 174 | 9,060 |
| [MiniMax-H3-GGUF](https://huggingface.co/unsloth/MiniMax-H3-GGUF) | unsloth | 155 | 137K |
| [MiniMax-H3-Turbo-Lora-ComfyUI](https://huggingface.co/drbaph/MiniMax-H3-Turbo-Lora-ComfyUI) | drbaph | 318 | 113K |
| [NVIDIA-NemotronLabs-VoiceChat-11B](https://huggingface.co/nvidia/NVIDIA-NemotronLabs-VoiceChat-11B) | nvidia | 380 | 1,366 |

- **unsloth/Muse-Glimmer-30B-GGUF**: The fastest path to running Meta's new multimodal model locally; already at 597K downloads.
- **Qwen3.6-27B-Fable-Fusion…DAU-NEO-MAX**: A community fine-tune of Qwen3.6 with 2.89M downloads, showcasing persistent demand for creative/uncensored variants.
- **MiniMax-H3 GGUF & LoRA family**: Platform-level ecosystem around MiniMax-H3 — single-file ComfyUI weights, Turbo LoRAs (including a Realism/People LoRA from fal) — indicating a healthy video-model plugin ecosystem.

---

## 3. Ecosystem Signal

Observing the trending list, the video-generation ecosystem around **MiniMax-H3** is the most energetic frontier: the base model, a Turbo variant, ComfyUI single-file distribution, GGUF, LoRAs (including specialized tuning for realism and people), all appearing simultaneously in the top-30. This is a mature open-weight ecosystem pattern resembling what Stable Diffusion achieved for image generation, now repeating for video.

On the language side, **Qwen** and **DeepSeek** are waging a "frontier MoE + dense" dual strategy, with Qwen's 2.4T-A95B leading in raw capability while DeepSeek's V4 Flash is maximizing developer adoption. **Meta's Muse-Glimmer-30B** is an important flagship because it runs on consumer hardware at 30B scale and commands 1.5K likes in one week — strong signal of community desire for multimodal chat models that aren't huge.

Quantization and fine-tuning activity also reveal a clear pattern: **unsloth** remains the indispensable bridge to local deployment in GGUF format, while **Comfy-Org** single-file distributions are becoming the distribution default for video models. Open-weight momentum is strongest in the 27B–30B range — the sweet spot between capability and local runtime viability — and in 4-bit formats (NVFP4, GGUF, FP8).

---

## 4. Worth Exploring

1. **Kimi-K3** — It has the highest weekly likes in the entire list (10.6K) and is a compressed-tensor multimodal model. Understanding how Moonshot is achieving compression while retaining multi-modal understanding could be a major architectural signal for the rest of the ecosystem.

2. **Qwen3.8-27B** — 8.8K likes on a fresh release is exceptional, and this is the official dense/flagship model from Qwen. It's worth studying for its vision-language reasoning, likely the best open-weight option at 27B scale in the near term.

3. **MiniMax-H3-Turbo-Lora-ComfyUI** — The combination of the Turbo variant and a ComfyUI-ready LoRA is a neatly packaged, fast, local video-to-text/audio pipeline. It demonstrates the new standard for streamlined video generation workflows and is representative of how an entire production stack is coalescing around one model family.

---
*This digest is auto-generated by [agents-radar](https://github.com/kky-wollu/agents-radar).*