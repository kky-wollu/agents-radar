# OpenClaw 生态日报 2026-08-15

> Issues: 500 | PRs: 500 | 覆盖项目: 13 个 | 生成时间: 2026-08-14 22:28 UTC

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

# OpenClaw 项目动态日报 — 2026-08-15

> 数据来源：github.com/openclaw/openclaw 公开仓库活跃数据（截至 2026-08-15 00:00 UTC）


## 1. 今日速览

过去 24 小时，OpenClaw 仓库维持了**极高的社区活跃度**：共产生 500 条 Issue 更新和 500 条 PR 更新，其中新开/活跃 Issue 491 条，待合并 PR 402 条。**值得警惕的是，今日合并/关闭的 PR 仅 98 条（约 19.6%），代码合并速度远低于提交速度，维护者审查积压正在加剧。** 新版本发布数为 0。Issue 侧呈现出明显的"老问题长期悬而未决"特征——评论数最高的多个 Issue（#121058、#44925、#91588）均为数周甚至数月前报告、至今未关闭的顽固 Bug；而 PR 侧则出现了一波来自 `vyctorbrzezowski` 和 `steipete` 两位核心贡献者的大规模 UI 重构与 Gateway 稳定性补丁浪潮（单日各自提交 6-8 个 PR），表明项目正在同时推进**前端体验统一**与**后端 Worker 架构加固**两条主线。总体来看，项目功能迭代活跃，但**稳定性债务（尤其是会话状态丢失、消息静默失败、内存泄漏）已成为社区最强烈的呼声，可能对用户信任构成实质性风险。**


## 2. 版本发布

过去 24 小时内无新版本发布（Releases: 0）。下一版本动态需关注 PR 合并节奏及维护者发布计划。


## 3. 项目进展

今日合并/关闭 98 个 PR，虽数量有限，但其中包含多项关键修复，值得注意的已合并/关闭项包括：

