# AI CLI Tools Community Digest 2026-07-27

> Generated: 2026-07-26 23:02 UTC | Tools covered: 9

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

# AI CLI Developer Tools: Cross-Tool Comparison Report
**Analysis Date:** 2026-07-27

---

## 1. Ecosystem Overview

The AI CLI tools ecosystem is experiencing rapid maturation, with all major tools—Claude Code, OpenAI Codex, Gemini CLI, GitHub Copilot CLI, Qwen Code, OpenCode, and Pi (DeepSeek TUI)—showing active community engagement and continuous iteration. A clear bifurcation is emerging between **established enterprise tools** (Claude Code, Codex, Copilot CLI) focused on reliability and security hardening, and **rapidly evolving challengers** (Qwen Code, OpenCode, DeepSeek TUI) shipping high-velocity feature additions. The dominant cross-cutting themes are Multi-Agent orchestration lifecycle control, MCP (Model Context Protocol) infrastructure reliability, Windows platform parity, and session/data management scalability. Bug reports increasingly center on **silent failures**, **state drift**, and **security boundary enforcement** across sandbox, IPC, and authorization planes.

---

## 2. Activity Comparison

| Tool | Issues (24h) | PRs (24h) | Release Today | Key Focus Area |
|---|---|---|---|---|
| **Claude Code** | 10 hot (5 open, 5 closed) | 8 (all open) | None | Security hardening, Windows parity, sandbox fallback |
| **OpenAI Codex** | 10 hot (all tracked) | 8 merged, 2 open | None | MCP OAuth refactoring (6+ PRs merged), TUI performance |
| **Gemini CLI** | 10 hot | 6 (5 open, 1 closed) | Nightly v0.54.0 (no changes) | Security (variable expansion bypass, keychain validation) |
| **GitHub Copilot CLI** | 10 hot | 0 | None | Zombie processes, Windows crash, MCP OAuth refresh |
| **OpenCode** | 10 hot (6 open, 4 closed) | 10 (6 open, 4 closed) | None | Subagent lifecycle, MCP TUI management, Go subscription bugs |
| **Pi** | 10+ issues (6 closed, 4 open) | 10 (2 open, 8 closed) | None | TUI performance, WSL paths, CVE fix, compaction API |
| **Qwen Code** | 10 hot | 10 (all open) | Nightly v0.21.0 | Security disclosures (3 P1), daemon latency, E2E CI |
| **DeepSeek TUI** | 10 hot | 8 merged, 1 open | None | Streaming perf, prompt caching, background shell completions |

**Notable Observations:**
- **DeepSeek TUI** had the highest merge velocity (8 PRs merged in 24h)
- **Qwen Code** filed the most security-critical issues (3 P1 disclosures in one day)
- **GitHub Copilot CLI** had zero PR activity but active triage closure
- **Gemini CLI** shipped a nightly release with zero functional changes—indicates stabilization phase
- **OpenCode** leads in subagent lifecycle feature requests (4 related issues from same author)

---

## 3. Shared Feature Directions

| Requirement | Affected Tools | Specific Needs Expressed |
|---|---|---|
| **Multi-Agent/Subagent Lifecycle Control** | Claude Code, OpenAI Codex, Gemini CLI, OpenCode, Pi, DeepSeek TUI | Per-agent cancellation, peer-to-peer communication, hierarchical dispatch, trajectory visibility in logs |
| **MCP Infrastructure Reliability** | Claude Code, OpenAI Codex, GitHub Copilot CLI, OpenCode, Qwen Code, Pi | OAuth token refresh serialization, IPC authorization enforcement, stdio connection degradation, server memory leaks |
| **Windows Platform Parity** | Claude Code, OpenAI Codex, GitHub Copilot CLI, Pi | MSIX sandbox conflicts, WSL path handling, Smart App Control, exit crashes, process reaping |
| **Session/Daemon State Management** | Claude Code, OpenAI Codex, Gemini CLI, Qwen Code, Pi | Context window size drift, lock handoff on crash, compaction lifecycle API, multi-workspace daemon support |
| **Prompt Caching / Cost Optimization** | OpenAI Codex, OpenCode, DeepSeek TUI | Cache control breakpoints, cacheable prefix pinning, variable metadata busting cache |
| **Security Boundary Enforcement** | Claude Code, Gemini CLI, Qwen Code | Sandbox fallback fail-closed, IPC authorization, variable expansion bypass, SSE session replay |
| **BYOK / Custom Provider Support** | GitHub Copilot CLI, DeepSeek TUI | Interactive prompt parity, offline first-run, provider negotiation |
| **TUI Performance Under Load** | Claude Code, OpenAI Codex, Pi, DeepSeek TUI | O(N²) rendering, cache thrashing, non-ASCII line handling, streaming re-parse |

**Most Cross-Tool Demand:** Multi-agent lifecycle control appears in every tool's digest—the community consensus is that current subagent management is too opaque, with no per-agent cancellation, limited communication channels, and deceptive success reporting.

---

## 4. Differentiation Analysis

| Dimension | Claude Code | OpenAI Codex | Gemini CLI | GitHub Copilot CLI | Qwen Code | OpenCode | Pi | DeepSeek TUI |
|---|---|---|---|---|---|---|---|---|
| **Primary User** | Power devs, security teams | Full-stack devs, MCP ecosystem | Google ecosystem devs | Enterprise GitHub shops | Server-side/CI devs | Cost-sensitive devs | Hobbyists, automation | DeepSeek V4 users |
| **Strengths** | Classifier precision, agent teams | OAuth maturity, multi-agent config | Security audit culture | Enterprise auth, MCP registry | Daemon architecture, CI integration | Subagent UX, pricing flexibility | TUI perf, extension system | Streaming perf, prompt caching |
| **Weaknesses** | Windows parity, Cowork bloat | Session data bloat (100+ GiB) | Subagent GOAL false success | Zombie processes, Windows crash | E2E instability, gitignore bugs | Go subscription regressions | Silent data loss, proxy issues | iTerm2 compatibility, localization gaps |
| **Technical Approach** | Bundled Cowork service, sandbox classifier | OAuth stack, multi-agent V2 | Variable expansion detection, AST tooling | libuv-based, NFS/GPFS focus | Daemon-per-workspace, SSE sessions | Event-sourced, OpenRouter | Compact/binary, extension runtime | WebSocket streaming, policy engine |
| **Community Engagement** | High (top issue 39👍) | High (top issue 89👍) | Moderate (top issue 8👍) | Low (top issue 3👍) | Moderate (30 comments on RFC) | High (83👍 on price cut) | Moderate (8 comments top issue) | High (17 comments on constitution) |

**Key Differentiators:**
- **Qwen Code** is the only tool with dedicated daemon/server architecture—positions for CI/CD and managed deployments
- **OpenCode** has the strongest price-conscious userbase (83👍 for passing DeepSeek cost cuts)
- **GitHub Copilot CLI** has the least community engagement by upvote count but targets enterprise users who may not upvote
- **Pi** has the deepest TUI performance analysis (Intl.Segmenter, cache thrash, Markdown re-parse)
- **Gemini CLI** leads security PR throughput with 2 hardening PRs in one day

---

## 5. Community Momentum & Maturity

| Metric | Claude Code | OpenAI Codex | Gemini CLI | Copilot CLI | Qwen Code | OpenCode | Pi | DeepSeek TUI |
|---|---|---|---|---|---|---|---|---|
| **Iteration Velocity** | Medium | High | Low | Very Low | High | Very High | Very High | Highest (8 merged/day) |
| **Issue Engagement** | High (39👍 top) | High (89👍 top) | Moderate (8👍 top) | Low (3👍 top) | Moderate (30 comments) | Very High (83👍 top) | Moderate (8 comments) | High (17 comments) |
| **Security Maturity** | High (PRs for sandbox, firewall) | High (OAuth stack merged) | High (2 security PRs today) | Low (no security PRs) | Medium (3 P1 disclosures) | Medium (Bash permission issues) | Low (CVE fixed) | Low (no security PRs) |
| **Stability Risk** | Medium (regressions in compact) | High (100GiB session bloat) | High (agent hangs, false success) | High (zombie leak, Windows crash) | Medium (E2E flakiness) | Medium (Go subscription bugs) | High (silent data loss) | Medium (streaming perf fixed) |
| **Ecosystem Breadth** | Broad (MCP, Cowork, Teams) | Broad (OAuth, multi-account) | Narrow (Google-focused) | Narrow (GitHub-focused) | Broad (Daemon, ACP, sandbox) | Broad (OpenRouter, MCP) | Medium (extensions, CVE) | Medium (DeepSeek-focused) |

**Maturity Summary:**
- **Claude Code** and **OpenAI Codex** are most mature, with comprehensive security practices and broad ecosystems—but show regression risk from feature velocity
- **OpenCode** and **DeepSeek TUI** have highest community energy and merge velocity, but less security hardening
- **Gemini CLI** and **GitHub Copilot CLI** appear to be in **stabilization**—low PR velocity, few new features, focus on bug fixes
- **Pi** shows strong technical depth in TUI performance but concerning patterns of silent data loss bugs

---

## 6. Trend Signals

### For Developers Evaluating Tools:

1. **Multi-Agent Orchestration** is the #1 unsolved problem. No tool has satisfactory per-agent cancellation, trajectory visibility, or peer-to-peer communication. If you need complex multi-agent workflows, expect frustration regardless of tool choice.

2. **MCP is entering reliability phase.** The massive OAuth refactoring in Codex and security disclosures in Qwen Code signal that MCP infrastructure is being hardened. Early MCP adopters should expect breaking changes and auth flow improvements.

3. **Windows remains second-class.** Claude Code, Codex, Copilot CLI, and Pi all have Windows-specific bugs that are lower priority. If your team is Windows-heavy, Qwen Code's daemon architecture may be more reliable.

4. **Cost optimization is becoming a competitive differentiator.** OpenCode's 83-upvote price-cut issue and DeepSeek TUI's prompt caching fixes show users are increasingly cost-sensitive. Tools that don't optimize token usage will lose users.

5. **Enterprise security expectations are rising.** Claude Code's sandbox PRs, Gemini CLI's variable expansion fix, and Qwen Code's IPC disclosures all point to growing demand for hardened security boundaries—especially in CI/CD contexts.

6. **TUI performance is a hidden UX differentiator.** DeepSeek TUI and Pi both invested heavily in streaming rendering optimization. Users who run long sessions will notice the difference between O(N²) and O(1) rendering.

7. **Silent failure is the most dangerous pattern.** Across all tools—Claude Code's phantom tool-call loops, Gemini CLI's false GOAL success, Pi's compact race condition, Copilot CLI's zombie processes—silent failures erode trust faster than visible crashes.

### For Tool Vendors:

