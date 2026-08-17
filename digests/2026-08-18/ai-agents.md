# OpenClaw 生态日报 2026-08-18

> Issues: 500 | PRs: 500 | 覆盖项目: 13 个 | 生成时间: 2026-08-17 22:28 UTC

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

# OpenClaw 项目动态日报 — 2026-08-18

## 1. 今日速览

过去24小时项目活跃度极高，共产生500条Issue更新和500条PR更新。Issue方面以新开和活跃讨论为主（489条），关闭仅11条，说明社区反馈热情高涨但处理速度有待提升；PR方面待合并409条、已合并/关闭91条，合并/关闭率约18%，处于正常偏低水平。值得关注的是，今日无新版本发布，但大量PR已进入"ready for maintainer look"状态，预示着下一版本正在酝酿中。**整体评估：社区活跃度★★★★★，项目健康度★★★★☆（Issue积压较多，需关注）**。


## 2. 版本发布

过去24小时内无新版本发布（Releases: 0）。当前最新版本为 `2026.6.1`（依据 Issue #91009 的版本信息）。多个高优先级 PR 已标记为 "ready for maintainer look"，预计下一版本将集中于稳定性修复和 Web UI 体验优化。


## 3. 项目进展

今日有91个PR被合并或关闭，以下是已合并/关闭的重要PR摘要：

