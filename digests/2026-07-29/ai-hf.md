# Hugging Face 热门模型日报 2026-07-29

> 数据来源: [Hugging Face Hub](https://huggingface.co/) | 共 30 个模型 | 生成时间: 2026-07-28 23:04 UTC

---

好的，作为AI模型生态分析师，以下是2026年7月29日的《Hugging Face 热门模型日报》。

---

### **Hugging Face 热门模型日报 | 2026-07-29**

#### **今日速览**

本周 Hugging Face 生态呈现三强争霸格局：**月之暗面（Moonshot AI）** 的 Kimi-K3 以绝对优势登顶，证明了其多模态基础模型的强大吸引力；**百度**的 Unlimited-OCR 凭借惊人的下载量展现了实用型工具模型的巨大市场；而以 **Qwen3.6** 为核心的社区微调与量化生态（如 HauhauCS、empero-ai 的版本）异常火爆，形成了庞大的“衍生模型舰队”。值得一提的是，**微软**在图像编辑（Mage-Flow）与语音（VibeVoice）领域多点开花，而 **Poolside** 的 Laguna-S-2.1 系列则稳固了其在代码生成领域的专业地位。

#### **热门模型**

##### 🧠 **语言模型（LLM、对话模型、指令微调）**

*   **zai-org/GLM-5.2** ([链接](https://huggingface.co/zai-org/GLM-5.2))
    *   **作者**: zai-org | **点赞**: 4,599 (**本周最高**) | **下载**: 1.26M
    *   **一句话**: 智谱 AI 最新一代对话模型，凭借强大的 MoE 架构和对话能力，成为本周点赞最高的非-多模态模型，热度不减。
*   **upstage/Solar-Open2-250B** ([链接](https://huggingface.co/upstage/Solar-Open2-250B))
    *   **作者**: upstage | **点赞**: 643 | **下载**: 4,804
    *   **一句话**: Upstage 开源的 250B 参数超大模型，首次亮相即收获关注，代表了开源社区向更大规模模型进军的趋势。
*   **Nanbeige/Nanbeige4.2-3B** ([链接](https://huggingface.co/Nanbeige/Nanbeige4.2-3B))
    *   **作者**: Nanbeige | **点赞**: 525 | **下载**: 18,933
    *   **一句话**: 一款小体量但性能强劲的 3B 参数语言模型，适合资源受限场景下的部署和应用。
*   **fdtn-ai/antares-1b** ([链接](https://huggingface.co/fdtn-ai/antares-1b))
    *   **作者**: fdtn-ai | **点赞**: 221 | **下载**: 7,666
    *   **一句话**: 专注于安全领域的 1B 参数混合专家模型（GraniteMoEHybrid），为特定垂直行业提供专用解决方案。

##### 🎨 **多模态与生成（图像、视频、音频、文本到X）**

*   **moonshotai/Kimi-K3** ([链接](https://huggingface.co/moonshotai/Kimi-K3))
    *   **作者**: moonshotai | **点赞**: 7,922 (**本周冠军**) | **下载**: 99,214
    *   **一句话**: 本周最热模型！月之暗面推出的新一代多模态基础模型，集图像理解与文本生成于一体，性能与热度均碾压全场。
*   **baidu/Unlimited-OCR** ([链接](https://huggingface.co/baidu/Unlimited-OCR))
    *   **作者**: baidu | **点赞**: 3,407 | **下载**: 2.69M (**本周最高下载**)
    *   **一句话**: 百度的通用 OCR 模型，因其极高的实用性，成为本周下载量最高的模型，是企业和开发者批量处理文档的利器。
*   **thinkingmachines/Inkling** ([链接](https://huggingface.co/thinkingmachines/Inkling))
    *   **作者**: thinkingmachines | **点赞**: 1,624 | **下载**: 39,052
    *   **一句话**: 一款新的多模态对话模型，因其优秀的图像与文本交互能力进入前十。
*   **microsoft/Mage-Flow** ([链接](https://huggingface.co/microsoft/Mage-Flow))
    *   **作者**: microsoft | **点赞**: 415 | **下载**: 2,007
    *   **一句话**: 微软推出的文本到图像生成模型，标志着其在扩散模型领域的又一重要布局，与 DALL-E 和 Midjourney 形成竞争。
*   **owensong/Inflect-Micro-v2** ([链接](https://huggingface.co/owensong/Inflect-Micro-v2))
    *   **作者**: owensong | **点赞**: 261 | **下载**: 645
    *   **一句话**: 专为 CPU 和边缘设备设计的轻量级文本转语音模型，推动了 AI 语音技术的本地化部署。
*   **microsoft/Fara1.5-27B** ([链接](https://huggingface.co/microsoft/Fara1.5-27B))
    *   **作者**: microsoft | **点赞**: 178 | **下载**: 1,543
    *   **一句话**: 微软推出的计算机使用（Computer Use）多模态模型，能理解屏幕截图并执行操作，代表 AI 从对话走向代理（Agent）的关键一步。
*   **ATH-MaaS/OvisOCR2** ([链接](https://huggingface.co/ATH-MaaS/OvisOCR2))
    *   **作者**: ATH-MaaS | **点赞**: 339 | **下载**: 47,129
    *   **一句话**: 基于 Qwen3.5 的 OCR 模型，是百度 Unlimited-OCR 的有力竞争者，也表明 OCR 赛道正变得异常拥挤。

##### 🔧 **专用模型（代码、数学、医疗、嵌入）**

*   **Kwaipilot/KAT-Coder-V2.5-Dev** ([链接](https://huggingface.co/Kwaipilot/KAT-Coder-V2.5-Dev))
    *   **作者**: Kwaipilot | **点赞**: 284 | **下载**: 6,275
    *   **一句话**: 基于 Qwen3.5-MoE 的代码生成模型，专注于提升代码生成任务的表现。
*   **moonshotai/Kimi-K2.7-Code** ([链接](https://huggingface.co/moonshotai/Kimi-K2.7-Code))
    *   **作者**: moonshotai | **点赞**: 1,331 | **下载**: 681,111
    *   **一句话**: Kimi 家族专为代码任务优化的版本，下载量极高，说明开发者对其代码能力寄予厚望。
*   **microsoft/VibeVoice-ASR-BitNet** ([链接](https://huggingface.co/microsoft/VibeVoice-ASR-BitNet))
    *   **作者**: microsoft | **点赞**: 88 | **下载**: 1,754
    *   **一句话**: 微软推出的语音识别模型，采用 BitNet 架构，探索了极低比特量化在 ASR 任务上的应用。

##### 📦 **微调与量化（社区微调、GGUF、AWQ）**

*   **DavidAU/Qwen3.6-27B-Fable-Fusion-711...** ([链接](https://huggingface.co/DavidAU/Qwen3.6-27B-Fable-Fusion-711-Uncensored-Heretic-NM-DAU-NEO-MAX-MTP-GGUF))
    *   **作者**: DavidAU | **点赞**: 841 | **下载**: 736,692
    *   **一句话**: 社区对 Qwen3.6 进行强力微调和无审查（Uncensored）处理的代表作，名字虽长但极具辨识度，满足了特定用户群体的需求。
*   **HauhauCS/Qwen3.6-35B-A3B-Uncensored-...** ([链接](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive))
    *   **作者**: HauhauCS | **点赞**: 3,157 | **下载**: 1.85M
    *   **一句话**: 在 Qwen 官方版基础上进行激进微调和无审查处理的版本，点赞和下载量均极高，是社区最活跃的衍生模型之一。
*   **prism-ml/Ternary-Bonsai-27B-gguf** ([链接](https://huggingface.co/prism-ml/Ternary-Bonsai-27B-gguf))
    *   **作者**: prism-ml | **点赞**: 1,082 | **下载**: 665,427
    *   **一句话**: 采用前沿的三元量化（Ternary）技术，将模型权重压缩至极低的 2-bit，代表了模型量化领域的前沿探索。
*   **prism-ml/Bonsai-27B-gguf** ([链接](https://huggingface.co/prism-ml/Bonsai-27B-gguf))
    *   **作者**: prism-ml | **点赞**: 672 | **下载**: 2.33M
    *   **一句话**: 采用更激进的 1-bit 量化，尽管质量可能损失，但下载量巨大，说明社区对极致模型压缩的渴望。
*   **LuffyTheFox/Qwen3.6-35B-A3B-Uncensored-...** ([链接](https://huggingface.co/LuffyTheFox/Qwen3.6-35B-A3B-Uncensored-Genesis-Hermes-V6-GGUF))
    *   **作者**: LuffyTheFox | **点赞**: 194 | **下载**: 99,660
    *   **一句话**: 另一个基于 Qwen3.6 的社区微调版本，集成了 Hermes 风格，显示了 Qwen3.6 微调生态的繁荣。
*   **empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF** ([链接](https://huggingface.co/empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF))
    *   **作者**: empero-ai | **点赞**: 2,501 | **下载**: 1.26M
    *   **一句话**: 一个极具特色的社区模型，可能融合了 Claude 风格的合成数据或理念，在推理任务上表现突出，下载量惊人。

#### **生态信号**

本周生态呈现出 **“基础模型 + 社区生态”** 的双轮驱动模式。**Qwen3.6** 无疑是本周最大的赢家，其衍生模型数量、点赞和下载量总和已远超其他家族，形成了类似 Linux 内核的强大社区生态。这标志着“开源基础模型 + 专业/个性化微调”的模式已成为绝对主流。**大量无审查（Uncensored）和激进微调版本的涌现**，也反映了社区对模型自由度与可控性的强烈需求。**微软**则展现了其“大而全”的开源策略，在多模态、图像生成、计算机使用、语音等多个前沿领域同时落子。量化方面，**Prism-ml** 的 1-bit 与 2-bit 模型引发了高度关注，尽管存在质量损失，但其在极低资源部署上的巨大潜力吸引了大量探索者。

#### **值得探索**

1.  **moonshotai/Kimi-K3** ([链接](https://huggingface.co/moonshotai/Kimi-K3)): 本周的绝对热度焦点，代表了国内多模态模型的最新高度。无论是研究性能还是体验最新多模态能力，都值得第一时间上手。
2.  **microsoft/Mage-Flow** ([链接](https://huggingface.co/microsoft/Mage-Flow)) : 微软在文本到图像生成领域的重磅产品。如果你是图像生成领域的开发者或爱好者，应该立即尝试，对比其与 DALL-E 3 和 Stable Diffusion 3 的能力差异。
3.  **prism-ml/Ternary-Bonsai-27B-gguf** ([链接](https://huggingface.co/prism-ml/Ternary-Bonsai-27B-gguf)): 如果你对模型量化前沿技术感兴趣或需要在极低资源下（如手机、树莓派）运行大模型，这款采用三元量化技术的模型将为你打开新世界的大门。

---
*本日报由 [agents-radar](https://github.com/kky-wollu/agents-radar) 自动生成。*