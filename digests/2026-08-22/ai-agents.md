# OpenClaw 生态日报 2026-08-22

> Issues: 500 | PRs: 500 | 覆盖项目: 13 个 | 生成时间: 2026-08-21 22:29 UTC

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

# OpenClaw 项目动态日报 — 2026-08-22

> 数据来源：github.com/openclaw/openclaw | 覆盖周期：2026-08-21 00:00 – 2026-08-22 00:00（UTC）


## 1. 今日速览

OpenClaw 项目今日呈现**高活跃、高输出、零发布**的典型"合并冲刺前夜"状态。过去 24 小时内 Issues 与 PR 更新各达 500 条（触达 GitHub 单页上限），但新版本发布数为 0，且 PR 合并/关闭仅 100 条（占 20%），大量 PR 处于"待维护者审阅"或"等待作者回复"状态——这暗示团队当前更侧重于**修复方向的收敛与审阅**，而非新功能合并。值得关注的是，今日有多个长期悬而未决的 P1 级 PR（如 #127475 进程监督、#126085 网关停止异常）进入 "ready for maintainer look" 状态，项目正稳步逼近一次质量加固型的版本释放。


## 2. 版本发布

**无新版本发布。** 上一已知版本为 2026.7.1-2（据 Issue #124751 中用户环境信息推断）。考虑到 80% 的 PR 仍在等待合并或审阅，预计下一次版本释放将包含一批稳定性修复。


## 3. 项目进展

今日合并/关闭的 100 条 PR 中，以下 3 条具有代表性意义（均为今日关闭/合并，按影响面排序）：

