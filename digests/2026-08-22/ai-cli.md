# AI CLI 工具社区动态日报 2026-08-22

> 生成时间: 2026-08-21 22:29 UTC | 覆盖工具: 9 个

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

# AI CLI 工具横向对比分析报告

**报告日期：2026-08-22**
**分析范围：Claude Code、OpenAI Codex、Gemini CLI、Copilot CLI、Kimi Code CLI、OpenCode、Pi、Qwen Code、DeepSeek TUI（CodeWhale）**


## 1. 生态全景

AI CLI 工具已全面进入 **"工程化深水区"** ——各主流工具不再比拼基础对话能力，而是围绕 **沙箱安全、长会话稳定性、成本透明度、多模型接入、远程控制** 等生产级诉求展开激烈竞争。安全过滤器的误报问题（Claude Code、Qwen Code）、后台任务的生命周期管理缺陷（Kimi、Gemini、CodeWhale）、以及 Provider 适配层的成本与兼容性差距（Pi、OpenCode）成为社区声量最大的共性痛点。同时，头部工具（如 Claude Code、Codex）正加速向企业级功能（数据驻留、Bedrock/Vertex 支持）渗透，而中小型工具（CodeWhale、Pi）则在细分场景（无人值守、终端兼容性）上寻求差异化突破。


## 2. 各工具活跃度对比

| 工具 | 今日 Issues | 今日 PR | Release | 备注 |
|---|---|---|---|---|
| **Claude Code** | 10+（Top 10 精选） | 0 | **v2.1.239** | 大量 AUP 误报 Issue；新版聚焦成本估算与全屏渲染扩展 |
| **OpenAI Codex** | 10+（Top 10 精选） | **10**（均合并） | **5 个 alpha** | 远程控制回归、macOS 稳定性问题集中 |
| **Gemini CLI** | 10（Top 10 精选） | **10**（含 1 合并 + 9 新增） | **v0.56.0-nightly** | 子代理假成功、Auto Memory 安全 |
| **Copilot CLI** | 10（精选） | 0 | **v1.0.81-7（预发布）** | BYOK 多模型呼声最高；Windows 问题频出 |
| **Kimi Code CLI** | 1 | 1 | 无 | 社区规模较小，但 #2615 属严重资源泄漏 |
| **OpenCode** | 10（Top 10 精选） | **10**（含 9 合并） | **v1.18.20 / v1.18.21** | 稳定修复为主，响应中断问题集中 |
| **Pi (pi-mono)** | 10（Top 10 精选） | **7** | 无 | 压缩机制缺陷、SDK 定制需求 |
| **Qwen Code** | 10（Top 10 精选） | **10**（含 1 合并） | **v0.21.14-nightly** | CI 安全加固、daemon 会话管理 |
| **CodeWhale (DeepSeek-TUI)** | 9（精选） | **10**（含 5 dependabot） | 无 | 监督式运行基础设施成核心主题 |

> **注**：Issue/PR 数量为各工具日报中精选/列出条目，非全量统计。


## 3. 共同关注的功能方向

以下需求在至少 3 个工具社区中形成共鸣：

| 功能方向 | 涉及工具 | 具体诉求 |
|---|---|---|
| **安全过滤器误报/过拦截** | Claude Code（Fable 5 模型误报）、Qwen Code（权限分类器 fail-open）、Gemini CLI（沙箱逃逸风险） | 合法开发任务（安全审计、自动化代码）频繁被中断；需要更细粒度的策略配置与误报快速解除机制 |
| **长会话稳定性与资源控制** | Kimi（#2615 后台子代理失控）、Gemini（#21409 子代理挂起）、Pi（#6879 压缩失效导致上下文溢出）、Qwen（#5180 主-子会话中途崩溃） | 子代理任务生命周期管理不完善，存在无限挂起、假成功、不可见资源消耗等问题 |
| **成本透明化与配额控制** | Codex（#35259 wait/status 轮询消耗配额）、Pi（#7995 缓存支持差距导致 2.5 倍成本惩罚）、OpenCode（#14524 模型选择器显示成本）、Claude Code（成本估算增强） | 用户对 token 消耗、缓存效率、配额计费的可见性要求急剧上升 |
| **多模型/Provider 适配** | Copilot CLI（BYOK 多模型切换）、Pi（OpenRouter reasoning 参数兼容）、Qwen（Kimi/小米 MiMo/钉钉）、OpenCode（ChatGPT Plus OAuth 失败） | 单一模型锁定已无法满足需求；第三方模型接入体验的工程成熟度参差不齐 |
| **MCP 生态稳定性** | Copilot CLI（BigInt 序列化失败）、Qwen（Windows MCP 连接关闭）、OpenCode（MCP 工具定义体积）、Gemini（MCP OAuth scope） | 跨工具普遍存在 MCP 边界场景处理不健壮的问题 |
| **Windows 平台体验** | Copilot CLI（#4549 控制台闪烁）、Qwen（#9666 IME 候选框）、Codex（#25220 EFS 加密插件不可用）、OpenCode（#30906 UI 冻结、#43850 OAuth 失败） | Windows 用户负面反馈集中，各工具在 Windows 上的工程质量均落后于 macOS/Linux |
| **会话恢复与状态一致性** | Copilot CLI（v1.0.81-7 会话自动恢复）、Claude Code（会话恢复误报）、Qwen（#9688 归档冲突）、Pi（#8428 会话重建工具结果重新配对） | 崩溃/重启后的会话恢复、状态一致性成为刚需 |


## 4. 差异化定位分析

| 工具 | 核心定位 | 目标用户 | 技术路线/特点 |
|---|---|---|---|
| **Claude Code** | 企业级全功能 Agent | 企业开发者、需要安全合规的组织 | 依托 Anthropic 模型 + Bedrock/Vertex 多云支持；强化成本估算、数据驻留；但对安全模型过度依赖（AUP 误报即体现） |
| **OpenAI Codex** | 全平台桌面 + 云端生态 | ChatGPT Plus/Pro/Ultra 订阅用户 | 桌面端 + Android/iOS 远程控制；Guardian 风险审查体系；Rust 核心；沙箱审批精细化 |
| **Gemini CLI** | Google 生态深度集成 | GCP 用户、Android 开发者、开源社区 | 强调研评基础设施（LLM-as-Judge、E2E 基准）；Agent 行为评测体系最完善；Auto Memory 机制 |
| **Copilot CLI** | GitHub 生态入口 | GitHub 重度用户、企业开发者 | BYOK 多模型支持（GitHub Models）；ACP 协议（Agent Client Protocol）；TUI 体验持续迭代；与 GitHub 深度绑定 |
| **Kimi Code CLI** | 轻量、快速 | 中文开发者、Moonshot 模型用户 | 社区规模较小但增长中；插件机制初具形态；文档安全规范完善 |
| **OpenCode** | 开源、协议兼容 | 开源社区、自托管用户 | 最活跃的开源实现之一；多 Provider 适配（OpenAI 兼容协议）；社区贡献者活跃（kitlangton 单日 4 PR） |
| **Pi** | 极致可定制的 TUI | 高度技术化的 CLI 用户、终端控 | 深度终端协议支持（Kitty、Windows Terminal）；压缩体系精细可配置；SDK 层开放定制能力 |
| **Qwen Code** | 阿里系国产全栈 | 中文开发者、阿里云用户 | review/CI 自动化治理投入最大；支持钉钉等国产 IM 渠道；国产模型（Kimi、MiMo）接入积极；SWE-bench 验证体系完善 |
| **CodeWhale** | 多路复用终端内的 TUI | Rust 开发者、Fleet 派发/无人值守场景 | 独特的多路复用终端集成（herdr）；监督式运行基础设施（控制套接字、生命周期事件）；TUI crate 分解重构推进 |


## 5. 社区热度与成熟度

**第一梯队（最活跃社区，Issue 日增 10+，PR 日增 10+）**
- **OpenAI Codex**：社区声量最大，远程控制与 macOS 稳定性问题引发集中反馈，但 PR 合入效率高（10 PR 全部合并），呈高频迭代态势。
- **Gemini CLI**：评估体系投入最大（多个评测 PR 并行），社区对 Agent 行为可信度（假成功、挂起）反馈集中。
- **OpenCode**：开源社区中最活跃者之一，贡献者质量高（kitlangton 连续高质量修复），迭代速度极快（1 天 2 个版本）。

**第二梯队（中等活跃度，Issue/PR 日增 5-10 条）**
- **Claude Code**：Issue 声量大但 PR 为 0，社区反馈主要围绕 AUP 误报且多被标记 duplicate/stale，反映官方响应/修复速度有待提升。
- **Copilot CLI**：功能需求呼声高（BYOK、会话分支）但 PR 停滞（今日 0 PR），预发布版本的会话恢复是亮点。
- **Qwen Code**：CI/CD 治理投入巨大，review 流水线安全加固持续深化，SWE-bench 验证体系成熟。
- **Pi**：社区讨论深度高，偏向技术细节（压缩、终端协议），核心维护者响应较快。

**第三梯队（小众但高活跃贡献者）**
- **CodeWhale（DeepSeek-TUI）**：社区规模小但贡献者活跃（M-Maciej 单日 1 个大 PR + 4 个 Issue），聚焦监督式运行场景。
- **Kimi Code CLI**：社区规模最小，今日仅 1 Issue 1 PR，但 #2615 的严重性不容忽视。


## 6. 值得关注的趋势信号

1. **安全过滤器正在成为"双刃剑"**：Claude Code 的 Fable 5 模型大规模误报，Qwen 的权限分类器 fail-open，说明安全机制在精确性上远未成熟。对开发者的启示：选择工具时需考虑安全策略的可配置性与误报反馈通道；对工具厂商而言，"开发者自证授权"通道将是必要的补救机制。

2. **"静默失败"与"假成功"是信任杀手**：Gemini 的子代理假成功（#22323）、CodeWhale 的工作流静默失败（#5528）、Kimi 的后台子代理失控（#2615）——这类"看起来成功实际失败"的问题比直接报错更消耗信任。状态透明性与真实终态语义将成为 Agent 工具的核心竞争力。

3. **成本可观测性成为刚需**：Pi 的 2.5 倍缓存成本差距（#7995）、Codex 的配额轮询消耗（#35259）、OpenCode 的成本显示需求（#14524）——多工具社区同时爆发成本焦虑，说明 Agent 的 token 消耗模式（轮询、重试、缓存）已复杂到用户无法直观预估，"成本可解释性"将直接影响工具选型。

4. **Windows 平台是"最后的洼地"**：Copilot CLI、Qwen、Codex、OpenCode 均出现 Windows 专属问题（控制台闪烁、IME 对比度、EFS 加密、OAuth 失败），反映各工具在 Windows 上的工程投入普遍不足。对 Windows 开发者而言，当前主流 AI CLI 的体验差距较大，选择时需格外谨慎；这也是潜在的市场空白。

5. **"监督式运行"与"无人值守"是下一波需求**：CodeWhale 的监督式运行基础设施（控制套接字、事件 Outbox、/relaunch）和 Copilot CLI 的会话自动恢复，指向同一趋势——Agent 从"交互式工具"走向"后台服务"。CI/CD 集成、远程监督、长时任务编排将成为下一阶段的功能高地。

6. **Agent 评估体系正在成为基础设施**：Gemini CLI 投入大量 PR 构建 LLM-as-Judge、E2E 基准运行器，Qwen 坚持 SWE-bench 验证——头部工具已开始将 Agent 质量验证体系化，这既是对自身能力的量化管理，也将成为行业评测的事实标准，普通开发者可据此作为工具选型的客观参考。

---

*报告完*

---

## 各工具详细报告

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills 社区热点

> 数据来源: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills 社区热点报告（数据截止 2026-08-22）

## 一、热门 Skills 排行（按关注度与讨论热度）

