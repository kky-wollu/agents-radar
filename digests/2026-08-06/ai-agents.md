# OpenClaw 生态日报 2026-08-06

> Issues: 500 | PRs: 500 | 覆盖项目: 13 个 | 生成时间: 2026-08-05 23:05 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [NanoBot](https://github.com/HKUDS/nanobot)
- [Hermes Agent](https://github.com/nousresearch/hermes-agent)
- [PicoClaw](https://github.com/sipeed/picoclaw)
- [NanoClaw](https://github.com/qwibitai/nanoclaw)
- [NullClaw](https://github.com/nullclaw/nullclaw)
- [IronClaw](https://github.com/nearai/ironclaw)
- [LobsterAI](https://github.com/netease-youdao/LobsterAI)
- [TinyClaw](https://github.com/TinyAGI/tinyagi)
- [Moltis](https://github.com/moltis-org/moltis)
- [CoPaw](https://github.com/agentscope-ai/CoPaw)
- [ZeptoClaw](https://github.com/qhkm/zeptoclaw)
- [ZeroClaw](https://github.com/zeroclaw-labs/zeroclaw)

---

## OpenClaw 项目深度报告

好的，这是 2026-08-06 的 OpenClaw 项目动态日报。

---

## OpenClaw 项目动态日报 (2026-08-06)

### 1. 今日速览

项目今日活跃度极高，24小时内Issue和PR更新均达到500条的上限，显示出非常活跃的社区和开发节奏。当前项目的主要精力集中在解决一批顽固的、影响会话状态和消息传递的P1级Bug（尤其是重复消息、会话挂起和状态丢失问题），以及由 `clawsweeper[bot]` 自动生成的修复PR。尽管没有新版本发布，但大量针对Slack、WhatsApp等渠道的修复和功能PR处于待合并或等待作者响应状态，表明项目正处于密集的缺陷修复和稳定性加固阶段，同时也在积极推动新功能（如WhatsApp投票支持）。值得注意的是，多个高优先级问题（如P0级的数据丢失、迁移失败）在近日被关闭，说明修复措施正在生效。

### 2. 版本发布

无新版本发布。

### 3. 项目进展

今日无直接合并的PR，但修复工作有显著推进，尤其是在数据安全和高优缺陷上：

- **修复P0级数据丢失风险**：PR #119088（[链接](https://github.com/openclaw/openclaw/pull/119088)）和 #119090（[链接](https://github.com/openclaw/openclaw/issues/119090)）均已被关闭，表明这两个导致`attachments.ttlHours`误删聊天历史媒体文件和清理程序在会话存储不可读时永久删除媒体的问题已得到解决。这是今日最重要的进展。
- **解决关键迁移阻断**：P0级Bug #119263（[链接](https://github.com/openclaw/openclaw/issues/119263)）——Agent数据库从v14迁移至v15/v16失败导致网关无法启动的问题已被关闭，意味着该阻塞性问题已解决。

### 4. 社区热点

今日讨论最激烈的问题集中在**会话状态丢失**和**消息传递可靠性**两个核心痛点上：

- **#116201** (评论:58) [Realtime voice work can retain unbounded provider and consult state](https://github.com/openclaw/openclaw/issues/116201) 实时语音会话的资源管理问题成为今日最高热度Issue，但赞数极少，说明用户更关注其带来的稳定性风险而非功能本身。
- **#44925** (评论:25, 👍2) [[Bug]: Subagent completion silently lost](https://github.com/openclaw/openclaw/issues/44925) 子代理任务在超时后静默丢失且无重试或通知，反映了用户对后台任务可靠性的高度关注。
- **#118846** (评论:19) [Gateway main thread saturated from boot by plugin-metadata snapshot](https://github.com/openclaw/openclaw/issues/118846) 网关主线程从启动起就被占满导致本地RPC断连，引发了关于性能瓶颈和启动流程的讨论。
- **#86519** (评论:14, 👍1) [[Bug]: Agent repeats identical replies 2-10x on Telegram](https://github.com/openclaw/openclaw/issues/86519) 这是一个影响广泛且长期未解决的回归问题，用户对重复回复的困扰依然强烈。

**背后诉求**：社区最迫切的需求是**稳定性和可靠性**，尤其是确保长时间运行的任务（如语音、子代理）不会静默失败，以及核心通信渠道（如Telegram）不会出现消息错乱。

### 5. Bug 与稳定性

今日报告的Bug主要集中在稳定性、会话状态和消息丢失方面，按严重程度排列：

**P0 - 严重（已解决）**
- [Bug]: Agent DB v14->v15 migration fails ... (已解决) [#119263](https://github.com/openclaw/openclaw/issues/119263)
- [Bug]: managed media cleanup fails open ... (已解决) [#119090](https://github.com/openclaw/openclaw/issues/119090)
- [Bug]: attachments.ttlHours sweeps media/outgoing ... (已解决) [#119088](https://github.com/openclaw/openclaw/issues/119088)

**P1 - 高（修复中或待响应）**
- [Bug]: Agent repeats identical replies 2-10x on Telegram (回归, 无新修复PR) [#86519](https://github.com/openclaw/openclaw/issues/86519)
- [Bug]: Subagent completion silently lost (无新修复PR) [#44925](https://github.com/openclaw/openclaw/issues/44925)
- Gateway main thread saturated from boot ... (已关闭，状态未知) [#118846](https://github.com/openclaw/openclaw/issues/118846)
- Realtime voice work can retain unbounded provider and consult state (无新修复PR) [#116201](https://github.com/openclaw/openclaw/issues/116201)
- [Bug]: Loop detection blocks exec but does not terminate stuck agent run (有打开的修复PR) [#106231](https://github.com/openclaw/openclaw/issues/106231)
- [Bug]: Large SQLite transcript cleanup blocks the gateway event loop (无新修复PR) [#112423](https://github.com/openclaw/openclaw/issues/112423)
- fix(slack): require confirmed thread placement for terminal receipts (等待作者) [#119737](https://github.com/openclaw/openclaw/pull/119737)

**P2 - 中**
- [Bug]: 看起来有人把工作路径hardcode进代码里 (无新修复PR) [#51429](https://github.com/openclaw/openclaw/issues/51429)
- Session context bloat: bootstrap files re-injected every turn (无新修复PR) [#67419](https://github.com/openclaw/openclaw/issues/67419)
- [Bug]: qqbot 消息重复发送 (回归, 无新修复PR) [#77306](https://github.com/openclaw/openclaw/issues/77306)

**今日新增值得关注的Bug**
- [Bug]: chat delta throttle has no trailing flush ... (P2) [#119557](https://github.com/openclaw/openclaw/issues/119557) - 新提交的节流器逻辑缺陷，可能导致消息延迟展示。

### 6. 功能请求与路线图信号

- **WhatsApp 投票功能**：PR #119256（[链接](https://github.com/openclaw/openclaw/pull/119256)）为 `@openclaw/whatsapp` 添加了 `poll_vote_received` hook，以支持读取投票结果。这是一个明确的新功能，有对应的Issue #119254。
- **控制台UI增强**：PR #113271（[链接](https://github.com/openclaw/openclaw/pull/113271)）为Control UI的聊天输入框增加了拖拽调整大小的功能，旨在改善长消息撰写体验。
- **Discord消息编辑/删除响应**：Issue #53654（[链接](https://github.com/openclaw/openclaw/issues/53654)）请求支持Discord的 `messageUpdate` 和 `messageDelete` 事件，以实现编辑后重新处理和删除后取消操作。该需求获得3个👍，是较受欢迎的功能请求。

**路线图信号**：`clawsweeper` 自动修复机器人（如PR #119737和#119735）正在被大量使用，表明项目正尝试通过自动化工具加速修复流程。

### 7. 用户反馈摘要

- **对重复/丢失消息的强烈不满**：多个Issue（如 #86519, #44925）反映了用户对消息重复发送、子代理任务静默丢失的严重不满，这些问题严重影响了核心体验和信任度。
- **对本地/专用模型支持的热情**：Issue #106779（[链接](https://github.com/openclaw/openclaw/issues/106779)）中，用户详细对比了ChatGPT和本地llama.cpp提供商的表现，显示出社区对本地模型支持的强烈兴趣，但同时也面临配置和兼容性挑战。
- **对透明度缺失的抱怨**：Issue #106786（[链接](https://github.com/openclaw/openclaw/issues/106786)）指出当模型被提供商拒绝时，系统会静默地使用备用模型，用户对此毫不知情。这反映出用户对系统行为透明度的需求。
- **自动化修复的双刃剑**：虽然 `clawsweeper` 机器人能快速生成修复PR，但其质量仍需人工审核。例如，PR #119057（[链接](https://github.com/openclaw/openclaw/pull/119057)）被标记为“需要作者说明”，表明部分自动生成的修复并未完全满足要求。

### 8. 待处理积压

以下问题长期未解决（多为3月份或更早报告，且状态仍为打开，近期无修复PR），建议维护者关注：

- **[P0] Persistent file-based provider cooldown blocks user for hours after billing recovery** [#70903](https://github.com/openclaw/openclaw/issues/70903) (04-24报告) - 付费恢复后仍被长期封锁，严重影响用户体验。
- **[P1] Umbrella: duplicate transcript, replay, and context assembly across channels** [#69208](https://github.com/openclaw/openclaw/issues/69208) (04-20报告) - 这是一个跨渠道的元问题，可能涵盖多个重复消息Bug的根源。
- **[P1] Auto-update can leave running gateway with stale hashed bundle imports** [#85844](https://github.com/openclaw/openclaw/issues/85844) (05-23报告) - 自动更新可能导致运行中的网关引用旧代码，存在稳定性隐患。
- **[P1] Cron jobs stall during AI model calls** [#91892](https://github.com/openclaw/openclaw/issues/91892) (06-10报告) - 定时任务在模型调用时挂起，功能基本不可用。
- **[Feature] --agent flag for TUI to select which agent handles the session** [#8892](https://github.com/openclaw/openclaw/issues/8892) (02-04报告) - 呼声较高的功能请求，已获得3个👍。

**提醒**：`clawsweeper[bot]` 生成的 PR #119737 和 #119735 均已创建但状态为“等待作者”，这通常意味着维护者需要介入审核或提供进一步信息。

---

## 横向生态对比

# 个人 AI 助手开源生态横向对比分析报告

**报告日期：2026-08-06** | **数据窗口：2026-08-05 至 2026-08-06**


## 1. 生态全景

当前个人 AI 助手/自主智能体开源生态正处于 **"密集修复 + 架构演进"双轨并行**的关键阶段。以 OpenClaw 为龙头的项目群落（含其派生生态 NanoBot、PicoClaw、NanoClaw、NullClaw、CoPaw、LobsterAI 等）在 24 小时内合计产生超过 **180 条 Issue 更新与 220 条 PR 更新**，但合并率普遍偏低，多项目出现 PR 积压与 review 带宽瓶颈。生态核心矛盾集中在三类共性问题上：**重复消息/会话状态丢失**（OpenClaw、NanoBot、Hermes、CoPaw 均有报告）、**MCP 工具的错误处理语义不完整**（NanoBot、CoPaw、ZeroClaw）、**多通道投递与配置一致性**（Telegram/WhatsApp/Slack/微信均有相关 Bug）。与此同时，多租户架构（Hermes #34352）、LLM 多模型回退（CoPaw、PicoClaw）、配置即代码（IronClaw #3036）、长期自治能力（Hermes #79686、ZeroClaw Goal mode）等前瞻性议题正在社区层面形成明确的需求共识。


## 2. 各项目活跃度对比

| 项目 | Issue 更新 | PR 更新 | 合并/关闭 PR | Release | 健康度评估 | 阶段判断 |
|---|---|---|---|---|---|---|
| **OpenClaw** | ~500（达上限） | ~500（达上限） | 0（今日无合并） | 无 | ★★★☆☆ | 高活跃但陷入 P1 Bug 修复泥潭 |
| **NanoBot** | 4 新开/0 关闭 | 16（8 合并/关闭） | 8 | 无 | ★★★★★ | 功能迭代密集，工程质量高 |
| **Hermes Agent** | 50（44 活跃/6 关闭） | 50（10 合并/关闭） | 10 | 无 | ★★★★☆ | 数据安全修复及时，PR 积压明显 |
| **PicoClaw** | 0 | 3（0 合并） | 0 | 无 | ★★☆☆☆ | 低活跃，PR 长期搁置 |
| **NanoClaw** | 2（活跃） | 10（1 合并） | 1 | 无 | ★★★☆☆ | 功能开发活跃，Issue 响应慢 |
| **NullClaw** | 0 | 2（0 合并） | 0 | 无 | ★★★☆☆ | 修复驱动收敛期，等待合并 |
| **IronClaw** | 43 | 50 | 10+ | v1.1.0-rc.1（8/3） | ★★★★☆ | 高速迭代，bug_bash 反馈集中 |
| **LobsterAI** | 3（全新开） | 13（12 合并/关闭） | 12 | 2026.8.5（8/5） | ★★★★☆ | 稳定推进 + 精细化迭代 |
| **CoPaw** | 23（17 活跃/6 关闭） | 50（21 合并/关闭） | 21 | 无（v2.1.0b1） | ★★★★☆ | 高活跃，P0 回归需关注 |
| **ZeroClaw** | 39（活跃） | 49（1 合并/关闭） | 1 | 无 | ★★★☆☆ | 高讨论低合并，RFC 积压 |
| **TinyClaw** | 0 | 0 | 0 | 无 | — | 无活动 |
| **Moltis** | 0 | 0 | 0 | 无 | — | 无活动 |
| **ZeptoClaw** | 0 | 0 | 0 | 无 | — | 无活动 |

> **注**：合并率 = 合并/关闭 PR ÷ 总 PR 更新。OpenClaw 因 Issue/PR 均达到 500 上限，实际活跃度可能更高。


## 3. OpenClaw 在生态中的定位

### 核心参照地位确立

OpenClaw 作为生态核心参照（github.com/openclaw/openclaw）的地位进一步巩固，主要体现为：

- **社区规模断层领先**：24 小时 Issue/PR 更新均达到 500 条上限，远超第二名 Hermes/CoPaw/IronClaw 的约 50 条。评论量最高的 Issue 达 58 条。社区基数不在一个量级。
- **派生生态繁荣**：LobsterAI（网易有道）、NanoClaw、CoPaw 等多个项目明确基于 OpenClaw 运行时构建，形成事实上的"OpenClaw runtime 兼容层"标准。
- **稳定性问题同样被放大**：重复消息（#86519 评论 14+）、子代理静默丢失（#44925 评论 25+）等核心体验问题，正因为用户基数大而被高度放大——这是龙头必须承受的"规模之痛"。

### 技术路线差异

| 维度 | OpenClaw | Hermes | IronClaw | CoPaw |
|---|---|---|---|---|
| **核心语言/运行时** | TypeScript/Node.js | Python | Rust + Python | Python（基于 OpenClaw） |
| **架构风格** | 网关 + 适配器 + 插件 | CLI 优先 + 桌面端 | Reborn 模块化重构 | OpenClaw 兼容 + 企业增强 |
| **渠道覆盖** | Telegram/Slack/WhatsApp/QQ 等全渠道 | Telegram/微信/QQ/Discord | Slack/Telegram/Web | 微信/钉钉/Matrix/OneBot |
| **核心优势** | 生态规模、渠道广度 | 本地模型支持、CLI 深度 | Rust 性能、配置即代码 | 中文社区、企业场景 |
| **关键短板** | 重复消息、状态丢失悬而未决 | 桌面端 UI 同步、macOS 兼容 | Agent 幻觉、MCP 验证缺失 | MCP 超时配置、桌面环境隔离 |


## 4. 共同关注的技术方向

### 4.1 会话状态保持与消息可靠投递（涉及：OpenClaw、NanoBot、Hermes、CoPaw、NullClaw）

- **重复消息/静默丢失**：OpenClaw #86519（Telegram 重复 2-10 次）、#44925（子代理静默丢失）、NanoBot #5256（/goal 重复回复）、CoPaw #6696（微信 context_token 消耗）、NullClaw #972（轮询线程静默失效）呈现跨项目、跨渠道的普遍性。这不仅是 Bug，更是**消息投递语义缺少统一事务保证**的架构级缺陷。

- **会话状态持久化**：OpenClaw #116201（实时语音状态无限膨胀）、Hermes #79391（中断压缩永久删除历史）、CoPaw #6726（长会话工具调用后 400）共同指向会话生命周期管理的复杂性。

### 4.2 MCP 集成深度与错误契约（涉及：NanoBot、CoPaw、ZeroClaw、IronClaw）

| 项目 | 问题 | 核心诉求 |
|---|---|---|
| NanoBot | #5237 MCP 业务错误被吞，LLM 空等超时 | 框架级修复，区分业务失败与成功 |
| CoPaw | #6724 MCP 工具调用无超时上限 | 可配置 timeout 字段 |
| IronClaw | #7248 无效 MCP 端点被接受；#7251 Agent 猜测认证类型 | 端点验证 + 真实错误上报 |
| ZeroClaw | #8642 MCP 工具 schema 克隆导致内存无限增长 | 内存边界控制 |

> **生态级判断**：MCP（Model Context Protocol）已成为事实上的工具集成标准，但**错误语义、超时控制、认证验证**三个基础契约仍未统一。这是当前生态最集中的共性技术债。

### 4.3 多模型路由与降级策略（涉及：CoPaw、PicoClaw、Hermes、OpenClaw）

- CoPaw 已合并 #5597/#5598（LLM Fallback 前后端落地），提供代理级/全局级回退配置
- PicoClaw #3200 正在推进可配置默认模型回退链
- Hermes #5254 LM-Studio 工具调用重复执行（4 个月未修复）
- 用户对本地模型支持与成本优化需求强烈（OpenClaw #106779、ZeroClaw #9631 缓存降本）

### 4.4 安全加固与权限控制（涉及：ZeroClaw、IronClaw、NanoBot、Hermes）

- ZeroClaw：SSRF 防护（#8826）、Git shell 策略（#9678）、高风险命令确认分级（#7155，三版迭代）
- NanoBot：#5258 含凭据 URL 转发至远程 reader（P1 安全漏洞）
- IronClaw：#7249 Slack DM 执行结果泄露到 Telegram（跨渠道信息泄露）
- Hermes：#34352 多租户隔离（Memory 操作绕过 hook）

### 4.5 长期自治与目标驱动（涉及：ZeroClaw、Hermes、OpenClaw）

- ZeroClaw #8303 Goal mode RFC（18 评论，最高热度）：多轮对话中有界目标追求
- Hermes #79686 长期自治缺口跟踪器：Retained subagents、Goal gates、Session heartbeats
- OpenClaw 社区对子代理可靠性的集中关注（#44925 评论 25+）


## 5. 差异化定位分析

### 功能侧重与目标用户

| 项目 | 目标用户 | 核心场景 | 差异化特征 |
|---|---|---|---|
| **OpenClaw** | 开发者/早期采用者（全球） | 多渠道个人助手、实验性自治 | 生态最大、渠道最广、插件丰富 |
| **Hermes** | 技术型用户/CLI 爱好者（欧美为主） | 本地模型、长时自治工作流 | CLI 深度、本地 LLM 优先、macOS 关注 |
| **IronClaw** | 企业团队/中型组织 | 团队协作、Slack 原生、配置管理 | Rust 性能、Reborn 架构、配置即代码规划 |
| **CoPaw** | 中文用户/企业（亚洲为主） | 微信/钉钉集成、多模型路由 | 中文社区活跃、LLM Fallback 已落地 |
| **LobsterAI** | 中文桌面用户 | 桌面端体验、企业账号隔离 | 网易背景、活动运营、桌面生命周期管理 |
| **NanoBot** | 开发者/自托管用户 | WebUI 丰富、MCP 集成 | Temporary Chat、项目终端、Mattermost 深度 |
| **ZeroClaw** | 安全敏感型用户 | WASM 插件、多 Agent 编排 | Rust 安全、插件隔离、RFC 驱动演进 |
| **PicoClaw** | OpenClaw 的嵌入式变体 | 简单部署、模型回退 | 轻量、配置灵活性（当前 PR 长期搁置） |
| **NanoClaw** | OpenClaw 容器化用户 | 容器隔离、Skill 扩展 | agent runner 隔离、MCP 环境透传 |
| **NullClaw** | 长时间运行部署用户 | 稳定性优先、无人值守 | 通道线程健康管理（修复驱动型） |

### 技术架构关键差异

- **语言/运行时**：TypeScript（OpenClaw 系） vs Python（Hermes/NanoBot/CoPaw） vs Rust（IronClaw/ZeroClaw）——Rust 系在性能与安全上具有天然优势，TypeScript 系在生态扩展上领先。
- **部署形态**：桌面端（Hermes、LobsterAI、CoPaw） vs Web 网关（OpenClaw、IronClaw） vs CLI 优先（Hermes） vs 容器化（NanoClaw）。
- **扩展机制**：插件市场（OpenClaw clawsweeper 自动化）、Skill 体系（NanoClaw、IronClaw）、MCP 统一（NanoBot、CoPaw、ZeroClaw）、WASM 插件（ZeroClaw）。


## 6. 社区热度与成熟度

### 快速迭代梯队（功能推进 + 合并率健康）

| 项目 | 合并率 | 特征 |
|---|---|---|
| **NanoBot** | 50%（8/16） | 工程效率标杆，Issue→Fix 闭环速度快（#5256→#5257 同日） |
| **CoPaw** | 42%（21/50） | 中文社区活跃，LLM Fallback 等核心特性快速落地 |
| **LobsterAI** | 92%（12/13） | 合并效率极高，版本频繁，稳定性修复精准 |
| **IronClaw** | 20%+（10/50） | 高速迭代 + bug_bash 反馈驱动，但合并率偏低 |

### 质量巩固梯队（侧重稳定性/架构而非新功能）

| 项目 | 合并率 | 特征 |
|---|---|---|
| **OpenClaw** | 0%（今日无合并） | 活跃度极高但在修复泥潭中挣扎，P0 修复靠 sweep 机器人推进 |
| **Hermes** | 20%（10/50） | 数据安全修复及时，但 40 条 PR 积压、老 PR 四个月未合并 |
| **ZeroClaw** | 2%（1/49） | 讨论积极但合并停滞，RFC 决策队列积压严重 |

### 低活跃/停滞梯队

| 项目 | 状态 |
|---|---|
| **PicoClaw** | PR #1951 搁置 135 天，#3200 搁置 36 天，无新 Issue |
| **NullClaw** | 仅 2 个关键修复 PR 等待合并，无 Issue 流动 |
| **TinyClaw / Moltis / ZeptoClaw** | 24 小时无活动，可能处于休眠或维护期 |


## 7. 值得关注的趋势信号

### 7.1 AI 助手从"对话工具"走向"自治工作主体"

ZeroClaw Goal mode（#8303）、Hermes 自治缺口追踪（#79686）、OpenClaw 对子代理可靠性的集中讨论，以及多项目对"长时间半自治工作流"的聚焦（Hermes #68927/#53839、CoPaw #6436），共同昭示：**生态正在从"单轮对话响应"向"多轮自主任务执行"跃迁**。开发者应关注短期内的关键瓶颈——**任务状态持久化与失败恢复**——这将是下一代 AI 助手的分水岭能力。

### 7.2 安全已成为 AI 助手采用的硬门槛

ZeroClaw 的 SSRF/Git shell/命令确认三线并发、NanoBot 的凭据泄露 PR、IronClaw 的跨渠道信息泄露，以及 Hermes 的多租户隔离提案——安全议题从"最佳实践"变为"必需条件"。对开发者而言，**将安全（输入验证、网络边界、凭据管理、审计日志）内建到 agent 设计原语**中，而非事后打补丁，是当前最值得投入的技术债。

### 7.3 MCP 正在成为"工具集成的事实标准"，但契约远未成熟

从 NanoBot 的 MCP 错误语义讨论、CoPaw 的超时配置请求，到 ZeroClaw 的内存泄漏、IronClaw 的端点验证缺失——MCP 的**错误契约、超时控制、资源边界**三个基础协议亟需标准化。对 MCP server 开发者和 agent 框架开发者而言，谁能率先定义并实现成熟的错误/超时/资源管理语义，谁就能在下一阶段生态中占据标准制定者的位置。

### 7.4 "配置即代码"与多租户需求的出现，标志着产品化拐点

IronClaw 的 Config-as-Code Epic（#3036，最高赞）、Hermes 多租户方案（#34352）、LobsterAI 企业账号隔离，以及 CoPaw 的 LLM Fallback 配置 UI——这些信号表明 AI 助手正在从个人开发者玩具，迈向**组织级产品形态**。多租户、审计、配置版本化、权限分级的出现，是生态从"hackable tool"走向"enterprise-ready platform"的典型标志。

### 7.5 自动修复机器人的双刃剑效应

OpenClaw 的 `clawsweeper[bot]` 大量生成修复 PR 提高了修复效率，但也出现 PR #119057 被标记"需要作者说明"、PR #119737/#119735 等待作者响应的情况。zeroClaw、Hermes 等也出现了 `sweeper:risk-*` 标签。**自动化工具在加速修复的同时，正在改变开源维护的协作模式**——维护者的核心角色从"写代码"向"审代码/定方向"转变，这对社区治理效率提出了新的考验。

### 7.6 中文社区的力量不可忽视

CoPaw 约 40% 的 Issue 为中文反馈、LobsterAI 为中文桌面用户深度定制、NanoBot 也有中文用户活跃。中文反馈普遍质量高（包含复现步骤、截图、代码定位），且企业场景特征明显（微信/钉钉集成、超大群支持）。对于面向全球市场的项目，**中文用户是企业级应用的先行指标**，满足中文社区需求是走向组织级市场的重要路径。


## 附录：对技术决策者的建议

| 关注维度 | 建议 |
|---|---|
| **选型参考** | 若需最强生态 → OpenClaw；若需本地模型 + CLI 深度 → Hermes；若需企业级安全 → IronClaw/ZeroClaw；若需中文企业场景 → CoPaw/LobsterAI；若需工程效率标杆 → NanoBot |
| **投入方向** | MCP 错误语义标准化、会话状态持久化框架、消息投递事务保证——三大共性技术债是当前生态的"卡脖子"问题 |
| **风险提示** | OpenClaw 的重复消息/状态丢失问题若久拖不决，可能引发用户向 Hermes/CoPaw 等替代方案迁移；多项目 PR 积压问题若不解决，将抑制社区贡献者积极性 |
| **值得借鉴** | NanoBot 的 Issue→Fix 闭环速度（同日修复）、CoPaw 的 LLM Fallback 实现模式、LobsterAI 的稳定性优先迭代节奏 |

---

*报告结束 · 数据基于各项目公开 GitHub 仓库 2026-08-05 至 2026-08-06 窗口*

---

## 同赛道项目详细报告

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot 项目动态日报 — 2026-08-06

*数据来源：HKUDS/nanobot GitHub 仓库；统计窗口：2026-08-05 至 2026-08-06（过去 24 小时）*


## 1. 今日速览

NanoBot 过去 24 小时整体活跃度较高，PR 流量显著放大（16 条，合并/关闭 8 条），WebUI 重构、Temporary Chat 模式、Mattermost 线程策略等多项功能密集落地，同时有 3 个 P1/P2 级 Bug 修复 PR 被合并或处于审查中。Issues 侧新增 4 条（新开 4，关闭 0），其中 #5256 `/goal` 消息重复回复问题与 #5257 修复 PR 同日出现，社区问题响应闭环速度优秀。无新版本发布，处于积累期。项目整体健康度良好，工程效率与社区反馈节奏均在正常偏快水平。


## 2. 版本发布

当前无新版本发布。项目处于功能积累阶段，近期合并的 PR 预计将在下一版本中集中释放。


## 3. 项目进展

今日合并/关闭 8 个 PR，关键进展如下：

**功能新增/推进**
- **[#5234]** feat(agent): 集成 mst-python 作为 metasearch 搜索提供商（P1，已合并）— [PR #5234](https://github.com/HKUDS/nanobot/pull/5234)
  新增 Meta-Search Tool 聚合 DuckDuckGo/Google/Brave/Bing 等搜索引擎结果，并通过 RRF 融合排序，覆盖度优于单一引擎。
- **[#5233]** feat(mattermost): 为线程增加独立 group policy 配置（P2，已合并）— [PR #5233](https://github.com/HKUDS/nanobot/pull/5233)
  跟进 #4459 频道支持，新增 `groupPolicyInThread` 配置字段，可在线程与主频道设置不同的 @ 提及要求，并在 WebUI 中暴露。
- **[#5249]** refactor(webui): 视觉一致性重构（P2，已合并）— [PR #5249](https://github.com/HKUDS/nanobot/pull/5249)
  菜单/弹窗/面板统一双层高度体系，Skills 与 Channels 布局扁平化，移除持久化消息的重播动画。
- **[#5250]** fix(webui): 修复活动面板边缘裁剪（P2，已合并）— [PR #5250](https://github.com/HKUDS/nanobot/pull/5250)
  为裁剪的代理活动面板添加方向感知的边缘羽化效果。

**Bug 修复**
- **[#5238]** refactor(session): 移除请求级会话访问授权（P1，已合并）— [PR #5238](https://github.com/HKUDS/nanobot/pull/5238)
  回退 #5211 引入的 `Tool.available()` 请求级权限层，恢复 `Tool.enabled()` 作为唯一构建期开关，同时保留会话工具的读取能力，消除了回归问题。
- **[#5203]** fix(whatsapp): 出站媒体内容检测（P2，已合并）— [PR #5203](https://github.com/HKUDS/nanobot/pull/5203)
  从文件内容而非扩展名检测 WhatsApp 出站媒体类型，修正 M4A/AAC 别名识别，并将不支持/不明确音频以文档形式发送。
- **[#5254]** feat: 添加提供商原生请求开关（P2，已合并）— [PR #5254](https://github.com/HKUDS/nanobot/pull/5254)
  WebUI 新增开关直接编辑原始提供商请求字段：OpenAI Codex Fast 模式、OpenAI/DeepSeek 网络搜索、xAI Grok X Search——在 24 小时内完成从提交到合并。

**小结**：今日合并 PR 覆盖面广，WebUI 体验（视觉一致性、边缘羽化）与通道能力（WhatsApp 媒体、Mattermost 线程策略、MST 搜索）双线推进，同时完成 3 个 P1 级修复（#5238、#5234、#5254 均含测试），项目整体向前迈进了一个功能密集迭代。


## 4. 社区热点

今日讨论最活跃的条目：

**Issue #5237 — MCP 工具业务错误被吞（评论 2，活跃讨论中）**
链接：[Issue #5237](https://github.com/HKUDS/nanobot/issues/5237)
当 MCP server 在 `CallToolResult.content` 内返回业务错误（如 `{"code": 404, "msg": "data not exist"}`）且 `isError = False` 时，nanobot 将其视为成功调用。LLM 无法感知失败，只能空等到 `tool_timeout` 触发，且超时后仍无法识别真实原因。社区对此关注度较高，涉及 MCP 集成中错误传递的深层次问题——契约层面的设计缺陷，而非单个工具的问题，可能需要框架级修复。

**Issue #5149 — WhatsApp 无法发送音频（评论 4，长期未解决）**
链接：[Issue #5149](https://github.com/HKUDS/nanobot/issues/5149)
用户报告 nanobot 在 WhatsApp 上可以接收但无法发送音频文件，日志中出现 `[neonize.utils.ffmpeg WARNING]` 相关错误。该 Issue 已持续 8 天，**但 PR #5203（今日已合并）正是针对此问题的修复**——通过文件内容检测而非扩展名识别来处理出站音频格式，预计将解决此问题。


## 5. Bug 与稳定性

按严重程度排列今日报告或活跃的 Bug：

| 严重程度 | Issue / PR | 描述 | 状态 |
|---------|-----------|------|------|
| **P1** | [#5237](https://github.com/HKUDS/nanobot/issues/5237) | MCP 工具业务错误被当成功处理，导致 agent 空等超时 | 无 fix PR，需框架级修复 |
| **P1** | [#5258](https://github.com/HKUDS/nanobot/pull/5258) | 含凭据的 URL（user:pass@/token/sig/X-Amz-* 等）被转发至远程 Jina reader，存在凭据泄露风险 | ✅ 已有 fix PR（审查中） |
| **P2** | [#5256](https://github.com/HKUDS/nanobot/issues/5256) | `/goal` 消息在等待用户回复时产生数十条重复回复，直至用户干预或模型识别为系统循环 | ✅ 已有 fix PR（[#5257](https://github.com/HKUDS/nanobot/pull/5257)，审查中） |
| **P2** | [#5149](https://github.com/HKUDS/nanobot/issues/5149) | WhatsApp 无法发送音频（接收正常），ffmpeg 相关警告 | ✅ 已有 fix PR（#5203 今日已合并） |
| **P2** | [#5248](https://github.com/HKUDS/nanobot/pull/5248) | Matrix 加入房间时发送空 POST body，Continuwuity 服务器返回 `M_BAD_JSON` 错误 | ✅ 已有 fix PR（审查中） |
| **P2** | [#5260](https://github.com/HKUDS/nanobot/pull/5260) | 跟踪的工作区目录内存在运行时文件（如 `.dream_cursor`）被误纳入记忆系统 | ✅ 已有 fix PR（审查中） |

**稳定性态势**：#5238 解决了 #5211 引入的访问授权回归，今日无明显新回归上报。安全方向 #5258 值得关注，建议尽快合入并发布。


## 6. 功能请求与路线图信号

**高潜力纳入下一版本的功能请求：**

- **Issue #5251 — MCP Apps host 支持（新开，0 评论）**
  [Issue #5251](https://github.com/HKUDS/nanobot/issues/5251)
  用户建议支持官方 MCP Apps 扩展（`io.modelcontextprotocol/ui`），使 MCP server 能附加交互式 UI 组件到工具结果中。当前 nanobot 将 MCP 调用结果仅作为模型可读的文本/图像。结合 [#5237](https://github.com/HKUDS/nanobot/issues/5237) 的 MCP 相关反馈，说明社区对 MCP 深度集成（UI 与错误契约）有持续需求。

- **PR #5255（Draft）— 外部管理服务器的真实 API 状态**
  [PR #5255](https://github.com/HKUDS/nanobot/pull/5255)
  提案让 WebUI API server 面板如实反映未被 gateway 启动的 `nanobot serve` 实例状态，并新增 `nanobot api status` 命令。对自托管/多实例部署场景有实际价值。

**已进入 PR 阶段的功能：**


- **PR #5252 — Temporary Chat 模式**（今日新开）— [PR #5252](https://github.com/HKUDS/nanobot/pull/5252)
  临时会话为连接所有、仅存内存，不写入会话历史/WebUI 转录/自动记忆。与 [#5184（已合并，Quick Chat）](https://github.com/HKUDS/nanobot/pull/5184) 形成互补。

- **PR #5253 — 共享交互式项目终端**（今日新开）— [PR #5253](https://github.com/HKUDS/nanobot/pull/5253)
  新增 WebUI 与 agent 共享的项目级持久 PTY（基于 xterm.js），支持人工输入、重连、重启与显式终止。核心功能，值得密切关注。

- **PR #5259 — 仅内存临时会话**（今日新开，基于 #5252）— [PR #5259](https://github.com/HKUDS/nanobot/pull/5259)

上述 WebUI 相关 PR（#5252/#5253/#5259）方向一致，均指向 WebUI 交互深度的显著提升，建议关注其合入节奏。


## 7. 用户反馈摘要

- **MCP 错误处理令人困扰**（[Issue #5237](https://github.com/HKUDS/nanobot/issues/5237)）：用户 Lucky314159 指出，MCP server 业务错误被当作成功调用处理，LLM 无法重新规划，只能等到工具超时。痛点在于**工具调用结果的语义契约不完整**，需要框架级支持区分“业务失败”和“成功”的边界。

- **WhatsApp 音频发送需求明确**（[Issue #5149](https://github.com/HKUDS/nanobot/issues/5149)）：用户期望 nanobot 不仅能“理解”音频，也能“发送”音频。修复 PR #5203 已合并，预计下版本解决。

- **/goal 模式体验问题**（[Issue #5256](https://github.com/HKUDS/nanobot/issues/5256)）：等待用户输入时，系统持续注入“继续或完成目标”提示，导致重复回复。这表明**目标引导循环缺少空闲检测机制**。修复 PR #5257 已在审查中。


## 8. 待处理积压

| 项目 | 创建时间 | 天数 | 说明 |
|------|---------|------|------|
| [Issue #5149](https://github.com/HKUDS/nanobot/issues/5149) WhatsApp 音频发送 | 2026-07-28 | 9 天 | ✅ 通过 PR #5203 已解决（今日合并），等待发布 |
| [Issue #5237](https://github.com/HKUDS/nanobot/issues/5237) MCP 错误被吞 | 2026-08-04 | 2 天 | 无 fix PR，高影响力，建议列入下迭代计划 |
| [PR #5255](https://github.com/HKUDS/nanobot/pull/5255) 真实 API 状态（Draft） | 2026-08-05 | 1 天 | Draft 状态，需要维护者确认方向 |
| [Issue #5251](https://github.com/HKUDS/nanobot/issues/5251) MCP Apps host 支持 | 2026-08-05 | 1 天 | 新功能请求，暂无明确排期 |

**维护者关注建议**：
1. 优先审查 [#5258](https://github.com/HKUDS/nanobot/pull/5258)（凭据泄露风险，P1）与 [#5257](https://github.com/HKUDS/nanobot/pull/5257)（/goal 重复回复，用户可见度高的 Bug）
2. 对 [#5237](https://github.com/HKUDS/nanobot/issues/5237) 给出框架级修复方向或临时规避方案
3. 关注 [#5149](https://github.com/HKUDS/nanobot/issues/5149) 在合并 #5203 后是否自然关闭，如未关闭需跟进


> **总结**：NanoBot 项目处于功能密集迭代期，WebUI 能力（临时会话、项目终端）与通道能力（WhatsApp 媒体、Mattermost 线程策略、Matrix 兼容、MST 搜索）双线推进。8 个 PR 合并中 6 个含测试，工程质量保持较高。安全相关的 #5258（凭据泄露）与 #5237（MCP 错误传递）需在下一版本前重点处理。整体项目健康度良好，社区反馈闭环速度快。

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent 项目动态日报 — 2026-08-06

> **数据覆盖窗口**：2026-08-05 至 2026-08-06（过去24小时） | **数据来源**：NousResearch/hermes-agent GitHub 仓库


## 1. 今日速览

过去 24 小时项目保持**高活跃度**：Issues 更新 50 条（44 条新开/活跃，6 条关闭），PR 更新 50 条（40 条待合并，10 条已合并/关闭），当日无新版本发布。值得关注的是，**多项 P0/P1 级会话数据安全修复已合并**——SQL LIKE 通配符逃逸修复（#79722、#78927、#78681）系列解决了 `hermes sessions prune/archive` 可能误删会话数据的严重问题。然而，生命周期守卫（lifecycle_guard）在终端命令扫描中的 `embedded null byte` 崩溃问题出现 **3 条重复报告**（#77780、#79704 等），形成明显的热点聚类。此外，社区围绕多租户架构（#34352）和 god-file 拆分史诗（#78647）的讨论持续升温，表明项目正经历架构演进关键期。


## 2. 版本发布

当日无新版本发布。最近已知版本为 v0.20.0（2026年8月，git 安装）及 v0.8.0（2026.4.8）。


## 3. 项目进展

今日合并/关闭的 10 个 PR 中，**会话数据安全修复是本日最重要的进展**。以下为按影响面排序的关键合并：

### 3.1 会话管理安全修复（P0/P1 级）

| PR | 标题 | 影响 |
|---|---|---|
| [#79722](https://github.com/NousResearch/hermes-agent/pull/79722) | fix(sessions): escape LIKE wildcards in prune/archive filters and the cwd-prefix clause | **P0 级修复**。`hermes sessions prune/archive` 的 `--title/--model/--branch` 子串过滤及 cwd-prefix 子句中的 `_` 和 `%` 被 MySQL/SQLite 解释为 LIKE 通配符，导致过滤条件如 `title_like='user_auth'` **可能匹配并删除** `user-auth`、`userXauth`、`user auth` 等其他会话。这是数据丢失级缺陷，已在 main 分支修复 |
| [#78927](https://github.com/NousResearch/hermes-agent/pull/78927) | fix(sessions): escape LIKE wildcards in the cwd-prefix clause | 修复会话列表、工作区恢复、prune/archive 中 cwd 前缀谓词的同类通配符注入问题（P1） |
| [#78681](https://github.com/NousResearch/hermes-agent/pull/78681) | fix(sessions): escape LIKE wildcards in prune/archive substring filters | 修复 `_prune_filter_where` 子串匹配契约中通配符未转义的问题（P1） |
| [#79737](https://github.com/NousResearch/hermes-agent/pull/79737) | refactor(state): consolidate SQL LIKE escaping onto one shared helper | 将散落的 7 处相同 `replace` 链合并为统一的 `escape_like()` 工具函数，纯重构，无行为变更 |

> **分析**：这三个 PR（#79722/#78927/#78681）属同一缺陷的不同表现面，由 `kshitijk4poor` 与 `Drexuxux` 分别独立发现并提交，最终在 [#79737](https://github.com/NousResearch/hermes-agent/pull/79737) 中完成统一收敛。从 Issue #79537/#79538 中 `jtstothard` 的 LCM 描述符生命周期工作来看，代码库中可能存在更多同类模式待清理。

### 3.2 其他值得关注的合并

- **[#79736](https://github.com/NousResearch/hermes-agent/pull/79736) fix(desktop): don't persist zoom fallback on a transient read failure** — 修复桌面端缩放设置（如 150%）间歇性重置为 90% 默认值的问题。根因是 `readZoomState()` 将"配置文件不存在"与"读取失败"两种情况合并返回 `null`，导致瞬态读取失败被持久化为默认值。
- **[#57867](https://github.com/NousResearch/hermes-agent/pull/57867) fix(environments): portable per-writer PID for atomic snapshot writes on bash 3.2** — 修复 macOS 自带 `/bin/bash` 3.2.57 中 `$BASHPID` 为空导致并发快照写入共享同一临时文件的问题。已关闭。
- **[#3230](https://github.com/NousResearch/hermes-agent/pull/3230) feat(skills): add Pi Coding Agent support** — 新增 Pi Coding Agent CLI 集成技能（`skills/autonomous-ai-agents/pi/SKILL.md`），支持一键任务执行与交互式 TUI 会话。已关闭。

### 3.3 整体项目健康度评估

项目在多条战线上同时推进：**会话数据安全加固**（LIKE 逃逸/通配符）、**macOS 兼容性修复**（bash 3.2 环境变量）、**桌面端稳定性**（缩放偏好持久化）、**CI 性能优化**（#79735 增加测试切片数）。架构级工作（god-file 拆分、多租户方案）仍在讨论/规划阶段。**项目正处于"高层架构讨论 + 底层数据安全加固"并行推进的模式**，健康度良好。


## 4. 社区热点

### 4.1 [#34352 Solving the Multi-Tenant Hermes Problem](https://github.com/NousResearch/hermes-agent/issues/34352) — 15 评论 | 2 👍

**状态**：OPEN | **标签**：type/feature, comp/agent, comp/gateway, tool/memory, P3, needs-decision

> **核心主张**：Memory 操作完全绕过 hook 系统，导致多租户隔离在不 fork 核心代码的情况下无法实现。作者声称已用自研修复在生产环境运行数月。

**分析**：这是目前社区最活跃的架构讨论。作者来自 `NimbleCoAI`，带着明确的产品立场（"Multiplayer agentic AI is the future"），其建议大概率涉及在 gateway 层增加 memory 操作的 hook 拦截点。`needs-decision` 标签表明维护者尚未给出明确方向。此 Issue 已开放 2 个多月，**可能需要维护者正式回应**。

### 4.2 [#78647 Epic: Shard all 20 god files — repo-wide god-file decomposition](https://github.com/NousResearch/hermes-agent/issues/78647) — 10 评论

**状态**：OPEN | **标签**：type/refactor, comp/agent, P3, needs-decision

> **核心主张**：仓库范围内所有 god 文件必须拆分，绝不回退。作者同时提交了多个针对具体文件的拆分子任务（#78638 Slack adapter 9,088 行、#78634 Discord adapter 10,114 行），并有配套 PR（[#79662](https://github.com/NousResearch/hermes-agent/pull/79662) 拆分 main.py）。

**分析**：`andrexibiza` 正在系统性推动 god-file 重构。配套 PR #79662 采用"盲证提取"方式拆分 `hermes_cli/main.py`，声称"逐字提取、零行为变更"。这类大规模重构容易引入回归，需要维护者审慎评估。**PR #79662 目前 P3 优先级待合并，可能是后续合并风暴的开端**。

### 4.3 [#77780 lifecycle_guard crashes on `ValueError: embedded null byte`](https://github.com/NousResearch/hermes-agent/issues/77780) — 11 评论

**状态**：OPEN | **标签**：type/bug, comp/tools, comp/cron, tool/terminal, P2

> **现象**：`cron/lifecycle_guard.py` 在扫描 heredoc / `-c` 载荷中的路径时触发 `ValueError: embedded null byte`，崩溃传播至 `contains_gateway_lifecycle_command_or_referenced_script`，导致所有终端命令失败。

**分析**：该 Bug 在 24 小时内出现 **3 条重复报告**（#77780、#79704、#79728，见下文）。这是一个影响面较大（所有终端命令）且触发条件隐蔽（特定命令形态）的缺陷。**社区通过重复报告的方式在向维护者施压**。

### 4.4 [#79728 Kanban block-loop recovery mis-decomposed into duplicate work](https://github.com/NousResearch/hermes-agent/issues/79728) — 1 评论

**状态**：OPEN | **标签**：type/bug, duplicate

> **现象**：同一阻塞类型复发两次后，已有 owner/worktree/branch/PR 的 Kanban 任务被路由到 `triage`，`auto_decompose: true` 导致网关将恢复 triage 卡片当作新任务重复分解。

**分析**：这是自动化工作流（Kanban + auto-decompose）的**自我干扰问题**——系统在恢复阻塞任务时产生了重复的分解工作。`duplicate` 标签表明维护者已意识到与某个已知问题重复，但尚未指定修复方案。


## 5. Bug 与稳定性

按严重程度排列（含已报告 Bug 及对应修复状态）：

### 🔴 P0 — 数据丢失

| Issue | 描述 | 修复状态 |
|---|---|---|
| [#79391](https://github.com/NousResearch/hermes-agent/issues/79391) | **Interrupted auto-compaction(`explicit_interrupt`) permanently deletes session history** — 无摘要、无归档、消息 ID 硬缺口。影响 Windows 桌面端 DeepSeek-v4-flash 用户 | ⚠️ 无专门 fix PR，但 #79741 的"compaction 冷却递增"修复思路可能部分缓解 |
| [#79722](https://github.com/NousResearch/hermes-agent/pull/79722) 关联 | 通配符注入导致 `prune/archive` **误删会话**（见上文 3.1） | ✅ 已合并 |

### 🟠 P1 — 功能中断/数据风险

| Issue | 描述 | 修复状态 |
|---|---|---|
| [#79678](https://github.com/NousResearch/hermes-agent/issues/79678) | `hermes update` 在 pull 成功后 **re-detach HEAD 丢弃更新**。启动 HEAD 为裸 SHA 时，更新被静默丢弃 | ✅ PR [#79734](https://github.com/NousResearch/hermes-agent/pull/79734) 已提交（"gate 'Code updated!' on HEAD actually moving"），待合并 |
| [#79624](https://github.com/NousResearch/hermes-agent/issues/79624) | Gateway 重启时 preflight 压缩导致 **exit(1) 进程崩溃**。会话超 98,304 tokens 时触发 | ✅ PR [#79741](https://github.com/NousResearch/hermes-agent/pull/79741) 已提交（实际为冷却递增而非崩溃修复，作者指出 exit(1) 非崩溃），待合并 |
| [#78541](https://github.com/NousResearch/hermes-agent/issues/78541) | Telegram 群组/论坛会话 **抑制正常最终发送**，吞掉完整回复。P1 | ✅ 已关闭（sweeper:risk-message-delivery） |

### 🟡 P2 — 功能异常

| Issue | 描述 | 修复状态 |
|---|---|---|
| [#77780](https://github.com/NousResearch/hermes-agent/issues/77780) | lifecycle_guard `embedded null byte` 崩溃，**所有终端命令失败**。已有 2 条重复报告（#79704、#79728） | ❌ 无 fix PR |
| [#5254](https://github.com/NousResearch/hermes-agent/issues/5254) | LM-Studio 下 **tool calls 重复执行**，碎片化为数十次单独调用 | ❌ 已开放 4 个月，无修复 |
| [#76901](https://github.com/NousResearch/hermes-agent/issues/76901) | Termux 安装脚本报错 | ❌ 无 fix PR |
| [#79762](https://github.com/NousResearch/hermes-agent/issues/79562) | 微信/WeCom `/approve` 文本回退在第一轮后**静默失效**（时序竞争） | ❌ 无 fix PR |
| [#79677](https://github.com/NousResearch/hermes-agent/issues/79677) | QQ Bot cron 投递**硬编码 `msg_type 0`**，markdown 表格不渲染 | ❌ 无 fix PR（标注 duplicate） |
| [#79704](https://github.com/NousResearch/hermes-agent/issues/79704) | 同上 #77780，venv 路径命令触发 | ❌ 无 fix PR（标注 duplicate） |

### 🟢 P3 — 低影响/边缘场景

- [#68927](https://github.com/NousResearch/hermes-agent/issues/68927) 桌面端长时间任务后 Enter 提交但 UI 不渲染用户气泡
- [#68876](https://github.com/NousResearch/hermes-agent/issues/68876) 桌面端 provider/model 切换后 UI 不同步
- [#43339](https://github.com/NousResearch/hermes-agent/issues/43339) macOS 桌面端删除 Profile 时 `.env` 不可变标志导致失败
- [#79664](https://github.com/NousResearch/hermes-agent/issues/79664) Vite configLoader 'native' 不支持的警告（duplicate）


## 6. 功能请求与路线图信号

### 6.1 长期自治缺口追踪（可能纳入后续版本）

**[#79686 Tracker: long-running autonomy gaps](https://github.com/NousResearch/hermes-agent/issues/79686)** — 作者 `kshitijk4poor` 整理了 5 个长期自治的缺口：

1. **Retained subagents** — 子代理跨任务保留（已有对应 issues）
2. **Goal gates** — 目标门控，长任务中检查点
3. **Self-edit audit/rollback** — 自修改审计与回滚
4. **Session heartbeats** — 会话心跳
5. **Inline shell** — 内联 shell 执行

> **信号**：该 tracker 将散落的自治能力需求整合为连贯路线图，可作为维护者规划下一阶段自主性功能的重要参考。作者同时提交了 #79741（compaction 冷却）和 #79737（LIKE 转义收敛），**表明其是深度用户兼贡献者，其需求可能代表核心用户群的共同痛点**。

### 6.2 API 会话自动标题

**[PR #63672 feat(api-server): auto-title API sessions](https://github.com/NousResearch/hermes-agent/pull/63672)** — 将 CLI/gateway 已有的自动标题功能移植到 `/v1/chat/completions`、`/v1/runs` 等 API 端点。这是 #9698 的移植和扩展，处于 P3 待合并状态近一个月，**可能因 god-file 重构浪潮而被延后**。

### 6.3 多租户架构（#34352）

详见"社区热点"。若维护者采纳社区方案，这将是 **Hermes 从"单用户代理"迈向"多用户平台"的关键一步**，但 `needs-decision` 标签表明方向未定。

### 6.4 桌面端与 Dashboard 持久化运行

**[#53839 Feature request: durable reconnectable runs](https://github.com/NousResearch/hermes-agent/issues/53839)** — 桌面端和 Web Dashboard 的交互式聊天生命周期与实时客户端传输紧耦合，需要可重连的持久化运行。1 👍。

### 6.5 Discord 链接预览开关（#60942）

Telegram 适配器有 `disable_link_previews` 开关，Discord 缺失对应功能——这是一个小而明确的可用性改进需求。


## 7. 用户反馈摘要

### 痛点提炼

1. **会话数据安全是核心焦虑** — #79391（中断压缩永久删除历史）和 #79722（通配符误删会话）都涉及**不可逆数据丢失**，这是用户最敏感的领域。`echoes666` 明确提到"message IDs show a hard gap"，说明用户对数据完整性问题有细致的观察。

2. **macOS 兼容性持续困扰用户** — 多个 macOS 相关 Bug（#57866 env 快照、#43339 profile 删除、#76901 Termux 安装）表明 macOS 是 Hermes 的重要使用平台，但**兼容性测试覆盖不足**。

3. **多平台消息投递不一致** — Telegram（#78541）、微信（#79562）、QQ（#79677）三个平台在同一天内都有消息投递/渲染 Bug 被报告，说明**网关适配器层缺少统一的投递验证机制**。用户 `GTHell` 在 #78541 中详细描述了 payload-less split-delivery 导致的 `content_delivered` 状态污染，显示出对 gateway 内部逻辑的深度理解。

4. **更新机制信任度受损** — #79678（更新被静默丢弃）会让用户对 `hermes update` 产生不信任，影响版本升级率。

5. **长时间运行是核心使用场景** — #68927（长任务后 UI 卡死）、#53839（持久化运行需求）、#79686（自治缺口 trackers）三者的共性表明用户**将 Hermes 用于长时间、半自治的工作流**，而不是短对话。

6. **桌面端 UI 状态同步问题** — #68927 和 #68876 都涉及桌面端 UI 与后端状态不同步，这可能是 Electron 渲染层与主进程通信的典型问题。值得注意 #68876 的作者 `shaoxianbilly` 同时提交了两个桌面端 Bug，对桌面端体验有持续关注。

### 正面信号

- `NimbleCoAI`（#34352，多租户方案）和 `kshitijk4poor`（#79686，自治 tracker）都是**在生产环境中深度使用 Hermes 的用户**，愿意投入精力撰写高质量提案，表明社区有较强的贡献意愿。
- `realchrisbarnes` 在 #57866 中精准定位了 `$BASHPID` 在 macOS bash 3.2 的兼容性问题，并提交了针对性修复 PR，**展示出社区贡献者具备生产级的调试能力**。
- PR #79599（桌面端离线安装包）将为用户提供**无需网络和 npm 的安装体验**，这是对 Termux 和其他网络受限环境用户反馈的直接回应。


## 8. 待处理积压

### 长期未响应 Issue

| Issue | 创建时间 | 持续时间 | 标签 | 问题 |
|---|---|---|---|---|
| [#5254](https://github.com/NousResearch/hermes-agent/issues/5254) LM-Studio 工具调用重复 | 2026-04-05 | **4 个月** | P2, comp/agent | 重要集成缺陷（LM-Studio 是主流本地推理工具），已有明确复现路径但无维护者回应 |
| [#34352](https://github.com/NousResearch/hermes-agent/issues/34352) 多租户方案 | 2026-05-29 | **2.5 个月** | P3, needs-decision | 核心架构决策待定，社区已投入大量讨论 |
| [#8576](https://github.com/NousResearch/hermes-agent/issues/8576) WhatsApp 桥 npm 漏洞 | 2026-04-12 | **~4 个月** | type/security | 已关闭（implemented-on-main），但关闭时间与创建时间之间隔了近 4 个月，期间用户暴露于知道的安全漏洞中。值得反思安全修复的响应时效 |
| [#8298](https://github.com/NousResearch/hermes-agent/pull/8298) `/background` 任务无超时 | 2026-04-12 | **~4 个月** | P2, sweeper:risk-session-state | 后台任务可能无限期挂起，PR 已提交但长期待合并 |
| [#8290](https://github.com/NousResearch/hermes-agent/pull/8290) cron tick loop 级联失败 | 2026-04-12 | **~4 个月** | P2, sweeper:blast-moderate | 单个 cron 调度错误可禁用全部 cron 任务，PR 已提交但长期未合并 |

### 分析

**#5254（LM-Studio 工具调用重复）是当前最紧急的积压问题**——P2 严重级别、已有明确复现步骤、持续 4 个月无回应。该问题直接影响使用本地模型的核心用户群体。在本地推理工具日益流行的背景下，此问题可能正在抑制 Hermes 在开源社区（非 OpenAI API 用户）的采用。

**#8298 与 #8290 两个 PR 同为 4 月 12 日提交且至今未合并**，但值得注意 #8290 有 `sweeper:blast-moderate` 标签，说明 sweeper bot 评估其合并影响为中等，这可能是合并缓慢的原因。两个 PR 的长期待合并状态可能反映维护者在**关键路径 PR 的审查上存在瓶颈**。


## 附录：项目健康度指标

| 指标 | 数值 | 评价 |
|---|---|---|
| 日活跃 Issues | 44 新开/活跃 | 🟢 高 |
| 日关闭 Issues | 6 | 🟡 较低（相对于 44 条活跃） |
| 日合并/关闭 PR | 10 | 🟢 正常 |
| 待合并 PR | 40 | 🟡 存在积压（含 #8298、#8290 等 4 个月老 PR） |
| 新版本发布 | 0 | ⚪ 正常（距上次 v0.20.0 约 1 个月） |
| 重复 Bug 报告 | 3 组（null byte、Vite、update HEAD） | 🟡 有聚类但可接受 |
| 数据安全级修复 | 4 个已合并 | 🟢 安全响应及时 |
| 长期未响应 Issue（>2 个月） | 3-5 个 | 🟡 需要关注 |

---

*报告生成时间：2026-08-06 | 数据窗口：2026-08-05 至 2026-08-06 | 来源：NousResearch/hermes-agent GitHub*

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw 项目动态日报

**日期：2026-08-06** | **数据来源：github.com/sipeed/picoclaw**


## 1. 今日速览

PicoClaw 项目当前处于**中低活跃度**状态。过去 24 小时无新 Issue 提交或关闭，但有 3 个 PR 处于开放状态，其中 #3318（pnpm-lock.yaml 修复）属于昨日新提交的紧急修复 PR，反映出项目在构建链稳定性方面仍有改进空间。项目近期没有新版本发布，核心功能推进速度趋缓，但 #3200（默认模型回退链）这类增强型 PR 正在持续迭代，表明项目仍在实质性演进而非停滞。目前有 3 个 PR 等待维护者 review 与合并，维护者响应速度值得关注。

## 2. 版本发布

**无新版本发布。** 上次 Release 距今已有一段时间，建议维护团队评估是否需要在近期规划一次版本发布，以纳入已合并的变更。


## 3. 项目进展

过去 24 小时**无 PR 被合并或关闭**，因此无直接的项目进展更新。但结合当前开放的 3 个 PR，可以观察到的演进方向包括：

| PR | 功能/修复方向 | 状态 | 等待时长 |
|---|---|---|---|
| [#3318](https://github.com/sipeed/picoclaw/pull/3318) | 修复 web/frontend 中损坏的 pnpm-lock.yaml（构建链修复） | 待合并 | 1 天 |
| [#3200](https://github.com/sipeed/picoclaw/pull/3200) | 为模型添加可配置的默认回退链（web UI + 后端 API 持久化） | 待合并 | 36 天 |
| [#1951](https://github.com/sipeed/picoclaw/pull/1951) | 将安装脚本从 docs 仓库迁移至主仓库（构建/文档工程化） | 待合并 | 135 天 |

> ⚠️ **维护者提醒**：#1951 已等待超过 4 个月，#3200 已等待超过 1 个月。若这两个 PR 仍有效，建议尽快 review 并合入或关闭，避免分支过期带来额外合并成本。


## 4. 社区热点

今日无高讨论量 Issue/PR。从近期状态来看，值得关注的 PR 包括：

- **[#3200 可配置默认模型回退链](https://github.com/sipeed/picoclaw/pull/3200)**：作者 lc6464 在 7 月 1 日发起，8 月 5 日仍然活跃更新。该 PR 提供了一个完整的工作流：用户在模型页面设置默认模型、添加回退模型、调整顺序并持久化到后端。这反映了社区对**多模型调度和容错**的强烈需求——当默认模型不可用时，可自动回退到备用模型，避免服务中断。

- **[#3318 pnpm-lock.yaml 修复](https://github.com/sipeed/picoclaw/pull/3318)**：虽然仅提交 1 天，但它是直接的构建阻断问题。如果此问题影响到了使用 pnpm 的开发者，可能会引发较多社区反馈。


## 5. Bug 与稳定性

以下按严重程度排列：

| 严重度 | 问题描述 | 状态 |
|---|---|---|
| 🔴 高 | **[构建阻断] `web/frontend/pnpm-lock.yaml` 存在重复映射键**（`semver@7.8.5` 同时在 `packages:` 和 `snapshots:` 中出现），导致 pnpm 拒绝解析 lockfile，报错 `ERR_PNPM_BROKEN_LOCKFILE` | 已有 fix PR [#3318](https://github.com/sipeed/picoclaw/pull/3318)，**待合并** |

目前无其他新报告的 Bug、崩溃或回归问题。


## 6. 功能请求与路线图信号

今日无新 Issue 提出功能需求，但以下两个 PR 传达了清晰的路线图信号：

| 信号 | 来源 | 分析 |
|---|---|---|
| **多模型回退/容错机制** | [PR #3200](https://github.com/sipeed/picoclaw/pull/3200) | 用户希望不仅能配置默认模型，还能设置一整套回退链（fallback chain）。这可能源于生产环境中模型 API 不稳定或限流问题，属于**可靠性增强**类需求，预计会被纳入下一版本功能规划。 |
| **工程化/文档一致性** | [PR #1951](https://github.com/sipeed/picoclaw/pull/1951) | 将安装脚本从 docs 仓库迁移到主仓库，简化用户安装流程。虽非新功能，但体现了项目对**开箱即用体验**的重视。 |


## 7. 用户反馈摘要

基于当前仅有 3 个开放 PR（无新 Issue），用户反馈有限。从 PR 内容中可提取的间接反馈如下：

- **构建体验痛点（来自 #3318）**：有用户尝试使用 pnpm 安装 web/frontend 依赖时遭遇 lockfile 解析失败。这提示项目在**依赖锁定文件的维护流程**上存在漏洞，可能源于 lockfile 的手动编辑或合并冲突未正确解决。
- **模型配置诉求（来自 #3200）**：用户希望在 UI 层面完整管理模型回退策略，说明当前仅支持单一默认模型的配置方式在真实使用场景中不够灵活，尤其是在某个模型 API 暂时不可用的场景下。


## 8. 待处理积压

以下 PR 长期未获维护者响应，提醒关注：

| 编号 | 标题 | 等待时长 | 建议 |
|---|---|---|---|
| [#1951](https://github.com/sipeed/picoclaw/pull/1951) | chore: move installation scripts from docs repo to here | **135 天** | 建议维护者明确回应该 PR 是否仍被接受。若接受的优先级较低，建议在评论区说明，避免贡献者长期悬置等待。 |
| [#3200](https://github.com/sipeed/picoclaw/pull/3200) | feat(models): add configurable default fallback chain | **36 天** | 建议在下一轮 review 中优先处理，功能价值明确，且多次更新表明作者有较强的维护意愿。 |
| [#3318](https://github.com/sipeed/picoclaw/pull/3318) | fix(web): repair unparseable pnpm-lock.yaml | **1 天** | 构建阻断类修复，建议**尽快合入**或指派 reviewer 推进。 |


### 📊 项目健康度评估

| 维度 | 评分 | 说明 |
|---|---|---|
| 活跃度 | ★★☆☆☆ | 24h 内无新 Issue、无版本发布，PR 合并为 0 |
| 响应速度 | ★★☆☆☆ | #1951 和 #3200 均存在长期未处理的情况 |
| 代码质量/稳定性 | ★★★☆☆ | 目前仅有 1 个构建链 Bug 待修，核心功能未见回归问题 |
| 路线图推进 | ★★★☆☆ | PR #3200 推进多模型能力，属实质功能演进 |
| 社区参与 | ★★★☆☆ | 贡献者有持续提交，但 Issue 讨论较少 |

**总体判断**：项目处于**稳定但偏慢**的迭代节奏。核心功能架构已然成型，当前的工作重心偏向工程质量与模型配置灵活性。建议维护者优先处理 #3318 以保构建链健康，并在近期内对 #3200 与 #1951 做出明确决策，以维护贡献者积极性。

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw 项目动态日报

**日期：2026-08-06** | **数据来源：github.com/qwibitai/nanoclaw**


## 1. 今日速览

过去 24 小时 NanoClaw 项目整体活跃度**中等偏高**：PR 侧迎来一波提交高峰（10 条更新），其中 9 条处于待合并状态，覆盖附件传递、WhatsApp 启动超时、MCP 环境变量透传等多个修复方向；Issue 侧保持 2 条活跃讨论，均为**持续近三个月未解决的老问题**（#2528 Signal 附件不可达、#2006 Docker 权限恢复路径失效），虽评论量不高但长期悬置已构成稳定性隐患。今日无新版本发布，项目处于**功能迭代与稳定性修复并行**的密集开发期。


## 2. 版本发布

今日无新版本发布。


## 3. 项目进展

今日**合并/关闭 1 条 PR**，另有 9 条 PR 处于待合并状态，整体推进节奏正常。

**今日已合并：**

| PR | 标题 | 核心价值 |
|---|---|---|
| [#3187](https://github.com/nanocoai/nanoclaw/pull/3187) | fix(agent-runner): disallow built-in SendMessage so agent-to-agent messaging works | 修复 agent-to-agent 消息链路，禁止内置 SendMessage 被错误拦截 |

**待合并 PR 中值得关注的进展：**

- **附件传递链路修复（#3156）**：`fix(agent-runner): carry channel attachments to providers as structured parts`，将附件作为结构化数据传递给 provider —— 直接对应 Issue #2528 反映的 Signal 图片/PDF 不可达问题，若合并可显著改善多模态消息体验。
- **宿主启动稳定性（#3191）**：`fix(whatsapp): bound setup() to a timeout`，防止 WhatsApp 会话登出后阻塞整个宿主启动 —— 这是对基础设施可靠性的重要加固。
- **安全性与环境一致性（#3188）**：`fix(container): forward OneCLI gateway env to spawned MCP servers`，解决子进程 MCP 服务器缺失 HTTPS_PROXY/CA 信任变量的问题。


## 4. 社区热点

今日讨论热度整体偏低，2 条活跃 Issue 均仅有 1 条评论，无高互动讨论。

**相对受关注的议题：**

- **[Issue #2528](https://github.com/nanocoai/nanoclaw/issues/2528) — Signal 附件不可达（更新于 08-05）**：由用户 brentkearney 报告，已存在近三个月。核心痛点是**图片/PDF 附件到达宿主但 agent 容器内无法访问**。该问题与待合并 PR #3156 直接相关，说明社区反馈已转化为实际修复，值得跟进合并进展。
- **[Issue #2006](https://github.com/nanocoai/nanoclaw/issues/2006) — Debian 12 LXC 安装 Docker 权限失败（更新于 08-05）**：安装脚本将用户加入 docker 组后，后续步骤仍在同一进程内执行、未能重新加载组权限，恢复路径未触发。该问题自 4 月 25 日报告以来已悬置超三个月，且涉及新用户首次安装体验，建议维护者优先响应。


## 5. Bug 与稳定性

今日共 2 条活跃 Bug 相关 Issue，均为长期未关闭问题：

| 严重程度 | Issue | 问题描述 | 状态 |
|---|---|---|---|
| **高** | [#2528](https://github.com/nanocoai/nanoclaw/issues/2528) | Signal 通道图片/PDF 附件在 agent 容器内不可达 | 已有对应 fix PR #3156 待合并 |
| **中** | [#2006](https://github.com/nanocoai/nanoclaw/issues/2006) | Debian 12 LXC 上 Docker socket 权限拒绝，恢复路径不触发，安装流程中断 | **无 fix PR**，长期未响应 |

> ⚠️ **重点提醒**：#2006 同时涉及安装体验和权限安全，自 4 月报告以来无任何修复进展。新用户首次部署即遭遇阻塞，对项目口碑影响较大，建议纳入近期 sprint。


## 6. 功能请求与路线图信号

今日无新功能请求 Issue 提交，但 PR 侧透露出清晰的路线图方向：

- **新增 Skill 生态扩展**（2 条）：
  - [#3190](https://github.com/nanocoai/nanoclaw/pull/3190) — Tavily MCP 工具 Skill（搜索能力）
  - [#3189](https://github.com/nanocoai/nanoclaw/pull/3189) — `add-why` Skill（单条消息行为解释）
- **新通道集成**（1 条）：
  - [#3050](https://github.com/nanocoai/nanoclaw/pull/3050) — Dial 通道接入 channel picker 及 wizard/skills（已提交三周，仍在待合并队列中）
- **架构演进**（2 条）：
  - [#3186](https://github.com/nanocoai/nanoclaw/pull/3186) — 为 skill 自有能力增加 host seams（宿主接缝抽象）
  - [#3172](https://github.com/nanocoai/nanoclaw/pull/3172) — 清理过期的 qodo 和 Google MCP skill
- **CLI 交互优化**（1 条）：
  - [#2346](https://github.com/nanocoai/nanoclaw/pull/2346) — 未知斜杠命令回退为普通聊天，避免响应被静默丢弃

> 上述 PR 中，#3190、#3189、#3186、#3172 均标记了 `follows-guidelines` 标签，合入概率较高，预计会在未来 1–2 个版本内落地。


## 7. 用户反馈摘要

从今日活跃 Issue 的评论中提炼的用户声音：

- **安装体验痛点**（#2006）：用户 dooha333 在 Debian 12 LXC 环境中执行标准安装流程即遭遇失败，`usermod -aG docker` 后未退出重登导致权限不生效，而安装脚本的恢复路径也未触发。**这暴露了安装脚本对组权限变更生效机制的假设错误** —— 同一进程内 `usermod` 不会自动刷新进程的组权限，需要在脚本中通过 `sg docker` 或 `newgrp` 等方式显式切换。
- **多模态消息需求**（#2528）：用户 brentkearney 期望 agent 能够查看通过 Signal 发送的图片（如 `archetype.png`）—— 这是 AI 助手走向多模态交互的基础诉求。目前附件在容器内不可达，直接限制了 agent 在视觉理解类任务上的能力边界。

> 两位用户均给出了清晰的复现步骤，属于高价值反馈。


## 8. 待处理积压

以下 Issue/PR 长期未获响应，建议维护团队重点关注：

| 类型 | 编号 | 标题 | 已搁置时长 | 建议 |
|---|---|---|---|---|
| Issue | [#2006](https://github.com/nanocoai/nanoclaw/issues/2006) | Debian 12 LXC 安装 Docker socket 权限拒绝 | **103 天** | 高优先级——直接阻塞新用户安装，建议指派维护者复现并修复 |
| PR | [#3050](https://github.com/nanocoai/nanoclaw/pull/3050) | feat(setup): add Dial to the channel picker | **23 天** | 功能性 Feature PR 长期未合并，建议确认是否纳入下个版本或关闭 |
| PR | [#2346](https://github.com/nanocoai/nanoclaw/pull/2346) | fix(formatter): treat unknown slash commands as normal chat | **90 天** | 已提交三个月未处理，属于交互体验修复，建议尽快 review |

---

**总结**：NanoClaw 今日处于**功能开发活跃、稳定性修复跟进中**的状态。社区提交质量较高（多条 PR 均带 `follows-guidelines`），但**长期积压的 Issue 响应速度偏慢**是当前主要健康度短板。建议维护者优先处理 #2006 安装阻塞问题，同时加速 #3156（附件传递）与 #3191（WhatsApp 超时）两条关键修复 PR 的合并评审。

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

# NullClaw 项目动态日报 — 2026-08-06

## 今日速览

NullClaw 昨日整体活跃度处于**中低水平**：无新 Issue 提交、无版本发布，但有两项关键修复 PR 处于待合并状态。两个 PR 均由贡献者 raskevichai 提交，分别针对代理会话栈溢出（#985）和 Telegram/Matrix 频道轮询线程静默失效（#984）两大稳定性顽疾。尽管 Issue 流动为零，但这两个 PR 均针对已提交的 Issue（#976、#972）提供根治方案，且均为运行时/通道层的核心修复，表明项目维护处于**修复驱动的收敛期**，而非功能扩张期。核心注意点：两项修复若未及时合并，用户侧（特别是 Telegram/Matrix 重度用户）的稳定性问题将持续存在。

- 新 Issues：0 | 活跃 Issues：0 | 已关闭 Issues：0
- 新 PRs：2（均待合并） | 合并 PRs：0
- 新版本发布：0

---

## 版本发布

今日无新版本发布。

---

## 项目进展

今日无 PR 被合并或关闭，但两项待合并 PR 值得重点关注，二者合计将解决两个长期存在的运行时稳定性缺陷：

**1. PR #985 — 为 Agent turn 路径分配 16 MiB 独立栈空间**

- **状态**：待合并（OPEN）
- **作者**：raskevichai
- **链接**：[nullclaw/nullclaw PR #985](https://github.com/nullclaw/nullclaw/pull/985)
- **修复内容**：修复 `SESSION_TURN_STACK_SIZE` 被错误别名到 `HEAVY_RUNTIME_STACK_SIZE`（2 MiB）的问题。该常量控制所有执行 `SessionManager.processMessage*()` 与 `Agent.turn()` 的线程栈大小，将其提升至 16 MiB 可消除代理在处理复杂会话时可能发生的栈溢出风险。
- **关联 Issue**：关闭 #976

**2. PR #984 — 允许轮询失败的通道线程自然老化退出**

- **状态**：待合并（OPEN）
- **作者**：raskevichai
- **链接**：[nullclaw/nullclaw PR #984](https://github.com/nullclaw/nullclaw/pull/984)
- **修复内容**：解决 Telegram 和 Matrix 通道在空闲一夜后静默失效、而 `nullclaw agent` 仍正常响应的问题。根因是 `supervisionLoop` 在结构上无法感知轮询线程的"死而不僵"状态；本 PR 让轮询失败能够触发线程老化并退出，使监督者可以正确重启。此前唯一恢复手段是完整重启网关。
- **关联 Issue**：关闭 #972

**项目整体进度评估**：这两项 PR 直指运行时稳定性的两大核心隐患（栈空间不足、通道线程假死）。合并后，项目在长时间无人值守运行（如服务器/网关部署）场景下的可靠性将显著提升，属于**夯实基础架构**的关键一步。目前尚无功能迭代迹象。

---

## 社区热点

今日无高热度讨论或高评论量 Issue/PR。两项 PR 均无评论且 👍 数为 0，但考虑到它们均为同一天创建、且带有完整根因分析，属于**高质量快速提交**，尚未引起社区广泛讨论。建议关注这两项 PR 合入后，是否会引发用户对 Telegram/Matrix 通道稳定性改善的反馈潮。

---

## Bug 与稳定性

今日无新 Bug 报告，但有 **2 个待合并的修复 PR**，对应此前报告的两个稳定性问题：

| 严重程度 | 问题描述 | 来源 | 修复状态 |
|---------|---------|------|---------|
| 高 | 代理会话轮询线程静默失效（Telegram/Matrix 通道一夜后无响应，仅重启网关可恢复） | [#972](https://github.com/nullclaw/nullclaw/issues/972) | 已有修复 PR [#984](https://github.com/nullclaw/nullclaw/pull/984)（待合并） |
| 中 | 代理 turn 路径栈溢出（`SESSION_TURN_STACK_SIZE` 被错误设置为 2 MiB） | [#976](https://github.com/nullclaw/nullclaw/issues/976) | 已有修复 PR [#985](https://github.com/nullclaw/nullclaw/pull/985)（待合并） |

两项修复均已提交且作者为同一人，维护者应优先评估合入，以消除这两个影响长时间运行部署的隐患。

---

## 功能请求与路线图信号

今日无新功能请求提交。两个待合并 PR 均为 Bug 修复而非功能新增,预计不会改变现有 API 或引入破坏性变更。项目路线图当前未见新功能信号，处于**稳定修复期**。

---

## 用户反馈摘要

今日无新用户评论或 Issue 反馈可供提炼。建议回顾前几日与 Telegram/Matrix 静默失效（#972）相关的用户描述，以判断修复 PR 是否覆盖了全部痛点场景（例如：空闲时长阈值、多通道并发下的失效概率等）。

---

## 待处理积压

| 项目 | 类型 | 创建时间 | 状态 | 备注 |
|------|------|---------|------|------|
| [#985 fix(runtime): 16 MiB agent turn 栈](https://github.com/nullclaw/nullclaw/pull/985) | PR | 2026-08-05 | 待合并 | 2 天未审阅，根因分析完整，建议维护者及时 review |
| [#984 fix(channels): 轮询线程老化退出](https://github.com/nullclaw/nullclaw/pull/984) | PR | 2026-08-05 | 待合并 | 2 天未审阅，针对长期稳定性问题，优先级高 |

> 注：两个 PR 均关联未关闭的 Issue（#976、#972），若长期积压不合并，相关问题将持续影响用户。当前无更早的遗留 Issue/PR 积压。

---

*数据来源：[github.com/nullclaw/nullclaw](https://github.com/nullclaw/nullclaw)，统计时间窗口：2026-08-05 至 2026-08-06*

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw 项目动态日报 — 2026-08-06

---

## 1. 今日速览

IronClaw 项目保持高速迭代节奏，过去 24 小时产生 43 条 Issue 更新和 50 条 PR 更新，活跃度处于高位。**核心进展集中在 v1.1.0-rc.1 发布后的稳定性修复与 Reborn 架构持续收敛**：发布分支已合入 MCP egress 与可读日志修复（#7260），迁移保护 PR（#7256）确保 1.0 状态在 1.1 RC 启动期间无损保留。**值得警惕的是 bug_bash 反馈集中爆发**——来自 Railway 测试实例的 7 个新 Bug 涉及 Agent 幻觉、MCP 端点验证缺失、跨渠道投递错误等问题，反映出 Agent 真实环境可靠性仍是短板。设计系统提案（#7038）、Admin-Managed Agents（#6578）等大型 Epic 正在推进中。

---

## 2. 版本发布

### ironclaw-v1.1.0-rc.1（1.1.0-rc.1 · 2026-08-03）

**发布亮点：**
- **扩展生态触达**：支持注册任意托管的 MCP 服务器；支持通过 IronHub deep links 安装扩展
- **跨渠道文件附件**：文件附件可在不同渠道（Slack/Telegram/Web）间持久化传递
- **Slack `/ironclaw` 斜杠命令**：新增原生 Slack 命令入口
- **失败可读性全面改进**：错误信息和诊断输出的可读性大幅提升

**⚠️ 破坏性变更与迁移注意：**
- 暂无明确破坏性变更声明，但 RC 版本意味着 API 可能仍有调整
- 发布分支上已合入 #7256（迁移保护 PR），确保 1.0 状态（线程/转录、定时任务、频道绑定、扩展/OAuth、流程/产品台账等）在 RC 启动期间通过无损迁移保留——**建议升级前备份数据并先在 staging 环境验证迁移**

---

## 3. 项目进展

### 今日合并/关闭的关键 PR

| PR | 标题 | 影响 |
|---|---|---|
| [#7256](https://github.com/nearai/ironclaw/pull/7256) | fix(migration): preserve 1.0 state during 1.1 RC startup | 确保 1.0 数据在 1.1 RC 启动时无损迁移，对升级路径至关重要 |
| [#7260](https://github.com/nearai/ironclaw/pull/7260) | fix(release): backport MCP egress and readable log fixes | 回传 #7241（托管 MCP 工具保留 HTTPS 端点作为显式网络目标）和 #7227（可读文本日志保持可写）至发布分支 |
| [#7258](https://github.com/nearai/ironclaw/pull/7258) | The narrowing tail: WS5/WS6/WS8/WS10 closures + both crate dissolutions | 7 个独立构建、独立验证的切片批量合入，推进 Reborn 重构的收尾阶段 |
| [#7133](https://github.com/nearai/ironclaw/pull/7133) | fix(tools): support bounded JSON file queries | 支持有界 JSON 文件查询，含 JSONPath 风格的 `$` 根路径解析，带可操作的诊断信息 |
| [#7227](https://github.com/nearai/ironclaw/pull/7227) | fix(coding): keep readable text logs writable | 修复 read-before-edit 校验后文本日志不可写的问题，附带回归测试 |

### 架构演进信号

- **`crates/ironclaw_assistant/src/reborn_services.rs` 超过 6,400 行**（#7245），超过 3,000 行阈值，已列入分解追踪
- **两个 crate 正在解散**：PR #7258 的一部分，Reborn 架构持续向新模块边界收敛

---

## 4. 社区热点

### 讨论热度最高

| 排名 | Issue | 评论数 | 主题 |
|---|---|---|---|
| 1 | [#3036](https://github.com/nearai/ironclaw/issues/3036) | 7 | **[EPIC] Configuration-as-Code**：面向租户蓝图和使用案例的声明式配置，替代手改 `.env`/`.system/`/settings JSON 的现状 |
| 2 | [#7194](https://github.com/nearai/ironclaw/issues/7194) | 3 | **Outbound 投递目标**：让 admin 允许的共享频道可被主机投递层作为最终回复路由目标 |
| 3 | [#6257](https://github.com/nearai/ironclaw/issues/6257) | 2 | **PDF 文件 MIME 类型错误**：生成/发送 PDF 时报 `Invalid value (attachments.mime_type)` |

### 核心诉求分析

- **#3036 是社区最高呼声**：配置管理碎片化（`.env` + `.system/` + settings JSON + 运行时 flags），无 schema、无 diff、无审计轨迹。这反映 Reborn 架构中配置面尚无统一抽象，是中型团队采用的关键障碍。
- **#7194 指向能力边界**：Agent 可以枚举和发消息到 Slack 频道，但主机投递层无法将其设为 outbound 目标——能力存在但不可编排，需要架构层面的统一。

---

## 5. Bug 与稳定性

### P1 严重级别

| Issue | 描述 | 状态 |
|---|---|---|
| [#7247](https://github.com/nearai/ironclaw/issues/7247) | **Agent 谎称 GitHub 已连接**：未验证实际认证状态即声称可用，下一次 GitHub 操作立即失败 | OPEN，无 fix PR |
| [#7246](https://github.com/nearai/ironclaw/issues/7246) | **Agent 编造自动化状态**：Automations 页面显示 "No automations yet"，但 Agent 声称 BTC 新闻摘要正在运行并发送至 Telegram | OPEN，无 fix PR |

### P2 严重级别

| Issue | 描述 | 状态 |
|---|---|---|
| [#7249](https://github.com/nearai/ironclaw/issues/7249) | **Slack DM 执行结果错误投递到 Telegram**：包含 Slack 特定收件人详情和事件元数据，不应泄露 | OPEN，无 fix PR |
| [#7248](https://github.com/nearai/ironclaw/issues/7248) | **无效自定义 MCP 端点被接受**：注册为成功安装后，Agent 反复尝试工具发现失败，run 以失败告终 | OPEN，无 fix PR |
| [#7250](https://github.com/nearai/ironclaw/issues/7250) | **DeepWiki MCP 误导性认证指引**：网络错误时 Agent 猜测原因（认证/URL/不可达）而非报告实际错误 | OPEN，无 fix PR |
| [#7251](https://github.com/nearai/ironclaw/issues/7251) | **Agent 猜测 MCP 认证类型**：不检查端点或发起认证流程，反而让用户选择认证类型并推测 | OPEN，无 fix PR |
| [#7254](https://github.com/nearai/ironclaw/issues/7254) | **无法访问 Slack feedback 线程中的附件**：产品反馈分类流程中无法下载/读取文件 | OPEN，无 fix PR |

### 回归与 CI

| Issue | 描述 | 状态 |
|---|---|---|
| [#7209](https://github.com/nearai/ironclaw/issues/7209) | **CI 回归门无法识别 node:assert 风格**：99% 的前端测试套件使用该风格，导致正确的前端 PR 被错误拦截 | OPEN，讨论中 |

### 已关闭 Bug

| Issue | 描述 |
|---|---|
| [#7204](https://github.com/nearai/ironclaw/issues/7204) | WebUI 聊天 composer 聚焦优化（修复 "+ New" 和线程打开时未聚焦 + 移除 focus-within 强调环） |

---

## 6. 功能请求与路线图信号

### 高概率进入 v1.1.0 的功能

| 功能 | 来源 PR/Issue | 状态 |
|---|---|---|
| **标准化消息框架** | [PR #6831](https://github.com/nearai/ironclaw/pull/6831) | 16 个核心操作 + 13 个保留操作名 + 规范化 JSON Schema + 12 码错误分类，v3-only `standard_op` manifest，待合并 |
| **显式频道投递工具（双通道模型）** | [PR #7157](https://github.com/nearai/ironclaw/pull/7157) | Lane 1（会话内最终回复）+ Lane 2（通知频道），删除旧的投递启发式逻辑 |
| **MCP 注册隐私保护** | [PR #7253](https://github.com/nearai/ironclaw/pull/7253) | 注册仅接受目录定义，不创建设装/设置状态/激活/发布 |
| **技能选择权交给模型** | [PR #6938](https://github.com/nearai/ironclaw/pull/6938) | 移除关键词评分器，由模型自主选择技能，保留调用轨迹 |

### 大型路线图信号

- **IronHub 集成**（[#6731](https://github.com/nearai/ironclaw/issues/6731)）：将 Agent 工具集从构建时固定列表变为可扩展市场，运行时发现和安装社区/第一方工具
- **Admin-Managed Agents**（[#6578](https://github.com/nearai/ironclaw/issues/6578)）：租户管理员可创建和操作非人类主体（产品 Agent、自动化、入站渠道、委托集成），不引入第二套身份层级
- **技能自创建/自发现闭环**（[#6941](https://github.com/nearai/ironclaw/issues/6941)）：模型可自建、发现、选择和使用的技能系统

---

## 7. 用户反馈摘要

### 真实痛点

1. **Agent 幻觉（最严重）**：来自 Railway 测试实例的反馈表明，Agent 会编造自动化运行状态、谎称 GitHub 已连接，**而非检查实际状态**——这直接侵蚀用户信任，属于 P1 级问题（[#7246](https://github.com/nearai/ironclaw/issues/7246)、[#7247](https://github.com/nearai/ironclaw/issues/7247)）
2. **MCP 端点验证缺失**：用户可以注册无效/未经验证的 MCP 端点，导致后续 run 失败且 Agent 无法有效诊断（[#7248](https://github.com/nearai/ironclaw/issues/7248)）
3. **PDF 文件 MIME 错误**：Slack 用户 Michael Kelly 反馈生成/发送 PDF 时报 `attachments.mime_type` 错误（[#6257](https://github.com/nearai/ironclaw/issues/6257)）
4. **反馈线程附件不可读**：产品反馈分类流程中无法读取 Slack 附件，影响用户反馈闭环（[#7254](https://github.com/nearai/ironclaw/issues/7254)）

### 满意度信号

- **积极的方面**：社区对 v1.1.0-rc.1 的扩展触达能力（MCP 注册、IronHub deep links、Slack 斜杠命令）反馈积极，工作重心已转向打磨稳定性和修复边界案例

---

## 8. 待处理积压

### 长期未关闭的高优先级 Issue

| Issue | 创建时间 | 主题 | 备注 |
|---|---|---|---|
| [#3036](https://github.com/nearai/ironclaw/issues/3036) | 2026-04-28 | Config-as-Code Epic | 已开放超 3 个月，7 条评论，社区呼声最高 |
| [#6257](https://github.com/nearai/ironclaw/issues/6257) | 2026-07-19 | PDF MIME 类型错误 | 开放超 2 周，来自外部用户反馈，尚无 fix |

### 长期未合并的大 PR

| PR | 创建时间 | 主题 | 备注 |
|---|---|---|---|
| [#5598](https://github.com/nearai/ironclaw/pull/5598) | 2026-07-03 | chore: release（ironclaw_common 0.5.0 + ironclaw_skills 0.4.0） | 开放超 1 个月，包含 API breaking changes，需协调合并窗口 |
| [#6831](https://github.com/nearai/ironclaw/pull/6831) | 2026-07-28 | 标准化消息框架 | 开放超 1 周，XL 级，风险 medium，涉及 16 个核心操作定义 |

### 提醒维护者关注

- **bug_bash 反馈积压**：来自 Railway 测试实例的 7 个 Bug（[#7246](https://github.com/nearai/ironclaw/issues/7246) 至 [#7254](https://github.com/nearai/ironclaw/issues/7254)）全部无 fix PR，建议优先分配资源——尤其两个 P1 幻觉类问题直接关系产品质量口碑
- **CI 回归门缺陷**（[#7209](https://github.com/nearai/ironclaw/issues/7209)）影响开发者体验，99% 前端测试使用的 assert 风格未被识别，阻塞正常 PR 流程

---

*数据来源：[IronClaw GitHub 仓库](https://github.com/nearai/ironclaw) · 统计周期：2026-08-05 ~ 2026-08-06*

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

# LobsterAI 项目动态日报 — 2026-08-06

> LobsterAI 是网易有道开源的个人 AI 助手框架项目，基于 OpenClaw 运行时构建，提供桌面端、企业级账号隔离、活动中心等多维能力。


## 1. 今日速览

项目今日活跃度**较高**，24 小时内共产生 3 条 Issue 更新（全部为新开）、13 条 PR 更新（12 条已合并/关闭，1 条待合并），并发布了 2026.8.5 版本。值得关注的是，昨日提交中包含多条针对**窗口生命周期**与 **OpenClaw 网关锁文件**的稳定性修复，以及一组"启动积分海报"活动相关的 UI 迭代。此外，今日新开的 2 条 Issue 直指**系统提示词重复注入**与**技能开关静默失效**两个设计层面问题，反馈质量较高，值得维护团队优先评估。整体项目推进速度平稳，社区反馈深度尚可，无阻塞性严重事故。


## 2. 版本发布

### LobsterAI 2026.8.5（发布于 2026-08-05）

**主要更新内容：**

- **feat(activity):** 新增原生每日签到体验（PR [#2408](https://github.com/netease-youdao/LobsterAI/pull/2408)）
- **feat(enterprise):** 实现账号级认证与服务流程隔离（PR [#2409](https://github.com/netease-youdao/LobsterAI/pull/2409)），企业用户的多账号体系不再互相干扰
- 另有部分 style 层面的代码整理（未注明具体范围）

**破坏性变更与迁移注意事项：**

- Release 说明中未标注任何破坏性变更（breaking changes），亦无明确迁移说明。企业版账号隔离为增量功能，现有单账号用户预计不受影响。建议升级后重点回归验证签到活动入口与多账号切换流程。


## 3. 项目进展

今日共合并/关闭 12 条 PR，覆盖稳定性、体验优化与依赖升级三大方向，整体进展健康：

| 方向 | PR | 说明 |
|---|---|---|
| **窗口生命周期加固** | [#2437](https://github.com/netease-youdao/LobsterAI/pull/2437) | 为 OpenAI-compat 代理与 HTML 预览服务器关闭流程引入 drain timer + 硬截止时间，修复 keep-alive 连接导致应用无法退出的问题；同时将主窗口激活推迟至首次渲染完成，避免 focus/二次实例启动时窗口闪现 |
| **网关锁文件防毒化** | [#2436](https://github.com/netease-youdao/LobsterAI/pull/2436) | 修复两处竞态：LobsterAI 强制终止网关（Windows TerminateProcess）时恰逢锁文件写半截，以及网关自身重启触发的锁冲突——两者均会导致后续网关重启最长失败 30 秒 |
| **标题栏会话搜索** | [#2435](https://github.com/netease-youdao/LobsterAI/pull/2435) | 在工件面板开关旁新增会话搜索按钮，复用侧栏搜索图标与现有搜索工作流，并优化了响应式样式与查询感知导航 |
| **启动积分海报迭代** | [#2432](https://github.com/netease-youdao/LobsterAI/pull/2432)、[#2433](https://github.com/netease-youdao/LobsterAI/pull/2433)、[#2438](https://github.com/netease-youdao/LobsterAI/pull/2438)、[#2439](https://github.com/netease-youdao/LobsterAI/pull/2439) | 关闭最终奖励自动弹窗、裁剪海报白边、更换为带关闭按钮的最新素材——活动视觉与交互持续打磨 |
| **依赖升级** | [#1279](https://github.com/netease-youdao/LobsterAI/pull/1279)、[#1280](https://github.com/netease-youdao/LobsterAI/pull/1280)、[#1281](https://github.com/netease-youdao/LobsterAI/pull/1281) | cross-env 7.0.3→10.1.0、react-dom 18.3.1→19.2.4、vite 5.4.21→8.0.9（均由 Dependabot 提交，属常规维护） |

上述 PR 合计反映了项目当前两条主线：**桌面端稳定性加固**（主进程生命周期 + 网关锁）与**活动/运营侧体验打磨**，整体处于"稳定推进 + 精细化迭代"区间。


## 4. 社区热点

今日社区讨论热度整体偏低，3 条新 Issue 均无评论互动。相对值得关注的是：

- **[Issue #2441](https://github.com/netease-youdao/LobsterAI/issues/2441)（技能开关按目录名写入但 OpenClaw 按 frontmatter name 匹配）** — 作者给出了完整的成因分析（含代码定位），指出配置同步逻辑与实际运行时匹配规则不一致导致开关静默失效，且 `openclaw.json` 被整文件覆盖、用户无法持久精简系统提示词。这是典型的"配置同步契约不匹配"问题，修复成本可能不高但影响面广，建议尽快确认。

- **[Issue #1200](https://github.com/netease-youdao/LobsterAI/issues/1200)（NIM 超大群 teamTypeNum 硬编码错误）** — 早在 4 月即已提出并附有修复 PR（[#1201](https://github.com/netease-youdao/LobsterAI/pull/1201)），至今仍未合并，今日被系统标记为 stale。该问题直接影响云信超大群内 @ 机器人场景的群名解析，相关 PR 修复方式仅需一行改动，建议优先处理。


## 5. Bug 与稳定性

今日报告的 Bug 共 3 条，按严重程度排列如下：

| 严重程度 | Issue | 描述 | 状态 |
|---|---|---|---|
| **中** | [#2441](https://github.com/netease-youdao/LobsterAI/issues/2441) | 技能开关按目录名写入，OpenClaw 按 frontmatter name 匹配，导致开关静默失效；`openclaw.json` 被整文件覆盖，用户无持久精简入口 | OPEN，无 fix PR |
| **中** | [#2440](https://github.com/netease-youdao/LobsterAI/issues/2440) | 桌面端每新会话首条消息注入的 `[LobsterAI system instructions]` 块中 78% 内容与 `AGENTS.md` 托管区逐字重复，模型相当于读两遍同一套指令 | OPEN，无 fix PR |
| **低（陈旧）** | [#1200](https://github.com/netease-youdao/LobsterAI/issues/1200) | NIM 超大群消息中 `teamTypeNum` 硬编码错误（team/p2p 类型号对调），导致群名获取失败、@ 机器人时显示原始 ID | OPEN，已有 fix PR [#1201](https://github.com/netease-youdao/LobsterAI/pull/1201) 待合并 |

稳定性修复方面，今日合并的 [#2436](https://github.com/netease-youdao/LobsterAI/pull/2436) 与 [#2437](https://github.com/netease-youdao/LobsterAI/pull/2437) 分别解决了**网关锁文件毒化**（最长 30 秒重启失败）和**应用退出卡死**两类问题，属于典型的"看不见但影响大"的工程债清理。


## 6. 功能请求与路线图信号

今日暂无明确的新功能请求（feature request）。但以下两条信号值得留意：

- **系统提示词精简入口（Issue [#2441](https://github.com/netease-youdao/LobsterAI/issues/2441)）**：作者明确提出"用户没有办法持久地精简进入每次新对话的系统提示词"，并指出 `openclaw.json` 被整文件覆盖的问题。结合同日 Issue [#2440](https://github.com/netease-youdao/LobsterAI/issues/2440) 的重复注入现象，社区对**提示词管理与去重**存在切实需求。该方向若纳入路线图，将同时解决两个反馈。

- **会话搜索（PR [#2435](https://github.com/netease-youdao/LobsterAI/pull/2435)）**：标题栏搜索入口虽为 UI 层优化，但反映出项目在**会话检索/历史管理**方向上的持续投入，后续版本或可见更多搜索相关能力（如全文搜索、时间线过滤等）。


## 7. 用户反馈摘要

今日社区反馈主要来自两条新 Issue，作者均为 fujingzhai（深度用户，报告中包含 `trajectory.jsonl` 采样数据、代码行号定位等，专业度较高）：

- **重复注入痛点（[#2440](https://github.com/netease-youdao/LobsterAI/issues/2440)）**：用户实测统计了 `finalPromptText` 中系统指令块与 `AGENTS.md` 托管区的重合度为 78%，明确表达"同一套指令让模型读了两遍"。此类反馈具有数据支撑，真实性和可复现性均较强，易引发其他用户共鸣。

- **配置同步契约问题（[#2441](https://github.com/netease-youdao/LobsterAI/issues/2441)）**：用户指出"技能开关按目录名写入，OpenClaw 按 frontmatter name 匹配"时开关静默失效，并补充了 `openclaw.json` 整文件覆盖导致"用户无法持久精简每次新对话系统提示词"的设计缺口。作者在描述中使用了"两个相关的问题，都指向同一件事"的表述，说明其核心诉求是**让用户对系统提示词拥有可持续的编辑能力**。

整体来看，今日反馈集中于**开箱即用的配置体验**与**上下文效率**，作者群体偏技术型用户，反馈可信度高。


## 8. 待处理积压

| 项目 | 类型 | 创建时间 | 最后更新 | 备注 |
|---|---|---|---|---|
| [Issue #1200](https://github.com/netease-youdao/LobsterAI/issues/1200) / [PR #1201](https://github.com/netease-youdao/LobsterAI/pull/1201) | Bug + 修复 PR | 2026-04-01 | 2026-08-05（今日被标 stale） | NIM 超大群 `teamTypeNum` 硬编码错误，PR 仅为一行修改，从 4 月至今已超过 4 个月未合并。今日已被 stale bot 标记，若再不处理将进入自动关闭流程。该问题影响超大群实际使用体验，建议维护者尽快评估合并。 |
| [PR #1279](https://github.com/netease-youdao/LobsterAI/pull/1279) / [#1280](https://github.com/netease-youdao/LobsterAI/pull/1280) / [#1281](https://github.com/netease-youdao/LobsterAI/pull/1281) | Dependabot 依赖升级 | 2026-04-02 | 2026-08-05（今日被关） | cross-env、react-dom 19、vite 8 三组升级均于今日被关闭（未注明合入或关闭原因）。若因兼容性问题被拒，建议维护者在关闭时补充原因说明以留档；若已合入，则需关注 react-dom 19 与 vite 8 引入的潜在破坏性变更影响。 |

---

*日报生成时间：2026-08-06 · 数据来源：LobsterAI GitHub 仓库公开数据*

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

# CoPaw 项目动态日报 — 2026-08-06

> 数据来源：[github.com/agentscope-ai/CoPaw](https://github.com/agentscope-ai/CoPaw)（数据概览窗口：2026-08-05 至 2026-08-06）

---

## 1. 今日速览

项目今日活跃度处于高位，24小时内产生 **23 条 Issue 更新**（新开/活跃 17 条、关闭 6 条）和 **50 条 PR 更新**（待合并 29 条、合并/关闭 21 条）。值得关注的是，**今日无新版本发布**，但合并/关闭的 21 条 PR 中包含了多个重要修复（如 #6675 DeepSeek reasoning_content 修复、#6718 应用市场统一、#5597/#5598 LLM Fallback 前后端落地），显示主干推进节奏稳健。社区反馈集中在 **通道稳定性**（WeChat/钉钉）、**MCP 工具调用超时**、**多模型路由** 和 **技能按需加载** 四个方面，其中由 `ChaosG` 提交的多个高质量 Bug 报告（#6707、#6708、#6724）为项目稳定性提供了重要输入。整体健康度良好，但大量待合并 PR（29 条）和新增的多个 v2.1.0b1 回归 Bug 需要维护团队优先跟进。

---

## 2. 版本发布

**无新版本发布**。当前最新版本仍为 v2.1.0-beta.1（近期发布）。注意：今日有两条针对 v2.1.0b1 的回归 Bug 报告（详见第 5 节），建议在下一 beta 版本中优先修复。

---

## 3. 项目进展

今日有 **21 条 PR 被合并/关闭**，其中以下合并对项目有实质性推进：

### 3.1 已合并 PR（实质性推进）

| PR | 标题 | 影响 |
|---|---|---|
| [#5597](https://github.com/agentscope-ai/QwenPaw/pull/5597) | `feat(backend): per-agent and global LLM model fallback with safe retry boundaries` | **核心特性落地**：实现 LLM 调用失败时自动切换备用模型，重试保持在同模型内、仅在明确失败时才切换，避免级联故障 |
| [#5598](https://github.com/agentscope-ai/QwenPaw/pull/5598) | `feat(console): add LLM fallback configuration UI for agent and global models page` | 配套控制台 UI：支持代理级/全局级 fallback 候选列表的增删改、排序与开关 |
| [#6675](https://github.com/agentscope-ai/QwenPaw/pull/6675) | `fix: force relay reasoning_content for DeepSeek models` | **重要修复**：解决 DeepSeek 思考模式多轮对话因上下文压缩丢失 `reasoning_content` 而被上游拒绝的问题（修复 #6667、#6541） |
| [#6718](https://github.com/agentscope-ai/QwenPaw/pull/6718) | `feat: unify app market listings` | 统一应用市场条目，提升市场页的一致性体验 |
| [#6713](https://github.com/agentscope-ai/QwenPaw/pull/6713) | `fix(router): add audit visibility for sensitive directory exclusion` | 增加敏感目录排除的审计可见性，提升安全性 |
| [#5447](https://github.com/agentscope-ai/QwenPaw/pull/5447) | `fix(channel): yield failed AgentResponse on console errors to unblock UI` | 修复控制台通道在模型/运行时错误时 UI 卡在永久等待状态的问题 |

### 3.2 待合并 PR（值得关注）

以下 PR 若合并将显著推进功能版图，目前仍在 review 中：

| PR | 标题 | 看点 |
|---|---|---|
| [#6302](https://github.com/agentscope-ai/QwenPaw/pull/6302) | `feat: unify provider discovery, model metadata, routing, and agent controls` | 统一 Provider 发现、模型元数据、路由与 Agent 控制，对应 #6167，是较大的架构级重构 |
| [#6719](https://github.com/agentscope-ai/QwenPaw/pull/6719) | `feat(chat): add persistent workspace artifact cards` | 对话中自动检测工作区文件变更，生成"工作区工件卡片"并持久化——**与今日新 Issue #6730（artifact canvas）直接呼应** |
| [#6669](https://github.com/agentscope-ai/QwenPaw/pull/6669) | `fix(desktop): stabilize Chrome native messaging and Windows restore locking` | 修复 Windows 端 Chrome 扩展原生消息通信与文件锁冲突问题 |
| [#6715](https://github.com/agentscope-ai/QwenPaw/pull/6715) | `feat(onebot): handle remote inbound voice and image media` | OneBot 通道支持远程 URL 媒体（CDN 语音/图片） |

**整体评估**：项目今日净前进约 2-3 个功能模块（LLM Fallback 全面落地、DeepSeek 兼容性修复、App Market 统一），但 29 条待合并 PR 的持续积压可能拖慢后续节奏。

---

## 4. 社区热点

### 4.1 讨论热度 TOP 3

| 排名 | Issue/PR | 评论数 | 主题 |
|---|---|---|---|
| 1 | [#6684 [enhancement] 增加频道的重试功能](https://github.com/agentscope-ai/QwenPaw/issues/6684) | 4 | 自建 Matrix 频道频繁失联，无自动重试/健康检测，每次重启需手动恢复 |
| 2 | [#6436 [enhancement] 自动模型路由](https://github.com/agentscope-ai/QwenPaw/issues/6436) | 3 | 按消息复杂度自动选择模型：简单轮次用本地小模型、图片用视觉模型、困难推理用大模型 |
| 3 | [#6480 [question] nohup 命令导致 agent 卡住](https://github.com/agentscope-ai/QwenPaw/issues/6480) | 2 | `nohup`/`&` 启动的子进程导致 `execute_shell_command` 永远不返回 idle |

### 4.2 背后诉求分析

- **通道可靠性是最大痛点**：`#6684`（Matrix 断连无重试）连续多日保持活跃，用户的核心诉求是 **"自愈能力"** —— 自动重试、健康检查、故障恢复，而非手动干预。这反映了自托管场景下连接稳定性的强需求。
- **多模型路由呼声渐高**：`#6436` 的诉求是 "不要把所有消息都发给同一个模型"，希望按需智能路由。该 Issue 与待合并 PR `#6302`（统一 Provider/路由）直接相关，但 #6302 目前更侧重架构统一，尚未覆盖自动路由逻辑，路线图信号明显。
- **有 29 条待合并 PR 中，0 条有 reviewer 评论**，说明 review 带宽不足，社区贡献者可能长时间等待反馈。

---

## 5. Bug 与稳定性

### 5.1 严重级（P0/P1，影响核心功能或数据安全）

| 严重度 | Issue | 描述 | Fix PR 状态 |
|---|---|---|---|
| 🔴 P0 | [#6697](https://github.com/agentscope-ai/QwenPaw/issues/6697) | **v2.1.0b1 桌面版注入 PYTHONHOME 到子进程环境，导致所有 python 子进程崩溃**（encodings ModuleNotFoundError） | 无 |
| 🔴 P0 | [#6707](https://github.com/agentscope-ai/QwenPaw/issues/6707) | **含工具调用的会话历史 + thinking-mode 上游 = 400 错误**，`reasoning_content` 转发失败，会话完全不可用 | 有相关 PR [#6721](https://github.com/agentscope-ai/QwenPaw/pull/6721)（retry reasoning-content errors，待合并） |
| 🟠 P1 | [#6726](https://github.com/agentscope-ai/QwenPaw/issues/6726) | **长会话大量工具调用后报 400** "tool must be a response to preceding message with tool_calls"，会话中断 | 无 |
| 🟠 P1 | [#6722](https://github.com/agentscope-ai/QwenPaw/issues/6722) | **后台 fork 子代理在 worktree finalization 失败时仍报告 completed**，提交丢失但状态显示成功（**误导性**） | PR [#6725](https://github.com/agentscope-ai/QwenPaw/pull/6725) 已提交修复 |
| 🟠 P1 | [#6696](https://github.com/agentscope-ai/QwenPaw/issues/6696) | **微信 iLink 一次性 context_token 被打字指示器消耗**，导致回复被拒（ret=-2）且"working"指示器卡住 | 无 |
| 🟠 P1 | [#6700](https://github.com/agentscope-ai/QwenPaw/issues/6700) | **超大工具输出导致历史会话加载卡死**，建议增加输出截断和历史分页 | 无 |

### 5.2 中等级（P2）

| 严重度 | Issue | 描述 | Fix PR 状态 |
|---|---|---|---|
| 🟡 P2 | [#6695](https://github.com/agentscope-ai/QwenPaw/issues/6695) | **仅微信通道时审批提示无法触达**（仅控制台弹窗、5 分钟自动拒绝） | 已关闭，表明已修复（新 Issue #6728 继续跟进中文审批按钮） |
| 🟡 P2 | [#6708](https://github.com/agentscope-ai/QwenPaw/issues/6708) | SSE 流中 503 错误事件不重试直接失败 | PR [#6714](https://github.com/agentscope-ai/QwenPaw/pull/6714) 已提交修复 |
| 🟡 P2 | [#6698](https://github.com/agentscope-ai/QwenPaw/issues/6698) | v2.1.0b1 浏览器 SDK：`open()` 始终 WireProtocolError: Target crashed | 无 |
| 🟡 P2 | [#6690](https://github.com/agentscope-ai/QwenPaw/issues/6690) | cron pause/resume 状态不持久化，重启后丢失 | 已关闭（修复完成） |
| 🟡 P2 | [#6687](https://github.com/agentscope-ai/QwenPaw/issues/6687) | OpenRouter 多模态探测将文档化的能力覆盖为 false | 无 |

### 5.3 已修复/关闭

- [#6690](https://github.com/agentscope-ai/QwenPaw/issues/6690) cron 状态持久化 ✅
- [#6695](https://github.com/agentscope-ai/QwenPaw/issues/6695) 微信审批不可达 ✅
- [#6716](https://github.com/agentscope-ai/QwenPaw/issues/6716) 集成测试确定性失败（关闭为 invalid）✅

---

## 6. 功能请求与路线图信号

### 6.1 高概率进入下版本（已有对应 PR 或明确开发方向）

| 功能请求 | 佐证 |
|---|---|
| **按需加载技能**（[#6699](https://github.com/agentscope-ai/QwenPaw/issues/6699)）：27+ 技能时描述占系统提示 25-30% token，建议懒加载 | 社区关注度高，与 #6650 拆分技能 API 的方向一致；优化空间明确 |
| **MCP 工具调用超时配置**（[#6724](https://github.com/agentscope-ai/QwenPaw/issues/6724)）：当前无超时上限，慢 MCP 服务可无限阻塞 | 已有 1 条评论，`MCPClientConfig` 增 `timeout` 字段的改动较小，易被采纳 |
| **Live artifact canvas**（[#6730](https://github.com/agentscope-ai/QwenPaw/issues/6730)）：控制台侧栏渲染 agent 生成的 HTML 产物 | 与待合并 PR [#6719](https://github.com/agentscope-ai/QwenPaw/pull/6719)（工作区工件卡片）形成互补，若 #6719 合入，此功能是自然的下一步 |

### 6.2 中期路线图信号（社区呼声高但未排期）

| 功能请求 | 分析 |
|---|---|
| **自动模型路由**（[#6436](https://github.com/agentscope-ai/QwenPaw/issues/6436)） | Issue 已存在两周，虽与 #6302 相关但无明确开发计划，适合作为 v2.1 或 v2.2 的候选特性 |
| **频道重试/健康检查**（[#6684](https://github.com/agentscope-ai/QwenPaw/issues/6684)） | 涉及 Matrix 等多种自建通道，核心诉求是自愈能力，建议纳入通道抽象层设计 |
| **智能体级 token 统计**（[#6392](https://github.com/agentscope-ai/QwenPaw/issues/6392)） | 已关闭，但用户明确表达了细粒度 token 统计的需求，社区可能有后续跟进 |

---

## 7. 用户反馈摘要

### 7.1 用户痛点（高频出现）

- **"自愈能力缺失"**：`#6684`（Matrix 断连）和 `#6480`（nohup 卡住）反映了用户在真实业务环境中对 **自动恢复** 的强烈需求。前者提问"每次服务器启动后都需要手动重新保存一次频道才能恢复连接"，后者则报告 "never returns to idle" —— 均与自动化运维场景相关。
- **"工具输出缺乏上限保护"**：`#6700` 的"超大工具输出导致历史会话加载卡死"与 `#6726` 的"大量工具调用后上下文损坏"指向同一个问题：**当前未对工具输出体量做截断或分页**，这在 agent 执行大型操作时会导致会话不可用。
- **"桌面版环境隔离不足"**：`#6697`（v2.1.0b1 PYTHONHOME 注入导致子进程崩溃）和 `#6698`（浏览器 SDK 目标崩溃）表明桌面版的环境隔离与进程管理在 beta 阶段仍需打磨。

### 7.2 用户满意点

- **稳定性在持续改善**：多条 v2.0.1 时期的 Bug（#6690 cron 持久化、#6695 微信审批不可达、#6700 大输出卡死）在今日均已关闭或进入修复通道，用户反馈的整体趋势是 "项目在快速迭代"。
- **零基础用户也能参与修复**：今日有 3 条 `[first-time-contributor]` PR（#6723、#6725、#6675），说明项目的贡献门槛对新手友好，社区生态活跃。

### 7.3 中文用户占比高、反馈质量高

今日 Issue 中约 **40% 为中文反馈**，且质量普遍较高（如 `#6697`、`#6700`、`#6684` 均包含详细的复现步骤、环境信息、截图），建议维护团队保持中文社区支持力度。

---

## 8. 待处理积压

### 8.1 长期未响应的重要 Issue

| Issue | 创建时间 | 标题 | 状态 |
|---|---|---|---|
| [#6684](https://github.com/agentscope-ai/QwenPaw/issues/6684) | 2026-08-04 | 增加频道的重试功能 | 🔴 已 2 天，评论 4 条，无维护者回复 |
| [#6436](https://github.com/agentscope-ai/QwenPaw/issues/6436) | 2026-07-24 | 自动模型路由 | 🟠 已 13 天，评论 3 条，无维护者回复 |
| [#6480](https://github.com/agentscope-ai/QwenPaw/issues/6480) | 2026-07-26 | nohup 命令卡住 | 🟠 已 11 天，评论 2 条，无明确跟进 |

### 8.2 待合并 PR 风险提醒

- 29 条待合并 PR 中，**0 条有 reviewer 评论**，说明 review 带宽不足，部分 PR（如 #6302 架构级重构）已等待 15 天以上（创建于 7-21）。建议维护团队评估是否有足够的 reviewer 资源，或考虑引入社区 reviewer 机制。
- 与 P0 级 Bug [#6707](https://github.com/agentscope-ai/QwenPaw/issues/6707)（thinking-mode 400 错误）直接相关的修复 PR [#6721](https://github.com/agentscope-ai/QwenPaw/pull/6721) 目前处于 OPEN 状态，建议优先 review。

---

## 附：项目健康度总评

| 维度 | 评分（5分制） | 说明 |
|---|---|---|
| **活跃度** | ★★★★★ | 23 Issue / 50 PR，生态活跃，多方贡献者参与 |
| **质量** | ★★★★☆ | 反馈质量高，修复及时，但 P0 级回归（#6697）需优先处理 |
| **维护响应** | ★★★☆☆ | 重要 Issue 有匹配 PR，但长期积压和 0 reviewer 评论值得警惕 |
| **社区健康** | ★★★★☆ | 新手友好，中文社区活跃，但新功能请求响应偏慢 |

---

*本报告由 AI 分析师生成，基于公开 GitHub 数据。如需进一步跟踪特定 Issue 或 PR，请点击链接查看详情。*

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

好的，我是您的 AI 智能体与个人 AI 助手领域开源项目分析师。以下是根据 ZeroClaw 项目在 2026-08-06 的 GitHub 数据生成的项目动态日报。

---

### ZeroClaw 项目动态日报 (2026-08-06)

#### 1. 今日速览

ZeroClaw 项目今日处于**高活跃度**状态，核心焦点集中在**架构演进（RFC讨论）** 与**安全/稳定性加固**。过去24小时内，共有 **39 个 Issue** 和 **49 个 PR** 处于活跃状态，但**合并率极低**（仅1个PR被合并/关闭），大量PR因需要作者响应而停滞。社区讨论主要围绕长周期目标（Goal mode）、Chat Completions API 兼容性等高影响力提案，同时多名贡献者提交了针对安全漏洞（SSRF、shell策略）和资源限制（内存、日志）的修复PR，但均未进入主线。

#### 2. 版本发布

**无新版本发布。**

#### 3. 项目进展

今日合并/关闭的 PR 较少，但仍有值得关注的进展。

- **合并/关闭的 PR:**
  - **[#9750 [CLOSED] fix(service): bound launcher-owned daemon logs](https://github.com/zeroclaw-labs/zeroclaw/pull/9750) (作者: Audacity88)**: 该PR被关闭，而非合并。它旨在通过引入共享的服务管理器，将启动器拥有的守护进程日志文件限制在8 MiB以内，以防止磁盘空间被无限增长的日志占满。**关闭原因未明，但该问题已被作者在新的PR中继续跟进**。

- **活跃 PR 中的功能开发:**
  - **资源限制与稳定性**: PR **[#9773](https://github.com/zeroclaw-labs/zeroclaw/pull/9773)** 正在尝试修复 macOS (launchd) 下的日志无限增长问题，使其与 #9750 的目标保持一致。此外，PR **[#9403](https://github.com/zeroclaw-labs/zeroclaw/pull/9403)** 旨在为 WASM 插件执行添加墙钟时间限制，防止插件运行时失控。
  - **安全加固 (Security Hardening)**: 多项PR专注于修补安全漏洞，包括为 `image_gen` 工具添加 SSRF 防护 ([#8826](https://github.com/zeroclaw-labs/zeroclaw/pull/8826))，加固 Git shell 策略参数 ([#9678](https://github.com/zeroclaw-labs/zeroclaw/pull/9678))，以及在管道中强制实施代理工具策略 ([#9737](https://github.com/zeroclaw-labs/zeroclaw/pull/9737))。
  - **新特性与集成**: 新PR **[#9772](https://github.com/zeroclaw-labs/zeroclaw/pull/9772)** 为 Telegram 频道增加了 `per_user_session` 配置，以解决群组聊天中的会话共享问题。

项目整体虽活跃，但**核心进展受阻**，大量代码等待审查和合并。

#### 4. 社区热点

今日最热门的讨论集中在几个高影响力的 RFC（Request for Comments）上，反映了社区对项目未来架构的深度关注。

- **[#8303 [RFC] Goal mode v1 — bounded foreground Matrix work](https://github.com/zeroclaw-labs/zeroclaw/issues/8303) (评论: 18, 👍: 1)**
    - **诉求**: 作为最高赞和评论数最多的Issue，社区强烈希望 ZeroClaw 能拥有一种持久化机制，在**多轮 Agent 对话中**追求一个有界的目标，而不是仅仅处理单轮指令。这可能是对更复杂、自主的 AI 助手工作流的直接需求。
- **[#8603 [RFC] ZeroClaw Chat Completions profile](https://github.com/zeroclaw-labs/zeroclaw/issues/8603) (评论: 16)**
    - **诉求**: 该 RFC 提议让 ZeroClaw 暴露与 OpenAI Chat Completions 协议兼容的接口。评论区的高热度表明有大量用户希望将 ZeroClaw 接入现有的 OpenAI 生态工具（如 Open WebUI、LobeChat、Continue.dev 等），以降低使用门槛。
- **[#7155 [RFC] Add a per-execution confirmation tier for high-risk shell commands](https://github.com/zeroclaw-labs/zeroclaw/issues/7155) (评论: 16)**
    - **诉求**: 自6月初提出以来，该 RFC 已更新至第三版。用户对于**高风险 Shell 命令**的执行安全非常在意，希望引入更细粒度的确认机制（allow/ask/deny），这体现了在自动化与安全性之间寻求平衡的关键诉求。

#### 5. Bug 与稳定性

今日报告的 Bug 主要集中在内存增长、关键功能失效和配置不一致上。

- **Critical / High (S1/S2)**
    - **[#9775 [Bug] OpenRouter streaming requests drop provider_extra (S1 - workflow blocked)](https://github.com/zeroclaw-labs/zeroclaw/issues/9775)**: **新Bug**。OpenRouter 流式请求会丢失用户配置的 `provider_extra`，可能导致请求失败或功能异常。**暂无关联修复PR。**
    - **[#9774 [Bug] Signal channel silently drops sourceUuid-only senders (S1 - workflow blocked)](https://github.com/zeroclaw-labs/zeroclaw/issues/9774)**: **新Bug**。Signal 频道会静默丢弃来自仅提供 `sourceUuid` 的联系人的消息，影响隐私敏感用户。**暂无关联修复PR。**
    - **[#8642 [Bug] MCP/tool-schema cloning drives unbounded RSS growth in the agent loop](https://github.com/zeroclaw-labs/zeroclaw/issues/8642)**: **老Bug**。MCP工具schema的克隆导致无限内存增长，是WSL2 OOM问题的根源之一。**已被接受，状态为进行中 (in-progress)，暂无明确修复PR。**
    - **[#9768 [Bug] daemon reload is not on SIGUSR1, and the degraded-security warning tells operators to send a signal that kills the daemon](https://github.com/zeroclaw-labs/zeroclaw/issues/9768)**: **新Bug**。文档/警告信息引导用户向守护进程发送错误的信号（SIGUSR1 未绑定重载功能），可能导致进程被杀。**暂无关联修复PR。**

- **Medium (S2/S3)**
    - **[#9697 [Bug] ZeroCode cannot connect to daemon launched by Windows Task Scheduler](https://github.com/zeroclaw-labs/zeroclaw/issues/9697)**: 用户环境集成问题，影响 Windows 用户。
    - **[#9652 [Bug] config set rejects a cron key whose alias contains a hyphen](https://github.com/zeroclaw-labs/zeroclaw/issues/9652)**: **已关闭 (CLOSED)**。配置 CLI 工具存在不一致的行为。

#### 6. 功能请求与路线图信号

除了 RFC，以下新提交的 Issue 也暗示了未来的发展方向：

- **[#9631 [Feature] Send stable session_id to OpenRouter for prompt-cache savings](https://github.com/zeroclaw-labs/zeroclaw/issues/9631)**: 用户请求兼容 OpenRouter 的提示词缓存，以减少成本。这是一个**高价值且实现路径明确**的特性，结合 #9775 的 Bug，OpenRouter 的集成将得到加强。
- **[#9727 [Epic] run and monitor multiple agents from a zerocode sidebar](https://github.com/zeroclaw-labs/zeroclaw/issues/9727)**: 这是一个史诗级任务，目标是让用户能在 ZeroCode 界面中同时运行和监控多个 Agent。这需要大量工作，像是未来版本 (v0.9.0?) 的重大功能。
- **安全与策略**: 多个已接受的 RFC（如 #7155, #7141）表明 v0.9.0 将重点加强**安全性**，包括更细粒度的权限控制和插件化的身份验证。

#### 7. 用户反馈摘要

- **成本敏感**: 用户 ([#9631](https://github.com/zeroclaw-labs/zeroclaw/issues/9631)) 明确抱怨“不必要的昂贵”API调用，希望利用缓存机制减少开销。这反映了真实用户在生产环境中的成本痛点。
- **Windows 体验待改进**: 用户 ([#9697](https://github.com/zeroclaw-labs/zeroclaw/issues/9697)) 报告了在 Windows 计划任务场景下的集成问题，且提到“expected to be resolved”，说明该问题可能是长期存在的。
- **会话与多任务需求**: 关于 Telegram 群聊 ([#9772](https://github.com/zeroclaw-labs/zeroclaw/pull/9772)) 和多 Agent 管理的 ([#9727](https://github.com/zeroclaw-labs/zeroclaw/issues/9727)) 的讨论，表明用户不再满足于单会话、单任务的交互模式，正在迈向更复杂的工作流。
- **安全担忧**: 关于危险命令执行 ([#7155](https://github.com/zeroclaw-labs/zeroclaw/issues/7155)) 和内部文件保护 ([#8424](https://github.com/zeroclaw-labs/zeroclaw/issues/8424)) 的长久高关注度，表明开发者对 AI Agent 的安全边界有很高的要求。

#### 8. 待处理积压

目前有 **49 个 PR 处于待合并状态**，还有大量RFC等待维护者决策。以下是一些需要维护者重点关注的项目：

- **待维护者决策的 RFC 队列**: [**[Tracker] Maintainer decision queue for RFCs**](https://github.com/zeroclaw-labs/zeroclaw/issues/8692) 本身就是一个需要维护者处理的追踪器，目前积压了大量高影响 RFC（如 #8303, #8603, #9487）。
- **重要 PR 停滞**: 多个 PR 因 `needs-author-action` 而停滞，这可能只是作者未响应，但也可能是审查沟通不畅的信号。其中，**`[fix(tool-call-parser)]` ([#9477](https://github.com/zeroclaw-labs/zeroclaw/pull/9477))** 和 **`[fix(anthropic)]` ([#9420](https://github.com/zeroclaw-labs/zeroclaw/pull/9420))** 是修复核心功能或支持重要集成（Anthropic OAuth）的关键 PR，值得优先处理。
- **长期未关闭的 Bug**: 尤其是 **[#8642](https://github.com/zeroclaw-labs/zeroclaw/issues/8642) (MCP内存泄漏)**，作为 OOM 的根源之一，长时间未修复会严重影响用户体验和项目声誉。
- **CI 问题**: [**[Bug] `zeroclaw-plugins` lib unit tests behind the plugins-wasmtime feature never execute in CI**](https://github.com/zeroclaw-labs/zeroclaw/issues/9462) 今日已关闭，但需确认是否已通过正确的方式（如 [PR #9755](https://github.com/zeroclaw-labs/zeroclaw/pull/9755) 中的 CI 增强）得到解决，以防止回归。

</details>

---
*本日报由 [agents-radar](https://github.com/kky-wollu/agents-radar) 自动生成。*