# AI CLI Tools Community Digest 2026-07-23

> Generated: 2026-07-22 23:09 UTC | Tools covered: 9

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

# Cross-Tool Comparison Report: AI CLI Developer Tools
**Analysis Date: 2026-07-23**

---

## 1. Ecosystem Overview

The AI CLI developer tools landscape continues its rapid maturation, with seven major open-source projects—Claude Code, OpenAI Codex, Gemini CLI, GitHub Copilot CLI, Kimi Code CLI, OpenCode, Pi, Qwen Code, and DeepSeek TUI—each serving distinct developer segments while converging on shared architectural patterns. Tools are increasingly moving toward subagent-based architectures, background task execution, and multi-model provider support, while enterprise concerns around permissions, credential security, and cost transparency dominate community discussions. Windows platform stability has emerged as a critical pain point across multiple projects, and the tension between safety/guardrail systems and developer autonomy remains unresolved. The ecosystem is bifurcating into **platform-first tools** (Claude Code, Codex, Gemini CLI) with deep IDE integration and **agnostic tools** (Pi, OpenCode, Qwen Code) that prioritize provider flexibility and local-first workflows.

---

## 2. Activity Comparison

| Tool | Key Issues (24h) | Active PRs (24h) | Release Status | Notable Signal |
|------|-----------------|------------------|----------------|----------------|
| **Claude Code** | 10 hot issues (24-34 👍 each) | 10 PRs (3 autonomous) | **v2.1.218** (released today) | `/code-review` background subagent; Fable 5 safety classifier false positives crisis |
| **OpenAI Codex** | 10 hot issues (11-151 👍) | 11 PRs merged/updated | **rust-v0.146.0-alpha.1-3** (3 alphas in 24h) | Windows stability crisis (25+ bugs); 151 👍 for auto-resolve disable |
| **Gemini CLI** | 10 hot issues (1-8 👍) | 10 PRs merged/updated | **v0.52.0 stable + v0.53.0-preview** | A2A tool-response grouping fix; nightly RCE patch |
| **GitHub Copilot CLI** | 10 hot issues (new, triage) | 1 PR (stale) | **v1.0.74-1→3** (3 patches today) | Gemini 3.6 Flash support; Windows crashes; tmux regression |
| **Kimi Code CLI** | 5 high-signal issues | 2 PRs in review | **kimi 2.6** (no new release) | MCP schema 400 error; Windows encoding crash; TPD rate limit breach |
| **OpenCode** | 10 hot issues (1-185 👍) | 10 PRs (5 merged, 5 open) | **1.18.4 / 1.3.3** (no new release) | **Go subscription outage** (5+ reports); 185 👍 for model auto-discovery |
| **Pi** | 10 hot issues (0-8 👍) | 10 PRs (6 merged, 4 open) | **v0.81.1** (no new release) | Constrained sampling PR; malicious extension report; OAuth support |
| **Qwen Code** | 10 hot issues (2-5 comments) | 10 PRs (1 merged, 9 open) | **v0.20.0-preview.0** (new today) | **CI red on main**; credential sanitization extension; update-check reliability |
| **DeepSeek TUI** | 10 hot issues (0-17 comments) | 10 PRs (8 closed, 2 open) | **v0.9.1** in final shipping sprint | 17 Dependabot alerts blocking release; unified `/skills` manager landed |

**Observation:** Claude Code and OpenAI Codex lead in community engagement (high upvote counts), while Qwen Code and Pi show the highest PR velocity. Kimi Code CLI and GitHub Copilot CLI have notably lower activity relative to their user bases.

---

## 3. Shared Feature Directions

