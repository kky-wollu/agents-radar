# AI CLI 工具社区动态日报 2026-08-15

> 生成时间: 2026-08-14 22:28 UTC | 覆盖工具: 9 个

- [Claude Code](https://github.com/anthropics/claude-code)
- [OpenAI Codex](https://github.com/openai/codex)
- [Gemini CLI](https://github.com/google-gemini/gemini-cli)
- [GitHub Copilot CLI](https://github.com/github/copilot-cli)
- [Kimi Code CLI](https://github.com/MoonshotAI/kimi-cli)
- [OpenCode](https://github.com/anomalyco/opencode)
- [Pi](https://github.com/badlogic/pi-mono)
- [Qwen Code](https://github.com/QwenLM/qwen-code)
- [DeepSeek TUI](https://github.com/Hmbown/DeepSeek-TUI)
- [Claude Code Skills](https://github.com/anthropics/skills)

---

## 横向对比

# AI CLI 工具生态横向对比分析报告

**报告日期：2026-08-15** | **覆盖工具：Claude Code / OpenAI Codex / Gemini CLI / Copilot CLI / Kimi Code / OpenCode / Pi / Qwen Code / DeepSeek TUI (CodeWhale)**


## 1. 生态全景

当前 AI CLI 工具已从"单机辅助编码"全面迈向"多代理协作、企业级治理、跨设备工作流"的深水区。头部工具（Claude Code、Codex、Gemini CLI）在 AI 代理核心能力上快速迭代，同时社区反馈重心从"功能缺失"转向"生产环境可靠性"——token 透明度、静默失败、资源泄漏、安全过滤器误伤成为跨工具共通的质疑焦点。与此同时，二三梯队工具（Qwen Code、Pi、CodeWhale、Kimi Code）正通过差异化定位（Web Shell 生态、跨提供商聚合、本地模型支持）抢占细分市场，整体生态呈现"寡头竞速、长尾分化"的格局。


## 2. 各工具活跃度对比

| 工具 | 今日 Issues | 今日 PR | 版本发布 | 社区热度信号 | 迭代阶段 |
|------|------------|---------|---------|------------|---------|
| **Claude Code** | 10+ 热点（74评论峰值） | 5+ 活跃 | v2.1.233, v2.1.232 | 147👍 交互改进请求；token 浪费 Bug 73 评论 | 成熟稳定，高频迭代 |
| **OpenAI Codex** | 10+ 热点（100 评论峰值） | 10+ 合入 | 6 个 alpha 版本 | Windows 性能回归 4 条集中投诉 | 快速迭代，平台适配攻坚 |
| **Gemini CLI** | 10 个精选（12 评论峰值） | 8+ 合入 | 1 个 nightly | MAX_TURNS 误报成功修复 | 活跃修复，系统化清理积压 |
| **Copilot CLI** | 8+ 热点 | 3 个 | v1.0.80 + 补丁 | MCP OAuth 回归持续发酵 | 稳定维护，企业痛点集中 |
| **Kimi Code** | 5 个精选 | 0 合并 | 无 | 记忆系统 39 评论 | 低活跃，功能诉求积累期 |
| **OpenCode** | 10+ 热点 | 10 个（含 1 个高关注新 PR） | 无 | 48-bit ID 回绕严重 Bug；Memory Megathread 131 评论 | 社区活跃，2.0 架构调整期 |
| **Pi** | 10 个精选（27 评论峰值） | 10 个 | v0.84.2 | Windows 使用征集 27 评论 | 稳定迭代，性能优化期 |
| **Qwen Code** | 10 个精选（12 评论峰值） | 10 个 | v0.21.12 + 预览版 | 图片回归 12 评论；serve 资源治理 | 快速迭代，Web Shell 生态发力 |
| **DeepSeek TUI (CodeWhale)** | 10 个精选（13 评论峰值） | 10 个（含社区修复） | v0.9.8 | 品牌更名，CI 红标 | 活跃但工程成熟度待提升 |


## 3. 共同关注的功能方向

### 3.1 Agent 可靠性（跨工具最集中的痛点）
- **"假成功"问题**：Gemini CLI #22323（MAX_TURNS 误报 GOAL）、Claude Code #84474（PR 评论静默失败）、OpenCode #42608（ID 回绕致会话静默失效）——三个工具社区独立报告了"报告成功但实际未执行"的破坏性问题。
- **Agent 挂起/冻结**：Gemini CLI #21409（generalist 无限挂起）、Copilot CLI #4306（子代理冻结）、Kimi Code 社区对上下文丢失的集体抱怨。

### 3.2 上下文与 Token 管理
- **Token 消耗透明度**：Claude Code #60334（图片处理失败浪费 70% token）、CodeWhale #1004（/dryrun 预览请求）——用户要求"花 token 前先看到账单"。
- **上下文压缩策略**：Codex #29356（压缩丢失操作连续性）、Gemini CLI #22745（AST 感知读取减少 token 噪声）、Kimi Code #1283（记忆系统跨会话保留上下文）。
- **长会话内存治理**：Qwen Code #2128（5个月未关闭）、OpenCode #20695（Memory Megathread 131 评论）、CodeWhale #4326（RSS 不回落）。

### 3.3 Windows 平台体验（多个工具的明显短板）
- Codex 的 Windows 性能回归（#38554/#38547）、Copilot CLI 的 OOM 崩溃（#4499）、Pi 官方发起 Windows 使用征集（#7547）、Qwen Code 图片加载回归、Gemini CLI 的 ripgrep EFTYPE——Windows 是当前所有工具共通的"最弱平台"。

### 3.4 MCP 生态兼容性
- Copilot CLI 的 OAuth 回归（#4480/#4490）、MCP 超时上限（Claude Code #16837）、工具数量超限（Gemini CLI #24246）、分页缺失（Copilot CLI #4006）——MCP 集成从"能用"进入"按规范兼容"阶段。

### 3.5 安全与权限边界
- Claude Code 安全过滤器误伤无人机开发（#71920）、Qwen Code 只读 Shell 命令注入绕过（#8582）、Copilot CLI 的 `/spawn` 跨会话注入风险（#4491）、CodeWhale 默认权限变更遭反对（#5293）——自动化越强，用户越关注信任边界。

### 3.6 代理间协作（Agent-to-Agent）
- Gemini CLI PR #28738（允许 Agent 调用 Agent）、Claude Code 子代理 fork 默认开启、Codex gRPC 会话数限制移除、OpenCode 子代理 ID 暴露（PR #36883）——多代理编排正从实验走向默认能力。


## 4. 差异化定位分析

| 工具 | 核心定位 | 目标用户 | 技术路线 |
|------|---------|---------|---------|
| **Claude Code** | 通用编码代理标杆 | 专业开发者、追求模型能力上限 | Anthropic 模型深度整合；子代理 fork + prompt cache；API 网关企业特性 |
| **OpenAI Codex** | 全平台开发伴侣 | 跨平台重度用户、远程协作 | Electron 桌面 + TUI 双前端；unified exec 统一执行模型；Windows 平台攻坚中 |
| **Gemini CLI** | 高可靠性 Agent 框架 | 多代理工作流用户、对可观测性敏感 | SSR Agent 自动化修复；行为评估体系（76 个测试）；AST 感知前瞻布局 |
| **Copilot CLI** | 企业级安全与治理 | 企业组织、GitHub 生态用户 | 与 GitHub 策略/模型目录深度绑定；MCP 兼容追赶；企业模型管理是核心场景 |
| **Kimi Code** | 国产模型编程入口 | 中文开发者、Kimi 生态用户 | 记忆系统为最大差异化卖点；Windows/PS 兼容优化收尾；社区活跃度有待提升 |
| **OpenCode** | 开源开放的多提供商聚合 | 独立开发者、自托管用户 | 完全开源；动态模型发现（PR #42660）；OpenCode Zen 中继服务；2.0 架构重构期 |
| **Pi** | 跨提供商统一终端 | 多模型对比用户、本地/云混合工作流 | 极简 Go 单体；提供商适配最广（xAI/SiliconFlow/Anthropic Vertex）；TUI 性能优化中 |
| **Qwen Code** | Web Shell + 服务化部署 | 云端开发、团队协作 | serve 守护进程模式；Web Shell 生态快速扩展（Goal v3、媒体引用、Electron 宿主评估）；国内提供商接入 |
| **CodeWhale (DeepSeek TUI)** | DeepSeek 深度优化终端 | DeepSeek 模型重度用户、追求性价比 | 本地模型一键配置（DS4）；Auto-Review 双层模式；插件系统规划中；工程成熟度需加强 |


## 5. 社区热度与成熟度

**第一梯队：高活跃 + 高成熟度**
- **Claude Code**：热度与成熟度均为最高。v2.x 高频迭代，Issue 讨论质量高（👍 数、评论数均有说服力），社区诉求集中在"打磨"而非"缺失"。
- **OpenAI Codex**：社区活跃度极高（Windows 性能问题 100 评论），但持续的 Windows 回归问题暴露了跨平台工程成熟度的短板。

**第二梯队：快速追赶期**
- **Gemini CLI**：SSR Agent 批量修复动作频繁，修复质量获社区认可（根因修复而非表面补丁），处于"系统性清债"阶段。
- **OpenCode**：社区活跃（Memory Megathread 131 评论），但 48-bit ID 回绕这类基础性 Bug 说明工程严谨性仍需提升。
- **Qwen Code**：迭代速度快（v0.21.12 + 多预览版），Web Shell 生态有清晰战略方向，但 CI 反复失败和回归频发令人担忧。

**第三梯队：稳定维护 / 蓄势期**
- **Copilot CLI**：企业级功能持续完善，但社区反馈集中在长期未解决的企业策略问题，创新节奏相对平稳。
- **Pi**：迭代稳定（v0.84.2），社区讨论务实（Windows、性能、提供商支持），处于健康成长期。
- **CodeWhale**：品牌更新后活跃度上升，社区修复响应快（24 小时内修复 CI 红标），但工程体系（CI、schema 治理）仍在建设中。
- **Kimi Code**：活跃度最低，记忆系统是最大亮点但尚未落地，需要更多功能交付来激活社区。


## 6. 值得关注的趋势信号

### 6.1 "静默失败"成为最不可接受的行为
从 Claude Code 的 PR 评论静默失败、Gemini CLI 的 MAX_TURNS 误报、到 OpenCode 的会话静默失效——三个独立社区在同一天将矛头指向同一类问题：**用户宁可看到显式报错，也不接受"报告成功但实际没做"**。对所有 AI CLI 工具而言，"结果可验证性"即将成为核心竞争维度。

### 6.2 多代理编排从"实验"走向"默认"
Claude Code 子代理 fork 默认开启、Gemini CLI 推动 Agent-to-Agent 调用、Codex 移除会话数限制——多代理协作正在成为默认能力。随之而来的子代理权限隔离、终止原因正确传递、hook 可观测性将是下一波技术攻坚重点。

### 6.3 Windows 是最后的"未攻克平台"
几乎每个工具的社区反馈中都存在 Windows 特有的稳定性/性能/兼容性问题。随着更多开发者在工作站使用 AI CLI，Windows 支持的成熟度将成为影响工具选型的关键变量。Pi 官方向社区征集 Windows 使用场景、Codex 集中修复性能回归——先啃下 Windows 这块硬骨头的工具将获得显著竞争优势。

### 6.4 MCP 生态进入"规范兼容"深水区
OAuth 认证回归、分页缺失、超时上限、工具数量限制——MCP 集成已度过"能用"阶段，社区开始按规范逐条核对兼容性。能提供"规范级" MCP 实现的工具将在生态整合中占据先机。

### 6.5 安全过滤器的"误伤治理"成为信任分水岭
Claude Code 无人机开发误伤、Qwen Code 只读 Shell 注入绕过、Copilot CLI 的 `/spawn` 跨会话风险——安全策略的精度直接决定用户的信任度。**过严则伤体验、过松则伤安全**，如何在自动化与安全之间找到精确平衡点，是各工具共同面临的治理难题。

### 6.6 上下文记忆正在成为差异化竞争点
Kimi Code 的记忆系统（39 评论，社区最高呼声）、Gemini CLI 的 AST 感知读取、OpenCode/CodeWhale 的上下文压缩管理——跨会话记忆与上下文高效利用正在成为下一轮功能竞争的主战场。

### 6.7 对开发者的建议

- **选型参考**：追求模型能力上限选 Claude Code；深度绑定 GitHub 企业生态选 Copilot CLI；多提供商灵活切换关注 Pi/OpenCode；国产模型与 Web 端工作流关注 Qwen Code；本地模型性价比关注 CodeWhale。
- **版本策略**：若使用 Copilot CLI 且依赖 Atlassian/GitLab MCP，建议暂锁 v1.0.78；Codex Windows 用户关注 26.810.4967.0 后续修复；Qwen Code 用户如遇图片加载异常可回退至 0.21.1。
- **关注窗口**：未来 2-4 周关注 Claude Code 子代理 fork 的稳定性反馈、Gemini CLI 的 AST 感知进展、OpenCode 动态模型发现的落地质量、CodeWhale 插件系统发布。

---

*本报告由 AI 技术分析师基于 2026-08-15 各工具 GitHub 社区公开数据整理，数据完整性与准确性以各仓库实际状态为准。*

---

## 各工具详细报告

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills 社区热点

> 数据来源: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills 社区热点报告（数据截止 2026-08-15）

## 一、热门 Skills 排行（按社区关注度与讨论热度）

| 排名 | Skill / PR | 功能简介 | 社区讨论热点 | 当前状态 |
|------|-----------|---------|-------------|----------|
| 1 | **run_eval.py 修复**（[PR #1298](https://github.com/anthropics/skills/pull/1298)） | 修复 skill-creator 评估脚本始终报告 0% 召回率的严重缺陷 | 社区高度关注：该问题被 #556 及 10+ 独立复现确认，直接影响 skill-creator 描述优化循环的有效性；同时涉及 Windows 子进程读取、触发检测和并行 worker 等多个问题 | OPEN |
| 2 | **document-typography**（[PR #514](https://github.com/anthropics/skills/pull/514)） | AI 生成文档的排版质量控制：孤字换行、寡妇段落（页底孤立标题）、编号对齐等 | 社区认为这些排版问题影响所有 Claude 生成文档，是高频痛点；讨论聚焦如何让排版规则可操作性更强 | OPEN |
| 3 | **ODT skill**（[PR #486](https://github.com/anthropics/skills/pull/486)） | OpenDocument 格式（.odt/.ods）的创建、填充、读取和转换 | 社区关注开源格式支持，尤其是 LibreOffice 生态的互操作性；触发条件设计详尽 | OPEN |
| 4 | **skill-creator 安全性修复**（[PR #541](https://github.com/anthropics/skills/pull/541)、[#539](https://github.com/anthropics/skills/pull/539)、[#538](https://github.com/anthropics/skills/pull/538)） | 修复 DOCX 修订冲突、YAML 解析静默失败、大小写敏感文件引用 | 社区集中反映 skill-creator 在文档类技能中的稳定性问题；w:id 碰撞、未加引号描述符等问题会导致文档损坏或技能静默失效 | OPEN |
| 5 | **ServiceNow 平台 Skill**（[PR #568](https://github.com/anthropics/skills/pull/568)） | 覆盖 ITSM、ITOM、ITAM/SAM、FSM、HRSD、SPM、安全响应、IntegrationHub 的全面 ServiceNow 平台助手 | 社区点评：从窄脚本助手扩展为全平台技能，覆盖面广；讨论持续活跃（更新至 2026-08-12），可能成为企业级用户的重要工具 | OPEN |
| 6 | **self-audit**（[PR #1367](https://github.com/anthropics/skills/pull/1367)） | AI 输出交付前的机械验证 + 四维推理质量门禁 | 社区对"交付前审计"概念反馈积极；四维优先级（按损害严重度排序）的推理审计机制引发讨论 | OPEN |
| 7 | **pyxel retro game**（[PR #525](https://github.com/anthropics/skills/pull/525)） | 复古/像素风游戏开发技能，基于 pyxel-mcp 的迭代式开发工作流 | 社区关注创意开发场景中 MCP 与 Skill 的结合；更新活跃（至 2026-07-15） | OPEN |
| 8 | **testing-patterns**（[PR #723](https://github.com/anthropics/skills/pull/723)） | 全覆盖测试模式：Testing Trophy 模型、单元测试（AAA 模式）、React 组件测试 | 社区认可其系统性；测试哲学与"哪些不该测"的边界讨论热度较高 | OPEN |


## 二、社区需求趋势（源自 Issues）

**1. 安全与信任边界**（[Issue #492](https://github.com/anthropics/skills/issues/492)，43 评论）
社区技能被分发在 `anthropic/` 命名空间下，冒充官方技能，构成信任边界滥用。用户可能向看似官方的社区技能授予过高权限。这是当前最集中的安全担忧。

**2. 组织级技能共享**（[Issue #228](https://github.com/anthropics/skills/issues/228)，16 评论，8👍）
企业用户期望 Skills 可直接在组织内共享，无需手动下载 .skill 文件再通过 Slack/Teams 传递。此诉求位列社区高赞需求。

**3. 开发工具链稳定性**（[Issue #556](https://github.com/anthropics/skills/issues/556)、[#1169](https://github.com/anthropics/skills/issues/1169)）
`run_eval.py` 的 0% 触发率 bug 严重削弱 skill-creator 优化循环的有效性，且长期未修复。社区对开发工具的可靠性有迫切需求。

**4. 文档类技能的可靠性**（[Issue #12](https://github.com/anthropics/skills/issues/12)、[#1175](https://github.com/anthropics/skills/issues/1175)）
DOCX/ODT 技能导致的文件损坏、SharePoint Online 文档处理的上下文窗口与安全担忧，反映出文档处理这一高频场景对稳定性的高要求。

**5. 去重复与一致性**（[Issue #189](https://github.com/anthropics/skills/issues/189)，6 评论，9👍）
`document-skills` 与 `example-skills` 插件安装后内容雷同，导致上下文窗口重复。社区对插件生态的一致性问题表示不满。

**6. 上下文窗口安全**（[Issue #1487](https://github.com/anthropics/skills/issues/1487)）
`claude-api` 技能单次调用注入 ~156k tokens，直接耗尽上下文窗口。反映社区对"技能体积 vs 上下文预算"的重视。


## 三、高潜力待合并 Skills（近期可能落地）

1. **ServiceNow 平台技能**（[PR #568](https://github.com/anthropics/skills/pull/568)）— 更新至 8 月中旬，讨论持续活跃，覆盖面广，企业级需求潜力大
2. **document-typography**（[PR #514](https://github.com/anthropics/skills/pull/514)）— 解决普遍排版痛点，讨论质量高，维护者关注度较好
3. **ODT skill**（[PR #486](https://github.com/anthropics/skills/pull/486)）— 开源格式需求明确，触发条件设计完备，4 月后仍有更新
4. **self-audit**（[PR #1367](https://github.com/anthropics/skills/pull/1367)）— 与生态最近的安全与质量诉求高度契合，且有配套 Issue（#1385）同作者推进
5. **testing-patterns**（[PR #723](https://github.com/anthropics/skills/pull/723)）— 系统性测试覆盖，社区认可度高，但需关注维护者合并意愿


## 四、Skills 生态洞察（一句话）

**当前社区在 Skills 层面的最集中诉求是：开发工具链的稳定性与信任安全——即修复 skill-creator 的核心评估缺陷、明确技能来源的官方性边界，同时提升文档类技能（DOCX/ODT/PDF）的可靠性，并抑制技能对上下文窗口的过度占用。**

生态呈现"功能拓展与基础设施加固并行"的态势：一方面新增技能持续向企业平台（ServiceNow）、创意领域（Pyxel）、质量审计（self-audit）延伸；另一方面，围绕 run_eval.py 的反复修复尝试（#1298、#1099、#1050）和技能规格合规性校验（#1538）暴露出官方开发工具链在跨平台稳健性和规范执行上仍有明显短板。

---

# Claude Code 社区动态日报

**日期：2026-08-15** | 数据来源：github.com/anthropics/claude-code


## 今日速览

Claude Code 发布 v2.1.233 与 v2.1.232 两个版本，带来 GitLab MR URL 支持、`forward_user_identity` 网关设置，并将子代理（subagent）fork 能力设为默认开启。社区层面，图片处理失败导致 API token 浪费的 Bug（#60334）持续发酵，成为最受关注的问题；关于 Enter 键发送消息的交互改进需求（#2054）以 147 个 👍 位居热度榜首；此外，MCP 超时上限被限制在 60 秒的问题（#16837）引发开发者对灵活配置的诉求。


## 版本发布

### v2.1.233（最新）
- **GitLab MR URL 支持**：`--worktree` 标志及 `claude agents` 视图新增 GitLab Merge Request URL 解析，MR 以 `!N` 格式展示
- **用户身份转发**：Anthropic 上游新增 opt-in 的 `forward_user_identity` apps 网关设置，可发送登录用户身份作为 headers，便于代理后端识别用户

### v2.1.232
- **子代理 fork 默认开启**：`subagent_type: "fork"` 的子代理现在默认继承完整对话和 prompt cache；交互式会话中非 teammate 的 agent 生成默认在后台运行
- **会话引用**：在提示符中输入 `@` 可按名称引用另一个 Claude 会话


## 社区热点 Issues（Top 10）

### 1. [Bug] 图片处理失败导致对话 token 大量浪费
**#60334** | 作者: cristian-milea | 评论: 73 | 👍: 19 | 状态: 已关闭
[链接](https://github.com/anthropics/claude-code/issues/60334)

> **摘要**：大量图片处理失败错误（"an image in the conversation could not be processed and was removed"）导致用户 5 小时窗口约 70% 的 token 被浪费，且用户并未实际使用图片。反馈 ID 和错误日志已附上。

**关注价值**：评论数高居榜首，反映用户对 token 消耗透明度和错误恢复机制的极高期望，是成本敏感型用户的痛点。


### 2. [Feature] 用 Enter 换行而非发送消息
**#2054** | 作者: tmokmss | 评论: 28 | 👍: 147 | 状态: 开放
[链接](https://github.com/anthropics/claude-code/issues/2054)

> **摘要**：希望提供选项让 Enter 键用于插入新行而非发送消息。CJK 语言用户中 Enter 常用于确认输入，当前绑定极易导致不完整消息误发，十分困扰。

**关注价值**：👍 数最高（147），是社区最渴望的交互改进之一。CJK 用户群体诉求明确，且问题已开放一年以上仍被高频顶起，说明官方尚未给出让社区满意的方案。


### 3. [Bug] MCP_TIMEOUT 超过 60 秒不生效
**#16837** | 作者: marcindulak | 评论: 15 | 👍: 16 | 状态: 开放
[链接](https://github.com/anthropics/claude-code/issues/16837)

> **摘要**：Claude Code 不遵守大于 60 秒的 `MCP_TIMEOUT` 值，无论设置多少，超时都被钳制在 60 秒。附有可复现步骤。

**关注价值**：直接影响使用 MCP 进行长时间任务（如大模型推理、批量处理）的开发者，配置灵活性不足是明确的功能缺陷。


### 4. [Bug] Apps gateway 的 OTLP 遥测端点缺少认证头
**#82092** | 作者: k-brooks | 创建: 2026-07-28 | 评论: 13 | 👍: 5 | 状态: 开放
[链接](https://github.com/anthropics/claude-code/issues/82092)

> **摘要**：Apps gateway 向 Claude Desktop 提供 `otlpEndpoint` 指向自身带 bearer 认证的 OTLP 采集端点，但未配置对应的 `otlpHeaders`，导致 Desktop 每次遥测 flush 都被拒绝（`missing_token`）。

**关注价值**：影响可观测性数据采集的可靠性，对依赖遥测做监控和排障的团队是直接阻塞。


### 5. [Bug] Max 20x 升级后周限额未同步更新
**#79773** | 作者: Remy-authority | 创建: 2026-07-21 | 评论: 7 | 👍: 0 | 状态: 开放
[链接](https://github.com/anthropics/claude-code/issues/79773)

> **摘要**：2026 年 7 月 16 日升级至 Max 20x 后，周限额仍按 Max 5x 速率消耗，升级未在限额系统中生效。

**关注价值**：涉及用户付费权益的准确性问题，直接影响用户信任和留存，属于高优先级商业逻辑 Bug。


### 6. [Bug] 工作流驱动的代码审查 PR 评论静默失败
**#84474** | 作者: gsdali | 创建: 2026-08-06 | 评论: 3 | 👍: 0 | 状态: 开放
[链接](https://github.com/anthropics/claude-code/issues/84474)

> **摘要**：工作流驱动的代码审查中，"post review to the pr" 步骤大多数时候静默失败，却报告 `completed` 并附带完整 findings。环境：darwin、tmux、版本 2.1.223。

**关注价值**：静默失败比显式报错更具破坏性——用户误以为审查已提交，实际 PR 上没有评论。与 CI/CD 集成相关的可靠性问题。


### 7. [Bug] 安全过滤器误伤：开源无人机地面站开发被阻断
**#71920** | 作者: sworrl | 创建: 2026-06-27 | 评论: 5 | 👍: 0 | 状态: 已关闭（重复）
[链接](https://github.com/anthropics/claude-code/issues/71920)

> **摘要**：Claude Code 的网络安全安全过滤器在开发者进行合法开源无人机地面站开发时错误触发，直接中断会话（session-halted）。作者提供了 Request ID 供服务端复现，并论证了工作内容的合法性。

**关注价值**：该用户提交了十余个高度相似的误伤报告（#71916–#71992），指向安全过滤器在特定领域（无人机、逆向工程）存在系统性误判。对安全敏感型开发者有参考意义。


### 8. [Bug] 间歇性无理由权限拒绝（bypassPermissions 下仍出现）
**#71950** | 作者: Ckscrivner | 创建: 2026-06-28 | 评论: 3 | 👍: 1 | 状态: 已关闭
[链接](https://github.com/anthropics/claude-code/issues/71950)

> **摘要**：`Edit` 和 `Write` 工具调用间歇性被以无解释消息拒绝（"Permission to use Edit has been denied."），即使在 `bypassPermissions` 模式下也会出现。

**关注价值**：无理由且绕过权限模式仍触发的拒绝，指向可能的内部状态错误而非权限策略问题，对自动化工作流影响较大。


### 9. [Docs] 权限文档遗漏 `$HOME` 路径匹配规则
**#65502** | 作者: coygeek | 创建: 2026-06-04 | 评论: 4 | 👍: 0 | 状态: 已关闭
[链接](https://github.com/anthropics/claude-code/issues/65502)

> **摘要**：权限文档未说明 home 路径 `Read(...)` 拒绝规则在 Bash 中对 `$HOME` 路径的匹配行为，`~/path` 模式的实际匹配逻辑与文档不符。

**关注价值**：文档缺失直接导致用户配置错误和安全意外，对权限敏感的企业用户尤为重要。


### 10. [Bug] 登录路由错误：Max 订阅用户被锁在免费账号外
**#71262** | 作者: CH408 | 创建: 2026-06-25 | 评论: 5 | 👍: 0 | 状态: 已关闭
[链接](https://github.com/anthropics/claude-code/issues/71262)

> **摘要**：使用 charleshoward55@gmail.com 登录时被错误路由到另一个 Gmail 账号的免费版本，导致 Max 订阅用户无法使用已购权益。

**关注价值**：账号路由 Bug 直接造成付费用户权益损失，属于高影响、低概率但必须修复的认证类问题。


## 重要 PR 进展（Top 10）

### 1. [PR #86746] 修复安全引导脚本：保留 Python 探测错误信息
作者: aayush598 | 更新: 2026-08-14 | 状态: 开放
[链接](https://github.com/anthropics/claude-code/pull/86746)

> 修复 #86709：`sg-python.sh` 此前将探测 stderr 重定向到 `/dev/null`，当 `python3`/`python`/`py -3` 全部失败时用户只能看到通用错误。本 PR 保留探测错误以便诊断。


### 2. [PR #86626] 新增 bash/zsh/fish Shell 补全脚本
作者: 5hal1n | 更新: 2026-08-14 | 状态: 开放
[链接](https://github.com/anthropics/claude-code/pull/86626)

> 为 `claude` CLI 添加 `completions/` 目录：`claude.bash`（兼容 macOS 自带 bash 3.2）、`_claude`（zsh）、`claude.fish`（fish），附 README 安装说明。让补全与已安装 CLI 保持同步。


### 3. [PR #86537] 修复 CHANGELOG.md 重复单词
作者: genesisdayabl-droid | 更新: 2026-08-13 | 状态: 开放
[链接](https://github.com/anthropics/claude-code/pull/86537)

> 修复 1.0.124 版本 `CLAUDE_BASH_NO_LOGIN` 条目中 "to to" 的重复单词错误。文档级修改，无功能变更。


### 4. [PR #83890] 新增 pylint CI 工作流
作者: KrypticKode007 | 更新: 2026-08-14 | 状态: 开放
[链接](https://github.com/anthropics/claude-code/pull/83890)

> 添加 pylint.yml 用于代码质量检查。对 Python 相关脚本的静态分析有补充价值，但目前描述较简略。


### 5. [PR #41611] 补充 Claude Code 缺失的 source
作者: tornikeo | 更新: 2026-08-14 | 状态: 开放
[链接](https://github.com/anthropics/claude-code/pull/41611)

> "add missing source to claude code"——描述简短，推测是补充某处缺失的资源引用或配置项。已开放数月仍被更新，存在一定争议或维护者要求补充说明。


## 功能需求趋势

从过去 24 小时更新的全部 Issues 中，社区最关注的功能方向集中在以下五类：

1. **交互体验优化**（#2054、#65241）：Enter 键行为可配置、VS Code 扩展通知系统（limit reset、任务完成、会话事件）等，开发者要求更细粒度的 UI 控制。
2. **权限系统可观测性**（#65502、#71950、#70591）：权限拒绝原因透明化、多 Agent 工作流统一审批通知、文档完整化，企业用户对权限可控性要求提升。
3. **MCP 配置灵活性**（#16837）：超时、认证等参数需支持更大范围的自由配置，而非硬编码上限。
4. **多账号/订阅管理**（#71262、#79773）：账号路由准确性、订阅级别与限额同步，付费用户权益保障成为关注重点。
5. **安全过滤器精度**（#71920 系列）：安全策略误伤合法开发工作（无人机、逆向工程等）在短期内出现大量重复报告，社区对模型层安全过滤的"勿伤无辜"原则有强烈诉求。

## 开发者关注点

1. **Token 消耗透明度**：图片处理失败导致大量 token 无效消耗（#60334），用户要求更清晰的错误提示和可恢复机制。结合 5 小时窗口限制，成本敏感型用户希望系统能提前预警。
2. **静默失败的危害**：工作流 PR 评论静默失败（#84474）被认为是比显式报错更严重的问题——"报告成功但实际没做"，开发者呼吁所有异步操作必须有可验证的结果确认。
3. **安全过滤器误伤频率**：同一用户的十余个重复报告（#71916–#71992）指向安全过滤器在无人机/固件领域的系统性误判。虽然均已关闭，但用户反复提交说明问题未得到根本解决。建议维护者关注这类聚集性误报以优化模型策略。
4. **付费权益一致性**：Max 20x 限额不生效（#79773）与登录路由错误（#71262）表明账号/订阅系统的准确性和实时性需要加强。

---

*本日报由 AI 辅助整理，如需更详细数据请访问 [github.com/anthropics/claude-code](https://github.com/anthropics/claude-code)*

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex 社区动态日报

**日期：2026-08-15** | **数据来源：github.com/openai/codex**


## 今日速览

过去24小时内，Codex 仓库发布了 6 个 `rust-v0.148.0-alpha` 系列迭代版本，同时在主分支上合入了多项与 TUI 启动流程优化、Windows 统一执行（unified exec）默认启用相关的 PR。社区反馈方面，Windows 平台上应用性能问题（系统级鼠标卡顿、CPU 空转）成为最集中的投诉点，多条新提交的 Issue 直指最新版 `26.810.4967.0` 的严重回归，需要团队优先关注。


## 版本发布

过去24小时内发布了 6 个版本，均为 `rust-v0.148.0-alpha` 系列迭代（alpha.13 至 alpha.18）。目前公开 changelog 仅包含版本号信息，无详细更新说明。结合同日合入的 PR 推测，这些迭代可能涉及 TUI 启动流程优化、MCP 协议发现指标、Windows unified exec 默认启用等方向的持续改进。

- rust-v0.148.0-alpha.13 至 alpha.18：[Releases 页面](https://github.com/openai/codex/releases)


## 社区热点 Issues

下列 10 个 Issue 反映了当前社区最集中的痛点和关注方向：

### 1. Windows 平台性能回归——最高热度事件
**Codex App 在 Windows 11 Pro 上频繁卡死/卡顿（#20214）**
- 作者: squarepots | 评论: 100 | 👍: 84
- 该 Issue 已持续近 4 个月，积累了 100 条评论，是当前社区中反馈最集中、讨论最活跃的问题。用户报告在系统资源充足（Ryzen 5 5600 + 32GB RAM）的情况下，应用仍频繁出现卡死和卡顿，尽管有大量用户确认复现，但至今仍未解决。
- https://github.com/openai/codex/issues/20214

### 2. Windows 桌面端无界 taskkill/进程清理风暴（#34260）
- 作者: RocStone | 评论: 35 | 👍: 11
- 当 Codex Desktop 进入无界进程清理循环时，会产生数百个 `taskkill.exe` 及对应 `conhost.exe` 存活进程，持续查询 WMI 导致系统整体性能严重下降。这一问题暴露了 Windows 平台的进程管理存在深层缺陷。
- https://github.com/openai/codex/issues/34260

### 3. Windows 版缺少“控制其他设备”选项（#28919）
- 作者: zi070410 | 评论: 33 | 👍: 34
- Pro 用户在 Windows 版中找不到控制远程设备的选项卡，且 34 个 👍 表明大量用户对此功能有明确需求。该问题已开放近两个月，影响远程开发体验。
- https://github.com/openai/codex/issues/28919

### 4. 26.810.4967.0 更新导致整个 PC 卡顿（#38554）
- 作者: smlhd1993 | 评论: 6 | 👍: 3
- 用户明确指出版本从 26.803.10989.0 更新到 26.810.4967.0 后，整个系统开始出现持续卡顿，完全退出 Codex 后恢复。该 Issue 与 #38547、#38583、#38546 高度相关，共同构成“8月14日 Windows 性能大规模回归”的证据链。
- https://github.com/openai/codex/issues/38554

### 5. 长期存在的 Windows 输入延迟问题（#28855）
- 作者: Yassycodes | 评论: 16 | 👍: 20
- 用户报告 Codex Desktop 26.611.8604.0 在 Windows 上导致系统级输入延迟（鼠标移动和键入明显卡顿），即使禁用插件、日志干净也无法避免。结合后续多个类似报告，这是一个长期未解决的架构性问题。
- https://github.com/openai/codex/issues/28855

### 6. 空闲时主进程 CPU 忙循环（#38547）
- 作者: 123kkksss | 评论: 11 | 👍: 5
- 最新版 26.810.4967.0 在完全空闲时进入 Electron 主进程 CPU 忙循环。用户明确指出了回归起点（26.803.10989.0 → 26.810.4967.0），指向 Chrome 插件 app-server 哈希逻辑。此问题与 #38554、#38583 互相印证。
- https://github.com/openai/codex/issues/38547

### 7. Android 远程连接 Windows Codex 卡在 “Waiting for desktop…”（#22733）
- 作者: yanivavrahami | 评论: 16 | 👍: 19
- 移动端远程连接 Windows 桌面的会话长期卡在等待状态，在 Android 和 Windows 平台的交叉场景影响广泛，已开放 3 个月仍未被解决。
- https://github.com/openai/codex/issues/22733

### 8. Windows 沙箱无法启动 MSIX 版 PowerShell（#35871）
- 作者: dgx80 | 评论: 14 | 👍: 3
- 当沙箱解析 shell 为 Microsoft Store（MSIX）版 PowerShell 7 时，`CreateProcessAsUserW` 失败（Access denied）。Windows 拒绝在沙箱受限令牌下启动打包应用，功能受限。
- https://github.com/openai/codex/issues/35871

### 9. 上下文压缩导致操作连续性丢失（#29356）
- 作者: 1dZb1 | 评论: 21 | 👍: 1
- 用户要求 Codex Desktop 在自动上下文压缩（context compaction）时保留最后 5 个操作步骤的原文，当前实现会导致长任务中的操作连续性丢失。类似的压缩相关问题还有 #31375（85% 概率断开连接）。
- https://github.com/openai/codex/issues/29356

### 10. Codex IDE 侧边栏 Git 轮询引发严重句柄增长（#35775）
- 作者: tmesias | 评论: 3
- 在 Windows 上启用 VS Code 扩展后，会持续产生短生命周期 `git.exe` 和 `conhost.exe` 进程，导致 PID 4 Section-handle 严重堆积。该问题揭示了扩展在 Windows 上的资源管理存在显著缺陷。
- https://github.com/openai/codex/issues/35775


## 重要 PR 进展

以下 10 个 PR 反映了当前开发重点：

### 1. Windows 平台默认启用 unified exec（#38625）
- [CLOSED] 在所有平台默认启用稳定的 `unified_exec` 特性，Windows 上以 `exec_command` 和 `write_stdin` 替代 `shell_command`。这是 Windows 沙箱执行模型的一次重要统一。
- https://github.com/openai/codex/pull/38625

### 2. TUI 启动期保留可编辑输入框（#38642）
- [CLOSED] 在配置加载和 app-server 初始化期间显示临时输入框，允许用户提前起草提示词，启动完成后自动迁移文本和光标位置，显著改善启动等待体验。
- https://github.com/openai/codex/pull/38642

### 3. 跳过项目配置的覆盖开关（#38647）
- [CLOSED] 新增 `LoaderOverrides::ignore_project_config`，可绕过项目根目录发现和所有项目配置层，保留会话覆盖和云配置，对调试场景有价值。
- https://github.com/openai/codex/pull/38647

### 4. TUI 启动输入处理加固（#38641）
- [CLOSED] 防止终端探测等启动工作期间缓冲的按键误触发交互或确认操作，同时保证面向输入框的 typeahead 输入不丢失，提升启动期的输入稳定性。
- https://github.com/openai/codex/pull/38641

### 5. 移除 gRPC code-mode 打开会话数限制（#38630）
- [CLOSED] 允许 gRPC code-mode 主机注册超过 `MAX_IN_FLIGHT_REQUESTS` 的打开会话数，原有 in-flight 请求、控制请求和活动 cell 限制保持不变。
- https://github.com/openai/codex/pull/38630

### 6. 无链接时跳过终端超链接布局（#38657）
- [CLOSED] 当提供的行中不包含超链接元数据时，`mark_buffer_hyperlinks` 提前返回，避免不必要的段落布局计算，一个实用的终端渲染性能优化。
- https://github.com/openai/codex/pull/38657

### 7. MCP 命名空间描述在工具缓存中的保留（#38623）
- [CLOSED] 将 MCP 命名空间描述在发布到进程级工具目录缓存时保留，使模型在惰性 MCP 连接完成初始化之前即可获取服务器指令，改善冷启动体验。
- https://github.com/openai/codex/pull/38623

### 8. Apple 公证签发者 ID 从 Key Vault 读取（#38646）
- [CLOSED] 从公证密钥的 `apple-issuer-id` 标签加载 Apple issuer ID，要求 UUID 格式有效，移除独立的 `APPLE_NOTARIZATION_ISSUER_ID` 环境变量，提升 macOS 公证流程的安全性。
- https://github.com/openai/codex/pull/38646

### 9. Guardian v2 风险分类可配置化（#38628）
- [CLOSED] 允许 `features.guardianv2` 作为布尔开关或包含分类器指令、审查阈值、推理力度及 token 限制的配置对象，并增加记录源、按条目控制等转录选项。
- https://github.com/openai/codex/pull/38628

### 10. TUI 启动时账户响应复用（#38649）
- [CLOSED] TUI 启动时可复用首次登录状态检查的账户响应，避免 bootstrap 阶段重复读取账户信息，消除一次冗余请求。
- https://github.com/openai/codex/pull/38649


## 功能需求趋势

从过去 24 小时的 Issues 中，可以提炼出以下社区重点需求方向：

| 需求方向 | 代表性 Issue | 热度 |
|---------|-------------|------|
| **Windows 性能与稳定性** | #20214（100 评论/84👍）、#34260（35 评论）、#38554、#38547、#38583 | 最高 |
| **上下文管理与压缩策略** | #29356（保留最后操作步骤）、#31375（压缩导致断连） | 中高 |
| **远程连接与跨设备控制** | #28919（Windows 缺“控制其他设备”）、#22733（Android 连接卡住） | 中高 |
| **Sandbox 兼容性** | #35871（MSIX pwsh 无法启动）、#38636（Computer Use EPERM） | 中 |
| **执行环境灵活配置** | #36098（PowerShell/WSL 按项目选择） | 中 |
| **CLI 功能增强** | #37160（Bedrock Ultra reasoning）、#38585（/cd 命令） | 新出现 |
| **会话所有权与管理** | #38629（VS Code 多窗口会话转移）、#32610（Chrome 侧边栏选择项目） | 新出现 |
| **资源占用与文件增长** | #35823（logs_2.sqlite 无限增长）、#33796（~71 Mbps 上行尖峰） | 中 |


## 开发者关注点

### 1. 最紧迫：8 月 14 日 Windows 版本性能回归
#38547、#38554、#38583、#38546 四条 Issue 在同一天集中提交，全部指向 `26.810.4967.0` 版本在 Windows 上的严重性能问题。用户描述包括系统级鼠标卡顿、空闲时 CPU 忙循环（10%）、整体 PC 卡顿等。核心怀疑点指向 Chrome 插件 app-server 哈希逻辑。**多位用户要求 revert 该版本**，这是当前最需要紧急回应的问题集群。

### 2. 长期存在：Windows 平台系统性性能缺陷
从 #20214（已开放 4 个月、100 评论）到 #28855（已开放 2 个月），Windows 平台的应用卡顿和系统输入延迟问题贯穿多个版本，且用户在禁用插件、清理日志后仍无法解决。这不是单一版本的问题，而是更深层的架构性缺陷，涉及 Electron 主进程、进程管理和系统资源占用等环节。

### 3. 上下文压缩影响任务连续性
#29356 和 #31375 分别从“操作连续性丢失”和“压缩时 85% 概率断连”两个角度指出当前上下文压缩机制在长任务中的不可靠性。用户建议保留最后若干操作步骤原文而非全部压缩，或需要更加稳健的压缩路径。

### 4. 沙箱兼容性缺陷
#35871 和 #38636 揭示了沙箱在 Windows 上的两类兼容性问题：MSIX 打包应用无法在受限令牌下启动、Computer Use 插件因 EPERM 权限错误无法初始化。对于依赖沙箱隔离的 Windows 用户，这严重限制了功能性使用。

### 5. 资源管理问题持续累积
#35823（logs_2.sqlite 无限增长，auto_vacuum 设置为 INCREMENTAL 但从未执行）和 #35775（Git 轮询引发 PID 4 Section-handle 增长）表明磁盘和句柄资源管理在 Windows 平台上缺乏有效的回收与释放机制，长期间运行会导致系统健康度持续恶化。

---

*本日报由 AI 自动生成，数据截至 2026-08-15。*

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI 社区动态日报

**日期：2026-08-15** | **数据来源：github.com/google-gemini/gemini-cli**


## 今日速览

今日社区动态聚焦于**Subagent 恢复机制的正确性修复**——一个长期困扰开发者的"MAX_TURNS 被误报为成功"的问题已被 SSR Agent 提交修复 PR。此外，**多个 PTY/Shell 相关修复**（文件描述符泄漏、内存泄漏）同日关闭，值得终端重度用户关注。功能需求方面，**AST 感知代码读取**与**代理间调用**是当前社区最期待的能力。


## 版本发布

**v0.56.0-nightly.20260814.gc0d192452**

本 nightly 版本包含两项核心修复：
- **test(e2e)：** 稳定慢速运行环境下的 file-system-interactive 测试（PR #28793）
- **fix(core)：** 针对容量错误（capacity errors）实现上下文感知的静默重试与可用性 TTL 机制（PR #28761），旨在减少因临时容量不足导致的用户可见报错

该版本暂无公开的详细变更日志，建议关注后续正式版发布说明。


## 社区热点 Issues

精选过去 24 小时内讨论最活跃、影响面最大的 10 个 Issue：

**1. Subagent 达到 MAX_TURNS 后误报 GOAL 成功**（#22323 | P1 | 12 评论）
- **现象：** `codebase_investigator` 子代理在达到最大轮次限制后，`Termination Reason` 仍显示为 `"GOAL"` 且状态为 `success`，掩盖了实际中断，导致主代理误判任务已完成。
- **重要性：** 这是 Agent 可靠性的核心问题，直接影响多代理协作场景下的任务正确性。
- **社区反应：** 讨论热度高，已有对应修复 PR（#28815）在今日提交。
- 链接：https://github.com/google-gemini/gemini-cli/issues/22323

**2. Generalist agent 无限挂起**（#21409 | P1 | 8 评论 | 👍 8）
- **现象：** 只要 Gemini CLI 将任务委派给 generalist agent，就会永久挂起（用户等待长达 1 小时）。强制模型不使用子代理可规避。
- **重要性：** 严重阻断依赖 agent 自动化的用户，且 👍 数高说明受影响面广。
- 链接：https://github.com/google-gemini/gemini-cli/issues/21409

**3. 组件级行为评估体系建设**（#24353 | P1 | 7 评论 | EPIC）
- **内容：** 在已有 76 个行为评估测试基础上，计划构建更细粒度的组件级评估框架，覆盖 6 个受支持的 Gemini 模型。
- **重要性：** 评估体系的完善是 Agent 质量提升的基础设施，属于长期战略性投入。
- 链接：https://github.com/google-gemini/gemini-cli/issues/24353

**4. AST 感知文件读取与检索的可行性评估**（#22745 | P2 | 7 评论 | EPIC）
- **内容：** 探究 AST 感知工具是否能提升代码读取精度（如精确定位方法边界）、减少 token 噪声、优化代码库映射。
- **重要性：** 若落地，将显著改善大型代码库的上下文利用效率，是 agent 能力的潜在质变。
- 链接：https://github.com/google-gemini/gemini-cli/issues/22745

**5. Gemini 不会主动使用自定义 skills 和 sub-agents**（#21968 | P2 | 6 评论）
- **现象：** 用户反馈 Gemini 几乎不会自主调用已配置的自定义 skills 和 sub-agents，即使描述高度相关，必须显式指令才会使用。
- **重要性：** 直接影响扩展生态的价值兑现，是插件/技能体系能否被真正用起来的关键。
- 链接：https://github.com/google-gemini/gemini-cli/issues/21968

**6. Shell 命令执行完成后卡在 "Waiting input"**（#25166 | P1 | 4 评论 | 👍 3）
- **现象：** 极简的 CLI 命令（不会请求任何输入）执行完后，终端仍显示命令活动并等待用户输入，持续挂起。
- **重要性：** 高频阻塞性问题，影响日常交互流畅度。
- 链接：https://github.com/google-gemini/gemini-cli/issues/25166

**7. 工具数量超限导致 400 错误**（#24246 | P2 | 3 评论）
- **现象：** 当可用工具超过 128 个时（用户报告 400 个），CLI 返回 400 错误。
- **重要性：** 随 MCP 生态发展，工具数量膨胀是必然趋势，模型需要更智能地对工具做范围裁剪。
- 链接：https://github.com/google-gemini/gemini-cli/issues/24246

**8. 模型频繁在随机位置创建临时脚本**（#23571 | P2 | 3 评论）
- **现象：** 模型在排斥 shell 执行后，倾向于在多个目录生成临时编辑脚本，导致工作区清理成本高。
- **重要性：** 反映模型在"工具受限"时的行为退化，是 agent 行为质量的一个代表性长尾问题。
- 链接：https://github.com/google-gemini/gemini-cli/issues/23571

**9. 子代理无需权限即可运行**（#22093 | P2 | 3 评论）
- **现象：** 升级到 v0.33.0 后，用户在配置中已禁用 agents mode，子代理（如 generalist）仍被自动调用。
- **重要性：** 权限模型的回归问题，引发用户对 CLI 控制力的担忧。
- 链接：https://github.com/google-gemini/gemini-cli/issues/22093

**10. Auto Memory 对低信号会话无限重试**（#26522 | P2 | 5 评论）
- **内容：** Auto Memory 仅在提取代理成功读取 transcript 时才将会话标记为已处理，导致低信号会话反复出现、永不归档。
- **重要性：** 背景任务的效率与资源浪费问题，长期运行会积累大量无效扫描。
- 链接：https://github.com/google-gemini/gemini-cli/issues/26522


## 重要 PR 进展

以下 10 个 PR 值得关注（今日合入的 PR 均来自 SSR Agent 批量修复）：

**1. 修复 Subagent 恢复时终止原因被覆盖**（#28815 | 已合入 | size/s）
- **修复：** 子代理达到 MAX_TURNS 或 TIMEOUT 后，在最后一次宽限轮调用 `complete_task` 时，保留原始终止原因（如 MAX_TURNS），不再错误地覆盖为 GOAL。
- **意义：** 直接解决今日热点 Issue #22323。
- 链接：https://github.com/google-gemini/gemini-cli/pull/28815

**2. 修复 TUI 在 bare Linux 终端无限挂起**（#28812 | 已合入 | size/s | help wanted）
- **修复：** `getProcessInfo()` 依赖 `execAsync` 执行 `ps`，在裸 Linux 环境下会无限挂起。通过增加执行超时机制阻止"Initializing..."卡死。
- **意义：** 提升 CLI 在最小化 Linux 环境中的健壮性。
- 链接：https://github.com/google-gemini/gemini-cli/pull/28812

**3. 修复 MessageBus.request 静默挂起**（#28816 | 已合入 | size/s）
- **修复：** `publish()` 的 floating promise 失败未被捕获，导致请求静默挂起 60 秒。现在失败会立即 rejected 并传播。
- **意义：** 消除一个潜在的响应延迟问题，提升交互响应性。
- 链接：https://github.com/google-gemini/gemini-cli/pull/28816

**4. 保留子代理工具调用在 hook state 中**（#28817 | 已合入 | size/m）
- **修复：** 非根调度器（子代理）的 `Executing` 状态工具调用（如后台任务）不再被过滤丢弃，而是正确进入 hook state。
- **意义：** 保证 hook 机制的完整可见性，增强可观测性。
- 链接：https://github.com/google-gemini/gemini-cli/pull/28817

**5. 修复 PTY 文件描述符泄漏**（#20916 | 已合入 | P1 | size/m | help wanted）
- **修复：** PTY master 文件描述符在进程退出/kill 后未正确关闭，导致 macOS 上 `kern.tty.ptmx_max`（511）被耗尽。
- **意义：** 解决长会话用户可能遇到的系统级 PTY 耗尽问题。
- 链接：https://github.com/google-gemini/gemini-cli/pull/20916

**6. 修复 PTY 内存泄漏：同步删除 active 条目**（#27154 | 已合入 | P2 | size/m）
- **修复：** `activePtys.delete()` 被包裹在 `cleanupLogStream()` 的 Promise `.then()` 中，若后台日志流挂起则条目永不删除。改为同步删除。
- **意义：** 补充修复了 #20916 未覆盖的路径，两者合璧解决 ShellExecutionService 的泄漏问题。
- 链接：https://github.com/google-gemini/gemini-cli/pull/27154

**7. 允许 Agent 调用 Agent**（#28738 | 开放中 | P2 | size/l | help wanted）
- **内容：** 通过 `tools:` frontmatter 允许子代理委派给其他子代理，或递归调用自身（修复 #22092）。
- **意义：** 实现代理间的深度协作能力，是 Agent 生态走向复杂编排的关键一步。
- 链接：https://github.com/google-gemini/gemini-cli/pull/28738

**8. 加载环境变量后再解析 settings 占位符**（#28597 | 已合入 | P2 | size/l）
- **修复：** 原先 settings 文件在解析时立即展开 `process.env`，但 `.env` 文件尚未加载，导致占位符展开竞态。现在先加载环境变量再解析。
- **意义：** 修复了本地 `.env` 配置无法正确注入 settings 的问题。
- 链接：https://github.com/google-gemini/gemini-cli/pull/28597

**9. 新增 `--list-all-sessions` 选项**（#28596 | 已合入 | P3 | size/l）
- **功能：** 列出所有注册工作区下的聊天会话，按工作区路径分组展示。
- **意义：** 解决多项目用户的会话管理痛点（用户自述经常忘记会话在哪个目录创建）。
- 链接：https://github.com/google-gemini/gemini-cli/pull/28596

**10. 修复 Windows 上 ripgrep 的 EFTYPE 错误**（#25378 | 开放中 | size/m | help wanted）
- **修复：** 在 Windows 上 `grep_search` 因下载的二进制与宿主架构不匹配而报 `spawn EFTYPE` 错误，现增加架构检查。
- **意义：** 解决 Windows（特别是 ARM 设备）用户的搜索功能不可用问题。
- 链接：https://github.com/google-gemini/gemini-cli/pull/25378


## 功能需求趋势

从今日活跃的 Issues 和 PR 中提炼出以下社区核心关注方向：

**1. Agent 可靠性与正确性（热度最高）**
- 子代理终止原因的正确标记（#22323、PR #28815）
- Agent 挂起问题的系统性排查（#21409、#25166、PR #28812）
- 代理间调用与深度协作能力（PR #28738）

**2. AST 感知代码理解（战略级投入）**
- AST 感知的文件读取、搜索和代码库映射（#22745、#22746），官方已启动系列调研，推荐 tilth 和 glyph 作为起点。方向明确指向减少 token 噪声、提升大型代码库的上下文利用效率。

**3. 权限控制与安全边界**
- 子代理绕过权限配置的问题（#22093）和模型破坏性行为的抑制（#22672）表明，用户对 agent 自主性的边界有着强烈诉求。
- Auto Memory 的确定性脱敏（#26525）涉及数据安全，预计后续会有更多收紧。

**4. 终端体验与稳定性**
- 终端 resize 无闪烁（#21924）、外部编辑器退出后的界面损坏（#24935）、PTY 泄漏（#20916、#27154）等，说明终端这一核心交互界面的体验打磨仍是一个持续主题。

**5. 会话与上下文管理**
- Auto Memory 系列问题（#26516 及其子问题 #26522、#26523）聚焦记忆系统的准确性与效率，包括低信号会话的归档策略、无效 patch 的隔离等。社区希望记忆系统更聪明、更克制。


## 开发者关注点

**高频痛点：**

1. **"假成功"问题突出**——Subagent 实际失败却被标记为成功（#22323）是今日讨论最热烈的话题，开发者对 agent 可能"掩盖错误"的行为表达了明确担忧。同时"Generalist agent 挂起"（#21409）也被多次提及，这两个问题共同指向核心执行链路的可靠性仍是最大痛点。

2. **PTY/Shell 泄漏与卡死**——PTY 文件描述符耗尽（#15945 系列）和命令执行后假性等待（#25166）在多个 PR/Issue 中反复出现，说明终端子系统的稳定性直接关系到日常使用的信任度。

3. **模型不按配置行动**——无论是"不用已配置的 skills"（#21968）还是"禁用 agent 后仍自动调用"（#22093），开发者都在反复表达同一个诉求：**让模型严格遵循配置边界**。

**值得注意的信号：**

- 今日批量合入的 SSR Agent 修复（8 个）表明官方在系统性地清理积压问题，且修复质量较高（涉及根因修复而非表面补丁）。
- 大量修复标注 `help wanted`，社区贡献者参与的 PR（如 #20916 由外部开发者 stevenelliottjr 提交）被正式合入，说明外部贡献通道是畅通的，项目对社区 PR 持开放态度。
- 用户对"会话管理"（如 #28596 的 `--list-all-sessions`）和"可观测性"（如 #22598 的 subagent 轨迹共享）的功能请求正在增多，暗示 CLI 正从单次交互工具向长期工作伙伴的角色演进。

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI 社区动态日报

**日期：2026-08-15** | 数据来源：github.com/github/copilot-cli


## 今日速览

昨日发布 v1.0.80 补丁版本，但 Atlassian MCP OAuth 认证回归问题仍在持续发酵（#4480/#4490），成为社区最热议题。同时，模型可用性与策略配置相关 Issue（#4345/#4390/#4422）持续占据关注焦点，反映出企业用户在模型管理与策略一致性方面的痛点。此外，昨日新增了多个关于 `/spawn` 命令安全性（#4491）、OOM 崩溃（#4499）及插件依赖管理（#4487）等新议题。


## 版本发布

**v1.0.80（2026-08-14）**
- 更新模型配置（Update model configurations）
- 包含多项修复与变更（Fixes and changes）
- 链接：[Release v1.0.80](https://github.com/github/copilot-cli/releases)

**v1.0.80-1（2026-08-14）**
- 补丁版本，包含修复与变更
- 链接：[Release v1.0.80-1](https://github.com/github/copilot-cli/releases)


## 社区热点 Issues

### 1. Atlassian MCP OAuth 认证回归（高热度）
- **#4480** [CLOSED] [1.0.79 回归] Atlassian MCP OAuth 失败："Incompatible authorization server (RFC 8414 §3.3)"
  - 作者: jfrost-fabric | 评论: 4 | 👍: 6
  - 从 1.0.71 升级至 1.0.79 后，连接 Atlassian 远程 MCP 服务器时 OAuth 发现流程失败。**该 Issue 虽已关闭，但昨日又新增了 #4490，确认 1.0.80 中问题依然存在**（见下条）。
  - 链接: https://github.com/github/copilot-cli/issues/4480

- **#4490** [OPEN] Atlassian MCP OAuth 认证在 1.0.80 中被破坏（RFC 8414 §3.3 回归）
  - 作者: ChandrasekarCK | 评论: 0
  - v1.0.80 仍存在与 #4480 相同的问题（1.0.78 中正常），说明该回归未被 v1.0.80 修复；另有 [#4439](https://github.com/github/copilot-cli/issues/4439) 报告 GitLab MCP OAuth 也存在同根因问题。**MCP 生态兼容性是社区最关心的问题之一。**
  - 链接: https://github.com/github/copilot-cli/issues/4490

### 2. 模型配置与可用性（持续高热）
- **#4345** [OPEN] Reasoning effort 'medium' 不受模型 `claude-haiku-4.5` 支持
  - 作者: indeherb | 评论: 6 | 👍: 4
  - 当两个服务端 feature flags 同时激活时，子代理执行期间持续报错。涉及 `reasoning effort` 参数兼容性问题。
  - 链接: https://github.com/github/copilot-cli/issues/4345

- **#4390** [OPEN] 企业组织已启用的模型未出现在目录中（Claude Sonnet 5/Opus 5 和 Kimi K3）
  - 作者: Rogn | 评论: 6 | 👍: 4
  - Copilot Business 组织显式启用的模型在 CLI 中缺失，所有 Anthropic 模型不可用。指向模型目录同步机制缺陷。
  - 链接: https://github.com/github/copilot-cli/issues/4390

- **#4422** [OPEN] 企业账户下所有 Claude 模型被禁用
  - 作者: joelpou | 评论: 3 | 👍: 3
  - 个人企业账户在设置中显示模型已启用，但 CLI 中所有 Claude 系列模型不可用，回滚版本无效。与 #4390 高度相关。
  - 链接: https://github.com/github/copilot-cli/issues/4422

- **#4494** [OPEN] 新启用模型需清除本地缓存/登录后才能生效
  - 作者: obonn1 | 评论: 0
  - 新启用模型因本地模型目录未刷新而不可用，需手动重置缓存——进一步佐证模型目录同步缺陷。
  - 链接: https://github.com/github/copilot-cli/issues/4494

### 3. 代理执行稳定性
- **#4306** [OPEN] 子任务冻结且无响应
  - 作者: rcollette | 评论: 3 | 👍: 2
  - 在 autopilot 模式使用 `/fleet use speckit-automate implement skill` 时，子代理循环执行中途会话冻结，不再响应。
  - 链接: https://github.com/github/copilot-cli/issues/4306

### 4. MCP 分页支持缺失
- **#4006** [OPEN] [triaged] MCP `tools/list` 分页（nextCursor）未实现
  - 作者: ari-luokkala | 评论: 1
  - 未遵循 MCP 规范中的游标分页，仅加载第一页工具，后续页面被静默忽略。该问题已标记 triaged。
  - 链接: https://github.com/github/copilot-cli/issues/4006

### 5. 新增：/spawn 命令安全风险
- **#4491** [OPEN] `/spawn` 命令模板自相矛盾：可导致向不相关会话注入上下文
  - 作者: apcsb | 评论: 1
  - 模板先声明"创建子会话"，但实际可能退化为"向无关运行中会话注入上下文"，且缺少审批门控。存在跨会话写入风险。
  - 链接: https://github.com/github/copilot-cli/issues/4491

### 6. 新增：Windows 上 OOM 崩溃
- **#4499** [OPEN] v1.0.79 自动模式致命错误 "Committing semi space failed"（V8 堆仅使用约 0.6/4.3 GB）
  - 作者: AndreiTkachyov | 评论: 0
  - 宿主内存提交失败导致崩溃，非堆限制问题，长期运行的 autopilot 会话受影响。
  - 链接: https://github.com/github/copilot-cli/issues/4499

### 7. 新增：插件文件锁冲突
- **#4488** [OPEN] 多个 Copilot CLI/VS Code 会话打开时插件更新失败（Access denied）
  - 作者: grjsrinivas | 评论: 1
  - 无关会话持有的文件锁会阻止插件更新。
  - 链接: https://github.com/github/copilot-cli/issues/4488

### 8. 新增：/restart 在 -w 会话中失败
- **#4493** [OPEN] 使用 `-w`（worktree）创建的会话无法通过 `/restart` 恢复
  - 作者: mingley | 评论: 0
  - 重启时 worktree 选项与现有会话 ID 选项冲突。
  - 链接: https://github.com/github/copilot-cli/issues/4493


## 重要 PR 进展

### 1. GitHub Actions 中 fork PR 标签自动化
- **#4497** [OPEN] 在 invalid-label 写入器中处理 fork PR 关联
  - 作者: mrecachinas
  - 当 GitHub 未填充 PR 关联信息时，搜索受信任的 workflow-run 元数据并要求恰有一个开放的 PR 匹配。
  - 链接: https://github.com/github/copilot-cli/pull/4497

### 2. 拉取请求自动化迁移（已合并）
- **#4449** [CLOSED] 将 PR 自动化从 `pull_request_target` 迁移
  - 作者: mrecachinas
  - 使用 issue 级写权限 token 直接关闭无效 issue；对可合并 PR 使用无权限的 `pull_request` 信号；特权操作使用带 token 的工作流运行。
  - 链接: https://github.com/github/copilot-cli/pull/4449

### 3. 工作流迁移验证（已关闭）
- **#4496** [CLOSED] [canary] 验证 PR 工作流迁移
  - 作者: mrecachinas
  - 仅含文档的临时 PR，用于验证 fork 来源 PR 的自动化行为，确认后关闭。
  - 链接: https://github.com/github/copilot-cli/pull/4496


## 功能需求趋势

从近期 Issues 中可提炼出以下社区核心需求方向：

| 方向 | 代表 Issue | 说明 |
|------|-----------|------|
| **MCP 生态兼容性** | #4480/#4490/#4439/#4006/#4478 | OAuth 认证回归（RFC 8414）、分页支持缺失、服务器名冲突检测大小写敏感等问题集中爆发，说明 MCP 集成进入深水区 |
| **模型管理与目录同步** | #4390/#4422/#4494/#4345 | 企业策略启用与 CLI 实际模型目录不同步、reasoning effort 参数与模型不匹配——模型配置一致性成为企业用户核心痛点 |
| **插件系统完善** | #4487/#4488 | 插件间依赖解析与自动安装、多会话文件锁冲突——插件机制基础能力有待加强 |
| **会话稳定性与恢复** | #4306/#4477/#4493/#4489 | 子代理冻结、停止操作导致会话丢失、/restart 失败、恢复会话时 agent 未被选中——会话生命周期管理需优化 |
| **新模型支持** | #4495 | 社区已开始要求支持 GPT-5.6 的 reasoning.mode 参数（"standard"/"pro"） |


## 开发者关注点

### 高频痛点

1. **企业模型策略混乱**：组织启用模型后 CLI 中不可用、需要重置本地缓存才能生效、Claude 系列全部不可用——这类问题在 #4390、#4422、#4494 中反复出现，涉及企业账户的开发者在模型选择上正遭遇严重的体验倒退。

2. **MCP OAuth 回归持续发酵**：Atlassian MCP OAuth 在 v1.0.79 中回归、v1.0.80 未修复，GitLab 自托管 MCP 同样受困。更多第三方 MCP 服务采用 OAuth 认证的背景下，该问题影响面持续扩大。

3. **Windows 平台稳定性**：V8 堆未满却因宿主内存提交失败而崩溃（#4499），WebView2 渲染器自中止（#4492），Windows 用户仍面临稳定性短板。

4. **权限请求超时**：编辑权限请求不响应会超时，对同时管理多个会话的重度用户造成严重干扰（#4486）。

5. **允许目录配置失效**：`allowed_directories` 配置无法抑制路径越界提示，权限配置的可靠性存疑（#4482）。

6. **内容安全误判**：Debugging 场景被 CAPI 422 误判为网络安全风险（#4479），以及模型输出不当词汇（"Enslaved"，#4498），内容安全策略存在过度/误触发问题。

### 建议关注

- 若你使用 Atlassian/GitLab MCP，建议暂时锁定 v1.0.78，等待修复确认。
- 若遇到模型列表异常，可先尝试清除本地 Copilot 缓存/重新登录，但根本修复需等待上游模型目录同步机制的更新。
- 关注 `/spawn` 命令的安全修复进度（#4491），该问题可能影响自动化工作流的安全性。

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI 社区动态日报

**日期：2026年8月15日**


## 1. 今日速览

过去24小时内，Kimi Code CLI 仓库无新版本发布或合并的 PR，社区讨论热度主要集中在 **Memory 记忆系统（跨会话持久上下文）** 和 **多设备远程控制/会话接力** 两大功能诉求上。其中记忆系统相关 Issue 已获得 39 条评论，是该仓库目前讨论度最高的话题之一；此外，Windows 平台下 Shell 工具的 PowerShell 上下文感知问题获得官方修复（PR 已合并并关闭 Issue #1136），标志着 Windows 端体验优化进入收尾阶段。


## 2. 版本发布

过去 24 小时内无新版本发布。


## 3. 社区热点 Issues

以下为本期筛选出的 5 个值得关注的热点 Issue：

**#1283 — Memory System：跨会话持久上下文记忆系统**
- 作者：CatKang | 更新：08-14 | 评论：39 | 👍：0
- **核心诉求**：实现一套完整的记忆系统，包括 AI 自动管理的笔记和用户手动定义指令，以在会话间保留项目模式与用户偏好。
- **社区反应**：39 条评论显示了极高的关注度，是目前社区最受期待的功能之一。用户普遍反映大项目开发中频繁丢失上下文是核心痛点。
- 链接：[Issue #1283](https://github.com/MoonshotAI/kimi-cli/issues/1283)

**#2269 — 远程控制 / 多设备会话接力（新晋热点）**
- 作者：lucianalima777 | 更新：08-14 | 评论：6 | 👍：1
- **核心诉求**：支持在一台设备上启动 Kimi CLI 会话，并在另一台设备（笔记本、Web 或手机）上无缝继续或远程控制该会话。
- **社区反应**：虽然评论数尚少，但 5 月创建至今仍保持活跃更新，且 👍 数在近期新增 Issue 中领先，跨设备工作流需求清晰可见。
- 链接：[Issue #2269](https://github.com/MoonshotAI/kimi-cli/issues/2269)

**#1478 — 记忆层优化诉求（与 #1283 形成共鸣）**
- 作者：hahy36 | 更新：08-14 | 评论：2 | 👍：0
- **核心诉求**：用户反馈在大型项目中因缺少记忆层而"很痛苦"，并指出参考文档中仅提及 `agent.md`，未找到记忆系统相关资料。贴出了 `.openclaw/workspace/` 目录结构（含 `SOUL.md`、`USER.md`、`MEMORY.md` 等）作为参考。
- **社区反应**：评论数不多，但揭示了文档缺失与功能诉求之间的落差，开发者对记忆系统的实施细节存在信息缺口。
- 链接：[Issue #1478](https://github.com/MoonshotAI/kimi-cli/issues/1478)

**#1136 — Shell 工具 PowerShell 上下文感知增强（CLOSED）**
- 作者：QIN2DIM | 更新：08-14 | 评论：0 | 👍：0
- **核心诉求**：针对 Kimi K2.5 (SGLang) 在 Windows 上首次命令生成时发现的三个关键问题（如 Shebang 歧义等），要求 Shell 工具增强 PowerShell 版本感知能力。
- **社区反应**：该 Issue 已于本期关闭，对应 PR 已合并，标志着 Windows 用户体验的一次实质性修复落地。
- 链接：[Issue #1136](https://github.com/MoonshotAI/kimi-cli/issues/1136)

**补充说明**：过去 24 小时内更新共 4 条（含以上），数据源中其余 Issue 均为历史归档。个别近期 Issue 活跃度与评论数在统计时仍处于累积阶段，建议持续跟踪排序变动。


## 4. 重要 PR 进展

过去 24 小时内无合并或更新的 Pull Requests。可确认的是，此前提交的 **Shell 工具 PowerShell 上下文感知增强** 相关 PR 已合入主干（对应 Issue #1136 随之关闭），这是本期唯一确认进入主干的功能改动。


## 5. 功能需求趋势

综合历史活跃 Issue 与本期数据，社区功能诉求集中在以下方向：

- **记忆系统（Memory System）**：最高呼声。要求跨会话保留项目上下文、用户偏好与 AI 笔记（#1283、#1478）。部分用户对照 `.openclaw/workspace/` 目录结构提出实现参考，说明对显式的三层记忆（人格、用户信息、长期/每日记忆）有一定期待。
- **多设备协同 / 远程控制**：从单设备延伸到跨设备会话接力与远程控制，显示用户对"随时随地进行开发"的强烈需求（#2269）。
- **Windows 平台体验优化**：对 Shell 工具在 PowerShell 下的兼容性持续关注，本期已有一项修复落地（#1136），预计后续仍会有 Windows 相关反馈。
- **文档完善**：用户对记忆系统等功能的官方文档缺失有明显困扰，多人在 Issue 中反映"找不到关于记忆的参考材料"——文档与功能开发需同步推进。

> 注：数据源中提及 IDE 集成、新模型支持等方向的标题未出现在本期更新列表中，暂不纳入结论。


## 6. 开发者关注点

- **大型项目上下文丢失是最普遍的痛点**：无论是 #1283 还是 #1478，开发者反复强调在复杂项目中频繁丢失上下文导致效率下降，希望记忆层成为内置能力（而非依赖 `agent.md` 等临时方案）。
- **跨设备工作流需求上升**：从"能否远程控制"的提问中可以看出，用户不满足于单机终端使用场景，对 Web/移动端接入抱有较高期待。
- **Windows 下命令生成的精确性问题值得重视**：虽然 #1136 已关闭，但其揭示了 Windows 环境下 Shell 工具在 pass-1 阶段可能生成不兼容命令的问题。建议使用 Windows 的开发者更新到最新版本以获取修复，并后续留意是否还有残余兼容性问题。
- **对功能透明度要求提高**：用户不希望功能"存在但找不到说明"，呼吁同步完善文档。

---

以上就是本期 Kimi Code CLI 社区日报全部内容。核心看点一句话总结：**社区正在集体呼唤"记忆"能力，而 Windows 平台体验正在逐步补齐**。欢迎持续关注仓库动态。

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode 社区动态日报 — 2026-08-14

> 技术分析师精选，基于 GitHub 公开数据（anomalyco/opencode）

---

## 今日速览

今日社区最重大的事件是 **48 位 ID 时间戳回绕 Bug（#42608）导致所有旧会话在 12:39:55 UTC 后静默失效**，影响面广且与多个"会话无响应"报告（#42605、#42611 等）高度关联。此外，**OpenCode Go 中继服务出现多项模型兼容性问题**（GLM、Kimi、DeepSeek 系列），以及一个 **PR #42660 动态模型发现功能** 获得高度关注，有望一劳永逸解决自定义 OpenAI 兼容提供方的配置痛点。

---

## 社区热点 Issues（Top 10）

### 1. #42608 — 48-bit ID 时间戳回绕导致所有旧会话失效
`[严重/紧急]` 作者: klly14 | 👍 3 | 💬 5
**描述**：2026-08-14 12:39:55 UTC 起，所有此前创建的会话静默停止处理新提示，根因是 `packages/opencode/src/id/id.ts` 中 48 位时间戳发生回绕。该问题覆盖范围极大（所有旧会话），并被标记为 #42605 等"会话无响应"报告的根因。
🔗 [查看 Issue](https://github.com/anomalyco/opencode/issues/42608)

### 2. #42605 — 会话保持打开但 agent 不处理后续提示
作者: ekatake-125 | 👍 0 | 💬 4
**描述**：OpenCode Desktop 在 agent 完成一次任务并向用户提问后，发送新消息无任何响应，会话看似正常但实际已卡死。与 #42608 时间高度吻合，疑似同源。
🔗 [查看 Issue](https://github.com/anomalyco/opencode/issues/42605)

### 3. #20695 — Memory Megathread（内存问题专帖）
`[长期置顶]` 作者: thdxr | 👍 98 | 💬 131
**描述**：社区内存问题集中讨论帖，作者明确提醒"不要用 LLM 建议解决方案"，呼吁用户提交堆快照以协助定位。已持续 4 个月，仍是社区最活跃的帖子之一。
🔗 [查看 Issue](https://github.com/anomalyco/opencode/issues/20695)

### 4. #8751 — [功能请求] 热重载 agents、skills 和 commands
作者: IgorWarzocha | 👍 91 | 💬 19
**描述**：允许 OpenCode 运行期间使配置失效并重新加载，用户无需重启即可创建/修改 agent 配置。获得 91 个赞，是长期最受欢迎的功能请求之一。
🔗 [查看 Issue](https://github.com/anomalyco/opencode/issues/8751)

### 5. #42616 — Zen Go Anthropic 端点：所有 GLM 模型的 tools 请求失败
作者: goldyard2022 | 👍 0 | 💬 2
**描述**：向 `https://opencode.ai/zen/go/v1/messages` 发送带非空 `tools` 数组的请求时，glm-5.3/5.2/5.1 全部返回 422 翻译错误；同请求去掉 tools 或换用其他模型（kimi 等）则正常。指向 OpenCode Go 网关侧的工具翻译缺陷。
🔗 [查看 Issue](https://github.com/anomalyco/opencode/issues/42616)

### 6. #25000 — DeepSeek V4 Pro (zen/go) 多轮工具调用中 `reasoning_content` 不一致导致报错
作者: WhiteGiverMa | 👍 0 | 💬 7
**描述**：经 `opencode.ai/zen/go/v1` 使用 DeepSeek V4 Pro 时，多轮工具调用会间歇性报错 `reasoning_content in the thinking mode must be passed back to the API`。已定位为 DeepSeek V4 Pro 的思考内容在多次请求间不一致所致。
🔗 [查看 Issue](https://github.com/anomalyco/opencode/issues/25000)

### 7. #25000 关联：#42385 — DeepSeek V4 Flash Free 返回 FreeUsageLimitError
作者: Anshukumarrr | 👍 0 | 💬 3
**描述**：`deepseek-v4-flash-free` 模型经 OpenCode Zen OpenAI 兼容接口调用时被稳定拒绝，提示 `FreeUsageLimitError`，但认证本身成功。疑似配额判定逻辑异常。
🔗 [查看 Issue](https://github.com/anomalyco/opencode/issues/42385)

### 8. #41518 — gpt-5.6-luna 经 OpenCode Go 中继返回 403 "not available in your region"
作者: 123lyc5 | 👍 0 | 💬 4
**描述**：通过 `opencode.ai` 的 "OpenCode Go" 中继访问 `gpt-5.6-luna` 时返回 403，报 "This model is not available in your region"。用户经 CC Switch 本地代理转发，怀疑中继服务区域限制逻辑有误（IP 判定为亚洲区域）。
🔗 [查看 Issue](https://github.com/anomalyco/opencode/issues/41518)

### 9. #38791 — 运行循环永不退出：消息 ID 不可按时间排序时（导入会话）会循环至 provider 400
作者: dkindlund | 👍 0 | 💬 6
**描述**：`SessionPrompt.runLoop` 以纯字符串比较消息 ID 来决定轮次结束，仅对 OpenCode 自带的时间戳型 ID 有效。任何第三方导入的会话（ID 不按时间排序）都会使循环陷入死循环，直至 provider 返回 400。此 Bug 与导入功能、多提供方兼容密切相关。
🔗 [查看 Issue](https://github.com/anomalyco/opencode/issues/38791)

### 10. #42657 — 多子代理会话下 TUI 严重卡顿（渲染线程占 97% CPU）
作者: BenjaMolina | 👍 0 | 💬 2
**描述**：2-4 个并发子代理运行时，TUI 输入延迟 1-3 秒、动画卡顿。在 Warp / Windows Terminal / WezTerm 下均复现，profiling 显示渲染线程 CPU 占用 97%。与 #37489（本地 LLM 下上下文缓存失效的性能问题）共同指向 2.0 版本的性能回归风险。
🔗 [查看 Issue](https://github.com/anomalyco/opencode/issues/42657)

> 补充关注：#42635（TUI 系统主题在 herdr 下不刷新配色）、#42613（OpenAI Responses 格式不兼容严格实现的服务端）。

---

## 重要 PR 进展（Top 10）

### 1. #42660 — 为自定义提供方添加动态模型发现（OPEN）
`[新功能]` 作者: Gr33ndev | 🆕 新增
**描述**：允许 OpenAI 兼容的自定义提供方（如 LiteLLM、LM Studio 等）通过 `/v1/models` 自动发现模型列表，免去在 `opencode.json` 中手动枚举的繁琐。一举关闭 #13891、#29308、#28999、#25624、#23327、#26863 共 6 个 issue。呼应社区 #27553 功能请求。
🔗 [查看 PR](https://github.com/anomalyco/opencode/pull/42660)

### 2. #42656 — 重构协议：将 worktree 路由移出 experimental 命名空间（已合并）
`[重构]` 作者: jlongster
**描述**：`/api/experimental/project/:projectID/worktree` 规整为顶层 `/api/worktree/:projectID`，属于 API 接口标准化步骤。
🔗 [查看 PR](https://github.com/anomalyco/opencode/pull/42656)

### 3. #36943 — 保持被中断的会话处于停止状态（已合并）
`[Bug 修复]` 作者: opencode-agent[bot]
**描述**：修复 V2 运行协调器——被中断的会话不应因迟到 wake 或重试继续执行，仅放行在中断之后产生的全新提示。解决旧会话"假死/复活"问题。
🔗 [查看 PR](https://github.com/anomalyco/opencode/pull/36943)

### 4. #36916 — 排队并发子代理的提问（已合并）
作者: lucas-gaitzsch
**描述**：当多个子代理同时提问时，按请求 ID 排序并保持当前活动请求选中，避免提问混乱。
🔗 [查看 PR](https://github.com/anomalyco/opencode/pull/36916)

### 5. #36906 — 首页快捷键保持右对齐（已合并）
作者: opencode-agent[bot]
**描述**：修复空会话目录导致首页底部 footer 变化后，快捷键组左移的问题。
🔗 [查看 PR](https://github.com/anomalyco/opencode/pull/36906)

### 6. #36898 — CLI 处理子孙级权限询问（已合并）
作者: eummo | Closes #36868
**描述**：`opencode run` 头less模式原先只响应根会话的权限请求，Task 子代理请求权限时会阻塞。此修复使所有层级的权限询问都能被正确处理。
🔗 [查看 PR](https://github.com/anomalyco/opencode/pull/36898)

### 7. #36869 — 为工具添加独立执行超时 + 中止 + 会话恢复（已合并）
`[新功能]` 作者: FahadBinHussain
**描述**：为内置工具和 MCP 工具增加执行超时控制，防止单个工具卡死拖垮整个 agent 循环，支持中断与会话恢复。关联 #20096、#34888、#20216、#34022、#34960 等多个"工具卡死"issue。
🔗 [查看 PR](https://github.com/anomalyco/opencode/pull/36869)

### 8. #36883 — 在子代理工具中向模型暴露有效的子代理 ID（已合并）
作者: Robin1987China | Closes #36761
**描述**：`subagent` 工具的 `agent` 字段此前仅描述"要运行的 agent"，未列出合法 ID，导致模型会猜出错误名称（如 `explorer` 而非 `explore`）。现在在工具 schema 中直接枚举可用的子代理 ID。
🔗 [查看 PR](https://github.com/anomalyco/opencode/pull/36883)

### 9. #36862 — 校验 desktop 的 openExternal URL 协议（已合并）
`[安全修复]` 作者: ulises-jeremias | Closes #30613
**描述**：`shell.openExternal` 原本接受任意 URL，存在 `file://`、`javascript:` 等危险协议被滥用的风险。此修复按协议白名单校验。
🔗 [查看 PR](https://github.com/anomalyco/opencode/pull/36862)

### 10. #36851 — 数据库启用 auto-vacuum 并添加定期维护（已合并）
作者: BYK | Closes #31526
**描述**：针对 SQLite 数据库持续增大导致性能下降的问题，启用自动 VACUUM 和定期维护任务。此 PR 由 #31528 重新提交（原 PR 被清理机器人误关）。
🔗 [查看 PR](https://github.com/anomalyco/opencode/pull/36851)

> 其他值得关注：#36870（文档化 provider 包加载）、#36861（从 OpenAI-compatible metadata 恢复缓存 token）、#36860（剥离 MiniMax 尾部 tool_call 泄漏）、#36880（V2 压缩模型标记回归修复）。

---

## 功能需求趋势

| 趋势方向 | 代表 Issue / PR | 热度信号 |
|---|---|---|
| **模型/提供方接入自动化** | #27553（自动发现 OpenAI 兼容模型）、PR #42660（动态模型发现） | 跨 6 个 issue 的长期诉求，PR 落地响应 |
| **配置热更新（无需重启）** | #8751（热重载 agents/skills/commands） | 91 👍，高赞功能请求 |
| **工具执行可靠性** | PR #36869（per-tool 超时+中止）、#38791（运行循环死循环） | 工具卡死/循环是高频痛点 |
| **会话稳定性与恢复** | #42608（ID 回绕）、#36943（中断会话保持停止）、#36861（缓存 token 恢复） | 2.0 版本会话可靠性成核心关注 |
| **TUI 性能与体验** | #42657（多子代理 TUI 卡顿）、#42635（主题刷新）、#36906/#36897（布局细节） | 多起 TUI 渲染性能/细节问题集中上报 |
| **网关/中继兼容性** | #25000、#42385、#42616、#41120、#41518（DeepSeek/GLM/Kimi/gpt-5.6 经 Go 中继的各类错误） | OpenCode Go 中继的模型适配仍是短板 |
| **DB 维护与性能** | PR #36851（auto-vacuum）、#37489（上下文缓存失效） | 长期运行性能劣化逐渐显现 |

---

## 开发者关注点（痛点 / 高频反馈）

1. **会话静默失效（今日最严重）**：ID 时间戳回绕（#42608）导致旧会话无法继续、新消息被忽略，且与 #42605 / #42611 / #42594 等多条报告高度重合。社区开发者对"无声失败"的反馈强烈——建议后续在 ID 生成器中加入回绕检测与迁移方案。

2. **OpenCode Go 中继的模型兼容性参差**：DeepSeek（#25000 思考内容不一致、#42385 免费额度误判）、GLM（#42616 tools 数组 422）、Kimi（#41120 函数名非法）、gpt-5.6-luna（#41518 区域 403）——中继层对各家模型特性的适配仍不稳定，尤其 Anthropic 兼容端点对工具调用的转换存在系统性缺陷。

3. **TUI 在多子代理场景明显退化**：渲染线程 97% CPU（#42657）并非个例，连同 #37489（上下文切换性能）指向 V2 架构在并发场景下的性能回归，需要尽快优化渲染管线与响应式更新频率。

4. **"付费了但用不了"类反馈增多**：#42637 / #42606 均为用户购买额度后无法在 desktop 使用；#42215 免费额度超 24 小时未重置。计费/配额系统的状态同步需排查，尤其在免费模型与订阅并存时。

5. **自动 PR 清理机器人造成误关**：多个 PR（#31517→#36853、#31528→#36851）因年龄被机器人误关，虽已重提，但暴露了自动化维护策略的副作用——建议提高清理阈值或增加人工复审环节。

---

*本日报由 AI 技术分析师整理，基于 GitHub 公开数据（截至 2026-08-14），不构成官方立场。*

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

# Pi 社区动态日报 — 2026-08-15

> 数据来源: github.com/badlogic/pi-mono

## 今日速览

今日发布 v0.84.2 版本，带来全屏转录搜索与可配置默认工具两项新特性。社区层面，Windows 平台使用体验讨论持续升温（#7547 已达 27 条评论），同时 TUI 在流式输出时单核占满的性能问题受到广泛关注。此外，Kimi 缓存 token 统计、代理环境下的 HTTP 提供商挂起等问题也进入了修复流程。

---

## 版本发布

### v0.84.2

**新特性**
- **全屏转录搜索** — 支持在全屏模式下搜索和浏览匹配项。参见 [TUI Fullscreen Viewport](https://github.com/earendil-works/pi/blob/v0.84.2/packages/coding-agent/docs/keybindings.md#tui-fullscreen-viewport)
- **可配置默认工具** — 允许自定义启动时加载的默认工具集

链接: [v0.84.2 Release](https://github.com/badlogic/pi-mono/releases/tag/v0.84.2)

---

## 社区热点 Issues（Top 10）

### 1. [OPEN] [Windows] [sink-thread] 你在 Windows 上如何使用 Pi？遇到了哪些问题？
- [#7547](https://github.com/earendil-works/pi/issues/7547) | 评论: 27 | 👍: 1
- Windows 上 Pi 的运行方式过于多样，维护者希望收集真实使用场景以确定优化优先级。社区讨论热度最高，反映 Windows 平台支持是当前关注焦点。

### 2. [CLOSED] [bug] WSL 中 GitHub Copilot 设备授权后 Pi 登录挂起
- [#6187](https://github.com/earendil-works/pi/issues/6187) | 评论: 26
- Pi 在 WSL 下完成浏览器授权后无法检测到授权状态，卡在登录等待。WSL 场景是 Windows 用户的主要入口，该问题关注度高。

### 3. [CLOSED] Anthropic provider 修改 thinking blocks 导致 Opus 4.8 返回 400 错误
- [#5223](https://github.com/earendil-works/pi/issues/5223) | 评论: 17 | 👍: 6
- 多轮对话中 Claude Opus 4.8（adaptive thinking）中途失败，报错指向 `thinking`/`redacted_thinking` 块异常。自适应思考场景下的稳定性问题。

### 4. [CLOSED] [bug] 终端无故滚动到开头
- [#5023](https://github.com/earendil-works/pi/issues/5023) | 评论: 12 | 👍: 2
- 模型工作输出时，终端随机跳转到会话开头并快速滚回底部，且复现频繁、无用户交互触发。随机性问题排查成本高，影响日常使用体验。

### 5. [OPEN] [inprogress] TUI 流式输出时单核占满：`Intl.Segmenter` 未缓存 + 逐块重建 Markdown
- [#6665](https://github.com/earendil-works/pi/issues/6665) | 评论: 12 | 👍: 3
- 长会话流式输出时 TUI 单核占用约 100%。已定位到两个主因：字素分割未缓存、逐块执行 Markdown 渲染。长会话卡顿的根因，已在修复中。

### 6. [CLOSED] [bug] GitHub Copilot 登录在模型较多的组织中触发 429 限流
- [#7850](https://github.com/earendil-works/pi/issues/7850) | 评论: 9 | 👍: 7
- 使用拥有 20+ 可用模型的组织时，设备授权成功后 Copilot 登录返回 429。企业用户受影响，热度上升中。

### 7. [CLOSED] Z.AI Coding Plan 默认值引用了已移除的模型
- [#8096](https://github.com/earendil-works/pi/issues/8096) | 评论: 5 | 👍: 1
- `defaultModelPerProvider` 仍为 `zai` 选择 `glm-5.1`，但 models.dev 生成的目录中已无此模型。提供商标识与实际目录不一致的问题。

### 8. [CLOSED] [no-action] pnpm 安装扩展时依赖解析失败（jiti + 隔离 node_modules）
- [#8092](https://github.com/earendil-works/pi/issues/8092) | 评论: 5
- pnpm 隔离布局下 symlink 导致 jiti 解析扩展依赖失败。影响 pnpm 用户的扩展安装与使用，已有对应 PR 提出修复。

### 9. [CLOSED] [bug] Copilot 账号登录持续返回 429
- [#8010](https://github.com/earendil-works/pi/issues/8010) | 评论: 4 | 👍: 2
- 企业新模型启用后，用户登出再登入以刷新模型列表，结果反复遇到 429 限流。与 #7850 同源，说明该问题影响面较广。

### 10. [OPEN] [bug] edit 工具渲染大 diff 导致 TUI 崩溃
- [#8036](https://github.com/earendil-works/pi/issues/8036) | 评论: 2
- 编辑 HTML 文件产生的约 14.5 MB diff 导致交互式 TUI 崩溃，且会话恢复时同样触发。极端但真实的大文件场景，值得关注。

---

## 重要 PR 进展（Top 10）

### 1. [OPEN] 实验性 append 压缩模式
- [#8120](https://github.com/earendil-works/pi/pull/8120)
- 启用 `PI_EXPERIMENTAL=1` 时使用 append 压缩，复用活动系统提示与 provider 缓存，降低压缩成本。独立模式仍为默认。

### 2. [OPEN] 修复 Kimi cached tokens 统计
- [#8119](https://github.com/earendil-works/pi/pull/8119)
- 将 Kimi 的顶层 `usage.cached_tokens` 计入缓存读取输入 token（对应 #8075），修正用量统计。

### 3. [OPEN] xAI 模型切换至 Responses API 并默认 Grok 4.6
- [#8124](https://github.com/earendil-works/pi/pull/8124)
- xAI 默认走 Responses API 而非 Completions，默认模型从 Grok 4.5 升级至 Grok 4.6。

### 4. [CLOSED] 全屏转录性能优化
- [#8143](https://github.com/earendil-works/pi/pull/8143)
- 全屏会话保留完整人类转录历史（含压缩前的），仅渲染视口相交块。配合 v0.84.2 的全屏搜索功能。

### 5. [OPEN] jiti 导入前对扩展条目执行 realpath
- [#8112](https://github.com/earendil-works/pi/pull/8112)
- 修复 #8092：pnpm 隔离布局下 jiti 无法解析扩展依赖。对 pnpm 用户属刚需修复。

### 6. [CLOSED] 修复 TUI 复制提示与剪贴板不一致问题
- [#8110](https://github.com/earendil-works/pi/pull/8110)
- `copySelectionToClipboard()` 仅写 OSC 52 序列并闪 "Copied!"，但部分终端不支持导致剪贴板为空。现改为通过宿主剪贴板复制，使提示真实有效。

### 7. [OPEN] 添加 Anthropic Vertex provider
- [#5262](https://github.com/earendil-works/pi/pull/5262)
- 内置 `anthropic-vertex` provider，支持 Google Cloud Vertex AI 上的 Claude。未合入但持续活跃。

### 8. [CLOSED] 新增 SiliconFlow provider
- [#8113](https://github.com/earendil-works/pi/pull/8113)
- 按 moonshot/minimax 模式新增内置 SiliconFlow provider，端点 `https://api.siliconflow.com/v1`，使用 `SILICONFLOW_API_KEY` 环境变量。

### 9. [CLOSED] 新增 ChatGPT OAuth 图像生成
- [#8139](https://github.com/earendil-works/pi/pull/8139)
- 为 `pi-ai` 添加原生 ChatGPT 图像生成传输层，复用现有 Codex OAuth 与 Responses 基础设施，无需 OpenAI API key。

### 10. [CLOSED] 检测 `api.kimi.com` 为 Moonshot 端点
- [#8109](https://github.com/earendil-works/pi/pull/8109)
- 修复指向 Kimi Coding 的 OpenAI 兼容提供商报 `role 'developer' is not allowed` 错误——`detectCompat` 仅识别 `api.moonshot.*`。

---

## 功能需求趋势

| 方向 | 代表 Issue/PR | 热度判断 |
|---|---|---|
| **新模型/提供商支持** | SiliconFlow（#8113）、Anthropic Vertex（#5262）、Amazon Bedrock Mantle（#6216）、xAI Grok 4.6（#8124）、ChatGPT 图像生成（#8139） | 持续主流，xAI 与国产厂商接入活跃 |
| **Windows/WSL 体验** | #7547、#6187 | 话题度最高，官方已主动征集反馈 |
| **性能优化** | TUI 全屏渲染（#8143）、append 压缩（#8120）、Intl.Segmenter 缓存（#6665） | 渲染与压缩是当前两大热点 |
| **用量统计准确性** | Kimi cached_tokens（#8119）、OpenAI-completions usage 解析（#8075） | 需求明确且具体，涉及多云成本核算 |
| **脚本化/CI 集成** | CLI args/env 直连（#8114） | 呼声初现，面向管道场景的一等公民支持 |

---

## 开发者关注点

- **Windows 支持模糊** — #7547 汇集 Windows 用户反馈，运行方式多样（原生/WSL/Git Bash 等）导致维护方难以聚焦。bash 工具在 Windows 上查找逻辑也需改进（#8108）。
- **429 限流困扰企业用户** — #7850 与 #8010 同源，组织中模型数量较多时 Copilot 登录频遭限流，影响企业体验。
- **TUI 在高负载下不稳定** — 流式输出 CPU 占满（#6665）、大 diff 渲染崩溃（#8036）、剪贴板无法直写（#7761），此类问题日常使用感知最强。
- **代理环境下的提供商兼容** — #8134 指出 HTTP 提供商经正向代理时在首次工具调用后挂起（0.84.0 引入），影响企业内部网络场景。
- **压缩行为与重放一致性** — #7724 报告冷恢复会重放已被实时恢复移除的溢出助手消息，破坏会话一致性。
- **扩展机制细节问题** — pnpm 依赖解析失败（#8092）、`registerFlag` 布尔默认值类型错误（#8123）、`streamSimple` 忽略 thinkingLevelMap（#8135）等，说明扩展 API 仍处于打磨期。
- **量化场景的 token 统计** — Kimi（#8075）、OpenAI 推理-only 响应处理（#8115）等精细化需求，反映开发者对成本追踪的要求在提高。

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code 社区动态日报

**日期：2026-08-15** | 数据来源：github.com/QwenLM/qwen-code


## 今日速览

昨日 Qwen Code 发布了 v0.21.12 及多个预览版，重点修复 Web Shell 会话保持问题并新增工作区文件拖拽上传功能。社区围绕 `qwen serve` 守护进程资源边界、CLI 架构重构和 CI 可靠性展开了激烈讨论；同时安全类 Issue（命令注入绕过、autofix PAT 隔离）仍在持续发酵。值得关注的是，社区开始出现 Electron 桌面宿主和 HTML 导出重构等新的功能提案，显示 Web Shell 生态正在加速演进。


## 版本发布

### v0.21.12（正式版）
- **新增**：Web Shell 编辑器支持通过拖拽或 @ 文件面板上传工作区文件，并带有进度跟踪（[#8874](https://github.com/QwenLM/qwen-code/pull/8874)）
- **优化**：autofix 审查中引入 diff 增长制动机制，限制单次审查的 diff 膨胀

### v0.21.12-preview.3 / preview.4
- `fix(web-shell)`: 修复独立会话目标丢失问题（[#9038](https://github.com/QwenLM/qwen-code/pull/9038)）
- `feat(web-shell)`: 支持工作区文件上传

### v0.21.11-nightly.20260814.45c2e73080
- 包含上述 web-shell 修复与文件上传功能

### 基准验证（dsw-eas-tb-e2e 系列）
- Terminal-Bench 2.0 得分 89，SWE-bench Verified 全部通过；基准参考版本 v0.21.2


## 社区热点 Issues（Top 10）

### 1. `qwen serve` 守护进程资源使用无上限 — [#8051](https://github.com/QwenLM/qwen-code/issues/8051)
**标签**：P2 / needs-triage / performance / daemon
**社区反应**：9 条评论，持续讨论中
当前仅按工作区和会话数做限制，但请求体字节数、WebSocket 组装缓冲等未被约束。多工作区生产环境下存在内存失控风险，是 serve 模式迄今最重要的资源治理缺口。

### 2. 图片加载崩溃（0.21.2 起回归）— [#8957](https://github.com/QwenLM/qwen-code/issues/8957)
**标签**：P2 / bug / need-information / file-operations
**社区反应**：12 条评论，最活跃的 Issue 之一
0.21.1 是最后一个正常版本，之后读取图片即崩溃。用户已附上 `/about` 信息等待官方回复，回归原因尚未定位。

### 3. 只读 Shell 分类器可被命令注入绕过 — [#8582](https://github.com/QwenLM/qwen-code/issues/8582) ⚠️ 已关闭
**标签**：P1 / security / vulnerability
**社区反应**：5 条评论
AST 分类器与运行时替换检测均可被行继续符 `\` 或 `${var@P}` 绕过，导致只读模式自动批准实际执行任意代码的命令。安全影响大，虽然已关闭但修复方案值得关注。

### 4. ACP 子进程报 "Unknown argument: acp" — [#8871](https://github.com/QwenLM/qwen-code/issues/8871)
**标签**：P2 / bug / daemon / need-information
**社区反应**：5 条评论
`qwen serve` 以 `--http-bridge=true` 启动时，主进程以 `--acp` 参数拉起子进程失败，导致 token 认证 401。直接影响 serve 模式的 ACP 集成。

### 5. utils/ 目录循环依赖 — [#9146](https://github.com/QwenLM/qwen-code/issues/9146)
**标签**：P2 / refactor / core+cli
**社区反应**：4 条评论（新开 Issue）
51 个文件产生 107 次向上导入，目录图已成环。属于"技术债清理"类 Issue，短期不影响功能，但会持续增加维护成本。

### 6. SDK Python 拒绝 `permission_mode="auto"` — [#9002](https://github.com/QwenLM/qwen-code/issues/9002)
**标签**：P3 / bug / SDK
**社区反应**：6 条评论
CLI 支持 `auto` 但 Python SDK 客户端校验将其拒绝（仅接受 default/plan/auto-edit/yolo），在到达 CLI 前即报 ValidationError。CLI 与 SDK 参数不一致问题。

### 7. 主分支 CI 反复失败：E2E Tests — [#9160](https://github.com/QwenLM/qwen-code/issues/9160)
**标签**：P1 / CI / autofix-in-progress
**社区反应**：4 条评论（bot 自动创建）
`qwen-serve-live-journal-recovery` 等 3 个测试失败。连同 #9143、#9159，昨日已有 3 个 CI 失败追踪 Issue，主干稳定性压力不小。

### 8. autofix PAT 任务与不可信代码同机运行 — [#9089](https://github.com/QwenLM/qwen-code/issues/9089)
**标签**：P1 / security / GitHub Actions
**社区反应**：3 条评论
审查 #8961 时发现：持有 PAT 的 job 与不可信分支代码共享同一 runner，构成横向移动风险。属于无法在 Actions step 内部解决的架构级安全问题，需 runner 级隔离。

### 9. 长会话内存无限增长 — [#2128](https://github.com/QwenLM/qwen-code/issues/2128)
**标签**：P1 / enhancement / session-management
**社区反应**：4 条评论（已持续 5 个月）
UI History 数组无上限增长，数十小时会话后内存持续攀升。虽为已知问题，但至今仍未关闭。

### 10. Electron 桌面宿主方案评估 — [#9168](https://github.com/QwenLM/qwen-code/issues/9168)
**标签**：P3 / feature-request / need-discussion / web-shell
**社区反应**：3 条评论（新开 Issue）
提议在 Tauri 之外提供 Electron 预览版，让社区评估其作为替代桌面宿主的可行性。Web Shell 桌面化路线出现新分支。


## 重要 PR 进展（Top 10）

### 1. [feat(web-shell): 采用 Goal v3 控制平面](https://github.com/QwenLM/qwen-code/pull/9087) — @qqqys
支持在首条消息前创建 Goal，并可直接检查、暂停/恢复、替换与清除，无需经由模型路由指令。这是 Web Shell 从"被动聊天"走向"主动任务控制"的关键一步。

### 2. [fix(serve): 按字节限制 ACP HTTP 预附加缓冲](https://github.com/QwenLM/qwen-code/pull/9007) — @doudouOUC
将 ACP HTTP 预附加缓冲从"按数量"改为"按字节"边界控制，直接响应 #8051 的资源治理议题。

### 3. [feat(serve): 空通道集优雅降级 + 仅恢复活跃通道](https://github.com/QwenLM/qwen-code/pull/8978) — @rockybot2026
`--channel all` 遇到空通道集时不再 `exit(1)` 拖垮整个守护进程，改为 no-op 并仅恢复活跃通道。

### 4. [feat(audio): 附件音频桥接](https://github.com/QwenLM/qwen-code/pull/8332) — @DragonnZhang
主模型不支持音频时，通过配置的批量语音模型转写用户附件，并标记为"不可信机器转写"。交互/无头模式的 `@` 附件和 ACP 音频提示均覆盖。

### 5. [feat(review): capture-tui — 渲染断言获得像素级证据](https://github.com/QwenLM/qwen-code/pull/8894) — @wenshao
Phase 2 证据图像方案：在私有 tmux server 中驱动被审代码，按断言精确截取终端渲染结果（如"面板在 80 列处截断"），替代纯文字描述。

### 6. [fix(ci): 发布分支强制推送替换失败尝试](https://github.com/QwenLM/qwen-code/pull/9082) — @qwen-code-dev-bot
解决发布重试时旧分支残留导致 "Commit and Condition" 阶段反复失败的问题。

### 7. [feat(cli): 纯文本 /review 评论 + 严重级别跟随 attribution](https://github.com/QwenLM/qwen-code/pull/9027) — @wenshao
`--comment` 发布的评论改为自然语言风格，并按 `review.attribution` 区分严重级别标识，提升可读性。

### 8. [feat(auth): 新增 Kimi 与小米 MiMo 提供商](https://github.com/QwenLM/qwen-code/pull/8368) — @DragonnZhang
Kimi 提供 Coding Plan/API Key（中国/国际）三种接入方式；小米 MiMo 提供按量付费及中国/新加坡/国际区域选项。

### 9. [feat: 端到端会话媒体引用](https://github.com/QwenLM/qwen-code/pull/9127) — @ytahdn
覆盖 daemon、ACP bridge、TypeScript SDK、Web Shell 全链路：图片仅上传一次，以 media ID + 元数据传递，支持中途队列、注入回声、对账快照等场景。

### 10. [fix(review): 修复流水线七个缺陷](https://github.com/QwenLM/qwen-code/pull/9175) — @wenshao
通过对 4 个真实 PR 的完整审查实践发现并修复 7 个缺陷（含 2 个结构性问题），增量锚点不再因"无人认领的维度"被扣留。


## 功能需求趋势

| 方向 | 代表 Issue/PR | 热度 |
|------|-------------|------|
| **Web Shell 生态扩展** | Electron 桌面宿主（#9168）、HTML 导出用 WebShellTranscript 渲染（#9186）、Goal v3 控制（#9087）、会话媒体引用（#9127） | 🔥🔥🔥 昨日最活跃方向，多个新提案集中出现 |
| **serve 模式资源治理** | 守护进程资源上限（#8051）、ACP 缓冲按字节限制（#9007）、空通道优雅降级（#8978） | 🔥🔥🔥 用户对生产环境稳定性诉求强烈 |
| **架构/技术债清理** | utils/ 循环依赖（#9146）、ACP 依赖 serve 内部实现（#8084）、core+CLI 架构审查（#4063） | 🔥🔥 长期跟踪型 Issue 持续更新 |
| **安全加固** | 只读 Shell 命令注入绕过（#8582）、autofix PAT runner 隔离（#9089） | 🔥🔥 已关闭但影响深远 |
| **新模型/提供商接入** | Kimi、小米 MiMo（#8368） | 🔥 社区对国内模型提供商有明确需求 |
| **CI/发布可靠性** | 发布分支强推（#9082）、多次 E2E 失败（#9143/#9159/#9160） | 🔥 自动化质量成为关注焦点 |


## 开发者关注点

1. **回归频发**：图片加载在 0.21.2 回归（#8957），CLI/SDK 参数不一致（#9002），开发者对版本稳定性的耐心正在消耗。

2. **serve 模式生产可用性**：守护进程资源无上限（#8051）、ACP 子进程崩溃（#8871）、空通道集拖垮进程（#8978）——"Run it in production" 的诉求非常集中。

3. **安全问题出现"审查盲区"**：只读 Shell 的命令注入绕过（#8582）和 autofix PAT 与不可信代码共享 runner（#9089）都指向自动化审查/执行链路中的信任边界问题——"自动化越强，信任边界越要清晰"。

4. **CI 失败已影响主干信心**：昨日 3 个 bot 自动创建的 CI 失败 Issue，且 #9143 被标记 `autofix/skip`——"发布流程本身开始成为瓶颈"的迹象。

5. **内存治理仍是长期痛点**：#2128 已持续 5 个月未关闭，长会话内存无上限增长是高频反馈——开发者对"数小时甚至数天不重启"的使用场景有真实需求。

6. **架构重构引发讨论但推进谨慎**：#4063 的 12 项结构性问题清单与 #9146 的循环依赖获得关注，但开发者普遍期待"小步快走"式演进而非大爆炸式重构。

---

*本日报由 AI 技术分析师自动生成，数据采集时间：2026-08-15T00:00:00Z*

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

# DeepSeek TUI 社区动态日报

**2026-08-15** | 数据来源: [Hmbown/DeepSeek-TUI](https://github.com/Hmbown/DeepSeek-TUI) (已更名为 CodeWhale)

---

## 今日速览

v0.9.8 发布并正式启用 **CodeWhale** 品牌，但 `main` 分支因多处测试断言未同步更新而出现跨平台 CI 红标，社区成员（Lstarsky0、EvanProgramming）已在 24 小时内提交修复。稳定性问题（会话索引数据丢失、webhook panic、输出区渲染回归）与功能增强（DS4 一键配置、Auto-Review 双层模式、插件系统规划）并行推进。

---

## 版本发布

### v0.9.8
- 正式启用 **Codewhale** 作为公开产品名，`codewhale` 命令及 npm 包统一采用小写标识符
- 旧 npm 包 `deepseek-tui` 已弃用，不再接收后续更新
- 新增 **DwarfStar (DS4) 本地模型**一键配置（`/setup provider ds4`）
- Auto-Review 升级为双层模式：确定性校验层不可绕过 + 新增 **model guardian** 兜底层
- 输出 token 上限从 65,536 提升至与 models.dev 目录一致的 384,000（针对 deepseek-v4-flash/pro）

---

## 社区热点 Issues（Top 10）

1. **[#3192] 请求接入 agentclientprotocol/registry** — [链接](https://github.com/Hmbown/CodeWhale/issues/3192)  
   *评论 13 | 开放中* — 用户希望项目入驻 agentclientprotocol 注册表以便 Zed 编辑器直接安装调用，反映了 IDE 生态集成诉求。

2. **[#1004] /dryrun 命令：预览下一次聊天请求** — [链接](https://github.com/Hmbown/CodeWhale/issues/1004)  
   *评论 9 | 开放中* — 在长上下文的 V4 Pro 会话中，开发者希望在发送前查看实际请求内容（系统提示、工具定义、提及文件等），避免巨额 token 浪费。

3. **[#5324] agent 工具 32 字段 schema 简化** — [链接](https://github.com/Hmbown/CodeWhale/issues/5324)  
   *评论 8 | 开放中* — 维护者 Hmbown 提出的核心架构问题：8 种动作共用零必填字段的 32 属性 schema 导致模型频繁报错，需拆分或简化。

4. **[#5374] 代理输出文本在 macOS 上显示乱码** — [链接](https://github.com/Hmbown/CodeWhale/issues/5374)  
   *评论 4 | 开放中* — 新用户反馈 macOS 上代理书写内容严重错乱，配图佐证，属于影响体验的显示层 bug。

5. **[#1482] nVidia NIM 不工作** — [链接](https://github.com/Hmbown/CodeWhale/issues/1482)  
   *评论 6 | 开放中* — 调用 NIM 端点返回 404，老版本问题至今未关闭，第三方推理服务兼容性待验证。

6. **[#4785] 464 处 #[allow(dead_code)] 掩盖代码漂移** — [链接](https://github.com/Hmbown/CodeWhale/issues/4785)  
   *评论 6 | 开放中* — 维护者自查发现大量死代码标注使编译器无法报告结构性问题，属于工程质量隐患。

7. **[#4326] 取消 32-worker 风暴后 RSS 不回落** — [链接](https://github.com/Hmbown/CodeWhale/issues/4326)  
   *评论 6 | 开放中* — 高并发 PTY 基准测试后内存驻留不释放，需区分分配器高水位与实际泄漏。

8. **[#5293] deny-by-default 权限选择应可配置** — [链接](https://github.com/Hmbown/CodeWhale/issues/5293)  
   *评论 5 | 👍 1 | 已关闭* — 用户指出 v0.9.4 开始权限对话框默认选项变更为「拒绝」，破坏既有交互习惯，易误操作。

9. **[#5370] P0: Web UI 完全损坏** — [链接](https://github.com/Hmbown/CodeWhale/issues/5370)  
   *评论 1 | 开放中* — 维护者确认公开 Web UI（codewhale.net）外观及功能均严重异常，需对照 harness 引用全面重建。

10. **[#5390] 关闭会话后旧代理持有写入锁** — [链接](https://github.com/Hmbown/CodeWhale/issues/5390)  
    *评论 1 | 已关闭* — 生产环境问题：会话关闭后旧代理仍持有实验目录写权限，阻止新子代理启动。

---

## 重要 PR 进展（Top 10）

1. **[#5382] 修复 StateStore 会话索引并发数据丢失** — [链接](https://github.com/Hmbown/CodeWhale/pull/5382)  
   `已关闭` — EvanProgramming 提交：将 `session_index.jsonl` 写入移入 `Arc<Mutex>` 保护范围，修复多 StateStore 克隆实例下的静默数据丢失（对应 #5380）。

2. **[#5381] 修复 webhook HTTP 客户端构建失败时 panic** — [链接](https://github.com/Hmbown/CodeWhale/pull/5381)  
   `已关闭` — 将 `.expect()` 替换为优雅降级，避免 TLS 后端配置异常导致宿主进程崩溃（对应 #5379）。

3. **[#5378] 修正九项 reasoning-effort 测试断言** — [链接](https://github.com/Hmbown/CodeWhale/pull/5378)  
   `已关闭` — Lstarsky0 修复 macOS/Windows CI 红标：9 个测试仍断言旧的 off/high/max 词汇表，已同步为新阶梯式定义。

4. **[#5376] 过滤 TUI 内部运行时事件** — [链接](https://github.com/Hmbown/CodeWhale/pull/5376)  
   `已关闭` — 防止内部投递事件泄漏到 session peek 面板，保持用户视图纯净（对应 #5375）。

5. **[#5384] 重新固定 provider-count 断言** — [链接](https://github.com/Hmbown/CodeWhale/pull/5384)  
   `开放中` — 将 CLI 测试中的 ProviderKind 计数从 43/38 更新至 v0.9.8 实际的 45/40（对应 #5383）。

6. **[#5365] DS4 本地模型一级配置支持** — [链接](https://github.com/Hmbown/CodeWhale/pull/5365)  
   `已关闭` — 新增 `/setup provider ds4` 一键预设，复用 OpenAI 兼容传输层，零密钥本地回环配置。

7. **[#5353] Auto-Review 双层模式 + model guardian** — [链接](https://github.com/Hmbown/CodeWhale/pull/5353)  
   `已关闭` — 确定性拒绝不可绕过，兜底升级为一次性模型守护者仲裁，对齐 Codex/Kimi 语义。

8. **[#5364] TUI 渲染 Markdown 引用块** — [链接](https://github.com/Hmbown/CodeWhale/pull/5364)  
   `已关闭` — SparkofSpike 实现 `>` 引用块带引号导轨渲染，支持嵌套、行内格式、换行及选区复制。

9. **[#5369] Moonshot schema 降级而非拒绝条件字段** — [链接](https://github.com/Hmbown/CodeWhale/pull/5369)  
   `已关闭` — 对 Moonshot 模型无法处理的条件 schema 做降级剥离而非整体拒绝，减少模型报错。

10. **[#5339] 过滤子进程 shell 补全事件** — [链接](https://github.com/Hmbown/CodeWhale/pull/5339)  
    `已关闭` — 子代理的后台 shell 补全事件不再混入父模型流，保留父级未接管补全及任务状态可见性。

---

## 功能需求趋势

| 方向 | 代表 Issue/PR | 热度 |
|------|--------------|------|
| **IDE / Agent 生态集成** | #3192（agentclientprotocol 注册）、#5311（插件系统 + 联邦市场） | 🔥🔥🔥 |
| **架构简化与 schema 治理** | #5324（32 字段 schema 拆分）、#5369（Moonshot 降级） | 🔥🔥🔥 |
| **可靠性 / 数据安全** | #5382（会话索引并发写）、#5381（webhook panic）、#5372（写锁残留） | 🔥🔥🔥 |
| **模型支持扩展** | #5365（DS4 本地）、#1482（NVIDIA NIM）、#5350（第三方模板） | 🔥🔥 |
| **TUI 体验打磨** | #5364（引用块渲染）、#5374（Mac 中文乱码）、#5322（宽屏自适应回归） | 🔥🔥 |
| **AI 辅助开发工作流** | #1004（/dryrun 预览）、#5353（Auto-Review 双层） | 🔥🔥 |
| **性能与资源治理** | #4326（32-worker 内存不回落）、#4785（dead_code 清理） | 🔥 |

---

## 开发者关注点

1. **CI 稳定性震荡** — v0.9.8 发布后 `main` 在 macOS/Windows 持续红标（#5377、#5383），均为断言未随功能更新同步，社区成员已快速响应提交修复，但暴露出发布流程缺少跨平台预检。

2. **第三方模型配置门槛** — #5350（中文反馈）指出配置 OpenCode Zen、美团 Sensenova 等服务商需手动填 URL/模型名/密钥，且保存后状态卡在 `not checked`，建议内置预制模板 + 测试连接按钮。

3. **高并发场景资源泄漏** — 32-worker PTY 基准测试后 RSS 不回落（#4326），以及关闭会话后写锁残留（#5372），表明子代理生命周期管理仍需加强。

4. **默认交互模式变更引发不满** — #5293 中用户明确反对 v0.9.4 将权限请求默认选项改为「拒绝」，社区对破坏肌肉记忆的 UI 变更非常敏感，需提供配置开关。

5. **Schema 复杂度已影响模型正确性** — #5324 中 32 字段零必填的 agent schema 让模型频繁报错，配合 #5369 的降级策略，开发者普遍认同「简化的 schema 比功能齐全但难用的 schema 更有价值」。

6. **旧版本遗留问题关闭缓慢** — #1482（NVIDIA NIM）自 5 月起持续开放，用户对第三方推理端点（NIM、vLLM 等）的兼容性验证需求强烈。

</details>

---
*本日报由 [agents-radar](https://github.com/kky-wollu/agents-radar) 自动生成。*