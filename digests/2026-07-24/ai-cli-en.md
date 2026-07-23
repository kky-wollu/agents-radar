# AI CLI Tools Community Digest 2026-07-24

> Generated: 2026-07-23 23:01 UTC | Tools covered: 9

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

## Cross-Tool Comparison

# AI CLI Developer Tools Ecosystem Report — 2026-07-24

## 1. Ecosystem Overview

The AI CLI developer tools landscape continues to mature rapidly across 8 major projects, with all tools showing sustained community engagement and frequent shipping cycles. Today's digest reveals a clear pattern: **platform stability and permission system reliability** have emerged as the dominant cross-cutting concerns, with every tool reporting at least one high-severity authentication, process management, or sandboxing issue. The Windows platform remains the weakest link across the ecosystem, with Claude Code, OpenAI Codex, and Kimi Code all reporting platform-specific crashes and performance regressions. Meanwhile, a wave of security hardening PRs (credential encryption, OAuth fixes, sandbox enforcement) signals that the ecosystem is transitioning from feature velocity to production-grade reliability.

---

## 2. Activity Comparison (Last 24 Hours)

| Tool | Issues (New/Updated) | PRs (Open/Closed) | Release Status | Notable Signal |
|------|---------------------|-------------------|----------------|----------------|
| **Claude Code** | ~10 notable | 4 key PRs | No new release | Quiet day; documentation gaps (100+ days stale) |
| **OpenAI Codex** | 10 notable | 10 key PRs | 2 alpha releases (v0.146.0-a.4/.5) | Rapid Rust iteration; Windows WMI crisis |
| **Gemini CLI** | 10 notable | 10 key PRs | Nightly v0.52.0 | Auth security fixes; SSR pipeline advancing |
| **Copilot CLI** | 10 notable | 2 PRs | v1.0.74 + v1.0.74-4 | Plugin spec support; Ctrl+C regression critical |
| **Kimi Code** | 6 notable | 10 PRs merged | No new release | Massive community contributor wave (lihailong00) |
| **OpenCode** | 10 notable | 10 key PRs | No new release | Provider compatibility; billing-for-blocked-outputs |
| **Pi** | 10 notable | 10 key PRs | No new release (v0.81.1 latest) | Constrained sampling; clipboard fixes |
| **Qwen Code** | 10 notable | 10 key PRs | No new release (v0.20.1 latest) | Enterprise memory proposal; CI flakiness |
| **CodeWhale** | 8 notable | 6 PRs updated | v0.9.1 security-gated | Stop-ship macOS bug; DeepSeek rebranding debt |

**Key Takeaways:**
- **OpenAI Codex** leads in release velocity (2 alpha releases in 24h)
- **Kimi Code** had highest community contributor throughput (15 PRs from lihailong00)
- **Claude Code** and **Kimi Code** had no releases — quieter days
- **Gemini CLI** and **Pi** most active on security infrastructure PRs

---

## 3. Shared Feature Directions

