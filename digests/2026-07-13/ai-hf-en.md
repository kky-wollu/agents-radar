# Hugging Face Trending Models Digest 2026-07-13

> Source: [Hugging Face Hub](https://huggingface.co/) | 30 models | Generated: 2026-07-12 20:39 UTC

---

# 🤗 Hugging Face Trending Models Digest — 2026-07-13

## 1. Today's Highlights

This week's trending models reveal a strong **multimodal shift** led by vision-language models, with **Qwen3.6**, **GLM-5.2**, and **Nemotron-Labs** families dominating the top spots. The **GGUF quantization ecosystem** continues to explode, driven by community fine-tunes and efficient deployment variants like `unsloth` and `empero-ai` models, many of which exceed 1M downloads. Notably, **NVIDIA** has made a major push with three high-likes models including a vision grounding model (LocateAnything-3B) and two large MoE reasoning models. **Baidu's** Unlimited-OCR and new **Cohere Arabic** ASR model signal growing enterprise and multilingual investment, while the AI agent and code-assistant segment sees strong traction from models like `Agents-A1` and the Gemma-4 agentic fine-tune.

---

## 2. Trending Models by Category

### 🧠 Language Models (LLMs, chat models, instruction-tuned)

- **[zai-org/GLM-5.2](https://huggingface.co/zai-org/GLM-5.2)** — *zai-org, 3,852 likes, 441K downloads*  
  A massively popular conversational MoE model based on the GLM architecture, trending for its strong reasoning and dialogue capabilities.

- **[deepreinforce-ai/Ornith-1.0-35B-GGUF](https://huggingface.co/deepreinforce-ai/Ornith-1.0-35B-GGUF)** — *deepreinforce-ai, 855 likes, 1.3M downloads*  
  A 35B-parameter GGUF-quantized model gaining traction for its MIT licensing and ready-to-deploy performance.

- **[nvidia/NVIDIA-Nemotron-Labs-3-Puzzle-75B-A9B-NVFP4](https://huggingface.co/nvidia/NVIDIA-Nemotron-Labs-3-Puzzle-75B-A9B-NVFP4)** — *nvidia, 111 likes, 34.8K downloads*  
  NVIDIA's 75B MoE model (9B active) using NVFP4 quantization, notable for pushing efficient large-model inference.

- **[nvidia/Nemotron-Labs-Audex-30B-A3B](https://huggingface.co/nvidia/Nemotron-Labs-Audex-30B-A3B)** — *nvidia, 131 likes, 901 downloads*  
  A 30B MoE variant with 3B active parameters, representing NVIDIA's continued investment in sparse, efficient LLMs.

- **[HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)** — *HauhauCS, 2,671 likes, 2.6M downloads*  
  An uncensored Qwen3.6 MoE fine-tune with vision support, trending for its aggressive prompt style and massive community adoption.

- **[CohereLabs/cohere-transcribe-arabic-07-2026](https://huggingface.co/CohereLabs/cohere-transcribe-arabic-07-2026)** — *CohereLabs, 95 likes, 9.9K downloads*  
  Cohere's dedicated Arabic automatic speech recognition model, signaling enterprise multilingual ASR expansion.

### 🎨 Multimodal & Generation (image, video, audio, text-to-X)

- **[baidu/Unlimited-OCR](https://huggingface.co/baidu/Unlimited-OCR)** — *baidu, 1,941 likes, 1.4M downloads*  
  Baidu's state-of-the-art OCR model (image-text-to-text pipeline), widely adopted for its high accuracy across diverse document types.

- **[nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)** — *nvidia, 2,714 likes, 1.5M downloads*  
  NVIDIA's vision-language grounding model for object localization, trending for its broad applicability in robotics and image analysis.

- **[open-gigaai/Giga-World-1](https://huggingface.co/open-gigaai/Giga-World-1)** — *open-gigaai, 122 likes, 0 downloads*  
  A diffusion-based world model (Apache-2.0) enabling video generation, still early but notable as an open-weight alternative.

- **[robbyant/lingbot-world-v2-14b-causal-fast](https://huggingface.co/robbyant/lingbot-world-v2-14b-causal-fast)** — *robbyant, 80 likes, 0 downloads*  
  An image-to-video world model using causal attention, building on the LingBot video MoE ecosystem.

- **[Alissonerdx/LTX-Best-Face-ID](https://huggingface.co/Alissonerdx/LTX-Best-Face-ID)** — *Alissonerdx, 107 likes, 0 downloads*  
  A reference-to-video LoRA for identity-preserving LTX video generation, trending for face-consistent generation.

- **[nineninesix/gepard-1.0](https://huggingface.co/nineninesix/gepard-1.0)** — *nineninesix, 84 likes, 2.3K downloads*  
  A text-to-speech model built on Qwen3.5 text backbone, bridging LLM and audio generation domains.

- **[OpenMOSS-Team/MOSS-Transcribe-Diarize](https://huggingface.co/OpenMOSS-Team/MOSS-Transcribe-Diarize)** — *OpenMOSS-Team, 125 likes, 14.5K downloads*  
  An audio-text-to-text model combining transcription and speaker diarization, interesting for meeting and call analysis.

### 🔧 Specialized Models (code, math, medical, embeddings, tabular)

- **[InternScience/Agents-A1](https://huggingface.co/InternScience/Agents-A1)** — *InternScience, 506 likes, 29K downloads*  
  A Qwen3.5-MoE-based agent model supporting image-text tasks, trending for its autonomous tool-use capabilities.

- **[yuxinlu1/gemma-4-12B-agentic-fable5-composer2.5-v2-3.5x-tau2-GGUF](https://huggingface.co/yuxinlu1/gemma-4-12B-agentic-fable5-composer2.5-v2-3.5x-tau2-GGUF)** — *yuxinlu1, 1,158 likes, 445K downloads*  
  A Gemma-4 fine-tune specialized for agentic coding and terminal use, one of the most downloaded agent models.

- **[google/tabfm-1.0.0-pytorch](https://huggingface.co/google/tabfm-1.0.0-pytorch)** — *google, 354 likes, 20.9K downloads*  
  Google's foundational tabular model supporting zero-shot classification and regression, a rare entry in the tabular foundation model space.

- **[SupraLabs/Supra-Router-51M](https://huggingface.co/SupraLabs/Supra-Router-51M)** — *SupraLabs, 105 likes, 1.4K downloads*  
  A tiny 51M routing model for selecting between LLM experts, reflecting growing serverless and mixture-of-experts infrastructure interest.

- **[meituan-longcat/LongCat-2.0](https://huggingface.co/meituan-longcat/LongCat-2.0)** — *meituan-longcat, 182 likes, 1.8K downloads*  
  Meituan's long-context conversational model, specialized for extended dialogue history management.

### 📦 Fine-tunes & Quantizations (community fine-tunes, GGUF, AWQ)

- **[empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF](https://huggingface.co/empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF)** — *empero-ai, 2,039 likes, 1.96M downloads*  
  The GGUF-quantized variant of an 8B Qwen3.5 fine-tune with 1M context, the most downloaded GGUF model this week by a wide margin.

- **[unsloth/Qwen3.6-27B-MTP-GGUF](https://huggingface.co/unsloth/Qwen3.6-27B-MTP-GGUF)** — *unsloth, 1,057 likes, 2.9M downloads*  
  Unsloth's 27B Qwen3.6 GGUF with Multi-Token Prediction (MTP), the highest-download model overall, reflecting the community's appetite for efficient, ready-to-run LLMs.

- **[unsloth/DeepSeek-V4-Flash-GGUF](https://huggingface.co/unsloth/DeepSeek-V4-Flash-GGUF)** — *unsloth, 151 likes, 44.6K downloads*  
  A DeepSeek V4 Flash GGUF quantization (arXiv:2606.19348), gaining interest for speed-optimized inference.

- **[bottlecapai/ThinkingCap-Qwen3.6-27B-GGUF](https://huggingface.co/bottlecapai/ThinkingCap-Qwen3.6-27B-GGUF)** — *bottlecapai, 82 likes, 312K downloads*  
  A token-efficient thinking model GGUF, designed for efficient reason-while-generating pipelines.

- **[bottlecapai/ThinkingCap-Qwen3.6-27B](https://huggingface.co/bottlecapai/ThinkingCap-Qwen3.6-27B)** — *bottlecapai, 259 likes, 4.5K downloads*  
  The non-quantized base version of the ThinkingCap reasoning model.

- **[GnLOLot/MiniCPM5-1B-Claude-Opus-Fable5-Thinking-GGUF](https://huggingface.co/GnLOLot/MiniCPM5-1B-Claude-Opus-Fable5-Thinking-GGUF)** — *GnLOLot, 200 likes, 49.3K downloads*  
  A 1B-parameter MiniCPM5 thinking model in GGUF, notable for its ultra-small footprint with reasoning capability.

- **[robbyant/lingbot-video-moe-30b-a3b](https://huggingface.co/robbyant/lingbot-video-moe-30b-a3b)** — *robbyant, 90 likes, 461 downloads*  
  A video diffusion MoE model (30B total, 3B active) for efficient video generation, building on the LingBot pipeline.

- **[conradlocke/krea2-identity-edit](https://huggingface.co/conradlocke/krea2-identity-edit)** — *conradlocke, 206 likes, 0 downloads*  
  A LoRA for identity-preserving image editing using the Krea-2 base model, gaining presence in the ComfyUI ecosystem.

- **[migtissera/Tess-4-27B](https://huggingface.co/migtissera/Tess-4-27B)** — *migtissera, 90 likes, 971 downloads*  
  A Qwen3.5-based multimodal conversational model, part of the Tess series gaining community attention.

- **[froggeric/Qwen-Fixed-Chat-Templates](https://huggingface.co/froggeric/Qwen-Fixed-Chat-Templates)** — *froggeric, 861 likes, 0 downloads*  
  A utility repo fixing chat templates for Qwen3.5 models, trending as infrastructure for reliable deployment.

- **[tencent/Hy3](https://huggingface.co/tencent/Hy3)** — *tencent, 714 likes, 8.7K downloads*  
  Tencent's Hy3 text-generation model (Hunyuan lineage), gaining attention as a major Chinese tech player's open-weight release.

---

## 3. Ecosystem Signal

**Qwen family dominance** is the defining trend this week: Qwen3.5 and Qwen3.6 variants appear in at least 8 of the top 30 models, including the #1 downloaded model (unsloth/Qwen3.6-27B-MTP-GGUF at 2.9M downloads). The community is rapidly adopting Qwen as the base for fine-tunes, quantizations, and agentic variants—suggesting it has become the de facto "Llama alternative" for the open-weight ecosystem.

**GGUF quantization is now the primary distribution format** for community models. Of the 30 trending models, 11 are GGUF variants, and many accumulate downloads in the millions. This reflects a maturing ecosystem where users prioritize deployability—models like `empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF` (1.96M downloads) and `unsloth/Qwen3.6-27B-MTP-GGUF` (2.9M) show that the largest audience is not experimenting with raw weights but running quantized models on consumer hardware.

**MoE (Mixture of Experts) architectures are becoming mainstream** across model sizes. From NVIDIA's 75B/9B active Nemotron-Labs to the 35B/3B active Qwen3.6 and GLM-5.2, MoE enables large parameter counts with manageable inference costs. This trend is reinforced by the rise of routing models like `SupraLabs/Supra-Router-51M`.

**Open-weight competition is intensifying** from Chinese tech giants (Tencent, Baidu, Zhipu/GLM), Western labs (NVIDIA, Google, Cohere), and community builders alike. The absence of OpenAI/Meta models in the top trending list suggests a shift toward third-party and foundation-model-as-base fine-tuning, rather than OpenAI-derived or Llama/Starling-style fine-tunes.

**Vision-language and multimodal models are surging**, with 10 of the 30 models using multimodal pipelines. This is not just image-text: we see audio (Cohere, MOSS), video (LingBot, Giga-World, LTX), and TTS (gepard) models trending simultaneously, indicating the ecosystem is broadening beyond pure text.

**Agentic and reasoning-focused models** form another major cluster, with `ThinkingCap`, `Qwythos-Mythos`, `Agents-A1`, and the Gemma-4 agentic fine-tune all showing strong engagement. The community is clearly prioritizing models that can "do things"—code, browse, use tools—rather than pure conversation.

---

## 4. Worth Exploring

- **[nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)** — With 2.7K likes and 1.5M downloads, this vision grounding model represents a powerful open-weight alternative to closed-source object detection APIs. Its "locate anything" capability is immediately useful for robotics, document parsing, and visual search pipelines.

- **[unsloth/Qwen3.6-27B-MTP-GGUF](https://huggingface.co/unsloth/Qwen3.6-27B-MTP-GGUF)** — The highest-download model of the week (2.9M) with Multi-Token Prediction. This is the model to study for anyone wanting to understand state-of-the-art in efficient, quantized LLM deployment. Its combination of Qwen3.6 quality, MTP efficiency, and Unsloth's GGUF optimization sets a new bar.

- **[InternScience/Agents-A1](https://huggingface.co/InternScience/Agents-A1)** — As agent-based AI workflows become central to both research and production, this Qwen3.5-MoE agent model offers a practical, open-weight entry point for building multimodal autonomous systems. Its 29K downloads and strong like-to-download ratio suggest early adopters are finding real value.

---
*This digest is auto-generated by [agents-radar](https://github.com/kky-wollu/agents-radar).*