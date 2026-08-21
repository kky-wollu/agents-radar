# Hugging Face 热门模型日报 2026-08-22

> 数据来源: [Hugging Face Hub](https://huggingface.co/) | 共 30 个模型 | 生成时间: 2026-08-21 22:29 UTC

---

# 🤖 Hugging Face 热门模型日报 — 2026-08-22

## 📌 今日速览

本周 Hugging Face 生态呈现**多模态与量化双轮驱动**的格局。Qwen3.8-27B 凭借 27B 参数、多模态能力与社区生态的全面爆发，以近 12K 周赞独占鳌头，衍生出超过 10 个量化/去审查/微调变体，形成完整的社区生态链。MiniMax 的 H3 视频生成模型以 4.3K 点赞和超 360 万下载量展示了视频生成赛道的火热。DeepSeek 与 Kimi 的旗舰模型（V4 系列、K3）热度不减，但下载量仍落后于 Qwen 衍生品，说明社区生态的活跃程度正在成为衡量模型影响力的重要指标。此外，"去审查"（abliterated/uncensored）模型在本周榜单中占据近三分之一席位，成为不容忽视的社区趋势。

---

## 🧠 语言模型

| 模型 | 作者 | 点赞 | 下载 | 说明 |
|------|------|------|------|------|
| [**Qwen/Qwen3.8-27B**](https://huggingface.co/Qwen/Qwen3.8-27B) | Qwen | 11,943 | 1,726,651 | 本周冠军。Qwen3.8 系列旗舰多模态模型，实现图像+文本联合理解，兼顾对话与视觉推理。 |
| [**moonshotai/Kimi-K3**](https://huggingface.co/moonshotai/Kimi-K3) | moonshotai | 10,910 | 2,448,810 | 月之暗面新一代多模态模型，主打超高压缩率（compressed-tensors），支持 feature-extraction。 |
| [**deepseek-ai/DeepSeek-V4-Pro-0813**](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro-0813) | deepseek-ai | 704 | 49,601 | DeepSeek V4 系列 Pro 版本，文本生成能力对标闭源前沿模型。 |
| [**Qwen/Qwen3.8-2.4T-A95B**](https://huggingface.co/Qwen/Qwen3.8-2.4T-A95B) | Qwen | 1,135 | 15,702 | Qwen3.8 巨型 MoE 变体，2.4T 总参数/95B 激活，面向高难度推理任务。 |
| [**deepseek-ai/DeepSeek-V4-Flash-0731**](https://huggingface.co/deepseek-ai/DeepSeek-V4-Flash-0731) | deepseek-ai | 3,605 | 2,833,064 | V4 Flash 轻量版，性能/速度平衡极佳，下载量位居前列。 |
| [**superwhisper/s1-mini**](https://huggingface.co/superwhisper/s1-mini) | superwhisper | 185 | 1,136 | 一体化语音识别+文本生成模型，基于 Qwen3 架构。 |

---

## 🎨 多模态与生成模型

| 模型 | 作者 | 点赞 | 下载 | 说明 |
|------|------|------|------|------|
| [**MiniMaxAI/MiniMax-H3**](https://huggingface.co/MiniMaxAI/MiniMax-H3) | MiniMaxAI | 4,289 | 3,614,443 | 新一代视频生成模型，支持文本/图像驱动视频生成，H3 架构实现跨模态一致性。 |
| [**Lightricks/LTX-2.5**](https://huggingface.co/Lightricks/LTX-2.5) | Lightricks | 1,481 | 654,175 | 全能视频生成工具，支持 image-to-video、text-to-video 等多任务，单文件即插即用。 |
| [**MiniMaxAI/MiniMax-Music3**](https://huggingface.co/MiniMaxAI/MiniMax-Music3) | MiniMaxAI | 1,157 | 15,678 | 文本到音乐生成模型，基于 diffusers 生态，扩展了文本生成边界。 |
| [**meta-models/Muse-Glimmer-30B**](https://huggingface.co/meta-models/Muse-Glimmer-30B) | meta-models | 1,731 | 505,113 | Meta 新一代多模态模型，30B 参数，支持图像+文本+对话联合理解。 |
| [**TenStrip/10Eros-Max**](https://huggingface.co/TenStrip/10Eros-Max) | TenStrip | 306 | 0 | MiniMax-H3 的社区微调版本，刚发布即获关注（尚未产生下载）。 |

---

## 🔧 专用模型

| 模型 | 作者 | 点赞 | 下载 | 说明 |
|------|------|------|------|------|
| [**ornith-ai/Ornith-1.5-35B-A3B**](https://huggingface.co/ornith-ai/Ornith-1.5-35B-A3B) | ornith-ai | 280 | 9,165 | 基于 Qwen3.5 MoE 的 35B/3B 激活模型，主打高性价比推理。 |
| [**ornith-ai/Ornith-1.5-35B-A3B-GGUF**](https://huggingface.co/ornith-ai/Ornith-1.5-35B-A3B-GGUF) | ornith-ai | 198 | 123,237 | Ornith 的 GGUF 量化版，MIT 许可，兼容 llama.cpp 等推理框架。 |
| [**froggeric/Qwen-Fixed-Chat-Templates**](https://huggingface.co/froggeric/Qwen-Fixed-Chat-Templates) | froggeric | 1,364 | 0 | 修复 Qwen 3.5 系列对话模板的 Jinja 补丁包，解决了社区广泛存在的通用问题。 |
| [**z-lab/Qwen3.8-27B-DFlash2**](https://huggingface.co/z-lab/Qwen3.8-27B-DFlash2) | z-lab | 167 | 21,092 | 带投机解码（speculative decoding）的 Qwen3.8 变体，推理加速。 |

---

## 📦 微调与量化模型

| 模型 | 作者 | 点赞 | 下载 | 说明 |
|------|------|------|------|------|
| [**unsloth/Qwen3.8-27B-GGUF**](https://huggingface.co/unsloth/Qwen3.8-27B-GGUF) | unsloth | 2,492 | 5,804,917 | 官方推荐 GGUF 量化版，下载量全网第一（580W+），unsloth 出品保证质量。 |
| [**orcarouter/Qwen3.8-27B-Uncensored-MLX**](https://huggingface.co/orcarouter/Qwen3.8-27B-Uncensored-MLX) | orcarouter | 813 | 18,193 | Apple Silicon 专用 MLX 格式去审查版，通过 abliterated 技术移除安全限制。 |
| [**orcarouter/Qwen3.8-27B-Uncensored-FP8**](https://huggingface.co/orcarouter/Qwen3.8-27B-Uncensored-FP8) | orcarouter | 774 | 107,520 | FP8 精度去审查版，推理更快且显存占用更低。 |
| [**JonathanColetti/Qwen3.8-27B-Uncensored-GGUF**](https://huggingface.co/JonathanColetti/Qwen3.8-27B-Uncensored-GGUF) | JonathanColetti | 560 | 1,126,222 | GGUF 去审查版，带 MTP 支持（Multi-Token Prediction），本地部署热门选择。 |
| [**OBLITERATUS/Qwen3.8-27B-OBLITERATED**](https://huggingface.co/OBLITERATUS/Qwen3.8-27B-OBLITERATED) | OBLITERATUS | 432 | 123,956 | 同时提供 MLX+GGUF+safetensors 三格式的"灭除"版。 |
| [**Qwen/Qwen3.8-27B-FP8**](https://huggingface.co/Qwen/Qwen3.8-27B-FP8) | Qwen | 656 | 1,939,895 | 官方 FP8 量化版，兼顾精度与显存，开源模型量化标杆。 |
| [**huihui-ai/Huihui-Qwen3.8-27B-abliterated-GGUF**](https://huggingface.co/huihui-ai/Huihui-Qwen3.8-27B-abliterated-GGUF) | huihui-ai | 226 | 338,221 | huihui-ai 出品的 abliterated GGUF，社区口碑极佳。 |
| [**unsloth/Qwen3.8-27B-NVFP4**](https://huggingface.co/unsloth/Qwen3.8-27B-NVFP4) | unsloth | 323 | 1,013,917 | 英伟达 NVFP4 精度量化，适用于最新 Hopper/Blackwell GPU。 |
| [**0bserverx/Qwen3.8-27B-Heretic-Abliterated-Uncensored-GGUF**](https://huggingface.co/0bserverx/Qwen3.8-27B-Heretic-Abliterated-Uncensored-GGUF) | 0bserverx | 206 | 421,918 | "Heretic"级去审查版本，移除更多安全层，下载量较高。 |
| [**HauhauCS/Qwen3.8-27B-Uncensored-HauhauCS-Aggressive-MTP-GGUF**](https://huggingface.co/HauhauCS/Qwen3.8-27B-Uncensored-HauhauCS-Aggressive-MTP-GGUF) | HauhauCS | 414 | 357,225 | 激进模式 MTP + GGUF 去审查版，本地推理性能优化。 |
| [**empero-ai/Qwen3.8-27B-Ridge-GGUF**](https://huggingface.co/empero-ai/Qwen3.8-27B-Ridge-GGUF) | empero-ai | 232 | 74,038 | llama.cpp 量化版，基于 Qwen3.5。 |
| [**Blackfrost-AI/Qwen3.8-27B-ABLITERATED-GGUF**](https://huggingface.co/Blackfrost-AI/Qwen3.8-27B-ABLITERATED-GGUF) | Blackfrost-AI | 195 | 197,667 | 又一个 Qwen3.8 ABLITERATED GGUF 社区版，dense 架构。 |
| [**DavidAU/Qwen3.8-27B-Cold-Fusion-GAIN-V1.1-NM-DAU-NEO-MAX-MTP-GGUF**](https://huggingface.co/DavidAU/Qwen3.8-27B-Cold-Fusion-GAIN-V1.1-NM-DAU-NEO-MAX-MTP-GGUF) | DavidAU | 162 | 155,208 | 采用 GAIN Training + COLD-FUSION 技术的 GGUF 合并版，探索模型融合新路径。 |
| [**orcarouter/Qwen3.8-27B-Uncensored-GGUF**](https://huggingface.co/orcarouter/Qwen3.8-27B-Uncensored-GGUF) | orcarouter | 282 | 68,275 | 同 OEM 系列 GGUF 去审查版。 |
| [**huihui-ai/Huihui-Qwen3.8-27B-abliterated**](https://huggingface.co/huihui-ai/Huihui-Qwen3.8-27B-abliterated) | huihui-ai | 225 | 17,521 | 非 GGUF 的 safetensors 格式 abliterated 版。 |

---

## 🌐 生态信号

- **Qwen 生态全面统治**：30 个热门模型中 19 个与 Qwen3.8 相关（63%），从官方旗舰到社区量化、去审查、微调，形成完整的"模型+周边"生态矩阵，这在 Hugging Face 历史上极为罕见。
- **多模态成为标配**：Qwen3.8、Kimi-K3、Muse-Glimmer、MiniMax-H3 均支持图像-文本联合理解/生成，纯文本模型逐渐边缘化。视频生成（LTX-2.5、H3）热度迅猛攀升。
- **"去审查"运动兴起**：近三分之一的上榜模型为 abliterated/uncensored 类型，覆盖 MLX/GGUF/FP8/safetensors 全格式，反映社区对生成自由的强烈需求。
- **量化加速向端侧迁移**：GGUF（llama.cpp）、MLX（Apple Silicon）、NVFP4（英伟达新一代 GPU）三线并进；unsloth 的 GGUF 版下载量已达惊人的 580 万次，远超原版模型。
- **开源+生态 > 参数规模**：DeepSeek-V4-Pro 参数规模大但下载量远低于 Qwen3.8 的量化衍生品，说明"好用、易部署、有生态"比"更大更强"更能驱动社区采纳——开源的胜利愈发明显。

---

## 🔭 值得探索

1. **[Qwen/Qwen3.8-2.4T-A95B](https://huggingface.co/Qwen/Qwen3.8-2.4T-A95B)** — 2.4T 总参数 MoE 模型是当前开源规模的天花板，探索其激活参数仅 95B 时的能力上限，对大模型研究极具意义。

2. **[froggeric/Qwen-Fixed-Chat-Templates](https://huggingface.co/froggeric/Qwen-Fixed-Chat-Templates)** — 以 0 下载量获得 1,364 点赞，说明这是一个直击痛点的工具型仓库（修复 Qwen 3.5 聊天模板缺陷），所有 Qwen3.5 用户都值得关注。

3. **[DavidAU/Qwen3.8-27B-Cold-Fusion-GAIN-V1.1-NM-DAU-NEO-MAX-MTP-GGUF](https://huggingface.co/DavidAU/Qwen3.8-27B-Cold-Fusion-GAIN-V1.1-NM-DAU-NEO-MAX-MTP-GGUF)** — 融合 GAIN Training 与 COLD-FUSION 技术的社区实验性合并模型，代表着模型推理阶段融合的前沿方向，值得跟踪其效果反馈。

---

> 📊 **数据说明**：榜单纯基于周点赞数排序，下载量为历史累计。本周 Qwen3.8 系列生态的爆发式增长表明，在开源模型时代"模型即产品、生态即壁垒"。订阅本日报，每日获取 HF 模型生态最新动态。

---
*本日报由 [agents-radar](https://github.com/kky-wollu/agents-radar) 自动生成。*