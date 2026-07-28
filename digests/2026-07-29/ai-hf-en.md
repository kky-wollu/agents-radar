# Hugging Face Trending Models Digest 2026-07-29

> Source: [Hugging Face Hub](https://huggingface.co/) | 30 models | Generated: 2026-07-28 23:04 UTC

---

Here is the structured Hugging Face Trending Models Digest for 2026-07-29.

---

## Hugging Face Trending Models Digest – 2026-07-29

### 1. Today's Highlights

This week’s trending ecosystem is defined by three major themes: the explosive growth of **Mixture-of-Experts (MoE) vision-language models**, the rise of **extreme quantization (1-2 bit)**, and the continued refinement of **code and state-of-the-art multimodal OCR**. **MoonshotAI’s Kimi-K3** continues to dominate absolute likes, while **Qwen/Qwen3.6-35B-A3B** leads in downloads, signaling a broad community appetite for efficient MoE architectures. On the quantization frontier, **prism-ml’s Ternary-Bonsai-27B-gguf** (2-bit) and **Bonsai-27B-gguf** (1-bit) are gaining significant traction, proving that aggressive compression is becoming a production reality. Finally, specialized models like **baidu/Unlimited-OCR** and **ATH-MaaS/OvisOCR2** highlight a growing demand for dedicated document and image-text extraction tools.

---

### 2. Trending Models by Category

#### 🧠 Language Models (LLMs, chat models, instruction-tuned)

- **[GLM-5.2](https://huggingface.co/zai-org/GLM-5.2)** – zai-org | 4,599 likes, 1.27M downloads
  A high-performance conversational MoE model (DSA architecture) that has captured the community's attention for its strong reasoning and multi-turn dialogue abilities.

- **[Nanbeige4.2-3B](https://huggingface.co/Nanbeige/Nanbeige4.2-3B)** – Nanbeige | 525 likes, 18.9K downloads
  A compact yet powerful 3B text-generation model, gaining traction for its efficient performance on resource-constrained devices.

- **[Solar-Open2-250B](https://huggingface.co/upstage/Solar-Open2-250B)** – upstage | 643 likes, 4.8K downloads
  A massive open-weight 250B model from Upstage, notable for pushing the boundaries of open-source scale.

- **[Laguna-S-2.1](https://huggingface.co/poolside/Laguna-S-2.1)** – poolside | 798 likes, 67.3K downloads
  Poolside’s flagship coding and general-purpose LLM, continuing to see strong interest from the developer and enterprise community.

- **[fdtn-ai/antares-1b](https://huggingface.co/fdtn-ai/antares-1b)** – fdtn-ai | 221 likes, 7.7K downloads
  A 1B parameter model with a GraniteMoEHybrid architecture, trending due to its focus on security-aligned text generation.

#### 🎨 Multimodal & Generation (image, video, audio, text-to-X)

- **[moonshotai/Kimi-K3](https://huggingface.co/moonshotai/Kimi-K3)** – moonshotai | 7,922 likes, 99.2K downloads / **[unslo](https://huggingface.co/unsloth/Kimi-K3)** | 146 likes
  The top-trending model, a compressed-tensor vision-language model (Kimi K3) setting a high bar for multimodal benchmarks and community engagement.

- **[Qwen/Qwen3.6-35B-A3B](https://huggingface.co/Qwen/Qwen3.6-35B-A3B)** – Qwen | 2,567 likes, 6.16M downloads
  The current download king; a 35B parameter MoE vision model with 3B active parameters, making advanced multimodal reasoning accessible and fast.

- **[microsoft/Mage-Flow](https://huggingface.co/microsoft/Mage-Flow)** – microsoft | 415 likes, 2K downloads / **[Mage-Flow-Edit-Turbo](https://huggingface.co/microsoft/Mage-Flow-Edit-Turbo)** | 109 likes
  A new generation of text-to-image and instruction-based image editing models from Microsoft, representing the cutting edge of image generation workflows.

- **[owensong/Inflect-Micro-v2](https://huggingface.co/owensong/Inflect-Micro-v2)** – owensong | 261 likes, 645 downloads / **[Inflect-Nano-v2](https://huggingface.co/owensong/Inflect-Nano-v2)** | 102 likes
  Small, CPU-friendly text-to-speech models designed for local and edge-AI deployment, attracting interest for their low latency and high voice quality.

- **[microsoft/VibeVoice-ASR-BitNet](https://huggingface.co/microsoft/VibeVoice-ASR-BitNet)** – microsoft | 88 likes, 1.8K downloads
  An automatic speech recognition model using BitNet and GGUF quantization, hinting at a future of highly compressed, edge-ready audio AI.

- **[baseten/GLM-5.2-Vision-NVFP4](https://huggingface.co/baseten/GLM-5.2-Vision-NVFP4)** – baseten | 130 likes, 2.8K downloads
  A quantized (NVFP4) version of the GLM-5.2 vision variant, optimized for high-throughput serving via SGLang.

- **[thinkingmachines/Inkling](https://huggingface.co/thinkingmachines/Inkling)** – thinkingmachines | 1,624 likes, 39K downloads
  A new multimodal conversation model that has captured attention for its engaging visual understanding and interactive capabilities.

#### 🔧 Specialized Models (code, math, medical, embeddings)

- **[Kwaipilot/KAT-Coder-V2.5-Dev](https://huggingface.co/Kwaipilot/KAT-Coder-V2.5-Dev)** – Kwaipilot | 284 likes, 6.3K downloads
  A MoE coder model built on Qwen3.5, designed to handle complex code generation and image-text-to-code tasks, trending among developer tools.

- **[moonshotai/Kimi-K2.7-Code](https://huggingface.co/moonshotai/Kimi-K2.7-Code)** – moonshotai | 1,331 likes, 681K downloads
  A specialized code-focused version of the Kimi K2.5 series, admired for its precision in solving programming and debugging tasks.

- **[ATH-MaaS/OvisOCR2](https://huggingface.co/ATH-MaaS/OvisOCR2)** – ATH-MaaS | 339 likes, 47.1K downloads
  A high-accuracy OCR model built on Qwen3.5, trending as a lighter alternative to larger OCR solutions for document processing.

#### 📦 Fine-tunes & Quantizations (community fine-tunes, GGUF, AWQ)

- **[prism-ml/Ternary-Bonsai-27B-gguf](https://huggingface.co/prism-ml/Ternary-Bonsai-27B-gguf)** – prism-ml | 1,082 likes, 665K downloads
  A 2-bit ternary quantized 27B model, proving that extreme compression can retain conversational quality while drastically reducing memory footprint.

- **[prism-ml/Bonsai-27B-gguf](https://huggingface.co/prism-ml/Bonsai-27B-gguf)** – prism-ml | 672 likes, 2.34M downloads
  The 1-bit cousin of the above; the highest download volume among quantized models, indicating massive community interest in minimal-resource LLMs.

- **[DavidAU/Qwen3.6-27B-Fable-Fusion-711](https://huggingface.co/DavidAU/Qwen3.6-27B-Fable-Fusion-711-Uncensored-Heretic-NM-DAU-NEO-MAX-MTP-GGUF)** – DavidAU | 841 likes, 737K downloads
  A heavily fine-tuned, uncensored Qwen3.6 variant in GGUF format, trending for its controversial fusion of multiple fine-tuning approaches.

- **[HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)** – HauhauCS | 3,157 likes, 1.86M downloads
  An uncensored, aggressive-style variant of the Qwen3.6 MoE vision model, demonstrating high demand for alignment-free, high-agency chat.

- **[empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF](https://huggingface.co/empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF)** – empero-ai | 2,501 likes, 1.26M downloads
  A quantized 9B reasoning model based on Qwen3.5, blending Claude-style mythos prompting with strong logical reasoning capabilities.

- **[poolside/Laguna-S-2.1-GGUF](https://huggingface.co/poolside/Laguna-S-2.1-GGUF)** – poolside | 160 likes, 90K downloads / **[unsloth/Laguna-S-2.1-GGUF](https://huggingface.co/unsloth/Laguna-S-2.1-GGUF)** – unsloth | 231 likes, 130K downloads
  Official and unsloth-quantized GGUF versions of the Laguna-S-2.1 model, enabling local deployment of this powerful 2.1B model.

- **[conradlocke/krea2-identity-edit](https://huggingface.co/conradlocke/krea2-identity-edit)** – conradlocke | 564 likes, 0 downloads
  A LoRA for Krea-2 focusing on identity-preserving image editing, highlighting the niche but dedicated ComfyUI and inpainting community.

---

### 3. Ecosystem Signal

The ecosystem is currently riding a **Qwen3.6/Qwen3.5 wave**, with nearly a third of trending models being derivatives or quantizations of the Qwen MoE vision-language family. The success of **Qwen3.6-35B-A3B (6M+ downloads)** signals that the market demands efficient, high-quality MoE architectures that scale active parameters down (3B active out of 35B total) without sacrificing capability. This aligns with the rise of **extreme quantization (Bonsai 1-bit, Ternary-Bonsai 2-bit)**, where the community is pushing storage efficiency to its absolute limits, making 27B models deployable on consumer hardware.

Open-weight models are clearly winning the trending race; proprietary pipelines are nearly absent from this list. The **MoonshotAI Kimi series** and **GLM-5.2** stand out as strong competitors to Qwen in the vision-language space. Finally, the **"uncensored" fine-tuning trend** remains robust—multiple Qwen3.6 variants with aggressive or uncensored tags are among the most downloaded, indicating a persistent sub-community prioritizing alignment flexibility over safety guardrails.

---

### 4. Worth Exploring

1. **[prism-ml/Ternary-Bonsai-27B-gguf](https://huggingface.co/prism-ml/Ternary-Bonsai-27B-gguf)**
   This is the most important model to study for anyone interested in on-device or resource-efficient AI. Its ability to maintain coherent conversation at 2-bit quantization represents a breakthrough in model compression, and it sets a precedent for future "bonzai trees" of AI—small, powerful, and locally runnable.

2. **[microsoft/Mage-Flow](https://huggingface.co/microsoft/Mage-Flow)**
   As image generation moves toward instruction-based editing and fine-grained control, Mage-Flow is a must-explore for diffusion enthusiasts. Its Turbo variant suggests Microsoft is optimizing for speed, making it a prime candidate for real-time creative tools.

3. **[ATH-MaaS/OvisOCR2](https://huggingface.co/ATH-MaaS/OvisOCR2)**
   For practitioners dealing with document intelligence, OvisOCR2 offers a compelling balance of accuracy and runtime efficiency. Its use of the Qwen3.5 backbone makes it compatible with the broader MoE ecosystem, and it may serve as the foundation for many enterprise RAG and data extraction pipelines.

---
*This digest is auto-generated by [agents-radar](https://github.com/kky-wollu/agents-radar).*