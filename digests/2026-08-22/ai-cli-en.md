# AI CLI Tools Community Digest 2026-08-22

> Generated: 2026-08-21 22:29 UTC | Tools covered: 9

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

# Cross-Tool Comparison Report — AI CLI Developer Tools
**Date:** 2026-08-22

---

## 1. Ecosystem Overview

The AI CLI tool landscape is rapidly consolidating around reliability and trust as core differentiators. While the tools differentiate on model ecosystems (Anthropic, OpenAI, Google, Qwen, DeepSeek, and multi-provider), they all face a common set of challenges: safety-filter false positives, silent session failures, agent lifecycle management, and long-session memory stability. The dominant theme is a shift from "what can these tools do" to "can I trust them to do it without burning money, hanging silently, or blocking legitimate work." Security hardening (sandboxing, permission granularity, audit trails) and multi-agent orchestration (subagent reliability, handoffs, parallelism) are the two highest-investment areas across all codebases.

---

## 2. Activity Comparison

| Tool | Issues Filed (24h) | PRs Merged/Active (24h) | Release Status | Release Type |
|------|-------------------|------------------------|----------------|--------------|
| **Claude Code** | ~10 notable (mostly AUP false positives) | 0 | v2.1.239 (stable) | Stable |
| **OpenAI Codex** | 10+ (8 Windows Remote wave) | 20 merged | 5 alpha releases | Alpha (rapid) |
| **Gemini CLI** | ~10 tracked | 10+ (8 PR-gen infra) | v0.56.0-nightly | Nightly |
| **Copilot CLI** | 10+ | 0 | v1.0.81-7 (prerelease) | Prerelease |
| **Kimi Code** | 1 critical bug | 1 docs PR | None | — |
| **OpenCode** | 10 tracked | 10+ | v1.18.21 (stable) | Stable patches |
| **Pi** | 17+ (TUI customization cluster) | 6+ merged | None | — |
| **Qwen Code** | 10+ | 10+ | v0.21.14-nightly | Nightly |
| **DeepSeek TUI** | 10+ | 10+ | None | Refactor phase |

**Observation:** OpenAI Codex shows the highest PR velocity (20 merged), while Claude Code's activity is entirely issue-driven (safety-filter fallout). Pi and DeepSeek TUI are in active architectural refactoring phases.

---

## 3. Shared Feature Directions

The following requirements surfaced across multiple communities this week:

| Direction | Tools | Specific Needs |
|-----------|-------|----------------|
| **Session recovery & persistence** | Copilot CLI, OpenCode, Pi, Qwen Code, DeepSeek TUI | Crash recovery, restore archived sessions, resume after restart, daemon-scoped session management |
| **Multi-model / BYOK flexibility** | Copilot CLI, Pi, OpenCode | In-session model switching, per-model settings (compaction, reasoning), multi-provider without restart |
| **Agent lifecycle & subagent reliability** | Gemini CLI, Kimi, Qwen Code, DeepSeek TUI | Kill/stop enforcement, no false GOAL success, watchdog timeouts, subagent crash recovery |
| **Cost transparency & control** | OpenAI Codex, OpenCode, Pi, Gemini CLI | Usage APIs, cache controls, per-model cost display, unified cost tracking, avoid hidden drains |
| **Safety filter context-awareness** | Claude Code, Qwen Code | Distinguish defensive/offensive, respect authorized work, avoid sentiment-based blocking |
| **MCP ecosystem stability** | Copilot CLI, OpenCode, Pi, Qwen Code | BigInt handling, lazy tool definitions, connection reliability, custom result types |
| **Granular permission/sandbox controls** | OpenAI Codex, Gemini CLI, Copilot CLI, Qwen Code | Per-origin browser access, per-app policies, disable-able sandbox, allowlist short-circuits |
| **TUI customization** | Pi, Qwen Code | Per-block expand/collapse, sticky headers, scroll sensitivity, detail mode defaults |

---

## 4. Differentiation Analysis

| Tool | Primary Focus | Target User | Technical Approach |
|------|--------------|-------------|-------------------|
| **Claude Code** | Safety & enterprise compliance | Enterprise developers | Heavy server-side safety filtering (AUP), data-residency support, fullscreen renderer |
| **OpenAI Codex** | Desktop automation & remote pairing | Prosumer + enterprise | Rust-based, Guardian security reviews, computer-use automation, Windows Remote |
| **Gemini CLI** | Autonomous agent orchestration | Technical power users | Deep sub-agent system, skills, Auto Memory, zero-dependency sandboxing proposals |
| **Copilot CLI** | GitHub-native workflow | GitHub ecosystem devs | ACP (Agent Client Protocol), tight GitHub integration, BYOK model support |
| **Kimi Code** | LLM lifecycle correctness | Moonshot ecosystem users | Plugin system, subagent quota management, docs-driven security clarity |
| **OpenCode** | Multi-provider flexibility | Proxy/provider-heavy users | Provider-agnostic core, streaming/fallback handling, MCP tool bloat mitigations |
| **Pi** | Terminal UX & customization | Terminal purists | SDK-level TUI customization, multi-terminal protocol support, per-model compaction |
| **Qwen Code** | CI/CD integration & review loops | Qwen ecosystem + enterprise CI | Automated review loops, autofix/takeover pipeline, worktree-based code execution |
| **DeepSeek TUI** | Unattended/supervised operation | Automation & ops engineers | Control sockets, lifecycle outboxes, `/relaunch` self-exec, crate decomposition |

---

## 5. Community Momentum & Maturity

**Most Active / Highest Velocity:**
- **OpenAI Codex** — 20 PRs merged in 24h, 5 alpha releases, aggressive hardening across sandboxing, Guardian reviews, and remote connectivity. Highest feature velocity.
- **Pi** — 17+ new issues (TUI customization cluster), 6+ merged PRs, active architectural improvements. Strong organic community engagement.
- **Gemini CLI** — 10+ PRs dedicated to PR-generation infrastructure, suggesting major internal investment in autonomous bug-fixing.

**Rapid Iteration / Prerelease Churn:**
- **Copilot CLI** — v1.0.81 prerelease shipped session recovery, but introduced regressions (memory writer, TUI freeze). Rapid iteration with visible instability.
- **Qwen Code** — Nightly releases with heavy CI/CD and review-loop hardening. Mature infrastructure, benchmark-verified.

**Stable but Issue-Heavy:**
- **Claude Code** — No PRs in 24h; community is entirely occupied with AUP false-positive fallout. Trust erosion risk is high despite stable release cadence.

**Early/Refactoring Phase:**
- **DeepSeek TUI** — In active architectural refactor (EPIC-005) with a clear vision for supervised ops. Community is engaged but small.
- **Kimi Code** — Low activity (1 critical bug, 1 docs PR). Minimal community engagement; likely a smaller user base.

---

## 6. Trend Signals

**1. Safety filters are creating trust crises.** Claude Code's AUP false positives (90% of issues) with session-halting severity is the single biggest cautionary tale. Signal: safety systems that block *legitimate defensive work* are worse than no filter — they actively destroy user trust and will drive users to competitors with less aggressive filtering.

**2. "Silent failure" is the new #1 enemy.** Across every tool: OpenCode (#41469 empty responses), DeepSeek TUI (#5528 silent workflow failures), Kimi (#2615 subagents calling LLM after kill), Pi (#6879 compaction fails silently). Users don't mind errors — they mind *not knowing*. Expect observability to become a purchase criterion.

**3. Cost visibility is a competitive differentiator.** Codex's polling re-entry consuming 19.8% of tokens, OpenCode's cost-tracking RFC, Pi's cache_control 2.5x cost penalty — users are increasingly cost-auditing their AI CLI usage. Tools that provide transparent usage APIs and cache controls will win cost-sensitive teams.

