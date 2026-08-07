# OpenClaw 生态日报 2026-08-08

> Issues: 500 | PRs: 500 | 覆盖项目: 13 个 | 生成时间: 2026-08-07 22:41 UTC

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

好的，作为您的 AI 智能体与个人 AI 助手领域开源项目分析师，以下是根据 OpenClaw 项目 GitHub 数据生成的 2026-08-08 项目动态日报。

---

# OpenClaw 项目动态日报 | 2026-08-08

## 1. 今日速览

OpenClaw 项目今日保持高度活跃，过去24小时内 Issue 和 PR 更新均达到500条上限，显示出庞大的社区参与度和维护压力。然而，项目健康度面临严峻挑战：**数据完整性和状态管理是当前最突出的痛点**，多个 P0 级 Bug（如数据库迁移失败、Token 膨胀导致过早压缩）正在阻碍用户升级和使用。尽管新版本发布数为 0，但 PR 队列中有大量针对核心架构（如 Code Mode 栈、Provider 重构）的长期分支等待合并，表明项目正处于深度维护和架构优化期。

## 2. 版本发布

**无新版本发布。**

## 3. 项目进展

*   **核心进展**：虽然今日无 PR 被合并（合并/关闭 PR 占总量的24%），但待合并队列中涌现出多个重量级 PR，预示着未来几天将有重大变更落地。
*   **Code Mode 重构**：由维护者 `vincentkoc` 主导的 **12层 Code Mode 前沿栈** 重构正在持续推进。今日活跃的 PR 包括 `#119237` (桥接生命周期精确核算) 和 `#119056` (强制主机并发不丢弃调用)。这表明项目正在从根本上重构 Codex/Claude CLI 集成的稳定性和资源管理。
*   **Provider 层统一**：PR `#120351` 试图为所有生成媒体（视频、音乐、语音）Provider 建立一个共享的下载保护和二进制响应处理机制，旨在消除重复代码并修复潜在的内存泄漏（未读响应体）。
*   **代码现代化**：PR `#120350` 是一次大规模重构，旨在将核心包中的辅助函数统一迁移到 `normalization-core` 叶子助手，减少策略重复和语义漂移。
*   **自动化修复**：`clawsweeper[bot]` 持续自动生成 PR（如 `#119731`），尝试绑定任务完成结果提示的长度，这为解决某些上下文溢出问题提供了自动化的修复路径。

## 4. 社区热点

