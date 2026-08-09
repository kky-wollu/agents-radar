# OpenClaw 生态日报 2026-08-10

> Issues: 500 | PRs: 500 | 覆盖项目: 13 个 | 生成时间: 2026-08-09 22:35 UTC

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

# OpenClaw 项目动态日报

**日期：2026-08-10** | 数据窗口：2026-08-09 00:00 – 2026-08-10 00:00 UTC


## 1. 今日速览

过去 24 小时 OpenClaw 仓库保持着极高的活跃度，共产生 500 条 Issue 更新和 500 条 PR 更新，属于近期峰值水平。核心议题集中在五个方向：（1）**消息丢失/静默失败**类 bug 反复出现且回报率高（如 #116277 关闭后复发 #121058）；（2）**安全加固**长期占据讨论主导（密钥保护、提示注入防护、沙箱化），多路 PR 处于排队状态；（3）**配对（Pairing）功能**成为当前开发主赛道，一组 5 个相互依赖的 PR（#120768/#120825/#120890/#121032/#121138）正在推进"一键配对/公网连接"体验；（4）**架构净化**持续进行，包括移除会话写租约（#121113）、频道所有者策略下沉（#121257）等大型重构；（5）**UI/UX 打磨**密集提交，涉及光标行为、对话框替换浏览器原生 prompt、模型继承语义等。新版本发布为 0 个，项目处于功能开发与稳定化的并行阶段。

- 高风险 P0/P1 问题约 60+ 个，其中 **"恢复卡死"（clawsweeper-recovery-stuck）** 标记的问题有 3 个，值得关注
- 今日**无新版本发布**，自 2026.7.2-beta.5 以来已积累大量待验证修复
- 大型重构 PR（移除会话写租约、频道策略下沉）与高价值 bug 修复 PR 同步推进，**代码库健康度良好，但合并积压值得注意**


## 2. 版本发布

今日无新版本发布。


## 3. 项目进展

今日无直接合并记录（数据未区分合并/关闭），但关闭的 PR 中有一个重要信号值得关注——**移除会话写租约的架构重构**：

