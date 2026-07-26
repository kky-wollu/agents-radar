# Hugging Face Trending Models Digest 2026-07-27

> Source: [Hugging Face Hub](https://huggingface.co/) | 30 models | Generated: 2026-07-26 23:02 UTC

---

Here is the **Hugging Face Trending Models Digest** for **2026-07-27**.

---

## 1. Today's Highlights

The spotlight this week is on **extreme model compression**, with **1-bit and 2-bit LLMs** (like `Ternary-Bonsai-27B` and `Bonsai-27B`) from **prism-ml** gaining massive traction—amassing over 2.8M combined downloads and proving that sub-4-bit quantization is now viable for production-grade reasoning. **Baidu/Unlimited-OCR** continues its runaway success as the most-liked model on the platform, signaling a hunger for universal OCR solutions. In the LLM space, **GLM-5.2** (from zai-org) leads in likes with a strong MoE architecture, while **MoonshotAI’s Kimi-K2.7-Code** and **Qwen3.6**-based fine-tunes dominate the code and reasoning niches. The robotics category sees a notable entry from **OpenBMB** with two new Vision-Language-Action models.

## 2. Trending Models

### 🧠 Language Models (LLMs, Chat, Instruction)

- **zai-org/GLM-5.2** – *Likes: 4,473 | Downloads: 827k*  
  A Mixture-of-Experts conversational model with strong DSA (dynamic sparse attention), leading the week in likes due to its balance of efficiency and reasoning quality.

- **upstage/Solar-Open2-250B** – *Likes: 589 | Downloads: 3.3k*  
  A massive 250B open-weight model from Upstage, competing at the frontier of open-source LLMs with strong multilingual and instruction-following capabilities.

- **Nanbeige/Nanbeige4.2-3B** – *Likes: 442 | Downloads: 14k*  
  A compact 3B LLM ideal for edge deployment, trending for its surprisingly strong performance-to-size ratio.

- **poolside/Laguna-S-2.1** – *Likes: 694 | Downloads: 56k*  
  Poolside’s flagship code-focused LLM, seeing multiple quantized variants (GGUF, NVFP4) and strong ecosystem adoption this week.

- **fdtn-ai/antares-1b** – *Likes: 185 | Downloads: 5.9k*  
  A 1B hybrid MoE model emphasizing security, trending as a lightweight, safety-aligned alternative for enterprise fine-tuning.

- **Motif-Technologies/Motif-3-Beta** – *Likes: 193 | Downloads: 2.4k*  
  A new feature-extraction and text-generation hybrid model, likely gaining attention for RAG and embedding use cases.

- **bottlecapai/ThinkingCap-Qwen3.6-27B** – *Likes: 555 | Downloads: 27k*  
  A fine-tune of Qwen3.6 optimized for chain-of-thought reasoning, popular among the reasoning-benchmark community.

### 🎨 Multimodal & Generation

- **baidu/Unlimited-OCR** – *Likes: 3,198 | Downloads: 2.59M*  
  A universal image-text-to-text OCR model from Baidu. **Most downloaded model this week**, likely the go-to for document parsing and digitization pipelines.

- **thinkingmachines/Inkling** – *Likes: 1,579 | Downloads: 34k*  
  A conversational multimodal model with strong image understanding, trending for its natural chat interaction style.

- **microsoft/Mage-Flow** – *Likes: 333 | Downloads: 1.3k*  
  Microsoft’s text-to-image diffusion model with built-in editing capabilities, signaling advances in instruction-based image generation.

- **microsoft/Mage-Flow-Edit-Turbo** – *Likes: 88 | Downloads: 946*  
  The faster, image-to-image sibling of Mage-Flow, enabling rapid local edits from reference images.

- **owensong/Inflect-Micro-v2** – *Likes: 173 | Downloads: 298*  
  A tiny, CPU-friendly text-to-speech model for edge AI, filling a gap for offline voice synthesis on low-resource devices.

- **nvidia/Cosmos3-Edge** – *Likes: 125 | Downloads: 32k*  
  NVIDIA’s edge-optimized diffusion model for Cosmos3, likely aimed at real-time image generation on IoT and mobile hardware.

### 🔧 Specialized Models

- **Kwaipilot/KAT-Coder-V2.5-Dev** – *Likes: 195 | Downloads: 3.7k*  
  A MoE coder model based on Qwen3.5, trending for its code generation accuracy and dual image-text support.

- **moonshotai/Kimi-K2.7-Code** – *Likes: 1,293 | Downloads: 730k*  
  MoonshotAI’s compressed coder model with strong feature extraction and compressed-tensor support, widely used for code completion and reasoning.

- **ATH-MaaS/OvisOCR2** – *Likes: 307 | Downloads: 35k*  
  A Qwen3.5-based OCR model, a strong alternative to Unlimited-OCR for specialized document understanding.

- **microsoft/Fara1.5-27B** – *Likes: 107 | Downloads: 1.2k*  
  A computer-use agent model (vision-language-action), representing Microsoft’s push toward autonomous GUI interaction.

- **openbmb/MiniCPM-RobotManip** – *Likes: 177 | Downloads: 643*  
  A Vision-Language-Action (VLA) model for robotic manipulation, enabling language-guided physical tasks.

- **openbmb/MiniCPM-RobotTrack** – *Likes: 130 | Downloads: 398*  
  A companion VLA model for visual tracking and robot navigation, both from OpenBMB’s expanding robotics suite.

### 📦 Fine-tunes & Quantizations

- **DavidAU/Qwen3.6-27B-Fable-Fusion-711-Uncensored-Heretic-NM-DAU-NEO-MAX-MTP-GGUF** – *Likes: 630 | Downloads: 552k*  
  An extensive GGUF quantization of Qwen3.6 with uncensored fine-tuning, highly downloaded for role-play and creative writing.

- **HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive** – *Likes: 3,112 | Downloads: 1.92M*  
  A highly popular MoE vision model with aggressive uncensored fine-tuning, breaking into the top-3 by likes this week.

- **empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF** – *Likes: 2,477 | Downloads: 1.41M*  
  A GGUF-optimized reasoning model blending Qwen3.5 base with Claude-style mythos training, trending for creative reasoning.

- **prism-ml/Bonsai-27B-gguf** – *Likes: 651 | Downloads: 2.18M*  
  A **1-bit** quantized 27B model using llama.cpp, proving that extreme compression can retain conversational quality.

- **prism-ml/Ternary-Bonsai-27B-gguf** – *Likes: 1,049 | Downloads: 631k*  
  A **2-bit ternary** variant of Bonsai, achieving remarkable efficiency for long-context and edge deployment.

- **unsloth/Laguna-S-2.1-GGUF** – *Likes: 200 | Downloads: 102k*  
  Unsloth’s optimized GGUF of Laguna-S-2.1, making poolside’s code model accessible to consumer GPUs.

- **poolside/Laguna-S-2.1-NVFP4** – *Likes: 143 | Downloads: 138k*  
  A FP4 quantization for NVIDIA GPUs, enabling high-speed inference on Hopper and Blackwell architectures.

- **poolside/Laguna-S-2.1-GGUF** – *Likes: 143 | Downloads: 82k*  
  Official poolside GGUF variant for CPU/offline inference.

- **LuffyTheFox/Qwen3.6-35B-A3B-Uncensored-Genesis-Hermes-V5-GGUF** – *Likes: 172 | Downloads: 73k*  
  Another uncensored Qwen3.6 fine-tune with Hermes-based alignment, popular in the creative and uncensored LLM community.

- **conradlocke/krea2-identity-edit** – *Likes: 542 | Downloads: 0*  
  A LoRA for identity-preserving image editing using Krea-2, trending for its potential in AI portrait editing.

- **baseten/GLM-5.2-Vision-NVFP4** – *Likes: 110 | Downloads: 2k*  
  NVIDIA FP4 quantization of GLM-5.2’s vision variant, enabling multimodal inference at ultra-low precision.

## 3. Ecosystem Signal

The most significant momentum is around **ultra-low-bit quantization** on large models (27B-35B at 1-bit/2-bit). **prism-ml’s Bonsai** series (both 1-bit and ternary) is defining a new sub-genre of "viable sub-4-bit LLMs", which are enabling tasks like long-context chat and reasoning on consumer hardware. The **Qwen3.6 ecosystem** remains the dominant base for fine-tunes and Quantization, with at least 5 variants in the top 30—especially uncensored and MoE configurations. **Open-weight competition** continues to intensify: Solar-Open2-250B, GLM-5.2, and Kimi-K2.7-Code show that large Chinese labs and Western startups are both pushing frontier open models. **Robotics VLA models** (MiniCPM-RobotManip/Track) are a notable new frontier, suggesting language models are increasingly being tuned for physical action, not just text. In quantization, **GGUF** still dominates CPU deployment, but **NVFP4** (NVIDIA’s FP4 format) is emerging as a new hardware-backed standard for GPU inference.

## 4. Worth Exploring

1. **prism-ml/Ternary-Bonsai-27B-gguf** – Absolutely worth studying as the frontier of 2-bit ternary quantization. It delivers conversational quality at a fraction of the memory cost, making it a benchmark for future edge LLMs.

2. **moonshotai/Kimi-K2.7-Code** – A compressed coder that has found massive adoption (730k downloads). Its use of compressed-tensors and feature extraction for code is a unique architecture worth diving into if you work on code LLM pipelines.

3. **openbmb/MiniCPM-RobotManip** – One of the first Vision-Language-Action models openly available. If you're exploring robotics or autonomous GUI agents, this is a must-try for understanding how LLMs transfer to physical action.

---
*This digest is auto-generated by [agents-radar](https://github.com/kky-wollu/agents-radar).*