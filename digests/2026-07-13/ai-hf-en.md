# Hugging Face Trending Models Digest 2026-07-13

> Source: [Hugging Face Hub](https://huggingface.co/) | 30 models | Generated: 2026-07-12 21:25 UTC

---

# 🤗 Hugging Face Trending Models Digest — 2026-07-13

## 1. Today's Highlights

This week's trending landscape is dominated by **Qwen 3.5/3.6 derivatives** and a wave of **high-demand GGUF quantizations**, reflecting a strong community appetite for efficient, deployable LLMs. Notably, **nvidia's LocateAnything-3B** (2.7K likes) signals growing interest in grounded vision-language models for object localization, while **zai-org/GLM-5.2** (3.9K likes) emerges as the week's most-liked model, showcasing the continued pull of Chinese MoE architectures. The rise of **uncensored and aggressive-style fine-tunes** (e.g., HauhauCS's Qwen3.6 variant) alongside **agentic coding models** (yuxinlu1's Gemma-4-based GGUF) points to a maturing ecosystem where users demand both performance and specialized behavioral tuning.

## 2. Trending Models by Category

### 🧠 Language Models (LLMs, chat models, instruction-tuned)

- **[GLM-5.2](https://huggingface.co/zai-org/GLM-5.2)** — zai-org | 3.9K likes, 441K downloads  
  Top-liked model of the week: a conversational MoE model (likely based on GLM architecture) with strong community traction, suggesting a breakthrough in Chinese-language or MoE performance.

- **[Tess-4-27B](https://huggingface.co/migtissera/Tess-4-27B)** — migtissera | 91 likes, 971 downloads  
  A Qwen 3.5-based image-text-to-text model continuing the Tess lineage, positioned as a versatile multimodal assistant.

- **[Supra-Router-51M](https://huggingface.co/SupraLabs/Supra-Router-51M)** — SupraLabs | 105 likes, 1.4K downloads  
  A tiny 51M-parameter router model, likely for MoE or agent routing — interesting for efficiency-focused research.

### 🎨 Multimodal & Generation (image, video, audio, text-to-X)

- **[LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)** — nvidia | 2.7K likes, 1.5M downloads  
  nvidia's standout vision-language model for open-vocabulary object localization; high downloads suggest strong practical utility.

- **[Unlimited-OCR](https://huggingface.co/baidu/Unlimited-OCR)** — baidu | 1.9K likes, 1.4M downloads  
  A high-performance OCR model from Baidu, likely supporting diverse document and scene text recognition.

- **[Giga-World-1](https://huggingface.co/open-gigaai/Giga-World-1)** — open-gigaai | 123 likes, 0 downloads  
  A Diffusers-based model (pipeline N/A), potentially a world model or video generation tool.

- **[lingbot-world-v2-14b-causal-fast](https://huggingface.co/robbyant/lingbot-world-v2-14b-causal-fast)** — robbyant | 82 likes, 0 downloads  
  An image-to-video "world model" with causal architecture, notable for the "world model" research direction.

- **[gepard-1.0](https://huggingface.co/nineninesix/gepard-1.0)** — nineninesix | 84 likes, 2.3K downloads  
  A text-to-speech model built on Qwen 3.5 backbone, blending LLM and audio generation.

### 🔧 Specialized Models (code, math, medical, embeddings, audio, video)

- **[yuxinlu1/gemma-4-12B-agentic-fable5-composer2.5-v2-3.5x-tau2-GGUF](https://huggingface.co/yuxinlu1/gemma-4-12B-agentic-fable5-composer2.5-v2-3.5x-tau2-GGUF)** — yuxinlu1 | 1.2K likes, 445K downloads  
  An agentic, terminal-friendly coding model based on Gemma 4, showing strong demand for on-device coding assistants.

- **[Nemotron-Labs-Audex-30B-A3B](https://huggingface.co/nvidia/Nemotron-Labs-Audex-30B-A3B)** — nvidia | 131 likes, 901 downloads  
  nvidia's MoE model with 30B total / 3B active params, optimized for inference efficiency.

- **[NVIDIA-Nemotron-Labs-3-Puzzle-75B-A9B-NVFP4](https://huggingface.co/nvidia/NVIDIA-Nemotron-Labs-3-Puzzle-75B-A9B-NVFP4)** — nvidia | 111 likes, 34.8K downloads  
  A massive 75B MoE model (9B active) using NVFP4 quantization, pushing the frontier of efficient large-model deployment.

- **[tabfm-1.0.0-pytorch](https://huggingface.co/google/tabfm-1.0.0-pytorch)** — google | 354 likes, 20.9K downloads  
  Google's foundation model for tabular data with zero-shot classification/regression capabilities.

- **[MOSS-Transcribe-Diarize](https://huggingface.co/OpenMOSS-Team/MOSS-Transcribe-Diarize)** — OpenMOSS-Team | 125 likes, 14.5K downloads  
  An audio-text-to-text model combining transcription and speaker diarization, likely for meeting/call analysis.

- **[cohere-transcribe-arabic-07-2026](https://huggingface.co/CohereLabs/cohere-transcribe-arabic-07-2026)** — CohereLabs | 95 likes, 9.9K downloads  
  A specialized Arabic automatic speech recognition model, addressing a critical language gap.

- **[LTX-Best-Face-ID](https://huggingface.co/Alissonerdx/LTX-Best-Face-ID)** — Alissonerdx | 107 likes, 0 downloads  
  A LoRA for identity preservation in text-to-video (LTX-Video pipeline).

- **[krea2-identity-edit](https://huggingface.co/conradlocke/krea2-identity-edit)** — conradlocke | 207 likes, 0 downloads  
  An image-editing LoRA for Krea-2 that enables identity-preserving edits.

### 📦 Fine-tunes & Quantizations (community fine-tunes, GGUF, AWQ)

- **[Qwen-Fixed-Chat-Templates](https://huggingface.co/froggeric/Qwen-Fixed-Chat-Templates)** — froggeric | 861 likes, 0 downloads  
  A non-model utility providing corrected chat templates for Qwen 3.5, highlighting a niche but critical community need.

- **[DeepSeek-V4-Flash-GGUF](https://huggingface.co/unsloth/DeepSeek-V4-Flash-GGUF)** — unsloth | 151 likes, 44.6K downloads  
  Unsloth's GGUF quantization of DeepSeek V4, making the latest DeepSeek accessible on consumer hardware.

- **[Ornith-1.0-35B-GGUF](https://huggingface.co/deepreinforce-ai/Ornith-1.0-35B-GGUF)** — deepreinforce-ai | 855 likes, 1.3M downloads  
  A heavily downloaded GGUF quant of a 35B model, likely a strong mid-scale performer.

- **[Qwen3.6-27B-MTP-GGUF](https://huggingface.co/unsloth/Qwen3.6-27B-MTP-GGUF)** — unsloth | 1.1K likes, 2.9M downloads  
  The most downloaded model this week (2.9M) — Unsloth's GGUF of the latest Qwen 3.6 with MTP (multi-token prediction).

- **[HauhauCS/Qwen3.6-35B-A3B-Uncensored-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)** — HauhauCS | 2.7K likes, 2.6M downloads  
  An "uncensored, aggressive" fine-tune of Qwen 3.6 MoE — extremely high engagement, reflecting demand for less-restricted outputs.

- **[ThinkingCap-Qwen3.6-27B](https://huggingface.co/bottlecapai/ThinkingCap-Qwen3.6-27B)** — bottlecapai | 260 likes, 4.5K downloads  
  A token-efficient thinking-cap enhanced Qwen 3.6 for improved reasoning.

- **[ThinkingCap-Qwen3.6-27B-GGUF](https://huggingface.co/bottlecapai/ThinkingCap-Qwen3.6-27B-GGUF)** — bottlecapai | 82 likes, 312K downloads  
  GGUF version of the above, enabling broader deployment.

- **[MiniCPM5-1B-Claude-Opus-Fable5-Thinking-GGUF](https://huggingface.co/GnLOLot/MiniCPM5-1B-Claude-Opus-Fable5-Thinking-GGUF)** — GnLOLot | 200 likes, 49.3K downloads  
  A tiny 1B GGUF with "thinking" capabilities, likely distilled from Claude — remarkable for its size.

- **[Agents-A1](https://huggingface.co/InternScience/Agents-A1)** — InternScience | 506 likes, 29K downloads  
  A Qwen 3.5 MoE model specialized for agent tasks (image-text-to-text).

- **[Qwythos-9B-Claude-Mythos-5-1M-GGUF](https://huggingface.co/empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF)** — empero-ai | 2.0K likes, 1.97M downloads  
  A heavily downloaded GGUF quant of a 9B Claude-inspired fine-tune, notable for its "mythos" persona and reasoning focus.

- **[Qwythos-9B-Claude-Mythos-5-1M](https://huggingface.co/empero-ai/Qwythos-9B-Claude-Mythos-5-1M)** — empero-ai | 773 likes, 188K downloads  
  The base model version (non-quantized) of the above, also highly popular.

## 3. Ecosystem Signal

**Qwen 3.5/3.6 dominates the ecosystem:** Nearly half of the top 30 models are derivatives of the Qwen 3.5/3.6 family, spanning base models, MoE variants, and uncensored fine-tunes. This reflects Alibaba's Qwen series becoming the community's preferred base for experimentation, likely due to competitive performance and permissive licensing.

**MoE is the architecture of the moment:** Models like GLM-5.2, nvidia's Nemotron series (30B/75B MoE), HauhauCS's Qwen3.6-A3B, and InternScience's Agents-A1 all leverage Mixture-of-Experts, enabling larger total parameters with lower active compute. This trend signals a shift from dense models to sparse, efficient architectures.

**GGUF quantization is the default delivery mechanism:** High-download models are overwhelmingly GGUF (llama.cpp-compatible), with Unsloth emerging as a key infrastructure provider. The most-downloaded model (Qwen3.6-27B-MTP-GGUF at 2.9M) underscores that the community prioritizes local deployment and inference speed over raw capability.

**Niche specialization is accelerating:** From Arabic ASR (CohereLabs) to tabular FM (Google TabFM), identity-preserving video LoRAs, and audio diarization (MOSS), the platform now hosts models for highly specific vertical use cases — a sign of ecosystem maturity.

**"Agentic" and "uncensored" are distinct demand signals:** Two emergent preference clusters — agentic/coding models (Gemma 4 agentic GGUF) and uncensored/aggressive fine-tunes (HauhauCS variant) — suggest users want models that either act (tools/code) or speak freely (uncensored chat), not just answer questions.

## 4. Worth Exploring

1. **[nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)** — With 2.7K likes and 1.5M downloads, this is the breakout vision model of the week. It fills a critical gap in open-vocabulary object detection, and its small 3B size makes it deployable on edge devices. Worth studying for anyone building grounded vision applications.

2. **[HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)** — This model's extraordinary engagement (2.7K likes, 2.6M downloads) signals a powerful latent demand for "uncensored" MoE models. It's worth examining for both technical quality (35B total / 3B active) and the behavioral implications of aggressive fine-tuning.

3. **[unsloth/Qwen3.6-27B-MTP-GGUF](https://huggingface.co/unsloth/Qwen3.6-27B-MTP-GGUF)** — The week's most-downloaded model (2.9M) represents the new standard for local LLM deployment. Its combination of Multi-Token Prediction (MTP) and GGUF quantization makes it a must-try benchmark for anyone evaluating on-device performance vs. quality trade-offs.

---
*This digest is auto-generated by [agents-radar](https://github.com/kky-wollu/agents-radar).*