| 排名 | Skill / PR | 功能定位 | 讨论热点 | 状态 |
|------|-----------|----------|----------|------|
| 1 | **skill-creator 修复** (#1298) | 修复 `run_eval.py` 评测工具 0% recall 的系统性缺陷（Windows 兼容 + 触发检测） | 评测工具失效导致 skill 优化循环失效，已获 10+ 独立复现，是当前最高优先级工程问题 | Open |
| 2 | **document-typography** (#514) | AI 生成文档的排版质量控制（孤词换行、孤行段落、编号对齐） | 用户普遍反映 AI 文档排版问题，需求覆盖面广 | Open |
| 3 | **ODT skill** (#486) | OpenDocument 格式（.odt/.ods）创建、填写、转换与解析 | 填补文档格式生态空白，与既有 docx/pdf skill 形成互补 | Open |
| 4 | **ServiceNow 平台 skill** (#568) | 覆盖 ITSM/ITOM/ITAM/FSM/SPM/CSDM 等全模块的 ServiceNow 平台助手 | 企业级平台需求明确，讨论周期长（3月至今）持续活跃 | Open |
| 5 | **self-audit 技能** (#1367) | AI 输出交付前的机械验证 + 四维推理质量审查，跨项目通用 | 对 AI 输出质量的系统性验证方法，与 #1385 提案形成配套 | Open |
| 6 | **pyxel 复古游戏开发** (#525) | 基于 Pyxel 引擎的像素风游戏开发工作流 | 创意类 skill 的代表，触发逻辑清晰（write→run→inspect→iterate） | Open |
| 7 | **Skill 质量/安全分析器** (#83) | 新增 skill-quality-analyzer 与 skill-security-analyzer 两个元技能 | 社区对 skill 本身的质量与安全检查需求上升 | Open |

## 二、社区需求趋势（来自 Issues）

1. **安全与信任边界**（#492，43 评论）：最强烈呼声 —— 社区 skill 被分发在 `anthropic/` 命名空间下造成信任混淆，要求建立明确的来源标识与权限管控机制。
2. **组织级共享**（#228，16 评论）：用户要求 skill 支持组织内直接共享/分发，而非手动文件传输。
3. **工具链可靠性**（#556，12 评论）：`run_eval.py` 评测工具的 0% 触发率 bug 已阻断 skill 迭代流程，成为生态健康的首要阻塞项。
4. **规范符合性**（#202，#412）：社区提案要求 skill-creator 从"教学文档"转向"操作指令"，并倡导 agent 治理/安全规范类 skill。
5. **去重与上下文优化**（#189，#1487）：重复安装导致 skill 冲突、以及某些 skill 单次注入 ~156k tokens 挤爆上下文窗口 —— 资源管理成为新关注点。

## 三、高潜力待合并 Skills（近期可能落地）

- **document-typography** (#514)：解决所有 AI 生成文档的通用排版痛点，需求验证充分，PR 结构完整，最有望尽快合并。
- **self-audit + Reasoning Quality Gate Pipeline** (#1367 + #1385)：质量门控体系已成体系化提案，且已有 v1.3.0 迭代版本，合并概率高。
- **ODT skill** (#486)：补齐文档格式矩阵（docx/pdf/odt），功能边界清晰，与现有 skill 无冲突。
- **pyxel skill** (#525)：由 Pyxel 引擎作者本人提交，质量有背书，触达创意开发者社区。
- **ServiceNow skill** (#568)：企业级平台集成需求明确，虽体量大但持续活跃，讨论已超 5 个月。

## 四、Skills 生态洞察

> **社区最集中的诉求是"工程质量与可信度"—— 既包括 skill 运行时工具链的可靠性（评测工具失效、Windows 兼容性），也包括 skill 本身的安全边界（命名空间信任、上下文窗口占用），而功能层面则以"文档全格式覆盖 + 通用质量验证"为两大主线。**

**核心数据参考：**
- 工具链可靠性问题（#1298 + #556 + #1099 + #1050）累计评论超 30 条，是最集中的工程痛点
- 安全信任问题（#492）以 43 条评论居 Issues 榜首，👍 2 次
- 文档相关（typography/ODT/docx）与质量验证（self-audit）构成 PR 数量最多的两大主题

---

## 📰 Claude Code 社区动态日报 — 2026-08-22

### 一、今日速览

今日发布 v2.1.239，主要在**成本估算**中纳入了数据驻留工作区的 1.1 倍美国推理附加费，并向 Bedrock、Vertex 等此前未覆盖的平台推出了全屏渲染器。社区层面，**大量 Issue 集中在 AUP/安全过滤器的误报问题**，多位用户报告在合法开发场景中被中断会话，涉及“Fable 5”安全模型的过度拦截。

---

### 二、版本发布

**v2.1.239**（最新）
- **成本估算增强**：`/cost` 命令、状态栏和 `--max-budget-usd` 现在会将数据驻留工作区的 1.1 倍美国专属推理附加费计入成本估算。
- **全屏渲染器支持扩展**：为 Bedrock、Vertex、Foundry 及其他此前未包含的平台新增一次性全屏渲染器选项，新安装用户默认启用该模式。

---

### 三、社区热点 Issues（Top 10）

**1. [#72712] Claude Code 仅加载固定 10 个系统 CA 证书，导致 /v1/messages 请求失败**
- 平台：macOS | 严重度：高（API 完全不可用）
- 作者报告 `CLAUDE_CODE_CERT_STORE` 环境变量不生效，无论设置值如何，工具始终只加载固定子集的系统根证书，导致企业代理/自签证书环境下主 API 请求报 `UNABLE_TO_GET_ISSUER_CERT`。
- 影响面大，涉及企业网络与自定义 CA 场景。
- 链接：[#72712](https://github.com/anthropics/claude-code/issues/72712)

**2. [#73126] 自研无人机地面站 FOSS 项目被误判为恶意反编译，会话终止**
- 平台：Linux | 类型：网络安全过滤器误报
- 用户构建开源地面控制站时被服务器端判定为“反编译攻击”并中断会话。属于安全过滤器 false positive 的典型场景，提醒开发者涉及二进制分析时需预判误报风险。
- 链接：[#73126](https://github.com/anthropics/claude-code/issues/73126)

**3. [#73183] 防御性漏洞清理自己的 Web 应用时，因一句“沮丧感叹”触发会话中止**
- 类型：AUP 误报 | 标记模型：Fable 5
- 用户在对自己授权拥有的 Web 应用进行防御性漏洞审计时，因输入了包含情绪化感叹的文本，被安全模型判定为违规并中止会话。
- 链接：[#73183](https://github.com/anthropics/claude-code/issues/73183)

**4. [#73172] 合法交易机器人升级部署 + 3D 可视化被标记为 AUP 违规**
- 类型：AUP 误报 | 工作域：general
- 用户已通过验证的交易机器人扩容升级和仪表盘 3D 视觉优化被拦截，社区认为安全模型在金融交易相关代码检测上存在过度敏感。
- 链接：[#73172](https://github.com/anthropics/claude-code/issues/73172)

**5. [#73181] 恢复对自己 Web 应用的防御性漏洞扫描时触发 AUP 拦截**
- 类型：AUP 误报 | 工作域：defensive-hardening
- 用户在暂停后恢复自己的漏洞扫描任务时被阻断，即使工作性质完全合法。多个同系列 Issue 表明 Fable 5 在**会话恢复**场景中的误报率偏高。
- 链接：[#73181](https://github.com/anthropics/claude-code/issues/73181)

**6. [#73168] 审计带 QR/Passkey 功能的内部模块交互时被拦截**
- 类型：AUP 误报 | 涉及认证流程代码
- 用户在代码审计时触发了安全过滤器，社区猜测认证相关代码（QR 码、Passkey）极易被安全模型误判为凭证窃取行为。
- 链接：[#73168](https://github.com/anthropics/claude-code/issues/73168)

**7. [#73195] Fable 5 将“然后继续”这样的普通恢复指令标记为违规**
- 类型：AUP 误报 | 会话中途切换模型后触发
- 用户在会话中切换模型后，发出无歧义的恢复指令（"then continue"）即被拦截。社区认为这是安全模型在**上下文切换后误判风险**的典型案例。
- 链接：[#73195](https://github.com/anthropics/claude-code/issues/73195)

**8. [#73145] GlassFalcon 项目中 ClAudit 误报（API Error）**
- 类型：AUP 误报 | 涉及 API 错误触发的连锁拦截
- 用户报告 API 错误本身触发了安全过滤链，导致会话被终止。这表明错误处理路径也可能成为误报来源。
- 链接：[#73145](https://github.com/anthropics/claude-code/issues/73145)

**9. [#73169] 常规代码审计（内部子系统变更）被安全防护阻断**
- 类型：AUP 误报 | 工作域：general
- 用户对内部子系统的常规代码审计被完全阻断，社区反馈这类"日常开发工作被中断"的模式出现频率显著增加。
- 链接：[#73169](https://github.com/anthropics/claude-code/issues/73169)

**10. [#73211] 对自己网站后端基础设施的例行安全审计被拦截**
- 类型：AUP 误报 | 工作域：general | 重复报告
- 属于 #73183 系列的重复报告，进一步佐证 Fable 5 安全模型在安全审计类任务上的高误报率。
- 链接：[#73211](https://github.com/anthropics/claude-code/issues/73211)

---

### 四、重要 PR 进展

过去 24 小时内无新增或更新的 Pull Request。

---

### 五、功能需求趋势

综合近 24 小时 Issue 数据，社区最关注的方向如下：

1. **安全过滤器的精准度**（占比超过 40%）
   - 核心诉求：AUP 过滤器（尤其 Fable 5 模型）的误报率过高，频繁阻断合法开发任务。
   - 常见触发场景：防御性安全审计、自主漏洞修复、FOSS 项目开发、机器人/无人机等自动化代码。

2. **CA 证书灵活配置**（高影响）
   - `CLAUDE_CODE_CERT_STORE` 环境变量不生效的问题直接影响到企业代理/自签证书用户，诉求为支持完整系统 CA 存储或用户自定义证书链。

3. **会话恢复的稳定性**（中等热度）
   - 多个 Issue 表明在会话恢复（尤其是切换模型后）时，安全模型容易将正常的恢复指令误判为风险操作。

---

### 六、开发者关注点

**痛点 1：AUP 安全过滤器误报频繁且阻断严重**
- 几乎所有 AUP 误报 Issue 的严重级别都是 **session-halted**（整个会话被终止），而非简单的操作拦截。意味着用户可能丢失未保存的上下文和进度，影响远大于单次操作失败。
- 情绪化文本（如“感叹”）、安全审计类任务、认证相关代码、会话恢复指令是高频误报场景。

**痛点 2：误报修复流程冗长**
- 几乎所有已关闭 Issue 均标注为 `[CLOSED]`，且多数带 `duplicate` 或 `stale` 标签，用户反馈缺乏实质性解决方案或公开修复计划。

**痛点 3：企业级功能部署困难**
- macOS 上 CA 证书问题直接影响企业环境使用；而新版本对 Bedrock/Vertex 等平台的全屏渲染支持，说明非 Anthropic 直连 API 部署仍存在功能差距。

---

> **编辑备注**：本期最值得关注的变化是 v2.1.239 对成本估算的修正（数据驻留附加费）和全屏渲染向更多平台的开放。但社区声量最大的是 AUP 误报问题——Fable 5 安全模型的过度拦截已经影响到大量正常开发流程，建议 Anthropic 尽快推出误报反馈和快速解除机制，或在安全模型中增加“开发者自证授权”的通道。

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex 社区动态日报 — 2026-08-22

## 今日速览

昨日 Codex 仓库共推送 5 个新 Release（均为 Rust 版本），并围绕沙箱审批流程、Guardian 风险审查、浏览器/计算机使用权限配置等方向合并了大量 PR。Issue 侧最突出的信号是 **Windows + Android 远程控制（Remote Control）功能出现集中性回归**，同时 macOS 桌面端爆出 Computer Use 进程反复崩溃（V8 OOM）与 auth 失效问题，社区反馈热度居高不下。

---

## 版本发布

过去 24 小时共发布 5 个 Rust 版本，均为 alpha 通道迭代。Release notes 暂未附带实质性变更说明，推测为 CI 构建与内部验证用途：

- [`rust-v0.150.0-alpha.5`](https://github.com/openai/codex/releases/tag/rust-v0.150.0-alpha.5)
- [`rust-v0.150.0-alpha.3`](https://github.com/openai/codex/releases/tag/rust-v0.150.0-alpha.3)
- [`rust-v0.150.0-alpha.2`](https://github.com/openai/codex/releases/tag/rust-v0.150.0-alpha.2)
- [`rust-v0.149.0-alpha.7.1`](https://github.com/openai/codex/releases/tag/rust-v0.149.0-alpha.7.1)
- [`rust-v0.149.0-alpha.4.1`](https://github.com/openai/codex/releases/tag/rust-v0.149.0-alpha.4.1)

---

## 社区热点 Issues（Top 10）

### 🔥 1. [macOS] Computer Use 进程反复崩溃（V8 OOM）
**Issue #38455** — 评论 35 | 👍 15  
macOS 15.7.7 / Apple Silicon / 32 GB 环境下，ChatGPT 桌面版 **26.810.41047** 在启动约 98 秒后反复以 `node::OOMErrorHandler` 崩溃，崩溃时 316 个线程中有 187 个名为 `computer-use`。此前版本（26.730.61639）无此问题。  
👉 链接: https://github.com/openai/codex/issues/38455

### 🔥 2. [macOS] 打开既有会话导致 auth 失效并跳转登录
**Issue #39162** — 评论 31 | 👍 22  
版本 **26.814.41407** 在打开历史会话时会直接使 ChatGPT token 失效，重定向至登录页。已知上一正常版本为 26.810.52044。  
👉 链接: https://github.com/openai/codex/issues/39162

### 🔥 3. [Windows] EFS 加密导致内置插件全部不可用
**Issue #25220** — 评论 27 | 👍 4  
Windows 11（26200 版本）下，因 WindowsApps 目录受 EFS 加密，`copyfile` 失败，Computer Use / Browser / Chrome / LaTeX 等内置插件在市场中全部显示不可用。  
👉 链接: https://github.com/openai/codex/issues/25220

### 🔥 4. [沙箱] 桌面自动化静默降级为 workspace-write
**Issue #15310** — 评论 21 | 👍 16  
定时/周期自动化任务总是以 `workspace-write` 沙箱启动，即使用户配置为 `danger-full-access`。仅当用户手动进入聊天界面后策略才会被纠正。  
👉 链接: https://github.com/openai/codex/issues/15310

### 🔥 5. [配额] Desktop 在 wait/status 轮询中反复消耗模型配额
**Issue #35259** — 评论 15 | 👍 8  
在 Ultra 与多智能体工作流中，Desktop 仅因等待智能体/轮询终端状态就反复进入模型。在一次重置至 49% 的配额窗口中，纯 wait/status 轮询即占用了约 **19.8% 的原始 token 量**。  
👉 链接: https://github.com/openai/codex/issues/35259

### 🔥 6. [CLI/Bedrock] GPT-5.6 Sol 缺少显式缓存控制
**Issue #37674**（已关闭）— 评论 12 | 👍 12  
通过 Amazon Bedrock 调用 GPT-5.6 Sol 时无法启用显式 prompt caching，导致 cache-write token 开销巨大。关联 #35300。  
👉 链接: https://github.com/openai/codex/issues/37674

### 🔥 7. [远程] Android Remote 大规模失联（Windows 主机）
**Issue #39947** — 评论 9 | 👍 3  
**26.814.5167.0**（Windows）+ Android 端，远程主机显示断连且长任务无法打开。同日还有多条同类报告（#39856、#39974、#39931 等）。  
👉 链接: https://github.com/openai/codex/issues/39947

### 🔥 8. [配额] Pro（20x）账号以 Pro 5x 容量运行
**Issue #38157** — 评论 7 | 👍 5  
官方 API 标记为 `plan_type: "pro"`，但实际 Codex 用量被限制为 Pro 5x 档位。多个 Pro 20x 账号受影响。  
👉 链接: https://github.com/openai/codex/issues/38157

### 🔥 9. [远程] QR 配对成功但会话无法建立（nextConnectionCount=0）
**Issue #39856** — 评论 8 | 👍 0  
**26.818.31338** 版本中，Windows 主机 QR 配对成功，但 Android 客户端无法建立会话，`nextConnectionCount=0`。  
👉 链接: https://github.com/openai/codex/issues/39856

### 🔥 10. [上下文] Desktop 在任务交接后提前停止
**Issue #33398** — 评论 8 | 👍 6  
上下文或任务交接后，Desktop 会进入等待新请求状态而非继续执行现有任务，用户需手动再次触发。  
👉 链接: https://github.com/openai/codex/issues/33398

---

## 重要 PR 进展（Top 10）

### 1. PR #40024 — 统一 exec 尊重细粒度沙箱审批
在统一执行路径中引入共享审批策略检查，使 `require_escalated` 命令在启用 `sandbox_approval` 时正常弹窗、禁用时被拒绝。  
👉 https://github.com/openai/codex/pull/40024

### 2. PR #40021 — 取消工具调用时同步取消 Guardian 审查
将工具取消令牌传播至 Guardian 审批流程，中断工具调用会自动中止其挂起的审查（含 MCP 审批）。  
👉 https://github.com/openai/codex/pull/40021

### 3. PR #40018 — 新增 Browser 与 Computer Use 配置
新增类型化 `browser_use`（历史/按域访问、下载/上传、CDP 策略）与 `computer_use`（macOS bundle ID、Windows AUMID/可执行路径、默认应用）配置。  
👉 https://github.com/openai/codex/pull/40018

### 4. PR #40015 — 加强远程插件缓存一致性
将远程已装/已加载插件快照按账号隔离，账号切换时丢弃在途加载；串行化 bundle 协调与直接安装/卸载流程。  
👉 https://github.com/openai/codex/pull/40015

### 5. PR #40013 — Guardian 异步风险评分复用审查结论
将同步 allow/deny 审查的有界证据保留并传递给 Guardian v2 异步分类器作为可信开发者上下文。  
👉 https://github.com/openai/codex/pull/40013

### 6. PR #40012 — 为 MCP Stop Hooks 保留 Executor 上下文
执行器提供的 stop-hook 调用限定在注册该 hook 的 MCP server 环境中，不匹配则拒绝；并随请求转发 turn 元数据。  
👉 https://github.com/openai/codex/pull/40012

### 7. PR #40007 — App Server 实现 Amazon Bedrock 配置
实现 `account/bedrock/discover`（枚举 AWS profiles 与凭据）与 `account/bedrock/setup`（持久化选定 region/profile）。  
👉 https://github.com/openai/codex/pull/40007

### 8. PR #40005 — 升级命令走同步 Guardian 审查
请求 `sandbox_permissions=require_escalated` 的命令（即使是重试场景之外）也必须经过完整的同步 Guardian 审查。  
👉 https://github.com/openai/codex/pull/40005

### 9. PR #40004 — 权限更新保留托管 deny-read 规则
运行时权限更新不再能削弱托管文件系统 `deny_read` 要求，非法 profile 会被拒绝。  
👉 https://github.com/openai/codex/pull/40004

### 10. PR #39997 — 为 `/copy` 添加响应目标选择器
新增选择器：可复制完整响应或其中任一代码块/引用块，按语言标注并保留空白与原格式。  
👉 https://github.com/openai/codex/pull/39997

---

## 功能需求趋势

1. **远程控制（Remote Control）稳定性** — 目前最集中的痛点。Android/iOS 客户端与 Windows/macOS 主机间存在大量连接建立、任务加载、断连问题，横跨多个版本。
2. **沙箱权限的精细控制与一致性** — 社区持续要求自动化任务与交互式会话遵循同一套沙箱策略，且 `deny_read` 等托管规则不应被运行时更新覆盖。
3. **浏览器与计算机使用（Computer Use）能力扩展** — 新 PR 显示项目正在推进按域访问控制、下载/上传策略、CDP 管控等配置能力，社区关注度较高。
4. **自定义模型供应商体验（Bedrock 等）** — 社区关注显式缓存控制、原生配置向导及配额透明度。
5. **MCP 生态完善** — 包括 OAuth scope 选择、CustomResult 解码、hook 上下文保留与 MCP 审批取消传播。
6. **TUI/CLI 工具可观测性** — 用户希望以 `config.toml` 控制工具调用的显示粒度。

---

## 开发者关注点

1. **Remote Control 在 Windows 主机上的质量问题极为集中** — 短时间内出现 #39947、#39856、#39974、#39931、#39850、#39915、#39916 等多条独立报告，涉及配对成功但无法建连、会话中途断线、任务骨架无法加载等，建议尽快定位。
2. **macOS 桌面的稳定性回归** — Computer Use 进程 V8 OOM 崩溃 + 打开既有会话触发 auth 失效，均指向最近两个桌面版本（26.810/26.814）引入的回归。
3. **配额与用量透明度不足** — 高频反复进入模型消耗配额（#35259）、Pro 20x 租户按 5x 计费（#38157）、配额计数异常加速（#38728）等问题说明用量计量与展示的信任度亟需提升。
4. **沙箱/安全策略一致性** — 自动化任务静默降级为低权限沙箱（#15310）、Windows 上 `deny_read_acl_state.json` 被 NUL 填充导致沙箱永久损坏且重装无效（#35718）等问题直接影响日常可用性。
5. **非 OpenAI 模型提供商的二等公民地位** — MCP CustomResult 解码失败（#29002）、subagent 编排不兼容（#17598）、Bedrock 缓存控制缺失（#37674）等问题显示自定义模型路径的工程成熟度仍有提升空间。

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI 社区动态日报（2026-08-22）

## 今日速览

今日发布 1 个 nightly 版本（v0.56.0-nightly），核心修复涉及符号链接处理和 shell 执行服务代码清理。Issue 与 PR 的高频主题集中在 Agent 行为可靠性（子代理意外挂起、浏览器代理与 Wayland 兼容性）、Auto Memory 系统的安全性与稳健性，以及 PR 自动生成评测管线的持续构建。社区对子代理假成功、shell 假卡死等问题的反馈热度较高，开发者对这些细节体验问题的关注显著。

## 版本发布

**v0.56.0-nightly.20260821.g30573d2e4** ([详情](https://github.com/google-gemini/gemini-cli/releases))

- fix(core): 确保忽略路径处理中符号链接评估的一致性（[#28915](https://github.com/google-gemini/gemini-cli/pull/28915)）
- refactor(core): 从 shellExecutionService 中移除 eslint-disable 和类型断言（[#28862](https://github.com/google-gemini/gemini-cli/pull/28862)）

## 社区热点 Issues

以下为过去 24 小时讨论最活跃的 10 个 Issue：

1. **[#22323] 子代理达到 MAX_TURNS 后被误报为 GOAL 成功，隐藏中断** ([链接](https://github.com/google-gemini/gemini-cli/issues/22323))
   核心问题：`codebase_investigator` 子代理实际因达到最大轮次而中断，却上报 `status: "success"` 和 `Termination Reason: "GOAL"`。这一"假成功"会掩盖真实中断，误导用户判断。获 👍 2，13 条评论。

2. **[#21409] Generalist 代理无限挂起** ([链接](https://github.com/google-gemini/gemini-cli/issues/21409))
   用户报告 `gemini-cli` 在委派给通用代理时（即便是创建文件夹这种简单操作）会无限挂起，最长等待一小时无响应。通过指示模型不使用子代理可绕过。获 👍 8，8 条评论，社区影响面较大。

3. **[#25166] Shell 命令完成后卡在 "Waiting input"** ([链接](https://github.com/google-gemini/gemini-cli/issues/25166))
   简单的 CLI 命令执行完毕但 CLI 仍显示"等待用户输入"并挂起，属于高频交互痛点。获 👍 3，4 条评论。

4. **[#26522] Auto Memory 对低信号会话无限重试** ([链接](https://github.com/google-gemini/gemini-cli/issues/26522))
   内存提取代理决定跳过低信号会话后，该会话仍被标记为未处理并反复出现，需要"停止机制"。5 条评论。

5. **[#21983] 浏览器子代理在 Wayland 下失败** ([链接](https://github.com/google-gemini/gemini-cli/issues/21983))
   在 Wayland 环境下浏览器子代理直接以 GOAL 终止。Linux 用户受此影响面较大。获 👍 1，4 条评论。

6. **[#21968] Gemini 不会主动使用 skills 和子代理** ([链接](https://github.com/google-gemini/gemini-cli/issues/21968))
   社区反馈模型几乎不会自发调用已配置的自定义技能和子代理，即使明确相关也不行，需显式指令才使用。6 条评论。

7. **[#22267] 浏览器代理忽略 settings.json 覆盖（如 maxTurns）** ([链接](https://github.com/google-gemini/gemini-cli/issues/22267))
   全局或项目级 `settings.json` 中配置的参数被浏览器代理忽略，`AgentRegistry` 虽正确合并但代理实际未采用。3 条评论。

8. **[#19987] Gemini CLI 不感知自身能力：CLI 标志、快捷键、自我执行** ([链接](https://github.com/google-gemini/gemini-cli/issues/21432))
   社区希望 CLI 能"自我认知"，可作为自己的专家指南提供准确的工具使用信息。2 条评论。

9. **[#26525] Auto Memory 需要确定性脱敏并减少日志** ([链接](https://github.com/google-gemini/gemini-cli/issues/26525))
   安全担忧：本地转录先进入模型上下文后才进行脱敏指令，存在先发送后脱敏的风险。4 条评论。

10. **[#19873] 利用模型 bash 亲和力：零依赖 OS 沙箱与执行后意图路由** ([链接](https://github.com/google-gemini/gemini-cli/issues/19873))
    长篇功能提案，建议充分利用 Gemini 3 模型原生 bash 操作能力，在不牺牲安全的前提下通过沙箱化提供原生体验。获 👍 1，8 条评论。

## 重要 PR 进展

1. **[#28934] History 回滚与重试提示优化** ([链接](https://github.com/google-gemini/gemini-cli/pull/28934))
   优化工具调用取消和重试提示，防止上下文窗口膨胀、减少 API 请求量并最大化前缀缓存效率。对长会话成本影响显著。

2. **[#28940] A2A 服务：清除新消息轮次中的过期取消错误** ([链接](https://github.com/google-gemini/gemini-cli/pull/28940))
   修复 A2A 服务器中的状态损坏问题，避免取消后用户后续提示立即崩溃 "Execution aborted"。宣称"一劳永逸"解决 GCA 执行停止问题。

3. **[#28935] macOS Seatbelt：隔离 Docker 与容器运行时套接字** ([链接](https://github.com/google-gemini/gemini-cli/pull/28935))
   安全加固：在 macOS Seatbelt 沙箱配置中阻止对容器运行时守护进程 UNIX 套接字、CLI 二进制及 Mach/XPC 服务查询的访问，防止容器逃逸。

4. **[#28827] 修复 401 子串导致的错误认证判断** ([链接](https://github.com/google-gemini/gemini-cli/pull/28827))
   修复 `isAuthenticationError` 将无关值（如包含 401 的端口号）误判为认证失败的问题，回归覆盖拒绝端口、退出码等场景。

5. **[#20238] 缓解杀毒软件对生成的 JSON 错误报告的误报** ([链接](https://github.com/google-gemini/gemini-cli/pull/20238))
   将错误报告从系统临时目录移至 `~/.gemini/tmp/<hash>/error-reports/`，并添加额外文件头以降低杀毒软件误报风险。

6. **[#28951] PR 生成：新增 Cloud Run 任务、Workflow 编排与部署管线** ([链接](https://github.com/google-gemini/gemini-cli/pull/28951))
   为 Caretaker PR 生成管线添加生产级 Cloud Run Job 配置、Cloud Workflow 编排和自动化部署脚本。

7. **[#28952] 新增交互式 Diff 对比可视化生成器** ([链接](https://github.com/google-gemini/gemini-cli/pull/28952))
   引入 HTML diff 可视化生成器，使用 Diff2HTML 和 Highlight.js 渲染代理生成的 PR diff 与 ground-truth 修复的并排对比。

8. **[#28949] 新增 LLM-as-a-Judge Diff 评估模块与评分标准** ([链接](https://github.com/google-gemini/gemini-cli/pull/28949))
   引入基于 LLM 评判器的 diff 评估模块和评分提示标准，用于对生成的 PR diff 与已接受 ground-truth PR 进行自动基准对比。

9. **[#28948] 新增评估套件基础设施与端到端基准运行器** ([链接](https://github.com/google-gemini/gemini-cli/pull/28948))
   引入 PR 生成评估基础设施（eval_suite、eval_orchestrator、eval_config）和端到端连锁流水线运行器，用于在策划的问题上对自动化 PR 代码生成代理进行基准测试。

10. **[#28862] 重构 shellExecutionService：移除 eslint-disable 与类型断言** ([链接](https://github.com/google-gemini/gemini-cli/pull/28862))
    清理 `shellExecutionService.ts` 中的 `eslint-disable` 和不安全类型断言，相关工作在 `fix/mac-pty-resource-leak` 分支上推进。

## 功能需求趋势

- **Agent 评测体系完善**：[#24353](https://github.com/google-gemini/gemini-cli/issues/24353) 关于组件级评测的 Epic 持续活跃，当前已有 76 个行为评测测试并覆盖 6 个 Gemini 模型版本；[#28948](https://github.com/google-gemini/gemini-cli/pull/28948)、[#28949](https://github.com/google-gemini/gemini-cli/pull/28949) 等 PR 正在搭建云端评测基础设施（Cloud Run、E2E 基准运行器、LLM Judge），说明团队正在系统化构建可量化的 Agent 质量验证体系。
- **AST 感知的代码读取与检索**：[#22745](https://github.com/google-gemini/gemini-cli/issues/22745) 及其配套调研 [#22746](https://github.com/google-gemini/gemini-cli/issues/22746) 追踪 AST 感知工具用于精确方法边界读取、减少 token 噪声的可能性，反映出社区的强烈诉求。
- **Agent 行为稳健性与可信度**：多个高赞 Issue（[#22323](https://github.com/google-gemini/gemini-cli/issues/22323)、[#21409](https://github.com/google-gemini/gemini-cli/issues/21409)、[#25166](https://github.com/google-gemini/gemini-cli/issues/25166)）均指向子代理"假成功"、挂起、误报等可信度问题。
- **子代理可视化和调试**：[#22598](https://github.com/google-gemini/gemini-cli/issues/22598) 建议通过 `/chat share` 可见子代理轨迹；[#21763](https://github.com/google-gemini/gemini-cli/issues/21763) 内核建议 `/bug` 报告包含子代理上下文。社区对"黑盒"执行路径的可见性需求强烈。
- **安全与隐私（Auto Memory）**：[#26525](https://github.com/google-gemini/gemini-cli/issues/26525) 要求确定性脱敏与减少日志；[#26523](https://github.com/google-gemini/gemini-cli/issues/26523) 要求隔离无效内存补丁，安全类需求在上周集中爆发。

## 开发者关注点

- **"假成功"误报问题最受关注**：子代理执行达到轮次上限却报告 GOAL 成功（[#22323](https://github.com/google-gemini/gemini-cli/issues/22323)），这种行为会误导用户对 Agent 完成状态的判断，影响信任度，呼吁改进终止理由的透明度。
- **Agent 挂起问题亟待解决**：通用代理在简单操作（如文件夹创建）时无限挂起（[#21409](https://github.com/google-gemini/gemini-cli/issues/21409)），shell 命令执行完毕后仍卡在 "Waiting input"（[#25166](https://github.com/google-gemini/gemini-cli/issues/25166)），这类"卡死"问题直接导致开发者无法使用工具，优先级最高。
- **安全边界与沙箱逃逸风险**：macOS 沙箱 Docker 套接字隔离（[#28935](https://github.com/google-gemini/gemini-cli/pull/28935)）和 401 误判（[#28827](https://github.com/google-gemini/gemini-cli/pull/28827)）揭示了安全相关的细节仍需打磨。
- **配置不生效问题**：settings.json 覆盖被浏览器代理忽略（[#22267](https://github.com/google-gemini/gemini-cli/issues/22267)）、符号链接的 agent 文件无法识别（[#20079](https://github.com/google-gemini/gemini-cli/issues/20079)），开发者对"配置了但没生效"的反馈集中。
- **高频工具缺失**：`/bug` 报告缺失子代理上下文（[#21763](https://github.com/google-gemini/gemini-cli/issues/21763)）、`/chat share` 不可见子代理轨迹（[#22598](https://github.com/google-gemini/gemini-cli/issues/22598)），开发者对调试工具的完备性提出更高要求。

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI 社区动态日报

**日期：2026-08-22**


## 1. 今日速览

今日发布预发布版本 v1.0.81-7，新增崩溃/重启后的会话恢复功能，显著提升意外中断场景下的使用体验。社区讨论热度集中在 BYOK 多模型支持、会话分支、Reasoning effort 兼容性等问题，同时 ACP 模式下的多个行为缺陷（取消语义、后台任务中断）成为今日新增 Issue 的焦点。


## 2. 版本发布

### v1.0.81-7（预发布）

**新增功能：**
- **会话自动恢复**：CLI 启动时会主动提示恢复上次异常退出（崩溃或机器重启）时仍处于打开状态的会话，免去手动逐个恢复终端的麻烦
- **模型信息增强**：`models.list` 现在包含服务端发布的每条模型的 infoMessages 和 warningMessages
- **新增命令**：`copilot app` 用于打开 GitHub 应用相关页面

> 注意：当前会话恢复功能处于预发布阶段，建议在测试环境验证。

🔗 [查看 Release 详情](https://github.com/github/copilot-cli/releases)


## 3. 社区热点 Issues（精选 10 条）

### 🔥 高热度 & 高赞

**#3709 — 允许 /model 在单个会话中切换多个模型（含 BYOK/本地模型）**
- 作者：juancarlosjr97 | 👍 27 | 💬 4
- **为什么重要**：BYOK 模式通过 `COPILOT_MODEL` 将会话锁定在单一模型上，且 `/model` 选择器仅列出 GitHub 托管模型，本地 BYOK 模型不可见。用户不得不在不同模型间切换时反复重启会话，严重阻碍工作流。
- 🔗 [Issue #3709](https://github.com/github/copilot-cli/issues/3709)

**#3282 — 支持在 Copilot CLI 中配置多个 BYOK 模型**
- 作者：shivsant | 👍 26 | 💬 8
- **为什么重要**：与 #3709 高度相关，是目前社区呼声最高的功能需求之一。当前仅支持通过环境变量配置单个 BYOK 模型，TUI 内无法切换，需终止会话并重新设置环境变量，体验割裂。
- 🔗 [Issue #3282](https://github.com/github/copilot-cli/issues/3282)

**#1313 — 会话分支（Session Branching）**
- 作者：lossyrob | 👍 13 | 💬 7
- **为什么重要**：用户希望从当前会话的任意节点派生出新会话，继承完整对话历史，同时保留原会话。适用于探索性开发、方案对比等场景，讨论热度持续较高。
- 🔗 [Issue #1313](https://github.com/github/copilot-cli/issues/1313)

### 🐛 活跃 Bug 反馈

**#4345 — Reasoning effort 'medium' 不适用于模型 'claude-haiku-4.5'**
- 作者：indeherb | 👍 4 | 💬 8
- **问题描述**：当 `copilot_cli_opus_medium_effort_default` 和 `copilot_cli_gpt_5_4_mini_for_explore` 两个功能开关同时启用时，子代理执行期间反复报错 `Reasoning effort 'medium' is not supported`，导致执行失败。
- **影响面**：涉及 feature flag 组合场景下的模型兼容性问题，预计影响部分开启新模型默认策略的用户。
- 🔗 [Issue #4345](https://github.com/github/copilot-cli/issues/4345)

**#4211 — Copilot CLI 无法处理 MCP 结构化响应中的 BigInt**
- 作者：xj-ms | 👍 3 | 💬 5
- **问题描述**：当 MCP 服务器返回大数字时，CLI 报错 `TypeError: Do not know how to serialize a BigInt` 并中止所有进行中的任务。对依赖 MCP 工具链的开发者影响直接。
- 🔗 [Issue #4211](https://github.com/github/copilot-cli/issues/4211)

**#4535 — v1.0.81 预发布版中 `store_memory` 报错 "Instance id is required"**
- 作者：DavidTeju | 💬 4
- **问题描述**：1.0.81 预发布版中，原生 memory writer 被调用时缺少必需的实例 ID，导致 `store_memory` 持续失败。对依赖长期记忆功能的用户影响较大。
- 🔗 [Issue #4535](https://github.com/github/copilot-cli/issues/4535)

**#4533 — 并行子代理生成时终端 UI 停止消费事件（输入+滚动失效）**
- 作者：bikramjitk | 💬 1
- **问题描述**：在 1.0.81-4/-5 预发布版中，当一轮操作生成并行子代理时，TUI 界面事件处理中断，输入与滚动失效，但 Rust 运行时不受影响，子代理继续执行。属于严重的 UI 阻塞问题。
- 🔗 [Issue #4533](https://github.com/github/copilot-cli/issues/4533)

**#4549 — Windows 下每次执行 shell 命令都会闪现 PowerShell 控制台窗口**
- 作者：siramk2022 | 💬 1
- **问题描述**：在 Windows 上，代理每次执行 shell 命令都会弹出可见的 PowerShell 窗口（而非隐藏），任务期间频繁闪烁并抢占焦点，体验极差。
- 🔗 [Issue #4549](https://github.com/github/copilot-cli/issues/4549)

**#4540 — wta.exe 启动失败 0x80070002：路径引号错误导致无法处理含空格的 "Program Files"**
- 作者：pedram6745 | 💬 1
- **问题描述**：Windows 环境下，智能终端组件 `wta.exe` 启动失败，错误码 0x80070002（文件不存在）。原因疑似路径处理时引号位置错误，导致含 "Program Files" 的路径解析失败。影响所有将 Copilot CLI 安装在默认路径下的 Windows 用户。
- 🔗 [Issue #4540](https://github.com/github/copilot-cli/issues/4540)

**#4560 — Model "auto" 始终以 reasoningEffort=null 运行，且拒绝用户配置**
- 作者：douglasjunior | 今日新增
- **问题描述**：选择 `auto` 模型时，所有请求均不携带 reasoning effort 参数（设为 null），且任何手动配置都会被拒绝。影响希望在使用自动路由时控制推理深度的用户。
- 🔗 [Issue #4560](https://github.com/github/copilot-cli/issues/4560)


## 4. 重要 PR 进展

今日无合并或更新的 Pull Requests。


## 5. 功能需求趋势

从近期活跃的 Issue 中，可提炼出以下社区最关注的功能方向：

| 方向 | 代表 Issue | 热度 |
|------|-----------|------|
| **多模型灵活切换（BYOK/本地/托管）** | #3282, #3709 | 🔥🔥🔥 高 |
| **会话管理增强**（分支、恢复、跨目录检索） | #1313, #4554, v1.0.81-7 会话恢复 | 🔥🔥🔥 高 |
| **ACP 协议完善**（取消语义、后台任务、标准化状态） | #4555, #4561 | 🔥🔥 中高（新增） |
| **MCP 兼容性与稳定性**（BigInt 序列化、配置热加载、服务器可用性） | #4211, #4542, #4552, #4562 | 🔥🔥 中高 |
| **交互式体验优化**（内联计划标注、交互式提问工具回归） | #4557, #4563 | 🔥🔥 中 |
| **跨平台体验**（Windows 控制台闪烁、macOS 剪贴板） | #4549, #4540, #4551 | 🔥🔥 中 |
| **模型推理参数配置**（reasoningEffort 控制） | #4345, #4560 | 🔥 中 |


## 6. 开发者关注点

### 高频痛点

1. **BYOK 模型切换困难**：无法在会话内动态切换模型（含本地/第三方模型），需反复重启 CLI，是当前社区最有共鸣的痛点（#3282、#3709 合计 👍 53）。

2. **崩溃/重启后会话丢失**：v1.0.81-7 的会话恢复功能直接回应此痛点，但用户对恢复时机、多会话恢复流程的体验仍有较高期待。

3. **Windows 平台体验明显落后**：控制台窗口闪现（#4549）与 wta.exe 路径解析错误（#4540）均为 Windows 专属问题，Windows 用户的使用体验与 macOS/Linux 差距明显。

4. **MCP 生态稳定性不足**：BigInt 序列化报错、配置热加载失效、服务器不可用被误报为 "waiting on ide"（#4552）等问题，显示 MCP 生态在边界场景下仍不够健壮。

5. **ACP 模式语义不标准**：`session/cancel` 返回 `end_turn` 而非 `cancelled`（#4561）、`session/prompt` 无差别中止后台子代理（#4555），暴露 ACP 实现与协议规范存在偏差，影响依赖 ACP 协议的外部工具集成。

### 社区呼声

- **内联注释/标注**（#4563）：希望在计划评审时可直接在文本上标注修改意见，而非在聊天中重新描述上下文，减少沟通成本。
- **可配置的会话恢复范围**（#4554）：提供开关以在 `/resume` 选择器中展示所有会话（不受 cwd/repo 相关性过滤），兼顾相关性与可见性。
- **交互式提问工具回归**（#4557）：旧版本中 `ask_user` 可显示交互式多选菜单，现版本不再触发，功能回退影响特定工作流。

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI 社区动态日报

**日期：2026年8月22日** | 数据来源：github.com/MoonshotAI/kimi-cli

---

## 今日速览

今日社区热度集中在**一项严重Bug报告**——后台子代理在任务超时或被标记为终止后，仍持续调用LLM造成配额消耗且无法终止（Issue #2615）。此外，一项关于**插件安全与持久化数据的文档改进**PR（#2614）正在评审中。今日无新版本发布。

---

## 社区热点 Issues

### #2615 [Bug] 后台子代理在 TaskStop/超时标记终止后仍持续发起 LLM 调用
**作者**: pc9527zxx | **更新**: 2026-08-21 | **评论**: 0 | 👍: 0

**详情**: 后台子代理在任务及元数据已被标记为`timed_out`或`killed`后，仍可继续发送LLM请求。任务从活跃跟踪列表中消失，导致配额消耗不可见，且`TaskStop`无法再终止该进程。

**重要性**: **★★★★★（极高）**——资源泄漏与权限控制问题。该Bug直接导致用户配额意外消耗，且失控子代理可能产生不可预知的副作用。虽仅有0条评论（可能因刚提交），但按严重程度推测将引发广泛关注。

**链接**: [MoonshotAI/kimi-cli Issue #2615](https://github.com/MoonshotAI/kimi-cli/issues/2615)

> *注：过去24小时仅此1条Issue更新。以下为本次未展示但值得关注的社区趋势参考方向（基于历史数据模式）：*

---

## 重要 PR 进展

### #2614 [docs] 完善插件安全与持久化数据文档
**作者**: QIANLING-0831 | **更新**: 2026-08-21 | 评论: 待确认

**简介**: 该PR旨在完善插件相关文档，明确以下要点：
- 插件工具作为本地子进程运行，拥有当前用户的文件与网络访问权限
- 规范`inject`凭据处理方式，警告用户勿在日志或提交中泄露注入值
- 说明重装插件会替换已安装目录，并建议用户隔离敏感数据

**重要性**: **★★★☆☆（中高）**——安全与合规是开发工具的关键环节。文档的明确化有助于减少因插件滥用导致的权限风险，提升平台信价比。适合在正式运行插件前仔细阅读。

**链接**: [MoonshotAI/kimi-cli PR #2614](https://github.com/MoonshotAI/kimi-cli/pull/2614)

> *注：过去24小时仅此1条PR更新。以下为根据可见信息归纳的趋势分析。*

---

## 功能需求趋势

基于近期Issues与当前代码库演变，社区关注的功能方向包括：

1. **进程生命周期管理与资源控制**（如 #2615）：如何更精准地终止后台子代理、避免隐性资源消耗，是当前稳定性优化的首要方向
2. **插件安全模型强化**：围绕子进程权限隔离、凭据注入的防护性设计，正在成为开发者关注的新热点
3. **可观测性**：任务状态是否真正"终态"、活跃任务跟踪是否透明化，直接关系到用户对配额与运行状态的信任度

---

## 开发者关注点

- **Bug修复优先级**：对"不可见资源消耗"类问题容忍度低——开发者明确希望 TaskStop 能完全终止一切关联进程
- **安全文档需求增强**：在引入插件机制后，用户开始关注权限边界与凭据管理，需官方提供更清晰的安全操作指引
- **状态一致性**：标记为终止的任务与实际行为脱节，容易造成误判，影响自动化流程设计与运维决策

---

*📌 提示：当前数据源仅包含当日更新记录。如需更全面的趋势分析，建议补充历史多日数据交叉对比。*

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode 社区动态日报 — 2026-08-22

## 今日速览

昨日核心动态集中在**稳定性修复**：v1.18.20/v1.18.21 连续发布，重点解决了模型异常终止与网络错误重试问题；社区端围绕"流式模式不可关闭""模型随机中断响应"展开激烈讨论，贡献者 kitlangton 连续提交 4 个高质量修复 PR，覆盖 MCP 错误展示、Provider 部分故障恢复等关键路径。

---

## 版本发布

### v1.18.21
**Core**
- 修复模型报告未知 finish reason 时提前停止响应的问题，确保对话持续进行
- Vertex AI `eu`/`us` 多区域 Gemini 请求现通过 REP 端点路由

**Desktop**
- 修复文件搜索结果在下次搜索加载时被清除的问题

### v1.18.20
- **Core**
  - 失败的子代理工具调用现带可恢复的 `task_id` 呈现
  - 对 `finish_reason: network_error` 的 Provider 响应自动重试
  - 扩展网络错误变体重试覆盖（含 `network-error`、`network_error`）
  - 子代理失败不再静默返回，而是可恢复呈现

---

## 社区热点 Issues（Top 10）

### 1. [#785 如何关闭流式模式？](https://github.com/anomalyco/opencode/issues/785)
- **作者**: SimonWai | **评论**: 31 | 👍: 38
- **重要性**: 当前最热 Issue。Credal OpenAI Proxy 不支持流式，导致服务不可用。关注度持续攀升，已持续一年多未解决，反映代理兼容性是刚需。
- **社区反应**: 大量用户表达同样需求，期待官方提供非流式回退方案。

### 2. [#41469 Session 在空响应时静默停止](https://github.com/anomalyco/opencode/issues/41469)
- **作者**: 3351163616 | **评论**: 10 | 👍: 0
- **重要性**: Provider 返回空 completion（0 tokens）时，opencode 将其视为正常结束，session 无提示退出。与 v1.18.21 修复的 finish reason 问题同源，影响所有依赖不稳定 Provider 的用户。

### 3. [#24153 归档会话无法恢复](https://github.com/anomalyco/opencode/issues/24153)
- **作者**: alohaninja | **评论**: 9 | 👍: 11
- **重要性**: 归档操作不可逆，会话从侧边栏消失。高赞需求，社区期待 unarchive/restore 能力，改善会话管理体验。

### 4. [#34473 opencode 随机中断响应](https://github.com/anomalyco/opencode/issues/34473)
- **作者**: dattarohu-coder | **评论**: 5 | 👍: 3
- **重要性**: v1.17.11 Desktop 上模型随机停止响应，无错误提示，甚至可能出现在思考过程中。与 #41469 类似，凸显 Provider 异常处理不完善的痛点。

### 5. [#14524 模型选择器显示成本](https://github.com/anomalyco/opencode/issues/14524)
- **作者**: ak127a | **评论**: 5 | 👍: 10
- **重要性**: 用户希望在 TUI 模型选择器中直接看到模型价格。高赞功能请求，与成本跟踪 RFC #12377 形成呼应，社区对成本透明的需求强烈。

### 6. [#35376 延迟加载 MCP 工具定义](https://github.com/anomalyco/opencode/issues/35376)
- **作者**: jijoyo | **评论**: 5 | 👍: 0
- **重要性**: 9 个 MCP 服务器时所有工具定义全量注入 system prompt，token 开销巨大。MCP 重度用户的典型性能痛点，社区密切关注。

### 7. [#28492 MaxListenersExceededWarning](https://github.com/anomalyco/opencode/issues/28492)
- **作者**: GoldenStain | **评论**: 7 | 👍: 2
- **重要性**: Web 界面启动后终端打印事件监听器泄漏警告，可能影响长时间运行稳定性，属于基础设施层面的信号。

### 8. [#41847 权限对话框未渲染，应用假死](https://github.com/anomalyco/opencode/issues/41847)
- **作者**: teran-netizen | **评论**: 4 | 👍: 0
- **重要性**: 27 天生成 3270 个权限提示但用户从未看到，后端阻塞在不可见的对话框上导致应用"冻结"。权限系统存在严重的 UI 层缺陷。

### 9. [#43850 ChatGPT Plus OAuth 失败](https://github.com/anomalyco/opencode/issues/43850)
- **作者**: KeyandBoy | **评论**: 3 | 👍: 0
- **重要性**: v1.18.20 Desktop 上 ChatGPT Plus OAuth 报"Token exchange failed: 403"。最新版本引入的认证回归，影响 Plus 订阅用户。

### 10. [#43983 通过 API Key 暴露 OpenCode Go 使用历史](https://github.com/anomalyco/opencode/issues/43983)
- **作者**: vulturetone | **评论**: 5 | 👍: 0
- **重要性**: 用户希望用 API Key 认证的方式查询 OpenCode Go 用量。用量透明化需求，与成本跟踪趋势一致。

---

## 重要 PR 进展（Top 10）

### 1. [#44002 自动恢复 Provider 部分故障](https://github.com/anomalyco/opencode/pull/44002)
- **作者**: kitlangton
- **内容**: Provider 输出部分内容后出现可重试的内部错误（且未执行工具调用），自动重试恢复。直接回应当前最热的响应中断问题。

### 2. [#44001 Fork 会话不继承运行中的 Shell](https://github.com/anomalyco/opencode/pull/44001)
- **作者**: kitlangton
- **内容**: 修复 fork 会话复制了仍在父会话运行的 shell 消息，避免子会话出现无意义的状态残留。

### 3. [#43999 按 _tag 而非 instanceof 匹配项目复制错误](https://github.com/anomalyco/opencode/pull/43999)
- **作者**: miladsoroush
- **内容**: 解决核心库重复加载时 instanceof 类身份比较失效的问题，关闭 #43995。

### 4. [#44003 收敛 MCP 侧边栏错误展示](https://github.com/anomalyco/opencode/pull/44003)
- **作者**: kitlangton
- **内容**: MCP 连接失败信息改为紧凑可扫描格式，服务器名称优雅截断，状态语义化右对齐。

### 5. [#44000 稳定生成的契约名称](https://github.com/anomalyco/opencode/pull/44000)
- **作者**: kitlangton
- **内容**: 生成的 TypeScript/OpenAPI 名称基于契约身份而非遍历位置，提升代码生成稳定性。

### 6. [#43915 限制 textVerbosity 注入范围](https://github.com/anomalyco/opencode/pull/43915)
- **作者**: joelstucki-taulia
- **内容**: 修复 `gpt-5.x` 模型经 openai-compatible Provider（如 LiteLLM）转发到 Bedrock 时注入 `textVerbosity: low` 导致请求失败的问题，关闭 #43911。

### 7. [#43844 拒绝缺失项目目录的请求](https://github.com/anomalyco/opencode/pull/43844)
- **作者**: shijiatongxue
- **内容**: 项目目录被删除/移动时，HTTP 中间件检查解码后的项目路径，返回明确错误而非静默异常，修复 #39471。

### 8. [#43998 Windows Git 查找旁路](https://github.com/anomalyco/opencode/pull/43998)
- **作者**: opencode-agent[bot]
- **内容**: Windows 上解析 Git 绝对路径并直接传递给子进程，绕过 `cross-spawn` 查找，规避 PATH 解析问题。

### 9. [#43775 Windows Git 查找旁路（早前版本）](https://github.com/anomalyco/opencode/pull/43775)
- **作者**: opencode-agent[bot]
- **内容**: 与 #43998 同主题，使用原生 `child_process.spawn` 执行绝对 `.exe`/`.com` 命令，保留非 Windows 动态 PATH 解析。已关闭，可能被 #43998 取代。

### 10. [#38138 校验缓存尾部数值合法性](https://github.com/anomalyco/opencode/pull/38138)
- **作者**: luojiyin1987
- **内容**: `messages.tail` 接受小数和负数，可产生非法索引。Schema 增加限制，提升配置健壮性。

---

## 功能需求趋势

1. **成本透明化**：#12377（成本跟踪架构 RFC）、#14524（模型选择器显示成本）、#43983（用量 API）共同指向用户对成本可视化的强烈需求，且已形成体系化诉求。
2. **非流式模式支持**：#785 长期高热度，代理/网关类 Provider 不支持流式场景下 opencode 需回退方案。
3. **会话管理增强**：#24153 归档恢复功能呼声高，配合 #36232（Web UI 版本号滞后），说明会话管理体验是用户日常痛点。
4. **MCP 体验优化**：#35376 延迟加载工具定义，反映 MCP 多服务器场景下 token 开销过大，需要精细化的按需加载。
5. **新模型/新平台适配**：#43829/#43805（DeepSeek 模型缺失）、#33219（FreeBSD 支持），体现跨平台与新模型接入的持续关注。

---

## 开发者关注点

- **响应中断问题集中爆发**：#34473、#41469 及相关讨论表明，Provider 异常处理是当前最大的稳定性瓶颈。v1.18.20/21 连续两个版本修复网络错误重试，但"空响应静默停止""未知 finish reason"等场景仍需更完善的兜底策略。
- **Windows 平台问题频发**：#30906（UI 冻结）、#43850（OAuth 失败）、#43775/#43998（Git 查找），Windows 用户体验待系统化改善。
- **MCP 工具定义体积焦虑**：多 MCP 服务器场景下 token 消耗成为实际痛点，延迟加载与命名空间优化（#36196）是高频优化方向。
- **错误可见性不足**：#41847 权限对话框不可见、#42657 TUI 高 CPU 卡顿、#34473 无错误静默停止，开发者对"失败可诊断"的要求不断提高。
- **自动化质量门禁显现**：今日大量标注 `automated-pr-cleanup` 的 PR 关闭，说明仓库已引入自动清理机制，但其中包含的实质性修复（如 #38138、#43775）仍需人工复核后合并，社区应对此保持关注。

---

*数据来源：[github.com/anomalyco/opencode](https://github.com/anomalyco/opencode) | 统计窗口：2026-08-21 ~ 2026-08-22*

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

# Pi 社区动态日报 — 2026-08-22

> 数据来源：github.com/badlogic/pi-mono（关注仓库已迁移至 earendil-works/pi）

---

## 今日速览

今日社区核心关注点集中在**压缩（compaction）机制缺陷**与**键盘协议兼容性**两大方向：auto-compaction 在超长会话中触发失效的 bug 获得最高关注度（19 评论、17 👍），同时 Kitty 终端协议下 Backspace 键行为异常已形成系列 Issue。PR 侧则有多项针对 ```coding-agent``` 会话重建、扩展加载失败恢复的实质性修复，以及 xAI Grok Build 模型的 reasoning 参数兼容性修复。另有 3 个 SDK 相关功能提案（块展开默认态、黏性头部、滚轮灵敏度）今日集中提交，值得关注。

---

## 社区热点 Issues（Top 10）

### 1. auto-compaction 在上下文超过 100% 后从不触发，直至 provider 溢出
🔗 [Issue #6879](https://github.com/earendil-works/pi/issues/6879)

> 19 评论 | 17 👍 | 状态：OPEN

**核心问题**：在 gpt-5.6-sol 上的一次 agentic 回合运行超过 2 小时，footer 越过压缩阈值后继续增长，直至 API 在 373k tokens 处拒绝请求，压缩才被触发。作者建议在每个 agent 步骤后检查上下文水位。

**重要性**：这是目前社区反应最激烈的问题，直接关系到长时间 agentic 会话的稳定性，且 373k tokens 才触发意味着用户可能产生大量额外 API 费用。

---

### 2. Backspace 和 Delete 键在 Windows Terminal 中工作异常
🔗 [Issue #2733](https://github.com/earendil-works/pi/issues/2733)

> 11 评论 | 1 👍 | 状态：CLOSED

**核心问题**：从 0.62.0 升级到 0.64.0 后，Windows Terminal 中 Backspace/Delete 行为异常。虽已关闭，但长期存在且影响 Windows 核心用户体验。

---

### 3. Kitty 终端协议下 Backspace 删除 2 个字符（release events 未过滤）
🔗 [Issue #7130](https://github.com/earendil-works/pi/issues/7130)

> 9 评论 | 1 👍 | 状态：OPEN

**核心问题**：Kitty 键盘协议下 Backspace 一次删除两个字符，与 #8442（herdr pane 中 Backspace 被忽略）形成同一协议的两面问题。终端兼容性仍是 TUI 层的持续痛点。

---

### 4. 压缩功能应支持独立的 thinking level/model 配置
🔗 [Issue #7553](https://github.com/earendil-works/pi/issues/7553)

> 8 评论 | 状态：OPEN（inprogress）

**核心问题**：自动/手动压缩无条件复用会话当前的 thinking level。对使用 reasoning 模型的用户，摘要的思考预算与正常对话无法分离。与 #8133（按模型配置压缩参数）方向一致，属压缩体系系统性改进的一部分。

---

### 5. openai-responses 实现缺少 Anthropic 风格 prompt-caching 支持
🔗 [Issue #7995](https://github.com/earendil-works/pi/issues/7995)

> 7 评论 | 状态：OPEN（inprogress）

**核心问题**：基于 870 次试验的 benchmark，`openai-responses` 实现无 Anthropic 风格 `cache_control` 支持，经 OpenRouter 使用 Claude 时带来 **2.5 倍实测成本惩罚**。直接影响用户成本，高优。

---

### 6. Agent 在通过正向代理连接纯 HTTP provider 时，首次工具调用后停止
🔗 [Issue #8134](https://github.com/earendil-works/pi/issues/8134)

> 4 评论 | 状态：OPEN

**核心问题**：自 0.84.0 起，通过 `HTTP_PROXY` 访问 `http://` 明文 baseUrl 时，首个工具调用成功但后续请求挂起。代理场景下的一处回归 bug，影响自托管用户。

---

### 7. 按模型配置压缩参数
🔗 [Issue #8133](https://github.com/earendil-works/pi/issues/8133)

> 3 评论 | 3 👍 | 状态：OPEN

**核心问题**：提出 `compaction.profiles` 映射表（按 model id 覆盖全局默认值）。与 #7553 相互补充，合起来构成"压缩行为可配置化"的完整图景，社区关注度稳定上升。

---

### 8. 长期会话崩溃：JavaScript heap out of memory (SIGABRT)
🔗 [Issue #2644](https://github.com/earendil-works/pi/issues/2644)

> 4 评论 | 状态：CLOSED

**核心问题**：约 30 分钟高强度工具使用后触发 Node.js OOM。已关闭，但在 #6879 的讨论中仍被引用为长会话稳定性问题的关联佐证。

---

### 9. Gemini 3.7 Flash 拒绝 `/tree` 分支摘要（MINIMAL thinking 不受支持）
🔗 [Issue #8456](https://github.com/earendil-works/pi/issues/8456)

> 3 评论 | 状态：CLOSED（untriaged）

**核心问题**：内置分支摘要请求未附带 `reasoning` 参数，Google adapter 侧默认行为导致 Gemini 3.7 Flash 直接报错。多模型适配层的一致性问题。

---

### 10. 全屏 TUI 工具输出块应支持独立的鼠标展开/折叠
🔗 [Issue #8344](https://github.com/earendil-works/pi/issues/8344)

> 4 评论 | 状态：CLOSED

**核心问题**：长会话中大量工具输出块，希望通过点击单个块独立展开/折叠，而非仅依赖 `Ctrl+O` 全局切换。同一时间段内 SDK 侧也提交了"按块类型配置默认展开态"的提案（#8448），TUI 可展开性正在成为社区关注的功能方向。

---

## 重要 PR 进展（Top 7）

### 1. fix(tui): 保留全屏双击选词中的 `/` 和 `-` 字符
🔗 [PR #8459](https://github.com/earendil-works/pi/pull/8459)

**内容**：修复 `Intl.Segmenter` 在双击选词时将 `/` 和 `-` 视为边界的问题——此前双击路径 `extensions/starline/fixed-editor/compositor.ts` 只能选中单个组件。**状态**：CLOSED。

---

### 2. feat(interactive-mode): 实验性 flag 下 /share 改用 Radius artifacts
🔗 [PR #8443](https://github.com/earendil-works/pi/pull/8443)

**内容**：`/share` 命令在 experimental flag 下改用 Radius artifacts 替代 gist；未登录时触发认证流程后生成 artifact。**状态**：CLOSED。

---

### 3. feat(coding-agent): 增加 --exclude-extensions 跳过指定扩展
🔗 [PR #8433](https://github.com/earendil-works/pi/pull/8433)

**内容**：解决扩展加载"全有或全无"的问题——此前只能全量自动发现或 `--no-extensions`，现在可以表达"我的正常扩展集，减去这几个"。第三方扩展无法自守卫的痛点得到解决。**状态**：CLOSED。

---

### 4. fix(coding-agent): 重建会话上下文时重新配对工具结果
🔗 [PR #8428](https://github.com/earendil-works/pi/pull/8428)

**内容**：修复 #8166 的会话损坏 bug——当从持久化会话树重建上下文（resume、compaction、分支导航）时，工具结果与发出工具调用的 assistant 消息重新配对，孤立结果被正确清除。**状态**：CLOSED。

---

### 5. fix(coding-agent): 丢弃失败的扩展工厂状态
🔗 [PR #8424](https://github.com/earendil-works/pi/pull/8424)

**内容**：当扩展工厂加载失败（throw 或 reject）时，丢弃已暂存的 flag 默认值和 provider 操作、移除事件总线监听器，并使后续对该失败工厂 API 对象的调用被拒绝。**状态**：OPEN。

---

### 6. fix(ai): xAI Grok Build 模型省略 reasoning effort 参数
🔗 [PR #8422](https://github.com/earendil-works/pi/pull/8422)

**内容**：xAI 拒绝包含 `reasoning.effort` 的 `grok-build-0.1` 请求。Pi 在显式设置 reasoning level 时总会附带该字段，默认路径下也可能发送 `"none"` 导致 HTTP 400。通过添加 Responses 兼容性 flag 修复。**状态**：OPEN。

---

### 7. feat: /exit 作为 /quit 的别名
🔗 [PR #4537](https://github.com/earendil-works/pi/pull/4537)

**内容**：与 codex、claude、opencode 等主流 agent 保持一致，为 `/quit` 添加 `/exit` 别名。**状态**：CLOSED（对应 Issue #6193 已关闭）。

---

## 功能需求趋势

从今日更新的 Issues 中可提炼出以下社区关注方向：

### 1. 压缩（Compaction）体系系统化改进
- **可配置性**：按模型配置压缩参数（#8133）、独立的 thinking level/model（#7553）、显式全跨度手动压缩模式 `/compact --all`（#8453）
- **可靠性**：auto-compaction 触发逻辑需根本性修复（#6879），默认压缩 prompt 需提升连续状态保真度（#8452）

### 2. 终端/键盘协议兼容性（持续痛点）
- Kitty 键盘协议相关：Backspace 多删（#7130）、legacy 0x7f 被忽略（#8442）
- Termux 键盘resize 豁免应推广至所有移动客户端（#8421）

### 3. TUI 可展开性与滚动体验
- 按块类型配置默认展开/折叠态（#8448）
- 滚动 transcript 中的黏性/固定头部组件（#8447）
- 滚轮滚动灵敏度可配置（#8446，含 per-OS 默认值差异考量）
- 全屏模式独立鼠标展开/折叠（#8344）、`fullscreenWheelScrollLines` 设置（#8370）

### 4. 新 Provider 支持持续活跃
- **Parasail.io**（#8450）：Kimi K3、GLM5.2、DeepSeek V4 Pro/Flash、MiniMax M3
- **SiliconFlow**（#4742）：双端点（国际 + 中国），OpenAI 兼容 API
- **Amazon Bedrock**：AgentCore MMDS 凭据支持（#8455）

### 5. Provider 适配层一致性问题
- OpenRouter reasoning-mandatory 模型：不应在后台调用中显式发送 `reasoning: {effort:"none"}`（#8454）
- 缓存支持差异：openai-responses 缺少 Anthropic 风格 cache_control（#7995）

---

## 开发者关注点

### 高频痛点
1. **长会话稳定性和成本控制**：OOM（#2644）与压缩失效（#6879）直接导致长任务中断或 API 费用激增，是当前最集中的痛点。
2. **终端兼容性回归**：Windows Terminal 与 Kitty 下输入键异常反复出现，跨终端测试覆盖需要加强。
3. **代理/网络边界场景**：通过正向代理访问明文 HTTP provider 时挂起（#8134），影响自托管和小型部署用户。

### 高频需求
1. **压缩行为可配置化**：希望将压缩的 thinking level、触发阈值、目标模型均纳入配置，并支持按模型区分。
2. **SDK 层 TUI 定制能力**：今日集中出现 4 个 SDK 提案（#8446-#8448、#8344），关注块展开默认态、黏性头部、滚轮灵敏度等面向第三方扩展开发者的能力开放。
3. **Provider 成本优化**：prompt-caching 支持差异带来的 2.5 倍成本差距（#7995）引发关注，多 provider 适配时的成本对称性需要保证。
4. **技能/模板调用方式统一**：技能应可在句中被调用（#8457），与 prompt 模板的调用方式保持一致。

### 较低优先级但值得注意
- RPC 模式的 provider 登录操作缺失（#8451），`/login` 仅限交互模式。
- 可重试 TLS/证书传输错误分类（#8458），提升弱网络环境下的鲁棒性。
- `app.models.save` 绑定被 `/model` 和 `/thinking` 选择器忽略（#8425），自定义键位绑定的行为一致性待修复。

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code 社区动态日报

**日期：2026-08-22** | **数据来源：** [github.com/QwenLM/qwen-code](https://github.com/QwenLM/qwen-code)


## 今日速览

今日社区最核心的动向是**安全与CI/CD加固**：围绕代码审查（review）流水线的安全边界问题（#9556、#9089）持续发酵，同时新增一个导致所有 CI 失败的依赖 CVE 高危告警（#9699）。功能需求方面，社区对 **daemon 会话恢复的完整性**（模型归属、HITL 恢复等，#9686、#9664、#9688）和多款新模型/平台支持（Kimi、小米 MiMo、钉钉）呼声集中。发布方面，今日发布了 v0.21.14-nightly 版本，并有两项 SWE-bench 基准验证成功（Full-500 与 Smoke）。


## 版本发布

### v0.21.14-nightly.20260821.9f2342d323
[查看 Release](https://github.com/QwenLM/qwen-code/releases)

- **核心变更**：`feat(review)` - 当审查循环无法收敛时，向作者说明原因（PR #9461）。
- **CI 修复**：停止某个 fallback 行为（具体内容见 commit）。

> 另有两项基准验证报告今晨回传（对应版本 ref: v0.21.15）：
> - **dsw-eas-full-20260821-r1**：SWE-bench Verified 500 + Terminal-Bench 2.0 89 全量跑测 **通过**。
> - **dsw-eas-tb-smoke-20260821-r1**：SWE + Terminal-Bench 端到端冒烟测试 **通过**。


## 社区热点 Issues

*精选 10 条过去 24 小时更新最频繁或影响面最大的 Issue（按评论热度与优先级综合排序）。*

### 1. CI 依赖 CVE 审计全量失败（P1，新增）
- **#9699** [OPEN] [priority/P1, type/bug, category/security, scope/ci-cd]
- 自 8-21 起，`npm audit` 步骤（`--audit-level=high`）在任何分支、任何作者下**必然失败**，报告 `1 low / 6 moderate / 1 high` 共 8 个漏洞。CI 已实质红屏，可能阻塞所有合入流程——**建议今日优先跟进**。
- [查看 Issue](https://github.com/QwenLM/qwen-code/issues/9699)

### 2. 代码审查流水线是否应继续以调用者身份执行代码（安全讨论）
- **#9556** [OPEN] [category/security, scope/ci-cd, need-discussion]
- 源自 #9221 二十轮审查后仍未解决的安全前提：审查进程以自身用户身份、在自身工作树内执行代码。该能力由更早的步骤授予，无法由 #9221 移除。社区讨论集中于 **runner 级隔离策略**。这是当前 review 安全加固方向的源头问题，已累积 7 条评论。
- [查看 Issue](https://github.com/QwenLM/qwen-code/issues/9556)

### 3. 安全自动修复：PAT 任务与不可信分支共享主机（P1，已关闭）
- **#9089** [CLOSED] [priority/P1, type/bug, category/security, scope/github-actions]
- 要求对携带 PAT 的 autofix 任务进行 **runner 级隔离**。PR #8961 已加固持久化池攻击面，但此问题被判定无法在 Actions 步骤内关闭，需上层架构决策。当前已关闭（关联到 #9556 的讨论中）。
- [查看 Issue](https://github.com/QwenLM/qwen-code/issues/9089)

### 4. MCP Windows 启动时连接关闭（即使未激活）
- **#9693** [OPEN] [status/need-retesting, priority/P2, type/bug, category/integration, scope/mcp]
- Qwen Desktop 在 Windows 上对 STDIO 传输的 MCP 服务器报 `MCP -32000: Connection closed`，且**在未激活 MCP 时也会出现**。与 #9675（服务间歇性失联）并列为 Windows 平台 MCP 稳定性的核心投诉。已进入待重测阶段。
- [查看 Issue](https://github.com/QwenLM/qwen-code/issues/9693)

### 5. 主会话（项目经理） + Subagent 执行中途崩溃
- **#5180** [OPEN] [priority/P2, type/bug, category/core, scope/token-management]
- 中文用户报告：主会话派发任务后，subagent 执行到一半崩溃，导致 12 小时长会话失败。关联长上下文、多智能体协作稳定性，已累积 7 条评论，是**中文社区高频痛点**。
- [查看 Issue](https://github.com/QwenLM/qwen-code/issues/5180)

### 6. Windows 终端 IME 中文输入法候选框对比度过低（新增）
- **#9666** [OPEN] [priority/P2, type/bug, category/ui, scope/windows, welcome-pr]
- 在 Win10 + PowerShell 深色背景下，微软拼音候选词被半透明方框包围、文字几乎不可辨认。已标记 `welcome-pr`（欢迎开发者提交修复）。
- [查看 Issue](https://github.com/QwenLM/qwen-code/issues/9666) 

### 7. 自动模式权限分类器在提供方不稳定时“失败开放”（回归 #7331，新增）
- **#9639** [OPEN] [status/need-information, priority/P2, type/bug, category/security]
- 分类器在 provider 不可用时可能 fail-open，导致本应拦截的快速权限检查被放行。8-17 与 8-18 两次故障窗口已造成具体影响。这是**安全与可用性权衡**的重要讨论点。
- [查看 Issue](https://github.com/QwenLM/qwen-code/issues/9639)

### 8. daemon：归档活动会话可造成 active + archived 冲突
- **#9688** [OPEN] [priority/P2, type/bug, category/cli, scope/session-management, daemon]
- 归档会话时若写入方仍在运行，会重新创建 `chats/<session-id>.jsonl`，导致**同一会话同时存在活动与归档两份副本**，Web UI 状态错乱。
- [查看 Issue](https://github.com/QwenLM/qwen-code/issues/9688)

### 9. 公共 Git 扩展安装要求 Git ≥ 2.37，Ubuntu 22.04 仅提供 2.34.1
- **#8993** [CLOSED] [priority/P2, type/bug, category/platform, scope/linux]
- 已关闭——对应的修复在 PR **#9690** 中落地（已合并，见下文），实现了针对旧版 Git 的安全回退下载方案。该闭环值得关注。
- [查看 Issue](https://github.com/QwenLM/qwen-code/issues/8993)

### 10. 遗留审查结论：autofix 容器门控的延期问题
- **#9524** [OPEN] [priority/P3, status/on-hold, type/bug, category/security, scope/ci-cd]
- PR #9214（autofix 在临时容器中运行验证门禁）被冻结；其验证结论在第 11 轮审查中仍有未决项。属于 autofix 安全加固的**存量技术债**。
- [查看 Issue](https://github.com/QwenLM/qwen-code/issues/9524)


## 重要 PR 进展

*精选 10 条当前最值得关注的 PR。*

### 1. 修复：支持旧版 Git 安装公共 GitHub 扩展 ✅（新合并）
- **#9690** [OPEN? 已合入] `fix(core): support public GitHub extensions with older Git`
- 针对 #8993：当系统 Git < 2.37 时，将 GitHub ref 解析为不可变 commit，再走已有公开扩展下载通道（不降级 Git 传输安全）。**即将（或已）关闭 #8993**。
- [查看 PR](https://github.com/QwenLM/qwen-code/pull/9690)

### 2. 功能：跨会话消息（带入站门禁）
- **#9576** [OPEN] [autofix/takeover] `feat(core): accept cross-session messages behind an inbound gate`
- 实现同机 Qwen Code 会话间通信：会话绑定 UNIX socket，接收换行分隔 JSON 帧，在策略允许时注入本会话输入队列（标记为非用户消息）。 是**多会话协作**的基础能力。
- [查看 PR](https://github.com/QwenLM/qwen-code/pull/9576)

### 3. 功能：钉钉（DingTalk Workspace）渠道
- **#9394** [OPEN] [autofix/needs-human] `feat(channels): add DingTalk Workspace channel`
- 复用已认证的 DWS CLI 配置，支持私聊、@提及、文档动态通知、原生待办等；包含 source-scoped sessions（保留发起人上下文）。 平台覆盖明显向国内 IM/协作工具延展。
- [查看 PR](https://github.com/QwenLM/qwen-code/pull/9394)

### 4. 功能：`qwen review capture-tui` —— 渲染类问题直接“给像素证据”
- **#9273** [OPEN] [autofix/takeover] `feat(review): capture-tui — rendering claims get pixels, not prose`
- 在**私有 tmux server** 中运行命令，捕获 pane 文本（`<out>.ans`），并在有 `freeze` 时渲染 PNG。用于验证 TUI 渲染类改动，不再靠代码推断。
- [查看 PR](https://github.com/QwenLM/qwen-code/pull/9273)

### 5. 功能：审查循环持续不收敛时的风险提示（land-with-residual-risk）
- **#9526** [OPEN] [autofix/takeover] `feat(review): add the persistently-critical convergence advisory`
- 当 telemetry 证明 Critical 级 finding 连续两轮未迁移，且在 posting volume 窗口内时，在审查结论中强制附加“带残存风险合入”的信息——将 #9461 的诊断升级为**可执行的出口规则**。
- [查看 PR](https://github.com/QwenLM/qwen-code/pull/9526)

### 6. 功能：审查时要求每个修复附带其测试，并裁决非收敛问题
- **#9596** [OPEN] [autofix/takeover] `feat(review): ask each fix for its test, and rule on non-convergence`
- Finding 现在必须携带“自身修复的验收标准”；同时新增“非收敛裁决”机制。与 #9623（机器可读收敛诊断）、#9526 共同构成 review 3.0 的收敛治理组。
- [查看 PR](https://github.com/QwenLM/qwen-code/pull/9596)

### 7. 重构：将 autofix push-and-report 逻辑移出 workflow 文件
- **#9653** [OPEN] [autofix/takeover] `refactor(autofix): move the push-and-report body out of the workflow file`
- 将 `qwen-autofix.yml` 中的 `Push and report` 步骤迁移到 `.github/scripts/autofix-push-and-report.sh`（保持字节级一致）。降低 workflow 维护成本与审计难度。
- [查看 PR](https://github.com/QwenLM/qwen-code/pull/9653)

### 8. 功能：新增 Kimi 与小米 MiMo 提供商
- **#8368** [OPEN] [autofix/needs-human] `feat(auth): add Kimi and Xiaomi MiMo providers`
- `/auth` 新增 Kimi（Coding Plan / 国内 / 国际 API Key）与 Xiaomi MiMo（按量付费 + 中国 / 新加坡 / 国际）预设。**国产模型支持持续扩展中**。
- [查看 PR](https://github.com/QwenLM/qwen-code/pull/8368)

### 9. 功能：Web Shell 实验性 Session Workflow 驾驶舱
- **#8583** [OPEN] `feat(web-shell): add an experimental session workflow cockpit`
- 在 WebShell 中打通 plan 捕获 → 基于修订的审批 → 转录投影 → Agent 执行全链路，并复用现有依赖图增加 Agent 活动视图。多智能体执行过程的**可视化与可控性**进一步增强。
- [查看 PR](https://github.com/QwenLM/qwen-code/pull/8583)

### 10. 修复：修复回、补 Aone 残差 —— composeUrl、测试计划路由、a1 版本下限
- **#9624** [OPEN] [autofix/takeover] `feat(review): close Aone residual gaps`
- Aone Code 平台支持的三项补全：真实 MR 链接（而非纯文本 “Posted:”）、测试计划路由、Aone a1 版本号下限校验。与 #9618（增量缓存）共同指向**Aone 集成成熟度提升**。
- [查看 PR](https://github.com/QwenLM/qwen-code/pull/9624)


## 功能需求趋势

综合近 24 小时 Issues 与 PR 观察，社区需求集中于以下方向：

1. **DAO（Daemon 守护进程）体验补全（明显上升趋势）**
   - 代表：#9686（按会话恢复上次使用的模型）、#9664（恢复未回答的 `ask_user_question` HITL）、#9688（归档与活动会话冲突）。说明后台常驻场景已进入实用阶段，用户开始要求**会话级状态完整还原**。

2. **模型与平台扩展支持**
   - 新模型/Provider：Kimi、小米 MiMo（#8368）；阿里内部平台 Aone Code 的 CR 支持强化（#9624、#9618）；新 IM 渠道钉钉（#9394）。

3. **多会话/多智能体协作基础设施**
   - 跨会话消息传递（#9576）、Teammate 消息的 tool-round 边界投递（#9638）、主-子 Agent 协作稳定性（#5180）——从“能用”走向“好用”。

4. **审查（review）与 CI 的自动化治理与安全边界**
   - review 循环收敛诊断与裁决（#9596、#9526、#9623）、runner 级隔离与权限最小化（#9556）、autofix 脚本去 workflow 化（#9653）。这是目前**投入最密集、讨论最深**的方向。


## 开发者关注点（痛点 / 高频反馈）

1. **Windows 平台体验仍是短板：**
   - IME 候选词框对比度过低（#9666）、MCP 连接在 Windows 上假死或失联（#9693、#9675）——Windows 用户是当前负面反馈的主要来源，建议优先倾斜测试资源。

2. **CI 红灯影响日常开发：**
   - CVE 审计步骤全量失败（#9699）直接阻塞合入信心；另有 review 相关 CI 反复调优导致的“老问题新修法”（#9524 等），均在消耗社区信任。开发者期望**更稳定的 CI 基线**。

3. **长会话 / 多任务可靠性：**
   - 12 小时主-子会话中途崩溃（#5180）、归档冲突（#9688）、Traffic 展示与加载状态不匹配（#9487）——在长时运行或多步任务中，UI 状态一致性与进程稳定性仍不达标。

4. **安全策略的双刃剑：**
   - 权限分类器 fail-open 风险（#9639）、Plan 模式只读命令白名单扩展（#9694）——社区在安全加固之外，也在寻求**更细粒度可控的策略配置**，而非一刀切。

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

# DeepSeek TUI 社区动态日报

**日期：2026-08-22** | 数据来源：[Hmbown/DeepSeek-TUI](https://github.com/Hmbown/DeepSeek-TUI)

> 注：根据仓库当前结构，核心项目已更名为 **CodeWhale**（原 DeepSeek-TUI），以下动态均来自 CodeWhale 仓库。

---

## 1. 今日速览

今日社区动态集中在 **"监督式运行"（Supervised Operation）** 主题——M-Maciej 提交的 Issue 集群（#5528-#5534）与大型 PR #5535 共同构建了外部监督长时会话的完整基础设施（生命周期事件、控制套接字、`/relaunch` 与节奏修复）。与此同时，**CodeWhale TUI 的 crate 分解重构（EPIC-005）** 持续推进，多个工具组 PR 已提交。依赖更新方面，dependabot 密集提交了 5 个 Rust 依赖升级 PR。

---

## 2. 版本发布

过去 24 小时无新 Release。

---

## 3. 社区热点 Issues（10 条）

### 🔥 监督式运行基础设施（M-Maciej 系列，8/21 集中提交）

**#5533 [enhancement] 监督式运行的控制面——每会话控制套接字**
- **摘要**：M-Maciej 在 herdr（终端多路复用包装器）、自动化测试框架和 CI 场景下运行 codewhale 会话，需要每会话控制套接字（消息/中断/重启/状态查询），以及 `RuntimeBackendKind::External` 运行时后端。
- **价值**：为无人值守/远程监督场景提供程序化控制通道，是自动化运维的基础设施。
- [查看 Issue](https://github.com/Hmbown/CodeWhale/issues/5533)

**#5531 [enhancement] 本地生命周期事件 Outbox（JSONL + Webhook）**
- **摘要**：长时会话在夜间无人值守运行时，需要 `turn_stalled` / `turn_failed` 等事件通过 JSONL 文件或 Webhook 通知外部监督者。
- **价值**：将 TUI 内部状态机事件暴露为机器可读格式，赋能告警和自动化恢复。
- [查看 Issue](https://github.com/Hmbown/CodeWhale/issues/5531)

**#5532 [enhancement] `/relaunch` 命令——将运行中会话切换到当前二进制**
- **摘要**：`/update` 安装新二进制后要求用户手动重启，但 CodeWhale 缺乏自执行/重启模式。M-Maciej 提出 `/relaunch` 使会话无缝切换到新版本。
- **价值**：消除版本升级的断崖式体验，支撑长时间运行的代理会话。
- [查看 Issue](https://github.com/Hmbown/CodeWhale/issues/5532)

**#5534 [bug] 目标延续节奏的静默期被绕过**
- **摘要**：`#5508` 提交的 `[goal] continuation_delay_seconds` 配置在 "轮内调度路径"（resumed/CLI 会话）上被绕过，导致连续 pass 立即触发而非等待配置的延迟。
- **价值**：修复可能引发无限快速循环的行为缺陷，保护 API 配额和系统资源。
- [查看 Issue](https://github.com/Hmbown/CodeWhale/issues/5534)

### 🚨 工作流可靠性问题（Hmbown，8/21）

**#5528 工作流运行静默失败：分发/模式错误从未在 TUI 中显示**
- **摘要**：两次工作流运行（review fan-out 和 phased build pipeline）在脚本求值阶段失败，但 TUI 中无任何提示——无 toast、无状态行、无工作流面板条目，操作者看到的只是"工作流正在运行"。
- **价值**：TUI 缺少错误可视化层，是运维信任度的关键缺口。
- [查看 Issue](https://github.com/Hmbown/CodeWhale/issues/5528)

**#5529 子代理无法可靠执行：三种故障模式**
- **摘要**：①两个 worker 子代理（117 和 83）在墙钟时间预算内死亡，未提交的工作丢失；②provider 路由故障阻塞分发；③shell 工具需要 workaround。
- **价值**：Fleet 派发核心价值主张（代理委派执行）目前不可用，属于高优先级缺陷。
- [查看 Issue](https://github.com/Hmbown/CodeWhale/issues/5529)

### 🧩 CodeWhale TUI Crate 分解（EPIC-005）

**#5316 EPIC-005: CodeWhale TUI Crate Decomposition（伞形跟踪）**
- **摘要**：跟踪 CodeWhale TUI crate 分解的伞形 EPIC，所有子 EPIC 和 FEAT 完成时汇报于此，所有相关 PR 在此记录。
- **价值**：这是当前最大规模的重构工程，影响所有 TUI 命令的执行边界与模块结构。
- [查看 Issue](https://github.com/Hmbown/CodeWhale/issues/5316)

### ⚙️ 其他

**#5526 Shell 补全已废弃**
- **摘要**：pwsh 用户发现 `codew completions powershell` 生成的内容过时，触发命令仍是 `codewhale-tui`（应为 `codewhale`），文档无相关说明。
- **价值**：破坏 pwsh 用户的补全体验，且暴露了二进制命名迁移不完整的问题。
- [查看 Issue](https://github.com/Hmbown/CodeWhale/issues/5526)

**#5541 [enhancement] 支持 DeepSeek-V4-Flash-Vision-Exp（多模态模型）**
- **摘要**：DeepSeek 家族首个多模态模型，要求在 `/model list` 中加入并支持 vision 功能。影响面：网站开发等视觉相关任务。
- **价值**：多模态支持是 TUI 客户端的重要能力扩展。
- [查看 Issue](https://github.com/Hmbown/CodeWhale/issues/5541)

**#4069 [documentation] 索引隐私控制（`.codewhaleignore`）**
- **摘要**：搜索、工作集遍历和项目上下文组装缺少一级 ignore 文件，无法排除密钥、vendor 树和本地工件——类似 Cursor 的 `.cursorignore`。信任与合规缺口。
- **价值**：企业级部署的合规底线，已开放约 6 周仍为 Open，社区关注度持续。
- [查看 Issue](https://github.com/Hmbown/CodeWhale/issues/4069)

---

## 4. 重要 PR 进展（10 条）

### 🏗️ 监督式运行堆栈（M-Maciej）

**#5535 监督式运行堆栈：生命周期 Outbox、/relaunch、每会话控制套接字 + 节奏修复**
- **内容**：单 PR 五个提交区域，覆盖 #5531/#5532/#5533/#5534 全部内容——生命周期事件 outbox（JSONL + webhook）、`/relaunch` 命令、控制套接字，以及目标延续静默期绕过修复。
- **评价**：这是今天最大的一体化 PR，将四个 Issue 的需求合并到同一 "seam" 上实现，工程效率极高。
- [查看 PR](https://github.com/Hmbown/CodeWhale/pull/5535)

### 🔧 TUI 重构（EPIC-005 推进）

**#5523 refactor(tui): 从回合循环中提取工具调用阶段**
- **内容**：`plan_tool_calls`、`execute_planned_tools`、`process_tool_results` 三阶段提取，保留原始控制顺序、可变状态流、取消行为和索引结果收集。
- **评价**：为后续工具调用的独立测试和扩展铺平道路，是分解重构的关键一步。
- [查看 PR](https://github.com/Hmbown/CodeWhale/pull/5523)

**#5525 refactor(tui): 在实用工具组中采用命令形状（FEAT-018）**
- **内容**：将 TUI 实用工具命令组（7 个命令文件）转换为 FEAT-014 引入的外部命令形状，仍保留在 `codewhale-tui` 下，变更执行边界而非物理移动。
- **评价**：EPIC-005 的渐进式落地——先改执行逻辑，再物理迁移。
- [查看 PR](https://github.com/Hmbown/CodeWhale/pull/5525)

### 🛠️ 功能修复与扩展

**#5530 fix(cli): 将遗留补全路由到公共二进制**
- **内容**：修复 #5526——`codewhale completions <shell>` 现在使用与 `codewhale completion <shell>` 相同的规范化补全生成器，生成脚本使用公共 `codewhale` 命令名。
- **评价**：快速响应用户反馈，消除补全命令的二进制命名混乱。
- [查看 PR](https://github.com/Hmbown/CodeWhale/pull/5530)

**#5524 feat(tui): 添加多文件 read_lints 操作**
- **内容**：模型可见的 `lsp` 工具新增 `read_lints` 操作，支持对多个工作区相对文件执行，复用现有 `LspManager` 及其传输池。
- **评价**：解决 #4070 的批准范围，避免为每个文件创建新的语言服务器生命周期。
- [查看 PR](https://github.com/Hmbown/CodeWhale/pull/5524)

### 📦 依赖更新（dependabot）

| PR | 依赖 | 版本变化 | 说明 |
|---|---|---|---|
| [#5540](https://github.com/Hmbown/CodeWhale/pull/5540) | similar | 3.1.2 → 3.2.0 | 新增结构化、基于行的 API |
| [#5539](https://github.com/Hmbown/CodeWhale/pull/5539) | rio-vt | 0.5.19 → 0.5.25 | 终端 VT 解析升级 |
| [#5538](https://github.com/Hmbown/CodeWhale/pull/5538) | jsonschema | 0.46.10 → 0.49.9 | JSON Schema 校验升级 |
| [#5390](https://github.com/Hmbown/CodeWhale/pull/5390) | rmcp | 2.2.0 → 3.1.2 | Rust MCP SDK 大版本升级 |
| [#5537](https://github.com/Hmbown/CodeWhale/pull/5537) | docker/setup-buildx-action | 4.2.0 → 4.3.0 | CI 构建工具升级 |

- **评价**：`rmcp 3.x` 属于破坏性版本升级，需关注与现有 MCP 工具的兼容性测试。

---

## 5. 功能需求趋势

| 方向 | 热度 | 代表 Issue/PR |
|---|---|---|
| **监督式运行/无人值守会话** | 🔥🔥🔥 | #5531、#5532、#5533、#5534、#5535——外部监督、事件通知、程序化控制 |
| **TUI 架构重构（crate 分解）** | 🔥🔥🔥 | #5316（EPIC-005）、#5523、#5525——模块化、命令形状标准化 |
| **多模态模型支持** | 🔥🔥 | #5541——DeepSeek-V4-Flash-Vision-Exp |
| **工作流/子代理可靠性** | 🔥🔥 | #5528、#5529——静默失败、子代理死锁与工作丢失 |
| **隐私/合规控制** | 🔥 | #4069——`.codewhaleignore` 索引排除机制 |
| **CLI/补全一致性** | 🔥 | #5526、#5530——公共命令名统一 |

---

## 6. 开发者关注点

### 高频痛点

1. **静默失败是最大信任杀手**：Hmbown（项目所有者）亲自上报工作流失败在 TUI 中完全不可见（#5528），说明开发者对 "有状态反馈" 的强烈需求——任何失败都应在 TUI 中显式呈现。

2. **子代理执行可靠性仍不达标**：墙钟预算死亡导致未提交工作丢失、provider 路由故障阻塞分发（#5529）——这直接打击 Fleet 派发模式的核心价值。

3. **版本升级体验断裂**：`/update` 要求手动重启（#5532），长时会话用户无法平滑升级，M-Maciej 的 `/relaunch` 提案获得积极响应。

4. **补全命令命名迁移不彻底**：`codewhale-tui` 二进制名仍出现在生成的补全脚本中（#5526），社区对 "公共命令名一致性" 有明确预期。

### 社区参与特征

- M-Maciej 是当前最活跃的贡献者，连续提交 4 个 Issue 和 1 个大型 PR，聚焦监督式运行场景。
- dependabot 的持续依赖维护保持仓库健康度。
- EPIC-005 重构由 aboimpinto 牵头推进，多个 FEAT 并行落地。

---

*日报生成时间：2026-08-22 | 数据覆盖：2026-08-21 00:00 - 2026-08-22 00:00 (UTC)*
*数据来源：[github.com/Hmbown/DeepSeek-TUI](https://github.com/Hmbown/DeepSeek-TUI)*

</details>

---
*本日报由 [agents-radar](https://github.com/kky-wollu/agents-radar) 自动生成。*