# Hugging Face 热门模型日报 2026-08-18

> 数据来源: [Hugging Face Hub](https://huggingface.co/) | 共 30 个模型 | 生成时间: 2026-08-17 22:28 UTC

---

# 🤖 Hugging Face 热门模型日报 — 2026-08-18

## 📌 今日速览

今日 Hugging Face 榜单由 **Qwen 家族** 全面领跑，`Qwen3.8-27B` 以单周 1.07 万赞的绝对优势登顶，其量化和非审查变体密集上榜，生态热度可见一斑。**MiniMax** 视频生成模型 `MiniMax-H3` 凭借 240 万下载量成为社区扩散版和 LoRA 微调的新宠。**DeepSeek-V4** 系列持续发力，Flash 版本以高性价比站稳脚跟。值得关注的是，**Kimi-K3** 以高达 1.08 万赞空降前二，但 H3 视频模型在 Comfy-Org 上已达 1400 万下载，呈现文本与视频双雄争霸的格局。

---

## 🔥 热门模型

### 🧠 语言模型（LLM、对话模型、指令微调）

| 模型 | 作者 | 👍 点赞 | 📥 下载 | 一句话说明 |
|------|------|---------|---------|------------|
| [Qwen3.8-2.4T-A95B](https://huggingface.co/Qwen/Qwen3.8-2.4T-A95B) | Qwen | 1,040 | 9,465 | Qwen 旗舰级 MoE 文本模型，2.4 万亿参数总量激活 950 亿，顶级推理性能 |
| [DeepSeek-V4-Pro-0813](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro-0813) | deepseek-ai | 572 | 25,006 | DeepSeek V4 专业版，面向复杂推理与编码任务，延续高性价比路线 |
| [DeepSeek-V4-Flash-0731](https://huggingface.co/deepseek-ai/DeepSeek-V4-Flash-0731) | deepseek-ai | 3,496 | 1,978,298 | V4 轻量高速版，单周近 200 万下载，兼顾性能与速度的主流选择 |
| [NVIDIA-Nemotron-3.5-Lightning-30B-A3B-NVFP4](https://huggingface.co/nvidia/NVIDIA-Nemotron-3.5-Lightning-30B-A3B-NVFP4) | nvidia | 307 | 231,271 | NVIDIA 30B-A3B MoE 模型，NVFP4 量化，高效推理的代表作 |
| [NVIDIA-Nemotron-3.5-Lightning-30B-A3B-BF16](https://huggingface.co/nvidia/NVIDIA-Nemotron-3.5-Lightning-30B-A3B-BF16) | nvidia | 169 | 69,833 | 上述模型的 BF16 全精度版本，适合追求精度的本地部署场景 |
| [LiquidAI/LFM2.5-2.6B](https://huggingface.co/LiquidAI/LFM2.5-2.6B) | LiquidAI | 653 | 147,270 | 2.6B 高效能液态神经网络语言模型，小参数撬动强表现 |

### 🎨 多模态与生成（图像、视频、音频、文本到X）

| 模型 | 作者 | 👍 点赞 | 📥 下载 | 一句话说明 |
|------|------|---------|---------|------------|
| [Qwen/Qwen3.8-27B](https://huggingface.co/Qwen/Qwen3.8-27B) | Qwen | 10,692 | 415,039 | 最强全能多模态对话模型，支持图像+文本输入，单周万人点赞登顶 |
| [MiniMaxAI/MiniMax-H3](https://huggingface.co/MiniMaxAI/MiniMax-H3) | MiniMaxAI | 4,086 | 2,403,238 | 文本/图像生成视频的旗舰模型，240 万下载验证其行业影响力 |
| [Lightricks/LTX-2.5](https://huggingface.co/Lightricks/LTX-2.5) | Lightricks | 1,101 | 465,529 | 视频生成新版本，支持图像/文本/视频到视频，创作工具链完善 |
| [MiniMaxAI/MiniMax-Music3](https://huggingface.co/MiniMaxAI/MiniMax-Music3) | MiniMaxAI | 900 | 10,375 | 音乐生成专用模型，文本直接生成完整音乐 🎵 |
| [lightx2v/Minimax-h3-Turbo](https://huggingface.co/lightx2v/Minimax-h3-Turbo) | lightx2v | 583 | 264,351 | H3 加速版，兼顾速度与画质，适合实时生成场景 |
| [Gazingstars123/Anima-2.9B](https://huggingface.co/Gazingstars123/Anima-2.9B) | Gazingstars123 | 233 | 23,202 | 动漫风格文生图模型，ComfyUI 单文件，二次元创作者首选 |
| [moonshotai/Kimi-K3](https://huggingface.co/moonshotai/Kimi-K3) | moonshotai | 10,800 | 2,163,953 | Kimi 多模态新作，支持特征提取，1.08 万赞空降榜眼 |
| [larryvrh/MiniMax-H3-Turbo-Lora](https://huggingface.co/larryvrh/MiniMax-H3-Turbo-Lora) | larryvrh | 786 | 0 | 新发布的 H3 Turbo LoRA，支持文字+音频生成视频 |
| [fal/MiniMax-H3-Realism-People-LoRA](https://huggingface.co/fal/MiniMax-H3-Realism-People-LoRA) | fal | 243 | 18,562 | 写实人物风格 LoRA，专为 H3 视频生成优化 |
| [LiquidAI/LFM2.5-VL-3B](https://huggingface.co/LiquidAI/LFM2.5-VL-3B) | LiquidAI | 162 | 6,816 | 液态神经网络视觉语言模型，3B 小参数多模态新锐 |

### 🔧 专用模型（代码、数学、医疗、嵌入等）

| 模型 | 作者 | 👍 点赞 | 📥 下载 | 一句话说明 |
|------|------|---------|---------|------------|
| [inclusionAI/Ling-3.0-tiny](https://huggingface.co/inclusionAI/Ling-3.0-tiny) | inclusionAI | 301 | 6,266 | 百灵混合架构小模型，MIT 协议，面向美国地区服务 |
| [dots-studio/dots3-note-prev](https://huggingface.co/dots-studio/dots3-note-prev) | dots-studio | 205 | 633 | 笔记转录专用多模态模型，dot3 命名系列第三版 |
| [meta-models/Muse-Glimmer-30B](https://huggingface.co/meta-models/Muse-Glimmer-30B) | meta-models | 1,660 | 334,099 | Meta 30B 多模态模型，延续 Muse 全家桶生态，热度持续升温 |

### 📦 微调与量化（社区微调、GGUF、AWQ）

| 模型 | 作者 | 👍 点赞 | 📥 下载 | 一句话说明 |
|------|------|---------|---------|------------|
| [unsloth/Qwen3.8-27B-GGUF](https://huggingface.co/unsloth/Qwen3.8-27B-GGUF) | unsloth | 1,622 | 2,727,609 | 顶级量化版本，270 万下载，本地部署 Qwen3.8 的事实标准 |
| [orcarouter/Qwen3.8-27B-Uncensored-FP8](https://huggingface.co/orcarouter/Qwen3.8-27B-Uncensored-FP8) | orcarouter | 428 | 15,812 | Abliterated 去审查版，解锁模型全能力，争议与热度并存 |
| [JonathanColetti/Qwen3.8-27B-Uncensored-GGUF](https://huggingface.co/JonathanColetti/Qwen3.8-27B-Uncensored-GGUF) | JonathanColetti | 295 | 357,701 | 社区非审查 GGUF 版，支持 MTP 加速，下载量可观 |
| [unsloth/Qwen3.8-27B-NVFP4](https://huggingface.co/unsloth/Qwen3.8-27B-NVFP4) | unsloth | 236 | 378,177 | NVIDIA 格式量化版，针对 Hopper/Blackwell 架构优化 |
| [Qwen/Qwen3.8-27B-FP8](https://huggingface.co/Qwen/Qwen3.8-27B-FP8) | Qwen | 526 | 495,646 | 官方 FP8 量化版，精度与性能的官方平衡方案 |
| [Qwen/Qwen3.8-2.4T-A95B-FP8](https://huggingface.co/Qwen/Qwen3.8-2.4T-A95B-FP8) | Qwen | 219 | 12,295 | 旗舰 MoE 的 FP8 量化版，降低超大规模模型使用门槛 |
| [unsloth/Muse-Glimmer-30B-GGUF](https://huggingface.co/unsloth/Muse-Glimmer-30B-GGUF) | unsloth | 470 | 755,125 | Meta Muse 模型 GGUF 版，75 万下载，本地多模态必选 |
| [Comfy-Org/MiniMax-H3](https://huggingface.co/Comfy-Org/MiniMax-H3) | Comfy-Org | 1,402 | 14,015,769 | ComfyUI 单文件版，1400 万次下载，视频生成新标杆 |
| [Comfy-Org/MiniMax-Music-3](https://huggingface.co/Comfy-Org/MiniMax-Music-3) | Comfy-Org | 166 | 256,988 | 音乐生成 ComfyUI 版，工作流集成友好 |
| [DavidAU/Qwen3.6-27B-Fable-Fusion-711-Uncensored-Heretic-NM-DAU-NEO-MAX-MTP-GGUF](https://huggingface.co/DavidAU/Qwen3.6-27B-Fable-Fusion-711-Uncensored-Heretic-NM-DAU-NEO-MAX-MTP-GGUF) | DavidAU | 2,117 | 3,033,928 | 社区魔改极致版，集非审查、多模型融合于一体，300 万下载 |
| [froggeric/Qwen-Fixed-Chat-Templates](https://huggingface.co/froggeric/Qwen-Fixed-Chat-Templates) | froggeric | 1,206 | 0 | 修复 Qwen 对话模板的 Jinja 插件，开发者福音 |

---

## 🌐 生态信号

**Qwen 家族一家独大**：从原版、官方量化到社区魔改，Qwen3.8 系列霸榜 10 席，生态广度无人能及，官方开放权重策略已形成完整生态链。

**视频生成竞争白热化**：MiniMax-H3 系列（原版+Turbo+LoRA+ComfyUI）合计超过 1700 万下载，Lightricks、LTX 紧随其后，视频生成进入应用爆发期。

**量化与微调成为标配**：GGUF、FP8、NVFP4 多路线并行，Unsloth 等工具链深度绑定头部模型；非审查（Uncensored）微调版本持续走红，反映社区对模型边界探索的持续兴趣。

**去中心化趋势明显**：开放权重模型全面开花，社区已具备"官方发布 → 量化 → 微调 → 工作流集成"的完整生产线。

---

## 💡 值得探索

1. **[Qwen/Qwen3.8-27B](https://huggingface.co/Qwen/Qwen3.8-27B)** — 当前社区热度最高的全能型多模态模型，单周破万赞证明了其综合实力。无论是研究前沿能力还是直接应用，它都是不可错过的首选。

2. **[Comfy-Org/MiniMax-H3](https://huggingface.co/Comfy-Org/MiniMax-H3)** — 1400 万次下载的视频生成模型新标杆，单文件即插即用。对于想体验或研究 SOTA 视频生成的开发者，这是最高效的入口。

3. **[moonshotai/Kimi-K3](https://huggingface.co/moonshotai/Kimi-K3)** — 1.08 万赞的黑马选手，定位独特（特征提取+多模态），可能代表 Kimi 拓展模型应用边界的新方向，值得深入研究其技术亮点。

---
*本日报由 [agents-radar](https://github.com/kky-wollu/agents-radar) 自动生成。*