*   **#116277 (Closed): DeepSeek v4 Flash 静默回复失败** (125条评论)
    *   **链接**: [Issue #116277](https://github.com/openclaw/openclaw/issues/116277)
    *   **分析**: 这是过去24小时讨论最激烈的问题。用户遭遇模型静默失败并收到通用兜底回复，严重影响了核心聊天体验。虽然该 Issue 已被关闭，但高评论数表明用户对“静默失败”和“回复丢失”的容忍度极低，大家关心的是如何避免此类问题以及失败时的补救机制。这与“Message Loss”和“UX Friction”标签相符。

*   **#101290 (Open): CLI 启动预检损坏活动状态数据库** (14条评论)
    *   **链接**: [Issue #101290](https://github.com/openclaw/openclaw/issues/101290)
    *   **分析**: 这是一个 P0 级数据损坏问题，被评为“Diamond Lobster”。用户报告的 `database disk image is malformed` 错误是灾难性的，因为它直接导致会话状态丢失。14条评论集中在排查根因，社区倾向于认为是 CLI 预检与运行中网关的并发访问冲突所致。这反映了用户对本地数据安全的高度关切。

*   **#85030 (Open): MCP 工具未注入子代理会话** (10条评论, 6 👍)
    *   **链接**: [Issue #85030](https://github.com/openclaw/openclaw/issues/85030)
    *   **分析**: 此问题获得较高点赞，说明有相当一部分高级用户依赖 MCP (Model Context Protocol) 生态。该 Bug 导致 `sessions_spawn` 生成的子代理无法使用配置的 MCP 工具，这严重限制了子代理的自主能力和复杂任务的执行。用户诉求是希望子代理能继承主会话的能力边界。

## 5. Bug 与稳定性

**P0 级 (严重)**：
*   **#119263**: Agent DB v14->v15 迁移失败 (`no such column: entry_valid`)，导致网关拒绝启动。**已有相关联的 PR 开放**（`clawsweeper:linked-pr-open`）。这是一个升级阻断器，影响所有从 2026.7.1 升级的用户。
*   **#118772**: `sessionEntry.totalTokens` 膨胀导致过早压缩（在上下文窗口的 4-8% 时触发），造成数据丢失。**已有相关联的 PR 开放**。这是 2026.7.1 引入的回归，严重影响长会话的连续性。
*   **#101290**: CLI 启动预检可以损坏活动网关正在使用的 SQLite 数据库。**暂无明确的修复 PR**。

**P1 级 (高)**：
*   **#118785**: 容器和外部应用 SDK 的 QA 验证积压，影响发布信心。
*   **#94939**: 6.x 状态迁移导致 MS Teams 频道会话存储为空，破坏主动消息发送。**已有相关联的 PR 开放**。
*   **#53408**: 长对话后 Write/Exec 工具参数被静默丢弃。**已有 PR `#120248` 声称修复了 Amazon Bedrock Provider 的此问题**，但根因可能不止于此。
*   **#86684**: `sessions_yield` 子代理唤醒可在低上下文占用时压缩父分支，导致父会话状态丢失。**已有相关联的 PR 开放**。
*   **#45494**: 在 LLM API 持续故障期间，Cron 任务静默超时而非快速失败，导致任务积压和结果延迟。**暂无明确的修复 PR**。

**P2 级 (中)**：
*   **#119796**: Windows 平台 vitest 测试拆除时 EBUSY 错误，属于测试基础设施问题。**已有相关联的 PR 开放**。
*   **#97616**: 钩子/工具子进程未被回收，导致僵尸进程积累和运行时性能下降。

## 6. 功能请求与路线图信号

*   **#45608 (Open)**: **预重置智能体记忆刷新**。该请求希望 `/new` 和每日重置也能像上下文压缩那样，在执行破坏性操作前运行一次记忆刷新。这一高赞（4 👍）请求如果实现，将显著提升跨会话记忆的连续性。结合现有的记忆索引重构 PR（#95724），这可能成为未来版本的一个重点方向。
*   **#99583 (Open)**: **智能会话自动命名**。提议利用已有的 LLM 生成器为会话懒生成、主题感知的标题，减少手动管理成本。这符合提升 UX 的趋势。
*   **#81061 (Open)**: **预路由入站消息钩子 (`before_route_inbound_message`)**。该需求为插件系统增加了一个前置路由拦截点，是实现频道桥接、代理和复杂消息处理的关键能力，有 3 👍。这暗示了社区正在构建更复杂的自动化工作流。
*   **#119256 (Open)**: **WhatsApp 投票结果钩子**。为 `@openclaw/whatsapp` 增加 `poll_vote_received` hook，补齐了创建和读取投票的能力闭环。这是一个具体的、针对性强的功能增强。

## 7. 用户反馈摘要

*   **对数据丢失零容忍**：从多个 P0/P1 Issue (#101290, #118772, #94939) 中可以看出，用户对任何形式的状态损坏、迁移失败或静默数据丢失都表现出极大的焦虑和不满。“数据库损坏”和“会话消失”是引发强烈情绪的关键词。
*   **“静默失败”是糟糕的体验**：多个 Issue (#116277, #53408, #86012) 都指向了“静默失败”问题——模型不回复、工具参数被丢弃、消息被静默丢失。用户表示，比起失败本身，**“没有任何反馈的失败”** 更令人困扰，这让他们无法判断是操作失误还是系统故障。
*   **对子代理能力的期待**：关于 MCP 工具未注入 (#85030) 和子代理完成投递错误 (#118018) 的讨论，反映出用户不仅仅将子代理视为简单的任务执行者，而是期待其具备与主代理相当的工具和上下文能力。
*   **对维护者的认可**：尽管问题繁多，但用户也在评论中表达了对维护者工作的认可，尤其是在 Issue #95601 中，一位 VoiceOver 用户特别感谢了团队在无障碍访问（屏幕阅读器）方面的改进。

## 8. 待处理积压

*   **#30381 (Open)**: `chatCompletions` 端点应忽略请求体中的 `model` 字段（当 `x-openclaw-agent-id` 头存在时）。这是一个创建于3月1日的“Diamond Lobster”级问题，已等待超过5个月。它影响到 OpenAI 兼容客户端的灵活性，急需维护者给出产品决策（`needs-product-decision`）。
*   **#75380 (Open)**: `provider-payload.jsonl` 和 `cache-trace.jsonl` 日志文件无限制增长。该问题自5月1日提出，被标记为安全影响和高优先级，但至今仍需产品决策。长期不处理可能导致用户磁盘空间耗尽。
*   **#91931 (Open)**: 预置的 SOUL.md/IDENTITY.md/USER.md 会触发自动完成引导并删除用户提供的 BOOTSTRAP.md。这是一个数据丢失风险较高的行为问题，涉及新用户首次体验，且已有 PR 开放 (#91931 关联)，但合并进度缓慢。
*   **#89287 (Open)**: 验证完成投递目标的 PR，创建于6月2日，目前仍标记为“需要验证”。虽然它解决了子代理完成通知的准确性问题，但长时间未合并可能意味着它处理的是边缘情况，或与更大的架构改动冲突。

---
**结论**：OpenClaw 项目正处于社区活跃度和技术债务的高峰期。短期内，维护者的首要任务是解决 **P0 级数据完整性** 问题，以恢复用户信任。中长期来看，**Code Mode 重构** 和 **Provider 统一** 的落地将决定平台的稳定性和可扩展性。社区反馈强烈指向“可靠性和可预测性”是当前最核心的诉求。

---

## 横向生态对比

# 个人 AI 助手开源生态横向对比分析报告

**报告日期：** 2026-08-08  
**数据覆盖：** 10 个核心项目（含 3 个无活动项目）  
**分析师视角：** 技术决策者与开发者


## 1. 生态全景

个人 AI 助手/自主智能体开源生态正处于**从功能竞争转向稳定性和安全性的关键转折期**。头部项目（OpenClaw、Hermes Agent、IronClaw、ZeroClaw）均面临 P0/P1 级数据完整性与状态管理挑战，反映出行业普遍存在的"快速迭代累积技术债"问题。与此同时，**安全加固**（会话隔离、路径逃逸防护、密钥清理）和**配置健壮性**（YAML 解析陷阱、损坏配置容错）成为多个项目共同的主攻方向。生态分化明显：通用型平台（OpenClaw/IronClaw）与垂直型工具（PicoClaw/LobsterAI）各占其位，前者重架构扩展，后者重场景落地。总体上，生态处于**高度活跃但工程质量参差不齐**的成长期。

## 2. 各项目活跃度对比

| 项目 | Issues 更新 | PR 更新 | 合并/关闭 PR | 新版本 | 今日健康度 | 核心特征 |
|------|------------|---------|-------------|--------|-----------|---------|
| **OpenClaw** | 500（达上限） | 500（达上限） | 24% | 无 | ⚠️ 高活跃/高压力 | 数据完整性 P0 问题突出，Code Mode 重构 |
| **Hermes Agent** | 50 | 50 | 7 | 无 | ✅ 健康 | P1 缺陷同日修复，配置陷阱批量处理 |
| **IronClaw** | 50 | 50 | 14 | 无 | ✅ 健康 | 文档漂移治理，状态感知 Bug 集中 |
| **ZeroClaw** | 50 | 50 | 3 | 无 | ⚠️ 高活跃/安全压力 | 6+ P1，Web 工具面收敛，品牌统一 |
| **NanoBot** | 10 | 21 | 11 | 无 | ✅ 健康 | 会话安全架构调整，WebUI 打磨 |
| **CoPaw** | 79（总量） | 79（总量） | 0 | **v2.1.0-beta.2** | ⚠️ 功能快/稳定性低 | Windows 安装问题，MCP 失效 |
| **PicoClaw** | 少量 | 少量 | 2 | 无 | ✅ 稳健 | PR 积压（Dependabot 占比高） |
| **NanoClaw** | 0 | 12 | 2 | 无 | ✅ 良好 | 渠道集成扩展，技能生态建设 |
| **LobsterAI** | 少量 | 6 | 6 | **2026.8.7** | ✅ 稳定 | Cowork 模块迭代，老 Issue 清理 |
| **NullClaw/TinyClaw/Moltis/ZeptoClaw** | 0 | 0 | 0 | 无 | ⚪ 无活动 | 24h 内无活跃 |

> **说明**：活跃度判断依据为 Issue/PR 更新量、修复效率、响应速度及积压情况综合评估。

## 3. OpenClaw 在生态中的定位

**优势：**
- **社区规模断层第一**：Issue/PR 更新量达到 GitHub 500 条上限，是第二梯队（50 条）的 10 倍以上，生态参与度无出其右
- **架构前瞻性**：Code Mode 12 层栈重构、Provider 统一、记忆索引重构等均是生态内最深入的架构级改造
- **自动化和工具链成熟**：`clawsweeper[bot]` 自动修复 PR 已形成流水线，领先其他项目

**技术路线差异：**
- 相比 IronClaw/ZeroClaw 的 Rust 路线，OpenClaw 的 TypeScript 全栈对 Web 开发者更友好
- 相比 Hermes Agent 的 Gateway 多平台模式，OpenClaw 更侧重单实例深度自治

**明确短板：**
- **数据完整性风险**：DB 迁移失败、token 膨胀、SQLite 损坏三大 P0 问题同时存在，已影响升级信心
- **维护压力过大**：500 条上限意味着维护者可能无法及时响应用户需求

**结论**：OpenClaw 仍居生态核心位置，但正处于**规模带来红利与负担的双刃剑阶段**，短期稳定性修复的优先级高于新功能开发。

## 4. 共同关注的技术方向

| 技术方向 | 涉及项目 | 具体诉求 |
|---------|---------|---------|
| **子代理/子会话能力边界** | OpenClaw（#85030 MCP 工具未注入子代理）、NanoBot（PR #5291 子代理对话持久化）、Hermes Agent（#81267 子代理 SessionDB 共享缺陷） | 子代理需继承主会话的工具权限、上下文记忆和会话隔离机制，当前普遍实现不完整 |
| **数据完整性保障** | OpenClaw（#101290 数据库损坏、#118772 token 膨胀）、IronClaw（#7380 持久化兼容性 epic）、LobsterAI（#1273 sql.js 内存崩溃） | 迁移失败、静默丢失、状态损坏是跨项目公敌，需要**事务性写入 + 迁移前验证 + 失败回滚**三管齐下 |
| **配置解析健壮性** | Hermes Agent（#81348 `bool("false")` 陷阱）、ZeroClaw（#9828 配置编辑安全通道）、CoPaw（#6806 配置保存失败）、PicoClaw（#3319 `exec` 参数误处理） | 手写配置/环境桥接下的类型解析错误、静默丢弃、越权修改是普遍痛点 |
| **"静默失败"治理** | OpenClaw（#116277、#53408）、ZeroClaw（#9786、#9783）、NanoBot（#5256 重复回复） | 模型/工具/定时任务失败时无反馈或误报成功，用户普遍要求"明确的失败优于自信的错误" |
| **安全边界与沙箱** | NanoBot（#5278/#5279/#5283 会话隔离）、ZeroClaw（#9815 forbidden_paths 失效、#9827 shell 逃逸）、IronClaw（#7295 DM 身份混淆） | Agent 文件系统越权、路径逃逸、跨会话数据泄露是安全加固的核心场景 |
| **跨平台/跨渠道会话延续** | Hermes Agent（#4335 CLI↔Telegram 共享上下文）、PicoClaw（#3307 多渠道会话管理）、LobsterAI（#1265 多 Agent 绑定不同机器人） | 用户期望在不同 IM/平台间延续对话上下文和 Agent 配置，当前各平台 session store 互相隔离 |

## 5. 差异化定位分析

| 项目 | 功能侧重 | 目标用户 | 技术架构关键差异 |
|------|---------|---------|----------------|
| **OpenClaw** | 全功能通用个人 AI 助手 | 技术爱好者/重度自托管用户 | TypeScript 全栈，Code Mode 深度集成，插件生态庞大 |
| **Hermes Agent** | 多平台消息网关 + 桌面应用 | 跨 IM 重度用户/远程工作者 | Gateway 架构，多 channel 接入，Electron 桌面端 |
| **IronClaw** | 自主智能体 + 自动化例行任务 | 自动化追求者/开发者 | Rust 实现，doc-truth 契约测试，双通道投递模型 |
| **ZeroClaw** | 安全优先 + Web 工具面收敛 | 安全意识强的开发者 | Rust + WASM，`forbid(unsafe_code)` 目标，SOP 引擎 |
| **NanoBot** | 轻量高效 + 会话安全 | 轻量部署/隐私敏感用户 | 架构简洁，会话级沙箱隔离，短期快速迭代 |
| **CoPaw** | 多功能聚合 + 桌面体验 | 普通用户/桌面端使用者 | Electron + Web 工作区，ReMe 记忆功能，插件市场 |
| **PicoClaw** | 轻量本地 + 多渠道 | 嵌入式/边缘设备用户 | Go 实现，WebRTC 支持，国内渠道（钉钉/微信）集成 |
| **NanoClaw** | 渠道扩展 + 技能生态 | 团队协作用户 | ChannelAdapter v2，Agent 模板系统 |
| **LobsterAI** | 办公场景 + OpenClaw 集成 | 企业/半专业用户 | Cowork 模块，OpenClaw 配置管理，Windows 优先 |

## 6. 社区热度与成熟度

**第一梯队：规模庞大，快速迭代（OpenClaw）**  
社区参与度极高（Issue/PR 达上限），但维护压力大，P0 问题影响信任度。处于**功能扩展 → 稳定性优先**的转型期。

**第二梯队：活跃度高，质量收尾（Hermes Agent、IronClaw、ZeroClaw、CoPaw）**  
- **Hermes Agent**：修复效率高（P1 同日提交修复），但 P2/P3 积压累积
- **IronClaw**：RC 发布后集中质量收尾，文档治理值得借鉴
- **ZeroClaw**：安全加固力度大，但 6+ P1 暴露质量保障压力
- **CoPaw**：功能迭代快但稳定性差（Windows 安装/误报/插件故障）

**第三梯队：稳定推进，局部优化（NanoBot、PicoClaw、NanoClaw、LobsterAI）**  
- **NanoBot**：安全架构调整领先，维护响应速度快
- **PicoClaw**：贡献质量高但 PR 积压需加速审查
- **NanoClaw**：核心团队主导路线图，渠道/技能方向明确
- **LobsterAI**：节奏稳定，但老 Issue 关闭后缺乏明确解决方案

**第四梯队：无活动（NullClaw、TinyClaw、Moltis、ZeptoClaw）**  
24h 内完全无动态，可能处于休眠、迁移或维护间歇期。

## 7. 值得关注的趋势信号

**1. "状态感知真实性"是下一代 Agent 的核心竞争力**  
IronClaw 的 5 个 P1 Bug（Agent 虚构自动化状态、错认连接状态、遗留记忆）和 OpenClaw 的"静默失败"问题共同指向：**用户对"自信的错误"容忍度极低**。能够准确报告自身状态的 Agent（何时连接、何时执行、何时失败）将成为体验分水岭——这不仅是工程问题，更是产品设计原则。

**2. 配置系统的"防呆"与"可逆"需求爆发**  
Hermes Agent 的 YAML 解析陷阱、ZeroClaw 的配置编辑安全通道、IronClaw 的"无重置模型设置"、CoPaw 的配置保存失败——多个项目不约而同地面临配置可靠性危机。**配置即代码的工程化（schema 校验、版本控制、原子写入、回滚机制）** 将成为 Agent 平台的标配能力。

**3. 子代理/多 Agent 协作从概念走向工程化**  
NanoBot 的子代理持久化、OpenClaw 的 MCP 工具注入问题、LobsterAI 的多 Agent 绑定不同机器人需求——说明用户已不满足于单 Agent 对话，而是探索**任务分解、工具继承、上下文共享、跨 Agent 协作**的复杂工作流。这将是下一阶段的核心技术赛道。

**4. 渠道打通从"接入"到"一致性"**  
Hermes Agent 的跨平台会话共享（128 天未响应）、PicoClaw 的多渠道会话管理、IronClaw 的双通道投递模型——**跨 IM/平台的无缝体验**是用户持续关注但尚未被充分满足的刚需。

**5. 安全从"功能安全"到"数据主权"**  
NanoBot 的会话级沙箱隔离、ZeroClaw 的 shell 逃逸修复、IronClaw 的身份混淆——**Agent 能接触什么数据、能执行什么操作**正在成为用户选择平台的关键决策因素。安全不再是加分项，而是底线。

**6. 可观测性与成本透明化是信任基石**  
NanoBot 的 token 消耗追踪需求、ZeroClaw 的成本上报 Bug、IronClaw 的 token 估算偏差——用户对 Agent 的**资源消耗透明度**要求显著提升。精确的用量追踪和成本可视化将成为企业级采用的前提。

---

*报告结束。本报告由 AI 分析生成，数据来源为各项目 GitHub 公开仓库。*

---

## 同赛道项目详细报告

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot 项目动态日报 — 2026-08-08

## 1. 今日速览

NanoBot 项目过去 24 小时活跃度处于**高位**，共产生 10 条 Issue 更新和 21 条 PR 更新，其中 11 条 PR 已合并/关闭，显示维护节奏紧凑。核心看点集中在**会话安全架构调整**：两条安全相关的 Issue（#5278 会话历史存放位置安全隐患）及对应 PR（#5279 将会话迁移出工作区、#5283 非 WebUI 通道按会话隔离沙箱）同日跟进，表明团队对 Agent 文件系统越权风险高度重视。此外，WebUI 侧连续合入 6 条修复/重构 PR，覆盖媒体附件签名、路由稳定性与 UI 细节，项目整体稳健推进。社区侧 Telegram 贴纸支持（#5289）和 token 消耗追踪（#5266）分别获得 0 和 10 条评论，后者暂无 👍 标记但讨论热度最高。

---

## 2. 版本发布

过去 24 小时无新版本发布。

---

## 3. 项目进展

今日合并/关闭的 11 条 PR 分布在多个方向，重点如下：

**安全架构（今日最显著推进）**
- **[PR #5279](https://github.com/HKUDS/nanobot/pull/5279) — [closed] fix(session): store session history outside the agent workspace**：将会话历史文件从 `<workspace>/sessions/` 迁出，解决 agent 文件工具可读/列目录越权读取会话记录的问题，呼应 Issue #5278。
- **[PR #5283](https://github.com/HKUDS/nanobot/pull/5283) — [open] feat(workspace): per-session sandbox isolation for non-WebUI channels**：新增 `per_session_sandbox` 选项，非 WebUI 会话各自获得独立沙箱目录，agent 文件工具限定在该目录内。

**WebUI 修复与打磨（合入 6 条）**
- [PR #5268](https://github.com/HKUDS/nanobot/pull/5268) — 历史读取时对 media root 之外附件进行 staging，修复刷新后媒体 URL 丢失（对应 Issue #5264）。
- [PR #5285](https://github.com/HKUDS/nanobot/pull/5285) — 修复新建对话路由在乐观更新与列表确认间的丢失。
- [PR #5284](https://github.com/HKUDS/nanobot/pull/5284) — 移除无人调用的旧版 `/api/sessions/{key}/messages` 路由，简化维护面。
- [PR #5281](https://github.com/HKUDS/nanobot/pull/5281) — 修复活动指示器文本在渐变遮罩下的模糊问题。
- [PR #5277](https://github.com/HKUDS/nanobot/pull/5277) — 模型预设编辑器支持行内展开，提升配置效率。
- [PR #5287](https://github.com/HKUDS/nanobot/pull/5287) — 修复渠道默认发送进度提示被覆盖的回归。

**会话与记忆**：PR #5272 修复会话裁剪时丢弃主动推送消息的回归（对应 Issue #5273）；PR #5280 让短会话也能为 Dream 归档 `history.jsonl`；PR #5231 补充 idle 会话归档能力；PR #5282 更新依赖恢复指引至插件命令。

**总体评估**：今日合入内容覆盖安全、WebUI、渠道稳定性、记忆归档四大块，项目在**安全性**与**会话完整性**两个维度有明显进步。

---

## 4. 社区热点

**[Issue #5266](https://github.com/HKUDS/nanobot/issues/5266) — [OPEN] token 消耗日志（10 评论）**  
用户 knoppix2 报告 nanoBot 在无明显交互下 2 小时消耗约百万 token，诉求是记录每次调用的 token 用量以便追踪。这是成本控制类需求，目前无 👍 标记但评论数居首，反映部分用户对资源消耗透明度有需求。

**[Issue #5149](https://github.com/HKUDS/nanobot/issues/5149) — [OPEN] WhatsApp 无音频输出（5 评论）**  
已持续 10 天，用户反映 nanoBot 无法在 WhatsApp 上发送音频文件（可接收），日志显示 neonize 相关警告。连续评论但尚未有对应 fix PR。

**[Issue #5198](https://github.com/HKUDS/nanobot/issues/5198) — [OPEN] 会话内模型切换失效（3 评论）**  
用户发现 `/model` 命令无法在已有会话内更新模型，只能全局重配置。属交互体验问题，无对应 PR 关联。

**趋势**：最热议题集中在**资源可观测性**与**渠道功能完整性**，安全问题讨论虽不多但已迅速转成 PR，说明维护方响应偏好明显。

---

## 5. Bug 与稳定性

按严重程度排列：

| 严重度 | Issue | 描述 | 状态 |
|--------|-------|------|------|
| 高 | [#5278](https://github.com/HKUDS/nanobot/issues/5278) | 会话历史存放于 agent 工作区内，agent 可越权读取全部会话记录 | 已有 [PR #5279](https://github.com/HKUDS/nanobot/pull/5279) 修复 |
| 中 | [#5256](https://github.com/HKUDS/nanobot/issues/5256) | `/goal` 指令产生数十条重复回复，直至用户干预或模型自动终止 | 待处理 |
| 中 | [#5149](https://github.com/HKUDS/nanobot/issues/5149) | WhatsApp 无法发送音频（neonize 相关） | 待处理，持续 10 天 |
| 中 | [#5198](https://github.com/HKUDS/nanobot/issues/5198) | 会话内无法切换模型，`/model` 命令无效 | 待处理 |
| 低 | [#5264](https://github.com/HKUDS/nanobot/issues/5264) | 历史接口不返回 media_root 之外文件的 media_urls | 已由 [PR #5268](https://github.com/HKUDS/nanobot/pull/5268) 修复 |
| 低 | [#5273](https://github.com/HKUDS/nanobot/issues/5273) | 会话裁剪丢弃主动推送消息 | 已由 [PR #5272](https://github.com/HKUDS/nanobot/pull/5272) 修复 |

另有 [PR #5156](https://github.com/HKUDS/nanobot/pull/5156) 仍在开放状态，修复 Telegram 轮询静默停止问题，对应 Issue #5171。该 PR 已挂 9 天，值得关注。

---

## 6. 功能请求与路线图信号

- **[PR #5279](https://github.com/HKUDS/nanobot/pull/5279) + [PR #5283](https://github.com/HKUDS/nanobot/pull/5283) — 会话级隔离**：Issue #5276 提出基于会话的临时文件隔离需求，PR #5283 即为对应实现（含 `per_session_sandbox` 参数），且 #5279 解决会话历史迁出。**两者大概率进入下个版本**。
- **[PR #5288](https://github.com/HKUDS/nanobot/pull/5288) — Agent Plugins 与 CLI Apps 整合**：将插件包格式统一接入 CLI 目录，改善可移植性，体现平台化方向。
- **[PR #5291](https://github.com/HKUDS/nanobot/pull/5291) — 子代理对话持久化**：保留完整思考链路，审计与调试场景友好。
- **[Issue #5289](https://github.com/HKUDS/nanobot/issues/5289) — Telegram 贴纸与消息反应**：已作为 feature 提案，但暂无对应实现 PR。对比评论区互动，值得关注。
- **[PR #5252](https://github.com/HKUDS/nanobot/pull/5252) — 临时聊天模式**：WebUI 不落盘的多轮临时对话，适合测试场景。
- **[PR #4276](https://github.com/HKUDS/nanobot/pull/4276) — 模型无关的 computer use + browser 工具**：已开放 59 天未见合并，若方向被认可，将是 Agent 能力的重要扩展。

---

## 7. 用户反馈摘要

- **资源消耗焦虑**（#5266）：用户称"百万 token / 2 小时"且"用户无感知"，希望有调用粒度的 token 日志。属于可观测性诉求，建议在 Release 说明中补充 Log 配置指引。
- **音频能力缺失**（#5149）："问它发送任何音频文件，没有反应"——渠道能力（WhatsApp）不完整影响实际使用。
- **交互限制**（#5198）："无法在会话中切换模型，除非重配整个实例"——灵活的模型切换对多模型用户是刚需。
- **会话数据安全**（#5278）：用户担心 agent 可读所有会话历史，属于"默认机制引以为忧"类反馈——虽然 workspace 的读写是预期设计，但对会话数据的边界需明确。
- **Telegram 贴纸需求**（#5289）：用户希望支持发送贴纸及 Agent 主动消息反应，社区对渠道功能丰富度有期待。

---

## 8. 待处理积压

| 项目 | 类型 | 持续天数 | 说明 |
|------|------|---------|------|
| [PR #4276](https://github.com/HKUDS/nanobot/pull/4276) | 功能 | 59 天 | 模型无关 computer use / browser 工具，能力跨度大，需维护者评估方向 |
| [PR #5156](https://github.com/HKUDS/nanobot/pull/5156) | Bug 修复 | 9 天 | Telegram 轮询静默停滞，线上稳定性风险，建议优先处理 |
| [Issue #5149](https://github.com/HKUDS/nanobot/issues/5149) | Bug | 10 天 | WhatsApp 音频发送缺失，无对应 PR，需确认修复排期 |
| [Issue #5198](https://github.com/HKUDS/nanobot/issues/5198) | Bug | 8 天 | 会话级模型切换不可用，交互体验问题，评论中已有复现路径 |

---

**总结**：NanoBot 项目今日处于**高频迭代 + 安全加固**状态。11 条合并的 PR 中多数是小步快跑的修复与重构，两条安全相关的 PR（#5279 + #5283）则代表架构级改进。主要风险点是 Telegram/WhatsApp 两个渠道的稳定性问题仍悬而未决，建议维护方将 #5156 的合并优先级提高。整体项目健康度良好，社区活跃度与维护响应速度都在健康区间。

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent 项目动态日报 — 2026-08-08

## 1. 今日速览

项目今日整体活跃度处于**高位**。过去 24 小时内有 50 条 Issue 更新（新开/活跃 47，关闭 3）与 50 条 PR 更新（待合并 43，合并/关闭 7），虽无新版本发布，但出现了 **P1 级紧急缺陷的快速修复响应**（#81343 修复 PR 与 #81267 问题报告同日提交），以及一批 **P2 级 "quoted false" 配置陷阱批量修复**。核心基础设施（桌面端、Telegram、终端工具、Cron 调度）均有多项修复落地。值得关注的是，多个 P2 级 Bug 已出现对应 fix PR，修复管线运转效率较高。此外，社区活跃度呈健康分布，既有长期挂起的老问题（#26006 已持续近 3 个月），也有大量当日新提交的 Issue 和 PR，说明项目处于快速迭代期。

---

## 2. 版本发布

无新版本发布。

---

## 3. 项目进展

今日共 **7 个 PR 被合并/关闭**，其中 2 个值得重点关注：

### 已合并

- **[#73249] fix(auth): preserve explicit credential status resets** — 修复凭证池持久化时显式状态重置丢失的问题，核心改动是让显式重置只绕过 new-on-disk 冷却合并、且仅在状态字段全部清除时生效，同时保留陈旧写入保护。这对多设备/多 profile 部署场景下的 OAuth 令牌轮换至关重要，直接消除了一个问题根源。
  [PR #73249](https://github.com/NousResearch/hermes-agent/pull/73249)

- **[#21683] fix: guard BlueBubbles sends with contact book** — 通过要求 BlueBubbles 目标精确匹配通讯录 ID/显示名/别名，直接电话号码须精确匹配已验证的 allow_outbound DM 句柄，**收紧了一个潜在的消息投递安全边界**。此改动存在了约 3 个月才合并，较反常，建议关注是否有额外审查环节。
  [PR #21683](https://github.com/NousResearch/hermes-agent/pull/21683)

### 值得注意的待合并 PR

- **#81343** — 修复子代理共享父 SessionDB 导致 use-after-close 的 P1 缺陷
- **#81348** — 修复 Cron 配置中 quoted `'false'` 被当作 `True` 的陷阱
- **#81347** — 修复终端复合命令后台化重写产生的 bash 语法错误

---

## 4. 社区热点

| 排名 | 标题 | 类型 | 评论数 | 热度信号 |
|------|------|------|--------|----------|
| 1 | **Desktop app becomes completely unresponsive after ~5 messages on macOS 27 beta** | Bug | 13 | 桌面端完全冻结，影响设置，无恢复手段，macOS beta 用户 |
| 2 | **Cross-platform session context sharing (CLI ↔ Telegram)** | Feature | 12 | 👍 3，跨平台会话共享需求，已开放 4+ 个月仍有热度 |
| 3 | **Hermes decomposition SL3-alpha: Writer primitives, attempt fencing, and public parity** | Epic | 8 | 项目内部自动分解的复杂任务，规划迭代多轮 |
| 4 | **WhatsApp Feature Parity & Alignment Campaign** | Meta-issue | 6 | WhatsApp 平台功能对齐运动，涉及多子任务 |
| 5 | **Hermes decomposition SL5: Goal turn markers, charge ledger, and fallbacks** | Epic | 7 | 内部自动化任务分解，rev 6/7 仍在调整 |

**Top 1 深度分析** (#63047)：**macOS 27 beta 上桌面应用在约 5 条消息后完全无响应（包括设置）**，这已是长达 27 天的老问题。用户描述为 "almost full UI freeze"（不只是输入延迟），唯一的恢复手段含糊不清（"hoping on some defreeze"），显然体验极差。同类桌面端恢复问题还包括 #79105（流式响应时滚动锁死），这些 Bug 反复出现引发了「桌面端响应流畅度」的系列社区讨论。

**Top 2 深度分析** (#4335)：**跨平台会话上下文共享（CLI ↔ Telegram）** 已开放 4 个多月、获得 3 个 👍，其核心痛点是 Hermes 的 Gateway 架构下各平台 session store 互相隔离，用户无法在不同平台间延续上下文。做为一个 P3 + needs-decision 的长期 Feature Request 仍保持高热度，说明有一定数量的用户在等待此能力的落地化。

---

## 5. Bug 与稳定性

### 🔴 P1 级

- **#81267** — Cron + 后台 delegate_task 共享 SessionDB 导致子代理 transcript 静默丢失，completions 无法路由。**✅ 已有修复 PR #81343（同日提交）**，但在合并前请关注是否需要 workaround。
  [Issue #81267](https://github.com/NousResearch/hermes-agent/issues/81267) · [PR #81343](https://github.com/NousResearch/hermes-agent/pull/81343)

### 🟠 P2 级

- **#81322** — `lifecycle_guard` 对 ELF 二进制路径抛 `embedded null byte` 错误，导致合法终端命令被拒绝。**无 fix PR**。
- **#80989** — v0.20.0 终端/澄清工具结果被 content-block 结构包裹，有时返回错误文件内容。**无 fix PR**。
- **#78993** — `relay_runtime.pop()` TypeError 导致 Gateway 内存泄漏，SWAP 打满 100%。**无 fix PR**（需复现）。
- **#81314** — Shell hooks 在桌面端不生效，因 `serve` 被排除在 `_AGENT_COMMANDS` 之外。**无 fix PR**，但与 #41457 同根因，建议维护者考虑合并处理。
- **#53329** — 非 git 项目文件夹在侧边栏显示重复 lane。**无 fix PR**。
- **#75801** — OpenCode Go gpt-5.6-luna 流式响应缺 `finish_reason` 导致 4 次假断流重连，且桌面端把完整回答裁掉。**无 fix PR**。
- **#78190** — Gmail MCP HTTP OAuth 在 CLI 下正常但 Gateway 进程内报 `OAuthRegistrationError: Registration failed 404`。**无 fix PR**。
- **#80439** — 自动生成的 hermes.desktop `Exec` 路径错误，破坏 KDE 任务栏固定（用户侧已发现 2 天）。**无 fix PR**。
- **#80184** — Windows 启动时 WSL 探测提示和 simple-git 自定义二进制警告噪音，看起来像崩溃。**✅ 有 PR #79250（修复告警 spam，待合并）**。
- **#41457** — Shell hooks 在桌面端（TUI gateway）和 ACP adapter 中未注册，`pre_tool_call` 静默失效。**无 fix PR**。

### 🟡 P3 级（精选）

- **#79001** — 桌面端从 state.db 删除会话后 localStorage 未同步清理，导致启动时 404。**无 fix PR**。
- **#79183** — 预览面板拖拽分隔条时面板收缩/塌陷。**无 fix PR**。
- **#78486** — 桌面端流式回复时视图跳转到历史消息。**无 fix PR**。
- **#78545** — Windows 下 ctrl+b 与侧边栏切换冲突，且 wake word 默认未启用。**无 fix PR**。
- **#79026** — macOS ARM64 (M4) 上 wake word 完全失效（两个引擎均无效）。**无 fix PR**。
- **#79331** — Telegram 富消息省略了代码块的复制按钮。**✅ 有 PR #81346（待合并）**。

---

## 6. 功能请求与路线图信号

### 有望进入下一版本的功能

| 功能 | 对应 PR | 信号强度 |
|------|---------|----------|
| **Desktop bundled installers**（自包含安装包：agent 源码 + uv + CPython + wheelhouse + node + 预构建 JS，首次启动零下载） | #79599 | 高 — 直接提升 desktop 的发行体验 |
| **skills.create_dir + 共享池自动提交**（将新技能写入共享目录而非 profile 本地） | #81002 | 中高 — 团队协作场景的核心需求 |
| **通用 ACP 客户端**（支持任意 ACP 兼容编码 agent，解决目前仅支持 Copilot 的局限） | #68222 | 中 — P4 + needs-decision，但有方向讨论基础 #5257 |
| **Dashboard 根落地页支持**（插件可通过 `tab.override: "/"` 成为落地页） | #71765 | 中 — 提升 dashboard 插件生态可能性 |
| **Windows 系统托盘支持**（关闭按钮隐藏到托盘而非退出，可开关） | #81342 | 中 — 直接回应 Windows 桌面用户常见需求 |

### 「quoted false」批量修复的启示

#81348、#81345 连续修复 `bool("false")` 为 `True` 的配置解析坑，提示 **YAML 手写或环境桥接配置的可靠性已是实际痛点**，建议维护者考虑在所有配置解析点统一引入 YAML 1.2 核心 schema（自动将未引用 `false` 解析为布尔），从源头杜绝此类问题。

---

## 7. 用户反馈摘要

- **桌面端冻结或卡死是最集中的不满意度来源** — 包括 #63047（macOS beta 完全无响应）、#79105（流式回复时滚动锁死）、#78486（回复时跳转到历史消息）三个独立报告，社区对「桌面端在回复生成过程中的交互流畅性」抱怨最为集中，而多个 PR 尚未直接针对「用户体验层」做修复。
- **长期用户对「多平台会话延续」存在持续需求** — #4335 中社区表达了希望 CLI 与 Telegram 之间共享上下文的愿望，即使列为 P3 也仍有 3 个 👍，说明这是真实使用场景下的跨平台痛点。
- **WhatsApp 平台功能不完整引发用户主动组织对齐运动** — #79890 meta-issue 创建仅一天便有 6 条评论，用户希望 Hermes 的 WhatsApp 面与官方 Business Platform Cloud API 对齐，暗示当前实现差距较大。
- **Windows 桌面用户体验细节被诟病** — 多个 Windows 专项报告（#80184、#78545、#80439），虽非致命，但密集出现说明该平台体验打磨度不足。
- **配置系统的「坑」开始引发「防呆」诉求** — 连续出现 `bool("false")` 解析错误、`.desktop` Exec 路径错误（#80439）、ELF 二进制被误判（#81322）等问题，用户对配置可预期性的信任在下降。

---

## 8. 待处理积压

### 长时间未响应的 Issue

- **[#26006] fix: invalidate update-check cache inputs**（PR，已开放 85 天）— 修复 CLI 更新横幅缓存导致本地 git checkout 下状态长期过期的问题。核心技术含量不高，但持续影响开发者的更新感知，建议优先合入。
  [PR #26006](https://github.com/NousResearch/hermes-agent/pull/26006)

- **[#51327] Desktop 在 .desktop 启动器下静默失败**（已开放 46 天）— Electron chrome-sandbox 缺少 setuid 4755 权限时无任何报错，普通 Linux 用户极易踩坑。建议至少在文档中增加启动前的权限检查指引。
  [Issue #51327](https://github.com/NousResearch/hermes-agent/issues/51327)

- **[#4335] 跨平台会话上下文共享**（已开放 128 天）— 作为长期热门的 feature request，仍处于 `needs-decision` 状态。建议维护者给出明确的时间表或可行性评估，回应社区热度。
  [Issue #4335](https://github.com/NousResearch/hermes-agent/issues/4335)

- **[#28006] fix(models): probe azure-foundry deployments for /model picker**（PR，已开放 82 天）— Azure Foundry 用户无法在 `/model` 选择器中看到任何模型，该 PR 已存在近 3 个月仍未合并。建议确认是否已被其他方案取代，或推动合入。
  [PR #28006](https://github.com/NousResearch/hermes-agent/pull/28006)

### 长期未合入的 PR

- **#26006（85 天）、#28006（82 天）、#21683（已合入但耗时 91 天）、#71765（13 天）、#68222（19 天）** — 显示较大功能或安全相关 PR 的审查周期较长。若项目有意加快迭代，建议对超过 2 周未合入的 PR 建立「reviewer 责任轮值」或「Ping 提醒」机制。

---

> **日报总结**：项目迭代速度较快，P1 缺陷在同日内即有 fix PR 跟进，但 P2/P3 级修复积压也在积累（部分已超 2 周），且多个潜伏的「配置解析」问题正在集中爆发。建议维护团队重点关注「桌面端用户交互体验」与「YAML 配置解析健壮性」两个方向，它们正在成为社区不满的主要来源。

*报告生成时间：2026-08-08*

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

好的，作为 AI 智能体与个人 AI 助手领域开源项目分析师，这是为您生成的 PicoClaw 项目动态日报。

---

# PicoClaw 项目动态日报
**日期**: 2026-08-08
**数据周期**: 过去 24 小时

## 1. 今日速览
PicoClaw 在过去 24 小时内保持中等活跃度。虽然无新版本发布，但 Issues 与 PR 均有实质更新，社区讨论热度稳定。值得关注的是，项目在 **核心架构优化、渠道兼容性修复** 和 **工具执行可靠性** 三个方向上有重要进展。尽管长期存在的 Dependabot 依赖更新 PR 占比较大（体现维护自动化），但涌现出多个由社区贡献者提交的高质量修复和改进提案，表明项目吸引力与协作生态良好。整体项目健康度为 **稳健**，需重点关注长期“stale”标记的 PR 和 Issue，以防社区贡献被忽视。

## 2. 版本发布
- **无新版本发布。**

## 3. 项目进展
今日有 2 项 PR 被合并或关闭，梳理如下：
- **[#3291] [CLOSED] build(deps): bump github.com/github/copilot-sdk/go from 0.2.0 to 1.0.8**：终于完成了 Copilot SDK 跨越多个大版本的依赖升级。此升级可能引入新功能或 API 变更，需注意随后的回归测试。
- **[#3289] [CLOSED] build(deps): bump github.com/pion/rtp from 1.10.2 to 1.10.5**：完成 WebRTC 底层库的补丁版本升级，有助于增强音视频传输的稳定性。

**项目迈进评估**：虽然今日没有核心功能 PR 被直接合并，但依赖的清理和及时更新为后续开发扫清了障碍，并降低了潜在的安全与兼容性风险。

## 4. 社区热点
今日讨论热度最高的为 Issue **#3093**（评论 6 条）。
- **链接**: [Issue #3093](https://github.com/sipeed/picoclaw/issues/3093)
- **议题**: 用户希望增加 SimpleX、Wire 或 Tox 这三种去中心化/隐私优先的通信协议网关。
- **诉求分析**: 这反映了用户群体对隐私保护的深切关注和对去中心化通信的强烈需求。PicoClaw 作为一款主打本地、轻量的 AI 助手，其用户群体对数据主权尤为敏感。该请求虽然已关闭（可能被标记为 stale），但获取了 1 个 👍，是扩展非主流渠道的重要潜在方向。

## 5. Bug 与稳定性
今日报告的 Bug 不多，但有数个严重的长期问题通过 PR 提出了修复方案，值得关注：

- **[严重，有修复 PR] WhatsApp 渠道完全不可用**
  - **描述**: PR **#3320** 指出，WhatsApp 官方已拒绝 PicoClaw 当前使用的客户端版本，导致频道连接后约 5 秒即断开，且无法重连（报错 "Client outdated (405)"）。
  - **修复**: [PR #3320](https://github.com/sipeed/picoclaw/pull/3320) 通过升级 `whatsmeow` 库来解决该问题。
  - **分析**: 此 Bug 直接影响核心渠道功能，虽未在 Issue 区反复出现，但 PR 的提出点明了紧迫性。

- **[中等，有修复 PR] `exec` 工具参数失效**
  - **描述**: PR **#3319** 仔细审查了 `exec` 工具的实现，发现其声明了 `timeout`、`background`、`pty` 参数，但在实际执行时却未处理，甚至将布尔值误作字符串。
  - **修复**: [PR #3319](https://github.com/sipeed/picoclaw/pull/3319) 旨在让工具执行严格遵循用户指令。
  - **分析**: 潜在影响较大，凡是依赖 `exec` 工具进行定时或后台任务的用户都可能遭遇到此问题。

- **[提示，无直接修复] 潜在架构隐患**
  - **描述**: Issue **#3308** 是一份针对代码库的核心组件（SeaHorse、Channel Manager、Hooks）的深度 Code Review，指出了并发风险、goroutine 泄漏和性能优化点。
  - **分析**: 尽管该问题被标记为 `stale`，但其中蕴含的技术债风险值得维护者重视，属于潜在的技术债务治理范畴。

## 6. 功能请求与路线图信号
- **OAuth 2.1 支持**: Issue **#3302** 请求为 MCP 服务器添加现代 OAuth 支持，标记为 “Nice-to-Have”。此功能将增强 PicoClaw 与企业级服务的互操作性，对于扩展专业用户群体有正向作用，建议维护者评估目前 OAuth 2.0 实现的迁移成本与收益。

- **多渠道会话管理**: Issue **#3307** 建议将 Web UI 的会话管理能力（列出、切换、删除会话）扩展到 Telegram 等其他聊天渠道。这是提升非 Web UI 用户操作体验的关键需求，但目前无对应 PR 支持。

- **模型默认回退链**: 长存 PR **#3200** 提出了设置“默认模型回退链”的功能，允许用户按顺序指定多个模型，并在主模型不可用时自动切换。这不仅是 Web 端体验升级，更是 7x24 小时无人值守运行的 AI Agent 的刚需（容错性体现），值得维护者密切关注。

- **新的 TTS 提供商与渠道支持**:
  - PR **#3270** 引入了阿里云 DashScope TTS 支持，并声称可以发送微信语音文件。
  - PR **#3283** 增加了钉钉渠道的图片消息接收支持。
  - 若有确认，这两项将填补国内常用办公与生活渠道（微信、钉钉）的能力空白，对扩大项目在中文社区的吸引力有较大帮助。

## 7. 用户反馈摘要
- **对隐私的关注（来源 Issue #3093）**：用户基于“使用场景”考虑，明确请求接入 SimpleX/Tox 等注重隐私的协议，表明核心用户对端到端加密和最小化数据暴露有较高期望。
- **对 AI 模型最新状态的关注（来源 PR #3271）**：有一位贡献者提交 PR，系统性地更新了 9 家提供商（OpenAI、Anthropic 等）的当前最新模型名称（如 `gpt-5.6-terra`），确保 PicoClaw 的默认配置不“落伍”。这反映出社区对模型时效性的敏锐度，以及愿意主动帮助项目保持更新的热情。

## 8. 待处理积压
- **长期未响应的功能 PR 积压**：
  - **[PR #3271](https://github.com/sipeed/picoclaw/pull/3271)** (2026-07-20): 更新默认模型列表至最新。
  - **[PR #3270](https://github.com/sipeed/picoclaw/pull/3270)** (2026-07-20): 添加 DashScope TTS 和微信语音发送。
  - **[PR #3283](https://github.com/sipeed/picoclaw/pull/3283)** (2026-07-22): 钉钉图片消息支持。
  - **[PR #3200](https://github.com/sipeed/picoclaw/pull/3200)** (2026-07-01): 可配置的默认模型回退链。
  - **建议**: 上述 PR 均已开放超过两周且标记为 “stale”，均有实质性改动，涉及功能或优化较广。为防止社区贡献动力消退，维护者需要尽快进行代码审查、反馈或合并，或明确拒绝理由。

- **被标记 stale 的 Bug 审查**：
  - **[Issue #3308](https://github.com/sipeed/picoclaw/issues/3308)** (2026-07-30): 针对 SeaHorse 等核心组件的代码审查，指出并发与内存问题。

---
**总结**：PicoClaw 项目正处于稳步迭代状态，社区贡献的质量颇高，尤其在与国内服务（钉钉/微信/DashScope）的集成方面体现了较强的本地化活力。然而，项目维护者需加速清理 PR 积压，防止因拖沓导致的贡献者流失。同时，建议将“模型回退链”需求评估并纳入规划，以强化其作为头部 AI 个人助手的稳定性优势。

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw 项目动态日报

**日期：2026-08-08** | **数据来源：GitHub (nanocoai/nanoclaw)**


## 1. 今日速览

项目今日整体活跃度**中等偏低**。过去24小时无新 Issue 产生、无新版本发布，但 Pull Request 侧有 **12 条动态更新**，其中 2 条已合并/关闭、10 条仍处于待合并状态。值得关注的是，今日有 3 个新 PR 提交（#3199、#3198、#3196），且多个 PR 带有 `core-team` 标签（#2909、#3198），说明核心团队仍在积极推动路线图落地。**项目健康度良好**：Issue 积压为零，PR 队列虽有一定积压（10 条待合并），但多数处于活跃迭代中而非无人响应。项目当前的重心明显偏向**渠道集成扩展**与**技能（Skills）生态建设**两大方向。


## 2. 版本发布

**无新版本发布。** 最近一次版本发布距今已有一段时间，建议维护团队评估是否需要基于当前积累的 10 条待合并 PR 规划下一个版本的发布节奏。


## 3. 项目进展

今日有 2 条 PR 关闭/合并，其中一条意义重大：

- **[PR #3197] fix(progress): 失败状态展示具体原因**（已关闭）— 作者: tier2tech-tian
  这是今日唯一确认合入的修复 PR。它解决了 agent-runner 过程卡片失败状态只显示泛化文案（如「执行系统检查失败」）的问题，改为从 `resultSummary` 中提取首条有效错误原因并展示。该修复包含完整的单测覆盖（274 定向测试 + 1427 全量测试通过），说明项目对代码质量的要求保持在高水准。修复了**多通道触达中的用户可观测性短板**。

- **[PR #546] Add Mattermost channel skill (/add-mattermost)**（已关闭）— 作者: wakqasahmed
  该 PR 于 2 月 26 日创建，历经 5 个多月后关闭，被新 PR #3199（基于 v2 `ChannelAdapter` 架构的全新重写）取代。关闭属于架构演进的正常结果——旧代码构建在已不存在的 `Channel`/`registry.ts` 架构之上，**关闭是清理历史债务的合理操作**。

**整体判断：** 今日项目实质进展集中在 bug 修复层面，核心架构与功能迭代主要依赖 10 条待合并队列的逐渐消化。


## 4. 社区热点

今日无高讨论量 Issue/PR（评论数为 0），但以下 PR 值得关注：

- **PR #3199 — Add Mattermost channel integration (v2 ChannelAdapter)**（打开）— 作者: wakqasahmed | 8月7日新提交
  这是对 #546 的重写，针对当前 `ChannelAdapter`/`channel-registry.ts` 合约的全新实现。**Mattermost 渠道集成历经两次迭代**，说明社区对工作流类 IM 工具有真实需求，且作者愿意跟随架构演进持续贡献。

- **PR #2909 — [core-team] feat(setup): template setup flow in the wizard and first-agent stamping**（打开）— 作者: amit-shafnir | 7月2日创建，8月7日更新
  `core-team` 标签表明这是官方路线图的一部分。该 PR 是「Agent 模板」系列的第二步（第一步 #2890 已完成），旨在安装向导中增加 Agent 模板选择流程。**更新于昨日**，说明仍在活跃推进。


## 5. Bug 与稳定性

今日无新 Bug 报告（0 条新 Issue），但队列中有若干修复型 PR 值得关注，按严重程度排列：

| 严重程度 | PR | 问题描述 | 状态 |
|---------|-----|---------|------|
| 中 | [#3145](https://github.com/nanocoai/nanoclaw/pull/3145) fix(db): backfill destinations for existing wirings | 已存在消息组 wiring 缺少 channel destinations，需要迁移回填（migration 021） | 打开，7/28 创建 |
| 中 | [#3149](https://github.com/nanocoai/nanoclaw/pull/3149) fix(cli): add --rw flag to groups config add-mount | CLI 的 `groups config add-mount` 缺少 `--rw` 只读/读写挂载控制 | 打开，7/29 创建 |
| 中 | [#3196](https://github.com/nanocoai/nanoclaw/pull/3196) Fix/add mount readonly | mount 只读属性缺失，与 #3149 疑似同一问题域 | 打开，8/7 新提交 |
| 低 | [#2346](https://github.com/nanocoai/nanoclaw/pull/2346) fix(formatter): treat unknown slash commands as normal chat | 未知斜杠命令被误判为 `passthrough`，导致 Agent SDK 输出被静默丢弃 | 打开，5/8 创建，**已积压 3 个月** |
| 低 | [#2705](https://github.com/nanocoai/nanoclaw/pull/2705) fix(use-native-credential-proxy): actually bypass the OneCLI gateway | 原生凭据代理技能实际未绕过 OneCLI 网关；`nativeCredentialsEnabled()` 只读环境变量，未读配置文件 | 打开，6/7 创建，**已积压 2 个月** |

**稳定性总体评价：** 无严重崩溃或数据安全类 Bug。主要的稳定性风险集中在**挂载（mount）权限控制**（#3149、#3196 两个 PR 从不同角度解决同一问题，建议维护者协调避免重复劳动）和**数据库存量数据迁移**（#3145）。


## 6. 功能请求与路线图信号

结合今日活跃 PR 与已有队列，以下功能方向有较大概率被纳入后续版本：

| 功能方向 | 相关 PR | 信号强度 | 分析 |
|---------|---------|---------|------|
| **Mattermost 渠道集成** | [#3199](https://github.com/nanocoai/nanoclaw/pull/3199)（新提交） | 强 | 对旧 PR #546 的全新重写，作者投入大且紧跟架构演进。若合入，将补齐 Mattermost 生态空白 |
| **Agent 模板系统** | [#2909](https://github.com/nanocoai/nanoclaw/pull/2909)（core-team） | 强 | 核心团队主导，第一步已合入（#2890），此 PR 为第二步（向导流程 + 首次 Agent 模板标记），是明确的路线图信号 |
| **Dial 渠道支持** | [#3050](https://github.com/nanocoai/nanoclaw/pull/3050) | 中 | 新增渠道选择器中的 Dial 选项，附带 `runChannelSkill` 模型扩展，7/14 创建、仍在更新 |
| **Tavily MCP 工具技能** | [#3190](https://github.com/nanocoai/nanoclaw/pull/3190) | 中 | 添加 Tavily 搜索 MCP 工具技能，属于工具生态扩展 |
| **AnyDoc 文档转换技能** | [#3198](https://github.com/nanocoai/nanoclaw/pull/3198)（core-team，新提交） | 强 | 带 `core-team` 标签，官方推的文档转换能力，扩展 Agent 对多格式文档的处理能力 |

**判断：** 下一个小版本很可能聚焦 **Agent 模板系统（#2909）+ 新渠道扩展（Mattermost / Dial）** 的组合。


## 7. 用户反馈摘要

由于今日无新 Issue 产生，以下反馈来自 PR 描述与代码改动中暴露的用户痛点：

- **失败可观测性不足** — PR #3197 的修复直接回应了用户痛点：agent-runner 执行失败时只显示泛化文案，用户无法获知具体失败原因。该修复上线后，失败卡片将展示「动作失败：具体原因（单行截断 38 字符）」，显著提升排障效率。
- **原生凭据代理失效** — PR #2705 揭示用户在生产环境（launchd/systemd 托管）中启用 `use-native-credential-proxy` 技能时，实际流量并未绕过 OneCLI 网关。此类配置类 Bug 对生产部署影响较大，但该 PR 已积压两月，**需提醒维护者关注**。
- **旧版渠道集成用户等待时间长** — PR #546 关闭后，Mattermost 用户从 2 月等待至今仍未获得可用的渠道集成。虽然 #3199 已提交，但仍在审查中，建议维护者推动合入或给出明确时间表。

## 8. 待处理积压

以下 Issue/PR 长期未获有效推进，建议维护团队关注：

| 项目 | 创建时间 | 积压天数 | 优先级建议 |
|------|---------|---------|-----------|
| [#2346](https://github.com/nanocoai/nanoclaw/pull/2346) fix(formatter): treat unknown slash commands as normal chat | 2026-05-08 | 92 天 | **高** — 会导致用户消息静默丢失，影响核心体验 |
| [#2705](https://github.com/nanocoai/nanoclaw/pull/2705) fix(use-native-credential-proxy): actually bypass the OneCLI gateway | 2026-06-07 | 62 天 | **高** — 生产环境配置失效，涉及凭据安全 |
| [#3149](https://github.com/nanocoai/nanoclaw/pull/3149) fix(cli): add --rw flag to groups config add-mount | 2026-07-29 | 10 天 | **中** — 与 #3196 问题重叠，建议合并处理 |
| [#3050](https://github.com/nanocoai/nanoclaw/pull/3050) feat(setup): add Dial to the channel picker | 2026-07-14 | 25 天 | **中** — 等待审查，涉及渠道选择器 UI 变更 |

---

**报告结束。** 如需特定 PR 的详细 diff 或审查意见分析，可进一步查询。

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw 项目动态日报 — 2026-08-08

> 数据来源：github.com/nearai/ironclaw | 统计窗口：2026-08-07 ~ 2026-08-08


## 1. 今日速览

过去 24 小时 IronClaw 保持高位活跃：50 条 Issue 与 50 条 PR 更新，其中各 14 条关闭/合并。今日主线非常清晰——**文档与事实漂移治理**（doc-truth 五连 PR #7375–#7381）和 **QA bug 集中修复**（多源自 Railway 测试实例）。值得警惕的信号：多个 P1 bug 涉及 agent 幻觉（虚构自动化状态、错认连接状态、遗留 Telegram 记忆），指向**状态感知与记忆一致性**是当前最突出的稳定性短板。CI 方面有专门的门禁审计 PR（#7373）出台。整体判断：项目处在 **v1.1.0-rc.1 发布后的密集质量收尾期**，工程质量投入显著。


## 2. 版本发布

**今日无新版本发布。** 最新仍为 `1.0.0-rc.1 → 1.1.0-rc.1` 升级周期（该过程暴露了持久化状态兼容性缺口，见 Issue #7380）。


## 3. 项目进展

### 3.1 已合并/关闭的重要 PR

| PR | 标题 | 影响 |
|---|---|---|
| [#7157](https://github.com/nearai/ironclaw/pull/7157) | **显式频道投递工具——双通道模型** | 实现 `2026-07-27` 审批的设计：每个 run 的最终回复落在其所在会话（Lane 1），同时提供独立的通知频道（Lane 2），删除旧的投递启发式逻辑。这是频道系统的架构级收口 |
| [#7372](https://github.com/nearai/ironclaw/pull/7372) | **钉住宽目录 schema-token 缩减下限** | 将 #6810 的 50% schema-token 缩减基准从"仅打印表格"升级为硬性断言，防止渐进式工具披露的性能优势被悄悄侵蚀 |
| [#7366](https://github.com/nearai/ironclaw/pull/7366) | **RC1 分支：OAuth 空 scope 省略** | 将 #7309 修复移植至 `release/1.1.0-rc.1`，附带 WebUI 设置路由与 turn-blocked OAuth 门禁的回归覆盖 |

**已关闭的 Issue（14 条）亮点：** Telegram 系列（#6643、#6644、#6475）与 Slack 编码问题（#6476）均关闭；`WebChat v2 HTTP "Illegal invocation"` 长期 bug（#4874）关闭；渐进式工具披露默认开启（#6810）与 schema 感知检索增强（#7177）关闭。

### 3.2 整体进度判断

- **频道/通知系统**：双通道投递模型（#7157）落地，下游 PR #7377（run 作为其发起者身份运行）已排入队列——频道系统进入一致性收尾。
- **文档可信度**：doc-truth 五连 PR 完整提交（#7375–#7379、#7381），从修复文档漂移、引入契约测试、扩大 CI 门禁到"docs-live 分支"部署机制，系统性地解决"文档描述未发布行为"的顽疾。
- **记忆可靠性**：#7365 一次性修复 #7185 的三个根因（无系统提示引导、无保存时机决策、无 always-on MEMORY.md 提示通道），是记忆功能的重大补强。
- **工具发现效率**：#7374 将 `tool_describe` 从单工具改为批量，消除多轮 schema 获取的开销。
- **工程质量**：#7373 全量审计了 37 个架构测试门禁文件 + 约 80 个 CI scripts,重新武装 5 个 fail-open 门禁——对 #7157 六连红 CI 的正面回应。


## 4. 社区热点

| 排名 | Issue/PR | 评论数 | 关注点 |
|---|---|---|---|
| 1 | [#7340](https://github.com/nearai/ironclaw/issues/7340) 无重置模型设置为出厂默认值 | 6 | 用户侧反馈：修改 provider/model 后无法恢复初始配置 |
| 2 | [#6989](https://github.com/nearai/ironclaw/issues/6989) Token 计算：`ModelWorkRequest` 从内容引用字符串估算输入 tokens | 4 | 混合 provider 用量 + 尾部估算的 token 记账问题，属 pi-harness 采用计划 P1 |
| 3 | [#7317](https://github.com/nearai/ironclaw/issues/7317) Doc-Truth 验证流水线提案 | 3 | 文档与代码漂移的根治提案，触发今日 doc-truth 五连 PR |
| 4 | [#7360](https://github.com/nearai/ironclaw/issues/7360) 扩展内置与持久化写入路径的压力覆盖 | 2 | 夜间压力测试未覆盖带工具调用的场景，存在回归盲区 |
| 5 | [#6476](https://github.com/nearai/ironclaw/issues/6476) Slack `extension_activate` 编码错误致模型幻觉（已关闭） | 2 | 工具失败信息被模型幻觉为"需要租户管理员权限"——模型面对工具报错时的典型误导 |

**诉求分析**：#7340 的 6 条评论表明用户对"配置可逆性"有强需求——当前没有 factory reset 概念，误配置即"锁定"。同时，幻觉类问题的集中出现（#7246、#7247、#7294、#7344）反映出社区对 **agent 状态感知真实性**的关注已形成规模。


## 5. Bug 与稳定性

### 🟥 P1 / 严重（影响核心功能）

| Issue | 描述 | Fix PR |
|---|---|---|
| [#7292](https://github.com/nearai/ironclaw/issues/7292) | 安装 CoinGecko 工具后无法使用，runner 心跳错误致 run 失败 | — |
| [#7298](https://github.com/nearai/ironclaw/issues/7298) | "请求在发送前失败"+"监控系统与 runner 失联"两类基础设施错误 | — |
| [#7295](https://github.com/nearai/ironclaw/issues/7295) | Agent 将 Slack DM 误发给另一用户（sergey.astretsov），用户身份泄漏/混淆 | — |
| [#7247](https://github.com/nearai/ironclaw/issues/7247) | Agent 谎称 GitHub 已连接，实际未认证 | — |
| [#7246](https://github.com/nearai/ironclaw/issues/7246) | Agent 虚构自动化运行中状态，UI 显示 "No automations yet" | — |
| [#7344](https://github.com/nearai/ironclaw/issues/7344) | Slack 已在 Messaging Channels 显示 ACTIVE，但 assistant 不识别 | — |
| [#7294](https://github.com/nearai/ironclaw/issues/7294) | Agent 声称已有 BTC 新闻 Telegram 例行程序，实际不存在 | — |
| [#5456](https://github.com/nearai/ironclaw/issues/5456) | 例行程序因 runner lease 90 秒不活动阈值过期而失败（多工具场景） | — |

### 🟨 P2 / 中等

| Issue | 描述 | Fix PR |
|---|---|---|
| [#7345](https://github.com/nearai/ironclaw/issues/7345) | Agent 称 61 个自动化，UI 显示 50 个 | — |
| [#6590](https://github.com/nearai/ironclaw/issues/6590) | Windows 上 `serve` 本地模式失败：workspace root 与默认 skill root 重叠 | — |
| [#7368](https://github.com/nearai/ironclaw/issues/7368) | 频道轮次在 DeepSeek 级模型上耗时数分钟（#6643 的根因） | — |
| [#7369](https://github.com/nearai/ironclaw/issues/7369) | Agent 报错时 UI 无 trace 捕获按钮 | [#7370](https://github.com/nearai/ironclaw/pull/7370) — 为失败 run 的错误消息附加 `turnRunId`，使 trace 可捕获 |

### 🟩 已修复 / 有关联修复

- [#6989](https://github.com/nearai/ironclaw/issues/6989) Token 估算 bug（从引用字符串而非内容估算）——**无对应 PR，仍开放**。
- [#7185](https://github.com/nearai/ironclaw/issues/7185) 跨会话记忆不可靠——**[#7365](https://github.com/nearai/ironclaw/pull/7365)** 三因齐修，PR 已提交。


## 6. 功能请求与路线图信号

| 请求 | 信号强度 | 分析 |
|---|---|---|
| **[#7340](https://github.com/nearai/ironclaw/issues/7340) 模型设置重置为默认** | 高（6 评论，0 👍） | 用户对配置可逆性诉求强烈，可能随设置面板增强进入 v1.2。目前无对应 PR |
| **[#7362](https://github.com/nearai/ironclaw/issues/7362) 用户可见失败摘要移入各 surface i18n** | 中（0 评论） | 65 条硬编码英文句子无法本地化。提议为 CLI 增加消息解析器。可能随 i18n 路线图推进 |
| **[#7380](https://github.com/nearai/ironclaw/issues/7380) 合并前强制持久化状态兼容性** | 高（epic） | 由 rc1→rc2 升级暴露，要求 PR 证明新二进制可读旧状态。可能催生新的 CI 门禁 |
| **[#7317](https://github.com/nearai/ironclaw/issues/7317) Doc-Truth 验证流水线** | 极高（已有 5 个 PR 跟进） | 提案在 24 小时内变为 5 连 PR——强烈信号表明这是项目当前重点。**已实现**：契约测试 + docs-live 分支 + CI 门禁扩展 |

**路线图判断**：#7317 的闪电落地表明项目对文档漂移的容忍度已到临界点；#7380 的 epic 化说明持久化兼容性将定义为强制性要求。两者均指向**发布工程化**是 v1.1 之后的主线。


## 7. 用户反馈摘要

**核心痛点：配置不可逆。** #7340 的用户反馈显示：修改模型设置后无法恢复默认，尝试无果。这暴露了配置管理的单向性——没有版本历史、没有导出/导入、没有 "reset"。

**记忆不一致的挫败感。** #7185 引述 IronClaw Champions 周会：多位测试者独立观察到"对话 A 中建立的信息在对话 B 中无法回忆"。法律场景的 Devon（经 Tobias 转述）特别指出 agent 无法访问此前提供的信息——对专业场景用户，这是信任破坏级别的缺陷。

**工具失败时的模型幻觉。** #6476（已关闭）与 #7246、#7294、#7344 构成同一模式：**工具调用失败/连接状态变化时，模型不报错而自圆其说**。如 #7246：UI 清显示 "No automations yet"，agent 却"自信地"声称 BTC 摘要正在运行。用户对"自信的错误"比"明确的失败"更失望。

**长期存在的平台性问题。** #5456（runner lease 过期）自 6/30 报告后持续未修，是 Routine 功能的主要失败模式；#6590 的 Windows 支持问题自 7/23 起一直开放。


## 8. 待处理积压

| 项目 | 年龄 | 状态 | 备注 |
|---|---|---|---|
| [#5456](https://github.com/nearai/ironclaw/issues/5456) runner lease 过期致例行程序失败 | 39 天 | OPEN，1 评论 | **最老未修的 P1 bug。** 90 秒不活动阈值在含模型推理+外部 API 的多工具例行程序中过于激进。6/30 即为当次测试的主流失败模式，至今无修复 |
| [#6590](https://github.com/nearai/ironclaw/issues/6590) Windows `serve` 启动失败 | 16 天 | OPEN，2 评论 | 本地开发完全不可用，涉及 reborn 组合配置的 workspace root 重叠判断 |
| [#6989](https://github.com/nearai/ironclaw/issues/6989) Token 记账：`ModelWorkRequest` 从引用字符串长度估算 | 7 天 | OPEN，4 评论 | P1 计划的组成部分，估算偏差可能导致成本计算失真或上下文超限。**有明确 bug 定位但无修复 PR** |
| [#7076](https://github.com/nearai/ironclaw/pull/7076) 安装目录已发布的 packages | 5 天 | OPEN，新贡献者 | 新人贡献者 neo-sky 的 PR，已 rebase 至当前 main。若长期无人 review，有挫伤贡献积极性的风险 |
| [#6938](https://github.com/nearai/ironclaw/pull/6938) 模型选择技能而非关键词评分器 | 8 天 | OPEN | **堆叠在未合并的 #6745 之上**，属 epic #6941。架构级变更（host 不再自动激活技能），长时间未合并需关注下游阻塞 |

---

**健康度小结**：项目响应力强（doc-truth 提案 24 小时内产出 5 个实现 PR），但 P1 bug 的 fix 转化率偏低——8 个 P1 级 bug 中 6 个尚无对应 PR，且最早者可追溯至 6/30。若将幻觉类问题的公共根因（状态感知工具化）作为优先项处理，可一次性缓解 #7246/#7247/#7294/#7344 等多个 P1。

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

# LobsterAI 项目动态日报 — 2026-08-08

> 数据来源：github.com/netease-youdao/LobsterAI | 统计周期：2026-08-07 至 2026-08-08


## 1. 今日速览

LobsterAI 今日活跃度**较高**，24小时内完成 1 个版本发布（2026.8.7）、6 个 PR 合并/关闭、3 个 Issue 关闭，同时新增 4 个待处理 Issue。当前积压的 3 个新 Issue 中，2 个为 Bug（含 1 个带 PR 修复）、1 个为功能请求，整体反馈质量良好，指向性强。老 Issue 的集中清理（4 个 stale 标记关闭）显示项目维护团队正在积极清理技术债。值得关注的是，社区对**多 Agent 绑定不同 IM 机器人和模型**的诉求（Issue #1265）已存在四月有余，虽然标记为 stale 关闭，但该需求在多 Agent 场景下仍具实际价值，建议团队评估将其纳入路线图或明确回应。此外，今日提交的 PR #2452（修复模型 ID 含斜杠问题）与 Issue #2443 直接对应，fix 效率较高，体现了良好的社区反馈闭环。


## 2. 版本发布

### LobsterAI 2026.8.7（2026-08-07 发布）

**主要更新内容：**
- **Cowork**：新增标题栏会话搜索功能（PR #2435，by @liuzhq1986）
- **Markdown 渲染**：支持 LaTeX 数学公式分隔符（PR #2449，by @fisherdaddy）
- **Windows 安装器**：修复 watchdog 空退出码问题（PR #2446，by @fisherdaddy）

**破坏性变更**：无

**迁移注意事项**：无特殊要求，常规升级即可。


## 3. 项目进展

今日项目合并了 6 个 PR，核心进展包括：

- **版本合并**：`release/2026.8.5` 合入 `main`（PR #2451），标志着 2026.8.5 系列功能的正式落地。该版本涵盖 Cowork 会话内搜索、数学公式渲染改进、IM 分析、OpenClaw 配置与插件安装优化、Windows 安装/更新可靠性提升。
- **会话搜索修复**：PR #2448 修复了聊天搜索相关问题，配合 PR #2435 的标题栏搜索功能，Cowork 模块的会话检索能力在本版本中得到了系统性增强。
- **OpenClaw 配置管理**：PR #2445 修复了插件索引管理的 key 被意外写入 `config.set` 的问题，避免了配置冲突。
- **Windows 全屏模式修复**：PR #2450 修复了 Windows 下全屏代码工具栏点击失效的问题（原因：全屏 overlay 被 Electron 标题栏拖拽区域覆盖）。

**整体评价**：本日合并内容以 bug 修复和体验优化为主，Cowork 模块和 OpenClaw 集成是当前迭代重点。


## 4. 社区热点

今日讨论热度整体偏低，单条 Issue/PR 评论数均为 1-2 条，无爆发性讨论。相对值得关注的有：

- **Issue #1263**（定时任务重复显示 + API rate limit）｜[链接](https://github.com/netease-youdao/LobsterAI/issues/1263) — 有 2 条评论，用户反馈定时任务在 UI 上重复显示且均报 rate limit 错误，涉及会话数据一致性问题。
- **Issue #1195**（自建 skill 安装到 OpenClaw 后技能面板无显示）｜[链接](https://github.com/netease-youdao/LobsterAI/issues/1195) — 有 2 条评论，涉及 skill 安装路径与 UI 面板同步问题，至今已开放 4 个月。

**诉求分析**：以上两个 Issue 均涉及**安装/配置后的 UI 状态不同步**问题，说明用户对"配置即时生效、状态可视化"有较强预期，也反映项目在配置变更后的反馈链路仍有改进空间。


## 5. Bug 与稳定性

| 严重程度 | Issue | 描述 | 状态 |
|---------|-------|------|------|
| 🔴 高 | [#1273](https://github.com/netease-youdao/LobsterAI/issues/1273) | sql.js (WASM) 高频操作导致 `memory access out of bounds` 崩溃及数据库损坏风险（非原子写入） | 已关闭（stale），未明确修复方案 |
| 🟡 中 | [#2443](https://github.com/netease-youdao/LobsterAI/issues/2443) | 模型 ID 含斜杠的自定义 Provider（SiliconFlow）无法在界面中使用 | **OPEN**，已有对应 PR [#2452](https://github.com/netease-youdao/LobsterAI/pull/2452) |
| 🟡 中 | [#1195](https://github.com/netease-youdao/LobsterAI/issues/1195) | 自建 skill 被安装到 OpenClaw 后，重启技能面板无显示 | 已关闭（stale），未解决 |
| 🟡 中 | [#1263](https://github.com/netease-youdao/LobsterAI/issues/1263) | 定时任务 UI 重复显示 + API rate limit | 已关闭（stale），未解决 |
| 🟢 低 | [#2447](https://github.com/netease-youdao/LobsterAI/issues/2447) | 执行命令无输出、无错误信息 | **OPEN**，缺少详细信息，待补充 |

**稳定性风险提示**：Issue #1273 所描述的 sql.js 内存崩溃与数据库损坏风险值得重视，虽然被标记为 stale 关闭，但建议维护团队确认该问题是否已在后续版本中通过其他 PR 解决，或需要单独跟踪。


## 6. 功能请求与路线图信号

**新提出的功能请求：**

- **Issue #2444** — 输入框编辑模式｜[链接](https://github.com/netease-youdao/LobsterAI/issues/2444)
  - 用户痛点：长 Prompt 编辑需频繁 Shift+Enter 换行，误触直接发送
  - 建议方案：设置中切换 Enter/Ctrl+Enter 发送策略，或增加「编辑模式」开关（展开输入框、默认换行、支持 WYSIWYG）
  - **落地可能性评估**：此改进涉及输入体验，改动范围可控（不影响核心逻辑），预计可实现，但优先级可能低于功能开发。建议加入后续迭代考虑。

**路线图信号**：结合已合并的 PR（Cowork 搜索、LaTeX 渲染）来看，项目当前重心在 **Cowork 编辑器体验与数学公式渲染** 方向，输入框编辑模式若被采纳，将与这一方向形成互补。


## 7. 用户反馈摘要

来自今日 Issue 与评论的真实用户声音：

- **多 Agent 场景需求明确**（Issue #1265）：用户提出「不同的 AGENT 绑定不同的 IM 机器人和模型」，并给出具体使用场景（调度机器人 + PPT 生成机器人协同、编程模型与对话模型分离）。说明社区已有用户在实际使用多 Agent 工作流，且对模型-角色匹配有精细化需求。该 Issue 虽已关闭，但需求本身的合理性值得团队参考。

- **操作易用性**（Issue #2444）：用户对"Shift+Enter 换行"的交互感到不便，并给出了两种对比方案（设置切换 vs. 编辑模式开关），说明用户对交互细节有明确预期，且愿意提供方案建议。

- **配置透明度**（Issue #1195、#1263）：用户反映"安装成功提示"与"实际 UI 状态"不一致，说明用户期望配置操作有明确状态反馈，同时也反映了 skill 安装链路（主 Agent → OpenClaw → UI 面板）的同步机制需要完善。


## 8. 待处理积压

以下为长期未响应或已关闭但可能仍需关注的事项：

- **Issue #1273**（sql.js 内存崩溃/数据库损坏，2026-04-02 开启，已 stale 关闭）｜[链接](https://github.com/netease-youdao/LobsterAI/issues/1273) — 即使已关闭，考虑到其数据安全风险等级较高，建议维护团队确认是否已在后续版本中处理，若无明确修复记录，建议重新开启跟踪。

- **Issue #1195**（自建 skill 不显示，2026-04-01 开启，已 stale 关闭）｜[链接](https://github.com/netease-youdao/LobsterAI/issues/1195) — 复现概率为必现，且问题描述清晰，建议在 OpenClaw 集成相关迭代中予以验证并给出回应。

- **Issue #1265**（多 Agent 绑定不同模型/机器人，2026-04-02 开启，已 stale 关闭）｜[链接](https://github.com/netease-youdao/LobsterAI/issues/1265) — 功能需求明确且有多 Agent 场景支撑，建议评估纳入路线图或明确回复不采纳的原因，而非静默关闭。

- **PR #2452**（[待合并]修复模型 ID 含斜杠问题）｜[链接](https://github.com/netease-youdao/LobsterAI/pull/2452) — 当前处于 OPEN 状态，与 Issue #2443 直接对应，建议尽快 review 合并以解决该问题。


## 项目健康度评估

| 维度 | 状态 | 说明 |
|------|------|------|
| **开发活跃度** | ✅ 活跃 | 正常发版节奏 + 每日多个 PR 合并 |
| **社区反馈闭环** | ✅ 良好 | Issue #2443 当天即有对应 PR；多数新 Issue 有维护者响应 |
| **Issue 处理效率** | ⚠️ 待改进 | 4 个老 Issue 被批量 stale 关闭，其中部分问题未明确解决（#1273、#1195） |
| **技术债务** | ⚠️ 存在风险 | sql.js 非原子写入问题尚不明确是否已解决 |
| **文档与沟通** | ✅ 正常 | PR/Issue 描述清晰，标签规范 |

**一句话总结**：项目保持稳定的迭代节奏，新版本持续打磨 Cowork 与 OpenClaw 集成体验；当务之急是处理 PR #2452 的合并，以及给社区反馈被 stale 关闭但未解决的老问题一个明确交代。

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

好的，我是您的 AI 智能体与个人 AI 助手领域开源项目分析师。以下是基于 CoPaw 项目 (github.com/agentscope-ai/CoPaw) 2026年8月7日 GitHub 数据生成的项目动态日报。

---

### CoPaw 项目日报 — 2026-08-08

**数据统计周期：** 2026-08-07 (过去24小时)

---

#### 1. 今日速览

CoPaw 项目在 8 月 7 日表现出**极高的社区活跃度**，Issues 与 PR 更新总量达到 79 条，反映出用户参与度和项目迭代速度均处于高位。最引人注目的是 **v2.1.0-beta.2** 的发布，但随之而来的是 **Windows 端一系列严重 Bug 的集中反馈**（安装失败、安全软件误报等），社区情绪呈现出“积极尝鲜”与“稳定性抱怨”并存的复杂态势。同时，**MCP 工具失效**和**Agent 死循环**等稳定性和可靠性问题依然是用户关注的核心痛点，相关修复 PR 已在推进中。整体来看，项目功能迭代速度很快，但**稳定性是当前亟需解决的首要矛盾**。

---

#### 2. 版本发布

- **v2.1.0-beta.2**
    - **链接：** [Releases/tag/v2.1.0-beta.2](https://github.com/agentscope-ai/QwenPaw/releases/tag/v2.1.0-beta.2)
    - **更新内容：** 此版本为 Beta 版，主要包含两项修复：
        1.  `fix(ci): fence-aware section extraction in real-behavior-proof`：修复了 CI 测试中的一个问题。
        2.  `fix(checkpoints): restore auto snapshots in web workspace bootstrap`：修复了在 Web 工作区启动时自动恢复快照的问题。
    - **影响与注意事项：** 该版本刚发布即收到用户反馈（如 Issue #6797 和 #6785），存在**桌面模式无法选中复制文本**和 **Profile 类别硬编码导致自定义角色文件无法切换**的回归问题。此外，**Windows 安装程序存在问题**（详见 Issue #6810）。建议**非Windows桌面版用户暂缓升级**，等待后续修复版本。

---

#### 3. 项目进展

今日没有 PR 被合并，但多个高价值 PR 正在积极迭代并进入关键阶段（如标记为 “Under Review”），项目正在从“功能开发”转向“稳定性加固”：

- **核心稳定性修复推进：**
    - **[PR #6617](https://github.com/agentscope-ai/QwenPaw/pull/6617) (`Under Review`)**：修复流式重试路径下的 `Retry-After` 上限问题，增强模型的限流策略。
    - **[PR #6615](https://github.com/agentscope-ai/QwenPaw/pull/6615) (`Under Review`)**：增强 `load_agent_config` 的健壮性，避免因损坏的配置文件导致崩溃。
    - **[PR #6564](https://github.com/agentscope-ai/QwenPaw/pull/6564) (`Under Review`)**：修复内存压缩前的挂起回合刷新问题，完善 Scroll 生命周期。
- **新功能与重要修复开发中：**
    - **[PR #6772](https://github.com/agentscope-ai/QwenPaw/pull/6772)**：一个重量级 PR，旨在增强 ReMe 记忆功能，包括 Embedding 模型生命周期管理、新增 Daily Paper 定时简报能力，并重构 Console 的记忆配置页面。
    - **[PR #6800](https://github.com/agentscope-ai/QwenPaw/pull/6800)**：新增智能邮件管理助手（插件），支持多邮箱、实时监控和自动响应。

---

#### 4. 社区热点

今日讨论焦点主要集中在 **v2.1.0-beta.2 发布后暴露的问题**以及一些长期存在的稳定性痛点。

- **#6116 [已关闭] Agent 死循环问题：** [Issue #6116](https://github.com/agentscope-ai/QwenPaw/issues/6116)（8条评论）
    - **热点分析：** 虽然该 Issue 已关闭，但单一工具在单轮对话中被重复调用数十次直至系统警告的问题引发了大量共鸣。这再次证明了“Doom loop”是 AI Agent 在实际应用中的核心痛点，严重影响用户体验和成本。相关报告（如 #6768）仍在出现，是社区的强烈诉求。
- **#6782 插件/应用市场维护中：** [Issue #6782](https://github.com/agentscope-ai/QwenPaw/issues/6782)（8条评论）
    - **热点分析：** Docker 版本用户反馈插件市场和应用市场始终显示维护中，无法使用。这直接阻断了用户通过市场扩展功能的核心路径，影响面较大，需要官方尽快确认是服务端问题还是客户端兼容性问题。
- **#6732 MCP 工具规律性失效：** [Issue #6732](https://github.com/agentscope-ai/QwenPaw/issues/6732)（6条评论）
    - **热点分析：** 此问题并非个例，用户表示 MCP 工具会在一段时间（数小时或一晚）后失效，重启 Docker 容器才能恢复。这暗示可能存在资源泄漏、连接超时或心跳机制缺陷，对于依赖 MCP 生态的用户是严重的可靠性问题。

---

#### 5. Bug 与稳定性

今日报告的 Bug 主要集中在 **Windows 平台**和**核心功能可靠性**上，按严重程度排列如下：

- **严重 (P0) - Windows 安装/更新阻断：**
    - **[Issue #6810](https://github.com/agentscope-ai/QwenPaw/issues/6810)**：v2.1.0b2 在 Windows 上安装失败，NSIS 安装程序报“无法打开要写入的文件”错误。社区已分析出原因可能是浏览器扩展 NM host 的锁文件占用。**目前无明确修复 PR。**
    - **[Issue #6775](https://github.com/agentscope-ai/QwenPaw/issues/6775)**：MalwareBytes 将 Windows 桌面版标记为 “Trojan Loader”，虽极有可能是误报，但已造成用户信任危机并拒绝使用。**需要官方立即澄清。**

- **高 (P1) - 核心功能回归与失效：**
    - **[Issue #6785](https://github.com/agentscope-ai/QwenPaw/issues/6785)**：[v2.1.0b2 回归] Files 页面 Profile 类别硬编码了官方角色文件，导致用户自定义的 `.md` 角色文件无法切换。已有对应修复 PR **([#6808](https://github.com/agentscope-ai/QwenPaw/pull/6808))** 提交。
    - **[Issue #6807](https://github.com/agentscope-ai/QwenPaw/issues/6807)**：`qwenpaw-creator` 插件在 Windows 上视频/图片生成功能完全无法工作。
    - **[Issue #6806](https://github.com/agentscope-ai/QwenPaw/issues/6806)**：`qwenpaw-creator` 插件在 Windows 上无法保存任何模型配置，报 “Internal Server Error”。
    - **[Issue #6803](https://github.com/agentscope-ai/QwenPaw/issues/6803)**：OpenAI 兼容请求中携带了 Responses-API 的流式字段，导致 StepFun 等严格提供商拒绝请求 (400 错误)。已有对应修复 PR **([#6809](https://github.com/agentscope-ai/QwenPaw/pull/6809))** 提交。

- **中 (P2) - 功能异常与稳定性：**
    - **[Issue #6811](https://github.com/agentscope-ai/QwenPaw/issues/6811)**：OpenAI Responses 的续写摘要忽略了 `disable_thinking` 配置，且会将 60 秒的取消操作误报为输出格式错误。
    - **[Issue #6812](https://github.com/agentscope-ai/QwenPaw/issues/6812)**：Google Gemini API 因发送了额外的 `$schema` 字段而拒绝请求，导致模型执行失败。
    - **[Issue #6780](https://github.com/agentscope-ai/QwenPaw/issues/6780)**：2.0.1 版在空闲几十分钟后卡死，需要重启进程才能恢复。
    - **[Issue #6786](https://github.com/agentscope-ai/QwenPaw/issues/6786)**：Telegram 频道的访问白名单在 multica 启动新任务时被重置，导致已批准用户被屏蔽。已有对应修复 PR **([#6788](https://github.com/agentscope-ai/QwenPaw/pull/6788))** 提交。

---

#### 6. 功能请求与路线图信号

- **新 Provider 支持：** **[Issue #6490](https://github.com/agentscope-ai/QwenPaw/issues/6490)** 请求添加火山引擎 Agent Plan 和小米 MiMo 标准 API 作为内置提供商。这表明用户对国内云厂商的接入需求旺盛，但该 Issue 已开放约两周，评论不多，可能已被项目方列入待办但优先级不高。
- **新模型支持：** **[Issue #6285](https://github.com/agentscope-ai/QwenPaw/issues/6285)** 请求在阿里云 Token Plan 模型列表中添加 `qwen3.8-max-preview`。
- **桌面模式与浏览器体验优化：**
    - **[Issue #6770](https://github.com/agentscope-ai/QwenPaw/issues/6770)**：建议让 Chrome 标签页的存活时间可配置，以适应不同的响应周期。
    - **[Issue #6790](https://github.com/agentscope-ai/QwenPaw/issues/6790)**：建议桌面模式改为单击打开应用，并增加返回完整模式的按钮。虽然已关闭，但反映了桌面模式交互细节有待打磨。
- **已有关联 PR 的功能需求：** 记忆功能的增强 (**[PR #6772](https://github.com/agentscope-ai/QwenPaw/pull/6772)**) 和智能邮件助手插件 (**[PR #6800](https://github.com/agentscope-ai/QwenPaw/pull/6800)**) 是项目正在推进的新方向，很可能成为未来版本的核心特性。

---

#### 7. 用户反馈摘要

- **核心痛点：** “稳定性”是用户最强烈的呼声。无论是 MCP 工具失效、Agent 死循环、空闲卡死还是各种插件故障，都指向了产品在实际长时间运行中的可靠性不足。用户对因 Bug 浪费的时间和 Token 表示明显不满。
- **版本态度：** 用户对 v2.1.0-beta.2 的尝试意愿很高，但对 Beta 版本质量颇有微词。特别是 Windows 安装失败和恶意软件误报问题，极大地损害了用户体验和信任度。用户 Jasonsun77 是典型的“积极尝鲜、失望反馈”型用户，连续提交了 3 个关于桌面模式的细节问题。
- **沟通诉求：** 用户希望提供一个“解绑 GitHub 账号”的按钮，而不是通过后台数据库操作。这反映了某些功能入口的设计不够直观或自助化程度不足。
- **正面反馈：** 在 Issue #6775 中，用户 boktoday 在表达对病毒误报的担忧时，也明确表示“我喜欢你们的工作，谢谢你们所做的一切”，说明用户对项目愿景和团队的努力总体上是认可的。

---

#### 8. 待处理积压

以下 Issue 和 PR 已开放较长时间且未获充分响应或解决，建议维护者重点关注：

- **待响应的关键 Issue：**
    - **[Issue #6732](https://github.com/agentscope-ai/QwenPaw/issues/6732)**：MCP 工具规律性失效问题，有 6 条评论，是社区热点，但未见到官方确认或修复方案。
    - **[Issue #6490](https://github.com/agentscope-ai/QwenPaw/issues/6490)**：请求添加新 Provider，已开放 11 天，虽有评论但无官方回应。
    - **[Issue #6285](https://github.com/agentscope-ai/QwenPaw/issues/6285)**：请求添加新模型，已开放 18 天，无官方回应。

- **长期未合并的关键 PR：**
    - **[PR #4694](https://github.com/agentscope-ai/QwenPaw/pull/4694)**：网站下载页面重构 PR，已开放超过 2 个月，处于关闭状态。虽然关闭，但若该功能仍被需要，建议维护者说明原因或重新开启。
    - **[PR #6564](https://github.com/agentscope-ai/QwenPaw/pull/6564)**：修复内存压缩的 PR，已标记为 “Under Review”，但此状态已持续一周，希望尽快推进合并。

---
**结论：** CoPaw 项目本周期的开发速度非常快，社区参与度极高，但“Beta 版本质量”和“核心功能的稳定性”已成为当前最突出的矛盾。建议项目组在高速迭代的同时，将更多精力投入到 **Windows 平台的安装与兼容性测试**，以及 **MCP 长时运行稳定性**的排查上，并积极回应用户对安全软件误报的关切，以维持社区的信任和健康的用户生态。

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# ZeroClaw 项目动态日报 — 2026-08-08

*数据覆盖周期：2026-08-07 至 2026-08-08*

---

## 1. 今日速览

ZeroClaw 在过去 24 小时保持**高活跃度**，Issue 与 PR 更新量均达 50 条。**今日无新版本发布**，大量工作集中于 Web 工具面重构（`web_research` 子代理、浏览器自动化策略调整）和安全加固（shell 逃逸防护、子进程沙箱、配置加载器保护）。值得关注的是，今日集中爆发了多个 **P1 级安全与功能 Bug**（预算上限失效、`forbidden_paths` 不可达、Telegram 健康检查误报），从报告中可知安全审查成为最近一段时间的核心关注点。一个值得注意的信号是 **[PR #9835]** 将根包名从 `zeroclawlabs` 重命名为 `zeroclaw`，表明项目已取回 crates.io 所有权，进入品牌统一阶段。整体活跃度评估：**高**，社区讨论密度大，维护者响应速度有待观察（多项 PR 标记 `needs-author-action`）。

---

## 2. 版本发布

今日无新版本发布。

---

## 3. 项目进展

**今日合并/关闭的 PR（3 条）**

- 今日关闭/合并的 PR 数量较少（3 条），且数据概览中未单独列出合并条目，以下为最近的已关闭 PR 记录（来自 Issue 关闭的关联）：
  - **PR #9563**（`needs-author-action`）— fix(channels): populate the typed media envelope from Telegram，仍在等待作者动作。
  - **PR #9548** — fix(config): warn on risky Codex CLI extra args（处于开放状态）。
  
  备注：数据中已关闭/合并 PR 仅 3 条，但未提供具体清单；以下从今日开放 PR 中识别出**已推动的项目方向**。

**今日新开放 PR 中值得关注的方向（8 条）**

| PR | 方向 | 说明 |
|---|---|---|
| [**#9835**](https://github.com/zeroclaw-labs/zeroclaw/pull/9835) | 品牌统一 | 根包名 `zeroclawlabs` → `zeroclaw`，取回 crates.io 名称所有权 |
| [**#9828**](https://github.com/zeroclaw-labs/zeroclaw/pull/9828) | 配置安全性 | 为 agent 提供经过 operator 审批的配置编辑路径（替代直接 `echo > config.toml`） |
| [**#9827**](https://github.com/zeroclaw-labs/zeroclaw/pull/9827) | 安全加固 | 三个 shell 逃逸修复：sandbox wrap 丢弃工作目录、子进程逃逸、shell 子进程限制 |
| [**#9829**](https://github.com/zeroclaw-labs/zeroclaw/pull/9829) | Web 工具面 | `web_fetch` 大响应溢出到文件而非截断 |
| [**#9830**](https://github.com/zeroclaw-labs/zeroclaw/pull/9830) | Web 工具面 | 完整浏览器自动化改为 opt-in，与 `browser_open` 分离 |
| [**#9831**](https://github.com/zeroclaw-labs/zeroclaw/pull/9831) | Web 工具面 | web-search 结果长度限制 + DuckDuckGo 抓取路径加固 |
| [**#9833**](https://github.com/zeroclaw-labs/zeroclaw/pull/9833) | Web 工具面 | 新增 `web_research` 委托工具，将裸 `web_search` 限定到子代理 |
| [**#9826**](https://github.com/zeroclaw-labs/zeroclaw/pull/9826) | 安全（防御纵深） | CLI 拒绝在 agent 的 shell 派生的进程中运行（防提权） |

**综合判断：** 今日提交量集中在 **Web 工具面的收敛**（由 [**#9824**](https://github.com/zeroclaw-labs/zeroclaw/issues/9824) 驱动）与 **安全纵深加固** 两大块，反映出项目在打磨默认工具暴露面和收紧 agent 越权路径上的持续投入。

---

## 4. 社区热点

**Issue 侧：**

1. **[#8933 — RFC: Add cross-turn conversation correlation to OTel export](https://github.com/zeroclaw-labs/zeroclaw/issues/8933)**（评论 13，已关闭）
   - 诉求：会话级关联追踪，在 OTel 导出中携带 `gen_ai.conversation.id`（符合 OpenTelemetry Semantic Conventions v1.41.0）。该提案经过长时间讨论（约 1 个月），今日关闭（accepted），对可观测性领域有里程碑意义。

2. **[#9246 — RFC: Preserve Todo tracker configuration during ZeroCode ownership migration](https://github.com/zeroclaw-labs/zeroclaw/issues/9246)**（评论 12，已关闭）
   - 背景：与 PR #9013 相关联，讨论 ZeroCode 所有权迁移时的 TodoWrite 配置保留策略。已关闭，表明该 RFC 已达成共识。

3. **[#5937 — refactor: Unify providers architecture and reqwest client management](https://github.com/zeroclaw-labs/zeroclaw/issues/5937)**（评论 12，仍开放）
   - 已开放超过 3 个月，是 providers 架构统一的核心诉求。今日仍活跃（有更新），说明仍在讨论中，涉及面广。

**PR 侧：**

- 今日新开的 PR 评论区普遍安静（评论数为 undefined），讨论多发生在 Issue 中。长期开放的 **[#8965](https://github.com/zeroclaw-labs/zeroclaw/pull/8965)**（declarative auto-activation，XL）和 **[#9013](https://github.com/zeroclaw-labs/zeroclaw/pull/9013)**（TodoWrite 配置迁移，XL）虽无今日评论，但始终是社区长期关注的大改动。

---

## 5. Bug 与稳定性

按严重程度排列：

| 严重度 | Issue | 描述 | 状态 |
|---|---|---|---|
| **P1** | [**#9816**](https://github.com/zeroclaw-labs/zeroclaw/issues/9816) | Anthropic provider 成本始终报告 `$0.00`，预算上限永不触发 | 已确认，无 fix PR |
| **P1** | [**#9815**](https://github.com/zeroclaw-labs/zeroclaw/issues/9815) | `forbidden_paths` 对所有 `allowed_roots` 及工作区内的路径完全失效 | 已确认，无 fix PR |
| **P1** | [**#9805**](https://github.com/zeroclaw-labs/zeroclaw/issues/9805) | SOP auto 模式从 channel/cron 触发后永远卡在 step 1，不执行 | 已确认，无 fix PR |
| **P1** | [**#9811**](https://github.com/zeroclaw-labs/zeroclaw/issues/9811) | `/health` 对从未连接过的 Telegram 频道报 healthy（实际 404 持续 19 小时） | 已确认，无 fix PR |
| **P1** | [**#9786**](https://github.com/zeroclaw-labs/zeroclaw/issues/9786) | 畸形 `SOP.toml` 被静默丢弃，`sop list`/`validate` 均误报成功 | 已确认，无 fix PR |
| **P1** | [**#9770**](https://github.com/zeroclaw-labs/zeroclaw/issues/9770) | `cron update` 静默丢弃 declarative 任务中 6 个字段的修改 | 已确认，无 fix PR |
| **P1** | [**#9775**](https://github.com/zeroclaw-labs/zeroclaw/issues/9775) | OpenRouter 流式请求丢失 `provider_extra`（S1 工作流阻塞） | in-progress |
| **P1** | [**#9386**](https://github.com/zeroclaw-labs/zeroclaw/issues/9386) | Gemini API key 在 URL 中未被 `sanitize_api_error` 清理，泄漏到聊天 | 已关闭（已修复） |
| **P2** | [**#9656**](https://github.com/zeroclaw-labs/zeroclaw/issues/9656) | Telegram 审批等待期间 typing 指示器一直运行，造成阻塞假象 | 已确认 |
| **P2** | [**#9708**](https://github.com/zeroclaw-labs/zeroclaw/issues/9708) | daemon 服务 stdout/stderr 日志无大小/轮转/数量限制 | in-progress |
| **P3** | [**#9834**](https://github.com/zeroclaw-labs/zeroclaw/issues/9834) | `zeroclaw-runtime` 间歇性测试失败（进程级共享状态 + `model_switch`） | 新报告 |

**已有对应 fix PR 的：**
- **#9775** → 尚无 PR
- **#9386** → 已关闭（已修复）
- Shell 逃逸相关（#9815 的延伸）→ [**PR #9384**](https://github.com/zeroclaw-labs/zeroclaw/pull/9384)（symlink 逃逸，best-effort 缓解）+ [**#9827**](https://github.com/zeroclaw-labs/zeroclaw/pull/9827)（子进程逃逸修复）

**注意：** 今日有 6+ 个 P1 安全/功能 Bug，大量 Bug 集中在 **安全策略（forbidden_paths、预算、密钥清理）**和 **SOP 引擎**，说明项目近期的质量保障压力较大，维护者需要重点关注。

---

## 6. 功能请求与路线图信号

| Issue/PR | 需求 | 推断 |
|---|---|---|
| [**#9824**](https://github.com/zeroclaw-labs/zeroclaw/issues/9824) | 将默认 web 工具收敛为 `web_fetch` + `web_research` + `http_request` 三个动词，`web_search_tool` 移入研究子代理 | **高度可能纳入 v0.9**：已有 4 个配套 PR（#9829–#9833）落地该方向 |
| [**#9810**](https://github.com/zeroclaw-labs/zeroclaw/issues/9810) | 加载 [Agent Plugins](https://agent-plugins.org/) 1.0 标准插件包（`plugin.json` + `skills/` + `mcp.json`） | **方向明确**，符合"生态兼容"战略，但早期阶段（1 天前创建） |
| [**#9832**](https://github.com/zeroclaw-labs/zeroclaw/issues/9832) | `--features hardware` 编译失败（`aardvark-sys::AardvarkHandle` 导入错误） | 需紧急修复，关联 #8043（独立 crate 退役计划） |
| [**#9820**](https://github.com/zeroclaw-labs/zeroclaw/issues/9820) | NVIDIA NIM 下 calculator 工具输出 `<TOOLCALL>` 伪语法而非真实函数调用 | 提示需要模型适配层对 NIM 系模型的工具调用格式兼容 |
| [**#9821**](https://github.com/zeroclaw-labs/zeroclaw/issues/9821) | cron 工具不被 agent 自动调用，回退到 shell crontab（策略拦截） | 暴露工具选择/策略提示词的问题 |

**路线图信号：** 版本节奏上，当前处于 0.8.x 成熟期，从多项 PR 的规模（XL）和 RFC 讨论密度来看，下一个 minor（0.9.0）或 major 版本预计包含 **Web 工具面重构、配置编辑安全通道、以及大规模 providers/可观测性整合**（#5937、#9346）。

---

## 7. 用户反馈摘要

- **安全与配置的"策略无效"感**：#9815 中用户明确指出 "`forbidden_paths` has no effect on any path that also falls under `allowed_roots`"，这是配置系统"看起来有但实际未生效"的典型痛点，说明配置项的关系语义需要更清晰的文档和校验（用户建议在 `doctor` 命令中加入配置冲突检测）。
- **健康检查的"假阳性"挫败感**：#9811 中，用户发现 Telegram bot token 无效时，`/health` 仍报告 `"healthy"`——这导致自动化运维误判，"404 持续 19 小时仍报 healthy" 的体验极差。
- **SOP 引擎的"静默失败"**：#9786 中，畸形 SOP 被静默丢弃，用户表示 "indistinguishable from a typo or a deleted SOP"，这与 #9783（失败原因被丢弃）呼应，用户对"无声失败"模式明显不满。
- **模型兼容性困扰（Raspberry Pi 场景）**：#9820/#9821 两个 Bug 来自同一用户（@fabricioartur），在 aarch64 + NVIDIA NIM 模型组合下，工具调用格式与交互出现多个问题。这提示项目 **需要更多边缘设备 + NVIDIA NIM 的兼容性测试**。
- **成本追踪可信度被质疑**：#9816 中预算上限永不触发的 Bug 直接破坏了用户对 `zeroclaw status` 中成本数字的信任。
- **正向反馈**：#9386（Gemini API 密钥泄漏）修复后已关闭，社区对安全修复及时性表示认可。

---

## 8. 待处理积压

**长期未响应的关键 Issue：**

| Issue | 创建日期 | 标签 | 说明 |
|---|---|---|---|
| [**#5937**](https://github.com/zeroclaw-labs/zeroclaw/issues/5937) | 2026-04-20 | enhancement, provider, accepted | 统一 providers 架构，已开放 **110 天**，最后一次更新为今日 |
| [**#7130**](https://github.com/zeroclaw-labs/zeroclaw/issues/7130) | 2026-06-03 | security, accepted | workspace 级 `forbid(unsafe_code)`，已开放 **66 天** |
| [**#8424**](https://github.com/zeroclaw-labs/zeroclaw/issues/8424) | 2026-06-28 | RFC, needs-author-action | 工作区相对路径 `forbidden_paths` 增强，已开放 **41 天** |
| [**#8043**](https://github.com/zeroclaw-labs/zeroclaw/issues/8043) | 2026-06-20 | RFC, no-stale | 退役 aardvark-sys 独立 crate，已开放 **49 天**，今日有更新 |

**长期开放的 PR（需要维护者/作者关注）：**

| PR | 创建日期 | 标签 | 说明 |
|---|---|---|---|
| [**#8965**](https://github.com/zeroclaw-labs/zeroclaw/pull/8965) | 2026-07-11 | size:XL, needs-author-action | declarative auto-activation（XL 级），依赖 #9563，已开放 **28 天** |
| [**#9063**](https://github.com/zeroclaw-labs/zeroclaw/pull/9063) | 2026-07-14 | size:XL, needs-author-action | Hindsight memory 后端（stack 1/7），已开放 **25 天** |
| [**#8948**](https://github.com/zeroclaw-labs/zeroclaw/pull/8948) | 2026-07-10 | priority:p1 | MCP server 僵尸进程回收，已开放 **29 天**，等待 #9418 落地后 rebase |
| [**#8443**](https://github.com/zeroclaw-labs/zeroclaw/pull/8443) | 2026-06-28 | size:XL, needs-author-action | Matrix 单消息进度草稿，已开放 **41 天** |

**维护者提醒：**
- **多项 PR 卡在 `needs-author-action` 状态**，部分已超过 2 周（#8965、#9063、#8443、#9563），项目参与者需要注意保持响应节奏。
- **重大 RFC（#9246、#8933）已关闭但配套实现尚未推进**，需要明确实施计划。
- **rust 无 unsafe 目标（#7130）与 aardvark-sys 退役（#8043）形成依赖链**，建议排期协同处理。

---

*本报告由 AI 分析生成，数据来源：[github.com/zeroclaw-labs/zeroclaw](https://github.com/zeroclaw-labs/zeroclaw)。*

</details>

---
*本日报由 [agents-radar](https://github.com/kky-wollu/agents-radar) 自动生成。*