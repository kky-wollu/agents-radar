# OpenClaw 生态日报 2026-08-11

> Issues: 500 | PRs: 500 | 覆盖项目: 13 个 | 生成时间: 2026-08-10 22:42 UTC

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

# OpenClaw 项目动态日报 — 2026-08-11

> 数据来源: github.com/openclaw/openclaw 社区公开数据

---

## 1. 今日速览

今日 OpenClaw 社区呈现**极高的活跃度**，过去 24 小时 Issues 与 PR 更新均为 500 条满额。新开/活跃 Issue 383 条、关闭 117 条；待合并 PR 357 个、已合并/关闭 143 个。本周无新版本发布，但 `steipete` 主导的一大批代码质量与重构 PR（gateway typing facade、helper 去重、概念目录迁移）正在极速推进，另有数条高优先级 bug 修复进入就绪状态。社区侧，两条长期高热度 issue（#121058 静默回复失败复发、#7707 记忆信任标记）评论数持续上涨，表明**消息投递可靠性与提示注入安全**仍是用户最关切的方向。项目整体推进节奏**强劲、健康**。


## 2. 版本发布

本日无新版本发布。上一次版本线仍停留在 2026.7.x 系列。

> **注意**: 多条 PR 标记为 `merge-risk: 🚨 compatibility` 或 `🚨 security-boundary`，预示下一版本（2026.8.x）可能包含接口或行为变更，升级前建议关注 changelog。


## 3. 项目进展

今日无直接合并记录披露（数据未含合并/关闭 PR 明细列表），但 PR 池中大量新提交与迭代值得注意，主要集中在以下几类收尾与前瞻工作：

- **Gateway 内部架构收敛**: `steipete` 连续提交多条迁移 PR，包括将内部 agent turn 调用迁移至类型化门面（#121715）、数据库引导期所有权序列化（#121526）、OpenAI 代理 turn 延迟优化（#121687）、辅助概念目录重组（#121553）与公共 helper 去重合并（#121366, #121431）。侧面反映核心团队正对 gateway 进行一轮系统性瘦身与加固。
- **安全与诊断收敛**: 两条安全相关 PR 值得关注——provider 诊断统一脱敏（#121599）与 DM 隔离诊断准确性修复（#121741），均剑指此前多个安全洞察类 issue 的痛点。
- **会话状态可靠性**: `/stop` 误触发 restart recovery 修复（#121235）与 durable context 长会话卡死修复（#121647）进入就绪或作者修改状态。
- **渠道与应用功能**: Mattermost 进度/终稿分离（#120854)、Slack 线程 24 小时活跃窗口延长（#121708）、Cloud Workers 桌面应用与浏览器自主能力（#121475）、Control UI 团队密钥管理（#121724）等多个功能面 PR 处于等待作者定稿或维护者审核阶段。

综合来看，项目正在从功能堆叠期切换到**架构整理 + 稳定性加固期**。


## 4. 社区热点

