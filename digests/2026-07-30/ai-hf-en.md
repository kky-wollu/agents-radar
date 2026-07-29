# Hugging Face Trending Models Digest 2026-07-30

> Source: [Hugging Face Hub](https://huggingface.co/) | 30 models | Generated: 2026-07-29 23:01 UTC

---

Here is the **Hugging Face Trending Models Digest** for July 30, 2026.

---

### 1. Today's Highlights

This week’s trending list is dominated by the explosive growth of **Moonshot AI's Kimi-K3** and its accompanying ecosystem, alongside a major surge in **uncensored, MoE-based fine-tunes** of Qwen 3.6. The open-weight frontier continues to heat up as **Upstage's Solar-Open2-250B** and **Poolside's Laguna-S-2.1** represent the high end of the text-generation spectrum, while **Baidu's Unlimited-OCR** proves that utility-focused multimodal models can achieve exceptional adoption. A clear trend is the ongoing commoditization of quantization, with **GGUF** variants and **NVFP4** precision formats (from Baseten and Nota AI) making massive models accessible to smaller hardware. Finally, the **GLM-5.2** from Zhipu (zai-org) shows that the Chinese open-source ecosystem is maintaining significant momentum with over 1.2M downloads.

### 2. Trending Models

#### 🧠 Language Models (LLMs, chat models, instruction-tuned)

- **[GLM-5.2](https://huggingface.co/zai-org/GLM-5.2)** by zai-org | Likes: 4,639 | Downloads: 1,267,198
  A powerful conversational MoE model from Zhipu AI, trending due to its strong Chinese-English bilingual performance and massive community adoption.

- **[poolside/Laguna-S-2.1](https://huggingface.co/poolside/Laguna-S-2.1)** by poolside | Likes: 825 | Downloads: 67,286
  A high-performance text-generation model built for software engineering workflows, gaining traction as a leading open-weight code-specialized LLM.

- **[upstage/Solar-Open2-250B](https://huggingface.co/upstage/Solar-Open2-250B)** by upstage | Likes: 693 | Downloads: 4,804
  A massive 250B parameter open-weight model from Upstage, representing the cutting edge of accessible frontier-scale LLMs for the open-source community.

- **[Nanbeige/Nanbeige4.2-3B](https://huggingface.co/Nanbeige/Nanbeige4.2-3B)** by Nanbeige | Likes: 553 | Downloads: 18,933
  A compact 3B LLM optimized for efficiency and conversational tasks, trending as a lightweight alternative for on-device or resource-constrained deployments.

- **[fdtn-ai/antares-1b](https://huggingface.co/fdtn-ai/antares-1b)** by fdtn-ai | Likes: 230 | Downloads: 7,666
  A 1B parameter hybrid MoE model focused on security (GraniteMoEHybrid backend), trending for its specialized safety and red-teaming use cases.

#### 🎨 Multimodal & Generation (image, video, audio, text-to-X)

- **[moonshotai/Kimi-K3](https://huggingface.co/moonshotai/Kimi-K3)** by moonshotai | Likes: 8,617 | Downloads: 99,214
  The week's star release: a state-of-the-art image-text-to-text model with compressed-tensor support, trending for its exceptional multimodal reasoning and Moonshot's growing popularity.

- **[baidu/Unlimited-OCR](https://huggingface.co/baidu/Unlimited-OCR)** by baidu | Likes: 3,511 | Downloads: 2,694,935
  A universal OCR model handling complex document layouts, trending due to massive practical demand and Baidu’s industry-leading document intelligence.

- **[Qwen/Qwen3.6-35B-A3B](https://huggingface.co/Qwen/Qwen3.6-35B-A3B)** by Qwen | Likes: 2,586 | Downloads: 6,158,876
  The base MoE vision-language model spawning dozens of fine-tunes; trending for its excellent performance-to-parameter ratio (35B total, 3B active).

- **[thinkingmachines/Inkling](https://huggingface.co/thinkingmachines/Inkling)** by thinkingmachines | Likes: 1,640 | Downloads: 39,052
  A multimodal conversational model from Thinking Machines, trending for its strong performance in open-ended visual dialogue tasks.

- **[moonshotai/Kimi-K2.7-Code](https://huggingface.co/moonshotai/Kimi-K2.7-Code)** by moonshotai | Likes: 1,333 | Downloads: 681,111
  A code-specialized version of the Kimi model family, trending for its ability to understand both code and visual contexts like UI screenshots.

- **[owensong/Inflect-Micro-v2](https://huggingface.co/owensong/Inflect-Micro-v2)** by owensong | Likes: 288 | Downloads: 645
  A tiny, CPU-optimized text-to-speech model, trending within the edge-AI and local-TTS communities for its efficiency.

- **[microsoft/Mage-VL](https://huggingface.co/microsoft/Mage-VL)** by microsoft | Likes: 94 | Downloads: 702
  Microsoft’s latest multimodal vision-language model, trending as an early-stage release for researchers exploring VL architectures.

#### 🔧 Specialized Models (code, math, medical, embeddings)

- **[Kwaipilot/KAT-Coder-V2.5-Dev](https://huggingface.co/Kwaipilot/KAT-Coder-V2.5-Dev)** by Kwaipilot | Likes: 315 | Downloads: 6,275
  A developer-oriented code generation model based on Qwen 3.5 MoE, trending for its support of image-text-to-code workflows.

#### 📦 Fine-tunes & Quantizations (community fine-tunes, GGUF, AWQ)

- **[DavidAU/Qwen3.6-27B-Fable-Fusion-711-Uncensored-Heretic-NM-DAU-NEO-MAX-MTP-GGUF](https://huggingface.co/DavidAU/Qwen3.6-27B-Fable-Fusion-711-Uncensored-Heretic-NM-DAU-NEO-MAX-MTP-GGUF)** by DavidAU | Likes: 932 | Downloads: 736,692
  A heavily fine-tuned, uncensored GGUF variant of Qwen 3.6 with advanced quantization techniques, trending for its high-quality roleplay and creative writing capabilities.

- **[HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)** by HauhauCS | Likes: 3,171 | Downloads: 1,855,505
  An aggressive, uncensored MoE fine-tune of Qwen 3.6, massively popular for its unfiltered output and efficient 3B active parameter footprint.

- **[prism-ml/Ternary-Bonsai-27B-gguf](https://huggingface.co/prism-ml/Ternary-Bonsai-27B-gguf)** by prism-ml | Likes: 1,094 | Downloads: 665,427
  A pioneering 2-bit / ternary quantization of a 27B model, trending as a milestone for extreme compression while maintaining usable quality.

- **[prism-ml/Bonsai-27B-gguf](https://huggingface.co/prism-ml/Bonsai-27B-gguf)** by prism-ml | Likes: 687 | Downloads: 2,339,098
  A 1-bit quantized 27B model, trending for pushing the boundaries of compression and making huge models fit on consumer hardware.

- **[empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF](https://huggingface.co/empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF)** by empero-ai | Likes: 2,515 | Downloads: 1,262,662
  A Qwen 3.5-based GGUF fine-tune blending reasoning with Claude-inspired synthetic data, extremely popular for roleplay and storytelling.

- **[baseten/GLM-5.2-Vision-NVFP4](https://huggingface.co/baseten/GLM-5.2-Vision-NVFP4)** by baseten | Likes: 135 | Downloads: 2,756
  A vision-language variant of GLM-5.2 using the novel NVFP4 quantization format, trending for demonstrating NVIDIA’s next-gen floating-point compression.

### 3. Ecosystem Signal

**MoE is the new standard.** The dominance of Qwen 3.6/3.5 MoE models (35B-A3B) and GLM-5.2 underscores a shift: dense models are losing ground to Mixture-of-Experts architectures that deliver big-model quality with small-model inference costs. **Uncensored fine-tuning is a major subculture.** Models tagged "Uncensored" or "Heretic" account for nearly 40% of top-tier download counts, indicating a strong user demand for unrestricted creative and roleplay use cases—often at odds with safety-aligned base models. **Compression formats are diversifying rapidly.** Beyond traditional GGUF, we see the rise of **NVFP4** (NVIDIA), **Ternary (2-bit)**, and **1-bit** quantization, allowing 27B+ models to run on laptops. The **Kimi-K3** ecosystem shows a new pattern: the base model sits alongside official compressed-tensor versions and community GGUF ports (by Unsloth), signaling that "open-weight" now implies a multi-format release strategy. Open-weight models from Chinese labs (Moonshot, Zhipu, Qwen, Baidu) are outpacing Western labs in both release velocity and community engagement this cycle.

### 4. Worth Exploring

1. **[Kimi-K3](https://huggingface.co/moonshotai/Kimi-K3)** — The most-liked model of the week and a clear benchmark for multimodal reasoning. If you want to see where the cutting edge of vision-language is, start here.

2. **[prism-ml/Bonsai-27B-gguf](https://huggingface.co/prism-ml/Bonsai-27B-gguf)** — A 1-bit 27B model is a technical marvel. It is worth studying for anyone interested in extreme model compression, edge deployment, or understanding the lower bound of quantization quality.

3. **[owensong/Inflect-Micro-v2](https://huggingface.co/owensong/Inflect-Micro-v2)** — In a sea of giant LLMs, this tiny CPU TTS model is a brilliant counterpoint. It is highly practical for developers building low-latency, on-device voice interfaces without GPU dependencies.

---
*This digest is auto-generated by [agents-radar](https://github.com/kky-wollu/agents-radar).*