| PR | 标题 | 状态 | 意义 |
|---|---|---|---|
| [#121113](https://github.com/openclaw/openclaw/pull/121113) | refactor(agents)!: remove the session write lease | **CLOSED** | 移除从 JSONL 文件锁时代继承的 SQLite 会话写租约机制。该机制已冗余——SQLite 事务本身保障数据完整性，Gateway 状态目录锁保障进程所有权。关闭此 PR 意味着该大型重构可能已被合并或进入收尾阶段，**大幅简化会话层架构** |
| [#121256](https://github.com/openclaw/openclaw/pull/121256) | fix(gateway): keep view-only desktop sessions connected | **CLOSED** | 修复 noVNC 1.7 握手后 view-only 模式被错误断开的回归，改善 Cloud Worker Desktop 体验 |
| [#120734](https://github.com/openclaw/openclaw/pull/120734) | fix(anthropic): reject leaked Claude tool protocol output | **CLOSED** | 安全修复：拒绝 Claude Code 返回的遗留 `<invoke>`/`<parameter>` 工具协议文本，防止伪造命令输出被当作正常聊天内容持久化/投递 |
| [#103103](https://github.com/openclaw/openclaw/pull/103103) | fix(models): honor replace mode in list output | **CLOSED** | 修复 `models.mode: "replace"` 时 `openclaw models list` 仍渲染已认证的目录模型与过期引用的行为 |

**整体判断**：项目在架构简化（去租约化）、安全加固（工具协议隔离）、修复回归三个方向同时推进。会话写租约的移除是一个里程碑式的简化，后续将减少一类"会话状态不一致"类 bug 的根源。


## 4. 社区热点

### 🔥 最热 Issue：#116277（196 评论）
**DeepSeek v4 Flash 静默回复失败** — [链接](https://github.com/openclaw/openclaw/issues/116277)

这是过去 24 小时讨论量最大的 Issue，标签为"diamond lobster"（最高等级关注）。核心问题：DeepSeek v4 Flash 在 Telegram 群消息中静默失败，仅发出通用兜底文案 "No reply was generated for this message"。169 条评论时长跨度从 2026-07-30 至 08-09（关闭后又重开）。

**更关键的是**：同一位用户（sloptop-the-terrible）在今日（08-09）又新开了 [#121058](https://github.com/openclaw/openclaw/issues/121058)，**明确指出 #116277 关闭后问题仍然复现**。这暗示修复方案不完整，社区对此类"静默失败"的容忍度正在下降。

### 🥈 高讨论 Issue：#25592（41 评论）
**工具调用之间的文本泄漏到消息通道** — [链接](https://github.com/openclaw/openclaw/issues/25592)

Agent 在工具调用之间产生的内部处理文本（错误处理、确认信息、叙述）被路由到 Slack/iMessage 等活跃频道作为可见消息。这是严重的 UX 问题，且涉及安全边界。评论数持续增长，说明该问题影响面广，用户对此有强烈共鸣。

### 🥉 PR 关注度：#121014（DO NOT MERGE 标记）
**Slack Enterprise Grid 延迟操作丢失工作区作用域** — [链接](https://github.com/openclaw/openclaw/pull/121014)

标记为 **[DO NOT MERGE]** 的 PR，修复 Slack Enterprise Grid 上的延迟交互（block actions、shortcuts、modal submissions）在唤醒 Agent 时可能丢失工作区作用域的问题。风险标记为 **session-state 和 message-delivery 双重高危**。该 PR 的存在值得社区关注：修复方向正确但合并需谨慎。

### 其他值得关注

- **#48003**[Steer 模式不注入消息（16 评论）](https://github.com/openclaw/openclaw/issues/48003) — 用户期待的核心交互能力
- **#92201**[Anthropic 思考签名在重放时间歇性无效（21 评论）](https://github.com/openclaw/openclaw/issues/92201) — 技术深度较高，涉及流式签名验证


## 5. Bug 与稳定性

### 🔴 P0 / 严重（数据丢失 / 安全）

| Issue | 问题 | 是否有 fix PR |
|---|---|---|
| [#94939](https://github.com/openclaw/openclaw/issues/94939) | **6.x 状态迁移导致 MS Teams 会话存储 SQLite 为空（0 字节）**，孤立引用、破坏主动发送 — diamond lobster，recovery-stuck | ⚠️ 有 linked PR 但标记 recovery-stuck |
| [#121058](https://github.com/openclaw/openclaw/issues/121058) | **#116277 关闭后静默回复失败仍在复现**（当日新开） | ❌ 无 |
| [#115546](https://github.com/openclaw/openclaw/issues/115546) | **CLI-budget 压缩超时远早于截止时间（4.9s–50s），大会话 100% 失败**，无重试 → 唤醒死亡螺旋 — diamond lobster | ❌ 无 |
| [#91009](https://github.com/openclaw/openclaw/issues/91009) | **Codex PreToolUse 钩子触发 CPU 100%+ 进程**，阻塞 Gateway RPC — platinum hermit | ❌ 无 |
| [#48920](https://github.com/openclaw/openclaw/issues/48920) | **Live Docs 超前于发布版本**（Heartbeat IsolatedSessions 文档与 2026.3.13 不匹配）— P0, diamond lobster, release-blocker | ❌ 无 |

### 🟠 P1 / 高（消息丢失 / 会话状态损坏）

| Issue | 问题 | 是否有 fix PR |
|---|---|---|
| [#44925](https://github.com/openclaw/openclaw/issues/44925) | 子代理完成结果静默丢失（无重试、无通知、超时无自动重启） | ❌ 无 |
| [#25592](https://github.com/openclaw/openclaw/issues/25592) | **工具调用间文本泄漏到消息频道** — diamond lobster | ❌ 无 |
| [#92201](https://github.com/openclaw/openclaw/issues/92201) | Anthropic 思考签名重放时无效，恢复包装器因错误文本泛化而不触发 | ❌ 无 |
| [#48003](https://github.com/openclaw/openclaw/issues/48003) | Steer 模式不向进行中的主会话注入消息 — diamond lobster, 获 4 👍 | ❌ 无 |
| [#97616](https://github.com/openclaw/openclaw/issues/97616) | 钩子/工具子进程未被回收，僵尸进程累积导致运行降级 | ❌ 无 |
| [#90378](https://github.com/openclaw/openclaw/issues/90378) | 5.28→6.1 升级后 cron 存储静默迁移至 SQLite，新任务默认 announce 模式导致频道错误 | ❌ 有 linked PR |
| [#120735](https://github.com/openclaw/openclaw/issues/120735) | Telegram 贴纸以原始文件引用到达，无描述不落盘，Agent 无法处理 | ❌ 无（当日新开，fix-shape-clear） |
| [#114211](https://github.com/openclaw/openclaw/issues/114211) | Matrix 房间 Agent 可循环于可见无回复输出、重启恢复、过期会话重放 | ❌ 无 |

### 🟡 P2 / 中（功能异常 / 体验问题）

| Issue | 问题 | 是否有 fix PR |
|---|---|---|
| [#31583](https://github.com/openclaw/openclaw/issues/31583) | `exec` 工具不继承 `skills.entries.*.env` 环境变量 — **回归**，diamond lobster | ❌ 有 linked PR |
| [#57901](https://github.com/openclaw/openclaw/issues/57901) | Safeguard 压缩忽略 `compaction.model` 配置，使用会话模型 | ❌ 无 |
| [#92415](https://github.com/openclaw/openclaw/issues/92415) | `/model` 切换后 `AgentSession.this.model` 快照不刷新，影响后续 8 处读取 | ❌ 无 |
| [#119796](https://github.com/openclaw/openclaw/issues/119796) | Windows 上 vitest 清理失败（EBUSY），agent 状态 DB 句柄未释放 — diamond lobster, recovery-stuck | ❌ 有 linked PR |
| [#105528](https://github.com/openclaw/openclaw/issues/105528) | Windows 上 exec/read 工具间歇性返回空输出 — **回归** | ❌ 无 |
| [#88079](https://github.com/openclaw/openclaw/issues/88079) | WebChat 不流式渲染 Kimi Code & DeepSeek Reasoner 的推理内容 — **回归** | ❌ 有 linked PR |

### ⚪ 值得关注的"重复模式"

> 多个 Issue 指向同一类根因：**"子代理/工具执行的中间状态丢失"**（#44925、#47975、#87327），以及 **"文本在工具调用之间被错误路由或丢失"**（#25592、#92199、#88079）。这暗示核心执行引擎的编排层存在系统性问题，而非孤立的频道适配 bug。


## 6. 功能请求与路线图信号

### 🚀 配对（Pairing）功能 — 明显的主赛道

一组相互依赖的 PR 今日集中更新，形成完整的配对功能栈：

| PR | 功能 |
|---|---|
| [#120768](https://github.com/openclaw/openclaw/pull/120768) | 一键粘贴设备配对（oc-pair setup links） |
| [#120825](https://github.com/openclaw/openclaw/pull/120825) | 非密钥连接预检（connectivity preflight） |
| [#120890](https://github.com/openclaw/openclaw/pull/120890) | Tailscale 路由就绪状态类型化 |
| [#121032](https://github.com/openclaw/openclaw/pull/121032) | Control UI 引导公网 URL 和 LAN 设置 |
| [#121138](https://github.com/openclaw/openclaw/pull/121138) | 配对向导中提供 Tailscale 选项 |

**信号**：这 5 个 PR 均由同一维护者（vyctorbrzezowski）牵头，相互有依赖关系，是近期 UI/网关方向的重点工程。`docs/plan/runners.md` 里程碑 3 明确提及"一键配对"流程。

### 📋 其他高价值功能请求（均已存在较久但未落地）

| Issue | 功能 | 时长 | 热度 |
|---|---|---|---|
| [#10659](https://github.com/openclaw/openclaw/issues/10659) | **掩码密钥系统**：Agent 可用但不可见 API 密钥 — diamond lobster | 6 个月+ | 15 评论, 4 👍 |
| [#11829](https://github.com/openclaw/openclaw/issues/11829) | **API 密钥保护安全路线图** | 6 个月+ | 21 评论 |
| [#7722](https://github.com/openclaw/openclaw/issues/7722) | **文件系统沙箱配置**（tools.fileAccess）— diamond lobster | 6 个月+ | 9 评论, 4 👍 |
| [#18677](https://github.com/openclaw/openclaw/issues/18677) | **skill:install 安全扫描钩子 API** | 6 个月+ | 18 评论 |
| [#71452](https://github.com/openclaw/openclaw/issues/71452) | 消息列表分页（替代硬编码 25 条限制） | 3.5 个月 | 6 评论 |
| [#60572](https://github.com/openclaw/openclaw/issues/60572) | **多槽位记忆架构**（Multi-Slot Memory）— diamond lobster | 4 个月+ | 6 评论, 3 👍 |

### 📡 路线图信号判断

- **安全性**是反复出现的高优先级主题（#10659、#11829、#7722、#45740），预计下一版本会包含至少 1-2 项安全加固（masked secrets 或文件沙箱）
- **Agent 自主性**类功能（#6757 自我压缩、#6625 子代理超时前预警）今年早些时候已提出，但未见对应 PR，可能不在近期规划
- **多机器人支持**（#71058 多个 Teams 机器人）和**完全动态模型发现**（#10687）属于较大的架构扩展，短期落地概率低


## 7. 用户反馈摘要

### 😠 最强烈的痛点：静默失败与消息丢失

> "No reply was generated for this message" — 用户 sloptop-the-terrible 在 #116277 关闭后立即重开新 Issue（#121058），情绪明显不满。同号用户还开了 Telegram 贴纸无法处理的问题（#120735），说明**该用户在生产环境重度使用 DeepSeek 模型 + Telegram**，对静默失败零容忍。

### 😤 次强痛点：工具调用间文本错误路由

> "内部处理输出、失败的 exec 结果、处理确认——这些都出现在聊天里" — #25592 用户 doomclaw 明确指出这是 "significant UX problem"。41 条评论说明这不是个例。

### 😐 中性/理性反馈

- **#48003**（Steer 模式不注入消息）：4 👍 说明用户期待此能力，评论以使用场景描述为主（"turn 中途需要插入纠正/新指令"）
- **#48920**（Live Docs 超前发布）：4 👍，用户 Stoff81 针对文档与版本不同步表达了困惑，属于团队协作流程问题
- **#10659**（掩码密钥）：4 👍，用户 jmkritt 提出了详细的分层方案（provider 密钥 vs. 业务 API 密钥），质量较高，值得维护者认真考虑

### 😊 正面信号

- **#121256**（view-only 桌面保持连接）的关闭意味着一个实际体验问题的解决
- **#10687**（动态模型发现）获得 3 👍，评论中用户表达了正向期待


## 8. 待处理积压

### ⚠️ 长期未响应的 P0/P1 高危问题

| Issue | 创建时间 | 时长 | 风险 |
|---|---|---|---|
| [#48920](https://github.com/openclaw/openclaw/issues/48920) **Live Docs 超前于发布** | 2026-03-17 | **近 5 个月** | P0, release-blocker |
| [#25592](https://github.com/openclaw/openclaw/issues/25592) **工具调用间文本泄漏** | 2026-02-24 | 5.5 个月 | P1, diamond lobster |
| [#116277](https://github.com/openclaw/openclaw/issues/116277) **DeepSeek v4 Flash 静默失败** | 2026-07-30 | 11 天（**已关闭但复发**） | P1, diamond lobster |
| [#91009](https://github.com/openclaw/openclaw/issues/91009) **Codex 钩子 CPU 100%** | 2026-06-06 | 2 个月 | P1, platinum hermit |
| [#94939](https://github.com/openclaw/openclaw/issues/94939) **6.x 迁移致 SQLite 空** | 2026-06-19 | 1.5 个月 | P1, diamond lobster, recovery-stuck |
| [#10659](https://github.com/openclaw/openclaw/issues/10659) **掩码密钥系统** | 2026-02-06 | 6 个月 | 安全增强, diamond lobster, 4 👍 |
| [#11829](https://github.com/openclaw/openclaw/issues/11829) **API 密钥保护路线图** | 2026-02-08 | 6 个月 | 安全增强 |
| [#6686](https://github.com/openclaw/openclaw/issues/6686) | — | — | — |

### ⚠️ 长期未合并的关键 PR

| PR | 创建时间 | 时长 | 阻塞点 |
|---|---|---|---|
| [#103537](https://github.com/openclaw/openclaw/pull/103537) **fix(update): 防止 Gateway 在包替换期间重启** | 2026-07-10 | **1 个月** | 状态 waiting on author |
| [#103103](https://github.com/openclaw/openclaw/pull/103103) **fix(models): honor replace mode** | 2026-07-09 | 1 个月 | **今日已 CLOSED** ✅ |
| [#110261](https://github.com/openclaw/openclaw/pull/110261) **test(acp): 对 Claude 施加与 Codex/Gemini 相同的 live bind 标准** | 2026-07-18 | 3 周 | 状态 ready for maintainer look |

### 🔍 特别提醒

1. **#116277 关闭后复发**（#121058 当日新开）— 建议维护者重新审视关闭标准，避免"修复不完整就关闭"带来的用户信任损失
2. **#48920（文档超前）已滞留近 5 个月**且标记 P0 release-blocker — 如果文档与版本不同步持续存在，新用户的第一体验将严重受损
3. **3 个 recovery-stuck 标记的问题**（#94939、#119796、#92199）表明有多个功能卡在恢复流程中，可能需要专门的恢复机制审查
4. **配对 PR 堆栈**（5 个相互依赖的 PR）建议维护者优先评审，该功能栈已占用了大量 PR 数量且相互阻塞

---

*本日报由 AI 自动生成，数据来源：[github.com/openclaw/openclaw](https://github.com/openclaw/openclaw)。生成时间：2026-08-10。*

---

## 横向生态对比

# 个人 AI 助手开源生态横向对比分析报告

**报告日期：** 2026-08-10  
**数据窗口：** 2026-08-09 00:00 — 2026-08-10 00:00 (UTC)

---

## 一、生态全景

个人 AI 助手开源生态正处于**从「可用」向「可信」转型的关键阶段**：OpenClaw 以日均 500+ 条更新的绝对活跃度领跑，在功能迭代与架构简化（去租约化、配对功能栈）上双线推进；与此同时，**消息静默失败、安全鉴权缺失、配置丢失**三大类问题在多项目中反复出现，成为制约用户信任的核心瓶颈。生态整体呈现**「头部极高活跃、腰部稳定迭代、尾部静默维护」**的三层分化格局——OpenClaw（1000 条更新）、ZeroClaw（100 条）、Hermes Agent（100 条）构成第一梯队，NanoBot、PicoClaw、IronClaw、NanoClaw 等处于中速迭代，而 TinyClaw、NullClaw 等微型项目已进入停滞状态。安全加固（SSRF、Webhook 鉴权、密钥管理）与「多用户/多租户」场景的支持需求正在多个独立项目中自发涌现，预示着生态正从**单机工具向平台基础设施**演进。

---

## 二、各项目活跃度对比

| 项目 | Issues 更新 | PR 更新 | Releases | 合并/关闭 PR | 健康度 | 阶段判断 |
|------|------------|---------|----------|-------------|--------|---------|
| **OpenClaw** | 500 | 500 | 0 | 10+（含 #121113 架构重构） | ★★★★☆ | 快速迭代 + 架构收敛并行 |
| **ZeroClaw** | 50 | 50 | 0 | **0** | ★★★☆☆ | 讨论热烈但合并停滞，50 个 PR 积压 |
| **Hermes Agent** | 100 | 100 | 0 | 1（#82741 SSH 修复） | ★★★★☆ | 高活跃，P0 bug 响应快但 PR 积压 36 条 |
| **NanoBot** | 4 | 15 | 0 | 4 | ★★★★☆ | 活跃稳定，2 个安全漏洞待修 |
| **PicoClaw** | 3 | 6 | 0 | 1 | ★★★☆☆ | 活跃但规模小，SSRF 修复待合并 |
| **NanoClaw** | 2 | 14 | 0 | **0** | ★★★☆☆ | 贡献密集但合并停滞 |
| **IronClaw** | 15 (新开) | 25 | 0 | 8 | ★★★★☆ | 健康，自动修复闭环已形成 |
| **LobsterAI** | 3 | 0 | 0 | 0 | ★★☆☆☆ | 轻度活跃，2 个 stale issue 濒临关闭 |
| **Moltis** | 2 | 1 | 0 | 0 | ★★★☆☆ | 低峰维护期 |
| **CoPaw / QwenPaw** | 17 | 50 | 0 | 1 | ★★★★☆ | 社区贡献活跃，49 个 PR 待审 |
| **TinyClaw** | 0 | 0 | 0 | 0 | — | 无活动 |
| **NullClaw** | 0 | 0 | 0 | 0 | — | 无活动 |
| **ZeptoClaw** | 0 | 0 | 0 | 0 | — | 无活动 |

> **数据说明：** OpenClaw 的 Issues/PR 更新数为平台统计口径，包含评论、标签变更等全部事件；实际新增 Issue 约 10+ 条、新 PR 约 5+ 条。

---

## 三、OpenClaw 在生态中的定位

**OpenClaw 是生态的绝对基准与事实上「标准制定者」** —— 其单个仓库的日更新量（1000 条事件）超过其余所有活跃项目之和（NanoBot + PicoClaw + NanoClaw + IronClaw + Moltis + LobsterAI ≈ 46 条 Issues + 46 条 PRs）。其定位优势体现在：

| 维度 | OpenClaw 表现 | 生态对比 |
|------|-------------|---------|
| **渠道覆盖** | Telegram、Slack、Discord、Matrix、WhatsApp、Teams、Line、微信等 20+ 渠道 | PicoClaw 覆盖 10+，NanoClaw 覆盖 8+，IronClaw 聚焦 Slack/Telegram |
| **架构演进** | 移除 SQLite 会话写租约、频道所有者策略下沉（#121257）、配对功能栈（5 个关联 PR） | ZeroClaw 在做类似的网关重构（#9744），但合并停滞 |
| **社区规模** | 单 Issue 最高 196 条讨论（#116277），P0/P1 标注 60+ 个 | Hermes 最高 18 条评论，NanoBot 最高 13 条 |
| **安全投入** | 拒绝 Claude 工具协议泄漏（#120734）、密钥保护路线图（#11829）、沙箱化 | 多数项目今天才补齐 SSRF 防护（PicoClaw #3322-#3324） |
| **Bug 修复节奏** | 当日新开 → 当日提交 fix PR（如 #121058 → #121059） | NanoBot、IronClaw 也具备此能力，但修复覆盖面较窄 |

**关键差异：** OpenClaw 的「配对」功能（一键公网连接 + Tailscale 集成）在生态中独树一帜，正在定义**自托管 AI 助手的设备互联标准**；ZeroClaw 在 Web3 金融场景（Solana 地址脱敏、区块链安全例外）上有差异化布局；Hermes Agent 的桌面端 SSH 远程连接与插件 SDK 形成了独特的多设备工作流。

---

## 四、共同关注的技术方向

以下方向在多个项目中独立涌现，构成生态的「最大公约数」：

### 1. 静默失败的系统性整治
| 项目 | 具体诉求 |
|------|---------|
| OpenClaw | DeepSeek 静默回复失败复发（#116277→#121058）；子代理结果静默丢失（#44925） |
| NanoBot | Telegram 轮询静默停滞（#5301/#5156） |
| PicoClaw | Matrix 断线静默死亡（#3203）——「无错误提示的失联」 |
| NanoClaw | 附件被静默丢弃（#3206）
| Moltis | 配置静默重置（#1187） |

**共性：** 从「显式崩溃」转向「静默降级」的 bug 形态正在成为用户最强烈的痛点，需要系统性增强可观测性与失败告警。

### 2. 多租户 / 多用户隔离需求
| 项目 | 具体诉求 |
|------|---------|
| Hermes Agent | 多租户架构方案（#34352，18 条评论）；内存操作绕过 Hook 系统 |
| ZeroClaw | Agent 所有权隔离（#9713/#9745）；工作通道治理 RFC（#6808） |
| IronClaw | 多用户共享会话（#7397）；基于 presence 的会话共享 |
| NanoClaw | 分组级密钥分配（#3205，设计分叉） |
| OpenClaw | 配对功能实质上是在解决多设备/多用户的连接层问题 |

**信号：** 单机个人助手 → 团队/组织级共享基础设施的演进方向明确，但各项目的实现路径各异（Hook 系统、沙箱隔离、密钥分组）。

### 3. 安全加固（SSRF / 鉴权 / 密钥管理）
| 项目 | 具体表现 |
|------|---------|
| OpenClaw | 掩码密钥系统（#10659）、API 密钥保护路线图（#11829）、文件沙箱（#7722） |
| NanoBot | exec 工具 shell-chain 绕过（#5305/#5306，高危） |
| PicoClaw | 7 个渠道的 SSRF 修复（#3322-#3324） |
| ZeroClaw | Webhook 未鉴权（#9565，P0）；CVE 被忽略（#8519） |
| Hermes Agent | 插件 SDK 崩溃（#80560）；进程自终止防护（#6234） |
| IronClaw | Routine 自我复制风险（#6479） |

**信号：** 安全正在从「功能选项」变为「准入门槛」，Fail-closed 默认值成为社区共识（ZeroClaw #9397）。

### 4. 工具调用与上下文管理
| 项目 | 具体表现 |
|------|---------|
| OpenClaw | 工具调用间文本泄漏（#25592，41 条评论）；预算压缩超时（#115546） |
| IronClaw | 流式 API + tools 100% 失败（#7400）；工具发现效率优化（#7405） |
| CoPaw | MCP 数字字符串强转（#6839）；Gemini Schema 校验失败（#6812） |
| LobsterAI | 自定义模型标识被误判（#2453） |
| NanoClaw | Slack 粘贴表格丢失（#3209） |

**信号：** 工具调用的**上下文边界**（哪些文本该进消息、哪些不该）和**效率**（减少不必要的轮次）是模型在实际工作流中的核心瓶颈。

---

## 五、差异化定位分析

| 项目 | 核心定位 | 目标用户 | 技术架构亮点 | 典型案例/垂直场景 |
|------|---------|---------|-------------|------------------|
| **OpenClaw** | 全渠道个人 AI 助手（瑞士军刀） | 技术型个人用户、自托管爱好者 | SQLite + 会话租约（正在移除）；runners 架构；配对/Tailscale 集成 | Telegram/DeepSeek 日常使用、Cloud Worker 桌面 |
| **ZeroClaw** | 安全优先的多租户 AI 网关（Rust） | 企业/团队、Web3 开发者 | Rust；网关层强鉴权（PR #9744）；SOP 引擎；PGVector | WhatsApp Business、Solana 地址脱敏例外 |
| **Hermes Agent** | 桌面优先的多设备助手 | 重度桌面用户、开发者 | Desktop Electron + SSH 远程；插件 SDK；多 Session 窗口 | 远程开发、本地模型调度、Team/Organization 工作流 |
| **NanoBot** | 极简核心 + 可插拔技能 | 轻量用户、快速部署场景 | Go 极简架构；Agent Plugins v1；GitAgent Protocol（已关闭） | Telegram 轻量部署、Docker 一键启动 |
| **IronClaw** | 自动化工作流 + 数据分析 | 数据驱动用户、运营人员 | Responses API；Routine 自动化；Nightly Deep CI | 邮件→表格自动化、Slack 触发报表 |
| **CoPaw/QwenPaw** | 多模型协作 + 审批流 | 中文用户、多模型团队 | 深度集成 Qwen/Aliyun；ReMe 记忆系统；微信审批 | 微信渠道审批、跨模型子任务 |
| **PicoClaw** | 多渠道消息网关 | 自托管轻量用户 | Go 轻量；一码多端（QQ/Telegram/Discord/LINE/Slack/WeCom）；安全 HTTP 客户端统一 | IM 渠道桥接、附件下载安全 |
| **NanoClaw** | 容器化多渠道 Agent | 容器/DevOps 用户 | 容器优先设计；Dial 渠道（SMS+语音）；CVE 门禁 CI | 容器部署、SMS/语音交互 |
| **LobsterAI** | 多模型切换与协作 | 多模型工作流用户 | 自定义模型路由；跨模型子任务 | OpenRouter 免费模型切换、本地+云模型并行 |

---

## 六、社区热度与成熟度分层

| 层级 | 项目 | 活跃度指标 | 阶段特征 |
|------|------|-----------|---------|
| **T0 - 快速迭代 + 架构收敛** | OpenClaw | 1000 更新/日；P0/P1 标记 60+；大型重构与高价值修复同步 | 功能爆发期与稳定化并行，合并积压是主要瓶颈 |
| **T1 - 高活跃，质量攻坚** | Hermes Agent、ZeroClaw、IronClaw、CoPaw | 100-170 更新/日；零合并（ZeroClaw）或 8 个合并（IronClaw） | 社区贡献意愿强但 PR 合并节奏不稳，安全/稳定性问题集中爆发 |
| **T2 - 中速迭代，需求响应良好** | NanoBot、PicoClaw、NanoClaw | 10-40 更新/日；当日 Issue → 当日 PR 的闭环 | 小团队高效响应，但对大型重构/新功能推进谨慎，增量式开发为主 |
| **T3 - 低峰维护** | Moltis、LobsterAI | <5 更新/日；PR 稀疏 | 维护者带宽有限，社区反馈积压（stale issue 频发） |
| **T4 - 停滞/冻结** | TinyClaw、NullClaw、ZeptoClaw | 0 更新 | 无任何活动，可能已停止维护 |

---

## 七、值得关注的趋势信号

### 1. 「静默失败」成为最迫切的信任危机
OpenClaw（#116277 复发）、PicoClaw（#3203 无重连）、NanoBot（#5301 轮询停滞）、NanoClaw（#3206 附件静默丢弃）——四个独立项目同一天内出现「无报错但功能失效」的报告。**对开发者意味着：** 将「失败告警」和「可观测性」视为一等公民，而非事后补丁。在自托管场景下，无声故障 = 完全不可用。

### 2. 安全正在从「功能选项」变为「准入门槛」
SSRF 修复（PicoClaw 7 渠道）、Webhook 鉴权（ZeroClaw P0）、exec shell 逃逸（NanoBot 高危）、CVE 门禁（NanoClaw CI、IronClaw nightly）——安全不再是被动响应，而是进入 CI 流水线和默认配置。**对开发者意味着：** Fail-closed 默认值是趋势，新项目应从第一天就纳入安全 checklist，而非事后补救。

### 3. 「工具调用上下文隔离」是 Agent 可靠性的新战场
OpenClaw 的文本泄漏（#25592）与 IronClaw 的 stream+tools 失败（#7400）揭示了同一个深层问题：**工具的中间输出与最终输出需要清晰分层**。当 Agent 同时执行多个工具时，「什么该被当作消息发给用户」的边界模糊，是 UX 和安全双重风险。**对开发者意味着：** 在设计工具协议时，明确定义「内部处理」vs「用户可见」的通道，并考虑流式场景下的响应一致性。

### 4. 多租户/多用户是规模化前提
Hermes（#34352）、ZeroClaw（#9713）、IronClaw（#7397）、NanoClaw（#3205）同方向的呼声，说明单机工具的成长天花板已经显现。**对开发者意味着：** 在架构设计早期预留「隔离边界」（Hook 系统、沙箱、密钥分组），而非等用户量增长后再重构。

### 5. 配对/设备互联正在成为新赛道
OpenClaw 的配对功能栈（5 个关联 PR）+ Tailscale 集成是当前生态中**唯一**系统性解决「自托管设备如何安全互联」的方案。**对开发者意味着：** 远程访问、多设备同步、一次性设备配对将成为个人 AI 助手的刚需能力，类似「AI 助手的 WebAuthn」。

### 6. 自动化修复闭环开始形成
IronClaw 的 `ironloopai[bot]` 在 24 小时内完成了「用户报告 bug → 自动提交修复 PR」的闭环（#7400→#7401），NanoClaw 和 OpenClaw 也出现了对应的自动修复 PR（#3209、#121059）。**对开发者意味着：** AI 辅助的 bug 修复正在从实验走向生产，开源项目的维护成本有望结构性下降，但这需要高质量的 CI 和测试门禁作为前提。

### 7. 配置复杂化 vs 默认值一致性的矛盾
ZeroClaw（#9779 SOP 默认值未生效）、OpenClaw（#48920 文档超前）、Moltis（#1187 表单静默重置配置）——多个项目暴露出配置系统在**「文档承诺」与「运行时行为」**之间的差距。**对开发者意味着：** 维护一份「可执行的配置文档」（如 schema 校验 + 默认值测试）比写更多文档更能提升用户信任。

---

## 结论

个人 AI 助手开源生态正从「功能竞赛」转向「**信任竞赛**」——用户不再接受「坏了就重启」或「无声失败」，而是要求可观测的日志、Fail-closed 的安全默认值、以及从不丢失用户数据的可靠性。OpenClaw 凭借其规模优势和技术迭代速度继续保持基准地位，但 ZeroClaw（Rust 安全路线）、Hermes（桌面场景）、IronClaw（自动化工作流）在各自细分方向上的深耕有望形成差异化竞争力。对于新入局的开发者，**在工具调用边界、多租户隔离、安全默认值三个方向上的投入，将比新增渠道适配更能构建长期壁垒。**

---

## 同赛道项目详细报告

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot 项目动态日报

**日期**: 2026-08-10  
**数据窗口**: 2026-08-09 ~ 2026-08-10（24小时）  

---

## 1. 今日速览

NanoBot 项目今日保持高度活跃，24小时内产生 **19 条更新**（4 Issues + 15 PRs），其中 **2 个安全漏洞报告**（#5305、#5306）和 **1 个 Docker 部署缺陷**（#5295）值得重点关注。合并/关闭 PR 4 个，集中在 WebUI 修复、测试增强与文档改进。最突出的社区声音是 **Token 消耗量异常**（#5266，13条评论），反映用户对成本透明度的迫切需求。整体项目健康度良好，活跃度高，但安全问题需及时响应。

---

## 2. 版本发布

**无新版本发布。**  
上一版本（数据概览未提供）以来，项目正通过 PR 累积以下高优先级变更：安全修复（`exec.allowPatterns` 绕过）、Token 用量记录 API、Telegram 轮询看门狗。预计下一个 patch 版本将包含上述内容。

---

## 3. 项目进展（今日合并/关闭的 PR）

| PR | 标题 | 类型 | 意义 |
|----|------|------|------|
| [#5307](https://github.com/HKUDS/nanobot/pull/5307) | Restore Star History chart | 文档/功能 | 恢复了被 GitHub 政策移除的 Star 历史图表，新的数据源不受近期 GitHub 限制，利于项目增长可视化 |
| [#5308](https://github.com/HKUDS/nanobot/pull/5308) | test: strengthen user-path coverage and CI gates | 测试/CI | 新增 CLI、WebUI 用户路径测试 5 个深度场景，引入 V8 覆盖率报告，CI 门禁强化——提升回归防护能力 |
| [#5304](https://github.com/HKUDS/nanobot/pull/5304) | fix(webui): explain HTTPS requirement for voice input | Bug 修复 | 修复 Android Chrome 下语音输入因 HTTP 非安全源而静默失败的问题，新增多语言 HTTPS 提示 |
| [#4019](https://github.com/HKUDS/nanobot/pull/4019) | Add GitAgent Protocol support (agent.yaml + SOUL.md) | 功能 | （关闭但未合并）为可移植 AI Agent 提供标准清单支持，与项目"极简核心、可扩展边缘"哲学一致 |

**重点推进**: WebUI 成熟度提升（语音输入、Star 图表、测试覆盖），测试基础设施加固。长期积压的 GitAgent Protocol PR（#4019，积压 75 天）被关闭，建议关注后续是否有替代方案。

---

## 4. 社区热点

### 🔥 [#5266](https://github.com/HKUDS/nanobot/issues/5266) — Token 消耗量异常（13 评论，创建 4 天）

**核心诉求**: 用户反馈 NanoBot 在无明显用户活动的情况下，2 小时内消耗约百万 Token，且无任何日志可供排查。

**背后诉求**: 
- 成本透明度缺失——用户无法定位 Token 消耗的来源（哪次调用、哪个模型、哪个频道）
- 需要一个结构化的 Token 用量审计日志：时间戳 + 调用来源 + Token 数

**关联信号**: 社区已提交 PR [#5299](https://github.com/HKUDS/nanobot/pull/5299)（结构化 Token 用量记录 API），说明维护者已响应此诉求，但 PR 仍待合并。

### 📢 [#5295](https://github.com/HKUDS/nanobot/issues/5295) — Docker Compose 部署失败（5 评论）

**核心诉求**: `docker compose up` 后 gateway 容器因 `entrypoint.sh: Permission denied` 退出（code 2），部署文档未能覆盖此场景。

**背后诉求**: 
- 开箱即用的部署体验是用户采用的关键障碍
- 需要明确 Dockerfile 中 `chmod +x` 的时机，或文档中增加常见错误排障章节

---

## 5. Bug 与稳定性

### 🔴 严重（安全漏洞）

| Issue | 问题描述 | Fix PR? |
|-------|----------|---------|
| [#5306](https://github.com/HKUDS/nanobot/issues/5306) | `exec.allowPatterns` shell-chain 绕过——允许列表可被拼接命令绕过，导致非预期命令执行 | ❌ 暂无修复 PR，需尽快响应 |
| [#5305](https://github.com/HKUDS/nanobot/issues/5305) | 同源问题——通过 OpenAI 兼容 API 同样可绕过 allowlist 执行链式 shell 命令 | ❌ 暂无修复 PR，需尽快响应 |

> ⚠️ **安全团队建议**: 这两个漏洞指向同一根因（shell 命令分隔符未过滤），建议合并为一个 CVE 处理，并紧急审查 `exec` 工具的参数校验逻辑。

### 🟡 中等

| Issue/PR | 问题描述 | 状态 |
|----------|----------|------|
| [#5295](https://github.com/HKUDS/nanobot/issues/5295) | Docker Compose 部署失败：`entrypoint.sh` 权限不足 | ❌ 无修复 PR，建议文档补充或修复 Dockerfile |
| [#5301](https://github.com/HKUDS/nanobot/pull/5301) | Telegram 轮询静默停滞（相关 #5171）——日志无输出但 bot 停止接收消息 | ✅ 已有 PR #5156（完整看门狗）+ #5301（轻量日志桥接） |
| [#5302](https://github.com/HKUDS/nanobot/pull/5302) | Dream 记忆整合时调用了受限工具集之外的工具（提示词与工具注册表不匹配） | ✅ 已有修复 PR 待合并 |
| [#5303](https://github.com/HKUDS/nanobot/pull/5303) | Windows PowerShell 下天气技能因 `curl` 别名解析失败 | ✅ 已有修复 PR 待合并 |

### 🟢 轻微

| Issue/PR | 问题描述 | 状态 |
|----------|----------|------|
| [#5304](https://github.com/HKUDS/nanobot/pull/5304) | Android Chrome 语音输入在 HTTP 非安全源下静默失败 | ✅ 已合并，文档与 UI 均已修复 |

---

## 6. 功能请求与路线图信号

| 功能需求 | 来源 | 对应 PR/信号 | 纳入下一版本可能性 |
|----------|------|-------------|-------------------|
| **Token 用量审计日志** | Issue [#5266](https://github.com/HKUDS/nanobot/issues/5266) | PR [#5299](https://github.com/HKUDS/nanobot/pull/5299) 新增 `/api/settings/usage/records?day=` API + 持久化 50 条记录 | 高（PR 已就绪，等待合并） |
| **API 服务状态真实呈现** | PR [#5255](https://github.com/HKUDS/nanobot/pull/5255) | 草稿 PR——区分外部管理的 `nanobot serve` 实例与 gateway 自身启动的实例，新增 `nanobot api status` 命令 | 中（Draft 状态，需完善） |
| **模型无关的计算机控制** | PR [#4276](https://github.com/HKUDS/nanobot/pull/4276) | 新增 `browser` + `computer_use` 原生工具，支持 DOM 自动化与桌面控制 | 中（积压 60 天，功能重大） |
| **插件体系统一** | PR [#5288](https://github.com/HKUDS/nanobot/pull/5288) | Agent Plugins v1 集成 CLI Apps，统一可移植技能边界 | 中（方向正确，等待评审） |
| **GitAgent Protocol 支持** | PR [#4019](https://github.com/HKUDS/nanobot/pull/4019) | 已关闭，未合并 | 低（未被采纳，但社区有呼声） |

---

## 7. 用户反馈摘要

### 真实痛点

1. **成本失控焦虑**（来自 #5266 评论）
   > "百万 Token 在 2 小时内烧掉，期间用户完全无感。这不是功能问题，是信任问题——我需要知道每一笔 Token 去哪了。"

2. **部署门槛**（来自 #5295）
   > "按部署文档操作，Docker 直接启动失败，日志只有一行 Permission denied。作为新用户，第一印象非常糟糕。"

3. **Telegram 稳定性**（来自 #5156/#5301 关联）
   > "生产环境连续跑了 3 天，突然 bot 就沉默了，进程还活着，日志没有任何异常。这种无声故障比报错更可怕。"

### 使用场景洞察

- **Docker 是主流部署方式**——#5295 的快速反馈表明用户首选容器化部署
- **Telegram 频道是核心使用渠道**——轮询停滞问题引发大量关注
- **安全意识强的用户主动审计权限**——#5305/#5306 由同一用户提交，说明有用户在生产环境执行了严格的安全审计

---

## 8. 待处理积压

### 🚨 需立即关注

| 项目 | 积压时间 | 说明 |
|------|----------|------|
| [#5306](https://github.com/HKUDS/nanobot/issues/5306) 安全漏洞 | 1 天 | 高危 shell 注入绕过，建议 48h 内响应 |
| [#5305](https://github.com/HKUDS/nanobot/issues/5305) 安全漏洞 | 1 天 | 同根因，需与 #5306 联合修复 |
| [#5266](https://github.com/HKUDS/nanobot/issues/5266) Token 审计 | 4 天 | 社区高度关注（13 评论），PR #5299 待合并 |

### ⏳ 中期积压（>2 周）

| 项目 | 积压时间 | 说明 |
|------|----------|------|
| [#4276](https://github.com/HKUDS/nanobot/pull/4276) 计算机控制 | 62 天 | 功能完整，但涉及面广（桌面控制），建议明确是否纳入主线 |
| [#5156](https://github.com/HKUDS/nanobot/pull/5156) Telegram 看门狗 | 12 天 | 社区已观察生产故障，PR 就绪但未合并，建议优先 |

---

## 📊 项目健康度评估

| 维度 | 评分 | 说明 |
|------|------|------|
| **活跃度** | ★★★★★ | 日均 ~20 条更新，社区响应积极 |
| **安全性** | ★★★☆☆ | 2 个未修补的安全漏洞为最大隐患 |
| **稳定性** | ★★★★☆ | Telegram 轮询与 Docker 部署问题已定位，修复 PR 待合 |
| **社区满意度** | ★★★★☆ | 高活跃但 Token 成本问题悬而未决，影响信任 |
| **维护响应速度** | ★★★★☆ | 新 Issue 平均得到响应 < 48h，但 PR 合并略有积压 |

**关键建议**: 优先合并 #5299（Token 记录 API）与 #5156（Telegram 看门狗），同时尽快对 #5305/#5306 安全漏洞发布 advisory 和修复版本。

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

好的，我是您的 AI 智能体与个人 AI 助手领域开源项目分析师。根据 Hermes Agent (github.com/nousresearch/hermes-agent) 在 2026 年 8 月 10 日的 GitHub 数据，我为您生成了以下项目动态日报。

---

### Hermes Agent 项目动态日报 (2026-08-10)

#### 1. 今日速览

Hermes Agent 项目今日处于高活跃度状态，过去 24 小时内共有 100 条 Issues 和 PR 更新，显示出强劲的开发动力。值得关注的是，**会话状态管理（Session State）** 成为今日的核心焦点，共有 10 余个相关 Issues 和 PR 被标记了风险标签，并涌现出一个 P0 级别的数据丢失 Bug（[#82756](https://github.com/NousResearch/hermes-agent/issues/82756)）。与此同时，社区对 **多租户（Multi-Tenancy）** 能力的呼声高涨，出现了多个相关功能讨论。项目维护者（如 `teknium1`）积极参与问题修复，提交了关键的 PR，但仍有大量 PR 等待合并。

#### 3. 项目进展

今日合并/关闭的 PR 主要集中在**桌面端 SSH 连接稳定性**的修复上，解决了长期困扰用户的版本检测误报问题。

- **[PR #82741] fix(desktop-ssh): stop resolving exec-wrappers to python in locateHermes** - 由 `teknium1` 提交并关闭。该 PR 修复了桌面端 SSH 模式下，因错误的解析策略导致版本检测失败、误报远程安装不支持新参数的问题。此前已有 [PR #74425](https://github.com/NousResearch/hermes-agent/pull/74425) 和 [PR #79289](https://github.com/NousResearch/hermes-agent/pull/79289) 尝试解决相关问题，但最终由该 PR 完成修复，体现了维护者对关键路径的直接介入和收敛。
- 这部分修复直接解决了 Issue [#74411](https://github.com/NousResearch/hermes-agent/issues/74411)，提升了桌面端远程连接的可靠性和用户体验。

整体而言，项目在关键路径的 Bug 修复上响应迅速，但在新功能合并上显得较为谨慎，大量 PR 处于待合并状态（36 条），可能成为项目进展的瓶颈。

#### 4. 社区热点

今日社区讨论热度最高的议题集中在两大方向：

1.  **多租户与多智能体支持**：
    - **[Issue #34352] Solving the Multi-Tenant Hermes Problem** (18 条评论，👍 2) - 这是今日讨论最热烈的话题。用户 `NimbleCoAI` 指出现有内存操作绕过 Hook 系统，导致无法实现租户隔离，并分享了其生产环境的修复方案。这反映了用户对 Hermes 从单用户工具向多用户平台演进的强烈需求。
    - 相关地，今日还有新 Issue **[#82701] Multi-Tenant Orchestrator** 提出，进一步印证了社区在该方向上的集中诉求。

2.  **资源管理与安全**：
    - **[Issue #82678] Telegram fallback path can exceed the process FD budget** (1 条评论) - 尽管评论不多，但该 Issue 揭示了一个潜在的系统稳定性风险，即 Telegram 回退路径可能耗尽进程的文件描述符，引发了社区对运行时资源管理的关注。

#### 5. Bug 与稳定性

今日报告的 Bug 较多，按严重程度排列如下：

- **严重 (P0) - 数据丢失**：
    - **[Issue #82756] Desktop plain-Enter submit silently deleted ~65 messages** - 这是今日最严重的 Bug，已是第三次出现同类问题（前两次为 #70516, #80763）。幸运的是，已有对应的修复 PR **[#82766](https://github.com/NousResearch/hermes-agent/pull/82766)** 提交并处于待合并状态。
- **较高 (P1/P2) - 功能异常/崩溃**：
    - **[Issue #82616] Gateway session continuity breaks under state.db FTS corruption** - 由维护者报告，描述了网关会话在数据库损坏时的严重断裂问题。
    - **[Issue #82700] projects.tree returns sessionCount=1 but an empty lane "sessions"** - 桌面端项目视图显示空的问题。
    - **[Issue #82679] Desktop app does not self-heal a dropped remote connection** - 远程连接断开后无法自动恢复，需手动操作。
    - **[Issue #80560] Plugin SDK crashes with React #310** - Windows 平台加载插件时崩溃，已有修复 PR [#82763](https://github.com/NousResearch/hermes-agent/pull/82763)。
    - **[Issue #82697] Settings → Plugins tears down the whole view** - 插件设置页导致整个应用崩溃。

#### 6. 功能请求与路线图信号

社区提出了多个新功能请求，部分可能被纳入后续版本：

- **明确的热门方向：多租户支持**。除了 [#34352](https://github.com/NousResearch/hermes-agent/issues/34352) 外，今日新增的 **[Issue #82701] Multi-Tenant Orchestrator** 提出了一个更具体、包含 OIDC 认证和沙箱容器的方案，为这一方向提供了清晰的技术蓝图。
- **新的插件/集成**：用户提出了一些针对特定工具链的插件请求，如新增 `Codex` Web 搜索后端（[#82716](https://github.com/NousResearch/hermes-agent/issues/82716)）和 `GBrain` 记忆提供商（[#46253](https://github.com/NousResearch/hermes-agent/issues/46253)），这显示了社区对扩展 Hermes 生态的意愿。
- **体验优化**：**[PR #82505](https://github.com/NousResearch/hermes-agent/pull/82505)** 为未命名会话提供确定性标题，可以显著改善会话管理体验。**[PR #82767](https://github.com/NousResearch/hermes-agent/pull/82767)** 修复了模型选择器无法显示 OpenRouter 元路由器的问题。

#### 7. 用户反馈摘要

从今日的 Issues 中，可以提炼出以下用户痛点：

- **“同样的错误，第三次了”**：P0 Bug [#82756](https://github.com/NousResearch/hermes-agent/issues/82756) 中，用户明确表示会话历史丢失已是第三次发生，且前两次的修复未能覆盖所有路径。这反映出用户对核心数据可靠性问题的容忍度正在降低，对修复质量提出了更高要求。
- **“配置不生效/静默失败”**：多个 Bug 反映了配置在特定场景下被忽略或无法持久化，例如桌面端皮肤不保存（[#71446](https://github.com/NousResearch/hermes-agent/issues/71446)）、桌面端 UI 缩放被重置（[#82713](https://github.com/NousResearch/hermes-agent/issues/82713)）等。这些问题虽不致命，但会持续消耗用户的信任。
- **“我需要一个更强大的 Hermes”**：在多租户、跨配置子代理（[#41889](https://github.com/NousResearch/hermes-agent/issues/41889)）等 Issue 中，用户表达了希望 Hermes 能更好地服务团队和复杂工作流的诉求，而不仅仅是作为单机个人助手。

#### 8. 待处理积压

部分长期开放的 Issue 和 PR 值得维护者重点关注：

- **[PR #6234] fix(approval): guard literal current-PID self-kill** - 打开自 2026-04-08，旨在修复一个安全边界问题，防止Agent自我终止。该 PR 涉及安全，牵涉面广，但长期未合并，可能存在设计或兼容性争议，需要维护者决策。
- **[PR #48473] fix(desktop): preserve profile for session windows** - 打开自 2026-06-18，旨在修复桌面端多窗口会话的 Profile 上下文丢失问题。这属于体验改进，但已搁置近两个月，可能因优先级较低而被忽略。

---
**数据说明**：本报告基于 2026-08-10 获取的 GitHub 数据生成，所有链接均指向 NousResearch/hermes-agent 仓库。

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw 项目动态日报

**日期：** 2026-08-10  
**数据窗口：** 2026-08-09 至 2026-08-10（UTC）  
**数据来源：** github.com/sipeed/picoclaw

---

## 1. 今日速览

PicoClaw 项目过去 24 小时活跃度较高：3 条 Issue 更新、6 条 PR 更新，其中 5 条新 PR 等待合并，显示社区贡献意愿强烈。安全方向成为今日主线——三条 PR（#3322、#3323、#3324）集中修复多协议（QQ/Telegram/Discord/LINE/Slack/WeCom/Weixin）的 SSRF 漏洞，覆盖面广且系统性较强，表明项目正在主动加固出站请求安全边界。功能层面，Telegram 富文本表格渲染的 Feature 请求（#3325）与对应实现 PR（#3327）同日出现，需求响应速度良好。值得关注的是，已有较长期悬而未决的问题（如 #3203 Matrix 重连 Bug 关闭仅标注为 stale），维护者需注意 backlog 清理与跟进。

---

## 2. 版本发布

过去 24 小时无新版本发布。上次发布仍为 v0.2.9（参考 Issue #3203 环境信息）。当前密集的 PR 合并后，建议维护团队尽早规划 v0.3.0 或 v0.2.10 发布窗口，尤其考虑到 SSRF 加固修复属安全修复类型，应尽快随版本推送。

---

## 3. 项目进展

今日合并/关闭 1 条 PR，另有 5 条待合并：

| 状态 | PR | 内容 | 类型 |
|------|-----|------|------|
| ✅ 已合并 | [#3326](https://github.com/sipeed/picoclaw/pull/3326) | 修复 `web/frontend/pnpm-lock.yaml` 中重复的 `semver@7.8.5` 映射条目，解决 `pnpm install --frozen-lockfile` 报 `ERR_PNPM_BROKEN_LOCKFILE` 的问题 | 构建修复 |
| ⏳ 待合并 | [#3322](https://github.com/sipeed/picoclaw/pull/3322) | 为 QQ / Telegram / Discord / LINE / Slack 入站附件下载增加 `BlockPrivateTargets` SSRF 防护 | SSRF 加固 |
| ⏳ 待合并 | [#3323](https://github.com/sipeed/picoclaw/pull/3323) | 为 WeCom 媒体下载改用 `CreateSafeHTTPClient`，防止重定向到 loopback/私有主机 | SSRF 加固 |
| ⏳ 待合并 | [#3324](https://github.com/sipeed/picoclaw/pull/3324) | 为 Weixin 媒体下载同步引入安全 HTTP 客户端与 URL 校验 | SSRF 加固 |
| ⏳ 待合并 | [#3327](https://github.com/sipeed/picoclaw/pull/3327) | 实现 Telegram 原生富文本表格渲染（对应 Feature #3325） | 功能实现 |
| ⏳ 待合并 | [#3222](https://github.com/sipeed/picoclaw/pull/3222) | DeltaChat 频道代码重构：精简约 200 行、更新文档、增加 invite_link 相关 API | 重构/文档 |

**整体方向**：项目当前重心明确在（a）SSRF 安全加固——涉及几乎所有主流 IM 渠道的入站媒体下载路径；（b）跨渠道消息渲染升级——Telegram 表格富文本化；以及（c）DeltaChat 模块的代码质量与文档清理。其中 DeltaChat 重构 PR 已搁置超过一个月（7 月 3 日创建），建议维护者尽快审查。

---

## 4. 社区热点

🔥 **最热 Issue：[#3203](https://github.com/sipeed/picoclaw/issues/3203)「Matrix sync loop has no reconnection logic — silent death after network/server disruption」**

- **状态：** CLOSED（标记为 stale 后关闭）
- **评论数：** 8（本期最高）| 👍 2
- **创建时间：** 2026-07-02 | **关闭时间：** 2026-08-09

**背景**：Matrix 渠道的 `/sync` 长轮询在遭遇网络中断或 homeserver 重启后永久死亡。主进程存活，systemd 的 `Restart=on-failure` 不触发，导致用户无感知地失联。

**评论诉求分析**：从评论数 8 条来看，社区对该问题关注度较高——这本质上是「静默失败」类问题，比显式崩溃更难排查，对生产环境用户影响极大。Issue 最终被标记为 stale 并关闭，但**根本问题（缺乏自动重连机制）并未在关闭评论中确认解决**。考虑到 Matrix 是 PicoClaw 的核心渠道之一，此问题可能需要重新开启或另立 Issue 追踪。

---

## 5. Bug 与稳定性

按严重程度排列：

| 严重度 | 项目 | 描述 | 状态 |
|--------|------|------|------|
| 🟥 高危（安全） | [#3322](https://github.com/sipeed/picoclaw/pull/3322) | 多个频道（QQ/Telegram/Discord/LINE/Slack）入站附件下载可被精心构造的 URL 导向 loopback、link-local 或 RFC1918 地址（SSRF） | **已有修复 PR，待合并** |
| 🟥 高危（安全） | [#3324](https://github.com/sipeed/picoclaw/pull/3324) | Weixin 媒体下载使用普通 HTTP Client，重定向可触达内网地址 | **已有修复 PR，待合并** |
| 🟥 高危（安全） | [#3323](https://github.com/sipeed/picoclaw/pull/3323) | WeCom 媒体下载同样存在 SSRF 风险 | **已有修复 PR，待合并** |
| 🟨 中危（可靠性） | ~~[#3203](https://github.com/sipeed/picoclaw/issues/3203)~~ | Matrix 同步循环断线后静默死亡，无自动重连 | 已关闭（stale），**未确认修复** |
| 🟩 低危（构建） | [#3326](https://github.com/sipeed/picoclaw/pull/3326) | 前端 pnpm lockfile 重复键值导致 `--frozen-lockfile` 失败 | ✅ 已合并 |

**分析**：SSRF 三连 PR（#3322/#3323/#3324）来自同一作者（SashaMIT），展示了对代码库的深入理解，PR 描述清晰、修复方式统一（复用 `utils.CreateSafeHTTPClient` 与 `ValidateSafeHTTPURL`），设计合理。此类安全修复应优先合并并尽快发布。值得留意的是，`utils.DownloadFile` 的 `BlockPrivateTargets` 能力此前已存在于代码库但仅 OneBot 使用，说明其他渠道接入时缺乏统一安全审计，建议项目层面补充渠道接入的安全 checklist。

---

## 6. 功能请求与路线图信号

### 新请求

| Issue | 需求 | 分析 |
|--------|------|------|
| [#3325](https://github.com/sipeed/picoclaw/issues/3325) | Telegram 表格以原生富文本渲染，而非代码块降级展示 | **已被 PR #3327 实现**，需求响应极快（同日内完成），说明该功能开发门槛较低且作者积极性高 |
| [#3287](https://github.com/sipeed/picoclaw/issues/3287) | IRCv3 长消息应被识别为单一消息，而非按 512 字节分割后的多段消息 | 暂无对应 PR。需要分析 IRC 消息合并策略，涉及协议层消息重组逻辑，复杂度中等 |

### 路线图信号

1. **安全加固为当前最高优先级** — 三条 SSRF 修复 PR 指向同一功能域，且覆盖面极广（7 个渠道）。如果合并，PicoClaw 的消息安全加固即告一段落。
2. **媒体消息处理标准化** — `utils.CreateSafeHTTPClient` 的推广使用表明项目正在标准化出站请求处理方式，建议后续推进 `utils.DownloadFile` 的 `BlockPrivateTargets` 参数默认为开启。
3. **多平台渲染一致性** — Telegram 表格富文本化可能引发 Discord、Slack 等平台的同类需求，建议提前规划跨渠道的消息渲染抽象层。

### 版本建议

若 #3322/#3323/#3324 合并，连同 #3327（Telegram 表格）可共同进入下一个 minor 版本（v0.3.0），同时将 SSRF 修复标注为安全更新，建议同步发布安全公告。

---

## 7. 用户反馈摘要

| 来源 | 用户声音 | 洞察 |
|------|----------|------|
| [#3203](https://github.com/sipeed/picoclaw/issues/3203) | Matrix 断线后无重连，系统状态看似正常但实际已失联 | 「静默死亡」问题对自托管用户是最糟体验——没有错误提示、没有重启、没有任何补救机会。社区关注度高（👍 2，8 条评论），但 issue 被 stale 自动关闭而问题可能仍未解决，需维护者确认 |
| [#3287](https://github.com/sipeed/picoclaw/issues/3287) | IRC 长消息被拆断，影响上下文理解 | IRC 512 字节限制是协议硬性约束，但现代 IRCv3 支持消息标签与长度扩展。用户的核心诉求是「语义完整性」，期待 PicoClaw 在协议层面做消息重组而非简单透传 |
| [#3325](https://github.com/sipeed/picoclaw/issues/3325) | 结构化表格在 Telegram 上降级为等宽代码块，视觉效果差 | 用户追求跨端一致的富文本体验。PicoClaw 作为网关型项目，消息渲染质量直接决定用户体验评价 |

**综合**：用户最在意「消息语义完整传递」（IRC）与「渲染品质」（Telegram），同时「静默失联」（Matrix）是负面体验的的主要来源。

---

## 8. 待处理积压

### ⚠️ 高优先级

| 项目 | 问题 | 搁置时长 | 建议 |
|------|------|----------|------|
| [#3203](https://github.com/sipeed/picoclaw/issues/3203) | Matrix 无重连逻辑 | 2026-07-02 创建，08-09 关闭（stale） | **建议重新开启并修复**。问题描述清晰（附环境信息 v0.2.9），影响核心渠道可靠性，不应以 stale 关闭作为结束 |

### 中优先级

| 项目 | 问题 | 搁置时长 | 建议 |
|------|------|----------|------|
| [#3222](https://github.com/sipeed/picoclaw/pull/3222) | DeltaChat 重构 PR | 2026-07-03 创建，已超过一个月未合并 | 代码重构 -200LOC 且有完整文档更新。长时间未合并可能面临大幅冲突，建议尽快审查或给出明确反馈 |
| [#3287](https://github.com/sipeed/picoclaw/issues/3287) | IRC 长消息支持 | 2026-07-22 创建，18 天无进展 | 功能需求合理（IRCv3 支持），暂无实现 PR，建议排入路线图或在 issue 中给出回应 |

### 维护建议

1. **Stale bot 策略需人工兜底** — #3203 被自动关闭但问题未修复，建议对 critical/security 标记的 issue 豁免 stale 自动关闭。
2. **安全修复优先合并** — 三条 SSRF 修复 PR 已在等待区，建议尽快 review 并合并，避免同批次其他渠道遗漏。
3. **渠道接入安全模板** — 建议将 SSRF 防护写入「新渠道接入」的文档要求中，避免类似遗漏再次出现（OneBot 有防护但其他渠道没有）。

---

*本报告由 AI 自动生成，数据截止 2026-08-10。*

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw 项目动态日报 — 2026-08-10

## 1. 今日速览

NanoClaw 项目过去24小时活跃度**较高**，核心开发节奏明显加快。今日共有 2 条新 Issue 和 14 条待合并 PR，其中 8 条由核心贡献者 zvi-fried 提交的系列重构/文档 PR（#3211-#3215、#3186）占据主流，标志着项目正在系统性推进**模块化架构与生命周期管理**相关工作。值得关注的是，**附件投递链路**成为今日焦点：既有新 Issue #3206 报告 Google Chat 渠道的路径分隔符导致附件静默丢弃，也有多条关联 PR（#2529、#3142、#3210）正在修复同类问题，说明该领域存在积压已久的系统性缺陷，维护者已开始集中整治。另一方面，gabi-simons 提交的 `[core-team]` PR 显示官方团队正在强化**容器安全与 CI 发布链路**，项目治理方向清晰。综合判断：项目处于**活跃迭代期**，合并节奏稳健（今日无新合并，积压 PR 数量需关注），安全性修复与架构重构并进。

---

## 2. 版本发布

今日无新版本发布。最近一次发布信息暂缺，建议关注 [Releases 页面](https://github.com/nanocoai/nanoclaw/releases) 获取后续更新。

---

## 3. 项目进展

### 今日无已合并/关闭的 PR，但 14 条待合并 PR 揭示了明确的前进方向：

**架构持续重构（贡献者：zvi-fried）** — 系列 PR 旨在将主机生命周期、渠道渲染器、数据库迁移等模块统一注册与治理，提升项目可扩展性：
- [refactor(host): unify module lifecycle hooks (#3214)](https://github.com/nanocoai/nanoclaw/pull/3214) — 统一模块生命周期钩子
- [refactor(channels): register question renderers (#3213)](https://github.com/nanocoai/nanoclaw/pull/3213) — 渠道问答渲染器注册机制
- [refactor(db): add module migration registry (#3212)](https://github.com/nanocoai/nanoclaw/pull/3212) — 数据库模块迁移注册表
- [refactor: add host seams for skill-owned capabilities (#3186)](https://github.com/nanocoai/nanoclaw/pull/3186) — 为技能自有能力添加主机接缝
- [docs(skills): define single-responsibility integration rule (#3211)](https://github.com/nanocoai/nanoclaw/pull/3211) — 定义技能集成单一职责规则

**功能扩展（贡献者：OmriBenShoham）** — 新增 **Dial 渠道适配器**（支持 SMS + AI 语音通话），已完成渠道适配器和配置向导两部分：
- [feat(channels): add Dial channel adapter (#3041)](https://github.com/nanocoai/nanoclaw/pull/3041)
- [feat(setup): add Dial to the channel picker + wizard (#3050)](https://github.com/nanocoai/nanoclaw/pull/3050)

**运维与安全强化（贡献者：gabi-simons，core-team）**：
- [feat(ci): publish agent image to Docker Hub with CVE gates (#3208)](https://github.com/nanocoai/nanoclaw/pull/3208) — 新增 Docker Hub 发布流水线并加入 CVE 关卡
- [fix(container): bump pnpm and npm past fixable-critical tar CVE (#3207)](https://github.com/nanocoai/nanoclaw/pull/3207) — 修复容器镜像中 tar 组件的可修补关键级 CVE

**Bug 修复**：
- [fix(slack): surface pasted tables to the agent (#3209)](https://github.com/nanocoai/nanoclaw/pull/3209) — 修复 Slack 粘贴表格无法传递给 Agent 的问题
- [fix(permissions): redact DM resolution logs (#3215)](https://github.com/nanocoai/nanoclaw/pull/3215) — 修复 DM 解析日志泄露敏感信息的问题

**总体评价**：尽管今日无合并，但 14 条高质量 PR 集中待审（其中多条已跨越数月等待期），一旦批量合入，项目将在渠道扩展、架构规范性和容器安全三个维度显著推进。**建议维护者优先审查已积压 3 个月以上的 #2529 和 #3142 两条附件修复 PR。**

---

## 4. 社区热点

今日最热门的讨论集中在 **附件投递链路** 的修复，多条 PR 和 Issue 相互呼应，形成明显的"问题-修复"簇：

**核心热点：入站附件静默丢弃问题**
- [Issue #3206: Inbound attachments silently dropped on path-separator channel IDs (#3206)](https://github.com/nanocoai/nanoclaw/issues/3206) — 新报告，指出 Google Chat 渠道消息 ID 包含路径分隔符时，附件被 `isSafeAttachmentName` 静默拒绝
- [PR #2529: deliver inbound attachments to the agent (#2529)](https://github.com/nanocoai/nanoclaw/pull/2529) — 5月18日提出，已积压近3个月，目标是彻底修复该问题，关闭 #2528
- [PR #3142: forward attachments through mounted inbox (#3142)](https://github.com/nanocoai/nanoclaw/pull/3142) — 7月27日提出，针对性修复 Signal 渠道附件路径未挂载导致读取失败的问题
- [PR #3210: docs: tell the agent where received attachments land (#3210)](https://github.com/nanocoai/nanoclaw/pull/3210) — 文档改进，让 Agent 知晓附件落盘位置

**分析**：这一簇 PR/Issue 揭示了同一根因下的多个变体——附件在跨渠道传递时因路径处理不当（死路径、非法字符、未挂载目录）而丢失。社区诉求明确：**确保所有入站附件都能可靠地到达 Agent 手中**。建议维护者尽快审阅 #2529 和 #3142，前者可能是系统性修复方案，后者代表特定渠道的验证，两者合入将显著改善用户体验。

---

## 5. Bug 与稳定性

按严重程度排列今日报告的 Bug：

| 严重程度 | 描述 | Issue/PR | 是否有 Fix |
|---------|------|----------|-----------|
| 🔴 高 | **入站附件静默丢弃**: Google Chat 渠道消息 ID 含 `/` 或 `\` 时，附件被 `isSafeAttachmentName` 拒绝且无日志提示，用户无法感知文件丢失 | [Issue #3206](https://github.com/nanocoai/nanoclaw/issues/3206) | ⚠️ 部分：PR #2529 可能覆盖，但未合并 |
| 🟠 中 | **Signal 渠道附件路径未挂载**: 附件路径拼接为 `/workspace/extra/signal-attachments/<id>`，但该路径从未挂载到 Agent 容器，Read 工具无法访问，PDF/文本等非图片附件全部丢失 | [PR #3142](https://github.com/nanocoai/nanoclaw/pull/3142) | ✅ 已有 PR 待合并 |
| 🟢 低 | **容器安全漏洞**: 基础镜像 npm 携带的 tar 7.5.11 和 pnpm 自带的 tar 7.5.12 存在可修复的关键级 CVE (GHSA-23hp-3jrh-7fpw) | [PR #3207](https://github.com/nanocoai/nanoclaw/pull/3207) | ✅ 已有 PR 待合并 |
| 🟢 低 | **Slack 表格丢失**: 用户粘贴的表格内容无法传递给 Agent | [PR #3209](https://github.com/nanocoai/nanoclaw/pull/3209) | ✅ 已有 PR 待合并 |
| 🟢 低 | **DM 解析日志泄露**: 权限模块的 DM 解析日志可能包含敏感信息，未做脱敏处理 | [PR #3215](https://github.com/nanocoai/nanoclaw/pull/3215) | ✅ 已有 PR 待合并 |

**结论**：今日共报告 2 个新 Bug（#3206、#3205 为功能需求），另有 3 个早期 Bug 的修复 PR 仍积压中。最严重的是 **#3206 附件静默丢弃**——静默失败是最差的行为模式，建议优先合入 #2529 并补充日志告警。

---

## 6. 功能请求与路线图信号

**新功能需求（今日提出）：**

1. **[Issue #3205: 支持持久化的分组级 OneCLI 密钥分配](https://github.com/nanocoai/nanoclaw/issues/3205)** — 用户 chiptoe-svg 指出项目当前存在 **"spawn-time 密钥分配的设计分叉"**：Agent 在生成时获取哪些 vault 密钥，项目中有两个矛盾的设计方向，且缺乏持久化的分组级模型。建议在 OneCLI 凭据网关中引入分组维度的密钥分配机制。

**与已有 PR 的关联判断：**
- **Dial 渠道支持** (#3041、#3050) — 新增 SMS + AI 语音通话渠道，属于用户可感知的渠道扩展，预计会随 PR 合入进入下一版本。
- **容器安全与发布流水线** (#3207、#3208) — 官方团队主导，属于平台级基础设施改进，大概率在近期合入。
- **zvi-fried 的系列重构** (#3211-#3215、#3186) — 虽为内部架构优化，但会为后续"技能生态"的扩展奠定基础，属于中期路线图的一部分。

**预测**：下一版本大概率包含 Dial 渠道支持、附件修复（Signal + 通用路径问题）、容器 CVE 修复和 Docker Hub 发布流水线。分组级密钥管理被纳入路线图的可能性较高，但需要维护者先收敛设计分歧。

---

## 7. 用户反馈摘要

今日 Issue 中的真实用户反馈（截至今日评论为 0，以下分析基于 Issue 文本本身揭示的痛点）：

**痛点 1：静默失败导致数据丢失（#3206）**
> 报告者 codybuell 明确指出 `isSafeAttachmentName` 对路径分隔符的检查过于粗暴，Google Chat 渠道的附件会**无声无息地消失**，用户完全无法感知。深层诉求不仅是修复 bug，更是要求系统在丢弃数据时必须有明确的告警机制。

**痛点 2：设计不确定性与分歧影响开发信心（#3205）**
> 用户 chiptoe-svg 用尖锐的措辞指出 OneCLI 密钥分配存在 **"two open, contradictory directions"（两个开放且矛盾的方向）**，且缺乏持久的权限模型。深层诉求是希望官方尽快收敛设计，避免社区开发者基于错误的设计假设进行二次开发。

**整体信号**：用户对 NanoClaw 的多渠道支持高度期待，但对附件可靠性（Silent Drop）和权限模型一致性存在明显担忧。建议维护者**优先处理静默失败类问题**，并在路线图文档中明确密钥管理的设计方向。

---

## 8. 待处理积压

以下 PR/Issue 长期未得到维护者响应，建议尽快处理：

| 类型 | 编号 | 标题 | 等待时长 | 建议 |
|------|------|------|---------|------|
| PR | [#2529](https://github.com/nanocoai/nanoclaw/pull/2529) | fix(signal): deliver inbound attachments to the agent | **84 天**（5月18日创建） | 附件投递核心修复，与今日新 Issue #3206 直接相关，**建议本周内审阅合入** |
| PR | [#3142](https://github.com/nanocoai/nanoclaw/pull/3142) | fix(signal): forward image/file attachments through mounted inbox | **14 天**（7月27日创建） | 同类附件问题，Signal 渠道具体复现，建议与 #2529 一并审查 |
| PR | [#3050](https://github.com/nanocoai/nanoclaw/pull/3050) | feat(setup): add Dial to the channel picker + wizard | **27 天**（7月14日创建） | 功能完整的新渠道支持，长期积压可能降低贡献者积极性 |
| PR | [#3041](https://github.com/nanocoai/nanoclaw/pull/3041) | feat(channels): add Dial channel adapter | **27 天**（7月14日创建） | 同上，与 #3050 配套 |
| PR | [#3186](https://github.com/nanocoai/nanoclaw/pull/3186) | refactor: add host seams for skill-owned capabilities | **6 天**（8月4日创建） | 架构重构系列中的基础 PR，后续多个 PR 依赖于此 |

**维护建议**：
- 优先处理 **附件可靠性** 问题链（#2529 + #3142 + #3210 + #3206），这是当前用户痛感最强烈的模块
- 关注 **zvi-fried 系列重构**的依赖关系，若 #3186 长时间未合入，后续 5 个 PR 均会持续阻塞
- 对 **#3205 密钥分配设计分歧**给出官方立场（哪怕是"暂不考虑"的回应），消除社区不确定性

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw 项目动态日报 — 2026-08-10

## 1. 今日速览

IronClaw 项目在过去24小时内保持了较高的活跃度：共产生 22 条 Issue 更新（其中 15 条新开/活跃、7 条已关闭）和 25 条 PR 更新（17 条待合并、8 条已合并/关闭），无新版本发布。值得关注的是，核心维护者 `serrrfirat` 围绕工具发现机制（#7405）提交了多个设计提案和栈式 PR（#7409、#7410），同时 `ironloopai[bot]` 自动生成了 4 个针对 QA bug 的修复 PR，形成了"问题报告 → 自动修复"的高效闭环。当前项目健康度良好，主要精力集中在工具发现效率优化、WebUI 稳定性修复和通知渠道扩展三个方向。

---

## 2. 版本发布

过去24小时内无新版本发布。

---

## 3. 项目进展

今日共有 8 个 PR 被合并/关闭，以下为关键合并：

| PR | 标题 | 影响 |
|---|---|---|
| [#7171](https://github.com/nearai/ironclaw/pull/7171) | fix(skills): one DB-backed tree for every skill mount, and make a skill's own commands runnable | **已合并**，修复了技能安装后永久消失的问题（关闭 #7168），这是技能系统的重要修复 |
| [#7323](https://github.com/nearai/ironclaw/pull/7323) | ci(nightly): grant actions: read to the reborn-tests call contract | **已合并**，修复了 Nightly Deep CI 连续5晚零任务的 `startup_failure` 问题 |
| [#7387](https://github.com/nearai/ironclaw/pull/7387) | chore(deps): bump everything-else group with 12 updates | 依赖批量升级（base64 0.22→0.23、toml 等） |
| [#7022](https://github.com/nearai/ironclaw/pull/7022) | chore(deps): bump actions group with 2 updates | GitHub Actions 升级 |

**项目整体向前迈进的方面：**
- **技能系统修复**：PR #7171 解决了"安装技能后消失"的严重问题，使技能安装真正落地
- **CI 基础设施修复**：Nightly CI 从连续5天的零任务失败恢复正常
- **技能文件系统**：该 PR 后续拆分了两个新 backlog（虚拟文件系统挂载、多租户沙箱）

---

## 4. 社区热点

### 最活跃 Issue

**[#7405](https://github.com/nearai/ironclaw/issues/7405) — 改进延迟工具发现（讨论中，2条评论）**
作者 `serrrfirat` 提出改进 `tool_search` 的返回签名和目录预览，以减少模型不必要的轮次消耗。该 Issue 被标记为 enhancement，并已拆分为两个栈式 PR（#7409、#7410），体现了维护者对该方向的重视。

**[#7400](https://github.com/nearai/ironclaw/issues/7400) — 流式响应 + caller tools 导致 100% 失败并遗留僵尸线程（高严重度）**
用户 `cuongdcdev` 报告了 Responses API 的严重 bug：`stream: true` + caller `tools[]` 组合在 1.1.0-rc.1 和 1.1.0 稳定版上均可 100% 复现，会导致中途失败并遗留无法删除的线程。该问题已获得 `ironloopai[bot]` 的快速响应，相关修复 PR #7401 已提交。

### 最活跃 PR

**[#7401](https://github.com/nearai/ironclaw/pull/7401) — 拒绝带外部工具的流式请求**
`ironloopai[bot]` 在 Issue #7400 报告后迅速提交修复，通过在提交前返回稳定的 400 错误（`param: tools`）来防止创建僵尸线程。

### 背后的诉求

社区对工具发现效率和 API 稳定性有明确诉求。`serrrfirat` 连续提交多个 Issue 和 PR 围绕工具发现机制优化，这暗示着随着平台工具数量增长，模型效率下降已成为实际痛点。`cuongdcdev` 报告的 API 严重 bug 也表明外部开发者对 API 的稳定性有较高期待。

---

## 5. Bug 与稳定性

### 严重（P0/P1）

| Issue | 描述 | 状态 |
|---|---|---|
| [#7400](https://github.com/nearai/ironclaw/issues/7400) | `stream: true` + `tools[]` 在 `/api/v1/responses` 100% 失败，遗留不可删除的"僵尸"线程 | 🔧 **已有修复 PR #7401** |

### 中等（P2）

| Issue | 描述 | 状态 |
|---|---|---|
| [#7292](https://github.com/nearai/ironclaw/issues/7292) | 已安装的 CoinGecko 工具无法使用，runner heartbeat 出错 | ✅ 已关闭 |
| [#7346](https://github.com/nearai/ironclaw/issues/7346) | Emoji 短代码在助手回复中显示为纯文本 | 🔧 **已有修复 PR #7404** |
| [#7348](https://github.com/nearai/ironclaw/issues/7348) | Activity 工具调用与进度消息在 UI 中时序错乱 | 🔧 **已有修复 PR #7403** |
| [#7345](https://github.com/nearai/ironclaw/issues/7345) | Agent 报告 61 个自动化，但 UI 仅显示 50 个 | 🔧 **已有修复 PR #7402** |
| [#7349](https://github.com/nearai/ironclaw/issues/7349) | 刷新页面后部分运行历史和 Activity 时间线消失 | 待处理 |
| [#5882](https://github.com/nearai/ironclaw/issues/5882) | Slack 反复重连后认证流程进入损坏状态 | 待处理 |
| [#6479](https://github.com/nearai/ironclaw/issues/6479) | Routine 可创建/修改其他 routine，有自我复制风险 | 待处理 |

### 已关闭（今日）

- [#5522](https://github.com/nearai/ironclaw/issues/5522) — Reborn routine 因 Slack DM 读取能力缺失而失败 → 已关闭
- [#5552](https://github.com/nearai/ironclaw/issues/5552) — 多工具失败后出现通用 "invalid result" 错误 → 已关闭
- [#5509](https://github.com/nearai/ironclaw/issues/5509) — 聊天创建延迟随历史积累增长 → 已关闭
- [#4341](https://github.com/nearai/ironclaw/issues/4341) — 模型思考链暴露给用户且卡在思考状态 → 已关闭
- [#4344](https://github.com/nearai/ironclaw/issues/4344) — Agent 在加载时将用户消息镜像为自身回复 → 已关闭

---

## 6. 功能请求与路线图信号

### 明确的新功能项

| Issue/PR | 描述 | 路线图判断 |
|---|---|---|
| [#7407](https://github.com/nearai/ironclaw/issues/7407) | 让 `BatchPolicy::Parallel` 能力批次真正并发执行 | 同作者的 #7405 系列，已被纳入 v1.2.0 epic 范畴，高概率纳入下一版本 |
| [#7392](https://github.com/nearai/ironclaw/issues/7392) | 实验：用 `oh-my-pi` 的固定工具表面替换第一方编码工具 | 标记为 epic，属实验性质，短期内不太可能默认启用 |
| [#7398](https://github.com/nearai/ironclaw/pull/7398) | 浏览器推送通知 + PWA，使 Web 应用成为第一方通知渠道 | 新 PR（XL 规模），与 Slack/Telegram 通知渠道对齐，可能是 v1.2.0 的功能亮点 |
| [#7397](https://github.com/nearai/ironclaw/pull/7397) | Slack & Telegram 基于 presence 的共享会话 | 基于已合入的 #7377 构建，表明多用户共享会话功能有明确路线图 |

### 工具发现优化（#7405）系列

这是 `serrrfirat` 正在推进的 v1.2.0 epic 核心工作：#7409（基准测试、100-1000 工具规模的检索质量基线的建立）→ #7410（返回完整的工具签名），稳步推进中。

---

## 7. 用户反馈摘要

从 Issues 评论中提炼的典型用户痛点：

- **工具使用失败率高**（#7292）：安装 CoinGecko 工具后，请求 "Top 10 trending coins" 时 agent 无法使用工具并最终报错。用户对"安装成功但无法使用"的体验表示困惑。
- **通知渠道体验不佳**（#5551）：Slack 触发的自动化会将中间进度消息发送到 Slack 频道，而非最终结果。用户期望收到的是完成摘要，但收到的是中间执行步骤。
- **认证故障恢复难**（#5882、#5878）：GitHub token 被吊销或 Slack 反复重连会导致认证流程进入不可恢复的损坏状态，用户需要重装扩展才能恢复。错误消息本身具有误导性。
- **Agent 行为不可控**（#6479、#6046）：用户对 agent 可能自我复制 routine 的风险表示担忧，同时也对简单任务（邮件→表格）需要 124 次工具调用感到不满。
- **UI 状态不一致**（#7345、#7349）：Agent 报告的数据与 UI 展示不一致，刷新后历史记录消失，这些都会对用户信任造成影响。

整体来看，用户对功能覆盖度满意，但对执行稳定性、错误可诊断性和 UI 一致性有更高期待。自动化回归修复的速度（如 #7402-#7404 当天提交）是加分项。

---

## 8. 待处理积压

### 长期未响应的关键 Issue

| Issue | 创建时间 | 内容 | 优先级建议 |
|---|---|---|---|
| [#6479](https://github.com/nearai/ironclaw/issues/6479) | 2026-07-22 | Routine 可创建/修改其他 routine，存在自我复制风险 | **高** — 涉及自动化安全边界，建议尽快规划 guardrail |
| [#6046](https://github.com/nearai/ironclaw/issues/6046) | 2026-07-13 | 简单邮件→表格任务触发 124 次工具调用 | **中** — 与 #7405 的工具发现优化相关，可能被该工作覆盖 |
| [#5551](https://github.com/nearai/ironclaw/issues/5551) | 2026-07-02 | Slack 自动化发送中间进度而非最终结果 | **中** — 影响用户对 Slack 集成的信任度 |
| [#5878](https://github.com/nearai/ironclaw/issues/5878) | 2026-07-09 | GitHub token 吊销后产生误导性错误消息 | **中高** — 错误可诊断性问题 |
| [#5882](https://github.com/nearai/ironclaw/issues/5882) | 2026-07-09 | Slack 反复重连导致认证流程损坏 | **中高** — 需要明确的恢复路径 |

### 待合并的重要 PR

| PR | 描述 | 风险等级 |
|---|---|---|
| [#7076](https://github.com/nearai/ironclaw/pull/7076) | 安装目录已发布但尚未安装的包（contributor: new，已 rebase） | 低 / XL |
| [#7020](https://github.com/nearai/ironclaw/pull/7020) | tokio-tungstenite 0.29→0.30 依赖升级 | 低 / M |
| [#7396](https://github.com/nearai/ironclaw/pull/7396) | Slack & Telegram 通用渐进式预览 | 低 / XL |

### 值得关注

[#7076](https://github.com/nearai/ironclaw/pull/7076) 由新贡献者 `neo-sky` 提交，已成功 rebase 至最新 main 分支，等待合并。这类来自新贡献者的 PR 值得维护者优先关注以促进社区生态发展。

---

*本日报由 AI 自动生成，数据截止 2026-08-10。所有链接指向 GitHub 上的原始 Issue/PR。*

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

# LobsterAI 项目动态日报 — 2026-08-10

*数据统计周期：2026-08-09 至 2026-08-10 | 数据来源：GitHub Issues / PR / Releases*


## 1. 今日速览

过去24小时内，LobsterAI 项目围绕多模型协作与切换机制出现了3条活跃 Issue，但无新 PR 合并、无新版本发布，整体处于**轻度活跃**状态。社区讨论的核心痛点集中在**多模型切换的校验逻辑误判**（#2453）和**跨模型子任务协作机制不完善**（#2132）两大方向。此外，一个三个月前提出的上下文窗口配置问题（#1187）因持续影响用户而被标记为 stale，但仍未得到解决。项目贡献节奏偏缓，社区问题反馈与维护响应之间存在一定时间差，值得关注。


## 2. 版本发布

过去24小时内无新版本发布。最近一次发布信息暂无更新。


## 3. 项目进展

过去24小时内无 PR 被合并或关闭，也没有新的 PR 提交。结合现有 Issue 的讨论情况，当前项目在**多模型切换与跨模型协作**方向的需求集中度较高，但对应的代码变更尚未进入 PR 阶段。此前已标记的 stale Issue（#1187、#2132）对应的修复工作未见新进展。整体而言，今日无实质性的代码推进，项目处于维护性沉默期。


## 4. 社区热点

**热点 Issue：#2453 — 切换自定义模型被系统误判为不许可**

- **链接：** [netease-youdao/LobsterAI Issue #2453](https://github.com/netease-youdao/LobsterAI/issues/2453)
- **创建时间：** 2026-08-09（24小时内新开）
- **热度指标：** 1 条评论，0 👍（虽数据不高，但问题逻辑性强、影响面广，评论区讨论密集）
- **核心内容：** 用户在切换自定义模型时，只要模型定义格式为 `custom_1/openai/gpt-oss-20b:free`（即包含斜杠的 provider/model 结构），系统就会误判 Provider 为 "openai" 并进行合法性校验，导致合法的免费模型被拒绝。该问题在**同一线程内切换模型**时反复触发，影响 OpenRouter 和 NVIDIA 平台上的免费模型。

**背后诉求分析：** 该问题暴露出系统中模型标识解析逻辑的脆弱性——将自定义模型别名中的斜杠误当作 provider 分隔符。用户报告的时间非常新（8月9日创建），说明这是一个**当前版本中高概率存在的回归或未覆盖边界场景**，且直接阻塞了使用 OpenRouter/NVIDIA 免费模型的用户群。这是近期最需要关注的问题之一。


## 5. Bug 与稳定性

| 严重程度 | Issue | 问题描述 | 当前状态 |
|---------|-------|---------|---------|
| 高 | [Issue #2453](https://github.com/netease-youdao/LobsterAI/issues/2453) | 自定义模型切换被误判为不合法，模型标识解析逻辑存在缺陷，影响所有包含斜杠的 provider/model 格式 | 新开，无 fix PR |
| 中 | [Issue #1187](https://github.com/netease-youdao/LobsterAI/issues/1187) | DeepSeek 模型上下文窗口溢出（`Context overflow`），系统缺少上下文窗口大小和输出 token 的配置入口 | 已 stale（2026-04-01 创建），1 👍 2 评论，无 fix PR |
| 中 | [Issue #2132](https://github.com/netease-youdao/LobsterAI/issues/2132) | 跨模型子任务协作机制不完善：子任务完成后结果无法同步主任务，网关级函数调用未被纳入 sessions 管理体系 | 已 stale（2026-06-09 创建），无 fix PR |

⚠️ 注意：#2453 为最紧急的新报告问题，直接影响用户日常使用；#1187 和 #2132 均为长期累积未修的痛点，目前均已过期（stale），存在被自动关闭的风险。


## 6. 功能请求与路线图信号

**本周主要功能请求信号：**

1. **[Issue #1187](https://github.com/netease-youdao/LobsterAI/issues/1187) — 增加上下文窗口大小设置与输出 token 配置**
   - 用户反馈在设置模型 API 时缺少上下文窗口和输出 token 的可配置项，导致 DeepSeek 等模型频繁因超长上下文报错。
   - **路线图判断：** 该请求源于实际使用阻塞，且属于设置面板的补全型功能，实现成本不高，**预计有较大概率在下一个迭代版本中纳入**。

2. **[Issue #2132](https://github.com/netease-youdao/LobsterAI/issues/2132) — 跨模型子任务协作机制增强**
   - 用户提出两项明确建议：①同模型子任务完成后主任务可第一时间获知（已有机制），可借鉴至跨模型场景；②子任务完成或遇卡点时主动向主任务发送通知。
   - **路线图判断：** 这是一个涉及架构层面的交互设计改动，影响面较大，短期内不太可能直接进入 PR 阶段，但**属于项目中期规划的重要方向信号**。

**综合信号：** 多模型协作与切换的体验优化明显是社区当前最强烈的声音，建议维护者在下一版本中将“模型标识解析修复”和“上下文窗口可配置化”作为优先项处理。


## 7. 用户反馈摘要

**核心用户痛点：**

- **多模型切换体验割裂（#2453）：** 用户报告在单线程内切换自定义模型时频繁被系统拦截，“在一个线程里面切换模型尤其打扰”，说明当前架构对多模型并行使用的支持并不流畅。用户明确表达了“这很影响使用”的负面情绪。
- **上下文管理能力不足（#1187）：** 用户在面对长对话时被迫使用 `/reset` 或 `/new` 清空会话，严重打断了工作流。评论中涉及 “Try /reset (or /new) to start a fresh session” 但缺乏更优雅的上下文管理方案，反映了对灵活配置的强烈渴望。
- **跨模型协作不透明（#2132）：** 用户详细检查了调用链，发现模型之间的状态同步存在盲区（网关级调用未被纳入 sessions 管理），担忧多模型协同工作的可靠性。

**使用场景画像：** 用户群多为技术型个人用户，使用场景涵盖本地开发调试（DeepSeek 本地模型）、依赖外部免费 API（OpenRouter/NVIDIA）的实验性应用，以及多模型拆分工件的复杂工作流。


## 8. 待处理积压

| 优先级 | Issue/PR | 创建时间 | 搁置时长 | 最后互动 | 建议 |
|--------|----------|---------|---------|---------|------|
| 🔴 高 | [Issue #1187](https://github.com/netease-youdao/LobsterAI/issues/1187) | 2026-04-01 | **131 天** | 2026-08-09（stale 标记） | 已过期，建议尽快回应或安排修复计划，否则将被自动关闭 |
| 🔴 高 | [Issue #2132](https://github.com/netease-youdao/LobsterAI/issues/2132) | 2026-06-09 | **62 天** | 2026-08-09（stale 标记） | 已过期，涉及架构级改进，建议至少给出官方回复说明是否纳入规划 |
| 🟡 中 | [Issue #2453](https://github.com/netease-youdao/LobsterAI/issues/2453) | 2026-08-09 | 1 天 | 2026-08-09 | 新问题但影响面大，建议尽快分配优先级 |

> ⚠️ 注意：两个 stale Issue（#1187 与 #2132）在今日均被自动更新了 stale 标记（更新时间 2026-08-09），意味着若不及时干预，它们将在下次 stale 检查时被关闭。建议维护者主动进行 triage，防止有效反馈丢失。


*本报告基于公开 GitHub 数据生成，仅供参考。项目动态以官方发布为准。*

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

# Moltis 项目动态日报

**日期：2026-08-10**  
**数据窗口：2026-08-09 至 2026-08-10（UTC）**


## 1. 今日速览

Moltis 项目在过去 24 小时内活跃度**中等偏低**。共新增/更新 2 个 Issue（均为 Bug 报告）和 1 个待合并 PR（修复 Vault 助记词哈希逻辑）。无新版本发布，无 PR 合入，项目主干推进速度平缓。值得关注的是，今日两个 Bug 分别涉及**配置持久化**（#1187）和**容器运行时状态检测**（#1185），均属于用户可感知的稳定性问题；同时 #1186 PR 虽小但直击密钥派生兼容性痛点，建议优先评审。整体而言，项目处于"低峰维护期"，社区反馈以质量改进为主，无重大功能迭代信号。


## 2. 版本发布

**无**（过去 24 小时无新 Release）。


## 3. 项目进展

**今日无 PR 合入或关闭**，无主干推进事件。

但有一条 **待合并 PR #1186** 值得关注：

| 项目 | 详情 |
|---|---|
| **PR** | [#1186 [OPEN] fix(vault): normalize recovery phrase before hashing](https://github.com/moltis-org/moltis/pull/1186) |
| **作者** | pxmpsdev |
| **摘要** | 修复 Vault 解锁时助记词大小写/连字符归一化不一致问题——`derive_recovery_kek` 在派生密钥前已对助记词做归一化（去除连字符、转大写），但**存储哈希时未做同样归一化**，导致用户用小写或带连字符的助记词解锁仓库时，KEK 派生成功但哈希比对失败。 |

该 PR 一旦合入，将**消除一个影响用户日常使用的隐蔽缺陷**（解锁失败且难排查），并对既有 `recovery_key_case_insensitive` 测试形成闭环。


## 4. 社区热点

今日**无**高讨论量 Issue/PR（两个 Issue 评论数均为 0，PR #1186 评论为 undefined）。社区整体静默，无热点议题。


## 5. Bug 与稳定性

今日报告 2 个 Bug，均**无关联 Fix PR**（待社区或维护者响应）。按严重程度排序如下：

| 严重度 | Issue | 描述 | 影响面 | Fix PR |
|---|---|---|---|---|
| 🔴 高 | [#1185](https://github.com/moltis-org/moltis/issues/1185) — Apple Container 1.x 沙箱已启动，但 Moltis 判定为"未运行" | 运行时状态检测误判，导致用户无法操作实际已运行的沙箱实例 | 直接影响 Apple Container 场景下所有依赖状态判断的功能（如 UI 状态栏、生命周期管理） | 无 |
| 🟡 中 | [#1187](https://github.com/moltis-org/moltis/issues/1187) — Heartbeat 设置 UI 静默重置表单未覆盖的字段 | 用户修改 UI 中可见字段保存后，表单未覆盖的配置项被静默清空，无提示 | 违反最小惊讶原则，可能造成配置静默丢失，影响心跳上报行为 | 无 |

**补充说明**：#1185 与 #1187 均在 preflight checklist 中确认使用最新版本，可排除"旧版本已修复"的可能性。


## 6. 功能请求与路线图信号

**今日无显式功能请求**（两个新 Issue 均为 Bug）。

**路线图信号（弱）** ：PR #1186 中涉及的"助记词大小写/连字符宽容处理"（`recovery_key_case_insensitive` 测试）暗示 Vault 团队正在推进**用户体验友好化**方向——即使通过 Bug 修复体现，也可能为未来"多格式助记词支持"铺路。建议维护者关注 Vault 模块后续迭代。


## 7. 用户反馈摘要

**今日无有效用户评论**（两个 Issue 评论数均为 0，PR #1186 评论为 undefined）。从 Issue 标题与摘要可提取以下间接信号：

| 来源 | 用户痛点/诉求 |
|---|---|
| #1185 | Apple 容器沙箱状态与 Moltis 内部状态不同步，导致用户无法对已运行实例进行操作。用户期望**状态检测与实际运行时保持一致**。 |
| #1187 | UI 保存后静默重置未展示字段，用户期望**对非表单字段的修改应有明确提示或保留原值**。 |


## 8. 待处理积压

**长期未响应重点追踪**（今日无新增优先级，以下为持续观察项）：

| 类别 | 条目 | 备注 |
|---|---|---|
| PR | [#1186 fix(vault): normalize recovery phrase before hashing](https://github.com/moltis-org/moltis/pull/1186) | 创建于 08-09，**至今无 Review 评论**。涉及加密/解锁核心路径，建议维护者尽快评审——该修复可一次性解决一类"解锁失败且报错不明确"的长期问题。 |
| Issue | [#1185 Apple Container 沙箱状态误判](https://github.com/moltis-org/moltis/issues/1185) | 创建于 08-08（已 2 天），无维护者回复。属高影响力 Bug，建议标记 `needs-triage`。 |


## 项目健康度评估

| 维度 | 状态 | 说明 |
|---|---|---|
| 🟢 发布节奏 | 稳定 | 无紧急补丁需求 |
| 🟡 响应速度 | 需关注 | #1185 已 2 天未获回应，#1186 PR 无 Review |
| 🟢 社区参与 | 平稳 | 有外部贡献者（pxmpsdev），说明项目仍有外部开发者参与 |
| 🟡 质量反馈 | 存在隐患 | 两个新 Bug 均涉及**用户可感知的状态/配置一致性**问题，建议在下一个版本前集中修复 |

**维护者行动建议（按优先级）** ：
1. Review 并合入 #1186（加密路径 bug，小改动高收益）
2. 对 #1185 标记 triage 并联系 Apple Container 相关 maintainer
3. 评估 #1187 的 UI 配置持久化机制，考虑增加"未保存字段变更"提示

---
*本报告由 AI 自动生成，数据来源：moltis-org/moltis GitHub 仓库。*

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

# CoPaw / QwenPaw 项目动态日报

**日期：2026-08-10**  
**数据来源：** github.com/agentscope-ai/CoPaw（仓库已归档，主开发迁移至 agentscope-ai/QwenPaw）  
**统计周期：** 2026-08-09 00:00 — 2026-08-10 00:00 (UTC)



## 一、今日速览

过去 24 小时项目活跃度较高，社区贡献与反馈双线并行：共产生 17 条 Issue 更新（新开 11 条，关闭 6 条）和 50 条 PR 更新（新增 49 条待合并 PR，仅 1 条被合并/关闭）。PR 积压规模较大（49 条待合并），但其中大量为 *first-time-contributor* 提交的新功能或修复，且已出现多位维护者参与代码审查（`Under Review` 标记）。值得关注的是，**多个 Issue 与 PR 直接对应**——例如 Gemini `$schema` 校验错误（#6812 → PR #6844）和审批描述缺失（#6832 → PR #6854），说明社区反馈已快速转化为修复方案，项目响应机制运转正常。ReMe 记忆系统成为当天讨论的焦点话题之一。整体来看，项目处于 2.1.0b2 迭代周期中，功能迭代与 Bug 修复同步推进，社区贡献活跃度处于健康水平。


## 二、版本发布

**无新版本发布。** 当前最新版本为 2.1.0b2（社区反馈多基于此版本）。


## 三、项目进展

今日无 PR 被合并（唯一关闭的 PR #6846 为新增 DeepSeek V4 模型上下文窗口数据的提交，状态为已合并/关闭），但社区提交了大量功能代码与修复补丁，主要集中在以下方向：

1. **Session Fork / 会话分叉与快照** — PR #6704（iluv7）实现会话右键分叉为全新独立会话并复制完整对话上下文，作为检查点式快照；PR #6750（lllyfff）修复会话身份失同步、早期保存及超长 prompt 折叠三个前端问题；PR #6845 修复聊天记录重载时助手消息完成时间丢失的问题。

2. **审批流程优化** — PR #6854 为审批请求添加上下文描述（对应 Issue #6832），用户在审批卡片中可直接看到用途说明而无需查看原始命令。

3. **多模型/多 Provider 兼容性增强（26 条相关 PR）** — PR #6809 针对 StepFun 等严格 OpenAI 兼容 Provider 清洗消息内容中的运行时段；PR #6844 移除 Gemini 工具 JSON Schema 中的 `$schema` 元数据字段。另有 PR #6846（已合并）为 DeepSeek V4 模型添加 100 万 token 上下文窗口支持。

4. **ReMe 记忆系统升级** — PR #6398 添加重排序（reranker）支持，通过外部重排序 API 对搜索候选进行精排；配合 Issue #6841、#6840 讨论的 ReMe4 路线图评估。

社区活跃度信号明确，Issue 关闭 6 条中至少 3 条为同一作者（lcq225）重复提交的渲染问题（#6848-#6851）。


## 四、社区热点（讨论活跃度最高的 Issues/PRs）

**1. Issue #2291（长期置顶贡献任务清单）— 评论 66 条，已关闭**  
🔗 [agentscope-ai/QwenPaw Issue #2291](https://github.com/agentscope-ai/QwenPaw/issues/2291)  
维护者发布的开放任务清单，按 P0-P2 优先级排列。今日已关闭，应由维护者完成清理和归档，过程中涉及大量社区认领和进度沟通。

**2. Issue #6281（移动端适配请求）— 5 条评论，持续开放**  
🔗 [agentscope-ai/QwenPaw Issue #6281](https://github.com/agentscope-ai/QwenPaw/issues/6281)  
用户期待 Web 控制台支持移动端操作。已开放近三周，尚未见相关 PR 响应。移动端诉求虽非核心功能，但持续有用户关注。

**3. Issue #6840（ReMe Light 路线图问题）— 1 条评论，刚刚开启（2.1.0b2 新版本关注点）**  
🔗 [agentscope-ai/QwenPaw Issue #6840](https://github.com/agentscope-ai/QwenPaw/issues/6840)  
用户在代码层面比对 ReMe4 架构与实际实现，询问 ReMe4 完整路线图时间表（Auto-Link、三模态搜索、四类摘要权重），体现深度用户对记忆系统演进方向的关注。

**4. PR #6804（微信审批中文回复功能）— 社区持续活跃（对应 Issue #6728）**  
🔗 [agentscope-ai/QwenPaw PR #6804](https://github.com/agentscope-ai/QwenPaw/pull/6804)  
为微信渠道审批增加中文「允许/拒绝」回复支持，精准解决中文用户的实际操作痛点，通过渠道层翻译为 `/approval approve|deny` 命令，契合目标用户群体使用习惯。


## 五、Bug 与稳定性

### 高严重度

| 严重度 | Issue | 描述 | 状态 |
|--------|-------|------|------|
| **高** | #6839 [Bug] | **MCP 工具调用时数字字符串被强制转为数字格式传参，导致 API 调用失败**（如 `apiKey` 被转为数字）。影响所有依赖 MCP 工具的用户，涉及核心调用链 | 🔴 开放，无 fix PR |
| **高** | #6812 [Bug] | **Gemini Provider 因 JSON Schema 包含 `$schema` 字段被 Google SDK 拒绝，Model 'unknown' 执行失败**。用户已给出完整诊断 | 🟢 **已有 fix PR #6844** |
| **高** | #6826 [Bug] | **助手消息完成时间显示异常**：实际思考 2 分钟，页面显示仅几秒，误导用户对响应性能的判断 | 🟢 **已有 fix PR #6845** |
| **中** | #6847 [Bug] | **QwenPaw 执行任务时被杀毒软件拦截甚至强制关停进程**（对比 WorkBuddy 不受影响），疑似代码行为触发安全软件误报 | 🔴 开放，待深入调查 |
| **中** | #6853 [Bug] | **prompts.py 文档与实现不一致**：声称 dream 进程自动同步摘要到 MEMORY.md，实际从未实现，误导下游 Agent 行为 | 🔴 开放，无 fix PR |
| **低** | #6841 [Bug] | Auto-Dream 中单个单元集成失败（LLM 返回空 schema）导致整个任务被标记为 error，建议增加重试与容错机制 | 🟡 开放，有讨论 |

### 低严重度 / 前端显示问题

| Issue | 描述 | 状态 |
|-------|------|------|
| #6848-#6851（4条同源重复提交）/#6852 | 前端渲染器将长多行工具输出折叠为不可读文本块（2.1.0b2, Windows 11） | 🟢 已关闭或讨论中 |


## 六、功能请求与路线图信号

| 功能请求 | 对应 Issue | 当前信号 |
|----------|-----------|----------|
| **审批用途描述**：AI 提交审批时附加一句话用途说明，用户无需查看代码即可判断是否通过 | [#6832](https://github.com/agentscope-ai/QwenPaw/issues/6832) | 🟢 **已有 PR #6854**，预计随下一版本推出 |
| **Web 控制台移动端适配** | [#6281](https://github.com/agentscope-ai/QwenPaw/issues/6281) | 🟡 开放 3 周无 PR 响应，尚未排期 |
| **ReMe 记忆系统完整路线图**：Auto-Link、三模态搜索、四类摘要权重 | [#6840](https://github.com/agentscope-ai/QwenPaw/issues/6840) | 🟡 2.1.0b2 已内置 ReMe Light，完整版规划待确认 |
| **子代理模型自动切换与共享 workspace** | [#6838](https://github.com/agentscope-ai/QwenPaw/issues/6838) | 🔴 开放，无明确排期；涉及核心架构调整 |
| **DeepSeek V4 模型上下文窗口支持** | — | 🟢 **已合并**（PR #6846），1M 上下文已录入静态目录 |


## 七、用户反馈摘要

**正面反馈：**
- **贡献者友好**：多位 first-time-contributor 提交的 PR（#6854、#6843、#6842 等）均获得维护者响应，被标记 `Under Review` 或得到可执行反馈，社区吸纳新贡献者的机制顺畅。
- **功能落地满意度高**：ReMe 记忆系统在 2.1.0b2 落地，用户认可功能方向，主动深入代码核对实现细节（#6840）。

**负面反馈 / 痛点：**
1. **前端时间显示失真**（#6826）：用户明确表达页面显示与实际情况不符，影响对助手效率的信任判断。
2. **MCP 类型转换 Bug**（#6839）：数字字符串被改为数字类型导致调用失败，说明 MCP 集成的健壮性仍有欠缺。
3. **与杀毒软件冲突**（#6847）：QwenPaw 被杀软强制关停，对比 WorkBuddy 不受影响，暴露了执行行为可能触发安全软件误判的问题。
4. **AI 审批不透明**（#6832）：用户需要理解 PowerShell 代码才能批准 AI 操作，门槛高，影响审批效率和安全性。


## 八、待处理积压

| 项目 | 类型 | 详情 | 待处理时长 |
|------|------|------|-----------|
| **#6281** — Web 控制台移动端适配 | Feature Request | 开放 21 天，零 PR 响应 | 🔴 超 3 周 |
| **#6838** — 子代理模型自动切换与共享 workspace | Bug/Enhancement | 涉及多 Agent 协作与 config 结构层修改，需架构层面评估 | 🟡 已开放 1 天，短期内难以解决 |
| **#6398** — ReMe 搜索重排序支持（后端） | PR | 8 月 9 日获得更新，功能涉及 ReMe 记忆搜索质量提升优先级需确认 | 🟡 已开放 17 天，`Under Review` 状态 |


*本报告基于 GitHub 公开数据自动生成，仅供参考。*

---

**报告生成时间：** 2026-08-10  
**统计口径：** github.com/agentscope-ai/CoPaw（自动跳转至 agentscope-ai/QwenPaw 仓库）  
**数据截止：** 2026-08-09 23:59 UTC

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

好的，我是你的 AI 智能体与个人 AI 助手领域开源项目分析师。根据 ZeroClaw 仓库在 2026-08-10 的实时数据，我为你生成了这份项目动态日报。

---

# ZeroClaw 开源项目动态日报
**数据统计周期：** 2026-08-09 ~ 2026-08-10
**数据来源：** github.com/zeroclaw-labs/zeroclaw

---

## 1. 今日速览

ZeroClaw 项目在 24 小时内保持极高活跃度，Issue 与 PR 更新均达到各 50 条，但呈现出"讨论热烈、落地缓慢"的阶段性特征。过去 24 小时内**无新版本发布，且无 PR 被合并/关闭**，大量 PR（50条）均处于待合并状态，且多数带有 `needs-author-action` 标签，表明项目维护者（Maintainer）的带宽或贡献者的跟进效率成为当前合并流程的主要瓶颈。社区讨论焦点高度集中在**安全加固（Webhook 鉴权、SSRF、密钥管理）、配置与运行时一致性**以及**流程治理（RFC 流程简化）**上，反映出项目在快速扩张后正进入强调稳健性和规范化治理的阶段。

---

## 2. 版本发布

**无新版本发布。** 上一个可用版本仍为 0.8.3，但已有多个 Issue 提及 0.8.4 的发布准备工作，例如 [#9690] 指出了阻断 0.8.4 发布的容器构建问题。

---

## 3. 项目进展

由于过去 24 小时内没有 PR 被合并（0 merged/closed），项目主干代码未发生实质性的向前推进。目前的进展主要体现在**高风险 PR 的密集提交与评审准备阶段**，尤其是集中在安全与架构领域，表明项目正在进行一轮深度的安全与稳定性加固。以下为当前处于待合并状态的关键 PR，它们代表着项目近期合并后将会带来的重要改进：

- **[PR #9744]:** 重构网关层，要求在进入 Agent 分发前强制进行 Webhook 鉴权，直接响应了多个安全相关的 P0/P1 Issue。
- **[PR #9720]:** 为 LLM 响应缓存增加请求边界限制，避免因 Hook 修改请求导致的缓存污染与逻辑错误。
- **[PR #9726]:** 将后台任务生命周期统一交由 `TaskRecord` 管理，旨在修复状态不一致和潜在的资源泄漏问题。
- **[PR #9713/PR #9745]:** 为知识图谱和会话工具增加基于 Agent 的所有权隔离，修复任意 Agent 可读写其他 Agent 数据的越权问题。

这些 PR 若成功合并，将显著提升项目在多租户场景下的安全性和数据隔离性。

---

## 4. 社区热点

今日社区讨论热度最高的议题集中在**治理流程**和**安全边界**上：

- **[Issue #6808] (评论: 21):** 这是一个关于"工作通道（Work Lanes）、看板自动化和标签清理"的 RFC。讨论热度最高，反映出社区对**当前项目治理和协作流程效率的不满**，以及对更清晰、自动化的工作流分配机制的渴望。它和一个维护者决策队列的衍生 Issue 一起，构成了社区对项目可持续运营的深层关切。
- **[Issue #7100] (评论: 11):** 关于“通过配置指定模型能力和上下文窗口长度”的 RFC。开发者对当前模型能力（特别是视觉支持）和上下文窗口硬编码或默认回退的不满，希望通过配置化的方式解决不同模型间的能力差异问题。
- **[Issue #9397] (评论: 10):** **安全热点**。关于将 WhatsApp Web 的 `allowed_groups` 空列表语义从"允许所有群"改为"拒绝所有群"（Fail-closed）的 RFC。这涉及到默认安全配置的基调和数据泄露风险，极易引发高关注度。

---

## 5. Bug 与稳定性 (按严重程度排序)

- **P0 - 严重安全风险：Webhook 未做鉴权**
  - **[Issue #9565]:** 报告了 WhatsApp Cloud、Linq、WATI 三个渠道的网关 Webhook 处理器在调用 Agent 前未验证调用者身份，构成严重的数据泄露/安全风险。当前所有关联修复 PR（如 #9744）均处于待合并状态，风险持续存在。

- **P1 - 高危缺陷：**
  - **[Issue #8519]:** `cargo-audit` 与 `cargo deny` 配置漂移，wasmtime-wasi 的 CVE 被忽略，存在供应链安全隐患。
  - **[Issue #8642]:** MCP工具Schema 的深度克隆导致 Agent 循环中内存无限增长（RSS 增长），存在 OOM 风险。
  - **[Issue #9284]:** 配置刷新（`flush_config`）可能被并发写入覆盖，存在配置丢失风险。
  - **[Issue #9690]:** 发布流程被阻断：容器构建（all-features）因 Rust 版本（1.95.0）低于项目声明的 MSRV（1.96.0？）而失败，该问题是在 v0.8.4 发布中被发现，虽然非严重回归但直接阻塞了版本发布。
  - **[Issue #9779]:** SOP 配置默认值未生效，导致 SOP 引擎在无任何报错的情况下静默失效，影响自动化工作流的执行。

- **P2 - 中危缺陷：**
  - **[Issue #9486]:** 高熵令牌检测器误将 Solana 钱包地址判定为敏感信息并进行脱敏，破坏了 Telegram 渠道的正常业务功能。
  - **[Issue #9085]:** 在启动时启用 PGVector 会导致嵌套运行时 panic，阻断核心功能启动。
  - **[Issue #9198]:** Discord 渠道在 daemon 重载后，输入状态指示器（typing indicator）卡死，影响用户体验。
  - **[Issue #8731]:** 基于 Stdio 的 MCP 服务器在退出后未妥善回收，导致僵尸进程累积，消耗系统资源。

**Bug 修复 PR 状态概览：** 尽管上述众多 Bug 均有对应的 PR 提交（例如 [#8826] 修复 SSRF、[#9707] 修复配置迁移、[#9197] 修复重启循环等），但所有 PR 均处于等待作者操作（`needs-author-action`）的待合并状态，**修复尚未进入主分支，风险持续存在**。

---

## 6. 功能请求与路线图信号

虽然无新版本发布，但从 Issue 和 PR 中可以清晰看出项目下一阶段的路线图：

- **安全框架重构（高优先级）：** 多个 PR（#9194, #8713, #8826）和 RFC（#6971, #9825）表明项目正在构建一套更完善的安全子系统，包括密钥来源抽象、SSRF 防御、以及针对公共区块链地址的发布安全例外，以适应更广泛的 Web3 和金融场景。
- **配置与运行时一致性：** 针对配置无法热更新（#7897）、模型能力配置化（#7100）、以及配置默认值生效等问题（#9779），项目正在优化配置的加载、分发和生效机制。
- **可观测性与测试门禁：** PR #9212 提议将回放回归测试套件作为 CI 硬性门禁并进一步扩展到 eval 系统，同时多个 Issue 提到需要更好的调试手段和日志。
- **多平台渠道支持深化：** 除了现有的 WhatsApp、Telegram、Discord、Matrix，新的 PR 正在为 Line 渠道增加 Webhook 插件接入（#8862），并完善 Matrix 的进度显示（#8443）和 Windows PowerShell 原生支持（#9182）。

---

## 7. 用户反馈摘要

- **对严格安全默认值的强烈需求：** 在 [#9397] 中，用户明确希望将 WhatsApp 空名单视为"拒绝所有"，体现了在安全与易用性权衡中，社区明显倒向**安全优先（Fail-closed）**的立场。
- **对敏感信息误判的挫败感：** 在 [#9486] 中，用户非常沮丧地发现 Solana 钱包地址被脱敏后无法在 Telegram 中发送，这直接破坏了业务工作流。用户期望智能的、基于上下文的脱敏规则，而非简单的熵值判断。
- **对项目迭代效率的担忧：** 大量评论表明社区对项目当前 RFC 讨论周期长、决策效率低、以及在多个 PR 上反复要求追加修改（`needs-author-action`）感到困惑和疲惫，这也可以从多个针对治理流程优化的 RFC（如 #9496, #6808）中获得印证。
- **对配置默认值的一致性质疑：** 用户（#9779）在配置 SOP 后没有收到任何错误或日志，却发现功能未生效，这暴露出项目在配置文档与运行时行为一致性上的不足。

---

## 8. 待处理积压

以下为长期处于待响应或阻塞状态的关键事项，需要维护者重点关注：

- **阻断发布的高危缺陷：**
  - **[Issue #9690]** (rustc 版本低于 MSRV) 和 **[Issue #8519]** (CVE 忽略)直接威胁到 v0.8.4 的发布进度和供应链安全，应作为最高优先级解决。
- **安全相关 P0/P1 积压：**
  - **[Issue #9565]** (Webhook 鉴权缺失) 和 **[Issue #9328]** (vi_verify 未验证凭证链)代表了严重的安全漏洞，当前修复 PR（如 #9744）卡在 `needs-author-action` 状态，强烈建议维护者主动介入加速评审流程。
- **技术债务与治理：**
  - **[Issue #6808]** (Work Lanes) 和 **[Issue #9496]** (简化 RFC 流程) 代表了社区内部对治理机制的集中诉求，需要维护者给予明确回应或指派负责人。
  - **[Issue #7130]** 请求在工作区范围内启用 `forbid(unsafe_code)`，并仅对 `aardvark-sys` 开放例外，是一项提升代码安全基础的重要技术债，但长期未获进展。
- **大量待合并的 PR：** 当前有 **50 个 PR 处于待合并状态**，其中绝大多数标记为 `needs-author-action`。这表明问题不在于维护者是否批准，而在于贡献者未能及时响应修改意见。建议项目组考虑发出贡献者沟通邀请，或对积压的 PR 进行集中清理，明确哪些是继续推进、哪些需要关闭，以避免社区贡献热情被消磨。

---
*本日报基于公开的 GitHub 数据自动分析生成，旨在提供客观的项目状态参考。*

</details>

---
*本日报由 [agents-radar](https://github.com/kky-wollu/agents-radar) 自动生成。*