| 排名 | Issue/PR | 标题 | 评论数 | 状态 |
|---|---|---|---|---|
| 1 | [#121058](https://github.com/openclaw/openclaw/issues/121058) | Silent reply failures still recurring after #116277 closed — no queued reply payload | 40 | OPEN |
| 2 | [#7707](https://github.com/openclaw/openclaw/issues/7707) | Memory Trust Tagging by Source | 33 | OPEN |
| 3 | [#42475](https://github.com/openclaw/openclaw/issues/42475) | Per-agent cost budget enforcement at the gateway level | 15 | OPEN |
| 4 | [#86519](https://github.com/openclaw/openclaw/issues/86519) | Agent repeats identical replies 2-10x on Telegram after 5.20 update | 15 | CLOSED |
| 5 | [#40001](https://github.com/openclaw/openclaw/issues/40001) | Write tool lacks append mode — isolated cron sessions destroy shared files | 13 | OPEN |

**热点诉求分析**:

- **#121058（40 条评论）**：静默回复失败在 #116277 关闭后仍然复发，且监控 cron 持续记录到新案例。该 issue 直接质疑维护者此前“已修复”的判断，社区对**消息投递可靠性的最终闭环**信心有所动摇。
- **#7707（33 条评论）**：记忆信任标记（Memory Trust Tagging）是社区长期高讨论度的安全增强请求——为记忆条目标记来源信任等级，防止恶意网页/第三方内容投毒。反映出**提示注入防御逐步从“应急补丁”走向体系化设计**。
- **#86519（关闭）**：Telegram 重复回复 bug 虽关闭，但此前“5.20 更新后重复 2-10 次、5.22 降为 2-3 次仍复现”的用户证词说明此类消息层问题对体感影响极大。


## 5. Bug 与稳定性

按严重程度排列（🟥 = P0/P1 高危，🟧 = P2 中危，🟨 = P3 低危/体验）：

### 🟥 高危（P0/P1）

| Issue | 标题 | 状态 | Fix PR |
|---|---|---|---|
| [#121058](https://github.com/openclaw/openclaw/issues/121058) | 静默回复失败在 #116277 修复后仍复发 | OPEN | 无 |
| [#115908](https://github.com/openclaw/openclaw/issues/115908) | Session 转写投影在持续写入下可活锁，阻塞主线程 | OPEN | 无 |
| [#111010](https://github.com/openclaw/openclaw/issues/111010) | Detached Codex 子代理在父 turn 释放后丢失原生工具 | OPEN | 无 |
| [#98702](https://github.com/openclaw/openclaw/issues/98702) | 继承的 OpenAI OAuth 在主代理成功、内建 runtime 代理被拒 | OPEN | 无 |
| [#119087](https://github.com/openclaw/openclaw/issues/119087) | Gateway 冷启动较 7.1-beta.1 回退 ~2.5x | OPEN | 无 |
| [#119333](https://github.com/openclaw/openclaw/issues/119333) | codex `request_user_input` 在 Default 模式暴露但运行时拒绝 | OPEN | 无 |
| [#100941](https://github.com/openclaw/openclaw/issues/100941) | 并行工具扇出下 Gateway 丢弃 WebSocket 连接（1006）| OPEN | 无 |
| [#83598](https://github.com/openclaw/openclaw/issues/83598) | anthropic:claude-cli OAuth 刷新在 5.12 仍失效 | OPEN | 无 |
| [#97983](https://github.com/openclaw/openclaw/issues/97983) | iOS/WebChat 消息追加至转写但不触发回复 | OPEN | 无 |

### 🟧 中危（P2）

| Issue | 标题 | 状态 | Fix PR |
|---|---|---|---|
| [#119796](https://github.com/openclaw/openclaw/issues/119796) | Windows 下 vitest teardown EBUSY（sqlite 句柄未释放）| OPEN | 有（[link](https://github.com/openclaw/openclaw/pull/121749) CI 探针） |
| [#119401](https://github.com/openclaw/openclaw/issues/119401) | DM 场景 NO_REPLY 抑制为无条件，无视 silentReply 策略 | OPEN | 无 |
| [#114020](https://github.com/openclaw/openclaw/issues/114020) | 7.2-beta.4 升级后 Feishu/Telegram 渠道分发失败 | OPEN | 无 |
| [#94919](https://github.com/openclaw/openclaw/issues/94919) | ECONNRESET 触发 fallback 但在 cron/子代理等异步场景不可见 | OPEN | 无 |
| [#120735](https://github.com/openclaw/openclaw/issues/120735) | Telegram 贴纸到达为原始文件引用且未暂存至磁盘 | OPEN | 有 |

### 🟨 低危/体验（P3+）

| Issue | 标题 | 状态 |
|---|---|---|
| [#33413](https://github.com/openclaw/openclaw/issues/33413) | Slack 助手线程状态仅显示“typing”而非具体工具进度 | OPEN |
| [#33102](https://github.com/openclaw/openclaw/issues/33102) | TUI `--deliver` 默认值缺乏 config 支持 | OPEN |
| [#45323](https://github.com/openclaw/openclaw/issues/45323) | Control UI 缺少 Slack 风格 @提及自动补全 | OPEN |

**特别关注**: 今日关闭了多条 P0/P1 历史遗留 issue（#43661 压缩超时挂起、#88870 长活跃运行被误中止、#93321 压缩保留孤儿 tool_use、#70334 压缩成功后会话锁死、#96242 重复 Telegram 消息、#84536 上下文溢出静默杀死内嵌会话），但 [#121058](https://github.com/openclaw/openclaw/issues/121058) 指出同类问题可能有**共性根因未除**——建议维护者核查上述关闭项是否真正闭环。


## 6. 功能请求与路线图信号

### 高可能性纳入（已有对应 PR 或维护者标记）

| 功能 | Issue | PR 或状态 |
|---|---|---|
| Gateway 层按代理成本预算强制（日/月上限） | [#42475](https://github.com/openclaw/openclaw/issues/42475) | OPEN，受社区关注 |
| 子代理工具权限隔离（per-spawn tool restrictions）| [#15032](https://github.com/openclaw/openclaw/issues/15032) | 有 linked PR |
| 从已注册项目启动会话（替代裸 host 路径）| — | PR [#121465](https://github.com/openclaw/openclaw/pull/121465) |
| 团队级密钥在 Control UI 可视化管理 | — | PR [#121724](https://github.com/openclaw/openclaw/pull/121724) |
| 子代理实时进度流式传输至任务事件 | — | PR [#121549](https://github.com/openclaw/openclaw/pull/121549) |
| WhatsApp poll 投票结果 hook | [#119254](https://github.com/openclaw/openclaw/issues/119254) | PR [#119256](https://github.com/openclaw/openclaw/pull/119256) |

### 社区高呼声、暂无 PR

| 功能 | Issue | 评论 | 备注 |
|---|---|---|---|
| 记忆来源信任标记（trust tagging） | [#7707](https://github.com/openclaw/openclaw/issues/7707) | 33 | 涉及安全架构设计，短期难落地 |
| `announceTarget` 子代理完成路由 | [#27445](https://github.com/openclaw/openclaw/issues/27445) | 12（👍5） | 多步工作流编排刚需 |
| context 超限时触发模型 fallback | [#9986](https://github.com/openclaw/openclaw/issues/9986) | 5 | 与现有 fallback 机制衔接需设计 |
| 备份 CLI 支持 .gitignore 式排除 | [#40786](https://github.com/openclaw/openclaw/issues/40786) | 9 | 实用性强、实现成本低 |
| 系统提示词注入 context 窗口占比 | [#38568](https://github.com/openclaw/openclaw/issues/38568) | 6（👍2） | 微小改动、高价值 |


## 7. 用户反馈摘要

### 核心痛点

- **消息丢失/重复仍是第一大信任杀手**： #121058（40 评论）与 #86519 用户的证词表明，**静默无回复**与**重复轰炸式回复**对生产可用性的伤害远超一般功能缺陷。
- **数据安全顾虑持续升温**：#7707 的 33 条评论集中体现了社区对“网页/第三方内容投毒记忆”的担忧；#40001 用户报告的“cron 会话用 write 工具覆盖共享 memory 文件”也进一步佐证了**会话隔离与数据保护机制**的不足。
- **自托管渠道插件受限**：#92516 用户反馈自托管容器无法信任外部化渠道插件（openKeyedStore 仅信任内置插件），**阻碍了 msteams 等渠道在自托管场景的落地**。
- **成本控制靠外部监控**：#42475 用户指出当前只能靠外部工具追踪 token 消耗，缺少 gateway 级成本预算闸门，**对生产运维构成经济风险**。

### 满意度信号

- 维护者对多条长期 issue 的关闭（#43661、#88870、#70334 等）展示了**持续跟进老问题的意愿**；但 #121058 的复发报告也提醒：**关闭 issue ≠ 真相闭环**，“关了就忘”会消耗社区信任。
- 功能请求（#33413 Slack 工具级进度、#28300 主题定制、#45323 @提及补全）多以 UX 体验细节为主，说明**核心消息链路之外，用户开始关注界面与交互打磨**。


## 8. 待处理积压

### 长期未响应的关键 Issue（更新超 30 天仍 OPEN）

| Issue | 标题 | 创建时间 | 最后更新时间 | 严重度 |
|---|---|---|---|---|
| [#7707](https://github.com/openclaw/openclaw/issues/7707) | Memory Trust Tagging by Source | 2026-02-03 | 2026-08-10 | P2（33 评论）|
| [#15032](https://github.com/openclaw/openclaw/issues/15032) | Per-spawn tool restrictions for sub-agents | 2026-02-12 | 2026-08-10 | P2（有 linked PR）|
| [#40001](https://github.com/openclaw/openclaw/issues/40001) | Write tool lacks append mode | 2026-03-08 | 2026-08-10 | P1（数据丢失）|
| [#83598](https://github.com/openclaw/openclaw/issues/83598) | anthropic:claude-cli OAuth 刷新失效 | 2026-05-18 | 2026-08-10 | P1 |
| [#89278](https://github.com/openclaw/openclaw/issues/89278) | Codex OAuth 10s 超时导致 cron/heartbeat 失败 | 2026-06-02 | 2026-08-10 | P1 |
| [#74986](https://github.com/openclaw/openclaw/issues/74986) | openclaw infer 在 4.27 上无限挂起（100% CPU） | 2026-04-30 | 2026-08-10 | P1 |

### 维护者提醒

- **#83598 与 #89278** 同属 OAuth 刷新链路问题，已跨 2-3 个月未解——**OAuth 稳定性是云端部署的基石，建议提升优先级**。
- **#40001** 导致 cron 会话直接覆盖共享记忆文件，属数据丢失类缺陷，且已有明确复现路径，建议尽快在 `write` 工具中增加 append/appendMode 选项。
- **#7707** 的 33 条评论与持续增长表明这是社区级安全共识，建议 RFC 流程中正式接纳设计讨论。

---

*日报生成时间: 2026-08-11 | 数据范围: 2026-08-10 ~ 2026-08-11*

---

## 横向生态对比

# 个人 AI 助手开源生态横向对比分析报告

**报告日期：2026-08-11 | 数据窗口：2026-08-10 ~ 2026-08-11**


## 1. 生态全景

个人 AI 助手/自主智能体开源生态正处于**从"功能堆叠"向"架构整理+安全加固"转型的关键阶段**。头部项目（OpenClaw、IronClaw、CoPaw）已跨越功能验证期，进入系统性的 gateway 架构收敛与稳定性攻坚；腰部项目（NanoBot、Hermes Agent、NanoClaw、ZeroClaw）则在快速迭代的同时面临合并积压与安全审计的双重压力；尾部项目（NullClaw、TinyClaw、ZeptoClaw）处于阶段性停滞。跨项目看，**消息投递可靠性（静默失败/重复回复）、提示注入防御（记忆投毒、工具权限隔离）、MCP 生态集成、多模型兼容性**是用户反馈最集中、技术投入最密集的四大主线。

值得强调的是，**"静默失败"已成为生态级信任危机**——OpenClaw #121058（40 评论）、PicoClaw #3311（工具循环无感知）、NanoClaw #3226（消息 ID 复用静默丢弃）、CoPaw #6782（Docker 市场不可用）等案例表明，用户对"失败无反馈"的容忍度已降至最低点，这应当是所有项目在下一阶段优先解决的体验底线问题。


## 2. 各项目活跃度对比

| 项目 | Issues 更新 | PR 更新 | 合并/关闭 | 待处理 | Release | 健康度 |
|------|------------|---------|----------|--------|---------|--------|
| **OpenClaw** | 500（新开 383 / 关闭 117） | 500（合并 143 / 待合并 357） | 260 | 357 PR | 无（7.x 线） | 🟢 强劲 |
| **IronClaw** | 50（新开 26 / 关闭 24） | 50（合并 19 / 待合并 31） | 43 | 31 PR | **v1.1.1-rc.1** | 🟢 优秀 |
| **CoPaw** | 40（新开 34 / 关闭 6） | 50（合并 20 / 待合并 30） | 26 | 30 PR | 无（v2.1.0 筹备中） | 🟢 良好 |
| **Hermes Agent** | 50（关闭 3） | 50（合并 0） | 3 | 44 PR | 无 | 🟡 活跃但积压 |
| **ZeroClaw** | 50（新开/活跃 50 / 关闭 0） | 50（合并 0） | 0 | 50 PR | 无 | 🟡 讨论密集/合并停滞 |
| **NanoBot** | 5（关闭 3） | 23（合并 10 / 待合并 13） | 13 | 13 PR | 无 | 🟢 高效 |
| **NanoClaw** | 4（新开 4） | 20（合并 10 / 待合并 10） | 10 | 10 PR | 无 | 🟢 良好 |
| **LobsterAI** | 1（关闭 1） | 33（合并 20 / 待合并 13） | 21 | 13 PR | 无 | 🟢 迭代快速 |
| **PicoClaw** | 4 | 9（合并 7） | 7 | 2 PR | 无（v0.3.1） | 🟢 稳健 |
| **Moltis** | 3（新开 3） | 1（更新 1） | 0 | 1 PR（4 个月） | 无 | 🟡 活跃度温和 |
| **NullClaw** | 1（关闭 1） | 1（Dependabot，搁置 57 天） | 1 | 1 PR | 无 | 🔴 停滞 |
| **TinyClaw** | — | — | — | — | — | ⚫ 无活动 |
| **ZeptoClaw** | — | — | — | — | — | ⚫ 无活动 |

**分层依据**：🟢 合并吞吐量高/迭代动能强；🟡 活跃但合并通道或 Bug 处置存在瓶颈；🔴 进入维护低谷期；⚫ 无可见活动。OpenClaw 以绝对体量（500+500）维持生态核心地位；IronClaw 以 50/50 的更新量配合 v1.1.1-rc.1 发布，展示了健康的迭代闭环；ZeroClaw 虽讨论活跃但 0 合并是本日最危险信号。

**关键警示**：Hermes Agent 与 ZeroClaw 均出现"高讨论、低合并"的剪刀差——社区投入热情充沛，但维护者响应速度不足以匹配，可能导致贡献者流失。建议两个项目优先清理合并通道（Hermes 的 44 个待合并 PR 与 ZeroClaw 的 50 个待合并 PR），而非继续吸纳新功能请求。


## 3. OpenClaw 在生态中的定位

**生态参照系：OpenClaw 是当前个人 AI 助手开源领域的"事实标准"与最大流量入口**，其社区体量（每日 500+500 的 Issue/PR 更新）是第二名 IronClaw 的 10 倍、NanoBot 的约 20 倍。

| 维度 | OpenClaw | IronClaw | NanoBot | Hermes Agent | CoPaw |
|------|----------|----------|---------|--------------|-------|
| **日活开发量** | 1000 条更新/日 | 100 条/日 | 28 条/日 | 100 条/日 | 90 条/日 |
| **核心定位** | 通用自主智能体运行时 | 企业级消息 Agent 平台 | 辅助工具型 Agent 网关 | 实验性 Agent 框架（Nous Research） | 多模态 Agent + 记忆系统 |
| **技术栈** | 多语言 Gateway（actix/axum） | Rust + WebAssembly 扩展 | Python + MCP SDK | Rust（疑似） | Python（agentscope）+ Tauri |
| **独特优势** | 渠道适配最广、社区最大 | Reborn 架构重构 + 租户隔离 | MCP 集成深度 + 社区反馈闭环速度快 | 桌面端 + Matrix E2EE + 多代理 Kanban | ReMe 记忆系统 + 多模态 |
| **主要短板** | 版本发布频率低（7.x 线停留） | 依赖升级积压 + 文件生成 bug | 体量小、Docker 权限支持缺失 | 合并通道严重堵塞、桌面端不稳 | Docker 市场不可用 + 第三方模型兼容性 |
| **安全态势** | 记忆信任标记、DM 隔离诊断、provider 诊断脱敏三线推进 | 架构审计制度化、租约恢复、权限隔离 | WebUI 迁移 WebSocket + OAuth 支持 | Matrix E2EE 验证补全 + 配置覆写修复 | 第三方提供商兼容性修复快速闭环，但 MCP 层工具调用稳健性欠缺 |
| **版本节奏** | 月级（7.x 停留近 6 周） | 双周+（v1.1.1-rc.1 今日发布） | 无固定节奏 | 无固定节奏 | 接近发布（v2.1.0 RC 中） |

**核心差异总结**：

- **OpenClaw vs IronClaw**：OpenClaw 走"大而全"路线，覆盖渠道/插件/WebUI，是社区生态的"操作系统层"；IronClaw 走"专而精"路线，聚焦企业级消息 Agent 场景（Slack/Telegram/Teams），以 Rust 性能与 WASM 扩展性为卖点，日活开发量约为 OpenClaw 的 1/10，但发布节奏更快、架构治理更制度化（Reborn 重构系列）。
- **OpenClaw vs NanoBot**：NanoBot 定位轻量级辅助 Agent（HKU DS 项目），在 MCP 集成深度（OAuth 浏览器授权、SDK v2 迁移）上走在前列，但体量差距悬殊，适合作为 OpenClaw 的轻量替代或实验场。
- **OpenClaw vs Hermes**：Hermes 背靠 Nous Research，在实验性功能（桌面 HUD、Matrix E2EE、Kanban 多代理）上更激进，但工程化成熟度落后——今日 44 个待合并 PR 与 TUI 核心功能 20 天未修复即为明证。
- **OpenClaw vs CoPaw**：CoPaw 继承了 OpenClaw 的网关架构基因（同为 gateway + provider 模式），但以 ReMe 记忆系统为差异点，在记忆检索质量（reranker + embedding 热更新）上建立了独有优势。二者是"同一技术路线的不同深度方向"——OpenClaw 做广度，CoPaw 做深度。


## 4. 共同关注的技术方向

以下为多项目同时涌现的需求信号，按共性强度排序：

### 4.1 消息投递可靠性（6/9 活跃项目）

| 项目 | 具体诉求 | 严重度 |
|------|----------|--------|
| OpenClaw | #121058 静默回复失败复发，40 评论 | P0 |
| OpenClaw | #86519 Telegram 重复回复 2-10 次 | 已关闭 |
| Hermes Agent | #83291 图片附件静默失败 | P1 |
| NanoClaw | #3226 消息 ID 复用静默丢弃 | P1 |
| NanoClaw | #3075 长时间运行后日志丢失 + 重复插入 | P1 |
| IronClaw | #7445 共享频道重复触发回复 | 已修复 |
| PicoClaw | #3311 工具循环失败无感知 | P1 |
| CoPaw | #6820 前端流式输出失效（全有或全无） | P2 |

**共性根因**：消息去重/幂等机制、错误传播到用户端的反馈链路、异步任务失败的可观测性，是跨项目普遍薄弱环节。

### 4.2 提示注入防御与安全边界（5/9 活跃项目）

| 项目 | 具体诉求 | 进展 |
|------|----------|------|
| OpenClaw | #7707 记忆信任标记，33 评论 | OPEN（设计讨论中） |
| NanoClaw | #3229 Telegram 配对码 CSPRNG | 修复 PR 待合并 |
| IronClaw | 架构审计系列 #7147/7149/7150/7151 | 已关闭 |
| ZeroClaw | 7 条 S0/S1 安全审计（LINE/Bluesky/WASI/审计日志） | 两周无修复 PR |
| Hermes Agent | #83488 Matrix E2EE curve25519 验证 | 修复 PR 待合并 |

**共性趋势**：安全从"应急补丁"走向"体系化设计"——记忆来源信任分级、工具权限隔离（per-spawn restrictions）、配置默认安全（secure-by-default）成为共识方向。

### 4.3 MCP 生态集成与工具调用稳健性（5/9 活跃项目）

| 项目 | 具体诉求 | 进展 |
|------|----------|------|
| NanoBot | #5316 浏览器 OAuth 授权（Xmind/Notion/Linear） | ✅ 已合并 |
| NanoClaw | #3092/#3221 远程 Streamable HTTP MCP | PR 迭代中 |
| CoPaw | #6405 工具 "Tool not found" | 19 天未修复 |
| CoPaw | #6839 数字字符串被强转 | 无修复 |
| ZeroClaw | #9339 自定义 CA 信任 | 无 PR |
| IronClaw | #6727 自定义 MCP 服务器支持 | ✅ 已关闭 |

**共性痛点**：MCP 工具调用的参数类型保持、OAuth 授权流程、故障隔离（单点 MCP 崩溃不应拖垮整个 gateway）是三大薄弱环节。

### 4.4 多模型/多 Provider 兼容性（4/9 活跃项目）

| 项目 | 具体诉求 | 进展 |
|------|----------|------|
| CoPaw | StepFun/Gemini/DeepSeek thinking-mode 兼容性 | #6809 已修复，尚余 3 个开放 |
| Hermes Agent | Mistral reasoning_effort 支持（8 👍） | 4 个月未落地 |
| OpenClaw | anthropic:claude-cli OAuth 刷新失效 | P1 积压 |
| ZeroClaw | OpenAI Chat Completions 端点 | PR #8486 待合并 |

**共性趋势**：第三方模型接入的"最后一公里"（OAuth 刷新、thinking-mode 回传、严格兼容模式的字段清洗）是跨项目普遍欠债。

### 4.5 成本控制与 token 用量透明化（3/9 活跃项目）

| 项目 | 具体诉求 | 进展 |
|------|----------|------|
| OpenClaw | #42475 Gateway 层成本预算强制 | 15 评论，OPEN |
| NanoBot | #5299 结构化 token 用量记录 API | conflict 待解决 |
| Hermes Agent | #83450 1M 上下文 compaction 成本平方增长 | 新发 |

**共性信号**：用户对 token 消耗的敏感度已从"事后追踪"升级为"事前闸门"，gateway 级成本控制将成为下一波功能需求。


## 5. 差异化定位分析

| 项目 | 功能侧重 | 目标用户 | 技术架构 | 核心差异化 |
|------|----------|----------|----------|------------|
| **OpenClaw** | 全能型个人 AI 助手（渠道/插件/WebUI/CLI） | 开发者、个人深度用户、社区生态参与者 | 多语言 Gateway（Rust + Python + Node），模块化插件体系 | **生态广度**：渠道适配数、插件数、社区规模均领先 |
| **IronClaw** | 企业级消息 Agent 平台（Slack/Teams/Telegram） | 企业团队、消息驱动的工作流用户 | Rust 核心 + WebAssembly 扩展 + Reborn 架构 | **工程化严谨度**：架构审计制度化、租户隔离、依赖管理规范 |
| **CoPaw** | 多模态 Agent + 记忆系统（ReMe） | 深度记忆需求用户、多模态场景 | Python（agentscope）+ Tauri 桌面端 + ReMe 记忆引擎 | **记忆系统深度**：reranker、embedding 热更新、Auto-Dream 容错 |
| **Hermes Agent** | 实验性 Agent 框架（桌面 HUD + Matrix E2EE） | 前沿功能尝鲜者、Matrix 生态用户 | Rust 核心 + 桌面端（Tauri?）+ 多代理编排 | **桌面端与隐私**：本地优先、E2EE、HUD 交互 |
| **NanoBot** | 轻量辅助型 Agent 网关 | 个人开发者、MCP 生态用户 | Python + MCP SDK + WebUI | **MCP 集成深度**：OAuth 浏览器授权、SDK v2 前瞻 |
| **ZeroClaw** | 社区驱动型 Agent 运行时 | 安全敏感用户、自托管部署者 | Rust? + WASM 插件 + 安全审计 | **安全审计体系**：批量 S0/S1 审计、WASI 策略控制 |
| **PicoClaw** | 轻量嵌入式 Agent | 树莓派等资源受限设备用户 | 轻量化架构 + 多渠道 | **资源效率**：低功耗设备运行 |

**关键差异点一句话总结**：OpenClaw 做"全"，IronClaw 做"稳"，CoPaw 做"深"，Hermes 做"新"，NanoBot 做"巧"，ZeroClaw 做"安"，PicoClaw 做"轻"。


## 6. 社区热度与成熟度分层

### 第一梯队：快速迭代 + 高合并吞吐（健康度 🟢）

| 项目 | 合并吞吐 | 特征 | 阶段 |
|------|----------|------|------|
| **OpenClaw** | 260 合并/日 | 架构整理 + 稳定性加固双线推进 | 成熟期，从功能堆叠切换到质量巩固 |
| **IronClaw** | 43 合并/日 | Reborn 重构收尾 + v1.1.1-rc.1 发布 | 快速迭代 + 质量巩固并行 |
| **LobsterAI** | 21 合并/日 | cowork 协作 UI 密集优化 + 网关稳定性修复 | 功能迭代密集期 |
| **CoPaw** | 26 合并/日 | v2.1.0 发布在即 + ReMe 三线推进 | 功能冲刺 + 兼容性修补 |

### 第二梯队：稳健推进 / 效率较高（健康度 🟢）

| 项目 | 合并吞吐 | 特征 | 阶段 |
|------|----------|------|------|
| **NanoBot** | 13 合并/日 | WebUI 安全重构 + MCP OAuth 快速闭环 | 高速功能迭代（回应速度快） |
| **NanoClaw** | 10 合并/日 | 架构模块化 + 远程 MCP 支持 | 功能扩展 + 架构硬化并行 |
| **PicoClaw** | 7 合并/日 | 安全硬化 + 渠道修复 | 稳定性加固期 |

### 第三梯队：活跃但存在瓶颈（健康度 🟡）

| 项目 | 合并吞吐 | 特征 | 瓶颈 |
|------|----------|------|------|
| **Hermes Agent** | 3 合并/日 | 桌面端多故障 + TUI 核心功能受阻 | **合并通道堵塞**：44 PR 待合并，P0 级修复滞留 |
| **ZeroClaw** | 0 合并/日 | 讨论密度高 + 安全审计积压 | **合并停滞**：50 PR 待合并，RFC 流程冗长 |
| **Moltis** | 0 合并/日 | 沙箱后端稳定性问题 + 长寿命 PR | **大型 PR 悬置**：4+ 个月未合入 |

### 第四梯队：维护低谷（健康度 🔴/⚫）

| 项目 | 合并吞吐 | 特征 |
|------|----------|------|
| **NullClaw** | 1 关闭 Issue | 近 3 天无新输入，依赖 PR 搁置 57 天 |
| **TinyClaw / ZeptoClaw** | 0 | 24 小时完全无活动 |


## 7. 值得关注的趋势信号

### 信号一：消息可靠性成为生态级信任底线

从 OpenClaw #121058（静默失败复发，40 评论）到 PicoClaw #3311（工具循环无感知），从 NanoClaw #3226（消息 ID 复用静默丢弃）到 IronClaw #7445（共享频道重复触发）——**"失败无反馈"已超越功能缺陷范畴，成为用户判定"这个 Agent 是否值得托付"的第一道门槛**。任何个人 AI 助手项目，若不能确保"每次失败都有明确、可感知的反馈"，将难以建立长期用户信任。

> **参考价值**：新项目在设计消息管线时应将"错误传播到用户端"作为一等公民需求，而非事后补充；已成熟项目应系统性审计所有静默失败路径。

### 信号二：记忆安全从"可选项"走向"默认要求"

OpenClaw #7707（记忆信任标记）的 33 条评论、PicoClaw #3297 的远程执行默认禁用、ZeroClaw 的 7 条批量安全审计、NanoClaw 的配对码 CSPRNG 加固——**安全不再是被动响应，而是主动设计**。用户开始要求：记忆按来源分级、工具按权限隔离、配置默认安全。这一趋势将在 2026 下半年持续深化，具备完善安全架构的项目将在企业级采纳中占据先机。

> **参考价值**：AI 助手开发者应将"来源可信度"纳入记忆系统设计的第一性原则；安全审计应常态化而非事件驱动。

### 信号三：MCP 正从"集成协议"演变为"生态入口"

NanoBot 的 MCP OAuth 授权（从 Issue 到合并仅 2 天）、NanoClaw 的远程 HTTP MCP 支持、CoPaw 的 MCP 工具参数稳健性问题、ZeroClaw 的自定义 CA 信任诉求——**MCP 已成连接 Agent 与外部工具链的"标准总线"**。能否提供稳定、安全、易用的 MCP 集成能力，将直接决定 Agent 的可扩展边界。对开发者而言，选择 MCP 生态支持深度的项目，等于选择未来的工具生态接入能力。

> **参考价值**：MCP 工具调用的"最后一公里"（参数类型保持、OAuth 流程、故障隔离）是当前共性欠债，也是差异化机会。

### 信号四：成本控制从"事后追踪"升级为"事前闸门"

OpenClaw #42475（Gateway 级成本预算，15 评论）、NanoBot #5299（结构化用量记录 API）、Hermes Agent #83450（1M 上下文成本平方增长）——**用户已不满足于"看账单"，而是要求"设上限"**。NanoBot 的 1000 万 token 消耗案例（Issue #5324）为整个生态敲响警钟：AI Agent 的自主执行若无成本闸门，可能产生失控性的资源消耗。这一需求将在生产级部署中愈发紧迫。

> **参考价值**：Agent 框架应将 token 计量与预算控制内置于 gateway 层，而非依赖外部监控工具。

### 信号五：架构治理走向制度化

IronClaw 的架构审计系列（#7147/7149/7150/7151 同日关闭）与 OpenClaw 的 gateway 类型化门面重构（#121715）表明——**头部项目已从"快糙猛"切换到"制度化技术债清理"**。ZeroClaw 的 RFC 流程简化讨论（#9496）也指向同一方向：当项目规模超过手工治理承载力时，自动化的板面流转、架构约束的 CI 强制、依赖升级的定期批量处理，将成为维持长期健康度的必要条件。

> **参考价值**：中大型 Agent 项目应尽早引入架构约束的 CI 审计（如 IronClaw 的 shrink-only 约束），避免技术债在快速迭代中失控。

### 信号六：多智能体协作从"概念"走向"真实负载"

Hermes Agent 的 Kanban 多代理系列（tracking issue #83376）、PicoClaw 的 dispatch rules 多 Agent 路由问题（#3301）、NullClaw 的 A2A 客户端工具（#700）、IronClaw 的子代理实时进度流式传输（#121549）——**多实例/多代理的互联互通、任务编排、会话隔离正在从演示走向生产**。NullClaw 用户自行实现 `a2a_call` 客户端工具填补官方空白，折射出用户对多 Agent 组网的真实需求未被主流项目充分满足。

> **参考价值**：多 Agent 场景的会话生命周期管理（/clear、自动压缩在路由场景下的一致性）与跨实例 A2A 协议支持，是下一波功能需求的候选方向。


**结语**：2026 年 8 月的个人 AI 助手生态，正在经历从"能做"到"可靠"的质变。消息投递的确定性、记忆安全的分级管控、MCP 生态的深度集成、成本控制的闸门化，构成了四大技术主轴。对不同角色的建议：**技术选型者**——优先关注合并吞吐量高 + 安全审计完善的头部项目（OpenClaw / IronClaw），并结合具体场景考察 MCP 生态支持深度；**生态参与者**——可把握 MCP OAuth 授权、消息可靠性审计、memory trust tagging 等共性痛点的第三方插件/工具机会；**底层框架开发者**——应将成本闸门、故障可观测性、来源可信记忆作为内建于框架的基础能力，而非可选的增值特性。

---

## 同赛道项目详细报告

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot 项目动态日报 — 2026-08-11

---

## 1. 今日速览

过去24小时 NanoBot 项目保持**高活跃度**：PR 活动频繁（23条），其中10条已合并/关闭，13条待处理；Issues 更新5条，其中3条已解决。核心开发集中在 WebUI 重构、MCP 集成稳定性与安全加固，社区持续反馈 provider 兼容性与资源消耗问题。值得关注的是，多个高优先级修复（P0/P1）已提交 PR 并有部分完成合并，整体项目健康度良好，但待合并队列中出现了多处 `conflict` 标记，需维护者及时处理。

---

## 2. 版本发布

**无新版本发布。**

---

## 3. 项目进展

今日合并/关闭的10条 PR 主要完成了以下推进：

### 3.1 MCP 与网关能力增强

- **[PR #5316] [已合并] feat(mcp): add browser OAuth for remote servers** — 为远程 Streamable HTTP 和 SSE MCP 服务器添加基于浏览器的 OAuth 授权支持，内置 Xmind、Notion、Linear 一键预设，并支持自定义 MCP 配置的 OAuth/Header 选择。直接回应了 Issue #5297 的功能诉求。  
  🔗 https://github.com/HKUDS/nanobot/pull/5316

- **[PR #5310] [已合并] fix(weixin): honor forced QR login** — 强制微信登录现在在 CLI 和 WebUI 均执行全新 QR 码流程，跳过已配置/持久化凭据。  
  🔗 https://github.com/HKUDS/nanobot/pull/5310

### 3.2 WebUI 安全与体验重构

- **[PR #5317] [已合并] fix(webui): move mutations to authenticated WebSocket requests** — 将 WebUI 所有状态变更操作从 GET/query-string/custom-header HTTP 调用迁移到已认证 WebSocket 连接上的关联 request/reply 帧，显著提升安全性（P1）。  
  🔗 https://github.com/HKUDS/nanobot/pull/5317

- **[PR #5315] [已合并] fix(webui): improve UX recovery and empty states** — 优化工作区级聊天创建失败时的恢复流程，保留首个提示词和拒绝的项目路径，改进认证挑战界面。  
  🔗 https://github.com/HKUDS/nanobot/pull/5315

- **[PR #5318] [已合并] refactor(webui): extract deterministic event projection helpers** — 将 `useNanobotStream` 中的确定性投影逻辑提取为独立工具模块，推理完成时间改为显式输入。  
  🔗 https://github.com/HKUDS/nanobot/pull/5318

- **[PR #5319] [已合并] refactor(agent): replace reflective runtime state access** — 用显式 `RuntimeControl` 协议替换 `MyTool` 的反射式循环状态包装，红act凭据字段，集中管理运行时变更。  
  🔗 https://github.com/HKUDS/nanobot/pull/5319

### 3.3 WebUI 架构演进

- **[PR #5321] [已合并] refactor(webui): make gateway own settings services** — 引入网关持有的 WebUI 设置服务，显式配置路径 + 序列化原子读-改-写操作，WebUI OAuth 流状态移入网关作用域注册表。  
  🔗 https://github.com/HKUDS/nanobot/pull/5321

### 3.4 Bug 修复

- **[PR #5325] [已合并] fix(files): reject no-op edits** — 拒绝 `edit_file` 中 `old_text` 与 `new_text` 完全相同的调用，返回可操作错误而非虚假成功。直接修复 Issue #5324（Dream 记忆整理无限循环）。  
  🔗 https://github.com/HKUDS/nanobot/pull/5325

**整体评估**：WebUI 安全与架构重构已取得关键进展；MCP OAuth 功能从 Issue 提出到 PR 合并仅 2 天，响应速度出色。项目正在为更复杂的多会话工作台（PR #5322）铺路。

---

## 4. 社区热点

### 热点一：MCP OAuth 网页授权支持（Issue #5297 → PR #5316）
- **Issue**：https://github.com/HKUDS/nanobot/issues/5297  
- **PR**：https://github.com/HKUDS/nanobot/pull/5316  
- 用户 sunboy0523 提出 Xmind MCP 等需要网页授权的服务无法配置，建议通过 gateway 获取授权信息。该诉求在 2 天内即被 PR #5316 实现并合并，是今日社区反馈最快闭环的案例。

### 热点二：Dream 记忆整理无限循环消耗 10M+ tokens（Issue #5324）
- 🔗 https://github.com/HKUDS/nanobot/issues/5324  
- 用户 jermeyhu 报告 Dream 记忆整理任务在 `edit_file` 接受无意义编辑时陷入无限循环，23 分钟内消耗超过 1000 万 tokens（约半个月用量）。此问题已由 PR #5325 修复（拒绝 no-op 编辑），是今日最严重的资源消耗问题。

### 热点三：MCP 连接失败导致网关崩溃（Issue #5300）
- 🔗 https://github.com/HKUDS/nanobot/issues/5300  
- 远程 MCP 返回 HTTP 530 时，anyio cancel scope 跨任务崩溃导致网关进程崩溃/卡死、CPU 飙升。该问题关注度较高，涉及 MCP SDK 1.29.0 异常处理路径，目前无直接 fix PR，但 PR #5179（MCP SDK v2 迁移）可能从架构层面解决。

---

## 5. Bug 与稳定性

| 严重程度 | Issue | 描述 | 状态 |
|---------|-------|------|------|
| **P0** | — | 会话后台任务保存竞态（PR #5271 修复中）——`/new` 期间 `maybe_generate_webui_title` 等后台任务可能覆写新会话数据 | 🔧 已有 PR #5271 待合并 |
| **P1** | [#5300](https://github.com/HKUDS/nanobot/issues/5300) | MCP 连接失败未隔离，anyio cancel scope 跨任务崩溃导致网关崩溃/CPU 飙升 | ⏳ 观察中，PR #5179 可能从架构层面解决 |
| **P1** | — | Docker 容器权限下降能力缺失（CI 未覆盖真实 entrypoint 路径） | 🔧 已有 PR #5320 待合并 |
| **P2** | [#5324](https://github.com/HKUDS/nanobot/issues/5324) | Dream 记忆整理在 `edit_file` 接受 no-op 编辑时无限循环，消耗 10M+ tokens | ✅ 已修复（PR #5325 合并） |
| **P2** | [#5327](https://github.com/HKUDS/nanobot/issues/5327) | 推理过程中随机重复同一消息 | ⏳ 新报告，待排查 |
| **P2** | [#5311](https://github.com/HKUDS/nanobot/issues/5311) | Agnes AI provider 将嵌套对象工具参数双重编码为 JSON 字符串，导致 MCP tool call 失败 | 🔧 已有 PR #5314 待合并 |

---

## 6. 功能请求与路线图信号

### 已实现（今日合并）
- **MCP 浏览器 OAuth 授权**（PR #5316）— 社区强烈需求的远程 MCP 网页授权功能已落地，内置 Xmind/Notion/Linear 预设
- **WebUI 变更操作迁移至 WebSocket**（PR #5317）— 安全架构升级

### 待合并（有望进入下一版本）
- **OrcaRouter 作为命名网关 provider**（PR #5328）— 单一端点接入 150+ 模型，具备网关级零信任安全特性
- **Agent Plugins 与 CLI Apps 集成**（PR #5288）— 推动 nanobot 成为通用宿主
- **结构化 token 用量记录 API**（PR #5299）— 新增 `GET /api/settings/usage/records` 按日查询
- **Tabbed Pane 工作台**（PR #5322）— 每个 Topic 内支持 1-4 个 Pane 会话，网格/行列/主从布局

### 潜在信号
- **MCP SDK v2 迁移**（PR #5179）— 可能解决 Issue #5300 的架构性根因
- **设置后端按领域拆分**（PR #5323）— 模块化演进方向

---

## 7. 用户反馈摘要

- **正面反馈**：社区对 MCP OAuth 功能的快速响应表示认可（从提出到合并仅 2 天）；微信强制 QR 登录修复获得关注。
- **资源消耗痛点**：Issue #5324 暴露了 `edit_file` 工具缺少 no-op 校验导致 AI 循环消费巨额 tokens，用户明确表示"约半个月用量被消耗"，说明 token 计量和防护机制仍需加强。相关修复 PR #5299（结构化用量记录）可能部分满足用户对用量透明化的需求。
- **Provider 兼容性**：Agnes AI 用户遭遇嵌套对象参数双重编码问题（Issue #5311），反映出 OpenAI-compatible provider 的边界情况处理仍需完善。
- **稳定性诉求**：MCP 连接失败导致整个网关崩溃（Issue #5300），用户期望故障隔离，避免单点 MCP 服务影响全局。
- **WebUI 体验**：PR #5315 和 #5326 持续优化交互细节（认证挑战、表单焦点样式），说明 UI 打磨进入精细化阶段。

---

## 8. 待处理积压

### 需维护者关注

| 类型 | 编号 | 描述 | 标记 | 状态 |
|------|------|------|------|------|
| PR | [#5179](https://github.com/HKUDS/nanobot/pull/5179) | MCP SDK v2 迁移（含 legacy 兼容） | `conflict`, **P1** | 未更新超过11天，需解决冲突并推进 |
| PR | [#5271](https://github.com/HKUDS/nanobot/pull/5271) | 防止后台任务覆写会话数据 | **P0** | 待合并，影响数据安全 |
| PR | [#5299](https://github.com/HKUDS/nanobot/pull/5299) | 结构化 token 用量记录 API | `conflict` | 待解决冲突 |
| PR | [#5257](https://github.com/HKUDS/nanobot/pull/5257) | 绑定持续目标续传上限 | `conflict` | 防止 token 浪费关键修复 |
| Issue | [#5300](https://github.com/HKUDS/nanobot/issues/5300) | MCP 连接失败导致网关崩溃 | **P1** | 无直接 fix，建议优先评估 PR #5179 |

### 冲突警告
当前有 4 条 PR（#5179、#5299、#5257、#5323）带有 `conflict` 标记，建议维护者优先解决，避免积压扩大。

---

*本报告基于 NanoBot (github.com/HKUDS/nanobot) 截至 2026-08-11 的 GitHub 数据生成。*

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent 项目动态日报 — 2026-08-11

---

## 1. 今日速览

过去 24 小时项目活跃度极高，共产生 50 条 Issue 更新和 50 条 PR 更新，多数为新提交内容，表明社区提交动力强劲。值得警惕的是，**桌面端（Desktop/TUI）稳定性问题集中爆发**，至少 8 个新 Issue 涉及 HUD 模式故障、渲染器崩溃、后端进程泄漏等问题，且多个 PR 正在并行修复中。此外，**Matrix 适配器的 E2EE 安全验证缺陷**在今日被同一作者连续提交多个 Issue 和对应修复 PR，体现了社区对安全问题的快速响应。**P0 级 Issue 缺失但多条 P2 级别的"感官体验"类 Bug（如 overlay 不可见）持续多日未合入修复**，是潜在的健康度风险信号。无新版本发布，但 44 个 PR 待合并，合并通道存在一定积压。

---

## 2. 版本发布

无新版本发布。

---

## 3. 项目进展

今日无直接合并的 PR 记录，但以下高价值 PR 处于**待合并状态**，一旦合入将显著推进项目稳定性：

| PR | 关键改进 | 状态 |
|---|---|---|
| [#83202](https://github.com/NousResearch/hermes-agent/pull/83202) — `fix(gateway/desktop): durable row-id addressing for rewind truncation` | **P0 级修复**：会话回退（rewind）/编辑/重新生成改为基于持久化 SQLite row_id 寻址，解决因用户轮次序号漂移导致的错误截断（Issue #82959） | OPEN |
| [#83490](https://github.com/NousResearch/hermes-agent/pull/83490) — `fix: bound gateway database and output handles` | 将 per-thread SQLite 读取器替换为固定四连接池，解决资源耗尽风险；复用进程级 stdout/stderr 代理 | OPEN |
| [#83485](https://github.com/NousResearch/hermes-agent/pull/83485) — `fix(delegation): identify internal completion events` | 为异步委托任务的终止事件增加稳定的事件信封，覆盖正常完成与崩溃恢复场景 | OPEN |
| [#83488](https://github.com/NousResearch/hermes-agent/pull/83488) — `fix(matrix): verify curve25519 and self-signature in device-key checks` | 补全 Matrix 设备密钥验证（curve25519 比对 + 自签名验证），修复 [#83481](https://github.com/NousResearch/hermes-agent/issues/83481) 安全缺陷 | OPEN |
| [#71548](https://github.com/NousResearch/hermes-agent/pull/71548) — `fix(gateway): coalesce concurrent native OAuth refresh requests` | 合并并发 OAuth 刷新请求，避免刷新令牌竞争；增加负面缓存吸收重试风暴 | OPEN |
| [#76527](https://github.com/NousResearch/hermes-agent/pull/76527) — `fix(terminal): prevent profile home snapshot leaks` | 修复终端环境快照跨 profile 泄漏 HERMES_HOME 的问题 | OPEN |

**信号**：桌面端与会话管理是本阶段的核心攻坚方向，6 个高相关 PR 同时处于开放状态，显示重构/修复力度在加强。

---

## 4. 社区热点

| 话题 | 热度指标 | 诉求分析 |
|---|---|---|
| [#69592](https://github.com/NousResearch/hermes-agent/issues/69592) — TUI `/sessions` 和 `/models` overlay 不可见（ambient widget dock 场景） | **11 评论，持续 20 天**（Day 13+），作者持续更新影响面 | 核心 TUI 工作流（切换会话/切换模型）已经中断两周，且 `/reload` 静默失败。该 Issue 标注 `sweeper:risk-session-state`，涉及用户日常高频操作，**优先级应为 P0 但当前停留于 P1**，社区耐心在消耗 |
| [#11243](https://github.com/NousResearch/hermes-agent/issues/11243) — Mistral AI 原生 `reasoning_effort` 支持 | **8 👍 + 6 评论**，自 4 月持续至今 | 用户明确需要 Mistral 的可调推理能力接入 Hermes，已提出精确的注入方案和模型家族守卫规则，属于**高确定性、可落地的功能请求** |
| [#58596](https://github.com/NousResearch/hermes-agent/issues/58596) — Python 3.14 兼容性：`DaemonThreadPoolExecutor` 崩溃 | **3 👍 + 6 评论** | 影响所有并发特性（delegate_task、异步委派、技能扇出、内存同步）。Python 3.14 用户群体正在扩大，该兼容性修复的优先级应上调 |
| [#83450](https://github.com/NousResearch/hermes-agent/issues/83450) — compaction 阈值无上限，1M 上下文模型成本平方增长 | 新发 Issue，响应迅速 | 用户在 Long-context 场景下的成本敏感度很高，compaction 策略需要更精细的配置能力 |

---

## 5. Bug 与稳定性

按严重程度排序（🔴 = 严重 / 🟠 = 中等 / 🟡 = 轻微）：

### 🔴 高严重度（阻断核心功能）

| Issue | 描述 | 状态 |
|---|---|---|
| [#69592](https://github.com/NousResearch/hermes-agent/issues/69592) | **TUI 会话/模型 overlay 不可见**，影响所有使用 ambient widgets 的用户 | OPEN 20+ 天，无 fix PR |
| [#83456](https://github.com/NousResearch/hermes-agent/issues/83456) | **Windows 更新回退会删除 Hermes.exe**，无失败回滚机制（重复 Issue） | OPEN，有 [#52508](https://github.com/NousResearch/hermes-agent/pull/52508) 相关但非直接修复 |
| [#83450](https://github.com/NousResearch/hermes-agent/issues/83450) | 1M 上下文模型 compaction 首次触发在 500K，长对话账单呈二次方增长 | OPEN |

### 🟠 中严重度（影响特定场景但可绕过）

| Issue | 描述 | 状态 |
|---|---|---|
| [#80898](https://github.com/NousResearch/hermes-agent/issues/80898) | macOS 桌面端反复重启导致 `hermes serve` 孤儿进程积累（内存泄漏） | OPEN |
| [#83482](https://github.com/NousResearch/hermes-agent/issues/83482) | Linux 桌面关窗后孤儿后端；SIGTERM 不升级为 SIGKILL（重复 Issue） | OPEN |
| [#83473](https://github.com/NousResearch/hermes-agent/issues/83473) | Linux/X11 (Xfce) HUD 点击穿透后无法重新武装，需重启 | OPEN |
| [#83484](https://github.com/NousResearch/hermes-agent/issues/83484) | 定时任务针对已关闭的 API 会话**无限重试** | OPEN |
| [#83291](https://github.com/NousResearch/hermes-agent/issues/83291) | 桌面图片附件预分析失败时静默丢弃整个回合（无响应） | OPEN |
| [#63395](https://github.com/NousResearch/hermes-agent/issues/63395) | Matrix 加密房间投递成功但随后数据库池停止报错并断开 | OPEN |
| [#83338](https://github.com/NousResearch/hermes-agent/issues/83338) | OAuth 刷新覆写 `~/.claude/.credentials.json` 并丢弃 subscriptionType，Claude Code 降级为 API-key 模式 | OPEN |
| [#83481](https://github.com/NousResearch/hermes-agent/issues/83481) + [#83468](https://github.com/NousResearch/hermes-agent/issues/83468) | Matrix 设备密钥验证缺失 curve25519/自签名检查；`mau.crypto` 非 TraceLogger 时 E2EE 静默中断 | OPEN，有 [#83488](https://github.com/NousResearch/hermes-agent/pull/83488) 修复 PR |
| [#83378](https://github.com/NousResearch/hermes-agent/issues/83378) | disk-cleanup 插件误删工具安装树中的 `test_*`/`tmp_*` 文件，破坏 npm/pyright 安装 | OPEN |

### 🟡 轻微（体验问题）

| Issue | 描述 |
|---|---|
| [#83362](https://github.com/NousResearch/hermes-agent/issues/83362) | HUD 模式"退出 HUD"按钮被裁剪到可视区域外 |
| [#83017](https://github.com/NousResearch/hermes-agent/issues/83017) | Windows HUD 模式无法通过应用内控制退出 |
| [#83380](https://github.com/NousResearch/hermes-agent/issues/83380) | 产物页面时间戳按毫秒解析秒级数据，全部显示 1970 年 1 月；图片无法显示 |
| [#83359](https://github.com/NousResearch/hermes-agent/issues/83359) | Wayland 原生环境下 GPU 内存压力导致渲染器表面损坏 |

---

## 6. 功能请求与路线图信号

| 功能请求 | 潜在纳入版本判断 |
|---|---|
| [#11243](https://github.com/NousResearch/hermes-agent/issues/11243) Mistral `reasoning_effort` 原生支持（8 👍） | 方案已明确，需求真实，**预计可在下个小版本落地** |
| [#83467](https://github.com/NousResearch/hermes-agent/issues/83467) WhatsApp self-chat 模式标记回复为未读（异步消息被标记为已读） | 当前为 P3 功能请求，但使用场景清晰，有望随 WhatsApp 适配器更新一并合入 |
| [#83487](https://github.com/NousResearch/hermes-agent/pull/83487) SkillSeal 技能认证/验证技能（新 PR） | 已在 PR 阶段说明为 bundle 技能，**路线图已明确** |
| [#83479](https://github.com/NousResearch/hermes-agent/issues/83479) 桌面 Home 会话列表无新建按钮 | P3 体验改进，可作为桌面端后续迭代项 |
| [#57369](https://github.com/NousResearch/hermes-agent/pull/57369) 项目级可信 MCP 基础（`.hermes/`） | 大特性 PR，已持续 40 天，合并后将成为多项目支持的重要基础设施 |
| [#83667](https://github.com/NousResearch/hermes-agent/pull/63667) Kanban 调度器失败生命周期钩子 | 已并入 tracking issue [#83376](https://github.com/NousResearch/hermes-agent/issues/83376)，目前处于多 PR 协同推进阶段 |

**路线图信号**：`kanban multi-agent` 系列（[#83376](https://github.com/NousResearch/hermes-agent/issues/83376) tracking issue）是当前最明确的路线图主线，涵盖 review 循环、上下文交接、成本分摊、合并仲裁等多个子项，预计将持续多周。

---

## 7. 用户反馈摘要

### 痛点聚焦

1. **TUI 核心功能不可用已超过两周**（[#69592](https://github.com/NousResearch/hermes-agent/issues/69592)）：用户 `apoapostolov` 持续更新影响，评论数 11 条，情绪从报告故障转向"何时修复？"，社区耐心正在被消耗。

2. **桌面端更新/关闭操作存在破坏性行为**（[#83456](https://github.com/NousResearch/hermes-agent/issues/83456)、[#80898](https://github.com/NousResearch/hermes-agent/issues/80898)）：
   > "The updater wiped the packaged build output during git-reset + ZIP-fallback steps" — 更新失败已删除可执行文件，且无回滚机制。

3. **配置文件被静默覆写**（[#83338](https://github.com/NousResearch/hermes-agent/issues/83338)）：OAuth 刷新导致 Claude Code 订阅降级，用户数据被破坏且无提示。
   > "The write emits at most 4 keys; the dropped keys include `subscriptionType`... downgrading Claude Code to API-key mode"

4. **图片附件功能不可靠**（[#83291](https://github.com/NousResearch/hermes-agent/issues/83291)）：拖拽单个图片静默失败，但拖入文件夹正常，说明文件处理路径存在不一致。

5. **磁盘清理插件危险**（[#83378](https://github.com/NousResearch/hermes-agent/issues/83378)）：自动清理在会话结束时**静默删除** npm/pyright 安装文件，属于数据破坏类 Bug。

### 满意点

- Matrix E2EE 安全问题被社区主动发现并快速提交修复 PR（[#83488](https://github.com/NousResearch/hermes-agent/pull/83488)），安全响应链路通畅。
- Kanban 多代理改进有专门跟踪 Issue（[#83376](https://github.com/NousResearch/hermes-agent/issues/83376)）和 4 个相关 PR 协同推进，社区协作机制运转良好。

---

## 8. 待处理积压

| 积压项 | 持续时间 | 状态与建议 |
|---|---|---|
| [#69592](https://github.com/NousResearch/hermes-agent/issues/69592) TUI overlay 不可见 | **20 天**，P1 未升级 | 影响核心工作流，强烈建议升级为 P0 并指派 fix PR |
| [#11243](https://github.com/NousResearch/hermes-agent/issues/11243) Mistral reasoning_effort | **4 个月**，8 👍 | 方案已明确，建议纳入近期迭代计划 |
| [#58596](https://github.com/NousResearch/hermes-agent/issues/58596) Python 3.14 兼容崩溃 | **37 天**，影响所有并发特性 | Python 3.14 用户群扩大中，建议作为兼容性 P1 处理 |
| [#57369](https://github.com/NousResearch/hermes-agent/pull/57369) 项目级可信 MCP 基础 | **40 天**待合并 | 大型特性 PR，建议维护者评审后合入 main 分支进行 beta 验证 |
| [#82816](https://github.com/NousResearch/hermes-agent/issues/82816) 会话标题生成在 OpenAI 兼容端点上 100% 失败（`json_schema`→`guided_grammar` 转换） | 新发（8 月 10 日） | 涉及 vLLM/xgrammar 生态，建议增加对非 JSON Schema 后端的兼容检查 |
| [#83308](https://github.com/NousResearch/hermes-agent/issues/83308) `plugins.enabled` 字符串值静默卸载所有插件 API | 新发（8 月 10 日） | 配置损坏后的 404 与"未安装"不可区分，建议增加配置校验及错误提示 |

---

## 健康度总评

| 维度 | 评分 | 说明 |
|---|---|---|
| **Issue 处理效率** | ⭐⭐☆☆☆ | 50 条更新中仅 3 条关闭；多个 P1/P2 级 Bug 积压超 2 周 |
| **PR 合并速度** | ⭐⭐☆☆☆ | 44 条待合并，核心修复（如 #83202 P0）滞留时间过长 |
| **社区活跃度** | ⭐⭐⭐⭐⭐ | 24 小时 100 条 Issue/PR 更新，新 Bug 反馈及时，修复响应快（如 Matrix 安全） |
| **安全响应** | ⭐⭐⭐⭐⭐ | Matrix E2EE 安全问题从发现到 PR 提交在一日内完成 |
| **稳定性趋势** | ⭐⭐☆☆☆ | 桌面端多故障点集中爆发，Windows 更新破坏性问题重现，TUI 核心功能持续受阻 |

**结论**：社区提交动力强劲、安全响应敏捷，但**合并通道和 Bug 处置效率是当前瓶颈**。桌面端稳定性和 TUI 核心可用性是近期最值得关注的健康度风险。建议维护者优先合并 P0/P1 修复 PR（#83202、#83490、#83488），并重新评估「长期开放且影响核心功能」的 Issue 优先级策略。

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw 项目动态日报 — 2026-08-11

## 今日速览

PicoClaw 在过去 24 小时保持了**稳健活跃**的维护节奏：4 条 Issue 更新和 9 条 PR 更新，反映出社区反馈与代码贡献的双向流动。值得关注的是，当前活跃议题集中在**工具调用可靠性**（shell 命令守卫、重复失败死循环）和**远程安全边界**两大方向，且均已有对应修复 PR 在途，说明维护者对关键问题响应及时。此外，两个来自社区的新功能/修复 PR（Telegram 原生表格渲染、pnpm lockfile 修复）在一天内被合并，体现了外部贡献的高效吸收。代码质量与安全问题依然是本周的焦点。

## 版本发布

在报告周期内，没有新的正式版本发布。最近的稳定版本仍为 **v0.3.1**。不过，多个已合并的修复（如安全硬化、通道修复和配置改进）可能要等到下一个版本才能与用户见面，建议关注上游可用的预发布构建。

---

## 项目进展

本周期内合并/关闭的 7 个 PR 涵盖了从安全、国际化到前端构建的多个方面，项目在**稳定性与安全加固**上明显推进：

- **安全硬化（重大）**：PR [#3297](https://github.com/sipeed/picoclaw/pull/3297) 由 SiYue-ZO 提交，集中加固了远程提示与执行边界。该 PR 将远程发送者元数据从系统指令中分离、默认禁用远程执行并引入独立按次审批、在运行时执行来源策略，同时将配置迁移至 schema v4。这是一个**破坏性变更**，涉及安全模型调整，升级时可能需要手动迁移配置。
- **通道稳定性**：PR [#3295](https://github.com/sipeed/picoclaw/pull/3295) 修复了 `SplitMessage` 在超大围栏头部时的挂起问题，对 Discord/Telegram 长消息场景是重要的健壮性提升。
- **Telegram 原生表格渲染**：PR [#3327](https://github.com/sipeed/picoclaw/pull/3327) 是一个亮点功能改进，使 Telegram 回复能用 Bot API 富消息渲染真正的表格，而非退化为等宽代码块。该 PR 在一天内被合并，表明维护者对提升用户体验持积极态度。
- **前端构建修复**：PR [#3326](https://github.com/sipeed/picoclaw/pull/3326) 移除了 `pnpm-lock.yaml` 中的重复条目，修复了 `pnpm install --frozen-lockfile` 报错的问题，对 Web 前端开发者是直接的利好。
- **国际化**：PR [#3296](https://github.com/sipeed/picoclaw/pull/3296) 补全了捷克语代码换行标签。

---

## 社区热点

本周期社区讨论最集中的是 **Issue #3301**（[链接](https://github.com/sipeed/picoclaw/issues/3301)）：`/clear` 与会话自动压缩在基于 dispatch rules 路由到非默认 agent 的聊天中失效。该问题拥有 3 条评论，涉及 Raspberry Pi 环境下的 Discord/Telegram 双通道。用户的诉求核心是**多 Agent 路由场景下的会话生命周期管理**，这反映了 PicoClaw 正被更多用户用于复杂的多代理架构，而不仅是简单的单会话聊天。

另一条值得关注的讨论是 **Issue #3311**（[链接](https://github.com/sipeed/picoclaw/issues/3311)），关于工具重复失败导致静默空转直到 `max_tool_iterations`，用户在生产环境的 Telegram 上发了一条要求执行 `git` 命令的消息却永远得不到回复。这条 Issue 引发的共鸣指向一个**核心可用性问题：失败时用户完全无感知**，而这直接关联到对应的修复 PR #3312。

---

## Bug 与稳定性

| 严重程度 | Issue | 状态 | 修复 PR |
|---|---|---|---|
| **高**（静默死循环，用户得不到任何响应） | [#3311](https://github.com/sipeed/picoclaw/issues/3311) 工具反复以相同错误失败，循环至 `max_tool_iterations`，用户永远得不到答案 | OPEN | [#3312](https://github.com/sipeed/picoclaw/pull/3312)（OPEN），机制：识别连续相同错误时提前终止轮次 |
| **中**（特定配置下核心会话功能失效） | [#3301](https://github.com/sipeed/picoclaw/issues/3301) `/clear` 与自动压缩在 dispatch 路由至非默认 agent 时失效 | OPEN | 暂无 |
| **中**（安全机制误伤合法命令） | [#3314](https://github.com/sipeed/picoclaw/pull/3314) `customAllowPatterns` 未生效，默认拒绝模式始终优先导致 `git push` 被拦截 | OPEN（含修复） | 即 PR #3314 本身 |
| **低**（命令行为与预期不符） | [#3294](https://github.com/sipeed/picoclaw/issues/3294) `/list models` 只展示当前模型而非全部配置模型 | CLOSED | 已关闭（状态未知） |

---

## 功能请求与路线图信号

- **AI Router 官方预设（已关闭）**：Issue [#3298](https://github.com/sipeed/picoclaw/issues/3298) 请求将 AI Router 作为 OpenAI 兼容 provider 的命名预设。虽已关闭，但若能以低成本支持可发现性，仍可能在未来版本中以“provider 预设”的形式演进。
- **模型级 `max_tokens` 配置（PR 已关闭）**：PR [#2132](https://github.com/sipeed/picoclaw/pull/2132) 提出支持模型特定的 `max_tokens` 参数并修复配置键冲突。该 PR 已关闭，但延期时间较长，若需求依旧强烈，后续有重新开启或采用的潜力。
- **多 Agent 场景下的会话管理**：来自 Issue #3301 的信号，随着 dispatch rules 的使用增多，用户会愈发期望 `/clear`、自动压缩等会话操作在**所有**路由下保持一致行为。这应纳入后续版本的重点验证范围。

---

## 用户反馈摘要

- **Remote exec 安全预期的分歧**：从 PR #3297 的改动（默认禁用远程执行）可见，用户对安全的诉求在该项目中快速升级。有用户在 Issue #3314 中反映，**安全机制过于严格导致允许列表形同虚设**，这是**安全性与便利性之间的典型张力**，未来在配置易用性方面仍有很大优化空间。
- **工具循环时缺乏用户反馈**：Issue #3311 描述了明确的痛点：工具反复失败时用户端完全无感知，直到最终超时。这类体验会严重影响生产环境用户对项目的信任。
- **Raspberry Pi + 多渠道**：Issue #3301 的作者在 Raspberry Pi 上通过 Discord 和 Telegram 运行 PicoClaw，说明轻量级本地部署仍是重要的使用场景，资源受限设备上的行为一致性值得持续关注。

---

## 待处理积压

⚠️ 以下项长期未获得充分关注，提醒维护者留意：

1. **PR #2132**：`feat(config): support model-specific max_tokens and fix config key conflicts`（由 dtapps 提交，创建于 2026-03-28，仍处于关闭状态）。该 PR 提出的模型级参数覆盖，在未来支持更细粒度模型配置时可能仍具参考价值。
2. **PR #1547**：`fix: merge PR #1466 #1465`（由 xuwei-xy 提交，创建于 2026-03-14，已合并）。历史合并请求，若关联的 #1466、#1465 尚未关闭，建议核实其修复是否已完整进入主分支。
3. **Issue #3301**：虽然信息丰富，但目前没有直接关联的修复 PR，作为活跃的多 Agent 场景 Bug，建议尽快分配责任人并评估复现方案。

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw 项目动态日报

**日期：2026-08-11** | **数据窗口：2026-08-10 至 2026-08-11**


## 1. 今日速览

NanoClaw 在过去 24 小时内保持了**非常高的社区活跃度**，共产生 4 条 Issue 更新和 20 条 PR 更新，其中 10 条 PR 已合并/关闭，10 条仍待合并。核心开发团队（core-team 标记）主导了多项重大架构演进，包括 Agent Plugins 1.0.0 格式迁移、远程 Streamable HTTP MCP 服务器支持，以及主机文件访问的单一写入者声明重构。**安全与稳定性是今日主题**：多个 PR 与 Issue 聚焦 Telegram 配对码 CSPRNG 加固、DM 日志隐私脱敏、入站消息去重及路由错误静默丢失等关键问题。值得关注的是，`dweekly` 和 `zvi-fried` 两位贡献者今日均有较多产出，社区协作氛围良好。整体来看，项目正处于积极的功能扩展和架构硬化并行阶段。


## 2. 版本发布

今日无新版本发布。


## 3. 项目进展

今日共 **10 条 PR 被合并或关闭**，覆盖安全加固、架构重构、文档完善等多个维度：

### 安全加固（已合并）
- **[PR #3222] feat(permissions): add opt-in privacy-safe DM logs**（[链接](https://github.com/nanocoai/nanoclaw/pull/3222)）— 新增 `privacySafeLogs` 可选配置，启用后省略用户 ID、句柄、消息组 ID 和原始适配器错误，保留非识别性通道上下文。默认保持现有详细日志行为。
- **[PR #3215] fix(permissions): redact DM resolution logs**（[链接](https://github.com/nanocoai/nanoclaw/pull/3215)）— 修复 DM 解析日志中敏感信息未脱敏的问题。

### 架构重构（已合并）
- **[PR #3186] refactor: add host seams for skill-owned capabilities**（[链接](https://github.com/nanocoai/nanoclaw/pull/3186)）— 为技能自有能力添加主机接缝层。
- **[PR #3213] refactor(channels): register question renderers**（[链接](https://github.com/nanocoai/nanoclaw/pull/3213)）— 将问题渲染器改为注册制。
- **[PR #3214] refactor(host): unify module lifecycle hooks**（[链接](https://github.com/nanocoai/nanoclaw/pull/3214)）— 统一模块生命周期钩子。
- **[PR #3212] refactor(db): add module migration registry**（[链接](https://github.com/nanocoai/nanoclaw/pull/3212)）— 新增模块迁移注册表。

### 文档与修复（已合并/关闭）
- **[PR #3216] docs(hardened-image): note that install_packages covers apt and npm only**（[链接](https://github.com/nanocoai/nanoclaw/pull/3216)）— 明确文档说明 `install_packages` 仅支持 apt 和 npm。
- **[PR #3211] docs(skills): define single-responsibility integration rule**（[链接](https://github.com/nanocoai/nanoclaw/pull/3211)）— 定义技能单一职责集成规则。
- **[PR #3228] fix: deduplicate turn-scoped chat delivery**（[链接](https://github.com/nanocoai/nanoclaw/pull/3228)）— 修复回合范围内聊天投递的重复问题。

**项目推进评估**：上述合并的 PR 为后续的 Agent Plugins 1.0.0 迁移和远程 MCP 支持奠定了基础设施（模块注册表、生命周期统一、主机接缝），项目整体正从单体架构向更模块化、可扩展的方向演进。


## 4. 社区热点

今日最受关注的讨论集中在以下两个方向：

### A. 入站消息静默丢失问题（Issue #3226）
[dweekly](https://github.com/nanocoai/nanoclaw/issues/3226) 报告了一个**影响用户信任度的高危问题**——当平台在同一会话中复用消息 ID 时，入站消息被静默丢弃，用户视角与"agent 无视我"无法区分。该问题在数小时内即获得修复 PR（[#3224](https://github.com/nanocoai/nanoclaw/pull/3224)），显示维护者对消息可靠性的高度重视。

### B. 长时间运行后的日志静默丢失 + 消息重复插入（Issue #3075）
[libellebilai-collab](https://github.com/nanocoai/nanoclaw/issues/3075) 报告了 WSL2 + Docker Desktop + Matrix 通道环境下长时间运行后的双重问题：日志静默丢失和入站消息重复插入错误。该 Issue 虽已创建近一个月，但今日仍有更新（8-10），评论 1 条，社区关注度稳定。该问题与 #3226 存在潜在关联（均涉及消息 ID 处理）。


## 5. Bug 与稳定性

按严重程度排列：

| 严重度 | Issue/PR | 描述 | 状态 |
|--------|----------|------|------|
| 🔴 高 | [#3226](https://github.com/nanocoai/nanoclaw/issues/3226) | 平台复用消息 ID 时入站消息静默丢弃，用户无法感知 | 有修复 PR [#3224](https://github.com/nanocoai/nanoclaw/pull/3224)，待合并 |
| 🔴 高 | [#3075](https://github.com/nanocoai/nanoclaw/issues/3075) | 长时间运行后日志静默丢失 + 入站消息重复插入错误 | 开放中，无明确修复方案 |
| 🟡 中 | [#3223](https://github.com/nanocoai/nanoclaw/issues/3223) | 定时任务执行出错时产生不可路由的错误消息被静默丢弃，操作者无法感知任务失败 | 开放中，无修复 PR |
| 🟡 中 | [#3229](https://github.com/nanocoai/nanoclaw/pull/3229) | Telegram 配对码使用 `Math.random()` 生成，可预测 | 修复 PR 待合并 |
| 🟢 低 | [#3225](https://github.com/nanocoai/nanoclaw/pull/3225) | 配对目录及存储文件权限过于宽松 | 修复 PR 待合并 |


## 6. 功能请求与路线图信号

### 高概率纳入下版本的功能

1. **Agent Plugins 1.0.0 格式迁移**（[PR #3220](https://github.com/nanocoai/nanoclaw/pull/3220)）— core-team 主导的格式迁移，将 agent templates 转化为 Agent Plugins 1.0.0 目录。此 PR 还包含安全加固（stamp-time symlink/caps/secret 硬化），属于架构级变更。配套的 setup 向导流程（[PR #2909](https://github.com/nanocoai/nanoclaw/pull/2909)）自 7 月初持续迭代至今，预计将随 1.0.0 一起落地。

2. **远程 Streamable HTTP MCP 服务器支持**（[PR #3092](https://github.com/nanocoai/nanoclaw/pull/3092) + [PR #3221](https://github.com/nanocoai/nanoclaw/pull/3221)）— 核心团队在推进引擎层 + Claude provider 支持 `{ type: 'http', url }` 格式的 MCP 服务器配置，配套 PR 将支持扩展到 codex 和 opencode provider。

3. **CLI 有界 JSON 标准输入**（[PR #3218](https://github.com/nanocoai/nanoclaw/pull/3218)）— zvi-fried 为 `ncl` 客户端添加 `--stdin-json` 输入模式，以有界方式接收结构化参数，不改变现有请求帧和命令注册表。

### Python 包管理支持的需求信号
[Issue #3217](https://github.com/nanocoai/nanoclaw/issues/3217) 明确要求 `install_packages` 增加 pip 通道，以支持 Python 依赖的 agent 采用加固预构建镜像。当前文档 PR（[#3216](https://github.com/nanocoai/nanoclaw/pull/3216)）只是记录了限制，但社区对此的需求是真实且迫切的。


## 7. 用户反馈摘要

- **"不可区分于被无视"的痛点**：Issue #3226 报告者明确指出，入站消息静默丢失从用户侧看与"agent 忽略了我"无法区分，这直接打击了用户对 agent 的信任。消息可靠性的任何隐患都值得最高优先级处理。
- **长时间运行稳定性隐忧**：Issue #3075 的 WSL2 环境问题虽属特定配置，但"日志静默丢失"和"重复插入"表明项目在长尾场景下的稳定性验证仍有不足。
- **定时任务失败不应被静默吞掉**：Issue #3223 报告的定时任务错误消息不可路由的问题，反映了设计上"agent 选择投递目标"的理念虽然灵活，但错误场景下的兜底策略缺失。
- **加固镜像采用障碍**：Issue #3217 显示的 pip 通道缺失导致 Python 依赖的 agent 无法使用加固镜像，这直接影响企业级采纳。用户需要的不是文档说明限制，而是补齐功能。


## 8. 待处理积压

### 长期未响应的重点 Issue

| Issue | 创建时间 | 持续天数 | 备注 |
|-------|----------|----------|------|
| [#3075](https://github.com/nanocoai/nanoclaw/issues/3075)：长时间运行后的日志丢失 + 重复插入 | 2026-07-17 | 25 天 | 今日仍有更新，已有一个修复方向（#3224 侧面解决 ID 复用问题），但完整的日志丢失根因仍未定位 |
| [#3092](https://github.com/nanocoai/nanoclaw/pull/3092)：远程 Streamable HTTP MCP 服务器 | 2026-07-19 | 23 天 | PR 已存在 23 天，今日有配套 PR (#3221) 补充，说明核心团队仍在积极迭代，但合并时间未定 |
| [#2909](https://github.com/nanocoai/nanoclaw/pull/2909)：setup 向导模板流程 | 2026-07-02 | 40 天 | 最长寿的未合并 PR，依赖 #3220 的格式迁移，两者属于同一个大功能的不同阶段，建议维护者统筹合并节奏 |

### 提醒
- [#3193](https://github.com/nanocoai/nanoclaw/pull/3193)（Telegram Chat SDK 富消息更新）已开放 5 天，无 core-team 响应，建议确认其优先级。

---

*本日报由 AI 自动生成，数据截至 2026-08-11。所有链接指向 nanocoai/nanoclaw 仓库。*

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

# NullClaw 项目动态日报 — 2026-08-11

> 数据来源：github.com/nullclaw/nullclaw | 统计窗口：2026-08-10 ~ 2026-08-11

---

## 1. 今日速览

NullClaw 项目在过去 24 小时内活跃度较低，属于**微热状态**。仅有关闭 Issue 1 条、待合并 PR 1 条（Dependabot 自动依赖更新），无新版本发布，也无新开 Issue。值得注意的是，**最近 3 天内没有任何新 Issue 或 PR 产生**，社区输入处于停滞期。一条搁置近 5 个月的 Issue（#700）于昨日关闭，表明维护者对 PR 积压开始进行清理，但整体节奏偏慢。从活动水平看，项目目前处于维护期而非高速迭代期。

---

## 2. 版本发布

**无新版本发布**。最近一次发布记录暂无，建议维护者考虑在近期打一个版本 tag 以汇总已有的 commits。当前主干分支上的 docker 镜像依赖更新 PR 已挂起近 2 个月（详见第 3 节），版本冻结期间未做镜像层变更。

---

## 3. 项目进展

**今日无 PR 被合并或关闭**，仅 Dependabot 提交的依赖更新 PR #956 仍处于开放待合并状态：

- **[#956] ci(deps): bump alpine from 3.23 to 3.24 in the docker-images group**（[链接](https://github.com/nullclaw/nullclaw/issues/956)）— 将 Docker 基础镜像从 Alpine 3.23 升级至 3.24。该 PR 已挂起 **57 天**，非功能性变更，不引入破坏性改动，但长期不合并会导致基础镜像停留在 EOL 版本，存在安全风险。建议维护者尽快处理。

**唯一进展**是昨日关闭的 #700 Issue（见第 4 节），说明其关联 PR 已被合入或放弃，但这并未反映在今日的 PR 数据中。

**总体评价**：项目今日无实质代码推进，技术债清理暂缓。

---

## 4. 社区热点

今日唯一有实质内容的 Issue 为 **#700（已关闭）**，链接：[nullclaw/nullclaw Issue #700](https://github.com/nullclaw/nullclaw/issues/700)

- **作者**：georgeglarson | **创建于**：2026-03-23 ，**关闭于**：2026-08-10 | **评论**：1 | 👍：1
- **内容**：作者实现了 `a2a_call` 客户端工具，使 nullclaw 能够通过 JSON-RPC 向远程智能体发送 `message/send` 请求，填补了项目 **A2A 协议（v0.3.0）只有服务端实现、缺少客户端能力**的空白。作者的实际使用场景是运行两个 nullclaw 实例（公共门卫 + 私有个人助手）之间的互联互通。

**背后的诉求分析**：虽然该 Issue 评论数不高，但反映出一个清晰的真实需求——**用户需要 nullclaw 实例之间的互相调用能力**。A2A 协议的服务端已就绪，但缺少客户端支持使得多实例部署无法真正组网。此类需求可能在未来多智能体协作场景中变得更加重要。

---

## 5. Bug 与稳定性

**今日无新增 Bug 报告**，无崩溃、回归或安全漏洞相关 Issue。

**基础设施层面的潜在风险**（非 bug 但值得注意）：

| 风险项 | 严重程度 | 说明 | 缓解措施 |
|---|---|---|---|
| Docker 基础镜像长期未升级（PR #956 挂起 57 天） | 中 | Alpine 3.23 已过维护窗口，存在已知 CVE 风险 | 尽快合并 #956 |

---

## 6. 功能请求与路线图信号

今日无新增功能请求。结合近期动态，**#700 的关闭意味着 `a2a_call` 客户端工具的开发工作已阶段性收尾**（无论是否合入），这恰好补全了 A2A 协议的客户端部分。该功能与此前关于多实例部署的社区讨论相互呼应，存在被纳入下一版本的可能性。

**路线图信号**：项目对 A2A 协议双向能力（服务端+客户端）的支撑正在走向完整，指示未来版本将围绕**去中心化多智能体互联**展开。若 #700 的 PR 被合入，建议维护者在下一版本 Release Notes 中重点突出该能力，并补充多实例部署的使用文档。

---

## 7. 用户反馈摘要

基于 #700 及其评论内容，提炼出以下用户洞察：

- **真实痛点**：A2A 协议支持不完整——服务端已有，客户端缺失，导致用户需要自行开发客户端桥接层。Issue #700 正是用户为解决这一痛点自建的工具。
- **使用场景**：多 nullclaw 实例部署（公共边界 + 私有个人智能体）的互联互通需求明确。
- **满意度信号**：该用户愿意花时间实现并提交代码，说明对项目架构的认可度高，但也暗示对官方功能推进速度存在不满（"has no client-side implementation"）。
- **隐性需求**：希望项目在文档中明确展示多实例通信的标准方案，减少重复造轮子。

---

## 8. 待处理积压 ⚠️

以下为长期未获得维护者响应的条目，建议优先处理：

| 编号 | 类型 | 标题 | 挂起时长 | 链接 | 备注 |
|---|---|---|---|---|---|
| #956 | PR | bump alpine from 3.23 to 3.24 | **57 天** | [链接](https://github.com/nullclaw/nullclaw/issues/956) | 非功能变更，合并成本低，建议近期处理 |
| — | Issue | #700 虽已关闭，但关联的 `a2a_call` 实现是否有对应 PR 合入/拒绝，需维护者补充说明 | 5 个月 | [链接](https://github.com/nullclaw/nullclaw/issues/700) | 关闭原因应在 Issue 中注明 |

---

## 项目健康度总评

| 维度 | 评分（5分制） | 说明 |
|---|---|---|
| 代码活跃度 | ⭐⭐ | 近 24h 几乎无代码活动，依赖更新也无人处理 |
| 社区参与度 | ⭐⭐ | 讨论稀少，仅 1 条 Issue 关闭 |
| 维护响应速度 | ⭐⭐ | Dependabot PR 积压 57 天，响应偏慢 |
| 项目方向明确性 | ⭐⭐⭐⭐ | A2A 双向支持的推进方向明确，具备长期价值 |

**建议行动项**：①尽快合并/关闭 #956；②确认 #700 关联 PR 的最终去向并在 Issue 中标注；③适时发布一个版本 tag 汇总近期 commits，重振社区活跃度。

---
*报告生成时间：2026-08-11 | 数据窗口：2026-08-10 ~ 2026-08-11 | 来源：GitHub Public API*

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw 项目动态日报 — 2026-08-11

## 1. 今日速览

IronClaw 在过去 24 小时内保持高强度迭代节奏：共处理 50 条 Issue（26 条活跃/新开、24 条关闭）和 50 条 PR（31 条待合并、19 条已合并/关闭），并发布了一个紧急补丁候选版本 **v1.1.1-rc.1**。核心团队（BenKurrek、serrrfirat、henrypark133 等）持续推进 Reborn 架构重构系列工作，包括架构约束审计（#7147、#7149、#7150、#7151）、Telegram 产品补全、以及 WebUI 和 CLI 的多项稳定性修复。值得关注的是，新开 Issue 中出现两个大型 Epic（#7467 持久化 profile 无关化、#7465 Company Brain FDE），同时多个 v1.3.0 目标功能（Extensions vNext、设计系统、Admin AI 配置）正在活跃推进。项目整体健康度良好，社区活跃，但 CI 存储配额和依赖升级积压值得留意。

---

## 2. 版本发布

### ironclaw-v1.1.1-rc.1（2026-08-10）

**发布性质：** 1.1 线紧急补丁候选版本

**重点内容：**
- **通道投递与配对（Channel delivery & pairing）修复**
- **IronHub/自定义 MCP 兼容性改进** — 与 #6727（自定义 MCP 服务器支持）相呼应
- **WebUI 流式传输稳定性增强**
- **持久化检索（durable retrieval）修复**
- **从 1.0.0 和 1.1.0 的安全升级路径**

**破坏性变更：** 无明确破坏性变更列出。

**迁移注意：**
> **从 1.0.0 升级：** 需停止所有写入操作（"Stop all writers"）。建议部署前仔细阅读完整 Release Notes 并按官方升级指引操作。

> 该版本为 RC 候选版，建议在生产环境部署前进行充分验证。

🔗 [查看 Release](https://github.com/nearai/ironclaw/releases)

---

## 3. 项目进展

今日合并/关闭的 PR 和 Issue 集中在以下几个方向：

### 渠道与消息体验
- **[PR #7446] 渠道运行状态指示器** — 为 Slack/Telegram 添加了新的工作状态提示：轮转的等待文案、失败状态、进度提醒，并统一了工作状态的一致性。已关闭。 [链接](https://github.com/nearai/ironclaw/pull/7446)
- **[PR #7445] 共享频道 @提及 触发修复** — 修复了共享频道中每条线程消息都触发 bot 响应的问题（此前实测导致同一 DM 发送 3 次、重复回复多条）。已关闭。 [链接](https://github.com/nearai/ironclaw/pull/7445)

### Telegram 产品补全（v1.1.0 目标）
- **[Issue #6733] 已关闭** — manifest 声明的 `/model` 和 `/status` 命令现已在 Telegram、Slack、WebUI 三个渠道上一致可用。 [链接](https://github.com/nearai/ironclaw/issues/6733)
- **[Issue #6483] 已关闭** — "Telegram 产品完整性" Epic 收尾，附件支持和命令管线打通。 [链接](https://github.com/nearai/ironclaw/issues/6483)

### 技能与 MCP
- **[Issue #6727] 已关闭** — 自定义/任意 MCP 服务器连接支持已落地（v1.1.0 目标）。 [链接](https://github.com/nearai/ironclaw/issues/6727)
- **[Issue #6941] 已关闭** — 技能自创建/自发现/自选择 Epic 关闭。 [链接](https://github.com/nearai/ironclaw/issues/6941)

### 架构治理与文档
- **[Issue #6926] 已关闭** — 将 IronClaw crates 迁移至十族布局（Ten-family layout），让所有权模型在磁盘上可见。 [链接](https://github.com/nearai/ironclaw/issues/6926)
- **多项架构审计问题关闭** — #7145、#7147、#7149、#7150、#7151 均已在今日关闭，标志着 Reborn 架构目标审计（epic #3773）的阶段性成果。 [查看 #7149](https://github.com/nearai/ironclaw/issues/7149) | [查看 #7151](https://github.com/nearai/ironclaw/issues/7151)

### 新提交的 PR（需关注）
- **[PR #7456] 持久化存储 profile 无关化**（XL）— 将 Reborn 存储直接挂载至 `IRONCLAW_REBORN_HOME` 下 profile 无关命名空间，并通过安全封套防止重启切换导致的租户隔离弱化。关联 Epic #7467。 [链接](https://github.com/nearai/ironclaw/pull/7456)
- **[PR #7471] 租约过期恢复安全执行**（XL）— 修复进程心跳共享连接池饥饿导致的 `lease_expired` 用户可见故障。 [链接](https://github.com/nearai/ironclaw/pull/7471)

---

## 4. 社区热点

### 最热 Issue 分析

| Issue | 标题 | 评论数 | 状态 |
|-------|------|--------|------|
| [#7137](https://github.com/nearai/ironclaw/issues/7137) | live-canary 分片产物 700MB–1.5GB，需排除可再生产物 | 12 | OPEN |
| [#7145](https://github.com/nearai/ironclaw/issues/7145) | WS2: extension_host → loops 重分层 | 4 | CLOSED |
| [#6257](https://github.com/nearai/ironclaw/issues/6257) | PDF 发送/生成报 "Invalid value (attachments.mime_type)" | 3 | OPEN |
| [#7147](https://github.com/nearai/ironclaw/issues/7147) | 两个 shrink-only 架构约束在主分支上携带未跟踪松弛 | 3 | CLOSED |
| [#5882](https://github.com/nearai/ironclaw/issues/5882) | Slack 反复重连后认证流程进入损坏状态 | 3 | CLOSED |

**热点分析：**

1. **#7137 最受关注（12 条评论）** — CI 产物体积失控引发开发者广泛讨论。单次 live-canary 运行产物超过 5GB，且 GitHub Actions 存储仅保留 14 天。背后诉求是**降低 CI 存储成本、提升调试效率**。已有对应 PR #7466（Trim live-QA shard artifacts）提交，方向正确。

2. **#7147 架构约束"名存实亡"** — 架构文档声称的约束在实际代码中未被强制，且三个 PR 持有同一基线的三个不同值。这类 issue 的高评论说明**社区对架构治理的严肃性有较高期待**。

> 💡 趋势判断：架构治理类问题（#7147、#7149、#7150、#7151）密集出现并获得快速关闭，说明 Reborn 重构的"技术债清理"已进入制度化阶段。这对项目长期健康度是强积极信号。

---

## 5. Bug 与稳定性

### 严重级别排序

| 级别 | Issue/PR | 描述 | 状态 |
|------|----------|------|------|
| 🔴 高 | #5882 | Slack 反复重连后认证流程进入不可恢复的损坏状态，唯一的恢复方式是卸载重装扩展 | 已关闭 |
| 🔴 高 | PR #7471 | 进程心跳连接池饥饿导致用户可见的 `lease_expired` 运行失败（run artifact: `8d64abb9`） | 待合并 |
| 🟠 中 | #6257 | 发送/生成 PDF 文件时报 `Invalid value (attachments.mime_type)` 错误 | OPEN（无 fix PR） |
| 🟠 中 | #6869 | 生成的 DOCX 文件被 Word 判定为损坏不可读 | OPEN（无 fix PR） |
| 🟡 低 | PR #7470 | `thread_index` 行缺少有序投影元数据时，线程在 `list_threads` 中不可见 | 待合并 |
| 🟡 低 | PR #7436 | 原生记忆搜索结果片段未限制大小 | 待合并 |

**无 fix PR 的待修复 Bug：**
- **#6257（PDF MIME 错误）** — 自 7/19 报告至今已有 3 周，无对应修复 PR。[链接](https://github.com/nearai/ironclaw/issues/6257)
- **#6869（DOCX 损坏）** — 自 7/29 报告已有近 2 周，用户对比 ChatGPT/Claude 可轻松完成此操作。[链接](https://github.com/nearai/ironclaw/issues/6869)

---

## 6. 功能请求与路线图信号

### 今日新增 Epic 级功能请求

| Epic | 描述 | 目标版本 |
|------|------|----------|
| [#7467](https://github.com/nearai/ironclaw/issues/7467) | Reborn 持久化状态 profile 无关化 + 旧 profile 根目录迁移 | — |
| [#7465](https://github.com/nearai/ironclaw/issues/7465) | Company Brain FDE（前端开发者体验） | — |
| [#7447](https://github.com/nearai/ironclaw/issues/7447) | Agent 调用工具过多后任务失败 | v1.3.0 |
| [#7354](https://github.com/nearai/ironclaw/issues/7354) | Extensions vNext：Web Push、富消息、Telegram 用户会话、Signal 渠道 | v1.3.0 |
| [#7038](https://github.com/nearai/ironclaw/issues/7038) | Storybook + AI 优先设计系统 | v1.3.0 |
| [#7046](https://github.com/nearai/ironclaw/issues/7046) | 从 AI 聊天中配置所有工具/渠道/扩展（Admin） | — |
| [#7044](https://github.com/nearai/ironclaw/issues/7044) | Channel-first 方式的新用户引导 | v1.4.0 |

### 下一版本信号

- **v1.3.0** 堆叠明显：#7038（设计系统）、#7354（Extensions vNext）、#7447（Agent 工具限制）均有明确 Epic 标签。
- **#7046**（AI 聊天配置管理）是一个值得关注的人机交互方向转变，与 "[#7044](https://github.com/nearai/ironclaw/issues/7044) Channel-first 引导" 构成组合拳。
- 今日新开的 PR #7471（租约恢复）、#7456（profile 无关存储）、#7468/#7469（logprobs 捕获/缩减）都在基础设施层面为下一阶段铺路。

---

## 7. 用户反馈摘要

### 正面反馈
- **Telegram 完整性达成** — #6733 的关闭意味着 channel 扩展通过 manifest 声明命令的机制已在三个渠道上验证一致，这是用户等待已久的跨渠道一致性。
- **Channel 修复快速落地** — #7445 的修复（共享频道仅在 @提及 时触发）直接解决了一个真实场景中的重复消息骚扰问题，且作者进行了实测验证。
- **自定义 MCP 支持关闭** — #6727 的关闭意味着用户可以连接自建的 MCP 服务器，此前仅有两个编译期内置服务器可供选择。

### 负面反馈 / 痛点
- **#6869 DOCX 损坏：** 用户（Davin Basi）反馈 "ChatGPT 和 Claude 可以轻松做到这一点"，而 IronClaw 两次尝试均失败（第一次协议违规中止、第二次生成文件损坏）。该反馈来自 7/29，至今未修复，**属于生产力工具的常见使用场景，优先级应提升**。
- **#6257 PDF MIME 错误：** 用户（Michael Kelly）在 Slack 渠道反馈生成 PDF 时报错，也持续 3 周未有修复。
- **#5882 Slack 认证损坏：** 用户反馈只能通过重装扩展恢复，这一体验损失相当严重（该问题已修复关闭）。

---

## 8. 待处理积压

### 长期未响应的活跃 Issue

| Issue | 标题 | 创建日期 | 天数 | 最后更新 | 备注 |
|-------|------|----------|------|----------|------|
| [#3762](https://github.com/nearai/ironclaw/issues/3762) | 在 WebUI 编辑 AGENTS.md 不更新系统提示词 | 2026-05-18 | ~85 天 | 2026-08-10 有评论 | P1 客户反馈，目标 v1.3.0 |
| [#6257](https://github.com/nearai/ironclaw/issues/6257) | PDF 附件 MIME 类型错误 | 2026-07-19 | ~23 天 | 8/10 有评论 | 无 fix PR |
| [#6869](https://github.com/nearai/ironclaw/issues/6869) | DOCX 生成文件损坏 | 2026-07-29 | ~13 天 | 8/10 更新 | 无 fix PR |
| [#7137](https://github.com/nearai/ironclaw/issues/7137) | live-canary CI 产物体积过大 | 2026-08-04 | ~7 天 | 8/10 更新（12 评论） | 已有 PR #7466 |

### 需要维护者关注的信号

1. **#3762 是唯一存活超过一个月的 P1 客户问题** — 用户期望"编辑 AGENTS.md 立即反映到系统提示词"，这直接影响"AI 行为可调"的核心体验。建议在 v1.3.0 排查中优先安排。

2. **#6257 与 #6869 是生产力场景的成对 bug** — 文件生成/发送是聊天产品的基础能力，且用户反馈中明确对比了竞品（ChatGPT/Claude）的表现。这两个问题的持续存在可能损害产品口碑。

3. **依赖升级 PR 积压** — [#7437](https://github.com/nearai/ironclaw/pull/7437)（16 个依赖一起升级）、[#7020](https://github.com/nearai/ironclaw/pull/7020)（tokio-tungstenite 0.29→0.30）和 #7020 均处于待合并状态。其中 tokio-tungstenite 升级自 8/2 起已等待 9 天，建议关注是否有阻塞原因。

---

*本日报由 AI 助手基于 IronClaw GitHub 仓库公开数据自动生成，时间为 2026-08-11。所有链接指向 GitHub 上的原始 Issue/PR。*

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

# LobsterAI 项目动态日报 — 2026-08-11

## 今日速览

过去 24 小时 LobsterAI 项目活跃度较高，共处理 33 条 PR（其中 20 条已合并/关闭，13 条待合并），项目正经历一个功能迭代密集期，主要集中于 cowork 协作模式的 UI 优化（活动分组折叠、附件卡片渲染、快捷键增强）以及 OpenClaw 网关稳定性的修复（轮询误杀、延迟错误吞没、provider 前缀保留）。Issues 侧仅有 1 条 stale 旧 Issue 被关闭，无新问题上报，社区反馈渠道趋于平稳。依赖更新（Vite、React、Mermaid 等）仍在持续批量推进，版本升级跨度较大，需关注兼容性验证。

## 项目进展

今日合并的 PR 集中展现了两个明确方向：**cowork 协作体验打磨** 与 **OpenClaw 网关可靠性加固**。

**Cowork 协作模式 UI 连续优化（4 个 PR 密集合并）**：`#2472` 新增活动分组折叠功能，`#2471` 将提交的非图片附件从原始文本路径渲染为可点击的文件卡片（图标 + 名称 + 类型），`#2469` 增加折叠 agent 任务快捷键并允许在输入时使用修饰键组合，`#2468` 统一流式加载指示器。这一组 PR 表明项目正在系统性完善多代理协作场景下的交互细节，2026.4.1 版本中"输入文件: /path"纯文本回显的问题得到直接修复。

**OpenClaw 稳定性修复（3 个 PR）**：`#2454` 修复工具循环保护误杀合法轮询请求的问题；`#2470` 修复了 deferred final 挂起时吞没真实 provider/LLM 运行时错误（如 idle timeout failover）的问题；`#2467` 修复 Windows 运行时升级后 pip shim 残留导致环境损坏的问题，通过共享模块统一收敛 shim 模板。

**其余合并项**：`#2466` 修复 renderer 初始化 IPC 卡死重试问题，`#1766`、`#1764`、`#1763` 为依赖升级（Vite 5→8、ReactDOM 18→19、@vitejs/plugin-react 4→6）。

综合来看，项目在 24 小时内完成了约 20 个 PR 的合入，覆盖交互优化、可靠性修复和基础依赖升级三条主线，代码合并节奏快速，项目迭代动能充沛。

---

## 社区热点

今日社区讨论热度整体温和，唯一有实质讨论的 Issue 为 `#1243`（qwen-portal-auth 插件配置循环写入导致网关频繁重启），虽被标记为 stale 并已关闭，但拥有 2 条评论。该 Issue 于 4 月初创建，8 月 10 日因过旧而关闭，未得到实质解决。用户报告网关每 5-20 分钟自动重启一次，伴随"AI 引擎正在启动网关..."弹窗，且明确指出此问题在配置非 Qwen 模型时同样出现。

此 Issue 被 stale 关闭而不有 fix 关联，可能意味着问题已在后续版本中通过其他修复（如 `#2454`、`#2470` 等网关稳定性修复）得到隐式解决，但缺少明确的回归验证说明。社区侧无高赞讨论，用户整体反馈以问题报告为主，情绪中性偏务实。

---

## Bug 与稳定性

**高严重度 — 网关频繁重启（已确认，待验证）**：Issue `#1243` 报告 qwen-portal-auth 插件配置持续自动变更导致 OpenClaw 网关高频重启（5-20 分钟/次），影响所有模型配置，非 Qwen 模型同样触发。此 Issue 已被 stale 关闭，无直接关联 fix PR，但今日合并的多个网关稳定性修复（`#2454`、`#2470`）理论上可缓解此类问题，建议维护者确认是否有回归测试覆盖此场景。

**中严重度 — OpenClaw 工具循环保护误杀合法轮询（已修复）**：PR `#2454` 修复此问题，涉及合法轮询请求被 tool-loop guard 错误终止的场景，已合并。

**中严重度 — 延迟 chat 错误吞没真实运行时故障（已修复）**：PR `#2470` 修复 deferred final 挂起时 provider/LLM 运行时错误（如 idle timeout failover）被吞没的问题，已合并。

**中严重度 — Windows 运行时升级 pip shim 损坏（已修复）**：PR `#2467` 修复健康检查仅验证文件存在性而忽略 pip shim 损坏的问题，已合并。

**低严重度 — Renderer IPC 初始化卡死（已修复）**：PR `#2466` 修复重试机制，已合并。

**低严重度 — 会话存储 provider 前缀丢失（待合并）**：PR `#2452`（待合并）修复含 `/` 的模型 ID（如 `deepseek-ai/DeepSeek-V4-Flash`）在持久化时丢失 OpenClaw provider 前缀（如 `custom_0`）的问题，导致 renderer 对会话解释错误。

---

## 功能请求与路线图信号

当前无新的显式功能请求 Issue 提交。但合并的 PR 揭示了一条清晰的路线图信号：**cowork 模式正从基础可用走向体验精细化**——非图片附件的卡片化渲染（`#2471`）、活动历史的分组折叠与快捷键操作（`#2472`、`#2469`）、流式加载态的统一（`#2468`），这些均指向产品化打磨阶段。结合 `#2452`（provider 前缀保留修复）来看，项目正在增强对自定义/第三方模型（如 DeepSeek-V4-Flash 通过 OpenClaw 接入）的会话可靠性，多供应商场景是重要演进方向。

---

## 用户反馈摘要

来自 Issue `#1243` 的有限但明确的信息显示：用户对 "AI 引擎正在启动网关..." 的频繁弹窗感到明显困扰，将其描述为"严重影响使用体验"。此问题在 Windows 10/11 平台、LobsterAI 2026.4.1 版本上复现。用户的操作路径清晰（安装 → 配置模型 → 正常使用 → 网关自动重启），体现出社区用户在实际工作流中会持续依赖网关稳定性，频繁重启会造成生产力中断。由于该 Issue 已 stale 关闭且无维护者回复记录，建议通过后续版本发布说明或回归测试声明向用户提供明确回应，避免用户因 unaddressed 问题产生流失。

---

## 待处理积压

**Open PR 队列中的依赖升级（需关注兼容性）**：13 个待合并 PR 中绝大多数为 dependabot 批量依赖更新，其中值得注意的包括 `#2465`（Vite 5.4.21 → 8.2.1）、`#2464`（ReactDOM 18.3.1 → 19.2.8）、`#2462`（Mermaid 10.9.8 → 11.16.1）、`#1277`（Electron 40.2.1 → 43.3.0）。此外，`#1766` 与 `#1764`（Vite 8.0.13、ReactDOM 19.2.6）已分别在同一领域先行合并，说明版本升级工作正在推进中。建议维护者评估 Electron 跨三大版本升级的破坏性影响，并优先合并 `#2452`（provider 前缀修复）以减少等待时间。

**长期未响应的依赖 PR**：`#1763`（@vitejs/plugin-react 4.7.0 → 6.0.1，4 月创建）与 `#1766`（Vite 5.4.21 → 8.0.13，4 月创建）在今日方被关闭，距创建已近 4 个月。`#1277`（Electron 组升级，4 月 2 日创建，至今待合并）为现存最久的打开 PR，需要维护者决策其去留。

---

*数据来源：LobsterAI GitHub 仓库（netease-youdao/LobsterAI），统计窗口为 2026-08-10 至 2026-08-11。*

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

# Moltis 项目动态日报 — 2026-08-11

## 1. 今日速览

过去24小时内，Moltis 项目保持了温和的活跃度：新增/更新 **3 个 Issue** 和 **1 个 PR**，无新版本发布。值得注意的是，本轮 Issue 有 **3 个均为 Bug 报告**，其中 2 个集中在 **apple-container 后端**（#1185、#1188），另有 1 个与沙箱构建依赖 URL 失效相关（#1189），表明用户正在多个场景下对沙箱/容器后端进行真实负载测试，稳定性问题开始浮出水面。PR #531（交互式浏览器 UI）虽创建于 4 月，但仍在持续更新，说明大型功能开发在稳步推进。综合来看，项目核心功能迭代与 bug 发现并行，处于活跃开发期。

---

## 2. 版本发布

**无新增版本发布。**

---

## 3. 项目进展

**未合并/关闭任何 PR，今日无功能落地。**

不过，长期开放的 [PR #531 — feat(browser): interactive browser viewing UI with CDP screencast](https://github.com/moltis-org/moltis/pull/531) 仍处于活跃状态，近期更新时间为 8 月 10 日。该 PR 为 Settings > Browser 页面添加完整的浏览器查看和交互 UI，支持：实时 CDP screencast 查看、鼠标/键盘/滚动交互、会话历史与操作日志回放、按 agent 隔离的浏览器配置文件（cookie 隔离）。此功能一旦合并，将显著提升 Moltis 在 GUI 自动化场景下的可观测性与调试效率，建议维护者评估其合入时机。

---

## 4. 社区热点

**最活跃 Issue：[#1185 — [Bug]: Apple Container 1.x sandbox starts but Moltis treats it as not running](https://github.com/moltis-org/moltis/issues/1185)**（3 条评论，持续更新至 8/10）

该问题描述了一个**状态检测不一致**的场景：Apple Container 1.x 沙箱实际已启动，但 Moltis 误判为未运行。评论区的讨论（3 条评论在同类问题中已属较活跃）表明这很可能不是个别环境问题，而是**容器生命周期状态同步的逻辑缺陷**，涉及沙箱状态检测机制的可靠性，值得优先排查。

---

## 5. Bug 与稳定性

| 严重程度 | Issue | 描述 | Fix PR | 状态 |
|:---:|---|---|:---:|---|
| **高** | [#1188](https://github.com/moltis-org/moltis/issues/1188) | apple-container 后端**未应用资源限制**（CPU/内存约束无效） | 无 | 待确认 |
| **中** | [#1185](https://github.com/moltis-org/moltis/issues/1185) | Apple Container 1.x 沙箱已启动但 Moltis 状态误报 | 无 | 讨论中 |
| **中** | [#1189](https://github.com/moltis-org/moltis/issues/1189) | 沙箱构建失败：gogcli GitHub URL 错误 | 无 | 等待修复 |

**分析**：#1188 影响面较大——资源限制失效可能导致容器失控占用宿主机资源，涉及生产环境稳定性；#1189 为外部依赖 URL 失效，修复成本低，需要快速跟上；#1185 涉及状态同步逻辑，建议重点关注并回归测试。

---

## 6. 功能请求与路线图信号

本周无新功能请求，但 [PR #531](https://github.com/moltis-org/moltis/pull/531) 所代表的**交互式浏览器 UI**（CDP screencast、会话回放、按 agent 隔离的浏览器配置）是当前最具分量的路线图信号。结合 2026 年 AI Agent 领域对**可观测性/可调试性**的持续需求，该功能极有可能被纳入下一版本。

---

## 7. 用户反馈摘要

基于本周 Issue 内容与评论，可提炼以下用户声音：

- **沙箱状态检测不可靠**（#1185）：用户已确认"沙箱实际运行正常"，但平台状态与真实状态脱节，直接影响自动化任务判断与用户信任。
- **多后端一致性存疑**（#1188、#1185 均指向 apple-container）：资源限制与容器命中的问题都出在同一后端，暗示该后端的**实现成熟度相对偏弱**，用户体验一致性有待提升。
- **构建链对第三方依赖敏感**（#1189）：外部 URL 失效即阻断沙箱构建，说明构建过程的容错与基础设施抽象还不够健壮。

---

## 8. 待处理积压

以下为长时间未获回应的重点 Issue/PR，提醒维护者关注：

- **[PR #531](https://github.com/moltis-org/moltis/pull/531)（创建于 3/31，距今 4+ 个月）**：交互式浏览器 UI 长期悬而未决。建议明确合入计划或给出阶段性反馈，避免社区 PR 长期搁置。

> 注：当前数据未涵盖更早期未更新 Issue 的积压情况；本次仅就可见数据进行提示。

---

*报告生成时间：2026-08-11 | 数据来源：[Moltis GitHub Repository](https://github.com/moltis-org/moltis)*

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

# CoPaw 项目动态日报 — 2026-08-11

> 数据来源: github.com/agentscope-ai/CoPaw · 统计周期: 过去24小时


## 1. 今日速览

过去24小时项目整体活跃度**高**。共产生 40 条 Issue 更新（新开/活跃 34，关闭 6）与 50 条 PR 更新（待合并 30，合并/关闭 20），无新版本发布。社区围绕 **2.0.1/2.1.0b2 的稳定性问题**（Docker 插件市场不可用、MCP 工具调用失败、Google/Gemini 兼容性、前端 UI 卡顿与内存占用）展开了密集反馈，同时 **ReMe 记忆系统** 成为功能讨论的焦点（Auto-Dream 容错、reranker 支持、ReMe4 路线图追问）。维护团队响应迅速：今日有 5 个直接针对社区反馈的修复 PR 进入管线（#6884 Auto-Dream 容错、#6845 助手回复时间戳、#6869 task_timeout、#6809 Chat Completions 内容清洗、#6877 窗口几何记忆），并有 #6875 正在准备 v2.1.0 正式版发布说明，**v2.1.0 发布已进入倒计时**。值得注意的风险信号是 **Windows 平台安装/更新器存在文件锁定缺陷**（#6810）及多起 macOS 崩溃报告（#6814 SQLite SIGBUS），建议优先处理。


## 2. 版本发布

**无新版本发布。** 但 [#6875](https://github.com/agentscope-ai/QwenPaw/pull/6875) 已提交 v2.1.0 发布说明（中英双语），涵盖用户可见特性、升级注意事项与安全说明，并在各 README 同步新闻条目。结合 2.1.0b2 已修复的多个问题，v2.1.0 正式版预计近期发布。


## 3. 项目进展

今日合并/关闭的 PR 对项目健康度有实质提升，重点如下：

**已合并/关闭（20 条）**

| PR | 内容 | 影响 |
|---|---|---|
| [#6809](https://github.com/agentscope-ai/QwenPaw/pull/6809) | 修复严格 OpenAI 兼容提供商（如 StepFun）拒绝 Chat Completions 请求的问题，清除内部运行时字段 | 直接对应 Issue #6803（6 评论），修复多轮对话 400 错误 |
| [#6878](https://github.com/agentscope-ai/QwenPaw/pull/6878) | Console 项目目录选择器增加隐藏文件夹切换 | 小但实用的可用性提升 |
| [#6615](https://github.com/agentscope-ai/QwenPaw/pull/6615) | 处理损坏的 agent.json 配置与无效 JSON | 增强配置读写的健壮性 |
| [#6398](https://github.com/agentscope-ai/QwenPaw/pull/6398) | 为 ReMe 记忆检索添加 reranker 支持（后端） | 记忆检索质量显著提升，与 #6840 的 ReMe4 路线图呼应 |

**待合并管线中的主要贡献（30 条待处理）**

- **#6870** Creator 插件聚合 PR：设置中心、Agent 技能、mm-plugins compose 编排、异步媒体生成、跨平台加固
- **#6884** Auto-Dream 集成容错（直接修复 #6841）
- **#6845** 保持助手消息的真实完成时间（直接修复 #6826）
- **#6869** 接受字符串形式 task_timeout 并给后台任务加默认超时
- **#6772** ReMe Light 增加 Embedding 热更新与 Daily Paper 能力
- **#6877** Tauri 桌面窗口位置与尺寸持久化（对应 #4634，已积压近 3 个月）

**项目整体向前推进：** v2.1.0 发布在即、ReMe 记忆系统持续进化（reranker + embedding 热更新 + Auto-Dream 容错三线并进）、跨平台兼容性（Windows/macOS）进入系统性修补阶段。


## 4. 社区热点

| 排名 | Issue | 评论数 | 核心诉求 |
|---|---|---|---|
| 1 | [#6782](https://github.com/agentscope-ai/QwenPaw/issues/6782) Docker 2.0.1 插件/应用市场始终"维护中" | 9 | **Docker 部署用户被阻塞**：无法安装任何插件或应用，核心功能不可用，急需修复或临时绕过方案 |
| 2 | [#6803](https://github.com/agentscope-ai/QwenPaw/issues/6803) OpenAI 兼容请求携带 Responses-API 内部字段被严格提供商拒绝 | 6 | **互操作性痛点**：自托管 VPS + Telegram 通道用户调用 StepFun 失败，恰好昨日 #6809 已修复并关闭 |
| 3 | [#6811](https://github.com/agentscope-ai/QwenPaw/issues/6811) OpenAI Responses 续写摘要忽略 `disable_thinking`，60 秒取消误报为 malformed output | 5 | **thinking-mode 模型多轮对话稳定性**：Scroll 压缩时主对话被阻塞 |
| 4 | [#6826](https://github.com/agentscope-ai/QwenPaw/issues/6826) 助手消息结束时间显示异常 | 5 | **前端时间戳可信度**：实际思考 2 分钟却显示几秒，用户对计时准确性存疑（已有 #6845 修复 PR） |
| 5 | [#4237](https://github.com/agentscope-ai/QwenPaw/issues/4237) 聊天内观察运行中的 shell 命令（查看/终止/延长超时） | 4 | **长任务控制权**：需要运行中命令的可视化面板，已有 approval-card 管线可复用 |

**趋势分析：** 社区热点集中在 **(a) 第三方模型/提供商兼容性**（StepFun、Gemini、DeepSeek thinking-mode）；**(b) Docker 与 Windows 部署体验**；**(c) 对话过程的可观测性与控制权**。前两点是 2.x 快速迭代期的典型"兼容性税"，第三点是用户对 Agent 自主执行信任度的真实诉求。


## 5. Bug 与稳定性

按严重程度排列：

### 🔴 严重（阻塞核心功能）

| Issue | 描述 | 状态 |
|---|---|---|
| [#6782](https://github.com/agentscope-ai/QwenPaw/issues/6782) | Docker 2.0.1 插件/应用市场始终提示"维护中"，完全不可用（9 评论，社区热点 #1） | 待处理，**无 fix PR** |
| [#6803](https://github.com/agentscope-ai/QwenPaw/issues/6803) | OpenAI 兼容请求携带 Responses-API 内部字段和原始流式字段，被 StepFun 等严格提供商以 400 拒绝 | ✅ 已在 #6809 修复并关闭 |
| [#6811](https://github.com/agentscope-ai/QwenPaw/issues/6811) | OpenAI Responses 续写摘要忽略 `disable_thinking`，且 60 秒取消误报为 malformed output，主对话被阻塞 | 待处理 |
| [#6821](https://github.com/agentscope-ai/QwenPaw/issues/6821) | thinking-mode 模型（DeepSeek V4）多轮对话必须回传 `reasoning_content`，否则 400 错误 | 待处理 |
| [#6812](https://github.com/agentscope-ai/QwenPaw/issues/6812) | Google Gemini API 拒绝包含 `$schema` 字段的工具 schema（已关闭） | ✅ 已修复关闭 |
| [#6867](https://github.com/agentscope-ai/QwenPaw/issues/6867) | Gemini 压缩错误：Function call 缺少 `thought_signature`，400 Bad Request | 待处理 |

### 🟠 中等（功能受限/体验受损）

| Issue | 描述 | 状态 |
|---|---|---|
| [#6814](https://github.com/agentscope-ai/QwenPaw/issues/6814) | macOS 打开 Scroll history.db（WAL 模式）时 SQLite SIGBUS 崩溃（`sqlite3WalFindFrame`） | 待处理 |
| [#6780](https://github.com/agentscope-ai/QwenPaw/issues/6780) | 2.0.1 空闲几十分钟后自行卡死，只能杀进程重启 | 待处理 |
| [#6847](https://github.com/agentscope-ai/QwenPaw/issues/6847) | 杀软拦截/强制关停 QwenPaw 进程（同任务 WorkBuddy 正常） | 待处理 |
| [#6405](https://github.com/agentscope-ai/QwenPaw/issues/6405) | 升级 2.0 后 MCP 工具总是提示 "Tool not found"（4 评论） | 待处理 |
| [#6839](https://github.com/agentscope-ai/QwenPaw/issues/6839) | MCP 工具调用时数字样字符串被强制转成数字格式，导致参数校验失败 | 待处理 |
| [#6813](https://github.com/agentscope-ai/QwenPaw/issues/6813) | `consume_model_response` 在 agentscope 2.x ChatResponse（dict 子类）上触发 `KeyError: '__aiter__'`，导致聊天自动标题生成失效 | 待处理 |
| [#6810](https://github.com/agentscope-ai/QwenPaw/issues/6810) | Windows 安装/更新在覆盖文件前未终止占用进程（浏览器扩展 NM host 锁文件），NSIS 报错 | 待处理 |

### 🟡 轻度（前端/体验）

| Issue | 描述 | 状态 |
|---|---|---|
| [#6820](https://github.com/agentscope-ai/QwenPaw/issues/6820) | 前端 UI 流式输出失效：模型输出/工具调用/思考过程全部完成后才一次性显示 | 待处理 |
| [#6828](https://github.com/agentscope-ai/QwenPaw/issues/6828) | Console 空闲时持续重绘（~20% CPU），源于无限 CSS 动画（ai-copilot-blink + antd load-more spinner） | 待处理 |
| [#6831](https://github.com/agentscope-ai/QwenPaw/issues/6831) | macOS 本地 Whisper 显示 "ffmpeg: disabled"（后端 PATH 排除 /opt/homebrew/bin） | 待处理 |
| [#6826](https://github.com/agentscope-ai/QwenPaw/issues/6826) | 助手消息结束时间显示异常（实际 2 分钟显示几秒） | ✅ [#6845](https://github.com/agentscope-ai/QwenPaw/pull/6845) 已在修复管线 |

**Bug 修复闭环率：** 今日关闭的 6 个 Issue 中 3 个为 Bug（#6803、#6812、以及 #6811?），其中 #6803 与 #6812 均为第三方提供商兼容性问题，说明团队在兼容性修复上响应迅速。但 **#6782（Docker 市场不可用）为社区最高热度且无 fix PR**，需优先关注。


## 6. 功能请求与路线图信号

| 功能请求 | 对应 Issue | 已有 PR 或路线图信号？ |
|---|---|---|
| **可配置 MCP 工具调用超时**（客户端配置 + 调用级保护） | [#6724](https://github.com/agentscope-ai/QwenPaw/issues/6724) | 无直接 PR，但 #6869 为后台任务添加了默认超时，方向一致 |
| **聊天内运行命令面板**（查看/终止/延长超时） | [#4237](https://github.com/agentscope-ai/QwenPaw/issues/4237) | 无，已开放 3 个月，社区持续关注 |
| **自动记忆后自动刷新会话标题** | [#6881](https://github.com/agentscope-ai/QwenPaw/issues/6881) | 无，但 #6813 的标题生成 bug 修复后此需求更可行 |
| **Auto-Dream 空 schema 容错 + 重试** | [#6841](https://github.com/agentscope-ai/QwenPaw/issues/6841) | ✅ [#6884](https://github.com/agentscope-ai/QwenPaw/pull/6884) 今日提交 |
| **完整 ReMe4 路线图**（Auto-Link、三模态检索、四类摘要权重） | [#6840](https://github.com/agentscope-ai/QwenPaw/issues/6840) | #6398 reranker 已合并、#6772 embedding 热更新推进中，**ReMe4 正在分阶段落地** |
| **后台任务面板默认折叠/收纳** | [#6876](https://github.com/agentscope-ai/QwenPaw/issues/6876) | 已关闭，需查看合并方式（可能已修复） |
| **窗口大小和位置记忆** | [#4634](https://github.com/agentscope-ai/QwenPaw/issues/4634) | ✅ [#6877](https://github.com/agentscope-ai/QwenPaw/pull/6877) 今日提交，积压近 3 个月的需求终于落地 |
| **接收字符数动态显示可关闭** | [#6585](https://github.com/agentscope-ai/QwenPaw/issues/6585) | 无 |
| **MCP 工具字符串参数保持为字符串** | [#6839](https://github.com/agentscope-ai/QwenPaw/issues/6839) | 无直接 PR，但属类型处理问题，可能随 MCP 重构修复 |

**路线图判断：** 社区反馈的功能请求正在被快速吸收进开发管线。**#6840（ReMe4 路线图）值得官方回应**——2.1.0b2 已搭载 ReMe 0.4.1.4，用户对完整路线图的时间表有明确期待。


## 7. 用户反馈摘要

- **Docker 用户被卡在门外**：#6782 用户反馈 2.0.1 Docker 版插件和应用市场完全不可用（9 条评论，无维护者回应迹象），这直接影响 Docker 部署用户的扩展能力，是当前**最迫切的用户痛点**。
- **第三方模型接入是双刃剑**：多位用户（StepFun、Gemini、DeepSeek）报告兼容性问题，说明 2.x 的多提供商支持在覆盖面上仍有缝隙。正面信号是团队修复速度较快（#6803 和 #6812 均已在当日关闭）。
- **Windows 用户环境依赖敏感**：用户反馈杀软强制关停进程（#6847）、安装器文件锁定报错（#6810），说明 Windows 打包与运行时行为需要更多打磨。
- **计时准确性影响信任**：前端显示助手几秒完成但实际上思考了 2 分钟（#6826），用户明确表达了对计时准确性的不信任。这是**感知层信任问题**，好在已有 PR #6845 处理。
- **前端流式输出退回"全有或全无"**：有用户反馈工具调用、思考过程不再逐字流出，而是全部完成才一次性渲染（#6820），回退到旧有交互模式，体验倒退感明显。
- **MCP 生态存在"最后一公里"问题**：工具名变更（`[mcp-key]__[tool_name]`）、Tool not found（#6405）、数字字符串被强转（#6839）等多个问题交织，说明 MCP 集成层需要一次系统性的稳健性提升。
- **ReMe 记忆系统获得早期采用者关注**：#6840 用户主动对比代码与 ReMe4 设计文档，询问路线图时间表；#6841 用户报告 Auto-Dream 单单元失败拖垮整个任务，但**表扬了日志可观测性**（"从日志看实际结果大部分成功"）。这是深度用户的声音。


## 8. 待处理积压

### 🚨 高优先级（阻塞核心功能 + 社区高热度）

| 项目 | 积压时长 | 备注 |
|---|---|---|
| [#6782](https://github.com/agentscope-ai/QwenPaw/issues/6782) Docker 插件/应用市场"维护中" | 4 天 | 9 条评论，活跃用户持续影响，无 fix PR |
| [#6405](https://github.com/agentscope-ai/QwenPaw/issues/6405) MCP 工具 "Tool not found" | 19 天 | 涉及 2.0 升级用户，多版本仍未解决 |

### 🟡 中优先级（影响面大但无活跃讨论）

| 项目 | 积压时长 | 备注 |
|---|---|---|
| [#4237](https://github.com/agentscope-ai/QwenPaw/issues/4237) 聊天内运行命令面板 | 91 天 | 已积压约 3 个月，4 条评论。能力已在 Roadmap 中，但排期未知 |
| [#4634](https://github.com/agentscope-ai/QwenPaw/issues/4634) 窗口大小/位置记忆 | 81 天 | 今日 #6877 已提交 PR，预计近期关闭 |
| [#6585](https://github.com/agentscope-ai/QwenPaw/issues/6585) 接收字符数动态显示开关 | 11 天 | 小功能但触及 UI 细节体验 |
| [#6724](https://github.com/agentscope-ai/QwenPaw/issues/6724) MCP 工具调用可配置超时 | 6 天 | 功能请求，与 #6869 有相关但未直接解决 |

### ⚠️ 需要维护者回应

- [#6840](https://github.com/agentscope-ai/QwenPaw/issues/6840) ReMe4 路线图时间表 —— 深度用户在等待官方规划说明。
- [#6814](https://github.com/agentscope-ai/QwenPaw/issues/6814) macOS SQLite WAL 崩溃 —— 涉及数据持久化安全性，建议优先排查。
- [#6847](https://github.com/agentscope-ai/QwenPaw/issues/6847) 杀软拦截报告 —— 附有详细截图，可能需要调整代码签名策略或行为模式。


**总结：** CoPaw 项目在 2026-08-11 展现出健康的迭代节奏——第三方兼容性问题快速闭环、ReMe 记忆系统三线推进、v2.1.0 发布在即。主要风险集中在 Docker 部署可用性、MCP 集成稳健性、以及 Windows/macOS 桌面端的平台适配三方面。建议维护团队优先处理 #6782（Docker 市场不可用），并在 v2.1.0 发布说明中对 ReMe4 路线图给出公开承诺。

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# ZeroClaw 项目动态日报 — 2026-08-11

## 1. 今日速览

ZeroClaw 在过去 24 小时保持稳定的活跃度：50 条 Issues 和 50 条 PR 均有更新，全部处于开放状态（新开或活跃讨论中），无新版本发布，合入/关闭数为 0。项目当前处于密集的 RFC 决策与安全审计修复期：多条高优先级安全类 Issues（S0/S1 级）长期在审但尚无对应修复 PR 合入，同时维护者正在通过 RFC 流程（#6808、#7100、#9496）系统性优化贡献者流程与配置能力。总体上，项目讨论热度高、安全关注度强，但**合并吞吐量偏低**，需关注积压风险。

---

## 3. 项目进展

过去 24 小时**无 PR 被合并或关闭**（合并/关闭: 0），50 条开放 PR 均处于待审或等待作者响应状态。值得关注的是，本周有多条高质量 PR 已进入**需要作者操作（needs-author-action）**阶段，说明维护者已给出反馈，等待提交方更新：

- **#8486** feat(gateway): 新增 OpenAI Chat Completions 端点，这将显著提升 ZeroClaw 与 LangChain、Continue.dev、Aider 等生态的互操作性（[PR #8486](https://github.com/zeroclaw-labs/zeroclaw/pull/8486)）
- **#8561** feat(channels/telegram): 添加 multi_message 流式模式，对齐 Discord/Matrix 的 paced delivery 能力（[PR #8561](https://github.com/zeroclaw-labs/zeroclaw/pull/8561)）
- **#9222** feat(eval): 新增 per-dimension LLM-judge 评估器，当前定位为诊断模式、不阻塞 CI（[PR #9222](https://github.com/zeroclaw-labs/zeroclaw/pull/9222)）
- **#9126** feat(plugins): 对 wasm 插件实例配置引入强类型 JSON Schema 校验（[PR #9126](https://github.com/zeroclaw-labs/zeroclaw/pull/9126)）
- **#9897** fix(cli): 修正文档中误导用户发送 SIGUSR1 的错误建议（该信号默认会杀死守护进程）（[PR #9897](https://github.com/zeroclaw-labs/zeroclaw/pull/9897)）

此外，两条几乎相同的 WhatsApp Web reactions 实现 PR（#9893 与 #9894）同日提交，疑似重复提交，维护者需协调合并。

---

## 4. 社区热点

| 排名 | 标题 | 评论数 | 链接 |
|------|------|--------|------|
| 1 | RFC: Work Lanes, Board Automation, and Label Cleanup | 23 | [#6808](https://github.com/zeroclaw-labs/zeroclaw/issues/6808) |
| 2 | RFC: Per-model capability & context-window config | 13 | [#7100](https://github.com/zeroclaw-labs/zeroclaw/issues/7100) |
| 3 | Maintainer decision queue for RFCs and design issues | 12 | [#8692](https://github.com/zeroclaw-labs/zeroclaw/issues/8692) |
| 4 | RFC: Empty WhatsApp Web allowed_groups 应视为拒绝所有 | 12 | [#9397](https://github.com/zeroclaw-labs/zeroclaw/issues/9397) |
| 5 | RFC: 简化 RFC 流程（讨论/投票/指派） | 7 | [#9496](https://github.com/zeroclaw-labs/zeroclaw/issues/9496) |

**热点分析：**

三条高讨论度的 RFC 均指向同一诉求：**ZeroClaw 的治理与决策流程需要降本增效**。#6808 提出引入 Work Lanes 与板面自动化以减轻维护者手工路由负担；#9496 则直接指出当前 RFC 流程"比其要支撑的决策本身更慢、更笨重"，建议缩短七日讨论期、放宽一致同意门槛。这两条 RFC 的共同信号是：**项目规模已超过现有手工治理模式的承载力**，自动化的标签计算（#9345）与板面流转将成为下一阶段基础设施建设的重点。

#7100 则反映了用户侧的配置痛点：模型能力（vision 支持）、上下文窗口等属性分散在多个配置来源中，Provider 家族默认值经常误报。用户需要 per-alias 的显式覆盖能力——这是生产部署中真实存在的配置漂移问题。

安全类 Issue #9397（WhatsApp Web 空 allowlist 默认放行所有群组）获得 12 条评论，社区对默认安全（secure-by-default）的关注度持续走高。

---

## 5. Bug 与稳定性

今日**无新 Bug 报告**（全部 50 条 Issues 均为存量更新），但存量中仍有大量高严重度问题**长期未修复且无对应 PR**：

### S0 级（数据丢失/安全风险）

| Issues | 描述 | 状态 | 修复 PR |
|--------|------|------|---------|
| [#9647](https://github.com/zeroclaw-labs/zeroclaw/issues/9647) | 知识图谱无 per-agent 归属，任意 agent 可读写其他 agent 知识 | in-progress | 无 |
| [#9855](https://github.com/zeroclaw-labs/zeroclaw/issues/9855) | Matrix 通道未实现 `.well-known` 委派解析，自托管服务器不可用 | accepted | 无 |
| [#9627](https://github.com/zeroclaw-labs/zeroclaw/issues/9627) | git 写操作可通过 `-C`/`--git-dir` 等全局选项绕过风险分类器 | in-progress | 无 |

### S1 级（工作流阻塞/高风险）

| Issues | 描述 | 状态 | 修复 PR |
|--------|------|------|---------|
| [#9207](https://github.com/zeroclaw-labs/zeroclaw/issues/9207) | web_fetch 对 gzip/brotli 压缩响应返回乱码二进制 | in-progress | 无 |
| [#9425](https://github.com/zeroclaw-labs/zeroclaw/issues/9425) | 运行中的 SOP 任务无操作者取消入口 | in-progress | 无 |
| [#9035](https://github.com/zeroclaw-labs/zeroclaw/issues/9035) | Docker Compose 网关可保持 loopback 绑定，端口不可达 | in-progress | 无 |
| [#9779](https://github.com/zeroclaw-labs/zeroclaw/issues/9779) | `sops_dir` 文档默认值未被守护进程遵循，SOP 静默不加载 | accepted | 无 |
| [#9393](https://github.com/zeroclaw-labs/zeroclaw/issues/9393) | Bluesky 与 Reddit 通道无发送者授权 | in-progress | 无 |
| [#9395](https://github.com/zeroclaw-labs/zeroclaw/issues/9395) | WASI HTTP 出口无目标策略与配置开关 | in-progress | 无 |
| [#9392](https://github.com/zeroclaw-labs/zeroclaw/issues/9392) | LINE 群消息跳过 allowlist 与配对握手 | in-progress | 无 |
| [#9389](https://github.com/zeroclaw-labs/zeroclaw/issues/9389) | 未认证 `/api/pair` 以攻击者可控 header 为锁定位键 | in-progress | 无 |
| [#9391](https://github.com/zeroclaw-labs/zeroclaw/issues/9391) | 命令审计日志默认开启但实际不写任何内容 | in-progress | 无 |

**观察：** 多条 S0/S1 级安全 Issues（#9392、#9393、#9395、#9389、#9391）由同一审计者（belumume）于 7 月 26 日批量提交，距今已两周有余，虽有 in-progress 标记但均无对应修复 PR 出现。这可能是维护者正在统一修复中，也可能是缺乏人力跟进——建议在下一个社区会议中明确时间表。

---

## 6. 功能请求与路线图信号

### 可能进入下一版本的功能（已有实现 PR）

| 功能 | PR | 说明 |
|------|-----|------|
| OpenAI Chat Completions 端点 | [#8486](https://github.com/zeroclaw-labs/zeroclaw/pull/8486) | 对接 OpenAI SDK 生态，扩展接入方式 |
| 自定义 CA 信任（远程 MCP 服务器） | Issue [#9339](https://github.com/zeroclaw-labs/zeroclaw/issues/9339) | 私有网络部署的硬需求，暂无 PR |
| Telegram multi-message 流式模式 | [#8561](https://github.com/zeroclaw-labs/zeroclaw/pull/8561) | 对齐 Discord/Matrix 行为 |
| Hailo-Ollama 原生支持 | [#9109](https://github.com/zeroclaw-labs/zeroclaw/pull/9109) | 边缘 AI 推理硬件适配 |
| 危险命令全姿态禁止（不可逆破坏性命令） | [#9839](https://github.com/zeroclaw-labs/zeroclaw/pull/9839) | 安全加固：即使 operator 配置了 `*` 放行也拦截 `rm -rf` 类命令 |

### 路线图信号（RFC 阶段的架构方向）

- **Per-model 能力/上下文窗口显式配置**（[#7100](https://github.com/zeroclaw-labs/zeroclaw/issues/7100)）：将模型能力声明与 Provider 家族默认值解耦，预期影响 UI 显示、context budget 计算等多处
- **工作板面自动化与标签清理**（[#6808](https://github.com/zeroclaw-labs/zeroclaw/issues/6808)）：配合 #9345（PR 风险/大小标签自动重算）构建更自动化的协作基础设施
- **RFC 流程简化**（[#9496](https://github.com/zeroclaw-labs/zeroclaw/issues/9496)）：缩短讨论周期、降低一致同意门槛，反映项目对决策速度的诉求

---

## 7. 用户反馈摘要

- **SOP 静默不加载问题**（[#9779](https://github.com/zeroclaw-labs/zeroclaw/issues/9779)）：用户按文档配置 `sops_dir` 后 SOP 始终未生效，且**无任何错误/警告/日志输出**。此类静默失败严重伤害用户对配置系统的信任，建议增加配置解析校验与启动告警。
- **WebChat 流式场景下自动滚动覆盖手动滚动**（[#9562](https://github.com/zeroclaw-labs/zeroclaw/issues/9562)）：用户在 agent 回复时无法回看历史消息，评论关联了 openclaw 上游的同类问题，说明这是跨项目通病，但用户仍期望 ZeroClaw 优先修复。
- **ZeroCode 的 CPU 指标存在误导**（[#9844](https://github.com/zeroclaw-labs/zeroclaw/issues/9844)）：Dashboard 显示的 CPU 数值实际来自所连接 daemon 的 `process.cpu_percent`，而非 ZeroCode 自身进程。用户认为该指标"有误导性"，涉及基本的可观测性可信度问题。
- **OpenAI Codex 端点无流式重试导致死循环**（PR [#9900](https://github.com/zeroclaw-labs/zeroclaw/pull/9900)）：Codex 后端要求 `stream=true`，但失败重试时带了 `stream=false` 导致持续 400 错误。该 PR 为定向修复，目前待审。
- **文档中 SIGUSR1 误导**（[#9768](https://github.com/zeroclaw-labs/zeroclaw/issues/9768)、PR [#9897](https://github.com/zeroclaw-labs/zeroclaw/pull/9897)）：降级安全警告建议用户发送 SIGUSR1 重载，但该信号无 handler，实际效果是**直接杀死守护进程**。用户评价此问题为 "misleading and dangerous"。

---

## 8. 待处理积压

以下为长期开放、高影响但缺乏明确推进计划的事项：

### 高优先级安全修复缺口（审计报告待跟进）

| Issues | 等级 | 报告日期 | 已存活 | 修复 PR |
|--------|------|----------|--------|---------|
| [#9389](https://github.com/zeroclaw-labs/zeroclaw/issues/9389) 未认证配对端点 lockout 可被绕过 | S1/安全 | 07-26 | 16 天 | 无 |
| [#9391](https://github.com/zeroclaw-labs/zeroclaw/issues/9391) 审计日志默认开启但零输出 | S1/安全 | 07-26 | 16 天 | 无 |
| [#9392](https://github.com/zeroclaw-labs/zeroclaw/issues/9392) LINE 群消息绕过 allowlist | S1/安全 | 07-26 | 16 天 | 无 |
| [#9393](https://github.com/zeroclaw-labs/zeroclaw/issues/9393) Bluesky/Reddit 无发送者授权 | S1/安全 | 07-26 | 16 天 | 无 |
| [#9395](https://github.com/zeroclaw-labs/zeroclaw/issues/9395) WASI HTTP 出口无策略控制 | S1/安全 | 07-26 | 16 天 | 无 |
| [#9647](https://github.com/zeroclaw-labs/zeroclaw/issues/9647) 知识图谱跨 agent 数据互读 | S0/安全 | 08-01 | 10 天 | 无 |
| [#9627](https://github.com/zeroclaw-labs/zeroclaw/issues/9627) git 全局选项绕过风险分类器 | S0/安全 | 08-01 | 10 天 | 无 |

### 长期待合并的重要 PR（含 needs-author-action 标记）

- **#8486** OpenAI Chat Completions 端点（06-29 创建，已存活 43 天，size:XL）
- **#8561** Telegram multi-message 流式模式（06-30 创建，已存活 42 天，size:XL）
- **#8713** file_download SSRF gate（07-04 创建，已存活 38 天，size:XL，安全相关）
- **#9109** Hailo-Ollama 原生支持（07-17 创建，已存活 25 天，size:XL）
- **#9222** LLM-judge 评估器（07-20 创建，已存活 22 天，size:XL）

### 建议关注

1. **批量安全审计修复的状态更新**：belumume 提交的 7 条安全 Issues 已两周无实质进展，建议维护者在 #8692 决策队列中明确优先级与排期。
2. **重复 PR 合并协调**：#9893 与 #9894 为同一功能的两个 rebase 版本，需尽快确定合并哪一个，避免贡献者困惑。
3. **#9779（SOP 静默不加载）** 虽然刚报告 5 天，但其"文档默认值被忽略 + 零日志输出"的复合问题对用户信任影响较大，建议优先处理。

</details>

---
*本日报由 [agents-radar](https://github.com/kky-wollu/agents-radar) 自动生成。*