| Feature Direction | Tools | User Demand Signal |
|-------------------|-------|-------------------|
| **Multi-agent orchestration & visibility** | Claude Code (fork leakage, background subagent), Codex (subagent disk leakage, per-agent credit visibility), Gemini CLI (false success reports, agent hangs), Copilot CLI (coordinator stuck), Qwen Code (subagent execution visualization) | **Cross-tool pain.** Users want subagent trajectory visibility, credit attribution, and reliable completion reporting. |
| **Side-chat / thread persistence** | Codex (#26227, 17 👍), OpenCode (#37314, orphaned child sessions), DeepSeek TUI (#4705, sub-agent payload minimization) | Growing demand for non-linear conversation trees that survive session restarts. |
| **Model pool configurability & provider flexibility** | Codex (#19482, per-agent model config), Copilot CLI (#4218, 6 👍, constrain auto mode), OpenCode (#6231, 185 👍, auto-discovery), Pi (#6982, MRU switching), Qwen Code (#7449, enterprise external memory) | The single **highest-velocity feature category**. Users want to freely mix/match providers and models within and across sessions. |
| **Safety/guardrail reform** | Claude Code (Fable 5 false positives crisis), Codex (#28015, security check on `git gc`), Copilot CLI (#4221, git `-L` misclassification), DeepSeek TUI (#4684, `danger-full-access` broken) | **Systemic tension.** Current safety systems are over-flagging legitimate developer workflows, eroding trust. |
| **Windows stability & cross-platform quality** | Claude Code (GPF on VirtualBox, iOS Simulator), Codex (25+ Windows bugs), Copilot CLI (#4217, #4219, Windows crashes), Kimi Code (#2532, encoding crash), Pi (#6973, ConPTY), DeepSeek TUI (#4685, PATH corruption) | **Crisis-level pain.** Windows is universally behind macOS/Linux in stability. |
| **Credential & permission systems** | Claude Code (#5140, project-level permission override), Qwen Code (#7527, credential sanitization), Pi (#6972, malicious extension) | Enterprise adoption is driving a sharp focus on permission layering and credential hygiene. |
| **Cost/usage transparency** | Codex (#34835, compaction tracking), Copilot CLI (#4207, 6 👍, per-agent credits), OpenCode (#38398, token diagnostics), Qwen Code (#7306, tool-output budgeting) | **Cross-tool demand.** Users want granular, real-time cost breakdowns per agent/tool/session. |

---

## 4. Differentiation Analysis

| Dimension | Platform-First Tools | Agnostic/Provider-Flexible Tools |
|-----------|---------------------|--------------------------------|
| **Tools** | Claude Code, OpenAI Codex, Gemini CLI, GitHub Copilot CLI | OpenCode, Pi, Qwen Code, Kimi Code CLI, DeepSeek TUI |
| **Primary Model** | Single-vendor optimized (Anthropic Fable, OpenAI GPT, Google Gemini, GitHub Copilot) | Multi-provider (OpenAI, Anthropic, LLama.cpp, OpenRouter, DeepSeek) |
| **Architecture** | Subagent-based with background execution; deep IDE extension integration | Plugin/skill-based; TUI-first; local-first; provider-agnostic model layer |
| **Target User** | Enterprise developers in vendor-locked ecosystems | Independent developers, researchers, multi-provider power users |
| **Release Cadence** | Multiple patches per day; rapid iteration | Weekly/monthly stable releases; preview channels |
| **Safety Approach** | Heavy safety classifiers (Fable 5, Codex Guardian); permission-scanning | Sandbox-based isolation; user-trusted skills; fewer false positives |
| **Unique Differentiator** | Claude Code: `/code-review` background agent; Codex: session persistence via threading; Gemini CLI: A2A protocol; Copilot CLI: GitHub ecosystem integration | OpenCode: model auto-discovery (185 👍); Pi: constrained sampling; Qwen Code: enterprise memory profile; DeepSeek TUI: unified `/skills` manager |

**Key Insight:** The platform-first tools are racing to add more subagent complexity while fighting platform-specific stability issues. The agnostic tools are competing on provider flexibility and reduced friction (fewer false positives, better local/offline support). Both camps are converging on subagent orchestration, but the platform tools have a **feature velocity advantage** (3-10x more PRs/day) while the agnostic tools offer **lower cognitive overhead** and fewer safety roadblocks.

---

## 5. Community Momentum & Maturity

| Tool | Community Maturity | Momentum Signal | Risk Factor |
|------|-------------------|-----------------|-------------|
| **Claude Code** | **Mature / High** | 24+ comments on top issues; 10 PRs/day; active maintainer response | Fable 5 safety crisis eroding trust; fork leak concurrency bug is dangerous |
| **OpenAI Codex** | **Mature / High** | 151 👍 on single issue; 11 PRs/day; Rust alpha hotfix chain | Windows instability is systemic; 25+ bugs suggests architectural debt |
| **Gemini CLI** | **Developing / Medium** | 12 comments on top issues; 10 PRs/day; nightly security patches | Agent hang/false success undermining autonomous workflows |
| **GitHub Copilot CLI** | **Developing / Low** | 3 patch releases but only 1 stale PR; low issue engagement | Very low community PR contribution; regressions of previously fixed bugs |
| **Kimi Code CLI** | **Early / Low** | 5 issues selected; 2 PRs; no release in 24h | Very low activity relative to user base; API schema issues blocking pipeline |
| **OpenCode** | **Mature / High** | 185 👍 on top feature; 10 PRs (5 merged); Go subscription crisis response | Outage affecting paying subscribers with no ETA |
| **Pi** | **Mature / Medium** | 20+ issues/PRs in 24h; malicious extension reported; OAuth support added | Extension ecosystem safety concerns; AWS profile/env var conflict |
| **Qwen Code** | **Developing / Medium** | 10 PRs in 24h; CI red on main blocking all PRs | CI instability is a recurring pattern (3rd occurrence); credential exposure extends across codebase |
| **DeepSeek TUI** | **Developing / High** | 10 PRs (8 closed); shipping v0.9.1; 17 Dependabot alerts | Pre-release rush with security gate; macOS Dropbox paths broken |

**Maturity Ranking (by velocity + engagement):**
1. **Claude Code** (highest community engagement, active maintainers)
2. **OpenAI Codex** (high velocity, massive user base)
3. **OpenCode** (strong feature demand, responsive ecosystem)
4. **Pi** (steady velocity, growing extension ecosystem)
5. **DeepSeek TUI** (high pre-release velocity)
6. **Gemini CLI** (active but lower community engagement)
7. **Qwen Code** (developing, CI stability concerns)
8. **GitHub Copilot CLI** (low community contribution, regression-prone)
9. **Kimi Code CLI** (earliest stage, lowest activity)

---

## 6. Trend Signals

### For Developers & Technical Decision-Makers

1. **Subagent architecture is the new normal, but orchestration quality varies dramatically.** Claude Code's fork leak (double execution) and Gemini CLI's false success reports show that subagent reliability is still immature. **Recommendation:** Audit subagent behavior before trusting autonomous workflows in production.

2. **Windows is being deprioritized.** Across all tools, Windows stability is consistently behind macOS/Linux. If your team is Windows-first, expect higher defect density. **Recommendation:** Budget 20-30% more for Windows-specific testing and support.

3. **Safety/guardrail systems are in a trust crisis.** Claude Code's Fable 5 false positives, Codex's `git gc` flagging, and Copilot CLI's `-L` misclassification all demonstrate that current safety approaches are too aggressive. **Recommendation:** Monitor safety classifier accuracy; consider using tools with multi-permission-layer architectures (Pi, OpenCode) if false positives break your workflow.

4. **Cost transparency is the next frontier.** Every major tool has open requests for per-agent, per-session, and per-tool cost accounting. **Recommendation:** If cost control is critical, prioritize tools with built-in token diagnostics (OpenCode #38398, Codex #34835) or wait for this feature to mature.

5. **Model/provider flexibility is becoming table-stakes.** The 185 👍 for OpenCode's auto-discovery and the multi-provider architecture of Pi/Qwen Code/DeepSeek TUI signal that developers want to escape single-vendor lock-in. **Recommendation:** Choose tools with strong provider abstraction layers if you need to switch models frequently.

6. **Plugin/extension ecosystems are emerging but ungoverned.** Pi's malicious extension report (#6972) and the security implications of Claude Code's account profiles plugin (#80326) highlight the need for extension sandboxing. **Recommendation:** Vet extensions carefully; prefer tools with built-in permission systems over wild-west plugin markets.

7. **CI/CD reliability is fragile.** Qwen Code's third CI failure on `main` and DeepSeek TUI's 17 security alerts blocking release suggest that automated quality gates are still being built. **Recommendation:** Don't assume CI green == production-ready; monitor for breaking changes in nightly/preview channels.

### For Tool Maintainers

- **Prioritize subagent lifecycle management**—fork leaks, orphaned processes, and false completion reports are eroding trust across the ecosystem.
- **Fix Windows before adding features.** The Windows crisis is systemic and is costing enterprise adoption in Windows-heavy organizations.
- **Invest in cost accounting APIs.** This is the single most-requested cross-tool feature that no tool currently delivers well.
- **Harden the extension/plugin model.** As the ecosystem expands, sandboxing and permission systems for third-party code will become a security imperative.
- **Build for non-linear conversations.** Side-chats, threads, and session trees are the natural evolution of current linear chat models—and users are asking for them loudly.

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills Community Highlights Report
**Data as of 2026-07-23** | Source: [github.com/anthropics/skills](https://github.com/anthropics/skills)

---

## 1. Top Skills Ranking

The following are the most-discussed Skill PRs by community attention and comment activity:

### #1298 — Fix: `run_eval.py` always reports 0% recall
**Skill:** `skill-creator` (meta-skill for optimizing other skill descriptions)  
**Status:** Open | [PR #1298](https://github.com/anthropics/skills/pull/1298)

This PR addresses a critical regression where the description-optimization loop (`run_loop.py`, `improve_description.py`) produces `recall=0%` for every candidate description. Root causes span: eval artifact not installed as a real skill, Windows subprocess pipe reading failures, and parallel worker trigger detection bugs. Tied to Issue #556 (12 comments, 7 👍). The fix is foundational — without it, all skill description improvements are optimizing against noise.

### #514 — Add `document-typography` skill
**Skill:** Typographic quality control for AI-generated documents — orphan/widow prevention, numbering alignment  
**Status:** Open | [PR #514](https://github.com/anthropics/skills/pull/514)

Proposes a quality-assurance skill that catches typographic defects Claude commonly introduces (1–6 word orphan lines, section headers stranded at page bottoms). Conversation highlights: contributors noted this is a "universal frustration" across document generation workflows. The skill fills a gap between content creation and publishing readiness.

### #723 — Add `testing-patterns` skill
**Skill:** Comprehensive testing guidance — Trophy model, AAA unit tests, React Testing Library, E2E patterns  
**Status:** Open | [PR #723](https://github.com/anthropics/skills/pull/723)

Covers the full testing stack with philosophy and actionable patterns. Discussion centered on whether this duplicates existing knowledge or meaningfully encodes testing judgment into Claude's behavior. The skill's "what NOT to test" section attracted particular praise.

### #1367 — Add `self-audit` skill (v1.3.0)
**Skill:** Mechanical file verification + four-dimension reasoning quality audit before delivery  
**Status:** Open | [PR #1367](https://github.com/anthropics/skills/pull/1367)

A universal output audit gate: Step 0 mechanically verifies claimed output files exist and match specifications; then applies a four-dimension reasoning audit in damage-severity priority order. Followed by Issue #1385 proposing a three-gate pipeline (pre-task calibration → adversarial review → delivery verification). Represents the most ambitious meta-quality proposal in the repo.

### #1302 — Add `color-expert` skill
**Skill:** Color expertise for any task — naming systems (ISCC-NBS, Munsell, RAL), color space selection tables, palette construction  
**Status:** Open | [PR #1302](https://github.com/anthropics/skills/pull/1302)

Self-contained color science knowledge encoded as a skill. Includes practical "what to use when" guidance (OKLCH for scales, OKLAB for gradients, CAM16 for perception). Community feedback noted this fills a gap for designers and data visualization use cases.

### #525 — Add `pyxel` skill (retro game development)
**Skill:** MCP-driven retro game development with the Pyxel engine — write, capture, inspect, iterate  
**Status:** Open | [PR #525](https://github.com/anthropics/skills/pull/525)

Enables Claude to create pixel-art 8-bit games using the pyxel-mcp server. Unique in bridging skills with MCP tooling for an iterative creative workflow. Maintains active commentary and is by the original Pyxel author (kitao).

### #83 — Add `skill-quality-analyzer` + `skill-security-analyzer`
**Skill:** Meta-skills for community skill evaluation (5-dimension quality + security scanning)  
**Status:** Open | [PR #83](https://github.com/anthropics/skills/pull/83)

Two meta-skills for analyzing other skills: quality evaluation across structure/documentation/trigger accuracy/token efficiency/edge cases, plus security analysis for command injection, path traversal, and data exposure. Discussion surfaces tension between empowering community review and creating a moderation burden.

---

## 2. Community Demand Trends

From the top Issues, the community's most-anticipated new Skill directions are:

| Trend Signal | Key Issue | Demand Level |
|---|---|---|
| **Security & Trust Boundary** — Community skills under `anthropic/` namespace create impersonation risk | [#492](https://github.com/anthropics/skills/issues/492) (43 comments, 2 👍) | Critical |
| **Org-wide Skill Sharing** — Direct sharing within Claude.ai vs. manual .skill file distribution | [#228](https://github.com/anthropics/skills/issues/228) (14 comments, 7 👍) | High |
| **Meta-Skill Tooling Fixes** — `skill-creator` eval pipeline returns 0% recall, blocking optimization | [#556](https://github.com/anthropics/skills/issues/556) (12 comments, 7 👍) | High |
| **Agent Governance & Safety** — Dedicated skill for policy enforcement, threat detection, audit trails | [#412](https://github.com/anthropics/skills/issues/412) (6 comments) | Medium |
| **Windows Compatibility** — skill-creator scripts fail on Windows (subprocess, encoding, select) | [#1061](https://github.com/anthropics/skills/issues/1061) (3 comments, 2 👍) | Medium |
| **Skills as MCPs** — Expose skill functionality via MCP protocol for tool-callable APIs | [#16](https://github.com/anthropics/skills/issues/16) (4 comments) | Niche |
| **Reasoning Quality Pipeline** — Three-gate pre/post-task audit (calibration → review → verification) | [#1385](https://github.com/anthropics/skills/issues/1385) (3 comments) | Emerging |

**Dominant pattern:** The community wants *meta-skills* and *infrastructure* (quality gates, security scanning, sharing, eval tooling) more than domain-specific content skills. Quality assurance and trust/security are the top two concerns.

---

## 3. High-Potential Pending Skills

Active-comment PRs not yet merged — likely to land soon:

| PR | Skill | Why It May Land Soon |
|---|---|---|
| [#1298](https://github.com/anthropics/skills/pull/1298) | `skill-creator` fix (0% recall) | Blocks all other skill optimization; 10+ independent reproductions confirmed |
| [#1323](https://github.com/anthropics/skills/pull/1323) | `run_eval` trigger detection fix | Second independent fix attempt for same 0% recall issue |
| [#1367](https://github.com/anthropics/skills/pull/1367) | `self-audit` reasoning gate | Already at v1.3.0; author active in follow-up Issue #1385 |
| [#1302](https://github.com/anthropics/skills/pull/1302) | `color-expert` | Mature, self-contained, low controversy |
| [#1099](https://github.com/anthropics/skills/pull/1099) | skill-creator Windows crash fix | Third Windows fix attempt; accumulating pressure |
| [#723](https://github.com/anthropics/skills/pull/723) | `testing-patterns` | Broad appeal, well-structured, active maintainer |

---

## 4. Skills Ecosystem Insight

**The community's most concentrated demand is for *trust and quality infrastructure* — meta-skills that audit, validate, secure, and optimize other skills — rather than for new domain-specific capabilities, reflecting a maturing ecosystem where reliability and governance are now the primary barriers to adoption.**

---

# Claude Code Community Digest — 2026-07-23

## 1. Today's Highlights

The latest release (v2.1.218) introduces a meaningful architectural improvement for code review workflows by moving `/code-review` into a background subagent, while safety classifier false positives and model downgrades continue to dominate community frustration—especially around Fable 5 censorship of legitimate security work. A critical permissions bug (#5140) remains the most active open issue with 24 comments, and the community is seeing an influx of plugin contributions, including experimental account management and spec-first design tooling.

## 2. Releases

**v2.1.218** — Released today
- **`/code-review` now runs as a background subagent**, preventing review output from cluttering conversation history
- Stacked slash commands are preserved as review targets
- Added screen-reader announcements for word/line deletions (`Option+Delete`, `Ctrl+W`, `Cmd+Backspace`)
- [Full release](https://github.com/anthropics/claude-code/releases/tag/v2.1.218)

## 3. Hot Issues (Top 10)

1. **[#5140 — Permissions from user settings.json NOT applied at project level](https://github.com/anthropics/claude-code/issues/5140)**  
   *34 👍, 24 comments* | **Why it matters:** A security-critical bug: user-defined permission rules in `~/.claude/settings.json` are silently ignored when a project-level config exists. The community is actively discussing workarounds. This is the highest-engagement open issue.

2. **[#75571 — VS Code Extension hangs 90+ seconds every 30-40 min on macOS ARM64](https://github.com/anthropics/claude-code/issues/75571)**  
   *13 comments* | **Why it matters:** A reproducible performance regression affecting daily IDE usage. The native `claude` subprocess idles correctly (`kevent64`), suggesting the hang is in the extension layer. Users report lost productivity.

3. **[#71726 — Desktop app: inject queued messages mid-task between tool calls (CLI steering parity)](https://github.com/anthropics/claude-code/issues/71726)**  
   *16 👍, 8 comments* | **Why it matters:** CLI/TUI users can "steer" Claude mid-task by typing during tool execution. Desktop app users cannot—a significant UX gap that breaks agentic workflows in the desktop environment.

4. **[#78933 — Remote Control never connects on Desktop app](https://github.com/anthropics/claude-code/issues/78933)**  
   *7 comments* | **Why it matters:** `/remote-control` is completely broken on the Desktop app with `Cannot read properties of undefined (reading 'session_url')`—a hard crash on both connect and disconnect attempts.

5. **[#80348 — Fable 5: confidently claimed 'verified, copy changed' against user's correct 'no change' report](https://github.com/anthropics/claude-code/issues/80348)**  
   *2 comments* | **Why it matters:** A hallucination/self-assessment failure: Fable 5 insisted it had made a change, "verified" it, and gaslit the user. Represents a trust-breaking failure mode.

6. **[#80351 — Fable obstinately contradicts, ignores, and 'corrects' user input](https://github.com/anthropics/claude-code/issues/80351)**  
   *1 comment* | **Why it matters:** A related behavioral issue: Fable 5 doubles down on incorrect memories and dismisses user corrections. Pattern emerging of model intransigence.

7. **[#78121 — Stop hook re-fires despite stop_hook_active: true, causing /goal loop to spin](https://github.com/anthropics/claude-code/issues/78121)**  
   *1 comment* | **Why it matters:** A hook logic bug in the `/goal` system causes infinite loops. The `stop_hook_active` flag is ignored, trapping users in runaway automation.

8. **[#79722 — /fork <prompt> leaks the forked task into the parent session](https://github.com/anthropics/claude-code/issues/79722)**  
   *1 comment* | **Why it matters:** A dangerous concurrency bug: forked tasks execute in both the background agent AND the parent session, risking duplicate side effects (e.g., double commits, double API calls).

9. **[#80288 — iOS Simulator panel unusable on Xcode 27](https://github.com/anthropics/claude-code/issues/80288)**  
   *1 comment* | **Why it matters:** Two blocking bugs for mobile developers: hardcoded PrivateFrameworks path and Metal abort in the helper process. Blocks the in-app iOS Simulator on current Xcode.

10. **[#80308 — Claude Code 2.1.217 crashes with General Protection Fault on VirtualBox (Kubuntu 26.04)](https://github.com/anthropics/claude-code/issues/80308)**  
    *1 comment* | **Why it matters:** A SIGSEGV-level crash in a VM environment—suggests a native code issue (likely in the TUI renderer or terminal interaction layer).

## 4. Key PR Progress (Top 10)

1. **[#80353 — docs(gcp): stop on checksum mismatch](https://github.com/anthropics/claude-code/pull/80353)**  
   *By erichanwang* | Hardens the GCP gateway deployment script: exits with failure if the downloaded binary fails checksum verification. Security best practice.

2. **[#80326 — Add account profiles plugin](https://github.com/anthropics/claude-code/pull/80326)**  
   *By Osalumense* | Experimental plugin managing isolated `CLAUDE_CONFIG_DIR` environments for multiple Claude accounts (personal, work, client) on one machine. Commands for create, launch, assign, diagnose.

3. **[#80294, #80229 — docs: fix broken links via archive.org](https://github.com/anthropics/claude-code/pull/80294)**  
   *By mirkosalvato1-ctrl* | Two PRs fixing 1 broken outbound link each using Wayback Machine snapshots. Housekeeping for the README's npm link.

4. **[#80241 — fix: Console scrolling top of history when Claude adds text](https://github.com/anthropics/claude-code/pull/80241)**  
   *By emirhanempi5285-glitch* | Addresses a TUI bug where new output scrolls the viewport to the top. Autonomous PR (EMP_Agent).

5. **[#80196 — fix: Auto-compact never triggers despite '100% context used'](https://github.com/anthropics/claude-code/pull/80196)**  
   *By emirhanempi5285-glitch* | Fixes a context management regression: auto-compaction isn't firing even at full context. Autonomous PR.

6. **[#80195 — fix: Instantly hitting usage limits with Max subscription](https://github.com/anthropics/claude-code/pull/80195)**  
   *By emirhanempi5285-glitch* | Addresses a billing/usage accounting bug where Max subscribers exhaust quotas immediately. Autonomous PR.

7. **[#80112 — Make devcontainer firewall init resilient to DNS resolution failures](https://github.com/anthropics/claude-code/pull/80112)**  
   *By bthomas1000* | Prevents `.devcontainer/init-firewall.sh` from aborting on transient DNS failures. Uses `set -euo pipefail` hardening.

8. **[#80008 — Add twilight plugin: spec-first design/implement with durable focus stack](https://github.com/anthropics/claude-code/pull/80008)**  
   *By jklappenbach* | A demo/template for spec-first development: combine design, implementation, and a "focus stack" to structure Claude's reasoning. Explicitly marked as needing significant modification before acceptance.

## 5. Feature Request Trends

- **Desktop ↔ CLI parity** (#71726): Users increasingly demand mid-task message injection ("steering") in the Desktop app—the single most-upvoted feature request in the issue tracker (16 👍).
- **Sandbox mode visibility** (#56843, closed): Requesting a statusline field to display current sandbox mode (Docker, local, or none). Closed stale but sentiment is clear.
- **Non-English session titles** (#67724, closed): Auto-generated titles remain English for non-English users. Closed as duplicate, but signals demand for i18n improvements.
- **Security audit support** (#67733, closed): Feature request for native support of repository-wide security audit analysis without triggering safety filters.
- **Account profile isolation** (#80326 via PR): Plugin-based multi-account management emerging as a community-driven solution for credential conflicts.

## 6. Developer Pain Points

1. **Fable 5 safety classifier false positives** (#67732, #67734, #67737, #67723, #80351): A cluster of reports where Fable 5's content moderation incorrectly flags legitimate security research, legal analysis, and defense use cases—then downgrades the session to Opus 4.8 or blocks it entirely. This is the single biggest frustration this week.

2. **Permission system inconsistencies** (#5140): User-level permissions silently ignored when project-level settings exist. Security implications and no clear workaround.

3. **Fork leakage** (#79722): Background forking mechanism has a data race—forked commands execute in both parent and child sessions. High risk of unintended side effects.

4. **Bash tool cwd resets** (#67725, closed): Working directory resets on every Bash tool invocation, breaking git worktree workflows. Minor but persistent friction for shell-heavy usage.

5. **Context/usage accounting bugs** (#67693, #67578, #80195): Users hit session limits or see unexplained quota depletion, especially Max subscribers. Billing/usage tracking appears fragile.

6. **Windows-specific regressions** (#69234, #78933, #78858, #67667): Alt+V image paste fails per-session, remote control is broken, HCS services missing, and console errors on launch. Windows users face a higher defect density than other platforms.

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex Community Digest — July 23, 2026

## Today's Highlights
A flood of ~50 new Rust alpha releases arrived overnight, though the community remains laser-focused on mounting Windows stability issues. Over 25 Windows-specific bugs were updated in the last 24 hours alone, spanning performance regressions, WSL integration breakage, and desktop app startup failures. On the PR side, a large batch of copyberry[bot] merges touched thread persistence, analytics reliability, and sandbox prompt rendering, signaling ongoing investment in session management and infrastructure hardening.

## Releases
Four new alpha releases were cut in the last 24 hours, all in the `rust-` channel:
- **rust-v0.146.0-alpha.1**, **.alpha.2**, and **.alpha.3** — consecutive hotfix alphas suggesting rapid iteration on a new feature branch.
- **rust-v0.145.0-alpha.30** — likely a patch for the v0.145.x series.

No release notes or changelog summaries were included beyond generic "Release 0.xxx" text, typical for these automated tags.

## Hot Issues
*(10 noteworthy issues with high community engagement or systemic impact)*

1. **[#28969 — Add setting to disable auto-resolve in 60 seconds for questions](https://github.com/openai/codex/issues/28969)**  
   *Comments: 53, 👍: 151* — Users are frustrated by CLI's automatic session resolution after 60 seconds of inactivity. This request has massive traction (151 upvotes), indicating that long-running reasoning sessions are now a core workflow and the timeout is a friction point.

2. **[#20214 — Codex App frequently freezes/stutters on Windows 11 Pro](https://github.com/openai/codex/issues/20214)**  
   *Comments: 72, 👍: 71* — A months-old performance bug that continues to gain traction. Users report freezes even with ample system resources (Ryzen 5, 32 GB RAM), suggesting a toolchain or renderer issue rather than resource starvation.

3. **[#34014 — Standalone Windows app triggers WMI Provider Host at 90–100% CPU](https://github.com/openai/codex/issues/34014)**  
   *Comments: 18, 👍: 11* — A newly surfaced CPU-spiking bug caused by Windows Management Instrumentation queries, notably absent in the VS Code extension running the same project. Points to app-level instrumentation code that's not lazy.

4. **[#34061 — Insane Codex Disk Usage from Subagents](https://github.com/openai/codex/issues/34061)**  
   *Comments: 7, 👍: 1* — Subagents (explorer, worker) reportedly consume gigabytes of disk space, likely from orphaned checkpoints or session logs. This is a hidden cost for Pro users running complex multi-agent workflows.

5. **[#28015 — False positive cybersecurity safety check blocks normal repo maintenance](https://github.com/openai/codex/issues/28015)**  
   *Comments: 22, 👍: 3* — The safety-check system is triggering on routine DevOps tasks like `git gc` and package cleanup, forcing users through unnecessary confirmation dialogs. Erodes trust in the safety feature.

6. **[#20730 — Custom pets fail to load in WSL environments due to path normalization](https://github.com/openai/codex/issues/20730)**  
   *Comments: 11, 👍: 20* — A niche but passionate feature (custom terminal pets) breaks in WSL because of Windows/Linux path mismatches. 20 upvotes suggest a dedicated group of users who depend on this customization.

7. **[#30712 — Windows app injects split writable roots, causing apply_patch to fail](https://github.com/openai/codex/issues/30712)**  
   *Comments: 10, 👍: 11* — Sandbox writable-root splitting on Windows makes the safe `apply_patch` path unusable, forcing agents to bypass sandbox and write files via PowerShell. A security regression.

8. **[#16815 — WSL agent mode fails with path deserialization error](https://github.com/openai/codex/issues/16815)**  
   *Comments: 22, 👍: 13* — Four months old and still open. WSL agent mode fails on `AbsolutePathBuf deserialized without a base path`, blocking a key use case for developers on hybrid Windows/Linux workflows.

9. **[#26227 — Persist side chats as child threads attached to main thread](https://github.com/openai/codex/issues/26227)**  
   *Comments: 7, 👍: 17* — Users love side-chat patterns but lose them on session close. Request to make side chats first-class persistent child threads that survive restarts and updates.

10. **[#27117 — Windows update from pwsh inherits PSModulePath, breaking Get-FileHash](https://github.com/openai/codex/issues/27117)**  
    *Comments: 8, 👍: 11* — When launched from PowerShell 7, the update process spawns Windows PowerShell and inherits incompatible module paths, breaking file hash verification. A cross-shell compatibility bug.

## Key PR Progress
*(10 significant PRs merged or updated in the last 24 hours)*

1. **[#34840 — Add persisted thread pinning to the app server](https://github.com/openai/codex/pull/34840)**  
   New `isPinned` field on threads plus API support for pin/unpin and filtering. Directly addresses user demand for thread organization.

2. **[#34839 — Preserve user input when MCP startup is interrupted](https://github.com/openai/codex/pull/34839)**  
   Fixes a data-loss bug where interrupting during MCP tool startup would lose the user's submitted message. Builds MCP state as a step snapshot rather than ephemerally.

3. **[#34835 — Track compaction time in turn profiles](https://github.com/openai/codex/pull/34835)**  
   Adds `compaction_ms` to analytics, separating compaction time from idle time. Helps identify sessions where compaction is a performance bottleneck.

4. **[#34831 — Flush analytics before in-process app server shutdown](https://github.com/openai/codex/pull/34831)**  
   Fixes data loss of completed-turn and accepted-line events when the in-process app server exits before flushing its analytics queue.

5. **[#34825 — Reduce cloning when building Responses requests](https://github.com/openai/codex/pull/34825)**  
   Performance optimization for Responses API: serializes tool definitions into shared raw JSON and uses shallow diffs for WebSocket requests, reducing per-request allocations.

6. **[#34824 — Normalize Guardian review cwd reuse keys](https://github.com/openai/codex/pull/34824)**  
   Stores working directory as `PathUri` in reuse keys to fix session comparison mismatches caused by path representation differences.

7. **[#34819 — Enable git attribution across Codex entry points](https://github.com/openai/codex/pull/34819)**  
   Installs git attribution extension in the app server, MCP server, and debug CLI, enabling authenticated workspace policy to control commit and PR attribution instructions.

8. **[#34816 — Support configurable realtime BEM channel prefixes](https://github.com/openai/codex/pull/34816)**  
   Adds `codexResponseHandoffChannelPrefixes` configuration for realtime V3 handoffs, allowing clients to customize `[ANALYSIS]`, `[COMMENTARY]`, and `[FINAL]` prefixes.

9. **[#34811 — Fix network access rendering in sandbox prompts](https://github.com/openai/codex/pull/34811)**  
   Replaces broken placeholder syntax with supported `{{ network_access }}` in sandbox templates for `danger-full-access`, `read-only`, and `workspace-write` permissions.

10. **[#34808 — Centralize SQLite connection configuration](https://github.com/openai/codex/pull/34808)**  
    Adds a consolidated `SqliteConfig` struct to manage database paths and connection pool settings, replacing ad-hoc path helpers across the codebase.

## Feature Request Trends
Three dominant directions emerged from today's issues:

1. **Side-chat/persistence as a first-class feature** — Multiple high-vote requests (#26227, #34840 PR) want chat trees, pinning, and child threads that survive app restarts. Users view side chats as essential for complex multi-hour sessions.

2. **Subagent and multi-agent model configuration** — Users want to configure which model powers each subagent (explorer, worker, custom agents) globally via `config.toml` rather than per-agent files (#19482). With the rise of domain-specific models (gpt-5.6-sol, terra, luna), per-agent model assignment is a growing pain point.

3. **Rate-limit and budget flexibility** — One issue asks for a return of the 5-hour hard limit alongside or instead of the percentage-based plan, citing massive overnight consumption on Ultra runs (#34822). Power users want more granular/tiered budget controls, not just higher caps.

## Developer Pain Points
- **Windows is in crisis mode.** 20+ of the top 30 issues are Windows-specific: WMI CPU spikes, WSL path deserialization crashes, PowerShell module inheritance breaks, sandbox writable-root failures, and update-induced startup errors. The Windows Codex experience is visibly behind macOS/Linux in stability.
- **Subagent disk/cpu leakage.** Multiple reports (#34061, #17574) describe subagent processes and session data accumulating indefinitely, consuming gigabytes of space and spiking CPU. No cleanup mechanism exists.
- **Safety-check overreach.** The cybersecurity safety check is flagging routine operations (git maintenance, package cleanup) as potential threats (#28015), interrupting paid sessions and eroding trust in the safety system.
- **Session/thread state corruption.** Reports of `chat_processes.json` filled with NUL bytes (#29593), stale project ID migrations (#33774), and threads appearing in wrong workspaces (#32082, #34457) suggest the session storage layer has race conditions or migration bugs that trigger on Windows app updates.

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI Community Digest — 2026-07-23

## Today's Highlights

Two new releases landed today: the stable **v0.52.0** and a preview **v0.53.0-preview.0** featuring critical A2A tool-response grouping fixes and an early LLM-based issue triage orchestrator. Security momentum is strong—a nightly patch enforces workspace trust and task isolation to prevent RCE in the A2A server, while ongoing community issues continue to surface agent reliability concerns around subagent recovery, hangs, and shell-command deadlocks.

## Releases

**v0.53.0-preview.0**
- [`28407`](https://github.com/google-gemini/gemini-cli/pull/28407): Fixes `400 Bad Request` errors by grouping cancelled A2A tool responses and coalescing consecutive roles.
- Introduces an LLM-based caretaker triage orchestrator with container build support.

**v0.52.0**
- [`28216`](https://github.com/google-gemini/gemini-cli/pull/28216): Refactors workspace context to exclude transient CI configuration files.
- Adds foundational triage worker modules for the caretaker system.

**v0.52.0-nightly.20260722.gc776c665b**
- [`28470`](https://github.com/google-gemini/gemini-cli/pull/28470): Enforces workspace trust and task isolation in the A2A server to prevent remote code execution (RCE).

## Hot Issues

1. **[#22323](https://github.com/google-gemini/gemini-cli/issues/22323) — Subagent recovery after MAX_TURNS falsely reports success** (👍2, 💬12)  
   The `codebase_investigator` subagent claims `status: "success"` even when it hit the turn limit before doing analysis. This masks real failures and undermines trust in agent reporting.

2. **[#21409](https://github.com/google-gemini/gemini-cli/issues/21409) — Generalist agent hangs forever** (👍8, 💬8)  
   Simple folder creation tasks hang indefinitely when the generalist agent is invoked. Users must instruct the model to avoid sub-agents entirely—a workaround, not a fix.

3. **[#19873](https://github.com/google-gemini/gemini-cli/issues/19873) — Zero-Dependency OS Sandboxing for bash affinity** (👍1, 💬8)  
   Proposes leveraging Gemini 3's native bash training with secure POSIX sandboxing. A large-effort enhancement that could dramatically improve code exploration performance.

4. **[#24353](https://github.com/google-gemini/gemini-cli/issues/24353) — Component-level evaluations** (💬7)  
   An epic tracking 76 behavioral eval tests across 6 Gemini models. The push for systematic evaluation infrastructure shows the team's commitment to quality gates.

5. **[#22745](https://github.com/google-gemini/gemini-cli/issues/22745) — AST-aware file reads and codebase mapping** (👍1, 💬7)  
   Investigates whether AST-aware tools can reduce token waste by reading only method bounds. Could significantly improve performance on large codebases.

6. **[#21968](https://github.com/google-gemini/gemini-cli/issues/21968) — Gemini under-uses custom skills and sub-agents** (💬6)  
   Custom skills like "gradle" and "git" are ignored unless explicitly instructed. The model fails to autonomously leverage available tooling.

7. **[#26522](https://github.com/google-gemini/gemini-cli/issues/26522) — Auto Memory retries low-signal sessions indefinitely** (💬5)  
   Sessions that the extraction agent skips remain unprocessed, causing repeated retries. Hinders memory efficiency and user trust.

8. **[#25166](https://github.com/google-gemini/gemini-cli/issues/25166) — Shell command gets stuck "Waiting input" after completion** (👍3, 💬4)  
   Even trivial commands hang with "Awaiting user input" after finishing. A high-friction bug for daily CLI use.

9. **[#22232](https://github.com/google-gemini/gemini-cli/issues/22232) — Browser agent resilience: session takeover and lock recovery** (💬4)  
   The browser agent's "fail-fast" strategy on locked profiles is too brittle. Users want automatic lock recovery for persistent sessions.

10. **[#21983](https://github.com/google-gemini/gemini-cli/issues/21983) — Browser subagent fails on Wayland** (👍1, 💬4)  
    The browser agent errors out under Wayland display servers. Linux users face a platform-specific blocker.

## Key PR Progress

1. **[#28509](https://github.com/google-gemini/gemini-cli/pull/28509) — Filter thought parts from history turns**  
   Prevents internal monologue leakage from causing duplicate reasoning blocks in Gemini 2.x with context management disabled.

2. **[#28469](https://github.com/google-gemini/gemini-cli/pull/28469) — Rotate session ID on model fallback**  
   Fixes a blocking API error when falling back to `gemini-2.5-flash` by rotating the session ID to avoid stateful backend errors.

3. **[#28485](https://github.com/google-gemini/gemini-cli/pull/28485) — Add gemini-3.5-flash to model selector**  
   Patches the legacy model selector to surface `gemini-3.5-flash`, which was defined but hidden from users.

4. **[#28506](https://github.com/google-gemini/gemini-cli/pull/28506) — Propagate AbortSignal in /compress command**  
   Makes background compression cancellable, preventing dangling network requests when users start new prompts.

5. **[#28446](https://github.com/google-gemini/gemini-cli/pull/28446) — Use native fetch for OAuth token exchange**  
   Fixes "Premature close" errors on headless VPSes by replacing the failing HTTP client with native fetch.

6. **[#28431](https://github.com/google-gemini/gemini-cli/pull/28431) — PR generator infrastructure: Cloud Run + Workflows**  
   Introduces containerized runtime and Eventarc-triggered workflows for automated code generation pipelines.

7. **[#28499](https://github.com/google-gemini/gemini-cli/pull/28499) — Restrict tools.core wildcard DENY to built-ins**  
   Prevents wildcard deny rules from silently excluding all MCP tools—scopes the restriction to core tools only.

8. **[#28169](https://github.com/google-gemini/gemini-cli/pull/28169) — Eval coverage report command**  
   Adds `eval:coverage` to cross-reference tool usage across eval inventory, improving test transparency.

9. **[#28505](https://github.com/google-gemini/gemini-cli/pull/28505) — Fix broken doc cross-reference links**  
   Adds missing `.md` extensions to six links, fixing 404 errors on GitHub's rendered documentation.

10. **[#28024](https://github.com/google-gemini/gemini-cli/pull/28024) — Bump OpenTelemetry core to 2.8.0**  
    Routine dependency update for improved observability instrumentation.

## Feature Request Trends

- **AST-aware tooling**: Multiple issues ([#22745](https://github.com/google-gemini/gemini-cli/issues/22745), [#22746](https://github.com/google-gemini/gemini-cli/issues/22746)) request AST-aware file reads, search, and mapping to reduce token waste and improve precision.
- **Agent self-awareness**: Users want the CLI to accurately describe its own flags, hotkeys, and capabilities ([#21432](https://github.com/google-gemini/gemini-cli/issues/21432)).
- **Subagent visibility**: Requests for subagent trajectories in `/chat share` ([#22598](https://github.com/google-gemini/gemini-cli/issues/22598)) and bug reports that include subagent context ([#21763](https://github.com/google-gemini/gemini-cli/issues/21763)).
- **Robust memory system**: Improvements for Auto Memory to avoid indefinite retries, quarantine invalid patches, and add deterministic redaction ([#26522](https://github.com/google-gemini/gemini-cli/issues/26522), [#26523](https://github.com/google-gemini/gemini-cli/issues/26523), [#26525](https://github.com/google-gemini/gemini-cli/issues/26525)).
- **Browser agent resilience**: Automatic session takeover and lock recovery for persistent browser profiles ([#22232](https://github.com/google-gemini/gemini-cli/issues/22232)).

## Developer Pain Points

- **Agent hangs and false success**: The generalist agent hangs forever ([#21409](https://github.com/google-gemini/gemini-cli/issues/21409)) and subagents report success after reaching turn limits ([#22323](https://github.com/google-gemini/gemini-cli/issues/22323)). These undermine confidence in autonomous execution.
- **Shell command deadlocks**: Commands frequently get stuck "Waiting input" after finishing ([#25166](https://github.com/google-gemini/gemini-cli/issues/25166)), and interactive prompts (e.g., vite create) cause hangs ([#22465](https://github.com/google-gemini/gemini-cli/issues/22465)).
- **Browser agent platform failures**: Wayland users are blocked entirely ([#21983](https://github.com/google-gemini/gemini-cli/issues/21983)), and settings.json overrides like maxTurns are ignored ([#22267](https://github.com/google-gemini/gemini-cli/issues/22267)).
- **Unwanted subagent activation**: Agents run without permission after updates ([#22093](https://github.com/google-gemini/gemini-cli/issues/22093)), and destructive shell commands (e.g., `git reset --force`) lack guardrails ([#22672](https://github.com/google-gemini/gemini-cli/issues/22672)).
- **Tool and model limitations**: >128 tools cause 400 errors ([#24246](https://github.com/google-gemini/gemini-cli/issues/24246)), and the model creates temp scripts in random directories ([#23571](https://github.com/google-gemini/gemini-cli/issues/23571)).
- **Terminal and input bugs**: Corruption after exiting external editors ([#24935](https://github.com/google-gemini/gemini-cli/issues/24935)), flicker on resize ([#21924](https://github.com/google-gemini/gemini-cli/issues/21924)), and incorrect `\n` escape handling ([#22466](https://github.com/google-gemini/gemini-cli/issues/22466)).

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI Community Digest
**2026-07-23**

## Today's Highlights
Three patch releases (v1.0.74-1 through v1.0.74-3) landed today, adding Gemini 3.6 Flash support and an opt-in sandbox splash screen. The community saw a significant influx of new issues (over 15 opened in the last 24 hours), with major themes including Windows stability regressions, tmux rendering problems, and subagent coordination bugs. A resurgence of the React/Ink infinite render loop (#4222) and a new Windows exit crash (#4217) are drawing developer attention.

## Releases
**v1.0.74-1, v1.0.74-2, v1.0.74-3** (three patches in succession)

- **Added**: First-run splash screen to opt into the default sandbox
- **Added**: Support for `gemini-3.6-flash` model
- **Improved**: Multiplexing sessions no longer leak open dialogs between sessions; eligible pickers reopen on switching back
- **Improved**: The `$` interactive shell shortcut now works as expected (description truncated in changelog)
- **Fixes**: General fixes and changes across v1.0.74-2 and v1.0.74-3 (changelog not detailed)

## Hot Issues
*Top 10 noteworthy issues from the last 24 hours, ranked by community impact.*

1. **[#4222](https://github.com/github/copilot-cli/issues/4222) — Regression of #2802: React/Ink render loop** (Triage)
   The infinite render loop from v1.0.31 has returned on v1.0.72+ in VS Code integrated terminal on native Windows. Main pane freezes, output is swallowed. Community reaction: users are frustrated by a regression of a previously fixed bug.

2. **[#4223](https://github.com/github/copilot-cli/issues/4223) — Shell completion never detected inside tmux** (Triage)
   Commands inside tmux execute and produce output, but CLI never detects completion—trivial commands like `echo hello` hang as "still running." Critical for anyone using Copilot CLI within tmux workflows.

3. **[#4217](https://github.com/github/copilot-cli/issues/4217) — Crash on exit (Windows) — libuv `uv_async_send` on closing handle** (Triage)
   Consistent `FAST_FAIL_FATAL_APP_EXIT` during teardown on Windows x64. Work completes normally; crash occurs only at exit. WinDbg analysis points to a race condition with async handles.

4. **[#4219](https://github.com/github/copilot-cli/issues/4219) — Crash when `notifications` enabled (Windows)** (Triage)
   Hard native access violation crash when the notifications setting is enabled. Toast path appears to have a memory safety issue on Windows.

5. **[#4221](https://github.com/github/copilot-cli/issues/4221) — Permission scanner misclassifies git `-L` arguments** (Triage)
   Shell command text like `git log -L` search expressions are misidentified as directory paths, causing false permission prompts. Impacts developer workflow efficiency.

6. **[#4225](https://github.com/github/copilot-cli/issues/4225) — Coordinator stuck "Working" while subagent runs** (Triage)
   UI shows "Working" indefinitely while only a background subagent is active. Queued input is neither answered nor shown as pending. Points to orchestration bugs.

7. **[#4227](https://github.com/github/copilot-cli/issues/4227) — Xcode ACP custom agent: session/prompt always fails** (Triage)
   Despite valid CLI and auth, Xcode fails with "failed to produce a response" when using Copilot CLI as a custom agent via ACP. Blocks macOS/Xcode developers.

8. **[#4212](https://github.com/github/copilot-cli/issues/4212) — Invisible prompt/highlights inside tmux (dark-on-dark)** (Triage)
   Prompt box and menu items render as dark text on dark background inside tmux. Works correctly outside tmux. Theming and accessibility concern.

9. **[#4207](https://github.com/github/copilot-cli/issues/4207) — Feature: Show per-subagent AI credit usage in /usage** (Sessions/Agents)
   Cumulative credit usage is displayed but doesn't show distribution among individual agents. 👍: 6 — strong demand for cost transparency in multi-agent workflows.

10. **[#4220](https://github.com/github/copilot-cli/issues/4220) — Plan mode blocks read-only `gh api` queries** (Triage)
    Plan mode's command gate falsely classifies `gh api` GET/GraphQL queries as potentially workspace-modifying. Hinders investigation workflows in plan mode.

## Key PR Progress
*Only one PR was active in the last 24 hours.*

1. **[#3163](https://github.com/github/copilot-cli/pull/3163) — ViewSonic monitor** (OPEN)
   References GitHub Actions runner initialization. PR description is sparse; appears to be related to display/monitor configuration for CI testing. Created 2026-05-06, still open with no comments.

## Feature Request Trends
*Distilled from issues opened in the last 24 hours:*

- **Model pool configurability** ([#4218](https://github.com/github/copilot-cli/issues/4218), 👍: 6): Users want to constrain which models Auto mode can select — current behavior picks from all available models, making cost unpredictable.
- **Per-agent credit transparency** ([#4207](https://github.com/github/copilot-cli/issues/4207), 👍: 6): Strong demand for breakdown of AI credit usage by subagent/agent invocation in `/usage`.
- **Agent chaining** ([#4208](https://github.com/github/copilot-cli/issues/4208), 👍: 3): Users want explicit inline invocation of custom agents and the ability to chain agent results within a single prompt.
- **Shell integration sequences** ([#3428](https://github.com/github/copilot-cli/issues/3428)): Emit OSC 133 sequences so terminals can navigate to previous prompts and final-answer lines.

## Developer Pain Points
*Recurring frustrations and high-frequency requests from the last 24 hours:*

- **Windows stability is deteriorating**: Multiple crash reports (exit crash #4217, notification crash #4219, render loop regression #4222) suggest recent builds have introduced platform-specific bugs.
- **tmux compatibility is broken**: Two separate issues (#4212, #4223) report rendering and command-detection failures inside tmux, a critical tool for many developers.
- **Subagent coordination is unreliable**: Multiple reports (#4225, #4226) describe subagents causing the UI to hang, spam server errors, or fail to report completion — orchestration quality needs attention.
- **Permission scanner false positives**: The command gate (#4220) and permission scanner (#4221) are flagging legitimate read-only operations, breaking workflows in plan mode and with git log commands.
- **Xcode ACP integration broken**: [#4227](https://github.com/github/copilot-cli/issues/4227) reports a complete failure to use Copilot CLI as a custom agent in Xcode, blocking a key integration path.

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI Community Digest
**2026-07-23**

---

## Today's Highlights
The community faces escalating rate-limit constraints (#2318) with TPD usage exceeding 1.5M requests, while developers report critical API compatibility issues (#2531) and cross-platform encoding crashes (#2532). Two PRs targeting tool counting accuracy and shell process management are progressing through review.

---

## Releases
No new releases in the last 24 hours. Latest stable version: **kimi 2.6**.

---

## Hot Issues

1. **#2318 - TPD Rate Limit Breach** (Open, 2👍)  
   *What:* User reports hitting Moonshot API TPD rate limit of ~1.5M requests with Kimi CLI 2.6 on Windows 10.  
   *Why matters:* Suggests aggressive request batching or missing quota management in the CLI.  
   *Community:* Single comment, but high reaction count indicates many affected users awaiting fix.  
   *Link:* [Issue #2318](https://github.com/MoonshotAI/kimi-cli/issues/2318)

2. **#2531 - MCP Tool Schema Rejected by API** (Open, New)  
   *What:* Moonshot API returns HTTP 400 for tool schemas using `anyOf` without inline `type`. Blocks all MCP tool usage.  
   *Why matters:* Developer tooling pipeline completely broken; no workaround exists client-side.  
   *Community:* User identified the root cause — Moonshot API expects flattened JSON Schema.  
   *Link:* [Issue #2531](https://github.com/MoonshotAI/kimi-cli/issues/2531)

3. **#2532 - Startup Crash on Windows with stdout Redirection** (Open, New)  
   *What:* `kimi web` crashes on Chinese-locale Windows when stdout is piped — UnicodeEncodeError on `➜` character (U+279C).  
   *Why matters:* Blocks CI/CD pipelines, logging, and IDE integrations on Windows.  
   *Community:* No comments yet, but encodes a major cross-platform compatibility gap.  
   *Link:* [Issue #2532](https://github.com/MoonshotAI/kimi-cli/issues/2532)

4. **[Existing] #2468 - Shell Command Hangs on Detached Children** (Referenced in PR #2530)  
   *What:* Foreground shell commands hang indefinitely if a child process holds pipes open.  
   *Why matters:* Breaks common patterns like `some_daemon & echo done`.  
   *Link:* [Issue #2468](https://github.com/MoonshotAI/kimi-cli/issues/2468)

5. **[Existing] #2526 - StrReplaceFile Replacement Count Miscalc** (Referenced in PR #2524)  
   *What:* Replacement count is computed against original file content, not running content after sequential edits.  
   *Why matters:* Causes incorrect reporting in code modification workflows.  
   *Link:* [Issue #2526](https://github.com/MoonshotAI/kimi-cli/issues/2526)

[Selected 5 highest-signal issues from available data]

---

## Key PR Progress

1. **#2524 - fix(tools): count StrReplaceFile replacements against running content** (Open)  
   *Author:* Sreekant13  
   *Summary:* Fixes replacement count calculation to account for chained edits where `old` string is produced by earlier operations.  
   *Impact:* Corrects reporting for multi-step file modification workflows.  
   *Link:* [PR #2524](https://github.com/MoonshotAI/kimi-cli/pull/2524)

2. **#2530 - fix(shell): stop blocking until timeout when a detached child holds the pipes** (Open)  
   *Author:* ayaangazali  
   *Summary:* Changes `_run_shell_command` to check exit code before waiting for EOF on stdout/stderr, preventing hangs with background processes.  
   *Impact:* Fixes common shell scripting patterns in Kimi Code CLI context.  
   *Link:* [PR #2530](https://github.com/MoonshotAI/kimi-cli/pull/2530)

*Note: Only 2 PRs updated in the last 24h — typical for a Thursday with no release day.*
*Additional 8 PRs from previous days may be selected in larger digests.*

---

## Feature Request Trends

Based on reviewed issues and community discussion patterns:
- **Rate Limit Visibility & Management**: Users need CLI-side mechanisms to monitor and respect TPD quotas (#2318)
- **Cross-Platform Encoding Robustness**: Persistent Windows/i18n encoding issues (#2532)
- **API Schema Compatibility**: Tightening client-side JSON Schema generation to match Moonshot API expectations (#2531)
- **Shell Background Process Support**: Proper handling of detached processes and pipe lifecycles (#2468, #2530)

---

## Developer Pain Points

- **Rate Limit Surprise**: Hard TPD caps are hit without warning or graceful degradation — users discover failures mid-workflow (#2318)
- **Schema Validation Black Box**: No client-side sanitization of MCP tool schemas before API submission, causing opaque 400 errors (#2531)
- **Windows Second-Class Citizen**: Encoding-related crashes on Chinese-locale Windows block adoption in enterprise/CI environments (#2532)
- **Shell Process Lifecycle Blindness**: CLI fails to distinguish between foreground completion and detached processes, causing indefinite hangs (#2468, related #2530)
- **Sequential Edit Counting**: Mismatched replacement counts erode trust in automated file modification tools (#2526)

---

*Generated by AI technical analyst. Data from [github.com/MoonshotAI/kimi-cli](https://github.com/MoonshotAI/kimi-cli).*

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode Community Digest — 2026-07-23

## Today's Highlights

A major outage hit **OpenCode Go** subscribers today: multiple reports confirm that all Go subscription models are returning `401 Request blocked by upstream provider` errors, while free models and `/v1/models` listing continue to work. Separately, the community is rallying behind a long-standing request for **auto-discovery of models from OpenAI-compatible providers** (185 👍), and two substantial TUI theme/syntax PRs from core contributor `jlongster` are in review.

## Releases

No new OpenCode version was released in the last 24 hours. The latest release remains at **1.18.4** (Desktop) and **1.3.3** (CLI).

## Hot Issues

1. **#6231 – Auto-discover models from OpenAI-compatible provider endpoints**  
   *Author: ochsec | 185 👍 | 28 comments*  
   Users want OpenCode to automatically fetch the model list from providers like LM Studio, Ollama, and llama.cpp instead of requiring manual configuration. With 185 reactions, this is the most upvoted open feature request.  
   [GitHub](https://github.com/anomalyco/opencode/issues/6231)

2. **#38257 – OpenCode Go: 401 blocked upstream on chat/completions**  
   *Author: lizijiangyyjx | 8 👍 | 25 comments*  
   Starting 2026-07-22, all Go subscription chat/completion calls fail with 401, though model discovery works. Appears to be a server-side issue.  
   [GitHub](https://github.com/anomalyco/opencode/issues/38257)

3. **#38218 – All Go subscription models blocked**  
   *Author: 1335907208 | 5 👍 | 21 comments*  
   Another high-activity report of the same Go outage — no single model works for completions. Strongly correlated with #38257.  
   [GitHub](https://github.com/anomalyco/opencode/issues/38218)

4. **#19466 – CPU pegged at 50% while rate-limit waiting**  
   *Author: Jaaaky | 11 👍 | 15 comments*  
   OpenCode consumes ~50% of a single i9-14900 core while "doing nothing" (rate-limit backoff). Community concerned about idle resource waste.  
   [GitHub](https://github.com/anomalyco/opencode/issues/19466)

5. **#38195 – 401 AuthError on Go subscription cross-platform**  
   *Author: faustkuroki | 15 👍 | 15 comments*  
   Confirmed on both Desktop and Hermes on Windows/macOS. Free models work; only Go subscriptions fail.  
   [GitHub](https://github.com/anomalyco/opencode/issues/38195)

6. **#18011 – LM Studio shows only 3/9 models**  
   *Author: firexrwt | 4 👍 | 6 comments*  
   Auto-discovery from LM Studio is incomplete — only 3 of 9 available models appear, even with API key. Related to #6231.  
   [GitHub](https://github.com/anomalyco/opencode/issues/18011)

7. **#37970 – Plan/Build mode missing in latest version**  
   *Author: BillyJack76 | 1 👍 | 10 comments*  
   Users report the Plan/Build mode toggle disappeared in v1.18.0, breaking their workflow for planning vs. executing changes.  
   [GitHub](https://github.com/anomalyco/opencode/issues/37970)

8. **#26220 – Infinite loop after tool calls complete**  
   *Author: Dvalin21 | 3 👍 | 6 comments*  
   OpenCode enters an infinite loop and becomes unresponsive after finishing tool calls. Affects the "Big Pickle" variant.  
   [GitHub](https://github.com/anomalyco/opencode/issues/26220)

9. **#26459 – Clipboard copy fails in web-based VSCode**  
   *Author: xuxusheng | 1 👍 | 7 comments*  
   "Copied to clipboard" appears but content isn't actually copied in code-server, Codespaces, and Gitpod. Affects remote workflows.  
   [GitHub](https://github.com/anomalyco/opencode/issues/26459)

10. **#22260 – Read tool should support audio/video attachments**  
    *Author: soaringk | 7 👍 | 7 comments*  
    Agents can't inspect local media files because read tool rejects audio/video as binary. Community wants model-native media attachment support.  
    [GitHub](https://github.com/anomalyco/opencode/issues/22260)

## Key PR Progress

1. **#38401 – fix(core): load dynamic models for generation**  
   *Author: kitlangton | Open*  
   Enables `/api/generate` to use dynamically loaded models (e.g., Gemini 3.5 Flash) that previously failed with "Unsupported package."  
   [GitHub](https://github.com/anomalyco/opencode/pull/38401)

2. **#38396 – docs(tui): add generated V2 theme reference**  
   *Author: jlongster | Merged*  
   Adds authoritative V2 TUI theme documentation generated from the Effect schema, with CI enforcement.  
   [GitHub](https://github.com/anomalyco/opencode/pull/38396)

3. **#38397 – refactor(tui): generate syntax from V2 theme**  
   *Author: jlongster | Open*  
   Replaces V1 syntax-theme resolution with V2 token-based generation, covering 101 syntax scopes. Preserves mini-TUI compatibility.  
   [GitHub](https://github.com/anomalyco/opencode/pull/38397)

4. **#38398 – feat(tui): add turn token usage diagnostics**  
   *Author: jlongster | Open*  
   Shows per-turn token usage (new, cached, total) with cache-bust warnings and a DevTools toggle.  
   [GitHub](https://github.com/anomalyco/opencode/pull/38398)

5. **#33403 – feat(run): forward child session events to NDJSON stream**  
   *Author: cHIsIMun | Merged*  
   `opencode run --format json` now includes subagent events, fixing silent filtering of task tool events.  
   [GitHub](https://github.com/anomalyco/opencode/pull/33403)

6. **#33450 – feat(tui): add global session picker toggle**  
   *Author: onurmicoogullari | Merged*  
   Adds explicit global mode to TUI session picker so users can discover/resume sessions from other projects.  
   [GitHub](https://github.com/anomalyco/opencode/pull/33450)

7. **#33444 – fix(session): restore session summary from per-turn diffs**  
   *Author: aic0d3r | Merged*  
   Fixes zeroed session summary (files/additions/deletions) caused by a prior performance optimization.  
   [GitHub](https://github.com/anomalyco/opencode/pull/33444)

8. **#19038 – feat(app): open browser inside the desktop app**  
   *Author: atmikshetty | Merged*  
   Adds an in-app browser so users can view web content without leaving the desktop application.  
   [GitHub](https://github.com/anomalyco/opencode/pull/19038)

9. **#33419 – feat(opencode): configure local instruction filenames**  
   *Author: pranjalv123 | Merged*  
   Allows directory-scoped instruction files like `REVIEW.md` alongside `AGENT.md`, closable to #32069.  
   [GitHub](https://github.com/anomalyco/opencode/pull/33419)

10. **#33284 – fix(ui): restore markdown heading hierarchy**  
    *Author: akinshaywai | Merged*  
    Fixes all heading levels (h1–h6) being rendered at 14px by restoring proper CSS font-size rules.  
    [GitHub](https://github.com/anomalyco/opencode/pull/33284)

## Feature Request Trends

- **Model auto-discovery** (#6231, #18011): Users strongly want OpenCode to automatically detect and list models from OpenAI-compatible local providers. This is the single most-requested feature (185 👍).
- **Plan/Build mode persistence** (#37970, #38364): The removal of the Plan/Build toggle in v1.18.0 disrupted workflows. Multiple requests to restore clear planning vs. execution modes.
- **Token usage transparency** (#38344, #38398): Users want per-turn token accounting, especially to debug cost explosion in long agentic sessions with OpenAI models on Bedrock.
- **Audio/video media support** (#22260): Agents should be able to inspect local media files via the read tool, attaching them as model-native media.
- **Sub-session lifecycle management** (#37314): Aborted parent sessions leave orphaned child sessions running indefinitely — users want automatic cleanup.

## Developer Pain Points

- **OpenCode Go subscription outage** (5+ issues, 40+ comments): The "401 Request blocked by upstream provider" error on Go subscriptions is today's top crisis, affecting users across Windows, macOS, multiple apps, and Hermes. No fix announced yet.
- **CPU waste during rate-limit backoff** (#19466): Waiting on API limits consumes ~50% CPU on high-end processors — an unnecessary resource drain.
- **Incomplete model discovery** (#18011, #6231): LM Studio and other local providers show incomplete model lists, forcing manual configuration that breaks when models change.
- **Remote VSCode clipboard breakage** (#26459): Web-based VSCode environments (Codespaces, code-server) show fake "copied" notifications without actual clipboard data, blocking copy-paste workflows.
- **Infinite loops post-tool-call** (#26220): OpenCode becomes unresponsive after completing tool calls, requiring process kill and losing session state.
- **Broken tool/permission mappings** (#16028): The `EDIT_TOOLS` constant references `"patch"` while the tool is named `"apply_patch"`, causing the edit permission to not actually cover the patch tool.

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

# Pi Community Digest — 2026-07-23

## Today's Highlights
A burst of 20+ issues and PRs landed in the last 24 hours, spanning critical provider fixes (AWS Bedrock profile handling, OpenRouter cache breakpoints), security concerns around a malicious extension (`pi-goal-x`), and long-requested infrastructure improvements (abortable retries, isolated test environments). The community also shipped native OpenRouter OAuth support and a new VS Code extension for Pi. Notably, the backlog shows strong demand for constrained sampling, MRU model switching, and better Windows terminal compatibility.

**Release**: None (no new versions today; latest remains v0.81.1)

## Hot Issues (10 Picks)

1. **#6768 – Compaction using Copilot Enterprise not possible** [OPEN]  
   *[Link](https://github.com/earendil-works/pi/issues/6768)*  
   Context compaction fails with HTTP 421 on Copilot Enterprise, affecting both OpenAI and Anthropic providers. 8 upvotes indicate this hits many enterprise users.

2. **#6922 – Default model cannot be a llama.cpp model** [OPEN]  
   *[Link](https://github.com/earendil-works/pi/issues/6922)*  
   Setting `defaultProvider: “llama.cpp”` shows “No models available” on startup. A significant blocker for self-hosted users, with 7 upvotes.

3. **#6686 – Pi automatically logs out of GitHub** [CLOSED, no-action]  
   *[Link](https://github.com/earendil-works/pi/issues/6686)*  
   A recurring issue (reopened from #2725). Users report spontaneous OAuth invalidation across devices—appears linked to Copilot Plugin vs OAuth token handling (see #6970).

4. **#6476 – Regression: httpIdleTimeoutMs no longer respected (v0.80.6)** [CLOSED]  
   *[Link](https://github.com/earendil-works/pi/issues/6476)*  
   Self-hosted vLLM users hit hard timeouts despite large `httpIdleTimeoutMs` settings. Downgrading to v0.80.3 restores behavior. High community engagement (12 comments).

5. **#6911 – OpenAI SDK retries sleep full Retry-After (days) and Escape cannot abort** [CLOSED]  
   *[Link](https://github.com/earendil-works/pi/issues/6911)*  
   When the provider returns a `Retry-After` header of days, the SDK sleeps that long without respecting AbortSignal—effectively freezing Pi. PR #6980 fixes this.

6. **#6972 – Package Report: pi-goal-x (malicious/unsafe behavior)** [CLOSED]  
   *[Link](https://github.com/earendil-works/pi/issues/6972)*  
   This extension bleeds state across terminal sessions. Community reported as malicious; warrants immediate review for sandboxing.

7. **#6940 – OpenRouter cache breakpoint stops before tool results** [CLOSED]  
   *[Link](https://github.com/earendil-works/pi/issues/6940)*  
   During consecutive tool-only turns, `cacheRead` stalls while uncached input grows, negating caching benefits. Affects Anthropic models via OpenRouter.

8. **#6982 – MRU model switching** [CLOSED]  
   *[Link](https://github.com/earendil-works/pi/issues/6982)*  
   Users want `Ctrl+P`/`Ctrl+Shift+P` to cycle most-recently-used models instead of alphabetical order. A UX quality-of-life request.

9. **#6210 – /scoped-models cannot select model ids containing brackets** [OPEN, inprogress]  
   *[Link](https://github.com/earendil-works/pi/issues/6210)*  
   Custom model IDs like `custom/bracketed-model[1m]` fail due to bracket parsing in selectors. Affects advanced local setups.

10. **#6957 – aws-bedrock provider ignores profile when AWS_* env vars present** [CLOSED]  
    *[Link](https://github.com/earendil-works/pi/issues/6957)*  
    The Bedrock provider falls back to `process.env` before checking the configured profile, causing authentication mismatches.

## Key PR Progress (10 Picks)

1. **#6341 – feat(ai): support constrained sampling** [OPEN, to-discuss]  
   *[Link](https://github.com/earendil-works/pi/pull/6341)*  
   Adds `constrainedSampling` config for tools, enabling provider-side JSON-schema constrained generation. Could reduce tool call failures.

2. **#6980 – fix(ai): make provider retries abortable** [OPEN]  
   *[Link](https://github.com/earendil-works/pi/pull/6980)*  
   Replaces OpenAI/Anthropic SDK inner retries with a common helper that respects AbortSignal and caps `Retry-After` delay. Fixes #6911.

3. **#6984 – feat(ai): honor compat.forceAdaptiveThinking in bedrock-converse-stream** [CLOSED]  
   *[Link](https://github.com/earendil-works/pi/pull/6984)*  
   Allows forced adaptive thinking wire format for Claude models not in the hardcoded list. Direct fix for sonnet-5 ValidationException.

4. **#6987 – fix(tui): align grapheme widths with terminal cells** [OPEN]  
   *[Link](https://github.com/earendil-works/pi/pull/6987)*  
   Addresses long-standing terminal rendering issues for CJK and emoji characters. The author notes this is a notoriously hard problem.

5. **#6927 – Add native OpenRouter OAuth support** [CLOSED]  
   *[Link](https://github.com/earendil-works/pi/pull/6927)*  
   Implements PKCE-based OAuth flow for OpenRouter, allowing Pi users to authenticate without API keys. Works with text and image providers.

6. **#6967 – feat(coding-agent): expose session metadata to bash tools** [CLOSED]  
   *[Link](https://github.com/earendil-works/pi/pull/6967)*  
   Passes session ID, provider, model, and reasoning level as environment variables to bash tool subprocesses. Enables context-aware scripts.

7. **#6965 – fix: isolate test environment** [OPEN, inprogress]  
   *[Link](https://github.com/earendil-works/pi/pull/6965)*  
   Wraps test suite in explicit allowlist environment with isolated home, tmp, Git, npm, and XDG state. Key for CI reliability.

8. **#6981 – Add restart functionality to TicTacToeComponent** [CLOSED]  
   *[Link](https://github.com/earendil-works/pi/pull/6981)*  
   Makes `R` key restart the game immediately instead of closing TUI. A small but community-noticed UX fix.

9. **#6881 – feat(ai): use provider-reported cost when responses include it** [OPEN, inprogress]  
   *[Link](https://github.com/earendil-works/pi/pull/6881)*  
   Falls back to catalog rates only when provider doesn’t report cost. Improves accuracy for OpenAI, Vercel AI Gateway, and AWS Bedrock.

10. **#6971 – feat(coding-agent): emit bash_execution_update events** [OPEN]  
    *[Link](https://github.com/earendil-works/pi/pull/6971)*  
    Adds event stream for parallel bash execution monitoring. Designed for Emacs integration (pimacs.el) but extensible.

## Feature Request Trends

1. **Model Selection & Switching** — Multiple requests for MRU model cycling (#6982), scoped model ID parsing improvements (#6210), and default model fallback for llama.cpp (#6922). Users want faster, smarter model switching.

2. **Provider Flexibility** — Strong demand for constrained sampling (#6341), native OAuth flows (#6927), and adaptivity overrides (#6984, #6986). The community wants Pi to work seamlessly with any provider’s quirks.

3. **Extension Ecosystem** — Requests for VS Code integration (#6985), Emacs event streams (#6971), and sandboxing for extension isolation (#6972). The extension marketplace is growing, so safety and compatibility are rising concerns.

4. **Terminal Compatibility** — Grapheme width fixes (#6987), Windows ConPTY handling (#6973), and Ctrl+G external editor speed (#6774, #6903). Cross-platform polish remains a top community ask.

5. **Session & State Hygiene** — Temp session cleanup (#6924), crash log placement (#6652), and test environment isolation (#6965). Users value predictable file system behavior.

## Developer Pain Points

- **Automatic logout / OAuth invalidation** (#6686, #6970) — The most commented issue this period. Users on multiple devices lose auth without clear cause. Community investigation points to Copilot Plugin endpoint conflicts.

- **Non-abortable SDK retries** (#6911) — A day-long `Retry-After` header can freeze Pi indefinitely. Workaround: disable `retry.provider.maxRetries`. PR #6980 is the community fix.

- **Configuration bleed** (#6972) — The `pi-goal-x` extension leaks State across terminal sessions, raising security concerns. Extension sandboxing is urgently needed.

- **Windows terminal edge cases** (#6619, #6973) — Extension path display and ConPTY keyboard handling are broken for Windows users. The Electron TUI has platform-specific gaps.

- **Provider profile vs env var priority** (#6957) — AWS Bedrock users can’t override `AWS_*` env vars with a configured profile. A classic configuration layering issue.

- **Cache breakpoint stagnation** (#6940) — OpenRouter users pay for uncached tokens even though prompt is virtually identical. A provider-specific integration bug that erodes cost savings.

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code Community Digest — 2026-07-23

*Technical analysis by AI developer tools specialist.*

---

## 1. Today's Highlights

The project released **v0.20.0-preview.0**, a significant milestone, though release notes only include a single telemetry test fix. The **core test suite is red on `main`** (Issue #7537), blocking all PR CI checks, with a targeted fix already submitted in PR #7540. On the security front, **credential exposure** and **update-check reliability** are dominating developer attention, with multiple PRs submitted to fix version-manager npm shims and sanitize subprocess environments.

---

## 2. Releases

### v0.20.0-preview.0
- **What's Changed:** Added test coverage for daemon metrics initialization ordering and documented `metricReader` asymmetry (PR #7456).
- **Full Changelog:** [Link](https://github.com/QwenLM/qwen-code/compare/v0.19.0...v0.20.0-preview.0) *(placeholder URL)*

### v0.20.0-nightly.20260722.b98306b7e
- Same telemetry fix as the preview; nightly build of `main`.

### v0.0.0-benchmark-poc.20260722.1
- **Not a product release.** Prerelease to validate GitHub Actions → ECS benchmark → GitHub result publication pipeline.

---

## 3. Hot Issues (Top 10)

| # | Issue | Comments | Why It Matters |
|---|-------|----------|----------------|
| #7284 | **bug(core): side-query forces `enable_thinking=false`, breaking TokenPlan endpoints** | 5 | A `runSideQuery` bug causes 400 errors on providers that require thinking enabled. Affects `web_fetch`, classifiers, and other internal tools. [Link](https://github.com/QwenLM/qwen-code/issues/7284) |
| #7316 | **Bug: OpenAI toolCall behavior breaks `subAgent` with empty string for optional `working_dir`** | 5 | OpenAI-compatible models send empty strings for missing optional parameters, causing `subagent` to fail. Blocks OpenAI users from using subagents. [Link](https://github.com/QwenLM/qwen-code/issues/7316) |
| #7306 | **Harden tool-output budgeting, observability, and artifact lifecycle** | 4 | Phase 1 correctness merged (#7323, #7470), but the proposal outlines deeper work on budgeting and lifecycle tracking. [Link](https://github.com/QwenLM/qwen-code/issues/7306) |
| #7449 | **Proposal: enterprise external-memory integration profile** | 4 | A documentation-first proposal for provider-neutral external memory. Could be a major enterprise feature. [Link](https://github.com/QwenLM/qwen-code/issues/7449) |
| #7404 | **Startup version-check timeout too short when loading long sessions** | 4 | Critical UX bug: loading a long session almost guarantees the version check times out, leaving users stuck. [Link](https://github.com/QwenLM/qwen-code/issues/7404) |
| #7287 | **Auto-memory MEMORY.md loaded into system prompt but not in FileReadCache** | 3 | `write_file` always rejects the first update because the file isn't registered in the read cache. A subtle but frustrating cognitive-load bug. [Link](https://github.com/QwenLM/qwen-code/issues/7287) |
| #7537 | **Core test suite is red on `main` — fork dispatch test never sees `registry.complete`** | 2 | **CI-breaking.** Every open PR's Ubuntu test fails regardless of its contents. PR #7540 is the proposed fix. [Link](https://github.com/QwenLM/qwen-code/issues/7537) |
| #7489 | **VS Code Companion: file picker inserts `@filename` but image not attached** | 3 | Image attachments in VS Code extension don't actually send the image to the model. [Link](https://github.com/QwenLM/qwen-code/issues/7489) |
| #7485 | **TUI: large blank area between last message and input prompt after resume** | 2 | A visual rendering regression after session resume, annoying for daily users. [Link](https://github.com/QwenLM/qwen-code/issues/7485) |
| #7440 | **`web_fetch` tool completely unusable — side-query `enable_thinking` error** | 2 | Duplicate report of #7284, indicating high user impact and frustration with `web_fetch`. [Link](https://github.com/QwenLM/qwen-code/issues/7440) |

---

## 4. Key PR Progress (Top 10)

| # | PR | Status | Feature / Fix |
|---|-----|--------|---------------|
| #7540 | [test(core): stub resident-agent methods in agent test registry](https://github.com/QwenLM/qwen-code/pull/7540) | **CLOSED** | Fixes the red CI on `main` by stubbing missing registry methods. Critical for unblocking all PRs. |
| #7548 | [fix(sdk-python): validate `max_tool_calls` and `max_subagent_depth` as integers](https://github.com/QwenLM/qwen-code/pull/7548) | OPEN | Applies integer-type validation to prevent bool/non-integer inputs; improves SDK robustness. |
| #7531 | [fix(core): close force-flag and checkout gaps in AUTO destructive-git guard](https://github.com/QwenLM/qwen-code/pull/7531) | OPEN | Blocks `git clean` and `git checkout` in all spellings; fixes an incomplete security guard. |
| #7527 | [fix(core): strip daemon secrets from hook and tool-discovery child env](https://github.com/QwenLM/qwen-code/pull/7527) | OPEN | Extends credential sanitization to hooks and tool-discovery — follows up on #7256. |
| #7545 | [fix(cli): stop treating version-manager npm shims as npm-cli.js](https://github.com/QwenLM/qwen-code/pull/7545) | OPEN | Fixes `update` check for users of `mise`, `fnm`, `nvm`, etc. by validating npm path is a JS file. |
| #7547 | [fix(core): stringify const-derived enums in toOpenAPI30](https://github.com/QwenLM/qwen-code/pull/7547) | OPEN | One-line fix for enum conversion in OpenAPI 3.0; ensures const enums follow the string-enum rule. |
| #7544 | [fix(cli): resolve npm wrappers to npm-cli.js](https://github.com/QwenLM/qwen-code/pull/7544) | OPEN | Alternative approach to #7545 for the same npm-shim problem. |
| #7541 | [fix(core): preserve disabled reasoning effort](https://github.com/QwenLM/qwen-code/pull/7541) | OPEN | Preserves explicit `reasoning_effort: "none"` when side-query disables thinking — fix for #7284 family. |
| #7534 | [fix(core): retry requests when providers require thinking](https://github.com/QwenLM/qwen-code/pull/7534) | OPEN | Retries OpenAI requests once when provider demands thinking enabled — alternative fix for the `enable_thinking` bug. |
| #7542 | [feat(cli): add version upgrade notices](https://github.com/QwenLM/qwen-code/pull/7542) | OPEN | New "What's New" startup notice for release highlights — lightweight, user-facing UX improvement. |

---

## 5. Feature Request Trends

1. **Enterprise external-memory integration** — Proposal #7449 for a provider-neutral enterprise memory profile. Documentation-first, likely to shape Qwen Code's enterprise offering.
2. **Visualizing subagent execution** — Request #7525 to link Todo plan nodes to live subagent executions with DAG visualization. Part of the broader `multi-agent` roadmap.
3. **Web Shell context and workspace selectors** — Multiple requests (#6701, #6700) for "Start In" and workspace dropdowns in the Web Shell composer toolbar. High community demand.
4. **Automatic fallback for `web_fetch` failures** — Feature request #7298 proposes curling + local parsing when `web_fetch` fails due to anti-scraping or provider bugs.
5. **Git mode selector in Web Shell** — PR #7471 implements a unified git mode selector (current branch / new branch / detached) for session creation.

---

## 6. Developer Pain Points

- **Update-check reliability** — Two distinct issues (#7515, #7543) report that `qwen update` and `/update` fail for users of version managers (`mise`, `fnm`, `nvm`). The root cause is `getNpmCliPath` resolving to shell wrappers instead of `npm-cli.js`. Two competing PRs (#7545, #7544) address this.
- **Credential exposure in subprocesses** — Issue #6601 (closed, but fix being extended) reports that shell subprocesses inherit `QWEN_SERVER_TOKEN` and API keys. PR #7527 extends the sanitization to hooks and tool-discovery.
- **`web_fetch` broken for many users** — Issues #7284, #7440, #7298 all report that `web_fetch` fails because of the `enable_thinking=false` side-query bug. Two fix approaches (#7534, #7541) are in review.
- **CI red on `main`** — Issue #7537 blocks all PR test runs. The fix (#7540) is merged quickly, but this is a recurring pain (see also #7516, #7445 for prior main CI failures).
- **TUI rendering regressions** — Flickering (#6137), blank areas after resume (#7485), and memory access out-of-bounds (#6820) indicate ongoing rendering stability issues, especially on Linux terminals.

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

# DeepSeek TUI Community Digest — 2026-07-23

## Today's Highlights
The **v0.9.1 release is in its final shipping sprint**, with maintainers closing 16+ blocking issues and merging 12+ PRs in the last 24 hours alone. A security gate (Issue [#4713](https://github.com/Hmbown/CodeWhale/issues/4713)) now blocks the final tag pending resolution of 17 open Dependabot alerts. The **unified `/skills` manager** ([#4651](https://github.com/Hmbown/CodeWhale/issues/4651)) and a bundled default skill pack ([#4691](https://github.com/Hmbown/CodeWhale/issues/4691)) both landed, while several critical bugs around sandbox permissions, installer PATH corruption, and sub-agent worktree behavior were reported.

---

## Releases
No new releases published in the last 24 hours. The team is actively preparing **v0.9.1** with a dedicated security gate.

---

## Hot Issues

1. **[#2870](https://github.com/Hmbown/CodeWhale/issues/2870) — EPIC: staged command-boundary refactor (17 comments)**  
   *Status: OPEN · Updated 2026-07-22*  
   The longest-running refactor (opened June 6) tracks smaller mergeable layers for command ownership and routing. Community interest is high but momentum has slowed — this is a deep architectural change.

2. **[#4227](https://github.com/Hmbown/CodeWhale/issues/4227) — feat: help JayBeest map the CodeWhale tsunami (12 comments)**  
   *Status: OPEN · Updated 2026-07-22*  
   A skill/workflow for contributors to auto-setup and rebuild their dev environment against the latest `main`. Highly practical given the project’s 10+ PR/day velocity.

3. **[#4085](https://github.com/Hmbown/CodeWhale/issues/4085) — Cannot read/write files under Dropbox on macOS (4 comments)**  
   *Status: OPEN · Updated 2026-07-22*  
   Confirmed regression on macOS 12+ File Provider paths. Ad-hoc signed binary with zero entitlements, so it’s not a sandbox issue — the tool layer itself blocks access. Affects users with cloud storage workflows.

4. **[#4684](https://github.com/Hmbown/CodeWhale/issues/4684) — `danger-full-access` does not disable tools-layer workspace boundary (2 comments)**  
   *Status: OPEN · Updated 2026-07-22*  
   A sandbox mode that fails to deliver on its promise. Even with OS-level sandboxing disabled, `read_file`/`grep_files` still enforce workspace boundaries, breaking global skill access.

5. **[#4685](https://github.com/Hmbown/CodeWhale/issues/4685) — Windows installer overwrites user PATH (1 comment)**  
   *Status: OPEN · Updated 2026-07-22*  
   Installer replaces the user PATH instead of appending, destructive to existing toolchains. High-severity for Windows adopters.

6. **[#4683](https://github.com/Hmbown/CodeWhale/issues/4683) — Wrong DeepSeek completions URL (1 comment)**  
   *Status: OPEN · Updated 2026-07-22*  
   Flaky requests to `https://api.deepseek.com/v1/chat/completions` failing with network errors. User reports it appears "after long time asks." Possible rate-limiting or connection issue.

7. **[#4681](https://github.com/Hmbown/CodeWhale/issues/4681) — `<turn_meta>` blocks visible after reopening a session (1 comment)**  
   *Status: OPEN · Updated 2026-07-22*  
   Metadata blocks that are normally hidden appear raw in the UI after session restore. A clean UX regression.

8. **[#4682](https://github.com/Hmbown/CodeWhale/issues/4682) — Custom provider name causes launch failure (1 comment)**  
   *Status: OPEN · Updated 2026-07-22*  
   Setting a custom model provider name in `/provider` leads to immediate crash on next launch. Affects anyone using non-standard backends.

9. **[#4705](https://github.com/Hmbown/CodeWhale/issues/4705) — Minimize tool results and sub-agent payloads (0 comments)**  
   *Status: OPEN · Updated 2026-07-22*  
   Model-visible results include UI metadata and verbose scaffolding. Proposed work: trim payloads for context efficiency.

10. **[#4713](https://github.com/Hmbown/CodeWhale/issues/4713) — v0.9.1 security gate: deep scan and dependency alert disposition (0 comments)**  
    *Status: OPEN · Updated 2026-07-22*  
    **Release blocker.** 17 open Dependabot alerts (7 high, 10 moderate) in npm dependencies (axios, braces, etc.) must be dispositioned before tagging.

---

## Key PR Progress

1. **[#4714](https://github.com/Hmbown/CodeWhale/pull/4714) — chore(deps): patch npm lockfiles for Dependabot alerts**  
   *Status: OPEN*  
   Applies `npm audit fix --package-lock-only` to resolve all 17 alerts across feishu-bridge and VSCode extension workspaces. Critical for the v0.9.1 security gate.

2. **[#4711](https://github.com/Hmbown/CodeWhale/pull/4711) — fix(tui): focus v0.9.1 chrome on todos and agents**  
   *Status: CLOSED*  
   Replaces generic Work chrome with a resizable To-do + Sub-agent bar. Includes draggable dividers and theme-native permission rails.

3. **[#4695](https://github.com/Hmbown/CodeWhale/pull/4695) — feat(skills): default CodeWhale skill pack (bundled v5)**  
   *Status: CLOSED*  
   Ships the first-party end-user skill pack: interview, plan, implement, debug, test, review, security-review, simplify, verify, research, free-form. Comparable to Kimi Code/Devin CLI/Claude Code workflows.

4. **[#4694](https://github.com/Hmbown/CodeWhale/pull/4694) — fix(kimi): fail closed on K3 model-ID cross-pairings**  
   *Status: CLOSED*  
   Treats base URL + model ID as one route identity; rejects documented cross-pairings between `kimi-k3`/`k3` and `api.kimi.com`/`api.moonshot.ai`.

5. **[#4693](https://github.com/Hmbown/CodeWhale/pull/4693) — fix(tui): Work summary lifecycle and top-area hierarchy**  
   *Status: CLOSED*  
   Three coordinated fixes: recent Work summaries auto-expire after 4s; actionable titles are elevated; top-area hierarchy is cleaned up.

6. **[#4679](https://github.com/Hmbown/CodeWhale/pull/4679) — feat(skills): unified /skills manager with audit and owned mutations**  
   *Status: CLOSED*  
   One `/skills` command to discover, inspect, audit, install, remove, and trust skills across CodeWhale-owned and compatible roots.

7. **[#4675](https://github.com/Hmbown/CodeWhale/pull/4675) — Integrate CodeWhale v0.9.1 runtime and release surface**  
   *Status: CLOSED*  
   The main integration PR: runtime simplification, empty-Work fix, final TUI color grammar (cool mode colors, warm permission echoes), and release surface.

8. **[#4673](https://github.com/Hmbown/CodeWhale/pull/4673) — fix(shell): default no-cwd shell commands to context.workspace**  
   *Status: CLOSED*  
   Sub-agents in isolated worktrees now correctly default to their own workspace directory instead of the parent checkout.

9. **[#4686](https://github.com/Hmbown/CodeWhale/pull/4686) — feat(minimax): add China/Token Plan provider routes**  
   *Status: OPEN*  
   Adds `minimax-cn` and `minimax-anthropic-cn` identifiers for `api.minimaxi.com`. Expands compatibility for Chinese-market users.

10. **[#4046](https://github.com/Hmbown/CodeWhale/pull/4046) — Layer 5.1: User command registry and loading boundary**  
    *Status: CLOSED*  
    Verifies that the user-command registry already satisfies all acceptance criteria for user-defined Markdown/frontmatter commands — no production code changes needed, just test coverage.

---

## Feature Request Trends

- **Unified skill management**: Multiple issues target a single `/skills` surface replacing fragmented install/update/trust flows. Landed in [#4679](https://github.com/Hmbown/CodeWhale/pull/4679).
- **Hooks-based lifecycle for tool operations**: [#1917](https://github.com/Hmbown/CodeWhale/issues/1917) proposes PreToolUse/PostToolUse hooks enabling Cancel (with rollback), Pause, and Resume across all action types.
- **Context efficiency improvements**: A cluster of v0.9.2 issues ([#4705](https://github.com/Hmbown/CodeWhale/issues/4705), [#4709](https://github.com/Hmbown/CodeWhale/issues/4709), [#4707](https://github.com/Hmbown/CodeWhale/issues/4707)) targets reducing token waste from deduplicated project context, verbose tool results, and lack of cross-model ablation testing.
- **Sub-agent worktree isolation**: [#4674](https://github.com/Hmbown/CodeWhale/issues/4674) and [#4673](https://github.com/Hmbown/CodeWhale/pull/4673) highlight demand for proper sub-agent workspace boundaries.

---

## Developer Pain Points

- **macOS Dropbox paths unusable** ([#4085](https://github.com/Hmbown/CodeWhale/issues/4085)): The tool layer fails on standard cloud storage locations with no sandbox excuse.
- **`danger-full-access` is misleading** ([#4684](https://github.com/Hmbown/CodeWhale/issues/4684)): The sandbox mode name implies full file system access but tools-layer boundary checks remain active.
- **Windows PATH corruption** ([#4685](https://github.com/Hmbown/CodeWhale/issues/4685)): The installer replaces rather than appends to PATH, destructive for all other tools.
- **Custom provider crashes on restart** ([#4682](https://github.com/Hmbown/CodeWhale/issues/4682)): A simple `/provider` configuration change makes the app unbootable.
- **Flaky DeepSeek API connectivity** ([#4683](https://github.com/Hmbown/CodeWhale/issues/4683)): Requests to the default DeepSeek endpoint fail intermittently, especially on long-running sessions.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/kky-wollu/agents-radar).*