| PR | 标题 | 状态 | 影响 |
|---|---|---|---|
| [#126424](https://github.com/openclaw/openclaw/pull/126424) | fix(gateway): keep conversation delivery within agent bindings | CLOSED | **跨渠道消息投递边界修复**。修复了多 Agent 场景下 conversation 工具可能将消息投递到错误 Agent 绑定的问题，影响 Discord/iMessage/Matrix/Mattermost/Slack/Telegram/Feishu 全部 7 个渠道，标记为 `merge-risk: 🚨 message-delivery`。关闭状态暗示已完成合并。 |
| [#125471](https://github.com/openclaw/openclaw/pull/125471) | fix(models): keep Claude CLI OAuth available in Control UI | CLOSED | **Claude CLI OAuth 修复**。解决了 Gateway 重启后 Claude CLI OAuth 刷新所有权丢失、Control UI 显示矛盾的 `anthropic: missing` 行的问题。标记 `merge-risk: 🚨 auth-provider`，为 P2 级但影响核心认证链路。 |
| [#123288](https://github.com/openclaw/openclaw/pull/123288) | fix(ui): show one session activity indicator | CLOSED | **Web UI 会话状态指示器修复**。消除"加载中"与"未读"双指示器并存造成的歧义，属体验打磨类 PR，附带视频证据。 |

**整体判断**：今日合并的 PR 集中在**消息投递正确性**、**认证链路稳定性**和**UI 状态一致性**三个方向。项目正在清理上一阶段（2026.7.x）遗留的渠道层回归问题，为下一版本铺路。


## 4. 社区热点

今日讨论热度最高的议题呈现"**多编码、多平台、多Agent编排**"三大主题：

| 议题 | 评论数 | 类型 | 热度信号 |
|---|---|---|---|
| [#48788](https://github.com/openclaw/openclaw/issues/48788) feat: centralized filename encoding utility | 19 | 功能提议 | 获得 19 条评论，**为今日最高**。核心诉求是为多编码（Shift-JIS、EUC-KR、GB18030 等）的 Content-Disposition 文件名处理建立**统一架构**，而非继续打补丁。 |
| [#53628](https://github.com/openclaw/openclaw/issues/53628) [Bug]: ${XDG_CONFIG_HOME} is not process when installing a skill | 14 | Bug | Docker 环境下 `XDG_CONFIG_HOME` 环境变量未被解析，导致 skill 安装路径错误。标注 `diamond lobster` 评级，社区关注度高。 |
| [#119796](https://github.com/openclaw/openclaw/issues/119796) [Bug]: Windows vitest teardown fails with EBUSY on agent state DB | 14 | Bug | Windows 下 SQLite 文件句柄未释放导致测试 teardown 失败，暴露了 Windows 平台上 agent 状态数据库的资源管理问题。 |
| [#42840](https://github.com/openclaw/openclaw/issues/42840) Feature: Add MathJax/LaTeX Support to Control UI | 8 | 功能提议 | 虽评论数仅排第四，但获得 **10 个 👍**（今日最高），社区对 Control UI 渲染数学公式的诉求强烈。 |

**社区诉求分析**：热度最高的编码统一提案（#48788）本质上反映了**非拉丁语系用户**（中文、日文、韩文）在 OpenClaw 多平台使用中持续遭遇的文件名乱码问题——这是一个跨 Feishu、Telegram、Discord 多个渠道的**系统性问题**，而非单一渠道缺陷。高赞的 MathJax/LaTeX 支持（#42840）则表明 **Control UI 正在被用于严肃的学术/科研场景**，用户已不满足于纯文本输出。


## 5. Bug 与稳定性

今日报告的 Bug 按严重程度排列如下（P1 为最高优先级）：

### P0 级（数据安全）

| Issue | 标题 | 状态 |
|---|---|---|
| [#119270](https://github.com/openclaw/openclaw/issues/119270) | **[P0]** file tools strip a leading @ from destination paths | 🔴 无 fix PR，需产品决策 |

文件工具会从目标路径剥离前导 `@` 符号，导致 `write`/`edit`/`apply_patch` 操作**写入并删除错误的文件**。当存在去 `@` 后的同名文件时，会造成**静默数据覆盖**。标注 `bulk-filed` 表明可能为批量提交的同类问题之一。

### P1 级（功能严重受损）

| Issue | 标题 | fix PR | 备注 |
|---|---|---|---|
| [#97616](https://github.com/openclaw/openclaw/issues/97616) | Leaks unreaped hook/tool child processes → zombie accumulation | ❌ 无 | 回归问题，长期运行后性能下降 |
| [#83598](https://github.com/openclaw/openclaw/issues/83598) | anthropic:claude-cli OAuth refresh still dead-ends in 2026.5.12 | ❌ 无 | **二次复发**，此前 #73682 的修复未完全解决问题 |
| [#86612](https://github.com/openclaw/openclaw/issues/86612) | Docker gateway container restart loop on Windows | ❌ 无 | `OPENCLAW_SANDBOX=1` 时触发 |
| [#84486](https://github.com/openclaw/openclaw/issues/84486) | Text before tool calls is lost in Feishu streaming card mode | ❌ 无 | 标记 `fix-shape-clear`，已有明确修复方向 |
| [#108215](https://github.com/openclaw/openclaw/issues/108215) | Context usage drops 57%→13% without compaction | ❌ 无 | 疑似上下文窗口管理逻辑缺陷 |
| [#126906](https://github.com/openclaw/openclaw/issues/126906) | Denying write tool silently disables memory persistence | ❌ 无 | **今日新开**，标记 `queueable-fix`，涉及记忆持久化完整性 |

### P2 级（功能受损但可绕行）

| Issue | 标题 | fix PR |
|---|---|---|
| [#120735](https://github.com/openclaw/openclaw/issues/120735) | Telegram inbound stickers arrive as raw file refs | ❌ 有 PR 关联 |
| [#43797](https://github.com/openclaw/openclaw/issues/43797) | Sandbox prune does not clean up workspace directory | ❌ 无 |
| [#50490](https://github.com/openclaw/openclaw/issues/50490) | Feishu 群聊 activation 模式切换无效 | ❌ 无 |
| [#87136](https://github.com/openclaw/openclaw/issues/87136) | Compaction absolute token thresholds break across models | ❌ 无 |
| [#50481](https://github.com/openclaw/openclaw/issues/50481) | Slack: no setSuggestedPrompts support | ❌ 无 |
| [#124751](https://github.com/openclaw/openclaw/issues/124751) | iOS app duplicates replies, no auto-scroll | ❌ 无 |
| [#58957](https://github.com/openclaw/openclaw/issues/58957) | Model switch fails silently with large context | ❌ 无 |
| [#87441](https://github.com/openclaw/openclaw/issues/87441) | memory thresholds parameter not wired to config | ❌ 无 |

**稳定性判断**：今日无 P0 级新增，但 P1 级积累量较大（7 个），且其中 **#83598（Claude CLI OAuth 二次复发）** 尤其值得关注——用户明确标注"despite #73682 fix"，说明此前的修复路径可能存在**架构性盲点**，而非简单的补丁遗漏。另外，P1 中 7 个问题仅 1 个有明确 fix PR 关联，修复覆盖率偏低。


## 6. 功能请求与路线图信号

结合今日活跃 Issues 与在途 PR，以下功能方向可能被纳入下一版本：

| 功能请求 | 热度 | 对应 PR / 信号 |
|---|---|---|
| **多编码文件名统一处理**（#48788） | 🔥🔥🔥 19 评论 | 无直接 PR，但社区讨论充分，注释中明确提到"proper architectural solution"，有产品决策标注 |
| **持久化自然语言规则学习**（#41366） | 🔥🔥 8 评论 | 涉及 `AGENTS.md` / `SOUL.md` 冲突，与今日 PR [#127469](https://github.com/openclaw/openclaw/pull/127469)（respect provenance in automatic context）方向一致 |
| **会话记忆 Hook 扩展**（#51572） | 🔥🔥 7 评论 | 要求 session-memory hook 在 reset/prune 时也触发，与 [#126906](https://github.com/openclaw/openclaw/issues/126906)（记忆持久化静默失败）形成互补 |
| **内置速率感知限流**（#45771） | 🔥🔥 7 评论 | 针对 Anthropic API 速率限制，适合自主 Agent 循环场景 |
| **Control UI MathJax/LaTeX**（#42840） | 🔥 10 👍 | 无对应 PR，但高赞数表明用户基础广泛 |
| **主题定制系统**（#28300） | 🔥 7 评论 | 6 套预设主题 + 自定义主题工作室，UI 方向 |
| **优雅网关重启与会话恢复**（#57425） | 🔥 6 评论 | 与 PR [#124953](https://github.com/openclaw/openclaw/pull/124953)（record interrupted trajectory ending）目标一致，后者已在审阅中 |

**路线图信号**：今日 PR 列表中有一个值得注意的集中方向——**记忆与身份体系的企业级增强**。包括：
- [#124643](https://github.com/openclaw/openclaw/pull/124643)（enterprise identity operations，XL 级，涉及 Entra/Google Workspace/Okta）
- [#127469](https://github.com/openclaw/openclaw/pull/127469)（memory provenance respect）
- [#126082](https://github.com/openclaw/openclaw/pull/126082)（owner-native lifecycle receipts）

这三个 PR 合计涉及 5 个扩展模块，暗示 OpenClaw 正在向**企业级记忆与权限治理**方向演进，这可能是下一大版本的核心主题。


## 7. 用户反馈摘要

### 真实用户痛点

1. **"修复未真正生效"的挫败感**
   - #83598（Claude CLI OAuth 二次复发）：用户明确写到 *"in `2026.5.12` on macOS, `anthropic:claude-cli` OAuth refresh still doesn't reach the runtime path even after the #73682 / `1824ceba54` fix"* —— 修复承诺未兑现会重创用户信任。
   - #58957（模型切换静默失败）：*"There is no clear error message... users cannot tell whether the problem is caused by..."* —— 用户对静默失败普遍不满，期望系统提供显式诊断。

2. **文档/日志与实际行为不一致**
   - #60612（Doctor 警告 NVM node 无法修复）：用户尝试手动修改 launchd plist，但 *"OpenClaw regenerates the launchd plist file on each restart"* —— 系统覆盖用户手动配置，属于**对抗性行为**。
   - #9607（Himalaya skill 文档缺失）：邮件格式化哲学未定义、HTML 邮件参考缺失，导致用户无法正确使用技能。

3. **跨平台痛点集中**
   - Windows：测试 teardown EBUSY（#119796）、Docker 重启循环（#86612）、沙箱清理不彻底（#43797）。
   - macOS：LaunchAgent 路径固定死（#52184），用户希望使用 Volta shim 而非版本固定路径。
   - iOS：消息重复、无自动滚动（#124751）。

4. **安全/数据完整性担忧**
   - #126906（今日新开）：*"Denying a tool via `tools.deny` can disable memory persistence, and nothing tells anyone"* —— 安全配置导致的数据静默丢失，用户标注为 P1。
   - #119270（P0 文件路径 @ 剥离）：静默写错文件，可能造成数据覆盖。

### 积极信号

- #42840（MathJax）的 10 个 👍 表明用户对产品有**超出预期的使用深度**——将 AI 助手用于学术内容产出。
- #48788 的 19 条评论展示出社区**愿意参与架构讨论**的意愿，用户在提出具体方案而非简单抱怨。
- #127660（cloud sessions retry）与 #127658（Control UI 可用性）等 PR 表明维护者在积极响应用户反馈。


## 8. 待处理积压

### 长期未响应的关键 Issue

| Issue | 创建时间 | 已存在 | 严重度 | 说明 |
|---|---|---|---|---|
| [#42803](https://github.com/openclaw/openclaw/issues/42803) | 2026-03-11 | **164 天** | P1 | Feishu 文本命令（/stop, /new, /status）在 Agent 活跃时不再立即执行，被排队。为 3.8 版本回归，用户已明确标注，且存在 open PR 关联——但 5 个月仍未合并。 |
| [#44502](https://github.com/openclaw/openclaw/issues/44502) | 2026-03-13 | **162 天** | P2 | Discord 路由/提及门控回归，影响消息投递正确性。 |
| [#97616](https://github.com/openclaw/openclaw/issues/97616) | 2026-06-29 | **54 天** | P1 | 子进程泄漏/僵尸进程累积导致运行时性能退化，目前无 fix PR。 |
| [#58957](https://github.com/openclaw/openclaw/issues/58957) | 2026-04-01 | **143 天** | P2 | 模型切换时上下文过大导致静默失败，无错误提示。 |

### 等待过久的 PR

| PR | 创建时间 | 已存在 | 标签 |
|---|---|---|---|
| [#117712](https://github.com/openclaw/openclaw/pull/117712)（dependabot actions 升级） | 2026-08-02 | 20 天 | `⏳ waiting on author` |
| [#118516](https://github.com/openclaw/openclaw/pull/118516)（extension security alignment） | 2026-08-03 | 19 天 | XL 级，`⏳ waiting on author` |

### 提醒关注

- **#42803 已积压 164 天**——这是 Feishu 渠道核心交互（/stop 无法及时停止 Agent）的回归，社区用户明确表达不满（2 个 👍），且已有对应 open PR，建议维护者优先处理。
- **#97616（僵尸进程）** 是 P1 级问题但无任何 fix PR 关联，54 天未解决，长期运行场景下可能造成内存/句柄耗尽。
- **#83598（Claude CLI OAuth 二次复发）** 今日获得 6 条评论和 2 个 👍，"despite #73682 fix"的措辞暗示用户对修复质量已有疑虑，建议在下一版本中作为必修复项验证。


## 总结

OpenClaw 项目正处于**高活跃度的稳定迭代期**：社区讨论活跃（编码统一、MathJax 支持等话题），修复方向清晰（消息投递、认证链路、UI 一致性），同时有一批 P1 级问题在库中待处理。值得警惕的信号是**部分 P1 问题积压时间过长（如 #42803 达 164 天）**，以及 **P1 级 Bug 的 fix PR 覆盖率不足 15%**（7 个 P1 中仅 1 个有关联 PR）。下一个版本释放若能在合并上述 PR 的同时覆盖 P1 修复，将显著改善项目健康度。

---

## 横向生态对比

# 个人 AI 助手开源生态横向对比分析报告

**日期：2026-08-22** | **分析视角：AI 智能体与个人 AI 助手开源生态** | **核心参照：OpenClaw**


## 一、生态全景

当前个人 AI 助手开源生态已进入**多极竞争、功能趋同、平台化演进**的成熟阶段。以 OpenClaw 为代表的成熟项目（500/500 条日更新、触达 GitHub 单页上限）正在向企业级记忆治理与权限体系纵深演进，而 NanoBot、NanoClaw、CoPaw 等中坚力量则在多通道集成（Mattermost、Dial、WhatsApp、Matrix）与稳定性加固之间并行推进。生态整体呈现**三层分化格局**——头部项目追求企业级能力（身份治理、记忆隔离、审计合规），腰部项目加速功能覆盖与渠道扩张，尾部小型项目（NullClaw、TinyClaw、ZeptoClaw）则依托架构红利以极低成本持续扩展供应商接入。跨项目对比显示，稳定性修复、LLM 供应商兼容、多编码/多语言支持是当日共同攻坚的技术焦点。


## 二、各项目活跃度对比

| 项目 | Issues 更新 | PR 更新 | PR 合并/关闭 | 新版本 | 健康度评分 | 阶段判断 |
|---|---|---|---|---|---|---|
| **OpenClaw** | 500（触顶） | 500（触顶） | 100（20%） | ❌ | ★★★★☆ | 合并冲刺前夜，P1 积压较多 |
| **Hermes Agent** | 50 | 50 | 8（16%） | ✅ v0.20.5（8/19） | ★★★☆☆ | 版本刚发布，社区反馈密集 |
| **ZeroClaw** | 50 | 50 | 2（4%） | ❌ | ★★☆☆☆ | 高产出低合并，XL 级 PR 拥堵 |
| **NanoClaw** | 1 | 25 | 11（44%） | ❌ | ★★★★☆ | 高强度迭代，多通道扩张 |
| **IronClaw** | 20 | 35 | 17（49%） | ❌ | ★★★★☆ | CI 重构 + 安全加固并行 |
| **LobsterAI** | 2（stale 关闭） | 13 | 12（92%） | ❌（v2026.8.21 合并） | ★★★★☆ | 发布后回归合并，节奏稳健 |
| **CoPaw** | 70（Issue+PR 合计） | — | 15 | ✅ v2.1.1b2（PR 合入） | ★★★☆☆ | 密集迭代，Bug 修复待合并 |
| **Moltis** | 2 | 8 | 1（关闭非合并） | ❌ | ★★★☆☆ | 多发 PR + 收敛 Bug，良性迭代 |
| **PicoClaw** | 1 | 4（集中清理） | 4 | ❌ | ★★★☆☆ | 积压 6 个月后集中清理 |
| **NanoBot** | 5 | 37 | 23（62%） | ❌ | ★★★★☆ | 快速迭代，Bug 闭环率高 |
| **NullClaw** | 0 | 1 | 0 | ❌ | ★★★☆☆ | 稳定观望，供应商扩展中 |
| **TinyClaw / ZeptoClaw** | 0 | 0 | 0 | ❌ | — | 无活动 |


## 三、OpenClaw 在生态中的定位

**OpenClaw 是生态的绝对头部与事实标准参照**，其优势体现在三个维度：

- **规模优势**：单日 Issues/PR 更新总量（1000 条）是第二梯队（Hermes、ZeroClaw 各 100 条）的 10 倍，社区参与广度无可匹敌。
- **治理深度**：已具备 P0/P1/P2 分级 Bug 管理体系、`merge-risk` 标注、`diamond lobster` 评级等精细化质量管控手段，是唯一建立**完整风险分级与修复追踪机制**的项目。
- **企业级演进**：当日 3 个 PR 合计涉及 5 个扩展模块（Entra/Google Workspace/Okta 身份操作、记忆来源追踪、生命周期回执），指向**企业级记忆与权限治理**方向，这是其他项目尚未系统性布局的领域。

**差异化短板**：合并效率偏低（当日仅 20%），且 P1 级 Bug 的 fix PR 覆盖率不足 15%，部分关键 Issue（如 #42803 Feishu 命令回归）已积压 164 天，治理体系的响应速度已开始滞后于社区预期。


## 四、共同关注的技术方向

| 技术方向 | 涉及项目 | 具体诉求 |
|---|---|---|
| **LLM 供应商兼容性** | NullClaw（Eden AI 接入）、PicoClaw（Anthropic 原生 API）、Hermes Agent（Anthropic cache_control 400）、ZeroClaw（Anthropic 预算 $0.00）、IronClaw（Claude CLI 凭据中介）、NanoClaw（Claude Code 升级） | 多供应商统一接入、Anthropic 兼容性反复出 Bug、预算/用量透明化 |
| **调度与定时任务可靠性** | Moltis（active_hours 失效）、ZeroClaw（cron 跨代理隔离）、Hermes Agent（cron 告警缺失）、LobsterAI（定时任务排序）、OpenClaw（调度器重构） | 配置语义一致性、代理级隔离、失败可观测性 |
| **多编码 / 多语言支持** | OpenClaw（#48788 编码统一）、CoPaw（中文文件名乱码）、LobsterAI（i18n 硬编码）、Moltis（繁体中文修订）、ZeroClaw（Lark 常量时间比较） | 非拉丁语系用户文件处理、i18n 规范执行、跨渠道文件名一致性 |
| **Windows / macOS 跨平台稳定性** | Hermes Agent（Windows 包重建）、IronClaw（WSL 修复）、NanoClaw（Matrix ESM 修复）、Moltis（Windows cmd.exe）、OpenClaw（Windows vitest EBUSY）、ZeroClaw（hardware 编译失败） | 文件句柄释放、shell 兼容、安装与更新流程可靠性 |
| **Agent 过程可观测性** | Hermes Agent（回合级可观测性 PR）、NanoBot（回合可观测性 PR）、ZeroClaw（SOP 运行日志）、CoPaw（工具调用过程显示）、IronClaw（TTFT 超时策略） | 推理过程透明化、用量统计、失败原因显式化 |
| **记忆系统加固** | OpenClaw（记忆持久化静默失败）、CoPaw（记忆搜索错乱）、IronClaw（可插拔内存架构）、NanoBot（Dream 游标修复）、Hermes Agent（state.db 损坏） | 记忆持久性、隔离性、跨会话一致性和防损坏能力 |


## 五、差异化定位分析

| 项目 | 功能侧重 | 目标用户 | 核心架构特征 |
|---|---|---|---|
| **OpenClaw** | 全渠道消息 Agent、企业级记忆/身份治理 | 重度个人用户、企业部署 | 多渠道网关 + 统一消息投递 + 企业身份集成 |
| **Hermes Agent** | 桌面优先 + Fleet 多设备管理 | 个人开发者、技术爱好者 | CLI + 桌面客户端 + Gateway，强调更新可靠性 |
| **NanoClaw** | 多通道快速扩张（Chat SDK 模式） | 团队协作、社区运营者 | `registerChannelAdapter` 标准化通道注册、Telegram 多实例 |
| **IronClaw** | Rust 高性能 + 沙箱安全 | 安全敏感型部署、开发者 | Rust 实现、Railway 代理 + 沙箱凭据中介、CI 体系重构建 |
| **NanoBot** | 轻量级聊天助手、工具调用 | 个人轻量用户、Slack 用户 | 稳定的 Slack/钉钉集成 + 轻量 TUI、Cron/Dream 功能 |
| **CoPaw** | 中文生态、桌面应用 + Hub | 中文用户、桌面端重度用户 | 桌面 WebView2 + 自托管 QwenPaw Hub、本地产物管理 |
| **ZeroClaw** | 多代理编排 + SOP 自动化 | 企业自动化运维、多代理场景 | 逻辑通道、SOP 流程自动化、ZeroRelay 安全传输（开发中） |
| **Moltis** | 插件化 + 连接器（WhatsApp 优先） | 轻度个人用户、插件开发者 | WhatsApp/浏览器自动化、插件系统（Windows 支持待合入） |
| **PicoClaw** | 嵌入式/轻量级 Agent 运行时 | 轻量部署、嵌入式场景 | 小体积、Go 实现、静默稳定迭代 |
| **NullClaw** | OpenAI 兼容网关聚合 | 多供应商模型调用者 | OpenAiCompatibleProvider 统一路由，零成本扩展新供应商 |
| **LobsterAI** | 本地产物管理 + DSH 实验运行时 | 内容创作者、知识管理用户 | 资料库/本地文件管理、DeepSeek Harness 实验性运行时 |


## 六、社区热度与成熟度

### 第一梯队：快速迭代期（活跃度高、合并速度快、功能推进密集）
| 项目 | 关键指标 | 阶段特征 |
|---|---|---|
| **NanoBot** | 37 条 PR/日，62% 合并率 | 迭代速度最快，Bug 闭环率高，功能与修复并进 |
| **IronClaw** | 35 条 PR/日，49% 合并率 | 安全加固 + CI 重构双线推进，响应迅速（24h 内闭环） |
| **NanoClaw** | 25 条 PR/日，44% 合并率 | 多通道扩张，核心团队极活跃，但依赖合并顺序管理有摩擦 |

### 第二梯队：质量巩固期（高产出，但合并节奏偏保守）
| 项目 | 关键指标 | 阶段特征 |
|---|---|---|
| **OpenClaw** | 1000 条更新/日，20% 合并率 | 高产出、审慎合并，正在为版本释放做质量收敛 |
| **Hermes Agent** | 100 条更新/日，16% 合并率 | 刚发布 v0.20.5（累积 323 个 PR），进入社区验证期 |
| **CoPaw** | 70 条更新/日，15 条合并 | 新版本已就绪（v2.1.1b2），集中修复 Bug 中 |

### 第三梯队：平稳积累期（低活跃度、等待关键节点）
| 项目 | 关键指标 | 阶段特征 |
|---|---|---|
| **LobsterAI** | 13 条 PR，92% 合并率 | 发布后回归合并阶段，合并效率最高 |
| **Moltis** | 8 条 PR，均待合并 | 代码活跃但合并停滞，需推动在途 PR |
| **ZeroClaw** | 50/50 更新，仅 2 合并 | 高产出低合并，安全审查与 XL 级 PR 排队长 |

### 第四梯队：观望期（低活跃度）
| 项目 | 阶段特征 |
|---|---|
| **PicoClaw** | 积压 6 个月 PR 今日集中清理，维护者进行大扫除 |
| **NullClaw** | 标准化供应商接入，等待维护者快速 review |
| **TinyClaw / ZeptoClaw** | 无活动，项目可能处于停滞或维护休眠状态 |


## 七、值得关注的趋势信号

### 1. 企业级能力成为头部项目的分水岭
OpenClaw 向企业级记忆与身份治理演进（Entra/Google Workspace/Okta、memory provenance、lifecycle receipts），IronClaw 强化沙箱凭据管理与审计日志，ZeroClaw 布局 SOP 自动化与逻辑通道。**个人助手从"单机工具"向"企业级基础设施"演进已成定局**，多代理隔离、审计合规、权限治理是下一阶段竞争焦点。

### 2. "回合级可观测性"是用户公认的体验缺口
Hermes Agent、NanoBot、CoPaw、IronClaw 四项目同日出现与"推理过程透明化、回合级用量统计、失败原因显式化"相关的 PR 或 Issue，共识强烈。**用户不再满足于"黑箱"输出**，期望像商业 SaaS 产品一样理解 AI 的"思考"过程和成本消耗。

### 3. LLM 供应商兼容性是反复出现的"隐形炸弹"
Anthropic 相关兼容性问题在 OpenClaw（Claude CLI OAuth 二次复发）、Hermes Agent（cache_control 400）、ZeroClaw（预算 $0.00）三项目同日暴露。**API 兼容层的稳定性直接决定用户信任度**，修复"未真正生效"的挫败感已多次出现在用户反馈中，是生态性风险。

### 4. 非拉丁语系用户需求正在形成规模化声量
OpenClaw 编码统一提案获 19 条评论（当日最高）、CoPaw 中文文件名乱码、LobsterAI i18n 硬编码、Moltis 繁体中文修订——**中文/日文/韩文用户在多平台使用中的痛点已跨项目趋同**，"统一编码架构"与"严格 i18n 规范"应成为各项目的基础设施级优先项。

### 5. 安全默认值正在从"可选"走向"强制"
IronClaw 沙箱凭据中介、Moltis 浏览器隐身模式默认开启 + 镜像请求校验、NanoClaw WhatsApp 下载安全校验、ZeroClaw 凭据片段脱敏——**安全能力正在从"高级配置"变为"默认行为"**，且逐步向供应链（镜像、依赖、凭据物化）延伸。

### 6. Windows 平台支持正在被重新审视
Moltis 的 Windows cmd.exe 修复 PR 积压 152 天后重新活跃，Hermes Agent 推进 Windows 事务性包重建，NanoClaw 修复 Node 22 的 Windows 兼容性，ZeroClaw 修复 aarch64 编译失败——**各项目开始意识到 Windows 用户占比远高于预期**，跨平台一致性将成为差异化竞争点。

### 7. CI/测试基础设施正在成为项目健康度的核心瓶颈
ZeroClaw CI 超时导致 fork PR 无法通过、IronClaw 发起系统的 CI T1-T4 重构、NanoClaw CI required check 失效导致主分支阻塞、OpenClaw 多次出现测试基础设施相关的合并阻塞——**CI 稳定性直接决定项目的合并吞吐与社区贡献者体验**，值得各项目优先投资。


**结论**：个人 AI 助手开源生态正处于从"功能竞赛"向"质量与治理竞赛"转型的关键节点。头部项目（OpenClaw）已验证市场空间，腰部项目（NanoBot、IronClaw、NanoClaw）正在加速追赶，尾部项目则在寻找细分切入点。对于技术决策者而言，选择哪个项目作为基础取决于对**渠道覆盖、安全合规、企业治理、社区响应速度**四大维度的优先级判断；对于开发者而言，"回合级可观测性、多编码统一、供应商兼容层、Windows 支持"将成为下一阶段最有价值的贡献方向。

---

## 同赛道项目详细报告

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

好的，作为 AI 智能体与个人 AI 助手领域开源项目分析师，这是基于 NanoBot (github.com/HKUDS/nanobot) 在 2026-08-22 的 GitHub 数据生成的项目动态日报。

---

# NanoBot 项目动态日报 — 2026-08-22

## 1. 今日速览

NanoBot 项目今日活跃度极高，尤其在 Pull Request (PR) 方面，全天共产生 37 条 PR 动态，其中 23 条已合并/关闭，展现出强劲的开发迭代速度。合并的 PR 重点覆盖了稳定性修复（如 Cron 任务、Dream 功能、Slack 下载安全）、新功能（如 DeepSeek V4 Flash Vision 支持、TUI 中 LaTeX 渲染）以及代码重构。Issues 方面，共 5 条更新，其中 4 条已关闭，Bug 修复闭环率较高。今日无新版本发布，但大量修复和新功能的合并且即将进入测试阶段，可能意味着新版本发布已临近。

## 2. 版本发布

**无**。今日无新版本 Release 发布。近期合并的 PR 积累了大量改进，预计未来几天内可能会有新版本（如 v0.x.y）发布。

## 3. 项目进展

今日合并/关闭的 PR 展示了项目在多个维度的扎实进展，主要体现在以下几个方面：

- **修复关键 Bug (稳定性与正确性)**：
    - **[PR #5407]** - `fix(cron)`: 修复了禁用 `heartbeat` 或 `dream` 功能后，持久化的系统任务仍在后台运行并消耗 Tokens 的问题，避免了用户的资源浪费。
    - **[PR #5442]** - `fix(dream)`: 修复了 #5441 中提到的 Dream 功能在工具错误恢复后仍被判定为失败，导致内存游标无法推进、历史批次被重复处理的问题。该 PR 直接解决了用户报告的核心痛点。
    - **[PR #5414]** - `fix(slack)`: 强化了 Slack 文件下载的安全校验，确保在重定向后仍能安全下载文件，修复了潜在的安全漏洞。
    - **[PR #5477]** - `fix(webui)`: 修复了 iOS PWA（渐进式 Web 应用）模式下控制按钮可能被刘海屏等区域遮挡的问题，提升了移动端用户体验。

- **推出新功能 (能力增强)**：
    - **[PR #5474]** - `feat(providers)`: 新增了对 DeepSeek V4 Flash Vision 实验性模型的支持，扩展了多模态能力。
    - **[PR #5476]** - `feat(tui)`: 为 TUI（终端用户界面）增加了 LaTeX 数学公式的 Unicode 渲染，让用户在终端中也能阅读公式，提升了可用性。
    - **[PR #5478]/[PR #5479]** - `refactor(providers)` / `feat(trajectory)`: 这是一组重构，为供应商用量定义了类型化契约，并尝试性地添加了统一的后端记录，为后续更精准的用量统计和轨迹追踪奠定了基础。

- **技术债务清理**：
    - **[PR #5475]** - `refactor`: 清理了大量未使用的死代码，并移除了不再需要的依赖，有助于降低维护成本和潜在的依赖风险。

## 4. 社区热点

今日最受关注的事件集中在 Issue #5198 和 PR #5420。

1.  **Issue #5198: 会话内无法切换模型**
    - **链接**: [HKUDS/nanobot Issue #5198](https://github.com/HKUDS/nanobot/issues/5198)
    - **热度**: 评论数最多（4条），日期跨度长（从7月31日讨论至今），虽然已关闭，但反映了用户对核心交互体验的持续关注。
    - **诉求分析**: 用户期望像使用商业 SaaS 产品一样，能够在聊天界面中快速切换模型（例如通过点按输入框旁的模型标签），而不仅仅是依赖 `/model` 命令，且该命令似乎还存在问题。这表明用户对灵活选择模型的体验有着较高的期望。

2.  **PR #5420: 回合级可观测性与安全恢复**
    - **链接**: [HKUDS/nanobot PR #5420](https://github.com/HKUDS/nanobot/pull/5420)
    - **状态**: 仍处于开启状态，且有 `[conflict]` 标签，需要解决代码冲突。
    - **焦点分析**: 该 PR 旨在将复杂的多轮工具调用、推理过程整合到一个统一的“回答”界面中，并提供用量统计。虽然尚未合并，但它的出现说明开发者和用户都在关注 Agent 工作流的**透明度和可理解性**，期望能更好地理解 AI 的“思考”过程和成本消耗。

## 5. Bug 与稳定性

今日报告的 Bug 数量较少（4个已关闭），但聚焦于一些深层次问题，均已有对应的 Fix PR。

- **高严重度**:
    - **[Issue #5441]** - `Dream` 进程因工具错误被迫中止，且无法推进记忆游标，导致后续 Drea 任务重复处理并复制编辑内容。已由 [PR #5442](https://github.com/HKUDS/nanobot/pull/5442) 修复。
- **中严重度**:
    - **[Issue #5454]** - 流式输出中，若中途发生 `server_error`，重试逻辑不会执行，即使之前已流式输出部分内容。这在长输出场景下会导致体验中断，需要用户重新生成。暂无直接关联的 Fix PR。
    - **[Issue #5463]** - DingTalk 通道存在后台任务泄漏隐患，任务生命周期缺乏终端观察者。这是一个潜在的内存泄漏和稳定性问题。暂无直接关联的 Fix PR。
- **低严重度（体验）**:
    - **[Issue #1168]** - 连接 Notion MCP 失败，用户反馈核查 API 无误仍连不上。该问题持续了较长时间后于今日关闭，但摘要中未见解决方案，可能属于外部服务兼容性问题。

## 6. 功能请求与路线图信号

- **`disable-model-invocation: true` 技能模式 (PR #5405)**: 该需求非常明确，即支持用户手动触发技能（如部署、发布），而不允许模型自动调用。这反映了用户对 Agent 安全控制和操作权限的精细化管理诉求，很符合 AI 助手在真实工作流中的落地场景，**极有可能被纳入下一个版本**。
- **元搜索提供商 (PR #5234)**: 通过 `mst-python` 聚合多个搜索引擎结果，提供更全面的信息检索。这是一个明确的功能增强，虽然今日更新，但可能因设计较为复杂需要更多评审。
- **统一供应商用量后端 (PR #5479)**: 尽管该 PR 被关闭（可能是被 #5481 取代），但结合 Issue #5198 中用户对模型选择的关注，以及对成本透明的普遍需求，**用量统计追踪功能**已成为一个明显的路线图信号。

## 7. 用户反馈摘要

- **痛点明确**: 用户在配置和使用 MCP（如 Notion）时遇到困难，反馈“核查了好几次API，没看出来有什么问题，但就是连不上”，这指出了当前工具在 MCP 连接层面的诊断能力不足。
- **体验期望明确**: 用户希望模型切换能像“Cloud SaaS AIs”一样直观，否定只在配置层面修改模型的方式。
- **对“伪失败”的困惑**: 用户在 #5441 中描述，即使AI已经成功修改了内存，也会因为过程中的错误被误判为未完成，这会让用户觉得AI“犯傻”，显示了对于Agent过程容错性的高要求。

## 8. 待处理积压

- **[PR #5420]** - `feat(webui): 增加回合可观测性和安全恢复`。该 PR 带有 `[conflict]` 标签，需要解决冲突。它承诺的功能（项目制回合视图、用量累计）对提升复杂 Agent 任务的透明度至关重要，建议维护者尽快处理冲突，推动该项目前进。
- **[Issue #1168]** - `连接 Notion MCP失败`。今日虽已关闭，但缺少明确的解决方案说明。如果用户问题确实未解决，这是项目在外围生态（MCP）兼容性上的一个隐患，值得维护者跟进核查。
- **[PR #5234]** - `feat(agent): 集成 mst-python 元搜索提供商`。作为一项新功能，其更新跨度较长，若功能设计合理，长期搁置可能导致功能过期或社区贡献者流失。建议维护者评估其优先级。

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

好的，这是为您生成的 Hermes Agent 项目动态日报：

---

## Hermes Agent 项目动态日报 — 2026-08-22

### 1. 今日速览

过去24小时，Hermes Agent 项目保持极高的社区活跃度，共产生50条 Issue 更新和50条 PR 更新。Issue 关闭率（12%）和 PR 合并率（16%）相对较低，表明社区在积极反馈问题并提交修复方案，但维护者在合并和关闭操作上存在一定积压。项目于昨日发布了 `v0.20.5` 补丁版本，将大量已合并的 PR 固化为稳定版本，但社区仍报告了若干高优先级（P0/P1）问题，尤其是在 Anthropic API 兼容性和多进程状态数据库（state.db）损坏方面，需要维护者重点关注。

### 2. 版本发布

**v2026.8.19 (v0.20.5)**
- **发布日期：** 2026年8月19日
- **性质：** 补丁版本（Patch Release）
- **核心内容：** 该版本主要是一个稳定化发布，将自 `v0.20.4` 以来合并的大约 323 个 PR 汇总为稳定的 tagged 版本，供下游用户（如 Docker 镜像、托管部署、新安装）使用。
- **迁移与注意事项：**
    - 该版本为补丁更新，主要带来稳定性提升和累积的 Bug 修复。
    - **潜在风险：** 尽管为补丁版本，但累计 323 个 PR 的变更量较大。社区在 Issue #89886 和 #90806 中报告了在升级后出现的 Anthropic API 兼容性问题和 SQLite 数据库损坏问题，建议用户在升级后密切关注相关功能。

### 3. 项目进展

今日合并/关闭的 PR 数量有限，但关键修复针对性很强，主要围绕 CLI 健壮性和数据库稳定性。

- **修复 CLI 会话恢复崩溃:** [PR #91860](https://github.com/NousResearch/hermes-agent/pull/91860) 已关闭。该 PR 修复了当恢复的会话包含空文本消息时，`hermes chat --resume` 抛出的 `IndexError` 问题 [Issue #59265](https://github.com/NousResearch/hermes-agent/issues/59265)。这一问题已影响用户近两个月，本次修复提升了 CLI 的稳定性。
- **修复 state.db 损坏问题:** [PR #91839](https://github.com/NousResearch/hermes-agent/pull/91839) 已关闭。该 PR 通过防止在外部进程持有数据库文件时进行实时 FTS 重建，解决了多进程共享 `state.db` 导致的 WAL 文件“脑裂”和数据库损坏问题（如 [Issue #90806](https://github.com/NousResearch/hermes-agent/issues/90806) 所述）。这是针对严重稳定性问题的重要修复。

此外，今天有多个关键的修复性 PR 处于待合并状态，一旦合并将显著改善项目健康度，它们分别是：
- [PR #91852](https://github.com/NousResearch/hermes-agent/pull/91852): 在 macOS 上为 `state.db` 所有修复连接强制应用写入屏障，以防自修复期间发生损坏。
- [PR #89344](https://github.com/NousResearch/hermes-agent/pull/89344): 在真正发生上下文溢出时，允许模型透明地升级到更大的上下文窗口。
- [PR #91079](https://github.com/NousResearch/hermes-agent/pull/91079): 使 Windows 包重建过程具备事务性和自愈能力。

### 4. 社区热点

今日讨论热度最高的 Issue 集中反映了用户在真实环境中的痛点：

- **[Issue #66616: Skills index is stale or degraded](https://github.com/NousResearch/hermes-agent/issues/66616)** (评论: 71)
    - **诉求：** 自动化探针连续多日报告 Skills Hub 的索引数据过期，导致文档站点的技能信息不准确。这是典型的自动化基础设施问题，用户关注度极高，希望得到及时修复以避免被误导。

- **[Issue #87093: Debian installation broken; uv.lock & npm install failed](https://github.com/NousResearch/hermes-agent/issues/87093)** (评论: 19, 👍: 3)
    - **诉求：** 在 Debian 13.6 上通过官方脚本安装失败。这是一个影响新用户入门的高频问题，安装流程的可靠性是项目健康度的关键指标。

- **[Issue #90473: "show earlier messages" paging is a broken UX](https://github.com/NousResearch/hermes-agent/issues/90473)** (评论: 13)
    - **诉求：** 用户对长会话中“显示更早消息”的分页交互设计极为不满，认为其体验糟糕。这反映了在长上下文场景下，桌面客户端的用户界面和交互设计仍有较大优化空间。

### 5. Bug 与稳定性

过去24小时内报告的 Bug 主要集中在数据一致性、关键兼容性和状态管理方面，按严重程度排列如下：

- **P0 (严重):**
    - **[Issue #89886: Anthropic-format API rejects cache_control (non-retryable 400)](https://github.com/NousResearch/hermes-agent/issues/89886):** `v2026.8.18` 版本中，任何包含工具结果的会话都会因 `cache_control` 参数被 Anthropic 格式 API 拒绝而直接失败。这会导致所有工具调用功能不可用。**目前尚无直接修复的PR。**
    - **[Issue #91830: proactive_prune_rearm_tokens invalidates prompt-cache prefix for sessions >10M tokens](https://github.com/NousResearch/hermes-agent/issues/91830):** 长会话（>10M tokens）的提示缓存完全失效，导致成本显著增加。已被标记为重复问题，但核心原因依然存在。

- **P1 (高):**
    - **[Issue #90806: state.db structural corruption with SQLite 3.53.1](https://github.com/NousResearch/hermes-agent/issues/90806):** 多进程并发打开 `state.db` 导致数据库反复损坏，这是一个严重的稳定性和数据安全问题。虽然 [PR #91839](https://github.com/NousResearch/hermes-agent/pull/91839) 已修复，但需要验证修复的彻底性。
    - **[Issue #88655: Scheduler-level cron errors bypass failure_nudge alerting](https://github.com/NousResearch/hermes-agent/issues/88655):** Cron 任务在调度层面失败时，不会触发失败通知，导致任务静默失败数小时。该问题已关闭，但需确认修复方案是否完全解决了告警缺失问题。

- **P2 (中):**
    - **[Issue #88661: MCP tool timeout parks server connection](https://github.com/NousResearch/hermes-agent/issues/88661):** 单个 MCP 工具超时会导致整个 MCP 服务器连接被挂起，所有工具注销，需要重启网关才能恢复。
    - **[Issue #91818: Projects leak across profiles (broken isolation)](https://github.com/NousResearch/hermes-agent/issues/91818):** Windows 平台下，多配置文件（Profile）隔离失效，一个配置文件创建的项目会串扰到其他配置文件中。

### 6. 功能请求与路线图信号

用户对新功能的需求集中在提升部署可靠性和扩展平台集成能力上：

- **Fleet 更新可靠性 (Issue #91277):** 社区维护者明确指出安装/更新功能是当前最不可靠的部分，并提出了统一本地、远程、多配置文件更新的计划。这已被标记为 P1，是明确的路线图信号。
- **Bot Mode 群聊访问 (Issue #89995):** 用户希望将桌面端的 Bot Mode 群聊功能扩展到 Web Dashboard 和 Gateway。这显示了用户对协作和功能统一访问的需求。
- **OpenRouter 路由配置 (PR #89555):** 提交者希望通过配置指定 OpenRouter 的托管提供商和量化级别，以获得更可控的服务质量和成本。如果被采纳，将增强高级用户的自定义能力。

### 7. 用户反馈摘要

- **对产品体验的批评：** Issue #90473 中，用户直指“显示更多消息”的分页设计是“愚蠢的设计”，这为产品经理和UI/UX设计师敲响了警钟。
- **对部署复杂性的抱怨：** Issue #91277 中机器人维护者坦言，更新一个包含本地+远程网关、多个配置文件、桌面客户端的“舰队”是“命令式按平台搭建的意大利面条”，这真实反映了个人代理从单机走向多设备、多环境时遇到的部署阵痛。
- **对敏感操作误报的困扰：** Issue #85557 中，用户报告一个多行的 `python3 -c` 命令因路径中可能包含 “gateway” 等关键词，触发了网关生命周期保护误报，被安全策略错误地阻止。这表明安全边界检查在识别复杂真实命令时仍存在误判，需要更智能的解析逻辑。

### 8. 待处理积压

以下 Issue 长期开放且关注度较高，但缺少维护者响应或有效的修复进展：

- **[Issue #48190: Session ↔ Workspace binding](https://github.com/NousResearch/hermes-agent/issues/48190) (创建于 2026-06-18):** 会话无法记录工作目录和 Git 仓库信息，这对于复杂的开发场景至关重要，该功能请求已公开超过两个月。
- **[Issue #18954: Model aliases not resolved for custom providers](https://github.com/NousResearch/hermes-agent/issues/18954) (创建于 2026-05-02):** 自定义 provider 无法使用模型别名，导致请求失败。该问题已存在近4个月，影响了部分用户的接入体验。
- **[PR #49093: Add Matrix room-admin tools](https://github.com/NousResearch/hermes-agent/pull/49093) (创建于 2026-06-19):** 这是一个功能完整的 PR，但已等待合并超过两个月，且涉及安全边界考量，需要维护者决策。

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw 项目动态日报

**日期：2026-08-22** | **数据来源：github.com/sipeed/picoclaw**

---

## 1. 今日速览

PicoClaw 项目今日活跃度**中等偏低**。过去24小时内新增 1 个 Issue（均为新开），无新版本发布；PR 方面有 4 个旧 PR 被集中合并/关闭（创建时间集中在 2-3 月，存在较长搁置后批量处理的情况），说明维护者进行了一轮积压清理。值得关注的新信号是 #3342 提出的"after-turn"转向模式，指向了 agent 并发消息处理机制的优化方向——当前已合并的 PR 多为功能增强和文档改进，无破坏性变更。整体来看，项目处于**稳定迭代期**，核心关注点在工具链完善与协议兼容性扩展。


## 2. 版本发布

**今日无新版本发布。**

> 最近一次 release 距今已有一段时间。考虑到今日有 4 个 PR 被合并（包括新协议支持、CLI 重构等），预计下一版本将包含这些变更，建议关注合并后是否有 RC 版本推出。


## 3. 项目进展

今日 4 个 PR 被合并/关闭，均为 2-3 月间创建的历史 PR，经长时间搁置后于今日集中处理。这些变更反映了项目在三个方向上的实质推进：

- **WebFetchTool 能力增强**（[PR #647](https://github.com/sipeed/picoclaw/pull/647)）：合入 HTML 实体解码（`&amp;`、`&lt;` 等）及块级元素换行保留逻辑，改善网页文本提取的可用性。提升工具返回内容的可读性和结构化程度。

- **Anthropic 原生 API 协议支持**（[PR #1158](https://github.com/sipeed/picoclaw/pull/1158)，Fixes [#269](https://github.com/sipeed/picoclaw/issues/269)）：新增 `anthropic-messages` 协议前缀，使仅支持 Anthropic 原生 Messages API（`/v1/messages`）格式的服务可直接接入。扩展了可接入的 LLM 服务范围。

- **技能（Skills）CLI 重构**（[PR #714](https://github.com/sipeed/picoclaw/pull/714)）：新增 `reinstall` 子命令、支持 `repo@branch` 及可选子路径安装，并通过 GitHub Trees API 实现完整目录抓取。安装体验显著改善，错误提示更清晰。

- **AGENTS.md 文档优化**（[PR #1182](https://github.com/sipeed/picoclaw/pull/1182)）：将维护指南改为"原则优先"的轻量风格，以 `go.mod` 为 Go 版本唯一事实来源，降低 AI 代理/贡献者的理解成本。


## 4. 社区热点

今日唯一新开 Issue 成为社区关注焦点：

- **[#3342 [Feature] Opt-in "after-turn" steering mode: queue busy-session messages instead of interrupting the running turn](https://github.com/sipeed/picoclaw/issues/3342)** — 新开，暂无评论，但值得关注。

**诉求分析：** 用户期望当 agent 正在处理第一轮任务时，第二条用户消息不再作为"中途转向"信号（跳过剩余工具调用并立即注入新消息），而是可选地进入待处理队列，待当前轮次自然结束后再被处理。这是对当前"抢占式"交互模型的一种补充，反映出用户在多轮复杂任务中希望保持任务连贯性的需求。该 Issue 是 `Opt-in` 设计，不会破坏现有行为。


## 5. Bug 与稳定性

**今日无新 Bug 报告。**

今日合并的 PR 中包含以下稳定性相关改进：

- **[PR #647](https://github.com/sipeed/picoclaw/pull/647)**：修复了 WebFetchTool 中 HTML 实体未被正确解码导致提取文本出现乱码的问题（如 `&amp;` 显示为原始字符串而非 `&`）。
- **[PR #714](https://github.com/sipeed/picoclaw/pull/714)**：修复 skill 已存在时安装无明确提示的问题，新增 reinstall 子命令。

未发现崩溃、回归或严重稳定性问题。


## 6. 功能请求与路线图信号

今日新功能需求 1 个，另有多项已在 PR 中落地或推进：

| 功能 | 来源 | 状态 | 纳入下一版本可能性 |
|------|------|------|--------------------|
| "After-turn" 转向模式：队列化忙碌会话消息 | [Issue #3342](https://github.com/sipeed/picoclaw/issues/3342) | 新开，无实现 | **中低** — 属于 `opt-in` 行为变更，需评估交互模型影响面，短期落地概率不大，但可能作为后续版本的可选功能 |
| Anthropic 原生 Messages API 协议支持 | [PR #1158](https://github.com/sipeed/picoclaw/pull/1158)（已合并） | ✅ 已完成 | **已包含** — 大概率进入下一版本 |
| Skill 安装 CLI 增强（reinstall/分支/子路径） | [PR #714](https://github.com/sipeed/picoclaw/pull/714)（已合并） | ✅ 已完成 | **已包含** — 大概率进入下一版本 |
| WebFetchTool HTML 解码与结构保留 | [PR #647](https://github.com/sipeed/picoclaw/pull/647)（已合并） | ✅ 已完成 | **已包含** — 大概率进入下一版本 |

**路线图信号：** 按日期推断，今日合并的 4 个 PR 可能已进入 main 分支，建议关注近期版本发布计划。


## 7. 用户反馈摘要

今日无新增用户评论内容（新 Issue 暂无评论）。基于 Issue 描述和已合并 PR 的内容，可以提炼以下用户侧信息：

- **[Issue #3342](https://github.com/sipeed/picoclaw/issues/3342) 用户痛点：** 在多轮交互中，用户发送第二条消息的本意并非打断当前任务，而是希望在当前任务完成后得到补充响应。当前"中断即跳转"的行为导致工具调用被丢弃（日志中出现 "Skipped due to queued user message."），用户希望有一种更符合直觉的"排队"模式。
- **[PR #1158](https://github.com/sipeed/picoclaw/pull/1158) 使用场景：** 有用户（或用户群体）使用仅兼容 Anthropic 原生 API 格式的代理服务，此前无法通过 Anthropic 兼容模式连接，说明社区对 LLM 服务商兼容性的需求较为迫切。
- **[PR #714](https://github.com/sipeed/picoclaw/pull/714) 使用场景：** skill 安装时对已存在 skill 的处理不友好，用户需要强制覆盖/重装的能力，且安装过程应支持指定分支和子路径，说明技能生态的安装管理体验是当前痛点之一。


## 8. 待处理积压

**长期未响应的 Issue/PR 提示：**

| 项目 | 创建时间 | 搁置时长 | 备注 |
|------|----------|---------|------|
| [PR #647](https://github.com/sipeed/picoclaw/pull/647)（WebFetchTool 增强） | 2026-02-22 | 约 6 个月 | 今日已合并，搁置期内无回复 |
| [PR #714](https://github.com/sipeed/picoclaw/pull/714)（skills CLI 重构） | 2026-02-24 | 约 6 个月 | 今日已合并，搁置期内无回复 |
| [PR #1158](https://github.com/sipeed/picoclaw/pull/1158)（Anthropic 协议） | 2026-03-06 | 约 5.5 个月 | 今日已合并 |
| [PR #1182](https://github.com/sipeed/picoclaw/pull/1182)（AGENTS.md） | 2026-03-06 | 约 5.5 个月 | 今日已合并 |

> ⚠️ **观察：** 以上 4 个 PR 均存在 5-6 个月的等待期，今日集中处理说明维护者可能进行了一次大扫除。**建议：** 对于新提交的 PR，若能建立更及时的 review 机制（如 2-4 周内响应），将有助于提升贡献者体验和项目活跃度。同时关注 [#3342](https://github.com/sipeed/picoclaw/issues/3342) 在社区的后续讨论热度，如评论增长较快，建议尽快给出方向性反馈。


*报告生成时间：2026-08-22 | 数据窗口：2026-08-21 至 2026-08-22 | 项目健康度评分：⭐️⭐️⭐️☆（3.5/5，稳定迭代，PR 积压清理积极，但 Issue 响应速度待提升）*

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw 项目动态日报

**日期：** 2026-08-22  
**数据来源：** github.com/qwibitai/nanoclaw  
**统计周期：** 2026-08-21 ~ 2026-08-22


## 1. 今日速览

过去 24 小时 NanoClaw 项目处于**高强度开发迭代期**。PR 侧非常活跃，共 25 条更新，其中 11 条已合并/关闭、14 条待合并；Issue 侧仅 1 条新开 Bug（无关闭）。今日无新版本发布。核心团队（core-team 标签）围绕 **Telegram 多实例支持** 和 **模板化 Agent 创建** 两个方向集中推进，同时完成了多项通道集成（Dial、Matrix、WhatsApp Cloud、Mattermost）的合并与修复。整体来看，项目正处于 **多通道能力扩张与稳定性加固并行** 的阶段，提交节奏密集，工程化程度较高（CI 矩阵、补丁管理等均有涉及）。需关注点：14 条待合并 PR 中有 9 条来自同一位核心成员（amit-shafnir），合并积压风险值得留意。


## 2. 版本发布

今日无新版本发布（Releases 为 0）。


## 3. 项目进展

今日合并/关闭了 11 个 PR，核心进展集中在以下三个方向：

### 3.1 通道集成与修复（合并 5 条）

| PR | 标题 | 说明 |
|---|---|---|
| [#3202](https://github.com/nanocoai/nanoclaw/pull/3202) | Add Mattermost channel integration | **Mattermost 通道正式合入**，作为 Chat SDK 新通道，与既有 `slack.ts` 模式对齐，通过 `registerChannelAdapter` 注册，封装社区适配器。关闭 Issue #1379。 |
| [#3401](https://github.com/nanocoai/nanoclaw/pull/3401) | fix(whatsapp-cloud): keep skill payload compatible with main | WhatsApp Cloud 技能在组合 main 分支时因依赖 channels 分支独有注册表助手而失败，已修复兼容性。 |
| [#3402](https://github.com/nanocoai/nanoclaw/pull/3402) | fix(providers): accept provider file events | 修复分支来源 provider 已发出但未被接受的 file 事件，无运行时行为变更。 |
| [#3403](https://github.com/nanocoai/nanoclaw/pull/3403) | fix(matrix): use a refresh-safe ESM patch | Matrix 适配器在 Node 22 下因无扩展名 ESM 导入失败，改用提交式 pnpm patch，刷新后自动重应用。 |
| [#3050](https://github.com/nanocoai/nanoclaw/pull/3050) | feat(setup): add Dial to the channel picker + wizard/skills | **Dial 通道正式进入安装向导**，涉及 `runChannelSkill` 模型，将 Dial 纳入 channel picker 和技能体系。该 PR 从 7 月 14 日提出至今历时 38 天，今日终于合入。 |

### 3.2 工程化与基础设施（合并 3 条）

| PR | 标题 | 说明 |
|---|---|---|
| [#3424](https://github.com/nanocoai/nanoclaw/pull/3424) | ci: test registry-backed skills | 新增 CI 流水线：自动发现所有从 channels/providers 拉取的 add-* 技能，在固定 registry 快照上执行构建与测试。 |
| [#3430](https://github.com/nanocoai/nanoclaw/pull/3430) | fix: restore stable CI required check | 修复 Node 22/24 矩阵导致 `ci` 必检项失效的问题，恢复稳定的 CI 门槛。 |
| [#3439](https://github.com/nanocoai/nanoclaw/pull/3439) | chore(container): bump claude-code to 2.1.238 and agent SDK to 0.3.238 | 容器依赖升级：Claude Code CLI 2.1.197 → 2.1.238，Agent SDK ^0.3.197 → ^0.3.238。 |

### 3.3 驱动层抽象（合并 1 条）

| PR | 标题 | 说明 |
|---|---|---|
| [#3429](https://github.com/nanocoai/nanoclaw/pull/3429) | feat(drivers): ratify the attach surface — a driver describes its exec argv | 定义 `SessionExecSpec { bin, argsTty, argsPlain }` 契约，驱动描述其运行时如何拼装 exec 调用，**为交互式终端附加（attach）会话提供描述性接口**。 |

### 3.4 小结

今日合入内容覆盖 **Mattermost 新通道、Dial 正式上线向导、Matrix/WhatsApp 修复、CI 加固、驱动层契约定义**。项目在多通道战略上迈出实质性一步——从 Slack 单一主导走向多平台覆盖；同时，`SessionExecSpec` 契约的落地为后续交互式调试工具铺平了道路。


## 4. 社区热点

今日 PR 评论数为 `undefined`（数据未返回），无法基于评论数判断热点。从 PR 标签和更新频率来看，以下几点值得关注：

- **[amit-shafnir 的 Telegram 多机器人系列（PR #3436 / #3435 / #3431 / #3438 / #3437）](https://github.com/nanocoai/nanoclaw/pull/3436)** — 今日核心成员 amit-shafnir 在同一时间窗口密集提交了 5 个相互关联的 PR，覆盖 Telegram 命名实例（`TELEGRAM_INSTANCES`）、实例绑定配对、向导二次添加、CLI 欢迎页和文档。**这套组合拳说明 Telegram 多租户支持是当前最优先的方向。**

- **[PR #3428 的"re-port"（重新移植）](https://github.com/nanocoai/nanoclaw/pull/3428)** — 标题中的 "re-port" 揭示了团队的一个协作问题：#3397 在依赖（#3396）未合入前就被提前合并，导致代码引用 trunk 上尚不存在的内容，被迫在分支上回滚后重新提交。**这反映了在并行开发时合并顺序管理存在摩擦。**

- **[Issue #3426（send_card 按钮丢失）](https://github.com/nanocoai/nanoclaw/issues/3426)** — 唯一的活跃 Issue，虽然评论为 0，但它是一个**有趣的"人机信任"问题**——Agent 被 `send_card` 文档误导，向用户错误归因平台能力。后续可关注是否引发文档修订。


## 5. Bug 与稳定性

### 5.1 今日新报 Bug

| 严重程度 | Issue/PR | 描述 | 状态 |
|---|---|---|---|
| ⚠️ 中 | [#3426](https://github.com/nanocoai/nanoclaw/issues/3426) | `send_card` 文档承诺支持 `actions`（按钮），但 bridge 丢弃所有无 `url` 的 action。Agent 看到按钮消失后，根据误导性的 `fallbackText` 向用户解释"平台不支持按钮"。 | **无修复 PR**，属于文档/实现不一致问题 |

### 5.2 今日修复的 Bug（已合并）

| 严重程度 | PR 链接 | 描述 |
|---|---|---|
| 🔴 高 | [#3403](https://github.com/nanocoai/nanoclaw/pull/3403) | Matrix 适配器在 Node 22 上因 ESM 扩展名问题**完全不可用**，现已通过 pnpm patch 修复 |
| 🟠 中高 | [#3439](https://github.com/nanocoai/nanoclaw/pull/3439) | 容器 CLI 版本落后（2.1.197），存在潜在安全/功能风险，已升至 2.1.238 |
| 🟡 中 | [#3401](https://github.com/nanocoai/nanoclaw/pull/3401) | WhatsApp Cloud 技能在 main 分支组合时测试失败（依赖 channels 独有助手） |
| 🟡 中 | [#3430](https://github.com/nanocoai/nanoclaw/pull/3430) | Node 22/24 矩阵引入后，原先唯一的 `ci` 检查被拆分为 `ci (22)` + `ci (24)`，导致仓库 required check **永久处于未满足状态**，主分支合并可能被阻塞 |

### 5.3 待合并修复 PR

| 严重程度 | PR 链接 | 描述 |
|---|---|---|
| 🟠 中高 | [#3434](https://github.com/nanocoai/nanoclaw/pull/3434) | **轮询型适配器错误地启动了 webhook 服务器**——这不是崩溃，而是不必要的资源浪费和潜在端口冲突。 |
| 🟡 中 | [#3431](https://github.com/nanocoai/nanoclaw/pull/3431) | Telegram 配对卡片显示 6 位数字（实际应该是 8 位？），用户会被误导 |
| 🟡 中 | [#3287](https://github.com/nanocoai/nanoclaw/pull/3287) | `getMessageIdBySeq()` 原样返回 `messages_in.id`，实则包含 agent-group 前缀，**导致入站消息 ID 处理错误**（Fixes #3153）。已等待 5 天 |


## 6. 功能请求与路线图信号

| 信号 | 来源 | 分析 |
|---|---|---|
| **Telegram 多机器人实例** | [PR #3436](https://github.com/nanocoai/nanoclaw/pull/3436) 等 5 个关联 PR | 最明确的路线图信号：`TELEGRAM_INSTANCES` 环境变量支持命名多个 bot，配合实例绑定的配对流程和向导二次添加入口。**预计进入下一版本**。 |
| **Agent 模板创建** | [PR #3396](https://github.com/nanocoai/nanoclaw/pull/3396) + [PR #3428](https://github.com/nanocoai/nanoclaw/pull/3428) | `create_agent` 工具增加可选 `template` 参数，支持从本地 `templates/` 目录或公共 registry 索引创建 agent。Slack 侧已配套打通。**跨通道模板化能力是下一阶段的重点。** |
| **驱动 exec 描述契约** | [PR #3429](https://github.com/nanocoai/nanoclaw/pull/3429)（已合并） | `SessionExecSpec` 定义了 driver 描述 exec argv 的标准方式。**为交互式终端 attach 功能铺路**，未来可能支持 agents 的实时终端接入。 |
| **Mattermost 通道** | [PR #3202](https://github.com/nanocoai/nanoclaw/pull/3202)（已合并） | 正式支持 Mattermost，通道矩阵进一步扩容：Slack → Telegram → Dial → WhatsApp → Matrix → Mattermost。 |
| **Registry-backed 技能测试** | [PR #3424](https://github.com/nanocoai/nanoclaw/pull/3424)（已合并） | CI 开始覆盖所有 registry 技能，**意味着 add-* 技能生态将被制度化**，未来新增技能会获得自动化保障。 |

**预测：** 下一版本的中期路线图很可能围绕 **Telegram 多实例 + 模板化 Agent + 交互式 attach** 三主线展开。


## 7. 用户反馈摘要

今日仅有一条活跃 Issue（#3426），评论为 0，缺乏直接用户话语。但结合已有数据可提取出以下信息：

| 反馈来源 | 用户诉求/痛点 |
|---|---|
| [Issue #3426](https://github.com/nanocoai/nanoclaw/issues/3426) | **文档承诺与实际行为的落差导致用户体验受损。** 用户实际经历是：Agent 声称"平台不支持按钮"，但真实原因是 bridge 丢弃了无 `url` 的 action。**用户对平台能力的判断被误导了**——当工具文档与实际实现不一致时，Agent 会把自身缺陷转嫁为"平台限制"，造成对 NanoClaw 能力的低估。 |
| [PR #3431](https://github.com/nanocoai/nanoclaw/pull/3431) | **Telegram 配对卡片显示错误的数字位数（6 位 vs 实际）**，用户按提示操作会失败。这类"小错误"对首次上手的用户是很大的摩擦。 |
| [PR #3287](https://github.com/nanocoai/nanoclaw/pull/3287) | 入站消息 ID 包含 agent-group 后缀导致处理异常，这会影响**消息去重、回复映射**等核心行为，对重度用户影响较大。 |

目前项目的用户反馈体系还比较简单——Issues 评论数为 0，也可能是数据导出未包含 comment 计数；从 Issue 本身来看，`send_card` 的问题是真实用户手动创建还是自动化 agent 报告（作者名为 "glifocat"，与 #3432 作者相同），值得关注。


## 8. 待处理积压

### 8.1 目录

- [ ] 以下 PR 和 Issue 已等待较长时间或涉及核心功能，需要维护者关注：

| 类型 | 编号/链接 | 主题 | 等待时长 | 严重度 | 备注 |
|---|---|---|---|---|---|
| PR | [#3287](https://github.com/nanocoai/nanoclaw/pull/3287) | 修复入站消息 ID 含 agent-group 后缀问题（Fixes #3153） | 5 天 | 中高 | 影响消息去重/回复映射，无 reviewer 介入迹象 |
| PR | [#3432](https://github.com/nanocoai/nanoclaw/pull/3432) | Dial 合并后跟进：凭据重跑、步骤标题、registry CI | 1 天 | 中 | 属于 #3050 合并后的技术债清理 |
| PR | [#3434](https://github.com/nanocoai/nanoclaw/pull/3434) | 轮询适配器不应启动 webhook 服务器 | 1 天 | 中 | 核心团队提交，大概率会被合入 |
| Issue | [#3426](https://github.com/nanocoai/nanoclaw/issues/3426) | `send_card` 文档与 bridge 行为不一致 | 1 天 | 中 | 无 fix PR，需要文档修正或实现调整 |

### 8.2 潜在系统性风险

**合并顺序管理问题**（今日 #3428 暴露）：#3397 在依赖 #3396 未合入时被提前合并，导致需要 revert 后重新提交。**当多个 PR 之间存在依赖关系时，仓库缺少自动化的依赖检查**（例如 GitHub 的 "required status check" 或 "dependent pr" 机制）。建议在 CONTRIBUTING 中添加硬性规则或使用 CI bot 检查 PR 合并顺序。

**同一位开发者大量并发 PR**：amit-shafnir 一人持有 9 个待合并 PR（占待合并总量的 64%），如果该开发者请假或转向其他任务，这 9 个 PR 将全部阻塞——包括 Telegram 多实例、向导改进等核心功能。建议考虑拆分 assignee 或安排 reviewer 轮值。

### 8.3 健康度评估

| 维度 | 状态 | 说明 |
|---|---|---|
| Issue 响应速度 | 🟢 良好 | 仅 1 条新 Issue，暂无积压 |
| PR 合并效率 | 🟡 一般 | 25 条更新中仅 11 条关闭，14 条积压 |
| 依赖管理 | 🟡 有风险 | #3397 提前合并暴露依赖顺序缺失 |
| CI 稳定性 | 🟢 良好 | #3430 修复了 required check 失效问题；#3424 扩展了 registry 测试覆盖 |
| 版本发布节奏 | 🟡 停滞 | 近期无 Release，可能在做积累 |
| 核心团队活跃度 | 🟢 极高 | Core-team 标签在 11/25 PR 上出现，多位核心成员（zvi-fried、gavrielc、amit-shafnir、glifocat）今日均有动作 |

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

# NullClaw 项目动态日报

**日期：2026-08-22** | 数据窗口：2026-08-21 至 2026-08-22  
**数据来源：** [github.com/nullclaw/nullclaw](https://github.com/nullclaw/nullclaw)

---

## 1. 今日速览

NullClaw 项目今日整体活跃度处于**低水平**，过去 24 小时无新 Issue 产生、无新版本发布，仅有 1 条 PR 提交且处于待合并状态。项目当前处于"提交暂歇、审查持续"的阶段——社区讨论安静但维护者保持节奏推进 provider 生态扩展。核心动向是 #990 将 Eden AI 作为 OpenAI 兼容网关接入，延续了近期通过 `OpenAiCompatibleProvider` 统一路由外部供应商的架构路线。整体项目健康度良好，无阻塞性问题或突发回归报告。

---

## 2. 版本发布

**今日无新版本发布。**

---

## 3. 项目进展

### 核心进展：PR #990 — Eden AI 作为 OpenAI 兼容网关接入

**状态：** 待合并 | [PR #990](https://github.com/nullclaw/nullclaw/pull/990)

**作者：** MVS-source | **创建：** 2026-08-21

**内容摘要：**
- 新增 **Eden AI** 作为 OpenAI 兼容网关 provider，完全复用既有 `OpenAiCompatibleProvider` 实现，不引入任何新的 provider 代码。
- 结构完全对齐此前 #922（NEAR AI Cloud 与 Atlas Cloud）的合并模式，属**标准化扩展**。
- Eden AI 核心卖点：**一个 API key 路由多家上游供应商**，且服务基地位于欧盟。

**项目推进意义：**
- 这是 NullClaw 本月第 3 次扩展 OpenAI 兼容网关生态（#922 → #990），表明项目正在 **系统性地降低用户接入多家 AI 供应商的摩擦成本**。
- **架构信号：** 不写新代码就能扩展供应商，验证了此前抽象层的设计质量，后续新增供应商的边际成本将逐步趋近于零。

---

## 4. 社区热点

今日唯一活跃 PR 为 [#990](https://github.com/nullclaw/nullclaw/pull/990)，暂无评论互动（评论数: undefined），未形成讨论热度。

项目整体讨论氛围平静，无热门 Issue 或高互动帖子。值得注意的是，**PR 作者选择直接按照既有模式提交而非先开 Issue 讨论**，从侧面反映了社区贡献流程的成熟度——新供应商接入已成为一条清晰的"标准化路径"。

---

## 5. Bug 与稳定性

**今日无新 Bug 报告、无崩溃、无回归问题。**

项目当前处于稳定状态，未发现需要优先处理的质量问题。

---

## 6. 功能请求与路线图信号

### 今日无新功能请求。

**路线图信号解读（基于 PR #990）：**

| 信号 | 判断依据 | 纳入下一版本可能性 |
|------|----------|-------------------|
| **多供应商聚合网关** 持续被引入 | Eden AI 以"一个 key 路由多家供应商"为卖点加入，且 #922 模式被复用 | **高** — 该方向已被验证并快速复制 |
| **欧盟数据合规诉求** | Eden AI 强调"EU based"，暗示用户对数据驻留的关切 | **中** — 可能引导后续优先引入欧盟区域供应商 |

---

## 7. 用户反馈摘要

今日无 Issue 评论数据可提取。基于 PR #990 的提交内容，可初步推断用户侧诉求：

- **痛点：** 用户希望减少管理多个 AI 供应商 API key 的复杂度，通过单一入口触达多家模型服务。
- **场景：** 需要在不同上游模型间灵活切换（如成本优化、性能对比），且对数据合规（尤其欧盟地区）敏感。
- **满意信号：** 贡献者选择直接 PR 而非讨论，说明现有 OpenAI 兼容抽象层已被社区理解和信任。

---

## 8. 待处理积压

无长期未响应的重要 Issue 或 PR。当前唯一待合并项为 [#990](https://github.com/nullclaw/nullclaw/pull/990)，建议维护团队**尽快安排 Review**，避免贡献者等待时间过长影响积极性。该 PR 属低风险扩展（无新代码、已有先例），可考虑走快速合并通道。

---

*本日报由 AI 自动生成，数据截至 2026-08-22 00:00 UTC。所有链接均指向 GitHub 原始数据。*

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw 项目动态日报

**日期：2026-08-22** | **数据来源：GitHub (nearai/ironclaw)** | **统计窗口：过去 24 小时**


## 1. 今日速览

过去 24 小时项目保持高强度迭代状态：**20 条 Issue 更新（15 条活跃/新开）** 与 **35 条 PR 更新（17 条已合并/关闭）** 显示核心团队与社区贡献者均在密集推进。当日无新版本 Release，但合并了多项关键修复（包括 `IRONCLAW_REBORN_WORKSPACE_ROOT` 前向移植、clippy 1.98 lint 修复、Telegram 配对逻辑分离等），并围绕 **CI 流水线重构（T1-T4 系列）**、**可插拔内存架构** 与 **WebUI 设计系统** 三大主线展开攻坚。值得关注的是，多条 `release/2026-08-17` 分支的 CI 全量故障（clippy 报错）已被紧急修复并合并，释放了分支合并阻塞。整体来看，项目处于 **高活跃、健康推进** 状态，但大型 PR（XL 级）数量较多，合并周期可能偏长。


## 2. 版本发布

**无新版本 Release。** 上一个版本仍为 `release/2026-08-17`。值得注意的是，今日合并的多个修复（如 #7805 clippy 修复、#7804 workspace-root 前向移植）均针对该版本分支，暗示下一次发布可能已有候选内容。


## 3. 项目进展

今日共 **17 条 PR 合并/关闭**，主要进展集中在以下方向：

| 方向 | 关键 PR | 影响 |
|---|---|---|
| **CI 稳定性修复** | [#7805 fix(ci): forward-port the clippy 1.98 lint fixes to 1.3](https://github.com/nearai/ironclaw/pull/7805) | 修复 `release/2026-08-17` 分支上 **所有 PR 的 clippy 全量失败**（`chunks_exact` 常量分块 lint 报错），解除分支合并阻塞 |
| **Workspace 配置修复** | [#7804 fix(workspace): honor IRONCLAW_REBORN_WORKSPACE_ROOT on 1.3](https://github.com/nearai/ironclaw/pull/7804) | 将 1.3 分支上的 workspace-root 覆盖变量前向移植至 main 和 release 分支，修复 CLI 双启动路径不一致问题 |
| **沙箱安全增强** | [#7807 / #7806 feat(sandbox): mediate GitHub CLI credentials](https://github.com/nearai/ironclaw/pull/7807) | 新增 GitHub CLI 凭据中介机制：凭据从活动扩展声明解析、经授权后一次性物化、沙箱内仅暴露调用占位符，强化凭据安全边界 |
| **Telegram 连接修复** | [#7803 fix(telegram): keep paired channels ready and collapse reply drafts](https://github.com/nearai/ironclaw/pull/7803) + [#7766 分离 bot 配对与个人设备绑定](https://github.com/nearai/ironclaw/pull/7766) | 修复 bot 配对与个人账号连接混淆问题，要求 WebUI 端显式选择连接模式（含 11 个语言包的权限声明更新），并保持已配对 bot 在无个人凭据时仍可用 |
| **沙箱审计增强** | [#7796 fix(sandbox): preserve failed Railway audit appends](https://github.com/nearai/ironclaw/pull/7796) | Railway 代理审计记录追加失败时 fail-closed 并保留暂存数据供重试 |
| **通知中心落地** | [#7699 feat(notifications): publish actionable run gates](https://github.com/nearai/ironclaw/pull/7699) 已关闭 | 批准、认证、阻塞运行事件已发布至持久化用户收件箱，使用稳定的 run/gate 派生 ID 保证重试幂等 |
| **文档/Agent 引导清理** | [#7797 docs(guidance): repo-wide agent-guidance audit](https://github.com/nearai/ironclaw/pull/7797) | 13 路并行审计 Agent 引导文档，修剪 ~21.5k 行，统一到 AGENTS.md 约定 |

**整体判断**：今日合并内容以 **修复分支阻塞、安全加固、连接体验修正** 为主，同时大型功能 PR（如 #7700 通知系统、#7750 Storybook 集成）仍在开放状态，尚未合并入主干。


## 4. 社区热点

**讨论最活跃的 Issue（评论数 ≥ 2）：**

| Issue | 评论数 | 主题 |
|---|---|---|
| [#7801 CI expedite T4: canonical preflight](https://github.com/nearai/ironclaw/issues/7801) | 3 | 统一预检门禁列表、worktree-safe hooks、自打印 REPRO |
| [#7799 CI expedite T2: nextest pipeline](https://github.com/nearai/ironclaw/issues/7799) | 3 | nextest 替换串行 `cargo test`、PR 并行上限调整 |
| [#7664 Pluggable memory over MCP](https://github.com/nearai/ironclaw/issues/7664) | 2 | 可插拔内存架构：Mnesis 作为首个消费者，定义 provider 契约 |
| [#7800 CI expedite T3: PR/queue convergence](https://github.com/nearai/ironclaw/issues/7800) | 2 | 绿色 PR/红色队列分歧治理、default-features clippy |
| [#7798 CI expedite T1: setup-rust composite](https://github.com/nearai/ironclaw/issues/7798) | 2 | 合并 43 处分散的 rust-toolchain 调用为单一 composite action |

**热点分析**：

- **CI 重构（T1-T4）是绝对焦点**：4 个关联 Issue 由 `henrypark133` 同日创建，目标直指当前 CI 的核心痛点——43 处散落的 toolchain 调用、串行测试耗时、PR/队列门禁不一致。这说明项目 **CI 基础设施正在经历系统性升级**，对贡献者体验和合并速度均有直接影响。
- **可插拔内存架构（#7664）** 持续获得关注，是架构层面的长期演进方向——将检索外包给外部 provider（Mnesis 首发），但宿主需在**写入路径**先行完成脱敏与 taint 元数据（见 #7808，最新阻断项）。


## 5. Bug 与稳定性

按严重程度排列：

| 严重度 | Issue/PR | 描述 | 状态 |
|---|---|---|---|
| **高** | [#7805](https://github.com/nearai/ironclaw/pull/7805) | `release/2026-08-17` 分支 **所有 PR 的 clippy(all-features) 全量失败**（`chunks_exact` lint），任何 PR 合入均被阻塞 | ✅ 已合并修复 |
| **中** | [#7783 LLM timeout policy: finalization can't measure TTFT](https://github.com/nearai/ironclaw/issues/7783) | 结构化输出 finalization 走非流式 HTTP 客户端：provider 请求停顿不可见（60s 总墙钟上限触发前无信号），75s deadline 会在重试完成前强杀运行。**单次传输停顿即导致整体运行失败** | ✅ 已关闭（2026-08-21），有修复 |
| **中** | [#7715 Telegram connection flow lacks consent/selection](https://github.com/nearai/ironclaw/issues/7715) | Telegram 连接流程未提供 bot 与个人账号之间的选择，用户不知当前处于哪种模式（Railway 测试实例发现） | ✅ 已关闭，对应修复已合并（#7766/#7803） |
| **低** | [#7796](https://github.com/nearai/ironclaw/pull/7796) | Railway 代理审计记录追加失败时静默吞掉，导致审计丢失 | ✅ 已合并修复（fail-closed + 保留重试） |
| **低** | [#7808 Memory write path: redaction + taint metadata required](https://github.com/nearai/ironclaw/issues/7808) | 内存写入路径当前以明文输出会话内容，绑定任何外部 provider 前必须在写入时完成脱敏 + taint 元数据 | 🔴 新增开放，无 fix PR 关联，系 #7664 的前置阻断项 |

**稳定性总评**：昨日报告的 LLM 超时策略缺陷（#7783）与 Telegram 连接问题（#7715）均已在 24 小时内闭环（修复已合并），响应速度值得肯定。当前主要稳定性风险集中在 CI 分支状态与内存写入路径的脱敏缺口。


## 6. 功能请求与路线图信号

结合今日 Issue/PR 动向，以下功能方向信号较强：

| 方向 | 信号来源 | 可能性判断 |
|---|---|---|
| **CI 编排优化（T1-T4）** | [#7798-7801 四个并行 tracks](https://github.com/nearai/ironclaw/issues/7798)，已有关联 PR（#7809 已开，实现 T4 任务 1-5） | **高——正在实施**，预计未来 1-2 周内分步合入，核心收益是贡献者体验与合并吞吐量 |
| **可插拔外部内存（Mnesis）** | [#7664 追踪 issue](https://github.com/nearai/ironclaw/issues/7664) + #7661（provider crate 草案）+ #7808（写入路径前置条件） | **中——架构方向明确，但前置条件（脱敏/taint）未完成**，可能延后 |
| **WebUI 设计系统（Phases 1-5）** | [#7038 (Phase 1)](https://github.com/nearai/ironclaw/issues/7038)、[#7781 (Phases 2-3)](https://github.com/nearai/ironclaw/issues/7781)、[#7782 (Phases 4-5)](https://github.com/nearai/ironclaw/issues/7782)，PR #7750（Storybook 集成）已重开待审 | **中——史诗重构中，5 个 Phase 拆分清晰**；#7781 已替换旧 Epic #7733，规划收敛良好 |
| **用户通知收件箱** | [#7687 epic](https://github.com/nearai/ironclaw/issues/7687) + PR #7700（权威运行结果通知）开放中 | **高——后端已合入（#7699），前端泛化（#7689）已关闭**，剩余 #7700 待合并后接近完成 |
| **AfterTurn 生命周期 Hook** | [#7765 PR（#7770 Phase 1）](https://github.com/nearai/ironclaw/pull/7765) 开放中 | **中——首个 act-capable hook 点**，仅限 Privileged 扩展（Builtin/Trusted），内存策展为首个消费者 |


## 7. 用户反馈摘要

从今日 Issue 评论、摘要中提取的用户声音：

- **CI 体验诉求强烈**（来自 #7798-7801）：贡献者在 PR 描述中明确表达了当前 CI 的痛点——(a) 12 个 workflow 文件中 43 处散落的 toolchain 调用导致漂移；(b) 串行 `cargo test` 循环使验证周期过长；(c) 绿色 PR 但红色队列的"计划器选择不足"根因已两度被证实。诉求是 **"一套门禁、工作区安全 hooks、自打印 REPRO"**，目标是将预检时间压缩至 **~5 分钟预测性反馈**。
- **运行时超时策略缺陷**（#7783）：开发者指出"单次传输停顿即摧毁整个运行"，最终化阶段的非流式客户端使 TTFT 不可测量，重试预算与 deadline 不匹配。"A single transport stall destroys a run"——这是对生产可用性的直接质疑。
- **Telegram 连接模式混乱**（#7715，QA 在 Railway 实例发现）：用户无法判断当前连接的是 bot 还是个人账号，缺少 consent/selection 步骤。修复方向为**显式选择 + 11 个语言包的权限声明**，体现了多语言场景下的合规意识。
- **WebUI 设计系统推进中**：Epic #7038 被重新划定范围（Phase 1 独立、Phases 2-3 合并至 #7781、4-5 拆至 #7782），说明团队在**控制史诗粒度**，避免 mega-issue 难以追踪。


## 8. 待处理积压

以下 Issue/PR 值得维护者关注：

| 项目 | 类型 | 创建时间 | 状态 | 关注点 |
|---|---|---|---|---|
| [#7038 WebUI Design System Phase 1 Epic](https://github.com/nearai/ironclaw/issues/7038) | Issue | 2026-08-03（已 19 天） | 开放，Phase 1 关联 PR #7750 已重开待审 | 设计系统是 WebUI 产品化的重要基础，需推动评审进度 |
| [#7042 Design System Phase 2: DESIGN.md governance](https://github.com/nearai/ironclaw/issues/7042) | Issue | 2026-08-03（已 19 天） | 开放，归属 #7781 | 依赖 #7781 推进 |
| [#7456 fix(reborn): make durable storage profile-agnostic](https://github.com/nearai/ironclaw/pull/7456) | PR | 2026-08-10（已 12 天） | 开放，XL 级，risk: medium | 存储架构调整涉及安全性（重启时 profile 切换不能削弱租户隔离），长时间未合入需关注是否存在阻塞性 review 意见 |
| [#7491 omp core-tool contract + engines + benchmark arm](https://github.com/nearai/ironclaw/pull/7491) | PR | 2026-08-11（已 11 天） | 开放，XL 级，risk: medium | 编码工具表面精简（6 个裸名称），涉及面广，需确认是否与 CI expedite 系列存在冲突 |
| [#7650 feat(automations): derive run outcomes from runtime evidence](https://github.com/nearai/ironclaw/pull/7650) | PR | 2026-08-14（已 8 天） | 开放，XL 级 | 以运行时证据替代基于答案的语义评判，是自动化可靠性升级，建议关注评审状态 |
| [#7785 / #7784 executor 测试代码拆分清理](https://github.com/nearai/ironclaw/issues/7785) | Issue | 2026-08-20 | 开放，无评论 | 测试支撑代码达 1,657 行单文件，属于技术债清理，优先级不高但可纳入 backlog |

**特别关注**：CI expedite T1-T4（#7798-7801）虽为今日新增，但直接阻塞贡献者体验与合并效率，建议优先排期；#7664（可插拔内存）依赖 #7808 的写入路径脱敏先行，该链条若遇阻需及时同步社区预期。

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

# LobsterAI 项目动态日报 — 2026-08-22

## 1. 今日速览

LobsterAI 项目过去 24 小时保持了中等偏高的活跃度，核心开发节奏集中于代码合并与发布流程（共 13 条 PR 更新，其中 12 条已合并/关闭）。当日完成了 `2026.8.21` 版本的发布回归合并（#2519），并集中推送了「资料库/本地产物」模块的体验优化（#2513/#2514/#2517）以及 DSH（DeepSeek Harness）实验性运行时的更新与分析能力增强（#2515/#2516/#2518）。Issue 侧主要为两条历史问题的自动 stale 关闭，无新问题涌入，项目整体处于健康稳定状态。


## 2. 版本发布

过去 24 小时无新版本发布，但通过 PR #2519 完成了 **`2026.8.21` 版本**由 `release/2026.8.21` 分支向 `main` 的合并，该版本包含以下亮点：

- **DSH 运行时升级**：将实验性 DeepSeek Harness（DSH）运行时更新至 `0.1.1-rc.1`（#2516），并新增了针对 DSH 启用开关及工作台打开行为的隐私友好型分析埋点（#2515）。
- **Windows 集成可靠性提升**：合并说明中明确包含改进 Windows 环境集成稳定性的相关改动。

> **正式 release notes 尚未发布**，建议等待项目组发布正式公告后，再确定是否有需要用户关注的破坏性变更。


## 3. 项目进展

今日合并/关闭的 12 条 PR 中，除 4 条历史遗留（4 月创建）的清理性关闭外，共有 **8 条实质性合入**，重点推进了以下几个方向：

### 3.1 资料库与本地产物模块（重点）
围绕本地产物预览与分享体验完成了两轮密集优化，并已作为 `2026.8.21` 版本的一部分发布：
- **#2513 / #2514**：调整预览弹窗尺寸与溢出约束适配不同窗口安全区域；移除资料库删除文件入口（精简操作）；区分资料库空状态与筛选无结果状态；为本地和云端搜索框增加一键清空；修复发布额度弹窗重复占位符替换问题。
- **#2517**：分享打包时保留 Unicode 文件名（仅替换不安全字符）；兼容历史版本文件名并优先展示原始标题；优化收藏状态的即时更新、筛选移除及失败回滚；避免收藏事件触发重复列表刷新；统一订阅与发布额度限制弹窗的样式、焦点和关闭行为。

### 3.2 DSH（实验性 DeepSeek Harness）
- **#2516**：DSH 运行时升级至 `0.1.1-rc.1`。
- **#2515 / #2518**：为 DSH 的启用开关和工作台打开行为新增使用分析埋点，并将埋点上报逻辑从主进程迁移至渲染进程，以更隐私友好的方式采集数据。

### 3.3 遗留 PR 清理
一批 4 月创建的 PR（#1215、#1218、#1219、#1220、#1224）因长期未合并被自动关闭。这些 PR 涉及 IM 聊天 handler 重建、定时任务排序规则重构、Cowork 会话列表重渲染优化及 N+1 查询消除等**具有明确价值的修复**，其中 #1218、#1219、#1220 的改动方向值得重新评估并跟进（详见第 8 节）。


## 4. 社区热点

今日无高热度讨论的 Issue 或 PR，这与当日以合并动作为主、无新问题涌入的整体状态一致。两条被自动关闭的历史 Issue（#1217、#1223）各拥有 2 条评论，是近期唯一产生过讨论的问题，相关诉求如下：

- **#1217【偶发网关重启】**：用户反馈在正常使用过程中网关偶发重启（每天 3-5 次），影响任务执行稳定性，该问题自 4 月报告后未获回应，于今日被 stale 机制关闭。
- **#1223【i18n 与弹窗体验】**：包含三个关联的 UX/i18n 问题——`CoworkPromptInput.tsx` 硬编码中文「输入文件」导致英文用户提示词混入中文；Agent 弹窗缺少 Escape 键关闭；删除操作缺少防重复点击保护。该问题已由 PR #1224 修复，但 #1224 同样因长期未合并被关闭。


## 5. Bug 与稳定性

今日报告的新 Bug 为 0 条，仅两条历史 Bug 被 stale 关闭。按严重程度整理如下：

| 严重程度 | 问题 | 状态 | 是否有 fix PR |
|---|---|---|---|
| 中 | **#1217** 网关偶发重启，每天 3-5 次，影响任务执行（win10, 版本 2026.3.26） | 已关闭（stale） | 无 |
| 低 | **#1223** （详见 4.2）Cowork 输入框硬编码中文；Agent 弹窗缺少 Escape 关闭及防重复点击 | 已关闭（stale） | 有（#1224，同样 stale） |

> ⚠️ 需特别注意：#1217（网关偶发重启）和 #1223/#1224（i18n 缺陷与修复）均因长时间无响应被自动关闭，但**问题本身可能仍然存在**，建议维护团队主动复查。


## 6. 功能请求与路线图信号

结合今日合入的 PR 和关闭的 Issue，可以捕捉到以下路线图信号：

- **隐私友好的分析能力（确定性信号）**：#2515/#2518 明确为 DSH 的启用开关与工作台打开增加了埋点，并特意将上报逻辑从主进程迁移至渲染进程。这表明团队在推进实验性功能的同时，重视用户隐私边界。
- **本地产物管理体验升级（确定性信号）**：#2513/#2514/#2517 合并展示了团队对「资料库/本地产物」模块的持续投入，尤其是分享文件名 Unicode 兼容、收藏交互即时反馈等细节打磨，预计该模块将是下一阶段用户感知最强的亮点之一。
- **无新功能请求提交**：今日无用户提出新功能需求。


## 7. 用户反馈摘要

今日无活跃的 Issue 评论互动，但结合近期关闭的问题仍可提炼出两条真实用户痛点：

1. **英文用户的 i18n 缺陷**（#1223）：`CoworkPromptInput` 将硬编码中文「输入文件」拼接进发送给 AI 的提示词，英文用户在使用含附件的消息时会看到中英混杂的提示词，严重影响非中文用户的体验一致性。这暴露了项目在 i18n 规范执行层面的疏漏。
2. **任务执行稳定性焦虑**（#1217）：网关偶发重启每天 3-5 次，用户特意附上了完整的日志压缩包，说明该问题已对其日常工作流造成了实质困扰。该问题从 4 月至今未获任何维护者响应，是当前社区信任度的一个负面信号。


## 8. 待处理积压

以下问题长期未获维护者响应，均已被 stale 机制自动关闭，但推测问题依然存在，建议项目团队重点关注并重新开放或跟进：

| 类型 | 编号 | 标题 | 创建时间 | 状态 | 说明 |
|---|---|---|---|---|---|
| Issue | **#1217** | 运行过程中偶发启动网关，影响正常使用 | 2026-04-01 | 已关闭（stale） | 稳定性缺陷，影响用户日常使用，**无任何维护者响应** |
| Issue | **#1223** | CoworkPromptInput 硬编码中文标签/i18n；Agent 弹窗缺少 Escape 关闭及防重复点击 | 2026-04-01 | 已关闭（stale） | 有修复 PR（#1224）但同样被 stale 关闭 |
| PR | **#1218** | fix(定时任务): 重构任务列表排序规则 | 2026-04-01 | 已关闭（stale） | 解决新建任务随机出现在列表中间的问题，价值明确，建议重新评估合入 |
| PR | **#1219** | perf(cowork): 消除会话列表和详情页的无效重渲染 | 2026-04-01 | 已关闭（stale） | 流式输出场景下的性能优化 |
| PR | **#1220** | perf(cowork): 消除 recentChats/conversationSearch 的 N+1 查询 | 2026-04-01 | 已关闭（stale） | 数据库查询性能优化，合并价值高 |
| PR | **#1215** | fix(im): always rebuild chat handler on setConfig | 2026-04-01 | 已关闭（stale） | 修复平台特定配置保存后 chat handler 未刷新的问题 |
| PR | **#1550** | fix(scheduledTask): 投递模式为「不通知」时去除 channel/to 字段 | 2026-04-07 | **OPEN**（唯一待合并 PR） | 修复会话创建的定时任务触发时网关报「Channel is required」错误，**已积压近 5 个月，建议优先处理** |

---

**项目健康度总结**：开发与发布节奏稳健、代码合并效率高，但存在明显的 **Issue/PR 响应延迟**问题 —— 多个月前的社区报告和高质量修复 PR 一直处于无人跟进状态，最终被 stale 机制自动关闭。这种「开发活跃、社区响应滞后」的状态，长期来看会影响社区的参与意愿，建议团队建立定期的积压清理与响应机制。

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

# Moltis 项目动态日报 — 2026-08-22

## 今日速览

项目过去24小时保持中等偏高活跃度：共新增/活跃 2 个 Issue，提交 8 个 PR（其中 7 个待合并，1 个已关闭）。今日 PR 集中在三大方向——WhatsApp 渠道功能补齐（文件持久化、Markdown 渲染）、Cron 调度正确性修复（active_hours 生效、定时输出路由）、以及安全加固（沙箱镜像请求校验、浏览器隐身模式默认开启）。值得关注的是，#1223（heartbeat active_hours 配置无效）与 #1208（heartbeat active_hours 修复 PR）形成前后呼应，表明维护者正在系统性修复调度模块的配置语义问题。社区侧有 1 个老牌 Windows 插件修复 PR（#468）时隔近5个月重新获得更新，可能预示着跨平台兼容性问题正在被重新审视。整体项目处于"多发 PR + 收敛 Bug"的良性迭代阶段。

---

## 版本发布

今日无新版本发布。

---

## 项目进展

今日无 PR 被合并，但 1 个 PR 被关闭（原因未知），其余 7 个仍处于待合并状态。

值得关注的是 #1220 [已关闭] `fix(whatsapp): render Markdown in outbound messages`（作者: rubenssoto）。该 PR 为 WhatsApp 出站消息增加 Markdown 至 WhatsApp 原生标记的转换能力，覆盖文本消息和媒体标题，同时保留会话历史与 Web UI 中的原始 Markdown。若关闭原因为合并，则 WhatsApp 连接器将获得显著的格式兼容性提升；若为关闭未合并，则需关注后续维护者的跟进说明。

其余 6 个待合并 PR 代表项目下一阶段的主要增量：

- **#1228** `fix(whatsapp): persist inbound files for local tools` — 将入站 WhatsApp 文件（图片/文档）持久化至会话媒体接口，为本地工具提供稳定的 `local_path`，并设 20 MB 上限和文件名消毒。
- **#1227** `fix(browser): enable Obscura stealth mode by default` — 默认启用 Obscura 防检测隐身模式，新增 `tools.browser.obscura_stealth` 配置项（默认 `true`）供运维按需关闭。
- **#1226** `fix(cron): deliver scheduled output to the originating chat` — 为定时任务新增 `deliver_to_current_chat` 临时路由方案，使输出自动回到触发任务的原始会话（含线程/话题路由）。
- **#1225** `fix(i18n): update and improve zh-TW Traditional Chinese locale` — 全面修订繁体中文翻译，大幅重写 `connectors.ts` 并统一术语和风格。
- **#1222** `fix(web): validate sandbox image requests` — 对沙箱镜像引用和包名增加校验，限制镜像构建和包检查权限至运维管理员。
- **#1208** `fix(cron): honor heartbeat active hours when the scheduler fires` — 修复 `heartbeat.active_hours` 从未生效的问题，追加 `heartbeat.active_hours` 规则到调度条件中（关联 #1205、#1223）。

综合来看，项目正朝三个方向纵深推进：**连接器成熟度**（WhatsApp 文件处理与格式化）、**调度可靠性**（定时任务的路由与时段控制）以及**安全默认值**（隐身模式、镜像校验）。

---

## 社区热点

今日讨论热度整体不高，2 个新 Issue 和 8 个 PR 均暂无评论。但有两个 PR 值得关注：

- **#468** `fix(plugins): use cmd.exe on Windows for shell hooks` — 该 PR 创建于 2026-03-23，近日（8月21日）重新获得更新。它在 Windows 上以 `cmd.exe /C` 替代 `sh -c` 执行 shell hooks，修复了 Windows 下插件机制不可用的问题，且已在 Windows 10 + moltis v0.9.10 环境实测通过。长期未合入的 PR 重新活跃，暗示维护者可能正在推进 Windows 平台支持相关的工作。链接：https://github.com/moltis-org/moltis/pull/468

- **#1208** `fix(cron): honor heartbeat active hours when the scheduler fires` — 该 PR 创建于 8月17日，对应 Issue #1205，与今日新提交的 Issue #1223 形成呼应。用户 Lstarsky0 同时是 Issue 提交者和 PR 作者，表明其发现 `active_hours` 逻辑完全未生效后，直接提交了修复代码。这类"用户自修"模式说明社区技术参与深度较高，但也侧面反映了项目在配置文档与实现一致性上的缺口。链接：https://github.com/moltis-org/moltis/pull/1208

---

## Bug 与稳定性

今日报告 2 个 Bug，均无现成修复 PR 关联（但其中一个有在途 PR）。按严重程度排列：

1. **中高 — heartbeat active_hours 配置完全失效**（#1223）
   - 影响：`heartbeat.active_hours` 无论用户如何设置（含默认 `start: "08:00", end: "24:00"`），都不会在任何时段抑制调度执行。`end: "24:00"` 处理逻辑存在解析顺序 bug，导致该窗口永远不生效。
   - 状态：已有 #1208 PR 在途修复（但该 PR 关联的是 #1205，覆盖面可能未完全包含 #1223 描述的边界情况，需维护者核实）。
   - 链接：https://github.com/moltis-org/moltis/issues/1223

2. **中 — 共享 Slack 频道中工具（Tools）停止工作**（#1224）
   - 影响：当 Moltis 被添加到共享 Slack 频道（跨组织）后，工具调用停止响应。涉及会话上下文或 Slack API 在共享频道的权限/事件差异，但 Issue 描述尚不完整（提交者未提供完整会话上下文）。
   - 状态：无关联 PR。
   - 链接：https://github.com/moltis-org/moltis/issues/1224

---

## 功能请求与路线图信号

今日无直接的新功能请求 Issue，但从 PR 中可以提炼出以下路线图信号：

1. **Windows 平台支持正在回归视野** — #468 的重新活跃暗示 Windows 下插件执行、shell hooks 兼容性有望在下一版本中修复。考虑到该 PR 已存在近 5 个月，若合入将显著改善 Windows 用户体验。链接：https://github.com/moltis-org/moltis/pull/468

2. **浏览器反检测能力正成为安全默认** — #1227 将 Obscura stealth 模式设为默认开启，表明项目对爬虫/自动化场景下被目标站点识别的风险正在采取更保守的默认策略。链接：https://github.com/moltis-org/moltis/pull/1227

3. **沙箱安全边界持续收紧** — #1222 对镜像引用和包名增加验证、限制管理员权限，延续了项目在沙箱逃逸防护方向的投资。链接：https://github.com/moltis-org/moltis/pull/1222

4. **本地化与国际化质量提升** — #1225（繁体中文全面修订）说明项目在非英语用户群体中已有实际使用反馈，正在打磨 UI 翻译质量。链接：https://github.com/moltis-org/moltis/pull/1225

---

## 用户反馈摘要

由于今日 2 个新 Issue 均无评论区讨论，以下基于 Issue 提交内容和关联 PR 提炼：

- **配置项语义困惑**（#1223）：用户 Lstarsky0 明确指出了一个"文档承诺与实际行为不一致"的问题——文档声称"midnight = always on until end of day"，但实际代码在 `end: "24:00"` 场景下解析顺序有误。这种"文档与实现脱节"的问题容易让用户在排查调度问题时走弯路。
- **共享频道集成受阻**（#1224）：用户在共享 Slack 频道中遇到工具停止工作的现象，且该用户已确认使用最新版本并搜索过已有 Issue。此类问题通常与 Slack 共享频道的权限边界（跨组织）相关，但当前 Issue 描述缺乏必要上下文，需要维护者引导补齐。
- **社区自修模式积极**（#1208 + #1223）：同一用户既报告了 Bug 又提交了修复 PR，说明社区中具备一定技术能力的用户愿意深度参与项目完善。但这也侧面提示，项目的配置校验和测试覆盖在 `active_hours` 这一功能点上存在盲区。

---

## 待处理积压

以下为长期未响应的关键 PR，提醒维护者关注：

- **#468** `fix(plugins): use cmd.exe on Windows for shell hooks` — 创建于 2026-03-23，已积压 152 天。修复 Windows 下 `sh -c` 不可用导致的插件 Hook 执行失败。已在 Windows 10 实测通过且 CI 正常。若长时间不合入，Windows 用户将持续受限。链接：https://github.com/moltis-org/moltis/pull/468

- **#1208** `fix(cron): honor heartbeat active hours when the scheduler fires` — 创建于 2026-08-17，已积压 5 天。修复 `heartbeat.active_hours` 从未生效的问题，与今日新报告 Issue #1223 形成关联。该 PR 的实现直接影响调度模块的核心语义，且已有社区用户跟进反馈，建议优先 review。链接：https://github.com/moltis-org/moltis/pull/1208

---

> 本报告基于 GitHub 公开数据自动生成，仅供参考。Issues/PRs 状态可能随时变化，请以 GitHub 页面为准。

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

好的，作为您的 AI 智能体与个人 AI 助手领域开源项目分析师，这是根据 CoPaw (github.com/agentscope-ai/CoPaw) 2026-08-22 的 GitHub 数据生成的日报。

---

# CoPaw 项目动态日报 - 2026-08-22

## 1. 今日速览
项目今日活跃度极高，处于密集迭代期。过去24小时内，Issue 与 PR 的更新总量达到 70 条，显示出社区参与度和开发速度都在提升。**值得注意**的是，新版本 (v2.1.1b2) 已通过 PR 发布，验证了开发流程的顺畅。今日的讨论焦点主要集中在 **稳定性修复**（如会话/工具/记忆问题）和 **用户体验优化**（如界面干扰、审批流程）两大方向，但尚未有针对这些问题的 fix PR 被合并，预期未来24-48小时会有集中修复动作。

## 2. 版本发布
**无正式 Release 发布。** 但值得注意的是，PR [#7200](https://github.com/agentscope-ai/QwenPaw/pull/7200) `chore: bump the version to v2.1.1b2` 已被合并，标志着 **v2.1.1-beta.2** 版本已准备就绪，预计很快会作为预发布版推出。

## 3. 项目进展
今日合并了 15 条 PR，主要围绕功能增强、测试修复和基础体验优化。

- **新版本就绪**: PR [#7200](https://github.com/agentscope-ai/QwenPaw/pull/7200) 发布 `v2.1.1b2` 版本，为下次迭代奠定基础。
- **平台能力扩展**: 新增了 **QwenPaw Hub** (PR [#7112](https://github.com/agentscope-ai/QwenPaw/pull/7112))，这是一个可选的自托管多用户控制平面，允许在本地账户中运行隔离的 QwenPaw 实例，是向企业级和多用户场景迈出的重要一步。
- **性能优化**: 合并了针对 Console 的优化 (PR [#7176](https://github.com/agentscope-ai/QwenPaw/pull/7176))，修复了长会话中流式更新同步解析 Markdown 导致的卡顿问题，大幅提升长对话的流畅度。
- **测试体系完善**: 一次性的重大修复 (PR [#7205](https://github.com/agentscope-ai/QwenPaw/pull/7205)) 解决了 Windows 集成测试覆盖率一直为 0% 的问题，并添加了 fail-closed 保护，确保了测试数据的有效性。这有助于提升项目健康度，防止回归。

## 4. 社区热点
今日讨论声量最大的 Issue 是 **[#6524](https://github.com/agentscope-ai/QwenPaw/issues/6524)【Bug】MCP 后端重启后客户端无法自动恢复**（6条评论）。该问题涉及 `streamable_http` 连接的 MCP Server 重启后 Session 失效，客户端无法自动恢复，需要手动执行命令才能重连。这反映出用户对 **MCP 集成的健壮性**和**自动恢复能力**有较高期望。

此外，今日还有多条新开的、获得较高评论的 Issue，反映用户在真实使用中的痛点：
- **[#6780](https://github.com/agentscope-ai/QwenPaw/issues/6780)【Question】2.0.1 版，不使用时几十分钟后自己会卡死**，指向了空闲状态下的稳定性问题。
- **[#7016](https://github.com/agentscope-ai/QwenPaw/issues/7016)【Bug】工具调用 404**，反映了流式会话中工具调用的可靠性问题。

## 5. Bug 与稳定性
今日报告的 Bug 主要集中在会话/工具管理、记忆系统、文件处理和桌面端稳定性几个方面。

**高优先级（需重点关注）**：
- **[#7206](https://github.com/agentscope-ai/QwenPaw/issues/7206)** (v2.1.1-beta.1): 手动 `/compact` 在特定配置 (`compact_threshold_ratio == 0.9`) 下总是失败，并报 `pydantic ValidationError`。这是一个明确的回归问题。
- **[#7210](https://github.com/agentscope-ai/QwenPaw/issues/7210)**: 工具配置全部启用，但会话的函数 schema 未注入，导致工具面的暴露不一致，这会严重影响 Agent 的工具调用。
- **[#7168](https://github.com/agentscope-ai/QwenPaw/issues/7168)** (已关闭): `history.db` 被 `recall_history` 的 expand 功能撑爆至 7.6GB，且同一区间重复落库，是严重的存储管理缺陷。
- **[#7193](https://github.com/agentscope-ai/QwenPaw/issues/7193)**: Agent 的会话记忆搜索出现错乱，搜索到了同一 Agent 其他会话的内容，导致行为异常。

**中优先级**：
- **[#7156](https://github.com/agentscope-ai/QwenPaw/issues/7156)**: embedding health check 超时导致向量召回降级。
- **[#6427](https://github.com/agentscope-ai/QwenPaw/issues/6427)**: WebView2 渲染进程在启动后约 7 秒崩溃（闪退），疑为前端代码变更触发。
- **[#7136](https://github.com/agentscope-ai/QwenPaw/issues/7136)**: 发送非 ASCII（中文）文件名时，文件卡片显示为百分号编码的乱码。
- **[#7199](https://github.com/agentscope-ai/QwenPaw/issues/7199)**: `daily_paper` 任务因 PDF 中的代理字符崩溃，导致任务失败。

**低优先级/环境相关**：
- **[#6430](https://github.com/agentscope-ai/QwenPaw/issues/6430)**: 桌面应用启动时后台卡顿约 85 秒。
- **[#7195](https://github.com/agentscope-ai/QwenPaw/issues/7195)**: 桌面模式对话窗口全屏后图标被遮挡。

## 6. 功能请求与路线图信号
用户提交了多项有价值的功能建议，其中一些已经有对应的 PR 正在开发中，很可能在近期版本中落地。

| 请求 | Issue 链接 | 对应 PR | 状态 |
| :--- | :--- | :--- | :--- |
| **会话级模型覆盖**：允许单个 Agent 在不同会话中使用不同 LLM | [#5992](https://github.com/agentscope-ai/QwenPaw/pull/5992) | PR [#5992](https://github.com/agentscope-ai/QwenPaw/pull/5992) | 待合并 |
| **会话作用域多项目目录**：一个聊天可绑定多个项目目录 | [#6976](https://github.com/agentscope-ai/QwenPaw/pull/6976) | PR [#6976](https://github.com/agentscope-ai/QwenPaw/pull/6976) | 待合并 |
| **按 Agent 统计 Token 用量**：让费用归属更清晰 | [#7207](https://github.com/agentscope-ai/QwenPaw/pull/7207) | PR [#7207](https://github.com/agentscope-ai/QwenPaw/pull/7207) | 待合并 |
| **优化工具调用/推理过程的显示体验**：提供开关选项，减少视觉干扰 | Issue [#7203](https://github.com/agentscope-ai/QwenPaw/issues/7203) & Issue [#7196](https://github.com/agentscope-ai/QwenPaw/issues/7196) | 无 | 待实现 |
| **优化会话审批模式**：减少对过程产物的审批干扰 | Issue [#7198](https://github.com/agentscope-ai/QwenPaw/issues/7198) | 无 | 待实现 |
| **自定义工具教程与支持**：用户不知道如何新增自定义 tool | Issue [#7204](https://github.com/agentscope-ai/QwenPaw/issues/7204) | 无 | 待实现 |
| **MCP 工具授权规则**：自定义频道无法被选中 | Issue [#7197](https://github.com/agentscope-ai/QwenPaw/issues/7197) | 无 | 待实现 |

## 7. 用户反馈摘要
- **满意度高点**：用户对项目的开发速度感到满意，多个长期存在的测试问题被修复，新增的 Hub 功能展现了项目的野心。用户对 Mac 平台的支持和文档改进（如新增 Mailbox 管理文档）也表达了积极反馈。
- **痛点与批评**：
    - **稳定性问题突出**：用户反映在长时间运行或特定操作后，应用会出现卡死（[#6780](https://github.com/agentscope-ai/QwenPaw/issues/6780)）、崩溃（[#6427](https://github.com/agentscope-ai/QwenPaw/issues/6427)）等问题，说明稳定性优化仍是重中之重。
    - **基础功能有明显缺陷**：关于「历史对话记录排序」（[#4816](https://github.com/agentscope-ai/QwenPaw/issues/4816)）的 Issue 被重新提及（虽然已关闭但评论再次活跃），反映出用户对此类基础体验的长期不满。用户认为“没有一个主流的 agent 产品像 qwenpaw 这样反人类设计”。
    - **可视信息干扰**：[#7203](https://github.com/agentscope-ai/QwenPaw/issues/7203) 和 [#7196](https://github.com/agentscope-ai/QwenPaw/issues/7196) 表明用户希望有更精细的控制权，特别是对推理过程和工具调用信息的显示，以提升工作时专注度。

## 8. 待处理积压
以下是在过去一段时间内持续活跃、但讨论热度有所下降且等待维护者处理的 Issue 和 PR。

| 类型 | 标识 | 标题 | 最后更新时间 | 状态 |
| :--- | :--- | :--- | :--- | :--- |
| **Issue** | [#6524](https://github.com/agentscope-ai/QwenPaw/issues/6524) | MCP 后端重启后客户端无法自动恢复 | 2026-08-21 | **OPEN** · 评论最多 |
| **Issue** | [#7016](https://github.com/agentscope-ai/QwenPaw/issues/7016) | 工具调用404 | 2026-08-21 | **OPEN** · 高活跃 |
| **Issue** | [#6427](https://github.com/agentscope-ai/QwenPaw/issues/6427) | WebView2 渲染进程崩溃（flashing crash）| 2026-08-21 | **OPEN** |
| **PR** | [#5992](https://github.com/agentscope-ai/QwenPaw/pull/5992) | Add per-session model overrides | 2026-08-21 | **OPEN** · 长时间未合并 |
| **PR** | [#6515](https://github.com/agentscope-ai/QwenPaw/pull/6515) | Add Volcengine Agent Plan & MiMo V2.5 providers | 2026-08-21 | **OPEN** · Under Review |
| **PR** | [#6399](https://github.com/agentscope-ai/QwenPaw/pull/6399) | Add reranker UI config panel | 2026-08-21 | **OPEN** · Under Review |

以上 PR 均已经持续一段时间（超过两周），希望维护者能重点关注，推动合并或给出明确反馈，以回应用户和贡献者的期待。

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# ZeroClaw 项目动态日报 — 2026-08-22

## 1. 今日速览

ZeroClaw 项目在过去24小时内保持高度活跃，共产生50条 Issue 更新和50条 PR 更新，其中新开/活跃 Issue 47条，待合并 PR 达48条，显示社区贡献意愿强烈。然而，今日**无新版本发布**，且大量高优先级 Issue（如安全策略绕过、预算上限失效）和巨型 PR（size:XL）仍处于待处理状态，合并速度明显滞后于提交速度。项目当前处于“高产出、低合并”的拥堵期，长期积压的 XS 和 XL 级 PR 同时等待处理，需要维护者优先疏通合并通道。值得注意的是，**涉及数据安全与隐私（S0级）的问题仍未被彻底关闭**，虽然相关 fix PR 已提交，但项目健康度整体仍有一定风险。

## 2. 版本发布

今日无新版本发布。

## 3. 项目进展

今日合并/关闭的 PR 数量较少（2条），但其中包含重要的安全修复；相关 Issue 关闭3条。

### 已合并/关闭的 PR

1. **fix(providers): redact Anthropic credential fragments** ([PR #10092](https://github.com/zeroclaw-labs/zeroclaw/pull/10092))
   - 由 Audacity88 提交，关闭了 Issue [#9976](https://github.com/zeroclaw-labs/zeroclaw/issues/9976)（S0级：停止记录 Anthropic 凭据片段）。该修复停止在调试事件中写入 `credential_head` 和 `credential_tail`，同时保留非机密诊断上下文（认证头和凭据长度），在安全性和可观测性之间取得平衡。
   - **影响评估**：修复了一个严重的安全漏洞，防止凭据片段泄露到日志中。

2. **zeroclaw-hardware fails to compile** ([Issue #9832](https://github.com/zeroclaw-labs/zeroclaw/issues/9832))
   - 该 Issue 被关闭，解决了 aarch64 Linux 下 `--features hardware` 编译失败的问题（未解析的导入 `aardvark_sys::AardvarkHandle`）。

### 整体进展评估

- 本项目今日**未关闭任何待合并的大型功能 PR**，合并进度有所停滞。>50% 的已合并/关闭 PR 来自安全修复，但没有新的功能特性和大的架构推进被合并。
- 社区有大量大型 PR（如 [#10142](https://github.com/zeroclaw-labs/zeroclaw/pull/10142) ZeroRelay 安全传输、[#10146](https://github.com/zeroclaw-labs/zeroclaw/pull/10146) 激活逻辑通道实例、[#10155](https://github.com/zeroclaw-labs/zeroclaw/pull/10155) SOP 运行日志）等待合并，核心功能推进处于停滞。

## 4. 社区热点

### Issue 热点

1. **Issue #9965 — runtime-written executable test fixtures hit ETXTBSY** ([Issue #9965](https://github.com/zeroclaw-labs/zeroclaw/issues/9965))
   - **评论数：7** | 优先级: p1 | 状态: in-progress
   - 该问题涉及并行运行时测试门下的 ETXTBSY 错误，已获维护者确认并标记为“进行中”，表明**测试基础设施的并发稳定性问题**正在影响开发的确定性。社区对此高度关注，可能是由于它阻塞了 CI 的稳定性。

2. **Issue #9815 — forbidden_paths is unreachable for any path under allowed_roots** ([Issue #9815](https://github.com/zeroclaw-labs/zeroclaw/issues/9815))
   - **评论数：5** | 优先级: p1 | 风险: high
   - 安全策略中 `forbidden_paths` 完全失效的问题。社区讨论的热点在于**该问题是否影响生产环境的沙箱隔离效率**。虽已有初步讨论，但该问题尚无对应的打开 PR，表明安全策略的修复需要更谨慎的验证。

3. **Issue #10059 — Support Option-Backspace word deletion in ZeroCode text inputs** ([Issue #10059](https://github.com/zeroclaw-labs/zeroclaw/issues/10059))
   - **评论数：3** | 优先级: p3 | 状态: in-progress
   - 用户强烈要求 ZeroCode 支持 macOS 的 Option-Backspace 快捷键。社区活跃度较高，**已有一个 opened PR ([#10078](https://github.com/zeroclaw-labs/zeroclaw/pull/10078)) 被标记为待处理**，同时也有两个重复的自动化 “Fix #10059” PR 被提交——说明贡献者试图绕过人工审查流程（详见图 5 分析）。

### PR 热点

所有 PR 今日评论数均为 0（或未公开），但以下 PR 因体积大、涉及面广而受关注：

1. **PR #10142 — feat(zerorelay): secure transport and browser enrollment frontdoor** ([PR #10142](https://github.com/zeroclaw-labs/zeroclaw/pull/10142))
   - 由 JordanTheJet 提交，是一个 size:XL 的巨型 PR，将远程 WSS 平面变为强制的双向 TLS，并引入 `zerorelay` 盲转发器。该 PR 取代了 #9080，预计将大幅提升 ZeroClaw 的远程拓扑安全性，但合并前需要重点审查。

2. **PR #10146 — feat(plugins): activate logical channel instances** ([PR #10146](https://github.com/zeroclaw-labs/zeroclaw/pull/10146))
   - 同样是 size:XL，重新实现了 #8852 的通道激活切片。此功能将推动逻辑通道实例在 daemon 层面的构筑，是插件体系的关键一环。

**社区诉求总结**：开发者对**安全策略的强化**（如定时清除工具、通道鉴权）和**开发体验改进**（如 ZeroCode 快捷键、macOS 惯例支持）比较关注。此外，**CI 超时和可观测性**（Issue #10042、#10040）也是社区热点。

## 5. Bug 与稳定性

| 严重程度 | Issue 链接 | 标题 | 风险 | 状态 | 是否已有修复 PR |
|---|---|---|---|---|---|
| S0 - 数据丢失/安全风险 | [Issue #9947](https://github.com/zeroclaw-labs/zeroclaw/issues/9947) | cron 工具未按代理隔离，任何代理可读/改/删其他代理任务 | high | in-progress | 无 |
| S0 - 数据丢失/安全风险 | [Issue #9855](https://github.com/zeroclaw-labs/zeroclaw/issues/9855) | Matrix 频道无法通过 `.well-known` 委派解析 homeserver | high | in-progress | 无 |
| S0 - 数据丢失/安全风险 | [Issue #9976](https://github.com/zeroclaw-labs/zeroclaw/issues/9976) | Anthropic 凭据片段写入日志 | high | **已关闭** | ✅ [PR #10092](https://github.com/zeroclaw-labs/zeroclaw/pull/10092) |
| S1 - 工作流阻塞 | [Issue #10061](https://github.com/zeroclaw-labs/zeroclaw/issues/10061) | 被提供方拒绝的图像会污染后续对话轮次 | high | accepted | 无 |
| S1 - 工作流阻塞 | [Issue #10042](https://github.com/zeroclaw-labs/zeroclaw/issues/10042) | CI 系统依赖安装可能耗尽作业超时 | medium | in-progress | 无 |
| S1 - 工作流阻塞 | [Issue #9946](https://github.com/zeroclaw-labs/zeroclaw/issues/9946) | agent-browser 子进程等待未设上限，可能无限挂起 | high | in-progress | 无 |
| S2 - 行为降级 | [Issue #9816](https://github.com/zeroclaw-labs/zeroclaw/issues/9816) | Anthropic 提供商报告 $0.00 消费，预算上限永不触发 | high | in-progress | 无 |
| S2 - 行为降级 | [Issue #9872](https://github.com/zeroclaw-labs/zeroclaw/issues/9872) | 委托代理解析文件系统到委托方而非自己的工作区 | high | accepted | 无 |
| S2 - 行为降级 | [Issue #9929](https://github.com/zeroclaw-labs/zeroclaw/issues/9929) | 无头 SOP 步骤回合未持久化到会话存储 | high | blocked | 无 |
| S2 - 行为降级 | [Issue #10058](https://github.com/zeroclaw-labs/zeroclaw/issues/10058) | ZeroCode 文件资源管理器搜索模式忽略行/页导航 | low | in-progress | ⚠️ 有重复的低质量 PR（[#10227](https://github.com/zeroclaw-labs/zeroclaw/pull/10227) 等） |
| S3 - 轻微 | [Issue #9983](https://github.com/zeroclaw-labs/zeroclaw/issues/9983) | 无视觉后备模型错误报告原因 | medium | in-progress | 无 |

**稳定性总结**：安全类 S0 问题仍有两项悬而未决（cron 跨代理访问控制、Matrix 域名委派），需要重点关注。新增的高关注点是 **CI 基础设施的稳定性短板**（超时、资源限制），反映在 #10042 和 #10040 上。

## 6. 功能请求与路线图信号

1. **按角色授权 Discord 成员（而不是仅限用户ID）** ([Issue #9970](https://github.com/zeroclaw-labs/zeroclaw/issues/9970))
   - 高需求，优先级 p2，当前 in-progress。已获维护者接受。与多代理/团队协作场景关系密切。

2. **QwenCloud 提供商体验升级** ([Issue #9943](https://github.com/zeroclaw-labs/zeroclaw/issues/9943))
   - 后向兼容的 DashScope/Qwen 提供商升级，目前状态 accepted。对国内用户是重要接入点。

3. **CI 基础设施改进** ([Issue #10040](https://github.com/zeroclaw-labs/zeroclaw/issues/10040))
   - 恢复 fork PR 的 Lint 超时余量。项目依赖 Blacksmith 8-vCPU 运行器，fork 的 PR 无法使用，导致超时。已有对应 PR ([#10174](https://github.com/zeroclaw-labs/zeroclaw/pull/10174)) 尝试在原生运行器上验证发布工具。

4. **SOP 运行日志与触发去重** ([PR #10155](https://github.com/zeroclaw-labs/zeroclaw/pull/10155))
   - 为 SOP 添加可互操作的运行日志和触发器去重功能。这是一个大型 PR（size:L），如果能合并，将为可观测性层增加很多价值。

**下一版本可能纳入**：从 PR 的活跃度和成熟度判断，`feat(sop): add interoperable run logs and trigger deduplication` ([PR #10155](https://github.com/zeroclaw-labs/zeroclaw/pull/10155)) 和 `fix(acp): persist interrupted turn progress` ([PR #10197](https://github.com/zeroclaw-labs/zeroclaw/pull/10197)) 有较大可能被合入。SOP 可观测性是社区持续关注的痛点（相关 Issue #9805、#9783 等），该 PR 将缓解多方面的运维问题。

## 7. 用户反馈摘要

**正面反馈**

- 用户高度认可 ZeroClaw 在可观测性和渠道网关方面的持续改进，特别是日志、追踪和运行状态可视化相关的功能推进。
- 对 **macOS 用户体验的重视**（Option-Backspace、Option-Left/Right）获得了社区点赞，期待尽快上线。

**主要痛点**

1. **超时与挂起问题频发**：多个用户报告了不同层面的挂起问题——`agent-browser` 子进程无超时挂起（#9946）、后台任务永远显示 running（#9805）、无头 SOP 从不执行（#9805）。这表明运行时和工具执行的**可靠性**是用户最关心的问题。
   - 案例：[Issue #9946](https://github.com/zeroclaw-labs/zeroclaw/issues/9946) 评论中开发者反馈：*“A wedged CLI hangs the agent turn indefinitely”*（一个卡死的 CLI 会让代理回合无限挂起）

2. **计费/预算不透明**：Anthropic 提供商预算记录 $0.00 导致预算控制形同虚设（#9816）。企业用户尤其关注成本管控，这是影响采用的关键因素。

3. **多代理隔离机制缺陷**：cron 任务（#9947）和委托代理（#9872）的作用域混乱，在部署需要严格职责分离的用户群体中引发了担忧。

4. **配置错误被静默忽略**：恶意格式的 `SOP.toml` 被静默丢弃（#9786），`POST /api/cron` 静默存储无效的 session_target（#10037），用户在排查问题时难以定位根因。

**渠道侧反馈**：Discord 用户希望按角色而非仅用户 ID 授权（#9970），Matrix 用户则受困于无法解析 homeserver 域名（#9855）。

## 8. 待处理积压

### 长期未关闭的重要 Issue

1. **[Issue #9805](https://github.com/zeroclaw-labs/zeroclaw/issues/9805)** (SOP auto-mode 从不执行) — p1，创建于 2026-08-07，至今**15天**未关闭，虽已被标记 in-progress。与此相关联的 #9929（无头回合不持久化）和 #9783（失败原因被丢弃）也仍打开。

2. **[Issue #9816](https://github.com/zeroclaw-labs/zeroclaw/issues/9816)** (Anthropic 预算 $0.00) — p1，创建于 2026-08-07，**15天**未关闭，导致预算控制失效。这是面向企业用户的关键功能。

3. **[Issue #9855](https://github.com/zeroclaw-labs/zeroclaw/issues/9855)** (Matrix 域名委派) — p1，S0 风险，创建于 2026-08-09，**13天**未关闭且无对应 PR。

### 长期未合并的大型 PR

1. **[PR #9678](https://github.com/zeroclaw-labs/zeroclaw/pull/9678)** (强化 Git shell 策略参数) — size:XL，等待作者操作，创建于 2026-08-02，已 **20天**。安全策略类的大型重构，需要作者响应用户反馈。

2. **[PR #9110](https://github.com/zeroclaw-labs/zeroclaw/pull/9110)** (Lark 常量时间比较) — size:XS，待维护者审查，创建于 2026-07-17，已 **36天**。虽然小型且安全相关，但长期被忽略，暗示维护者对近期批量安全修复的审查有积压。

3. **[PR #10015](https://github.com/zeroclaw-labs/zeroclaw/pull/10015)** (硬件数据表下载限制) — 标记 `do-not-merge`，创建于 2026-08-15，待维护者审查。可能由于风险较高需要更长时间评估。

### 周期提醒

Issue #9947（cron 跨代理安全）优先级为 p1，风险为 S0，但**尚未分配任何 PR**，需要维护者立即关注。

---

*本报告基于 zeroclaw-labs/zeroclaw 公开数据生成，数据截至 2026-08-22。*

</details>

---
*本日报由 [agents-radar](https://github.com/kky-wollu/agents-radar) 自动生成。*