| Shared Requirement | Tools Expressing Interest | Specific Needs |
|-------------------|--------------------------|----------------|
| **MCP Tool Inheritance/Sharing** | Copilot CLI (#4143), Kimi Code (#2538), Pi (#6970) | Tools connected in one context (VS Code, IDE) should auto-available in CLI session; MCP server session reuse |
| **Hook Payload Enrichment** | Claude Code (#80446, #72110), CodeWhale (#4610), OpenCode (#33523) | Usage totals, timestamps, token counts in hook/stop payloads for observability and cost tracking |
| **Per-Agent Model Selection** | Kimi Code (#2533), Qwen Code (#7449), OpenCode (subagent routing) | Cost-tiered multi-agent workflows — cheap models for simple tasks, capable models for complex ones |
| **Remote Session Continuity** | Kimi Code (#1282, #2545), OpenCode (#33163) | Hand off CLI sessions across devices (phone/tablet) without losing context |
| **Enterprise Integration Profiles** | Qwen Code (#7449), Copilot CLI (#4016), Pi (#6970) | Provider-neutral interfaces for corporate knowledge stores, BYOK/SSO, persistent memory |
| **Windows Platform Reliability** | ALL tools (Claude #78179, Codex #34260, Copilot #4165, Kimi #2553) | Specific fixes: WMI storms, session resume hangs, UTF-8 encoding, keyboard layout compatibility |
| **AST-Aware Code Intelligence** | Gemini CLI (#22745), OpenCode (patch error improvements) | Replace naive file reads with AST-aware tools for precise method boundaries and reduced token consumption |

---

## 4. Differentiation Analysis

| Dimension | Claude Code | OpenAI Codex | Gemini CLI | Copilot CLI | Kimi Code | OpenCode | Pi | Qwen Code | CodeWhale |
|-----------|------------|--------------|------------|-------------|-----------|----------|-----|-----------|-----------|
| **Primary Target** | Power devs, plugin ecosystem | Windows .NET/enterprise | Google Cloud devs | GitHub ecosystem | Chinese devs, Moonshot AI | Cross-platform CLI | Tinkerers, local LLMs | Qwen model users | Multi-provider CLI |
| **Unique Strength** | Permission system depth | TUI customization | AST-aware tools, SSR pipeline | MCP plugin spec v1 | High community contributor velocity | Provider auto-discovery | Grammar/constrained sampling | Enterprise memory, CI tooling | Cross-provider sandboxing |
| **Key Weakness** | Documentation staleness | Windows WMI storms | False GOAL terminations | CAPI 5MB limit | Plugin worker deadlocks | Billing for blocked outputs | Package manifest fragility | CI flakiness | DeepSeek rebranding debt |
| **Model Strategy** | Anthropic-only | Multi-model (GPT-5 focus) | Gemini-only | Copilot/GitHub model | Moonshot + third-party | Multi-provider | Multi-provider + local | Qwen + third-party | Multi-provider |
| **Platform Maturity** | Most mature permissions | Most active releases | Fastest security iteration | Strongest plugin ecosystem | Fastest community growth | Most configurable providers | Most advanced local LLM | Most enterprise-focused | Most security-conscious |

---

## 5. Community Momentum & Maturity

### Most Active Communities (by issue/PR velocity)
1. **OpenAI Codex** — 20+ PRs, 2 releases, 10 hot issues. Highest raw velocity, but Windows stability concerns are dragging community sentiment.
2. **Gemini CLI** — 10 key PRs, nightly releases, major auth security fixes. Strong iterative cadence with clear security-first trajectory.
3. **Kimi Code** — 15 merged PRs from a single community contributor. Highest community contributor throughput; signals healthy onboarding pipeline.
4. **Qwen Code** — 50 PRs, 44 issues. High volume, but CI flakiness suggests testing infrastructure needs investment.

### Most Mature (production-readiness indicators)
- **Claude Code** — Most sophisticated permission system; hooks API maturing (usage totals, timestamps). Documentation gaps are the primary maturity lag.
- **Copilot CLI** — Plugin Spec v1 support, clear `--acp` mode for tooling. Enterprise authentication remains a gap.
- **Pi** — Constrained sampling PR (#6341) and grammar-aware tools signal advanced technical depth. Package management needs stabilization.

### Most Rapidly Iterating
- **OpenAI Codex** — 2 alpha releases in 24 hours; Rust-based CLI alpha suggests architectural rewrite in progress.
- **Gemini CLI** — SSR code generation pipeline (Antigravity) under active development; automated issue-to-PR pipeline is ambitious.
- **CodeWhale** — Final stages of v0.9.1 release; security gate process shows maturation, but stop-ship bug blocks delivery.

---

## 6. Trend Signals

### For Technical Decision-Makers

**1. Platform Parity Is Non-Negotiable**
Windows is the single largest community pain point across all tools. OpenAI Codex's WMI storms, Claude Code's VS Code CPU load, Copilot CLI's session resume hangs, and Kimi Code's `/plugins` crash collectively signal that the "Windows experience" remains second-class. **Recommendation:** Evaluate Windows support maturity carefully if your team is Windows-heavy; Gemini CLI and Pi show fewer Windows-specific complaints.

**2. Permission and Security Systems Are Entering Production Phase**
Every tool shipped at least one security-related PR today — credential encryption (Gemini CLI), shell injection fixes (Claude Code), sandboxing (CodeWhale), OAuth hardening (Pi). The era of "allow everything for development" is ending. **Recommendation:** Expect permission prompts to increase; plan for tool approval workflows that are more detailed (and more disruptive) than 6 months ago.

**3. Multi-Provider Strategy Is Becoming Table Stakes**
Users are actively running Claude, Gemini, GPT-5, Qwen, DeepSeek, and local LLMs through the same CLI. Tools that lock to a single provider (Claude Code, Copilot CLI) are seeing feature request pressure for more flexibility. **Recommendation:** If your workflow requires model diversity, favor multi-provider tools (OpenCode, Pi, Qwen Code) or prepare workarounds for single-provider tools.

**4. MCP Standardization Is Accelerating Cross-Tool Tooling**
Copilot CLI's Plugin Spec v1 support, Kimi Code's MCP session reuse fixes, and OpenCode's observability hooks all point toward a converging MCP ecosystem. Tooling built on MCP will increasingly work across CLI tools. **Recommendation:** Invest in MCP-based tooling over tool-specific plugins if cross-tool portability matters.

**5. Enterprise Demands Are Growing Faster Than Implementation**
Enterprise memory profiles (Qwen Code), BYOK authentication (Copilot CLI), and provider-neutral SSO (Pi, CodeWhale) are all community-driven requests that remain unimplemented. **Recommendation:** Enterprise adopters should expect manual configuration for SSO, knowledge store integration, and audit compliance for the next 6-12 months.

### For Developers

- **Local LLM users** should watch Pi (constrained sampling, llama.cpp integration) and Qwen Code (cache optimization for local contexts)
- **Multi-platform teams** should diversify — no tool handles Windows, macOS, and Linux equally well today
- **Plugin/extension developers** should target MCP-first architectures; the ecosystem is converging on this standard
- **Cost-conscious users** should monitor the billing-for-blocked-outputs issue in OpenCode (#35475) — it's a pattern that may appear in other tools as content filtering becomes more aggressive
- **Power CLI users** should prioritize tools with per-agent model selection (Kimi Code) and customizable TUI (OpenAI Codex, CodeWhale) for cost-optimized multi-agent workflows

The overall signal: **The AI CLI ecosystem is transitioning from "can it work?" to "does it work reliably across my entire workflow?"** — and the answers remain mixed, with no single tool delivering on all dimensions of platform parity, security, and enterprise readiness simultaneously.

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills Community Highlights Report
**Data snapshot:** 2026-07-24 | Source: github.com/anthropics/skills

---

## 1. Top Skills Ranking

The following Pull Requests have attracted the most community discussion (sorted by comment volume). Note: GitHub's API reports `undefined` for comment counts on this dataset; ranking is inferred from discussion depth and cross-referencing Issues.

### #1298 — `fix(skill-creator): run_eval.py always reports 0% recall` (OPEN)
**Author:** MartinCajiao | **Updated:** 2026-06-23  
**Functionality:** Fixes the `run_eval.py` script so that skill description optimization actually works—currently `recall=0%` for every description regardless of quality, making the entire `run_loop.py` / `improve_description.py` pipeline optimize against noise.  
**Discussion highlights:** Addresses #556 (12 comments, 7 👍), the single most-reported bug in the repository. Multiple independent reproductions confirmed the issue is systemic. The PR installs the eval artifact as a real skill, fixes Windows stream reading, trigger detection, and parallel worker bugs.  
**Status:** Open | [GitHub](https://github.com/anthropics/skills/pull/1298)

### #514 — `Add document-typography skill` (OPEN)
**Author:** PGTBoos | **Updated:** 2026-03-13  
**Functionality:** Prevents orphan word wrap (1–6 words on a new line), widow paragraph headers stranded at page bottoms, and numbering misalignment in AI-generated documents. Universal across all document types.  
**Discussion highlights:** Users noted these issues affect "every document Claude generates" and that typographic polish is rarely requested but widely appreciated.  
**Status:** Open | [GitHub](https://github.com/anthropics/skills/pull/514)

### #538 — `fix(pdf): correct case-sensitive file references in SKILL.md` (OPEN)
**Author:** Lubrsy706 | **Updated:** 2026-04-29  
**Functionality:** Fixes 8 case-sensitivity mismatches (`REFERENCE.md` → `reference.md`, `FORMS.md` → `forms.md`) that break on case-sensitive filesystems (Linux/macOS).  
**Discussion highlights:** A small but critical fix—underscores the cross-platform compatibility challenges in the Skills ecosystem.  
**Status:** Open | [GitHub](https://github.com/anthropics/skills/pull/538)

### #486 — `Add ODT skill — OpenDocument text creation and template filling` (OPEN)
**Author:** GitHubNewbie0 | **Updated:** 2026-04-14  
**Functionality:** Creates, fills, reads, and converts OpenDocument Format files (.odt, .ods). Triggers on mentions of ODT, ODS, ODF, OpenDocument, or LibreOffice documents.  
**Discussion highlights:** Addresses a clear gap—LibreOffice/OpenOffice users represent a significant portion of the open-source doc ecosystem. The PR includes parse-ODT-to-HTML conversion.  
**Status:** Open | [GitHub](https://github.com/anthropics/skills/pull/486)

### #1367 — `feat(skills): add self-audit — mechanical verification + reasoning quality gate` (OPEN)
**Author:** YuhaoLin2005 | **Updated:** 2026-07-02  
**Functionality:** A meta-skill that audits AI output before delivery: mechanical file verification first, then a four-dimension reasoning audit in damage-severity priority order. Universal across any project/tech stack/model.  
**Discussion highlights:** Related to Issue #1385 (Reasoning Quality Gate Pipeline proposal). Represents growing community interest in output quality assurance rather than just task execution.  
**Status:** Open | [GitHub](https://github.com/anthropics/skills/pull/1367)

### #723 — `feat: add testing-patterns skill` (OPEN)
**Author:** 4444J99 | **Updated:** 2026-04-21  
**Functionality:** Comprehensive testing coverage: Testing Trophy model philosophy, AAA pattern, React component testing with Testing Library, end-to-end patterns, and edge case guidance.  
**Discussion highlights:** Responds to demand for software engineering best-practice skills beyond pure feature-building.  
**Status:** Open | [GitHub](https://github.com/anthropics/skills/pull/723)

### #525 — `Add pyxel skill for retro game development` (OPEN)
**Author:** kitao (Pyxel creator) | **Updated:** 2026-07-15  
**Functionality:** Integrates with `pyxel-mcp` (MCP server for the Pyxel retro game engine). Covers write → run_and_capture → inspect → iterate workflow for pixel-art/8-bit games.  
**Discussion highlights:** Unique among skills—bridges MCP servers and game development. Authored by the Pyxel maintainer, signaling ecosystem collaboration. Long-running PR (since March).  
**Status:** Open | [GitHub](https://github.com/anthropics/skills/pull/525)

---

## 2. Community Demand Trends

From Issues analysis, the most-anticipated new Skill directions are:

| Trend | Signal | Key Issue |
|-------|--------|-----------|
| **🔐 Security & Trust Boundary** | Highest-comment Issue (#492, 43 comments, 2 👍). Community alarmed by skills distributed under `anthropic/` namespace impersonating official content. User trust is the #1 concern. | [#492](https://github.com/anthropics/skills/issues/492) |
| **🏢 Organization-wide Skill Sharing** | Second-highest demand (#228, 14 comments, 7 👍). Users want shared skill libraries or direct sharing links instead of manual `.skill` file exchange via Slack/Teams. | [#228](https://github.com/anthropics/skills/issues/228) |
| **🔧 Skill-Creator Tooling Reliability** | Multiple issues (#556, #1169, #1061, #202) all report the same bug: `run_eval.py` gives 0% recall on every query. The optimizer is broken for Windows users and for skills with defined slash-commands. Critical infrastructure need. | [#556](https://github.com/anthropics/skills/issues/556) |
| **🧠 Reasoning Quality / Agent Governance** | Two related proposals (#412, #1385) for safety patterns, threat detection, audit trails, and pre-delivery quality gates. The community wants guardrails, not just capabilities. | [#412](https://github.com/anthropics/skills/issues/412) |
| **🧩 MCP Integration** | Early but persistent demand (#16) to expose Skills as MCP tools. Suggests users want Skill capabilities accessible via standardized protocol, not just Claude CLI commands. | [#16](https://github.com/anthropics/skills/issues/16) |
| **📄 Duplicate Skill Management** | #189 (6 comments, 9 👍) reports that `document-skills` and `example-skills` plugins install identical content, cluttering context windows. Community wants deduplication. | [#189](https://github.com/anthropics/skills/issues/189) |
| **🪟 Windows Compatibility** | #1061 (3 comments, 2 👍), cross-referenced by multiple PRs. The skill-creator pipeline is effectively unusable on Windows—the platform gap is a recurring blocker. | [#1061](https://github.com/anthropics/skills/issues/1061) |

---

## 3. High-Potential Pending Skills

These active-comment PRs are not yet merged but show strong momentum:

| PR | Skill | Why It May Land Soon |
|----|-------|---------------------|
| [#1298](https://github.com/anthropics/skills/pull/1298) | `run_eval.py` fix (0% recall) | **Highest-priority fix in the repo.** Unblocks the entire skill creation pipeline. Multiple authors (#1099, #1050, #1323) independently submitted fixes for the same issue—convergence suggests a merge is imminent. |
| [#1367](https://github.com/anthropics/skills/pull/1367) | Self-audit skill (mechanical + reasoning quality gate) | Recent (June 28), actively discussed (#1385 proposal). Addresses the growing governance/quality trend. |
| [#1302](https://github.com/anthropics/skills/pull/1302) | `color-expert` — color naming, spaces, systems | Self-contained, no external dependencies. Updated July 21. Broad applicability (design, data viz, branding). |
| [#723](https://github.com/anthropics/skills/pull/723) | `testing-patterns` — full testing stack | Addresses a clear coverage gap. No major controversies in comments. |
| [#525](https://github.com/anthropics/skills/pull/525) | `pyxel` — retro game dev via MCP | Author is the Pyxel maintainer. Unique MCP integration. Long open but actively maintained (updated July 15). |
| [#514](https://github.com/anthropics/skills/pull/514) | `document-typography` — orphan/widow fix | Simple, universally useful, no external deps. Has been open since March without rejection signals. |

---

## 4. Skills Ecosystem Insight

**The community's most concentrated demand is for *infrastructure reliability*—fixing the broken skill-creation pipeline (0% recall bug, Windows incompatibility, YAML parsing failures) before new skills can be effectively developed, with a secondary surge toward *quality assurance and governance* skills that verify AI output rather than simply generating it.**

---

# Claude Code Community Digest — 2026-07-24

## Today's Highlights
A quiet day on the release front with no new versions, but the community remains active with a wave of bug reports filed July 16 now being closed out. Two important PRs landed today addressing shell injection in the `/ralph-loop` command and fixing pagination in the auto-close-duplicates script. Meanwhile, long-standing documentation gaps—now over 100 days old for many issues—continue to accumulate without resolution.

## Releases
No new releases in the last 24 hours.

## Hot Issues
1. **[#62135 – Bash read-only commands still prompt for permission despite allow rules](https://github.com/anthropics/claude-code/issues/62135)**  
   Users configuring allow rules for read-only commands like `curl` and `gh api` report that permission prompts persist. Community reaction (👍1) suggests this is a known friction point in the permissions system.

2. **[#80446 – Include session usage totals in Stop/SubagentStop hook payload](https://github.com/anthropics/claude-code/issues/80446)**  
   Freshly filed feature request requesting usage statistics in hook payloads for better cost tracking. Zero community engagement yet but represents a clean extension to the hooks API.

3. **[#78240 – macOS security flagger blocking work](https://github.com/anthropics/claude-code/issues/78240)**  
   A frustrated user reports false positive security flags interfering with productivity. This is part of a larger pattern of security-flag complaints filed on July 16, all now closed.

4. **[#78251 – False positive security warning for web scraping](https://github.com/anthropics/claude-code/issues/78251)**  
   Another security-flagging complaint: web scraping operations being misclassified as cybersecurity threats. Closed without resolution (needs-repro).

5. **[#78227 – Auto-classifier unavailable – manual approval required](https://github.com/anthropics/claude-code/issues/78227)**  
   The automatic permission classifier went down, forcing manual approval for all operations. Points to reliability concerns in the classification infrastructure.

6. **[#78179 – VS Code extension causes high CPU load on Windows](https://github.com/anthropics/claude-code/issues/78179)**  
   Performance bug with attached CPU profile showing extension unresponsiveness. Critical for Windows users relying on the VS Code integration.

7. **[#78180 – Agent repeatedly generates incorrect self-corrections](https://github.com/anthropics/claude-code/issues/78180)**  
   Pattern of "The actual defect was my..." self-corrections indicates cascading error states in the model. Closed with needs-repro label.

8. **[#78209 – Assistant appends unrelated documents to response output](https://github.com/anthropics/claude-code/issues/78209)**  
   Model hallucination where an unrelated document was appended to legitimate responses. Raises quality concerns for longer sessions.

9. **[#78219 – Non-issue bug report about LinkedIn profile](https://github.com/anthropics/claude-code/issues/78219)**  
   User mistakenly filed a cybersecurity work credential as a bug report. Community noise, but highlights need for better issue templates.

10. **[#72110 – Add time to JSONL "usage" property](https://github.com/anthropics/claude-code/issues/72110)**  
    Request to timestamp usage entries in JSONL logs for better billing and cost attribution. Practical ergonomic improvement for heavy users.

## Key PR Progress
1. **[#80508 – fix(scripts): paginate comments and reactions in auto-close-duplicates](https://github.com/anthropics/claude-code/pull/80508)**  
   Critical fix for the auto-close-duplicates script that was missing paginated reads for comments and reactions. This was causing incomplete duplicate detection for repos with active issue volumes.

2. **[#80495 – fix(ralph-wiggum): stop parsing /ralph-loop prompt text as shell code](https://github.com/anthropics/claude-code/pull/80495)**  
   Security fix addressing shell injection vulnerability (#16037) in the `/ralph-loop` command where user prompt text was directly interpolated into shell commands, causing failures.

3. **[#42604 – Remove "retro-futuristic" recommendation from Frontend Design Skill](https://github.com/anthropics/claude-code/pull/42604)**  
   Old PR (April) finally closed today. Trivial content fix removing a stylistic recommendation from Claude's frontend design guidance.

4. **[#18217 – feat(plugins): add /planwith command for inline plan mode prompts](https://github.com/anthropics/claude-code/pull/18217)**  
   Long-dormant feature PR (January) closed today without merge. Would have added inline argument support to `/plan`, eliminating the two-step workflow for planning tasks. 

## Feature Request Trends
- **Hook payload enrichment**: Requests for usage totals and timestamps in hook/stop payloads (#80446, #72110) for better observability and cost tracking.
- **Inline command arguments**: Strong interest in commands that accept arguments directly rather than requiring a two-step toggle (#18217 pattern).
- **Permission system transparency**: Users want clearer, more reliable classification of read-only vs destructive operations (#62135).
- **Documentation completeness**: Over a dozen stale documentation issues (100+ days old) covering undocumented features across VS Code, MCP, plugins, sandboxing, and Linux support.

## Developer Pain Points
- **False positive security flags**: Multiple reports of aggressive security classification blocking legitimate development work (web scraping, general coding). Pattern from July 16 filings shows this is a top frustration.
- **Permission classification reliability**: The auto-classifier going down (#78227) and false positives (#78113, #78176, #78251) create workflow friction that undermines trust in the safety system.
- **Model quality degradation**: Self-correction loops (#78180), document hallucination (#78209), and inconsistent prompt interpretation (#78187) indicate model instability in longer sessions.
- **VS Code extension performance**: High CPU load (#78179) on Windows is a platform-specific pain point affecting IDE integration users.
- **Documentation staleness**: Issues from March-April (now 3-4 months old) remain unaddressed, covering features that exist but are undocumented—particularly around MCP, plugins, and VS Code integration.

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex Community Digest — 2026-07-24

## Today's Highlights
The Codex team pushed two new Rust alpha releases (`v0.146.0-alpha.4` and `v0.146.0-alpha.5`) alongside a burst of 20+ closed PRs addressing process management, TUI responsiveness, and plugin attribution. Windows stability remains the dominant community concern, with multiple high-engagement issues reporting WMI storms, runaway `taskkill.exe` processes, and unbounded memory growth. A long-standing Linux desktop app request (#11023) continues to attract overwhelming support (825 👍), signaling strong demand for cross-platform parity.

## Releases
- **rust-v0.146.0-alpha.4 / rust-v0.146.0-alpha.5** — Two consecutive alpha releases pushed within 24 hours. No detailed changelog provided in the release notes, but the rapid iteration suggests active work on the Rust-based Codex CLI components.

## Hot Issues (10 Noteworthy)

1. **[#11023] Codex desktop app for Linux** — 825 👍, 185 comments. The top-voted open feature request. The author cites power efficiency issues on macOS (#10432) and wants Linux-native support. **Why it matters**: Linux developer adoption is gated by this; current workarounds (Wine, VMs) are inadequate.

2. **[#20214] Codex App frequently freezes/stutters on Windows 11 Pro** — 73 comments, 72 👍. Desktop app freezes despite 32 GB RAM and a modern AMD CPU. **Community reaction**: Users report the freeze coincides with background WMI queries.

3. **[#28969] Add setting to disable 60-second auto-resolve for questions** — 153 👍, 55 comments. CLI users want control over the auto-resolve timer. **Why it matters**: Time-sensitive workflows break when the agent self-resolves before user input.

4. **[#17827] Customizable status line (TUI)** — 122 👍, 32 comments. Users want real-time token usage, model, git branch in the terminal UI—inspired by Claude Code. **Trend**: Signals demand for transparent model/context visibility.

5. **[#34260] Unbounded taskkill.exe/conhost.exe cleanup storm exhausts WMI** — 27 comments. Desktop spawns hundreds of `taskkill.exe` processes, crashing WMI. **Impact**: System-wide performance collapse on Windows.

6. **[#33776] ChatGPT.exe spawns 287 taskkill.exe processes** — 21 comments. Similar to #34260, with DWM degradation. **Pattern**: A critical Windows bug family now affecting multiple users.

7. **[#34014] Standalone Windows app triggers WMI Provider Host at 90–100% CPU** — 21 comments. Same project works fine in the VS Code extension. **Implication**: The standalone app has a unique WMI polling pathology.

8. **[#24948] Codex session logs grow to 700MB–2GB** — 19 comments. Compaction history and raw tool output bloat. **Developer pain point**: Storage exhaustion on developer machines.

9. **[#34967] Regression: automatic approval broken for GPT-5 models (26.715.72359)** — Just filed today, 3 comments. Windows Store update broke auto-approval for all GPT-5 variants. **Urgency**: Blocks automated workflows.

10. **[#34658] Completed subagents leave 245 STDIO MCP Node.js processes (18 GB)** — 3 comments but severe: orphaned processes accumulate indefinitely. **Risk**: OOM crashes on developer machines.

## Key PR Progress (10 Important PRs)

1. **[#35024] Allow custom providers to opt into standalone web search** (Open) — Adds `supports_standalone_web_search` model-provider setting. **Impact**: Enables custom model providers to use `web.run` independently.

2. **[#35021] Adapt keyboard event reporting to the terminal** (Closed) — Fixes key-event leaks in iTerm2 and tmux Shift+Enter issues. **User-facing**: Better terminal compatibility.

3. **[#35020] Attribute command executions to trusted plugin scripts** (Closed) — Resolves commands against trusted plugin roots, adds `pluginId` and `scriptPath` fields. **Security**: Audit trail for plugin actions.

4. **[#35011] Keep side conversations open when switching threads** (Closed) — New `toggle_side_conversation` TUI action bound to `ctrl-/`. **Quality of life**: No more lost context when switching threads.

5. **[#35000] Make TUI turn interrupts nonblocking** (Closed) — Background dispatch for app-server interrupts, coalesces duplicate requests. **Performance**: Prevents TUI freezes during interrupt storms.

6. **[#34997] Warn when skill catalogs exceed their context budget** (Closed) — Emits warning when catalog rendering is truncated. **Transparency**: Users know when model-visible skill details are missing.

7. **[#34991] Allow omitting MCP tool prefixes per server** (Closed) — Accepts `server_names` list to remove `mcp__` prefix selectively. **Flexibility**: Cleaner tool names for specific MCP servers.

8. **[#34989] Preserve timestamps when importing external agent sessions** (Closed) — Uses source timestamps instead of import time. **Data integrity**: Chronological accuracy for imported sessions.

9. **[#34986] Enforce single-writer ownership for paginated threads** (Closed) — Filesystem locking for paginated thread writes. **Data safety**: Prevents corruption from concurrent writers.

10. **[#34981] Record externally completed agent config imports** (Closed) — New `externalAgentConfig/import/recordHistory` API. **API**: Enables external tools to record import results.

## Feature Request Trends

1. **Cross-platform desktop support** — #11023 (Linux app) remains the single most-requested feature. Users want native Linux builds, not workarounds. **Expectation**: Community may fork if not addressed soon.

2. **Customizable TUI/CLI experience** — #17827 (status line), #28969 (auto-resolve timer), and #32823 (`reasoning.mode` for GPT-5.6) point to demand for per-user configuration of agent behavior and visibility.

3. **Enhanced MCP/WSL integration** — #13690 (WSL MCP calls), #34991 (tool prefix control), and #20863 (custom pet animations) show users want deeper plugin and environment customization.

4. **Remote control expansion** — #34028 (Windows-to-Windows remote) and #31561 (per-thread target selection) indicate that remote control is valued but incomplete—users want universal host-target support.

5. **Windows-to-Android remote** — #31786 (broken) and #26640 (Mac-to-Mac broken) suggest remote control reliability is a cross-cutting issue.

## Developer Pain Points

1. **Windows WMI storms** — Issues #34260, #33776, #34014, #29499 collectively describe a systemic problem: the standalone Windows app repeatedly spawns resource-intensive WMI queries (process enumeration, file system watchers) that degrade or crash the entire system. This is the #1 stability complaint.

2. **Orphaned process accumulation** — #34658 (245 dead MCP Node.js processes, 18 GB), #33776 (287 taskkills), and #34260 (unbounded taskkill loop) reveal that Windows process cleanup is fundamentally broken. Developers report out-of-memory scenarios.

3. **Session log bloat** — #24948 shows logs reaching 2 GB from compaction history and raw tool output. Developers on storage-constrained machines (VMs, containers) are hit hardest.

4. **Rate limit consumption on startup** — #22073 reports that the app consumes rate limits without user action, wasting daily quotas on idle background operations.

5. **Auto-approval regressions** — #34967 (filed today) shows that the latest Windows Store build broke GPT-5 model auto-approval. This is a recurring pattern—previous updates have broken the same feature.

6. **Sandbox reliability** — #29908 (Bubblewrap loopback errors on Ubuntu 24.04) and #34841 (corrupted `deny_read_acl_state.json` after crash) show sandbox environments are brittle across both Linux and Windows.

7. **MCP/WSL gap** — #13690 (2 comments but 2 👍) indicates Windows users cannot call MCP servers when the agent environment is WSL—a blocker for hybrid Linux-on-Windows workflows.

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI Community Digest — 2026-07-24

## Today's Highlights

Two significant security fixes land today: credential encryption now enforces explicit 128-bit authentication tags, and OAuth token exchange moves to native `fetch` to resolve "Premature close" failures on headless systems. Meanwhile, the Caretaker triage system receives major prompt-evaluation improvements, and the new SSR code generation pipeline (Antigravity) progresses with Firestore dual-locking and Cloud Run infrastructure landing across multiple PRs.

## Releases

**v0.52.0-nightly.20260723.g9681621c6** — [Release](https://github.com/google-gemini/gemini-cli/releases/tag/nightly.20260723)
- Fix: Sequentially verify cached credentials and restore `GOOGLE_APPLICATION_CREDENTIALS` fallback
- Feat: Add eval coverage report command

## Hot Issues

1. **[#22323](https://github.com/google-gemini/gemini-cli/issues/22323) — Subagent reports GOAL success after MAX_TURNS** (P1, 12 comments, 2 👍)  
   The `codebase_investigator` subagent signals `Termination Reason: "GOAL"` even when hitting max turn limits before doing any real analysis. This masks agent failures and undermines trust in agent-completion metrics. Community consensus: termination reasons must be truthfully propagated.

2. **[#21409](https://github.com/google-gemini/gemini-cli/issues/21409) — Generalist agent hangs forever** (P1, 8 comments, 8 👍)  
   The generalist agent hangs indefinitely on simple tasks (e.g., folder creation). Users report that explicitly blocking subagent delegation works around the issue. With 8 upvotes, this is the highest-signal bug this week.

3. **[#19873](https://github.com/google-gemini/gemini-cli/issues/19873) — Zero-dependency OS sandboxing for bash affinity** (P2, 8 comments)  
   Proposes leveraging Gemini 3 models' native bash proficiency via sandboxed POSIX toolchains. A large-effort enhancement that could dramatically reduce tool-call overhead for codebase exploration.

4. **[#25166](https://github.com/google-gemini/gemini-cli/issues/25166) — Shell execution stuck "Waiting input" after command completes** (P1, 4 comments, 3 👍)  
   After trivial shell commands finish, the CLI hangs showing "Awaiting user input." Reproducible with simple commands, suggesting a terminal state-management bug.

5. **[#26522](https://github.com/google-gemini/gemini-cli/issues/26522) — Auto Memory retries low-signal sessions indefinitely** (P2, 5 comments)  
   The extraction agent only marks sessions processed upon successful `read_file`, causing low-signal sessions to be re-surfaced infinitely. Core memory-system reliability issue.

6. **[#26525](https://github.com/google-gemini/gemini-cli/issues/26525) — Deterministic redaction and reduced Auto Memory logging** (P2, 4 comments)  
   Auto Memory sends transcript content to model context *before* secret redaction occurs. This highlights a privacy architecture gap where sensitive data touches model context before sanitization.

7. **[#21000](https://github.com/google-gemini/gemini-cli/issues/21000) — Native file tools for task tracker maintenance** (P3, 4 comments)  
   Experiment to replace agent-driven task tracker updates with native file I/O tools, potentially reducing turn count and improving reliability of task state management.

8. **[#21983](https://github.com/google-gemini/gemini-cli/issues/21983) — Browser agent fails on Wayland** (P1, 4 comments, 1 👍)  
   Browser subagent exits with `Termination Reason: GOAL` but has performed zero actions. Wayland display-server incompatibility continues to affect Linux users.

9. **[#23571](https://github.com/google-gemini/gemini-cli/issues/23571) — Model creates tmp scripts in random directories** (P2, 3 comments)  
   When restricted to shell execution, the model scatters edit scripts across the filesystem, making cleanup and clean commits difficult. Suggests need for temporary-directory confinement.

10. **[#22745](https://github.com/google-gemini/gemini-cli/issues/22745) — AST-aware file reads, search, and mapping** (P2, 7 comments)  
    EPIC investigating AST-aware tools for precise method-bound reads, reducing token noise and turn count. Could be a significant accuracy and efficiency improvement for codebase investigators.

## Key PR Progress

1. **[#28519](https://github.com/google-gemini/gemini-cli/pull/28519) — Prevent infinite auth loop** (P1, core)  
   Fixes a critical bug where `gemini login` entered an infinite loop because `oauth_creds.json` writes were not awaited. Now forces consent prompt on refresh failure.

2. **[#28481](https://github.com/google-gemini/gemini-cli/pull/28481) — Fix MCP OAuth token refresh** (P1, security)  
   OAuth token refresh for MCP servers was failing before any network I/O, then deleting stored credentials. This fix uses the stored client ID for refresh, preventing forced re-auth cycles.

3. **[#28523](https://github.com/google-gemini/gemini-cli/pull/28523) — Enforce explicit tag length in file keychain** (core, security)  
   Configures mandatory 128-bit (16-byte) authentication tag enforcement for file-based credential storage, closing a cross-runtime compatibility gap.

4. **[#28446](https://github.com/google-gemini/gemini-cli/pull/28446) — Use native `fetch` for OAuth token exchange** (P1, security)  
   Replaces HTTP client with native `fetch` to fix "Premature close" errors on headless VPSes during `gemini login`. Reporter confirmed the endpoint works fine via curl, isolating the bug to the previous client implementation.

5. **[#28524](https://github.com/google-gemini/gemini-cli/pull/28524) — Caretaker triage prompt hill-climbing**  
   3 weeks of prompt evaluation tuning yielding significant quality improvements. Introduces a dedicated `code_explorer` skill and updates the triage orchestrator.

6. **[#28485](https://github.com/google-gemini/gemini-cli/pull/28485) — Add gemini-3.5-flash to model selector** (P2, core)  
   Users on v0.51.0 couldn't select newer flash models because `buildAvailableModels` surfaced only `gemini-2.5-flash`. Fix enables model selection for all users.

7. **[#28509](https://github.com/google-gemini/gemini-cli/pull/28509) — Filter thought parts from history turns** (core)  
   Prevents internal monologue/thinking parts from leaking into history when context management is disabled. Fixes duplicate reasoning blocks in Gemini 2.x+ models.

8. **[#28517](https://github.com/google-gemini/gemini-cli/pull/28517) — Enforce HTTPS for GoogleCredentialsAuthProvider** (security)  
   Prevents ADC access/identity tokens from being transmitted over cleartext HTTP. Protocol verification added at the auth provider level.

9. **[#28469](https://github.com/google-gemini/gemini-cli/pull/28469) — Rotate session ID on model fallback** (core, closed)  
   When falling back to `gemini-2.5-flash`, the stale session ID caused blocking API errors. Session rotation on fallback prevents "Please submit a new query" errors.

10. **[#28432](https://github.com/google-gemini/gemini-cli/pull/28432) + [#28434](https://github.com/google-gemini/gemini-cli/pull/28434) — SSR Code Generation Pipeline** (feature, large)  
    Multi-PR feature implementing Firestore dual-locking, Antigravity agent runners, iterative bug-fixing state machines, and Cloud Run infrastructure. This is the Gemini CLI's automated issue-to-PR pipeline, currently under active development.

## Feature Request Trends

The most requested feature directions from this week's issues cluster into three themes:

1. **Agent self-awareness and tool selection**: Multiple requests (e.g., [#21968](https://github.com/google-gemini/gemini-cli/issues/21968), [#24246](https://github.com/google-gemini/gemini-cli/issues/24246), [#21432](https://github.com/google-gemini/gemini-cli/issues/21432)) ask the agent to better understand its own capabilities — accurately reporting CLI flags, hotkeys, and *limiting tool scope* when >128 tools are available.

2. **AST-aware code intelligence** ([#22745](https://github.com/google-gemini/gemini-cli/issues/22745), [#22746](https://github.com/google-gemini/gemini-cli/issues/22746)): Growing interest in replacing naive file reads/AST-unaware search with Abstract Syntax Tree-aware tools for precise method boundaries, reduced token consumption, and more accurate codebase mapping.

3. **Memory system hardening and transparency** ([#26522](https://github.com/google-gemini/gemini-cli/issues/26522), [#26523](https://github.com/google-gemini/gemini-cli/issues/26523), [#22598](https://github.com/google-gemini/gemini-cli/issues/22598), [#26516](https://github.com/google-gemini/gemini-cli/issues/26516)): Users want memory patches surfaced/quarantined when invalid, subagent trajectories visible via sharing, and deterministic redaction before content reaches model context.

## Developer Pain Points

Several recurring frustrations emerge across this week's data:

- **False "success" termination** – Both [#22323](https://github.com/google-gemini/gemini-cli/issues/22323) (subagent GOAL success on MAX_TURNS) and [#21983](https://github.com/google-gemini/gemini-cli/issues/21983) (browser agent GOAL on Wayland) show the system reporting success when agents actually failed. This erodes trust in agent telemetry.

- **Indefinite hangs** – [#21409](https://github.com/google-gemini/gemini-cli/issues/21409) (generalist agent) and [#25166](https://github.com/google-gemini/gemini-cli/issues/25166) (post-command hang) both describe scenarios where the CLI becomes permanently unresponsive. Users resort to cancellation after up to an hour of waiting.

- **Auth cycle failures** – Two high-severity auth bugs this week: infinite auth loops ([#28519](https://github.com/google-gemini/gemini-cli/pull/28519)) and "Premature close" on headless systems ([#28446](https://github.com/google-gemini/gemini-cli/pull/28446)). Authentication is a fundamental gating item that continues to be fragile across environments.

- **Untracked filesystem pollution** – [#23571](https://github.com/google-gemini/gemini-cli/issues/23571) (random temp scripts) and [#25166](https://github.com/google-gemini/gemini-cli/issues/25166) (stuck shell) both create artifacts that users must manually clean up, adding friction to agent-assisted workflows.

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI Community Digest — 2026-07-24

## Today's Highlights

The team shipped **v1.0.74** with official support for Open Plugin Spec v1 manifests and `mcp.json` configuration, alongside a critical IDE integration reconnection fix. Community attention is focused on two systemic regressions: Ctrl+C no longer interrupts active agent runs (a **24-hour-old issue** with 0 comments but high urgency), and session-resume hangs on Windows cold starts. The `apply_patch` binary-deletion bug continues to frustrate users, permanently exceeding the 5 MB CAPI limit with no recovery path.

---

## Releases

### [v1.0.74](https://github.com/github/copilot-cli/releases/tag/v1.0.74) (2026-07-23)
- **Typing `?` with the search bar open no longer opens quick help** — enters `?` as text instead.
- **Open Plugin Spec v1 manifests and `mcp.json` configuration** are now supported.
- **IDE integration reconnection** is now reliable when the CLI reloads MCP servers or changes directory.
- **Multi-turn subagent** work continues (cut-off in release notes).

### [v1.0.74-4](https://github.com/github/copilot-cli/releases/tag/v1.0.74-4) (2026-07-23)
- Same plugin-manifest support as v1.0.74.
- **Improved:** Subagent timelines now indicate whether prompts originated from the main agent or another subagent.
- **Fixed:** IDE integration reconnection reliability (identical fix).

---

## Hot Issues (10 notable)

1. **[#4235](https://github.com/github/copilot-cli/issues/4235) — Ctrl+C no longer cancels/interrupts an active agent run (regression)**  
   Filed hours ago, this is a **critical regression** — Ctrl+C previously aborted in-progress turns; now the run continues and the keypress is ignored. **0 comments yet**, but immediate escalation expected. 🚨

2. **[#4097](https://github.com/github/copilot-cli/issues/4097) — `apply_patch` stores deleted binary in session history, permanently exceeding CAPI 5 MB limit**  
   A **systemic issue**: deleting a large binary via `apply_patch` stores the entire file as a textual diff in conversation history, causing every subsequent request to fail. `/compact` cannot recover. **5 👍, 4 comments** — the community is frustrated by the lack of recovery.

3. **[#4165](https://github.com/github/copilot-cli/issues/4165) — `copilot --resume` hangs at "Resuming session" on Windows cold start**  
   Resuming a session from PowerShell hangs indefinitely. Workaround exists (start TUI first, then resume), but this blocks headless/automated Windows workflows. **1 👍, 3 comments**.

4. **[#4016](https://github.com/github/copilot-cli/issues/4016) — BYOK still rejected in `--acp` mode: `session/new → -32000 Authentication required`**  
   This is a **recurring regression** (same class as #3048, #3902). Custom providers work in `-p` mode but gate on GitHub login in `--acp` mode. **4 👍, 5 comments** — enterprise users are vocal.

5. **[#3534](https://github.com/github/copilot-cli/issues/3534) — WSL2 (ARM64): `/copy` fails with `clip.exe exited with code 1`**  
   Clipboard writes via the Windows path break on WSL2 ARM64 due to a `cmd.exe` quoting bug. **4 👍, 5 comments** — affects WSL2 ARM64 adopters.

6. **[#4233](https://github.com/github/copilot-cli/issues/4233) — [ACP] Emit `usage_update` for context window + AI credits parity**  
   ACP clients (Zed, etc.) cannot show context-window or AI-credit usage because the CLI never emits the `usage_update` session update — even though the data is computed for `/context` and `/usage`. **2 👍 — clean feature gap**.

7. **[#4143](https://github.com/github/copilot-cli/issues/4143) — CLI should inherit MCP tools from connected VS Code instance**  
   MCP extensions installed in VS Code are invisible to the connected CLI session. **5 👍 — high demand** for cross-editor MCP sharing.

8. **[#4237](https://github.com/github/copilot-cli/issues/4237) — Steering message in `preToolUse` "ask" denial is silently dropped**  
   When a hook returns `permissionDecision: 'ask'`, custom denial text is ignored — only the default prompt is shown. **0 comments** but filed today; affects all hook-based permission workflows.

9. **[#4238](https://github.com/github/copilot-cli/issues/4238) — Failed GitHub MCP tool details render server label one character per line**  
   A **rendering bug**: `(MCP: github-mcp-server)` renders in a ~1-character-wide column, making expanded error details unusable. Cosmetic but impactful for debugging.

10. **[#4206](https://github.com/github/copilot-cli/issues/4206) — Environment footer stuck on "Loading:" forever when built-in GitHub MCP handshake stalls**  
    The status footer never transitions to "loaded" despite `/env` showing everything is ready. **2 👍, 3 comments** — users are confused about whether the session is functioning.

---

## Key PR Progress

- **[#4228](https://github.com/github/copilot-cli/pull/4228) — Withdrawn: incorrect scope for #3534**  
  Submitted, then withdrawn. The author realized the PR changed documentation instead of the private clipboard runtime; source branch deleted.

- **[#3163](https://github.com/github/copilot-cli/pull/3163) — ViewSonic monitor**  
  Stale PR (opened May 2026). Appears to be a mis-filed monitor-config issue, not a code change. No bot action visible.

---

## Feature Request Trends

1. **MCP tool inheritance** — Multiple requests (#4143, #3125) ask for tools connected in one context (VS Code, another IDE) to be automatically available in the CLI session. The community wants a **unified MCP ecosystem**.

2. **ACP parity features** — Users want the CLI's `--acp` mode to emit the same rich session updates (`usage_update`, context-window info) that the interactive TUI provides (#4233). Tooling builders need this for integration.

3. **Instruction/tag scoping** — `applyTo` glob patterns are seen as insufficient for large monorepos; users want domain/category tags in `.instructions` files (#4231).

4. **MCP resource subscriptions** — Building on #1803 and #1518, users want `resources/subscribe` and `notifications/resources/updated` for autonomous agent workflows (#3073).

5. **Plugin MCP server project resolution** — Plugin-loaded MCP servers get their working directory set to the plugin root, not the project — making project-scoped servers useless (#4234).

---

## Developer Pain Points

- **CAPI 5 MB limit is a recurring nightmare** — Two active issues (#3767, #4097) describe irreversible session wedging when attachments or tool results exceed the limit. `/compact` cannot fix it; users must destroy sessions.

- **Windows platform is fragile** — Session resume hangs (#4165), WSL2 ARM64 clipboard failures (#3534), and infinite render loops (#2802) collectively paint Windows as a second-class experience.

- **Authentication friction for enterprise/BYOK** — Custom providers work inconsistently across modes (`-p` vs `--acp`), and GHE authentication for ACP is entirely unsupported (#3161, #4016). Enterprise users are repeating the same complaint.

- **Regression velocity is worrying** — Two **day-old** issues (#4235: Ctrl+C broken, #4232: Playwright on localhost) suggest test coverage gaps. Users are noticing quality slips after recent releases.

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI Community Digest — 2026-07-24

## Today's Highlights
A massive wave of 15 pull requests merged today, primarily driven by community contributor **lihailong00**, addressing critical stability issues across Windows, MCP, shell completion, and plugin systems. Notably, a `TypeError` crash in the `/plugins` screen when 2+ plugins are installed (Issue #2553) and a plugin worker pool blocking all sessions (Issue #2538) are under active investigation. The remote control feature request (#1282) continues to gain community traction with 16 👍.

---

## Releases
No new releases in the last 24 hours. Latest stable: **v0.29.0**.

---

## Hot Issues

### 1. #1282 — [enhancement] Remote Control: Continue local sessions from any device
- **Author**: CatKang  
- **Why it matters**: The most upvoted open feature request (16 👍). Users want to hand off CLI sessions to phone/tablet without losing context. Community discussion spans 6 comments.  
- **Link**: [Issue #1282](https://github.com/MoonshotAI/kimi-cli/issues/1282)

### 2. #2553 — /plugins crashes with TypeError when 2+ plugins installed (v0.29.0, Windows)
- **Author**: tovipy-png  
- **Why it matters**: **Critical bug** — the plugin management screen crashes entirely with a `TypeError: Cannot read properties of undefined (reading 'value')`. Only affects Windows. With 0 or 1 plugin it works fine.  
- **Link**: [Issue #2553](https://github.com/MoonshotAI/kimi-cli/issues/2553)

### 3. #2552 — [Bug] Poor font kerning for Cyrillic text in Kimi Desktop chat markdown
- **Author**: Serg2000Mr  
- **Why it matters**: Cyrillic users experience broken letter spacing in markdown blocks on Windows, making text untidy and hard to read.  
- **Link**: [Issue #2552](https://github.com/MoonshotAI/kimi-cli/issues/2552)

### 4. #2545 — [enhancement] Synchronize queued prompts to backend for phone users
- **Author**: vilicvane  
- **Why it matters**: Mobile users lose prompts when switching apps or locking the phone. The request is to queue and flush prompts when the browser returns to foreground.  
- **Link**: [Issue #2545](https://github.com/MoonshotAI/kimi-cli/issues/2545)

### 5. #2538 — [Bug] kimi-datasource plugin worker pool blocks all sessions on timeout
- **Author**: cloxichjc  
- **Why it matters**: **High severity** — when multiple sessions use the `yahoo_finance` plugin, a single failing call can block all concurrent sessions completely. Reported on Linux.  
- **Link**: [Issue #2538](https://github.com/MoonshotAI/kimi-cli/issues/2538)

### 6. #2534 — [Bug] Model API error 400: Unsupported parameter(s): `prompt_cache_key`
- **Author**: dewrama  
- **Why it matters**: Third-party API users (e.g., Nvidia nim models) are broken after v0.29.0 because Moonshot-specific `prompt_cache_key` is now sent to endpoints that don't support it.  
- **Link**: [Issue #2534](https://github.com/MoonshotAI/kimi-cli/issues/2534)

### 7. #2533 — [Feature Request] Per-agent model selection for sub-agents
- **Author**: bob0x-ai  
- **Why it matters**: Developers want cost-tiered multi-agent workflows — cheap models for simple tasks, capable models for complex ones. Currently sub-agents inherit the session's default model.  
- **Link**: [Issue #2533](https://github.com/MoonshotAI/kimi-cli/issues/2533)

---

## Key PR Progress

### 1. #2548 — fix(mcp): reuse initialized client sessions
- **Author**: lihailong00  
- **What it does**: Keeps MCP client sessions open for the toolset lifetime instead of re-initializing on every call. Prevents rejection from strict MCP servers that refuse double `initialize`.  
- **Link**: [PR #2548](https://github.com/MoonshotAI/kimi-cli/pull/2548)

### 2. #2551 — fix(shell): search past file completion limit
- **Author**: lihailong00  
- **What it does**: Improves `@` file completion to search beyond the first 1000 filesystem entries, with bounded budgets (1000 result cap, 10000 scan cap).  
- **Link**: [PR #2551](https://github.com/MoonshotAI/kimi-cli/pull/2551)

### 3. #2549 — fix(shell): index tracked vendor files
- **Author**: lihailong00  
- **What it does**: Allows Git-tracked files under `vendor/` in `@` file completion while still excluding `node_modules` and untracked vendor trees.  
- **Link**: [PR #2549](https://github.com/MoonshotAI/kimi-cli/pull/2549)

### 4. #2547 — fix(windows): configure stdio as utf-8
- **Author**: lihailong00  
- **What it does**: Configures Windows stdout/stderr for UTF-8 at startup, fixing cp936 encoding issues on Windows Terminal.  
- **Link**: [PR #2547](https://github.com/MoonshotAI/kimi-cli/pull/2547)

### 5. #2546 — fix(print): escape markup in echoed stdin prompts
- **Author**: lihailong00  
- **What it does**: Prevents Rich markup interpretation of user input (e.g., `[/login]`) by rendering stdin prompts literally.  
- **Link**: [PR #2546](https://github.com/MoonshotAI/kimi-cli/pull/2546)

### 6. #2543 — fix(hooks): notify on permission prompts
- **Author**: lihailong00  
- **What it does**: Emits documented `permission_prompt` hooks for manual approval, while avoiding duplicate notifications for yolo/AFK/cached approvals.  
- **Link**: [PR #2543](https://github.com/MoonshotAI/kimi-cli/pull/2543)

### 7. #2541 — fix(mcp): continue after deferred startup failure
- **Author**: lihailong00  
- **What it does**: Prevents optional background MCP startup failures from aborting interactive turns. Only `MCPRuntimeError` is caught at the deferred wait boundary.  
- **Link**: [PR #2541](https://github.com/MoonshotAI/kimi-cli/pull/2541)

### 8. #2539 — fix(mcp): normalize tools for Moonshot API
- **Author**: lihailong00  
- **What it does**: Generates stable Moonshot-compatible aliases for MCP tool names and fixes schema shape issues with `object` type and `anyOf`/required distribution.  
- **Link**: [PR #2539](https://github.com/MoonshotAI/kimi-cli/pull/2539)

### 9. #2537 — fix(shell): support numeric keypad input
- **Author**: lihailong00  
- **What it does**: Recognizes DEC application-keypad SS3 sequences from Windows Terminal, inserting keypad digits 0-9 into the prompt buffer.  
- **Link**: [PR #2537](https://github.com/MoonshotAI/kimi-cli/pull/2537)

### 10. #2535 — fix(llm): scope prompt cache keys to Moonshot APIs
- **Author**: Sanjays2402  
- **What it does**: Resolves #2534 by removing `prompt_cache_key` from requests to third-party Kimi-compatible endpoints, while keeping it for official Moonshot APIs.  
- **Link**: [PR #2535](https://github.com/MoonshotAI/kimi-cli/pull/2535)

---

## Feature Request Trends

1. **Remote session continuity**: The ability to transfer or continue CLI sessions across devices (phone, tablet, browser) remains the #1 community desire (#1282, #2545).
2. **Per-agent model selection**: Developers demand granular control over which model powers each sub-agent to enable cost-optimized multi-agent workflows (#2533).
3. **Mobile/web UX parity**: Browser users, especially on phones, want queued prompts to be reliably flushed to the backend even when the app is backgrounded (#2545).

---

## Developer Pain Points

1. **Windows-specific crashes**: The `/plugins` crash with 2+ plugins (#2553) and Cyrillic kerning issues (#2552) highlight ongoing Windows stability gaps. Multiple Windows-focused PRs this sprint indicate the team is addressing this.
2. **Plugin worker pool deadlocks**: The `kimi-datasource` blocking all sessions on timeout (#2538) is a recurring theme — plugin resource isolation remains fragile.
3. **Third-party API compatibility breakage**: The `prompt_cache_key` regression (#2534) broke many users on Nvidia nim and other non-Moonshot endpoints, underscoring the need for stricter provider-specific parameter scoping.
4. **MCP session management**: Implementations are hardening against strict MCP servers that reject duplicate initialization, suggesting real-world MCP ecosystem diversity is higher than expected.

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode Community Digest — 2026-07-24

---

## 1. Today's Highlights

Integration and provider compatibility issues dominated the past 24 hours, with a cluster of reports around false-positive content filtering on `claude-fable-5` which resulted in real billing charges for blocked outputs. The team is actively shipping PRs to improve error handling in the core tool execution layer and to preserve raw finish reasons from providers. A significant cross-cutting concern emerged around subagent lifecycle management, with multiple reports of zombie child processes and infinite loops after tool call completion.

---

## 2. Releases

**No new releases in the last 24 hours.** Latest known version: OpenCode Desktop v1.18.4.

---

## 3. Hot Issues

### #6231 — Auto-discover models from OpenAI-compatible provider endpoints *(187 👍, 30 comments)*
Users currently must manually configure all available models for local providers (LM Studio, Ollama, llama.cpp). This is "tedious and error-prone" as models change frequently. The 187 reactions make this the most upvoted open issue.
[GitHub](https://github.com/anomalyco/opencode/issues/6231)

### #37012 — Keep legacy layout option *(30 👍, 29 comments)*
A vocal community segment prefers the old layout's "easy access to everything from the main window." The new version requires navigation through the app to find options.
[GitHub](https://github.com/anomalyco/opencode/issues/37012)

### #35475 — False positive content-filter on claude-fable-5 — charged ~$20 *(10 comments)*
Three benign queries were blocked by the content filter, yet each cache write was billed at ~$6.69. Total: ~$20 for zero output. Follow-up issue #35643 expands on the billing system bug.
[GitHub](https://github.com/anomalyco/opencode/issues/35475)

### #19130 — Windows ARM64 native: OpenTUI fails to initialize *(8 👍, 13 comments)*
Native ARM64 binary works for CLI commands but TUI fails with a `bun:ffi dlopen TinyCC error`. Blocks Windows on ARM users from interactive sessions.
[GitHub](https://github.com/anomalyco/opencode/issues/19130)

### #27875 — Stuck at permission granting; Enter key not working *(1 👍, 8 comments)*
The subagent requests permission but the Enter key is unresponsive. User resorted to "CTRL+Enter to add a new line" but cannot confirm. Described as a blocking UX defect.
[GitHub](https://github.com/anomalyco/opencode/issues/27875)

### #26220 — Infinite loop after tool calls complete *(3 👍, 7 comments)*
OpenCode enters an infinite loop and stops responding to user input after completing tool calls. Affected version: "Big Pickle." Process stays alive but never exits.
[GitHub](https://github.com/anomalyco/opencode/issues/26220)

### #37326 — Math equations not rendered *(1 👍, 7 comments)*
OpenCode Desktop v1.18.2 fails to render LaTeX math equations. Equations appear as raw text.
[GitHub](https://github.com/anomalyco/opencode/issues/37326)

### #36766 — [2.0] Handle truncated OpenAI tool arguments *(4 comments)*
The native OpenAI Responses path intermittently finalizes tool calls with truncated JSON arguments. V2 correctly rejects malformed input but terminates the entire execution without sufficient diagnostics.
[GitHub](https://github.com/anomalyco/opencode/issues/36766)

### #38564 — Subagent termination does not kill spawned child processes *(2 comments)*
When a task subagent is cancelled, PowerShell child processes continue running at 100% I/O. Only way to stop is manual process kill. Disk abuse risk highlighted.
[GitHub](https://github.com/anomalyco/opencode/issues/38564)

### #38565 — Freeze and main thread block at 1 core full use *(2 comments)*
"Everything freezes" when main thread saturates one CPU core at 100%. User suggests the main thread work could be better split.
[GitHub](https://github.com/anomalyco/opencode/issues/38565)

---

## 4. Key PR Progress

### #38539 — fix(tui): preview written file content
Renders completed writes as block cards with real before/after diffs instead of one-line tool rows. Uses red/green diff rendering for creates, overwrites, and wipes.
[GitHub](https://github.com/anomalyco/opencode/pull/38539)

### #38452 — fix(llm): preserve response message phases
Decodes OpenAI Responses assistant message `phase` values from streamed output items. Replays provider-originated assistant history as complete `ResponseOutputMessage` items with proper metadata.
[GitHub](https://github.com/anomalyco/opencode/pull/38452)

### #38423 — feat(ai): preserve raw finish reasons
Models terminal reasons as `{ normalized, raw }` across all major providers (OpenAI, Anthropic, Gemini, Bedrock). Exposes through `LLMResponse.finishReason`.
[GitHub](https://github.com/anomalyco/opencode/pull/38423)

### #38369 — fix(core): improve patch errors
Identifies malformed add/delete/move hunks with operation paths. Reports matching failures without redundant error prefixes while preserving `tool.execution` classification.
[GitHub](https://github.com/anomalyco/opencode/pull/38369)

### #33553 — feat: enforce tagged error messages *(merged)*
Adds repository-local Oxlint rule requiring `Schema.TaggedErrorClass` to expose a message. Migrates operational errors to field-derived message getters.
[GitHub](https://github.com/anomalyco/opencode/pull/33553)

### #33547 — fix(go): filter models list to only show oa-compat supported models *(merged)*
Fixes `/zen/go/v1/models` returning every model in the lite catalog without checking Go endpoint compatibility.
[GitHub](https://github.com/anomalyco/opencode/pull/33547)

### #33523 — feat: Add LLM and session observability hooks *(merged)*
Adds four observability hooks to the plugin SDK so plugins can observe the real LLM stream, tool execution, and agent-run state.
[GitHub](https://github.com/anomalyco/opencode/pull/33523)

### #33521 — fix(opencode): scope --continue to the current worktree directory *(merged)*
Fixes bug where `opencode --continue` would continue the wrong session in git worktree setups.
[GitHub](https://github.com/anomalyco/opencode/pull/33521)

### #33519 — fix(cli): support headless console login *(merged)*
Skips automatic browser launches on Linux when `xdg-open` is unavailable. Keeps device URL/code flow running in headless containers.
[GitHub](https://github.com/anomalyco/opencode/pull/33519)

### #33505 — feat: Added voice input functionality *(merged)*
Reverts recent configuration changes to restore original stable setup and adds voice input for the coded agent.
[GitHub](https://github.com/anomalyco/opencode/pull/33505)

---

## 5. Feature Request Trends

- **Provider auto-discovery**: The most upvoted request (#6231) is for automatic model discovery from OpenAI-compatible endpoints, eliminating manual configuration for local providers.
- **Subagent visibility**: Multiple requests (#26266, #37267) ask for dedicated views showing subagent reasoning levels, status, and outputs — distinct from the main agent's rapid log updates.
- **Mobile control**: A user wants to connect their phone to check terminal output and send new tasks (#33163).
- **RTL language support**: Proper rendering for right-to-left languages like Arabic in the input field and agent replies (#6284).
- **Customizable layout**: Strong community sentiment for keeping the legacy layout accessible alongside the new UI (#37012).

---

## 6. Developer Pain Points

- **Billing for blocked outputs**: The false-positive content filter issue (#35475, #35643) is particularly damaging — users pay full generation costs for zero delivered output. This erodes trust in the billing system.
- **Permission flow breakage**: Both the Enter key being unresponsive (#27875) and "Always Allow" not persisting (#37880) indicate systemic issues in the permission request UX.
- **Subagent lifecycle leaks**: Zombie child processes surviving cancellation (#38564) and infinite loops after tool calls (#26220) suggest the agent orchestration layer has robustness gaps.
- **Cross-provider compatibility regressions**: The `thinking` vs `reasoning_effort` conflict with Kimi K2.6 (#38329) and DeepSeek V4 failures (#38554) point to insufficient testing across the rapidly expanding provider matrix.
- **Performance degradation**: Main thread freezing (#38565) and TUI crashes on undefined state access (#38574) suggest memory safety or reactivity issues in the rendering layer.

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

# Pi Community Digest — 2026-07-24

**Data Source:** github.com/badlogic/pi-mono (mirror of earendil-works/pi)

---

## 1. Today's Highlights

A major burst of activity hit the repo today with 22 PRs and 50 issues updated in the last 24 hours, signaling the community is closing a batch of long-standing bugs before the next release. Hot topics include a cluster of clipboard and copy-related fixes (three issues/PRs on `wl-copy` alone), early work on constrained/grammar sampling support emerging from prototype to PR, and a community-driven push to add SiliconFlow as a first-class provider alongside better llama.cpp integration. Notably, a flurry of "untriaged" closures suggests maintainers are doing a rapid sweep to triage incoming reports.

## 2. Releases

No new releases in the last 24 hours. The latest published version remains **0.81.1**.

---

## 3. Hot Issues

1. **#6306 — [CLOSED] Support Strict Tools / Grammar**  
   *Opened by mitsuhiko*  
   Lays groundwork for "free form" and "strict" tool support tied to LLM grammar-aware probing (related to #6278). Closed after 22 comments; directly feeds into PR #6341.  
   https://github.com/earendil-works/pi/issues/6306

2. **#6951 — [OPEN] Qwen3.8-max-preview reasoning effort tiers mismatch**  
   *Opened by Demonese*  
   Pi uses `minimal/low/medium/high` but Qwen's API expects `low/medium/xhigh`. A simple config mismatch that blocks correct usage.  
   https://github.com/earendil-works/pi/issues/6951

3. **#6999 — [OPEN] Hot-reload of models.json broken after ModelRuntime (0.80.8+)**  
   *Opened by airpodsp*  
   Power users who edit `models.json` mid-session can no longer reload without restarting. This regression has a pending fix in PR #7036.  
   https://github.com/earendil-works/pi/issues/6999

4. **#6994 — [CLOSED] llama.cpp provider hardcoded 16,384 maxTokens**  
   *Opened by parasyte*  
   All llama.cpp providers were capped at 16,384 output tokens regardless of context window. Immediately fixed in PR #7034.  
   https://github.com/earendil-works/pi/issues/6994

5. **#7026 — [CLOSED] openai-completions gateway-routed prompt_cache_key gate broken**  
   *Opened by johnstegeman*  
   `prompt_cache_key` incorrectly checked for literal `api.openai.com` in baseUrl, breaking gateway-routed models like Cloudflare AI Gateway.  
   https://github.com/earendil-works/pi/issues/7026

6. **#6872 / #7012 — /copy falsely reports success when wl-copy fails**  
   *Opened by calvinalkan and rkfshakti*  
   Duplicate reports: `wl-copy` exit code is never awaited, so sandboxed/bwrap environments get fake success messages and never fall back to xclip/OSC 52. Fix in PR #7009.  
   https://github.com/earendil-works/pi/issues/6872 | https://github.com/earendil-works/pi/issues/7012

7. **#7002 — [CLOSED] Anthropic tool-call ID normalization collision risk**  
   *Opened by yearth*  
   Long foreign IDs truncated during cross-provider conversion could collide. Closed as "no-action" after maintainer analysis.  
   https://github.com/earendil-works/pi/issues/7002

8. **#6970 — [OPEN] GitHub Copilot Plugin auth causes token invalidation on multi-device**  
   *Opened by bittervec*  
   Pi uses the non-standard "GitHub Copilot Plugin" OAuth flow instead of proper OAuth, causing token invalidation when used alongside `copilot-lsp`/neovim on two devices.  
   https://github.com/earendil-works/pi/issues/6970

9. **#7033 — [CLOSED] Malformed package manifest crash-loops session boot**  
   *Opened by EzraEllette*  
   A single misconfigured installed package (e.g., `"skills": "./skills"` instead of `["./skills"]`) causes an unrecoverable crash on every startup. Urgent fix needed for package authors.  
   https://github.com/earendil-works/pi/issues/7033

10. **#7027 — [CLOSED] API-key login hangs when model catalog refresh stalls**  
    *Opened by possibilities*  
    `/login openrouter` can leave the TUI permanently stuck after key submission if the model-catalog request times out. Credential is saved but UI never recovers.  
    https://github.com/earendil-works/pi/issues/7027

---

## 4. Key PR Progress

1. **#6341 — [to-discuss] feat(ai): support constrained sampling**  
   *Author: mitsuhiko*  
   Opt-in `constrainedSampling` config for tools enabling JSON-schema constrained (strict) tool input generation at the provider level. Lays foundation for grammar-aware sampling.  
   https://github.com/earendil-works/pi/pull/6341

2. **#7036 — [OPEN] fix(coding-agent): reload model config in picker**  
   *Author: mitsuhiko*  
   Direct fix for #6999 (hot-reload broken); restores ability to edit `models.json` mid-session and see changes in `/model`.  
   https://github.com/earendil-works/pi/pull/7036

3. **#7034 — [CLOSED] fix(coding-agent): use llama context for output limit**  
   *Author: christianklotz*  
   Removes the hardcoded 16,384-token cap for llama.cpp providers; derives max output tokens from each model's actual context window.  
   https://github.com/earendil-works/pi/pull/7034

4. **#7009 — [CLOSED] fix: await wl-copy exit code and fall through to xclip**  
   *Author: rkfshakti*  
   The `/copy` command now properly awaits `wl-copy` exit and falls back to `xclip`/OSC 52 on failure. Fixes #6872 and #7012.  
   https://github.com/earendil-works/pi/pull/7009

5. **#7031 — [OPEN] fix(coding-agent): keep model registry tests offline**  
   *Author: tmustier*  
   CI was failing due to network timeouts hitting the pi.dev Anthropic model catalog. Disables networking for model registry tests.  
   https://github.com/earendil-works/pi/pull/7031

6. **#7017 — [CLOSED] feat(tui): experimental support for limited repainting**  
   *Author: mitsuhiko*  
   Experimental setting to avoid repainting the entire transcript on long sessions—greatly improves performance for power users.  
   https://github.com/earendil-works/pi/pull/7017

7. **#6965 — [CLOSED] fix: isolate test environment**  
   *Author: christianklotz*  
   Hardens the test suite by running from an explicit environment allowlist, isolating home/temp/Git/npm/XDG state. Reduces flaky tests across platforms.  
   https://github.com/earendil-works/pi/pull/6965

8. **#7028 — [CLOSED] fix(coding-agent): keep /resume unfiltered after a resume**  
   *Author: simonckemper*  
   Running `/resume` inside a session already started via `/resume` collapsed results to a single self-reference. Now idempotent.  
   https://github.com/earendil-works/pi/pull/7028

9. **#7011 — [OPEN] fix(coding-agent): share host modules with native ESM extensions**  
   *Author: haoqixu*  
   Extensions could load private copies of Pi packages via Jiti native imports, causing module state divergence. Intercepts native imports to reuse host modules.  
   https://github.com/earendil-works/pi/pull/7011

10. **#6980 — [CLOSED] fix(ai): make provider retries abortable**  
    *Author: petrroll*  
    Replaces Anthropic/OpenAI SDK inner retries with a common abortable helper that respects `maxRetryDelayMS` and `AbortSignal`. Fixes #6911.  
    https://github.com/earendil-works/pi/pull/6980

---

## 5. Feature Request Trends

- **SiliconFlow as a built-in provider** — Two issues (#4742, #7013) request SiliconFlow, an aggregator similar to OpenRouter hosting Qwen, GLM, and other open models. Community interest is high, with multiple users independently filing.
- **Grammar-aware / constrained tool input** — #6306 and PR #6341 represent a major push for "strict" tools and JSON-schema constrained sampling, enabling more reliable tool execution.
- **Per-message thinking labels** — PR #7018 adds `hiddenThinkingLabel` to `AssistantMessage`, allowing extensions to show per-message thinking duration rather than a single global label.
- **Argument-hint frontmatter for skills** — #5799 requests parity with prompts for skill argument hints (spec compliance).
- **Provider model catalog improvements** — Several issues request better fallback diagnostics for unavailable models (#7032), scoped model configurability, and hot-reload (#6999).

---

## 6. Developer Pain Points

- **Clipboard/sandbox friction** — Three separate reports (#6872, #7012, #7013) highlight `/copy` always claims success even in sandboxed/bwrap environments because `wl-copy` exit codes are ignored. PR #7009 addresses this.
- **Race conditions at startup** — #6948 reports that the default model/provider in `settings.json` is not applied at startup because async model refresh races with session initialization.
- **Package manifest fragility** — #7033 shows that a single malformed `package.json` (`"skills": "./skills"` instead of `["./skills"]`) crash-loops the entire session at boot with no recovery path.
- **Auth flow confusion** — #6970 reveals Pi uses a non-standard "GitHub Copilot Plugin" OAuth flow, causing token invalidation when used alongside other Copilot clients on multiple devices.
- **CJK text rendering broken** — #7021: Up/Down cursor navigation computes visual column in UTF-16 code units, so CJK characters (2 display columns, 1 code unit) cause vertical cursor misplacement.
- **Home-path abbreviation edge cases** — #7006: `path.startsWith(homedir())` renders `/Users/alice-work/file.ts` as `~-work/file.ts`, making sibling directories look like they're inside `~`.

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code Community Digest — 2026-07-24

## Today's Highlights
The past 24 hours saw a flurry of activity with 50 PRs and 44 issues, though no new releases were cut. A batch of CI failures on `main` (E2E and release pipeline) consumed significant maintainer attention, while several long-standing bugs around update checking (npm 12 and `mise` compatibility) were finally closed. On the feature front, proposals for enterprise memory integration and external context providers signal growing interest in making Qwen Code suitable for organizational deployments.

## Releases
No new releases in the last 24 hours. The latest public release remains v0.20.1.

## Hot Issues (Top 10)

1. **[#5736](https://github.com/QwenLM/qwen-code/issues/5736) — Full prompt reprocessing after recent update** (7 comments, CLOSED)  
   A user reports that `llama.cpp` logs show forced full prompt re-processing even during simple conversation continuation. This is a performance regression in the caching layer that directly affects local LLM users with limited context windows. Community upvoted once.

2. **[#7599](https://github.com/QwenLM/qwen-code/issues/7599) — Workspace artifacts created via `record_artifact` have no `managedId`** (5 comments, CLOSED)  
   Internal artifacts written to the workspace (e.g., HTML files) are emitted without a `managedId`, breaking the managed-artifact contract. This affects anyone relying on `sse.artifact_changed` events for downstream tooling.

3. **[#7449](https://github.com/QwenLM/qwen-code/issues/7449) — Proposal: Enterprise external-memory integration profile** (5 comments, OPEN)  
   A detailed proposal defining a provider-neutral interface for plugging Qwen Code into enterprise knowledge stores (e.g., Confluence, SharePoint). The discussion has converged on a documentation-first approach with incremental compatibility tests. No Core API changes required.

4. **[#7485](https://github.com/QwenLM/qwen-code/issues/7485) — TUI: Large blank area between last message and input after resume** (4 comments, OPEN)  
   After `qwen resume`, the terminal UI renders a large empty gap between the conversation history and the input prompt. Annoying for daily interactive users, and labeled `welcome-pr`.

5. **[#7264](https://github.com/QwenLM/qwen-code/issues/7264) — Cold-start follow-ups: remaining lazy-loading candidates from ACP eager-closure audit** (4 comments, OPEN)  
   An esbuild-based audit found that the ACP child process eagerly loads 17.24 MiB / 2420 modules on every cold start before it can respond to `initialize`. This issue tracks the remaining modules that could be lazy-loaded. Directly impacts startup latency.

6. **[#6014](https://github.com/QwenLM/qwen-code/issues/6014) — New version no longer shows which file the agent read** (4 comments, OPEN)  
   A UX regression: read operations now show `read 1 file` instead of the actual filename. Commenters call this a "downgrade" and request the filenames be restored.

7. **[#6806](https://github.com/QwenLM/qwen-code/issues/6806) — Status line context usage doesn't refresh after `/compress`** (4 comments, OPEN)  
   The footer token-counter stays stuck at pre-compression values until the next model request. Minor but confusing for users trying to manage context windows in local LLM setups.

8. **[#5958](https://github.com/QwenLM/qwen-code/issues/5958) — Web Shell CodeMirror not working on mobile browsers** (3 comments, CLOSED)  
   The input editor is non-functional on iOS Safari and Android Chrome. Core usability issue for web-first users.

9. **[#7287](https://github.com/QwenLM/qwen-code/issues/7287) — Auto-memory MEMORY.md not registered in FileReadCache** (3 comments, CLOSED)  
   The auto-memory system loads `MEMORY.md` into the system prompt but doesn't register it in `FileReadCache`, so `write_file` is rejected because `checkPriorRead()` returns false. Blocks the core memory update workflow.

10. **[#7616](https://github.com/QwenLM/qwen-code/issues/7616) — Do we really need this many E2E tests?** (2 comments, OPEN)  
    A maintainer questions whether 30+ E2E failures in 12 days (mostly non-deterministic) are worth the CI burden. Proposes replacing brittle model-API-dependent tests with deterministic unit tests. Reflects growing CI fatigue.

## Key PR Progress (Top 10)

1. **[#7268](https://github.com/QwenLM/qwen-code/pull/7268) — feat(serve): Hot-reload workspace trust changes**  
   Enables workspace trust policy changes without restarting the daemon. Uses semantic snapshots and per-workspace runtime generations. Useful for enterprise multi-tenant setups.

2. **[#7471](https://github.com/QwenLM/qwen-code/pull/7471) — feat(web-shell): git mode selector for new session creation**  
   Adds a unified git workflow selector (current branch, new branch, or detached HEAD) to the Web Shell session creation flow. Embedded in the composer chip popover.

3. **[#7607](https://github.com/QwenLM/qwen-code/pull/7607) — feat(core): configurable image generation models**  
   Adds a user-configured image generation model alongside existing voice/vision model selections. Includes a built-in approval-gated tool that saves verifiable outputs.

4. **[#7302](https://github.com/QwenLM/qwen-code/pull/7302) — feat(cli): prior session references via `@` and completion tabs**  
   Enables project-scoped prior session completion via `@session:<id>`, inserting a deterministic read-only transcript summary. Improves multi-session workflows.

5. **[#7469](https://github.com/QwenLM/qwen-code/pull/7469) — feat(ci): intelligent core review router**  
   Replaces blanket CODEOWNERS with a GitHub Actions workflow that analyzes changed paths, diff complexity, and author history to route review requests to the most relevant maintainer.

6. **[#6451](https://github.com/QwenLM/qwen-code/pull/6451) — refactor(cli): Fleet View rewrite to match Claude Code UI**  
   A significant rewrite of the multi-session Fleet View, bringing it closer to the Claude Code agent view UI pattern. Has been open for 17 days — likely a large, high-impact change.

7. **[#7620](https://github.com/QwenLM/qwen-code/pull/7620) — fix(web-shell): parse 256-color and truecolor SGR sequences**  
   Fixes `parseAnsi` to properly consume extended color arguments (`38`/`48`/`58`) instead of treating each parameter as a standalone code. Directly fixes rendering in the web shell.

8. **[#7531](https://github.com/QwenLM/qwen-code/pull/7531) — fix(core): close force-flag and checkout gaps in destructive-git guard**  
   Widens `DESTRUCTIVE_GIT_PATTERNS` so `git clean` and `git checkout` are blocked in all spellings, not just the most common ones. Safety fix.

9. **[#7580](https://github.com/QwenLM/qwen-code/pull/7580) — feat: visualize ordinary-session plan execution**  
   Adds a Session Workflow view that projects Todo plans, Agent executions, and the transcript into a dependency graph with stable node IDs and `blockedBy` edges.

10. **[#6096](https://github.com/QwenLM/qwen-code/pull/6096) — feat(tool): opt-in zvec-grep search tool**  
    Integrates `zvec_grep` as a first-class workspace search tool offering both semantic search and regex/regex-like exact search. Supports scoped search over project directories. Open for 23 days — likely awaiting review of the new dependency.

## Feature Request Trends
- **Enterprise integration**: Multiple proposals ([#7449](https://github.com/QwenLM/qwen-code/issues/7449), [#7585](https://github.com/QwenLM/qwen-code/issues/7585)) target making Qwen Code pluggable into corporate knowledge stores and external memory services. The common pattern is a provider-neutral profile that doesn't require core API changes.
- **Session and workspace workflows**: Features like prior session references ([#7302](https://github.com/QwenLM/qwen-code/pull/7302)), plan visualization ([#7580](https://github.com/QwenLM/qwen-code/pull/7580)), and git mode selectors ([#7471](https://github.com/QwenLM/qwen-code/pull/7471)) all point toward richer session lifecycle management.
- **Image and video input**: Support for configurable image generation models ([#7607](https://github.com/QwenLM/qwen-code/pull/7607)) and native video input in `/learn` ([#7497](https://github.com/QwenLM/qwen-code/pull/7497)) show growing modality ambitions.

## Developer Pain Points
- **Update check failures**: Three separate issues ([#7543](https://github.com/QwenLM/qwen-code/issues/7543), [#7520](https://github.com/QwenLM/qwen-code/issues/7520), [#7515](https://github.com/QwenLM/qwen-code/issues/7515)) report the `/update` and startup update checks breaking — two caused by npm 12 compatibility, one by `mise` wrapping the npm binary. This is a high-frequency support burden.
- **CI flakiness**: E2E tests on `main` fail repeatedly ([#7516](https://github.com/QwenLM/qwen-code/issues/7516), [#7559](https://github.com/QwenLM/qwen-code/issues/7559), [#7605](https://github.com/QwenLM/qwen-code/issues/7605)), and issue [#7616](https://github.com/QwenLM/qwen-code/issues/7616) explicitly questions the value of non-deterministic tests. CI reliability is a recurring theme.
- **Mobile and Web Shell usability**: The CodeMirror mobile issue ([#5958](https://github.com/QwenLM/qwen-code/issues/5958)) and the TUI blank-area bug ([#7485](https://github.com/QwenLM/qwen-code/issues/7485)) illustrate ongoing web and terminal UI polish gaps.
- **Permissions and caching corner cases**: The auto-memory `FileReadCache` bug ([#7287](https://github.com/QwenLM/qwen-code/issues/7287)) and the Telegram topic routing fix ([#7609](https://github.com/QwenLM/qwen-code/issues/7609)) reveal integration complexity that frustrates users relying on channel/automation features.

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

# DeepSeek TUI Community Digest — 2026-07-24

**Note:** The project has been rebranded from "DeepSeek TUI" to **CodeWhale**. This digest tracks the repository `github.com/Hmbown/CodeWhale`.

---

## 1. Today's Highlights

The CodeWhale community is in the final stages of the v0.9.1 release gate, with a mandatory security scan and dependency alert disposition in progress. A stop-ship bug (immediate TUI exit on macOS) was opened and is under investigation, while the team is actively merging UX polish PRs—including archived shell output and editable previews. Several legacy "DeepSeek-era" branding artifacts remain in the settings menu, signaling ongoing migration debt.

---

## 2. Releases

**No new releases in the last 24 hours.** The latest candidate is `v0.9.1 (0dfe9170)`, which is undergoing security auditing before tagging.

---

## 3. Hot Issues (10 selected)

| Issue | Status | Title | Why It Matters |
|-------|--------|-------|----------------|
| [#4042](https://github.com/Hmbown/CodeWhale/issues/4042) | **CLOSED** | feat: Environment-level tool sandboxing for sub-agents | Core security infrastructure for multi-agent sandboxing. Confirmed `--disallowed-tools` works; now enforcing at session, sub-agent, Fleet, and MCP levels. Community consensus on design. |
| [#4713](https://github.com/Hmbown/CodeWhale/issues/4713) | OPEN | v0.9.1 security gate: deep scan and dependency alert disposition | **Release blocker.** 17 open Dependabot alerts (7 high, 10 moderate). Affects `axios`, `body-parser`, `express` among others. Team must disposition each before tagging. |
| [#4716](https://github.com/Hmbown/CodeWhale/issues/4716) | OPEN | TUI: exits immediately on launch (`[Process completed]`) | **Stop-ship bug.** Fresh macOS Terminal.app tabs die instantly; v0.9.1 candidate affected. Root cause not yet confirmed. High urgency. |
| [#4719](https://github.com/Hmbown/CodeWhale/issues/4719) | OPEN | Composer: large pasted prompts get byte-corrupted | Path truncation (`codewhale-v091...` → `work-88a158-ci`) and line mangling on paste. Breaks agent workflows relying on exact paths. |
| [#4723](https://github.com/Hmbown/CodeWhale/issues/4723) | OPEN | AltGr+Q on Brazilian ABNT2 opens help overlay instead of typing "/" | Keyboard layout bug on Windows. `AltGr+Q` (the `/` key) is reported as `Ctrl+Alt+Q`, conflicting with an accelerator. Affects non-English developers. |
| [#4717](https://github.com/Hmbown/CodeWhale/issues/4717) | OPEN | Settings: legacy "DeepSeek fallback model" shown on non-DeepSeek providers | UI debt: when provider is `zai`/`GLM-5.2`, the settings still display a prominent "DeepSeek fallback model" row. Confusing for multi-provider users. |
| [#4720](https://github.com/Hmbown/CodeWhale/issues/4720) | OPEN | Provider/model setup and auto-switching feel under-baked | Runtime auto-switched `deepseek → zai` without clear user visibility. No deliberate UX for provider/model transitions. |
| [#4718](https://github.com/Hmbown/CodeWhale/issues/4718) | OPEN | TUI transcript: information density too high | Repetitive "Option+V to inspect" hints on every tool card; stacked reasoning states. Clutters terminal output. |
| [#4721](https://github.com/Hmbown/CodeWhale/issues/4721) | OPEN | Settings menu audit: catalog legacy / density / labeling issues | Tracking issue for broader settings UX cleanup after fixing specific menu bugs. |
| [#4519](https://github.com/Hmbown/CodeWhale/issues/4519) | OPEN | *Not shown in 24h, but contextually relevant:* `[v0.9.1]` Completion board | Parent issue for the v0.9.1 release board, tracking all work items for this release. |

---

## 4. Key PR Progress (6 selected — all updated in last 24h)

| PR | Status | Title | Key Detail |
|----|--------|-------|------------|
| [#4724](https://github.com/Hmbown/CodeWhale/pull/4724) | OPEN | fix(tui): archive completed background shell output | Archives final visible stdout/stderr tail into originating ExecCell; freezes display duration. Reduces terminal clutter. |
| [#4346](https://github.com/Hmbown/CodeWhale/pull/4346) | **CLOSED** | fix: sanitize tool input_schema for Anthropic adapter | Hotfix merged: removes `oneOf`/`anyOf`/`allOf` from top-level tool `input_schema` to prevent Anthropic HTTP 400 rejection. |
| [#4722](https://github.com/Hmbown/CodeWhale/pull/4722) | OPEN | fix(tui): show complete edit previews in details | Keeps compact `edit_file` cards, builds full `-/+` diff in Alt+V details pager. Adds regression test. |
| [#4610](https://github.com/Hmbown/CodeWhale/pull/4610) | OPEN | feat(tui): add configurable session token header | Opt-in `header_items = ["tokens"]` shows cumulative input/cache-hit/output token counts. Targets v0.9.2. |
| [#4679](https://github.com/Hmbown/CodeWhale/pull/4679) | **CLOSED** | feat(skills): unified /skills manager with audit and owned mutations | Delivered on v0.9.1 board: `/skills` manager for inventory, audit, install/import, update, remove, trust. |
| [#4087](https://github.com/Hmbown/CodeWhale/pull/4087) | OPEN | refactor(hooks): split config and executor modules | Separates hook config definitions from execution runtime, improving reviewability. Targets v0.9.3. |

---

## 5. Feature Request Trends

- **Configurable UI headers:** Token counters, customizable header items ([#4610](https://github.com/Hmbown/CodeWhale/pull/4610)). High community interest in monitoring token usage without external tools.
- **Unified skills management:** Centralized `/skills` CLI for lifecycle operations ([#4679](https://github.com/Hmbown/CodeWhale/issues/4679)). The merged PR landed in v0.9.1.
- **Provider-agnostic settings:** Remove DeepSeek-specific branding from non-DeepSeek provider views ([#4717](https://github.com/Hmbown/CodeWhale/issues/4717), [#4720](https://github.com/Hmbown/CodeWhale/issues/4720)). Users want a generic "fallback model" concept.
- **Transparent provider switching:** Better user awareness when the runtime auto-switches providers/models ([#4720](https://github.com/Hmbown/CodeWhale/issues/4720)).
- **Security hardening:** Mandatory security gates before releases; environment-level tool sandboxing for sub-agents ([#4042](https://github.com/Hmbown/CodeWhale/issues/4042), [#4713](https://github.com/Hmbown/CodeWhale/issues/4713)).

---

## 6. Developer Pain Points

- **Stop-ship bugs blocking releases:** The "TUI exits immediately" bug ([#4716](https://github.com/Hmbown/CodeWhale/issues/4716)) on macOS is a showstopper for v0.9.1 tagging.
- **Paste corruption in Composer:** Large multi-line prompts losing bytes before submission ([#4719](https://github.com/Hmbown/CodeWhale/issues/4719)). Workflow-breaking for any developer using long inputs.
- **Keyboard layout incompatibility:** Windows ABNT2 users cannot type `/` ([#4723](https://github.com/Hmbown/CodeWhale/issues/4723)). Blocks basic TUI navigation for Brazilian developers.
- **High information density in TUI:** Repeated hints and stacked reasoning states clutter the transcript ([#4718](https://github.com/Hmbown/CodeWhale/issues/4718)).
- **Legacy branding debt:** The settings menu still prominently shows "DeepSeek fallback model" even when the active provider is not DeepSeek ([#4717](https://github.com/Hmbown/CodeWhale/issues/4717)). Confusing for multi-provider setups.
- **Dependency alert backlog:** 17 unaddressed Dependabot alerts (7 high) blocking the v0.9.1 release ([#4713](https://github.com/Hmbown/CodeWhale/issues/4713)). Team must manually triage each.
- **Provider switching opacity:** The runtime switches providers without clear user-facing indication ([#4720](https://github.com/Hmbown/CodeWhale/issues/4720)). Developers want control and visibility over the routing decisions.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/kky-wollu/agents-radar).*