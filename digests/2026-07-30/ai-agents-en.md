# OpenClaw Ecosystem Digest 2026-07-30

> Issues: 500 | PRs: 500 | Projects covered: 13 | Generated: 2026-07-29 23:01 UTC

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

## OpenClaw Deep Dive

Here is the OpenClaw project digest for 2026-07-30.

---

## OpenClaw Project Digest — 2026-07-30

### 1. Today's Overview

The OpenClaw project is exhibiting **very high activity** today, with 500 issues and 500 pull requests updated in the last 24 hours. The open-to-closed ratio is high (437 open issues vs. 63 closed, 414 open PRs vs. 86 merged/closed), indicating a significant **backlog pressure** on maintainers. The “Top 50” issues reveal a deeply complex ecosystem grappling with **reliability, security, and stability** concerns, particularly around the `Codex` app-server integration and session/state recovery. While no new releases were cut today, the velocity of bug reports (including several P0 and P1 regressions) suggests the project is in a **high-refinement or pre-release stabilization phase**.

### 2. Releases

**No new releases were published today.**

### 3. Project Progress

Despite the high volume of open work, 86 PRs were merged or closed today, including several high-impact fixes:

- **Core Stability:** PRs like `#115812` (Bug: `enqueuePluginNextTurnInjection` returns undefined causing silent session recovery failure) and `#112003` (test coverage for `extractRawAssistantText`) targeted specific session recovery and code quality gaps.
- **Multi-Platform Fixes:** A notable fix in `#115484` (`fix(clickclack): gate group replies on mentions`) prevents shared-workspace ClickClack accounts from responding to all group messages. Another fix in `#116042` (`fix(ios): restore Magic Keyboard return in chat composer`) addresses a user-facing regression on iPad.
- **Plugin/Agent Architecture:** PR `#116091` (`fix(plugins): deliver subagent completion to current requester`) closes a long-standing bug (#55517) where deferred subagent results had no return path to the external requester.
- **Build & CI:** PRs like `#116084` (`chore(i18n): refresh native locales`) and various dependency bumps (`#113927`) ensure the project’s infrastructure and localization remain current.

### 4. Community Hot Topics

Community discussion is heavily concentrated on **reliability and data integrity**:

- **Memory Trust & Security (#7707, 22 comments):** The most commented-on issue, this feature request for “Memory Trust Tagging by Source” reflects a deep user concern about **memory poisoning attacks**. Users are worried about malicious instructions hidden in web-scraped or third-party content influencing agent behavior.
- **CPU-Bound Crash Loops (#91009, 18 comments):** The `Codex PreToolUse` hook relay spawning CPU-bound processes is a **critical stability threat**, causing gateway stalls and RPC hangs. The `🦞 diamond lobster` and `impact:crash-loop` labels indicate this is a top-tier production issue.
- **Permanent Channel Suppression (#115326, 16 comments):** A user reports a **catastrophic state failure** where the crash-loop breaker permanently suppresses Discord/WhatsApp channels, and the documented recovery path fails. This is a direct hit on user trust in the system’s self-healing capabilities.
- **OAuth & Auth Provider Wedges (#86215, 10 comments):** Users are reporting that Codex OAuth refresh failures can **wedge an agent for hours** without clear alerts. This points to a need for more aggressive failover and better operator observability.

### 5. Bugs & Stability

A significant number of high-severity bugs are active today, many with `impact:crash-loop` or `impact:data-loss`:

- **P0 (Data Loss):**
    - **`#84882`:** memory-core Dreaming silently **deletes daily memory files** (`memory/YYYY-MM-DD.md`). (No fix PR linked yet).
    - **`#115421`:** Schema downgrade recovery **quarantines/wipes the state DB**, causing loss of cron jobs. (Linked to PR `#116115`).
- **P1 (Crash/Major Instability):**
    - **`#91009`:** CPU-bound `openclaw-hooks` processes stalling the gateway (Linked PRs exist).
    - **`#115326`:** Crash-loop breaker permanently suppressing Discord/WhatsApp (No fix PR).
    - **`#115424`:** Gateway V8 heap OOM converts one crash into a **7-core-dump loop** (No fix PR).
    - **`#115812`:** `enqueuePluginNextTurnInjection` returning `undefined` causing silent session recovery failure (**CLOSED** by `#115812`).
- **P2 (Significant Regressions):**
    - **`#97616`:** OpenClaw leaks unreaped hook/tool child processes, causing **zombie accumulation** and runtime degradation.
    - **`#74378`:** CLI commands remain alive as `node.exe` processes on Windows.
    - **`#98976`:** Provider refusals (Anthropic/OpenAI) **never trigger the model fallback chain**, causing hard failures.

### 6. Feature Requests & Roadmap Signals

Several long-standing feature requests suggest the community is pushing for greater **operational control and observability**:

- **Dynamic Model Discovery (#10687, 9 comments):** Users are frustrated with the static model catalog and want OpenClaw to auto-discover models from providers like OpenRouter.
- **Memory Lifecycle Curation (#87660, 7 comments):** Requests for the `MEMORY.md` file to be truly lifecycle-aware, protecting durable anchors while auto-archiving transient data. This aligns with the Memory Trust Tagging (#7707) request.
- **Slack Modal Support (#88154, 7 comments):** A business-user focused request for structured form input in workflows, moving beyond simple message prompts.
- **Gateway Lifecycle Hooks (#43454, 8 comments):** Users want workspace hooks to fire on specific agent lifecycle events (e.g., `onSubagentComplete`, `onToolCallThreshold`), indicating a desire for more sophisticated automation and orchestration.
- **Predicting Next Release:** Given the volume of P1 stability and security issues, the next version is likely to focus on fixing the **Codex app-server relay, session recovery, and the memory poisoning vulnerability** (#7707). The "production-readiness stability label" request (#73537) also suggests a push towards a more stable, production-grade release.

### 7. User Feedback Summary

User feedback today is overwhelmingly focused on **pain points** rather than praise.

- **Dissatisfaction:** Users are experiencing fundamental reliability failures. The sentiment from bug reports is one of **frustration and alarm** at silent data loss (`#84882`), permanent channel suppression (`#115326`), and complete session wedges (`#86215`). The phrase “documented recovery path fails” is a recurring theme, eroding confidence.
- **Pain Points:**
    - **Zero Observability:** Users can’t tell why an agent is slow, stuck, or failed (`#91009`, `#86996`).
    - **Complex Failures:** Bugs are rarely singular; they are cascading failures involving auth, sessions, and delivery paths (`#80040`, `#98790`).
    - **Data Integrity:** The silent deletion of daily memory files is deeply concerning for users who rely on the agent for long-term personal or business history.
- **Needs:** The underlying need is clear: users want OpenClaw to be a **dependable, self-healing system** that either recovers gracefully or provides clear diagnostics when it cannot.

### 8. Backlog Watch

Several critical issues remain open with no fix PR and are tagged `clawsweeper:needs-maintainer-review` or `clawsweeper-recovery-stuck`:

- **`#7707` (Memory Trust Tagging, 22 comments):** A high-value feature request for security, still awaiting a product decision and maintainer review.
- **`#39476` (A2A sessions_send duplicates, 13 comments):** A fundamental protocol bug in agent-to-agent communication that is **stale** and has a linked PR open but needs a live repro.
- **`#10687` (Dynamic Model Discovery, 9 comments):** A critical usability feature that is being blocked by `clawsweeper:needs-info` and `needs-maintainer-review`.
- **`#73537` (Production-readiness label, 8 comments):** A community-driven request for better release tracking and stability guarantees.
- **`#115424` (Gateway OOM -> Core-dump loop, 6 comments):** A newly reported, extremely severe crash bug with no fix PR yet. It is tagged `clawsweeper:needs-maintainer-review`.

---

## Cross-Ecosystem Comparison

# Cross-Project Ecosystem Comparison Report
**Date:** 2026-07-30

---

## 1. Ecosystem Overview

The personal AI agent open-source ecosystem is experiencing explosive growth, with **major stability challenges emerging alongside rapid feature iteration**. Across 12 tracked projects, we observe over **350 issues and 200 pull requests updated in a single day**, with community concerns shifting from "can it work" to "can it work reliably and securely." The ecosystem is fragmenting into two tiers: **full-stack desktop agents** (OpenClaw, IronClaw, Hermes Agent) that integrate deeply with desktop environments, and **lightweight, modular platforms** (NanoBot, ZeroClaw, Moltis) optimized for specific deployment scenarios like edge devices or enterprise orchestration. A **shared crisis of state persistence and data integrity** cuts across all projects, signaling that the ecosystem has hit the reliability wall that precedes production-grade maturity.

---

## 2. Activity Comparison

| Project | Issues Updated (24h) | PRs Updated (24h) | New Releases | Health Score | Activity Tier |
|---|---|---|---|---|---|
| **OpenClaw** | 500 | 500 | 0 | ⚠️ **Strained** | Very High |
| **ZeroClaw** | 50 | 50 | 0 | ⚠️ **Strained (design phase)** | Very High |
| **IronClaw** | 50 | 50 | 0 | ⚠️ **Strained (QA issues)** | Very High |
| **Hermes Agent** | 50 | 50 | 0 | ⚠️ **Moderate (Windows bugs)** | High |
| **CoPaw (QwenPaw)** | 25 | 50 | 0 | ✅ **Healthy** | High |
| **NanoBot** | 5 | 33 | 0 | ✅ **Healthy** | High |
| **LobsterAI** | 0 | 15 | 0 | ✅ **Healthy** | Moderate |
| **Moltis** | 1 | 6 | 0 | ✅ **Healthy** | Moderate |
| **NanoClaw** | 2 | 7 | 0 | ✅ **Steady** | Moderate |
| **NullClaw** | 1 | 4 | 0 | ✅ **Steady** | Low |
| **PicoClaw** | 1 | 2 | 0 | ⚠️ **Stalled** | Low |
| **TinyClaw** | 0 | 0 | 0 | 💤 **Inactive** | None |
| **ZeptoClaw** | 0 | 0 | 0 | 💤 **Inactive** | None |

*Health Score: Green (✅) = active issue resolution, acceptable backlog. Yellow (⚠️) = high open/closed ratio, systemic bugs, or design churn.*

---

## 3. OpenClaw's Position

**OpenClaw remains the reference implementation** and the largest project by raw activity (500 issues/PRs daily), but this scale is a double-edged sword:

### Advantages Over Peers
- **Largest plugin ecosystem** — ClickClack, Codex, and A2A protocol integrations are unmatched in breadth
- **Most mature multi-platform support** — Discord, WhatsApp, Telegram, Slack, iOS, iPad, and CLI
- **Deepest feature surface** — Memory systems, lifecycle hooks, dynamic model discovery, and agent-to-agent communication
- **Highest community investment** — 22-comment discussions on memory trust tagging (#7707) reflect an engaged, technically sophisticated user base

### Technical Approach Differences
- **Plugin-first architecture** — Unlike IronClaw's compact "Reborn" rewrite or ZeroClaw's Rust-native design, OpenClaw is JS/TS-based with a plugin sandbox (WASM-style hooks)
- **Heavy coupling to Codex** — The `Codex` app-server relay is a single point of failure, visible in today's crash-loop and session-wedge bugs (#91009, #86215)
- **Self-healing complexity** — The crash-loop breaker and session recovery mechanisms are advanced but fragile (PR #115326 shows permanent suppression)

### Community Size Comparison
- **Comment volume:** Highest in ecosystem (22-comment threads commonplace) vs. IronClaw (7-comment max) and NanoBot (6-comment max)
- **Backlog** 437 open issues vs. 63 closed suggests a **backlog crisis** — maintainers can't keep pace with bug reports
- **External contributor flow** — Weak compared to NanoBot (5 first-time contributors today) and CoPaw (5 first-time contributors)

### Key Vulnerability
OpenClaw's **P0 data loss bugs** (#84882 memory file deletion, #115421 schema downgrade wipe) are unmatched in severity by any peer project. No other project today reports silent daily file deletion.

---

## 4. Shared Technical Focus Areas

Across all active projects, **five requirements are emerging independently**, signaling industry consensus:

| Requirement | Affected Projects | Specific Community Signal |
|---|---|---|
| **State persistence & crash recovery** | OpenClaw (#115326, #7707), IronClaw (#6720, #6815), NanoBot (#5118), CoPaw (#6542), ZeroClaw (#9048) | "Documented recovery path fails" (OpenClaw), "Session history loss on crash" (CoPaw), "Background offload kills subprocess" (ZeroClaw) |
| **Memory/data integrity & poisoning defense** | OpenClaw (#7707, #84882), ZeroClaw (#9048, #9103), NanoBot (#5118) | "Memory Trust Tagging by Source" (OpenClaw), "Separate conversation history from long-term memory" (ZeroClaw) |
| **Multi-model/provider orchestration** | OpenClaw (#98976), NanoClaw (#1350, #3057), Hermes Agent (#58546), ZeroClaw (#8568) | Claude→Codex fallback (NanoClaw), Mixture-of-Agents (ZeroClaw), Provider failure opacity (ZeroClaw PR #9056) |
| **Observability & failure diagnostics** | OpenClaw (#91009, #86996), ZeroClaw (#9056), IronClaw (#6805), NanoBot (#5156) | "Zero Observability" (OpenClaw), "Generic 'all providers failed'" (ZeroClaw), "Telegram silent polling stall" (NanoBot) |
| **Session routing & multi-agent dispatch** | PicoClaw (#3301), NanoClaw (#2440), OpenClaw (#115326), ZeroClaw (#9487) | "/clear broken for non-default agents" (PicoClaw), "Runtime-owned conversation sessions" (ZeroClaw) |

### Critical Pattern
**Data loss** is the #1 cross-project concern, appearing in every project with significant activity. The ability to survive restarts and crashes without losing configuration, memory, or conversation history is now table-stakes for any production deployment.

---

## 5. Differentiation Analysis

| Dimension | OpenClaw | IronClaw | Hermes Agent | NanoBot | ZeroClaw | CoPaw (QwenPaw) |
|---|---|---|---|---|---|---|
| **Target User** | Advanced enthusiasts, developers | Enterprise operators, deployment teams | Desktop power users, Apple ecosystem | CLI/automation users, developers | Systems engineers, crypto/DeFi users | Chinese market, desktop consumer |
| **Core Language** | JS/TS | Rust (Reborn) / JS | Rust | Python | Rust | Python |
| **Primary Channel** | Multi-platform (Discord, WhatsApp, Slack, iOS) | Web UI, sandbox | Desktop (macOS/iOS focus), CLI | Telegram, CLI | CLI, WebSocket, Web dashboard | Desktop (Windows/macOS), Feishu |
| **Architecture** | Plugin-heavy, Codex-coupled | Compact "Reborn" monolithic | Desktop-native with MCP server | Modular skill marketplace | Crate-based modular, WASM plugins | Cloud-first with desktop GUI |
| **State Management** | Session recovery, crash-loop breaker | Turn-state store (LibSQL) | SQLite, session compression | Session consolidation, WeakValueDictionary | Config-driven, memory separation RFCs | Background offload, checkpoint store |
| **Security Approach** | Memory trust tagging (proposed), plugin sandbox | CapabilityAllowSet, egress proxy | Skills Guard, pairing auth, credential pools | none visible today | HMAC receipts, high-entropy detector, file write validation | Resource path restriction (import-local) |
| **Current Phase** | Stabilization (pre-release) | Reborn migration (active) | Windows regression fixing | Feature consolidation | Architectural redesign (v1.0 RFCs) | Bug fixing + feature work |
| **Unique Strength** | Largest plugin ecosystem | Production deployment focus (QA instance) | macOS/Apple ecosystem | Skill marketplace, strict typing | Cryptographic verification, MoA | Chinese market, Feishu integration |
| **Unique Weakness** | Data loss bugs, backlog pressure | QA reliability (service_unavailable every 30 min) | Windows update broken, OOM crashes | Telegram silent failure, power-limited | 7+ unratified RFCs, design churn | Western market gap, MCP fragility |

### Architectural Spectrum
- **Monolithic heavyweights:** OpenClaw, IronClaw, Hermes Agent — full desktop integration, richest feature surface
- **Modular platforms:** NanoBot, ZeroClaw, Moltis — smaller core, extensible via plugins/skills/marketplaces
- **Regional specialists:** CoPaw (China), PicoClaw (edge/Raspberry Pi), NullClaw (hobbyist)

---

## 6. Community Momentum & Maturity

### Tier 1: Very High Velocity, Stabilizing (Rapid iteration, but bugs piling up)
- **OpenClaw** — Highest raw numbers, but 7:1 open-to-closed ratio on issues signals a **maintainer bottleneck**. Community driven by bug reports, not features. **Risk:** Backlog may cause contributor burnout.
- **ZeroClaw** — Intensive RFC phase with 7 architectural proposals in 48 hours. **Risk:** Design paralysis — too many RFCs, too few implementations. 75-day-old Signal crashloop (#6724) undermines credibility.
- **IronClaw** — Reborn migration advancing (#3031 closed), but QA instance has 5 P1 bugs in 24 hours. **Risk:** Shipping Reborn without fixing production reliability.

### Tier 2: High Velocity, Healthy Balance (Active feature + bugfix work)
- **CoPaw (QwenPaw)** — Strong contributor inflow (5 first-timers today). Feature and bug PRs merge in parallel. **Healthiest balance** of any large project.
- **NanoBot** — 18 PRs merged/month cadence, strict typing enforcement, skillful bug triage. **Best open/closed ratio** among active projects. Nearing a release.
- **Hermes Agent** — High volume, but **Windows regression cluster** (3 P1 bugs in 24h) indicates a quality dip from recent updater changes.

### Tier 3: Moderate Steady (Maintenance mode or focused development)
- **Moltis** — Small but high-quality commits (ACP protocol, Langfuse instrumentation). Focused on enterprise readiness. No backlog concerns.
- **LobsterAI** — Cowork UX polish. Depends on OpenClaw ecosystem. No new features, only fixes and refactoring.
- **NanoClaw** — Steady mid-size project with useful features (dual-engine fallback, Slack thread fix). Copilot SDK request (#1350) unanswered for 4 months is a warning sign.

### Tier 4: Low/Inactive (Stalled or single-maintainer risk)
- **NullClaw** — 2-month-old scheduler bug (#915) unfixed despite a fix PR existing. **Single point of failure risk.**
- **PicoClaw** — PR #1951 stale for 4 months. Maintainer has likely deprioritized.
- **TinyClaw, ZeptoClaw** — No activity. Effectively archived.

---

## 7. Trend Signals

For AI agent developers and decision-makers, five industry trends emerge from today's data:

### 1. Reliability is the #1 Barrier to Production Adoption
Every active project has at least one **data loss or permanent-failure bug** that would make production deployment risky:
- OpenClaw: Memory file deletion, channel suppression
- IronClaw: `service_unavailable` every 30 min, task hang with broken stop button
- NanoBot: Media paths silently dropped on archive
- ZeroClaw: CLI cron jobs silently discard output

**Signal:** The ecosystem needs **standardized recovery testing** — most projects don't formally test their self-healing mechanisms.

### 2. Memory Architecture is Undergoing a Shift
Until now, memory was append-only conversation logs. The community is demanding:
- **Ephemeral vs. curated separation** (OpenClaw #87660, ZeroClaw #9048)
- **Trust tagging by source** (OpenClaw #7707) to prevent poisoning
- **Synchronous recall** (Hermes Agent #5820) for query-aware retrieval

**Signal:** Expect a "Memory 2.0" wave in next 3-6 months across all major projects, with explicit lifecycle management.

### 3. Multi-Provider Orchestration is Becoming Table-Stakes
Projects are rushing to support **automatic failover, model routing, and quota management**:
- NanoBot: Dual-engine Claude→Codex fallback (#3057)
- Hermes Agent: Credential pool confusion (#58546, P1)
- OpenClaw: Provider falls never triggering fallback (#98976, P2)

**Signal:** Users run multiple models simultaneously. Static provider configuration is dead; dynamic routing is the future.

### 4. Security Awareness is Increasing — but Inconsistently
- **Cryptographic verification** is an emerging theme (ZeroClaw HMAC receipts #4830, Moltis privilege separation #1170)
- **Basic input validation** is still being added (CoPaw import-local path restriction #6487, IronClaw tool_search disclosure #5712)
- **Poisoning/consent** is a hot topic (OpenClaw #7707 Memory Trust Tagging, Hermes Agent #16462 first-invoke MCP approval)

**Signal:** Security is a **differentiator** today, but will become a **compliance requirement** in 12 months.

### 5. Platforms are Fragmenting by Deployment Form
- **Desktop-first** (OpenClaw, Hermes Agent, CoPaw) — richest features, highest complexity, toughest reliability
- **Server/cloud-first** (IronClaw, ZeroClaw) — production-oriented, better observability, lower desktop integration
- **Edge/lightweight** (PicoClaw, NullClaw, TinyClaw) — single-board computers, constrained environments

**Signal:** The "one agent to rule them all" vision is failing; **specialization by deployment** is winning. This increases integration overhead for developers who need multiple deployment forms.

### Key Takeaway for Developers
The ecosystem is **entering the "trough of disillusionment" after the hype peak**. Early adopters who rushed to build agents are now hitting reliability walls. The next 6 months will determine which projects invest in production readiness (testing, observability, data integrity) versus continuing feature churn. **NanoBot** and **CoPaw** show the strongest balance of feature velocity and stability today, while **OpenClaw** remains the most feature-complete but highest-risk for production deployment. **ZeroClaw's RFC-driven approach** could pay off in architectural excellence, but only if the design phase concludes before community patience runs out.

---

## Peer Project Reports

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot Project Digest — 2026-07-30

## 1. Today's Overview
NanoBot sustained very high development velocity, with **33 PRs updated** and **18 merged/closed** in the last 24 hours—one of the most active days in recent history. The team addressed **5 issues**, closing 2 bugs (a PowerShell UTF-8 corruption fix and a session consolidation data-loss fix) while keeping **3 open active discussions** alive. No new releases were published today, but the sheer volume of merged PRs signals that a release may be imminent. Project health is strong, though the large backlog of 15 open PRs indicates the maintainers are juggling multiple concurrent feature and stabilization tracks.

## 2. Releases
**No new releases today.**  
The last 24 hours saw zero tagged releases, despite 18 merged PRs. Given the volume of regressions fixed and new features merged, a patch or minor release (e.g., v0.7.x or v0.8.0) is likely in the next 48–72 hours.

## 3. Project Progress (Merged/Closed PRs Today — 18 total)
Major merged/closed items:

- **Type Safety Landmark:** [#5158] [MERGED] Enforced BasedPyright `strict` type checking across all 273 modules in `nanobot/`, a foundational refactor that will prevent entire classes of runtime errors.
- **Session Consolidation Data Loss Fix:** [#5157] [MERGED] Exposed media references to session consolidation, fixing the critical bug where uploaded media paths (stored only in `media[]`) were silently dropped during archiving. Companion PR [#5139] also merged for this fix.
- **Windows Unicode Pipeline Fix:** [#5160] [MERGED] Fixed PowerShell 5.1 UTF-8 corruption by configuring `$OutputEncoding`, resolving a production bug affecting non-ASCII native pipeline input.
- **Optimistic Message Delivery UI:** [#5162] [MERGED] New WebUI feature tracking user message status through `sending`, `accepted`, and `failed` states, with hover-visible gateway error details.
- **Skill Marketplace Management:** [#5116] [MERGED] Added Discover view for skills.sh and SkillHub search, marketplace-specific trending, and third-party skill installation workflows.
- Other merged fixes: lock release cleanup ([#5151]), buffered session output bounds ([#5150]), token-usage day key validation ([#5146]).

## 4. Community Hot Topics

| Issue/PR | Type | Comments | 👍 | Topic |
|----------|------|----------|---|-------|
| [#5000] | Issue (Open) | 6 | 0 | Multi-agent collaboration proposal |
| [#5118] | Issue (Closed) | 2 | 0 | Session consolidation media data loss |
| [#5034] | PR (Open) | — | 0 | Durable state-graph goal planning |
| [#4919] | PR (Open) | — | 0 | Custom Telegram Bot API base URL |
| [#5166] | PR (Open) | — | 0 | Goal permission context var expiration |

**Deepest discussion:** [#5000] "Proposal: evolve subagent system toward multi-agent collaboration" has attracted 6 comments over 10 days. The author argues that NanoBot's current subagent model is essentially "background task delegation" rather than true multi-agent collaboration, lacking persistent identities, shared state, and inter-agent negotiation. This is a foundational design discussion that could shape NanoBot's architecture for months to come.

**Underlying need:** The community wants NanoBot to move from a single-agent-with-subtasks model to a collaborative multi-agent system where agents have memory, identity, and can negotiate task dependencies. Contributor [bingqilinweimaotai] is driving both this issue and the corresponding PR [#5034] for durable state-graph planning—suggesting this is a planned feature track, not just user feedback.

## 5. Bugs & Stability

**Severity: P1 (Critical)**
- **Session consolidation data loss** [#5118] — Media paths stored only in `media[]` silently dropped after archiving. **FIXED** in [#5157] and [#5139], both merged.
- **PowerShell 5.1 UTF-8 corruption** [#5159] — Non-ASCII pipeline input becomes corrupted on Windows. **FIXED** in [#5160], merged.
- **Idle session lock retention** [#5151] — `AgentLoop._session_locks` leaked memory across session lifetimes. **FIXED** via `WeakValueDictionary`, merged.
- **Buffered output unbounded growth** [#5150] — Exec session stdout/stderr readers could grow unbounded. **FIXED** with head/tail budget, merged.

**Severity: P2 (Medium)**
- **Manual cron completion state loss** [#5163] — Race condition between `CronService.run_job()` and store-reading APIs on WebUI reload. **No fix PR yet.**
- **WebUI microphone false silence errors** [#5165] — Web Audio analyser reported silent on non-empty audio. **Fix PR open** [#5165].
- **Malformed token-usage day keys** [#5146] — Single malformed key breaks all `/api/settings` requests. **FIXED**, merged.

**Severity: P3 (Low)**
- **Telegram silent polling stall** [#5156] — After transient network blips, bot stops receiving messages with zero log output. **Fix PR open** [#5156].

## 6. Feature Requests & Roadmap Signals

**Likely in next version:**
- **Goal state-graph planning with recovery** (PR #5034) — The author also opened feature request #5000. This is the most substantial feature in the pipeline, adding durable execution plans with dependency state tracking and failure recovery. High maintainer investment indicates it's a priority.
- **Skill marketplace** (PR #5116, already merged) — Community-curated skill discovery and installation. Ready for the next release.
- **Custom Telegram Bot API base URL** (PR #4919) — For enterprise/self-hosted Bot API servers. Waiting with conflict marker for 15 days—may need maintainer rebase.

**Speculative (later versions):**
- **True multi-agent collaboration** (Issue #5000) — If the community design discussion converges, expect a major architecture change in v0.9+.
- **Goal permission context var scoping** (PR #5166) — Fixes inherited permission leak; small but important for security.
- **Optimistic message delivery UI** (PR #5162, already merged) — Improved user-facing reliability feedback.

## 7. User Feedback Summary

**Pain points expressed:**
- **Data loss on archive:** "files become unrecoverable after archive" (#5118) — This is a high-impact bug affecting any user who uploads media. The multi-renderer disagreement (live replay vs. consolidation) suggests a deeper architectural inconsistency.
- **PowerShell pipeline breakage:** "corrupts non-ASCII native pipeline input" (#5159) — Affects Windows users, particularly those working with CJK or accented characters.
- **Telegram silent failure:** "bot can stop receiving messages permanently" (#5156) — Production reliability issue observed in a deployed instance; hard to diagnose because logs stay silent.
- **Manual cron unreliability:** "WebUI keeps the previous Failed state" (#5163) — UI/state sync bug that undermines trust in automation features.

**Satisfaction signals:**
- 18 PRs merged in one day shows rapid response to reported bugs.
- The strict typing enforcement (#5158) was likely a community ask for quality assurance; its completion signals that maintainers are investing in codebase health.
- The skill marketplace (#5116) addresses a long-standing desire for third-party extensibility.

**Unmet need (silent):** No issues or PRs address native mobile app support, offline mode, or local-first architecture—areas where competitors like Ollama or GPT4All have stronger stories.

## 8. Backlog Watch

| Issue/PR | Days Waiting | Type | Status |
|----------|-------------|------|--------|
| [#4812] | 24 | Fix (memory KeyError) | Open, needs review |
| [#4919] | 16 | Feature (Telegram API base) | Open, conflict marker |
| [#5000] | 10 | Feature request (multi-agent) | Open, heavy discussion |
| [#5034] | 8 | Feature (goal state graph) | Open, conflict marker |
| [#5094] | 4 | Fix (OpenRouter URL) | Open, conflict marker |

**Most critical:** [#4812] "fix(memory): use .get() for role key to prevent KeyError on malformed messages" has been waiting 24 days with no maintainer comment. This is a simple defensive fix for a crash-on-malformed-data scenario. The long wait may indicate low prioritization for edge-case robustness, but it leaves a known crash path open.

**Riskiest:** [#4919] (custom Telegram API base) and [#5034] (goal state graph) both carry conflict markers, meaning they've diverged from `main`. If the maintainers don't rebase these soon, the effort to resolve conflicts will grow—potentially killing two valuable features.

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent Project Digest
**Date:** 2026-07-30  
**Data Period:** 2026-07-29 – 2026-07-30

---

## 1. Today's Overview

Hermes Agent is experiencing a **high-activity day** with 50 issues and 50 pull requests updated in the last 24 hours, indicating intense development velocity. The project maintains a healthy balance of bug fixes and feature work, though the open-to-closed ratio (49:1 for issues, 34:16 for PRs) suggests a significant **backlog accumulation** relative to resolution rate. A notable cluster of **Windows-specific issues** has emerged, particularly around update infrastructure failures and desktop rendering problems, suggesting a recent release may have introduced platform regressions. The project saw **zero new releases** today, but the volume of merged PRs (16) points to a likely forthcoming patch release.

---

## 2. Releases

**None** — No new releases were published during this reporting period.

---

## 3. Project Progress

**16 PRs were merged/closed today**, advancing several critical areas:

### Fixed: Pairing & Authentication
- **[#66761](https://github.com/NousResearch/hermes-agent/pull/66761)** (merged) — Fixed misleading `"Code"` column label in `hermes pairing list` that displayed a hash prefix instead of an approvable code, causing operator confusion.
- **[#62145](https://github.com/NousResearch/hermes-agent/pull/62145)** (merged) — Reset the failed-approval counter on successful code approval, preventing rate-lockout after legitimate approvals.
- **[#46584](https://github.com/NousResearch/hermes-agent/pull/46584)** (merged) — Returned a stable request ID for pending pairing requests, enabling dashboard and CLI approval to work correctly.

### Merged: Security & Guard Improvements
- **[#57990](https://github.com/NousResearch/hermes-agent/pull/57990)** (open) — Closed scanning gaps in Skills Guard for PowerShell (.ps1), batch (.bat/.cmd), and extensionless scripts.

### In Progress (Open PRs with Active Discussion)
- **Update Infrastructure**: [#74436](https://github.com/NousResearch/hermes-agent/pull/74436) fixes three simultaneous updater race conditions on Windows; [#74420](https://github.com/NousResearch/hermes-agent/pull/74420) extends SQLite runtime repair to `.venv` installs.
- **Kanban System**: [#74437](https://github.com/NousResearch/hermes-agent/pull/74437) enables clicking attachments to preview them; [#74432](https://github.com/NousResearch/hermes-agent/pull/74432) honors explicit requeue events after PR evidence.
- **Gateway Stability**: [#62272](https://github.com/NousResearch/hermes-agent/pull/62272) bounds the final shutdown cleanup to prevent hang during `/restart`.

---

## 4. Community Hot Topics

### Most Commented Issues

| Issue | Comments | Type | Summary |
|-------|----------|------|---------|
| [#16462](https://github.com/NousResearch/hermes-agent/issues/16462) | 12 | Feature | First-invoke approval for MCP server tools |
| [#29849](https://github.com/NousResearch/hermes-agent/issues/29849) | 10 | Bug | `no_agent=True` cronjobs ignore remote terminal backend |
| [#5820](https://github.com/NousResearch/hermes-agent/issues/5820) | 8 | Feature | Synchronous memory recall for current turn |
| [#60197](https://github.com/NousResearch/hermes-agent/issues/60197) | 7 | Bug | RuntimeError during `/exit` from MCP server shutdown |

### User Pain Points Driving Discussion

1. **Security & User Intent**: Issue [#16462](https://github.com/NousResearch/hermes-agent/issues/16462) (12 comments, 3 👍) reflects strong community demand for a **human-in-the-loop approval** step when MCP servers are first invoked. Users want explicit consent before an LLM can call newly registered MCP tools, indicating growing security awareness in the community.

2. **Terminal Backend Inconsistency**: Issue [#29849](https://github.com/NousResearch/hermes-agent/issues/29849) (10 comments, 3 👍) reveals frustration that cron jobs configured with `terminal.backend=ssh` still execute locally, bypassing user intent. This affects workflows that depend on remote execution for homelab/edge deployments.

3. **Memory Recall Latency**: Issue [#5820](https://github.com/NousResearch/hermes-agent/issues/5820) (8 comments) highlights that memory recall happens asynchronously (next turn) rather than synchronously against the current query, making recalled information potentially irrelevant. Users want **query-aware, immediate recall**.

---

## 5. Bugs & Stability

### Critical (P1) Bugs Reported Today

| Issue | Description | Fix Status |
|-------|-------------|------------|
| [#74386](https://github.com/NousResearch/hermes-agent/issues/74386) | **Windows update blocked on gateway-enabled installs** — three-layer chain (Electron→Rust→Python) fails to coordinate gateway pause/resume | No PR yet |
| [#74326](https://github.com/NousResearch/hermes-agent/issues/74326) | **Windows desktop update button can never succeed** on gateway-enabled installs — venv-blocker preflight aborts on always-running gateway | No PR yet |
| [#74339](https://github.com/NousResearch/hermes-agent/issues/74339) | **Credential-pool write-through disables after first refresh per profile** — regression of #48415/#43589, exposing users to stale credentials | No PR yet |
| [#74429](https://github.com/NousResearch/hermes-agent/issues/74429) | **Agent enters post-completion loop using stale context** after tool failure — ignores current tool result | No PR yet |

### High-Severity (P1) Bugs from Previous Days

| Issue | Description | Status |
|-------|-------------|--------|
| [#58546](https://github.com/NousResearch/hermes-agent/issues/58546) | `resolve_anthropic_token()` prefers auto-discovered Claude Code OAuth over explicit `ANTHROPIC_API_KEY` | Open, P1 |
| [#69180](https://github.com/NousResearch/hermes-agent/issues/69180) | Desktop renderer OOM crash-loop on empty chat | Open, P1 |
| [#60197](https://github.com/NousResearch/hermes-agent/issues/60197) | `RuntimeError: Event loop is closed` during `/exit` | Closed (fix merged) |

### Significant P2 Bugs

- **[#70131](https://github.com/NousResearch/hermes-agent/issues/70131)** — Emoji truncation loop fix incomplete: ✨ (U+2728) and ✅ (U+2705) still trigger the bug
- **[#74267](https://github.com/NousResearch/hermes-agent/issues/74267)** — Windows updater falsely detects running Hermes processes, aborts update
- **[#74312](https://github.com/NousResearch/hermes-agent/issues/74312)** — Substring "azure.com" match on URL path misclassifies non-Azure hosts, picks wrong credentials (security boundary)
- **[#74358](https://github.com/NousResearch/hermes-agent/issues/74358)** — Test suite silently exits after 33% completion due to `os._exit(0)` in gateway test

### Windows-Specific Regression Cluster

The **three interrelated Windows update bugs** ([#74267](https://github.com/NousResearch/hermes-agent/issues/74267), [#74326](https://github.com/NousResearch/hermes-agent/issues/74326), [#74386](https://github.com/NousResearch/hermes-agent/issues/74386)) all filed today suggest a **systemic issue in the recent updater redesign** (commits `95d303138` and `30c783589`, 2026-07-28/29). Fix PR [#74436](https://github.com/NousResearch/hermes-agent/pull/74436) addresses the race condition but does not resolve the gateway process coordination gaps.

---

## 6. Feature Requests & Roadmap Signals

### High-Engagement Features Under Discussion

| Issue | Feature | Comments | Potential Priority |
|-------|---------|----------|-------------------|
| [#16462](https://github.com/NousResearch/hermes-agent/issues/16462) | First-invoke approval for MCP tools | 12 | **Likely P2** — security-critical, aligns with recent pairing auth fixes |
| [#5820](https://github.com/NousResearch/hermes-agent/issues/5820) | Synchronous memory recall for current turn | 8 | **Possible P2** — addresses core UX gap in memory system |
| [#66238](https://github.com/NousResearch/hermes-agent/issues/66238) | Pluggable database backend (beyond SQLite) | 3 | **Long-term P3** — security-sensitive deployments, but architectural scope is large |
| [#8830](https://github.com/NousResearch/hermes-agent/issues/8830) | Xiaomi MiMo V2 TTS as native provider | 6 | **P3 niche** — strong Chinese TTS demand, but small user segment |

### Predictions for Next Version

Based on merged PRs and open work:
- **MCP security**: First-invoke approval ([#16462](https://github.com/NousResearch/hermes-agent/issues/16462)) is likely to move forward given the security focus in recent merges.
- **Windows update fix**: A hotfix release (0.17.1 or 0.19.1) is probable within days given the severity of P1 Windows update blockers.
- **Kanban UX improvements**: PRs [#74437](https://github.com/NousResearch/hermes-agent/pull/74437) (attachment preview) and [#74432](https://github.com/NousResearch/hermes-agent/pull/74432) (requeue behavior) suggest Kanban features are nearing stabilization.
- **Session compression**: PR [#72531](https://github.com/NousResearch/hermes-agent/pull/72531) (reset compression attempt counter) and [#74355](https://github.com/NousResearch/hermes-agent/pull/74355) (keep long tool turns recoverable) indicate continued investment in context management.

### Open PR: Split Runtime ([#63966](https://github.com/NousResearch/hermes-agent/pull/63966))

This 16-day-old PR proposes letting clients execute their own tools against a remote Hermes agent — a **major architectural change** that would enable on-device capabilities (phone timers, intents) while keeping the agent server-hosted. If merged, this would be the most significant feature advance in the next major release.

---

## 7. User Feedback Summary

### Expressed Pain Points

1. **Windows Update Frustration** — Multiple users report that the desktop update button is non-functional on gateway-enabled installs, requiring manual workarounds. User mitraphix-design ([#74267](https://github.com/NousResearch/hermes-agent/issues/74267)) notes the issue persists even after a full reboot, indicating a persistent lock detection bug.

2. **macOS Permission Revocation** — User vmavromatis ([#74331](https://github.com/NousResearch/hermes-agent/issues/74331)) reports that TCC grants (Full Disk Access, Accessibility, Screen Recording) are revoked on every Hermes.app reinstall due to ad-hoc signing, making the app non-functional after updates.

3. **Voice Conversation Reliability** — Users LordNikon1983 ([#73649](https://github.com/NousResearch/hermes-agent/issues/73649)) and ianarsenault-tn ([#74337](https://github.com/NousResearch/hermes-agent/issues/74337)) report that desktop voice conversations complete one turn then stop listening, requiring manual mic re-arming.

4. **Credential Confusion** — User luizfneves404 ([#58546](https://github.com/NousResearch/hermes-agent/issues/58546)) highlights that auto-discovered Claude Code OAuth tokens silently override explicit `ANTHROPIC_API_KEY` configuration, a security boundary issue that could cause unexpected billing.

### Satisfaction Signals

- **Pairing improvements** received positive attention — the merges of [#46584](https://github.com/NousResearch/hermes-agent/pull/46584) and [#66761](https://github.com/NousResearch/hermes-agent/pull/66761) address long-standing confusion about approval codes.
- The community is actively engaged in **testing edge cases**, filing detailed reproduction steps with versions and environments, suggesting a technically sophisticated user base invested in stability.

---

## 8. Backlog Watch

### Issues Needing Maintainer Attention

| Issue | Age | Type | Why It Matters |
|-------|-----|------|----------------|
| [#29849](https://github.com/NousResearch/hermes-agent/issues/29849) | 70 days | Bug (P2) | `no_agent=True` cronjobs ignore `terminal.backend` — marks 10 weeks without resolution despite 10 comments and 3 👍. Marked `needs-decision`. |
| [#5820](https://github.com/NousResearch/hermes-agent/issues/5820) | 114 days | Feature (P3) | Memory recall timing issue — 8 comments, marked `sweeper:risk-session-state`. Has been open since April without maintainer decision. |
| [#8830](https://github.com/NousResearch/hermes-agent/issues/8830) | 108 days | Feature (P3) | Xiaomi MiMo TTS — 6 comments, 2 👍. Community has provided detailed implementation suggestions. |
| [#44763](https://github.com/NousResearch/hermes-agent/issues/44763) | 47 days | Bug (P2) | `computer_use` element bounds always zero on macOS — marked `needs-repro`. Blocks spatial grounding for macOS users. |
| [#66238](https://github.com/NousResearch/hermes-agent/issues/66238) | 12 days | Feature (P3) | Pluggable database backend — 3 comments, marked `needs-decision`. Architecturally significant but no maintainer response. |

### Open PRs Requiring Review

| PR | Age | Type | Risk |
|----|-----|------|------|
| [#63966](https://github.com/NousResearch/hermes-agent/pull/63966) | 17 days | Feature (Split Runtime) | **Multiple risk labels** — session state, security boundary, compatibility, blast-moderate. This is a major architectural PR with no comments from maintainers. |
| [#57990](https://github.com/NousResearch/hermes-agent/pull/57990) | 26 days | Security | Skills Guard scanning gaps — 4 risk labels, no comments. Security fixes should typically be higher priority. |
| [#63079](https://github.com/NousResearch/hermes-agent/pull/63079) | 17 days | Bug (Session resume) | Fixes dead local endpoint issue on auto-resume. Multiple risk labels including session state. |

### Recommendation

The **Windows update crisis** (three P1 bugs filed today) should take precedence in the next 24-48 hours. Following that, the **credential priority inversion** ([#58546](https://github.com/NousResearch/hermes-agent/issues/58546), P1) and **test suite silent exit** ([#74358](https://github.com/NousResearch/hermes-agent/issues/74358)) represent significant quality and security risks. The 70-day-old [#29849](https://github.com/NousResearch/hermes-agent/issues/29849) (cron terminal backend) needs a decision to avoid further regression for remote execution users.

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw Project Digest — 2026-07-30

## 1. Today's Overview
PicoClaw shows low activity today with only 1 issue updated and 2 pull requests (both untouched for days). No new releases are available, and no PRs were merged or closed in the last 24 hours. The single open issue reports a functional bug in chat routing, while the two open PRs — one enhancing DingTalk image support and another reorganizing installation scripts — remain stalled. Overall project momentum is quiet, with no recent merges or maintainer responses to the newer issue and PR.

## 2. Releases
No new releases in the last 24 hours. The latest available version remains **0.3.1** from an earlier snapshot.

## 3. Project Progress
No pull requests were merged or closed today. Two PRs remain open:
- **#3283** — [fix(dingtalk): support picture/image message inbound](https://github.com/sipeed/picoclaw/pull/3283) — Adds inbound image message handling for DingTalk channel, including OpenAPI token caching and media download. Last updated 2026-07-29, no merge yet.
- **#1951** — [chore: move installation scripts from docs repo to here](https://github.com/sipeed/picoclaw/pull/1951) — Relocates scripts from `picoclaw_docs` into the main repo. Long-open since March, last updated 2026-07-29.

No features advanced to completion today.

## 4. Community Hot Topics
The only active conversation today is Issue **#3301**:
- **[BUG] /clear and session auto-compression don't work in chats routed to non-default agent via dispatch rules**  
  [Issue #3301](https://github.com/sipeed/picoclaw/issues/3301)  
  Reported by j-v, created 2026-07-29, 0 comments, 0 reactions.  
  **Analysis**: The user configured dispatch rules to route chats to a non-default agent (DeepSeek via OpenCode Go) on a Raspberry Pi over Discord/Telegram, but `/clear` and session auto-compression fail. This indicates a missing integration point between the dispatch rule engine and the session management layer — likely the clearing/compression logic only runs for the default agent. Underlying need: reliable memory management in multi-agent routing scenarios.

## 5. Bugs & Stability
One bug reported today:
- **Severity: High** — [Issue #3301](https://github.com/sipeed/picoclaw/issues/3301): `/clear` and session auto-compression broken for non-default agent chats via dispatch rules.  
  Impact: Users with custom routing (e.g., Raspberry Pi users leveraging multiple AI models) cannot reset or compress session history, leading to unbounded token usage and degraded performance.  
  No fix PR exists yet.

## 6. Feature Requests & Roadmap Signals
No new feature requests were filed today. The open PR **#3283** (DingTalk image support) is the most concrete pending feature enhancement. Given it was authored on 2026-07-22 and still unmerged, it may land in the next patch release if maintainers review soon. The installation scripts PR **#1951** (from March) suggests a desire for better contributor onboarding, but its extreme staleness raises questions about maintenance bandwidth.

## 7. User Feedback Summary
The single issue today reveals a real pain point: **session management fails under dispatch rules**. The user is running on Raspberry Pi and using DeepSeek via a custom provider — a fairly advanced setup. The frustration is that core chat utilities (`/clear`, auto-compression) do not respect routing configurations. This implies dissatisfaction with multi-agent support completeness. No positive feedback or satisfaction signals observed.

## 8. Backlog Watch
- **PR #1951** — [chore: move installation scripts from docs repo to here](https://github.com/sipeed/picoclaw/pull/1951)  
  Open since **2026-03-24** (4+ months), last updated 2026-07-29. Simple reorganization that would improve documentation.  
  **Risk**: Long dormancy suggests maintainer may have deprioritized or lacks capacity for infrastructure improvements.

- **PR #3283** — [fix(dingtalk): support picture/image message inbound](https://github.com/sipeed/picoclaw/pull/3283)  
  Open since **2026-07-22** (8 days), last updated 2026-07-29. No comments from maintainers.  
  **Risk**: If unaddressed, contributors may lose motivation. The feature is important for DingTalk channel users.

No open issues older than 7 days other than those linked to the PRs.

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw Project Digest — 2026-07-30

## Today's Overview
Moderate activity with 7 PRs and 2 issues updated in the last 24 hours, indicating steady development velocity. The project saw 4 PRs merged/closed, including a significant infrastructure improvement for container image distribution, a Slack thread history fix, and a zombie process fix in containers. Two open issues remain unresolved, including a potentially disruptive empty-message bug in Telegram integration. No new releases were published today.

## Releases
**None.** No new versions were released in the last 24 hours.

## Project Progress
Four PRs were merged or closed today, advancing several areas:

- **Container Infrastructure (#3150, closed)** — Core team member `gavrielc` added support for fetching a prebuilt, hardened agent container image from the NanoClaw registry, built by Echo (echo.ai), as an alternative to local image building. Building locally remains the default, no-account-required path. [PR #3150](https://github.com/nanocoai/nanoclaw/pull/3150)

- **Session Routing & Pre-compaction Notification (#2440, closed)** — `poisson-le` fixed a bug where `poll-loop` incorrectly used the first message in a restart batch (potentially an approval notification) as the reply channel, now correctly uses `session_routing`. Also added pre-compaction notification to agents. [PR #2440](https://github.com/nanocoai/nanoclaw/pull/2440)

- **Slack Thread History (#2904, closed)** — `gergokekesi` fixed a critical issue where `@mention`-mode Slack wirings only delivered the single tagged message, making all human replies in the thread invisible to the bot. [PR #2904](https://github.com/nanocoai/nanoclaw/pull/2904)

- **Container Zombie Reaping (#3060, closed)** — `tenequm` added `--init` to agent container spawn args so PID 1 properly reaps zombie processes, and corrected the documentation that had documented this gap. [PR #3060](https://github.com/nanocoai/nanoclaw/pull/3060)

## Community Hot Topics
- **#1350 — GitHub Copilot SDK as AI Backend (👍8, 3 comments)** — The highest-reacted open issue, requesting native Copilot model support beyond the current Claude-only restriction. This has been open since March 2026 with no maintainer response. [Issue #1350](https://github.com/nanocoai/nanoclaw/issues/1350)

- **#3151 — Telegram rich_message Inbound Empty (no comments)** — Brand-new issue filed yesterday, describing a likely critical bug where Telegram messages with Bot API 10.1 `rich_message` content arrive empty with no errors. [Issue #3151](https://github.com/nanocoai/nanoclaw/issues/3151)

- **#3145 — DB Migration Backfill (open)** — Fix PR adding migration 021 to provision missing channel destinations for existing messaging-group wirings. [PR #3145](https://github.com/nanocoai/nanoclaw/pull/3145)

- **#3057 — Dual-Engine Quota Fallback (open)** — A substantial feature branch adding automatic Claude→Codex quota fallback, handoff recaps, and proactive quota warnings, battle-tested in production since July 6. [PR #3057](https://github.com/nanocoai/nanoclaw/pull/3057)

- **#3149 — CLI --rw Flag for Mounts (open)** — Enhancement adding a `--rw` flag to `groups config add-mount` for read-write mounts. [PR #3149](https://github.com/nanocoai/nanoclaw/pull/3149)

## Bugs & Stability
**High severity:**
- **Telegram rich_message empty (#3151)** — Bot API 10.1 rich messages arrive completely empty (no text, attachments, or errors). This means all formatted content pasted from web pages is silently dropped. No fix PR exists yet. Filed yesterday. [Issue #3151](https://github.com/nanocoai/nanoclaw/issues/3151)

**Medium severity (recently fixed):**
- **Slack @mention thread invisibility (#2904)** — Fixed yesterday. Bot could not see full thread history when re-engaged via @mention. [PR #2904](https://github.com/nanocoai/nanoclaw/pull/2904)

**Low severity (fixed):**
- **Container zombie processes (#3060)** — Fixed yesterday. Agent containers leaked zombie processes due to missing `--init` flag. [PR #3060](https://github.com/nanocoai/nanoclaw/pull/3060)
- **Poll-loop session routing (#2440)** — Fixed yesterday. First message after container restart could be misidentified as reply channel. [PR #2440](https://github.com/nanocoai/nanoclaw/pull/2440)

## Feature Requests & Roadmap Signals
- **GitHub Copilot SDK Backend (#1350)** — Strong community demand (8 upvotes) to add Copilot models as an alternative AI backend alongside Claude. This has been open for 4+ months with no public response from maintainers. Likely for an upcoming release given high interest. [Issue #1350](https://github.com/nanocoai/nanoclaw/issues/1350)

- **Dual-Engine Quota Fallback (#3057)** — Feature branch adding Claude→Codex fallback on quota exhaustion, with handoff recaps. Already production-tested for 3+ weeks, suggesting imminent merge. [PR #3057](https://github.com/nanocoai/nanoclaw/pull/3057)

- **Prebuilt Hardened Images (#3150)** — Already merged today. Provides an alternative to local builds with pre-hardened images. [PR #3150](https://github.com/nanocoai/nanoclaw/pull/3150)

- **CLI --rw Mount Flag (#3149)** — Small usability enhancement adding read-write mount support to CLI. [PR #3149](https://github.com/nanocoai/nanoclaw/pull/3149)

## User Feedback Summary
- **Positive:** The dual-engine quota fallback feature has been successfully battle-tested on live WhatsApp deployments since July 6, indicating real-world reliability and utility for users facing Claude quota limits.
- **Negative:** The Telegram rich_message bug (#3151, filed yesterday) directly impacts users who paste formatted content from web pages — messages are silently dropped without error, a frustrating user experience.
- **Underserved Need:** The 4-month-old Copilot SDK request (#1350) with 8 upvotes represents a clear community desire for model diversity beyond the current Claude-only constraint.

## Backlog Watch
- **#1350 — GitHub Copilot SDK Backend (4 months old, 8 👍, zero maintainer response)** — The most prominent long-unanswered request. Despite strong community interest, the core team has not publicly acknowledged or assigned this feature. Risk of community frustration if not addressed. [Issue #1350](https://github.com/nanocoai/nanoclaw/issues/1350)

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

**NullClaw Project Digest — 2026-07-30**

**1. Today's Overview**
Activity on NullClaw remains moderate, with one new issue and four pull requests updated in the last 24 hours. Three PRs remain open, one was merged/closed, and no new releases were cut. The project is in a steady development phase, with contributions focused on provider integration, scheduler authentication fixes, and memory configuration improvements. A lingering bug report about scheduler authorization signals ongoing reliability concerns in multi-user or cron scenarios.

**2. Releases**
No new releases were published in the last 24 hours. The latest stable release remains unlisted; users are building from source or using the latest commit.

**3. Project Progress**
One PR was merged/closed today:
- **[PR #961](https://github.com/nullclaw/nullclaw/pull/961) (closed)**: `feat(memory)`: Added configurable `auto_recall`, `recall_limit`, and `max_context_bytes` settings under the `memory` configuration block. This feature advanced memory management by allowing users to limit context window size and disable automatic memory queries.

**4. Community Hot Topics**
The most active issue is the long-standing scheduler bug:
- **[Issue #915](https://github.com/nullclaw/nullclaw/issues/915) (open, 3 comments, 1 👍)**: User reports the scheduler fails to authenticate in both Telegram and cron environments when using an external Ollama host (Qwen3.6:27b on RTX 3090). No resolution or maintainer response yet. The number of comments and reactions shows this is a recurring pain point for users relying on scheduled tasks.

Other active PRs (all authored by *valonmulolli*, created today):
- **[PR #981](https://github.com/nullclaw/nullclaw/pull/981)**: Adds `grok-cli` provider for xAI Grok CLI, following the same spawn-per-request pattern as the existing `codex-cli` provider.
- **[PR #980](https://github.com/nullclaw/nullclaw/pull/980)**: Fixes scheduler authentication by persisting paired token to disk during `/pair`—directly addresses the underlying cause of Issue #915.
- **[PR #979](https://github.com/nullclaw/nullclaw/pull/979)**: Same feature set as merged PR #961 (auto_recall, recall_limit, max_context_bytes), likely a duplicate or re-submission.

**5. Bugs & Stability**
One active, high-severity bug reported (and unfixed):
- **[Issue #915](https://github.com/nullclaw/nullclaw/issues/915) — Scheduler unauthorized (Severity: High)**: Scheduler fails to authenticate because the token generated by `/pair` is stored only in memory and never written to disk. The cron/schedule tool then reads `paired_token` from disk and finds `null`, blocking scheduled task execution. A fix PR **#980** exists and is open; once merged, this bug should be fully resolved.

No new crashes, regressions, or security vulnerabilities were reported today.

**6. Feature Requests & Roadmap Signals**
The following feature signals appear in today’s activity:
- **Provider expansion**: PR #981 adds support for xAI Grok CLI, indicating user demand for more LLM provider backends.
- **Memory control configuration**: Merged PR #961 (and open duplicate #979) gives users granular control over memory recall behavior—likely to be included in the next minor release.
- **Scheduler reliability**: The fix in PR #980 (persist paired token) is a clear roadmap priority to address the highest-friction issue (#915).

**7. User Feedback Summary**
- **Pain points**: Scheduler authentication failure is the most common user complaint, blocking use of cron/telegram automation. Users running external Ollama hosts on Ubuntu with Qwen models are particularly affected.
- **Use cases**: The project is clearly used for automated LLM tool calling in terminal and chat environments (Telegram). The addition of Grok CLI support suggests demand for diverse model providers.
- **Satisfaction**: No explicit praise or complaints beyond the scheduler issue. The memory configuration feature (auto_recall) suggests users want to fine-tune context usage, indicating moderate engagement.

**8. Backlog Watch**
- **[Issue #915](https://github.com/nullclaw/nullclaw/issues/915) — Scheduler unauthorized (created 2026-05-15, last updated 2026-07-29)**: This is the longest-open, highest-impact issue in the project. It has been open for over two months with no maintainer response. A fix PR (#980) was submitted today but has not been merged. This should be prioritized to restore trust in scheduled task functionality.

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw Project Digest — 2026-07-30

## 1. Today's Overview

Project activity remains high with 50 issues and 50 PRs updated in the last 24 hours, though new release output is zero. The Reborn migration is clearly the dominant project concern, with many closed issues reflecting completed product-surface migration blockers and runtime policy work. However, there is a concerning number of **P1 bugs** surfacing in the QA instance (intermittent `service_unavailable`, indefinite task runs, broken stop buttons, Gemini tool-call 400s), indicating that while the architecture is advancing, production stability is under strain. The open PRs show heavy investment in CI/testing infrastructure (hermetic deterministic suites, product-surface coverage matrices, regression promotion loops) and fixes for core Reborn subsystems (skills, streaming, compaction, error recovery). Notably, 36 PRs remain open against only 14 merged/closed, suggesting a widening review pipeline.

---

## 2. Releases

**No new releases in the last 24 hours.**

The most recent release work appears to be in open PR #5598 (`chore: release`), which has been open since July 3 and proposes breaking changes in `ironclaw_common` (0.4.2 → 0.5.0) and `ironclaw_skills` (0.3.0 → 0.4.0). This release PR has **not yet merged**, suggesting the project is holding releases while the Reborn migration stabilizes.

---

## 3. Project Progress

**Merged/closed PRs today (14 total):**

| PR | Title | Notes |
|----|-------|-------|
| [#6696](https://github.com/nearai/ironclaw/pull/6696) | Collapse lifecycle state into the row-native process journal | DB migration, makes `ironclaw_processes` lifecycle authority — **major architectural change** |
| [#6346](https://github.com/nearai/ironclaw/pull/6346) | Export full-thread QA artifacts | Adds `ironclaw.thread_artifact.v1` export capability |
| [#5598](https://github.com/nearai/ironclaw/pull/5598) | Chore: release | Still open, **not merged yet** |

**Key features advanced:**

- **Process journal kernel** moved into `ironclaw_processes` (issue [#6666](https://github.com/nearai/ironclaw/issues/6666)) — the turn-run lifecycle can now be represented as a neutral process journal, separating concerns from `ironclaw_turns`
- **Durable approval-policy port** (#3891 closed) — adds approval resolution beyond exact-invocation authority, supporting persistent policy evaluation
- **No-exposure safeguards** (#3032 closed) — production-readiness safety layer preventing raw sensitive data from crossing boundaries
- **Reborn product-surface migration EPIC** (#3031 closed) — completed the tracked migration work for preserving user/operator behavior on the Reborn surface
- **Runtime presets and effective runtime policy** (#3045 closed) — adds operator-facing runtime mode selection without hand-wiring low-level grants

---

## 4. Community Hot Topics

### Most Active Issues (by comment count)

1. **[#3031](https://github.com/nearai/ironclaw/issues/3031) — [EPIC] Reborn product surface migration** (7 comments, CLOSED)
   - **Underlying need:** Track the complete migration of current IronClaw user/operator behavior onto the Reborn product surface. This was the central coordination EPIC for the Reborn effort.
   
2. **[#6524](https://github.com/nearai/ironclaw/issues/6524) — Epic: Hermetic capability and journey testing platform** (4 comments, OPEN)
   - **Underlying need:** The project cannot mechanically answer "Does every supported capability and critical user journey have deterministic, meaningful coverage?" This epic tracks building a hermetic testing platform to fill that gap.
   
3. **[#6786](https://github.com/nearai/ironclaw/issues/6786) — Gemini tool call 400s — empty "type" in functionDeclarations** (3 comments, OPEN)
   - **Underlying need:** A discovered provider compatibility bug affecting all Gemini LLM tool-calling; tool schemas ship without required `type` field.
   
4. **[#3045](https://github.com/nearai/ironclaw/issues/3045) — Reborn runtime presets** (3 comments, CLOSED)
   - **Underlying need:** Operators need understandable runtime mode selection (like `ironclaw dev` vs `ironclaw prod`) without manual configuration.

### Most Active PRs

- **[#6881](https://github.com/nearai/ironclaw/pull/6881)** — CI: publish product-surface coverage matrix (new today, S size)
- **[#6886](https://github.com/nearai/ironclaw/pull/6886)** — Complete WS9 generated state machines (new today, S size)
- **[#6740](https://github.com/nearai/ironclaw/pull/6740)** — TLS termination seam for sandbox egress proxy (XL size, 3 days open)

**Analysis:** The community is deeply engaged with Reborn migration (closed) and now pivoting to testing infrastructure and provider compatibility. The Gemini tool-calling issues (#6786, #6880) are gathering attention as they represent cross-cutting breakage for a major LLM provider.

---

## 5. Bugs & Stability

**Critical/High Severity:**

| Issue | Severity | Description | Fix PR? |
|-------|----------|-------------|---------|
| [#6786](https://github.com/nearai/ironclaw/issues/6786) | **High** | Gemini `provider_id="gemini"` — every tool call returns 400 because builtin tool schemas ship empty `type` to `functionDeclarations` | None yet |
| [#6880](https://github.com/nearai/ironclaw/issues/6880) | **High** | Gemini OAuth (`provider_id="gemini_oauth"`) — same 400s, tool schemas bypass `shape_tool_schema` entirely | None yet |
| [#6790](https://github.com/nearai/ironclaw/issues/6790) | **High** | Restart during pending Codex device authorization blocks WebUI and hides recovery code | None yet |
| [#6815](https://github.com/nearai/ironclaw/issues/6815) | **High** | Turn-state store latches "degraded" forever after one write-behind flush failure (requires restart) — observed on QA deploy | None yet (CLOSED) |
| [#6805](https://github.com/nearai/ironclaw/issues/6805) | **High** | Instance intermittently returns `service_unavailable` ~every 30 min on Railway QA instance | None yet (CLOSED) |
| [#6720](https://github.com/nearai/ironclaw/issues/6720) | **High** | Task runs indefinitely, stop button fails to cancel | None yet (CLOSED) |
| [#6879](https://github.com/nearai/ironclaw/issues/6879) | **Medium** | Automation runs execute as plain interactive chat turns when they should be unattended | None yet |
| [#6806](https://github.com/nearai/ironclaw/issues/6806) | **Medium** | Automation output doesn't appear in web chat — must navigate to Automations page | None yet (CLOSED) |
| [#6348](https://github.com/nearai/ironclaw/issues/6348) | **Medium** | Gmail extension auto-authorized without user consent after reinstall | None yet (CLOSED) |
| [#5712](https://github.com/nearai/ironclaw/issues/5712) | **Medium** | `tool_search` discloses full unnarrowed capability catalog under narrowed `CapabilityAllowSet` — information leakage | None yet (CLOSED) |

**Stability Summary:** Five P1 bugs were reported in the last 24 hours on the Railway QA instance, including persistent `service_unavailable` errors (every 30 min), indefinite task runs with non-functional stop buttons, and a write-behind flush failure that degrades the turn-state store permanently until restart. These suggest the deployment has significant reliability issues. The Gemini tool-calling breakage is provider-specific but blocks all Gemini LLM users.

---

## 6. Feature Requests & Roadmap Signals

**Strong signals for next release:**

1. **Hermetic testing platform** — [#6524](https://github.com/nearai/ironclaw/issues/6524) (OPEN epic) is getting heavy attention with 4 linked PRs today ([#6881](https://github.com/nearai/ironclaw/pull/6881), [#6883](https://github.com/nearai/ironclaw/pull/6883), [#6884](https://github.com/nearai/ironclaw/pull/6884), [#6886](https://github.com/nearai/ironclaw/pull/6886)). *Prediction: will land as CI enforcement within 1-2 weeks.*

2. **Process journal kernel** — [#6666](https://github.com/nearai/ironclaw/issues/6666) merged to `ironclaw_processes` with PR [#6696](https://github.com/nearai/ironclaw/pull/6696) (closed today). *Prediction: foundation for future turn-run lifecycle improvements.*

3. **TLS termination for sandbox egress** — [#6740](https://github.com/nearai/ironclaw/pull/6740) ports TLS intercept from sandbox trunk onto main. *Prediction: improves sandbox proxy security for channel attachments.*

4. **WebUI streaming fix** — [#6876](https://github.com/nearai/ironclaw/pull/6876) restores smooth streaming and preserves model phases. *Prediction: improves user experience for live chat responses.*

5. **Skill system usability** — [#6745](https://github.com/nearai/ironclaw/pull/6745) fixes installed and agent-authored skills being unusable (skill bodies never injected, private skill deserialization fails). *Prediction: critical for self-improvement workflows.*

**User-facing requests visible in issues:**

- [#6877](https://github.com/nearai/ironclaw/issues/6877) — Channel command gating needs activation guard and door-asymmetry decision (OPEN)
- [#3577](https://github.com/nearai/ironclaw/issues/3577) — Track v1 channel ports for legacy channels (OPEN)
- [#6745](https://github.com/nearai/ironclaw/pull/6745) — Skill usability fixes for self-improvement benchmarks

---

## 7. User Feedback Summary

**Dissatisfaction / Pain Points:**

1. **Gemini provider broken for all tool-calling** — Two independent reports (#6786, #6880) confirm that both `provider_id="gemini"` and `provider_id="gemini_oauth"` produce 400 errors on every tool call. This blocks all Gemini users from using tools/function-calling.

2. **QA instance reliability unacceptable** — The Railway deployment (`ironclaw-qa-testing-libsql`) shows intermittent `service_unavailable` errors every ~30 minutes (#6805), permanent degradation after write-behind flush failure (#6815), and tasks that run indefinitely with a broken stop button (#6720).

3. **Automation UX inconsistent** — Automations don't surface in web chat (#6806), run results are hit-or-miss with small models (#6879), and unattended runs execute as interactive chat turns.

4. **Information leakage concern** — `tool_search` under a narrowed `CapabilityAllowSet` can still disclose the full capability catalog (#5712).

5. **Gmail consent bypass** — Reinstalling the Gmail extension automatically authorizes without re-prompting OAuth consent (#6348).

**Satisfaction / Positive Signals:**

- The **Reborn migration EPIC** (#3031) closed, indicating the core product-surface migration work is tracking toward completion
- **Process journal architecture** moving to `ironclaw_processes` (#6666) shows architectural maturity
- **Testing infrastructure investment** is strong — 4 PRs today focused on hermetic deterministic testing, coverage matrices, and regression promotion

---

## 8. Backlog Watch

**Issues needing maintainer attention (long-open, important):**

| Issue | Days Open | Priority | Reason for Concern |
|-------|-----------|----------|-------------------|
| [#3577](https://github.com/nearai/ironclaw/issues/3577) | 77 days | P2 | Tracks classification and porting of ALL v1 legacy channels to Reborn — no activity since May, but blocks full migration. Suggested P2, but needs triage. |
| [#3238](https://github.com/nearai/ironclaw/issues/3238) | 88 days | P1 (design) | Reborn cancellation semantics design — closed but the PR for actual implementation may be stalled. Critical for task management reliability (#6720 relates). |
| [#6805](https://github.com/nearai/ironclaw/issues/6805) | <2 days | bug_bash_P1 | QA instance unavailable every 30 min — CLOSED but no fix PR linked. Risk of production regression. |
| [#6786](https://github.com/nearai/ironclaw/issues/6786) | <2 days | qa-bug | Gemini tool-call 400s — OPEN with no linked fix. Blocks all Gemini users. |
| [#6880](https://github.com/nearai/ironclaw/issues/6880) | <1 day | (unlabeled) | Gemini OAuth same 400 issue — NEW today, same root cause as #6786. |

**Notable:** The open PR [#5598](https://github.com/nearai/ironclaw/pull/5598) (`chore: release`) has been open for **27 days** (since July 3) with breaking changes to `ironclaw_common` and `ironclaw_skills`. The release pipeline appears blocked, likely waiting for Reborn migration to stabilize. This is the **longest-remaining open PR** with significant impact.

---

*Generated from GitHub data retrieved 2026-07-30. All links use `nearai/ironclaw` repository. Activity counts may vary slightly from Data Overview total due to deduplication and filtering.*

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

# LobsterAI Project Digest — 2026-07-30

## 1. Today's Overview
The project is steadily active, with 15 PRs updated in the last 24 hours—13 of which were merged or closed today. No new releases were published, and no new issues were reported. The development cadence is focused on polishing the Cowork and OpenClaw areas, with significant bugfixing and feature refinements. The open PR count remains low (2), indicating maintainers are effectively triaging incoming work. A major release artifact (PR #2407) was closed, suggesting the team is consolidating for a new publish window.

## 2. Releases
No new releases were published in the last 24 hours.

## 3. Project Progress
13 PRs were merged or closed today, reflecting substantial cleanup and stabilization. Notable items:

- **Release consolidation**: PR #2407 (Release/2026.7.24) was closed, bundling multiple area changes across renderer, build, docs, main, OpenClaw, skills, cowork, and artifacts.
- **Cowork side-chat enhancements**:
  - PR #2405 — *feat(cowork): add selected text tags to side chat* (merged) — adds removable context tags, direct sending, follow-up editing, and state safeguards.
  - PR #2406 — *fix(cowork): improve side chat input handling* (merged) — accumulates selected text excerpts, removes product-level length limits, and preserves bounded context.
- **Bugfixes**:
  - PR #2376 — Export modal rendered above sidebar via body portal (stacking context fix).
  - PR #2364 — Prevents scroll jumps on session refresh by scoping refresh events to session ID.
  - PR #2363 — Eliminates periodic IM message flicker by improving history window reconciliation.
  - PR #2360 — Preserves local callback across login retries (auth stability).
  - PR #2355 — Aligns Windows caption button hover colors with sidebar controls.
  - PR #2347 — Reduces update check interval from 12h to 2h for faster notifications.
  - PR #2346 — Opens email diagnostics in a new chat to avoid stale history overrides.
- **OpenClaw refactoring**:
  - PR #2404 — *Refactor/kimi k3 auto only compat* (merged) — compatibility adjustments.
  - PR #2403 — Reverts the client-side "run-safety-contract" gate for no-progress token burn after review-blocking issues were found.
- **Long-standing fixes closed today**:
  - PR #1322 — True LRU eviction for LLM memory judge cache (fixes documented-LRU-behavior mismatch).
  - PR #1232 — Scheduled task first-run result not pushed to UI (Chinese-language fix).

## 4. Community Hot Topics
- **PR #1277** (open) — `chore(deps-dev): bump the electron group` (dependabot). Updates Electron from 40.2.1 to 43.2.0. This is a major dependency upgrade and is still open, likely awaiting review and compatibility testing. *🔗 [View PR #1277](https://github.com/netease-youdao/LobsterAI/pull/1277)*
- **PR #2403** (closed today) — Reverted a client-side safety-contract feature after review found "release-blocking issues" (receipt identity keying, false-success followups, compaction runId handling, byte-accounting mismatches). This generated significant internal discussion and reflects maintainers' high bar for correctness. *🔗 [View PR #2403](https://github.com/netease-youdao/LobsterAI/pull/2403)*

No issues with high comment or reaction counts were observed in the last 24h.

## 5. Bugs & Stability
All bugs reported today have fix PRs that were merged. Severity ranking:

- **High**: PR #2406 — Side chat input handling was accumulating state incorrectly and had no length limit safeguards. Fixed by adding bounded context and transport safety checks.
- **Medium**: PR #2376 — Export modal hidden behind sidebar due to stacking context. Fixed via body portal.
- **Medium**: PR #2364 — Scroll jumps on session refresh caused UX disruption. Fixed by scoping refresh events.
- **Medium**: PR #2363 — Periodic IM message flicker degraded cowork reliability. Fixed by improving reconciliation logic.
- **Medium**: PR #2355 — Windows caption button hover colors mismatched UI theme. Fixed.
- **Low**: PR #2346 — Email diagnostics opening in stale chat instead of new chat. Fixed.

Additionally, a major regression (PR #2403 reversion) was caught during review and rolled back before reaching users.

## 6. Feature Requests & Roadmap Signals
- **Side-chat context enrichment** (PR #2405) — showing selected text as removable tags with editing and sending is a clear UX improvement. Users likely requested better context control during cowork sessions. Expect this in the next release.
- **Faster update checks** (PR #2347) — interval reduced from 12h to 2h. Reflects user desire for earlier update notifications.
- **True LRU eviction** (PR #1322, closed today) — Cache behavior alignment shows attention to memory management under load.
- **OpenClaw feature reversion** (PR #2403) suggests the team is cautious about deploying novel safety contracts. The refactoring in PR #2404 (Kimi K3 auto-only compat) signals continued work on model compatibility, likely targeting a stable release with minimal risk.

## 7. User Feedback Summary
No explicit user feedback is captured in this data. However, patterns from PRs imply:
- **Pain point**: Side-chat interactions losing context or having length limits (addressed by PR #2406).
- **Pain point**: Export modal being hidden behind sidebar (PR #2376).
- **Pain point**: Scroll instability during session refresh in cowork (PR #2364).
- **Satisfaction signal**: Active merger of UX polish (caption button colors, update interval, email chat isolation) indicates maintainers are responsive to polish-level complaints.
- **Satisfaction signal**: Reversion of a risky feature (PR #2403) rather than shipping with known bugs shows a user-trust-first approach.

## 8. Backlog Watch
- **PR #1277** — `chore(deps-dev): bump the electron group across 1 directory with 2 updates` (last updated 2026-07-29, open since 2026-04-02). This dependency update spans a major Electron version jump (40 → 43) and needs maintainer review for compatibility. The 3.5-month open status is a concern—especially if it blocks other Electron-dependent work. *🔗 [View PR #1277](https://github.com/netease-youdao/LobsterAI/pull/1277)*
- **PR #1232** — `fix(scheduledTask): 修复定时任务首次执行结果不推送到 UI` (Chinese description: fix scheduled task first-run result not pushed to UI). Open since 2026-04-01, updated 2026-07-29 but still no decision. This is a functional bug in a core feature (scheduled tasks) and warrants prioritization. *🔗 [View PR #1232](https://github.com/netease-youdao/LobsterAI/pull/1232)*

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

# Moltis Project Digest — 2026-07-29

## 1. Today's Overview
The Moltis project remains in a highly active development phase, with six pull requests updated in the last 24 hours and one issue resolved. Four PRs remain open, indicating ongoing work across distinct features: an ACP agent interface, Slack integration improvements, instrumentation infrastructure, and privilege enforcement. The maintainer team (primarily `penso`) is driving multiple parallel streams, suggesting good cadence and capacity. No new releases were published today. Overall project health appears strong, with a focus on production hardening, observability, and security boundaries.

## 2. Releases
No new releases were published today. The latest stable release remains unchanged.

## 3. Project Progress
**Two PRs were merged/closed today:**

- **#1173 [feat(pwa)]: Make push notifications reliable and non-disruptive** (merged) — Implements robust PWA notifications with re-alerting for new messages in ongoing chat threads, privacy-safe titles, rich formatting stripping, and cross-tab unread badge management. This closes a long-standing reliability gap for mobile/web users.

- **#1172 [fix(web)]: Hide archived cron sessions by default** (merged) — Fixes archiving a cron session having no visible effect (Issue #1111) by applying the shared archived-session preference to the Cron tab. Includes Playwright regression tests for the hide/show/re-hide workflow.

**Key features advanced in open PRs:**
- ACP (Agent Communication Protocol) stdio agent exposure with session isolation and bounded resources
- Slack per-message acknowledgment reactions with lifecycle safety under queueing and cancellation
- Langfuse v4 / OTLP instrumentation and end-user reaction feedback collection
- Operator-based privilege enforcement for sensitive commands and host tools

## 4. Community Hot Topics
No issues or PRs received significant community comments or reactions today. Activity remains dominated by maintainer contributions.

**Notable high-impact PRs under active review:**
- **#1169** — ACP stdio agent exposure (largest structural change, impacts API surface)
- **#1174** — Instrumentation and feedback collection (involved integration with multiple backends)
- **#1166** — Slack Block Kit and acknowledgment phases (builds on recently merged #1165)

The underlying need appears to be making Moltis interoperable (ACP), observable (instrumentation), and more user-friendly in Slack (reactions & Block Kit).

## 5. Bugs & Stability
**One bug was closed today:**
- **#1111** (severity: medium) — Archiving a cron session had no visible effect in UI. User reported that the archive action appeared to do nothing. *Fix PR #1172 was merged*, which hides archived cron sessions by default while keeping the "Show archived sessions" toggle available.

**No new bugs were reported in the last 24 hours.** No crashes, regressions, or security vulnerabilities were disclosed.

## 6. Feature Requests & Roadmap Signals
No new feature requests were filed today. However, the following in-progress features signal strong roadmap direction:
- **ACP protocol support (#1169)** — Points toward integration with agent ecosystems and tool orchestration standards
- **Langfuse/OTLP instrumentation (#1174)** — Indicates enterprise-grade observability is a priority, likely for production deployments
- **Operator privilege separation (#1170)** — Suggests multi-tenant or team usage is being designed for explicitly
- **Slack Block Kit (#1166)** — Shows investment in Slack as a first-class channel beyond simple messaging

**Prediction for next release:** Most likely includes ACP agent mode, Slack reactions/Block Kit, instrumentation export, and the privilege enforcement fix. PWA notification improvements are already merged.

## 7. User Feedback Summary
No direct user feedback (comments, reactions, or new issues) was recorded in the last 24 hours. The closed bug #1111 indicates a user pain point around UI feedback for archival actions—this has been addressed in the merged PR #1172. The PWA notification work (#1173) suggests that reliability and non-disruptiveness of notifications were user pain points. Overall, the project appears to be user-driven in its maintenance cycle, with recent fixes targeting real UI/UX annoyances.

## 8. Backlog Watch
- **Issue #1111** was the only open/active issue in the last 24h and has now been closed via PR #1172.
- No long-unanswered issues or PRs were identified. The oldest updated item (Issue #1111) was created 2026-06-06 and was resolved.
- All open PRs (#1169, #1166, #1174, #1170) have received recent updates (within 1-3 days), indicating maintainer engagement.

**No items require maintainer attention at this time.**

---

*All data sourced from [moltis-org/moltis](https://github.com/moltis-org/moltis) as of 2026-07-29. Generated 2026-07-30.*

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

# CoPaw Project Digest
**Date:** 2026-07-30  
**Source:** GitHub (github.com/agentscope-ai/CoPaw)  
**Project:** QwenPaw (Agent Desktop & Cloud Platform)

---

## Today's Overview

CoPaw (QwenPaw) showed **high activity** on July 30, 2026, with **25 updated issues** (21 open/active, 4 closed) and **50 updated pull requests** (35 open, 15 merged/closed) in the last 24 hours. No new releases were published today. The community is actively contributing, with **5 first-time contributors** submitting PRs (#6562, #6531, #6486, #6543, #6563), though a CI workflow bug (#6563) is blocking fork-based contributions. The project's focus remains on stability fixes (MCP reconnection, context compression bugs, Windows installer issues) alongside significant feature work, including desktop GUI automation (#6424), creator plugin enhancements (#6556), and unified provider model metadata (#6302).

---

## Releases

**No new releases today.** The latest available version remains **QwenPaw 2.0.1** (Desktop) and **v2.0.0.post3** (server). Users calling `qwenpaw --version` should verify their local installation.

---

## Project Progress

**15 PRs were merged or closed today**, including notable improvements:

| PR | Author | Description | Status |
|---|---|---|---|
| [#6487](https://github.com/agentscope-ai/CoPaw/pull/6487) | `qbc2016` | Restrict import-local source path to prevent arbitrary directory exfiltration | **Merged** (security fix) |
| [#6496](https://github.com/agentscope-ai/CoPaw/issues/6496) | `YMG001` | Legacy plugin version compatibility — implicit max version derivation | **Closed** (bug acknowledged) |
| [#6056](https://github.com/agentscope-ai/CoPaw/issues/6056) | `rayrayraykk` | Background offload kills subprocess immediately | **Closed** (fix applied) |
| [#6245](https://github.com/agentscope-ai/CoPaw/issues/6245) | `feng183043996` | Session permanently blocked when shell command exceeds coordinator deadline | **Closed** (regression fix) |

**Key features advanced (still open):**
- **[#6424](https://github.com/agentscope-ai/CoPaw/pull/6424)** — Native desktop GUI automation for Windows & macOS (accessibility-first + Tauri control mode), under human review
- **[#6556](https://github.com/agentscope-ai/CoPaw/pull/6556)** — Creator plugin iteration: creation checkpoints, home redesign, media recovery, export/import
- **[#6302](https://github.com/agentscope-ai/CoPaw/pull/6302)** — Unified provider discovery, model metadata, routing, and agent controls (addresses #6167)
- **[#6269](https://github.com/agentscope-ai/CoPaw/pull/6269)** — Workspace checkpoint management via shadow Git store
- **[#6398](https://github.com/agentscope-ai/CoPaw/pull/6398)** — Reranker support for ReMe memory search (backend)
- **[#6553](https://github.com/agentscope-ai/CoPaw/pull/6553)** — App Center redesign split into My Apps/Official Apps/App Market tabs
- **[#6527](https://github.com/agentscope-ai/CoPaw/pull/6527)** — Cancellation-safe lifecycle hooks (ON_CANCEL) for persisting interrupted state

---

## Community Hot Topics

The following issues and PRs drew the most engagement in the last 24 hours:

| Issue/PR | Type | Comments | Summary |
|---|---|---|---|
| [#6537](https://github.com/agentscope-ai/CoPaw/issues/6537) | Bug | **9** | Skill tags disappear on restart — regression of #3270. Tags save to `skill.json` but are lost during manifest reconciliation on startup |
| [#6460](https://github.com/agentscope-ai/CoPaw/issues/6460) | Bug (Chinese) | **4** | High CPU usage on Edge+Wayland at homepage with large result sets / WebSocket push triggering | 
| [#6524](https://github.com/agentscope-ai/CoPaw/issues/6524) | Bug | **3** | MCP backend restart breaks client connection — must execute `list mcp` manually to restore |
| [#6542](https://github.com/agentscope-ai/CoPaw/issues/6542) | Enhancement | **3** | Auto-archive mechanism requested to prevent chat history loss on crash |
| [#6056](https://github.com/agentscope-ai/CoPaw/issues/6056) | Bug | **3** | Background offload kills subprocess immediately (CLOSED) |

**Underlying need analysis:**  
The most active issues reveal three persistent user pain points: **(1)** state persistence failures (skill tags, MCP sessions, chat history) — users want QwenPaw to survive restarts and crashes without losing configuration or conversation data; **(2)** performance degradation under load (CPU, large sessions, scrolling); **(3)** integration reliability with external services (MCP servers, Feishu audio).

---

## Bugs & Stability

### Critical / Blocking

| Issue | Severity | Description | Fix PR |
|---|---|---|---|
| [#6537](https://github.com/agentscope-ai/CoPaw/issues/6537) | **High** | Skill tags disappear on restart (regression of #3270) | None yet |
| [#6534](https://github.com/agentscope-ai/CoPaw/issues/6534) | **High** | NSIS Windows installer infinite loop — matches its own process as "still running" | None yet |
| [#6541](https://github.com/agentscope-ai/CoPaw/issues/6541) | **High** | Scroll context compression uses `role=user` instead of `role=system` — causes `MODEL_EXECUTION_ERROR` on DeepSeek | None yet |
| [#6524](https://github.com/agentscope-ai/CoPaw/issues/6524) | **High** | MCP backend restart breaks client — stale `mcp-session-id` | None yet |
| [#6557](https://github.com/agentscope-ai/CoPaw/issues/6557) | **High** | MCP tool names starting with `-` violate OpenAI function calling spec — cause 400 errors | **Yes** — [#6561](https://github.com/agentscope-ai/CoPaw/pull/6561) |
| [#6555](https://github.com/agentscope-ai/CoPaw/issues/6555) | **Medium** | Dream/memory compression misses early-session events when context scrolls out before daily md generation | None yet |
| [#6510](https://github.com/agentscope-ai/CoPaw/issues/6510) | **Medium** | Feishu channel URL-encodes Chinese file paths — files not found | None yet |

### Moderate / Annoying

| Issue | Severity | Description | Fix PR |
|---|---|---|---|
| [#6533](https://github.com/agentscope-ai/CoPaw/issues/6533) | **Medium** | `/mission` command raises `TypeError` — missing `verification_instructions` param | **Yes** — [#6535](https://github.com/agentscope-ai/CoPaw/pull/6535) & [#6562](https://github.com/agentscope-ai/CoPaw/pull/6562) |
| [#6529](https://github.com/agentscope-ai/CoPaw/issues/6529) | **Medium** | ACP `new_session` response missing `models` field — external clients can't discover models | **Yes** — [#6531](https://github.com/agentscope-ai/CoPaw/pull/6531) |
| [#6558](https://github.com/agentscope-ai/CoPaw/issues/6558) | **Medium** | Multi-chat session UI data integrity — messages lost on switch, instructions drift | None yet |
| [#6559](https://github.com/agentscope-ai/CoPaw/issues/6559) | **Medium** | Unwanted session forking — no parent-child grouping, chaotic session list | None yet |
| [#6544](https://github.com/agentscope-ai/CoPaw/issues/6544) | **Medium** | Feishu audio messages silently fail transcription in 2.x | None yet |
| [#6547](https://github.com/agentscope-ai/CoPaw/issues/6547) | **Low** | Misplaced cursor UI in Coding Mode editor | None yet |
| [#6549](https://github.com/agentscope-ai/CoPaw/issues/6549) | **Low** | Desktop App input box hidden behind scroll — UI layout issue on high-DPI | None yet |

### CI / Infrastructure

| Issue | Severity | Description |
|---|---|---|
| [#6563](https://github.com/agentscope-ai/CoPaw/issues/6563) | **Blocking (contributors)** | `real-behavior-proof.yml` workflow fails on all fork PRs — "Resource not accessible by integration" |

---

## Feature Requests & Roadmap Signals

### Features requested today:

| Issue | Author | Description | Likelihood for Next Release |
|---|---|---|---|
| [#6560](https://github.com/agentscope-ai/CoPaw/issues/6560) | `aEgoist` | Chat UX improvements: copy, undo, stop, mission mode, scroll performance, session ID, context transfer | **High** — addresses core UX gaps |
| [#6475](https://github.com/agentscope-ai/CoPaw/issues/6475) | `One-sixth` | `notice_after_complete` tool — Agent can start long-running tasks, reply to other questions, then push completion notification | **Medium** — aligns with task management roadmap |
| [#6421](https://github.com/agentscope-ai/CoPaw/issues/6421) | `ook826092-cloud` | QQ channel streaming output support | **Medium** — channel parity improvement |
| [#6542](https://github.com/agentscope-ai/CoPaw/issues/6542) | `fengye-2006` | Auto-archive mechanism to prevent crash-induced chat loss | **High** — addresses critical data loss |
| [#6551](https://github.com/agentscope-ai/CoPaw/issues/6551) | `StevenZhang2002` | Align Aliyun model catalog with official website | **Low** — data correction |

### Predictions for next release:

1. **MCP stability improvements** — merging #6561 (tool name fix) and addressing #6524 (session reuse)
2. **Chat history resilience** — auto-archive (#6542) likely follows from high community demand
3. **Session management UX** — #6560's UX improvements (copy, undo, stop) address fundamental interaction gaps
4. **Windows installer fix** — #6534 is a blocking issue for Windows adoption

---

## User Feedback Summary

### Pain Points
- **Data loss anxiety**: Multiple users report session history loss on crash (#6542), skill tag loss on restart (#6537), and message loss during session switching (#6558)
- **Integration fragility**: MCP server restarts break connections silently (#6524), Feishu channel corrupts Chinese paths (#6510), Dream memory misses important early-session events (#6555)
- **UI/UX frustration**: Desktop App input box hidden (#6549), no copy/undo/stop (#6560), chaotic session forking (#6559), misplaced cursor in code editor (#6547)
- **Platform-specific issues**: Windows installer broken (#6534), high CPU on Edge+Wayland (#6460), deprecated OneBot/QQ integration (#6543)

### Satisfaction Signals
- **Active community contributions**: 5 first-time contributors in a single day
- **Feature appetite**: Users requesting advanced capabilities (desktop GUI automation, cancellation hooks, unified providers) indicate mature adoption
- **Response from maintainers**: Multiple fix PRs in flight for reported bugs (#6535, #6561, #6531, #6543)

---

## Backlog Watch

### Issues needing maintainer attention:

| Issue | Date | Subject | Reason for Concern |
|---|---|---|---|
| [#6421](https://github.com/agentscope-ai/CoPaw/issues/6421) | 2026-07-24 | QQ channel streaming output — 6 days without maintainer response | No comments from team |
| [#6475](https://github.com/agentscope-ai/CoPaw/issues/6475) | 2026-07-26 | `notice_after_complete` tool — 4 days, only user discussion | No maintainer acknowledgment |
| [#6544](https://github.com/agentscope-ai/CoPaw/issues/6544) | 2026-07-29 | Feishu audio transcription silent failure | No response yet (1 day) |

### Stale high-value PRs needing review:

| PR | Date | Subject | Priority |
|---|---|---|---|
| [#6325](https://github.com/agentscope-ai/CoPaw/pull/6325) | 2026-07-22 | Built-in tool docs in Console | **Medium** — UX improvement |
| [#6383](https://github.com/agentscope-ai/CoPaw/pull/6383) | 2026-07-23 | Unelevated sandbox for Windows | **High** — security + Windows parity |
| [#6424](https://github.com/agentscope-ai/CoPaw/pull/6424) | 2026-07-24 | Desktop GUI automation (Windows/macOS) | **High** — major feature |

### CI blocker:
- [#6563](https://github.com/agentscope-ai/CoPaw/issues/6563) — Fork PR CI failure is **blocking all external contributors**. This warrants immediate maintainer attention.

---

*Digest generated from agentscope-ai/CoPaw GitHub data as of 2026-07-30.*

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# ZeroClaw Project Digest — 2026-07-30

## Today's Overview
ZeroClaw continues at a high velocity with **50 issues and 50 PRs updated in the last 24 hours**, of which 9 issues and 5 PRs were closed/merged. The project is in a **intensive design and refactoring phase**, with 7 new high-risk RFCs proposed in the last 48 hours alone (Issues #9487, #9488, #9506, #9507, #9508, #9509, #9511). A major toolchain bump to Rust 1.97.1 is underway (PR #9527). The backlog of open RFCs awaiting maintainer ratification is growing, particularly around memory architecture (#9048, #9103) and session lifecycle (#9487). No new releases were cut today.

## Releases
**None.** No new releases were published in the last 24 hours.

## Project Progress
**5 PRs were merged or closed today:**

| PR | Description | Impact |
|---|---|---|
| [#9418](https://github.com/zeroclaw-labs/zeroclaw/pull/9418) | **fix(mcp): multiplex stdio calls** — Fixes response ID mismatches and hidden replay of unknown outcomes in stdio MCP servers | **Critical stability fix** for concurrent MCP tool execution |
| [#9299](https://github.com/zeroclaw-labs/zeroclaw/pull/9299) | **fix(config): default `context_compression.enabled` to false** — Resolves a misleading default that was silently inert since runtime compressor was removed | **Cleanup** — eliminates configuration surface that does nothing |
| [#9235](https://github.com/zeroclaw-labs/zeroclaw/issues/9235) | **ci: npm audit fix** — Closed the 2026-07-21 npm advisory | **Security** — 3 high/critical npm vulnerabilities resolved |
| [#9239](https://github.com/zeroclaw-labs/zeroclaw/issues/9239) | **fix(config): `config patch --json` error paths** — Two failure paths were emitting bare `anyhow::Error` instead of structured JSON | **UX fix** — consistent structured error output |
| [#9422](https://github.com/zeroclaw-labs/zeroclaw/issues/9422) | **fix(config): Windows compilation** — `EnvValueGuard` was gated on `cfg(unix)` only, broke `cargo test` on Windows | **Platform fix** — unblocked Windows CI |

Additionally, **feature work** continues on:
- **Email threading improvements** (PR #9523) — adds proper RFC 5322 References chains and Reply-To preservation
- **CPAL audio library upgrade** (PR #9547) — CPAL 0.15.3 → 0.18.1 for Voice Wake
- **Runtime Rust version bump** (PR #9527) — workspace-wide to 1.97.1

## Community Hot Topics

### Most Discussed Issues (by comment count)

1. **[#9048](https://github.com/zeroclaw-labs/zeroclaw/issues/9048) — RFC: Separate conversation history from agent-curated long-term memory** (11 comments)
   - **Need:** Users report that session history and long-term memory are still mixed in runtime code despite being documented as separate lifecycle concepts. The `MemoryCategory::Conversation` implementation writes conversational turns into the general memory backend, defeating the separation.
   - **Underlying concern:** Memory pollution — agent-curated knowledge gets contaminated with raw conversation turns, reducing retrieval quality.

2. **[#9127](https://github.com/zeroclaw-labs/zeroclaw/issues/9127) — RFC: Abstract a `KeySource` trait for master-key material** (8 comments)
   - **Need:** 93 config fields use `#[secret]` annotation with ChaCha20-Poly1305 AEAD encryption, but there is no unified way to classify master-key material by source (file, env, TPM, KMS).
   - **Underlying concern:** Enterprise deployment requirements — different deployment forms need different key provisioning.

3. **[#4830](https://github.com/zeroclaw-labs/zeroclaw/issues/4830) — HMAC tool execution receipts for hallucination detection** (7 comments, **closed**)
   - **Need:** Cryptographic receipts for tool outputs to enable runtime verification that results are genuinely from tool execution, not model hallucination.
   - **Underlying concern:** Trustworthiness of agent outputs in regulated environments — users need proof that a tool was actually invoked.

4. **[#8603](https://github.com/zeroclaw-labs/zeroclaw/issues/8603) — RFC: OpenAI Chat Completions compatibility adapter** (6 comments)
   - **Need:** Third-party frontends (Open WebUI, LobeChat) speak OpenAI API format; ZeroClaw only offers WebSocket and webhooks. Each integration must build a custom adapter.
   - **Underlying concern:** Ecosystem lock-in — ZeroClaw cannot be used as an agent backend by popular chat UIs without custom middleware.

5. **[#9487](https://github.com/zeroclaw-labs/zeroclaw/issues/9487) — RFC: Runtime-owned conversation sessions** (4 comments, **filed 2026-07-28**)
   - **Need:** Make `zeroclaw-runtime` the single owner of conversation execution and session lifecycle, with adapters for WebSocket, Web dashboard, channels, and ACP.
   - **Underlying concern:** Architectural fragmentation — each transport/surface currently manages its own session state, causing inconsistency.

6. **[#9488](https://github.com/zeroclaw-labs/zeroclaw/issues/9488) — RFC: Unified attachment architecture** (4 comments, **filed 2026-07-28**)
   - **Need:** Web chat and channels handle attachments differently; security policies for file uploads are duplicated.
   - **Underlying concern:** Security and UX inconsistency — attachment handling needs a single pipeline with uniform sanitization.

## Bugs & Stability

### Critical (S1 — Workflow Blocked)
| Issue | Description | Fix PR? |
|---|---|---|
| [#9186](https://github.com/zeroclaw-labs/zeroclaw/issues/9186) | **MCP stdio response ID not matched** — three interacting defects: response ID ignored, 30s hard timeout vs 180-600s tool budget, Mutex held for entire call. **CLOSED** | [[#9418]](https://github.com/zeroclaw-labs/zeroclaw/pull/9418) merged |
| [#9340](https://github.com/zeroclaw-labs/zeroclaw/issues/9340) | **CLI cron jobs silently discard output** — `delivery.mode = "none"` hardcoded; agent runs but output goes nowhere | Open |
| [#9362](https://github.com/zeroclaw-labs/zeroclaw/issues/9362) | **Browser tool screenshot: arbitrary file write escape** — `path` parameter not validated against workspace policy | [[#9362]](https://github.com/zeroclaw-labs/zeroclaw/pull/9362) open |

### High (S2 — Degraded Behavior)
| Issue | Description | Fix PR? |
|---|---|---|
| [#6724](https://github.com/zeroclaw-labs/zeroclaw/issues/6724) | **Enabled Signal/Voice Call with empty credentials causes supervisor crashloop** — every ~2 seconds | Open |
| [#9486](https://github.com/zeroclaw-labs/zeroclaw/issues/9486) | **High-entropy detector redacts Solana wallet addresses** — `high_entropy_tokens=false` does not stop it on channel path | Open |
| [#9506](https://github.com/zeroclaw-labs/zeroclaw/issues/9506) | **Email channel cannot preserve CC recipients or send Reply All** — only single-recipient replies | [[#9523]](https://github.com/zeroclaw-labs/zeroclaw/pull/9523) open |
| [#9278](https://github.com/zeroclaw-labs/zeroclaw/issues/9278) | **`context_compression.enabled` defaults true while runtime ignores it** — misleading default, **CLOSED** | [[#9299]](https://github.com/zeroclaw-labs/zeroclaw/pull/9299) merged |
| [#8948](https://github.com/zeroclaw-labs/zeroclaw/issues/8948) | **Stdio MCP servers pile up as zombie processes** — `kill_on_drop(true)` insufficient for pooled servers | [[#8948]](https://github.com/zeroclaw-labs/zeroclaw/pull/8948) open |

### Medium (S3 — Minor)
| Issue | Description | Fix PR? |
|---|---|---|
| [#9462](https://github.com/zeroclaw-labs/zeroclaw/issues/9462) | **zeroclaw-plugins unit tests never execute in CI** — gated behind `plugins-wasmtime` feature flag | Open |
| [#9422](https://github.com/zeroclaw-labs/zeroclaw/issues/9422) | **zeroclaw-config unit tests cannot compile on Windows** — **CLOSED** | Fixed |

### Key Security Note
The **browser tool arbitrary file write** (Issue #9362) is a high-severity vulnerability. A fix PR exists and is under review. Additionally, the **high-entropy detector redacting Solana addresses** (Issue #9486) is a significant usability issue for crypto-related use cases.

## Feature Requests & Roadmap Signals

### Strongest Signals for Next Release

1. **OpenAI Chat Completions adapter** (Issue #8603) — 6 comments, high demand from ecosystem integration perspective. Would unlock Open WebUI, LobeChat, and custom integrations. Likely **v0.9 target**.

2. **Runtime-owned conversation sessions** (Issue #9487) — Filed 2026-07-28, already 4 comments. Represents a major architectural change. If accepted, would be a **v1.0 architectural foundation**.

3. **Unified attachment architecture** (Issue #9488) — Companion to #9487. Shared attachment handling pipeline with uniform security. Also **v1.0 candidate**.

4. **Mixture-of-Agents (MoA) virtual provider** (Issue #8568) — Running judge+reference models in parallel with aggregator. 3 comments, design is mature. Could be **v0.9 feature**.

5. **Realtime speech-to-speech channel (Gemini Live)** (Issue #8780) — 4 comments, detailed RFC. Could be **v0.9 or v1.0**.

6. **A2A outbound client (A2ATool)** (Issue #9106) — 4 comments. Allows agents to proactively call external A2A agents. **v0.9 target**.

### Emerging Themes
- **Plugin architecture** — Moving channels/tools from compile-time features to WASM plugins (Issue #8850 tracker)
- **Advisory macOS/Windows tests** (PR #9398) — Platform expansion beyond Linux
- **Diff-aware CI preflight** (Issue #9509) — CI efficiency improvements
- **Crate dependency enforcement** (Issue #9507) — Architecture governance

## User Feedback Summary

### Pain Points Expressed

1. **Memory mixing** (Issue #9048): "conversation history and long-term memory [are] still mixed in important paths" — affects all users relying on memory for agent quality.

2. **Cron output silently lost** (Issue #9340): "agent job runs on schedule, calls its tools, and then discards its output. The run is recorded as ok, so nothing indicates the result went nowhere." — impacts automation users.

3. **Solana wallet addresses redacted** (Issue #9486): Agent can't state a wallet address via Telegram despite `high_entropy_tokens=false`. Directly impacts crypto/DeFi use cases.

4. **Email channel limited** (Issue #9506): Cannot preserve CC recipients or send Reply All. Users accustomed to email threading find ZeroClaw's email integration inadequate.

5. **MCP timeout mismatch** (Issue #9186, **closed**): Stdio MCP had 30s hard timeout vs 180-600s tool budget — tool-heavy workflows were broken. Users reported S1 severity.

6. **Provider failure diagnostics opaque** (PR #9056): Terminal failures surfaced as generic "All model_providers/models failed" — users couldn't distinguish API key rejection from server downtime.

### Use Cases Revealed
- **Crypto wallet interaction** via MCP servers (Issue #9486)
- **Multi-platform deployment** requiring Windows compilation (Issue #9422, fixed)
- **Third-party frontend integration** (Issue #8603 — Open WebUI, LobeChat)
- **Automated cron workflows** with delivery (Issue #9340)
- **Inter-agent collaboration** via A2A protocol (Issue #9106)

### Satisfaction Signals
- HMAC tool execution receipts (Issue #4830) was **closed** with 7 comments — suggests community interest in cryptographically verifiable tool execution
- High engagement on architectural RFCs (Issues #9487, #9488 filed 2 days ago, already 4 comments each) — community actively shaping v1.0 architecture

## Backlog Watch

### Issues Needing Maintainer Attention

| Issue | Age | Why Critical |
|---|---|---|
| [#6724](https://github.com/zeroclaw-labs/zeroclaw/issues/6724) — Signal/Voice Call crashloop | **75 days** (2026-05-16) | S2 severity, supervisor crashloop. No fix PR. Needs triage. |
| [#8568](https://github.com/zeroclaw-labs/zeroclaw/issues/8568) — Mixture-of-Agents provider | **29 days** (2026-07-01) | Needs maintainer review; `needs-maintainer-review` label. Design is mature. |
| [#8603](https://github.com/zeroclaw-labs/zeroclaw/issues/8603) — OpenAI adapter RFC | **28 days** (2026-07-02) | High community demand. `needs-maintainer-review`. |
| [#6864](https://github.com/zeroclaw-labs/zeroclaw/issues/6864) — Invert channels → runtime dependency | **68 days** (2026-05-23) | Architectural blocker. Only 2 comments. |
| [#8780](https://github.com/zeroclaw-labs/zeroclaw/issues/8780) — Gemini Live channel | **24 days** (2026-07-06) | `needs-maintainer-review`. 4 comments, detailed RFC. |
| [#9103](https://github.com/zeroclaw-labs/zeroclaw/issues/9103) — Separate memory storage from enrichment | **14 days** (2026-07-16) | `needs-maintainer-review`. Could unblock #9048. |
| [#9246](https://github.com/zeroclaw-labs/zeroclaw/issues/9246) — Todo tracker config migration | **9 days** (2026-07-21) | `needs-maintainer-review`. Blocks PR #9013. |

### PRs Needing Maintainer Action

| PR | Age | Status Issue |
|---|---|---|
| [#8948](https://github.com/zeroclaw-labs/zeroclaw/pull/8948) — Fix zombie MCP processes | **19 days** (2026-07-10) | S1 severity, no recent review activity |
| [#8969](https://github.com/zeroclaw-labs/zeroclaw/pull/8969) — Slack thread hydration | **19 days** (2026-07-11) | `needs-author-action` — author inactive? |
| [#8955](https://github.com/zeroclaw-labs/zeroclaw/pull/8955) — Telegram media group batching | **19 days** (2026-07-10) | `needs-author-action` |
| [#9419](https://github.com/zeroclaw-labs/zeroclaw/pull/9419) — Rotate provider credentials after rate limits | **4 days** (2026-07-26) | `needs-author-action`, high risk/XL size |

### Tracker for Maintainer Decisions
Issue [#8692](https://github.com/zeroclaw-labs/zeroclaw/issues/8692) serves as the active decision queue for all pending RFCs and design issues. At least **8 RFCs** currently carry the `needs-maintainer-review` label.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/kky-wollu/agents-radar).*