| PR | 标题 | 状态 | 意义 |
|----|------|------|------|
| [#116489](https://github.com/openclaw/openclaw/pull/116489) | feat(security): require acknowledgement for install policy warnings | 已关闭 | 安全策略确认机制落地，为高危插件安装增加人工确认环节，提升安全边界 |
| [#123861](https://github.com/openclaw/openclaw/pull/123861) | fix(ci): invalidate plugin SDK declarations on auth changes | 已关闭 | 修复 CI 边界检查反复失败的问题，保障插件 SDK 类型声明的正确性 |

**核心趋势**：今日活跃的 PR 中，UI 重构（`vyctorbrzezowski` 的 8 个 PR）和 Gateway/Worker 稳定性加固（`steipete` 的 6 个 PR）构成两大主力，但多数仍处于 `waiting on author` 或 `ready for maintainer look` 状态。一个值得关注的新模式是 **cloud workers for codex runtime**（[#123743](https://github.com/openclaw/openclaw/pull/123743)），该 PR 解除了云 Worker 对 OpenClaw 运行时（runtime）的硬性限制，允许 Codex harness 用户使用云执行，若被合并将显著扩展产品适用面。


## 4. 社区热点

**最热 Issue（94 条评论）**：
- [#121058](https://github.com/openclaw/openclaw/issues/121058) [OPEN] Silent reply failures still recurring after #116277 closed — no queued reply payload
  - 用户 `sloptop-the-terrible` 报告：静默回复失败在 #116277 关闭后**仍在持续发生**，监控 cron 持续记录到新故障。该问题创建仅 6 天即获 94 条评论，说明大量用户都受此问题困扰。
  - 热点原因：具备**可自动检测的监控手段**，用户能明确感知问题是否复发；而该项目其它神级 issue 往往"关了就完了，但问题还在"。

**高赞 Issue**（反映社区共同诉求）：
- [#108435](https://github.com/openclaw/openclaw/issues/108435)（👍 3）:更新至 2026.7.1 后 Gateway 无法启动，涉及 systemd/ollama/手动三种启动方式，影响面广。
- [#38327](https://github.com/openclaw/openclaw/issues/38327)（👍 3）:google-vertex/gemini-3.1-pro-preview 报 "Cannot convert undefined or null to object"。
- [#13219](https://github.com/openclaw/openclaw/issues/13219)（👍 1）:请求提供 Per-model 使用量日志以支持成本核算。

**核心诉求提炼**：社区已从"能不能加新功能"转向**"能不能让我稳定地用下去"**——大量的高评论 Issue 集中在**静默丢失消息、会话状态损坏、内存泄漏导致 OOM**这三类"隐形数据安全"问题上。


## 5. Bug 与稳定性

今日活跃的 Bug/回归问题中，以下问题需优先关注。按严重程度排序：

### P0（致命/数据安全）

| Issue | 问题 | 现状 |
|-------|------|------|
| [#91588](https://github.com/openclaw/openclaw/issues/91588) | **Gateway 内存泄漏**：RSS 从 350MB 涨至 15.5GB 后 OOM，反复重启 | 已持续 2 个月+，无 fix PR |
| [#108435](https://github.com/openclaw/openclaw/issues/108435) | **2026.7.1 更新后 Gateway 无法启动**，三种启动方式均失败 | 无 fix PR |
| [#119270](https://github.com/openclaw/openclaw/issues/119270) | **文件工具剥离目标路径开头的 @ 符号**，静默写入/删除错误文件 | 数据损坏风险，无 fix PR |

### P1（严重功能损坏）

| Issue | 问题 | 现状 |
|-------|------|------|
| [#121058](https://github.com/openclaw/openclaw/issues/121058) | 静默回复失败在 #116277 修复后**复发**，无队列回复负载 | 94 评论，无 fix PR |
| [#44925](https://github.com/openclaw/openclaw/issues/44925) | 子代理完成结果静默丢失（超时无重试/无通知/无自动重启） | 5 个月未关闭，无 fix PR |
| [#62505](https://github.com/openclaw/openclaw/issues/62505) | **编码代理完全无法完成任务**（2026.4.2 之前正常，现为回归） | 4 个月未关闭 |
| [#86215](https://github.com/openclaw/openclaw/issues/86215) | Codex OAuth 刷新失败导致代理数小时无响应，无告警 | 无 fix PR |
| [#87109](https://github.com/openclaw/openclaw/issues/87109) | Gateway 堆内存空闲时持续增长至 1073MB+，cron 任务静默失败 | 无 fix PR |
| [#120563](https://github.com/openclaw/openclaw/issues/120563) | 自定义/Ollama Provider 不发送对话历史，每轮固定大小上下文，**严重限制场景** | 无 fix PR |

### 值得注意的新增 Bug（近 7 天内创建）

| Issue | 问题 | 现状 |
|-------|------|------|
| [#121058](https://github.com/openclaw/openclaw/issues/121058) | 静默回复失败复发（已列入 P1） | 94 评论 |
| [#121083](https://github.com/openclaw/openclaw/issues/121083) | SecretRef `provider: "default"` 隐式内建别名未在文档中说明，用户配置报错 | 有一个清洁修复 PR 待处理 |
| [#121046](https://github.com/openclaw/openclaw/issues/121046) | `temporalDecay` 不适用于 memory/dreaming/ 子目录下的日期文件 | 已有 linked PR 开放 |

**稳定性判断**：严重 Bug 的 **fix PR 覆盖率极低**——上表中 12 项 P0/P1 问题仅 2 项有 linked PR，且均为"待审查"状态。结合 98/500 的合并率，**维护者在 Bug 修复上的响应速度已明显落后于社区预期**，这是当前项目健康度最大的隐患。


## 6. 功能请求与路线图信号

结合近期（7-8 月）活跃 PR 与 Issue，以下功能需求可能被纳入后续版本：

| 功能/改进 | 参考 Issue/PR | 信号强度 | 说明 |
|-----------|---------------|----------|------|
| **Cloud workers for codex runtime** | PR [#123743](https://github.com/openclaw/openclaw/pull/123743) | ★★★ 强，已有实现 | 解除 Cloud Worker 对 OpenClaw 运行时的硬限制，扩展 Codex 用户使用云执行的能力 |
| **Telegram 复制文本按钮** | PR [#123837](https://github.com/openclaw/openclaw/pull/123837) | ★★★ 强，已有实现 | 支持一键复制富文本消息中的代码/ID/Token，提升 Telegram 交互便捷性 |
| **每模型使用量日志** | Issue [#13219](https://github.com/openclaw/openclaw/issues/13219) | ★★☆ 中，需求稳定 | 社区长期请求，便于成本追踪与模型混合优化 |
| **动态模型发现（OpenRouter）** | Issue [#10687](https://github.com/openclaw/openclaw/issues/10687) | ★★☆ 中，已获 3 👍 | 支持快速变化的模型目录，减少静态模型列表维护成本 |
| **Slack Modal 支持** | Issue [#88154](https://github.com/openclaw/openclaw/issues/88154) | ★★☆ 中 | 结构化表单输入，提升 Slack 工作流交互能力 |
| **反应触发代理轮次** | Issue [#17840](https://github.com/openclaw/openclaw/issues/17840) | ★☆☆ 弱 | Emoji 投票、快捷操作等交互模式 |
| **Slack Modal / Mattermost 进程隔离** | PR [#120854](https://github.com/openclaw/openclaw/pull/120854) | ★★☆ 中，已有实现 | 将进展帖与最终回复隔离，避免刷屏（Mattermost 先行，Slack 可参考） |

**路线图信号**：UI 侧，`vyctorbrzezowski` 的系列 PR 表明官方正在对 Web UI 进行系统性重构（侧边栏图标/排版/信息密度），下一个版本 UI 将有明显变化；后端侧，`steipete` 集中修复 Worker 生命周期、调度一致性与传输清理问题，说明 **Worker 架构正在经历内部加固期**，目标可能是为 Cloud Workers 铺路。


## 7. 用户反馈摘要

**积极反馈**（来自近期 Issue/评论）：
- [#73537](https://github.com/openclaw/openclaw/issues/73537) 用户 `Reneb-cafe` 表示："Thank you for OpenClaw. We've been running it as a family and business assistant (Telegram integration, automations, cron jobs, Home Assistant control) and it has genuinely become part of our daily workflow." —— **说明 OpenClaw 在真实生产环境（家庭+小型商业）中已被深度依赖**。

**核心痛点**（按出现频次排序）：

1. **静默失败问题**（出现 3+ 次）——用户最反感的是"代理显示正常，但消息产出/投递消失，且无任何错误提示"。典型例子：#121058（静默回复失败复发）、#91892（cron 任务在 AI 调用时卡死无输出）、#87109（cron 任务静默失败）。

2. **升级/回滚后遗症**（出现 3 次）——#92241（滚动回滚后进程持有旧模块路径导致消息静默丢弃）、#94939（6.x 状态迁移致 SQLite 空文件）、#108435（2026.7.1 Gateway 启动失败）。**用户对升级风险的恐惧正在累积**。

3. **多代理/多运行时一致性问题**（出现集中）——#120563（自定义 Provider 不携带对话上下文）、#98702（子代理继承 OAuth 被拒）、#86214（Codex app-server 客户端中途关闭）。

4. **长期未决问题的挫败感**——用户反复在 #121058 等 Issue 下追问修复进展，而维护者响应节奏远远落后于用户预期。


## 8. 待处理积压

以下为长期未解决、已严重影响用户体验或存在数据安全风险的历史遗留 Issue/PR：

| 编号 | 标题 | 首次报告 | 持续时长 | 状态及影响 |
|------|------|----------|----------|------------|
| [#44925](https://github.com/openclaw/openclaw/issues/44925) | 子代理完成结果静默丢失，超时无重试/重启 | 2026-03-13 | **5 个月** | 影响 Telegram 论坛机器人场景，无法感知任务状态 |
| [#62505](https://github.com/openclaw/openclaw/issues/62505) | 编码代理完全无法完成任务（回归） | 2026-04-07 | 4 个月 | 核心编码场景不可用，用户已升级为 P1 |
| [#91588](https://github.com/openclaw/openclaw/issues/91588) | Gateway 内存泄漏至 OOM（P0） | 2026-06-09 | 2 个月+ | 导致反复崩溃及 cron 任务静默失败 |
| [#38327](https://github.com/openclaw/openclaw/issues/38327) | 2026.3.2 起 google-vertex/gemini 模型无法使用 | 2026-03-06 | 5 个月 | 特定模型全家不可用 |
| [#96834](https://github.com/openclaw/openclaw/issues/96834) | WhatsApp 图片卡住主通道 ~3 分钟（P1） | 2026-06-25 | 6 周 | 多模态场景阻断 |

**维护者提醒**：上述 5 项均为 P0/P1 且已持续 2 个月以上，且全部仍处于 `clawsweeper:needs-maintainer-review` 状态。以当前合并速度计算，即便今天全部指派，也需要至少 2-3 周才能完成审查与合入。建议维护者考虑：
1. 优先对 #91588（内存泄漏）与 #44925（子代理丢失）进行**热修复版本发布**；
2. 为 #62505（编码代理回归）安排专项复现与根因定位；
3. 在 6.x 向 7.x 演进中，为升级迁移路径提供**更充分的自动检测与回滚保护**（参考 #94939 教训）。

---

*本日报由 AI 分析师基于 GitHub 公开数据自动生成，数据截止时间为 2026-08-15 00:00 UTC。*

---

## 横向生态对比

# 个人 AI 助手开源生态横向对比分析报告

**报告日期：2026-08-15**
**分析范围：** OpenClaw、NanoBot、Hermes Agent、PicoClaw、NanoClaw、NullClaw、IronClaw、LobsterAI、TinyClaw、Moltis、CoPaw、ZeptoClaw、ZeroClaw


## 1. 生态全景

个人 AI 助手/自主智能体开源生态正处于**从“功能拓展”转向“可靠性优先”的关键转折期**。头部项目（OpenClaw、IronClaw、Hermes Agent）日 PR 数量在 40-500 条的高位区间，但普遍面临合并速率低于提交速率、P0/P1 级 Bug 修复覆盖率不足 20% 的“稳定性债务”压力。社区最强烈的共同呼声已从“能不能加新功能”转向三个核心词：**静默失败（silent failure）、会话一致性（session consistency）、跨平台兼容性（cross-platform compatibility）** 。与此同时，二线项目（NanoBot、LobsterAI、CoPaw）运维效率更高（关闭率 76%-100%），中小项目（NullClaw）则在基础设施灵活性上深耕。整体来看，生态已跨越“demo-ready”门槛，正集体面向 **“生产环境可用性”** 发起攻坚。


## 2. 各项目活跃度对比

| 项目 | Issues 更新 | PR 更新 | 合并/关闭 PR | 新版本 | 健康度评估 |
|------|------------|---------|-------------|--------|-----------|
| **OpenClaw** | 500（新开491） | 500 | 98（19.6%） | 0 | ⚠️ 高风险：活跃度极高但合并率极低，12项P0/P1仅2项有fix PR，稳定性债务累积 |
| **Hermes Agent** | 50（30活跃/20关闭） | 50（45待合并） | 5 | 0 | ⚠️ 高活跃但积压明显：45条PR待合并，无合并发生，桌面端P1 Bug无fix |
| **IronClaw** | 25（16新开） | 48 | 23（48%） | ✅ v1.2.0 | 🟢 健康：发布节奏明确，Bug→fix PR转化快，QA流程有效运转 |
| **ZeroClaw** | 33 | 50 | 3 | 0 | 🟡 活跃但技术债累积：多个已接受RFC未落地，测试不稳定阻塞CI |
| **LobsterAI** | 2 | 27 | 22（81%） | ✅ 2026.8.14 | 🟢 健康：合入效率高，Issue侧响应滞后（4个月未处理项） |
| **CoPaw** | 50（38关闭） | 41 | 0 | 0 | 🟡 中等：关闭率76%反映维护响应好，但核心PR评审慢（#5992积压34天） |
| **NanoBot** | 3 | 23 | 8（35%） | 0 | 🟢 健康：Bug响应快（当日闭环），社区活跃维持高 |
| **PicoClaw** | 1活跃/2关闭 | 3待合/5关闭 | 5 | 0 | 🟢 稳定：核心Bug已有修复PR，stale机制清理积压 |
| **NanoClaw** | 2（新开） | 9 | 3 | 0 | 🟢 健康：Bug响应快，供应链安全加固（签名验证链路） |
| **NullClaw** | 0 | 1 | 1 | 0 | 🟢 稳定但低活跃：基础设施小幅推进（SQLite路径可配置） |
| **Moltis** | 0 | 1（待合） | 0 | 0 | 🟢 稳定：低活跃，大型PR #1190等待评审 |
| **TinyClaw** | — | — | — | — | ⚪ 无活动 |
| **ZeptoClaw** | — | — | — | — | ⚪ 无活动 |


## 3. OpenClaw 在生态中的定位

**社区规模与影响力：** OpenClaw 以日均 500 条 Issue + 500 条 PR 的量级遥遥领先所有竞品（第二名 IronClaw 仅 25+48），是生态中**绝对的用户规模头部**。其个人/家庭/小型商业场景的深度渗透（用户“家庭+企业双助理”案例）反映了其作为**通用型前端**的生态位优势。

**技术路线差异：**
- **Gateway + Worker 架构**是 OpenClaw 的核心技术标识，但这也成为当前主要痛点源（内存泄漏、静默失败、Worker 生命周期不稳定）。对比 IronClaw 的 Rust 实现，OpenClaw 在多运行时一致性上承压更大。
- 当前正推进 **Cloud Workers for Codex runtime**（#123743），试图解除运行时限制，方向正确但可能进一步扩大技术面。

**核心短板：** 合并节奏严重滞后（今日仅 19.6%），P0/P1 修复覆盖不足 17%，12 项严重 Bug 仅 2 项有 fix PR。**社区信心在持续消耗**——高频“复发类”问题（#121058）正向用户传达“修复不彻底”的信号。若此趋势不扭转，用户可能向 IronClaw（Rust 性能优势）或 NanoBot（社区响应快）迁移。


## 4. 共同关注的技术方向

| 技术方向 | 涉及项目 | 具体诉求 |
|---------|---------|---------|
| **静默失败/消息丢失** | OpenClaw（#121058 94评论）、NanoBot（#5391）、Hermes（#67442）、IronClaw（#6879） | 代理状态看似正常但消息/结果丢失且无提示，用户普遍要求“显式错误优于静默吞掉” |
| **会话状态一致性** | OpenClaw（#44925子代理丢失）、NanoBot（#5271 p0）、Hermes（#67442跨进程）、CoPaw（#7011身份串线） | 跨进程/跨设备/多会话场景下状态同步与隔离 |
| **MCP 生态兼容与稳定性** | PicoClaw（#3269挂起26天）、IronClaw（#7626认证卡死）、CoPaw（#6958重复写入）、ZeroClaw（#10002） | MCP 认证流程、连接失败容错、结果一致性 |
| **安装/升级体验** | NanoClaw（#3248 Node检测漏洞、#3245 AVX2）、Hermes（#86223桌面更新崩溃）、OpenClaw（#108435升级后无法启动） | 安装脚本健壮性、升级回滚保护、预构建产物兼容性 |
| **Windows 兼容性** | NanoBot（#5382 PermissionError）、NanoClaw（#3246容器清理）、ZeroClaw（#7462 74测试失败）、IronClaw（Windows修复合入） | Windows 平台长期是短板，多项目在补课 |


## 5. 差异化定位分析

| 项目 | 功能侧重 | 目标用户 | 技术架构 | 核心差异 |
|------|---------|---------|---------|---------|
| **OpenClaw** | 通用型多平台助手（Telegram/WhatsApp/Home Assistant） | 家庭/小型商业用户 | Node.js Gateway+Worker | 生态最广，但稳定性承压 |
| **IronClaw** | 自动化可靠性、MCP 深度集成 | 开发者/企业自动化 | Rust（性能导向） | 发布纪律最优，自动化可靠性为当前核心（#6879 五子任务） |
| **Hermes Agent** | 桌面端（Win/macOS）+ 多 Provider + i18n | 桌面重度用户/多语言用户 | Python（session DB 插件钩子） | 桌面端体验与本地化是差异化点 |
| **NanoBot** | WebUI 体验 + 技能市场 | 轻量级个人用户 | Python | 社区反馈闭环快（Bug当日修复） |
| **CoPaw** | 多渠道（飞书等中国渠道）+ 插件 | 跨时区/多UI用户 | agentscope 框架 | 中国渠道（飞书）是独特优势 |
| **LobsterAI** | cowork 协作 + OpenClaw 技能兼容 | 网易生态/技能开发者 | TypeScript | 与 OpenClaw 技能生态绑定 |
| **PicoClaw** | 嵌入式/低资源设备 | 极客/硬件爱好者 | Go（<10MB RAM） | 资源占用极小是其护城河 |
| **NanoClaw** | 自托管/容器化 | NAS/软路由用户 | Node+Bun 容器化 | 供应链安全（签名验证）投入显著 |
| **NullClaw** | 基础设施灵活性 | 容器化/CI 场景 | SQLite 存储引擎 | 面向受限环境部署 |
| **Moltis** | 数据集成（日历/邮件连接器） | 需要多渠道数据同步 | 供应商无关持久化层 | 专注数据管道而非对话 AI |
| **ZeroClaw** | 安全架构 + OpenAI 兼容 | 开发者/平台构建者 | 兼容层设计 | 安全策略精细化是一个方向 |


## 6. 社区热度与成熟度分层

**第一梯队：高速迭代期（日 PR > 40）**
- OpenClaw（500 PR）、Hermes Agent（50）、IronClaw（48）、ZeroClaw（50）、CoPaw（41）
- 共同特征：功能推进快但合并瓶颈明显，稳定性债务伴随增长

**第二梯队：健康推进期（日 PR 10-30）**
- LobsterAI（27）、NanoBot（23）
- 特征：合入效率高（LobsterAI 81%）、Bug 闭环快（NanoBot 当日修复），社区体验良好

**第三梯队：稳定维护期（日 PR < 10）**
- PicoClaw、NanoClaw、NullClaw、Moltis
- 特征：集中在少数关键修复/功能，无大版本发布

**质量巩固 vs 快速迭代：**
- **快速迭代但质量承压：** OpenClaw、Hermes（P0/P1 修复覆盖率 17%/0%）
- **质量巩固中：** IronClaw（QA bug-bash 第三天）、NanoBot（Pyright 严格检查）、NanoClaw（供应链安全 live-fire 测试）


## 7. 值得关注的趋势信号

**对 AI 智能体开发者而言，以下趋势值得密切跟踪：**

1. **“确定性”正成为核心竞争力** —— IronClaw 围绕“自动化运行必须可预测”拆解了 5 个子任务；OpenClaw 社区对“静默失败”的激烈反馈（94 评论）说明，**用户对“输出可预期”的需求已超越对“功能数量”的需求**。开发者应在架构设计时将“失败可见”设为一等公民。

2. **安全策略从“黑名单”走向“策略即代码”** —— ZeroClaw 的 high-risk 命令确认层（#7155）、OpenClaw 的安装策略确认（#116489）、IronClaw 的 origin-scoped OAuth（#7665）共同指向**细粒度的、可配置的安全决策管道**。这是从“消费者工具”迈向“企业级平台”的必经之路。

3. **供应链安全成为新战场** —— NanoClaw 连续两天进行签名验证 live-fire 测试，IronClaw 发布分支回合并流含金丝雀验证，ZeroClaw 扩展 Blacksmith runner 加速 CI。**预构建产物的可验证性是自托管类项目建立信任的关键。**

4. **渠道能力不对等引发用户流失风险** —— CoPaw 的“飞书会话串线”、PicoClaw 的“Telegram 无会话管理”、Hermes 的“桌面端更新崩溃”均指向：**次要渠道的体验瑕疵会直接影响主渠道的用户忠诚度**。全渠道体验一致性是留存的关键。

5. **低功耗/嵌入式设备是尚未充分开发的蓝海** —— PicoClaw（<10MB RAM 原生 Go）与 NanoClaw（NAS/软路由用户）的活跃反馈表明，**在“边缘端运行个人 AI 助手”的需求真实存在且增长中**。指令集兼容性（AVX2）和资源占用是这一市场的基础门槛。

6. **记忆系统的契约化成为共同瓶颈** —— Hermes 的外部记忆 Provider 契约违背（#85622）、IronClaw 的 Pluggable Memory over MCP（#7661/#7664）、NanoBot 的 Session 持久化一致性（#5378）都指向：**记忆/状态管理层是当前技术架构中最脆弱的环节，也是最值得投入的方向。**

---

*报告基于各项目 GitHub 公开数据生成，数据截止 2026-08-15 00:00 UTC。*

---

## 同赛道项目详细报告

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot 项目动态日报

**日期：2026-08-15** | **数据周期：2026-08-14 至 2026-08-15**


## 今日速览

NanoBot 项目今日保持高度活跃，过去 24 小时内有 23 条 PR 更新，其中 8 条已合并/关闭，15 条处于待合并状态；另有 3 条 Issue 更新（1 条新开、2 条已关闭）。虽然没有新版本发布，但项目在 WebUI 体验优化、Session 稳定性修复、Anthropic 流式超时修复三个方向上有明确推进。值得关注的是，社区提交的 Bug 修复（#5391、#5378）均在当日获得对应 fix PR 响应并闭环，维护响应速度较快。多个 WebUI 相关的 PR 因依赖关系互相标记为 conflict，可能预示着一轮较大的前端重构即将落地。

- 活跃度评估：**高**。24 小时 23 条 PR + 3 条 Issue，且多个 PR 更新频繁（同日内多个 commit 推送）。


## 版本发布

**无新版本发布。** 项目仍处于当前版本的迭代周期中。


## 项目进展

### 已合并/关闭的 PR（8 条）

| PR | 标题 | 类型 | 状态 |
|---|---|---|---|
| [#5392](https://github.com/HKUDS/nanobot/pull/5392) | fix(anthropic): treat stream idle timeout as inactivity only | Bug 修复 | 已合并 |
| [#5393](https://github.com/HKUDS/nanobot/pull/5393) | feat(webui): polish sidebar and session transitions | UI 改进 | 已合并 |
| [#5395](https://github.com/HKUDS/nanobot/pull/5395) | feat(webui): refine conversation groups and shared shapes | UI 改进 | 已合并 |
| [#4689](https://github.com/HKUDS/nanobot/pull/4689) | feat(providers): surface OAuth status and expiry warnings | 功能增强 | 已关闭 |
| [#5018](https://github.com/HKUDS/nanobot/pull/5018) | feat(skills): support explicit context loading | 功能增强 | 已关闭 |
| [#5390](https://github.com/HKUDS/nanobot/pull/5390) | Agent/knowledge graph | 功能 | 已关闭 |

**核心推进：**
- **Anthropic 流式超时修复（#5392）** ：此前 `NANOBOT_STREAM_IDLE_TIMEOUT_S` 在 no-callback 路径上被误当作总超时使用，导致长时但活跃的生成任务被强杀。该 PR 将其改为仅作为空闲超时，修复了一个真实的生产环境问题。
- **WebUI 侧边栏与会话切换优化（#5393、#5395）** ：拆分自 #5358 的 UI 独立改进已合并，侧边栏层级更清晰、分组拖拽体验更完善，本地化工作也在推进中。


## 社区热点

### 今日最受关注：Pyright 严格检查重构（#5161 / #5396）

[Issue #5161](https://github.com/HKUDS/nanobot/issues/5161) 提出了将基于 Pyright 的 `strict` 检查推广至整个 `nanobot/` 代码库，当前 31 个文件级抑制指令需要逐文件精化。该 PR 涉及 20+ 个工具文件的修改，覆盖面广，关注者多。提交者 [ojassharma7](https://github.com/ojassharma7) 为首次贡献者，PR 体量较大。

**背后诉求：** 项目对代码质量有较高追求，正在系统性地消除类型检查的"灰色地带"，提升代码库的可维护性和安全性。这也是开源项目走向成熟阶段常见的基建投入。

### 另一个热点：市场技能与内置技能优先级冲突（#5309）

[PR #5309](https://github.com/HKUDS/nanobot/pull/5309) 致力于解决一个功能性 Bug：当工作区技能与内置技能同名时，用户无法通过市场安装工作区副本，因为系统误判所有市场技能已安装。该 PR 已开放 6 天仍在讨论中，涉及技能加载器的核心逻辑。


## Bug 与稳定性

### 已修复（当日闭环）

| 严重度 | Issue | 问题描述 | 修复 PR | 状态 |
|---|---|---|---|---|
| **高** | [#5391](https://github.com/HKUDS/nanobot/issues/5391) | Anthropic 流式超时被误用作总超时，长时活跃生成被无端终止（默认 90s） | [#5392](https://github.com/HKUDS/nanobot/pull/5392) | ✅ 已合并 |
| **中** | [#5378](https://github.com/HKUDS/nanobot/issues/5378) | 文件归档失败时，Session 状态在持久化前已被变更，导致内存与磁盘状态不一致 | 待确认 | ❌ 无对应 PR |

### 待合并的修复 PR

| PR | 问题 | 严重度 | 备注 |
|---|---|---|---|
| [#5271](https://github.com/HKUDS/nanobot/pull/5271) | 后台任务保存可能覆盖 `/new` 之后的 Session 数据 | **p0** | 已开放 9 天，待合并 |
| [#5382](https://github.com/HKUDS/nanobot/pull/5382) | Windows 下 `os.replace()` 偶发 `PermissionError` 导致 gateway 崩溃（已确认发生 2 次） | **p2** | 已开放 2 天 |


## 功能请求与路线图信号

### 高可能性纳入下一版本

1. **WebUI 会话协作（#5358）** ：通过 `@mention` 实现会话间协作文档化。由于相关 UI 改进 #5393 已合入 main，该功能落地概率显著提升。需解决 `conflict` 标记后将准备合入。
2. **拖拽式会话分组（#5389）** ：与 #5395 的 UI 改进形成功能衔接，同上，待冲突解决后可合入。
3. **WebUI 粒子动效背景（#5340）** ：产品体验层面的锦上添花，优先级较低但已可见完整实现。

### 观望阶段

4. **TypeScript 原生终端 UI（#4329）** ：将 `nanobot agent` 重构为 TypeScript/OpenTUI 客户端，继续由 Python gateway 提供后端服务。该 PR 已开放 2 个月，方向明确但体量大，短期合入可能性较低。
5. **MCP SDK v2 迁移（#5179）**：从 v1 `ClientSession` API 迁移至 v2 高层级 `Client` API，同时保留对旧 SSE 传输协议的兼容性。属于基础设施升级，优先级 p1，持续更新中。


## 用户反馈摘要

- **对超时机制的不满（#5391）** ：用户 `shen0122` 报告 Anthropic 流式超时问题时明确指出，**长达 90 秒的活跃生成被误杀**，影响了真实使用场景中长任务（如代码生成、长文档处理）的可靠性。该问题当日获得修复，体现了维护者对用户反馈的重视。
- **对会话一致性的担忧（#5378）** ：用户 `dajiaohuang` 发现 Session 文件归档失败时数据仍会被变更但未持久化，担心后续成功保存时静默覆盖内存中的旧数据。该问题尚未有修复 PR，值得持续关注。


## 待处理积压

### 长期未合并的功能 PR

| PR | 标题 | 开放时长 | 备注 |
|---|---|---|---|
| [#4145](https://github.com/HKUDS/nanobot/pull/4145) | fix: resolve #3958 — Weather Skill | **75 天** | 示例技能贡献，长时间无维护者响应 |
| [#4329](https://github.com/HKUDS/nanobot/pull/4329) | feat(cli): add native TypeScript terminal UI | **63 天** | 重大架构调整，需谨慎评审 |
| [#4689](https://github.com/HKUDS/nanobot/pull/4689) | feat(providers): surface OAuth status and expiry warnings | 43 天 | 今日已被关闭（状态未知） |

### 待跟进的 p0 级 Bug 修复

| PR | 标题 | 开放时长 | 风险 |
|---|---|---|---|
| [#5271](https://github.com/HKUDS/nanobot/pull/5271) | fix(session): prevent stale background task saves | 9 天 | 涉及 Session 数据一致性，p0 严重度 |

> ⚠️ **维护者提醒：** Issue #5378（文件归档失败的状态变更问题）目前尚无对应修复 PR，建议尽快评估并分配。此外，PR #5271 作为 p0 级修复已开放 9 天未见合并，如涉及设计分歧建议尽早讨论并对外同步结论。

---

*以上数据均来自 NanoBot GitHub 仓库公开信息，数据获取时间为 2026-08-15。*

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent 项目动态日报 — 2026-08-15

---

## 1. 今日速览

过去 24 小时项目保持高活跃度：50 条 Issue 更新（30 条活跃 / 20 条关闭）与 50 条 PR 更新（45 条待合并 / 5 条已关闭）显示出维护与社区贡献双轨并行。今日无新版本发布，但值得关注的是，提交于今日的 `#86223`（Windows 桌面端连续两次更新后后端崩溃）与 `#86385`（macOS 屏幕录制权限循环）均标记为 P1/P2 高优先级，涉及桌面端发布质量与平台兼容性。与此同时，社区侧出现了大量 i18n 本地化 PR（葡萄牙语、波斯语）与桌面 UI 体验优化，但 **45 条待合并 PR 的积压数量值得关注**。另外，涉及 session 状态管理的技术债（跨进程序列化 `#67442`、外部记忆提供器抑制内置注入 `#85622`）正在积累，需要维护层决策。

---

## 2. 版本发布

**无新版本发布。** 上一版本线索：桌面端 2026-08-14 更新被 `#86223` 报告为破坏性更新（后端退出、无法自重启），建议维护者优先核实该版本发布质量后再推进下一次发布。

---

## 3. 项目进展

今日无 PR 被合并，但存在多项进入社区讨论的关键 PR，显示下一迭代的潜在方向：

- **安全加固（合入候选）**：`#86216` 在模型调度边界（`model_tools.py`）增加 JSON Schema 参数投影校验，剥离未声明的控制面参数，属于纵深防御改进；`#72127`（dashboard 回环代理安全模式）已挂起 20 天，涉及安全边界应优先合入。
- **会话与状态管理**：`#86298` 在 `hermes_state.SessionDB` 的 sqlite 边界新增 `transform_message_store` / `transform_message_load` 插件钩子（关闭 #86297），是对社区反复报告的会话持久化 / 外部记忆 Provider 问题的结构性接缝；`#86408` 修复 `/new` 重置后 `session_search` 无法召回昨晚会话内容的问题（关闭 #85756）。
- **桌面端体验**：`#86415` 删除新装用户必须经过 Provider 选择器的"墙"，改为后台铸客账号 + 立即进入对话，显著降低首次使用摩擦；`#86414` 修复主 Agent 模型选择无法持久化为 profile 默认值的问题（由 @rashidkhan 报告）。
- **连接器增强**：`#86369` 为 A2A 协议增加 `SendStreamingMessage` 客户端实现，带能力卡降级；`#86324` 为 Discord REST v10 构建类型安全 embed 构建器（Omniscience M4，修复 #86321）。

整体判断：会话状态管理（session-state）与外部 Provider 兼容性是两个持续投入的主线，安全加固亦在推进，但合入节奏偏慢——今日 0 合并。

---

## 4. 社区热点

| 排名 | Issue/PR | 评论数 | 核心诉求 |
|------|----------|--------|----------|
| 1 | [#67442](https://github.com/NousResearch/hermes-agent/issues/67442) — [OPEN] 跨进程 turn 序列化：CLI-continuity 需要 DB 级租约 | 16 | 作者 `teknium1` 跟进 #64934（已关闭），指出 `gateway/run.py` 将路由键重新指向 CLI 现有 session_id 后，会话需要跨 OS 进程的数据库级租约，目前属于"可接受的边界"但存在竞态窗口。 |
| 2 | [#60693](https://github.com/NousResearch/hermes-agent/issues/60693) — [CLOSED] [GUI] 110% 缩放设置间歇性重置回 100% | 13 | 桌面端 UI 缩放持久性问题的"元老"，今日关闭。与其同族的多个缩放问题（#81879、#82713、#84274）说明该问题在 Windows/macOS 多触发条件下反复出现。 |
| 3 | [#80424](https://github.com/NousResearch/hermes-agent/issues/80424) — [OPEN] Grok/xAI 功能对齐战役（meta-issue） | 10 | 社区推动 Hermes 与 xAI 官方平台全功能对齐（推理、流式、图像/语音），体现用户对前沿模型能力的强需求。 |
| 4 | [#85622](https://github.com/NousResearch/hermes-agent/issues/85622) — [OPEN] 外部记忆 Provider 抑制内置 MEMORY.md/USER.md 注入 | 9 | 用户指出外部记忆 Provider 在 both 模式下违反文档承诺的"additive"契约，属于契约违背类问题。 |
| 5 | [#85125](https://github.com/NousResearch/hermes-agent/issues/85125) — [OPEN] 统一 deadline 层：4 阶段架构修复超时/挂起积压 | 6 | 提出结构性解决 400+ 超时挂起 Issue 积压的架构方案，高屋建瓴但推进需维护者拍板。 |

用户的核心诉求集中在：（1）会话状态在跨进程/跨设备场景下的可靠性与一致性；（2）记忆系统契约的可预期性；（3）桌面端 UI 设置在焦点变化后的持久性；（4）对前沿模型（Grok/xAI）的能力对齐。

---

## 5. Bug 与稳定性

**按严重程度排列：**

| 严重度 | Issue | 描述 | Fix PR |
|--------|-------|------|--------|
| 🔴 P1 | [#86223](https://github.com/NousResearch/hermes-agent/issues/86223) | Windows 桌面端连续两次更新后后端退出 (1)、无法自重启、WinError 32 锁链 | **无** — 今日 8/14 报告，需紧急响应 |
| 🔴 P1 | [#83185](https://github.com/NousResearch/hermes-agent/issues/83185) （已关闭） | Gateway 在 `gateway.platforms` 为 list 时崩溃（`AttributeError`），影响所有 Telegram/Discord 消息 | 修复已合入（commit 003b4c889 引入的回归） |
| 🟠 P2 | [#86385](https://github.com/NousResearch/hermes-agent/issues/86385) | macOS 屏幕录制权限循环：签名修复 #73681 后旧 TCC 授权失效且无法重新授权 | **无** |
| 🟠 P2 | [#86411](https://github.com/NousResearch/hermes-agent/issues/86411) | `terminal.cwd` 显式配置在 mid-turn 时重新固定工作目录，覆盖启动目录（违背 #19214/#19242 约定） | **无** |
| 🟠 P2 | [#86317](https://github.com/NousResearch/hermes-agent/issues/86317) | Docker 每进程清理可能退出在 stop 之后 rm 之前，遗留已停止容器 | **无** |
| 🟠 P2 | [#77472](https://github.com/NousResearch/hermes-agent/issues/77472) | 安全：请求转储、trajectory JSONL、pending_messages、/save 持久化未脱敏工具内容（11 个活转储最大 166KB） | **无** |
| 🟡 P3 | [#86403](https://github.com/NousResearch/hermes-agent/issues/86403) | Xiaomi MiMo v2.5 Pro 工具调用损坏，启用的工具未暴露给模型 | **无** |
| 🟡 P3 | [#86393](https://github.com/NousResearch/hermes-agent/issues/86393) | Kanban 运行时 `TERMINAL_CWD` 被误报为弃用 .env 设置（重复类） | **无** |
| 🟡 P3 | [#84274](https://github.com/NousResearch/hermes-agent/issues/84274) | RDP 重连后 UI 缩放重置为 100%（reassert 遗漏 display-metrics-changed 事件） | **无** |

**观察**：今日 Bug 集中在桌面端（3 个）与配置/工作目录语义（2 个），均无对应修复 PR，存在响应时间风险。此外，`#8751`（walk 父目录时 PermissionError，4/13 创建）至今仍开放，属长期未响应。

---

## 6. 功能请求与路线图信号

| 功能请求 | 对应 PR/Issue | 状态 | 纳入判断 |
|----------|---------------|------|----------|
| **巴西葡萄牙语本地化** | PR [#86292](https://github.com/NousResearch/hermes-agent/pull/86292) | 待合并 | 高概率纳入：i18n 目录已有多语言，成本低 |
| **波斯语 + RTL** | PR [#86335](https://github.com/NousResearch/hermes-agent/pull/86335) | 待合并 | 同上（需验证 RTL 布局质量） |
| **无鉴权多 Provider 故障转移池（Freemaxxing）** | PR [#85631](https://github.com/NousResearch/hermes-agent/pull/85631) | 待合并，含 `needs-decision` | 中等概率：涉及鉴权模型变更，需安全评估 |
| **统一超时/deadline 层（4 阶段）** | Issue [#85125](https://github.com/NousResearch/hermes-agent/issues/85125) | OPEN，社区提出 | 低概率立即纳入，属架构级变更，需 roadmap 决策 |
| **独立记忆 Provider 端到端支持** | PR [#82649](https://github.com/NousResearch/hermes-agent/pull/82649) | DRAFT | 需维护者明确方向；与 #85622 契约问题联动 |
| **Twilio 电话/SMS 技能** | Issue [#409](https://github.com/NousResearch/hermes-agent/issues/409) | OPEN（3 月创建） | 社区呼声高（Discord 演示），但复杂度和运维成本高 |
| **窗口磨砂玻璃效果** | PR [#84329](https://github.com/NousResearch/hermes-agent/pull/84329) | 待合并 | 高概率纳入：纯前端、无风险 |
| **复制文本去除终端装饰** | PR [#86301](https://github.com/NousResearch/hermes-agent/pull/86301) | 待合并 | 高概率纳入：体验优化显著，无破坏性 |
| **消息存储/加载转换插件钩子** | PR [#86298](https://github.com/NousResearch/hermes-agent/pull/86298) | 待合并，`needs-decision` | 需评估插件 API 稳定性承诺 |

路线图信号：项目正从单机 CLI 走向多前端（Desktop + Dashboard + Gateway）+ 多 Provider + 多语言生态，i18n 与插件系统是当前主线；Grok/xAI 对齐（#80424）是社区最活跃的外部需求。

---

## 7. 用户反馈摘要

- **记忆契约矛盾**（#85622）：用户 `TeaShaman-cyber` 指出文档声称外部记忆 Provider "additive, never replacing"，但实际运行中内置 MEMORY.md/USER.md 注入在 both 模式下被抑制。"文档说继续像以前一样工作，但我的新对话里完全没有内置记忆的痕迹。" 这属于契约违背，影响用户对记忆系统的信任。
- **桌面更新体验受损**（#86223）：用户 `aKa368` 在 Windows 上连续两次更新失败，后端退出且无法自重启，"Reopen Hermes to finish" 后依然失败，被迫回退 git 流程手动处理，说明更新管道健壮性不足。
- **CLI/CWD 语义矛盾**（#86411）：用户 `lxman` 表示显式 `terminal.cwd` 配置在会话中途重新固定工作目录，掩盖了启动目录的权威性——"启动时正确，几轮对话后就错了"。
- **手动缩放是高频痛点**：多个 zoom 重置 Issue（#81879、#82713、#84274）的共同特征是 `zoom-state.json` 中保存的缩放值未丢失，但 UI 渲染回退到 100%，需要用户手动重新触发——用户 `sceboucher` 描述为"设置项显示 125%，界面却显示 100% 的割裂感"。
- **Gateway 纯文本/平台配置冲突**（#83185）：用户 `cjyuna79` 反馈标准 `gateway.platforms` list 写法让所有平台消息报错，回归由一次 perf 提交引入，说明测试覆盖对配置变体的漏检。
- **Grok 对齐的社区推力**（#80424）：用户 `andrexibiza` 发起 meta-issue，将 Hermes 的 xAI 能力面与官方文档逐项对比，诉求具体且全面（模型、推理、函数调用、流式、图像、语音），反映出用户希望 Hermes 作为前端能快速跟进新模型能力。
- **macOS 权限迁移问题**（#86385）：用户 `DavidMetcalfe` 报告签名修复后旧授权无法回收，"toggle 显示开启但实际无效，也无法重新触发授权弹窗"，属升级平滑性问题。

满意度总体偏正面（Issue 关闭率 40%），但桌面端更新体验、记忆契约一致性和 CWD 语义矛盾是当前用户旅程中的主要摩擦点。

---

## 8. 待处理积压

| 类型 | 编号 | 标题 | 创建时间 | 备注 |
|------|------|------|----------|------|
| Issue | [#8751](https://github.com/NousResearch/hermes-agent/issues/8751) | PermissionError when walking parent directories for .git root | 2026-04-13 | **4 个月未响应**，权限边界场景，影响多用户环境 |
| Issue | [#409](https://github.com/NousResearch/hermes-agent/issues/409) | Feature: Twilio Skill — 电话/短信/语音 | 2026-03-05 | **5 个月未处理**，社区高呼声，曾有关键演示 |
| PR | [#74243](https://github.com/NousResearch/hermes-agent/pull/74243) | fix(acp): 保护 JSON-RPC stdin 免被子进程读取 | 2026-07-29 | 安全加固，17 天未合入，涉及 ACP 协议纵深防御 |
| PR | [#74242](https://github.com/NousResearch/hermes-agent/pull/74242) | fix(acp): 容忍 turn 取消时 null final_response | 2026-07-29 | 修复 JetBrains 集成非可恢复会话失败，17 天未合入 |
| PR | [#72127](https://github.com/NousResearch/hermes-agent/pull/72127) | fix(dashboard): 安全回环 public URL 代理模式 | 2026-07-26 | 安全边界 20 天未合入，且带 `blast-moderate` 标记 |
| PR | [#76616](https://github.com/NousResearch/hermes-agent/pull/76616) | feat(desktop): 安全重启当前后端 | 2026-08-02 | 涉及桌面端 SSH/本地双模式，13 天未合入 |
| Issue | [#35530](https://github.com/NousResearch/hermes-agent/issues/35530) | fix(tui): 添加 SIGWINCH 回退 | 2026-05-30 | TUI 缩放兼容性，标 invalid 但未关闭，可能已过时 |
| Issue | [#77472](https://github.com/NousResearch/hermes-agent/issues/77472) | 安全：请求转储/轨迹持久化未脱敏 | 2026-08-03 | 标注 HIGH 严重度，12 天无修复 PR，需优先安排 |

**优先建议**：合入安全/稳定性 PR（#72127、#74242、#74243、#86216）；对 #86223 和 #86385 两个桌面端高优 Bug 进行 hotfix 处理；清理 14 天以上未合并 PR 队列，避免社区贡献者流失；对 #8751 权限问题给出至少一个官方回应。

---

*报告生成时间：2026-08-15 | 数据源：NousResearch/hermes-agent GitHub 仓库 | 统计窗口：过去 24 小时*

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw 项目动态日报

**日期：** 2026-08-15  
**数据窗口：** 2026-08-14 ~ 2026-08-15

---

## 1. 今日速览

PicoClaw 项目今日活跃度中等偏上，核心事件集中在 MCP 服务器连接故障导致 Agent 循环挂起的已知 Bug 上——该问题自 7 月 20 日汇报以来持续引发讨论，今日出现对应的修复 PR（#3337），有望在近期解决这一影响用户核心体验的稳定性问题。过去 24 小时内，Issue 侧新增 1 条活跃、关闭 2 条（均为 stale 标记）；PR 侧 3 条待合并（含 1 条关键修复）与 5 条关闭/合并。无新版本发布。整体看，项目处于"稳定性加固 + 功能扩展并行"的阶段，维护者正在通过 stale 机制清理旧积压，同时核心 Bug 修复已进入 PR 审核环节。

---

## 2. 版本发布

**无新版本发布。** 当前最新版本仍为 nightly 构建（git: 2cf030d2），用户可关注此构建中的修复进展。

---

## 3. 项目进展

今日合并/关闭的 PR 均为 stale 清理或此前已提交的改动，无新增合并。**但值得关注的是，今日出现了一个针对核心稳定性问题的高优先级修复 PR（#3337），目前处于待合并状态，这是今日最重要的项目进展信号。**

| PR | 状态 | 内容 | 意义 |
|---|---|---|---|
| [#3337](https://github.com/sipeed/picoclaw/pull/3337) | 🟡 待合并 | 修复 MCP 连接失败导致 Agent 循环挂起 | 直接解决 #3269 报告的聊天界面停止响应问题，影响用户核心体验 |
| [#3319](https://github.com/sipeed/picoclaw/pull/3319) | 🟡 待合并 | `exec` 工具：使 per-run `timeout` 生效，修正 `background`/`pty` 布尔类型声明 | 修复工具参数与行为不一致的功能缺陷，属于工具链完善 |
| [#3200](https://github.com/sipeed/picoclaw/pull/3200) | 🟡 待合并 | 为模型页面增加可配置的默认回退链（fallback chain） | 功能性增强，方便用户设置模型主备切换策略 |
| [#3303](https://github.com/sipeed/picoclaw/pull/3303) | ✅ 已关闭 | 依赖升级 `actions/stale` v10→v11 | 工具链维护 |
| [#3283](https://github.com/sipeed/picoclaw/pull/3283) | ✅ 已关闭 | 钉钉渠道支持图片消息接收 | 渠道能力扩展（已完成） |
| [#3279](https://github.com/sipeed/picoclaw/pull/3279) | ✅ 已关闭 | 修复 seahorse 摘要中工具调用格式泄漏问题 | 修复同类症状的另一个触发路径 |
| [#3271](https://github.com/sipeed/picoclaw/pull/3271) | ✅ 已关闭 | 9 家提供商默认模型名称更新至 2026-07 最新 | 模型列表时效性维护 |
| [#3270](https://github.com/sipeed/picoclaw/pull/3270) | ✅ 已关闭 | 新增 DashScope TTS 提供商 + 微信音频发送 | 音频能力扩展（已完成） |

**整体判断：** 项目在功能广度上已有相当积累（钉钉图片、DashScope TTS、WeChat 音频、多提供商支持），当前重点正转向**稳定性加固与工具行为一致性修正**，这是项目从"可用"向"可靠"过渡的关键阶段。

---

## 4. 社区热点

### 🔥 最热 Issue [#3269](https://github.com/sipeed/picoclaw/issues/3269) — MCP 连接失败导致 Agent 循环挂起

- **创建时间：** 2026-07-20，持续活跃近 4 周
- **评论数：** 5 | 👍 1
- **核心诉求：** 当 MCP 服务器不可达/损坏时，`AgentLoop.Run` 返回错误并退出，导致 PicoClaw 聊天界面完全停止回复用户。报告者使用的是 nightly 版本 + Qwen3 模型。
- **关键进展：** 今日出现对应修复 PR [#3337](https://github.com/sipeed/picoclaw/pull/3337)，修复思路是改变错误传播路径——当 `ensureMCPInitialized` 失败时，不再让 Agent 循环直接退出，而是优雅降级继续运行。

**分析：** 该问题影响力极大——任何使用 MCP 服务器的用户都可能因服务器临时故障而完全失去对话能力。修复 PR 从"错误传播导致整体退出"改为"容错降级"，方向正确。建议维护者优先审合并，并补充分支测试覆盖 MCP 不可达场景。

### 次热点 [#3308](https://github.com/sipeed/picoclaw/issues/3308) — SeaHorse/Channel Manager/Hooks 并发安全审查

- **状态：** 已关闭（stale）
- **内容摘要：** 社区成员 Rehanasharmin 对 SeaHorse、Channel Manager 和 Hooks 模块进行了代码审查，指出并发风险（concurrency hazards）、goroutine 泄漏以及内存/速度优化空间。
- **诉求：** 希望维护者关注底层架构的健壮性，特别是并发场景下的稳定性。

---

## 5. Bug 与稳定性

### 🔴 高严重度

**Issue [#3269](https://github.com/sipeed/picoclaw/issues/3269) — MCP 连接失败导致 Agent 循环挂起、聊天界面彻底失去响应**
- 影响面：使用 MCP 的全部用户
- 已存在：26 天
- 修复 PR：[#3337](https://github.com/sipeed/picoclaw/pull/3337) 今日提交，待合并 ✅

### 🟡 中严重度

**PR [#3319](https://github.com/sipeed/picoclaw/pull/3319) — `exec` 工具的 per-run `timeout` 参数被静默忽略（同步执行始终使用全局超时）、`background`/`pty` 在 schema 中声明为 string 实为 boolean**
- 影响面：使用命令行工具的场景，超时控制不精确且参数类型误导开发
- 当前状态：待合并，已有修复方案

### 🟢 已解决（今日无新增 Bug 报告）

- Issue #3308、#3307 均为 stale 自动关闭，非新 Bug。

---

## 6. 功能请求与路线图信号

### 近期信号（可能纳入下一版本）

| 功能需求 | 来源 | 当前状态 | 判断依据 |
|---|---|---|---|
| **模型默认回退链（fallback chain）** | PR [#3200](https://github.com/sipeed/picoclaw/pull/3200) | 待合并 | 已在 Web UI + API 层实现，功能完成度高，合并可能性大 |
| **Telegram 会话列表/切换命令** | Issue [#3307](https://github.com/sipeed/picoclaw/issues/3307)（stale 关闭） | 待实现 | 用户明确诉求：Web UI 有完整会话管理，但 Telegram 渠道缺乏对等能力。原始 PR 曾被 stale 关闭，但需求真实存在 |

### 远期信号

- 从 PR #3283（钉钉图片）、#3270（DashScope TTS + 微信音频）等已合并功能看，**项目在多渠道接入（钉钉、微信、Telegram）上持续投入**，渠道能力是路线图重点之一。
- 从 PR #3279（seahorse 格式泄漏修复）与 #3269（MCP 稳定）看，**工具调用链路稳定性**是当前质量提升的聚焦方向。

---

## 7. 用户反馈摘要

### 核心痛点

1. **MCP 故障即"全盘停摆"**（Issue #3269）：用户遇到 MCP 服务器不可达时，整个对话界面完全失去响应，无超时恢复机制，体验极差。当基础设施（MCP 服务器）不稳定时，AI 助手反而变成了比没有更糟糕的负担。
2. **渠道能力不对等**（Issue #3307）：Web UI 提供了完整的会话管理（列表、切换、删除），但 Telegram 等其他渠道完全缺失。用户被迫只能在 Web 端管理会话，移动/IM 场景受阻。

### 满意之处

- 社区用户对 PicoClaw 在低硬件成本（$10 设备、<10MB RAM、亚秒启动）上实现原生 Go AI 助手表示了认可（Issue #3308 的表述）。
- 多提供商模型支持（已覆盖 9 家）获得社区建设性贡献（PR #3271 等），说明项目的可扩展架构得到了开发者的认可并愿意为之贡献。

---

## 8. 待处理积压

### 建议优先关注

1. **[#3337](https://github.com/sipeed/picoclaw/pull/3337) — MCP 故障修复 PR**（8 月 14 日提交，等待审核）
   - **优先级：** 🔴 极高
   - **原因：** 直接修复 #3269 这个影响最大的稳定性问题，且修复方案合理（容错降级而非终止循环）。建议合并后补充测试用例覆盖 MCP 不可达、超时、半连接（部分初始化）等场景。

2. **[#3200](https://github.com/sipeed/picoclaw/pull/3200) — 默认模型回退链**（7 月 1 日创建，等待 45 天）
   - **优先级：** 🟡 中
   - **原因：** 功能完成度较高，对多模型提供商用户有实际价值。但已积压超过 6 周，存在与当前代码产生冲突的风险，建议维护者尽快评估。

3. **[#3319](https://github.com/sipeed/picoclaw/pull/3319) — exec 工具 timeout/boolean 修复**（8 月 7 日创建）
   - **优先级：** 🟡 中
   - **原因：** 属于工具行为正确性修复，对开发者的工具链使用有直接影响，等待时间尚可接受。

### 长期未响应的观察项

- **Issue #3308（SeaHorse/Channel Manager/Hooks 并发审查）** 已 stale 关闭，但评论中提出的 goroutine 泄漏与并发安全问题值得维护者在后续架构迭代中留意——建议 @ 作者 Rehanasharmin 或将其内容归档到项目文档的"known tech debt"部分。
- **Issue #3307（Telegram 会话管理）** 虽然 stale 关闭，但需求真实且细化（有具体操作清单：列表/切换/删除），建议在下一版本规划中纳入考虑，避免长期未响应造成社区负反馈。

---

## 项目健康度总结

| 维度 | 评分 | 说明 |
|---|---|---|
| 活跃度 | ⭐⭐⭐⭐ | Issue/PR 均有持续流转，社区贡献活跃 |
| 稳定性 | ⭐⭐⭐ | 存在 1 个高影响 Bug 尚未修复落地，但已有修复方案 |
| 功能进度 | ⭐⭐⭐⭐ | 多渠道、多模型、TTS 等扩展持续合并 |
| 维护响应 | ⭐⭐⭐ | 核心 Issue 修复 PR 当天即出现，但 #3200 等 PR 积压较久 |
| 社区健康 | ⭐⭐⭐⭐ | 社区成员主动贡献代码与代码审查，质量较高 |

**核心关注建议：** 优先合并 [#3337](https://github.com/sipeed/picoclaw/pull/3337) 并补齐测试，同时关注 stale 清理机制是否过于激进导致有效 Issue/PR 被误关（如 #3307、#3308 均为合理讨论却因 stale 关闭，建议调整 stale 期限或人工复核后重新打开）。

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw 项目动态日报

**日期：2026-08-15** | **数据周期：2026-08-14 至 2026-08-15**


## 1. 今日速览

NanoClaw 过去 24 小时活跃度**中高**：新增 2 个 Issue、9 个 PR 动态。值得关注的是，社区连续提交了两个安装/运行环境相关的 Bug（Node 版本检测失效、Bun 二进制 AVX2 指令集兼容性），且均有配套 fix PR 跟进，修复链路完整。核心团队完成了签名验证链路的第二轮测试，并修复了一个关键验证逻辑问题（#3243 已合并）。此外，社区贡献者正在推进 Dial 渠道集成（SMS + AI 语音），且有多个稳定性修复等待合并。整体项目健康度**良好**——虽无新版本发布，但社区活跃、Bug 响应迅速、代码质量流程（签名验证、自动审批链）在持续加固。


## 2. 版本发布

今日无新版本发布。


## 3. 项目进展

今日共有 **3 个 PR 关闭**（其中 2 个为核心团队的内部测试 PR）：

| PR | 类型 | 说明 |
|---|---|---|
| [#3243](https://github.com/nanocoai/nanoclaw/pull/3243) **已合并** | [core-team] 验证逻辑修复 | **最值得关注**。修复了 `verify-agent-image` 工作流中一个关键逻辑缺陷：此前 `Enable auto-merge` 步骤的失败（如在 draft PR 上、或关闭了 allow_auto_merge 时）会被误判为镜像验证失败。现在 `verify` 已是必过检查，工作流会独立触发 `approve-agent-image` 做二次验证并给出审批意见。显著提升了容器镜像签名验证链路的可靠性。 |
| [#3244](https://github.com/nanocoai/nanoclaw/pull/3244) 已关闭（未合并） | 核心团队 live-fire 测试 #2 | 验证 #3243 修复后完整链路（verify → approve → cosign → review）是否能跑通。按计划关闭。 |
| [#3242](https://github.com/nanocoai/nanoclaw/pull/3242) 已关闭（未合并） | 核心团队 live-fire 测试 #1 | 第一轮签名审批链路测试，已完成使命。 |

除上述关闭的 PR 外，另有 **6 个 PR 正在等待合并/审查**（详见第 8 节）。项目在持续推进渠道集成（Dial）、调度稳定性、Windows 容器清理兼容性等方面的工作。


## 4. 社区热点

**今日最热议题：安装与运行环境的兼容性问题。**

1. **[Issue #3248](https://github.com/nanocoai/nanoclaw/issues/3248) + [PR #3249](https://github.com/nanocoai/nanoclaw/pull/3249)（同一作者 glifocat 提交）** — `setup.sh` 的 Node 版本检测逻辑存在漏洞：当检测到已安装的 Node 版本过低时，会调用 `install-node.sh` 来安装新版本，但该脚本因检测到已有 Node 而直接短路跳过，导致用户陷入"版本过旧但安装不上"的死循环。这是典型的安装脚本交互逻辑缺陷，社区用户已提交修复 PR。

2. **[Issue #3245](https://github.com/nanocoai/nanoclaw/issues/3245)** — 预构建的 agent 镜像使用非基线 x64 目标编译的 Bun 二进制，**要求 CPU 支持 AVX2 指令集**。在 Intel Tremont/Elkhart Lake 等低功耗 Atom 处理器（如 Celeron J6413/N5105）上直接触发 SIGILL（非法指令）崩溃。这影响了一批 NAS、软路由、小主机用户，而这类设备恰好是自托管 AI 助手的常见部署环境。目前**尚无对应的 fix PR**，建议维护者优先关注。

**诉求分析**：这两个 Issue 共同指向一个用户核心诉求——**"开箱即用"的安装体验**。NanoClaw 的目标用户群体中包含大量非资深开发者（家用服务器、NAS 用户），他们对安装脚本的健壮性和预构建产物的兼容性有较高期待。


## 5. Bug 与稳定性

按严重程度排列：

| 严重度 | Issue | 描述 | 状态 |
|---|---|---|---|
| **高（崩溃）** | [#3245](https://github.com/nanocoai/nanoclaw/issues/3245) | 预构建镜像内 Bun 二进制要求 AVX2，在老旧/低功耗 CPU 上直接 SIGILL 崩溃，导致 agent 无法运行 | ⚠️ **暂无 fix PR**，已提交至社区等待响应 |
| **中（功能受阻）** | [#3248](https://github.com/nanocoai/nanoclaw/issues/3248) | `setup.sh` Node 版本检测分支失效，存在旧版 Node 时无法升级安装 | ✅ **[PR #3249](https://github.com/nanocoai/nanoclaw/pull/3249)** 已提交修复 |

**待合并的稳定性修复 PR**（今日提交）：

- **[PR #3247](https://github.com/nanocoai/nanoclaw/pull/3247)**（jsboige）：修复调度模块中畸形 cron 表达式（如 `0 21-5 * * *` 这种 min>max 的写法）导致每次 sweep 都重复报错的问题，改为直接废弃该条目。提升调度系统在异常输入下的自愈能力。
- **[PR #3246](https://github.com/nanocoai/nanoclaw/pull/3246)**（jsboige）：修复 Windows 下孤儿容器清理静默失效的问题——`execSync` 中 POSIX 单引号参数在 `cmd.exe` 下被错误传递。影响 Windows 用户的容器生命周期管理。


## 6. 功能请求与路线图信号

**Dial 渠道集成（SMS + AI 语音通话）** 是当前最强的路线图信号：

- **[PR #3050](https://github.com/nanocoai/nanoclaw/pull/3050)**：在 setup 向导的渠道选择器中加入 Dial，并配套 runChannelSkill 模型。
- **[PR #3041](https://github.com/nanocoai/nanoclaw/pull/3041)**：实现 Dial 渠道适配器（SMS + AI 语音），属 feature skill + 源码改动。

这两个 PR 已存在一个月以上，今日渠道选择器 PR 有更新，说明作者仍在活跃推进。若被合并，NanoClaw 将获得短信和 AI 语音通话能力，是向"多渠道个人助手"方向迈出的重要一步。**建议维护者安排 review 资源**，避免 PR 因长期积压而失活。


## 7. 用户反馈摘要

今日 Issue/PR 中暂无用户评论互动，反馈主要通过 Issue 描述和 PR 内容传递：

- **真实痛点**：
  - 低功耗 x86 设备（NAS、软路由、迷你主机）用户是 NanoClaw 的真实使用群体，预构建产物的指令集兼容性直接决定产品能否在他们的硬件上跑起来。
  - 存在已有 Node 环境的用户不在少数（开发者在机器上装了旧版本 Node 很常见），安装脚本需要正确区分"无 Node"和"有但版本过旧"两种场景。

- **值得注意的信号**：
  - 核心团队连续两天进行"签名审批链路"的 live-fire 测试（#3242 → #3243 → #3244），表明项目正在认真构建供应链安全能力。虽然这些 PR 对普通用户不可见，但反映出项目在工程化、安全合规层面的投入。
  - Windows 平台的容器清理问题（#3246）表明 Windows 用户群体真实存在，且在使用容器化部署方式。

- **满意之处**：社区贡献者（glifocat、jsboige）能够快速定位问题、提交符合规范的修复 PR，且作者主动认领自己报告的 Issue 并附上修复，形成良好的"报告-修复"闭环。


## 8. 待处理积压

### 待合并 PR（6 个）

| PR | 内容 | 等待时长 | 优先级建议 |
|---|---|---|---|
| [#3041](https://github.com/nanocoai/nanoclaw/pull/3041) | Dial 渠道适配器（SMS + AI 语音） | 32 天 | ⭐ 高 — 功能型 PR，长时间未合，建议维护者关注 |
| [#3050](https://github.com/nanocoai/nanoclaw/pull/3050) | setup 向导集成 Dial 渠道 | 32 天 | ⭐ 高 — 同上，与 #3041 配套 |
| [#3249](https://github.com/nanocoai/nanoclaw/pull/3249) | 修复 Node 过旧时的安装死循环 | <1 天 | 🟡 中 — 对应 Issue #3248，建议尽快合入 |
| [#3246](https://github.com/nanocoai/nanoclaw/pull/3246) | 修复 Windows 孤儿容器清理失效 | <1 天 | 🟡 中 — 涉及 Windows 用户，建议纳入近期里程碑 |
| [#3247](https://github.com/nanocoai/nanoclaw/pull/3247) | 修复畸形 cron 表达式反复报错 | <1 天 | 🟡 中 — 稳定性提升，低风险 |
| [#3230](https://github.com/nanocoai/nanoclaw/pull/3230) | 修复技能移除文档指向已停用的镜像路径 | 3 天 | 🟢 低 — 文档修复 |

### 需关注的无 PR Issue

- **[Issue #3245](https://github.com/nanocoai/nanoclaw/issues/3245)（Bun 需要 AVX2，低功耗 CPU 直接崩溃）** — 无对应 PR，且影响面较大（NAS/软路由/旧 PC 用户群）。**建议维护者在下一个版本中考虑提供 baseline x64 构建产物，或改为可选下载 AVX2 版本。**

### 长期遗留提示

- 两个 Dial 渠道 PR（#3041、#3050）已悬置一月有余，建议维护者明确回应（合并 / 要求修改 / 关闭），避免社区贡献者的积极性受挫。


> **总结**：NanoClaw 正处于稳步迭代期。核心团队在加固供应链安全，社区在贡献新渠道、修复真实痛点。安装兼容性（Node 检测、AVX2）是当前最应优先处理的问题——它们直接影响新用户的首次体验。建议在下一个版本中至少解决 AVX2 兼容性（提供 baseline 构建或降级方案），并加速 Dial 渠道 PR 的审查进程。

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

# NullClaw 项目动态日报 — 2026-08-15

> 数据来源：github.com/nullclaw/nullclaw | 统计窗口：2026-08-14 ~ 2026-08-15


## 1. 今日速览

NullClaw 项目今日整体活跃度处于 **低位水平**。过去 24 小时无新开 Issues 和版本发布，仅出现 1 条 PR 活动且为合并/关闭状态。这说明项目当前处于**合并消化期**，开发重心在于清理存量 PR 而非开启新议题。值得关注的是，今日关闭的 PR #986（SQLite 内存数据库路径可配置）是近期少数针对核心存储引擎的改动，表明项目在基础设施灵活性方面仍持续推进，但整体节奏较前几日有所放缓。维护者响应速度良好，从 PR 创建到关闭仅间隔约 1 天。


## 2. 版本发布

今日无新版本发布。最近一次 Release 信息请参考上一期日报或 GitHub Releases 页面。


## 3. 项目进展

### 核心 PR 合并/关闭

| PR | 标题 | 状态 | 说明 |
|---|------|------|------|
| [#986](https://github.com/nullclaw/nullclaw/pull/986) | GEN-548: make SQLite memory database path configurable | ✅ 已关闭（合并） | 为基于 SQLite 的主记忆引擎新增 `memory.database_path` 配置项 |

**本次合并的意义：**

- **核心存储灵活性提升** — 此前 SQLite 记忆文件固定存放在 `<workspace>/memory.db`，现在允许用户自定义路径。该改动主要面向：
  - **只读工作区部署**：部分容器化或 CI 场景下工作区为只读挂载，无法写入 memory.db，通过指定绝对路径可解决此约束
  - **多实例隔离**：同一工作区可运行多个 NullClaw 实例并各自指定独立数据库文件
- **向后兼容**：当 `memory.database_path` 为空时，默认行为保持不变（仍使用 `<workspace>/memory.db`），存量用户无需任何迁移操作。相对路径将基于工作区解析，绝对路径直接使用。

这是 NullClaw 在**部署灵活性和环境适配性**上的重要一步，项目向着"可在受限环境中运行"的目标持续推进。


## 4. 社区热点

今日无可活跃讨论的 Issues/PRs。PR #986 从创建到关闭仅约 1 天，且无评论互动，未形成社区讨论。

**分析**：今日社区关注度极低，可能原因：a) 该 PR 属于基础设施类改动，用户感知度低；b) 当前处于版本间歇期，用户注意力集中在已发布功能的使用上；c) 项目维护节奏以维护者驱动为主，社区主动贡献占比不高。


## 5. Bug 与稳定性

今日无 Bug 报告、崩溃或回归问题。PR #986 本身无 Bug 性质，属功能增强。


## 6. 功能请求与路线图信号

PR #986 所解决的 **"数据库路径可配置"** 需求本身就是一个强烈的功能请求信号：

- **用户痛点**：在只读文件系统、容器化部署、多实例共存的场景下，默认的固定路径（`<workspace>/memory.db`）成为部署障碍
- **路线图判断**：该需求已被纳入 GEN-548 工单并在 PR 中落地，说明项目维护者重视**部署环境适配**这一方向。后续合理推测，可能会有更多围绕 ├─ 配置化（如日志路径、缓存路径）、容器化（Docker/K8s）部署文档完善、以及环境变量支持等方面的改动被纳入路线图
- **重要信号**：从 PR 标题（GEN-548）可看出项目使用内部工单系统管理需求，社区用户若希望推动新功能建议，通过 GitHub Issues 提出后需注明与现有 GEN 编号体系的关联更易于被采纳


## 7. 用户反馈摘要

今日无任何 Issues 评论，无法提取新的用户反馈。结合 PR #986 的改动动机推测用户侧需求主要集中在：

- **部署灵活性** — 希望 NullClaw 能在 Docker / K8s / CI 等受限环境中运行，不强制依赖可写工作区
- **多实例支持** — 在同时运行多个实例时能隔离存储

这些属于从代码改动反推的隐含需求，非显式用户评论。


## 8. 待处理积压

今日无长期未响应的重要 Issue 或 PR。建议维护者关注以下方向（非今日新增，但值得留意）：

- 仓库是否有超过 **7 天** 无维护者回应的 Open Issues（今日数据无此统计，建议人工确认）
- PR 队列中是否存在已提交但未获 review 的旧 PR（今日数据仅显示 1 条 PR 活跃记录，整体队列状态需查看 GitHub PR 列表确认）

---

*本日报由 AI 分析师自动生成，数据截至 2026-08-15。项目健康度评级：🟢 稳定（低活跃但无异常）。*

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw 项目动态日报

**日期：2026-08-15** | **数据窗口：2026-08-14 00:00 - 2026-08-15 00:00 UTC**


## 1. 今日速览

IronClaw 在过去 24 小时保持高强度开发节奏，共产生 25 条 Issue 更新和 48 条 PR 更新，其中合并/关闭 PR 达 23 条（净关闭率 48%），新开活跃 Issue 16 条。核心主线集中在两大方向：**v1.3.0 自动化可靠性工程**（围绕 #6879 的五个子任务集中推进，含确定性静默结果、预检授权租约、模型固定、语义结果持久化等）和 **Pluggable Memory over MCP 架构落地**（#7661/#7664 双线并进）。此外，1.2.0 版本正式稳定发布，并完成了 release 分支回合并流（#7657/#7663），标志着 1.2 系列进入维护模式。QA bug-bash 进入第三天，Telegram/Slack 集成层暴露若干 P2 级缺陷，已有一半以上获得对应修复 PR。整体项目健康度良好，无 P0 级阻塞问题，但自动化可靠性问题（#6879）的复杂性值得持续关注。


## 2. 版本发布

### IronClaw v1.2.0（稳定版）— 2026-08-13

**变更内容**：该版本由 `1.2.0-rc.3` 稳定晋升，包含 RC2/RC3 中验证的全部修复及 RC1 的完整功能集。主要亮点包括：线程索引投影修复（thread-index projection repair）、Windows 文件系统与 smoke 测试可靠性改进、Windows 下 JSON 输出清理，以及**运行时容器内置 curl**（供编排器对 worker 进行 HTTP 健康检查）。

**破坏性变更**：无已知破坏性变更。

**迁移注意事项**：
- `1.2.0` 的发布修复已通过 [#7663](https://github.com/nearai/ironclaw/pull/7663) 前向移植至 `main`，并在 [#7657](https://github.com/nearai/ironclaw/pull/7657) 完成 release 分支回合并流。1.0/1.1→1.2 的启动迁移为状态保留式（state-preserving），已覆盖后端与领域契约。
- 运维团队需注意：新容器镜像体积略增（新增 curl 依赖），但换取了编排器健康检查的确定性。


## 3. 项目进展

今日合并/关闭的 23 条 PR 中，以下几条对项目影响最大：

**已合并/关闭（重要）：**

- **[#7657](https://github.com/nearai/ironclaw/pull/7657) — 1.2.0 release 分支合回 main**（XL, core）: 将验证过的 `release/2026-08-11` 分支完全合回主干，前向移植启动迁移、Windows 修复及发布构件升级金丝雀。这标志着 1.2 系列开发闭环完成，项目整体基线前移。

- **[#7665](https://github.com/nearai/ironclaw/pull/7665) — origin-scoped 托管 MCP OAuth 支持**（L, core）: 为 MKT1 使用的 HTTPS `/mcp` 端点提供 RFC 9728 受限 OAuth 形状支持，贯穿 resolved-manifest 持久化、DCR、token exchange 与 refresh。这是 MCP 生态兼容性的重要补强。

- **[#7668](https://github.com/nearai/ironclaw/pull/7668) — 扩展 Provider 认证诊断透出**（XL, core）: 将 GitHub provider 的受限错误信息与稳定错误码透传至 WASM、扩展工具 ABI、能力门、运行时门与持久化门记录，使模型下一轮可基于诊断信息自纠。

- **[#7652](https://github.com/nearai/ironclaw/pull/7652) — 生产 DB 写入负载测量**（XL, core）: 完成 #7592 的核心测量任务（10 个能力调用 + 11 次模型尝试的典型 agent turn），为 DB 写压史诗建立回归基线。

- **[#7658](https://github.com/nearai/ironclaw/pull/7658) — Telegram 2FA 网关识别与登录码位置提示**（M, core）: 修复 linked-device QA 第一天发现的两个联机缺陷，包括 QR 扫描遇 2FA 账户的识别与提示。

- **[#7655](https://github.com/nearai/ironclaw/pull/7655) — CI 集成覆盖率地板重新钉定**（XS, core）: 基于 main 自身门禁输出，将 slack/telegram 两个 crate 的覆盖率地板调至观测值。

**仍打开（关键推进中）：**

- **[#7634](https://github.com/nearai/ironclaw/pull/7634) — unbound-turns 完全切换**（XL, core）: 完成 prepared-context turns 模型的全部切换，包含 71 条设计文档一致性审计。叠加于 #7562 之上。

- **[#7648](https://github.com/nearai/ironclaw/pull/7648) — ACP 执行器**（XL, core）: 在 `Arc<dyn TurnRunExecutor>` 上实现每运行配置档路由器，为 claude-code 作为循环执行器铺路。


## 4. 社区热点

**今日讨论热度相对分散**（大部分 Issue 评论数为 0），但以下条目获得了社区关注：

- **[#6879](https://github.com/nearai/ironclaw/issues/6879) — 自动化运行可靠性史诗（1 条评论）**：唯一有实质讨论的核心 Issue。其子任务（#7644、#7645、#7646、#7647）在一天内全部开出，说明核心维护者对这一问题已有明确拆解方案并正在密集执行。用户痛点是**小型模型（DeepSeek V4 Flash）上同一 prompt 时而成功时而空转**，这已被证实是结构性缺陷而非模型噪声——触发后执行的是普通交互式聊天轮次而非自动化运行。

- **[#7661](https://github.com/nearai/ironclaw/pull/7661) — MCP-backed 内存 Provider**（XL）: 虽然评论数为 0，但该 PR 与追踪 Issue #7664 的联动（#7664 本身引用了 #7661 作为 draft PR）表明这是架构级改动，社区对"可插拔内存"的期待长期存在。Mnesis Core 作为首个消费者将验证该契约。

**诉求分析**：社区对 IronClaw 的核心诉求集中在**确定性**——自动化运行必须可预测（#6879 系列），登录/连接流程必须可诊断（#7658、#7667），UI 状态必须反映真实连接状态（#7660）。这与项目从"demo-ready"走向"production-ready"的阶段定位一致。


## 5. Bug 与稳定性

**今日报告 Bug 按严重程度排列：**

| 严重度 | Issue | 描述 | 修复 PR 状态 |
|--------|-------|------|-------------|
| **P2** | [#7662](https://github.com/nearai/ironclaw/issues/7662) | Telegram 发送 MP4 附件失败，报 `invalid_value (attachments.mime_type)`，即使文件已被识别为 `video/mp4` | ❌ 尚无对应 PR |
| **P2** | [#7660](https://github.com/nearai/ironclaw/issues/7660) | Slack 已连接且功能正常，但 UI 错误显示 "Reconnect" 与 "Finish Setup" 徽章 | ✅ [#7666](https://github.com/nearai/ironclaw/pull/7666) 已包含修复 |
| **P2** | [#7659](https://github.com/nearai/ironclaw/issues/7659) | 其他用户安装的扩展出现在当前用户的 Extensions/Registry 页面上（状态泄漏） | ❌ 尚无对应 PR |
| **P2** | [#7667](https://github.com/nearai/ironclaw/issues/7667) | Telegram phone-mode 登录码提示未反映 `sentCode.type_`（raw-TL 发送路径），用户收不到码 | ✅ [#7658](https://github.com/nearai/ironclaw/pull/7658) 已合并修复相关 2FA 路径 |
| **P1** | [#7626](https://github.com/nearai/ironclaw/issues/7626) | 自定义 MCP 需要浏览器/邮箱认证时，IronClaw 卡死（用户报告，创建于 08-13，今日无更新） | ❌ 尚无对应 PR |

**回归风险评估**：今日无新发现的回归问题。1.2.0 合并回 main 的 PR（#7657、#7663）包含 Windows 文件系统/smoke 修复的前向移植，需关注 CI 是否持续通过。

**稳定性观察**：#7655 将 slack/telegram 集成层覆盖率地板重新钉定到观测值，虽为务实之举，但也暗示这两块代码的测试覆盖可能尚未达到理想水平。


## 6. 功能请求与路线图信号

**明确纳入 v1.3.0 的功能（标签确认）：**

- **自动化可靠性五件套**（全部今日开票）：确定性无投递结果（[#7647](https://github.com/nearai/ironclaw/issues/7647)）、预检授权租约（[#7646](https://github.com/nearai/ironclaw/issues/7646)）、按自动化模型固定（[#7645](https://github.com/nearai/ironclaw/issues/7645)）、武装前验证（[#7644](https://github.com/nearai/ironclaw/issues/7644)）。这些直接回应用户对"无人值守运行可靠性"的核心诉求。

**高信号功能请求（无 v1.3.0 标签但已有 PR 对应）：**

- **Pluggable Memory over MCP**（[#7664](https://github.com/nearai/ironclaw/issues/7664) + [#7661](https://github.com/nearai/ironclaw/pull/7661)）: 通过配置而非编译期 match arm 绑定外部内存系统。契约将随 [#7661](https://github.com/nearai/ironclaw/pull/7661) 发布。

- **WebUI 结构化 Ask User 卡片**（[#7653](https://github.com/nearai/ironclaw/issues/7653)）: 基于现有终端 `LoopCompletionKind::AskUserReply` 实现模型可见的 `ask` 工具。刻意设计为非可恢复循环门。

**低信号但方向正确：**

- **共享组件抽取**（[#7569](https://github.com/nearai/ironclaw/issues/7569) SearchField、[#7639](https://github.com/nearai/ironclaw/issues/7639) InlineNotice、[#7637](https://github.com/nearai/ironclaw/issues/7637) 设计系统类型边界、[#7638](https://github.com/nearai/ironclaw/issues/7638) Toast 替换 alert）: italic-jinxin 的系统性 UI 清理系列，反映 Reborn WebUI 进入质量打磨期。


## 7. 用户反馈摘要

**来自 Issues 的真实用户痛点：**

- **自动化不确定性（[#6879](https://github.com/nearai/ironclaw/issues/6879)）**：用户反映同一存储 prompt 时而成功、时而产出无用结果，尤其是在 DeepSeek V4 Flash 这类小型模型上。核心维护者已确认这是触发→运行管道的结构性问题——触发触发的是普通交互式聊天轮次，而非自动化运行。这是当前最严重的用户体验问题。

- **MCP 认证流程卡死（[#7626](https://github.com/nearai/ironclaw/issues/7626)）**：用户连接需要浏览器+邮箱双重认证的 MCP 时，Hermes 弹出了浏览器授权但 IronClaw 卡死。MKT1 场景（付费访问需要邮箱+浏览器验证）受影响明显。

- **生成 DOCX 文件损坏（[#6869](https://github.com/nearai/ironclaw/issues/6869)，已关闭）**：用户反馈 IronClaw 生成的带标记 NDA 的 .docx 文件无法被 Word 打开，并指出"ChatGPT 和 Claude 可以轻松做到"。该 Issue 今日从关闭状态更新，值得确认根因修复是否正确合入。

- **扩展状态跨用户泄漏（[#7659](https://github.com/nearai/ironclaw/issues/7659)）**：用户发现其他用户安装的扩展出现在自己的 Registry 页面上，多租户隔离存在隐患。

- **Slack UI 状态误报（[#7660](https://github.com/nearai/ironclaw/issues/7660)）**：连接完全正常但 UI 显示"需要重连"，影响用户信任。


## 8. 待处理积压

**需维护者关注的项目：**

- **[#7626](https://github.com/nearai/ironclaw/issues/7626) — 自定义 MCP 认证卡死（08-13 创建，今日无更新）**：P1 级认证缺陷，阻塞了需要浏览器/邮箱验证的 MCP 场景。尚无 PR 认领，且今日没有新的动态更新。建议优先分配。

- **[#7624](https://github.com/nearai/ironclaw/issues/7624) — ACP 执行器 v0（08-13 创建，14 日更新）**：核心维护者明确标注"这是现在唯一要构建的 pluggable-loops 工作项"，后续三个阶梯任务（#7621/#7622/#7623）均以该 v0 验证为前提。目前已有对应 PR（[#7648](https://github.com/nearai/ironclaw/pull/7648)），进展正常，但作为解锁后续工作的关键节点，值得持续关注。

- **[#7255](https://github.com/nearai/ironclaw/pull/7255) — APDD Kit 治理评估（08-05 创建，已 10 天无实质进展）**：来自 regular contributor 的文档型 PR，评估将 APDD 治理框架纳入 IronClaw。虽标记为 XL 且 scope 为 docs，但 10 天未获 review 可能造成外部贡献者流失风险。同类问题也影响 [#7378](https://github.com/nearai/ironclaw/pull/7378) 和 [#7379](https://github.com/nearai/ironclaw/pull/7379)（doc-truth 系列，08-07 创建）。

- **[#7456](https://github.com/nearai/ironclaw/pull/7456) — Reborn 可持久化存储 profile 无关化（08-10 创建，5 天）**：解决 Reborn 多 profile 根目录一致性的关键 PR（将存储直接挂于 `IRONCLAW_REBORN_HOME` 下），含安全信封持久化。已 5 天未获 review，建议优先处理。

**长期未关闭 Issue 观察**：[#6869](https://github.com/nearai/ironclaw/issues/6869)（DOCX 损坏）从 07-29 创建至 08-14 关闭，历时 16 天，最终修复方案值得确认并回写已知问题清单。


**总体评估**：IronClaw 项目处于 v1.2 收尾与 v1.3 规划叠加的高活跃期。自动化可靠性（#6879）与可插拔内存是两个核心推进方向，QA bug-bash 流程运转有效（bug 发现→修复 PR 的转化速度较快）。健康度指标：无 P0 阻塞、1.2 稳定版顺利发布、release 回合并流及时。需关注的风险点是部分外部贡献者 PR 等待 review 时间偏长，以及 MCP 认证类阻塞问题的推进速度。

---
*数据来源：[IronClaw GitHub Repository](https://github.com/nearai/ironclaw)*

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

# LobsterAI 项目动态日报 — 2026-08-15

> **项目健康度：高**。过去24小时合入22个PR并发布1个新版本，项目处于快速迭代阶段；Issue侧活跃度偏低（仅2条），社区讨论热度一般，需关注长尾积压问题。


## 1. 今日速览

LobsterAI 过去24小时处于**高活跃度发布/合入期**：共处理27条PR（22条已合并/关闭），发布 `2026.8.14` 版本，涵盖侧边栏日历签到与横幅轮播、多智能体任务筛选、cowork 过程折叠修复、OpenClaw 技能键值修复等一系列功能与稳定性改进。Issue 侧活跃度偏低，仅新增1条功能请求和1条测试覆盖请求，社区反馈量不大。**主要关注点**：PR 合入节奏快、质量把控较好（依赖升级仍走 Dependabot 通道），但一批 4 月前遗留的旧 PR（含中文功能请求）仍未得到明确处理。


## 2. 版本发布

### LobsterAI 2026.8.14（发布于 2026-08-14）

**主要更新内容：**

| 变更类型 | 内容 | 对应 PR |
|---------|------|---------|
| ✨ 新功能 | 侧边栏支持签到与横幅轮播 | #2411 |
| ✨ 新功能 | 侧边栏增加多智能体任务活动筛选 | #2418 |
| ✨ 新功能 | 用户可在 **Settings → General** 中永久隐藏侧边栏广告横幅（回应 Issue #2342） | #2374 |
| 🖼️ UI 改进 | 账户积分图标换新（堆叠点数新样式，适配明暗主题） | #2494/#2492 |
| 🖼️ UI 改进 | 默认 UI/代码字号提升，并带一次性迁移 | #2495 |
| 🐛 修复 | cowork 回合过程在答案生成前不再过早折叠 | #2499 |
| 🐛 修复 | OpenClaw 技能按 frontmatter name 而非目录 ID 索引（修复前后端键不匹配，使 UI 技能开关真正生效） | #2483/#2491 |
| 🐛 修复 | 会话导出图片与卡片切换 UI 修复 | #2493 |
| 🔤 文案 | cowork goal 与 steer 文案改进（i18n） | #2497 |

**⚠️ 破坏性变更 / 迁移注意：**

- `rimraf` 从 5.0.10 升级至 6.1.3（待合入），**行为变更**：6.x 迁移至原生 `fs/promises`，不再支持同步 API `rimraf.sync()`——如项目有使用同步删除的代码需适配。
- `vite` 从 5.4.21 升级至 8.2.1（待合入），**跨大版本跃迁**，需验证 dev server、构建产物及插件生态的兼容性，建议安排专门的回归测试。

> 注：发布说明中未提供完整变更列表，以上为可见 PR 内容的汇总。


## 3. 项目进展

过去24小时合入的 PR 主要集中在 **cowork 模块体验打磨、OpenClaw 正确性修复、账户 UI 细节改进** 三个方向。重点如下：

**cowork 体验连续性修复**
- `#2499` 保持回合过程展开直到答案出现，避免用户误判为失败
- `#2496` 徽章 popover 限制在视口内且不遮挡后续消息
- `#2490` 浏览器标注截图以编号卡片形式展示在用户消息中，并支持在 artifact 面板专用视图打开（替代通用图片预览弹窗），并支持全页截图捕获与归一化
- `#2493` 会话导出图片与卡片切换 UI 修复

**OpenClaw 集成正确性修复**
- `#2483`/`#2491` 修复技能启用开关失效问题——根因是 `resolveSkillKey()` 按 frontmatter name 解析开关覆盖，但 LobsterAI 用目录 ID 写入 `skills.entries`，两者不一致导致静默失效。两日内双 PR 合入（后者为前者的更强版本），修复思路一致，建议后续合并时确认无重复提交。

**账户/UI 细节**
- `#2495` 默认字号提升并附带一次性迁移（避免重复执行）；`#2494`/`#2492` 账户积分图标更新与明暗主题颜色对齐。

**关于 #2422/#2423（Liuzhq/fix btw tools 及其 Revert）**：两日内先后合入和回滚，疑似功能有未预见的回归。此类 revert 链应重点关注后续是否有修复版跟进。


## 4. 社区热点

过去24小时讨论热度整体偏低。最受关注的话题是 **为 commandSafety 和 coworkMemoryJudge 补充单元测试**：

- **Issue #1154** — 讨论最活跃（1条评论）  
  [netease-youdao/LobsterAI Issue #1154](https://github.com/netease-youdao/LobsterAI/issues/1154)  
  由 `MaoQianTu` 于 2026-03-31 提出，至今已积压 4 个多月。诉求明确且专业：`commandSafety.ts`（危险命令检测，被 coworkRunner 和 IM 自动审批共用）与 `coworkMemoryJudge.ts`（记忆候选质量评分）均为核心安全/质量模块却无任何测试覆盖，建议补充 Vitest 单元测试。该 issue 同时标记为 `[stale]`，需维护者确认是否仍在处理。

- **Issue #2489** — “快更新v4pro！”  
  [netease-youdao/LobsterAI Issue #2489](https://github.com/netease-youdao/LobsterAI/issues/2489)  
  作者 `nimamasl114514`，2026-08-14 创建。无实质描述内容，推测为催促 v4 Pro 版本的发布。此类低质量 issue 无信息量，建议标记「需要更多信息」或关闭。


## 5. Bug 与稳定性

| 严重程度 | 问题描述 | 状态 | 关联 PR |
|---------|---------|------|---------|
| 🟠 中 | **OpenClaw 技能启用开关静默失效**：LobsterAI 以目录 ID 写入 `skills.entries`，而 OpenClaw 按 frontmatter name 解析开关，导致 UI 技能开关操作无效果 | ✅ 已修复（#2483，增强版 #2491 同日合入） | [#2491](https://github.com/netease-youdao/LobsterAI/pull/2491) |
| 🟡 低 | **cowork 回合过早折叠**：回合停止流式但不代表结束（如 sessions_yield 等待父进程时），被折叠成空时长行，用户误判失败 | ✅ 已修复（#2499） | [#2499](https://github.com/netease-youdao/LobsterAI/pull/2499) |
| 🟡 低 | **徽章 popover 溢出视口**：超出视口或被后续消息遮挡 | ✅ 已修复（#2496） | [#2496](https://github.com/netease-youdao/LobsterAI/pull/2496) |
| ⚪ 需关注 | **Liuzhq/fix btw tools 被回滚**（#2422 合入后 #2423 revert） | ⚠️ 已回滚，无跟进版 | [#2423](https://github.com/netease-youdao/LobsterAI/pull/2423) |

另外有一批 **4 月前创建但近期才标注 stale 并关闭** 的修复类 PR（#1228、#1231 等），虽然状态为已关闭，但需确认这些修复是否已以其他方式进入主线，避免功能遗漏。


## 6. 功能请求与路线图信号

| 功能请求 | 来源 | 状态/信号 |
|---------|------|-----------|
| **持久隐藏侧边栏广告横幅** | Issue #2342 → PR #2374 | ✅ 已纳入 2026.8.14 版本（Settings → General 新增开关） |
| **commandSafety / coworkMemoryJudge 单元测试** | Issue #1154 | ⚠️ 4+ 月未响应，已标记 stale；核心安全模块无测试覆盖，建议优先排期 |
| **会话「标记为未读」** | PR #1228（2026-04-01 创建） | 🔍 已关闭但未在 Release Notes 中确认合入，需核实在哪个版本落地 |
| **会话内页内搜索（Ctrl+F）** | PR #1155（2026-03-31 创建） | 🔍 已关闭未确认合入；建议从关闭原因推断是否已通过其他方式实现 |

**路线图判断**：广告横幅持久隐藏确认进入产品，说明项目对商业化 UI 的用户诉求响应较快；侧边栏新增签到与横幅轮播表明在探索用户增长/留存玩法。安全相关测试覆盖的诉求长期未响应是当前路线图中明显的短板。


## 7. 用户反馈摘要

- **对安全隐患的担忧**（Issue #1154）：贡献者明确指出 `commandSafety.ts` 误判将导致 AI 静默执行 `rm -rf`、`git push --force` 等破坏性命令，评分模块出错会污染用户记忆写入。用户对 AI 安全边界有较高期待，缺乏测试覆盖会削弱对项目的信任感。
- **版本更新催促**（Issue #2489）：有用户急切等待 v4 Pro 版本。虽难以从单一 issue 判断具体诉求，但结合团队版（Team Edition）账户和配额流程的引入（PR #2498），推测用户对 Team/Pro 版本能力有明确期待，建议官方发布节奏或路线图更透明化。
- **UI 横幅困扰**（Issue #2342）：多个用户对侧边栏广告横幅不满，新版本已提供持久关闭方案。此类「商业化 vs 用户体验」的矛盾需持续关注比例与默认行为。


## 8. 待处理积压

以下为长期未得到明确响应的 Issue/PR，提醒维护者关注：

| 类型 | 编号 | 标题 | 创建时间 | 备注 |
|------|------|------|---------|------|
| Issue | [#1154](https://github.com/netease-youdao/LobsterAI/issues/1154) | 为 commandSafety 和 coworkMemoryJudge 补充 Vitest 单元测试 | 2026-03-31 | 4.5 个月未响应，已标记 stale；核心安全模块建议尽快排期 |
| PR | [#1153](https://github.com/netease-youdao/LobsterAI/pull/1153) | 修复 buildOpenAIChatCompletionsURL 处理 Google Gemini /v1 路径时 URL 拼接错误 | 2026-03-31 | 已标记 stale；URL 拼接缺陷可能影响 Gemini 用户，建议核实是否已通过其他 PR 修复 |
| PR | [#1155](https://github.com/netease-youdao/LobsterAI/pull/1155) | feat(cowork): 会话内页内搜索（Ctrl+F） | 2026-03-31 | 4.5 个月未处理；功能已实现，从描述看质量较高（TreeWalker + CSS Custom Highlight API），建议评估是否合入 |
| PR | [#2374](https://github.com/netease-youdao/LobsterAI/pull/2374) | feat: 添加持久隐藏侧边栏广告横幅设置 | 2026-07-21 | 今日随新版本合入 ✅，已移除积压 |
| PR | [#2460](https://github.com/netease-youdao/LobsterAI/pull/2460) | chore(deps-dev): bump rimraf 5→6 | 2026-08-10 | Dependabot 提的待合并 PR；跨大版本，需注意 `rimraf.sync()` 移除 |
| PR | [#2465](https://github.com/netease-youdao/LobsterAI/pull/2465) | chore(deps-dev): bump vite 5→8 | 2026-08-10 | 跨 3 个大版本；建议独立分支验证后合入 |

> **维护者建议**：项目 PR 合入效率高、版本迭代快，但 Issue 侧响应明显滞后（4 个月未响应的问题未被关闭或转移），建议建立 issue 定期 triage 机制（如「30 天无响应自动标记并提醒」），避免社区贡献者流失。


*报告生成时间：2026-08-15 | 数据来源：netease-youdao/LobsterAI GitHub 仓库 | 数据窗口：过去 24 小时*

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

# Moltis 项目动态日报 — 2026-08-15

## 1. 今日速览

过去 24 小时 Moltis 项目整体活跃度较低：**无新增或关闭的 Issue，也无版本发布**；仅有 1 条 PR 处于待合并状态（#1190）。项目当前处于功能开发的酝酿期，**唯一的 PR 涉及范围较大**（连接器持久化、调度、全文搜索等），可能需要较长时间的 review 和社区讨论。项目整体健康度稳定，社区反馈平淡，未见紧急 Bug 或重大回归报告。

---

## 3. 项目进展

### 待合并 PR（重要，未合并）

| PR | 标题 | 作者 | 最后更新 | 说明 |
|----|------|------|----------|------|
| [#1190](https://github.com/moltis-org/moltis/pull/1190) | Add durable calendar, channel, and email connectors | penso | 2026-08-14 | **OPEN** |

**要点提炼：**

- 引入**供应商无关的连接器持久化机制**，包含原子快照、调度、投影和本地受限全文搜索。
- 新增**只读的 CalDAV、Gmail、Himalaya v2 及可复用的频道历史数据集**，数据使用供应商自有 schema，**不涉及凭证复制**。
- 加入**按供应商划分的信任边界**设计。

**影响评估：** 该 PR 是 Moltis 在**连接器生态扩展**方向上的重大基础设施升级，若合并，将显著提升多源数据集成能力和本地检索能力，并为后续新连接器接入奠定标准。

---

## 4. 社区热点

过去 24 小时内无新 Issue 或 PR 评论活动集中产生。现有 PR #1190 已存在 4 天（创建于 08-11，更新于 08-14），捕获的讨论相对有限（无评论数据标注），但从改动范围来看，其涉及的**持久化与信任边界**话题预计将成为社区近期关注焦点。

---

## 5. Bug 与稳定性

过去 24 小时**无新增 Bug 报告**，无崩溃或回归问题提交。项目当前稳定性表现良好，未见需要紧急介入的缺陷。

---

## 6. 功能请求与路线图信号

当前无独立的新功能 Issue 提交。但在 **PR #1190** 中隐含了明确的产品方向信号：

- **多供应商连接器持久化与调度能力** — 意味着 Moltis 在向“长期运行的数据同步与集成平台”方向演进；
- **本地全文搜索支持**（有界范围） — 显示对**离线/本地优先**使用场景的重视；
- **CalDAV + Gmail + Himalaya v2 只读适配** — 暗示下一阶段将覆盖**日历与邮件领域的数据接入**。

以上特性若合并，极有可能进入下一版本（如 v0.x 或 v1.0 的功能集）。

---

## 7. 用户反馈摘要

过去 24 小时内无新 Issue 评论或用户反馈输入。暂无第一手用户痛点或使用场景反馈可供提炼。

---

## 8. 待处理积压

目前仅有 **PR #1190** 处于待处理状态，且已存在 4 天。考虑到其改动量较大，建议维护者：

- 明确 review 计划和时间表，避免长时间悬挂；
- 就**信任边界设计**和**持久化性能**征求更广泛的社区反馈，尤其是对安全敏感的集成场景。

> 链接：[https://github.com/moltis-org/moltis/pull/1190](https://github.com/moltis-org/moltis/pull/1190)

---

*本报告基于 GitHub 公开数据自动生成，仅供参考。*

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

# CoPaw 项目动态日报 — 2026-08-15

> 数据来源：github.com/agentscope-ai/CoPaw | 统计周期：2026-08-14 全天


## 1. 今日速览

过去 24 小时 CoPaw 项目保持高活跃度：**50 条 Issue 更新、41 条 PR 更新**，其中 Issue 关闭率达 **76%**（38/50），显示出维护团队响应速度良好。值得关注的是，**今日无新版本发布**，但 PR 侧引入了多项值得关注的新功能（动态技能加载、DataPaw 应用运行时、每会话模型覆盖），另有大批 PR 处于收尾阶段。社区讨论集中于 **MCP 工具兼容性、会话管理（拆分/单条删除）、聊天标题自动同步、桌面端自动更新** 等真实使用场景，用户对 Windows 桌面端体验和本地模型支持有持续诉求。


## 2. 版本发布

**无新版本发布。** 距上一版本（v2.1.0）已过去一段观察期，目前有 1 个 PR（#6908 升级 agentscope 至 2.0.6）等待合并，预计将在下次发版时纳入。


## 3. 项目进展

今日无 PR 被合并，但以下 PR 正处于活跃评审状态，部分已接近合并：

| PR | 标题 | 状态 | 说明 |
|---|---|---|---|
| [#7033](https://github.com/agentscope-ai/QwenPaw/issues/7033) | 动态技能加载+自动卸载+frontmatter修复 | OPEN | 为技能系统引入运行时生命周期管理，修改后重新提交 |
| [#7032](https://github.com/agentscope-ai/QwenPaw/issues/7032) | 聊天标题自动同步 | OPEN | 自动记忆关联的标题刷新，修改后重新提交 |
| [#6969](https://github.com/agentscope-ai/QwenPaw/issues/6969) | 修复 MCP 结构化内容导致工具结果重复写入 | OPEN | 对应 Issue #6958，修复方案已明确 |
| [#6940](https://github.com/agentscope-ai/QwenPaw/issues/6940) | 新增 DataPaw 应用运行时和持久化分析工作区 | OPEN | 首次贡献者提交，功能体量较大 |
| [#5992](https://github.com/agentscope-ai/QwenPaw/issues/5992) | 每会话模型覆盖 | OPEN | 长期在评审中（7月至今），功能较为完整 |
| [#6302](https://github.com/agentscope-ai/QwenPaw/issues/6302) | 统一 Provider 发现/模型元数据/路由/Agent 控制 | OPEN | 涉及核心架构，评审周期预计较长 |
| [#7035](https://github.com/agentscope-ai/QwenPaw/issues/7035) | 控制台子代理会话分组 | OPEN | UI 改进，无破坏性变更 |
| [#7036](https://github.com/agentscope-ai/QwenPaw/issues/7036) | 媒体附件下载控制 | OPEN | UI 改进，补充音频下载按钮 |
| [#6869](https://github.com/agentscope-ai/QwenPaw/issues/6869) | 后台任务超时统一 | OPEN | 统一 submit_to_agent/CLI/spawn_subagent 超时契约 |

**总体评价：** 项目在核心架构层（Provider 统一、会话生命周期）和体验层（技能动态加载、标题同步、媒体下载）都有实质推进，但核心 PR 的合并速度偏慢，需关注。


## 4. 社区热点

今日讨论最集中的议题：

1. **[#3045] 自动获取模型不可用（已关闭，8 评论）** — [链接](https://github.com/agentscope-ai/QwenPaw/issues/3045)  
   用户报告模型自动获取失败，引发较多讨论和排查建议，最终在今日关闭。从 Issue 已关闭状态来看问题已解决或定位到原因。

2. **[#7010] QwenPaw 缺少真正的后台/守护模式（已关闭，6 评论）** — [链接](https://github.com/agentscope-ai/QwenPaw/issues/7010)  
   用户通过 SSH 启动 `qwenpaw app` 时命令一直挂住。该诉求涉及部署场景，反馈指向缺失 daemon 模式。今日已关闭，建议关注关闭时的解决方案说明。

3. **[#7011] Console 停止请求误取消飞书会话（持续更新，5 评论）** — [链接](https://github.com/agentscope-ai/QwenPaw/issues/7011)  
   2.1.0 版本中多 UI 会话下会话身份串线，作者更新了最新发现。这是一个较严重的 Bug，当前为 OPEN 状态，关联飞书渠道。

4. **[#4001] 对话中手动删除单条消息（OPEN，4 评论）** — [链接](https://github.com/agentscope-ai/QwenPaw/issues/4001)  
   用户希望像微信那样支持单条消息删除，包含误发消息、隐私保护等场景。该请求从 5 月至今未关闭，反应了较强的功能诉求。

5. **[#7025] QwenPaw Creator 插件导致其他插件全部失效（OPEN，4 评论）** — [链接](https://github.com/agentscope-ai/QwenPaw/issues/7025)  
   安装 Creator 插件后所有插件失效，附带截图和日志。反映插件隔离机制存在缺陷。


## 5. Bug 与稳定性

按严重程度排列今日报告的 Bug：

| 严重度 | Issue | 标题 | 状态 | 是否有 Fix PR |
|---|---|---|---|---|
| **高** | [#7011](https://github.com/agentscope-ai/QwenPaw/issues/7011) | Console 停止请求误取消飞书会话（2.1.0） | OPEN | 无 |
| **高** | [#7025](https://github.com/agentscope-ai/QwenPaw/issues/7025) | QwenPaw Creator 插件导致所有插件失效 | OPEN | 无 |
| **中** | [#7016](https://github.com/agentscope-ai/QwenPaw/issues/7016) | 工具调用 404（流式会话轮询 offload 接口） | OPEN | 无 |
| **中** | [#6958](https://github.com/agentscope-ai/QwenPaw/issues/6958) | FastMCP 工具结果写入两份重复数据 | OPEN | [#6969](https://github.com/agentscope-ai/QwenPaw/pull/6969) 待评审 |
| **中** | [#6972](https://github.com/agentscope-ai/QwenPaw/issues/6972) | Chrome 扩展 WebSocket 发送 tab.create 后断连 | CLOSED | — |
| **低** | [#7040](https://github.com/agentscope-ai/QwenPaw/issues/7040) | “Stop Running”拼写错误（“Stopp Running”） | CLOSED | 已标记 invalid |

**稳定性整体评价：** 今日关闭的 Bug 数量远多于新开（38 vs 12），维修效率高。但 2.1.0 版本暴露的多会话身份串线问题（#7011）和插件隔离问题（#7025）值得重视，建议优先排查。


## 6. 功能请求与路线图信号

今日收集到的功能需求信号如下：

| 功能 | 来源 Issue | 相关 PR | 信号强度 |
|---|---|---|---|
| 动态技能加载/卸载 | — | [#7033](https://github.com/agentscope-ai/QwenPaw/issues/7033) | 高（代码已完成） |
| 聊天标题自动同步 | — | [#7032](https://github.com/agentscope-ai/QwenPaw/issues/7032) | 高（代码已完成） |
| 每会话模型覆盖 | — | [#5992](https://github.com/agentscope-ai/QwenPaw/issues/5992) | 中（长期评审中） |
| 对话中单条消息删除 | [#4001](https://github.com/agentscope-ai/QwenPaw/issues/4001) | 无 | 中（用户持续追问） |
| 会话拆分（部分消息转移到新会话） | [#4436](https://github.com/agentscope-ai/QwenPaw/issues/4436) | 无 | 中 |
| 桌面端自动更新 | [#2846](https://github.com/agentscope-ai/QwenPaw/issues/2846)、[#3464](https://github.com/agentscope-ai/QwenPaw/issues/3464) | 无 | 中（多次被提出） |
| 支持 OpenAI Responses API 格式 | [#3002](https://github.com/agentscope-ai/QwenPaw/issues/3002)、[#944](https://github.com/agentscope-ai/QwenPaw/issues/944)、[#2737](https://github.com/agentscope-ai/QwenPaw/issues/2737) | 无 | 中（三个 Issue 有共同主线） |
| 支持 Computer Use | [#5551](https://github.com/agentscope-ai/QwenPaw/issues/5551) | [#7037](https://github.com/agentscope-ai/QwenPaw/issues/7037)（观察相关窗口） | 中（已有初步 PR） |
| 本地 GGUF 模型一键运行 | [#6433](https://github.com/agentscope-ai/QwenPaw/issues/6433) | 无 | 中 |
| 零配置后台运行模式 | [#7010](https://github.com/agentscope-ai/QwenPaw/issues/7010) | 无 | 中 |

**路线图判断：** 动态技能加载、标题自动同步、Computer Use 相关支撑最有可能进入下一版本；“单条消息删除”和“会话拆分”在需求侧信号持续增强，建议排期。


## 7. 用户反馈摘要

从今日活跃的 Issue 评论中提炼的用户真实反馈：

- **部署与运维痛点**：多名用户（#7010、#2846、#3464）表示桌面端更新流程繁琐（需卸载后重装），同时缺少守护进程模式影响远程部署。这体现了产品在“生产环境可用性”方面需要补强。
- **MCP 使用困惑**：#6405 用户升级 2.0 后 MCP 工具频繁提示 Tool not found，从工具名格式到调用链路都缺少清晰的排查指引。
- **插件生态完善度**：#7025 用户安装 Creator 插件后其他插件全部失效，影响信任度；#6819 指出 Channel 工具在需要审批时无提示，用户无法判断工具状态。
- **对话体验精细化需求**：#4001 提出的单条消息删除被用户反复提及，涉及误发、隐私保护等场景，说明用户在将 CoPaw 用于真实工作流而非简单测试。
- **文档错别字**：#7040 用户反馈多个按钮文案拼写错误（“Stopp Running”），虽是小事但影响产品专业度感知。


## 8. 待处理积压

以下 Issue/PR 长期未获响应或长期处于评审中，建议维护团队关注：

| 类型 | 编号 | 标题 | 创建时间 | 最后活跃 | 积压天数 |
|---|---|---|---|---|---|
| Issue | [#2418](https://github.com/agentscope-ai/QwenPaw/issues/2418) | 新增 skills-hub 管理页面 | 2026-03-27 | 2026-08-14 | ~140 天 |
| Issue | [#2314](https://github.com/agentscope-ai/QwenPaw/issues/2314) | Provider 无关的会话历史格式 | 2026-03-26 | 2026-08-14 | ~141 天 |
| Issue | [#2554](https://github.com/agentscope-ai/QwenPaw/issues/2554) | 定时任务支持不投递 | 2026-03-30 | 2026-08-14 | ~137 天 |
| Issue | [#4731](https://github.com/agentscope-ai/QwenPaw/issues/4731) | Edge 浏览器启动失败退出码 21（Windows 11） | 2026-05-27 | 2026-08-14 | ~79 天 |
| PR | [#5992](https://github.com/agentscope-ai/QwenPaw/issues/5992) | 每会话模型覆盖（首个贡献者） | 2026-07-12 | 2026-08-14 | 评审中 ~34 天 |
| PR | [#2105](https://github.com/agentscope-ai/QwenPaw/issues/2105) | Whisper 安装文档（首个贡献者） | 2026-03-23 | 2026-08-14 | 评审中 ~144 天 |

**特别提醒：** PR #2105（Whisper 文档）已滞留评审近 5 个月，作为 first-time-contributor 的提交，长时间不处理会影响社区贡献积极性。PR #5992 的功能本身高频被社区讨论引用，建议加速评审或给出明确方向。

---

*本日报由 AI 分析师基于 GitHub 公开数据自动生成，仅供参考。*

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

好的，作为您的 AI 智能体与个人 AI 助手领域开源项目分析师，这是为您生成的 **ZeroClaw 项目动态日报 (2026-08-15)**。

---

# ZeroClaw 项目日报 — 2026-08-15

## 1. 今日速览

ZeroClaw 项目今日处于**高活跃度、高讨论密度**的状态。过去 24 小时内，Issue 和 PR 的更新量均处于高位（33 条 / 50 条），主要集中在**安全架构**、**协议兼容性**（如 OpenAI Chat Completions）和 **Agent 运行时可靠性**等核心领域。虽然暂无新版本发布，但社区围绕多个重量级 RFC 的讨论愈演愈烈，且修复类 PR 的提交速度显著加快，表明项目正处于密集的架构演进与稳定性加固阶段。项目健康度良好，但存在大量已接受 RFC 待落地和 #9965 等测试不稳定问题，需警惕技术债累积。

## 2. 版本发布

**无新版本发布。**

## 3. 项目进展

过去 24 小时内暂无 PR 被合并（数据源显示已合并/关闭 3 条，但未列出具体条目）。不过，今日新增了多个针对已接受 RFC 的**实现性 PR**，这表明项目正从讨论阶段快速迈向落地执行，是项目向前迈出的关键一步。

- **安全策略落地与修复**：
  - **[PR #9996] fix(security): make action budget accounting atomic**：该 PR 由核心维护者 Audacity88 提交，旨在修复并发场景下 `max_actions_per_hour` 限额可能被超出的问题。将动作预算计费原子化，是安全策略实现精细化的关键补丁。
  - **[PR #10002] fix(tools): accept camelCase segments in google_workspace validation**：修复了 Google Workspace 工具因不接受驼峰命名（如 `calendarList`）而无法正常工作的问题。

- **渠道功能增强**：
  - **[PR #9997] feat(channels/telegram): add secure model picker**：实现了 Issue #9895 中提出的 Telegram `/model` 命令的提供者分组、分页选择器，显著改善了移动端的用户体验。
  - **[PR #9994] feat(zerocode): add transcript copy context menu**：为 ZeroCode 界面增加了右键复制菜单，提升了可用性。

- **运行时健壮性改进**：
  - **[PR #9999] fix(compatible): classify output-limited terminal responses**：解决了 Issue #9421 中关于“不完整终态响应被误报为成功”的问题。该修复针对 OpenAI 兼容接口的 `finish_reason: "length"` 进行了分类，确保由输出限制导致的截断被正确识别为失败，而非成功。

- **CI 基础设施优化**：
  - **[PR #9985] ci(runners): extend Blacksmith to msrv, parallel-runtime-test, installer-drift**：进一步扩展了 Blacksmith 自定义 Runner 的使用范围，旨在加速 CI 流程，缩短验证时间。

## 4. 社区热点

今日社区讨论热度最高的几个议题，反映了开发者对 **ZeroClaw 作为通用 Agent 平台**的强烈期待：

- **[Issue #8303] RFC: Goal mode v1 — bounded foreground Matrix work** (22 评论)
  该 RFC 旨在为 ZeroClaw 引入“目标模式（Goal mode）”，使其能够在多个 Agent 轮次中追踪一个有界的目标。这是从“对话式助手”迈向“任务执行者”的关键一步。高讨论度表明社区对**复杂任务编排**和**长时任务执行**有明确需求。
  [链接](https://github.com/zeroclaw-labs/zeroclaw/issues/8303)

- **[Issue #7155] RFC: Add a per-execution confirmation tier for high-risk shell commands** (20 评论)
  这是对安全领域的直接呼声，希望引入类似 Claude Code 的 `allow/ask/deny` 命令策略。用户渴望在不牺牲安全性的前提下获得更流畅的自动化体验，讨论聚焦于如何在“安全”与“效率”之间找到平衡点。
  [链接](https://github.com/zeroclaw-labs/zeroclaw/issues/7155)

- **[Issue #8603] RFC: ZeroClaw Chat Completions profile** (19 评论)
  社区对**生态兼容性**的需求强烈，希望 ZeroClaw 能成为 OpenAI Chat Completions 协议的后端，以无缝接入 Open WebUI、LobeChat、Continue.dev 等成熟的客户端生态。若该 RFC 落地，将极大降低用户接入门槛。
  [链接](https://github.com/zeroclaw-labs/zeroclaw/issues/8603)

## 5. Bug 与稳定性

今日反馈的 Bug 主要集中于平台兼容性、安全边界和测试稳定性上。

- **高优先级 (P1)**:
  - **[Issue #9421] [Bug]: Incomplete terminal responses can be reported as successful** — `S1`级别，工作流受阻。好消息是 **已有对应修复 PR #9999**，正在审查中，且 **PR #9999** 是对此的直接修复。
  [链接](https://github.com/zeroclaw-labs/zeroclaw/issues/9421)
  - **[Issue #7462] [Bug]: 74 test failures on Windows** — `S2`级别，CI 覆盖盲区导致 Windows 平台存在大量测试失败，影响跨平台可靠性。
  [链接](https://github.com/zeroclaw-labs/zeroclaw/issues/7462)
  - **[Issue #9919] fix(memory): reject Qdrant in builder-only factory without storage config** — 内存后端配置错误可能导致静默切换到错误的持久化层，存在数据安全隐患。
  [链接](https://github.com/zeroclaw-labs/zeroclaw/issues/9919)

- **中优先级 (P2)**:
  - **[Issue #9486] [Bug]: High-entropy detector redacts Solana wallet addresses** — `S2`级别，错误地拦截了合法用户数据（加密货币地址），影响特定场景下的正常工作流。
  [链接](https://github.com/zeroclaw-labs/zeroclaw/issues/9486)
  - **[Bug #9965] cron custom-shell test hits ETXTBSY** — `P1`级别，一个测试不稳定问题，会阻塞无关的 PR 合并，需在 CI 层面解决。
  [链接](https://github.com/zeroclaw-labs/zeroclaw/issues/9965)

## 6. 功能请求与路线图信号

今日讨论与提交中，以下功能表现出较强的落地潜质：

- **Telegram 体验优化**：除了已实现的 PR #9997（模型选择器），Issue #9895 的讨论还显示用户对个性化交互的追求。这些小型、聚焦的改进通常会快速进入开发流程。
- **更强大的 Agent 能力**：Issue #8303 (Goal mode) 和 **PR #9833** (add web_research delegate) 表明项目正试图赋予 Agent 更强、更自主的任务处理能力。`web_research` 通过有界子代理进行搜索-抓取-提炼，是弥补原始搜索工具不足的重要尝试，极有可能被纳入下一版本。
- **“安全策略即代码”**：包括 Issue #7155 和 PR #9839，项目正努力提供更细粒度的、可配置的安全控制。未来可能看到更多类似“策略覆盖层（overlay）”的机制出现。
- **可移植性**：PR #9986 增加导出 Agent 为便携包的功能，这将是企业级部署和分发的重要补充，预计会在后续版本中提供。

## 7. 用户反馈摘要

- **对生态兼容的渴望**：用户明确希望能通过 OpenAI Chat Completions 协议使用现有的工具链（如 Open WebUI、Aider 等）来连接 ZeroClaw，这反映了新项目在推广时面临的“生态适配”挑战。
- **官方托管服务的需求**：在 Issue #9982 中，有用户推荐第三方托管内存服务（尽管被标记为 `wontfix`），这从侧面反映了部分用户希望有“开箱即用”的云端服务，以规避自建基础设施的复杂性。
- **对安全细节的关切**：用户对“高熵数据误删”和“高风险命令执行”非常敏感，特别是涉及加密货币或敏感操作时，任何误报或漏判都会严重影响信任度。
- **对跨平台一致性的抱怨**：Windows 平台上 74 个测试失败，直接冲击了 Windows 开发者用户的信心，他们希望项目能在 CI 中提供与 Linux 同等的保障。

## 8. 待处理积压

以下 Issue/PR 长期未得到维护者响应，或已进入僵持状态，建议维护者关注。

- **长周期已接受 RFC**：多个状态为 `status:accepted` 且 `risk:high` 的 RFC 仍停留在讨论阶段，例如 **#7141** (Pluggable inbound authentication) 和 **#7142** (Runtime-owned security decision pipeline)。这些是安全架构的基石，建议加快“决策记录(ADR)”的撰写并分派实现。
- **等待维护者审核的 PR**：部分 PR 被标记为 `needs-maintainer-review`，且为高优先级修复，如 **[PR #9002]**（保持 viewer 断开后的 Agent turn 存活）和 **[PR #9281]**（配置保存失败时回滚别名）。这些等待时间过长会增加合并成本和冲突风险。
- **测试稳定性问题**：**[Issue #9965]** 虽已标记，但属于 CI 可靠性问题，长期来看会影响开发效率，建议优先处理以避免阻塞主分支合并。
  [链接](https://github.com/zeroclaw-labs/zeroclaw/issues/9965)

---
**数据来源**: GitHub ZeroClaw 仓库 (github.com/zeroclaw-labs/zeroclaw) 公开数据。
**报告日期**: 2026-08-15

</details>

---
*本日报由 [agents-radar](https://github.com/kky-wollu/agents-radar) 自动生成。*