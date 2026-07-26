# OpenClaw Ecosystem Digest 2026-07-27

> Issues: 348 | PRs: 500 | Projects covered: 13 | Generated: 2026-07-26 23:02 UTC

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

# OpenClaw Project Digest — 2026-07-27

## Today's Overview
OpenClaw shows elevated community activity with **348 issues** and **500 pull requests** updated in the last 24 hours, reflecting a highly engaged contributor base. A significant portion of the activity centers on **regression fixes**, **session-state reliability**, and **compaction/context management** — recurring themes that indicate the project is stabilizing after a series of rapid releases. The 97 closed issues and 237 merged/closed PRs suggest a productive triage cycle, though the large backlog of open items (251 open issues, 263 open PRs) indicates sustained maintenance pressure. No new releases were published today, with the most recent version being `2026.7.2-beta.3`.

## Releases
🟢 **No new releases today.** The latest available version remains **2026.7.2-beta.3** (referenced in issue #111519 as the upgrade source for a reported Telegram regression).

## Project Progress
237 PRs were merged or closed today. Notable structural improvements include:

- **Refactoring & Cleanup** (by maintainer `steipete`): Multiple PRs address technical debt — splitting the native hook relay ([#113626](https://github.com/openclaw/openclaw/pull/113626)), consolidating test state fixtures ([#113576](https://github.com/openclaw/openclaw/pull/113576)), sharing ingress lifecycle code across 7 channel plugins ([#113648](https://github.com/openclaw/openclaw/pull/113648)), and deduplicating UI logic ([#113649](https://github.com/openclaw/openclaw/pull/113649)).
- **Claude Opus 5 Runtime Support** — PR [#113633](https://github.com/openclaw/openclaw/pull/113633) (closed) completed Anthropic support, fixing fallback costs and native fast mode wiring.
- **Mobile App Fixes** — Restored live session updates after native reconnects across iOS, Android, and macOS ([#113634](https://github.com/openclaw/openclaw/pull/113634)).
- **Gateways & State** — Fixed retained verified owner authority for OpenAI HTTP endpoints ([#113638](https://github.com/openclaw/openclaw/pull/113638)), removed stalled UI behavior for multi-select archiving ([#113623](https://github.com/openclaw/openclaw/pull/113623)).

## Community Hot Topics
The most active discussions reflect deep user investment in reliability and feature completeness:

- **#75 – Linux/Windows Clawdbot Apps** (115 comments, 👍80) — The top-voted issue continues to be a community priority. Users want parity with existing macOS/iOS/Android apps. High engagement suggests this is a key adoption blocker for non-Apple ecosystems.

- **#99241 – Tool outputs render as unreadable image attachments** (24 comments) — A P1 bug affecting ANSI-heavy workflows. Agents lose access to original stdout/stderr text, causing context-blindness in long-running sessions. The community has provided detailed reproduction steps.

- **#102020 – Second message fails with "reply session initialization conflicted"** (15 comments) — A cross-channel, position-dependent session bug. The first turn works; the second fails consistently. Reporters across Signal and Discord confirm the pattern.

- **#86996 – Active Memory + Codex latency cascade** (13 comments, 👍2) — Users report 30-90 second delays and startup aborts when combining Active Memory with OpenAI/Codex and Lossless Claw context engine. This is a recurring pain point for power users.

- **#86519 – Agent repeats replies 2-10x after 5.20 update** (12 comments, 👍1) — A regression affecting Telegram users specifically. Partially mitigated in 5.22 but not fully resolved.

## Bugs & Stability
**High Priority (P1)**

| Issue | Summary | Fix PR? |
|-------|---------|---------|
| [#113315](https://github.com/openclaw/openclaw/issues/113315) | Telegram inbound update permanently lost after offset persistence with no ingress, spool, or dispatch | No (open) |
| [#113466](https://github.com/openclaw/openclaw/issues/113466) | `/new` and `/reset` don't actually create new sessions in 2026.7.1-2 | No (open) |
| [#111519](https://github.com/openclaw/openclaw/issues/111519) | Telegram DM replies fall back after stale DM-scope cleanup in 2026.7.2-beta.3 | No (open) |
| [#112423](https://github.com/openclaw/openclaw/issues/112423) | Large SQLite transcript cleanup blocks the gateway event loop | No (open) |
| [#108473](https://github.com/openclaw/openclaw/issues/108473) | cron tool schema breaks llama.cpp tool-calling (regression) | No (open) |
| [#113474](https://github.com/openclaw/openclaw/issues/113474) | Gateway crash loop on Raspberry Pi 5 (crash, closed) | Closed as duplicate/insufficient info |

🟡 Several P1 issues have **linked PRs open** but not yet merged:
- [#94251 – Ollama streaming not consumed](https://github.com/openclaw/openclaw/issues/94251) (PR open)
- [#106403 – Terminal-main reconciliation race](https://github.com/openclaw/openclaw/issues/106403) (PR open)
- [#90414 – Memory search "index metadata missing"](https://github.com/openclaw/openclaw/issues/90414) (PR open)

**Regressions (P1)**
- **2026.7.2-beta.3**: Telegram DM reply ownership loss ([#111519](https://github.com/openclaw/openclaw/issues/111519))
- **2026.7.1-2**: `/new` and `/reset` commands broken ([#113466](https://github.com/openclaw/openclaw/issues/113466))

**Platform-Specific Issues**
- **Raspberry Pi**: Crash loop cycle ([#113474](https://github.com/openclaw/openclaw/issues/113474))
- **Node 26**: `ERR_INVALID_STATE` from FileHandle GC ([#99263](https://github.com/openclaw/openclaw/issues/99263) — closed)
- **ARM64/macOS**: Gateway crashes on missing workspace directory ([#103917](https://github.com/openclaw/openclaw/issues/103917))

## Feature Requests & Roadmap Signals
- **Clawdbot Desktop Apps for Linux/Windows** ([#75](https://github.com/openclaw/openclaw/issues/75)) — Remains the top community request with 115 comments and 80 upvotes. Likely targeted for next major release cycle.
- **Per-agent dreaming configuration** ([#67413](https://github.com/openclaw/openclaw/issues/67413)) — Users request control over memory-core dreaming schedules to avoid OOM kills. PR open.
- **Exec-approvals denylist support** ([#6615](https://github.com/openclaw/openclaw/issues/6615)) — Enable "allow everything except X" policies. Strong community interest (8 upvotes). P2.
- **Distributed Agent Runtime** ([#42026](https://github.com/openclaw/openclaw/issues/42026)) — RFC for separating control plane from agent compute. Active discussion.
- **OpenRouter cost exposure** ([#9016](https://github.com/openclaw/openclaw/issues/9016)) — Per-message cost tracking requested for agent transparency.
- **WhatsApp sticker support** ([#7476](https://github.com/openclaw/openclaw/issues/7476)) — Channel parity request; inbound works, outbound missing.
- **TUI agent selection** ([#8892](https://github.com/openclaw/openclaw/issues/8892)) — `--agent` flag requested for TUI to connect to non-main agents. 3 upvotes.

**Prediction**: The **denylist for exec-approvals** and **per-agent dreaming** are most likely for next release given linked PRs and sustained maintainer attention.

## User Feedback Summary
- **Pain Points**: Session reliability dominates complaints — messages lost after compression, duplicated replies, session initialization conflicts, and state recovery failures are reported across Telegram, Discord, and Slack channels. Users consistently report that the agent becomes "unusable" after certain state transitions (e.g., resets, network reconnects, compaction).
- **Missing Desktop Support**: The *#75 Linux/Windows Clawdbot Apps* issue remains the most vocal community demand, with 115 comments from users blocked from adopting OpenClaw on non-Apple systems.
- **Mixed Satisfaction**: Closed issues like [#99263](https://github.com/openclaw/openclaw/issues/99263) (Node 26 crash) and [#98938](https://github.com/openclaw/openclaw/issues/98938) (Matrix OOM) were resolved, showing the team responds to blocker-level bugs. However, P1 regressions like the broken `/new` and `/reset` commands in 2026.7.1-2 suggest release quality control may need tightening.
- **Heavy Users Signal Concerns**: Advanced configurations (Active Memory + Codex + Lossless Claw) produce critical latency and reliability failures, indicating the project's architecture for long-running or multi-agent workflows needs optimization.

## Backlog Watch
Issues needing maintainer attention (no-fix-PR, stale, or awaiting decision):

| Issue | Age | Status | Notes |
|-------|-----|--------|-------|
| [#11665](https://github.com/openclaw/openclaw/issues/11665) — Webhook session re-use | 5 months | P2, needs product decision | Documented behavior doesn't match implementation |
| [#42026](https://github.com/openclaw/openclaw/issues/42026) — Distributed Agent Runtime RFC | 4 months | P2, needs security review | Architectural scope; may need RFC approval |
| [#6615](https://github.com/openclaw/openclaw/issues/6615) — Exec-approvals denylist | 5 months | P2, linked PR open | Community demand (8 👍) but stalled |
| [#8299](https://github.com/openclaw/openclaw/issues/8299) — Suppress sub-agent announce | 5 months | P2, needs live repro | Users want config option |
| [#8892](https://github.com/openclaw/openclaw/issues/8892) — TUI agent selection flag | 5 months | P3, needs product decision | Low priority but useful for multi-agent setups |
| [#87325](https://github.com/openclaw/openclaw/issues/87325) — Azure Foundry GPT Realtime | 2 months | P2, needs security review | Enterprise Azure users blocked |
| [#95610](https://github.com/openclaw/openclaw/issues/95610) — OpenAI prompt-cache churn | 1 month | P2, needs live repro | Affects cost and latency for OpenAI users |
| [#95840](https://github.com/openclaw/openclaw/issues/95840) — contextPruning dead for OpenAI | 1 month | needs live repro | Firebreak never fires on highest-volume provider |

---

## Cross-Ecosystem Comparison

Here is the cross-project comparison report based on the community digest summaries you provided.

---

### Cross-Project Comparison Report: Personal AI Agent Open-Source Ecosystem

**Date:** 2026-07-27

---

#### 1. Ecosystem Overview

The open-source personal AI agent ecosystem is currently in a **high-intensity stabilization and security hardening phase**, following a period of rapid feature expansion. Projects are converging on a set of shared challenges: session-state reliability, data integrity during memory compaction, and the security boundaries of multi-channel, multi-provider architectures. **OpenClaw** remains the dominant reference implementation and community hub, while specialized forks like **Hermes Agent** and **ZeroClaw** are driving innovation in desktop UX and security auditing, respectively. The ecosystem is characterized by a widening gap between a few highly active "core" projects and a long tail of smaller, less active forks, indicating both a healthy competitive landscape and the potential for contributor concentration.

---

#### 2. Activity Comparison

The following table compares project activity over the last 24 hours. "Health Score" is a qualitative assessment based on the ratio of resolved issues to new bug reports, PR merge velocity, and maintainer responsiveness.

| Project | Issues (Open/Total Updated) | PRs (Open/Total Updated) | Release Status | Health Score |
| :--- | :--- | :--- | :--- | :--- |
| **OpenClaw** | 251 / 348 | 263 / 500 | **None** (v2026.7.2-beta.3) | **Stressed** (High backlog, regressions) |
| **NanoBot** | N/A / 9 | N/A / 28 (22 merged) | **None** | **Healthy** (Rapid bug-fix sprint) |
| **Hermes Agent** | 43 / 50 | N/A / 50 (4 merged) | **None** (v0.19.0) | **Moderate** (Growing backlog, responsive to critical bugs) |
| **PicoClaw** | N/A / 4 | N/A / 7 | **None** | **Stable** (Steady, moderate activity) |
| **NanoClaw** | 4 / 4 | 8 / 10 (2 merged) | **None** | **Critical** (Regression causing silent message drops) |
| **NullClaw** | N/A / 1 | 0 / 0 | **None** (v2026.5.29) | **Dormant** (Critical aarch64 bug unattended) |
| **IronClaw** | N/A / 3 | N/A / 18 (7 merged) | **Pending** (Release PR blocked) | **Healthy** (Active arch. refactoring) |
| **LobsterAI** | N/A / 2 | N/A / 8 (1 merged) | **None** | **Stressed** (Stale backlog, critical gateway bug) |
| **Moltis** | 0 | 8 / 8 | **None** | **Healthy** (Focused feature dev) |
| **CoPaw (QwenPaw)** | 13 / 13 | 5 / 5 | **None** | **Critical** (v2.0.1 release regressions, no maintainer response) |
| **ZeroClaw** | 41 / 44 | 49 / 50 (1 merged) | **None** (v0.8.4 pending) | **Healthy** (High-volume, responsive security audit) |
| **TinyClaw** | N/A | N/A | **None** | **Dormant** (No activity) |
| **ZeptoClaw** | N/A | N/A | **None** | **Dormant** (No activity) |

---

#### 3. OpenClaw's Position

- **Advantages vs. Peers:**
    - **Dominant Community & Activity:** OpenClaw's raw issue and PR volume (348/500) dwarfs all other projects, indicating the largest contributor base and community momentum.
    - **Vendor & Platform Agnosticism:** Its deep integration with Claude, Gemini, Ollama, and other providers (including the new Claude Opus 5 runtime) offers unparalleled flexibility, whereas projects like **Hermes Agent** or **CoPaw** (QwenPaw) appear more aligned with specific LLMs.
    - **Feature Breadth:** OpenClaw is the most feature-complete reference, covering mobile, desktop (MacOS/iOS/Android), multi-channel (Telegram, Discord, Slack), and advanced memory (Active Memory, Lossless Claw context engine).

- **Technical Approach Differences:**
    - **Session-State Complexity:** OpenClaw’s sophisticated session and context management (“Lossless Claw”) is a double-edged sword. It provides powerful features but is the source of the highest number of regressions and friction (e.g., session initialization conflicts, state recovery failures), which are less prominent in simpler projects like **NullClaw** or **NanoBot**.
    - **Monolithic vs. Modular:** While OpenClaw is a monolithic reference, **ZeroClaw** is pursuing a runtime plugin architecture (RFC #8850) and **Moltis** is building a discrete agent (ACP). This suggests a future fragmentation where OpenClaw remains the core, but modular/forked projects cater to specialized needs (security, specific channels).

- **Community Size Comparison:**
    - OpenClaw’s community is orders of magnitude larger than any other single project. Its most-watched issue (#75, Linux/Windows desktop apps) has far more engagement (115 comments) than the entire issue tracker of most other projects.

#### 4. Shared Technical Focus Areas

Multiple projects are independently converging on the same challenges, indicating ecosystem-wide pain points.

| Shared Focus Area | Affected Projects | Specific User Need |
| :--- | :--- | :--- |
| **Session State & Data Integrity** | **OpenClaw**, **NanoClaw**, **NanoBot**, **Hermes Agent** | Users across all projects report session initialization failures, silent data loss, message duplication, and corruption after compaction or upgrades. (e.g., OpenClaw #99241, NanoClaw #3140, Hermes #54403). |
| **Security Hardening** | **ZeroClaw**, **IronClaw**, **PicoClaw**, **Hermes Agent** | There is a clear push for *safe-by-default* configurations, attestation, and auditing. ZeroClaw is undergoing a major security audit; IronClaw is enforcing a "recoverability contract"; Hermes is fixing symlink bypasses and mention-gating exploits. |
| **Cross-Platform Desktop Parity** | **OpenClaw**, **Hermes Agent**, **LobsterAI** | The demand for native desktop apps on Linux and Windows is the single most vocal community request across the ecosystem. All three projects have open issues addressing this gap (OpenClaw #75, Hermes #57848, LobsterAI #273). |
| **Provider & Tool Interoperability** | **OpenClaw**, **NanoBot**, **Hermes Agent** | MCP tool schema incompatibilities (NanoBot #5040) and broken fallback logic (Hermes #25123, OpenClaw #108473) are common. Users need a reliable contract between agents and LLM providers. |
| **Memory Management & Latency** | **OpenClaw**, **NanoBot**, **CoPaw** | "Active Memory + Codex" latency cascades (OpenClaw) and Dream process starvation (NanoBot) show that memory subsystems are a key bottleneck for advanced use cases. |

#### 5. Differentiation Analysis

The ecosystem is not a single market but several overlapping ones, defined by project priorities.

| Dimension | OpenClaw | Hermes Agent | ZeroClaw | Moltis |
| :--- | :--- | :--- | :--- | :--- |
| **Primary Focus** | Core Reference, Maximum Features | Desktop & Dashboard UX | Security & Hardening | Multi-Protocol Agent (ACP/Nostr) |
| **Target User** | Power users, developers, anyone wanting a complete solution. | Developers needing a robust desktop IDE/dashboard. | Security-conscious deployers, enterprise. | Developers building interoperable agent workflows. |
| **Tech Architecture** | Monolithic, stateful core with extensive plugin system. | Desktop-first (Electron), strong TUI focus. | Runtime plugin architecture, Rust-based, security-audit driven. | Agent Communication Protocol (ACP) native. |
| **Deployment Priority** | Linux, macOS, iOS, Android. Windows/Linux desktop is the #1 gap. | Desktop (macOS, Windows, Linux). Self-hosted server. | Cross-platform, strong security defaults. | Interoperable agent-to-agent services. |

**Summary:** **OpenClaw** is the feature king; **Hermes Agent** is the desktop champion; **ZeroClaw** is the security sentinel; **Moltis** is the interoperability pioneer.

#### 6. Community Momentum & Maturity

Projects can be grouped into three tiers based on their current phase.

- **Tier 1: Rapid Iteration & High Momentum (Health Score: Healthy)**
    - **ZeroClaw**: Exceptional momentum driven by a major security audit. High PR throughput and rapid fix response.
    - **NanoBot**: Strong bug-fix velocity, prioritizing stability and data safety.
    - **IronClaw**: Intense architectural refactoring around error recoverability, signaling a maturing project.

- **Tier 2: Stabilization & Maintenance (Health Score: Moderate to Stressed)**
    - **OpenClaw**: Large community, but stressed by a high volume of regressions after rapid releases. The focus is on triage and stabilization.
    - **Hermes Agent**: Growing backlog of platform-specific bugs, but responsive to critical installation and security issues.
    - **LobsterAI**: Stale backlog of significant fixes and a critical gateway bug erodes user trust.

- **Tier 3: Critical Instability & Dormancy (Health Score: Critical to Dormant)**
    - **NanoClaw**: A major regression (silent message drop) makes the latest release nearly unusable for existing users.
    - **CoPaw (QwenPaw)**: A critical release (v2.0.1) with multiple regressions and no maintainer response. This creates high user churn risk.
    - **NullClaw, TinyClaw, ZeptoClaw**: Effectively dormant. Their existence signals the ecosystem's long tail, but they have negligible community activity.

#### 7. Trend Signals for AI Agent Developers

The community feedback reveals several industry trends critical for developers:

1.  **The "Reliability Tax" is Now the Main Focus:** The novelty of having an AI agent has worn off. The overwhelming demand is for **predictable, reliable, and recoverable systems.** Developers should prioritize session state management, data integrity, and error recovery over new feature bloat. Projects like **IronClaw** are leading this charge.

2.  **Security is a Differentiator, Not an Afterthought:** The ecosystem is waking up to the second-order effects of agent autonomy. **ZeroClaw's** explicit security audit is a clear signal. Developers must plan for message authorization, credential hygiene, tool access controls (denylists/allowlists), and sandboxing from day one.

3.  **The "Desktop Application" is the Gateway for Prosumers:** The consistent, loud demand for Linux and Windows desktop apps (OpenClaw #75, Hermes #57848) indicates that the CLI and mobile-only paths are insufficient for the next wave of users. A polished desktop experience is the key to expanding the user base beyond developers.

4.  **Interoperability is a Blessing and a Curse:** While ACP (Moltis) and MCP offer a wonderful vision of a connected agent ecosystem, the reality today is a mess of **schema incompatibilities** (NanoBot), **broken fallbacks** (Hermes), and **tool-calling failures** (OpenClaw). The "plug and play" promise is not yet fulfilled; developers should expect to invest heavily in adapter logic and error handling.

5.  **Memory is the New Performance Bottleneck:** User feedback on "Active Memory + Codex latency cascades" (OpenClaw) and "Dream process starvation" (NanoBot) signals that memory management is the top performance challenge for advanced agents. Efficient vectorization, compression (CoPaw's Visual Compact), and compaction strategies are becoming a core engineering discipline.

---

## Peer Project Reports

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot Project Digest — 2026-07-27

## 1. Today's Overview

NanoBot has seen very high activity over the past 24 hours, with **28 updated PRs (22 merged/closed)** and **9 issues updated (7 closed)**. The development pace indicates a major bug-fix and stability sprint is underway, with 8 P1-priority fixes merged. No new releases were published. The maintainers are actively addressing regressions, edge cases in memory and provider handling, and hardening the system against data loss and schema incompatibilities.

---

## 2. Releases

No new releases this period.

---

## 3. Project Progress

22 PRs were merged or closed in the last 24 hours. Key advances:

- **Agent & Execution**
  - **Length recovery fix (#5056):** Preserves all output segments when model response is truncated by token limit, rather than keeping only the last continuation [PR #5056](https://github.com/HKUDS/nanobot/pull/5056)
  - **Idle compaction configurable (#5036):** Makes the background scan interval configurable — critical for resource-constrained devices like Raspberry Pi [PR #5036](https://github.com/HKUDS/nanobot/pull/5036)
  - **Extra bwrap bind roots (#4625):** Allows deployments to expose user tool directories inside the bubblewrap sandbox [PR #4625](https://github.com/HKUDS/nanobot/pull/4625)

- **Memory & Dream**
  - **No-op Dream progress (#5054):** Advances the Dream cursor even when durable memory has no diff, preventing starvation of later history entries [PR #5054](https://github.com/HKUDS/nanobot/pull/5054)
  - **Dream history preservation (#5099, open):** Protects unprocessed Dream entries during compaction [PR #5099](https://github.com/HKUDS/nanobot/pull/5099)

- **Provider & MCP**
  - **MCP schema normalization (#5057):** Converts non-`#/$defs/` local schema refs so strict providers (Kimi/Moonshot) don't reject the entire tool list [PR #5057](https://github.com/HKUDS/nanobot/pull/5057)
  - **Gemini Flash image aspect ratio (#4656):** Forwarded size/aspect-ratio hints to Flash image generation path [PR #4656](https://github.com/HKUDS/nanobot/pull/4656)
  - **Codex OAuth in Quick Start (#4939):** Exposed OpenAI Codex in the CLI setup with interactive OAuth flow [PR #4939](https://github.com/HKUDS/nanobot/pull/4939)

- **Channels & WebUI**
  - **DingTalk private chat gate (#4446):** Added flag to forbid 1:1 chats; mentions in group replies [PR #4446](https://github.com/HKUDS/nanobot/pull/4446)
  - **Heartbeat for unified sessions (#4928):** Routes heartbeat delivery to last known concrete channel [PR #4928](https://github.com/HKUDS/nanobot/pull/4928)
  - **Mobile thread width fix (#5100):** Prevents long Markdown messages from widening view on mobile [PR #5100](https://github.com/HKUDS/nanobot/pull/5100)
  - **Pending message runtime context (#5084):** Preserves sender/channel metadata for mid-turn queued messages [PR #5084](https://github.com/HKUDS/nanobot/pull/5084)

- **Data Safety & Robustness**
  - **Null tolerance (5 PRs):** Handled null `approved`/`pending` maps, null `runHistory`, null `multi_url`/`list`/`text` fields in Feishu and triggers — these caused crashes on load [PR #5088](https://github.com/HKUDS/nanobot/pull/5088), [#5087](https://github.com/HKUDS/nanobot/pull/5087), [#5089](https://github.com/HKUDS/nanobot/pull/5089), [#5092](https://github.com/HKUDS/nanobot/pull/5092), [#5093](https://github.com/HKUDS/nanobot/pull/5093)
  - **Connect cancellation safety (#5069):** Prevents saved credentials from cancelled QR connections [PR #5069](https://github.com/HKUDS/nanobot/pull/5069)

---

## 4. Community Hot Topics

Most active issues and PRs (by comments and reactions):

- **Issue #4924** (4 comments) — `_pick_heartbeat_target_from_sessions` fails with `unifiedSession: true` when no regular sessions exist. **Resolved** by PR #4928 (merged). [Issue #4924](https://github.com/HKUDS/nanobot/issues/4924)

- **Issue #1012** (2 comments, open) — Stale feature request to add subagent profiles with configurable tools/skills. No maintainer response since February. [Issue #1012](https://github.com/HKUDS/nanobot/issues/1012)

- **Issue #4792** (2 comments, open) — `/stop` command silently discards queued messages without re-publishing. Still awaiting fix. [Issue #4792](https://github.com/HKUDS/nanobot/issues/4792)

- **Issue #4107** (1 reaction) — Request for configurable bwrap bind mounts. **Resolved** by PR #4625 (merged). [Issue #4107](https://github.com/HKUDS/nanobot/issues/4107)

*Underlying needs:* Users are demanding correctness in session routing, data persistence, and memory management. The high volume of P1 fixes (8 today) indicates the community accepts bleeding-edge builds but expects rapid regression correction.

---

## 5. Bugs & Stability

| Severity | Bug | Status | Fix PR |
|----------|-----|--------|--------|
| **Critical** | `/stop` silently discards pending queue messages — permanent message loss (#4792) | **Open** | None yet |
| **High** | AgentRunner length recovery loses all but last continuation segment (#5051) | **Closed** | #5056 merged |
| **High** | MCP tools with non-`#/$defs/` refs break entire model on Kimi/Moonshot (#5040) | **Closed** | #5057 merged |
| **High** | Completed no-op Dream batches starve all later history (#5041) | **Closed** | #5054 merged |
| **Medium** | Null `approved`/`pending` maps crash pairing load | **Closed** | #5088 merged |
| **Medium** | Null `runHistory` crashes trigger loading | **Closed** | #5087 merged |
| **Medium** | Feishu: `null multi_url`/`list`/`text` fields crash card/post extraction | **Closed** | #5089, #5093 merged |
| **Medium** | String `lastRunAtMs` in triggers crashes int comparisons | **Closed** | #5092 merged |
| **Medium** | Pending mid-turn messages lose sender/channel context (#4064) | **Closed** | #5084 merged |
| **Medium** | Connect cancellation can save credentials from cancelled session | **Closed** | #5069 merged |
| **Low** | WebUI mobile thread widens with long Markdown | **Closed** | #5100 merged |

**Now-open security PR:** #5095 hardens image URL downloads through DNS-pinning SSRF transport with hop validation [PR #5095](https://github.com/HKUDS/nanobot/pull/5095).

---

## 6. Feature Requests & Roadmap Signals

**Merged this cycle:**
- Configurable bwrap bind mounts (#4625) — responds to sandbox isolation needs
- Configurable idle compaction interval (#5036) — for low-resource devices
- DingTalk private chat gate and group mentions (#4446) — channel-specific UX
- Codex OAuth in Quick Start (#4939) — simplifies onboarding

**Open requests likely in next release:**
- **Subagent profiles (#1012)** — stale but fundamental; would enable specialized agent roles (research, coding). Likely to be picked up as the project expands agent capabilities.
- **Image download SSRF hardening (#5095, open PR)** — security must-have, likely merged within days.

---

## 7. User Feedback Summary

**Positive signals:**
- Rapid turnaround on reported bugs — most P1 issues closed within 24–48 hours.
- Raspberry Pi user reported success with idle compaction config — "I'm running nanobot on Raspberry Pi, and I noticed it's always consuming 30-40% of 1 CPU core when idle" — now configurable (#5036).

**Pain points:**
- **Data loss risk:** `/stop` silently discarding queued messages (#4792) is a severe UX failure — users cannot safely stop the bot mid-conversation without losing user input.
- **Provider incompatibility:** MCP tools with non-standard JSON Schema refs break the entire chat-completion on Kimi/Moonshot (#5040) — a single misconfigured tool disables the bot.
- **Memory starvation:** No-op Dream batches could indefinitely prevent memory compaction for new entries (#5041) — silently reduces system usefulness over time.
- **Setup friction:** Unified session heartbeat failures (#4924) made the feature unusable in the no-session case; missing Codex OAuth in Quick Start (#4939) blocked a provider path.

---

## 8. Backlog Watch

| Issue | Age | Status | Why Watch |
|-------|-----|--------|-----------|
| **#1012 — Subagent profiles** | 5 months | Open, 0 maintainer comments | Stale but high-value feature request; no maintainer engagement since creation |
| **#4792 — `/stop` silent discard** | 21 days | Open | **Active critical bug** with no fix PR yet; permanent message loss pending |
| **#5099 — Dream history preservation** | 1 day | Open PR | Companion to #5054 fix; ensures ongoing memory correctness |

**Maintainers** should prioritize #4792 (message loss) and #5099 (memory edge case). The long-dormant #1012 would benefit from a maintainer triage comment to set expectations — it's a popular concept but may require architectural changes.

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent Project Digest — 2026-07-27

## 1. Today's Overview

High activity across the project with 50 issues and 50 PRs updated in the last 24 hours. The community is actively reporting and addressing bugs, with 8 PRs merged/closed today (4 of which are fix salvages authored by maintainer `teknium1`). No new releases were published. The open issue count remains high (43 open/active), suggesting a growing backlog but also strong community engagement in surfacing edge cases. Security-boundary issues and session-state corruption bugs continue to be recurring themes that attract maintainer attention.

## 2. Releases

No new releases were published today. The latest available version remains **v0.19.0**.

## 3. Project Progress

**4 PRs merged/closed today:**

- **#72224** (by teknium1) — `fix(install): reap Windows cua installer process tree and clear stale install.lock` — Salvage of #71329, fixing orphaned PowerShell processes that held `install.lock` on Windows after timed-out CUA driver installs.
- **#72232** (by teknium1) — `fix(gateway): deliver kanban notifications to Telegram DM topics` — Salvage of two earlier PRs (#60769, #63927) that unblocks kanban notification delivery into Telegram DM topics.
- **#72230** (by OutThisLife) — `fix: make the bootstrap-complete marker consistent across every install path` — Fixes the macOS reinstall loop (#60721) where `.hermes-bootstrap-complete` was written inconsistently across installer code paths.
- **#72274** (by vadimcomanescu) — `Fix gateway tests terminating pytest early` — Prevents gateway service tests from invoking the production hard-exit hook and isolates systemd restart tests from the host environment.

**Key fixes advancing:**
- The `bounded model fallback` PR (#61326 by konsisumer) continues to receive updates — centralizing fallback logic for invalid model IDs and quota failures across all agent contexts.
- Gateway execution policy support (#66966 by Raphiiko) is moving forward, enabling per-route `toolsets` and `reasoning_effort` configuration in API model routes.

## 4. Community Hot Topics

**Most discussed issues (by comment count):**

- **#55367** (4 comments) — [OPEN] *ACP auto-approve sensitive-path guard ignores symlinks* — This security-boundary bug is receiving sustained discussion because it creates a credential-exfiltration vector through innocuously named symlinks. The label `sweeper:risk-security-boundary` signals high maintainer concern.

- **#31862** (3 comments) — [CLOSED] *ChatPage clears header action buttons on ALL pages* — A dashboard TUI regression that affected multiple pages (Cron, Model Management). Closed today.

- **#55427** (3 comments) — [OPEN] *Native Gemini: history starting with assistant turn 400s the request* — Affects all users of Google's Gemini models through the native adapter; a clear protocol-level bug in `_build_gemini_contents`.

- **#9816** (3 comments, 👍3) — [OPEN] *Feishu/Lark messages poorly formatted due to excessive Markdown escaping* — High reaction count suggests many Chinese users are affected by broken Markdown rendering on the Feishu/Lark platform.

- **#67605** (3 comments) — [OPEN] *Dashboard/desktop profile switch is partial — MCP tools never load* — A complex hybrid-profile bug where secrets and MCP tools resolve from the launch profile instead of the selected one, affecting all desktop/dashboard users with multiple profiles.

**Underlying community needs:** Users are consistently encountering edge cases around **session state consistency** (profile switching, reconnection behavior, interrupt handling) and **platform-specific formatting** (Markdown on Feishu/Lark, code blocks losing indentation on long messages).

## 5. Bugs & Stability

**High severity (P2 — likely to affect production users):**

1. **#71319** (CLOSED) — *cua-driver installer stale-lock recovery is POSIX-only* — Windows users remain vulnerable to permanently wedged installer processes. **Fix PR #72224 merged today.**

2. **#72287** (OPEN) — *Live subagent activity panel stays empty under `hermes serve`* — Desktop app's subagent monitoring does not receive progress events from the `subagent` topic when running in serve mode. **No fix PR yet.**

3. **#72272** (OPEN) — *v0.19.0 --oneshot exits 0 with non-challenge response under openai-codex* — The CLI's deterministic challenge mode silently passes when it should fail, potentially hiding model regressions. Tagged `needs-repro`.

4. **#72278** (CLOSED) — *WhatsApp self-chat replies can falsely satisfy group mention gating* — A social-engineering vector where replies to one's own messages in self-chat mode bypass mention requirements. **Fixed today.**

5. **#64732** (OPEN) — *Thinking-prefill retry cascade triggers on reasoning responses with visible content* — The conversation loop's structured-reasoning check lacks a `final_response` validation, causing unnecessary retries.

6. **#54403** (OPEN) — *ENTRY_DELIMITER not validated in user content → silent memory corruption* — Any memory entry containing `\n§\n` is silently corrupted on next read. A data-integrity bug in the memory tool.

**Medium severity (P3 — affecting specific platforms or use cases):**

- **#63428** — Computer Use: `app-scoped capture 0x0` after reconnect (macOS, cua-driver 0.7.1)
- **#54579** — Long code blocks lose indentation when reply is split into multiple messages
- **#43339** — Profile deletion fails when `.env` has macOS immutable flag
- **#41305** — Windows Desktop app shows default Electron icon (PNG format unsupported)
- **#53432** — `_expand_tilde` breaks on consecutive slashes (`~//foo`) — **Fix PR #72286 open**
- **#26697** — `send_message` tool ignores `markdown_support` config for QQ platform

**Fix PRs open today addressing bugs:** #72286 (tilde slashes), #72283 (model output cap errors), #72285 (HTTP auth binding), #72279 (session-search scrolling), #72282 (Telegram TTS), #72231 (interrupt marker), #72276 (stale skill hub results), #72271 (Mattermost cron delivery), #72284 (setup wizard max_turns).

## 6. Feature Requests & Roadmap Signals

**Feature requests with maintainer/community traction:**

- **#64662** (OPEN, P3) — *Allow llm_execution middleware to intentionally block provider execution* — Plugin developers need the ability to abort model execution from middleware, not just fall through. If adopted, this would unlock advanced moderation, caching, and routing plugins.

- **#57848** (OPEN, P3) — *Custom background image for Desktop app* — A simple personalization request that has been open since July 3. Likely low priority but straightforward to implement.

- **#37491** (OPEN, P3) — *One-click installer for Windows users in China* — Addresses accessibility barriers for Chinese users (slow GitHub/npm access, dependency complexity). Has 1 like; may gain momentum as the China user base grows.

- **#53081** (OPEN, P3) — *Robust autostash backup, restore, and failure notification for Hermes update* — A PRD-level feature request for making the update mechanism production-grade. May appear in a v0.20.x release focused on reliability.

**Signals for next release (v0.20.0):**
- The bounded model fallback centralization (#61326) is a strong candidate — it's been open since July 9 and addresses multiple related bugs (invalid model IDs, quota failures).
- Gateway execution policy (#66966) would be a meaningful API enhancement.
- The bundle of install-path consistency fixes (#72224, #72230) suggests maintainers are prioritizing installation reliability before the next release.

## 7. User Feedback Summary

**Pain points reported by real users:**

1. **Profile isolation is broken** (#67605): *"Selecting a profile in the desktop app does not give you that profile — it gives you a hybrid."* — SuperDodge. This affects users who manage multiple model providers or MCP tool configurations.

2. **Reconnect degrades Computer Use** (#63428): *"Hermes Computer Use can report healthy transport yet fail app-scoped capture... silently degrade a dead/reconnected cua session into a 0x0 success."* — blazarb0t. A reliability blocker for production Computer Use workflows.

3. **Memory corruption from user content** (#54403): The `ENTRY_DELIMITER` bug means users who naturally write `\n§\n` in their notes experience silent data loss without error messages.

4. **Long code blocks lose formatting** (#54579): *"When an outbound reply is longer than a platform's per-message limit... indentation is lost."* — MaxFreedomPollard. Affects developers sharing code snippets.

5. **Windows installer lock can wedge permanently** (#71319): *"install.ps1's file lock can still wedge permanently"* — kaya0548. Windows users face a complete install failure that requires manual cleanup.

6. **OAuth login intermittent failure** (#56750): *"Remote dashboard OAuth login fails intermittently with 'Missing PKCE state cookie'"* — repfigit. Cross-site redirect cookie handling creates unreliable login UX.

**Satisfaction signals:** The rapid closure of 4 fix PRs today (especially the Windows stale-lock and macOS reinstall-loop fixes) shows maintainers are responsive to critical installation/setup issues.

## 8. Backlog Watch

**Issues needing maintainer attention (long-unanswered with no assignment):**

- **#9816** (2026-04-14, P3) — *Feishu/Lark messages poorly formatted due to excessive Markdown escaping* — Open 3+ months with 3 likes and 3 comments. The `_escape_markdown_text` function is clearly broken for Feishu/Lark, but no fix PR has materialized. This affects a measurable segment of the Chinese user base.

- **#10990** (2026-04-16, P2) — *Gateway can send stale "Still working..." heartbeats after restart* — Open 3+ months. A race condition between gateway restart and background task completion creates misleading UX. Despite being labeled P2, no fix PR is open.

- **#13800** (2026-04-22, P3) — *banner_logo not centered when using custom skins* — Open 3+ months. A cosmetic bug in the skin/customization system.

- **#26697** (2026-05-16, P2) — *send_message tool ignores markdown_support config for QQ platform* — Open 2+ months. A P2 bug affecting the QQ platform adapter's Markdown rendering.

- **#25123** (2026-05-13, P2) — *Fallback to gemini-3-flash-preview fails with 400 (thinking_config)* — Open 2+ months. The mandatory `thinking_config` parameter injection breaks fallback to certain Gemini model versions.

**PRs needing review:**
- **#61326** (2026-07-09) — *fix(agent): centralize bounded model fallback* — Open 18 days, touches core agent conversation logic. A high-impact fix that has been waiting for maintainer merge or feedback.
- **#66966** (2026-07-18) — *feat(gateway): support execution policy in API model routes* — Open 9 days. A significant feature enhancement for the API server.

**Project health indicator:** The backlog of long-unanswered P2 issues (especially platform-specific adapter bugs for Feishu/Lark, QQ, and Windows) suggests the project's platform support breadth may be outpacing its maintainer capacity. The `type/security` labeled issues are being addressed promptly (e.g., WhatsApp mention gating fixed same day), which is encouraging for trust in the project's security posture.

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw Project Digest — 2026-07-27

## Today's Overview
The PicoClaw project shows moderate activity with 4 issues and 7 PRs updated in the last 24 hours. Today saw strong contributor momentum with 6 new pull requests opened and 1 closed, alongside 3 new open issues. The project is processing both bug fixes and feature additions at a healthy cadence. There are no new releases today, and the backlog contains several stale items that may require maintainer attention. Overall, the project appears to be in a stable, active development phase.

## Releases
No new releases today. The latest release remains unchanged from previous reporting.

## Project Progress
One pull request was merged/closed today:
- **#3248** (closed/merged) — fix: bump Go to 1.25.12 to remediate stdlib vulnerabilities  
  Author: afjcjsbx | [PR #3248](https://github.com/sipeed/picoclaw/pull/3248)  
  This security fix bumps the Go toolchain from 1.25.11 to 1.25.12, addressing `GO-2026-5856` in `crypto/tls` and `GO-2026-4970` in `os`. This is a critical infrastructure improvement that ensures CI builds use a patched standard library.

Several new PRs open today signal active feature and fix work:
- **#3299** — Add native Exa web search provider  
- **#3297** — Harden remote prompt and exec boundaries  
- **#3295** — Prevent SplitMessage hang on oversized fence headers  
- **#3296** — Complete Czech code wrap labels

## Community Hot Topics
Most active issues and PRs by comments/reactions:

1. **#3264** (OPEN, 1 comment) — [BUG] SplitMessage hangs on an oversized fenced-code info string  
   Author: floze-the-genius | [Issue #3264](https://github.com/sipeed/picoclaw/issues/3264)  
   A blocking bug where `channels.SplitMessage` can loop infinitely when a fenced code block near the start of a chunk has an info string extending beyond the split point. A fix PR (#3295) has already been submitted today by ErzerLP, showing responsive issue-to-fix turnaround.

2. **#3265** (OPEN, 1 comment) — Gateway startup fails with 'channel deltachat has unknown type deltachat'  
   Author: Cipher208 | [Issue #3265](https://github.com/sipeed/picoclaw/issues/3265)  
   A confusing startup error where the gateway fails because it finds a deltachat channel type it doesn't recognize, even when no deltachat configuration is present. This suggests possible leftover defaults in the gateway's channel discovery logic.

3. **#3298** (OPEN, 0 comments) — Feature: Add AI Router as an OpenAI-compatible provider preset  
   Author: airouter-dev | [Issue #3298](https://github.com/sipeed/picoclaw/issues/3298)  
   New request from the maintainer of AI Router to add it as a named provider preset for easier configuration.

## Bugs & Stability

| Severity | Issue | Description | Fix PR? |
|----------|-------|-------------|---------|
| **High** | #3264 | `SplitMessage` hangs infinitely on oversized fence headers | Yes — PR #3295 opened today |
| **Medium** | #3265 | Gateway fails on unrecognized `deltachat` channel type, even when not configured | No PR yet |
| **Low** | #3252 (closed) | `splitKnownProviderModel` strips provider prefix incorrectly when model ID contains alias | Closed as stale; root cause may still exist |

**Worth noting:** The `SplitMessage` hang bug (#3264) is a high-severity issue that can cause message processing to block indefinitely. The fast turnaround with PR #3295 from ErzerLP is positive. The gateway startup issue (#3265) remains unfixed and could prevent users from running the gateway in standard configurations.

## Feature Requests & Roadmap Signals

1. **Native Exa web search provider** (PR #3299) — Already submitted as a pull request today by kesku. This would add `Exa` as a native web search provider, supporting time-range filters and highlights. Likely to be included in the next release given it's already coded.

2. **AI Router provider preset** (Issue #3298) — Request to add AI Router as a named OpenAI-compatible provider, authored by the service maintainer who offered to contribute. High probability of inclusion in the next version given contributor support.

3. **Security hardening for remote prompts** (PR #3297) — SiYue-ZO submitted a comprehensive fix that keeps remote sender metadata in a normalized envelope, disables remote exec by default, and migrates configs to schema v4. This addresses significant security boundaries and may be prioritized for the next release.

4. **Czech localization completion** (PR #3296) — Minor i18n improvement, likely to be merged soon.

**Prediction for next release (v0.9.x or v1.0.x?):** The Exa provider (PR #3299) and the remote exec security hardening (PR #3297) are the two most significant changes and are likely candidates. The AI Router preset (Issue #3298) may follow as a quick contribution.

## User Feedback Summary

- **Pain point — Gateway configuration confusion:** Issue #3265 shows a user frustrated that the gateway fails with an unrecognized channel type (`deltachat`) even when they haven't configured it. This suggests a gap in default channel handling during startup.
- **Pain point — Infinite loop on message splitting:** Issue #3264 describes a blocking scenario that can freeze message processing. The community responded quickly with a fix PR, indicating responsiveness but also that the bug could affect real-world usage.
- **Positive signal — Contributor offer from AI Router maintainer:** airouter-dev self-identified and offered to contribute a provider preset, showing healthy external contributor engagement.
- **Internationalization interest:** PR #3296 from KrtCZ demonstrates continued interest in Czech language support, suggesting a multilingual user base.

## Backlog Watch

Items that may need maintainer attention due to age or lack of response:

1. **#3265** — Gateway deltachat startup error (OPEN, created 2026-07-19, updated 2026-07-26, 1 comment)  
   [Issue #3265](https://github.com/sipeed/picoclaw/issues/3265)  
   No fix PR exists yet. The issue has been open for 8 days with only initial triage. The underlying problem could affect many users who run the gateway without deltachat configured.

2. **#3202** — fix(routing): strip leading/trailing underscores in ID normalization (OPEN, PR, created 2026-07-01, updated 2026-07-26)  
   [PR #3202](https://github.com/sipeed/picoclaw/pull/3202)  
   A routing bug fix has been open for 26 days with no merge or further discussion. The PR addresses documented normalization constraints not being enforced.

3. **#3267** — fix scope bug for refresh agy token (OPEN, PR, created 2026-07-19, updated 2026-07-26)  
   [PR #3267](https://github.com/sipeed/picoclaw/pull/3267)  
   An antigravity token refresh bug fix that has been open for 8 days. The bug causes `PERMISSION_DENIED` errors during token refresh, which could lock users out of antigravity authentication.

These backlog items, while not critical individually, represent unresolved issues that could degrade user experience or accumulate technical debt if left unattended.

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw Project Digest — 2026-07-27

## Today's Overview

NanoClaw is in a **highly active maintenance and stabilization phase**, with 4 open issues and 10 pull requests updated in the past 24 hours. Two PRs were merged/closed today, primarily addressing message routing bugs and feature enhancements. The project is currently dealing with a **serious regression** introduced by the explicit-destinations migration (Issue #3140), where pre-existing chat configurations silently lose agent replies after an update—a high-priority concern requiring immediate attention. While no new releases are available, the volume of PR activity (8 open) suggests a substantial patch release is being assembled.

## Releases

**None** — No new releases were published today. Given the cluster of fix PRs and severity of ongoing issues, a patch release may be imminent once the explicit-destinations regression is resolved.

## Project Progress

**Merged/Closed PRs Today (2):**

- **[PR #3028]** `fix: avoid duplicate replies after send_message` (author: ogarciarevett, closed 2026-07-26) — Prevents the agent from sending duplicate replies when `send_message` already wrote a chat reply to the trigger channel. This addresses a long-standing annoyance where the final summary triggered a re-wrap nudge.
- **[PR #3125]** `feat: per-agent-group timezone override` (author: Koshkoshinsk, closed 2026-07-26, core-team) — Adds an optional IANA timezone override per agent group, stored via migration 020. Includes CLI command `ncl groups config update --timezone <IANA>` and resolution logic (`resolveGroupTimezone`) that cascades from group override → install global. This is a significant feature for multi-region deployments.

## Community Hot Topics

The most active items are all **newly opened with 0 comments**, suggesting recent arrivals that haven't yet generated discussion:

- **Issue #3140** — `Explicit-destinations migration: pre-existing wirings have no own-chat destination` ([link](nanocoai/nanoclaw Issue #3140)) — **Highest severity.** Reports that after updating to the explicit-destinations requirement (`to` destination now mandatory), all agent replies in long-standing chat groups are silently dropped. The root cause: pre-existing group wirings lack an "own-chat" destination entry. No comments yet, but this is the most critical open issue.

- **Issue #3136** — `sendToDestination stamps a foreign in_reply_to on outbound rows` ([link](nanocoai/nanoclaw Issue #3136)) — A routing bug where `sendToDestination()` incorrectly reuses the waking batch's `in_reply_to` when the destination has no prior inbound history, potentially corrupting a2a return-path routing.

- **Issue #3132** — `bug: follow-up poll pushes accumulate (trigger=0) messages` ([link](nanocoai/nanoclaw Issue #3132)) — Identifies an inconsistency in the accumulate gate: one consumer path (`processQuery`'s follow-up poller) bypasses the `trigger=1` check, allowing non-triggered messages into active queries. Has a corresponding fix PR (#3133).

## Bugs & Stability

**High Severity (1):**
- **Issue #3134** — `Messages the host sends on an agent's behalf are absent from that agent's context` — An agent has no record of host-sent messages (approval cards, reject-reason prompts, registration notices) because they never pass through the container. **Fix PR #3135 already exists**, authored by the same reporter (brianjcohen). This suggests a quick turnaround is likely.

**Medium Severity (3):**
- **Issue #3140** — Explicit-destinations regression causing silent message drops after update. **No fix PR yet.** Given this affects all pre-existing installations, this is the most urgent unaddressed bug.
- **Issue #3136** — Foreign `in_reply_to` stamping in `sendToDestination()` causing lost messages. **No fix PR yet.**
- **Issue #3132** — Follow-up poll accumulate bypass. **Fix PR #3133 already open** (author: buzali), implementing a `trigger=1` gate on the second consumer path.

**Low Severity:**
- **PR #3139** — `fix(whatsapp): shared-number mode silences the owner` — Addresses a specific WhatsApp channel issue where `fromMe` messages from the owner are incorrectly dropped.

## Feature Requests & Roadmap Signals

- **Per-agent-group timezone override** (PR #3125, merged) — A completed feature that enables timezone-aware scheduling per agent group. Likely to be included in the next release.
- **Dial channel integration** (PR #3050, still open) — Adds Dial to the channel picker/wizard. Active since 2026-07-14, indicating steady progress on expanding channel support.
- **Self-serve wiring controls** (PR #3137, open) — Allows group-scoped agents to inspect their wirings and request approved engagement-policy updates. Suggests the team is moving toward more autonomous agent configuration.
- **OpenCode compatibility** (PR #3122, open) — Fixes main compatibility, custom-endpoint transport, and memory parity with OpenCode. Signals cross-platform integration priorities.

## User Feedback Summary

**Pain Points (from issues):**
- **Migration regressions hurt trust.** Issue #3140 shows that upgrading can silently break existing chat groups with no error feedback ("silently dropped"). This undermines user confidence in version upgrades.
- **Inconsistent message routing.** Issue #3136 and #3132 both describe scenarios where messages are lost or misrouted due to subtle bugs in the accumulation and routing logic. Users are frustrated by non-deterministic message delivery.
- **Poor host-message visibility.** Issue #3134 reveals that agents have no memory of actions performed on their behalf—a fundamental UX gap for multi-agent coordination.

**Use Cases:**
- Multi-agent group chats with long-running conversations (affected by #3140)
- Agent-to-agent (a2a) communication relying on correct `in_reply_to` routing (#3136)
- Participants using host-initiated messages (approval flows, registration) (#3134)

**Satisfaction Signals:** Two PRs merged today (timezone feature, duplicate reply fix) show responsive development, though the high bug count may offset short-term satisfaction.

## Backlog Watch

- **Issue #3132** (bug: follow-up poll accumulate, opened 2026-07-25) — Has a fix PR (#3133) but no comments from maintainers. The fix is straightforward, so this should merge quickly.
- **Issue #3134** (host-sent messages absent from context, opened 2026-07-26) — Also has a fix PR (#3135) from the same day. No maintainer comments yet; watch for merge.
- **Issue #3050 PR** (Dial channel, opened 2026-07-14) — Longest open item among recent PRs (12 days). No comments or updates beyond creation. If Dial integration is a roadmap item, this PR needs attention to avoid stalling.
- **Issue #3136** (foreign `in_reply_to` stamping, opened 2026-07-26) — No fix PR yet. Given the routing implications, this could become high priority once the explicit-destinations regression (#3140) is resolved.

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

# NullClaw Project Digest — 2026-07-27

## Today's Overview
The NullClaw project shows very low activity over the past 24 hours, with only a single open issue updated and no pull requests or new releases. The project appears to be in a quiet phase, though a critical stability bug (#976) continues to affect users on aarch64 Linux systems. No feature development or code merges were recorded today, suggesting maintainers may be focusing on issue triage or other priorities.

## Releases
No new releases were published today. The latest available version remains **v2026.5.29**, which is the version affected by the crash bug described below.

## Project Progress
No pull requests were merged or closed in the last 24 hours. No feature development or bugfix merges were recorded.

## Community Hot Topics
**Most Active Issue:**
- **[#976 — SIGSEGV on every inbound Telegram message](https://github.com/nullclaw/nullclaw/issues/976)** (3 comments, 0 reactions)
  - *Author:* wonhotoss
  - *Summary:* On aarch64 Linux, nullclaw v2026.5.29 segfaults on every inbound Telegram message. The inbound worker thread is spawned with only ~512 KB stack, which overflows. This causes a crash-loop as a systemd service with `Restart=always`, dropping every message.
  - *Underlying need:* Users on ARM64 (aarch64) platforms — typical for Raspberry Pi, low-power servers, or cloud ARM instances — need a stable Telegram gateway. The thread stack size is too small for the platform's ABI or function call depth, indicating a platform-specific threading configuration issue. The lack of replies or workarounds suggests maintainer attention is needed.

## Bugs & Stability
| Severity | Issue | Description | Fix PR Exists? |
|----------|-------|-------------|----------------|
| **Critical** | [#976](https://github.com/nullclaw/nullclaw/issues/976) | SIGSEGV on every inbound Telegram message on aarch64 Linux; crash-loop prevents any message processing. Thread stack overflow (512 KB) | No |
| **High** | (none) | — | — |

**Analysis:** This is a critical production-blocking bug for anyone running NullClaw on ARM64 hardware. The crash is deterministic (every message), data-destructive (messages dropped on restart), and affects the Telegram gateway core functionality. No fix PR or workaround has been identified in public data.

## Feature Requests & Roadmap Signals
No new feature requests were filed today. The primary user feedback signal is the demand for **aarch64 stability**, which may drive the next point release (v2026.5.30 or similar) focused on platform thread configuration fixes.

## User Feedback Summary
The only available user feedback comes from issue #976:
- **Pain point:** Complete service failure on ARM64 Linux — nullclaw becomes unusable as a Telegram gateway.
- **Use case:** Running nullclaw as a systemd service with `Restart=always`, typical for production/always-on deployments.
- **Satisfaction/Dissatisfaction:** Clear dissatisfaction — the user reported a deterministic crash with no resolution after 10 days (issue opened Jul 16, updated Jul 26 with no reply). The 0 reactions suggest this may be an isolated platform issue, but it is no less severe for those affected.

## Backlog Watch
- **[Issue #976](https://github.com/nullclaw/nullclaw/issues/976)** — *Critical, unattended for 10 days.* Opened 2026-07-16, updated 2026-07-26 but with no maintainer response. This is the highest-priority item requiring immediate maintainer attention, as it blocks all ARM64 deployments and sheds user trust. A fix would likely involve increasing the thread stack size (e.g., to 2–4 MB) and/or making it configurable.

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw Project Digest — 2026-07-27

## Today's Overview

IronClaw shows moderate activity today with 3 open issues and 18 pull requests updated in the last 24 hours. The project is in a **high-reliability engineering phase**, with core contributors aggressively consolidating error-handling architecture around the "recoverability contract" (epic #6284) and removing dead code. Seven PRs were merged or closed, reflecting steady cleanup and refactoring momentum. No new releases were published, but the `chore: release` PR #5598 (ironclaw_common 0.5.0, ironclaw_skills 0.4.0) remains open, suggesting a release may be queued pending these architectural changes.

## Releases

No new releases in the last 24 hours. The open release PR #5598 ([nearai/ironclaw PR #5598](https://github.com/nearai/ironclaw/pull/5598)) proposes version bumps with API-breaking changes in `ironclaw_common` (0.4.2 → 0.5.0) and `ironclaw_skills` (0.3.0 → 0.4.0), adding `Copy` implementations. This release has been open since July 3 and appears blocked by ongoing refactoring work.

## Project Progress

**7 PRs merged or closed today:**

- **#6679** (core, L): *Harden struct ratchet and remove dead Gemini API* — Switches from line-oriented scanner to `syn` parsing for multi-line `cfg_attr` and `impl` header checks; removes deprecated Gemini API code.
- **#4032** (regular, M): *Chore: bump wasm group* — Updates `wit-component` and `wit-parser` dependencies (closed after extended stay).
- **#5369** (new contributor, XS): *Fix: suppress Cranelift debug log floods* — Adds Wasmtime compiler targets to Reborn log guard.
- **#6365** (new contributor, XL): *P2b: per-user hosted-MCP discovery* — Reference PR for per-hire connector tools; superseded by rebased #6683.
- **#6677** (core, XL): *Compile-forced recoverability conformance matrix* — Adds `RecoverabilityClass` enum and exhaustive classifier for seven error enums, implementing §11.7 of the architecture spec.
- **#6669** (core, XL): *Move extension host ownership out of composition* — Refactors Reborn extension-host modules into `ironclaw_extension_host::reborn`, removes composition facade.
- **#6680** (core, XS): *Fix: preserve workspace tree state across root navigation* — WebUI fix for breadcrumb navigation state loss.

**Key advances:**
- **Error recoverability** (#6677, #6684): The `RecoverabilityClass` framework (Retry, ModelVisible, Park, Terminal) is now compile-enforced, with PR #6684 collapsing five failure-kind enums into one 35-variant `FailureKind` — a major architectural consolidation.
- **Sandbox cleanup** (#6686): Dead `DockerProcessSandboxBackend` identified for removal, part of the persistent sandbox migration.
- **Attested signing** (#6672): Phase B of the Ledger revival plan introduces signed intent and per-agent key lifecycle, adding cryptographic attestation to agent transactions.

## Community Hot Topics

1. **#6284 — Error-recoverability endgame** ([Issue](https://github.com/nearai/ironclaw/issues/6284)) — 8 comments, 0 reactions. The most commented issue, driving three active PRs today (#6677, #6681, #6684). Epic defining the recoverability contract: every mid-run error must survive, be visible to the model with cause + fix hint, and give the model a turn to act. **Underlying need:** The project is doubling down on autonomous error recovery — this is the defining architectural theme of the current development cycle.

2. **#6640 — Dependencies bump (31 updates)** ([PR](https://github.com/nearai/ironclaw/pull/6640)) — Dependabot PR with "everything-else" group; being rebased. Signals active dependency maintenance despite the focus on core refactoring.

3. **#6672 — Attested signing Phase B** ([PR](https://github.com/nearai/ironclaw/pull/6672)) — Core contributor PR with minimal comments but high architectural significance (cryptographic agent attestation).

## Bugs & Stability

**High Severity:**

- **#6575 (implicit, via PR #6652):** `systemctl --user status ironclaw-reborn.service` reports `Loaded: bad-setting` after `ironclaw onboard` on Linux. Fix PR #6652 ([nearai/ironclaw PR #6652](https://github.com/nearai/ironclaw/pull/6652)) removes erroneous quoting from `WorkingDirectory=` in the systemd unit file. **Status: Fix open.**

**Medium Severity:**

- **#6682 — Daily failure taxonomy** ([Issue](https://github.com/nearai/ironclaw/issues/6682)): Daily benchmark reveals clawbench run (82 non-pass) dominated by "genuine model-quality partial completions" — the agent produces valid, self-verifying but incomplete responses. This is a **quality gap, not a crash**, but signals the error-recoverability (#6284) work is timely.

**Low Severity / Cleanup:**

- **#6686 — Dead code** ([Issue](https://github.com/nearai/ironclaw/issues/6686)): `DockerProcessSandboxBackend` found to have no production constructor, slated for removal.

## Feature Requests & Roadmap Signals

**Active features being built:**

1. **Error recoverability conformance** (#6284, #6677, #6681, #6684): The largest ongoing effort. Once the `FailureKind` collapse (#6684) and mutation-audit harness (#6681) land, the next version should include compile-time guarantees on error classification.

2. **Attested signing** (#6672): Phase B of Ledger revival — signed intents and per-agent key lifecycle. Likely candidate for the next major release (ironclaw_common 0.5.0).

3. **Per-user hosted-MCP discovery** (#6683): Rebased P2b feature enabling worker agents to get per-hire connector tools. Supersedes draft #6365; targets the channel/CLI and sandbox scopes.

**Predicted next version features** (based on #5598 release PR + active work):
- `ironclaw_common` 0.5.0 with `Copy` implementations and API breaks
- `ironclaw_safety` 0.2.3 (compatible)
- `ironclaw_skills` 0.4.0 with breaking changes

## User Feedback Summary

- **Pain point: systemd service broken** (#6575 → #6652) — New Linux users hitting `Loaded: bad-setting` immediately after onboarding. Core contributor fix in review.
- **Pain point: model quality gaps** (#6682) — Daily benchmarks show agents produce "valid, self-verifying partial completions" rather than fully correct outputs. The recoverability epic (#6284) directly addresses this by ensuring the model gets feedback and retry opportunities.
- **Satisfaction signal:** No user complaints about CI instability — the failure taxonomy notes "zero failures due to flakiness," suggesting the test infrastructure is stable.
- **Contributor onboarding:** Two "new contributor" PRs (#5369, #6365) closed today, indicating the project is accessible to external contributors despite the deep refactoring work.

## Backlog Watch

- **#5598 — Release PR** ([PR](https://github.com/nearai/ironclaw/pull/5598)): Open since July 3 (24 days). Blocked by ongoing architecture changes. The API-breaking bumps in `ironclaw_common` and `ironclaw_skills` should be aligned with the ongoing `FailureKind` and signing work before release.
- **#5664 — Actions group dependencies** ([PR](https://github.com/nearai/ironclaw/pull/5664)): Open since July 5 (22 days), bumping 16 GitHub Actions (including Claude Code action from 1.0.88 to 1.0.183). Low risk, likely pending maintainer bandwidth.
- **#6284 — Error-recoverability epic** ([Issue](https://github.com/nearai/ironclaw/issues/6284)): Open since July 19, but is actively driven by 3 open PRs. Not stalled — this is the project's primary focus.
- **#6685 — WASM dependencies** ([PR](https://github.com/nearai/ironclaw/pull/6685)): Fresh (opened today) but bumps critical WASM infrastructure (`wasmtime`, `wasmtime-wasi`, `wit-component`, `wit-parser`). Needs review given the sandbox integration work in progress.

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

# LobsterAI Project Digest — 2026-07-27

## Today's Overview

The LobsterAI project shows a moderate level of maintenance activity over the past 24 hours, with 2 issues and 8 pull requests receiving updates. The majority of PRs (7 of 8) remain open, including several from early April that are now stale, suggesting a backlog of pending feature work and fixes. One issue was closed, while one open bug regarding gateway instability remains active. Despite no new releases being published, the PR queue indicates ongoing work on UI polish, i18n completeness, and OpenClaw gateway reliability. Overall, project health is stable but warrants attention to the growing stale backlog.

## Releases

No new releases were published in the last 24 hours. The latest known release remains dated 2026.4.1.

## Project Progress

One pull request was merged/closed today:

- **[#1325 [CLOSED] feat(ui): 为新建对话图标按钮添加悬停提示](https://github.com/netease-youdao/LobsterAI/pull/1325)** — Added `title` attributes to the "New Conversation" icon button across CoworkView, CoworkSessionDetail, AgentsView, and McpView for native tooltip support when the sidebar is collapsed. A small but meaningful UX improvement for navigation clarity.

Other PRs remain open and are detailed below.

## Community Hot Topics

The following items have drawn the most community attention recently:

- **[Issue #273 [CLOSED] 希望能在Linux上运行](https://github.com/netease-youdao/LobsterAI/issues/273)** — A Linux port request that received 2 comments before being closed. This signals ongoing, albeit latent, demand for cross-platform support beyond Windows.

- **[Issue #1243 [OPEN] 插件配置循环写入导致网关频繁重启](https://github.com/netease-youdao/LobsterAI/issues/1243)** — A critical stability bug affecting all users (non-Qwen models included). The issue has only 1 comment but describes a severe regression: gateways restarting every 5–20 minutes. This is likely a high-impact item causing user frustration.

- **[PR #1249 [OPEN] fix(cowork): DiffView不渲染](https://github.com/netease-youdao/LobsterAI/pull/1249)** — Addresses a visual regression where cowork session diff views fail to render for Claude SDK and OpenClaw tool calls due to overly narrow tool name matching. This PR has been open since April 1st.

**Underlying need**: Users are experiencing silent regressions (DiffView not rendering, gateway flapping) that degrade core workflow experiences. The stale state of these fixes indicates a bottleneck in review or integration bandwidth.

## Bugs & Stability

| Severity | Issue | Status | Description | Fix PR Exists? |
|----------|-------|--------|-------------|----------------|
| **Critical** | [#1243](https://github.com/netease-youdao/LobsterAI/issues/1243) | OPEN | `qwen-portal-auth` plugin causes config loop, triggering OpenClaw gateway restart every 5–20 min. Affects all model configurations. No workaround mentioned. | No |
| **High** | [#1249](https://github.com/netease-youdao/LobsterAI/pull/1249) | OPEN (PR) | DiffView component fails to render for Claude SDK (`str_replace_editor`, `TextEditor`) and OpenClaw (`file_editor`) tool calls due to regex mismatch. | PR #1249 itself |
| **Medium** | [#1325](https://github.com/netease-youdao/LobsterAI/issues/1325) (now closed) | CLOSED | Missing tooltip on "New Conversation" button when sidebar collapsed. Fixed. | PR #1325 (merged) |

The gateway restart bug (#1243) is the most pressing stability concern, as it directly impacts uptime and user experience for all installations. No fix PR has been submitted yet.

## Feature Requests & Roadmap Signals

- **[Issue #273](https://github.com/netease-youdao/LobsterAI/issues/273) (closed) — Linux support**: Though closed, this request reflects a persistent desire for Linux compatibility. As the project matures, a Linux build could expand the user base significantly.

- **[PR #1256 [OPEN] 定时任务配置优化：支持自然语言](https://github.com/netease-youdao/LobsterAI/pull/1256)**: Introduces natural language input for scheduled task cron expressions via an LLM-based parser. Users can choose between natural language and manual cron entry. This is a notable UX innovation that could ship in the next minor release.

- **[PR #1252 [OPEN] 定时任务表单未保存修改确认弹窗](https://github.com/netease-youdao/LobsterAI/pull/1252)** and **[PR #1258](https://github.com/netease-youdao/LobsterAI/pull/1258)**: Both add unsaved changes confirmation dialogs for scheduled task forms, preventing accidental data loss. The duplication suggests early-stage coordination issues, but the feature itself is user-requested.

**Prediction**: The scheduled task natural language input (PR #1256) and unsaved changes guard (PR #1252/#1258) are likely candidates for the next version. The DiffView fix (PR #1249) also appears close to merge.

## User Feedback Summary

- **Pain Points**: The most severe reported pain point is the **gateway restart loop** (Issue #1243), which makes LobsterAI unusable for extended sessions. Users have no known workaround.

- **UX Regressions**: The **missing DiffView rendering** (PR #1249) impacts cowork sessions, a core collaboration feature. Users see raw tool I/O text instead of visual diffs, reducing productivity.

- **Satisfaction Signals**: The closure of PR #1325 (tooltip on new conversation button) suggests maintainers are responsive to small UX friction points. The i18n fix (PR #1257) shows attention to completeness.

- **Unmet needs**: Despite Linux demand (Issue #273), no official Linux build exists. Users on Windows may also be affected by the gateway bug without a Linux fallback.

## Backlog Watch

The following items have been **stale since early April 2026** and remain unresolved, requiring maintainer attention:

| Item | Created | Last Updated | Risk |
|------|---------|--------------|------|
| [#1243](https://github.com/netease-youdao/LobsterAI/issues/1243) — Gateway restart loop | 2026-04-01 | 2026-07-26 | **High** — critical bug, no fix |
| [#1247](https://github.com/netease-youdao/LobsterAI/pull/1247) — OpenClaw model switch recovery | 2026-04-01 | 2026-07-26 | Medium — fixes provider limit edge cases |
| [#1249](https://github.com/netease-youdao/LobsterAI/pull/1249) — DiffView rendering fix | 2026-04-01 | 2026-07-26 | High — UX regression for cowork |
| [#1252](https://github.com/netease-youdao/LobsterAI/pull/1252) — Unsaved changes modal | 2026-04-01 | 2026-07-26 | Low — enhancement, duplicate with #1258 |
| [#1256](https://github.com/netease-youdao/LobsterAI/pull/1256) — Natural language scheduling | 2026-04-01 | 2026-07-26 | Medium — feature, appears complete |
| [#1257](https://github.com/netease-youdao/LobsterAI/pull/1257) — Missing i18n keys | 2026-04-01 | 2026-07-26 | Low — simple fix, pending merge |
| [#1258](https://github.com/netease-youdao/LobsterAI/pull/1258) — Duplicate unsaved changes | 2026-04-01 | 2026-07-26 | Low — overlaps with #1252 |
| [#1259](https://github.com/netease-youdao/LobsterAI/pull/1259) — Gateway bundling refactor | 2026-04-01 | 2026-07-26 | Medium — dependency/build optimization |

**Priority attention needed**: The stale issue #1243 (gateway restart) and stalemated PRs #1247, #1249, and #1259 represent real functional and stability improvements that have been pending for nearly 4 months. Addressing these would significantly boost user confidence and project health.

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

# Moltis Project Digest — 2026-07-27

## Today's Overview
Moltis is in a high-development phase with **8 open pull requests** but no merged activity in the last 24 hours, indicating a focus on review and iteration rather than landing features. No new releases or fresh issues were reported, suggesting current effort is concentrated on finishing substantial cross-cutting work across ACP bidirectional support, Slack integration, Nostr group chat, and PWA reliability. The project remains healthy and actively maintained by a small core team (demyanrogozhin, penso, shixi-li), with `penso` accounting for the majority of contributions.

## Releases
**None.** No new versions were cut in the last 24 hours, and there are no releases listed in the latest data.

## Project Progress
**No PRs were merged or closed today** — all 8 items in the activity window remain open. Notable features under active development:

- **Memory backend (PR #1158):** A new `zvec` vector database backend for memory, feature-gated behind the `zvec` Cargo feature, designed to run against an external `llama-cpp` embedding server.
- **ACP agent exposure (PR #1169):** Moltis now exposes itself as an ACP agent over stdio, enabling other ACP harnesses (Zed, `buzz-acp`) to use Moltis as their agent — previously only the client side existed.
- **ACP selection UX (PR #1171):** Installed ACP clients are moved into the composer model picker, removing the legacy header ACP selector and `Built-in LLM agent` option.
- **PWA push notifications (PR #1173):** Fixes service worker `renotify` bug where second chat messages silently replaced first notifications; now includes sound and alert guarantees.
- **Slack reactions and Block Kit (PR #1166):** Extends acknowledgment reactions (#1165) with phase feedback, reconnect supervision, and rich Block Kit rendering.
- **Nostr NIP-29 support (PR #1168):** Adds group chat support for Buzz channels via NIP-29 over NIP-42 authentication.

## Community Hot Topics
All PRs have **0 comments** and **0 reactions**, indicating either a tight-knit team that communicates off-GitHub or that these are still fresh submissions awaiting review. The most technically significant discussions would likely center on:

- **PR #1158 (memory via zvec/redb):** An experimental vibe-coded backend; may attract architecture debate about memory backends.
- **PR #1170 (privileged tool gating):** Security-sensitive change addressing host command execution via `/sh` in group chats; likely a priority for review.
- **PR #1168 (Nostr NIP-29):** Integration with Buzz (Block's open-source workspace) signals a strategic partnership or broader interoperability push.

## Bugs & Stability
- **PR #1172 [fix] — High severity (UX):** Archived cron sessions were shown by default, causing clutter. Fix applies shared archived-session preference to the Cron tab and includes Playwright regression tests.
- **PR #1170 [fix] — Critical severity (security):** `/sh` and privileged tools were accessible to any sender passing channel access gate, enabling arbitrary host command execution in Discord or group chats. Fix adds per-account operators list.
- **PR #1173 [fix] — High severity (PWA reliability):** Service worker `renotify` bug caused missed notifications when multiple messages arrived in same chat. Fix makes notifications audible and non-replacing.

All three have fix PRs already open and under review.

## Feature Requests & Roadmap Signals
No explicit user feature requests are present in this data. However, roadmap direction is clearly visible from current PRs:

- **Next release likely includes:** ACP bidirectional support (client + agent), Slack real-time acknowledgments with Block Kit, Nostr NIP-29 group chat for Buzz, secure operator gating for privileged commands, and PWA notification reliability.
- **Strategic signals:** The Zvec memory backend (PR #1158) indicates interest in non-vector-database-native storage; Buzz/Nostr integration suggests enterprise/team-focused product expansion.

## User Feedback Summary
No explicit user feedback, comments, or reactions were recorded in the last 24 hours. The project's user base appears to communicate outside of GitHub Issues/PRs (possibly Discord or Matrix). Inferred satisfaction is positive given active feature development; the security fix in PR #1170 suggests a pain point for multi-user/shared-channel deployments.

## Backlog Watch
**No long-unanswered issues** exist in this window — the issue tracker is clean with 0 open/active items. The 8 open PRs range from 1 day to 9 days old (PR #1158 from 2026-07-17) and may need maintainer attention:

- **PR #1158 (memory zvec backend, 9 days open):** Experimental, may need review from memory-subsystem maintainer or decision on whether to merge or close as experimental.
- **PR #1166 (Slack reactions, 3 days open):** Large build on earlier PR #1165; may be waiting for that to land first.
- **PR #1169 (ACP agent, 1 day open):** Fresh; likely needs architectural sign-off.

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

# CoPaw Project Digest — July 27, 2026

## Today’s Overview
CoPaw (QwenPaw) is experiencing a **high-activity day** with 13 open issues and 5 open pull requests updated in the last 24 hours. No new releases were published. The issue tracker is dominated by **regressions and bugs in the v2.0.1 stable release**, including at least three duplicates of an MCP transport hardcoding bug, a critical video delivery pipeline defect, and several integration failures (Matrix E2EE, plugin installation, Cron misfires). The project is actively reviewing two large feature PRs (unified browser SDK and a creator app) while a MiniMax model sync PR from a first-time contributor signals ongoing provider maintenance. Overall, the project is in a **stability-focused phase** with significant community engagement but mounting quality concerns.

## Releases
**None.** No new releases were published today.

## Project Progress
**No PRs were merged or closed today.** The 5 open PRs remain under review:

- **#6276 [feat(browser): unified browser — one SDK, any backend]** — Introduces a control-plane/execution-plane split for browser automation with socketpair transport. Under review.
- **#6284 [feat(apps): add qwenpaw-creator app]** — Adds a script→assets→storyboard→video creation workflow as an app-type plugin. Under review.
- **#6456 [DO NOT MERGE] [feat(context): Visual Compact]** — Implements PawFocus visual context compression for long agent histories, with recovery support. Explicitly marked do-not-merge, likely a design preview.
- **#6477 [first-time-contributor] [docs(faq): align zh sub-section headings with en]** — Minor documentation consistency fix.
- **#6479 [first-time-contributor] [fix(providers): sync MiniMax model baseline]** — Synchronizes hardcoded MiniMax model lists with current upstream API.

## Community Hot Topics

### Active Issues with Most Comments
- **#6470 / #6469 / #6468 — MCP driver ignoring transport config (3x duplicate)** 🟡
  - Author: JohnyLe | Comments: 4 + 1 + 1
  - [Link](agentscope-ai/QwenPaw Issue #6470) | [Duplicate 1](agentscope-ai/QwenPaw Issue #6469) | [Duplicate 2](agentscope-ai/QwenPaw Issue #6468)
  - **Analysis:** Three separate issue filings (likely from the same user) all point to the same root cause: `mcp_stateful_client.py` lines ~800 hardcode `sse_client` instead of reading the `transport: streamable_http` YAML config. No maintainer response yet. The duplicates suggest user frustration or attempts to escalate.

### Underlying Needs
1. **Configuration fidelity:** Users expect MCP transport protocol selection to be respected as configured.
2. **Regression concern:** This appears to be a new issue in v2.0.1, suggesting a codebase change broke previously working behavior.
3. **Missing triage:** No maintainer has acknowledged any of the three duplicates — this is a red flag for project health.

## Bugs & Stability

### Critical Severity 🔴
| Issue | Summary | Severity | Fix PR? |
|-------|---------|----------|---------|
| #6470/6469/6468 | MCP driver hardcodes SSE, breaks `streamable_http` config | **Critical** — blocks all non-SSE MCP connections | None |
| #6474 | `view_video` returns success but video never reaches LLM | **Critical** — visual pipeline silently broken | None |
| #6471 | APScheduler AsyncIOScheduler misfires under long idle | **High** — cron/scheduled tasks unreliable | None |

### High Severity 🟠
| Issue | Summary | Status |
|-------|---------|--------|
| #6473 | Plugin "Agent Kanban" fails with import error on v2.0.1 | No workaround |
| #6476 | Matrix E2EE unusable — olm/vodozemac dependency chain broken | User attempted manual fix, still fails |
| #6460 | High CPU on Edge+Wayland with ComfyUI workflow results | Suspected WebSocket/render issue |
| #6239 | Windows PATH concatenation drops ';' between User+Machine paths | Affects npm global discovery |

### Medium Severity 🟡
| Issue | Summary |
|-------|---------|
| #6472 | JSON files no longer display line numbers in programming mode (v2.0.1 regression) |
| #6480 | `nohup` / `&` detached shell processes never return to idle in `execute_shell_command` |

### Notes
- No fix PRs are open for any of the critical bugs.
- Three bugs (#6470, #6474, #6471) were all filed on July 26 — a **concentrated bug report surge** after the v2.0.1 release.

## Feature Requests & Roadmap Signals

### New Requests (July 26–27)
- **#6475 — `notice_after_complete` tool:** User wants agents to acknowledge long-running shell/sub-agent tasks, reply "task started, will notify you," then handle other conversations, with a completion push notification. **Prediction:** High-value UX improvement, may be considered for v2.1.
- **#6478 — Traditional Chinese localization:** Community member has completed zh-TW translations but requests permission to push. **Prediction:** Likely accepted as a documentation/UI contribution soon.

### In-Progress Features (PRs)
- **#6276 — Unified browser SDK** — If merged, provides a single API for any browser backend.
- **#6284 — QwenPaw Creator** — A full media creation workflow inside CoPaw.
- **#6456 — Visual Compact (PawFocus)** — Context compression for long agent histories; currently exploratory (DO NOT MERGE).

## User Feedback Summary

### Positive Signals
- **Community contributors are growing:** Two first-time-contributor PRs (#6477, #6479) show onboarding is working.
- **Deep engagement:** Users are filing detailed bug reports with root cause analysis (e.g., #6474 includes full code path tracing).
- **Localization efforts:** A user proactively translated the project to Traditional Chinese (#6478).

### Pain Points & Dissatisfaction
- **v2.0.1 stability regression:** Multiple bugs reported as "worked before, broken now" (MCP transport, JSON line numbers, Matrix E2EE).
- **Silent data pipeline failure:** The `view_video` bug (#6474) is particularly concerning — the system reports success while silently dropping user data.
- **No maintainer responses:** None of the 13 open issues have received a maintainer reply. This may indicate bandwidth constraints.
- **Duplicate filings:** Three identical MCP bugs suggest the project lacks a consolidation mechanism, leading to issue tracker noise.

## Backlog Watch

### Issues Needing Maintainer Attention
| Issue | Created | Days Open | Reason for Concern |
|-------|---------|-----------|-------------------|
| #6239 | July 18 | 9 | Windows PATH concatenation bug; severity grows over time but no response |
| #6470/6469/6468 | July 26 | 1 | **Critical duplicate cluster** — needs consolidation and triage urgently |
| #6474 | July 26 | 1 | Critical video pipeline bug, silent data loss |
| #6473 | July 26 | 1 | Plugin installation regression on latest release |

### Unanswered PRs
- **#6276 (feat: unified browser)** — Open since July 20, 7 days without merge or review closure.
- **#6284 (feat: qwenpaw-creator)** — Same age (7 days). Feature PRs of this size typically need maintainer bandwidth to land.

### Recommendation
The most pressing action is **triaging and consolidating the MCP transport bug (#6470 cluster)** and the **video pipeline bug (#6474)**, as both represent core functionality regressions in v2.0.1 with no known workarounds.

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# ZeroClaw Project Digest — 2026-07-27

## Today's Overview

ZeroClaw is experiencing a **major security audit wave** today, with a dramatic surge in issue and PR activity driven by systematic security hardening. The project saw **44 issues updated** (41 open, 3 closed) and **50 PRs updated** (49 open, 1 merged/closed) in the last 24 hours — roughly **double** normal daily volume. This spike is almost entirely attributable to a coordinated security audit conducted by maintainer `@belumume`, who filed **12 security-related issues and RFCs** in a single day (July 26), spanning WhatsApp Web, Gemini, LINE, Bluesky, Reddit, Slack, Telegram, Matrix, and the core runtime. The maintainer team has responded rapidly: a corresponding wave of **fix PRs** (at least 12) were opened on the same day addressing many of these findings. No new releases were cut today, but a **v0.8.4 release PR** (#9376) remains open as a release gate. The project remains highly active and responsibly responsive to security findings, though the volume of open work (49 open PRs, 41 open issues) indicates a widening backlog.

## Releases

**No new releases in the last 24 hours.**

## Project Progress

Only **1 PR was merged/closed** in the last 24 hours, though many remain in-progress. Key open PRs with significant progress include:

- **#9420** (fix: anthropic OAuth support) — Adds optional `auth_mode = "oauth"` for Anthropic model aliases to use stored auth profiles instead of static API keys.
- **#9419** (fix: rotate credentials after rate limits) — Binds reliable-provider attempts to concrete credentials and cools only the credential that returned a retryable 429.
- **#9418** (fix: MCP multiplex stdio) — Routes JSON-RPC responses by child generation and request ID to prevent concurrent call reply confusion.
- **#9416** (fix: tool-access policy in catalog) — Applies `allowed_tools`/`excluded_tools` at built-in tool catalog construction, not just dispatch.
- **#9410** (fix: default command audit logging to disabled) — Changes the default of command audit logging from "enabled but writes nothing" to "disabled" (#9391).

## Community Hot Topics

The most active discussions today are overwhelmingly security-focused:

- **#9348** «WhatsApp Web answers every DM and group under mode = business» (9 comments) — A critical S1 security issue where `allowed_groups` defaults to empty, which incorrectly permits all groups. A fix PR (#9382) is already open.  
  [Issue #9348](https://github.com/zeroclaw-labs/zeroclaw/issues/9348)

- **#9396** (CLOSED) «CLI approval prompt renders tool arguments without stripping control characters» (6 comments) — A security vulnerability where control characters in tool arguments could bypass visual inspection. Has been resolved.  
  [Issue #9396](https://github.com/zeroclaw-labs/zeroclaw/issues/9396)

- **#8654** «skill-review fork panics (out-of-range slice) → daemon SIGSEGV» (5 comments) — A high-severity crash affecting skill-review forking after tool-heavy turns. Marked `status:in-progress`.  
  [Issue #8654](https://github.com/zeroclaw-labs/zeroclaw/issues/8654)

- **#8850** «Move optional channels & tools from compile-time features to runtime plugins» (4 comments) — A long-running architecture RFC to shrink the default binary and eliminate recompilation for new channel/tool adoption.  
  [Issue #8850](https://github.com/zeroclaw-labs/zeroclaw/issues/8850)

- **#8303** «RFC: Goal mode for bounded autonomous session work» (4 comments) — A highly-requested feature for persistent goal-oriented agent sessions with budget exhaustion.  
  [Issue #8303](https://github.com/zeroclaw-labs/zeroclaw/issues/8303)

The underlying need across these discussions is clear: **production-grade security hardening** and **predictable agent behavior** in both failure and boundary cases.

## Bugs & Stability

Today saw a **major security bug intake** across multiple components. Ranked by severity:

### S1 — Security Risk (7 new bugs)

| Bug | Component | Summary | Fix PR? |
|-----|-----------|---------|---------|
| [#9395](https://github.com/zeroclaw-labs/zeroclaw/issues/9395) | plugins/wasi:http | No egress destination policy or configuration knob for WASM plugins | — |
| [#9386](https://github.com/zeroclaw-labs/zeroclaw/issues/9386) | provider:gemini | API key in URL survives sanitize, posted to originating chat | — |
| [#9389](https://github.com/zeroclaw-labs/zeroclaw/issues/9389) | gateway | Unauthenticated `/api/pair` keys lockout on attacker-supplied header | — |
| [#9390](https://github.com/zeroclaw-labs/zeroclaw/issues/9390) | runtime/security | Emergency stop is CLI-only state file that no runtime path reads | — |
| [#9392](https://github.com/zeroclaw-labs/zeroclaw/issues/9392) | channel:line | LINE group messages skip allowlist and pairing handshake | — |
| [#9393](https://github.com/zeroclaw-labs/zeroclaw/issues/9393) | channel:bluesky, reddit | No sender authorization and no central gate | — |
| [#9387](https://github.com/zeroclaw-labs/zeroclaw/issues/9387) | channel:telegram, slack, lark, matrix | Interactive approval responses accepted from any chat member | — |

### S2 — Degraded Behavior (5 bugs)

| Bug | Component | Summary |
|-----|-----------|---------|
| [#9357](https://github.com/zeroclaw-labs/zeroclaw/issues/9357) | ci/runtime | `cargo test -p zeroclaw-runtime --lib` fails 19/20 runs; global mutex poisoning |
| [#9284](https://github.com/zeroclaw-labs/zeroclaw/issues/9284) | runtime | Config flush can overwrite concurrent writes |
| [#9380](https://github.com/zeroclaw-labs/zeroclaw/issues/9380) | plugins | Vendored wit/v0 drifts fail only at registration |
| [#9363](https://github.com/zeroclaw-labs/zeroclaw/issues/9363) | config/gateway | Config metadata remains English in localized UI |
| [#9391](https://github.com/zeroclaw-labs/zeroclaw/issues/9391) | security/audit | Command audit logging defaults to enabled but writes nothing |

### S3 — Minor Issues (1 bug)

- [#9366](https://github.com/zeroclaw-labs/zeroclaw/issues/9366) — WhatsApp Web accepts `approval_timeout_secs` and never reads it (fix PR #9385 open)

**Fix PRs exist** for: #9391 (PR #9410), #9348 (PR #9382), #9366 (PR #9385), #9255 (PR #9403), #9395 (no PR yet), #9284 (no PR yet). The maintainer team is clearly in active remediation mode.

## Feature Requests & Roadmap Signals

Today's feature requests fall into three themes:

1. **Security hardening defaults**: #9397 (RFC: treat empty WhatsApp Web `allowed_groups` as permit-none) signals a shift toward **safe-by-default** configuration semantics.

2. **Runtime plugin architecture**: #8850 (move compile-time features to runtime plugins) and #9126 (validate typed instance config for plugins) continue advancing toward a more extensible architecture. Likely for **v0.9.0**.

3. **Goal mode for autonomous sessions**: #8303 remains a popular (1 reaction) discussion for bounded, persistent agent objectives. This is a strong candidate for **v0.9.x**.

4. **Localization completeness**: #8584 (bring dashboard into Fluent flow) and #9363 (config metadata localization) indicate ongoing investment in **i18n parity** across all surfaces.

## User Feedback Summary

**Pain points visible in today's data:**

- **Windows support gap**: #7462 highlights 74 test failures on Windows 11 (Simplified Chinese), which CI does not catch. A long-standing bug (opened June 10) with no fix PR.
- **Reliability under load**: #9357 shows the runtime test suite fails 19/20 runs on master, with a flaky assertion poisoning a global mutex — this directly impacts developer confidence.
- **Security surprises**: Multiple S1 bugs show that configs intended as "locked down" (WhatsApp `business` mode, LINE allowlists) behave as fully open. Users cannot trust their security posture without deep audit.
- **Localization gaps**: #6548 (bypassed Fluent localization) and #9363 (English metadata in localized UI) are minor but erode trust for international users.

**Satisfaction signals:** The maintainers' rapid response to today's security audit — opening fix PRs on the same day as bug filings — suggests a **highly responsive** project culture that users likely appreciate.

## Backlog Watch

Issues and PRs requiring maintainer attention:

- **#7384** (not in top 30 but referenced in #7462) — Windows test infrastructure. No movement since June. With 74 failing tests, this blocks Windows as a first-class platform.
- **#7462** (14 comments) — [Bug]: 74 test failures on Windows. High-comment, zero-reaction, **no fix PR**. The root cause (Unix-only test commands, path semantics, console encoding) is deep and likely requires CI rearchitecture.
- **#8519** (3 comments, opened June 30) — Reconcile cargo-audit ignores and remediate wasmtime-wasi CVEs. Marked `priority:p1`, `risk:high`, but `status:in-progress` with no PR yet. The security posture of WASM plugins depends on this.
- **#9115** (needs-author-action) — CI runner optimization for Blacksmith runners. Has been waiting for author action since July 17. Could meaningfully improve CI compile times.
- **#8486** (XL, needs-author-action) — OpenAI chat completions endpoint. A major feature PR (37 files changed) that has been awaiting author action since June 29. This is one of the most impactful gateway features on the roadmap.

---

*Digest generated from [github.com/zeroclaw-labs/zeroclaw](https://github.com/zeroclaw-labs/zeroclaw) public data as of 2026-07-27.*

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/kky-wollu/agents-radar).*