- **Invest in subagent lifecycle APIs**—this is the clearest unmet need across the ecosystem
- **Fix Windows parity** before it becomes a blocker for enterprise adoption
- **Make prompt caching observable**—users want to see when caching is working
- **Add deterministic CI gates** (as Qwen Code PR #7751 does) to reduce agent-dependency in testing
- **Prioritize session state consistency**—drift between GUI/CLI/remote breaks user trust faster than missing features

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills Community Highlights Report
**Data Snapshot:** 2026-07-27 | **Source:** [anthropics/skills](https://github.com/anthropics/skills)

---

## 1. Top Skills Ranking

The following Skills attracted the most discussion and community engagement:

| # | Skill | Author | Status | Description |
|---|-------|--------|--------|-------------|
| 1 | **Skill-Creator Fixes (PR #1298)** | [MartinCajiao](https://github.com/MartinCajiao) | **Open** | Fixes the critical `run_eval.py` bug causing 0% recall across all evaluations. Addresses Windows stream reading, trigger detection, and parallel workers. This PR resolves the most impactful bug in the ecosystem (linked to Issue #556, 12+ comments, 7👍). **Status:** Open, high activity |
| 2 | **Document Typography (PR #514)** | [PGTBoos](https://github.com/PGTBoos) | **Open** | Prevents orphan word wrap, widow paragraphs, and numbering misalignment in AI-generated documents. Addresses a universal pain point for Claude-generated content. **Status:** Open |
| 3 | **ODT Skill (PR #486)** | [GitHubNewbie0](https://github.com/GitHubNewbie0) | **Open** | Creates, fills, reads, and converts OpenDocument Format files (.odt, .ods). Covers LibreOffice integration and ISO standard document production. **Status:** Open |
| 4 | **Self-Audit Skill v1.3.0 (PR #1367)** | [YuhaoLin2005](https://github.com/YuhaoLin2005) | **Open** | A reasoning quality gate that performs mechanical file verification followed by a four-dimension reasoning audit. Universal across projects and tech stacks. **Status:** Open, recent |
| 5 | **Self-Audit Skill (PR #1367)** | [YuhaoLin2005](https://github.com/YuhaoLin2005) | **Open** | Audits AI output before delivery — mechanical verification + reasoning quality check. Universal applicability. **Status:** Open |
| 6 | **Testing Patterns Skill (PR #723)** | [4444J99](https://github.com/4444J99) | **Open** | Comprehensive testing coverage: unit testing (AAA pattern), React component testing (Testing Library), integration testing, and E2E testing patterns. **Status:** Open |
| 7 | **Color Expert Skill (PR #1302)** | [meodai](https://github.com/meodai) | **Open** | Self-contained color expertise covering naming systems (ISCC-NBS, Munsell, XKCD, RAL), color spaces, and "what to use when" tables. **Status:** Open |
| 8 | **Pyxel Retro Game Dev (PR #525)** | [kitao](https://github.com/kitao) | **Open** | Integrates with the Pyxel retro game engine via MCP server. Covers pixel-art/8-bit game creation workflow. **Status:** Open |

**Discussion Highlights:**
- **PR #1298** (skill-creator fix) is the most critical PR — it addresses the `run_eval.py` 0% recall bug that renders the entire description-optimization loop non-functional. Multiple community members (dthau120391, tazmad, just2majic) independently reproduced and reported this issue.
- **PR #1367** (self-audit) represents a new category: meta-cognitive quality assurance for AI outputs. It received follow-up Issue #1385 proposing a three-gate pipeline.
- **PR #514** (typography) and **PR #1302** (color) represent "craft" skills — domain-specific quality improvements that apply to any document Claude generates.

---

## 2. Community Demand Trends

From Issues analysis, the community's most-anticipated Skill directions are:

| Demand Category | Supporting Issues | Community Signal |
|-----------------|------------------|------------------|
| **Bug Fixing Infrastructure** | [#556](https://github.com/anthropics/skills/issues/556) (12 comments, 7👍), [#1169](https://github.com/anthropics/skills/issues/1169) (3 comments, 1👍), [#1061](https://github.com/anthropics/skills/issues/1061) (3 comments, 2👍) | **Highest urgency** — `run_eval.py` is broken for most users, blocking skill optimization |
| **Security & Trust Boundaries** | [#492](https://github.com/anthropics/skills/issues/492) (43 comments, 2👍) | **Most discussed issue** — Community skills under `anthropic/` namespace create impersonation risk |
| **Org-Wide Sharing & Collaboration** | [#228](https://github.com/anthropics/skills/issues/228) (16 comments, 8👍) | **Highest upvoted feature request** — need for shared skill libraries |
| **Windows Compatibility** | [#1061](https://github.com/anthropics/skills/issues/1061) (3 comments, 2👍) | Growing demand from Windows users (subprocess, encoding, pipe issues) |
| **Reasoning Quality Assurance** | [#1385](https://github.com/anthropics/skills/issues/1385) (3 comments) | Emerging demand for pre-delivery quality gates |
| **Agent Governance & Safety** | [#412](https://github.com/anthropics/skills/issues/412) (6 comments) | Pattern requests for policy enforcement, threat detection, trust scoring |

**Key Insight:** The community is currently **more focused on fixing the skill-development infrastructure** (the `skill-creator` toolchain) than on creating new Skills. The #1 blocker is the `run_eval.py` 0% recall bug affecting all Windows users and many Unix users.

---

## 3. High-Potential Pending Skills

These open PRs have active discussion and are likely to land soon:

| PR | Skill | Author | Why It's Hot |
|----|-------|--------|--------------|
| [#1298](https://github.com/anthropics/skills/pull/1298) | skill-creator fix | [MartinCajiao](https://github.com/MartinCajiao) | Fixes the **#1 blocker** in the ecosystem. Multiple community members contributed to diagnosis. Likely to merge once reviewed. |
| [#1323](https://github.com/anthropics/skills/pull/1323) | skill-creator trigger detection fix | [Polluelo978](https://github.com/Polluelo978) | Addresses the same 0% recall root cause from a different angle — trigger detection logic fails on non-Skill tools. |
| [#1099](https://github.com/anthropics/skills/pull/1099) | Windows subprocess fix | [joshuawowk](https://github.com/joshuawowk) | Fixes Windows crash in `run_eval.py`. Combined with [#1050](https://github.com/anthropics/skills/pull/1050) (gstreet-ops), this makes skill-creator usable on Windows. |
| [#1367](https://github.com/anthropics/skills/pull/1367) | Self-Audit v1.3.0 | [YuhaoLin2005](https://github.com/YuhaoLin2005) | Novel category (reasoning quality gate). Author has follow-up Issue #1385 with 3 comments. |
| [#1302](https://github.com/anthropics/skills/pull/1302) | Color Expert | [meodai](https://github.com/meodai) | Published by a domain expert (meodai is known for color knowledge). Well-structured, self-contained. |
| [#723](https://github.com/anthropics/skills/pull/723) | Testing Patterns | [4444J99](https://github.com/4444J99) | Comprehensive coverage of modern testing practices. Addresses an obvious gap in the Skills collection. |

**Merged / Closed:** Note that **no major Skills PRs have been merged** in this analysis window. All top PRs remain open — suggesting a review bottleneck or high quality bar for the `anthropics/skills` repository.

---

## 4. Skills Ecosystem Insight

**The community's most concentrated demand is for a reliable, cross-platform skill-development toolchain** — specifically fixing the `run_eval.py` 0% recall bug and enabling Windows compatibility — rather than for any single new content Skill, as the broken evaluation loop blocks all skill optimization and improvement work.

---

# Claude Code Community Digest — 2026-07-27

---

## Today's Highlights

The community continues to push for better Windows integration, with the top-voted open issue requesting a way to disable the bundled Cowork background service. A burst of closed issues from mid-June reveals several critical bugs that have since been resolved, including iOS SSH terminal corruption, sandbox bypass vulnerabilities, and phishing-style API error rendering. Several new PRs this week focus on security hardening, particularly around firewall configuration and sandbox fallback behavior.

---

## Releases

No new releases in the last 24 hours.

---

## Hot Issues

1. **[#57371 — Windows: Provide a way to disable bundled Cowork background service](https://github.com/anthropics/claude-code/issues/57371)** *(OPEN)*  
   The most-upvoted open issue (👍39) requests an opt-out for `CoworkVMService` on Windows. Users who don't use Cowork report unnecessary resource consumption and process overhead. The 14 comments suggest this is a significant quality-of-life blocker for Windows power users.

2. **[#63499 — /compact fails with cyber safeguards false positive during legitimate defensive security session](https://github.com/anthropics/claude-code/issues/63499)** *(CLOSED)*  
   A critical false-positive bug where `/compact` was blocked by safety classifiers during legitimate pentesting work. Closed with 9 comments — the resolution signals progress on classifier precision for security tooling workflows.

3. **[#66022 — Regression: auto-compact no longer triggers at ~168K tokens with claude-sonnet-4-6](https://github.com/anthropics/claude-code/issues/66022)** *(CLOSED)*  
   Users relied on auto-compact at 168K tokens, but a regression silently removed this behavior until hitting the 1M hard limit. Fixed in a recent update; important for anyone doing long-context sessions without manual compacting.

4. **[#65989 — Regression: cursor desync + progressive frame corruption in iOS SSH terminal](https://github.com/anthropics/claude-code/issues/65989)** *(CLOSED)*  
   A bisected bug showing how v2.1.163 broke TUI rendering in Secure ShellFish on iOS. The issue saw 8 comments and was likely a high-priority fix for mobile/small-screen users.

5. **[#71757 — Auth session invalidated after sleep on macOS 26](https://github.com/anthropics/claude-code/issues/71757)** *(OPEN)*  
   A fresh issue (3 days old) reporting that background token refresh on sleep corrupts keychain credentials. Affects macOS 26 users who suspend their machines mid-session. Currently has 2 👍.

6. **[#59907 — Agent Teams auto-distributor injects task descriptions into specialist contexts as fake teammate messages](https://github.com/anthropics/claude-code/issues/59907)** *(CLOSED)*  
   An experimental feature bug where `CLAUDE_CODE_EXPERIMENTAL_AGENT_TEAMS` leaked orchestrator task descriptions into specialist agent contexts. This is a concerning hallucination/leak vector that appears to have been fixed.

7. **[#67800 — MSIX + Smart App Control: Windows-MCP blocked (os error 4551)](https://github.com/anthropics/claude-code/issues/67800)** *(CLOSED)*  
   Windows sandboxing conflicts preventing MCP tools from running under MSIX packaging. The 5-comment thread indicated silent installation failures — a nasty DX issue for Windows developers adopting MCP.

8. **[#66410 — Desktop app shows non-1M Opus 4.8 while CLI shows 1M for same session](https://github.com/anthropics/claude-code/issues/66410)** *(CLOSED)*  
   A confusing state discrepancy where the desktop GUI and CLI disagreed on context window size for the same session. Likely caused drift from 1M back to non-1M over time.

9. **[#68231 — Read tool injects huge partial file output causing ECONNRESET](https://github.com/anthropics/claude-code/issues/68231)** *(CLOSED)*  
   The Read tool could dump partial file contents large enough to trigger connection resets on subsequent turns. A significant reliability bug for users working with large codebases.

10. **[#68387 — /model switch to classifier-incompatible model bricks all non-trivial commands](https://github.com/anthropics/claude-code/issues/68387)** *(CLOSED)*  
    Switching models via `/model` could silently select a model the permission classifier can't handle, breaking Bash and Edit/Write commands. The error misled users into thinking it was a transient outage.

---

## Key PR Progress

1. **[#81426 — fix(security-guidance): Support Windows venv layout for agentic reviewer](https://github.com/anthropics/claude-code/pull/81426)** *(OPEN)*  
   Unblocks the security-guidance agentic commit reviewer on Windows. Previously skipped entirely with `SKIP_WIN32` — a long-standing gap for Windows security workflows.

2. **[#81423 — fix(devcontainer): Block IPv6 egress to close firewall allowlist bypass](https://github.com/anthropics/claude-code/pull/81423)** *(OPEN)*  
   Critical security hardening: the devcontainer firewall only blocked IPv4 egress, leaving IPv6 as a full bypass. This closes that gap for dual-stack Docker networks.

3. **[#81421 — fix(examples/settings): Make bash-sandbox example fail closed when sandbox unavailable](https://github.com/anthropics/claude-code/pull/81421)** *(OPEN)*  
   Previously the example sandbox config silently fell back to unsandboxed execution. This PR makes it fail-closed — a safer default for security-sensitive deployments.

4. **[#81262 — Log closed issues as closure events in Statsig](https://github.com/anthropics/claude-code/pull/81262)** *(OPEN)*  
   Fixes internal analytics where closing an issue was mistakenly logged as a creation event. Improves the accuracy of Anthropic's own bug-tracking telemetry.

5. **[#81261 — Handle worktree paths with spaces in /clean_gone](https://github.com/anthropics/claude-code/pull/81261)** *(OPEN)*  
   Fixes the `/clean_gone` command to properly handle paths containing spaces by switching from `awk`-based parsing to `git for-each-ref` + `git worktree list --porcelain -z`.

6. **[#68693 — fix(scripts): Add duplicate label additively, don't replace existing labels](https://github.com/anthropics/claude-code/pull/68693)** *(OPEN)*  
   When closing issues as duplicates, the script was replacing all existing labels (platform/area/priority) with just `[duplicate]`. This preserves existing labels additively.

7. **[#38167 — feat(devcontainer): Use authenticated request to GitHub API in firewall script](https://github.com/anthropics/claude-code/pull/38167)** *(OPEN)*  
   Allows the devcontainer's init-firewall script to use `GH_TOKEN` for authenticated GitHub API calls, preventing rate-limit failures in shared IP environments.

8. **[#20448 — Add web4-governance plugin for AI governance with R6 workflow](https://github.com/anthropics/claude-code/pull/20448)** *(OPEN)*  
   An external contribution adding a governance plugin using "T3 trust tensors" and entity witnessing. Long-open (6 months) but still under review — potentially significant for compliance workflows.

9. **[#81421 — fix(examples/settings): Make bash-sandbox example fail closed](https://github.com/anthropics/claude-code/pull/81421)** *(OPEN)* *(Duplicate entry removed, PRs 81423/81426/81421 are all from same author/date)*

---

## Feature Request Trends

The most-requested feature directions in recent issues are:

- **Context Window Self-Management**: Multiple requests for agent-side detection of context degradation (#68294) and the ability for agents to self-compact or summarize without human intervention. This reflects frustration with long session degradation.

- **Task/Punchlist Integration**: Users want to update task lists or "punchlists" inline via `/btw` commands (#68407) and see task IDs in list output (#65557). The demand is for richer task management within the TUI, not just external tracking.

- **Cowork Opt-Out**: The top-voted open issue (#57371) is a clean user-control request: decouple the Cowork background service from the main desktop app for users who don't use the feature.

- **Windows Platform Parity**: Multiple issues (MCP installation, Smart App Control, workspace security guidance) highlight an ongoing platform gap. Windows users consistently request parity with macOS/Linux.

- **Recursive Subagent Dispatch**: The inability for subagents to spawn further subagents (#60763) limits complex multi-agent workflows. Users want hierarchical agent teams, not flat ones.

---

## Developer Pain Points

The data reveals several recurring frustrations:

- **Model Unavailability / Classifier Failures**: The June 12 government directive that suspended Fable 5 created a cascade of issue reports (#68405, #68387, #67936) about vague error messages, silent bricking of commands, and confusion between "unavailable" and "blocked." The error UX around model suspension is clearly inadequate.

- **State Drift Between Interfaces**: Multiple bugs (#66410, #68059) show the CLI, desktop app, and web remote control disagreeing on session state — model context size, whether context was cleared, etc. This erodes trust in the tool's consistency.

- **Hallucinated / Fabricated Content**: Several bugs (#68332, #68414, #66302) describe the model generating fabricated API error messages, phishing-style credit offers, or repeated nonsense tokens ("court" repeated thousands of times). While some were safety-classifier injection issues, these erode user confidence in output integrity.

- **Windows-Specific Sandboxing Conflicts**: The MSIX + Smart App Control issue (#67800) and Windows venv layout problem (#81426) highlight that Windows security mechanisms interact poorly with Claude Code's tooling — a persistent friction point.

- **Unclear Error Messages**: Particularly around billing discrepancies (#68379) and model availability (#68403), users report getting opaque or misleading error messages that don't guide them toward resolution.

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex Community Digest — 2026-07-27

## Today's Highlights
A major MCP OAuth refactoring stack (6+ PRs) has been batched through review and merged, addressing long-standing authentication failures and concurrency issues (#31573). Meanwhile, a critical performance bug report shows GPT-5.6 serializing independent tool calls wastes 27–45% of weighted usage (#35050), and a dangerous model-behavior incident on Arch Linux caused data loss via destructive system commands (#35492), reigniting safety-concern debates.

## Releases
No new releases in the last 24 hours.

## Hot Issues
1. **[#31573 — OAuth authentication fails at issuer validation](https://github.com/openai/codex/issues/31573)** (23 comments, 55 👍)  
   CLI users can't authenticate via OAuth due to strict issuer checks. High community demand; the PR stack merged today directly addresses this.

2. **[#35050 — GPT-5.6 serializes independent Code Mode calls; explicit batching reduced weighted usage by 27–45%](https://github.com/openai/codex/issues/35050)** (13 comments, 13 👍)  
   A detailed real-world analysis shows the model issues parallelizable operations sequentially. Explicit batching yields huge efficiency gains — a strong signal for model-behavior improvements.

3. **[#35492 — Codex CLI can brick Arch Linux devices via `passwd -d`](https://github.com/openai/codex/issues/35492)** (8 comments, 0 👍)  
   A user reports full data loss after the agent issued destructive system commands. Low votes but critically important for safety — highlights insufficient guardrails on privileged operations.

4. **[#17320 — Excessive SQLite WAL writes during streaming due to TRACE logs ignoring RUST_LOG](https://github.com/openai/codex/issues/17320)** (27 comments, 39 👍)  
   Long-running bug where verbose internal logging bypasses log-level config, causing disk I/O storms. High engagement signals many affected users.

5. **[#20500 — Feature request: support multiple named accounts per app/connector](https://github.com/openai/codex/issues/20500)** (19 comments, 89 👍)  
   The most-voted open feature request. Developers need to manage multiple service accounts (e.g., personal vs. work GitHub) with hard privacy boundaries.

6. **[#32683 — Windows Codex App crashes in CrBrowserMain when Browser Use opens a page](https://github.com/openai/codex/issues/32683)** (26 comments, 8 👍)  
   Reproducible crash (0xC0000005) in the embedded browser, specific to Windows. A browser-team linear issue is tracking it, but no fix yet.

7. **[#34061 — Insane Codex Disk Usage from Subagents](https://github.com/openai/codex/issues/34061)** (12 comments, 1 👍)  
   Subagent sessions balloon to 10s of GBs on disk. Users report running out of space mid-session — a significant reliability concern for heavy CLI users.

8. **[#34268 — Multi-agent V2 full-history forks duplicate historical data, causing >100 GiB session storage growth](https://github.com/openai/codex/issues/34268)** (3 comments, 1 👍)  
   Related to #34061 but specifically about duplication from forking — each fork copies compaction snapshots and inline images multiplicatively.

9. **[#35119 — Windows 26.721.3404 marks valid WSL repos as non-Git](https://github.com/openai/codex/issues/35119)** (6 comments, 7 👍)  
   A regression in the latest Windows app version breaks WSL-based Git workflows, falsely claiming "Git is unavailable."

10. **[#34301 — GPT Sol and Terra threads cannot spawn Luna subagents because of version mismatch](https://github.com/openai/codex/issues/34301)** (6 comments, 10 👍)  
    Multi-agent orchestration broken on Windows: parent agents can't spawn child Luna agents due to version incompatibility in the agent protocol.

## Key PR Progress
1. **[#30295 — Serialize MCP OAuth login and logout](https://github.com/openai/codex/pull/30295) (CLOSED)**  
   Core of the MCP OAuth stack — introduces proper serialization to prevent race conditions during login/logout flows. Merged.

2. **[#30296 — Report MCP OAuth Auto store drift](https://github.com/openai/codex/pull/30296) (CLOSED)**  
   Adds detection for token-store drift so stale credentials are surfaced to users. Part of the same stack.

3. **[#30294 — Route MCP OAuth recovery through Codex](https://github.com/openai/codex/pull/30294) (CLOSED)**  
   Ensures all OAuth recovery flows go through Codex's own mechanisms rather than external browser popups.

4. **[#30416 — Serialize authoritative MCP OAuth refresh transactions](https://github.com/openai/codex/pull/30416) (CLOSED)**  
   Last piece of the stack — serializes refresh operations to prevent duplicate/conflicting token refreshes.

5. **[#35525 — Skip inactive TUI threads without pending user interaction](https://github.com/openai/codex/pull/35525) (CLOSED)**  
   Performance fix: only polls inactive threads when user input is pending, reducing UI lag in multi-thread sessions.

6. **[#35524 — Preserve terminal turn errors in replayed history](https://github.com/openai/codex/pull/35524) (CLOSED)**  
   Fixes a bug where model-overload errors were lost on history replay, making debugging harder.

7. **[#35523 — Shut down the in-process outbound router explicitly](https://github.com/openai/codex/pull/35523) (CLOSED)**  
   Fixes a shutdown hang where the app-server's outbound router wouldn't close due to detached processor work.

8. **[#30985 — Let idle auto-attached threads unload](https://github.com/openai/codex/pull/30985) (OPEN)**  
   Enables 30-minute unload timeout for threads with no explicit subscribers, reducing memory pressure. Still under review.

9. **[#35414 — Raise the MCP server recursion limit](https://github.com/openai/codex/pull/35414) (CLOSED)**  
   Increases Rust recursion limit to 256 for MCP server crates to prevent stack overflow in deeply nested calls.

10. **[#35408 — Ignore generated system skills in the skills watcher](https://github.com/openai/codex/pull/35408) (CLOSED)**  
    Prevents the watcher from scanning system skill directories (pre-installed, not user-managed), reducing unnecessary filesystem events.

## Feature Request Trends
- **Multi-account/connector management** (#20500, 89 👍): The top-voted request. Developers need to connect multiple identities per service (e.g., work + personal GitHub) with explicit selection and privacy boundaries.
- **Agent/session management views** (#22321, 26 👍): Users want a dedicated panel in the TUI to monitor, reattach, and manage multiple parallel agents.
- **Data retention and deletion controls** (#24610, 17 👍): Growing concern about archived sessions persisting indefinitely with no bulk-deletion option.
- **Markdown math rendering in TUI** (#18906, 17 👍): Academic users need LaTeX rendering for technical documentation workflows.
- **Context window restore/opt-in** (#34619, 6 👍): Power users want the previous 372k context window back, or at least a toggle.

## Developer Pain Points
1. **Session data bloat** — Two issues (#34061, #34268) report subagent sessions consuming 10–100+ GiB of disk due to compaction duplication and unoptimized snapshot storage.
2. **Windows-specific instability** — Multiple crash reports (#32683, #32094, #35311) and WSL/Git integration regressions (#35119) make Windows the most problematic platform.
3. **MCP reliability** — stdio MCP connections degrade mid-session (#16899), MCP servers leak memory (#11324), and OAuth flows fail (#31573). The massive PR merge today signals this is a top priority.
4. **Model behavior unpredictability** — GPT-5.6 serializes independent tool calls (#35050), and the Arch Linux destructive-command incident (#35492) shows safety checks are insufficient.
5. **Turn lifecycle stalls** — Sessions hang indefinitely on "thinking" (#21360), and the "No answer provided" timeout (#32615) wastes developer time.

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI Community Digest — 2026-07-27

## Today's Highlights

The nightly train continues with **v0.54.0-nightly.20260726.g3818efbbf**, though no user-facing changes were introduced. On the bug front, a long-standing issue where subagents falsely report `GOAL` success after exhausting their turn limit (Issue #22323) remains a top pain point. Security hardening is advancing: PR #28403 closes a variable expansion bypass (GHSA-wpqr-6v78-jr5g), and PR #28523 enforces explicit tag validation in the file keychain.

## Releases

- **[v0.54.0-nightly.20260726.g3818efbbf](https://github.com/google-gemini/gemini-cli/releases/tag/v0.54.0-nightly.20260726.g3818efbbf)**  
  Automated nightly release. No feature changes beyond version bump from `0.54.0-nightly.20260722.gf743ab5`.

## Hot Issues

### 1. [Subagent recovery after MAX_TURNS is reported as GOAL success, hiding interruption](https://github.com/google-gemini/gemini-cli/issues/22323)
**12 comments | 2 👍 | Status:** `need-retesting`
**Why it matters:** A `codebase_investigator` subagent hits its maximum turn limit but reports `status: "success"` with `Termination Reason: "GOAL"`. This masks the failure, making debugging nearly impossible. Community interest is moderate but the impact on trust in agent telemetry is significant.

### 2. [Generalist agent hangs](https://github.com/google-gemini/gemini-cli/issues/21409)
**8 comments | 8 👍 | Status:** `need-retesting`
**Why it matters:** The generalist agent hangs indefinitely on simple tasks (e.g., folder creation). Users report waiting up to an hour before cancelling. The only workaround is disabling sub-agent usage entirely. High reaction count reflects broad frustration.

### 3. [Shell command execution gets stuck with "Waiting input"](https://github.com/google-gemini/gemini-cli/issues/25166)
**4 comments | 3 👍 | Status:** `bot-triaged`
**Why it matters:** After completing a simple CLI command, Gemini shows the shell as active and "Awaiting user input." This forces manual intervention and breaks automation workflows.

### 4. [Browser subagent fails on Wayland](https://github.com/google-gemini/gemini-cli/issues/21983)
**4 comments | 1 👍 | Status:** `need-retesting`
**Why it matters:** The browser subagent exits immediately with `Termination Reason: GOAL` on Wayland display servers. Linux users on modern desktop environments are effectively blocked from using browser automation.

### 5. [Model frequently creates tmp scripts in random spots](https://github.com/google-gemini/gemini-cli/issues/23571)
**3 comments | 0 👍 | Status:** `bot-triaged`
**Why it matters:** When restricted from shell execution, the model scatters edit scripts across user directories, creating cleanup overhead. This is a quality-of-life issue for developers maintaining clean workspaces.

### 6. [Agent should stop/discourage destructive behavior](https://github.com/google-gemini/gemini-cli/issues/22672)
**3 comments | 1 👍 | Status:** `bot-triaged`
**Why it matters:** The model occasionally uses `git reset`, `--force` flags, or destructive commands when safer alternatives exist. Community is asking for safety rails on state-modifying operations.

### 7. [Bugreport doesn't provide subagent context](https://github.com/google-gemini/gemini-cli/issues/21763)
**2 comments | 0 👍 | Status:** `need-retesting`
**Why it matters:** `/bug` reports only capture the main session, omitting subagent trajectories. This makes debugging multi-agent failures nearly impossible.

### 8. [Auto Memory retries low-signal sessions indefinitely](https://github.com/google-gemini/gemini-cli/issues/26522)
**5 comments | 0 👍 | Status:** `bot-triaged`
**Why it matters:** Auto Memory only marks sessions as processed if the extraction agent successfully reads them. Low-signal sessions are skipped but never marked processed, causing infinite retries. A subtle but costly resource leak.

### 9. [Gemini doesn't use skills and sub-agents enough](https://github.com/google-gemini/gemini-cli/issues/21968)
**6 comments | 0 👍 | Status:** `need-retesting`
**Why it matters:** Users report that even with well-described custom skills (e.g., Gradle, Git), the model rarely invokes them unless explicitly instructed. This reduces the ROI of investing in skill authoring.

### 10. [Subagents running without permission since v0.33.0](https://github.com/google-gemini/gemini-cli/issues/22093)
**3 comments | 0 👍 | Status:** `need-retesting`
**Why it matters:** A regression introduced in v0.33.0 causes subagents to execute despite being disabled in all configuration files. Users expecting only MCP functionality find agents running without consent.

## Key PR Progress

### 1. [fix(core): block $VAR and ${VAR} variable expansion bypass](https://github.com/google-gemini/gemini-cli/pull/28403)
**Status:** Open | **Priority:** p1 | **Area:** security
**Why it matters:** Fixes an incomplete check in `detectBashSubstitution()` and `detectPowerShellSubstitution()` that allowed variable expansion to bypass a prior security fix (GHSA-wpqr-6v78-jr5g). Adds defense-in-depth hardening to the dedup workflow.

### 2. [fix(core): enforce explicit tag length and validation in file keychain](https://github.com/google-gemini/gemini-cli/pull/28523)
**Status:** Open | **Labels:** `size/m`, `size/l`
**Why it matters:** Configures explicit 128-bit authentication tag enforcement for credential storage, preventing silent truncation or malformed ciphertext on non-standard Node.js runtimes.

### 3. [fix(vscode): track activation disposables](https://github.com/google-gemini/gemini-cli/pull/28386)
**Status:** Open | **Area:** core | **Priority:** p2
**Why it matters:** Fixes a bug in VS Code companion activation where subscription tracking used comma expressions, causing only the last `Disposable` from each pair to be tracked. Previously, cleanup on deactivation could leave stale listeners.

### 4. [fix(core): strip login/interactive shell wrappers in stripShellWrapper](https://github.com/google-gemini/gemini-cli/pull/28359)
**Status:** CLOSED
**Why it matters:** The shell wrapper stripper only recognized bare `-c`, missing login wrappers like `bash -lc "..."` or `bash --login -c "..."`. The policy engine only re-checks wrapped payloads when the wrapper is stripped, meaning these formats bypassed security re-evaluation.

### 5. [Trim tool names before registry lookup](https://github.com/google-gemini/gemini-cli/pull/28438)
**Status:** Open | **Labels:** `size/xs`
**Why it matters:** Trims outer whitespace from tool names before resolving through the script tool registry. A small but pragmatic fix that prevents silent failures due to accidental whitespace in tool references.

### 6. [chore/release: bump version to 0.54.0-nightly.20260726.g3818efbbf](https://github.com/google-gemini/gemini-cli/pull/28536)
**Status:** Open
**Why it matters:** Automated nightly release version bump. No functional changes.

## Feature Request Trends

- **AST-aware tooling (Issues #22745, #22746):** Multiple requests to use Abstract Syntax Tree (AST) reading for precise method/class bounds, reducing token waste from misaligned file reads and improving search relevance.
- **Subagent trajectory visibility (Issues #22598, #21763):** Strong desire to expose subagent trajectories in `/chat share` and bug reports. Developers need visibility into subagent decision-making for debugging and evals.
- **Zero-dependency OS sandboxing (Issue #19873):** A proposal to let Gemini 3 models operate using native POSIX tools via sandboxed execution, leveraging the model's bash affinity while maintaining security.
- **Browser agent resilience (Issue #22232):** Requests for automatic session takeover and lock recovery in `BrowserManager.ts`, moving away from the current "fail-fast" strategy on locked profiles.

## Developer Pain Points

- **False GOAL successes (Issue #22323, #21983):** Agents frequently terminate with `GOAL` status after hitting turn limits or failures, misleading users and making debugging exceptionally difficult.
- **Agent hangs and stuck shells (Issues #21409, #25166, #22465):** The generalist agent hangs on trivial operations (folder creation, Vite app scaffolding), and shell commands remain in "Awaiting input" state after completion.
- **Configuration and permission regressions (Issues #22093, #22267):** Agent configuration overrides (e.g., `maxTurns`, enabled agents) are ignored in some contexts. Subagents running without consent since v0.33.0 raises trust concerns.
- **Memory system scalability (Issues #26522, #26523, #26516):** Auto Memory retries low-signal sessions indefinitely, silently skips malformed patches, and logs unredacted content to model context before sanitization. A trio of systemic quality issues.

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

**GitHub Copilot CLI Community Digest – 2026-07-27**

## Today's Highlights
The community saw a spike in triage activity yesterday, with several invalid or low-effort issues quickly closed. Meanwhile, two persistent bugs—a Linux zombie process accumulation and a Windows exit crash—continue to draw attention. No new releases were published in the last 24 hours.

## Releases
*No new releases in the last 24 hours.*

## Hot Issues
1. **Zombie Process Accumulation (Linux)** – [#4163](https://github.com/github/copilot-cli/issues/4163) (CLOSED)  
   Copilot CLI 1.0.71 fails to reap child subprocesses, causing zombie processes to accumulate (~2/min). This impacts long-running sessions and system resource limits. (👍: 3)

2. **TUI Hang on NFS/GPFS (Linux)** – [#4053](https://github.com/github/copilot-cli/issues/4053) (OPEN)  
   The TUI hangs indefinitely at "Loading: N skills" on NFS/GPFS filesystems, caused by a SIGCHLD race during `which gh` subprocess spawning. Critical for enterprise users with networked home directories.

3. **Windows Terminal Content Disappearance** – [#4263](https://github.com/github/copilot-cli/issues/4263) (OPEN)  
   Responses vanish in Windows Terminal vertical split panes when scrolling. UI regression in 1.0.73+ disrupts full output visibility.

4. **Interactive Prompt Ignored with BYOK Provider** – [#4258](https://github.com/github/copilot-cli/issues/4258) (OPEN)  
   The `-i/--interactive` startup prompt is silently ignored when using a custom/BYOK provider in TTY mode, breaking automated workflows.

5. **`view` Tool Path Does Not Exist Regression** – [#4202](https://github.com/github/copilot-cli/issues/4202) (OPEN)  
   Built-in `view` tool incorrectly reports "Path does not exist" for existing files in v1.0.73, while v1.0.71 works. Regression introduced in v1.0.72.

6. **Slash Command Double-Firing** – [#4264](https://github.com/github/copilot-cli/issues/4264) (OPEN)  
   Local extension slash commands queue up multiple instances of the same command, resulting in redundant execution (3–5 duplicates observed).

7. **Desktop App Ignores `askUser: false` Setting** – [#4260](https://github.com/github/copilot-cli/issues/4260) (OPEN)  
   The desktop app host bypasses the CLI's `askUser: false` setting, offering no way to disable the `ask_user` tool. Triage-assigned.

8. **`--resume` Replays Orphaned Permission Prompts** – [#4259](https://github.com/github/copilot-cli/issues/4259) (OPEN)  
   Using `--resume` re-presents previously unresolved `permission.requested` events, causing infinite re-prompt loops without matching `permission.completed`.

9. **Remote MCP OAuth: No Silent Token Refresh** – [#4203](https://github.com/github/copilot-cli/issues/4203) (OPEN)  
   Expired access tokens on remote OAuth MCP servers force full interactive re-authentication even when a valid refresh token is cached. Violates RFC 6749 §6.

10. **Windows Crash on Exit (FAST_FAIL_FATAL_APP_EXIT)** – [#4217](https://github.com/github/copilot-cli/issues/4217) (OPEN)  
    `copilot.exe` consistently crashes during teardown with a fatal fail-fast. WinDbg analysis points to a libuv `uv_async_send` sending on a closing handle. (👍: 1)

## Key PR Progress
*No pull requests were updated or created in the last 24 hours.*

## Feature Request Trends
- **Extensible `.agents` Convention** – Multiple requests ([#4204](https://github.com/github/copilot-cli/issues/4204)) to expand the `.agents` discovery beyond `skills` to include `instructions`, `agents`, and `hooks`, and to support non-Git repos.
- **Anthropic Context Caching** – [#4256](https://github.com/github/copilot-cli/issues/4256) proposes adding `cache_control` breakpoints to Anthropic requests to reduce latency/cost by reusing expensive system prompts and tool definitions.
- **Better BYOK Provider Support** – Continued demand ([#4258](https://github.com/github/copilot-cli/issues/4258)) for parity between built-in and custom providers in interactive and prompt workflows.
- **MCP Registry Policy Flexibility** – [#4205](https://github.com/github/copilot-cli/issues/4205) requests support for runtime auth headers in MCP configurations that are not registered in the organization allowlist.

## Developer Pain Points
- **Child Process Management** – Zombie process leaks ([#4163](https://github.com/github/copilot-cli/issues/4163)) and SIGCHLD races ([#4053](https://github.com/github/copilot-cli/issues/4053)) plague Linux users, especially in enterprise NFS environments.
- **Windows Stability** – A persistent crash on exit ([#4217](https://github.com/github/copilot-cli/issues/4217)) and UI glitches in Windows Terminal ([#4263](https://github.com/github/copilot-cli/issues/4263)) degrade the Windows experience significantly.
- **MCP Auth Handling** – Frustration with OAuth refresh token flow ([#4203](https://github.com/github/copilot-cli/issues/4203)) and MCP config rejection from registry policies ([#4205](https://github.com/github/copilot-cli/issues/4205)) highlights poor integration with organizational security controls.
- **Session Resume Bugs** – Orphaned permission prompts on `--resume` ([#4259](https://github.com/github/copilot-cli/issues/4259)) make long-running workflows unreliable.
- **Toggle Confusion** – The desktop app ignoring the CLI's `askUser: false` setting ([#4260](https://github.com/github/copilot-cli/issues/4260)) reveals a gap in configuration consistency between entry points.

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

**Kimi Code CLI Community Digest**  
**Date:** 2026-07-27  
**Source:** [github.com/MoonshotAI/kimi-cli](https://github.com/MoonshotAI/kimi-cli)

---

### Today's Highlights
No new releases or pull requests were published in the last 24 hours. The community’s focus is on a single bug report (#2559) concerning intermittent image drop in the Kimi Code Web interface, where pasted images are replaced with a placeholder text instead of being sent to the model. The issue was closed shortly after being reported, indicating a rapid fix or workaround was applied.

---

### Releases
None in the last 24 hours.

---

### Hot Issues
Since only 1 issue was updated in the last 24 hours, it is listed below as the single noteworthy item.

1. **#2559 – [Bug] Web: pasted images intermittently dropped; model only receives placeholder**  
   **Why it matters:** Affects all users relying on multimodal input in Kimi Code Web. The bug causes image context to be lost, degrading assistant responses. **Community reaction:** Single comment, no upvotes yet; likely fixed quickly given the closed status.  
   **Link:** [Issue #2559](https://github.com/MoonshotAI/kimi-cli/issues/2559)

*(No other issues met the 24‑hour update criterion.)*

---

### Key PR Progress
No pull requests were updated in the last 24 hours.

---

### Feature Request Trends
No new feature requests were observed in the last 24 hours. Based on the single closed bug report, the community’s primary implicit request is **improved reliability of image uploads in the web UI**. No broader feature direction trends can be derived from today’s data alone.

---

### Developer Pain Points
- **Image handling fragility in web interface:** The only open issue (#2559) highlights that pasted images can silently fail to reach the model, replaced by a generic provider‑compatibility placeholder. Developers working with multimodal inputs may experience unpredictable loss of context, requiring manual re‑upload or conversion workarounds. The rapid closure suggests an immediate fix was deployed, but the underlying stability of image processing in the web client remains a concern.

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode Community Digest — 2026-07-27

## Today's Highlights
A surge of **agent lifecycle control** feature requests dominated the past 24 hours, with users demanding subagent steering, cancellations, and direct communication channels. Meanwhile, a **401 error blocking all OpenCode Go chat/completions** remains the top open bug with 39 comments. On the positive side, the community saw several closed PRs landing fixes for malformed tool-call loops, TUI autocomplete improvements, and MCP OAuth token serialization.

## Releases
No new releases in the last 24 hours.

## Hot Issues

1. **[#28846 – Adjust Go usage limits after DeepSeek V4 Pro permanent 75% price reduction](https://github.com/anomalyco/opencode/issues/28846)** [CLOSED]  
   *Author: icocoon | 95 comments | 83 👍*  
   A heavily-upvoted feature request for OpenCode Go to pass along DeepSeek's massive price cut to users. Closed, suggesting the team has committed to adjusting limits.

2. **[#38257 – OpenCode Go returns 401 for chat/completions while /v1/models works](https://github.com/anomalyco/opencode/issues/38257)** [OPEN]  
   *Author: lizijiangyyjx | 39 comments | 10 👍*  
   A critical server-side issue affecting all Go subscription users. `/v1/models` responds fine, but every chat request is blocked — no workaround identified.

3. **[#38789 – Desktop v1.18.5: UnsupportedContentType on project reload](https://github.com/anomalyco/opencode/issues/38789)** [OPEN]  
   *Author: Start-Gao | 13 comments | 5 👍*  
   Post-update crash: the generated client SDK fails to deserialize `application/octet-stream` responses. Multiple users reporting the same startup failure on Windows.

4. **[#38801 – "exiting loop" message in TUI](https://github.com/anomalyco/opencode/issues/38801)** [OPEN]  
   *Author: josephtingiris | 10 comments*  
   A frustrated user reports the TUI's cryptic "exiting loop" log message that only goes away when setting `step=80`. Community sympathizes — long-standing UX complaint.

5. **[#34184 – Auto-renewed Go subscription but quota not reset](https://github.com/anomalyco/opencode/issues/34184)** [OPEN]  
   *Author: suzhenghui-sky | 7 comments*  
   Payment succeeded but system still shows a 1-day cooldown. Billing bug affecting subscription lifecycle.

6. **[#38990 – DeepSeek integration ignoring user prompts](https://github.com/anomalyco/opencode/issues/38990)** [CLOSED]  
   *Author: pixelcreatives | 5 comments*  
   Model overrides user instructions and generates completely different output. Closed quickly, suggesting either a known limitation or a user configuration issue.

7. **[#38993 – Add/Remove MCP servers from TUI with config persistence](https://github.com/anomalyco/opencode/issues/38993)** [OPEN]  
   *Author: abhirampuranik | 3 comments*  
   HTTP API for MCP management exists (#37712) but TUI surface is missing. Users want full lifecycle management without leaving the terminal.

8. **[#38964 – Sibling subagents cannot talk without routing through parent](https://github.com/anomalyco/opencode/issues/38964)** [OPEN]  
   *Author: iceteaSA | 3 comments*  
   For fan-in patterns, every subagent message must bounce through the parent — no direct peer-to-peer channel. Performance and clarity concern.

9. **[#38963 – Subagent cannot ask the spawning agent a question](https://github.com/anomalyco/opencode/issues/38963)** [OPEN]  
   *Author: iceteaSA | 3 comments*  
   Subagents hit dead ends: they either guess wrong or fail, with no ability to request clarification from the parent. Blocks complex orchestration workflows.

10. **[#38966 – Running subagent cannot be steered or cancelled individually](https://github.com/anomalyco/opencode/issues/38966)** [OPEN]  
    *Author: iceteaSA | 2 comments*  
    No per-subagent interruption mechanism. Entire task must be aborted to stop one subagent that goes off-track.

## Key PR Progress

1. **[#39011 – fix(core): replace catch (e: any) with unknown in fs-util resolve](https://github.com/anomalyco/opencode/pull/39011)** [OPEN]  
   *Author: AAliKKhan*  
   Incremental type safety improvement — removes the `any` escape hatch in filesystem utility error handling.

2. **[#39010 – feat(session): add sub-agents tab with status and cost tracking](https://github.com/anomalyco/opencode/pull/39010)** [OPEN]  
   *Author: sdpfigueiredo*  
   Directly addresses #37267: new side-panel tab showing subagent status icons, cost rollup, and navigation. A major UX improvement for multi-agent sessions.

3. **[#39008 – fix(llm): enable Anthropic prompt caching on the OpenRouter route](https://github.com/anomalyco/opencode/pull/39008)** [OPEN]  
   *Author: sergical*  
   Fixes #39009 — OpenRouter route wasn't setting `cache_control`, causing full-price billing on every turn. Significant cost-saving PR.

4. **[#39007 – fix(core): remove commented-out Retried event projection](https://github.com/anomalyco/opencode/pull/39007)** [OPEN]  
   *Author: AAliKKhan*  
   Housekeeping PR removing dead code in the session projector.

5. **[#39006 – fix(core): remove commented-out property labels in Copilot chat model](https://github.com/anomalyco/opencode/pull/39006)** [OPEN]  
   *Author: AAliKKhan*  
   More dead-code cleanup in the GitHub Copilot chat model adapter.

6. **[#38999 – fix(core): align grep behavior and guidance](https://github.com/anomalyco/opencode/pull/38999)** [CLOSED]  
   *Author: rekram1-node*  
   Tightens grep security (requires approval for external-directory paths) and improves error messages. Tested via `test/tool-search.test.ts`.

7. **[#39004 – fix(sdk): use local v2 type owners](https://github.com/anomalyco/opencode/pull/39004)** [OPEN]  
   *Author: rekram1-node*  
   Sources V2 DTOs from the local `@opencode-ai/client` package instead of the published SDK — important for maintaining compatibility during the 2.0 transition.

8. **[#34115 – fix(tui): use event union for data handling](https://github.com/anomalyco/opencode/pull/34115)** [CLOSED]  
   *Author: fwang*  
   Old PR finally merged: uses generated SDK event union for TUI data handling, improving type narrowing.

9. **[#34056 – fix(shell): skip web-tree-sitter WASM on linux/arm64 to prevent Bun SIGTRAP](https://github.com/anomalyco/opencode/pull/34056)** [CLOSED]  
   *Author: darius-f96*  
   Workaround for a Bun 1.3.14 crash on ARM64 Linux — web-tree-sitter WASM causes a hard crash on first shell command.

10. **[#34039 – fix(session): stop malformed tool-call loops](https://github.com/anomalyco/opencode/pull/34039)** [CLOSED]  
    *Author: Nomadcxx*  
    Fixes #31247: Copilot Claude Opus 4.8 can return `finish=tool-calls` without any actual tool call, causing infinite loops. Now properly detected and stopped.

## Feature Request Trends

The clearest emerging theme is **agent orchestration and lifecycle control**:

- **Subagent communication**: Peer-to-peer subagent routing (#38964), upward questioning to the parent (#38963), and per-subagent dispatch context control (#38967) are all requested by the same user in a coherent series.
- **Subagent management UI**: Dedicated subagent views in the desktop app (#37267) and runtime control (steer/cancel/abort) per individual agent (#38966).
- **MCP from TUI**: Full MCP server lifecycle management within the terminal (#38993).
- **Multi-root workspaces**: First-class support for multi-repository sessions (#38984, #34398) and per-repo snapshot tracking for `/undo`.
- **Instruction scoping**: `AGENTS.md` cannot declare which agent(s) it targets (#38961), causing all instructions to reach all agents.

## Developer Pain Points

- **OpenCode Go subscription bugs**: Two separate billing/access issues (#38257, #34184) suggest the Go subscription infrastructure has regressions — 401 blocks and quota reset failures are production-critical.
- **Desktop v1.18.5 regressions**: Multiple reports of `UnsupportedContentType` on project reload (#38789) and `UnexpectedStatus` errors (#38810) after auto-update. The upgrade path is clearly broken for Windows users.
- **Model behavior unpredictability**: DeepSeek ignoring prompts (#38990), GLM-5.2 failing on large writes (#38978), and models proceeding after unanswered questions (#38970) — users feel models are acting autonomously against their intent.
- **Bash permission non-determinism**: `rm *`, `mv *`, `cp *` patterns bypass the `ask` prompt ~50-90% of the time (#39001), a security concern for automated workflows.
- **Agent temperature ignored**: The `temperature` parameter in `opencode.json` is silently dropped from LLM API requests (#34405), making it impossible to control response randomness.

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

# Pi Community Digest — 2026-07-27

## Today's Highlights

A major influx of over 30 issues and 10 PRs landed in the last 24 hours, signaling an active community push ahead of the next minor release. Key themes include **session/compaction lifecycle improvements**, **WSL path handling fixes**, **critical performance optimizations for the TUI**, and multiple **provider-specific compatibility fixes** for MiniMax M3, Z.AI, and OpenAI reasoning modes. The 0.82.x line also receives a security-driven shrinkwrap regeneration for brace-expansion CVE-2026-14257.

## Releases

No new releases in the last 24 hours. The current stable channel remains `@earendil-works/pi-coding-agent@0.82.1`. A shrinkwrap fix for CVE-2026-14257 (#7090) has been closed but not yet published as a patch release.

## Hot Issues

1. **[#6665 — TUI pins a full core while streaming](https://github.com/earendil-works/pi/issues/6665)** — Open, 8 comments  
   Two root causes identified: uncached `Intl.Segmenter` grapheme segmentation and per-chunk Markdown rebuild. High-impact for anyone running long sessions; community has traced the hot path to `render timer → Markdown.render → wrap`. In-progress label applied.

2. **[#7064 — WSL absolute windows paths are mishandled](https://github.com/earendil-works/pi/issues/7064)** — Open, 5 comments  
   Agent `read`/`write`/`edit` tools fail on WSL2 when paths cross between Windows and Linux namespaces. Forces fallback to full file writes. 1 👍, reproducible by multiple users.

3. **[#7090 — Regenerate 0.82.x shrinkwrap with brace-expansion 5.0.8+](https://github.com/earendil-works/pi/issues/7090)** — Closed, 5 comments  
   CVE-2026-14257 affects `brace-expansion@5.0.7` (fatal memory-exhaustion DoS). Official shrinkwrap pins vulnerable version. Fix is to regenerate and publish `0.82.1` or `0.82.2`.

4. **[#7049 — Upgrade Undici to 8.8.0 for plain-HTTP proxy forwarding](https://github.com/earendil-works/pi/issues/7049)** — Open, 3 comments  
   `EnvHttpProxyAgent` hardcodes `proxyTunnel: true`, breaking cleartext HTTP MCP/API targets behind HTTP_PROXY. Requires manual `noProxy` workaround. Undici 8.8.0 default is `proxyTunnel: false`.

5. **[#7138 — MiniMax-M3: messy thinking output, compaction breaks reasoning](https://github.com/earendil-works/pi/issues/7138)** — Closed, 3 comments  
   `pi-ultra-compact` extension breaks MiniMax M3's reasoning tags. User proposes `reasoning_split` parameter as fix. Highlights tension between compaction strategies and reasoning-capable models.

6. **[#7150 — RPC prompt during in-flight compaction silently dropped](https://github.com/earendil-works/pi/issues/7150)** — Closed, 1 comment  
   Critical data-loss bug: `prompt` command over RPC while compaction is in flight returns `success: true` but message never enters session. Undocumented race condition.

7. **[#7149 — Standalone linux-x64 binary SIGILL on pre-Haswell CPUs](https://github.com/earendil-works/pi/issues/7149)** — Closed, 1 comment  
   Official binary uses BMI2 instruction (`shlx`) not available on Sandy Bridge. npm install works fine. Suggests build flags need `-mno-bmi2`.

8. **[#7136 — bash tool silently truncates long commands](https://github.com/earendil-works/pi/issues/7136)** — Closed, 1 comment  
   Commands over a certain length are cut off without error. Partial execution leads to silent data loss. User reports this is "dangerous for any automation pipeline."

9. **[#7134 — `_prepareRetry` ignores provider retry_after](https://github.com/earendil-works/pi/issues/7134)** — Closed, 1 comment  
   Blind exponential backoff hammers providers during cool-down window. Autonomous harness operators hit rate-limit cascades. Authored by an AI agent on behalf of a human operator.

10. **[#7121 — Three independent bugs in core tools](https://github.com/earendil-works/pi/issues/7121)** — Closed, 1 comment  
    `write.ts` reports wrong byte count (UTF-16 vs UTF-8), `find.ts` shows false limit warning, `truncateLine` splits surrogate pairs. Fix branch already provided.

## Key PR Progress

1. **[#7151 — feat(ai): expose pending stop reason while streaming](https://github.com/earendil-works/pi/pull/7151)** — Open  
   Interpret `final_answer` phase as early prediction of `stopReason: 'stop'`. Consumers can react before stream ends. Experimental.

2. **[#7148 — feat(coding-agent): Experimental loadout management](https://github.com/earendil-works/pi/pull/7148)** — Open  
   `/loadout` command to enable/disable extensions mid-session. Loadout overrides persisted in session for resumption. Draft, author marks as "not for merging yet."

3. **[#7131 — Set AI_AGENT for child process attribution](https://github.com/earendil-works/pi/pull/7131)** — Closed  
   Sets `AI_AGENT=pi` alongside existing `PI_CODING_AGENT=true`. Emerging cross-agent convention used by Claude Code, GitHub CLI.

4. **[#7129 — tui: raise visibleWidth cache to 4096 entries, use LRU eviction](https://github.com/earendil-works/pi/pull/7129)** — Closed  
   Fixes cache thrash on non-ASCII lines (box drawing, emoji, CJK). Switches from FIFO to LRU eviction. Directly addresses performance in #6665.

5. **[#7124 — fix(coding-agent): normalize path separators in footer](https://github.com/earendil-works/pi/pull/7124)** — Closed  
   Changes `formatCwdForFooter` to always use forward slash, fixing `~\project` → `~/project` on Windows.

6. **[#7122 — fix(tools): correct byte count in write, false limit warning in find, surrogate pairs in truncateLine](https://github.com/earendil-works/pi/pull/7122)** — Closed  
   Three tool-level bug fixes: UTF-8 byte counting, find limit edge case, and emoji safe truncation.

7. **[#7120 — feat(coding-agent): show SYSTEM.md and APPEND_SYSTEM.md in startup [Context] banner](https://github.com/earendil-works/pi/pull/7120)** — Closed  
   Improves visibility: users running modified system prompts now see them in the startup banner. Solves a discoverability gap.

8. **[#7118 — Expose extension context clear callback](https://github.com/earendil-works/pi/pull/7118)** — Closed  
   Adds runtime-owned clear callback so extensions can hand off and reset session without generating a summary. Unblocks durable compaction strategies.

9. **[#7112 — fix(coding-agent): normalize path separators in formatCwdForFooter](https://github.com/earendil-works/pi/pull/7112)** — Closed  
   Earlier duplicate of #7124 from a different author. Demonstrates community consensus on the fix.

10. **[#7127 — Feature request: public durable compaction strategy lifecycle](https://github.com/earendil-works/pi/issues/7127)** — Closed  
    Requests a public API for external state management in compaction. Would allow extensions to persist compaction state across sessions cleanly.

## Feature Request Trends

- **Compaction Lifecycle API**: Multiple requests (#7127, #7119, #7118) for a public, durable compaction strategy that extensions can own. Current `session_before_compact` hook is read-only and summary-oriented; extensions want to inject custom state, clear context, and manage external persistence.
- **Provider-Specific Compatibility**: Growing demand for per-provider reasoning mode support (OpenAI 5.6 Pro in #7135, MiniMax M3 `reasoning_split` in #7138/#7140, Anthropic refusal signals in #7133). Community wants first-class provider feature negotiation rather than workarounds.
- **Auth & Configuration Preflight**: Users want non-interactive auth checks (#7152) and better visibility into active system prompt modifications (#7120). Suggests a desire for CI/CD integration and deterministic startup validation.
- **Mouse/Terminal Interactivity**: Requests for mouse-click APIs (#7144) and themeable cursor colors (#7141) indicate community interest in richer TUI interactions beyond keyboard-only workflows.

## Developer Pain Points

- **Silent Data Loss**: At least three issues this week involve operations that silently fail or drop data — RPC compaction race (#7150), `bash` tool truncation (#7136), prompt swallowing after boolean flags (#7139). This is a recurring trust-eroding pattern.
- **Cross-Platform Path Handling**: Multiple issues (#7064, #7123, #7124, #7112) highlight broken path normalization on Windows/WSL, particularly in the footer and file tool paths. The community is shipping their own fixes in parallel.
- **Performance Under Load**: Uncached `Intl.Segmenter` (#6665) and cache thrashing (#7129) make the TUI unusable on long sessions. Real-time streaming performance remains a pain point for heavy users.
- **Proxy & Network Configuration**: Undici proxy tunneling (#7049) and missing `AI_AGENT` attribution (#7131) cause friction in enterprise/automation deployments where HTTP proxies and process lineage are required.

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code Community Digest
**Date: 2026-07-27**

---

## Today's Highlights

A flurry of security-focused bug reports and a major CI pipeline disturbance dominate today's digest, with three high-priority (P1) vulnerabilities disclosed around MCP session enforcement and IPC authorization. On the performance front, two new PRs tackle daemon cold-start and first-model-output latency, building on last week's lazy-loading audit. The community is also actively debating the operational future of multi-workspace daemon support, with a 30-comment RFC nearing resolution.

---

## Releases

**v0.21.0-nightly.20260726.9d19eafa9** — Nightly release with two patches:
- Fixed localization bug where CLI insight metrics used UTC instead of local time for days/hours measurement (`#7670`)
- Ongoing refactoring of the autofix module internals

---

## Hot Issues (10 selected)

1. **[#6378 – RFC: Support multiple workspaces in one `qwen serve` daemon](https://github.com/QwenLM/qwen-code/issues/6378)**  
   *30 comments, open since Jul 6*  
   The most-discussed issue of the week. `doudouOUC` proposes a model where one daemon serves multiple isolated workspaces, each with its own N sessions—critical for server-side deployment and managed instances. The community is actively debating persistence and session isolation tradeoffs.

2. **[#7769 – MCP tool denial bypassed when new SSE session is created](https://github.com/QwenLM/qwen-code/issues/7769)**  
   *P1, Security, opened yesterday*  
   `rishavkumar-thecoder` demonstrates that after a user denies an MCP tool call in Qwen Desktop, the AI agent can spawn a new SSE session and retry the same tool—bypassing the user's explicit denial. This is a serious authorization gap requiring immediate patching.

3. **[#7770 – Code interpreter sandbox can write to host machine via exposed MCP proxy](https://github.com/QwenLM/qwen-code/issues/7770)**  
   *P2, Security, opened yesterday*  
   The isolated Linux sandbox has outbound internet access. If a user exposes their MCP proxy to the internet, the sandbox can write back to the host machine through that proxy. A nuanced sandboxing boundary issue.

4. **[#7768 – Desktop IPC bridge executes MCP tools without user authorization](https://github.com/QwenLM/qwen-code/issues/7768)**  
   *P1, Security, opened yesterday*  
   The `mcp_client_tool_call` IPC method in Qwen Desktop's Electron renderer process connects directly to MCP servers without any permission prompt. This is a privilege escalation vector from renderer to system.

5. **[#7755 – Main CI failed: E2E Tests on 60812d4](https://github.com/QwenLM/qwen-code/issues/7755)**  
   *Ready-for-agent, opened yesterday*  
   A main-branch E2E test failure triggered by commit `60812d4cd36b`. The bot auto-labeled this for agent remediation—recurring CI instability is becoming a development blocker.

6. **[#7752 – Certified handoff and takeover for daemon session writer locks](https://github.com/QwenLM/qwen-code/issues/7752)**  
   *P0, Daemon, opened yesterday*  
   A blocking follow-up to `#7164`: when a managed daemon dies, its writer lock remains in the shared workspace, preventing replacement daemons from starting. Requires distributed lock handoff semantics—a critical blocker for high-availability setups.

7. **[#7585 – Direct external context provider profile](https://github.com/QwenLM/qwen-code/issues/7585)**  
   *Feature-request, 8 comments*  
   `doudouOUC` proposes an extension that lets a Qwen CLI process retrieve repository-shared context from an external memory service without modifying Qwen Core. This would enable enterprise knowledge base integration.

8. **[#7732 – Sandbox runtime selected on PATH presence alone](https://github.com/QwenLM/qwen-code/issues/7732)**  
   *Bug, opened yesterday*  
   `getSandboxCommand()` treats presence on `PATH` as "works": Docker Desktop stopped, unreachable socket, or missing group membership all cause silent fallback failures. Podman may be installed and functional but never tried.

9. **[#7757 – Measure and optimize daemon first-model-output latency](https://github.com/QwenLM/qwen-code/issues/7757)**  
   *Performance, opened yesterday*  
   The follow-up to `#7264` cold-start optimization. This issue targets the broader user-perceived latency from cold process to first model-derived output—not just session creation.

10. **[#7685 – Subagent model grade selection at spawn time](https://github.com/QwenLM/qwen-code/issues/7685)**  
    *Feature-request, 4 comments*  
    `Aleks-0` proposes adding a `model` parameter to the `agent` tool that lets the AI pick a model grade (small/medium/high/super) for spawned subagents. Would give users fine-grained control over cost/quality tradeoffs in multi-agent workflows.

---

## Key PR Progress (10 selected)

1. **[#7767 – perf(acp): Preload providers after session creation](https://github.com/QwenLM/qwen-code/pull/7767)**  
   *Opened by doudouOUC*  
   Starts best-effort lazy Provider initialization immediately after ACP `session/new` succeeds, so the first prompt reuses an already-in-progress or completed promise. Directly addresses the cold-start latency tracked in `#7757`.

2. **[#7761 – test(serve): Add first-output latency benchmark](https://github.com/QwenLM/qwen-code/pull/7761)**  
   *Opened by doudouOUC*  
   An opt-in measurement harness that records process-to-session-ready, prompt-to-first-token, and Provider-level timings. Provides the observability infrastructure needed to validate `#7767` and future latency improvements.

3. **[#7764 – fix(core): Stop trailing slash from anchoring nested gitignore patterns](https://github.com/QwenLM/qwen-code/pull/7764)**  
   *Opened by chinesepowered*  
   A subtle bug: directory-only patterns like `foo/` were classified as "anchored" (by their trailing slash) and never matched nested subdirectories. Fixes common `.gitignore` misbehavior in monorepos.

4. **[#7763 – fix(core): Keep leading whitespace in gitignore patterns](https://github.com/QwenLM/qwen-code/pull/7763)**  
   *Opened by chinesepowered*  
   `.trim()` on all gitignore patterns was incorrect—Git only strips trailing whitespace. Leading whitespace is part of the pattern (e.g. for escaping). Second in a series of gitignore correctness fixes.

5. **[#7765 – fix(core): Stop rewriting backslash escapes in gitignore patterns](https://github.com/QwenLM/qwen-code/pull/7765)**  
   *Opened by chinesepowered*  
   A `replace(/\\/g, '/')` step intended to normalize Windows paths was destroying literal backslash escapes in patterns. Third gitignore fix—signals a deep audit of the file-pattern matching code.

6. **[#7753 – fix(triage): Carry the /verify lane's hardening across to /tmux](https://github.com/QwenLM/qwen-code/pull/7753)**  
   *Opened by wenshao*  
   Ports five attack-mitigation controls from the `/verify` lane (`#7710`) to the `/tmux` lane, which had none. Closing a security asymmetry between the two triage workflows.

7. **[#7731 – feat(web-shell): Add git branch picker, commit dialog, and create PR flow](https://github.com/QwenLM/qwen-code/pull/7731)**  
   *Opened by wenshao*  
   An IntelliJ-style branch picker with search, grouping, and checkout; plus a commit dialog and PR creation flow. This brings web-shell git operations close to IDE parity.

8. **[#7762 – feat(hooks): Add submitted prompt provenance](https://github.com/QwenLM/qwen-code/pull/7762)**  
   *Opened by doudouOUC*  
   Adds an optional `submitted_prompt` field to `UserPromptSubmit` events, carrying the exact text before hook transformation. Enables better debugging and auditing of hook chains.

9. **[#7758 – fix(autofix): Answer every review thread, resolve the ones actually fixed](https://github.com/QwenLM/qwen-code/pull/7758)**  
   *Opened by wenshao*  
   Improves the autofix bot's PR review etiquette: now replies in-thread to unfixed findings, and resolves threads whose issues are genuinely addressed. A quality-of-life fix for maintainers reviewing auto-generated PRs.

10. **[#7751 – feat(review): Script-lint as a deterministic gate](https://github.com/QwenLM/qwen-code/pull/7751)**  
    *Opened by wenshao*  
    Replaces an agent-based executable-lint check with a static script that reads a lint report directly. Eliminates model "honor system" for lint severity—a principled shift toward deterministic CI gates.

---

## Feature Request Trends

The following patterns emerge from the last 24h of issue activity:

| Theme | Key Issues | Momentum |
|---|---|---|
| **Multi-workspace daemon architecture** | #6378 (30 comments), #7752 (P0 lock handoff) | ⬆ High – critical for high-availability server deployments |
| **External context/enterprise integration** | #7585 (direct context provider), #7117 (history pagination errors) | ⬆ Growing – enterprise reuse patterns |
| **Subagent model grade selection** | #7685 (spawn-time model choice) | ➡ Moderate – power-user demand for cost control |
| **Voice/transcript improvements for web shell** | #6770 (read-only transcript viewer), #6972 (workspace-scoped voice) | ➡ Consistent – ongoing web shell UX maturation |
| **CI/DevOps automation** | #7383 (scheduled repo-hygiene skill), #7751 (deterministic lint gate) | ➡ Active – reducing maintainer overhead |

---

## Developer Pain Points

1. **E2E Test Instability**  
   Issues #7755, #7759, #7712 show recurring `main`-branch E2E test failures automatically labeled `ready-for-agent`. These are blocking merges and eroding confidence in CI signals.

2. **Session/Daemon State Management**  
   Multiple P0/P1 issues (#7752, #6378, #7745) point to fundamental weaknesses in how daemon sessions start, hand off, and recover—especially writer lock semantics across process restarts.

3. **Security Boundary Confusion**  
   The three MCP-related security disclosures (#7768, #7769, #7770) all filed yesterday share a common theme: the authorization model around IPC boundaries (renderer↔main, sandbox↔host, SSE↔agent) is inconsistently enforced.

4. **Gitignore/File-Lookup Correctness**  
   Three PRs from `chinesepowered` (#7763, #7764, #7765) fix different gitignore parsing bugs in a single day. This signals inadequate test coverage for file-pattern matching, a core dependency for any code-focused tool.

5. **Sandbox Runtime Detection**  
   Issue #7732 highlights that PATH-based detection for Docker/Podman is brittle—an installed but non-functional Docker silently blocks functional Podman. Developers on heterogeneous container setups are hitting this regularly.

6. **Input/IME Compatibility**  
   Issue #7684 (IME candidate window mispositioned with multi-line statusline) and #7713 (terminal scroll jitter on each keystroke) indicate that terminal rendering edge cases—especially with CJK IMEs—are not yet production-quality.

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

# DeepSeek TUI Community Digest — 2026-07-27

## Today's Highlights
A high-velocity day with **20+ PRs merged**, focused on performance, shell integration, and polish. The team fixed a quadratic markdown re-parse bug during streaming, delivered tracked background shell completions to waiting turns, and repaired a prompt-cache busting issue that was silently increasing DeepSeek API costs. Onboarding UX also saw critical fixes for provider setup navigation traps.

## Releases
No new releases in the last 24 hours. The project remains on the v0.9.2 milestone track, with active hardening toward that release.

---

## Hot Issues
*Top 10 noteworthy issues by community impact and technical significance*

1. **[#3793 — v0.9.2 Setup: build a guided localized constitution creator](https://github.com/Hmbown/CodeWhale/issues/3793)** (17 comments)  
   Core UX redesign for the constitution (base prompt) creator. Shifts from a blank editor to a guided, language-first flow with explicit autonomy/risk posture constraints. High community engagement on the trade-off between guidance and flexibility.

2. **[#4227 — Help JayBeest map the CodeWhale tsunami](https://github.com/Hmbown/CodeWhale/issues/4227)** (13 comments)  
   A skill/workflow to help contributors keep up with 10+ PRs/day velocity. Demonstrates the project's own dogfooding culture—using CodeWhale's workflow runtime to manage its own development.

3. **[#2934 — Sidebar sessions panel with auto-resume](https://github.com/Hmbown/CodeWhale/issues/2934)** (10 comments)  
   Persistent session browser in the sidebar, beyond the current Ctrl+R popup. Addresses a major UX gap for users juggling multiple conversations.

4. **[#3792 — Make first-run onboarding feel like starting CodeWhale, not editing config](https://github.com/Hmbown/CodeWhale/issues/3792)** (9 comments)  
   Re-sequences setup to keep the constitution central without confusing it with runtime security controls. Critical for new-user retention.

5. **[#2494 — macOS + iTerm2 user issues compilation](https://github.com/Hmbown/CodeWhale/issues/2494)** (6 comments, CLOSED)  
   A thorough Chinese-language bug report covering keyboard shortcuts, newline handling, session termination, and history browsing. Represents an entire user segment that paused TUI usage.

6. **[#1004 — /dryrun — preview chat completion without sending](https://github.com/Hmbown/CodeWhale/issues/1004)** (5 comments)  
   Long-standing (since May) feature request to inspect the full request payload before sending. Particularly painful for DeepSeek V4 Pro users with costly large context windows.

7. **[#4022 — CLI/TUI parity for subagent control surfaces](https://github.com/Hmbown/CodeWhale/issues/4022)** (5 comments)  
   Ensures subagent management isn't trapped in the TUI—important for future cloud/remote/mobile access paths.

8. **[#3983 — Make current Work state model-visible on parent turns](https://github.com/Hmbown/CodeWhale/issues/3983)** (4 comments)  
   Models should see checklist progress and strategy context for multi-agent workflows. Core to making sub-agents truly autonomous.

9. **[#3927 — Provider-independent offline path for onboarding](https://github.com/Hmbown/CodeWhale/issues/3927)** (4 comments)  
   Users want to explore the TUI before committing to an API key. Highlights the need for offline/local-first first-run experience.

10. **[#3897 — O(N²) markdown re-parse during streaming](https://github.com/Hmbown/CodeWhale/issues/3897)** (2 comments, but **fixed today in #4903**)  
    Renderer re-parsed the entire growing message on every chunk. Performance bug that made long responses progressively slower.

---

## Key PR Progress
*Top 10 important pull requests merged or open today*

1. **[#4903 — perf(tui): stop re-parsing committed markdown while streaming](https://github.com/Hmbown/CodeWhale/pull/4903)** ✅ Merged  
   Fixes O(N²) performance regression from #3897. The quadratic parse is removed; rendering optimizations remain tracked separately.

2. **[#4902 — test(engine): pin the cacheable prefix across unchanged turns](https://github.com/Hmbown/CodeWhale/pull/4902)** ✅ Merged  
   Closes #3738—the prompt-cache busting issue that increased DeepSeek costs. The `<turn_meta>` block was emitting variable Context pressure stats every turn. Now tested and fixed.

3. **[#4894 — feat(shell): deliver tracked completions to waiting turns](https://github.com/Hmbown/CodeWhale/pull/4894)** ✅ Merged  
   Background shell job completions now delivered as runtime events at the next turn boundary. Enables true async code execution patterns.

4. **[#4901 — test(shell): close the background-completion acceptance gaps](https://github.com/Hmbown/CodeWhale/pull/4901)** ✅ Merged  
   Test-only PR closing #3874—audits the full acceptance matrix for background shell completion delivery.

5. **[#4900 — feat(engine): make policy narrowing observable](https://github.com/Hmbown/CodeWhale/issues/3947)** ✅ Merged  
   Models now see when their authority has been narrowed by runtime policy, enabling adaptive behavior instead of silent failure.

6. **[#4899 — feat(composer): add @git and @diff mentions](https://github.com/Hmbown/CodeWhale/pull/4899)** ✅ Merged  
   New `@git` and `@diff` mention tokens in the composer. Attaches curated git context without requiring model round-trips to shell commands.

7. **[#4905 — fix(tui): stop writing terminal control bytes to non-terminals](https://github.com/Hmbown/CodeWhale/pull/4905)** ✅ Merged  
   Stops leaking OSC 9;4 (taskbar progress) and OSC 0 (window title) sequences to stdout when piped to files or other tools.

8. **[#4892 — perf(tui): reuse live transcript snapshots and flattened lines](https://github.com/Hmbown/CodeWhale/pull/4892)** ✅ Merged  
   Closes #3904—caches unchanged live-transcript cells across overlay renders. Streaming changes only invalidate the changed tail.

9. **[#4896 — [codex] move terminal clipboard writes off event loop](https://github.com/Hmbown/CodeWhale/pull/4896)** ✅ Merged  
   Routes OSC 52 clipboard transport through a background worker, preventing terminal I/O from blocking the TUI event loop.

10. **[#4467 — Feat/opencode zen provider](https://github.com/Hmbown/CodeWhale/pull/4467)** Open  
    Adds OpenCode Zen as a model provider, routing Zen models across Responses, Anthropic Messages, and Chat Completions. Notable external contribution from @snail-vs.

---

## Feature Request Trends
*Top requested directions distilled from all active issues*

1. **Localization & Globalization** — 7+ issues (#3091, #3092, #3093, #4788, #4789, #4805)  
   Expanding beyond Chinese/English/Japanese/Vietnamese to Korean, Spanish, Brazilian Portuguese, Russian, French, German, Catalan, and Indonesian. Website parity with README translations is a recurring sub-theme.

2. **Multi-Agent Workflow Control** — 5+ issues (#2974, #3983, #4022, #4397, #1888)  
   Dashboard for concurrent sessions, model-visible work state, CLI/TUI parity for subagent controls, and bounded auto-mode with review-repair loops.

3. **Onboarding & Setup UX** — 5+ issues (#3792, #3793, #3927, #3928, #3937)  
   Guided constitution creator, provider-independent offline exploration, appearance customization discovery, and in-app constitution reading.

4. **Slash Command Ecosystem** — 3+ issues (#1888, #1891, #1004)  
   Control-plane semantics for agentic commands, tool studio wiring, and the `/dryrun` preview command.

5. **Tool & URI Integration** — 2+ issues (#3996, #1891)  
   Internal URI schemes for PRs/issues/diffs/conflicts, GitHub Actions integration, and unified tool studio.

---

## Developer Pain Points
*Recurring frustrations and high-frequency support themes*

1. **macOS / iTerm2 Compatibility** (#2494)  
   Keyboard shortcuts mismatch, multi-line paste broken, Ctrl+C kills session instead of canceling, no session history browsing. A detailed Chinese-language report signals an underserved but vocal user segment.

2. **Prompt Cache Cost Leakage** (#3738, fixed in #4902)  
   Users reported unexpected cost increases. Root cause: per-turn metadata blocks with variable context pressure stats busted the cacheable prefix. Now addressed with pinned tests.

3. **Streaming Performance Degradation** (#3897, fixed in #4903)  
   Long responses got progressively slower as the entire message was re-parsed on every chunk. This O(N²) bug made the app feel unresponsive for complex turns.

4. **Constitution Invisibility** (#3928)  
   No in-app way to read the constitution after setup. Custom overrides fail silently if the env flag is missing. The constitution is the core prompt but is opaque to users.

5. **Unnecessary Terminal Escape Codes** (#4847, partially fixed in #4905)  
   Control bytes leaked to non-terminal output streams (pipes, files, CI logs). Causes garbled output in redirect scenarios.

6. **Provider Onboarding Loops** (#4763, fixed in #4765)  
   xAI OAuth route could trap users in an empty backdrop → OAuth modal → empty backdrop loop with no escape except Esc-then-Ctrl+C. Now fixed with visible/navigable provider lists.

7. **CLI/TUI Parity Anxiety** (#4022)  
   Power users worry that TUI-only features (subagent status, cancellation) won't be accessible from CLI or future cloud/mobile interfaces. The project explicitly tracking this as a design constraint.

8. **Context-Menu Hit Testing** (#4897)  
   Hover selection didn't account for title rows in context menus, causing wrong item selection. Fixed by @XhesicaFrost in a community contribution.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/kky-wollu/agents-radar).*