### 安全与治理
- **[feat(security): require acknowledgement for install policy warnings](https://github.com/openclaw/openclaw/pull/116489)（已关闭，security-boundary）** — 该 PR 建立了安装策略警告的外部命令返回机制，支持交互式CLI和Control UI审查可疑插件/技能安装。多平台（macOS、Web UI、CLI）完整支持已落地。
- **[feat(ui): review install policy warnings](https://github.com/openclaw/openclaw/pull/120900)（已关闭，security-boundary）** — 配套的 Control UI 界面让管理员可直接在页面审查安装策略警告并决定是否继续安装，标志着“人类审核循环”功能的完整落地。两者结合构成完整的插件安装安全防线。

### 稳定性修复
- 今日关闭的91个PR中，多数为依赖更新和小型修复。CI 基础设施方面有 **fix(ci): support macOS Bash in shared image helper**（#125290，🦞 diamond lobster 评级）解决了 macOS Bash 3.2 兼容性问题，维持了 CI 跨平台稳定性。

### 关键结论
核心进展集中在**安全治理**方向，通过 #116489 和 #120900 的合并，OpenClaw 的插件安装安全模型已升级为“警告 + 人工确认”模式，具备里程碑意义。


## 4. 社区热点

### 最热门 Issue

1. **[#77598 Track live dev agent behavior and trajectory](https://github.com/openclaw/openclaw/issues/77598)（评论23，👎/👍 1）**
   - **内容**：持续跟踪 Pash 开发代理的 24 小时行为记录，属观察性质。
   - **分析**：社区对 AI 代理自主行为的关注度极高，开发者对“代理如何工作”有浓厚兴趣。作为长期运行笔记，该 Issue 已持续3个多月，反映出社区对开发过程透明化的需求。

2. **[#91009 Codex PreToolUse native hook relay spawns CPU-bound processes](https://github.com/openclaw/openclaw/issues/91009)（评论20，👍 2, P1, 🐚 platinum hermit）**
   - **内容**：Codex 集成的 PreToolUse 钩子会生成多个高 CPU 占用的 `openclaw-hooks` 进程，导致网关 RPC 停滞。
   - **分析**：自 6 月报告以来已持续 2 个多月，涉及 Codex 集成性能问题，是稳定性领域的核心痛点。关联 PR #125384（worker turns node-only）可能部分缓解。

3. **[#68596 Configurable streaming watchdog timeout threshold](https://github.com/openclaw/openclaw/issues/68596)（评论15，👍 8, P2）**
   - **内容**：请求可配置的流式看门狗超时阈值，解决长思考模型（kimi-k2.5、DeepSeek-R1）触发误报问题。
   - **分析**：高赞需求（8 👍），反映长推理模型使用者的真实痛点，属于高优先级功能请求。

4. **[#62505 Coding Agent never completes anything](https://github.com/openclaw/openclaw/issues/62505)（评论15，👍 1, P1, 回归）**
   - **内容**：编码代理在 2026.4.2 后完全不完成任务，仅提供模糊状态更新。
   - **分析**：严重回归（P1），涉及核心编码场景，已持续4个月未修复，是社区重点关切。

5. **[#96834 WhatsApp 1:1: inbound image wedges main lane ~3min](https://github.com/openclaw/openclaw/issues/96834)（评论15，👍 1, P1, 🐚 platinum hermit）**
   - **内容**：WhatsApp 图片消息导致主通道阻塞约3分钟，多模态运行卡在 `active_reply_work`。
   - **分析**：6月报告，已持续近2个月，涉及 WhatsApp 通道的稳定性问题（platinum hermit 评级）。


## 5. Bug 与稳定性

### 🔴 P0（紧急）
- **[#70903 Persistent file-based provider cooldown blocks user for hours](https://github.com/openclaw/openclaw/issues/70903)（P0, 🦞 diamond lobster）** — 计费恢复后仍被持久化的冷却时间阻塞数小时。**无 fix PR**，长期未响应（2026-04-24创建）。⚠️ 注意：该 Issue 虽标记 stale，但 P0 影响严重，需维护者重新评估优先级并尽快给出处理方案。

### 🟠 P1（高）
| Issue | 标题 | 影响 | Fix PR |
|-------|------|------|--------|
| [#91009](https://github.com/openclaw/openclaw/issues/91009) | Codex hook relay CPU-bound 进程 | crash-loop, RPC停滞 | ❌ 无 |
| [#62505](https://github.com/openclaw/openclaw/issues/62505) | Coding Agent 永不完成任务（回归） | session-state, message-loss | ❌ 无 |
| [#96834](https://github.com/openclaw/openclaw/issues/96834) | WhatsApp 图片阻塞主通道 3 分钟 | session-state, message-loss | ❌ 无 |
| [#74586](https://github.com/openclaw/openclaw/issues/74586) | AM 嵌入运行中止 memory_search | session-state | ❌ 无 |
| [#38327](https://github.com/openclaw/openclaw/issues/38327) | "Cannot convert undefined or null to object"（google-vertex） | auth-provider | ❌ 无 |
| [#50093](https://github.com/openclaw/openclaw/issues/50093) | WhatsApp 重连后丢失消息 | message-loss | ❌ 无 |
| [#39476](https://github.com/openclaw/openclaw/issues/39476) | A2A sessions_send 重复消息 | session-state, message-loss | 🔗 [有链接PR](https://github.com/openclaw/openclaw/issues/39476) |
| [#67777](https://github.com/openclaw/openclaw/issues/67777) | 子代理完成投递可能丢失 | session-state, message-loss | ❌ 无 |
| [#86215](https://github.com/openclaw/openclaw/issues/86215) | Codex OAuth 刷新失败阻塞数小时 | auth-provider | ❌ 无 |
| [#53408](https://github.com/openclaw/openclaw/issues/53408) | 长对话后工具参数静默丢失 | session-state | ❌ 无 |
| [#78493](https://github.com/openclaw/openclaw/issues/78493) | sudo 更新导致所有权混乱 | crash-loop | ❌ 无 |
| [#71689](https://github.com/openclaw/openclaw/issues/71689) | SQLite 损坏导致任务注册恢复失败 | session-state, data-loss | ❌ 无 |
| [#53540](https://github.com/openclaw/openclaw/issues/53540) | 大参数工具调用触发"Network connection lost" | session-state, message-loss | ❌ 无 |
| [#97616](https://github.com/openclaw/openclaw/issues/97616) | 钩子/工具子进程泄漏（僵尸进程） | crash-loop | ❌ 无 |

### 🟡 P2（中）
- **[#51429 工作路径被硬编码（wangtao）](https://github.com/openclaw/openclaw/issues/51429)**（P2, 🦞 diamond lobster）— 开发者将个人路径硬编码进代码并被合并发布，引发社区对代码审查流程的质疑。相关 PR #125117 改善插件元数据扫描错误报告，但与此问题无直接关联。
- **[#77930 Discord channel not loaded](https://github.com/openclaw/openclaw/issues/77930)**（P2, 回归）— 从 2026.5.4 起 Discord 通道无法加载。已有 [linked PR](https://github.com/openclaw/openclaw/issues/77930)。
- **[#68105 RTL bidi isolation missing](https://github.com/openclaw/openclaw/issues/68105)**（P2, 🐚 platinum hermit）— 希伯来语/阿拉伯语标点渲染在错误一侧。

### 🟢 值得注意的修复 PR
今日提交的 **fix(agents): stop canceled subagents reporting timeouts** (#125407is, 🐚 platinum hermit) 修复了取消子代理被误报为超时的问题，直接关联核心子代理管理稳定性。


## 6. 功能请求与路线图信号

### 🔥 高热度功能请求（可能进入下版本）

1. **可配置的流式看门狗超时阈值**（[#68596](https://github.com/openclaw/openclaw/issues/68596), 👍 8）— 社区对长推理模型支持需求强烈，已讨论4个月仍在开放状态。同类问题还有 [#58957](https://github.com/openclaw/openclaw/issues/58957)（模型切换静默失败）和 [#67419](https://github.com/openclaw/openclaw/issues/67419)（上下文膨胀浪费 token）。

2. **多机器人/多账户支持**（[#71058](https://github.com/openclaw/openclaw/issues/71058), [#112811](https://github.com/openclaw/openclaw/pull/112811)）— 多个 Teams 机器人支持，已有对应 PR #112811 处于"needs proof"状态，有可能进入下版本。

3. **YAML 配置文件支持**（[#45758](https://github.com/openclaw/openclaw/issues/45758), 👍 2）— 用户对可读性更好的配置格式有需求。

4. **Control UI 增强**（PR #123356、#123535、#125242、#125241）— UI 大幅改善（命令参数、会话目录管理、Markdown 渲染、消息样式），集中在 Web UI 体验优化上。

5. **多索引嵌入内存 + 故障转移**（[#63990](https://github.com/openclaw/openclaw/issues/63990)）— 内存系统的生产级可靠性需求。

6. **MathJax/LaTeX 支持**（[#42840](https://github.com/openclaw/openclaw/issues/42840), 👍 10）— 数学与科学内容呈现需求。

7. **持久任务状态面板**（[#52640](https://github.com/openclaw/openclaw/issues/52640), 👍 2）— 长时运行通道任务需要权威状态展示。

### 📋 路线图信号
- #125384 **refactor(workers): make worker turns node-only** — 扩展标记 `crabbox`，明确执行模式收敛方向，已 "ready for maintainer look"。
- #123482/#123535/#123556 **会话加载性能优化是当前重点** — 多个PR围绕会话目录加载、Git checkout 探测共享、目录刷新风暴解决。
- 安全治理方向（#116489/#120900）已完成，下一阶段可能是更细粒度的权限控制。


## 7. 用户反馈摘要

### 真实痛点

1. **“更新即破坏”的恐惧**（[#62505](https://github.com/openclaw/openclaw/issues/62505)）：*“我的编码代理已经正常工作数周，但更新后什么都不干了。”* — 对版本更新缺乏信心。

2. **配置流程不透明**（[#51429](https://github.com/openclaw/openclaw/issues/51429)）：中文用户发现工作路径被硬编码进发布版，质疑代码审查流程。

3. **长上下文场景的稳定性问题**（[#53408](https://github.com/openclaw/openclaw/issues/53408)）：*“15轮对话后，write 和 exec 工具开始静默丢弃所有参数。”* — 长对话场景下工具调用变得不可靠。

4. **多模态消息阻塞**（[#96834](https://github.com/openclaw/openclaw/issues/96834)）：WhatsApp 发图导致3分钟无响应，用户体验严重受损。

5. **资源空转**（[#97616](https://github.com/openclaw/openclaw/issues/97616)）：僵尸进程累积导致运行缓慢 — 长期运行实例的稳定性问题。

6. **配置项缺失**（[#71142](https://github.com/openclaw/openclaw/issues/71142)）：Control UI 文件上传硬编码 5MB 限制，无法满足图片上传需求。

### 满意点
- **安装策略警告审查功能**获得正面评价（PR #116489/#120900）
- 用户认可 OpenClaw 在 Telegram、Home Assistant 等场景的实用性（[#73537](https://github.com/openclaw/openclaw/issues/73537) 用户致谢）
- 社区积极使用和反馈，项目有真实活跃用户群

### 社区情绪
整体情绪偏向“**功能强大但稳定性欠佳**”。用户认可 OpenClaw 的能力，但对更新带来的回归、长场景下的不稳定性和部分问题修复周期长表示不满。P0/P1 问题平均存活时间超过4个月（部分已超5个月），修复速度难以匹配社区期望。


## 8. 待处理积压

### ⚠️ 长期未响应/未解决的关键 Issue（按严重程度排序）

| Issue | 优先级 | 创建时间 | 存活天数 | 最后更新 | 状态 |
|-------|--------|----------|----------|----------|------|
| [#70903](https://github.com/openclaw/openclaw/issues/70903) Provider cooldown 阻塞用户 | **P0** | 2026-04-24 | **116天** | 08-17 | 无 fix PR，标记 stale |
| [#38327](https://github.com/openclaw/openclaw/issues/38327) Google Vertex 无法使用 | **P1** | 2026-03-06 | **165天** | 08-17 | 无 fix PR |
| [#62505](https://github.com/openclaw/openclaw/issues/62505) Coding Agent 永不完成任务 | **P1** | 2026-04-07 | **133天** | 08-17 | 无 fix PR，社区强烈关注 |
| [#50093](https://github.com/openclaw/openclaw/issues/50093) WhatsApp 消息丢失 | **P1** | 2026-03-19 | **152天** | 08-17 | 无 fix PR |
| [#91009](https://github.com/openclaw/openclaw/issues/91009) Codex hook CPU 问题 | **P1** | 2026-06-06 | **73天** | 08-17 | 无 fix PR |
| [#53540](https://github.com/openclaw/openclaw/issues/53540) 大参数工具调用断开 | **P1** | 2026-03-24 | **147天** | 08-17 | 无 fix PR |
| [#53408](https://github.com/openclaw/openclaw/issues/53408) 长对话工具参数丢失 | **P1** | 2026-03-24 | **147天** | 08-17 | 无 fix PR |
| [#96834](https://github.com/openclaw/openclaw/issues/96834) WhatsApp 图片阻塞 | **P1** | 2026-06-25 | **54天** | 08-17 | 无 fix PR，需 live-repro |

### ⏳ 长期待审 PR

| PR | 标题 | 创建时间 | 存活天数 | 状态 |
|----|------|----------|----------|------|
| [#112811](https://github.com/openclaw/openclaw/pull/112811) | 多 Teams 机器人支持 | 2026-07-23 | 26天 | needs proof |
| [#120443](https://github.com/openclaw/openclaw/pull/120443) | Codex 线程绑定+自动压缩修复 | 2026-08-08 | 10天 | needs proof |
| [#80396](https://github.com/openclaw/openclaw/pull/80396) | MEDIA token 跳过警告 | 2026-05-10 | 100天 | waiting on author |

### 📌 维护者关注建议
1. **#70903 (P0)** 已存活116天且标记 stale，但 P0 影响严重，建议维护者重新评估优先级并尽快给出处理方案。
2. **#62505** 和 **#38327** 分别存活133天和165天，均为 P1 回归，社区讨论热度高但缺乏官方回应。建议在项目路线图中明确优先级或给出预期修复时间。
3. **#51429** 涉及代码审查流程漏洞（硬编码路径被合并），建议团队排查是否存在类似问题并加强审查。
4. 多个 P1 问题（#91009、#96834、#74586、#67777 等）均标记 `needs-live-repro`，建议维护者协调资源优先复现，或考虑通过远程调试会话加速诊断。
5. **PR #125407**（取消子代理误报超时修复）虽仅提交1天，但与 P1 子代理稳定性问题直接相关，建议优先review。

---

## 横向生态对比

# 个人AI助手与自主智能体开源生态横向对比分析报告

**报告日期**: 2026-08-18  
**数据窗口**: 2026-08-17 至 2026-08-18 (UTC)

---

## 1. 生态全景

当前个人AI助手/自主智能体开源生态正处于 **从"可用"向"可信"转型的关键阶段**。各项目普遍面临稳定性与功能的拉锯战——OpenClaw、ZeroClaw、NanoClaw等核心项目在快速迭代功能的同时，均出现了P0/P1级Bug积压超过百天的情况，反映出社区需求增长已超出维护者处理能力。与此同时，安全治理（插件安装审查、密钥管理、附件沙箱）和跨平台支持（Windows/macOS CI覆盖）正成为各项目共同投入的优先方向。生态整体呈现"**功能先行、安全补课、稳定性欠债**"的特征，而多项目不约而同地收到"接入OpenAI兼容协议"和"本地Web界面"的社区诉求，表明用户希望将智能体嵌入既有工具链的强烈意愿。

---

## 2. 各项目活跃度对比

| 项目 | Issues (24h) | PRs (24h) | Release | 健康度评估 |
|------|-------------|-----------|---------|-----------|
| **OpenClaw** | 500更新 (489新开) | 500更新 (91合并/关闭) | 无 (最新 2026.6.1) | ★★★★☆ 活跃度极高，Issue积压严重 |
| **ZeroClaw** | 50更新 (47活跃) | 50更新 (9合并) | 无 (最新 v0.8.4) | ★★★★☆ 安全加固密集，PR审查积压 |
| **Hermes Agent** | 50更新 | 50更新 (9合并) | **v2026.8.16.2 (v0.20.3)** | ★★★★☆ 高速迭代，更新机制脆弱 |
| **NanoClaw** | 4更新 | 34更新 (21合并) | 无 | ★★★★☆ 平台化扩展点推进，稳定性短板 |
| **CoPaw** | 49更新 (6关闭) | 49更新 (22合并) | 无 | ★★★★☆ Bug修复与功能扩展并行，社区贡献活跃 |
| **LobsterAI** | 7更新 | 21更新 (17合并) | 无 | ★★★☆☆ UX改进积极，4个月+遗留Bug待解 |
| **NanoBot** | 2新开/1关闭 | 15更新 (5合并) | 无 | ★★★★☆ Telegram修复闭环，WebUI升级在即 |
| **Moltis** | 2关闭 | 9更新 (6合并) | 无 | ★★★★☆ 历史PR消化，配置语义修复 |
| **PicoClaw** | 4更新 (3开放) | 4更新 (3合并) | 无 | ★★★★☆ 响应迅速，"发现即修复" |
| **IronClaw** | 新建多个Bug | 大量合并 | 无 | ★★★★☆ 性能优化攻坚，功能扩展积极 |
| **NullClaw** | 0 | 1 (待合并) | 无 | ★★★☆☆ 稳定维护期，依赖更新延迟 |
| **TinyClaw** | — | — | — | 无活动 |
| **ZeptoClaw** | — | — | — | 无活动 |

---

## 3. OpenClaw 在生态中的定位

### 核心优势

- **社区规模断崖式领先**: 24小时内500条Issue+500条PR更新，远超其他项目（第二梯队约50条），是生态中唯一达到此量级的项目。
- **版本迭代节奏稳定**: 最新版本2026.6.1维持定期发布节奏，拥有完善的安全治理机制（"警告+人工确认"安装审查模式已进入里程碑阶段）。
- **多平台覆盖最广**: 支持macOS、Web UI、CLI，并持续推进跨平台CI基础设施。

### 与其他项目的关键差异

| 维度 | OpenClaw | 同类对比 |
|------|----------|----------|
| **架构路线** | 单体核心 + 插件生态 | NanoClaw正向"扩展点(Seam)"平台化转型；Hermes走桌面端优先路线 |
| **功能侧重** | 全功能型（聊天/编码/渠道/安全） | PicoClaw聚焦轻量多渠道；IronClaw侧重性能与协议扩展 |
| **社区治理** | RFC机制成熟，但决策偏慢 | ZeroClaw同样面临RFC流程"过慢"争议 |
| **稳定性短板** | P1问题平均存活4个月+（如#62505编码代理回归133天未修复） | 各项目普遍存在类似问题，但OpenClaw的影响面更大 |

### 相对不足

- **Issue积压与处理速度不匹配**: 489条新开Issue vs 仅11条关闭，处理率仅2.2%，低于NanoBot（5/15合并率33%）和CoPaw（22/49合并率45%）。
- **核心编码场景稳定性受质疑**: "Coding Agent永不完成任务"（#62505）持续133天未修复，直接冲击其作为"自主编码助手"的核心定位。

---

## 4. 共同关注的技术方向

### 方向一: 安全与权限治理

| 项目 | 具体表现 |
|------|----------|
| **OpenClaw** | 安装策略警告审查（#116489/#120900已合并），安全边界完备 |
| **ZeroClaw** | Email附件读取漏洞修复（#9993）、WhatsApp令牌泄漏修复（#9612）、Gemini密钥URL泄漏修复（#9973待合并） |
| **NanoBot** | 混合消费防火墙提议（#5409），防Agent死循环烧钱 |
| **LobsterAI** | 日志脱敏修复（#1661已合并） |
| **CoPaw** | 媒体附件URL本地化（#7087），防会话污染 |

**结论**: 安全已从"可选项"变为"必修课"，且关注点从外部攻击转向内部数据泄漏与资源滥用。

---

### 方向二: OpenAI协议兼容与生态互操作

| 项目 | 具体表现 |
|------|----------|
| **ZeroClaw** | RFC #8603（23评论）——用户强烈要求支持Chat Completions协议以接入Open WebUI、LobeChat等工具 |
| **IronClaw** | 新增ACP协议支持（#7513待审） |
| **Moltis** | 新增MiniMax Code ACP代理（#1204已合并） |
| **LobsterAI** | OrcaRouter提供商接入（#2504待合并） |
| **CoPaw** | 多模型提供商内置（#6515待审） |

**结论**: 智能体不再是"孤岛"，用户要求将其嵌入现有的LLM工具链生态。

---

### 方向三: 本地Web界面/可视化层

| 项目 | 具体表现 |
|------|----------|
| **NanoClaw** | 两个独立开发者同日提交本地Web聊天渠道PR（#3290、#3298） |
| **NanoBot** | WebUI侧栏会话、@提及跨会话、后续建议三PR集中待审 |
| **OpenClaw** | Control UI持续优化（#123356/#123535/#125242等4个PR） |
| **Moltis** | Files库 + Settings浏览器（#1206待审） |
| **Hermes Agent** | 桌面端Bot Chat体验集中修复（4个PR） |

**结论**: "非技术用户如何与Agent交互"成为共性痛点，各项目均在Web/桌面可视化层加大投入。

---

### 方向四: 跨平台支持（Windows/macOS）

| 项目 | 具体表现 |
|------|----------|
| **ZeroClaw** | Windows 74个测试失败（#7462），新增跨平台CI矩阵（#9398已合并） |
| **Hermes Agent** | Windows更新机制失效（#86093）、Debian安装失败（#87093） |
| **NanoBot** | 连续4个PR修复Windows兼容（#5412/#5415/#5416/#5341） |
| **LobsterAI** | Windows右键菜单支持（#1642已合并） |
| **PicoClaw** | 配置解析修复覆盖Fly部署（#271已合并） |

**结论**: 非Linux平台用户不再是"二等公民"，但修复成本高、战线长。

---

### 方向五: 长时间运行稳定性与资源配置

| 项目 | 具体表现 |
|------|----------|
| **OpenClaw** | Codex hook CPU绑定（#91009）、WhatsApp图片阻塞（#96834）、僵尸进程泄漏（#97616） |
| **NanoBot** | Telegram轮询静默失联修复闭环（#5156/#5301已合并） |
| **ZeroClaw** | ETXTBSY竞态（#9965）、日志模型名误导（#10023） |
| **NanoClaw** | 历史任务日志丢失回归（#3301）、pending消息内存风险（#3289） |
| **LobsterAI** | Ollama本地模型失效4个月（#1635） |

**结论**: 24x7运行的Agent面临"资源泄漏、静默失败、会话状态损坏"三大类顽疾，是用户信任的最大威胁。

---

## 5. 差异化定位分析

| 项目 | 功能侧重 | 目标用户 | 技术架构关键差异 |
|------|----------|----------|-----------------|
| **OpenClaw** | 全功能型旗舰（编码+聊天+多渠道+安全治理） | 开发者/高级用户/企业 | 单体核心+插件生态，Web UI+CLI双前端 |
| **Hermes Agent** | 桌面端优先，本地化技能与MCP | 桌面用户/个人效率 | Desktop App原生体验，Project-local技能沙箱 |
| **ZeroClaw** | 多渠道大规模部署（WhatsApp/Telegram/QQ等） | 社区运营/企业客服 | 安全加固优先，RFC驱动治理 |
| **NanoClaw** | 平台化扩展点（Seam）体系 | 渠道开发者/集成商 | 插件化架构，Chat SDK bridge抽象 |
| **NanoBot** | 轻量级Telegram/WebUI个人助手 | 个人用户/极简主义者 | Python实现，低成本部署 |
| **CoPaw** | 多渠道+Web控制台，飞书/钉钉/微信全覆盖 | 国内用户/企业IM场景 | Qwen/MiniMax等国产模型深度绑定 |
| **LobsterAI** | 桌面应用形态，Cowork协作功能 | Windows用户/知识工作者 | Electron桌面壳+OpenClaw runtime |
| **PicoClaw** | 极致轻量多渠道（IRC/Slack/微信） | 极简部署场景/嵌入开发 | 单二进制，无外部依赖 |
| **IronClaw** | 性能优化与企业级持久化 | 企业/大规模部署 | CoalescingEventSink、WASM工具链 |
| **Moltis** | 外部代理编排（ACP） | 多代理协作场景 | 代理生态扩展+Files库管理 |
| **NullClaw** | 未知（低活跃） | — | 处于稳定维护期 |

---

## 6. 社区热度与成熟度分层

### 第一梯队: 快速迭代期（日PR合并 > 15条）

| 项目 | 阶段特征 |
|------|----------|
| **OpenClaw** | 社区驱动为主，Issue量远超处理能力，功能迭代快但稳定性欠债 |
| **ZeroClaw** | 安全加固+CI基建投入期，v0.9.0目标明确，RFC治理成熟 |
| **CoPaw** | 功能扩展与Bug修复并进，社区贡献活跃（first-time contributors） |
| **NanoClaw** | 核心团队主导平台化重构，扩展点体系成型 |

### 第二梯队: 质量巩固期（日PR合并 5-15条）

| 项目 | 阶段特征 |
|------|----------|
| **Hermes Agent** | 桌面体验集中修复，Patch版本整合125个PR，处于稳定化窗口 |
| **NanoBot** | Telegram问题闭环，WebUI升级在即，处于"修复→增强"过渡 |
| **LobsterAI** | UX改进批量合并，但4个月+遗留Bug侵蚀信任 |
| **IronClaw** | 性能优化攻坚+新功能扩展并行，仍处高速期但方向更专注 |
| **Moltis** | 历史PR消化期，维护者开始清理积压 |

### 第三梯队: 维护/低活跃期

| 项目 | 阶段特征 |
|------|----------|
| **PicoClaw** | 小步快跑，响应迅速但规模有限 |
| **NullClaw** | 依赖自动更新仅有一项活动，处于事实休眠 |
| **TinyClaw / ZeptoClaw** | 无活动，不建议开发者投入 |

---

## 7. 值得关注的趋势信号

### 趋势一: "安全即功能"成为标配

从OpenClaw的安装审查到ZeroClaw的密钥泄漏修复、NanoBot的消费防火墙提议，安全能力正从"后端加固"转向"前端用户体验"。开发者应将安全机制设计为**用户可见、可配置、可审计**的一等公民，而非事后补丁。

### 趋势二: OpenAI协议兼容是通往主流用户的必经之路

ZeroClaw的Chat Completions RFC获得23条评论，是近期最高讨论量之一。用户拒绝为每个Agent学习新的连接方式——**"如果不能用Open WebUI/LobeChat连上，我就不用"**。新项目应从第一天就实现OpenAI兼容端点。

### 趋势三: 本地优先的交互层成为差异化竞争点

NanoClaw两个独立开发者同日提交本地Web聊天渠道，NanoBot三个WebUI增强PR并进。**Agent的"外壳"（聊天界面、文件管理、设置面板）正成为用户体验的关键战场**，而非仅靠底层模型能力。

### 趋势四: 更新机制是信任的隐形杀手

Hermes Agent的Windows更新失效、OpenClaw的"更新即破坏"恐惧、LobsterAI的配置被覆盖——**用户对"更新后一切照旧"的信心正在崩塌**。提供原子化更新、回滚机制、配置迁移工具将是赢得长期信任的关键。

### 趋势五: 长时间运行的可靠性是最大技术债

跨项目的P0/P1 Bug平均存活时间超过100天（OpenClaw #70903达116天、LobsterAI #1635超120天），问题集中在**资源泄漏（僵尸进程、WAL连接）** 和 **会话状态损坏（参数丢失、消息阻塞）**。新进入者如果能从架构层面解决"24x7不重启"的可靠性问题，将获得显著的差异化优势。

### 趋势六: 多Agent协作从愿景走向落地

NanoClaw跨会话上下文（#3285已合并）、LobsterAI Agent间感知（#1644）、CoPaw单窗口协作（#6925）、Moltis外部代理编排——**A2A通信从"概念验证"进入"用户日常需求"**。标准化（如ACP协议）与去中心化（如VOKO项目推广）两种路线正在竞争。

---

*本报告基于各项目2026-08-18 GitHub公开数据自动生成，数据源链接详见各项目日报。*

---

## 同赛道项目详细报告

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot 项目动态日报 — 2026-08-18

> 数据时间窗口：2026-08-17 ~ 2026-08-18 | 数据源：HKUDS/nanobot GitHub Repository


## 1. 今日速览

过去 24 小时 NanoBot 项目保持**高活跃度**，主要集中在 **Telegram 轮询稳定性修复**、**gateway 进程生命周期管理**与 **WebUI 交互增强**三大方向。15 条 PR 中 5 条已完成合并/关闭（合并率 33%），10 条待审 PR 全部为近三天内新开，审查队列新鲜度高、无严重积压。值得关注的是，与 Telegram 轮询静默失联问题（#5171）相关的两个 PR（#5156、#5301）**同日关闭**，标志着该问题已完成修复闭环；同时，社区连续提交了 WebUI 侧栏会话、后续建议、@提及跨会话通信等多个新功能 PR，显示项目正在从"修 Bug"向"打磨交互体验"阶段过渡。整体项目健康度良好。

- 活跃度：🔥🔥🔥🔥🔥（高）
- 合并率：33%（5/15）
- 新开 Issue：2 条，关闭 1 条
- 无新版本发布


## 3. 项目进展

### 今日已完成合并/关闭的关键 PR（5 条）

| PR # | 标题 | 状态 | 关键内容 |
|------|------|------|----------|
| [**#5156**](https://github.com/HKUDS/nanobot/pull/5156) | fix(telegram): recover from silently stalled polling | ✅ 已合并 | 修复 Telegram 轮询在网络瞬时故障后静默失联、永不恢复的问题（对应 Issue #5171），是电信级稳定性修复的核心 PR |
| [**#5416**](https://github.com/HKUDS/nanobot/pull/5416) | fix(gateway): stabilize process identities | ✅ 已合并 | 将 macOS 下依赖 locale 的 `ps lstart` 替换为原生 `proc_pidinfo` 时间戳，统一跨平台进程身份契约，消除 locale 差异导致的 Gateway 客户端租约误判 |
| [**#5301**](https://github.com/HKUDS/nanobot/pull/5301) | fix(telegram): bridge stdlib logging and detect stalled polling | ✅ 已合并 | 将 stdlib logging 桥接至 loguru，并增加轻量轮询存活检测（仅日志，不做重建），为 #5156 的完整方案提供可观测性基础 |
| [**#5406**](https://github.com/HKUDS/nanobot/pull/5406) | feat(cli): add native TypeScript terminal UI | ✅ 已合并 | 新增原生 TypeScript 终端 TUI（恢复 #4329 的提交历史），为 CLI 交互提供现代化终端界面 |
| [**#5410**](https://github.com/HKUDS/nanobot/pull/5410) | fix(goal): stop repeating clarification replies | ✅ 已合并 | 修复 Sustained Goal 激活时，AgentRunner 将普通文本回复误判为需要持续注入，导致 LLM 重复输出澄清类回复的问题 |

### 进度小结

- **Telegram 稳定性问题（#5171）修复闭环**：从 Issue 报告（7 月 29 日）到 PR 合并（8 月 17 日），历时约 3 周，覆盖日志桥接、存活检测和连接池重建三层修复，链路完整。
- **跨平台 Gateway 稳定性集中修复**：进程身份（#5416）、Windows venv 进程收养（#5415）、后台子进程输出刷新（#5412）三个方向同步推进，表明团队正系统性地修复 Gateway 在 Windows 上的进程生命周期问题。
- **WebUI 新功能井喷**：侧栏临时会话（#5364）、@提及跨会话消息（#5358）、后续建议（#5408）三个 WebUI 增强 PR 同时待审，预示着下一版本将带来显著的交互体验升级。


## 4. 社区热点

### 热度最高 Issue — [#4864](https://github.com/HKUDS/nanobot/issues/4864) ⭐ 7 条评论

**`complete_goal` 工具陷入死循环：网关将 recap 参数解析为裸字符串而非 JSON 对象**

- 创建于 7 月 9 日，持续 1 个多月，累计 7 条评论、1 个 👍
- 核心问题：recent update 中工具参数序列化方式变更，导致 `complete_goal` 的 `recap` 参数以纯字符串（而非 JSON 对象）形式传给工具，工具端解析失败后持续报错重试，形成无限循环
- 社区关注度虽不高（1 👍），但**死循环**问题直指 LLM 成本失控风险（每次循环都在消耗 Token）——这与新 Issue #5409（混合消费防火墙）的诉求形成呼应

### 评论趋势解读

社区对 Bug 修复的讨论呈现出 **"生产环境痛点驱动"** 的特征：Telegram 轮询静默失联（#5171）、进程身份 locale 依赖（#5416）、Windows venv 进程收养（#5415）等均为生产环境实际运行的稳定性问题。对 WebUI 功能增强的讨论则集中在**多会话管理与交互效率**方向。


## 5. Bug 与稳定性

今日报告/处理的 Bug 按严重程度排列如下：

### 🔴 高严重度
| Issue/PR | 问题 | 状态 |
|----------|------|------|
| [#4864](https://github.com/HKUDS/nanobot/issues/4864) | **`complete_goal` 死循环**：Gateway 将 `recap` 参数解析为裸字符串导致工具反复报错，形成无限循环 | ⚠️ 仍 OPEN，无关联修复 PR，已持续 40 天 |
| [#5407](https://github.com/HKUDS/nanobot/pull/5407) | **Cron 系统 Job 禁用失效**：`heartbeat.enabled=false` 后，持久化在 `cron/jobs.json` 中的任务仍持续触发，**持续消耗 Token** | 🔧 已有修复 PR（待合并） |

### 🟡 中严重度
| Issue/PR | 问题 | 状态 |
|----------|------|------|
| [#5413](https://github.com/HKUDS/nanobot/pull/5413) | **Provider 异常可绕过 fallback 策略**：LLM Provider 抛异常时直接逃逸，未触发已有的 fallback 循环 | 🔧 已有修复 PR（待合并） |
| [#5412](https://github.com/HKUDS/nanobot/pull/5412) | **后台子进程输出阻塞**：非 TTY 环境下 Python 块缓冲导致启动日志延迟写入 | 🔧 已有修复 PR（待合并） |

### 🟢 已修复
| PR | 问题 | 状态 |
|----|------|------|
| [#5156](https://github.com/HKUDS/nanobot/pull/5156) | Telegram 轮询静默失联（[#5171](https://github.com/HKUDS/nanobot/issues/5171)） | ✅ 已合并 |
| [#5410](https://github.com/HKUDS/nanobot/pull/5410) | Sustained Goal 重复澄清回复 | ✅ 已合并 |
| [#5416](https://github.com/HKUDS/nanobot/pull/5416) | 进程身份依赖 macOS locale（`ps lstart`） | ✅ 已合并 |

### 关键判断

- **#4864（死循环）**为当前最值得关注的开放问题——同时涉及 Gateway 参数序列化机制和 LLM 成本控制，且两个维度分别与 #5409（消费防火墙）和 #5407（Token 烧毁）有交集，建议维护者优先处理。


## 6. 功能请求与路线图信号

### 新功能/特性请求

| Issue/PR | 功能描述 | 状态 | 可能纳入版本 |
|----------|----------|------|-------------|
| [#5409](https://github.com/HKUDS/nanobot/issues/5409) | **混合消费防火墙（Hybrid Spend Firewall）**：为防 AI Agent 无限循环导致 LLM 预算超支，建议构建消费上限（硬上限 + 软上限双层防护） | NEW Issue，无评论 | 较远，属商业化安全考量，但参考价值高 |
| [#5364](https://github.com/HKUDS/nanobot/pull/5364) | **WebUI 临时侧栏会话**：`/side` 命令开启当前主题旁的临时会话，支持多标签切换、独立 drafts/messages/streaming 状态、侧栏与主会话并行发送 | PR 待合并 | 下一版本 |
| [#5358](https://github.com/HKUDS/nanobot/pull/5358) | **WebUI @提及跨会话消息**：为持久化会话分配稳定的 `@name`（不暴露原始 session key），支持在 composer 中通过 @ 向其他会话发送消息 | PR 待合并 | 下一版本 |
| [#5408](https://github.com/HKUDS/nanobot/pull/5408) | **WebUI 后续建议（Follow-up Suggestions）**：会话成功后生成短时效、会话内 Follow-up 建议，provider-neutral，与 DeerFlow 交互一致；空 composer 直接发送，已有草稿则追加 | PR 待合并 | 下一版本 |
| [#5406](https://github.com/HKUDS/nanobot/pull/5406) | **原生 TypeScript 终端 UI** | ✅ 已合并 | 已在 main |

### 路线图信号解读

- **WebUI 交互层正迎来一次集中升级**：侧栏会话 + @提及消息 + 后续建议三个 PR 同步推进，且均由不同贡献者提交，说明社区对 WebUI 多任务并行的需求非常强烈。
- **Commercialization 安全考量开始浮现**：#5409 消费防火墙虽为新 Issue 且无评论，但其出现表明用户对 Agent 无限循环可能导致的财务损失已有关注——配合 #4864（死循环）和 #5407（Token 烧毁），"成本控制"已成为一个跨多个 Issue 的隐性主题。
- **@提及与临时会话两个 PR 均标注 `conflict`**，意味着与现有代码存在冲突，需要维护者协调合并顺序，建议优先处理。


## 7. 用户反馈摘要

### 真实用户痛点

1. **"修好就停不下来"：LLM 回复死循环的财务焦虑**
   Issue [#4864](https://github.com/HKUDS/nanobot/issues/4864) 的评论中，用户描述 `complete_goal` 死循环期间 Token 持续被消耗，"每次循环都在烧钱"。这种对 Agents 失控成本的担忧也体现在新 Issue #5409 中——用户直接建议给 Anthropic/OpenAI 的消耗做硬性防火墙，并主动提出可以贡献实现。

2. **"日志静默 = 最危险的故障"**
   Telegram 轮询静默失联（[#5171](https://github.com/HKUDS/nanobot/issues/5171)）的用户反馈中，描述了"进程在跑、日志无声、消息堆积"的现象。该 Issue 没有获得大量评论（0 条），但其修复过程（#5156 + #5301 双 PR 组合）说明维护者**认真对待了这类生产环境隐形事故**。

3. **Windows 用户持续处于二等公民地位**
   当日多条修复（#5341 curl 别名、#5415 venv 进程、#5416 locale 身份）都指向 Windows 平台差异问题。虽然没有直接的用户评论，但从 PR 数量规律推断，Windows 用户的稳定性体验与 macOS/Linux 仍存在差距。

### 使用场景与需求

- 社区对 **WebUI 多会话并行** 的需求明确（#5364、#5358 均来自不同贡献者）
- **CLI 体验现代化**（#5406 TypeScript TUI）获得合并，说明维护者重视开发者日常使用工具的体验


## 8. 待处理积压

### ⚠️ 需维护者关注

| 项目 | 积压时长 | 严重度 | 建议 |
|------|----------|--------|------|
| [#4864](https://github.com/HKUDS/nanobot/issues/4864) complete_goal 死循环 | **40 天未响应**（自 7 月 9 日） | 🔴 高（Token 持续消耗 + 涉及 Gateway 参数序列化机制） | **优先处理**——影响用户成本且定位较明确（recap 参数序列化），建议明确是否已在新版本中修复，若未修复请安排排期 |
| [#5341](https://github.com/HKUDS/nanobot/pull/5341) weather skill Windows 兼容 | 自 8 月 11 日待审，标注 `conflict` | 🟡 中 | 已停滞 6 天，存在冲突需处理。同类 Windows 修复 PR（#5415、#5416）已合并，建议同步解决此 PR 的冲突问题 |
| [#5364](https://github.com/HKUDS/nanobot/pull/5364) WebUI 侧栏会话 | 自 8 月 13 日待审，标注 `conflict` | 🟡 中 | 与 #5358、#5408 同属 WebUI 交互升级，建议集中安排 Review 顺序，避免三个冲突 PR 相互阻塞 |

### 📋 批量合并建议

#5411、#5412、#5413、#5414、#5415 五个 PR 同属 Gateway/Provider 稳定性修复方向，集中在 8 月 17 日提交，建议维护者**组织一次性集中 Review** 后批量合并，避免长时间占用待审队列。


> **分析师总结**：NanoBot 项目正处于**稳定性修复收官 + WebUI 交互升级启动**的过渡期。Telegram 轮询问题已闭环，Gateway 跨平台修复集中推进；接下来几日内，若 10 条待审 PR 能顺利合并，项目将在 WebUI 多会话管理、Provider fallback 健壮性和 Windows 支持三个维度同时获得显著提升。需重点关注 #4864 死循环问题的处理进度与 #5409 成本控制议题的方向讨论。

> ⚠️ **数据说明**：日报中引用的 GitHub 链接均指向 HKUDS/nanobot 仓库真实 Issue/PR 页面；部分 Issue/PR 的评论数在数据快照中可能因 API 限制未完整反映，以链接页面实际数据为准。

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

好的，我是你的 AI 智能体与个人 AI 助手领域开源项目分析师。以下是根据 Hermes Agent 仓库 2026-08-18 的 GitHub 数据生成的项目动态日报。

---

# Hermes Agent 项目动态日报 — 2026-08-18

## 1. 今日速览

项目今日活跃度**极高**，处于密集的迭代与问题修复周期。过去24小时内，项目共有50条Issue和50条PR更新，其中PR关闭/合并9条，说明核心团队正在快速响应社区反馈并合并修复。新版本 v0.20.3 已发布，整合了自上版本以来的约125个PR。从今日Issue分布来看，**稳定性与可靠性**是当前最突出的主题，包括Windows平台更新失败、会话状态损坏（FTS索引、WAL连接泄漏）、以及更新后Gateway混合版本运行等关键问题。同时，围绕项目本地化（Project-local）技能与MCP的安全模型、以及桌面端Bot Chat体验的优化形成了显著的开发主线。

## 2. 版本发布

- **[v2026.8.16.2 (v0.20.3)](https://github.com/NousResearch/hermes-agent/releases)**：这是一个 **Patch 版本**，主要目的是将自 v0.20.2 以来合并的约 125 个 PR 汇总为一个稳定的标签版本，供下游消费者（Docker 镜像、托管部署、新安装）使用。
    - **破坏性变更**：根据发布说明，此版本为 Patch 版本，未提及破坏性变更。
    - **迁移注意事项**：未明确说明。但鉴于其整合了大量变更，建议用户关注从 v0.20.2 升级后的配置兼容性，特别是涉及到 `state.db`、技能索引和网关配置的更改。

## 3. 项目进展

今日合并的PR主要集中在修复桌面客户端（Desktop App）的会话体验和稳定性问题。

- **桌面端 Bot Chat 体验修复**：这是一个重点。多个PR协同解决了点击Bots列表时打开错误会话或空白会话的问题。
    - PR [#88690](https://github.com/NousResearch/hermes-agent/pull/88690) 和 [#88148](https://github.com/NousResearch/hermes-agent/pull/88148) 确保点击Bots列表总是打开固定的（pinned）规范Bot Chat，而不是错误地创建新会话。
    - PR [#88292](https://github.com/NousResearch/hermes-agent/pull/88292) 修复了侧边栏预览与实际打开会话不一致的问题。
    - PR [#88699](https://github.com/NousResearch/hermes-agent/pull/88699) 修复了切换Profile时因404错误导致跳转到空白新聊天路由的问题。
- **跨机器Bot私信功能补全**：PR [#88678](https://github.com/NousResearch/hermes-agent/pull/88678) 的合并，完成了跨机器Bot DMs的闭环，即远程@提及可以到达收件人的固定Bot Chat，并能将回复中继回去，这是对之前仅实现“发送”的一半功能的补充。

## 4. 社区热点

- **Issue [#66616](https://github.com/NousResearch/hermes-agent/issues/66616) - Skills index is stale or degraded** (评论: 47)
    - 这是今日讨论最激烈的问题。该问题自7月18日创建以来已持续一个月，自动化探针反复报告技能索引（`skills-index.json`）过期。47条评论表明这是一个长期困扰用户的问题，严重影响了技能发现和加载功能。社区对此的耐心可能正在耗尽，需要我们高度关注。

- **Issue [#23717](https://github.com/NousResearch/hermes-agent/issues/23717) - RFC: Pluggable SessionDB Provider** (评论: 17, 👍: 7)
    - 这是一个存在已久的RFC，提议将SessionDB从SQLite抽象为可插拔的Provider（如PostgreSQL）。社区对此需求强烈，主要动机是解决热更新时SQLite文件锁导致的“死亡螺旋”问题。此问题虽不紧急，但代表了用户对更健壮、可扩展架构的长期诉求。

## 5. Bug 与稳定性

**严重等级：高 (P1)**

- **Windows更新机制彻底失效**：[#86093](https://github.com/NousResearch/hermes-agent/issues/86093) `hermes update` 在Windows上总是失败，因为运行中的 `hermes.exe` 无法被重命名，而当前的隔离机制（quarantine）无效。
- **Debian安装失败**：[#87093](https://github.com/NousResearch/hermes-agent/issues/87093) 在Debian 13.6系统上安装脚本失败，原因是 `uv.lock` 和 `npm install` 步骤出错。
- **更新后Gateway静默失败**：[#88654](https://github.com/NousResearch/hermes-agent/issues/88654) 更新程序在尝试自动重启Gateway时，可能因PID到Profile映射失败而静默跳过，导致不同组件运行在混合代码版本上，进而引发其他错误（如 #88655）。**已有修复PR: [#88703](https://github.com/NousResearch/hermes-agent/pull/88703)**。
- **计划任务静默死亡**：[#88655](https://github.com/NousResearch/hermes-agent/issues/88655) 调度器层面的cron处理错误绕过了 `failure_nudge` 告警系统，导致任务可能静默失败数小时无人知晓。

**严重等级：中 (P2)**

- **WAL连接泄漏**：[#79742](https://github.com/NousResearch/hermes-agent/issues/79742) `SessionDB` 的每线程WAL读连接在持有线程死亡后不会被释放，最终导致文件描述符耗尽（EMFILE）。
- **搜索索引永久丢失**：[#72716](https://github.com/NousResearch/hermes-agent/issues/72716) 在 `optimize-storage` 过程中，如果被中断，可能会将全文搜索（FTS）索引永久清空。**已有修复PR: [#88696](https://github.com/NousResearch/hermes-agent/pull/88696)**。
- **TTS重复播放**：[#87823](https://github.com/NousResearch/hermes-agent/issues/87823) 和 [#86601](https://github.com/NousResearch/hermes-agent/issues/86601) 桌面端的“朗读回复”功能会因临时ID到规范ID的变更以及流式播放结束事件，导致同一条回复被播放两次。
- **代码压缩过早触发**：[#88695](https://github.com/NousResearch/hermes-agent/issues/88695) Codex OAuth模型的上下文窗口已提升到900K，但原生的压缩阈值仍停留在200K，导致会话过早被压缩。

## 6. 功能请求与路线图信号

- **项目本地化安全模型上线**：EPIC [#48970](https://github.com/NousResearch/hermes-agent/issues/48970) 及其子任务（[#48975](https://github.com/NousResearch/hermes-agent/issues/48975), [#48974](https://github.com/NousResearch/hermes-agent/issues/48974)）今日有了重大进展。虽然子任务被关闭，但相关的实现PR [#88704](https://github.com/NousResearch/hermes-agent/pull/88704)（项目信任sidecar）和 [#88700](https://github.com/NousResearch/hermes-agent/pull/88700)（跨worktree的信任身份规范化）已被提出，这表明该功能正进入落地阶段。
- **自主音乐生成**：PR [#88705](https://github.com/NousResearch/hermes-agent/pull/88705) 提议将MiniMax音乐生成插件内置到项目中，这暗示了“媒体工作室”插件即将发布，并且智能体将具备从聊天中直接生成音乐的能力。
- **可插拔会话数据库**：Issue [#23717](https://github.com/NousResearch/hermes-agent/issues/23717) 的强烈反响（👍: 7）表明社区对架构演进有持续的需求，这将是路线图上的一个重要考量点。

## 7. 用户反馈摘要

- **核心痛点集中在更新与稳定性**：许多用户反馈集中在 `hermes update` 在不同平台（Windows、Debian）上失败的问题，以及更新后遗留的Gateway进程导致版本混乱。这表明安装升级路径的用户体验是当前最影响信任的问题之一。
- **桌面端体验细节备受关注**：Bots侧边栏预览错误、点击后打开错误会话、TTS重复播放等小问题被频繁报告，说明桌面端的交互逻辑正在经历社区的大规模使用和检验，用户对细节体验的要求很高。
- **配置安全隐忧**：Issue [#4775](https://github.com/NousResearch/hermes-agent/issues/4775)（Hermes重写原始config.yaml并展开环境变量密钥）虽然已关闭，但仍有用户关注。同时，关于Desktop与Gateway配置双写冲突的问题（[#37751](https://github.com/NousResearch/hermes-agent/issues/37751)）也再次被提及，这涉及敏感信息的安全问题，需要持续关注。

## 8. 待处理积压

- **长期未决的RFC**：[#23717](https://github.com/NousResearch/hermes-agent/issues/23717) 提议可插拔SessionDB Provider。该问题已开放超过3个月，获得7个👍，是社区对项目架构演进的重要声音。建议维护者考虑将其纳入路线图或给出明确回应，以避免社区诉求长期悬置。

---
**项目健康度评估**：
项目处于高速迭代期，合并频率高，对社区反馈响应迅速。然而，今日的Issue和PR分布也揭示了“更新机制脆弱”和“状态管理复杂性”两大核心短板，这些是导致许多衍生问题（如混合版本、数据损坏）的根源。虽然已有PR在修复相关问题，但彻底解决可能需要更根本的架构性调整。

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw 项目日报 — 2026-08-18

## 今日速览

PicoClaw 项目在过去24小时内保持了温和活跃度：4条Issue更新（3开放/1关闭）和4条PR更新（3合并/1待合并）。昨日刚关闭的Issue #3311（工具重复失败导致静默无响应）对应的修复PR #3312已于今日合并，证明社区对稳定性问题响应迅速。值得关注的是两个新上报的Bug（Slack图片上传失败 #3338、Antigravity 429错误 #3339），其中前者已由同一作者提交修复PR #3340，体现了高效的"发现即修复"节奏。整体项目健康度良好，工具链与渠道接入类问题成为当前开发焦点。

---

## 版本发布

无新版本发布。

---

## 项目进展

今日共合并3个PR，均已关闭：

**稳定性修复（核心进展）**
- **[PR #3312: fix(agent): stop turn early on repeated identical tool failure](https://github.com/sipeed/picoclaw/pull/3312)** — 由lucapette提交。修复当工具（如`git`命令无凭证）每次调用返回相同错误时，Agent循环直到`max_tool_iterations`仍不回复用户的严重问题。合并后，Agent将在识别到重复相同故障时提前终止当前轮次，避免长时间静默。

**配置管理修复**
- **[PR #271: fix: env overrides when config.json is missing](https://github.com/sipeed/picoclaw/pull/271)** — 由tbeaudouin05提交。修复Fly部署（仅用secrets/env）等场景下config.json缺失时环境变量覆盖未生效、导致错误使用默认模型（glm-4.7）的问题。现在无论config.json是否存在都会执行`env.Parse(cfg)`。

**渠道能力增强**
- **[PR #2606: feat: enhance Weixin channel support and configuration](https://github.com/sipeed/picoclaw/pull/2606)** — 由dsus4wang提交。增强微信公众号渠道的多实例支持：增加渠道目录与动态实例管理，加强非法渠道名校验与多实例流程稳定性。属于功能性增强，覆盖backend/frontend/docs三端。

**待合并PR**
- **[PR #3340: fix(slack): set FileSize on media upload params](https://github.com/sipeed/picoclaw/pull/3340)** — 修复Slack图片上传始终失败的Bug，待维护者review合并。

**总体判断**：项目在"错误容错"和"渠道适配"两条线上均有实质推进，修复质量较高。

---

## 社区热点

**讨论热度最高：Issue #3287 (6条评论)**

**[[Feature] Better support long messages in IRC](https://github.com/sipeed/picoclaw/issues/3287)** — 由superuser-does于7月22日提出，至今仍开放且有持续讨论。该需求源于IRCv3的512字节消息长度限制：超过限制的消息会被IRC客户端自动拆分，而PicoClaw目前将拆分后的每个片段视为独立消息，导致长消息语义被割裂。这是IRC渠道的可用性痛点，涉及消息协议层理解与重组策略，属于功能性改进。

**其他活跃讨论**
- **[#3311: Repeated identical tool failure loops silently to max_tool_iterations](https://github.com/sipeed/picoclaw/issues/3311)** — 虽已关闭（修复PR #3312已合并），但该Issue在Telegram生产环境中被发现，反映了对"用户得不到回复"这一静默失败的高度关注。

---

## Bug 与稳定性

按严重程度排列：

**高 - 静默无限循环**
- **[#3311: Repeated identical tool failure loops silently to max_tool_iterations](https://github.com/sipeed/picoclaw/issues/3311)** — 已关闭，修复已合并。Agent在工具连续返回相同错误时不中断循环，用户长时间收不到回复，且无任何提示。在Telegram生产环境中发现。✅ 已由PR #3312修复。

**中 - Slack媒体上传完全不可用**
- **[#3338: Slack does not attach image media content](https://github.com/sipeed/picoclaw/issues/3338)** — 今日新增，由octavioturra报告并同时提交修复PR #3340。`SendMedia`构建`slack.UploadFileParameters`时未设置`FileSize`，导致slack-go SDK在发起任何网络请求前即以`file size cannot be 0`拒绝。✅ 修复PR #3340待合并。

**中 - Antigravity API配额误报**
- **[#3339: Antigravity generation returns generic 429 despite valid OAuth scopes](https://github.com/sipeed/picoclaw/issues/3339)** — 今日新增。Google Antigravity认证和模型发现均正常，但所有生成请求都返回429配额耗尽错误，且无`quota`相关详细信息。授权合法但被限流，可能需要检查API key配额设置或PicoClaw的请求头构造。

**其他**
- **[PR #271: env overrides when config.json is missing](https://github.com/sipeed/picoclaw/pull/271)** — 已合并。解决无config.json时环境变量不生效、应用错误使用默认模型的配置回归问题。

---

## 功能请求与路线图信号

**IRC长消息支持（值得关注）**
- **[#3287: Better support long messages in IRC](https://github.com/sipeed/picoclaw/issues/3287)** — 虽然该Issue已标记为stale，但其核心诉求（IRCv3长消息需被识别为单一连续消息）是多渠道一致性的合理改进。PicoClaw当前将每次拆分片段当作独立消息处理，可能影响IRC用户的对话体验。

**生态信号**
- 微信渠道增强（PR #2606）与Slack修复（PR #3340）显示团队正积极丰富与完善多平台对接，这是PicoClaw作为"多渠道个人助手"的关键竞争力。

---

## 用户反馈摘要

- **工具失败体验**：用户在Telegram上请求Agent执行`git`命令时，因缺少凭证导致工具持续失败，Agent静默循环了数分钟直到达到`max_tool_iterations`，用户始终未收到回复（即使是一条错误提示）。这反映了当前实现中"错误反馈回路缺失"的痛点，修复后Agent将更早终止并在对话中主动反馈。
- **部署配置困扰**：使用配置文件缺失的部署模式（如Fly.io仅用secrets）时，环境变量未正确覆盖默认配置，导致Agent使用了错误的默认模型并因凭证缺失而无法正常工作。这提示"环境变量优先"的配置逻辑需要更一致地应用。
- **媒体消息需求**：用户期望通过Slack向Agent发送图片内容，但当前`SendMedia`只发送引用，实际文件未附加，Slack端报"file size cannot be 0"，导致"图片消息"功能完全不可用。

---

## 待处理积压

**长期未解决（stale）但仍有价值：**
- **[Issue #3287: Better support long messages in IRC](https://github.com/sipeed/picoclaw/issues/3287)** — 创建于7月22日，已被标记为stale但讨论仍在继续。如有IRC渠道的用户，可考虑是否纳入长消息重组支持。

**值得关注的PR：**
- **[PR #3340: fix(slack): set FileSize on media upload params](https://github.com/sipeed/picoclaw/pull/3340)** — 修复Slack图片上传Bug的PR已提交，建议尽快review合并，以解阻塞。

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw 项目动态日报 — 2026-08-18

## 今日速览

项目在过去24小时内保持高度活跃，共产生 4 条 Issue 更新和 34 条 PR 更新。值得关注的是，核心团队（gavrielc）今日连续提交并关闭了 6 个 PR，围绕渠道扩展桥接、路由钩子和工具注册扩展点展开系统性重构，表明项目正在平台化（extension/seam）方向上发力。同时，社区提交的 PR 质量和数量均较高——glifocat 提交了针对 #3301（聊天会话中任务触发导致日志丢失）的修复 PR #3303，以及 #3291 的轮询绑定修复；此外还有 3 个独立的新渠道实现（webchat 和 local web chat），反映出社区渠道诉求强烈。今日有 1 个 Issue 被关闭（文档问题 #1143），但仍有数个严重 Bug 悬而未决（详见下文）。整体判断：项目处于活跃爬坡期，平台生态雏形显现，但稳定性问题（任务模式、轮询、信道消息 ID）仍是主要短板。

---

## 版本发布

无新版本发布。

---

## 项目进展

今日共 21 个 PR 被合并或关闭（其中大部分来自 core-team 的 gavrielc）。核心进展集中在以下四个方向：

1. **模块化扩展点（Seam）体系建设**（gavrielc 系列，全部合并）：
   - **PR #3292** — 渠道入站策略注册点：允许模块在 Chat SDK bridge 上包装 `ChannelSetup`，在单一拦截点截获所有入站分发路径，替代此前需要编辑 bridge 源码的做法。
   - **PR #3293** — 路由会话创建钩子：新会话建立时通知已注册模块，支持平台专属会话引导（线程命名等）。
   - **PR #3294** — 投递后钩子（含首次投递标志）：为渠道模块提供会话首条外发消息的一站式跟进能力（如 onboarding 引导）。
   - **PR #3295** — Chat SDK bridge 通用成员事件钩子：将 chat 4.29.0 的 `onMemberJoinedChannel` 转发到按渠道类型注册的处理器。
   - **PR #3296** — `extendTool`：容器内 MCP 工具注册表的新增扩展点，可增量扩展基础工具的参数 schema、描述和 payload 透传键。
   - **PR #3297** — 设置向导的渠道前置处理与配套技能声明（合并）。
   - **PR #3285** — 跨会话上下文（多会话 Agent 组）：整合了 #3254–#3257 四个前期 PR，实现触发消息的"会话回声"传播、DM 回填、回显修剪和 `ncl sessions history` 命令。

   这些合并 PR 标志着 NanoClaw 正在从单体桥接逻辑走向插件化架构，价值在于：渠道适配工作可以独立包封装，无需侵入核心代码。

2. **Bug 修复合入**：
   - **PR #3303**（OPEN，glifocat）— 针对 #3301 的修复：保留聊天会话中任务行的运行日志。尚未合并。
   - **PR #3287**（OPEN，wakqasahmed）— 修正入站平台消息 ID 不剥离 agent-group 后缀的问题（对应 Issue #3153）。尚未合并。
   - **PR #3286**（OPEN，wakqasahmed）— `ncl groups restart --rebuild` 在未配置 packages 时跳过镜像重建（对应 Issue #2701）。尚未合并。
   - 今日并无修复类 PR 被合并，核心团队今日合入的均为扩展点/功能类。

3. **新渠道贡献**：
   - **PR #3290**（OPEN，viiluxx）— **webchat 渠道**：由 daemon 自身托管的本地浏览器聊天，零依赖（仅 Node `http` 内建模块），单页实现。
   - **PR #3298**（OPEN，amit-shafnir）— **Local Web Chat 渠道**：回环专用本地 Web 渠道适配器，带小型浏览器聊天 UI。
   - 两个独立开发者同日在 PR 层面提交了相同方向的渠道，说明"本地浏览器聊天"是社区真实痛点。

4. **CLI 改进**：
   - **PR #3218**（OPEN，zvi-fried）— `ncl` 客户端新增 `--stdin-json` 有界 JSON 输入模式，覆盖 host 和 container 两端。
   - **PR #3302**（OPEN，wakqasahmed）— 修正 OneCLI 网关默认绑定地址（对应 Issue #2903）。

**评估**：今日合入的核心贡献集中在"扩展点"和"渠道钩子"层面，项目从"可配置"走向"可扩展"的平台化阶段推进明显。但注意：#3303 等严重 Bug 修复尚未合并，用户侧稳定性问题仍在。

---

## 社区热点

今日社区讨论热度集中在以下几个 PR/Issue：

1. **#3290 和 #3298 — 两个独立本地 Web 聊天渠道 PR**（同日均出现，且互不知晓）
   - [PR #3290 — Add webchat channel](https://github.com/nanocoai/nanoclaw/pull/3290)（viiluxx）
   - [PR #3298 — feat(channels): add local web chat](https://github.com/nanocoai/nanoclaw/pull/3298)（amit-shafnir）
   - **诉求分析**：两者由不同开发者独立提交，明确表明"除一次性 CLI 外，所有会话界面都需经外部渠道路由"是当前明显的功能空白。社区对"由 daemon 自身提供的本地 Web 界面"需求强烈，背后可能是对现有渠道（Chat SDK 等）配置复杂的间接反馈。

2. **#3301 / #3303 — 聊天会话中任务触发导致日志丢失 / 修复 PR**
   - [Issue #3301](https://github.com/nanocoai/nanoclaw/issues/3301)（glifocat）
   - [PR #3303](https://github.com/nanocoai/nanoclaw/pull/3303)（glifocat）
   - **诉求分析**：报告者自称"每次聊天中任务触发都丢失日志"，且该问题源于 #2988 中引入的单通道任务分发变更（2.1.48）。这属于日常使用高频场景的回归问题，影响面较大，且从描述看问题还牵涉"对话系列未列出"等衍生现象。修复 PR 已提交但尚未合并，社区关注度有待提升。

3. **#3288 — /add-clawmetry 技能 PR**（vivekchand）
   - 提供只读本地仪表盘（ClawMetry）的安装技能，定位为"调试 FAQ 只建议用 Claude Code"的替代方案。反映出用户在"阅读会话、夜间扫描、操作记录"等运维场景中缺乏可视化工具。

4. **#3203 — codex 提供商事件类型错误导致容器 typecheck 失败**
   - [Issue #3203](https://github.com/nanocoai/nanoclaw/issues/3203) 创建于 2026-08-08，已有 1 条评论（但未展示内容），目前无对应修复 PR。此问题涉及 provider 开发流程，对上游用户影响有限，但若涉及 image 生成功能则影响实质使用。

---

## Bug 与稳定性

按严重程度从高到低排列：

| 严重度 | Issue/PR | 描述 | 状态 |
|---|---|---|---|
| **高** | [#3301](https://github.com/nanocoai/nanoclaw/issues/3301) | 聊天会话中触发的任务整条会话切换至任务模式（row 影响范围扩大），日志丢失、回复被吞、系列未列出。报告者称"所有历史任务行"都受影响。 | 已有修复 PR [#3303](https://github.com/nanocoai/nanoclaw/pull/3303)（open，尚未合并） |
| **中高** | [#3289](https://github.com/nanocoai/nanoclaw/issues/3289) | `getPendingMessages()` 将全部既有 pending 行加载入内存后才应用 `max_results`，积压量大时存在内存风险。 | 已有修复 PR [#3291](https://github.com/nanocoai/nanoclaw/pull/3291)（open） |
| **中** | [#3203](https://github.com/nanocoai/nanoclaw/issues/3203) | codex provider 发出未声明的 `file` ProviderEvent，导致 `/add-codex` 在当前 main 上 typecheck 失败、生成的图片被静默丢弃。 | open，无 fix PR |
| **中** | [#3287](https://github.com/nanocoai/nanoclaw/pull/3287) | `getMessageIdBySeq()` 返回的入站消息 ID 未剥离 agent-group 后缀，导致 ID 与平台实际 ID 不一致，影响去重/关联逻辑。 | fix PR open（对应 [#3153](https://github.com/nanocoai/nanoclaw/issues/3153)），尚未合并 |
| **低** | [#1143](https://github.com/nanocoai/nanoclaw/issues/1143) | Skills 文档中引用了已删除的 `/data/env` 路径（文档问题），今日已关闭。 | CLOSED |
| **低** | [#3300](https://github.com/nanocoai/nanoclaw/pull/3300) | `formatAttachments` 未对 attachment 的 `type` 字段做 XML 转义，可能导致 XML 注入/格式错误。 | fix PR open |

**提醒**：#3301 和 #3289 的修复 PR（#3303、#3291）目前均为 open，项目维护者应优先安排合并窗口——二者分别影响日常任务使用和长期运行实例的内存稳定性。

---

## 功能请求与路线图信号

今日 PR 中提出的新功能可归入以下方向，结合现有 PR 判断下一版本可能纳入的内容：

| 功能方向 | 相关 PR | 纳入可能性判断 |
|---|---|---|
| **本地 Web 聊天界面**（两个独立实现） | [#3290](https://github.com/nanocoai/nanoclaw/pull/3290)，[#3298](https://github.com/nanocoai/nanoclaw/pull/3298) | 两者实现思路接近（loopback-only + 零依赖单页），若维护者选择合入，大概率会合并为统一渠道模块。高概率纳入下一版本（社区强烈需求）。 |
| **可观测性/运维仪表盘**（ClawMetry） | [#3288](https://github.com/nanocoai/nanoclaw/pull/3288) | 独立运维技能，低侵入性，可能以 skill 形式纳入而非核心代码。 |
| **CLI 有界 JSON 输入**（`--stdin-json`） | [#3218](https://github.com/nanocoai/nanoclaw/pull/3218) | 纯增量，不改变现有协议，属于合规性/自动化友好方向，有纳入可能。 |
| **跨会话上下文机制** | [#3285](https://github.com/nanocoai/nanoclaw/pull/3285) | 已合并。未来版本将支持多会话 Agent 组的信息互喂机制，无需再通过外部编排实现。 |
| **扩展点/钩子体系**（会话创建、投递后、成员事件、extendTool） | 今日 gavrielc 系列（#3292–#3296） | 核心团队已系统性合入，这意味着下一版本（2.2.x 或更高）对渠道侧的生态接入能力大幅增强。 |

此外，今日 Issue 层面无新功能请求，以 Bug 报告为主。

---

## 用户反馈摘要

1. **glifocat（#3301）对任务模式变更的影响面反馈**：
   >“Since #2988 (one-door task delivery, 2.1.48)... on my install that is every legacy task row."（意思是：自 #2988 引入单通道任务分发后，其安装上的每一个历史任务行都会受影响。）
   
   反映问题不仅限于新建任务，而是波及存量数据，涉及面广。修复优先级应拉高。

2. **glifocat（#3289）对轮询内存行为的担忧**：
   >“loads every due pending row into JavaScript before applying `max_results`."（把每条到期 pending 行先全部载入 JS 内存，然后才应用 `max_results` 限制。）
   
   对长期运行实例的内存表现有实际顾虑。

3. **#3203 报告者对 codex 集成断裂的失望**（间接）：
   从描述看，"生成的图片被静默丢弃"是最具破坏性的部分——用户执行 `/add-codex` 后可能无任何报错，但产出缺失，对 agent 发布流程影响明显。

4. **CLI/工具链层面的正面反馈**：
   - zvi-fried（#3218）的设计描述显示其对现有协议保持谨慎——"不改变现有请求框架、daemon 分发器、命令注册表、授权或输出行为"，这类有约束意识的 PR 质量在社区中较为难得。
   - wakqasahmed 两个 PR 均指向具体操作性痛点（网关部署 + restart 流程），表明其实际部署使用中遇到配置类和流程类问题。

---

## 待处理积压（需维护者关注）

| 类别 | 项目 | 持续天数 | 状态 | 备注 |
|---|---|---|---|---|
| **等待 Review 的修复 PR** | [#3303](https://github.com/nanocoai/nanoclaw/pull/3303)（任务日志丢失修复） | 1 天 | 待合并 | 高危，需尽快 review/merge |
| **等待 Review 的修复 PR** | [#3291](https://github.com/nanocoai/nanoclaw/pull/3291)（pending 消息轮询绑定） | 1 天 | 待合并 | 影响内存稳定性 |
| **等待 Review 的修复 PR** | [#3287](https://github.com/nanocoai/nanoclaw/pull/3287)（消息 ID 未剥离前缀） | 1 天 | 待合并 | 对应 Issue #3153，建议确认 | 
| **多日未处理 Bug** | [#3203](https://github.com/nanocoai/nanoclaw/issues/3203)（codex 事件类型错误，typecheck 失败） | 10 天 | open，无 fix PR | 建议维护者确认是否已有内部修复方案 |
| **长期待审的功能 PR** | [#3218](https://github.com/nanocoai/nanoclaw/pull/3218)（`--stdin-json` CLI 输入） | 9 天 | open | 功能完整，建议安排 reviewer |

---

*本日报基于 2026-08-18 00:00 UTC 的 GitHub 数据生成。*

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

# NullClaw 项目动态日报 — 2026-08-18

## 今日速览

过去24小时内，NullClaw 项目活跃度处于**较低水平**：无新开/关闭 Issues，仅新增1条来自 Dependabot 的依赖更新 PR（#956），暂未合并。项目当前处于**稳定维护期**，无新版本发布，无功能开发迹象。值得关注的是，唯一活跃的 PR 是自动依赖更新，说明仓库中尚有1条待合并的维护性改动。整体来看，项目正在经历一段**低调期**，长期健康度取决于待办积压的处理节奏。

---

## 版本发布

无新版本发布。

---

## 项目进展

**今日合并/关闭 PR：0 条**

**待合并 PR（1条）：**
- [#956 [dependencies, docker] ci(deps): bump alpine from 3.23 to 3.24 in the docker-images group](https://github.com/nullclaw/nullclaw/pull/956) — 由 Dependabot 创建（2026-06-15），将 Docker 基础镜像 Alpine 从 3.23 升级至 3.24。该 PR 已存在超过两个月，目前处于待合并状态，属于安全/维护性更新。合并后可提升容器运行环境的安全性与稳定性。

**评估**：今日无功能/修复代码落地，项目推进速度缓慢。唯一进展是依赖维护自动化仍在运作，但合并延迟可能削弱其时效性。

---

## 社区热点

**活跃度最高的 PR：**
- [#956 [dependencies, docker] ci(deps): bump alpine from 3.23 to 3.24](https://github.com/nullclaw/nullclaw/pull/956)

该 PR 自6月15日创建以来已持续2个月未获合并，期间无评论、无表情回应。虽然 Dependabot 持续推送更新，但维护者响应不足，这反映了**依赖维护流程存在延迟**。社区诉求核心：安全基线的及时更新需要维护者更高效的审核节奏。

---

## Bug 与稳定性

过去24小时内无新增 Bug 报告，无崩溃或回归问题。当前无紧急稳定性风险。

---

## 功能请求与路线图信号

无新功能请求提交。结合当前待合并 PR（基础镜像升级）来看，项目近期路线图可能聚焦于**基础设施维护**而非新特性开发。alpine 3.24 升级为合并后，将为后续容器化部署场景提供更稳定的运行基础。

---

## 用户反馈摘要

过去24小时内无用户评论产生。需持续观察后续互动才能获取有效的用户反馈。

---

## 待处理积压

以下为长期未获响应的更新请求，建议维护者优先关注：

1. **[#956 alpine 3.23 → 3.24 基础镜像升级](https://github.com/nullclaw/nullclaw/pull/956)** — 已存在 **64天**，属于安全及维护性更新，长时间未合并可能意味着容器运行环境停留在旧版本。建议尽快完成审查/合并或关闭，并明确后续依赖升级处理策略。

---

**项目健康度总结**：NullClaw 当前处于低活跃/稳定状态，依赖维护自动化运行正常但响应延迟。无 Bug 积压、无新功能需求，长期健康度中等——需警惕维护响应速度对自动化流程效率的拖累。建议维护者优先处理 #956，并明确版本发布节奏，以恢复项目活跃度信号。

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

好的，这是 2026-08-18 的 IronClaw 项目动态日报。

---

## IronClaw 项目动态日报 — 2026-08-18

### 1. 今日速览

IronClaw 项目今日活跃度**极高**，尤其是在性能优化和稳定性修复方面。核心团队正围绕“降低持久化数据库写入压力”这一史诗级议题 (#7591) 展开密集攻坚，提出了多项具体的优化方案并已提交相应 PR。同时，项目也在积极扩展功能边界，包括新增 Google Docs 语义编辑、WASM 工具类型化响应、ACP 协议支持等。社区反馈的 Bug（如 MCP 服务器配置、Telegram 连接流程）得到快速响应，并产出了对应的修复 PR。整体来看，项目正处于一个功能迭代与核心架构优化并行的高速发展期。

### 2. 版本发布

- **无新版本发布。**

### 3. 项目进展

今日虽无新版本发布，但核心代码库有大量 PR 被合并或关闭，标志着多项关键工作的重大进展：

- **性能优化（Epic #7591）**：
    - **合并/关闭**：Tier 1 的 #7594 (路由循环里程碑通过 CoalescingEventSink) 和 Tier 2 的 #7598 (折叠能力调用状态写入) 已被关闭，表明这些减负措施已落地或被替代方案吸收。
    - **新提交**：为继续推进该史诗，提交了多个新 PR，包括 #7717 (修复 libSQL 写通道饥饿)、#7712 (使 BeforeModel 检查点批处理可选且副作用安全) 和 #7709 (限制租约围栏读取)。
- **功能开发**：
    - **Slack 私密连接提示**：PR #7682 为未关联账户的 Slack 用户提供私密的、一键式连接引导，修复了 #7681 中公开回复和流程繁琐的问题，且 #7710 已针对该 PR 的多智能体审查意见进行了修复。
    - **Google Docs 语义编辑**：PR #7718 新增了四个语义化 Google Docs 能力（结构化检查、锚定批量编辑、表格填充、确定性验证），在不破坏现有 11 个遗留工具的前提下扩展了功能。
    - **WASM 工具链**：PR #7711 (已取代 #7703) 完成了能力响应规范化栈的最后一环，引入了类型化的工具响应和访客迁移，提升了 WASM 工具生态的健壮性。
- **其他重要合并**：PR #7663 将 1.2 版本的修复（如 Windows 文件系统/发布冒烟可靠性）向前移植到了主分支，并包含了线程索引修复。

### 4. 社区热点

今日讨论最活跃的议题集中在**数据库写入压力优化**上，这既是内部性能优化的重点，也直接关联到用户报告的外部问题。

- **Issue #7714 (Bug): libSQL: 共享写入连接导致资源调控器日志饥饿** (评论: 0, 新建) - 该问题详细描述了在基准测试中，由于 libSQL 单一共享写连接导致资源调控器日志阻塞，进而引发级联故障的严重问题。这直接催生了 PR #7717，体现了社区反馈到核心修复的高效闭环。
- **Issue #7705 (Bug): CoalescingEventSink 的无限关闭刷新和 pending_flush_error 锁存** (评论: 0, 新建) - 由一个已合并的 PR (#7631) 审查引出的两个非阻塞性问题，表明项目对代码质量的把控深入到事后追踪。
- **Issue #7702 (Bug): 义务审计记录未在生成环境附加** (评论: 0, 新建) - 在审计写入压力时发现了一个与预期相反的问题：契约要求的审计记录实际上根本没有写入。这显示了团队在优化时不仅关注性能，也在验证系统契约的完整性。

### 5. Bug 与稳定性

今日报告的 Bug 按严重程度排列如下：

- **严重 (P0/P1)**:
    - **#7714 (Bug, risk: medium):** libSQL 写通道饥饿导致资源调控器级联故障。这是今日最严重的问题，会导致能力调用失败和资源泄漏。**已有对应修复 PR #7717。**
- **中等 (P2)**:
    - **#7716 (Bug, qa-bug):** "添加 MCP 服务器"流程缺少 Bearer 密钥认证和传输选项。**暂无对应 PR。**
    - **#7715 (Bug, qa-bug):** Telegram 连接流程在 Bot 和个人账户之间缺乏明确选择。**暂无对应 PR。**
- **其他**:
    - **#7705 (Bug):** 事件接收器在关闭时可能挂起及错误锁存问题。**暂无对应 PR，但已在持续追踪。**
    - **#7702 (Bug):** 审计记录未按契约写入，属于契约违约问题。**暂无对应 PR，但已记录在案。**
    - **#7707 (Bug):** 通过最新检查点类型推断副作用的逻辑不安全，已在集成测试中证明。**已拆分为独立问题，是实际节省的关键所在。**

### 6. 功能请求与路线图信号

多个用户侧的功能请求和内部规划的功能增强正在并行推进：

- **用户请求**:
    - **#7719**: 请求在 GitHub 工具中支持操作 Projects v2 字段。这显示用户有更精细的项目管理需求。
    - **#7716**: MCP 服务器流程需要**认证支持**，这是企业级应用落地的必要能力。
    - **#7715**: Telegram 连接需要**模式选择**，避免隐私混淆。
- **内部规划**:
    - **通知系统重构**：一系列相关 Issue (#7687, #7688, #7689, #7690, #7691) 和 #7706 表明，团队正计划将现有仅限审批的通知中心，升级为支持多种类型（审批、认证、运行状态）的持久化用户收件箱。这是一个重要的产品功能增强。
    - **自动化结果推导**：PR #7650 旨在用运行时证据取代基于答案的语义判断，使自动化运行结果更可靠、可审计。
    - **后端持久化建议**：PR #7694 引入了产品表面无关的 `suggestions` 操作，为 WebUI 等客户端提供持久化的后端建议功能。

### 7. 用户反馈摘要

- **痛点**：用户对 GitHub Projects v2 字段无法操作感到不便 (#7719)，对 MCP 服务器和 Telegram 连接流程中的配置缺失感到困惑 (#7715, #7716)。Slack 公共频道中的连接提示暴露隐私且流程繁琐 (#7681)。
- **需求**：功能请求集中在**更强的集成能力**（GitHub Projects、MCP 认证）和**更清晰的连接引导**（Telegram、Slack）上。这些反馈均被项目团队快速承接，并转化为明确的开发任务或修复 PR。
- **满意度**：从部分 Issue/PR 被快速关闭来看，社区对问题响应的速度和透明度是认可的。特别是 #7598 和 #7594 等性能优化被快速处理，展示了团队的行动力。

### 8. 待处理积压

以下 Issue/PR 已存在较长时间且未被解决，值得维护者关注：

- **Issue #3762 (已开放 ~3 个月)**: 在 Web UI 中编辑 `AGENTS.md` 不会更新当前或未来对话的系统提示词。这是一个客户报告的 P1 问题，但长时间未关闭，可能涉及架构层面的调整，需要重点跟踪。
- **PR #7184 (已开放 ~2 周)**: 为 WASM 工具添加 Nostr 主机函数。虽然内容完整，但状态始终未更新，可能需要确认其优先级或是否被其他工作阻塞。
- **PR #7513 (已开放 ~1 周)**: 来自新贡献者的 ACP 服务命令（含流式与取消支持）。新贡献者的 PR 需要及时跟进，以避免打击其积极性。

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

# LobsterAI 项目动态日报 — 2026-08-18

## 今日速览

LobsterAI 项目在过去 24 小时内维持中高活跃度：共产生 21 条 PR 动态和 7 条 Issue 动态，其中 17 条 PR 已合并/关闭，4 条待合并；7 条 Issue 全部处于开启状态，暂无新关闭。值得关注的是，今日有**两批 PR 集中涌入**——一批是当天新提交的近期功能（如 dsh 引擎集成、OrcaRouter 提供商接入），另一批是 4 月提交的 12 条 PR 被集中清理合并（标记为 stale 后统一处理），说明维护者正在对积压 PR 进行系统性的收尾。Issue 方面虽然新开仅 1 条（#2500 项目推广贴），但 6 条历史 stale issue 均在今日获得评论更新，说明社区用户仍在等待官方回应，维护者需关注长期未解决的反馈。

---

## 版本发布

过去 24 小时内**无新版本发布**（最新 Releases 为空）。但值得关注的是近期 PR #1663 将 OpenClaw runtime 从 v2026.3.2 升级至 v2026.4.12（已于今日合并），并同步升级了 openclaw-weixin 插件至 2.1.8（修复了与新版 plugin-sdk 的兼容性问题）。建议关注下一次正式版本发布，预计将包含多项近期的功能增强。

---

## 项目进展

今日项目推进集中在以下几个方面：

### 1. Agent 工作目录独立配置（已合并，值得关注）
**PR #1668** 为每个非 main Agent 添加了独立工作目录配置，支持自定义工作目录，未配置时自动回退到 OpenClaw 默认行为。涉及数据迁移，存量数据自动兼容。这是对 #1644 中用户"main agent 感知不到其它 agent"问题的部分回应。

### 2. 用户体验与交互修复（合并 8 条）
合并了 12 条 4 月标记为 stale 的 PR，其中大部分为 Cowork 功能的交互改进：
- **#1636** 聊天窗口新增悬浮「滚动到底部」按钮
- **#1637** AI 回复消息新增「重新生成」按钮
- **#1639** 修复多处按钮 tooltip 硬编码英文未国际化
- **#1640** 工具执行结果增加一键复制按钮
- **#1641** 所有弹窗统一支持 Esc 键关闭
- **#1642** Windows 右键菜单支持
- **#1661** 导出日志脱敏（安全修复）

**#1642** 的右键菜单功能是 Windows 用户呼声较高的功能，现已在 Windows 资源管理器中开放 LobsterAI 快捷入口，对 Windows 用户使用体验提升明显。

### 3. 模型提供商支持增强
- **PR #2504** 新增 **OrcaRouter** 作为一级提供商集成（待合并），支持 Anthropic/OpenAI 兼容的模型路由网关
- **PR #1667** 将 Qwen 控制台链接从阿里云灵积迁移至百炼（已合并），避免用户访问即将下线的旧控制台

### 4. dsh (DeepSeek Harness) 引擎集成（今日最高频关键词）
- **PR #2502** dsh engine integration（macOS，已合并）
- **PR #2505** dsh process launcher（已合并）
- **PR #2506** dsh runtime setup instructions（待合并）

### 5. 其他修复
- **#2503** Electron 文本输入框增加编辑右键菜单（剪切/复制/粘贴/全选）（已合并）
- **#2501** 技能升级进度弹窗修复，改为通过 document.body 渲染覆盖整个应用外壳（已合并）
- **#1669** 设置页模型提供商体验修复：禁用逻辑优化、自定义提供商名称显示修正（已合并）
- **#1675** 会话列表按时间分组（今天/昨天/7天/30天/更早按月细化）（已合并）

---

## 社区热点

### 热点 1：Issue #2500 — 项目推广（VOKO：AI Agent 跨平台通信层）
- 评论数：1 | 状态：OPEN
- 链接：[#2500](https://github.com/netease-youdao/LobsterAI/issues/2500)
- 分析：VOKO 作者以"点 star 表示支持"的方式推广其开源项目，定位为"AI 智能体的跨平台通信层"，已接入 OpenClaw、VOKO IM、AstrBot，具有群协作能力。这反映了社区对 **A2A（Agent-to-Agent）标准化**的需求正在上升，LobsterAI 面临潜在的生态位竞争与合作机会。

### 热点 2：Issue #1644 — Agent 间互相感知与协作
- 评论数：1（今日更新） | 状态：OPEN（stale）
- 链接：[#1644](https://github.com/netease-youdao/LobsterAI/issues/1644)
- 分析：用户期望 main agent 能感知和管理其它 agent，并通过基于 md 文件的工作流将多个 agent 组织起来完成复杂任务。这是对 **Agent 编排**方向的明确需求信号，结合今日合并的 #1668（Agent 独立工作目录），项目正在朝 Agent 间协作方向演进。

### 热点 3：Issue #1653 — groupPolicy 覆盖问题
- 评论数：2 | 状态：OPEN（stale）
- 链接：[#1653](https://github.com/netease-youdao/LobsterAI/issues/1653)
- 分析：用户报告 groupPolicy 周期性被覆盖为 allowlist，超过 4 个月未解决，属于配置持久化层面的稳定性问题。

---

## Bug 与稳定性

| 严重程度 | Issue | 描述 | 状态 | 是否有 Fix |
|---------|-------|------|------|-----------|
| 中 | [#1653](https://github.com/netease-youdao/LobsterAI/issues/1653) | groupPolicy 每过一会就被覆盖为 allowlist，配置无法持久化 | OPEN / stale，4个月+ | 无 |
| 中 | [#1635](https://github.com/netease-youdao/LobsterAI/issues/1635) | Ollama 本地模型（qwen3 至 gemma4）均无法使用，CherryStudio 正常 | OPEN / stale，4个月+ | 无 |
| 中 | [#1662](https://github.com/netease-youdao/LobsterAI/issues/1662) | 除 SSE 之外的 MCP 引擎无法找到并使用 | OPEN / stale，4个月+ | 无 |
| 低 | [#1643](https://github.com/netease-youdao/LobsterAI/issues/1643) | 手动创建定时任务保存时误报"还有内容未保存"（实际已保存成功） | OPEN / stale，4个月+ | 无 |
| 低 | [#1671](https://github.com/netease-youdao/LobsterAI/issues/1671) | md 转 word 时 SSE 响应中断（finish reason: full） | OPEN / stale，4个月+ | 无 |

**稳定性评估：** 今日合并的 **#1661**（日志脱敏）解决了导出日志中明文密钥泄漏的安全隐患，建议维护者尽快发布包含此修复的版本。但上述 5 个历史 Bug（均超过 4 个月）至今无对应修复 PR，已成为影响用户留存的关键问题，建议按优先级排期处理。

---

## 功能请求与路线图信号

### 新功能诉求（来自 Issues）

| 用户诉求 | 来源 | 状态 | 版本纳入可能性 |
|---------|------|------|---------------|
| **Agent 间协作**：基于 md 文件的工作流组织多 Agent 完成复杂任务 | [#1644](https://github.com/netease-youdao/LobsterAI/issues/1644) | OPEN | **高**（已有独立工作目录 #1668 合并，方向一致） |
| **A2A 互通**：跨 Agent 框架、跨 IM 渠道通信与群协作 | [#2500](https://github.com/netease-youdao/LobsterAI/issues/2500) | OPEN | 中（VOKO 可作参考实现） |

### 今日合并的功能增强
- 非 main Agent 独立工作目录配置（#1668）
- 会话列表时间分组（#1675）
- 弹窗 Esc 关闭、右键菜单、滚动到底部、重新生成等交互改进（#1636/#1637/#1641/#1642）
- 工具结果复制按钮（#1640）
- OrcaRouter 提供商接入（#2504，待合并）
- dsh 引擎集成（#2502/#2505/#2506）

### 路线图信号
结合用户需求和已合并 PR，**Agent 编排与协作**方向是当下最明确的路线图信号。建议关注：
1. Agent 间的感知与通信机制
2. 多 Agent 工作流编排能力
3. 日志脱敏后的安全加固

---

## 用户反馈摘要

从今日活跃的 Issues 和 PR 评论中提炼的核心用户反馈：

**满意度提升点：**
- 今日合并的 12 条 UX 改进 PR 涵盖了用户在聊天交互（底部按钮、重新生成、复制）和弹窗体验（Esc 关闭、右键菜单）等高频场景中的常见需求，这批改动预计将显著提升日常使用效率。
- 会话列表按时间分组、独立工作目录等精细化功能正在缩小与主流 Chat 产品（微信、Slack 等）的体验差距。

**核心痛点（长期未解决）：**
1. **Ollama 本地模型全面失效**（#1635）——用户强调"ollama 本身没有问题，cherrystudio 可以正常调用"，问题定位在 LobsterAI 与 Ollama 的集成层，4 个月未修复，影响本地模型用户群体。
2. **groupPolicy 配置被覆盖**（#1653）——配置持久化问题影响企业组策略场景，用户对"每次过一会就被覆盖"表示困惑。
3. **非 SSE 的 MCP 无法使用**（#1662）——限制了 MCP 生态的接入范围，用户选择 LobsterAI 作为 MCP 客户端的核心诉求受阻。
4. **Agent 间互不感知**（#1644）——用户尝试通过 memory_search 和 agents_list 发现已创建的 agent 未果，反馈了当前多 Agent 架构的信息孤岛问题。

**特别关注：**
- Issue #1643 中用户反馈："应用已经保存成功了"但界面仍提示"还有内容未保存"——这说明是一个 **UI 误报 Bug** 而非功能缺陷，修复难度低，建议优先处理。

---

## 待处理积压

以下为长期未响应、可能影响项目健康度的 Issue/PR，建议维护者重点关注：

### 需优先处理的 Issues

| 编号 | 标题 | 创建时间 | 等待时长 | 优先级建议 |
|------|------|---------|---------|-----------|
| [#1635](https://github.com/netease-youdao/LobsterAI/issues/1635) | Ollama 本地模型无法使用 | 2026-04-12 | 4个月+ | 🔴 高 — 影响本地模型核心用户 |
| [#1653](https://github.com/netease-youdao/LobsterAI/issues/1653) | groupPolicy 被覆盖 | 2026-04-13 | 4个月+ | 🔴 高 — 配置可靠性问题 |
| [#1662](https://github.com/netease-youdao/LobsterAI/issues/1662) | 非 SSE 的 MCP 无法使用 | 2026-04-14 | 4个月+ | 🟡 中 — 影响 MCP 生态扩展 |
| [#1643](https://github.com/netease-youdao/LobsterAI/issues/1643) | 定时任务保存误报 | 2026-04-12 | 4个月+ | 🟢 低 — 仅 UI 误报 |

### 待合并 PR

| 编号 | 标题 | 创建时间 | 备注 |
|------|------|---------|------|
| [#1660](https://github.com/netease-youdao/LobsterAI/pull/1660) | 非 main agent 首页显示 agent 名称和描述 | 2026-04-13 | stale，待维护者 review |
| [#2504](https://github.com/netease-youdao/LobsterAI/pull/2504) | OrcaRouter 提供商接入 | 2026-08-17 | 新提交，待 review |
| [#2506](https://github.com/netease-youdao/LobsterAI/pull/2506) | dsh runtime setup 文档 | 2026-08-17 | 新提交，待 review |
| [#1277](https://github.com/netease-youdao/LobsterAI/pull/1277) | electron 依赖升级（40.2.1 → 43.4.0） | 2026-04-02 | dependabot，已积压 4 个月+ |

### 风险提示

- 6 条 stale Issues 今日均获得"最后更新"但无官方回复，说明用户仍在等待。大量 4 个月未解决的问题可能引发**用户流失和社区信任度下降**。
- 建议维护者在本周内对上述 4 个高/中优先级 Issues 给出明确回应（计划修复，或说明原因），避免社区情绪进一步积累。

---

> **总结：** LobsterAI 今日在功能迭代上表现活跃（尤其是 UX 改进和 dsh 集成），但长期积压的 Bug 和 stale PR 仍是项目健康度的主要风险点。建议在推进新功能的同时，分配资源清理历史遗留问题，特别是涉及本地模型和 MCP 生态的核心痛点，以稳固社区基础。

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

# Moltis 项目日报 | 2026-08-18

## 今日速览

Moltis 项目过去24小时保持中高活跃度：共处理 **2 条 Issue**（全部关闭）和 **9 条 PR**（其中 3 条待合并、6 条已合并/关闭）。CI 流水线红灯问题（#1202）已解决，活跃 PR 集中在**心跳调度修复**与**Files 库/设置浏览器**两个方向。值得注意的是，两个较老的功能性 PR（#1125、#1130）在积压两个月后终获合并，说明维护者正在清理历史 PR 积压。整体项目健康度良好，核心功能持续推进，依赖更新保持常态化。

---

## 版本发布

今日无新版本发布。最近一次 Release 信息暂无。

---

## 项目进展

今日关闭/合并的 PR 中，有 4 项属实质性进展：

| PR | 内容 | 意义 |
|---|---|---|
| [#1130](https://github.com/moltis-org/moltis/pull/1130) | make webui rpc timeout configurable | 对应 Issue #1127（6月提出），耗时两个月后合并，解决了 WebUI RPC 超时不可配置的问题 |
| [#1125](https://github.com/moltis-org/moltis/pull/1125) | Support model and effort selection for external agents | 为外部代理（external-agent）在 `/model` 中增加 model/effort 选择支持，扩展了多代理场景下的灵活性 |
| [#1103](https://github.com/moltis-org/moltis/pull/1103) | fix(browser): pierce shadow DOM lookups efficiently | 修复浏览器自动化中 Shadow DOM 穿透查询的效率问题，对依赖浏览器快照的功能是重要性能改进 |
| [#1204](https://github.com/moltis-org/moltis/pull/1204) | feat: add MiniMax Code ACP agent | 新增 MiniMax Code 作为外部代理种类，扩展了支持的代理生态 |

此外，两个 Dependabot 依赖更新 PR（#1207、#1087）也已合并，涵盖 wasmtime-wasi、quinn-proto、serde_with、tar 等库的安全与功能更新。

**项目整体向前迈进的判断**：上述合并（尤其 #1125 与 #1130）意味着 Moltis 在多代理配置灵活性和 WebUI 可操作性上均有实质提升，且历史 PR 积压正在被消化。

---

## 社区热点

今日讨论最集中的是 3 个待合并 PR，均为 **Lstarsky0** 提交，分别针对 **gateway 配置语义**与 **cron 调度缺陷**：

- [#1209](https://github.com/moltis-org/moltis/pull/1209)：fix(gateway): treat heartbeat.update params as a patch, not a whole config — 修复 `heartbeat.update` 将整个配置覆盖的问题（`#[serde(default)]` 导致未传字段被重置为默认值而非保留原值）
- [#1208](https://github.com/moltis-org/moltis/pull/1208)：fix(cron): honor heartbeat active hours when the scheduler fires — 修复 `heartbeat.active_hours` 从未生效的 bug（`is_within_active_hours` 已写好但从未被调用）
- [#1206](https://github.com/moltis-org/moltis/pull/1206)：Add managed Files library and Settings browser — 新增持久化 Files 库（支持流式上传/下载/移动/删除）和 Finder 风格设置浏览器

**热点分析**：前两个 PR 都在修复**配置语义不一致**的问题——一个是覆盖而非补丁（#1209），一个是配置存在但完全不生效（#1208）。这类问题容易导致用户配置"看起来设置了但实际不如预期"，反馈价值高。第三个 PR 则是较大的功能扩展（新增 Files 库 + 管理界面），可能是 Moltis 向"更完整的工作台形态"演进的信号。

---

## Bug 与稳定性

今日无新报 Bug，两起已关闭 Issue 分类如下：

**中优先级（已修复）**

- **#1202** — CI 格式检查红灯：`scripts/check-file-size.sh` 在 main 分支（594ffaf1）失败，两个文件超 1500 行限制（`crates/memory-zvec/src/store.rs` 1799 行、`crates/gateway/src/methods/services/admin.rs` 1531 行），均源自 9b47001a 提交。该问题导致 `Format` CI job 持续红色，已关闭（同日修复）。

**已闭环**

- **#1127** — 功能请求：允许配置 RPC 超时（6月17日提出，8月17日随 PR #1130 合并关闭）。用户需要可调的 RPC 超时参数以应对慢速远端服务。

```mermaid
xychart-beta
    title "Issue 存活时长（天）"
    x-axis ["#1202", "#1127"]
    y-axis ["天数", 0, 70]
    bar [1, 61]
```

---

## 功能请求与路线图信号

| Issue/PR | 请求内容 | 状态 | 可能纳入版本 |
|---|---|---|---|
| #1127（Issue 已关闭） | WebUI RPC 超时可配置 | ✅ 已合并（#1130） | 已纳入 |
| #1125（PR 已合并） | 外部代理支持 model/effort 选择 | ✅ 已合并 | 已纳入 |
| #1204（PR 已合并） | MiniMax Code ACP 代理 | ✅ 已合并 | 已纳入 |
| #1206（PR 待合并） | 托管 Files 库与 Settings 浏览器 | ⏳ 待审 | 有较大概率进入下一版本（功能较完整） |

**路线图信号小结**：三个方向正在推进——**代理生态扩展**（MiniMax + model/effort 选择）、**WebUI 可配置性**（RPC 超时）、**本地文件管理能力**（Files 库）。前两者已落地，后者正处于审查阶段。

---

## 用户反馈摘要

从今日活跃（含关闭/合并）的 Issue 与 PR 评论中提炼：

- **配置语义易混淆**（#1209/#1208）：`heartbeat.update` 的整配置覆盖行为与 `active_hours` 完全不生效，反映出用户对配置应当"增量更新"和"每项配置都应有实际效果"的期望。这两个修复均来自同一贡献者（Lstarsky0），属于典型的"实际使用后发现问题并回馈"模式。
- **工具链约束被重视**（#1202）：文件行数超限导致 CI 红灯，虽非功能性问题，但说明项目对代码风格约束有自动化保障，且维护者对该约束的执行是持认真态度的。
- **依赖更新自动化的顺畅体验**：两个 Dependabot PR 均在当天被合并，体现自动化依赖管理流程的高效。

---

## 待处理积压

以下为需关注的历史遗留项：

| 项目 | 创建时间 | 存活天数 | 当前状态 | 备注 |
|---|---|---|---|---|
| [#1103](https://github.com/moltis-org/moltis/pull/1103) 原 PR #1100 的替代路径 | 2026-06-04 | 74 天 | 🔒 今日已合并 | 从"需要维护者关注"转为"已解决" |
| [#1206](https://github.com/moltis-org/moltis/pull/1206) (OPEN) | 2026-08-17 | 1 天 | ⏳ 待审 | 功能面较大，建议尽快安排 reviewer |
| [#1208](https://github.com/moltis-org/moltis/pull/1208) (OPEN) | 2026-08-17 | 1 天 | ⏳ 待审 | 明确 bug 修复，风险低 |
| [#1209](https://github.com/moltis-org/moltis/pull/1209) (OPEN) | 2026-08-17 | 1 天 | ⏳ 待审 | 配置语义修复，建议与 #1208 一并审阅 |

**提醒维护者**：今日 3 个 OPEN PR 均来自同一贡献者（Lstarsky0），且相互关联（都涉及 `heartbeat` 配置/调度），建议合并审阅以快速闭环。历史上 #1127 存活 61 天且 PR #1130 也被搁置两个月才合并，缩短此类功能性 PR 的审阅周期有助于提升贡献者积极性。

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

好的，这是根据您提供的 CoPaw (github.com/agentscope-ai/CoPaw) GitHub 数据生成的 2026-08-18 项目动态日报。

---

# CoPaw 项目动态日报 - 2026年08月18日

## 1. 今日速览

今日 CoPaw 项目（QwenPaw）整体活跃度极高，共处理了 49 项 Issue/PR 更新，显示出强劲的社区参与度和开发迭代速度。Bug 修复和稳定性增强是今日的重点，共关闭了 6 个 Issue 和 22 个 PR（含合并），其中解决了多个影响用户的关键问题，如 MCP 工具调用崩溃、图片附件丢失、插件热重载失效等。同时，社区对功能改进的呼声很高，涌现了多个高质量的 Feature Request（如按频道配置模型、定时任务细节展示），并有首个贡献者提交了针对性的 PR。项目目前处于快速修复与功能扩展并行的良性发展阶段。

## 2. 版本发布

- 无新版本发布。

## 3. 项目进展

今日有 22 个 PR 被合并或关闭，主要集中在 Bug 修复和体验优化，体现了项目对稳定性的重视。

- **修复关键 Bug**: 合并了 `fix(console): update context-usage ring after compact` ([#6975](https://github.com/agentscope-ai/QwenPaw/pull/6975))，修复了 `/compact` 后上下文用量环不更新的问题；合并了 `fix(token-usage): stop counting image base64 as text tokens` ([#6968](https://github.com/agentscope-ai/QwenPaw/pull/6968))，解决了因 Base64 图片被错误计为文本 Token 导致上下文窗口被迅速占满的误报问题。
- **增强前端体验**: 合并了 `feat(console): add media download controls` ([#7036](https://github.com/agentscope-ai/QwenPaw/pull/7036))，为聊天中的媒体附件（如音频）添加了下载功能。合并了 `feat(console): remove approval hints from i18n placeholders` ([#6981](https://github.com/agentscope-ai/QwenPaw/pull/6981))，对多语言 UI 文案进行了优化。
- **PawApp 生态建设**: 合并了重量级 PR `feat(pawapp): add native DataPaw app runtime and durable analysis workspace` ([#6940](https://github.com/agentscope-ai/QwenPaw/pull/6940))，为平台引入了原生的 DataPaw 应用运行时和持久化分析工作区，是生态扩展的重要一步。同时，相关 CI pipeline 的 PR ([#7089](https://github.com/agentscope-ai/QwenPaw/pull/7089)) 也已开启，旨在为其建立独立的发布流程。
- **UI 细节修复**: 合并了 `fix(GitPanel): fix tabs styles not applied due to incorrect class prefix` ([#5151](https://github.com/agentscope-ai/QwenPaw/pull/5151))，修复了 GitPanel 样式不生效的遗留问题。

## 4. 社区热点

今日社区讨论最热烈的问题主要围绕升级后和特定渠道的兼容性问题。

- **热度 Issue**: **[#6405] [Question]: 升级2.0以后，mcp工具总是提示Tool notfound** ([链接](https://github.com/agentscope-ai/QwenPaw/issues/6405))。该问题评论数最多（7条），由用户 `70995781` 提出。尽管该 Issue 今日被标记为已关闭，但用户报告在升级到 2.0 后，即使工具名带了 `[mcp-key]__` 前缀，MCP 工具仍无法被找到。这反映出升级过程可能存在兼容性问题，是用户迁移时的主要痛点。
- **活跃 Bug 讨论**: **[#7011] [Bug] Console stop request can cancel an active Feishu session under multiple UI sessions** ([链接](https://github.com/agentscope-ai/QwenPaw/issues/7011))。该问题获得了 6 条评论，用户 `djj532` 详细更新了研究发现，证实了在多个 UI 会话下，一个控制台的停止请求会错误地取消另一个活跃的飞书会话。这涉及到复杂的会话管理和并发控制问题，社区对此关注度较高。

## 5. Bug 与稳定性

今日报告的 Bug 大多有对应的修复 PR 或在讨论中，整体可控。按严重程度排列如下：

- **高严重度 - 崩溃问题**:
    - **[#7063] [Bug]: Agent 执行工具调用时必现崩溃** ([链接](https://github.com/agentscope-ai/QwenPaw/issues/7063))。`v2.1.0` 版本中，Agent 在执行工具调用时因 `async for` 错误遍历 coroutine 而崩溃。该 Issue 已关闭，表明问题已通过某种方式解决或标记为无效。
- **中严重度 - 功能异常**:
    - **[#7088] [Bug]: OneBot 频道传递短期有效的 QQ 图片 URL 给模型，导致会话被污染** ([链接](https://github.com/agentscope-ai/QwenPaw/issues/7088))。该问题已关闭，但描述了一个严重的会话污染问题（因 URL 过期导致模型报错并影响后续回复）。幸运的是，已有关联 PR **[#7087](https://github.com/agentscope-ai/QwenPaw/pull/7087)** 提出在模型请求前本地化远程媒体 URL，可能会从根本解决此类问题。
    - **[#7082] [Bug]: Model 'unknown' execution failed. `_StructuredOutputDynamicClass` is not fully defined** ([链接](https://github.com/agentscope-ai/QwenPaw/issues/7082))。控制台渠道初始化时因 Pydantic 模型定义问题导致 `MODEL_EXECUTION_ERROR`，影响功能使用。
    - **[#7077] [Bug]: Plugin runtime hooks silently lost after workspace reload** ([链接](https://github.com/agentscope-ai/QwenPaw/issues/7077))。插件在工作区热重载后，其运行时钩子会静默丢失，影响插件功能的稳定性。
- **低严重度 - UI/交互问题**:
    - **[#7084] [Bug]: 历史对话只有一条时，打开新聊天后点不开历史会话** ([链接](https://github.com/agentscope-ai/QwenPaw/issues/7084))。一个特定的前端交互问题。
    - **[#7048] [Bug]: `cron update` 命令返回成功但 prompt 未更新** ([链接](https://github.com/agentscope-ai/QwenPaw/issues/7048))。CLI 工具的一个功能性 Bug。

## 6. 功能请求与路线图信号

今日用户提交了多个高质量的功能建议，均可能成为后续版本迭代的方向。

- **配置与管理**:
    - **[#7085] [Feature]: 按频道独立配置模型** ([链接](https://github.com/agentscope-ai/QwenPaw/issues/7085))。用户希望不同渠道（钉钉、微信、控制台）可以使用不同的模型，这比当前的全局配置更灵活。
    - **[#7075] [Feature]: 增加定时任务的运行细节** ([链接](https://github.com/agentscope-ai/QwenPaw/issues/7075))。用户希望看到定时任务更详细的运行状态（开始时间、时长、结果等），而非仅在失败时看到信息。
- **记忆与协作**:
    - **[#7079] / [#7080] [Feature]: Add optional PowerContext pluggable long-term memory backend** ([Issue](https://github.com/agentscope-ai/QwenPaw/issues/7079) / [PR](https://github.com/agentscope-ai/QwenPaw/pull/7080))。开发者 `kic635` 提出了一个完整的、可插拔的长期记忆后端方案，并直接提交了实现 PR。这显示出社区开始为项目贡献核心架构能力。
    - **[#6925] [Feature]: 智能体协作希望在一个会话窗口里** ([链接](https://github.com/agentscope-ai/QwenPaw/issues/6925))。用户对当前多智能体协作需要切换会话窗口的体验提出了改进期望，希望能在单一窗口内查看和交互。
- **生态集成**:
    - **[#7081] [PR]: feat: integrate AnySearch web search (SearchProvider + MCP)** ([链接](https://github.com/agentscope-ai/QwenPaw/pull/7081))。继被关闭的 [#6817](https://github.com/agentscope-ai/QwenPaw/pull/6817) 之后，`anysearch-ai` 再次提交了集成 AnySearch 搜索能力的 PR，表明该第三方集成意愿强烈，并可能提供了更完善的实现。

## 7. 用户反馈摘要

从今日的 Issues 和评论中，可以提炼出以下用户声音：

- **升级阵痛**: 用户 `70995781` 在升级到 2.0 后遇到 MCP 工具无法使用的严重问题 ([#6405](https://github.com/agentscope-ai/QwenPaw/issues/6405))，这在短期内是影响用户体验的主要因素，但也说明核心功能的兼容性需要在新版本发布前得到更多验证。
- **对精细化控制的需求**: 多个请求（按渠道配置模型 [#7085](https://github.com/agentscope-ai/QwenPaw/issues/7085)、定时任务细节展示 [#7075](https://github.com/agentscope-ai/QwenPaw/issues/7075)）表明，用户已不满足于基础的可用性，开始追求更灵活、更透明的配置和监控能力。
- **社区贡献意愿强**: 出现了多个由“first-time-contributor”提交的、具有一定完成度的 PR（如 PowerContext 记忆后端 [#7080](https://github.com/agentscope-ai/QwenPaw/pull/7080)、AnySearch 集成 [#7081](https://github.com/agentscope-ai/QwenPaw/pull/7081)），反映出 CoPaw 社区的活跃度和开发者的参与热情。

## 8. 待处理积压

以下 Issue 或 PR 已存在一段时间，仍处于开放状态，建议维护者关注：

- **长期未合并的大规模 PR**: **[#6302] feat: unify provider discovery, model metadata, routing, and agent controls** ([链接](https://github.com/agentscope-ai/QwenPaw/pull/6302))。此 PR 由 `wangfei010313` 于 2026-07-21 创建，旨在统一 Provider 发现、模型元数据和路由，属于架构层面的重大改动。该 PR 已开放近一个月，需评估其复杂度和合并计划。
- **待定夺的第三方集成**: **[#6515] feat(providers): add Volcengine Agent Plan and Xiaomi MiMo V2.5 API as built-in providers** ([链接](https://github.com/agentscope-ai/QwenPaw/pull/6515))。此 PR 自 7月28日 开放，提议增加两个新的内置模型提供商。是否接受此集成，需要项目方进行权衡。
- **安全问题相关 PR**: **[#6986] fix(sandbox): fix antivirus software blocking issues** ([链接](https://github.com/agentscope-ai/QwenPaw/pull/6986))。该 PR 解决沙箱被杀毒软件阻止的问题，虽描述模糊，但可能涉及安全性或兼容性问题，建议尽快跟进。
- **需求明确的待办 Issue**: **[#6925] [Feature]: 智能体协作希望在一个会话窗口里** ([链接](https://github.com/agentscope-ai/QwenPaw/issues/6925))。此需求提出一周，评论有一定讨论，且直接影响多智能体使用体验，值得在路线图中考虑。

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# ZeroClaw 开源项目动态日报

**日期**: 2026-08-18  
**数据窗口**: 2026-08-17 至 2026-08-18 (UTC)

---

## 1. 今日速览

ZeroClaw 项目在过去 24 小时内保持高位活跃：共更新 50 条 Issues 和 50 条 PR，其中 47 条 Issue 处于活跃或新开状态，41 条 PR 等待合并审查。项目当前正处于 v0.9.0 安全架构与网关重构的关键推进期——今日合并的 PR 覆盖了 WhatsApp 审批令牌泄漏修复、SOP 定义路径修复、跨平台 CI 测试矩阵上线以及 Email 附件隐式文件读取漏洞修复，显示了维护团队在安全加固和基础设施完善上的持续投入。需要关注的是，项目积压了大量高优先级 RFC（#7155 shell 策略、#7141 认证机制、#9487/#9488 会话与附件架构），且多个 PR 仍处于待合并状态，审查积压成为当前主要瓶颈。此外，Windows 平台 74 个测试失败（#7462）与 ETXTBSY 竞态问题（#9965/#10011）反映了测试基础设施的跨平台兼容性仍是薄弱环节。

---

## 2. 版本发布

过去 24 小时内没有新版本发布。当前最新版本为 0.8.4（依据 #6808 中的版本线索），v0.9.0 正按计划推进中（见 #7432 tracker）。

---

## 3. 项目进展

今日共合并/关闭 9 个 PR，主要成果如下：

### 🔒 安全修复（最高优先级）

- **[PR #9993] fix(email): stop implicit attachment file reads** — 修复 Email 外发附件可能将显示文件名隐式映射为本地文件读取的安全漏洞；现在仅从 `MediaAttachment.data` 构建 MIME 附件。同时补充回归测试覆盖字节、空载荷等场景。（[链接](https://github.com/zeroclaw-labs/zeroclaw/pull/9993)）

- **[PR #9612] fix(channels): tie the WhatsApp Cloud approval token to a guard so no exit orphans it** — 修复 WhatsApp Cloud 审批令牌在异常退出路径下残留孤儿凭证的问题；`request_approval` 在进程全局 `PENDING_APPROVALS` 映射中注册令牌，阻止工具调用决策中的悬挂凭证。（[链接](https://github.com/zeroclaw-labs/zeroclaw/pull/9612)）

### 🛠️ 功能与架构修复

- **[PR #9765] fix(sop): load SOP definitions from the shared workspace, not data_dir** — 修复 SOP 引擎错误地使用 `data_dir` 加载 SOP 定义（而非共享工作区）的问题；此前所有调用者均传入 `config.data_dir` 导致定义加载错误。（[链接](https://github.com/zeroclaw-labs/zeroclaw/pull/9765)）

### 🤖 CI/测试基础设施

- **[PR #9398] ci(tests): add scheduled macOS and Windows tests** — 新增每日 03:17 UTC（可手动触发）的 macOS/Windows 测试矩阵，弥补此前 CI 仅覆盖 Linux 的空白；此 PR 与 #7462（Windows 74 个测试失败）直接相关，是提升跨平台稳定性的重要一步。（[链接](https://github.com/zeroclaw-labs/zeroclaw/pull/9398)）

### 📦 其他合并

- 另有多项依赖升级和测试修复（含与 #9965 ETXTBSY 问题相关的部分修复）已合入。

**整体评估**：今日合并的 PR 聚焦安全加固与 CI 现代化，表明了维护者在发布 v0.9.0 前清理高危漏洞和构建跨平台验证能力的明确意图。项目正从核心功能开发阶段转向稳定化与加固阶段。

---

## 4. 社区热点

今日讨论最活跃的议题集中在以下几个方面：

### 🔥 高度活跃的 RFC 讨论

项目内多项 RFC 持续获得大量社区参与，反映出 ZeroClaw 社区在治理流程上的活跃度与参与感：

1. **[#6808] RFC: Work Lanes, Board Automation, and Label Cleanup**（23 评论）— 已批准/正在推进的治理型 RFC，包含 26 个修订版本，讨论热度居高不下。（[链接](https://github.com/zeroclaw-labs/zeroclaw/issues/6808)）

2. **[#8603] RFC: ZeroClaw Chat Completions profile**（23 评论）— 社区对 OpenAI Chat Completions 协议兼容的呼声很高。需求方包括 Open WebUI、LobeChat、Continue.dev、Aider、LangChain 及 OpenAI SDK 用户群体。核心诉求是：当前仅通过 WebSocket、ACP 和 per-channel webhooks 暴露代理能力，无法对接主流 OpenAI 协议客户端。（[链接](https://github.com/zeroclaw-labs/zeroclaw/issues/8603)）

3. **[#8303] RFC: Goal mode v1 — bounded foreground Matrix work**（22 评论，1 👍）— 关于实现跨多轮 agent 会话的持久化目标跟踪的提案讨论。（[链接](https://github.com/zeroclaw-labs/zeroclaw/issues/8303)）

### 📌 关键分析

社区热点集中在三个方向：
- **开放协议兼容性**（#8603）：表明用户希望将 ZeroClaw 嵌入现有的 LLM 工具链生态
- **治理与工作流优化**（#6808，#9496）：社区讨论显示项目自身的决策流程正在成为重点优化对象
- **安全策略与配置**（#7155，20 评论；#9487/#9488，各 19/18 评论）：高风险的架构与安全决策获得了持续的深度讨论

---

## 5. Bug 与稳定性

### 严重性分级

| 严重度 | Issue | 描述 | 状态 |
|--------|-------|------|------|
| **S1 - 安全漏洞** | — | Email 附件隐式本地文件读取（PR #9993 已合入修复） | ✅ 已修复 |
| **S1 - 安全漏洞** | — | WhatsApp 审批令牌孤儿悬挂（PR #9612 已合入修复） | ✅ 已修复 |
| **S2 - 严重缺陷** | [#7462](https://github.com/zeroclaw-labs/zeroclaw/issues/7462) | **Windows 平台 74 个测试失败** — 涉及 Unix-only 测试命令、路径语义和控制台编码（代码页 936），CI 未覆盖导致长期未被发现 | ⚠️ 已有 PR #9398 合并（增加 macOS/Windows CI），但修复仍需推进 |
| **S2 - 严重缺陷** | [#9965](https://github.com/zeroclaw-labs/zeroclaw/issues/9965) | **ETXTBSY 竞态** — 运行时写入的可执行测试夹具在并行运行时条件下触发"文本文件忙"错误 | ⚠️ 已有 PR #10010 修复 cron 测试，其余追踪中（#10011） |
| **S2 - 严重缺陷** | [#10023](https://github.com/zeroclaw-labs/zeroclaw/issues/10023) | **错误日志模型名** — 失败日志显示请求的模型名而非实际服务的 pinned fallback 模型，造成排查误导（2 评论） | 🔴 待处理 |
| **S3 - 一般缺陷** | PR #9056 | Provider 失败诊断信息笼统，缺少具体失败原因 | ⚠️ 需作者操作，有 stale 风险 |

**今日新提交的关键安全 PR（未合并）：**

- **[#9973] fix(providers): keep Gemini API keys out of URLs** — 将 Gemini API 密钥从 URL 移至 `x-goog-api-key` 标头，防止密钥通过 URL 日志泄漏（[链接](https://github.com/zeroclaw-labs/zeroclaw/pull/9973)）
- **[#10000] fix(channels): bound QQ and Mattermost downloads** — 为 QQ/Mattermost 添加入站下载大小限制，防止无限下载（[链接](https://github.com/zeroclaw-labs/zeroclaw/pull/10000)）

---

## 6. 功能请求与路线图信号

### 高可能性纳入 v0.9.0 的功能

基于 RFC 状态和 PR 匹配度研判：

| 功能 | 相关 Issue/PR | 信号强度 |
|------|--------------|----------|
| **Chat Completions 协议兼容** | #8603（23 评论，讨论热烈） | ⭐⭐⭐ 社区需求明确，但仍有风险讨论 |
| **Per-execution shell 命令确认机制** | #7155（20 评论，已修订至 Rev 3） | ⭐⭐⭐ 已进入规范化阶段 |
| **可插拔入站认证与规范主体** | #7141（16 评论，Rev 8，已接受） | ⭐⭐⭐ 已接受，目标为 v0.9.0 |
| **运行时拥有的安全决策管线** | #7142（11 评论，Rev 6） | ⭐⭐ 目标 v0.9.0 安全架构 |
| **统一附件架构** | #9488（18 评论，已接受） | ⭐⭐ 与 #9487 捆绑，需维护者评审 |
| **Hailo-Ollama 原生支持** | PR #9109（新增 provider，需作者操作） | ⭐⭐ 功能完成度高，等待审查 |
| **每模型能力与上下文窗口配置** | #7100（13 评论，已接受） | ⭐⭐ 已接受，等待落地 |

### 低概率但值得关注

- [#6653](https://github.com/zeroclaw-labs/zeroclaw/issues/6653) 模拟安装的主机架构策略 — P3 优先级
- [#10059](https://github.com/zeroclaw-labs/zeroclaw/issues/10059) ZeroCode 支持 macOS Option-Backspace 按键 — 良好的 first issue，P3

### 新提交的可选功能

- PR #10065：ZeroCode 文件浏览器搜索模式下的键盘导航修复（新提交，待审查）

---

## 7. 用户反馈摘要

> *以下反馈从今日活跃 Issues/PR 中提取。*

### 真实用户痛点

1. **"跨平台支持仍是短板"** （源自 #7462）
   Windows 11（简体中文，代码页 936）环境运行测试产出 74 个失败，涉及 Unix-only 命令、路径语义和控制台编码。CI 此前仅覆盖 Linux 导致问题长期未被发现——这反映了非 Linux 用户的体验盲区。

2. **"我想把 ZeroClaw 接入我的 AI 工具链"** （源自 #8603）
   多位用户反馈希望使用 Open WebUI 或 LobeChat 等界面连接到 ZeroClaw 的代理能力，但当前仅支持 WebSocket/ACP/webhooks，这限制了 ZeroClaw 融入主流 LLM 生态。

3. **"安全配置应该更细粒度"** （源自 #7155）
   社区要求对高风险 shell 命令增加"每次执行确认"的层级，类似 Claude Code 的 allow/ask/deny 策略，期望在灵活性和安全性之间取得更好的平衡。

4. **"配置热更新不生效，必须重启守护进程"** （源自 #7897）
   持久化配置变更不会自动应用到运行时子系统，需要手动触发 `/admin/reload` 才能让安全策略、频道配置等生效，在频繁调整配置的场景下非常不便。

5. **"错误日志会误导排查方向"** （源自 #10023）
   "当回退 provider 实际服务于不同的模型时，日志显示的还是请求的模型名。我在排查 gemini 和 openai 之间的故障转移时浪费了大量时间"——错误信息与实际行为不一致降低了可观测性的信任度。

### 值得关注的社区治理反馈

维护者和贡献者普遍反映 ZeroClaw 的 RFC 流程存在**"过慢"**问题（源自 #9496）：七天的讨论窗口、广泛的共识要求和手动投票协调使决策效率低下，这正在被追踪并制定简化方案。

---

## 8. 待处理积压

以下重要工作项长期未获得有效推进或需要维护者关注：

| 项目 | 类型 | 至今时长 | 状态 | 需要关注的原因 |
|------|------|----------|------|----------------|
| [#7462](https://github.com/zeroclaw-labs/zeroclaw/issues/7462) Windows 74 个测试失败 | Bug | 69 天（6/10 创建） | 已接受 | 虽然 #9398 已上线跨平台 CI，但 74 个测试失败的修复工作尚未被认领 |
| [#7155](https://github.com/zeroclaw-labs/zeroclaw/issues/7155) Shell 命令策略 RFC | RFC | 76 天（6/3 创建） | 已接受 | 已修订至 Rev 3，范围已收敛，但缺少已分配的负责人 |
| [#6165](https://github.com/zeroclaw-labs/zeroclaw/issues/6165) 轻量化核心/外部集成 RFC | RFC | 113 天（4/27 创建） | 需维护者评审 | 长期未获决定，影响核心架构方向 |
| [#9056](https://github.com/zeroclaw-labs/zeroclaw/pull/9056) Provider 诊断信息增强 | PR | 35 天（7/14 创建） | 需作者操作 | 有 `stale-candidate` 标签，若作者不响应可能被关闭 |
| [#9563](https://github.com/zeroclaw-labs/zeroclaw/pull/9563) Telegram 媒体信封填充 | PR | 19 天（7/30 创建） | 需作者操作，有 `stale-candidate` 标记 | P1 优先级，影响 Telegram 渠道图片/文档的附件传递链 |
| [#8691](https://github.com/zeroclaw-labs/zeroclaw/issues/8691) ADR 基线恢复与审计 | Tracker | 45 天（7/4 创建） | 已接受 | 属文档架构维护，优先级较低，但长期无人认领 |

### ⚠️ 维护者行动建议

1. **PR 审查积压严重**：41 个 PR 等待合并，涵盖 3 个 P1 安全修复（#9973 Gemini 密钥泄露、#10000 QQ/Mattermost 下载限制）、1 个 P1 Telegram 修复（#9314 长轮询偏移）——建议优先审查安全与 P1 优先级的 PR
2. **Windows 测试修复分配**：#7462 有明确的修复方向但缺少负责人，#9398 已消除 CI 空白，建议将此任务标记为 `help wanted`
3. **Github Actions 中的老旧 PR 处理**：多个 PR 带 `stale-candidate` 标签，需明确维护者决定是继续支持还是关闭

---

## 项目健康度评估

| 维度 | 状态 | 说明 |
|------|------|------|
| **社区活跃度** | 🟢 优秀 | 24h 内 47 条活跃 Issues，RFC 讨论参与度高 |
| **安全响应速度** | 🟢 良好 | 高危漏洞（Email 附件读取、WhatsApp 令牌）在数日内修复 |
| **发布进度** | 🟡 正常 | v0.9.0 目标明确（#7432 tracker），当前处于 0.8.x 稳定期 |
| **审查效率** | 🔴 不足 | 41 个 PR 等待合并，多个 P1 修复悬置 |
| **测试覆盖** | 🟡 改善中 | 跨平台 CI 已上线（PR #9398），但 Windows 失败修复尚未认领 |
| **文档与治理** | 🟡 自优化中 | RFC 流程简化提案（#9496）正在进行中 |

---

*本日报基于 GitHub 公开数据自动生成，如需更详细的数据或特定议题分析，请提供补充要求。*

</details>

---
*本日报由 [agents-radar](https://github.com/kky-wollu/agents-radar) 自动生成。*