**4. Long-session reliability is THE trust factor.** Sessions that die at 30 minutes (#2644), compaction that never triggers (#6879), checkpointing hangs (#2862), session recovery after crashes (Copilot CLI v1.0.81-7) — the industry consensus is clear: an agentic tool that can't reliably sustain multi-hour sessions is not production-viable.

**5. Multi-agent orchestration is the next frontier.** Subagent crashes, handoff stalls, GOAL false-success (Gemini #22323), parallelism freezes (Copilot #4533) — every tool is struggling with multi-agent reliability. This is the hardest unsolved problem and the clearest signal of where the industry is heading: workflows that require orchestrating multiple agents with different roles.

**6. Security hardening is accelerating.** Guardian reviews (Codex), sandbox isolation (Gemini #28935), permission granularity (Codex PR #40024), MCP stop hooks (#40009), content-filter isolation (Qwen #9566) — security infrastructure is being rebuilt from the ground up, driven by both compliance pressure and the reality of autonomous code execution.

**7. BYOK and multi-model flexibility is table stakes.** Copilot CLI's most-upvoted requests (#3282, #3709) and Pi's per-model settings (#8133) signal that users want choice and control over which models power their workflows — and want to switch without restarting.

---

*Report generated from community digests for 2026-08-22. Data reflects a single 24-hour window and may not capture longer-term trends.*

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills Community Highlights Report
**Data Snapshot:** 2026-08-22 | **Source:** github.com/anthropics/skills

---

## 1. Top Skills Ranking

The following Skills have generated the most community discussion and attention via Pull Requests:

**① skill-creator — Evaluation Pipeline Fixes**
- **PRs:** #1298 (MartinCajiao), #1099 (joshuawowk), #1050 (gstreet-ops), #539 (Lubrsy706)
- **Status:** Open (multiple related PRs)
- **Functionality:** The skill-creator meta-skill includes `run_eval.py`, `run_loop.py`, and `improve_description.py` scripts that measure skill description quality (precision/recall) and auto-optimize descriptions. These PRs fix systemic bugs: the eval always reports `recall=0%` because Claude never triggers the test skill in subprocess mode (#1298), Windows subprocess pipe reading crashes (#1099, #1050), and YAML frontmatter parsing fails on unquoted descriptions with colons (#539).
- **Discussion Highlights:** This is the single most-worked-on area — 4 independent PRs across 3 months. The consensus is that the evaluation loop has been "optimizing against noise," undermining the entire skill-creation workflow. The fixes are complementary (stream handling, artifact installation, YAML validation), suggesting maintainers may merge a composite fix.
- **Links:** [#1298](https://github.com/anthropics/skills/pull/1298) · [#1099](https://github.com/anthropics/skills/pull/1099) · [#1050](https://github.com/anthropics/skills/pull/1050) · [#539](https://github.com/anthropics/skills/pull/539)

**② document-typography — Document Quality Control**
- **PR:** #514 (PGTBoos) | **Status:** Open
- **Functionality:** A skill that prevents typographic defects in AI-generated documents: orphan words (1–6 words spilling to a new line), widow paragraph headers stranded at page bottoms, and numbering misalignment. These are universal problems in Claude-generated content.
- **Discussion Highlights:** The author argues these issues affect "every document Claude generates" and that users rarely explicitly request typographic cleanup. The skill has broad applicability across docx, pdf, html, and ODT outputs.
- **Link:** [#514](https://github.com/anthropics/skills/pull/514)

**③ ODT Skill — OpenDocument Format Handling**
- **PR:** #486 (GitHubNewbie0) | **Status:** Open
- **Functionality:** Create, fill, read, and convert OpenDocument Format files (.odt, .ods, .odf). Triggers on keywords like "OpenDocument," "LibreOffice document," and "ISO standard." Includes template filling and ODT-to-HTML conversion workflows.
- **Discussion Highlights:** Fills a gap in the document-skills family — the ecosystem has docx, pdf, and pptx covered but lacks a native open-format equivalent. The PR has been open 5 months with sustained comment activity.
- **Link:** [#486](https://github.com/anthropics/skills/pull/486)

**④ frontend-design — Clarity & Actionability Overhaul**
- **PR:** #210 (justinwetch) | **Status:** Open
- **Functionality:** Revises the frontend-design skill to make instructions executable in a single conversation — specific enough to steer behavior without being prescriptive. The goal is eliminating vague guidance that Claude can't operationalize.
- **Discussion Highlights:** Representative of the broader community push toward skills that are precise, testable instructions rather than educational documents (see Issue #202's critique of skill-creator's "verbose, educational tone").
- **Link:** [#210](https://github.com/anthropics/skills/pull/210)

**⑤ testing-patterns — Full-Stack Testing Guide**
- **PR:** #723 (4444J99) | **Status:** Open
- **Functionality:** Comprehensive testing skill covering the Testing Trophy model, what-to-test vs. what-not-to-test, AAA unit test patterns, React component testing (Testing Library), and edge case identification.
- **Discussion Highlights:** Broad scope with high potential — testing is a universal developer need. The skill aims to encode the "Testing Trophy" philosophy into actionable Claude instructions.
- **Link:** [#723](https://github.com/anthropics/skills/pull/723)

**⑥ ServiceNow Platform Skill**
- **PR:** #568 (Vanka07) | **Status:** Open
- **Functionality:** A broad ServiceNow platform assistant covering ITSM, ITOM, ITAM/SAM Pro, FSM, HRSD, CSM, SPM/PPM, Vulnerability Response, Security Incident Response, CSDM, and IntegrationHub — far beyond a narrow scripting helper.
- **Discussion Highlights:** The most enterprise-focused skill in the top tier; sustained comment activity over 5 months (March → August) suggests meaningful community engagement with scope and content.
- **Link:** [#568](https://github.com/anthropics/skills/pull/568)

---

## 2. Community Demand Trends

**🔒 Security & Trust Boundary Management** (Issue #492, 43 comments) — The most-commented issue in the repository. Community members are concerned that skills distributed under the `anthropic/` namespace (via the official marketplace) may include community-authored skills that users can't distinguish from Anthropic-official ones. Demand is for namespace governance, clearer provenance labeling, and permission-scope warnings.

**📤 Organizational Skill Sharing** (Issue #228, 16 comments) — Significant demand for org-wide skill libraries: shared skill repositories, direct sharing links, and centralized management instead of manual `.skill` file downloads and Slack/Teams transfers.

**🔧 Skill-Creator Reliability** (Issue #556, 12 comments; Issue #202, 8 comments) — Two-fold demand: (a) the evaluation tooling must produce trustworthy signals (0% trigger rate is a hard blocker), and (b) the skill itself should be rewritten as operational instructions rather than developer documentation.

**🧠 Context Window Efficiency** (Issue #1487, 4 comments; Issue #189, 6 comments) — The `claude-api` skill injects ~156k tokens in a single tool call, exhausting context windows. Duplicate skills from overlapping plugins (`document-skills` vs `example-skills`) compound this. Demand is for lighter-weight skills and de-duplication.

**🌐 Platform Expansion** (Issues #29, #16 — Bedrock support; MCP exposure) — Ongoing demand for AWS Bedrock compatibility and exposing skills as MCP servers for cross-tool interoperability.

---

## 3. High-Potential Pending Skills

These active PRs are not yet merged but show strong community engagement:

| Skill | PR | Status | Notes |
|---|---|---|---|
| **skill-quality-analyzer + skill-security-analyzer** | [#83](https://github.com/anthropics/skills/pull/83) | Open since Nov 2025 | Meta-skills that evaluate skills across 5 dimensions (structure, documentation, security). Directly addresses the trust-boundary concerns in Issue #492. |
| **self-audit — Reasoning Quality Gate** (v1.3.0) | [#1367](https://github.com/anthropics/skills/pull/1367) | Open since Jun 2026 | Mechanical file verification + four-dimension reasoning audit (damage-severity prioritized). Complements Issue #1385's proposal for a three-gate pipeline. |
| **ServiceNow Platform Skill** | [#568](https://github.com/anthropics/skills/pull/568) | Open since Mar 2026 | Broad enterprise platform coverage; sustained activity for 5 months. |
| **pyxel — Retro Game Development** | [#525](https://github.com/anthropics/skills/pull/525) | Open since Mar 2026 | MCP-server-backed skill for Pyxel (Python retro game engine). Community has shown interest in MCP-integrated skills (Issue #16). |
| **SAP-RPT-1-OSS Predictor** | [#181](https://github.com/anthropics/skills/pull/181) | Open since Dec 2025 | Predictive analytics using SAP's open-source tabular foundation model (Apache 2.0), released at SAP TechEd 2025. |
| **Spec Compliance Fixes** | [#1538](https://github.com/anthropics/skills/pull/1538) | Open since Aug 2026 | Fixes two bundled skills to pass `skills-ref validate` against the Agent Skills spec — likely to be merged quickly as it enforces repository standards. |

---

## 4. Skills Ecosystem Insight

**The community's most concentrated demand is for trust and reliability: fixing the skill-creation evaluation pipeline (so generated skills actually work), establishing security/quality auditing of distributed skills (so users can trust what they install), and making skills context-window-efficient (so installed skills don't break the very sessions they're meant to enhance) — with the "skill-creator evaluation loop is broken" cluster (#1298, #1099, #1050, #539, #556) representing the single highest-urgency pain point in the ecosystem.**

---

# Claude Code Community Digest — 2026-08-22

## Today's Highlights

Claude Code shipped v2.1.239, which adds cost estimate adjustments for data-residency workspaces and extends the fullscreen renderer offer to Bedrock, Vertex, and Foundry installs. The community's attention remains concentrated on a large wave of closed false-positive safety blocks — dozens of routine sessions reportedly halted by the "Fable 5" AUP filter, many of them affecting defensive security audits and mobile UI automation work.

## Releases

**v2.1.239** — Two changes:
- Cost estimates (`/cost`, status line, `--max-budget-usd`) now reflect the 1.1× US-only-inference premium applied to data-residency workspaces.
- One-time fullscreen renderer offer now also applies on Bedrock, Vertex, Foundry, and other previously excluded setups; new installs there start in fullscreen mode.

## Hot Issues

1. **[#73126 — [Bug][cyber] Blocked decompiling own drone app to build FOSS ground-control station](https://github.com/anthropics/claude-code/issues/73126)** — A cybersecurity safety filter false positive reportedly halted a legitimate FOSS drone GCS project. Closed as a duplicate, but notable as the highest-comment-count issue in the batch and a canonical example of the "cyber kind" classification.

2. **[#73183 — [Bug][aup] Frustrated exclamation triggered block mid defensive vuln scrub](https://github.com/anthropics/claude-code/issues/73183)** — A user's own web app security review was interrupted by the AUP filter after an emotional utterance. Part of a striking pattern: simple frustration is repeatedly being misread as policy-violating behavior.

3. **[#73181 — [Bug][aup] Block fired while resuming defensive vulnerability scrub](https://github.com/anthropics/claude-code/issues/73181)** — Another session-halting false positive in the AUP category; this time the filter intervened on a defensive-hardening workflow the user explicitly initiated.

4. **[#73172 — [Bug][aup] Deploying validated trading-bot sizing upgrade flagged as AUP](https://github.com/anthropics/claude-code/issues/73172)** — A routine deployment plus UI polish work was halted by the safety filter, suggesting the false-positive issue may extend beyond security-adjacent tasks into standard development workflows.

5. **[#73171 — [Bug][aup] Blocked while auditing code integrating with internal module](https://github.com/anthropics/claude-code/issues/73171)** — The filter interrupted a post-auth-flow code audit; the user reports the block halted an authorized, routine session. Highlights the cost of the false-positive wave on trust in the tool.

6. **[#73169 — [Bug][aup] Safeguards blocked routine code audit](https://github.com/anthropics/claude-code/issues/73169)** — Represents the high-volume "general" domain false positives, where a simple code review gets flagged. Community reaction is largely frustration about the filter's inability to distinguish defensive from offensive work.

7. **[#73312 — [BUG] Claude Code loads fixed subset (10) of system CA certificates](https://github.com/anthropics/claude-code/issues/73312)** — The only non-AUP issue in the top set: a macOS networking bug where `CLAUDE_CODE_CERT_STORE` is ignored, causing `/v1/messages` requests to fail with `UNABLE_TO_GET_ISSUER_CERT`. Matters because it breaks connectivity for enterprise users with custom certificate authorities.

8. **[#73145 — [Bug][aup] ClAudit false-positive in GlassFalcon](https://github.com/anthropics/claude-code/issues/73145)** — A user-named project ("GlassFalcon") got flagged, and the report includes a specific Request ID for server-side repro. Useful for Anthropic's debugging and a data point on the filter's reach into everyday development contexts.

9. **[#73201 — [Bug][aup] Frustrated exclamation during Android adb UI automation blocked](https://github.com/anthropics/claude-code/issues/73201)** — The filter flagged tap/swipe/screencap automation flows when users expressed frustration, blocking the session. A reminder that emoji-free technical work is being caught in the crossfire of sentiment-based filtering.

10. **[#73217 — [Bug][aup] Block on fixing incorrect safe takeoff/landing commands in FOSS drone GCS](https://github.com/anthropics/claude-code/issues/73217)** — A particularly ironic case: fixing *incorrect* drone commands — a safety-improving change — was blocked by the safety filter. Strong candidate for "false positive of the week" and a clear example of over-broad filtering.

## Key PR Progress

No pull requests were updated in the last 24 hours. The repository's current activity is entirely issue-driven, centered on the AUP filter false-positive reports and the CA certificate bug.

## Feature Request Trends

There are no explicit feature requests in the current issue set. The dominant implicit request — across dozens of closed issues — is for the AUP/cyber safety filters to become context-aware enough to recognize authorized, defensive, and ordinary-development work. Users are not asking for new capabilities; they're asking for the existing ones to stop halting legitimate sessions mid-task.

## Developer Pain Points

- **AUP filter false positives are the #1 pain point.** Roughly 90% of the issues in the past 24 hours are safety-filter blocks for routine work: security audits, code reviews, UI automation, and even session resumption. One common trigger appears to be "frustrated exclamations" — the filter seems to auto-flag negative user sentiment, regardless of what the code work actually is. Another trigger is `ClAudit`-style code reviews of the user's own projects. The severity is consistently "session-halted," meaning these are not minor annoyances — they kill workflows in progress.
- **Difficulty distinguishing defensive from offensive security work.** Several blocked workflows were explicitly defensive (vulnerability scans, audit reviews, fixing drone safety commands). The filter's current model appears to over-index on keywords and sentiment, not on whether the target is the user's own property or whether the work is harm-reducing.
- **Noisy issue tracker from duplicate reports.** The rapid-fire filing of nearly identical AUP issues (many closed as duplicates) suggests users are not finding prior reports before filing — or that each instance is unique enough to warrant a new report. Either way, the pattern indicates a support and triage process that's not yet coping with the scale of the problem.
- **CA certificate handling still broken on macOS.** For enterprise users on macOS, `CLAUDE_CODE_CERT_STORE` is silently ineffective, and the client always loads only the first 10 system CAs, causing hard connectivity failures. The issue is marked with a repro and indicates the problem is not a temporary environment glitch.

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex Community Digest — 2026-08-22

## Today's Highlights

The Codex team shipped five new Rust alpha releases (0.149.0-alpha.4.1 through 0.150.0-alpha.5) with no public changelog details, while the community converged on a major **Windows Remote Control instability wave** — at least eight new issues filed in the last 24 hours report pairing/auth/session failures between Android/iOS clients and Windows hosts. On the development side, 20 PRs merged today focusing on **Guardian security reviews**, **executor plugin stop hooks**, **Amazon Bedrock setup**, and **browser/computer-use permission policies**, signaling a hardening push across sandboxing and remote connectivity.

## Releases

Five new Rust releases in the last 24 hours, all alpha and without detailed changelogs:

- **rust-v0.150.0-alpha.5** — latest; 0.150.0-alpha.5
- **rust-v0.150.0-alpha.3** — 0.150.0-alpha.3
- **rust-v0.150.0-alpha.2** — 0.150.0-alpha.2
- **rust-v0.149.0-alpha.7.1** — 0.149.0-alpha.7.1
- **rust-v0.149.0-alpha.4.1** — 0.149.0-alpha.4.1

All releases are tagged as "Release X" with no changelog body. Notably, some issues reference `codex-cli 0.149.0-alpha.4` and `0.148.0-alpha.15` as bundled CLI versions in desktop apps, suggesting these alphas are being shipped in-app ahead of public announcement.

## Hot Issues (10)

1. **[#38455 — ChatGPT desktop repeatedly spawns Computer Use workers and crashes with V8 OOM on macOS](https://github.com/openai/codex/issues/38455)** — 35 comments, 15 👍. A macOS idle crash spawning 187 `computer-use` threads leading to SIGABRT via V8 OOM.  The most-discussed issue this week, likely because it's a regression from a previously working build and impacts idle users — no user action required to trigger.

2. **[#39162 — Opening an existing conversation invalidates ChatGPT auth on macOS](https://github.com/openai/codex/issues/39162)** — 31 comments, 22 👍. A critical auth regression: simply opening an old conversation redirects to sign-in. High engagement suggests wide impact, with the reporter explicitly noting the last-known-good build.

3. **[#25220 — Windows bundled plugins unavailable: copyfile fails on EFS-encrypted WindowsApps files](https://github.com/openai/codex/issues/25220)** — 27 comments, 4 👍. A long-running (since May) Windows issue where Computer Use, Browser, Chrome, and LaTeX plugins fail to install on EFS-encrypted systems. The EFS angle makes this a niche but recurring pain point.

4. **[#15310 — Desktop automations silently fall back to workspace-write sandbox](https://github.com/openai/codex/issues/15310)** — 21 comments, 16 👍. Scheduled/recurring tasks ignore the configured `danger-full-access` sandbox until a user manually enters chat UI. Security-relevant: users believe automations have full access when they silently don't.

5. **[#35259 — Codex Desktop re-enters the model during wait/status polling, consuming credits](https://github.com/openai/codex/issues/35259)** — 15 comments, 8 👍. 19.8% of raw local token volume was spent on model turns whose only action was waiting or polling. A billing-integrity concern for heavy multi-agent users.

6. **[#37674 — Amazon Bedrock GPT-5.6 Sol lacks explicit cache controls, producing high cache-write spend](https://github.com/openai/codex/issues/37674)** — 12 comments, 12 👍, CLOSED. Community validated the issue with production usage evidence, and it's now closed — likely addressed by today's Bedrock-related PRs (#40007).

7. **[#38157 — ChatGPT Pro (20x) accounts appear to receive Pro 5x Codex usage capacity](https://github.com/openai/codex/issues/38157)** — 7 comments, 5 👍. Accounts identified as `plan_type: "pro"` behave like the smaller Pro 5x tier. Billing accuracy issue with high trust impact.

8. **[#29002 — MCP tools/call fails with Unexpected response type when valid result decodes as CustomResult](https://github.com/openai/codex/issues/29002)** — 6 comments, 7 👍. Interop bug affecting custom MCP servers with non-standard result types — a blocker for MCP ecosystem builders.

9. **[#33398 — Codex Desktop stops prematurely after context/task handoff](https://github.com/openai/codex/issues/33398)** — 8 comments, 6 👍. Agent halts after handoff, requiring a nudge message to resume. Disruptive for long-running multi-step tasks.

10. **[#39856 — Windows Remote: QR pairing succeeds but Android clients cannot establish session](https://github.com/openai/codex/issues/39856)** — 8 comments, 0 👍. Newest of the Windows Remote wave; `nextConnectionCount=0` suggests a server-side session bug.

## Key PR Progress (10)

1. **[#40024 — Honor granular sandbox approvals in unified exec](https://github.com/openai/codex/pull/40024)** — Ensures `require_escalated` commands respect `sandbox_approval` granular settings, closing a security gap between policy and execution.

2. **[#40021 — Cancel Guardian reviews with their tool calls](https://github.com/openai/codex/pull/40021)** — Propagates cancellation tokens so interrupting a tool aborts its pending Guardian approval, improving interrupt responsiveness.

3. **[#40018 — Add browser and computer use configuration](https://github.com/openai/codex/pull/40018)** — Typed settings for browser history/per-origin/CDP policies and computer-use app access (macOS bundle IDs, Windows AUMIDs). Foundation for fine-grained remote/permission controls.

4. **[#40015 — Harden remote installed plugin cache reconciliation](https://github.com/openai/codex/pull/40015)** — Scopes plugin caches to active accounts and serializes reconciliation with installs/uninstalls — likely addressing remote-session plugin races seen across Windows issues.

5. **[#40013 — Reuse Guardian reviews in async risk scoring](https://github.com/openai/codex/pull/40013)** — Feeds completed synchronous Guardian decisions into v2 async classifiers as trusted context, improving risk-scoring consistency.

6. **[#40012 — Preserve executor context for MCP stop hooks](https://github.com/openai/codex/pull/40012)** — Scopes stop-hook calls to the originating MCP environment, preventing cross-environment hook invocation.

7. **[#40009 — Run allowlisted executor plugin stop hooks](https://github.com/openai/codex/pull/40009)** — Accepts only the bundled Computer Use `Stop` hook for `node_repl.turn_ended`, locking down what plugins can execute at turn end.

8. **[#40007 — Implement Amazon Bedrock setup in the app server](https://github.com/openai/codex/pull/40007)** — Adds `account/bedrock/discover` and `account/bedrock/setup` endpoints for AWS profile/credential validation. Directly addresses #37674 and the broader Bedrock provider story.

9. **[#40005 — Route escalated commands through synchronous Guardian review](https://github.com/openai/codex/pull/40005)** — Closes a bypass where non-retry escalated commands skipped Guardian; now all escalation requests get full review.

10. **[#39997 — Add a response target picker to `/copy`](https://github.com/openai/codex/pull/39997)** — Lets users copy the whole response or a specific fenced code block/blockquote with language labels and whitespace preservation — a UX win for CLI users.

## Feature Request Trends

- **Tool call visibility controls** ([#39819](https://github.com/openai/codex/issues/39819), 2 comments, 3 👍): Users want the collapsed tool-call view reverted to a configurable option in `config.toml`. A quality-of-life request following a UI regression.
- **Browser/computer-use granular permissions**: Multiple PRs today (#40018, #39995, #40000) and related issues show demand for per-origin browser access, per-app computer-use policies, and persistent approval controls.
- **Explicit cache controls for third-party providers** ([#37674](https://github.com/openai/codex/issues/37674)): Cost-conscious users want opt-in prompt caching for Bedrock and other providers.
- **Remote-control reliability on Windows**: The volume of new issues (#39947, #39856, #39915, #39931, #39974) signals a dominant theme — Windows Remote is currently the platform's weak link.

## Developer Pain Points

1. **Windows Remote is broken or flaky in 26.8xx** — at least 8 issues in 24 hours covering QR-pairing failures, `Transport unavailable`, disconnects, timeouts, and cross-device inconsistency. This is the #1 community frustration right now.
2. **Sandbox behavior ambiguity** — automations silently running under `workspace-write` instead of `danger-full-access` (#15310) and `deny_read_acl_state.json` unrecoverable corruption (#35718) erode trust in sandbox guarantees.
3. **Sandbox recovery is poor** — the NUL-filled state file on Windows survives uninstall/reinstall (#35718), and there is no apparent self-healing mechanism.
4. **Auth instability** — stale-token 401s (#39850) and conversation-open auth resets (#39162) interrupt workflows with no clear trigger or recovery path.
5. **Hidden credit/billing drains** — polling re-entry (#35259), Pro-tier metering mismatch (#38157), and cache-write costs (#37674) show users feel blindsided by usage spikes they cannot control or predict.
6. **MCP custom-provider friction** — `CustomResult` decode failures (#29002) and native subagent orchestration issues with non-OpenAI providers (#17598) remain open for months, slowing MCP ecosystem adoption.

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI Community Digest — 2026-08-22

## Today's Highlights
This week's Digest is dominated by a massive PR-generation infrastructure push (8+ PRs) for automated bug-fixing evaluation pipelines, alongside continued focus on long-standing reliability issues around agent hangs, subagent turn handling, and Auto Memory bugs. A new nightly release (v0.56.0-nightly.20260821) includes a fix for symlink handling in ignore paths and refactoring of the shell execution service.

## Releases
**v0.56.0-nightly.20260821.g30573d2e4** — Nightly release with two changes:
- fix(core): ensure consistent symlink evaluation in ignore path handling ([PR #28915](https://github.com/google-gemini/gemini-cli/pull/28915))
- refactor(core): remove eslint-disable and type-asserts from shellExecutionService ([PR #28862](https://github.com/google-gemini/gemini-cli/pull/28862))

## Hot Issues

1. **[#22323 — Subagent recovery after MAX_TURNS is reported as GOAL success](https://github.com/google-gemini/gemini-cli/issues/22323)** (P1, 13 comments) — A `codebase_investigator` subagent reports `status: "success"` and `Termination Reason: "GOAL"` even when it hits the max turn limit before doing any analysis. This is a critical correctness bug that masks real failures in agent workflows.

2. **[#21409 — Generalist agent hangs forever](https://github.com/google-gemini/gemini-cli/issues/21409)** (P1, 8 comments, 8 👍) — Simple changes like folder creation hang indefinitely when the generalist agent is deferred to. Users report waiting up to an hour before cancelling. Workaround: explicitly instructing the model not to defer to sub-agents.

3. **[#19873 — Leverage model's bash affinity via Zero-Dependency OS Sandboxing](https://github.com/google-gemini/gemini-cli/issues/19873)** (P2, 8 comments) — Gemini 3 models are "native bash users" chaining POSIX tools. This enhancement proposes a sandboxing approach to let models use their preferred tooling without compromising security.

4. **[#24353 — Robust component level evaluations](https://github.com/google-gemini/gemini-cli/issues/24353)** (P1, 7 comments) — Epic tracking expansion of 76 behavioral eval tests across 6 Gemini models. The community wants more robust, component-level testing infrastructure.

5. **[#22745 — Assess AST-aware file reads, search, and mapping](https://github.com/google-gemini/gemini-cli/issues/22745)** (P2, 7 comments) — Epic investigating whether AST-aware tools could reduce token usage by precisely reading method bounds and navigating codebases more efficiently.

6. **[#21968 — Gemini does not use skills and sub-agents enough](https://github.com/google-gemini/gemini-cli/issues/21968)** (P2, 6 comments) — Users report the CLI doesn't autonomously use custom skills (e.g., gradle, git) even when relevant. Requires explicit instruction to activate them.

7. **[#26522 — Stop Auto Memory from retrying low-signal sessions indefinitely](https://github.com/google-gemini/gemini-cli/issues/26522)** (P2, 5 comments) — Auto Memory re-processes low-signal sessions repeatedly if the extraction agent decides not to read them, causing wasted API calls and potential loops.

8. **[#26525 — Add deterministic redaction and reduce Auto Memory logging](https://github.com/google-gemini/gemini-cli/issues/26525)** (P2, 4 comments) — Security concern: transcript content is sent to the extraction model before redaction happens. Community wants deterministic redaction before content enters model context.

9. **[#25166 — Shell command execution gets stuck with "Waiting input" after completion](https://github.com/google-gemini/gemini-cli/issues/25166)** (P1, 4 comments, 3 👍) — Simple CLI commands hang after completion, showing "Awaiting user input" indefinitely. Extremely common reliability issue affecting everyday workflows.

10. **[#22232 — Enhance browser_agent resilience](https://github.com/google-gemini/gemini-cli/issues/22232)** (P3, 4 comments) — Browser agent uses a "fail-fast" strategy on locked browser profiles. Community wants automatic session takeover and lock recovery instead.

## Key PR Progress

1. **[#28934 — (FIX) history rollback and retry nudge optimizations](https://github.com/google-gemini/gemini-cli/pull/28934)** (size/l) — Optimizes tool call cancellations and retry nudges to prevent context window bloat and maximize prefix caching efficiency. Rolls back synthetic tool call history on cancellation.

2. **[#28827 — fix(core): avoid false authentication errors for 401 substrings](https://github.com/google-gemini/gemini-cli/pull/28827)** (size/s) — Fixes #28203 by preventing `isAuthenticationError` from treating unrelated values containing `401` (e.g., ports, exit codes) as authentication failures.

3. **[#28940 — fix(a2a-server): clear stale cancellation error on new message turns](https://github.com/google-gemini/gemini-cli/pull/28940)** (size/l) — Fixes state corruption in the A2A server where subsequent prompts crash with `Execution aborted` after a request cancellation.

4. **[#28935 — fix(sandbox): isolate Docker and container runtime sockets in macOS Seatbelt](https://github.com/google-gemini/gemini-cli/pull/28935)** (size/l) — Security hardening: denies access to container runtime daemon sockets and binaries to prevent sandbox escape via hypervisor filesystem mounts.

5. **[#28955 — Update dependencies, add MCP configuration, and integrate ECC bundles](https://github.com/google-gemini/gemini-cli/pull/28955)** (size/xl) — Large dependency update and integration of ECC (error correction code) bundles plus MCP configuration.

6. **[#28949 — feat(pr-generation): add LLM diff judge evaluation module and rubric](https://github.com/google-gemini/gemini-cli/pull/28949)** (size/l) — Introduces automated LLM-as-a-Judge evaluation of generated PR diffs against accepted ground-truth PRs.

7. **[#28948 — feat(pr-generation): add evaluation suite harness and e2e benchmark runner](https://github.com/google-gemini/gemini-cli/pull/28948)** (size/xl) — Adds a full evaluation harness for benchmarking automated PR code generation across curated issues.

8. **[#28952 — feat(pr-generation): add interactive diff comparison visualizer generator](https://github.com/google-gemini/gemini-cli/pull/28952)** (size/xl) — Visualizer for side-by-side comparison of agent-generated diffs vs ground-truth fixes using Diff2HTML and Highlight.js.

9. **[#28933 — feat(pr-generation): implement iterative orchestrator state machine](https://github.com/google-gemini/gemini-cli/pull/28933)** (size/l, closed) — Centralized orchestrator for repository setup, multi-turn coding, evaluation, and ESLint static analysis with trajectory logging.

10. **[#28947 — feat(triage-eval): Update Golden Issues Dataset Schema](https://github.com/google-gemini/gemini-cli/pull/28947)** (size/xl, closed) — Adds standardized 89-issue Golden Dataset (45 OK, 44 non-OK) with production Firestore schema for benchmark evaluation.

## Feature Request Trends

1. **Automated PR Generation & Evaluation Infrastructure** — A massive wave of PRs (#28933, #28948, #28949, #28952) builds an end-to-end pipeline for auto-fixing bugs and evaluating the results. This suggests a major internal push toward autonomous bug-fixing agents.

2. **AST-Aware Code Navigation** — Multiple issues (#22745, #22746) advocate for AST-aware file reads, search, and codebase mapping to reduce token bloat and improve precision. Tools like `tilth` and `glyph` are recommended as starting points.

3. **Agent Self-Awareness & Autonomy** — Users want the CLI to better understand its own capabilities (#21432), use skills/sub-agents autonomously (#21968), and discourage destructive behaviors like `git reset --force` (#22672).

4. **Memory System Improvements** — A cluster of issues (#26516, #26522, #26523, #26525) focus on Auto Memory reliability: deterministic redaction, quarantining invalid patches, and avoiding retry loops.

5. **Enhanced Agent Sandboxing** — Both #19873 (zero-dependency sandboxing) and #28935 (macOS Seatbelt isolation) indicate strong interest in letting models operate freely while maintaining security boundaries.

## Developer Pain Points

1. **Agent Hangs & False Success Reports** — The most critical recurring frustration: agents hang indefinitely (#21409), report GOAL success when actually interrupted (#22323), and shell commands get stuck after completion (#25166). These reliability issues undermine trust in autonomous workflows.

2. **Sub-Agent & Browser Agent Reliability** — Users report browser agent failures on Wayland (#21983), ignored settings.json overrides (#22267), and lock-related crashes (#22232). Sub-agent trajectories are also hard to inspect or share (#22598, #21763).

3. **Context Window Management** — Large file reads "firehose" the context (+15k tokens/turn), and models create scattered tmp scripts across directories (#23571). There's strong demand for token-frugal reads (#19561) and rollback optimizations (#28934).

4. **Tool Limit Errors** — Encounters 400 errors when more than 128 tools are available (#24246), suggesting the agent isn't smart about limiting tools in scope.

5. **Security & Privacy Concerns** — Auto Memory sends transcript content to models before redaction (#26525), and antivirus false positives on error reports in temp directories (#20238) remain unresolved.

6. **Configuration & Setup Friction** — Symlinked agent files aren't recognized (#20079), interactive prompts (e.g., vite app creation) hang (#22465), and output hooks can crash the entire CLI (#22186).

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI Community Digest — 2026-08-22

## Today's Highlights
The v1.0.81-7 prerelease introduces session recovery after crashes or machine restarts, eliminating the need to manually reopen terminal sessions. The issue tracker is dominated by model configuration complaints—users want multi-model BYOK support, in-session model switching, and are hitting reasoning-effort incompatibilities across Claude models. A new wave of ACP (Agent Client Protocol) bugs has surfaced, including incorrect `stopReason` values and unconditional session aborts that kill background sub-agents.

## Releases
**v1.0.81-7** (prerelease)
- **Session recovery:** On startup, the CLI now offers to restore sessions that were still open when the CLI exited unexpectedly (crash or machine restart), so work in progress isn't lost.
- **Model metadata:** `models.list` now includes service-published `infoMessages` and `warningMessages` per model, improving transparency around model status and limitations.
- **New command:** `copilot app` added to open the GitHub app.

## Hot Issues

1. **[#3282 — Add multiple BYOK model capability in copilot cli](https://github.com/github/copilot-cli/issues/3282)** — 🔥 26 👍, 8 💬  
   Users are locked to a single BYOK model per session via env var. Switching models forces a full session restart. Community strongly wants multi-model BYOK support within the TUI.

2. **[#3709 — Allow /model to switch between multiple models, including BYOK/local providers](https://github.com/github/copilot-cli/issues/3709)** — 🔥 27 👍, 4 💬  
   The `/model` picker only lists GitHub-hosted models, ignoring configured local BYOK providers. This is the most-upvoted open request—users want one session to span multiple providers without restarting.

3. **[#4345 — Reasoning effort 'medium' not supported for claude-haiku-4.5](https://github.com/github/copilot-cli/issues/4345)** — 4 👍, 8 💬  
   Server-side feature flags trigger a `reasoningEffort: medium` for models that don't support it, causing repeated execution failures during sub-agent runs. Flag interaction bug affecting Claude models.

4. **[#1313 — Session Branching](https://github.com/github/copilot-cli/issues/1313)** — 13 👍, 7 💬  
   Users want to fork a session at any point, inheriting full history while preserving the original branch. A long-standing power-user request (open since February).

5. **[#4211 — Copilot CLI can't handle BigInt in MCP responses](https://github.com/github/copilot-cli/issues/4211)** — 3 👍, 5 💬  
   A single `BigInt` value from an MCP server crashes the CLI and aborts all active tasks. Blocking for teams using MCP servers that return large numeric IDs.

6. **[#4535 — `store_memory` fails in v1.0.81 prereleases: "Instance id is required"](https://github.com/github/copilot-cli/issues/4535)** — 0 👍, 4 💬  
   Native memory writer invoked without a required instance ID. Memory persistence is broken in the prerelease channel—a regression vs. stable builds.

7. **[#4521 — Sandbox cannot be disabled](https://github.com/github/copilot-cli/issues/4521)** — 4 👍, 3 💬  
   Config shows sandbox disabled, but runtime still enforces it. Users cannot opt out despite explicit configuration.

8. **[#4542 — Workspace .mcp.json detected but not connected in sessions](https://github.com/github/copilot-cli/issues/4542)** — 1 👍, 1 💬  
   `mcp list` shows workspace MCP servers as enabled, but they're silently unavailable in actual agent sessions. Configuration desync between discovery and runtime.

9. **[#4533 — Terminal UI freezes when turn spawns parallel subagents](https://github.com/github/copilot-cli/issues/4533)** — 0 👍, 1 💬  
   Prerelease regression: the TUI stops consuming events (input + scroll dead) when parallel subagents launch. The runtime keeps working, so users can't see results or interrupt.

10. **[#4549 — Windows: every shell command spawns visible PowerShell window](https://github.com/github/copilot-cli/issues/4549)** — 0 👍, 1 💬  
    Near-constant console window flashing during agent activity on Windows. Steals focus, highly disruptive for interactive use.

## Key PR Progress
No pull requests were updated or merged in the last 24 hours.

## Feature Request Trends

- **Multi-model flexibility (dominant):** Users consistently ask for the ability to use multiple BYOK/local models within a single session, switch models mid-session via `/model`, and have the picker list all available providers. Issues #3282 and #3709 share this direction.
- **Session recovery and branching:** Beyond the crash-recovery shipped in v1.0.81-7, users want explicit branching (#1313) and an unscoped `/resume` picker to escape cwd/repo grouping (#4554).
- **Inline plan annotations:** #4563 asks for selecting plan text and attaching inline feedback, avoiding verbose restating of context in chat.
- **Interactive user questioning:** #4557 requests restoration of the `ask_user` interactive multi-choice menu that worked in older versions (v1.0.6) but no longer triggers.

## Developer Pain Points

- **Model configuration friction:** The inability to switch models (especially BYOK) without restarting sessions is the single most common pain point, echoed across multiple high-engagement issues.
- **MCP reliability gaps:** BigInt serialization crashes (#4211), unavailable servers reported as "waiting on ide" hangs (#4552), and workspace configs detected but not connected (#4542) collectively make MCP integration fragile and hard to debug.
- **Prerelease regressions:** v1.0.81 introduced serious issues—`store_memory` failures (#4535), terminal UI freezes with parallel subagents (#4533)—undermining confidence for teams testing early builds.
- **Windows experience:** Visible PowerShell console windows on every shell command (#4549) and `wta.exe` path-quoting failures (#4540) degrade the Windows developer experience significantly.
- **Reasoning effort incompatibilities:** Feature-flag-driven misconfiguration causing repeated model-call failures (#4345, #4560) wastes developer time and requires deep debugging to trace back to server-side flags.

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

**Kimi Code CLI Community Digest — 2026-08-22**

---

### 1. Today's Highlights

The community is currently focused on a **critical runtime lifecycle bug** where background subagents continue consuming LLM quota after being marked `timed_out` or `killed`, rendering `TaskStop` ineffective. On the docs front, a new PR clarifies the security boundaries of the plugin system, specifically warning about local subprocess execution and credential leakage risks. No new releases were published in the last 24 hours.

---

### 2. Releases

No new releases were published in the last 24 hours. (Last release remains the previous build; no changelog updates to report.)

---

### 3. Hot Issues

**#2615 — [Bug] Background subagent keeps making LLM calls after TaskStop/timeout marks it terminal**  
[GitHub](https://github.com/MoonshotAI/kimi-cli/issues/2615)  
- **Why it matters:** This creates an invisible cost leak: the task disappears from active tracking, but the LLM requests continue. Users cannot stop it, and quota burns silently.  
- **Community reaction:** No comments yet, but the issue is clearly high-severity (lifecycle state machine edge case). Likely to receive quick triage due to the direct CDN impact on user billing.

---

### 4. Key PR Progress

**#2614 — docs(plugins): document security and persistent data**  
[GitHub](https://github.com/MoonshotAI/kimi-cli/pull/2614)  
- **What it does:** Documents that plugin tools execute as local subprocesses with the invoking user's file/network permissions. Adds warnings against logging or committing injected credential values, clarifies plugin reinstallation behavior (replaces install directory), and recommends separate environments for sensitive work.  
- **Why it matters:** Addresses a gap in community knowledge—many users treat plugins as sandboxed when they are not. This is an important trust/safety doc improvement needed before wider plugin adoption.

---

### 5. Feature Request Trends

No new feature requests were logged in the last 24 hours. The dominant signal remains the lifecycle bug above, which may spawn a feature request for **watchdog/guardrail timeout enforcement** on subagent LLM calls.

---

### 6. Developer Pain Points

- **Process lifecycle management:** The inability to forcefully terminate a stuck subagent at the LLM-call level is a recurring pain—`TaskStop` and timeout metadata are not sufficient to enforce termination at the network layer.  
- **Invisible resource consumption:** When subagents drop off active-task tracking, developers lose visibility into quota usage, making cost attribution and debugging harder.

---

*Data window: 2026-08-21 00:00 UTC → 2026-08-22 00:00 UTC*

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode Community Digest — 2026-08-22

## Today's Highlights
Two patch releases (v1.18.20, v1.18.21) shipped robust reliability fixes: retries for `network_error` finish reasons, resumable subagent task IDs, and proper handling of unknown provider finish codes. The community is focused on streaming limitations (#785, 38 👍), silent session terminations on empty responses (#41469), and the ongoing cost-tracking RFC (#12377) that would unify subagent and multi-model cost aggregation. Desktop issues around OAuth failures (#43850) and renderer freezes (#30906) remain pain points for Windows users.

## Releases

### v1.18.21
**Core Bugfixes:**
- Continue responses when a model reports an unknown finish reason instead of stopping early
- Route Vertex AI `eu` and `us` multi-region Gemini requests through REP endpoints

**Desktop Bugfixes:**
- Keep file search results visible while the next search is loading

### v1.18.20
**Core Bugfixes:**
- Surface failed subagent tool calls with a resumable `task_id`
- Retry provider responses that end with `finish_reason: network_error`
- Retry more network error variants, including `network-error` and `network_error`
- Surface resumable subagent failures instead of returning incomplete data

---

## Hot Issues

### 1. [#785 — Is there a way to disable streaming mode?](https://github.com/anomalyco/opencode/issues/785) (OPEN, 31 comments, 38 👍)
Proxy providers (Credal OpenAI Proxy) that don't support streaming are blocking usage entirely. High engagement signals a real gap — no non-streaming fallback exists. Created July 2025 and still unresolved.

### 2. [#12377 — [RFC] Cost Tracking Architecture](https://github.com/anomalyco/opencode/issues/12377) (CLOSED, 10 comments)
Proposes unified cost tracking for subagent aggregation and multi-model correctness. Community consensus that cost display is inaccurate for multi-agent workflows. Closed, likely with a design decision pending implementation.

### 3. [#41469 — Session silently stops on empty LLM response](https://github.com/anomalyco/opencode/issues/41469) (OPEN, 10 comments)
Empty completions (0 tokens, no content) cause the session loop to exit silently. Critical because users get no error feedback, and #34473 reports similar random stops.

### 4. [#24153 — [FEATURE] Add unarchive/restore for archived sessions](https://github.com/anomalyco/opencode/issues/24153) (OPEN, 9 comments, 11 👍)
Archiving is a one-way operation — sessions vanish from the sidebar forever. Users need restore capability. Clear, well-scoped UX improvement with solid community demand.

### 5. [#30906 — Desktop v1.16.0 Windows: UI freeze on large file diffs](https://github.com/anomalyco/opencode/issues/30906) (CLOSED, 7 comments)
Electron renderer freezes completely when sessions involve large files — a regression from v1.15.13. Closed as fixed in recent releases; relevant for Windows users tracking stability.

### 6. [#28492 — MaxListenersExceededWarning after web interface starts](https://github.com/anomalyco/opencode/issues/28492) (OPEN, 7 comments)
EventTarget memory leak warning (11 listeners). Minor but recurring; users report it persists across sessions. Likely an internal architecture issue.

### 7. [#43983 — [FEATURE] Expose OpenCode Go usage history via API key](https://github.com/anomalyco/opencode/issues/43983) (OPEN, 5 comments)
Users want an API-key-authenticated endpoint for usage history on the OpenCode Go gateway. The gateway is a paid service — usage transparency requirements.

### 8. [#35376 — [Feature] Lazy-load MCP tool definitions to reduce token overhead](https://github.com/anomalyco/opencode/issues/35376) (OPEN, 5 comments)
All MCP tool definitions from all servers are injected into every prompt. With 9 servers, token overhead is massive. High-impact optimization for MCP-heavy workflows. **Author: jijoyo**

### 9. [#43829 — Deepseek-v4-flash-free Not Available](https://github.com/anomalyco/opencode/issues/43829) (OPEN, 5 comments)
Free-tier DeepSeek model missing from model picker and unusable — possibly removed from free tier entirely. Users report inability to start it in any free tier.

### 10. [#34473 — Opencode randomly stops responses](https://github.com/anomalyco/opencode/issues/34473) (OPEN, 5 comments, 3 👍)
Sessions end randomly with no error, play the completion sound, and stop mid-thinking. Related to #41469 — possibly the same root cause (empty/unknown finish reason).

---

## Key PR Progress

### 1. [#44002 — fix(core): recover partial provider failures](https://github.com/anomalyco/opencode/pull/44002) (OPEN, contributor: kitlangton)
Automatically recovers retryable provider-internal failures that arrive after partial output (e.g., reasoning, text), provided no tool activity occurred. Fixes a frustrating "output then crash" pattern.

### 2. [#44001 — fix(core): omit running shells from forks](https://github.com/anomalyco/opencode/pull/44001) (OPEN, contributor: kitlangton)
Prevents forked sessions from inheriting a standalone shell projection still running in the parent — fixes orphaned/duplicate shell state in forks.

### 3. [#44003 — fix(tui): contain MCP sidebar errors](https://github.com/anomalyco/opencode/pull/44003) (OPEN, contributor: kitlangton)
Keeps MCP connection failures compact in the sidebar — truncates server names and adds a stable, right-aligned semantic status. Clean UX fix for noisy MCP errors.

### 4. [#44000 — fix(codegen): stabilize generated contract names](https://github.com/anomalyco/opencode/pull/44000) (OPEN, contributor: kitlangton)
Generated TypeScript and OpenAPI names now derive from contract identity instead of traversal position, making the codegen output stable across refactors.

### 5. [#43844 — fix(server): reject requests for missing project directories](https://github.com/anomalyco/opencode/pull/43844) (OPEN, contributors: shijiatongxue)
Fixes #39471 — HTTP middleware now rejects requests when the saved project directory has been deleted or moved, preventing silent failures.

### 6. [#43915 — fix(provider): guard textVerbosity injection for @ai-sdk/openai-compatible providers](https://github.com/anomalyco/opencode/pull/43915) (CLOSED)
Closes #43911. Prevents auto-injection of `textVerbosity: "low"` for `gpt-5.x` models on non-Azure openai-compatible providers — broke Bedrock Mantle via LiteLLM.

### 7. [#43775 / #43998 — fix(core): bypass Windows Git lookup](https://github.com/anomalyco/opencode/pull/43998) (OPEN, both by opencode-agent[bot])
Two concurrent PRs resolving Git executable path resolution on Windows — uses `child_process.spawn` with absolute `.exe` paths and preserves dynamic PATH on non-Windows. Duplicate work, but same fix.

### 8. [#43999 — fix(server): match project copy errors by _tag instead of instanceof](https://github.com/anomalyco/opencode/pull/43999) (OPEN, contributor: miladsoroush)
Closes #43995 — replaces `instanceof` checks with `_tag` matching to handle duplicate `@opencode-ai/core` loads in a process (bundler boundaries, workspace path mapping).

### 9. [#38194 — fix(opencode): skip tui migration when tui.jsonc exists](https://github.com/anomalyco/opencode/pull/38194) (CLOSED)
Closes #38167 — legacy TUI migration only checked for `tui.json`, causing startup crashes when a commented `tui.jsonc` already existed.

### 10. [#38171 — fix(config): escape substitutions before JSONC parsing](https://github.com/anomalyco/opencode/pull/38171) (CLOSED, contributor: doomsday616)
Closes #32695 — `{env:VAR}` values were substituted raw, so native Windows paths like `C:\Users\...` broke JSONC parsing. Escapes substitutions before parsing.

---

## Feature Request Trends

**1. Cost transparency (gain momentum)**
- #43983: usage history API endpoint
- #14524: display model cost in model picker (10 👍,  5 comments)
- #12377: unified cost tracking architecture RFC
- There's a clear push for cost visibility across pickers, sessions, and APIs.

**2. Session lifecycle control**
- #24153: unarchive/restore archived sessions (11 👍)
- #34473/#41469: silent session termination — users want control/visibility into why sessions end
- Expect more session-management features (pause/resume, explicit error surfacing).

**3. Token overhead optimization**
- #35376: lazy-load MCP tool definitions
- Tool definitions bloat prompts; users want selective/deferred tool loading. High impact for MCP-heavy setups.

**4. Streaming flexibility**
- #785: non-streaming mode support
- Proxy/provider compatibility remains an issue — want opt-out of streaming.

**5. Free-tier model availability**
- #43829, #43805: DeepSeek free models missing from pickers — users depend on free tiers.

**6. Cross-platform parity**
- #33219: FreeBSD support
- Windows-specific issues keep recurring (Git lookup, renderer freeze). Community wants broader platform stability.

---

## Developer Pain Points

**1. Silent failures / no error propagation**
- #41469 (empty completion, session silently exits), #34473 (random stops), #43924 (no response, exits without error). Recurring theme — the system swallows provider errors, leaving devs guessing.

**2. Provider compatibility friction**
- #785 (no streaming support in proxy), #43911 (textVerbosity injection breaking LiteLLM/Bedrock), #43915 (guard logic). OpenCode makes assumptions about provider behavior that break non-standard gateways.

**3. MCP tool bloat**
- #35376 — all tool definitions injected into every prompt; token overhead is a real cost driver. Lazy loading is a high-priority request.

**4. Desktop/Windows instability**
- #30906 (renderer freeze on large files), #43850 (OAuth fails on Windows), #28492 (memory leak warning). Windows users face regressions and infrastructure issues more frequently.

**5. Subagent monitoring and recovery**
- #42657 (TUI lag with multi-subagent sessions, 97% CPU), #40217 (invisible permission dialogs — 3270 prompts never seen!). Multi-agent workflows are powerful but unwieldy to monitor and debug.



</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

# Pi Community Digest — 2026-08-22

## Today's Highlights

A significant cluster of 17+ new issues filed yesterday focuses on SDK-level TUI customization: per-block expand/collapse defaults, sticky headers, and runtime wheel-scroll sensitivity. Two critical fixes landed — session context re-pairing on rebuild (PR #8428, addressing the #8166 corruption bug) and extension factory failure cleanup (PR #8424). The community also saw progress on `/exit` alias (PR #4537, closing the long-standing #6193) and a Radius-artifacts-based `/share` command (PR #8443), while auto-compaction reliability (#6879) remains the most-engaged open issue with 19 comments.

## Releases

No new releases in the last 24 hours.

## Hot Issues

1. **[#6879 — Auto-compaction never triggers until provider overflow](https://github.com/earendil-works/pi/issues/6879)** • 19 comments • 17 👍
   The most active open issue. A 2-hour agentic session on GPT-5.6-sol blew past the 100% context window, and compaction only fired when the API rejected at 373k tokens. Community strongly supports checking after every agentic turn instead of relying solely on pre-turn checks. **Why it matters:** Compaction is core to long-session reliability; silent failure wastes tokens and breaks flows.

2. **[#2733 — Backspace/Delete broken in Windows Terminal](https://github.com/earendil-works/pi/issues/2733)** • 11 comments
   Regression from 0.62 → 0.64 affecting Windows Terminal key bindings. Long-running issue (since March) that keeps resurfacing — multiple key-event bugs suggest deeper input-handling fragility on Windows.

3. **[#7130 — Backspace deletes 2 chars in Kitty](https://github.com/earendil-works/pi/issues/7130)** • 9 comments
   Companion input bug: Kitty protocol release events aren't filtered, so a single Backspace removes two characters. Pairs with #2733 — the community is clearly hitting repeated key-event regressions across terminals.

4. **[#7553 — Configurable thinking level/model for compaction](https://github.com/earendil-works/pi/issues/7553)** • 8 comments • In Progress
   Auto-compaction currently reuses the session's thinking level, making summarization expensive and slow on reasoning models. Separation of thinking budget is widely wanted.

5. **[#7995 — No Anthropic cache_control support in openai-responses transport](https://github.com/earendil-works/pi/issues/7995)** • 7 comments • In Progress
   2.5x measured cost penalty for Claude via OpenRouter responses, from an 870-trial benchmark. Real money issue for heavy users; maintainers are already investigating.

6. **[#8133 — Per-model compaction settings](https://github.com/earendil-works/pi/issues/8133)** • 3 comments • 3 👍
   Compaction settings are global today; this proposes model-specific profiles with global fallback. A natural companion to #7553, and a common ask for mixed-model workflows.

7. **[#8134 — Agent stops after first tool call via forward proxy](https://github.com/earendil-works/pi/issues/8134)** • 4 comments
   Since 0.84.0, plain-HTTP providers through a forward proxy hang on the follow-up model call after a tool result. Infrastructure-level bug blocking proxy users.

8. **[#8344 — Per-tool output expansion in fullscreen TUI](https://github.com/earendil-works/pi/issues/8344)** • 4 comments
   Independent mouse-driven expand/collapse per tool output block. Small interaction quality-of-life change with clear demand in long sessions.

9. **[#6093 — Scoped Anthropic API keys misidentified](https://github.com/earendil-works/pi/issues/6093)** • 6 comments
   Key type detection relies on `sk-ant-oat…` prefix, but Claude Code scoped keys look like regular keys, causing wrong headers. Closed as no-action; a known gap that still affects users.

10. **[#2644 — Long sessions crash with Node.js OOM (SIGABRT)](https://github.com/earendil-works/pi/issues/2644)** • 4 comments
    Heavy tool-use sessions hit fatal heap exhaustion after ~30+ minutes. Closed, but resurfaces in community discussions about long-running reliability.

## Key PR Progress

1. **[PR #8428 — Re-pair tool results when rebuilding session context](https://github.com/earendil-works/pi/pull/8428)** • Merged
   Fixes the session-corruption bug from #8166: resume, compaction, and branch navigation now correctly re-pair tool results with their invoking assistant messages and drop orphans. Critical correctness fix for long-lived sessions.

2. **[PR #8424 — Discard failed extension factory state](https://github.com/earendil-works/pi/pull/8424)** • Open
   Staged defaults and provider operations now roll back if an extension factory throws; event-bus listeners are removed. Prevents partial state from poisoned factories. Important for extension ecosystem stability.

3. **[PR #8422 — Omit reasoning effort for xAI Grok Build](https://github.com/earendil-works/pi/pull/8422)** • Open
   `grok-build-0.1` rejects requests with `reasoning.effort` — HTTP 400 on explicit levels and on the default `"none"` path. Adds a Responses compatibility flag to skip the field. Niche but blocking for Grok Build users.

4. **[PR #8459 — Keep `/` and `-` inside fullscreen double-click word selection](https://github.com/earendil-works/pi/pull/8459)** • Merged
   Fixes `Intl.Segmenter` treating path separators as word boundaries. Double-clicking a path now selects the whole component. Small but daily-visible UX fix.

5. **[PR #8443 — Share via Radius artifacts under experimental flag](https://github.com/earendil-works/pi/pull/8443)** • Merged
   `/share` now uses Radius artifacts instead of gist when enabled; triggers auth flow if logged out. Drives platform migration forward.

6. **[PR #8433 — Add `--exclude-extensions` flag](https://github.com/earendil-works/pi/pull/8433)** • Merged
   Solves the all-or-nothing extension loading dilemma: full auto-discovery or none, with no way to say "defaults minus these." Guarding inside extensions only works for ones you own — this flag lets users skip specific third-party extensions.

7. **[PR #4537 — Add `/exit` alias for `/quit`](https://github.com/earendil-works/pi/pull/4537)** • Merged
   Closes #6193; aligns with codex, claude, and opencode conventions. Simple, community-requested ergonomic fix.

## Feature Request Trends

- **Granular TUI customization** — The clearest pattern in this window: per-block expand/collapse defaults (#8448, #8344), sticky headers (#8447), runtime wheel-scroll sensitivity (#8446, #8370), and per-model compaction settings (#8133, #7553). The SDK/TUI is reaching feature parity where users now tune interactions, not just functionality.
- **Provider ecosystem expansion** — Parasail.io (#8450), SiliconFlow (#4742), AgentCore IMDS/MMDS for Bedrock (#8455), and OpenRouter reasoning-mandatory model handling (#8454, #8422) show momentum for both new providers and deeper existing-provider compatibility, especially around auth and reasoning fields.
- **Compaction ergonomics and fidelity** — Explicit full-span manual compaction (#8453), customizable compaction prompts for continuation-state fidelity (#8452), and the per-model burst from #8133/#7553 — users want precise, controllable context management, not just "auto when full."
- **RPC/multi-surface operations** — Provider login via RPC (#8451) and skills invocable mid-sentence like templates (#8457) surfaced from the SDK/RPC side: users want the same power in headless clients as in interactive mode.

## Developer Pain Points

- **Key-event handling remains the most persistent recurring bug class** — Backspace/Delete issues across Windows Terminal (#2733), Kitty (#7130, #8442), and legacy `0x7f` sequences show a pattern of terminal protocol edge cases being missed. These are high-visibility, hard-to-test regressions that keep resurfacing.
- **Proxy and transport edge cases** — Plain-HTTP providers through forward proxies hanging after tool calls (#8134) and TLS/certificate errors not treated as retryable (#8458) highlight that transport robustness improves more slowly than features.
- **Memory and long-session stability** — The OOM crash (#2644) is old but still referenced; when combined with the auto-compaction failure (#6879), users are signaling that long-running reliability is the #1 trust factor. A session that dies at 30 minutes is worse than one that never started.
- **Key-type detection and auth ambiguity** — Scoped Anthropic keys being misclassified (#6093) and keyless `AuthResult` handling for Bedrock (#8455) show credential-chain complexity is a real friction point for provider adoption.

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code Community Digest — 2026-08-22

## Today's Highlights
The 24-hour window shows a mature project in heavy CI/CD iteration: review-loop infrastructure is being hardened on multiple fronts (convergence advisories, content-filter isolation, machine-readable observations), while a cluster of new feature requests targets daemon session management (model restoration, HITL persistence, archive conflict safety). A notable community concern emerged around dependency CVE audit failures blocking every PR, alongside a persistent thread on Windows MCP instability and IME input issues.

## Releases
**v0.21.14-nightly.20260821.9f2342d323** — single commit noted: `feat(review): tell the author why a review loop is not settling` (#9461). Nightly only; no stable release in this window.

Benchmark runs against v0.21.15 reference: **SWE-bench Verified — SUCCEEDED**; **Terminal-Bench 2.0 (89 tasks) — SUCCEEDED** via DSW EAS full pipeline.

## Hot Issues
1. **[#9699 — Dependency CVE audit fails on every PR (P1, security/CI)**](https://github.com/QwenLM/qwen-code/issues/9699) — `npm audit` reports 8 vulnerabilities (1 high) in existing deps as of 2026-08-21, blocking all PRs. Community impact: every contribution pipeline is red. High urgency, no workaround posted yet.

2. **[#9556 — Should pipeline keep granting code execution as invoking user? (security/CI)**](https://github.com/QwenLM/qwen-code/issues/9556) — wenshao flags a 20-round review finding: code already runs as the review user in worktrees before any review logic executes. Open design decision on privilege scope. 7 comments, unresolved.

3. **[#9639 — Auto-mode permission classifier fail-open regression (P2, security)**](https://github.com/QwenLM/qwen-code/issues/9639) — During provider outages (2026-08-17/18), every Bash call bypassed the permission classifier, regressing #7331. Users want deterministic allow-rule short-circuit + configurable timeout/fallback. 3 comments, needs discussion.

4. **[#5180 — Subagent crashes mid-task in manager/subagent mode (P2, long-context)**](https://github.com/QwenLM/qwen-code/issues/5180) — User reports 12h13m session where subagent dies mid-execution; no error surfaced. Long-standing (June), 7 comments, still triaging. Core multi-agent stability concern.

5. **[#9693 — MCP -32000 Connection closed on Windows startup (P2, MCP/Windows)**](https://github.com/QwenLM/qwen-code/issues/9693) — Qwen Desktop reports MCP stdio transport failures even when MCP is not activated. Squares with #9675 (server disconnect between sessions) and #379 (stdio serialization bugs). Windows MCP stack is a clear weak spot.

6. **[#5966 — Chinese IME completely broken in 0.19.3 UI (P2, UI)**](https://github.com/QwenLM/qwen-code/issues/5966) — Input method fails intermittently, forces pinyin-only communication. Long-running (June), 6 comments, user frustrated ("nodejs实在是烦死了"). Related: #9666 (IME candidate box low contrast) — input hygiene for CJK users still lacking.

7. **[#5180-adjacent: #1775 — Stuck in observation loop (badcase)**](https://github.com/QwenLM/qwen-code/issues/1775) — Agent repeatedly re-observes without progress; persists since February. 3 comments. Signals loop-detection gaps outside review contexts.

8. **[#9688 — Archiving live session recreates active transcript (P2, daemon)**](https://github.com/QwenLM/qwen-code/issues/9688) — Writer continues appending after archive, leaving active+archived copies of same `chats/<session-id>.jsonl`. Web UI shows duplicates/conflicts. Fresh, 2 comments.

9. **[#2862 — Startup hangs with checkpointing enabled**](https://github.com/QwenLM/qwen-code/issues/2862) — Indefinite "Initializing…" screen; only force-quit resolves. April → August, 3 comments, still open. Reliability blocker for checkpointing users.

10. **[#8993 — Public extension installs require Git 2.37; Ubuntu 22.04 has 2.34.1 (CLOSED)**](https://github.com/QwenLM/qwen-code/issues/8993) — Resolved by PR #9690 (secure fallback: resolve ref → immutable commit → existing public download path). Good example of community-rooted fix flow.

## Key PR Progress
1. **[#9638 — Teammate messages delivered at tool-round boundaries](https://github.com/QwenLM/qwen-code/pull/9638)** — Agent Team leader now receives teammate pings between tool rounds, not at whole-task end. Improves real-time collaboration feel.

2. **[#9566 — Screen content filters before probe tree restore (autofix/takeover)](https://github.com/QwenLM/qwen-code/pull/9566)** — `scratch-tree` now refuses to operate when local config defines content filters (`filter.<name>.smudge`); prevents checkout-time code execution.

3. **[#9576 — Cross-session messages behind inbound gate (autofix/takeover, needs-human)](https://github.com/QwenLM/qwen-code/pull/9576)** — UNIX-socket-based inter-session messaging with policy gate; marked as non-user input. Foundation for multi-agent workflows.

4. **[#9690 — Public GitHub extensions with older Git](https://github.com/QwenLM/qwen-code/pull/9690)** — Directly addresses #8993: resolve ref → immutable commit → download via existing public path; no weakening of pinned Git transport.

5. **[#9596 — Ask each fix for its test; rule on non-convergence (autofix/takeover)](https://github.com/QwenLM/qwen-code/pull/9596)** — Findings now carry acceptance criteria for their own fixes; targets review-loop round count.

6. **[#9623 — Convergence observation gets machine-readable half (autofix/takeover)](https://github.com/QwenLM/qwen-code/pull/9623)** — Complements #9461's human-readable diagnosis with caller-actionable output; round report introspects its own machinery.

7. **[#9526 — Persistently-critical convergence advisory (autofix/takeover)](https://github.com/QwenLM/qwen-code/pull/9526)** — Land-with-residual-risk advisory when Criticals recur across rounds and posting-volume window is present.

8. **[#9653 — Move push-and-report body out of workflow YAML (autofix/takeover)](https://github.com/QwenLM/qwen-code/pull/9653)** — Byte-identical extraction to `.github/scripts/autofix-push-and-report.sh`; key step toward testable CI scripts.

9. **[#9624 — Close Aone residual gaps: composeUrl, test-plan routing, version floor](https://github.com/QwenLM/qwen-code/pull/9624)** — Provider-owned canonical MR URL; routes test plans; enforces Aone API version floor.

10. **[#9340 — Say when the approach, not the patch, is the open question (autofix/takeover)](https://github.com/QwenLM/qwen-code/pull/9340)** — Advisory paragraph + verdict clause when PR grew enough that shape-of-change is the real open question.

## Feature Request Trends
- **Daemon session management** (new cluster): restore per-session model (#9686), restore unanswered `ask_user_question` HITL (#9664), archive-writer conflict safety (#9688). Users want resilient long-running sessions.
- **Plan mode configurability**: read-only command allowlist (#9694) — extend built-in set via `settings.json`.
- **UI/UX defaults**: start in expanded detail mode (#9670); bottom-align short content (#9305); avoid default-selected confirmation boxes (#9571).
- **Session/model persistence**: ongoing from earlier windows; now explicitly daemon-scoped.
- **Web Shell / Electron evaluation** (#9168, closed): community asked for Electron reference implementation; Tauri remains default.

## Developer Pain Points
1. **CI friction**: CVE audit failures block all PRs (#9699); PAT-bearing job isolation unresolved (#9089); release-triggered smoke/flake churn.
2. **Windows MCP instability**: startup connection errors (#9693), mid-session disconnects (#9675), stdio serialization bugs (#379) — three separate reports converging on "Windows + MCP is broken."
3. **CJK input issues**: IME completely broken (#5966) + low-contrast candidate box (#9666) — Chinese input remains unreliable across versions.
4. **Review-loop fatigue**: convergence advisories proliferating (#9461→#9623→#9526→#9596) — maintainers are spending significant cycles making the review skill explain itself.
5. **Session reliability**: checkpointing hangs (#2862), transcript mid-sentence recovery (#8094), observation loops (#1775) — long-standing reliability debt.
6. **Subagent control**: users want ability to disable built-in general-purpose subagent (#1212); crashes in manager/subagent mode (#5180) persist.

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

# DeepSeek TUI Community Digest — 2026-08-22

## Today's Highlights
The community's focus has shifted decisively toward **supervised, unattended operation** of long-lived sessions. A substantial PR stack from M-Maciej (#5535) consolidates the control-surface work — lifecycle outbox, `/relaunch`, per-session control sockets, and a quiet-period bug fix — into a single cohesive seam. In parallel, maintainer Hmbown filed two critical reliability reports (#5528, #5529) documenting silent workflow failures and sub-agent wall-time deaths, signaling that production-readiness and observability are now the dominant community priorities.

## Releases
No new releases in the last 24 hours. The project remains in an active refactoring and stabilization phase, with the EPIC-005 crate decomposition (#5316) and the FEAT-018 command-shape migration (#5525) still in flight.

## Hot Issues

1. **[#5316 — EPIC-005: CodeWhale TUI Crate Decomposition (Umbrella)](https://github.com/Hmbown/CodeWhale/issues/5316)** — The umbrella epic tracking the entire TUI crate decomposition effort. 11 comments in the last day, showing active coordination across sub-epics and PRs. This structure defines the architectural direction all recent refactoring PRs report into.

2. **[#5526 — Deprecated shell completion](https://github.com/Hmbown/CodeWhale/issues/5526)** — PowerShell users hit stale completion scripts that still trigger the old `codewhale-tui` binary name. The doc surface provides no guidance on regeneration. A straightforward discoverability and consistency bug, now with a targeted fix in PR #5530.

3. **[#5541 — DeepSeek-V4-Flash-Vision-Exp support](https://github.com/Hmbown/CodeWhale/issues/5541)** — The first multi-modal model in the DeepSeek family should be assignable via the model list, with vision working end-to-end. The impact case is strong: all vision-related website and design tasks currently have no TUI-native path.

4. **[#5534 — Goal-continuation cadence bypassed on within-turn dispatch](https://github.com/Hmbown/CodeWhale/issues/5534)** — The quiet period (`continuation_delay_seconds`) added in #5508 is ignored on the within-turn path, so resumed/CLI sessions fire continuation passes instantly. A race-condition-grade bug that defeats the intended throttling. Already fixed within PR #5535.

5. **[#5533 — Control surface for supervised operation](https://github.com/Hmbown/CodeWhale/issues/5533)** — Requests a per-session control socket (message / interrupt / relaunch / status) plus `RuntimeBackendKind::External`. Filed for supervisor wrappers, automation harnesses, and CI-driven sessions. This is the feature spine for unattended operation.

6. **[#5532 — `/relaunch` — switch a running session to the current binary](https://github.com/Hmbown/CodeWhale/issues/5532)** — After `/update` installs a new binary, the user is told to restart manually because the codebase lacks a self-exec/relaunch pattern. Directly addresses the restart friction that breaks long-running supervised sessions.

7. **[#5531 — Local lifecycle event outbox (JSONL + webhook)](https://github.com/Hmbown/CodeWhale/issues/5531)** — Wants `turn_stalled` / `turn_failed` and other lifecycle events emitted to a JSONL outbox and/or webhook, for supervisors like `herdr` watching overnight or unattended runs. Mirrors the same needs as #5533 but from the event-stream side.

8. **[#4069 — Indexing privacy controls (`.codewhaleignore`)](https://github.com/Hmbown/CodeWhale/issues/4069)** — Long-running request (open since July) for a first-class ignore file so secrets, vendor trees, and local artifacts are excluded from search and context assembly — parity with `.cursorignore`. Trust and compliance blocker for enterprise adoption; only 1 comment in the last day, suggesting it may still be waiting for traction.

9. **[#5529 — Sub-agents cannot reliably execute](https://github.com/Hmbown/CodeWhale/issues/5529)** — Critical report: wall-time budget deaths lose uncommitted work, provider-route failures block dispatch entirely, and shell tooling needs workarounds. Two workers died mid-task today (IDs 117 and 83). The Fleet delegation value proposition is effectively unusable in this environment.

10. **[#5528 — Workflow runs fail silently](https://github.com/Hmbown/CodeWhale/issues/5528)** — Two workflow runs (review fan-out, phased build pipeline) failed at script-evaluation time with zero TUI surface — no toast, no status line, no workflow panel entry. Operators see "the workflow is working" with no visualization or error state. An observability gap with operational safety implications.

## Key PR Progress

1. **[#5535 — Supervised operation stack](https://github.com/Hmbown/CodeWhale/pull/5535)** — The day's most substantial PR. Five commits on one seam: lifecycle event outbox (`turn_start` / `turn_end` / `turn_stalled` / `subagent_spawn` / `subagent_complete` / `session_*` events, opt-in JSONL + webhook), `/relaunch` re-exec, per-session control socket, and the goal-continuation quiet-period fix from #5534. One PR to watch — the control surface for unattended operation.

2. **[#5525 — Refactor TUI utility command group to command shapes (FEAT-018)](https://github.com/Hmbown/CodeWhale/pull/5525)** — Converts the complete utility command group to the external command shapes from FEAT-014/015. Seven command files stay under `codewhale-tui` but change their execution boundary. Registers `/a...` commands; part of the EPIC-005 decomposition march.

3. **[#5530 — Route legacy completions through public binary](https://github.com/Hmbown/CodeWhale/pull/5530)** — The legacy `codewhale completions <shell>` now uses the same canonical generator as `codewhale completion <shell>`, and generated scripts use the public `codewhale` command name. Directly addresses #5526.

4. **[#5524 — Multi-file `read_lints` operation](https://github.com/Hmbown/CodeWhale/pull/5524)** — Extends the model-visible `lsp` tool with a `read_lints` operation for multiple workspace-relative files, reusing the session's `LspManager` transport pool — no extra language-server lifecycle. Addresses approved scope of #4070.

5. **[#5523 — Extract tool-call stages from turn loop](https://github.com/Hmbown/CodeWhale/pull/5523)** — Refactoring that splits the turn loop into `plan_tool_calls`, `execute_planned_tools`, and `process_tool_results`. Preserves control order, mutable state flow, cancellation behavior, and indexed outcome collection. The kind of structural cleanup that makes the codebase testable.

6. **[#5540 — Bump `similar` from 3.1.2 to 3.2.0](https://github.com/Hmbown/CodeWhale/pull/5540)** — Routine dependency bump. `similar` 3.2.0 adds structured, line-oriented diff features — useful for future diff display work in the TUI.

7. **[#5539 — Bump `rio-vt` from 0.5.19 to 0.5.25](https://github.com/Hmbown/CodeWhale/pull/5539)** — Routine dependency bump for the VT emulation crate; likely relevant to TUI rendering fidelity.

8. **[#5390 — Bump `rmcp` from 2.2.0 to 3.1.2](https://github.com/Hmbown/CodeWhale/pull/5390)** — Major-version bump (2.x → 3.x) in the Rust MCP SDK. Worth watching for breaking changes and MCP protocol-level improvements.

9. **[#5538 — Bump `jsonschema` from 0.46.10 to 0.49.9](https://github.com/Hmbown/CodeWhale/pull/5538)** — Substantial bump with many minor-version steps; likely includes correctness fixes for JSON Schema evaluation — relevant to workflow schema validation.

10. **[#5537 — Bump `docker/setup-buildx-action` from 4.2.0 to 4.3.0](https://github.com/Hmbown/CodeWhale/pull/5537)** — CI tooling bump for Docker Buildx setup in GitHub Actions.

## Feature Request Trends

- **Supervised operation stack (dominant theme).** Three features — control socket (#5533), lifecycle outbox (#5531), and `/relaunch` (#5532) — are highly consistent: users want to run sessions unattended, monitor them out-of-band, restart them without manual intervention, and receive telemetry when stalls or failures occur. This is the clearest directional signal from the community right now.

- **Multi-modal model support.** #5541 requests DeepSeek-V4-Flash-Vision-Exp for vision workloads. The model family is expanding; the TUI's model list must keep pace.

- **Privacy and exclusion controls.** #4069 (`.codewhaleignore`) is a persistent ask for enterprise trust. It has been open for six weeks with minimal recent activity, yet the need hasn't gone away — just less vocal.

- **Workflow observability.** #5528 (silent workflow failures) and #5529 (sub-agent execution unreliability) both underscore: the platform needs better failure surfacing, not just features.

## Developer Pain Points

1. **Silent failure modes.** Both #5528 and #5529 describe failures that produce no TUI-visible signal — workflows that look "like they're working" while failing at script-evaluation, sub-agents dying on wall-time budgets without persisting work. For operators running unattended sessions, this is the most dangerous category of bug.

2. **Restart friction.** The `/update` → "please restart" loop (addressed by #5532) is a recurring churn point for anyone running long-lived sessions.

3. **Shell completion inconsistency.** #5526 repeats a familiar story: a legacy command path (`codewhale-tui`) that no longer matches the public binary name, with no documentation pointing to the fix. The PR (#5530) is a welcome correction but the underlying discoverability problem (deprecated commands, stale docs) persists.

4. **Sub-agent execution fragility.** #5529 enumerates three concrete failure modes — wall-time deaths, provider-route failures blocking dispatch, and shell tooling workarounds. The Fleet value proposition (delegated execution) is currently undermined by reliability issues in the execution environment.

5. **Dependency churn at scale.** Five of the ten PRs today are dependency bumps, including a major-version bump (rmcp 2.x → 3.x). This is normal for an active Rust project, but the volume suggests maintainers are juggling a long tail of maintenance work alongside the EPIC-005 structural refactor.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/kky-wollu/agents-radar).*