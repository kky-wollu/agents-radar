# Hugging Face Trending Models Digest 2026-08-08

> Source: [Hugging Face Hub](https://huggingface.co/) | 30 models | Generated: 2026-08-07 22:41 UTC

---

# 🤖 Hugging Face Trending Models Digest — 2026-08-08

---

## 1. Today's Highlights

The Hub is dominated by **video generation** this week, with MiniMax-H3 spawning an entire ecosystem of fine-tunes, LoRAs, GGUF quantizations, and ComfyUI integrations. On the LLM front, **DeepSeek-V4-Flash-0731** is making waves as a new flash-tier conversational model with massive adoption (702K downloads), while **GLM-5.2** from Zhipu AI cements itself as a MoE powerhouse. Multimodal models are surging with **Kimi-K3** (10.2K likes) leading the image-text-to-text category and Baidu's Unlimited-OCR showing OCR is far from solved. Community fine-tunes and quantizations (GGUF, NVFP4, INT8) are proliferating rapidly around both MiniMax-H3 and the Qwen3.6 family, signaling a maturing open-weights ecosystem with strong DIY momentum.

---

## 2. Trending Models by Category

---

### 🧠 Language Models (LLMs, chat, instruction-tuned)

**DeepSeek-V4-Flash-0731** — [link](https://huggingface.co/deepseek-ai/DeepSeek-V4-Flash-0731)  
*Author: deepseek-ai | 👍 2,737 | ⬇️ 702,709*  
A flash-tier conversational model with massive adoption, likely the most practical daily driver in the DeepSeek V4 line.

**GLM-5.2** — [link](https://huggingface.co/zai-org/GLM-5.2)  
*Author: zai-org | 👍 4,886 | ⬇️ 2,430,330*  
Zhipu AI's latest MoE-DSA architecture model with 2.4M downloads, marking GLM as a flagship open-weights contender.

**Kimi-K3** — [link](https://huggingface.co/moonshotai/Kimi-K3)  
*Author: moonshotai | 👍 10,274 | ⬇️ 1,308,186*  
Moonshot's multimodal compression-focused model with the highest like count today — a strong feature-extraction and image-text candidate.

**LiquidAI/LFM2.5-2.6B** — [link](https://huggingface.co/LiquidAI/LFM2.5-2.6B)  
*Author: LiquidAI | 👍 376 | ⬇️ 77,973*  
Small-but-mighty liquid transformer model, gaining traction as an efficient 2.6B option.

**deepgrove/maple-preview** — [link](https://huggingface.co/deepgrove/maple-preview)  
*Author: deepgrove | 👍 222 | ⬇️ 686*  
A Mixture-of-Experts causal LM preview from a new lab worth watching for its architectural choices.

**inclusionAI/Ling-3.0-flash** — [link](https://huggingface.co/inclusionAI/Ling-3.0-flash)  
*Author: inclusionAI | 👍 202 | ⬇️ 3,065*  
Flash-tier hybrid-architecture conversational model with custom code, showing growing emphasis on efficient inference.

**mistralai/Shieldstral-1.0-3B** — [link](https://huggingface.co/mistralai/Shieldstral-1.0-3B)  
*Author: mistralai | 👍 183 | ⬇️ 2,480*  
A compact 3B safety/guardrail-focused model from Mistral, built on Mistral-3 architecture.

---

### 🎨 Multimodal & Generation (image, video, audio, text-to-X)

**MiniMaxAI/MiniMax-H3** — [link](https://huggingface.co/MiniMaxAI/MiniMax-H3)  
*Author: MiniMaxAI | 👍 2,939 | ⬇️ 18,112*  
The breakout image-text-to-video model of the week, spawning an entire ecosystem of fine-tunes, quantizations, and ComfyUI tooling.

**baidu/Unlimited-OCR** — [link](https://huggingface.co/baidu/Unlimited-OCR)  
*Author: baidu | 👍 3,953 | ⬇️ 2,836,694*  
Baidu's versatile OCR model (image-text-to-text) with 2.8M downloads, positioning itself as a universal document/vision reader.

**microsoft/Mage-VL** — [link](https://huggingface.co/microsoft/Mage-VL)  
*Author: microsoft | 👍 301 | ⬇️ 456,140*  
Microsoft's multimodal vision-language model achieving widespread adoption in under a week.

**Audio8/Audio8-TTS-Preview-0.6b** — [link](https://huggingface.co/Audio8/Audio8-TTS-Preview-0.6b)  
*Author: Audio8 | 👍 305 | ⬇️ 12,633*  
A compact 0.6B TTS model (ARK-TTS) signaling a trend toward lighter, faster speech synthesis.

**thinkingmachines/Inkling-Small** — [link](https://huggingface.co/thinkingmachines/Inkling-Small)  
*Author: thinkingmachines | 👍 335 | ⬇️ 25,340*  
Multimodal conversational model from a new lab, gaining traction for its image-text-to-text flexibility.

**black-forest-labs/FLUX.1-dev** — [link](https://huggingface.co/black-forest-labs/FLUX.1-dev)  
*Author: black-forest-labs | 👍 14,026 | ⬇️ 512,841*  
The evergreen FLUX.1-dev remains the most-liked model on the Hub, the gold standard for open text-to-image.

**lodestones/Kroma** — [link](https://huggingface.co/lodestones/Kroma)  
*Author: lodestones | 👍 221 | ⬇️ 0*  
A Krea-2 LoRA for text-to-image with ComfyUI support — zero downloads suggests very fresh release worth watching.

---

### 🔧 Specialized Models (code, OCR, embeddings, safety)

**Kwaipilot/KAT-Coder-V2.5-Dev** — [link](https://huggingface.co/Kwaipilot/KAT-Coder-V2.5-Dev)  
*Author: Kwaipilot | 👍 531 | ⬇️ 17,399*  
Qwen3.5-MoE-based coding model with image-text-to-text support, a strong open-weights code assistant option.

**baidu/Unlimited-OCR** — [link](https://huggingface.co/baidu/Unlimited-OCR)  
*Author: baidu | 👍 3,953 | ⬇️ 2,836,694*  
(Also listed above — a specialized OCR model that bridges vision and text extraction.)

**nvidia/NVIDIA-NemotronLabs-VoiceChat-11B** — [link](https://huggingface.co/nvidia/NVIDIA-NemotronLabs-VoiceChat-11B)  
*Author: nvidia | 👍 226 | ⬇️ 359*  
NVIDIA's voice-chat model, specialized for spoken interaction, backed by three papers.

**mistralai/Shieldstral-1.0-3B** — [link](https://huggingface.co/mistralai/Shieldstral-1.0-3B)  
*Author: mistralai | 👍 183 | ⬇️ 2,480*  
(Also listed above — a safety/guardrail-specific model from Mistral.)

---

### 📦 Fine-tunes & Quantizations (Community fine-tunes, GGUF, LoRA)

**DavidAU/Qwen3.6-27B-Fable-Fusion-711-Uncensored-Heretic-NM-DAU-NEO-MAX-MTP-GGUF** — [link](https://huggingface.co/DavidAU/Qwen3.6-27B-Fable-Fusion-711-Uncensored-Heretic-NM-DAU-NEO-MAX-MTP-GGUF)  
*Author: DavidAU | 👍 1,704 | ⬇️ 2,217,339*  
An elaborately merged Qwen3.6 fine-tune family, 2.2M downloads shows a strong appetite for creative/uncensored variants.

**unsloth/DeepSeek-V4-Flash-0731-GGUF** — [link](https://huggingface.co/unsloth/DeepSeek-V4-Flash-0731-GGUF)  
*Author: unsloth | 👍 585 | ⬇️ 161,253*  
The official GGUF quantization of DeepSeek's flash model, enabling local deployment on consumer hardware.

**larryvrh/MiniMax-H3-Turbo-Lora** — [link](https://huggingface.co/larryvrh/MiniMax-H3-Turbo-Lora)  
*Author: larryvrh | 👍 407 | ⬇️ 0*  
A fresh MiniMax-H3 LoRA aiming at turbo-speed video generation — zero downloads suggests just released.

**realrebelai/MiniMax-H3_GGUFs** — [link](https://huggingface.co/realrebelai/MiniMax-H3_GGUFs)  
*Author: realrebelai | 👍 168 | ⬇️ 87,870*  
Community GGUF quantizations for MiniMax-H3, making video gen accessible on local machines.

**LuffyTheFox/Qwen3.6-35B-A3B-Uncensored-Genesis-Hermes-V7-GGUF** — [link](https://huggingface.co/LuffyTheFox/Qwen3.6-35B-A3B-Uncensored-Genesis-Hermes-V7-GGUF)  
*Author: LuffyTheFox | 👍 426 | ⬇️ 332,992*  
An uncensored Qwen3.6 MoE GGUF quant with massive community pickup — 333K downloads.

**EschaLabs/Qwen3.6-35B-A3B-Escha-W2** — [link](https://huggingface.co/EschaLabs/Qwen3.6-35B-A3B-Escha-W2)  
*Author: EschaLabs | 👍 236 | ⬇️ 3,622*  
A weight-compressed Qwen3.6 MoE variant, 2-bit quantizations becoming a viable option.

**Abiray/Minimax-H3-nvfp4-INT4-INT8-Convrot** — [link](https://huggingface.co/Abiray/Minimax-H3-nvfp4-INT4-INT8-Convrot)  
*Author: Abiray | 👍 127 | ⬇️ 452,420*  
NVFP4/INT4/INT8 quantized MiniMax-H3 for video generation — 452K downloads shows deep demand for low-precision video.

**drbaph/MiniMax-H3-Turbo-Lora-ComfyUI** — [link](https://huggingface.co/drbaph/MiniMax-H3-Turbo-Lora-ComfyUI)  
*Author: drbaph | 👍 176 | ⬇️ 0*  
ComfyUI-ready pruned MiniMax-H3 Turbo LoRA — part of the broader ComfyUI × MiniMax wave.

**ethanfel/Qwen3-VL-32B-Ultra-Heretic-H3-ComfyUI-INT8-ConvRot** — [link](https://huggingface.co/ethanfel/Qwen3-VL-32B-Ultra-Heretic-H3-ComfyUI-INT8-ConvRot)  
*Author: ethanfel | 👍 377 | ⬇️ 0*  
A Qwen3-VL-32B + MiniMax-H3 hybrid ComfyUI INT8 text-encoder conversion.

**sakamakismile/Qwen3-VL-32B-Heretic-MiniMax-H3-NVFP4** — [link](https://huggingface.co/sakamakismile/Qwen3-VL-32B-Heretic-MiniMax-H3-NVFP4)  
*Author: sakamakismile | 👍 121 | ⬇️ 0*  
NVFP4 Qwen3-VL-32B text-encoder for MiniMax-H3 ComfyUI pipelines — part of the H3 tooling ecosystem.

**Comfy-Org/MiniMax-H3** — [link](https://huggingface.co/Comfy-Org/MiniMax-H3)  
*Author: Comfy-Org | 👍 931 | ⬇️ 3,139,920*  
The ComfyUI-packaged single-file MiniMax-H3, 3.1M downloads — the most downloaded model today.

**LiquidAI/LFM2.5-2.6B-GGUF** — [link](https://huggingface.co/LiquidAI/LFM2.5-2.6B-GGUF)  
*Author: LiquidAI | 👍 143 | ⬇️ 31,489*  
Official GGUF quant for LLM.cpp users of the LFM2.5 model — local-first LLM momentum.

---

## 3. Ecosystem Signal

The dominant signal this week is the **MiniMax-H3 ecosystem explosion**. With base model, ComfyUI single-file, GGUF, LoRA, NVFP4/INT4/INT8 quantizations, and even hybrid Qwen3-VL text-encoder conversions all trending simultaneously, MiniMax-H3 is clearly the **"FLUX moment" for video generation** — open-weights video is now community-driven.

**Open-weights momentum is accelerating**, with DeepSeek, GLM, Kimi, and Qwen families all showing strong official + community presence (GGUF, MoE compression, fine-tunes). The 2.6B–27B parameter range dominates, suggesting a shift toward **efficiency-first deployment**.

**Quantization depth is maturing**: NVFP4 for mmGPU inference, INT8/INT4 for consumer hardware, GGUF for llama.cpp — the ecosystem now expects multi-format availability as the norm, not a feature. Meanwhile, "uncensored/heretic" fine-tunes continue to drive downloads, reflecting a community appetite for unrestricted generation.

---

## 4. Worth Exploring

1. **MiniMax-H3** ([link](https://huggingface.co/MiniMaxAI/MiniMax-H3)) — The defacto most influential video model this week. Studying its architecture and the ecosystem around it (Comfy-Org single-file, GGUF quantizations) is essential to understand where open-weights video is headed.

2. **Kimi-K3** ([link](https://huggingface.co/moonshotai/Kimi-K3)) — With 10.2K likes, it's the fastest-rising multimodal model. Its compressed-tensors + feature-extraction positioning suggests Moonshot is pursuing efficiency-aware multimodal reasoning — closely tracking it could reveal the next standard for VLMs.

3. **unsloth/DeepSeek-V4-Flash-0731-GGUF** ([link](https://huggingface.co/unsloth/DeepSeek-V4-Flash-0731-GGUF)) — The official GGUF of DeepSeek's flash model is poised to become the default local LLM for many users. Its rapid adoption (161K downloads in days) makes it a strong candidate for the next "Llama-3 moment" in local deployment.

---
*This digest is auto-generated by [agents-radar](https://github.com/kky-wollu/agents-radar).*