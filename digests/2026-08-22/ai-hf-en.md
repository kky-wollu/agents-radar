# Hugging Face Trending Models Digest 2026-08-22

> Source: [Hugging Face Hub](https://huggingface.co/) | 30 models | Generated: 2026-08-21 22:29 UTC

---

# 🤖 Hugging Face Trending Models Digest — 2026-08-22

---

## 1. Today's Highlights

Qwen's **Qwen3.8-27B** dominates the hub this week, amassing nearly 12K likes and 1.7M downloads, with an entire ecosystem of quantized, abliterated, and uncensored variants trailing close behind—clear evidence that the open-weight community is building fast on this release. **MiniMax-H3** continues its viral run with 4.3K likes and 3.6M downloads for video generation, while **Kimi-K3** from Moonshot AI debuts strong with 10.9K likes, signaling renewed momentum in compressed/latent-space models. DeepSeek's V4 line shows up with both **Pro** and **Flash** variants, indicating a two-tier strategy (quality vs. speed/efficiency) that's becoming standard for frontier labs. The sheer volume of GGUF and abliterated fine-tunes (at least 10 of the 30 entries) reveals an extremely active community layer focused on local deployment and uncensored use cases. Notably, the **Uncensored** variants of Qwen3.8 are consistently outperforming many official releases in downloads, suggesting strong demand for both creative freedom and runnable formats.

---

## 2. Trending Models by Category

### 🧠 Language Models (LLMs, chat models, instruction-tuned)

| Model | Author | Likes | Downloads |
|---|---|---|---|
| [Qwen/Qwen3.8-27B](https://huggingface.co/Qwen/Qwen3.8-27B) | Qwen | 11,943 | 1,726,651 |
| [deepseek-ai/DeepSeek-V4-Pro-0813](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro-0813) | deepseek-ai | 704 | 49,601 |
| [Qwen/Qwen3.8-2.4T-A95B](https://huggingface.co/Qwen/Qwen3.8-2.4T-A95B) | Qwen | 1,135 | 15,702 |
| [moonshotai/Kimi-K3](https://huggingface.co/moonshotai/Kimi-K3) | moonshotai | 10,910 | 2,448,810 |
| [meta-models/Muse-Glimmer-30B](https://huggingface.co/meta-models/Muse-Glimmer-30B) | meta-models | 1,731 | 505,113 |
| [deepseek-ai/DeepSeek-V4-Flash-0731](https://huggingface.co/deepseek-ai/DeepSeek-V4-Flash-0731) | deepseek-ai | 3,605 | 2,833,064 |

**Qwen3.8-27B** is the flagship multimodal + text model from Qwen that has ignited the community with strong reasoning and vision capabilities. **DeepSeek-V4-Pro-0813** is the new frontier open-weight LLM that brings competitive performance for its size. **Qwen3.8-2.4T-A95B** is Qwen's massive MoE model (2.4T total params, 95B active) targeting enterprise-scale reasoning. **Kimi-K3** is Moonshot AI's compressed-latent model, generating buzz for efficient long-context handling. **Muse-Glimmer-30B** is Meta's image-text-to-text model that blurs the line between LLM and multimodal understanding. **DeepSeek-V4-Flash-0731** is the speed-optimized sibling of V4-Pro, designed for low-latency inference.

---

### 🎨 Multimodal & Generation (image, video, audio, text-to-X)

| Model | Author | Likes | Downloads |
|---|---|---|---|
| [MiniMaxAI/MiniMax-Music3](https://huggingface.co/MiniMaxAI/MiniMax-Music3) | MiniMaxAI | 1,157 | 15,678 |
| [Lightricks/LTX-2.5](https://huggingface.co/Lightricks/LTX-2.5) | Lightricks | 1,481 | 654,175 |
| [MiniMaxAI/MiniMax-H3](https://huggingface.co/MiniMaxAI/MiniMax-H3) | MiniMaxAI | 4,289 | 3,614,443 |
| [TenStrip/10Eros-Max](https://huggingface.co/TenStrip/10Eros-Max) | TenStrip | 306 | 0 |

**MiniMax-Music3** is a text-to-music diffusion model pushing the boundaries of AI-generated compositions. **LTX-2.5** is Lightricks' versatile image/video generation suite covering text-to-video, image-to-video, and video-to-video in one model. **MiniMax-H3** is the video generation powerhouse that has become the default base for many community fine-tunes. **10Eros-Max** is a MiniMax-H3 fine-tune focused on cinematic/adult-style video generation, showing the creative (and controversial) edges of the community.

---

### 🔧 Specialized Models (code, math, medical, embeddings)

| Model | Author | Likes | Downloads |
|---|---|---|---|
| [superwhisper/s1-mini](https://huggingface.co/superwhisper/s1-mini) | superwhisper | 185 | 1,136 |
| [ornith-ai/Ornith-1.5-35B-A3B](https://huggingface.co/ornith-ai/Ornith-1.5-35B-A3B) | ornith-ai | 280 | 9,165 |

**s1-mini** combines speech recognition (ASR) with Qwen3-based generation, creating a compact model for voice-to-text-to-response pipelines. **Ornith-1.5-35B-A3B** is an efficient MoE model (only 3B active) designed for high-throughput serving with MIT licensing.

---

### 📦 Fine-tunes & Quantizations (community fine-tunes, GGUF, AWQ)

| Model | Author | Likes | Downloads |
|---|---|---|---|
| [unsloth/Qwen3.8-27B-GGUF](https://huggingface.co/unsloth/Qwen3.8-27B-GGUF) | unsloth | 2,492 | 5,804,917 |
| [orcarouter/Qwen3.8-27B-Uncensored-MLX](https://huggingface.co/orcarouter/Qwen3.8-27B-Uncensored-MLX) | orcarouter | 813 | 18,193 |
| [orcarouter/Qwen3.8-27B-Uncensored-FP8](https://huggingface.co/orcarouter/Qwen3.8-27B-Uncensored-FP8) | orcarouter | 774 | 107,520 |
| [JonathanColetti/Qwen3.8-27B-Uncensored-GGUF](https://huggingface.co/JonathanColetti/Qwen3.8-27B-Uncensored-GGUF) | JonathanColetti | 560 | 1,126,222 |
| [OBLITERATUS/Qwen3.8-27B-OBLITERATED](https://huggingface.co/OBLITERATUS/Qwen3.8-27B-OBLITERATED) | OBLITERATUS | 432 | 123,956 |
| [HauhauCS/Qwen3.8-27B-Uncensored-HauhauCS-Aggressive-MTP-GGUF](https://huggingface.co/HauhauCS/Qwen3.8-27B-Uncensored-HauhauCS-Aggressive-MTP-GGUF) | HauhauCS | 414 | 357,225 |
| [Qwen/Qwen3.8-27B-FP8](https://huggingface.co/Qwen/Qwen3.8-27B-FP8) | Qwen | 656 | 1,939,895 |
| [froggeric/Qwen-Fixed-Chat-Templates](https://huggingface.co/froggeric/Qwen-Fixed-Chat-Templates) | froggeric | 1,364 | 0 |
| [empero-ai/Qwen3.8-27B-Ridge-GGUF](https://huggingface.co/empero-ai/Qwen3.8-27B-Ridge-GGUF) | empero-ai | 232 | 74,038 |
| [orcarouter/Qwen3.8-27B-Uncensored-GGUF](https://huggingface.co/orcarouter/Qwen3.8-27B-Uncensored-GGUF) | orcarouter | 282 | 68,275 |
| [huihui-ai/Huihui-Qwen3.8-27B-abliterated-GGUF](https://huggingface.co/huihui-ai/Huihui-Qwen3.8-27B-abliterated-GGUF) | huihui-ai | 226 | 338,221 |
| [ornith-ai/Ornith-1.5-35B-A3B-GGUF](https://huggingface.co/ornith-ai/Ornith-1.5-35B-A3B-GGUF) | ornith-ai | 198 | 123,237 |
| [0bserverx/Qwen3.8-27B-Heretic-Abliterated-Uncensored-GGUF](https://huggingface.co/0bserverx/Qwen3.8-27B-Heretic-Abliterated-Uncensored-GGUF) | 0bserverx | 206 | 421,918 |
| [unsloth/Qwen3.8-27B-NVFP4](https://huggingface.co/unsloth/Qwen3.8-27B-NVFP4) | unsloth | 323 | 1,013,917 |
| [huihui-ai/Huihui-Qwen3.8-27B-abliterated](https://huggingface.co/huihui-ai/Huihui-Qwen3.8-27B-abliterated) | huihui-ai | 225 | 17,521 |
| [Blackfrost-AI/Qwen3.8-27B-ABLITERATED-GGUF](https://huggingface.co/Blackfrost-AI/Qwen3.8-27B-ABLITERATED-GGUF) | Blackfrost-AI | 195 | 197,667 |
| [z-lab/Qwen3.8-27B-DFlash2](https://huggingface.co/z-lab/Qwen3.8-27B-DFlash2) | z-lab | 167 | 21,092 |
| [DavidAU/Qwen3.8-27B-Cold-Fusion-GAIN-V1.1-NM-DAU-NEO-MAX-MTP-GGUF](https://huggingface.co/DavidAU/Qwen3.8-27B-Cold-Fusion-GAIN-V1.1-NM-DAU-NEO-MAX-MTP-GGUF) | DavidAU | 162 | 155,208 |

This category is a goldmine of community innovation. **unsloth's GGUF** is the highest-downloaded quantization with 5.8M pulls, making Qwen3.8-27B the de facto local LLM standard. The **orcarouter** lineage provides MLX, FP8, and GGUF formats of the abliterated Qwen, catering to Apple Silicon, NVIDIA, and CPU users alike. **Qwen's own FP8** release is notable for bringing official low-precision support. **froggeric's chat template fix** (with 1.3K likes but 0 downloads, since it's a template not a model) speaks to a real pain point in the ecosystem. The **DavidAU Cold-Fusion GAIN** model represents the extreme of community experimentation, combining multiple training tricks (GAIN, COLD-FUSION, MTP, NEO-MAX) into a single GGUF. **NVFP4 from unsloth** points toward 4-bit NVIDIA-specific formats becoming mainstream.

---

## 3. Ecosystem Signal

The Qwen3.8/3.5 family has clearly become this cycle's Llama 3 — the release that anchors the open-weight ecosystem. The fact that nearly half of the trending list consists of Qwen3.8 variants (GGUF, FP8, NVFP4, abliterated, uncensored) signals that a healthy community infrastructure (unsloth, huihui-ai, orcarouter) now surrounds these models. The explosion of "uncensored" and "abliterated" fine-tunes (8+ distinct variants) points to a persistent demand for models without safety restrictions — a niche that's now industrialized with naming conventions (Eric Hartford's abliteration technique has become standard).

Open-weight models from Qwen, DeepSeek, and Moonshot are clearly competing head-on with closed-source offerings, and the fact that all three labs release both flagship and "Flash/lite" versions signals a market segmentation strategy mirroring OpenAI's GPT-4/GPT-4o-mini split. On the video front, MiniMax-H3 dominates as the base model, with community fine-tunes (like 10Eros-Max) emerging — though their low download counts suggest this niche is still early. Quantization warfare is between GGUF (CPU/Apple) and FP8/NVFP4 (NVIDIA), with unsloth cementing itself as the distribution layer.

---

## 4. Worth Exploring

**1. [Qwen/Qwen3.8-27B](https://huggingface.co/Qwen/Qwen3.8-27B)** — This is the model to study. With 11.9K likes and nearly 2M downloads, it's the center of gravity for the current open-source wave. Whether you're building multimodal apps, LLM reasoning, or just want to understand what's driving the community, this is your baseline — and the sheer size of its fine-tune ecosystem makes it the safest bet for long-term investment.

**2. [moonshotai/Kimi-K3](https://huggingface.co/moonshotai/Kimi-K3)** — Kimi-K3 with 10.9K likes and a "compressed-tensors / feature-extraction" tag suggests Moonshot is pushing novel architectures for efficient long-context. It's not just another LLM — it's a potential paradigm shift in how we think about latent compression. Worth studying for both performance and architectural novelty.

**3. [froggeric/Qwen-Fixed-Chat-Templates](https://huggingface.co/froggeric/Qwen-Fixed-Chat-Templates)** — Surprisingly impactful despite 0 downloads: it's a chat template fix, not a model. The fact it received 1.3K likes in a week tells you that the community is struggling with broken or inconsistent chat templates in Qwen's ecosystem. If you're building on Qwen, this is the first thing to check. It's a reminder that model quality isn't just weights — it's also the glue code around them.

---
*This digest is auto-generated by [agents-radar](https://github.com/kky-wollu/agents-radar).*