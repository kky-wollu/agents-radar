# OpenClaw Ecosystem Digest 2026-07-13

> Issues: 500 | PRs: 500 | Projects covered: 13 | Generated: 2026-07-12 21:25 UTC

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

Based on the GitHub data for OpenClaw (github.com/openclaw/openclaw), here is the project digest for **2026-07-13**.

---

## OpenClaw Project Digest — July 13, 2026

### 1. Today's Overview

OpenClaw is experiencing a period of **extremely high activity**, with 500 issues updated and 500 pull requests updated in the last 24 hours. However, significant maintenance and stabilization challenges are apparent: 200 issues were closed (40% of recent activity), but 300 remain open, and the majority of PRs (354 of 500) are still open. While no new releases exist, the repository is dense with P0/P1 critical bug reports, including major regressions and memory leaks affecting session state and message delivery. The community is highly engaged, but maintainer bandwidth appears strained, as many high-severity items remain in review queues (e.g., `needs-maintainer-review`, `needs-product-decision`).

### 2. Releases

**None.** No new releases were published for this digest period.

### 3. Project Progress

In the last 24 hours, **146 PRs were merged or closed**, indicating substantial development velocity. Key advancements include:

- **Orchestration Internals:** A refactor (Issue #104871, closed) targeting high-churn orchestration surfaces into explicit state and ownership boundaries without changing public contracts was reviewed and accepted.
- **Bug Fixes:** Several high-impact bugs were addressed:
    - **ACP Runtime on Windows:** A fix was merged for `browser: EINVAL` when spawning the `claude` adapter via ACP (Issue #93465, closed).
    - **Feishu Drive Pagination:** A fix for false "File not found" errors on pages beyond the first was resolved (Issue #93928, closed).
    - **Browser File Chooser:** Flaky file upload flows that misreported stale-click failures as timeouts were fixed (Issue #38844, closed).
    - **Backup Race Condition:** The `openclaw backup create` command failing with ENOENT due to session cleanup during backup was resolved (Issue #67417, closed).
- **Feature Work:** A major feature, the "beta3 wake replay foundation" (PR #105660, open), is currently under review. This large PR (XL) aims to add a durable wake/replay mechanism.

### 4. Community Hot Topics

The most engaged issues reveal deep-seated user concerns about **agent visibility, data integrity, and platform support**.

1.  **Portability of Clawdbot (Issue #75)** : With **110 comments** and **81 thumbs-up**, this is the runaway top topic. Users are demanding Linux and Windows apps to match the macOS/iOS experience. This signals a critical community need for cross-platform agent management.
    - [Issue #75: Linux/Windows Clawdbot Apps](https://github.com/openclaw/openclaw/issues/75)

2.  **"See attached image" Bug (Issue #99241 & #104721)** : Two distinct but related issues about tool outputs being replaced by unreadable image placeholders are generating significant heat. This is a **critical usability problem** that breaks the core agent feedback loop.
    - [Issue #99241: Tool outputs render as image attachments](https://github.com/openclaw/openclaw/issues/99241)
    - [Issue #104721: Tool results return "(see attached image)" literal string](https://github.com/openclaw/openclaw/issues/104721)

3.  **Memory Trust & Security (Issue #7707 & #10659)** : Users are actively concerned about **memory poisoning** and **credential leaks**. The desire for trust tagging by source (#7707) and masked secrets (#10659) shows a shift toward security-conscious AI agent usage.
    - [Issue #7707: Memory Trust Tagging by Source](https://github.com/openclaw/openclaw/issues/7707)
    - [Issue #10659: Feature Request: Masked Secrets](https://github.com/openclaw/openclaw/issues/10659)

### 5. Bugs & Stability

The project is facing a **stability crisis**, with several P0 (critical) and P1 (high) regressions actively degrading user experience.

- **P0 - Critical: "See attached image" Regression (Issue #104721)**: Tool results are replaced with a literal placeholder string, breaking all automated workflows. This is a **current, severe regression**.
    - *Fix PR?* No specific fix PR is linked, though related PRs (#102082 for Slack chrome suppression) attempt to address related display issues.
- **P0 - Critical: Gateway Memory Leak (Issue #91588)**: RSS grows from 350MB to 15.5GB over days, causing OOM crashes and restart loops. This is a **major infrastructure stability threat**.
    - *Fix PR?* None identified.
- **P0 - Critical: CLI Preflight Corrupts State DB (Issue #101290)**: Running CLI checks while the gateway is live can corrupt the SQLite database (`malformed database image`), causing cascading failures.
    - *Fix PR?* None identified.
- **P1 - High: Repeated Hard Resets & Message Loss (Issues #63216, #102020, #39476)**: Multiple reports of session conflicts, duplicate messages, and silent context-overflow resets indicate deep-seated session management issues.
    - *Fix PR?* PR #103823 (subagent double-resume fix) is part of this stability push.
- **P2 - Moderate: Prompt Cache Breaks Across Boundaries (Issue #102175) & Provider Fallback Logic (Issue #47910)**: These bugs degrade efficiency and reliability, showing growing pains in the architecture's complexity.

### 6. Feature Requests & Roadmap Signals

The community is actively shaping the future of OpenClaw with requests focused on **safety, granular control, and administrative insight**.

- **High Priority (Likely in next major release)** :
    - **Masked Secrets (Issue #10659)** : Very popular request to prevent agents from reading raw API keys. Likely to be prioritized given security implications.
    - **Filesystem Sandboxing (Issue #7722)** : Users need configurable `allow`/`deny` paths for `tools.fileAccess`.
    - **Provider Fallback by Failure Class (Issue #47910)** : Smart failover that doesn't retry auth-failed providers. Already has a linked PR (#103823) suggesting active development.
    - **Agent Max Iteration / MaxTurns (Issues #9912 & #6890)** : To prevent agents from looping infinitely, especially with certain models.

- **Medium Priority (Pipeline items)** :
    - **Webhook Multi-Turn Support (Issue #11665)** : Fixing the documented but non-functioning `sessionKey` for webhooks.
    - **Dynamic Model Discovery (Issue #10687)** : For providers like OpenRouter with rapidly changing model catalogs.
    - **Configurable Sub-Agent Announce (Issue #8299)** & **Denylist for Exec-Approvals (Issue #6615)** : User-facing polish and safety.

### 7. User Feedback Summary

User sentiment is a mix of **high engagement and deep frustration**.

- **Frustration**: The most vocal feedback centers on **broken reliability**. Phrases like "This is completely broken" (from Issue #104721) and reports of agents "silently dropping parameters" or "repeating hard resets" indicate a trust deficit in the current stable channel. Users feel the "stable" label is misleading given the volume of regressions.

- **Dissatisfaction**: There is significant friction with **missing platform support** (Linux/Windows Clawdbot - Issue #75) and **poor user experience on specialized hardware** (e.g., screen readers failing due to unicode symbols in TUI - Issue #9637).

- **Satisfaction**: High engagement (110 comments on platform request) shows a strong, invested community that *wants* the product to succeed. The requests for advanced security features (masked secrets, denylists) imply sophisticated users who rely on OpenClaw for serious work and are invested in its evolution.

### 8. Backlog Watch

Several critical or long-standing issues remain in the `needs-maintainer-review` or `clawsweeper:needs-product-decision` state, indicating potential bottlenecks.

- **Critical Memory Leak (Issue #91588)** : P0, 18 comments, **needs-maintainer-review** and **needs-product-decision**. This is a top risk for production deployments.
- **Stale: Heartbeat Isolated Mode Regressions (Issue #65161)** : P2, 15 comments, stale since April. The `clawsweeper:needs-live-repro` tag suggests maintainers cannot reproduce it, leaving users in limbo.
- **Stale: Silent Abandonment of Task Execution (Issue #59618)** : P2, 6 comments, stale for 3 months. Auto-compaction during tool use silently kills the task.
- **Heavy PRs Awaiting Maintainer Attention**: **PR #69822** (`socket.drain` for session evictions), **PR #80497** (Plugin SDK for diagnostic events), and **PR #95996** (fix for yielded parent runs) all have detailed proofs and are marked "ready for maintainer look" but are stuck in queue. These are medium-to-large changes that block subsequent merge requests.

**Conclusion**: OpenClaw is a **highly active but currently unstable** project. The community is demanding and loyal, but maintainers must prioritize addressing the P0 regressions (especially the "see attached image" bug and memory leak) to restore confidence in the stable release channel. The backlog of important features (like masked secrets and sandboxing) is healthy, but the immediate focus must be on **stability and hardening**.

---

## Cross-Ecosystem Comparison

# AI Agent / Personal AI Assistant Open-Source Ecosystem — Cross-Project Comparison Report
**Date:** 2026-07-13

---

## 1. Ecosystem Overview

The personal AI agent open-source ecosystem is experiencing a **stabilization crisis masked by high development velocity**. While projects like OpenClaw, ZeroClaw, IronClaw, and NanoClaw show intense activity (cumulatively 800+ issues and 700+ PRs updated in the past 24 hours), the majority are grappling with **post-release regressions, CI instability, and user trust erosion from broken upgrade paths**. Two distinct dynamics are emerging: established projects (OpenClaw, Hermes Agent) are prioritizing hardening and security governance, while newer or leaner implementations (NanoBot, LobsterAI, CoPaw) are addressing fundamental reliability gaps in multi-agent, cross-platform, and memory persistence features. The ecosystem is converging on **sandboxing, prompt caching, session continuity, and observability** as critical shared requirements—but each project's approach to these challenges reveals diverging architectural priorities and target user segments.

---

## 2. Activity Comparison

| Project | Issues Updated (24h) | PRs Updated (24h) | Releases (24h) | Health Score | Key Signal |
|---------|---------------------|-------------------|----------------|--------------|------------|
| **OpenClaw** | 500 | 500 | None | 🟡 **Unstable** | 200/500 issues closed; P0 regressions active |
| **ZeroClaw** | 49 | 50 | None | 🟡 **High risk** | 5 S1 bugs open; 3-month-old context budget bug unfixed |
| **IronClaw** | 9 | 50 | None | 🟢 **Active** | 33 PRs merged; CI red ~70% of July |
| **NanoClaw** | 3 | 13 | None | 🟢 **Rapid hardening** | 2 crashes fixed; 2 P0 regressions with fix PRs |
| **Hermes Agent** | 50 | 50 | None | 🟢 **Healthy** | 31 issues closed; 4 PRs merged |
| **CoPaw** | 19 | 10 | None | 🟡 **Post-release stress** | 14 open bugs vs v2.0.0; skill system broken |
| **PicoClaw** | 5 | 3 | None | 🟡 **Moderate** | Matrix sync critical bug (11 days open) |
| **NanoBot** | 3 | 11 | None | 🟢 **Healthy** | 1 PR merged; security fix landed |
| **LobsterAI** | 1 | 2 | None | 🟢 **Stable** | Data resurrection fix merged |
| **Moltis** | 0 | 0 | None | ⚪ **Idle** | No activity |
| **TinyClaw** | 0 | 0 | None | ⚪ **Idle** | No activity |
| **NullClaw** | 0 | 0 | None | ⚪ **Idle** | No activity |
| **ZeptoClaw** | 0 | 0 | None | ⚪ **Idle** | No activity |

**Health Score Legend:** 🟢 Active/Healthy — 🟡 Moderate/Risk — 🔴 Critical — ⚪ Idle

---

## 3. OpenClaw's Position

**Advantages vs. peers:**
- **Scale and momentum:** 500 issues/500 PRs updated daily—3× the activity of the next busiest project (ZeroClaw or Hermes). This is both an asset (more contributions) and a liability (review bottleneck).
- **Feature depth:** The closest to a full-featured personal AI agent, with advanced orchestration, sub-agents, wake/replay mechanisms, and ACP runtime for cross-platform adapters.
- **Community investment:** The most vocal and demanding user base—110 comments on a single platform request (Issue #75) indicates deep engagement and loyalty.

**Technical approach differences:**
- OpenClaw has the **most complex sub-agent and orchestration architecture**, but this complexity has generated the highest density of P0 regressions (memory leaks, session state corruption, output placeholder bugs).
- Its Rust core (inferred from "ACP runtime," "Clawdbot") differs from Python-dominant peers like NanoBot or LobsterAI, providing performance advantages but slower iteration on fixes.

**Community size comparison:**
- OpenClaw leads in absolute issue/PR volume (5× CoPaw, 10× NanoBot), but its **open-to-closed ratio (60% issues open, 71% PRs open)** signals that maintainer bandwidth is strained. Hermes Agent closes more efficiently (62% issues closed, ~8% PRs merged/closed daily).

**OpenClaw's core challenge:** Restoring trust in the "stable" channel while managing the overhead of its own success. The P0 "see attached image" regression and gateway memory leak are existential risks for production deployments.

---

## 4. Shared Technical Focus Areas

Requirements emerging across **multiple projects**, with specific project mentions:

### a. Prompt Caching / Token Efficiency
- **NanoBot** (#4867): "+60 seconds per turn" without cache—"totally unusable" on Ollama.
- **PicoClaw** (#3251): PR adding cache token capture for Anthropic providers.
- **OpenClaw** (#102175): Prompt cache breaks across conversation boundaries.

### b. Multi-Agent Session Management & Isolation
- **LobsterAI** (#2293): USER.md overwritten on restart for all agents—data loss.
- **NanoClaw** (#3023): All Claude agents silently capped at 32K output tokens.
- **ZeroClaw** (#5808): Default context budget ~3.3× too small on first iteration.

### c. Cross-Platform / Adapter Reliability
- **Hermes Agent**: 6+ platform-specific bugs (WhatsApp routing, SimpleX silent drops, Windows file I/O, Feishu crashes, Mattermost threads).
- **CoPaw** (#5999): Cross-channel session continuity (Console, Feishu, DingTalk).
- **NanoBot** (#4855): Guided setup for Feishu, QR handoff—new user onboarding.
- **OpenClaw** (#75): Linux/Windows Clawdbot apps—110 comments, 81 👍.

### d. Security / Governance
- **OpenClaw** (#7707, #10659): Memory trust tagging by source, masked secrets—high community demand.
- **NanoClaw** (#2986): Unified guard seam—every privileged action passes `guard()`.
- **CoPaw** (#5994, #5982): Governance fires on every operation in AUTO mode; shell execution approval fatigue.
- **IronClaw** (#6009, #6010): GLM-5.2 model availability and inference hangs.

### e. Observability & Debugging
- **Hermes Agent** (#18127): "Hard to know whether agent is making progress, stuck, or burning iteration budget."
- **NanoClaw** (#3016): Every rate limit event logged as quota error—82 false alarms/week on one install.
- **ZeroClaw** (#6641): Turn-level OTel trace correlation (open 60 days, in-progress).
- **IronClaw** (#6011): Daily CI failure taxonomy—systematic approach to observability.

### f. Upgrade / Migration Stability
- **CoPaw**: 6+ v1.x → v2.0.0 migration issues (session mapping, media compatibility, missing features).
- **OpenClaw** (#104871): Orchestration refactor that changes internal state boundaries without public contract changes—user-visible regressions.

### g. Sandboxing & Containers
- **OpenClaw** (#7722): Filesystem sandboxing with configurable allow/deny paths.
- **NanoClaw** (#3027): Container startup failure from root-owned TMPDIR—agent silence on WhatsApp.
- **Hermes Agent** (#63361): Daytona sandbox image comparison missing on resume.
- **CoPaw** (#5979): Electron CLI crashes in sandbox (root mapping issue).

---

## 5. Differentiation Analysis

| Dimension | Projects | Characteristic |
|-----------|----------|----------------|
| **Target User** | OpenClaw, Hermes Agent | Power users / production operators—advanced orchestration, sub-agents, multi-model |
| | NanoBot, LobsterAI | Individual developers—simpler setup, local model focus (Ollama), UI polish |
| | CoPaw, ZeroClaw | Enterprise teams—cross-channel, governance, audit trails, skilling |
| **Primary Language** | IronClaw (Rust), OpenClaw (Rust-core) | Performance-critical, complex internals |
| | NanoBot, LobsterAI, CoPaw (Python) | Faster iteration, broader contributor base |
| | Hermes Agent (mixed) | Multi-language with platform adapter complexity |
| **Architecture Philosophy** | OpenClaw, ZeroClaw | Maximalist—feature-rich, complex orchestration, WASM plugins |
| | NanoBot, PicoClaw, TinyClaw | Minimalist—lean runtime, container-based, skill-focused |
| | IronClaw | Safety-first—test taxonomy, CI hardening, Responses API coverage |
| **Distribution Model** | OpenClaw, Hermes Agent | Heavy CLI/TUI + mobile companion apps |
| | NanoClaw, ZeroClaw | Gateway/channel-centric (WhatsApp, Telegram, Matrix, Slack) |
| | LobsterAI, CoPaw | Desktop-first with chat UI |
| **Maturity Phase** | IronClaw, Hermes Agent | Stabilization—CI hardening, bug bash taxonomy, release blocking |
| | NanoClaw, CoPaw | Post-release cleanup—fixing regressions from new features |
| | OpenClaw, ZeroClaw | Scale stress—high activity but unstable, reviewer bottleneck |

---

## 6. Community Momentum & Maturity

### Activity Tiers

**Tier 1 — Rapidly Iterating (High Velocity, Some Instability)**
- **OpenClaw**: 500+ issues/PRs daily, but 60% open ratio signals bottleneck
- **ZeroClaw**: 50+ issues/PRs daily, deep milestone push (v0.8.3)
- **IronClaw**: 50 PRs updated, highest merge rate (33/day)

**Tier 2 — Healthy Motion (Active, Controlled)**
- **Hermes Agent**: 50 issues/50 PRs, efficient closure (62% closed)
- **NanoClaw**: 3 issues/13 PRs, targeted hardening—2 P0s fixed same day
- **CoPaw**: 19 issues/10 PRs, post-v2.0 stabilization with community engaged

**Tier 3 — Stable/Low Activity**
- **NanoBot**: 3 issues/11 PRs, healthy but lower volume
- **PicoClaw**: 5 issues/3 PRs, moderate with one critical bug
- **LobsterAI**: 1 issue/2 PRs, stable but quiet

**Tier 4 — Idle (No Recent Activity)**
- **Moltis, TinyClaw, NullClaw, ZeptoClaw**: Unclear if dormant or stable—no data to assess

### Stabilization vs. Innovation

- **Projects in stabilization phase**: IronClaw (CI hardening), Hermes Agent (platform adapter fixes), NanoClaw (re-wrap nudge, guard seam)
- **Projects in feature expansion**: ZeroClaw (WASM plugins, memory overhaul, OpenAI endpoint), CoPaw (per-session model overrides, cross-channel)
- **Projects balancing both**: OpenClaw—adding wake/replay foundation while fighting P0 regressions

### Community Health Indicators

| Metric | Strongest | Most Concerning |
|--------|-----------|----------------|
| First-time contributor engagement | CoPaw (4/10 PRs from new contributors) | LobsterAI (single issue, no new PRs) |
| Issue response time | NanoClaw (fix PR same day as bug report) | ZeroClaw (#5808, 88 days open, no fix PR) |
| Upgrade path management | Hermes Agent (31 issues closed, migration supported) | CoPaw (6+ v1→v2 migration failures) |

---

## 7. Trend Signals

**Extracted from community feedback across all projects:**

### Signal 1: "Secure by Default" Is Becoming a Hard Requirement
Users across OpenClaw (masked secrets, memory trust tags), NanoClaw (unified guard seam), and CoPaw (governance fatigue) are demanding **agent-level security controls that don't break workflows**. The trend is toward **configurable safety** (allow/deny lists, approval tiers, audit logs) rather than all-or-nothing approval prompts. Projects that fail to provide this will lose enterprise adopters.

**Value for AI agent developers:** Ship sandboxing *before* users ask for it. The community is punishing projects that release governance as an afterthought.

### Signal 2: Cross-Platform Agents Are the Most Fragile—And Most Valued
WhatsApp, Telegram, Matrix, Feishu, Slack, SimpleX—the platform adapter is the most common failure point across Hermes Agent (6+ bugs), PicoClaw (Matrix sync), NanoClaw (container startup via WhatsApp), and CoPaw (missing Feishu features). Meanwhile, OpenClaw's #75 (Linux/Windows apps) has 110 comments—the most engaged issue in the entire ecosystem.

**Value for AI agent developers:** Adapter reliability is a competitive moat. Users tolerate agent bugs but not silent delivery failures. Invest in platform-agnostic test harnesses.

### Signal 3: Prompt Caching Is the New "Table Stakes" Performance Requirement
NanoBot's "totally unusable" +60s/turn with Ollama, OpenClaw's cache boundary breaks, and PicoClaw's cache token tracking PR all point to the same insight: **local and cloud model costs drive caching to priority #1**. Users are willing to sacrifice features for responsiveness.

**Value for AI agent developers:** Cache-aware prompt orchestration (breakpoint tokens, prefix stabilization) is not optional—it's the difference between "works" and "unusable" on local models.

### Signal 4: The "Stable" Label Is Losing Meaning
OpenClaw's P0 regressions in a "stable" channel, CoPaw's broken v2.0 upgrade path, and ZeroClaw's 3-month-old context budget bug all erode trust in semantic versioning. The community is increasingly treating "latest" as "experimental."

**Value for AI agent developers:** Adopt a **canary release model** (feature-flagged, opt-in) before cutting "stable" releases. The damage from a premature release (CoPaw: 14 open post-v2.0 bugs) can outweigh months of feature development.

### Signal 5: Multi-Agent Architecture Complexity Is Outpacing Reliability
OpenClaw (sub-agent double-resume), ZeroClaw (fork panics, skill-review SIGSEGV), LobsterAI (agent ID resurrection, USER.md overwrite), and CoPaw (tool_call/tool_result pairing breakage) all suffer from **state management bugs in multi-agent workflows**. The industry is reaching the limits of simple session-per-agent designs.

**Value for AI agent developers:** Invest in **deterministic state machine models** for agent sessions. The current pattern of "agent as conversation participant" is leading to untraceable bugs when agents interact.

### Signal 6: Observability Is Demand-Pull, Not Feature-Push
Hermes Agent (#18127: "hard to know whether agent is making progress"), NanoClaw (#3016: noisy logs masking real errors), and IronClaw (#6011: CI taxonomy) all reflect users forced to build their own monitoring because built-in observability is insufficient. The community is calling for **per-turn traces, live session inspection, and actionable error signals**.

**Value for AI agent developers:** Treat observability as a **product feature**, not an operational afterthought. The projects winning user trust (IronClaw, Hermes Agent) are the ones investing in systematic failure taxonomy.

---

**Bottom line:** The personal AI agent ecosystem is in a **consolidation burst**—200+ closed bugs across 9 active projects in 24 hours, but the trust deficit from unstable releases, platform adapter fragility, and insufficient caching is the defining challenge for the next quarter. The winners will be projects that ship **reliable fundamentals** (caching, sandboxing, session persistence) over ambitious feature sets.

---

## Peer Project Reports

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot Project Digest — 2026-07-13

## 1. Today's Overview
The NanoBot repository shows moderate activity over the past 24 hours, with 3 issues updated and 11 pull requests active. The project remains in a healthy development cadence, with one PR merged (a security-focused workspace access fix) and a steady flow of open proposals across bug fixes, feature work, and refactoring. No new releases were published today, suggesting the team is consolidating changes rather than cutting a new version. The community is actively engaged on a performance-critical issue around Ollama caching, which remains the most discussed topic.

## 2. Releases
**No new releases.** The latest stable version remains unreleased since the previous cycle; contributors appear focused on landing pending PRs before the next cut.

## 3. Project Progress
- **PR #4892** — [CLOSED] `fix(webui): allow remote workspace access reduction` (by Re-bin). A security improvement that lets remote WebUI sessions reduce their own permissions without altering the workspace-wide default, and limits access escalation to localhost/native clients. This was the only merged PR today.
- The 10 other open PRs continue to be updated, but none reached a merge state today.

## 4. Community Hot Topics
- **Issue #4867** — *[CLOSED] Preserve exact prompt prefix to enable caching in Ollama* (4 comments). The most active discussion. Author reports NanoBot adds **+60 seconds per turn** with Ollama due to prompt prefix variation breaking KV-cache reuse, making the experience "totally unusable" even with 32GB VRAM. The community is debating prefix stabilization strategies to match what llama.cpp/Ollama expect for cache hits. → [Issue #4867](https://github.com/HKUDS/nanobot/issues/4867)
- **PR #4371** — `fix(cache): add breakpoint before Recent History so the stable system prefix caches` (by sumleo). Directly addresses the same caching pain point as Issue #4867, adding a "breakpoint" token before the ever-growing Recent History block so the stable system prompt prefix can be cached. This PR is actively discussed and has a `conflict` label, indicating it may need rebase or review. → [PR #4371](https://github.com/HKUDS/nanobot/pull/4371)
- **PR #4855** — `feat(webui): add guided setup flows` (by Re-bin). A large feature PR adding productized Channel setup flows with validation, QR handoff, and Feishu assistant management. Updated today with additional comments, signaling maintainer interest. → [PR #4855](https://github.com/HKUDS/nanobot/pull/4855)

## 5. Bugs & Stability
| Severity | Issue | Summary | Fix PR? |
|----------|-------|---------|---------|
| **High** | [#4894](https://github.com/HKUDS/nanobot/issues/4894) | `prune_dream_sessions()` fails to match base64-encoded Dream session filenames (e.g., `ZHJlYW06…jsonl`); uses old `dream_*.jsonl` glob. Causes orphaned files. | No fix PR yet |
| **Medium** | [#4893](https://github.com/HKUDS/nanobot/issues/4893) | `/dream-log` and `/dream-restore` show non-Dream commits (backup, manual edits) because no Git commit filter is applied. | No fix PR yet |
| **Medium** | [PR #4813](https://github.com/HKUDS/nanobot/pull/4813) (open) | `.strip()` crashes on `list[dict]` multimodal content in `AgentLoop`. Two code paths affected. | PR #4813 exists (open, conflict) |
| **Low** | [PR #4842](https://github.com/HKUDS/nanobot/pull/4842) (open) | `asyncio.CancelledError` unhandled in MCP shutdown when subprocess times out. | PR #4842 exists (open) |

**Note:** Both Dream-related bugs (#4894, #4893) were opened by the same author (groudas) and both lack any fix PRs — these are low-effort regressions that could be addressed quickly.

## 6. Feature Requests & Roadmap Signals
- **Prompt prefix caching (Issue #4867, PR #4371)** — Strong community demand. Likely to land soon in a patch release once #4371 is rebased. Cache breakpoints are a standard pattern and would dramatically improve Ollama usability.
- **Model presets bound to sessions (PR #4866)** — by chengyongru. Persists selected model/preset in session metadata, captures immutable LLM runtime per turn, and propagates through subagents. This is a significant architectural improvement for multi-model workflows and is labeled `priority: p1`. Likely to be merged within the next 1–2 weeks.
- **Guided setup flows (PR #4855)** — Productizes Channel configuration with validation, QR handoff, and Feishu integration. If merged, this will be a major UX upgrade for new users.
- **Sustained-goal opt-in flag (PR #4879)** — Gates the `long_task` auto-continuation behind an opt-in to avoid blocking user interaction. Labeled `priority: p2` but addresses a real usability complaint; could make it into the next release.
- **Weather Skill example (PR #4145)** — An older PR nearing completion, adding a documented weather skill. Low risk, good for onboarding new contributors.

## 7. User Feedback Summary
- **Pain point #1 (critical):** Ollama prompt caching — users report **60-second delays per turn** on local models, making NanoBot effectively unusable with Ollama on modest hardware. The community is vocal about this being a "totally unusable" experience (Issue #4867).
- **Pain point #2 (moderate):** Dream sessions regression — after switching to base64-encoded filenames, pruning and log/restore commands broke silently, causing clutter and confusion (Issues #4894, #4893).
- **Pain point #3 (minor):** Multimodal content crashes in `AgentLoop` — users receiving image data from channels hit `AttributeError` due to missing list-type handling (PR #4813).
- **Positive signal:** The guided setup flows PR (#4855) and model-preset binding (#4866) respond to longstanding requests for easier configuration and multi-model session management.

## 8. Backlog Watch
The following items require maintainer attention:

| Item | Age | Status |
|------|-----|--------|
| [PR #4145](https://github.com/HKUDS/nanobot/pull/4145) — Weather Skill | 42 days | Open, no recent merges; needs final review or closure |
| [PR #4371](https://github.com/HKUDS/nanobot/pull/4371) — Cache breakpoint for Ollama | 27 days | Conflict label; highly requested fix is stalled |
| [PR #4616](https://github.com/HKUDS/nanobot/pull/4616) — Route subagent results in-turn | 12 days | Conflict label; core agent routing change |
| [PR #4650](https://github.com/HKUDS/nanobot/pull/4650) — Extract turn history recovery | 11 days | Conflict label; refactor with no recent activity |
| [Issue #4894](https://github.com/HKUDS/nanobot/issues/4894) — Dream pruning regression | 1 day | New, no PR; trivial fix for base64 glob |
| [Issue #4893](https://github.com/HKUDS/nanobot/issues/4893) — Dream log/restore filtering | 1 day | New, no PR; needs Git commit filtering |

**Assessment:** The overlap between #4867 (user complaint) and #4371 (stalled fix) represents the highest-risk backlog item for user satisfaction. The two new Dream bugs are low-hanging fruit that would benefit from a quick patch.

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent Project Digest — 2026-07-13

## Today's Overview

Hermes Agent is in a **high-activity maintenance and stabilization phase** with 50 issues and 50 PRs updated in the past 24 hours. The project shows strong community engagement with 19 open/active issues and 46 open PRs, while maintainers have closed 31 issues — indicating a healthy triage and fix cadence. The milestone backlog of open PRs (46) suggests a large pipeline of contributions awaiting review, largely from feature branches and experimental work. No new releases were published today, and attention is concentrated on resolving platform-specific bugs (Windows, WhatsApp, Feishu), sandbox reliability, and multi-agent orchestration capabilities.

## Releases

No new releases today. The last notable release remains **v0.12.0** (commit range around `bbbce926`). Users should monitor for fixes to Windows file I/O, session state migration, and gateway connectivity issues noted in recent bug reports before the next planned release.

## Project Progress

The following PRs were **merged or closed** today (4 total):

- **#18109** [CLOSED, not-planned] — `feat(environments): universal RTK command rewriting across all backends` — A broad refactor of Rust Token Killer command rewriting, extended from Local to Docker/SSH/Modal/Daytona/Singularity backends. **Not planned for merge** due to blast radius across security and compatibility boundaries.
- **#18107** [CLOSED, not-planned] — `feat(providers): add Manifest open-source LLM router` — Proposed integration of Manifest as a built-in aggregator provider. Marked not-planned, likely due to provider ecology concerns.
- **#18084** [CLOSED, implemented-on-main] — `fix(skills): align creative ideation skill name` — A small but impactful fix aligning skill frontmatter names with directory slugs to prevent lookup confusion.
- Additional 1 other PR closed (not in top 20 by comments).

Key **regression and bug fixes confirmed on `main`** via issue closure labels include:
- WhatsApp group message routing fix (`send_message` no longer routes to home channel)
- Reasoning token tracking for chat_completions mode models
- Session title leakage of thinking tokens (e.g., MiniMax-M2.7, DeepSeek-R1)
- Windows local file read fixes for `D:\` drives and non-WSL environments
- Feishu plugin executor shutdown preventing message replies
- Dashboard permission errors on stale gateway.lock
- Mattermost thread session isolation

## Community Hot Topics

### Most Engaged Issues (by comments)

1. **#18080** (28 comments, 50 👍) — *Improved Themes for Dashboard* — [Issue Link](https://github.com/NousResearch/hermes-agent/issues/18080) — CLOSED. A high-reaction feature request to replace non-standard serif fonts, low-contrast color schemes, and improve dashboard readability. The strong upvote count signals widespread user dissatisfaction with the current visual design.

2. **#18646** (8 comments) — *WhatsApp group message routing bug* — [Issue Link](https://github.com/NousResearch/hermes-agent/issues/18646) — CLOSED. A critical functional bug that caused group-targeted WhatsApp messages to be delivered to a user's home channel instead.

3. **#18529** (5 comments) — *Session title leaks reasoning tokens* — [Issue Link](https://github.com/NousResearch/hermes-agent/issues/18529) — CLOSED. A privacy-relevant bug where thinking model outputs leaked into auto-generated session titles.

4. **#46265** (4 comments, OPEN) — *SimpleX adapter silently drops all DM replies* — [Issue Link](https://github.com/NousResearch/hermes-agent/issues/46265) — An ongoing issue where `@<contactId>` syntax for SimpleX DMs resolves incorrectly, causing silent delivery failures. This is the **top open issue by engagement** and has been open since June 14 without a fix in flight.

5. **#63361** (3 comments, OPEN) — *Daytona sandbox image comparison missing on resume* — [Issue Link](https://github.com/NousResearch/hermes-agent/issues/63361) — A reliability concern for Daytona cloud sandbox environments.

### Underlying Needs

Community posts reveal **three core unmet expectations**:
- **Demand for visual polish**: The dashboard theme issue (50 👍) shows users want professional, readable UI even in developer-focused tools.
- **Cross-platform reliability is a major pain point**: Multiple Windows, WhatsApp, Feishu, and SimpleX issues indicate that platform adapters remain the weakest quality vector.
- **Observability shortfall**: Users want to monitor in-flight gateway sessions (Issue #18127) and understand agent progress, especially in production deployments.

## Bugs & Stability

### Critical / High Severity (OPEN, needs attention)

| Issue | Description | Severity | Fix PR Exists? |
|-------|-------------|----------|----------------|
| [#63361](https://github.com/NousResearch/hermes-agent/issues/63361) | Daytona persistent sandbox resumes without image comparison; no forced recreation path | P2 | **Yes** — [#63368](https://github.com/NousResearch/hermes-agent/pull/63368) |
| [#63200](https://github.com/NousResearch/hermes-agent/issues/63200) | Empty-content assistant messages with tool_calls break DeepSeek API (HTTP 400) — intermittent, affects all DeepSeek users | P2 | None yet |
| [#46265](https://github.com/NousResearch/hermes-agent/issues/46265) | SimpleX adapter silently drops all DM replies — delivery failure with no error in logs | P3 (but open 29 days) | None yet |
| [#63411](https://github.com/NousResearch/hermes-agent/issues/63411) | Desktop lint fails on main — three import-order errors blocking CI/commits | P3 | None yet |

### Notable Bugs Fixed Today (CLOSED)

- **WhatsApp group routing** (#18646) — Fixed `send_message` behavior
- **Reasoning token accounting** (#18466) — `normalize_usage` now extracts `completion_tokens_details`
- **Feishu executor shutdown** (#18740) — Fixed `RuntimeError` on reply after prolonged runtime
- **Dashboard permission error** (#18935) — `PermissionError` on stale `gateway.lock` in Docker
- **Cron jobs.json race** (#18003) — Concurrent create/update/remove now properly serialized

## Feature Requests & Roadmap Signals

### Merged or Near-Complete Features

- **Multi-agent orchestration pipeline** (#18420) — Implemented on `main` via delegate task improvements
- **Cross-surface session continuity** (#18457) — Implemented on `main`, allowing session portability across terminal, Telegram, Discord, and Slack
- **WhatsApp silent-skip delivery path** (#18848) — Added for group chats where bot should stay silent when not addressed

### In Flight (Open PRs with maintainer activity)

- **#18135** — Per-turn current time context injection (P3, broad blast radius)
- **#18133** — Conductor mission process management for dashboard-started workflows
- **#18098** — Security policy posture surface for operators
- **#18096** — Production-grade autonomous evolution engine (GRPO + SGLang on H100)
- **#18077** — Stale Nous gateway auth fail-closed behavior

### Predicted Next Version Inclusions
Based on community demand and implementation status:
1. **Cross-platform file I/O reliability** (Windows paths, terminal exit codes)
2. **Gateway session observability** (agent.log live attach)
3. **Platform adapter hardening** (SimpleX, Feishu, Weixin, WhatsApp)

## User Feedback Summary

### Positive Signals
- Dashboard theme improvements received **50 upvotes** and were implemented — users appreciate customization control
- Community contributors actively submit fixes for platform-specific issues (Windows, Feishu, WhatsApp)
- Multi-agent orchestration and session continuity features are landing, suggesting roadmap alignment with power-user needs

### Pain Points
1. **Windows native support is fragile**: Users report `read_file` returning "File not found" on `D:\` drives, terminal always returning exit code 126, and Chinese text rendering glitches in TUI
2. **Gateway reliability is inconsistent**: Mattermost thread isolation, Feishu executor crashes, SimpleX silent drops, and Weixin stale session handling all erode trust in gateway deployments
3. **Configuration is error-prone**: Hardcoded `Path.home() / ".hermes"` bypasses `HERMES_HOME` env var in 23 production files (#18060), causing Docker deployments to write to wrong locations
4. **Observability is insufficient**: No way to observe in-flight gateway sessions (#18127) — "hard to know whether the agent is making progress, stuck, or burning the iteration budget"

### Satisfaction Trends
- The project maintains strong contributor velocity and issue resolution rate
- However, the **46 open PRs vs 4 merged today** ratio suggests a growing review bottleneck
- Long-open issues like #46265 (SimpleX, 29 days) and #63200 (DeepSeek, opened today) indicate some platform adapters may be under-served

## Backlog Watch

| Issue | Age | Importance | Concern |
|-------|-----|------------|---------|
| [#46265](https://github.com/NousResearch/hermes-agent/issues/46265) (SimpleX adapter) | 29 days (since Jun 14) | P3 — but affects all SimpleX DM users | No fix PR; user reports "no error in logs" meaning silent failure |
| [#18060](https://github.com/NousResearch/hermes-agent/issues/18060) (Path.home() bypass) | Closed today | P2 — Docker deployment breakage | Closed as "cannot reproduce" despite clear code-level evidence of 23 hardcoded paths |
| [#63361](https://github.com/NousResearch/hermes-agent/issues/63361) (Daytona sandbox resume) | 1 day (since Jul 12) | P2 — cloud sandbox stability | **Has a fix PR** (#63368) — requires review and merge |
| [#63411](https://github.com/NousResearch/hermes-agent/issues/63411) (Desktop lint failing) | 1 day (since Jul 12) | P3 — blocks CI | No fix applied; trivial import-order errors |

### PRs Stalled / Needs Reviewer Attention

- **#18135** (per-turn time context) — Open since May 1, no comments, 4 sweeper risk labels
- **#18133** (conductor mission management) — Open since May 1, 5 sweeper risk labels
- **#18098** (security policy posture) — Open since Apr 30, 4 risk labels, broad blast radius
- **#18096** (autonomous evolution engine) — Open since Apr 30, massive feature, unclear maintainer interest
- **#18105** (Weixin stale session fix) — Open since Apr 30, needs review for gateway reliability

### Recommendation
The **SimpleX DM delivery failure** (#46265) is the most impactful unattended bug — users receive no error and messages are silently lost. A fix PR should be prioritized. The **Daytona sandbox PR** (#63368) is ready for merge. The project would benefit from a **review sprint** to clear the backlog of 46 open PRs, especially those affecting gateway reliability and Windows platform support.

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw Project Digest — 2026-07-13

## Today's Overview

Project activity is moderate today with 5 Issues updated and 3 PRs active in the last 24 hours. Two issues were closed (one feature request for ARMv7 Docker support and one stale encrypted-message bug), while three bugs remain open — including a potentially serious Matrix sync reliability defect. One new PR addresses cache token tracking in Anthropic providers, signaling continued attention to observability and provider correctness. No new releases have been cut since the last digest.

## Releases

No new releases were published in the last 24 hours. The latest stable version remains v0.2.9 (referenced in Issue #3203).

## Project Progress

Two PRs were merged/closed in the last 24 hours:

- **PR #3190** (closed) — **fix(i18n): sync missing locale keys from en.json to bn-in and cs translations** (chengzhichao-xydt). Added missing translation keys (`chat.dropImagesActive`, `chat.disableCodeWrap`, `chat.enableCodeWrap`) to Bengali (India) and Czech locale files. This is a low-risk internationalization fix that prevents fallback-to-English for users of these languages. [GitHub](https://github.com/sipeed/picoclaw/pull/3190)

- **PR #3249** (closed) — **Skill enable/disable state + cron RunNow** (m4n3z40). Introduces skill-level disable state stored in `workspace/skills/.skills-state.json` and a "RunNow" capability for cron-triggered skills. The implementation leverages mtime-tracking for automatic cache invalidation when a skill's enabled state changes, so disabled skills gracefully disappear from `<skills>` context without manual restart. This is a fork-derived feature ported from the Ethos project (P6.6). [GitHub](https://github.com/sipeed/picoclaw/pull/3249)

## Community Hot Topics

- **Issue #3203: Matrix sync loop has no reconnection logic** (weissfl) — 2 comments, 1 👍. Reports that the Matrix `/sync` long-polling loop silently dies after any network disruption or homeserver restart. No automatic reconnection means the process stays alive, defeating systemd's `Restart=on-failure`. This affects all users depending on Matrix channel reliability in production. [GitHub](https://github.com/sipeed/picoclaw/issues/3203)

- **Issue #3182: Android version bug** (Monessem) — 3 comments, 0 👍. A stale issue (created 2026-06-26) about failing to launch the service on Android. User reports full permissions but inability to change path from settings. Still open with no resolution. [GitHub](https://github.com/sipeed/picoclaw/issues/3182)

- **Issue #3252: splitKnownProviderModel strips provider prefix when model ID contains known provider alias** (v2up-32mb) — 0 comments, 0 👍, created today. A parsing bug where model IDs like `openai/gpt-4` get incorrectly split because the model ID contains a known provider substring. Affects custom provider model configurations. [GitHub](https://github.com/sipeed/picoclaw/issues/3252)

## Bugs & Stability

**High Severity:**

- **Issue #3203 — Matrix sync loop silent death** (weissfl, open, updated today). No reconnection logic after network/homeserver disruption. The channel stops syncing permanently with no process crash to trigger restart policies. No fix PR exists yet. This is a reliability-critical defect for any deployment using Matrix. Rank: **Critical**. [GitHub](https://github.com/sipeed/picoclaw/issues/3203)

**Medium Severity:**

- **Issue #3252 — Provider model ID parsing bug** (v2up-32mb, open, created today). The `splitKnownProviderModel` function in `pkg/providers/factory.go` incorrectly strips provider prefixes. Affects any configuration where the model ID contains a substring matching a known provider alias (e.g., `openai/gpt-4` with provider `openai`). No fix PR yet. Rank: **High** (configuration-breaking). [GitHub](https://github.com/sipeed/picoclaw/issues/3252)

**Low Severity (fixed):**

- **Issue #3194 — Received encrypted message but crypto is not enabled** (Damian-o2, closed today). This stale bug about Matrix encrypted messages being received without crypto support was closed, likely as a duplicate or resolved in a prior release. [GitHub](https://github.com/sipeed/picoclaw/issues/3194)

## Feature Requests & Roadmap Signals

- **ARMv7/armhf Docker support** (Issue #3250, closed). User zhang090210 requested Docker Compose support for ARMv7 devices like OneCloud/玩客云 and Raspberry Pi Zero. The request was closed, suggesting either it was merged or deferred. This signals demand for low-power edge deployment. [GitHub](https://github.com/sipeed/picoclaw/issues/3250)

- **Prompt cache token visibility in Anthropic providers** (PR #3251, open). hydrogenbond007's PR adds capture of cache-related token metrics (cache creation read/write tokens) from Anthropic SDK and Messages API providers. This addresses an operability gap where operators cannot verify cache effectiveness or diagnose unexpected billable token counts. Likely to be included in the next release. [GitHub](https://github.com/sipeed/picoclaw/pull/3251)

- **Skill enable/disable UI and cron features** (PR #3249, merged). Although a fork-derived feature, the merged PR suggests upstream interest in skill lifecycle management (toggling skills from UI and ad-hoc cron execution). This could signal a roadmap direction toward richer skill orchestration.

## User Feedback Summary

- **Pain point: Matrix reliability.** User weissfl's report (#3203) highlights a production blocking issue for Matrix-based deployments: silent sync death after transient network failures. The lack of reconnection logic means manual intervention required for recovery, which is unacceptable for always-on home/gateway deployments.

- **Pain point: Android compatibility.** Issue #3182 (stale, 3 comments) suggests the Android version remains difficult to set up. The user has permission but cannot modify the service path — ongoing friction for mobile users.

- **Pain point: Provider configuration ambiguity.** The new issue #3252 reveals a subtle but frustrating bug: model IDs that happen to contain a provider name are incorrectly parsed. Users configuring custom models must now ensure their model ID doesn't collide with any known provider alias — a non-obvious constraint.

- **Positive signal: i18n contributions.** PR #3190 (merged) shows community investment in internationalization, with contributors adding missing translation keys for Bengali and Czech. This suggests growing non-English user base and volunteer-driven localization.

## Backlog Watch

- **Issue #3182 — Android version bug** (updated 2026-07-12 after a 16-day silence, still open, 3 comments, no assignee). Despite the recent update, there is no indication of a fix or maintainer acknowledgment. With an Android-specific showstopper, this may be a recurring pain point for mobile-first users. [GitHub](https://github.com/sipeed/picoclaw/issues/3182)

- **Issue #3203 — Matrix sync loop silent death** (open since 2026-07-02, 1 👍, no assignee, no linked PR). This critical reliability bug has been open for 11 days with no maintainer activity. The severity (complete channel downtime) warrants elevated attention. [GitHub](https://github.com/sipeed/picoclaw/issues/3203)

- **PR #3251 — Anthropic cache token capture** (open since today, no reviews yet). While not "long-unanswered," this PR addresses a gap that directly impacts billing transparency. If left unreviewed, cache inefficiencies may go undiagnosed. [GitHub](https://github.com/sipeed/picoclaw/pull/3251)

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw Project Digest — 2026-07-13

## Today's Overview

NanoClaw shows **very high activity** over the past 24 hours, with **13 PRs updated** (11 open, 2 merged/closed) and **3 active issues** reported. The project is clearly in a **rapid stabilization and hardening phase**, as the majority of activity centers on fixing regressions from recent nudging, guard, and container infrastructure changes. Key themes include output token caps silently throttling Claude agents, container startup failures due to root-owned TMPDIR issues, and duplicate replies from the re-wrap nudge mechanism. The core team is also advancing substantial architectural work on guided approvals and guard seams, indicating both reliability improvements and new governance capabilities are nearing completion.

## Releases

**No new releases** were published in the last 24 hours. The project is currently in a heavy pre-release stabilization period, with multiple interconnected fixes in flight.

## Project Progress

**Two PRs merged/closed today:**

- **[#3024 — fix(container): raise the agent SDK's 32000 output-token cap to the model's real ceiling](https://github.com/nanocoai/nanoclaw/pull/3024)** (Closed) — This was a **critical fix** for the regression reported in issue #3023. All Claude agents were silently capped at 32,000 output tokens because the `CLAUDE_CODE_MAX_OUTPUT_TOKENS` environment variable was never set. A similar but improved fix is now open as PR #3025.
- **[#2952 — Skill/add opencode stack](https://github.com/nanocoai/nanoclaw/pull/2952)** (Closed) — A merged operational/container skill that adds OpenCode stack support to the agent environment.

**Key features advancing (open PRs with updates today):**
- **Guarded approvals CLI** (#3029) — Adds `approve`, `reject`, `reject-with-reason` verbs to `ncl approvals`, enabling operators to resolve pending approvals from the command line.
- **Unified guard seam** (#2986) — Every privileged action now passes a single `guard()` decision function (`allow | hold | deny`), replacing the previous voluntary gating system.
- **Scheduled tasks in templates** (#3022) — Templates can now define recurring scheduled tasks via `tasks/*.md` files with cron schedules, auto-created paused on agent group stamp.
- **Per-group harness capability toggles** (#2983) — Extends the existing pattern of disabling Claude Code cron in favor of NanoClaw's own scheduler to additional harness capabilities, with per-group configuration.
- **Local audit log skill** (#2987) — An opt-in audit log for the `ncl` surface, rebased onto the new guard seam.

## Community Hot Topics

**Most active issues and PRs (by engagement and recency):**

- **[#3023 — Every Claude agent is silently capped at 32000 output tokens](https://github.com/nanocoai/nanoclaw/issues/3023)** (0 comments, 0 reactions) — While low on direct engagement, this is the **most impactful bug** reported today, affecting every Claude agent running long output tasks (CAD, OpenSCAD generation). The fix PR (#3024) was already closed and a refined version (#3025) is open.

- **[#3016 — Every rate_limit_event is logged as a quota error, even when status is "allowed"](https://github.com/nanocoai/nanoclaw/issues/3016)** (1 comment, 0 reactions) — A regression from PR #2965 causing noisy quota-error logging on every normal turn. The reporter logged 82 instances in a week on their install, yet all replies delivered successfully. **Underlying need:** Users need actionable, accurate error logs — not noise that desensitizes them to real quota issues.

- **[#3026 — Re-wrap nudge re-runs the model and duplicates replies when the agent already replied via send_message](https://github.com/nanocoai/nanoclaw/issues/3026)** (0 comments) — A behavior regression in the unwrapped-output nudge. When an agent sends a message but omits the XML `<message>` wrapper, the nudge re-runs the model and produces a duplicate reply. **Underlying need:** Users need reliable, non-duplicating message delivery without requiring perfect adherence to XML output format.

- **[#3020 — fix(agent-runner): rescue undelivered unwrapped replies after the re-wrap nudge](https://github.com/nanocoai/nanoclaw/pull/3020)** — Direct fix for #2369, #2393, and flavor of #2404. This is the companion PR to issue #3026, but addresses the broader class of silent message drops when the model omits `<message to>` wrappers.

## Bugs & Stability

**Ranked by severity (highest first):**

1. **Critical — All Claude agents silently capped at 32,000 output tokens** (Issue [#3023](https://github.com/nanocoai/nanoclaw/issues/3023))
   - Long turns fail mid-response with "exceeded the 32000 output token maximum" error
   - No existing code sets `CLAUDE_CODE_MAX_OUTPUT_TOKENS`; all agents are affected
   - **Fix status:** PR #3024 closed (simple fix), improved version in PR #3025 (open)
   - Impact: Every Claude agent generating long outputs (CAD, code files, documentation) hits this silently

2. **High — Container startup failure when TMPDIR resolves to root-owned directory** (PR [#3027](https://github.com/nanocoai/nanoclaw/pull/3027))
   - Agents go silent because `wakeContainer` fails with `EISDIR: illegal operation on a directory`
   - Root cause: `onecli-proxy-ca.pem` can be poisoned into a root-owned dir on `/tmp`
   - **Fix status:** PR #3027 open by caburi00, relocating TMPDIR off `/tmp`
   - Impact: Intermittent agent silence on channels (e.g., WhatsApp) — high user frustration

3. **Medium — Re-wrap nudge causes duplicate replies after send_message** (Issue [#3026](https://github.com/nanocoai/nanoclaw/issues/3026))
   - The unwrapped-output nudge re-runs the model when it can't see replies already sent via `send_message`
   - **Fix status:** PR #3028 open by ogarciarevett
   - Impact: Duplicate messages to users; degrades trust in agent reliability

4. **Low — Every rate_limit_event logged as quota error even when allowed** (Issue [#3016](https://github.com/nanocoai/nanoclaw/issues/3016))
   - Regression from PR #2965 causes `[poll-loop] Error: Rate limit (retryable: false, quota)` on normal turns
   - **Fix status:** No dedicated fix PR yet; likely needs logging-level adjustment
   - Impact: Log noise, potential user alarm, reduced signal-to-noise in monitoring

## Feature Requests & Roadmap Signals

**User-requested features emerging this week:**

- **Operator approval resolution from CLI** (PR [#3029](https://github.com/nanocoai/nanoclaw/pull/3029)) — Users (operators) need to unblock held actions without leaving the terminal. This PR adds `approve/reject/reject-with-reason` to `ncl approvals`. **Prediction:** This is highly likely to land in the next release — it's a core-team PR completing the approvals surface.

- **Pre-warning for shared WhatsApp numbers** (PR [#3021](https://github.com/nanocoai/nanoclaw/pull/3021)) — Users should be warned before connecting a personal/shared WhatsApp number due to risk of temporary suspension. **Prediction:** Likely to merge soon — small, user-protective change.

- **Scheduled tasks in templates** (PR [#3022](https://github.com/nanocoai/nanoclaw/pull/3022)) — Template authors want to avoid manually recreating scheduled tasks after agent creation. **Prediction:** Strong candidate for next release — core-team PR, substantial feature addition.

**Roadmap signals:**
- The **unified guard seam** (#2986) and **local audit log** (#2987) suggest NanoClaw is building toward **enterprise-grade governance capabilities** — a significant strategic direction.
- The re-wrap nudge fixes (#3020, #3028, #3026) indicate the team is **investing heavily in output format reliability** to reduce fragility from XML-based message protocols.

## User Feedback Summary

**Real pain points expressed directly by users:**

- **"My install logged it 82 times in about a week, and every one of those turns delivered its reply."** (Issue #3016) — Users are **frustrated by noisy, non-actionable error logs** that make it harder to spot real problems.

- **"A long turn dies partway through"** with a 32K token cap error (Issue #3023) — Users generating **long technical outputs (CAD files, OpenSCAD)** are hitting invisible limits that silently truncate their work.

- **"Agents intermittently go silent — the host routes inbound messages but no container ever spawns"** (PR #3027) — Users on **channels like WhatsApp experience complete agent unavailability** without clear error messages.

- **"ncl can observe pending approvals but can't resolve one"** (PR #3029) — Operators using the CLI want **parity with the GUI** for approval workflows.

**Satisfaction signals:**
- Multiple core-team PRs are advancing with active engagement — the team is responsive to reported regressions within 24-48 hours (fix PR #3024 was opened and closed on the same day as bug report #3023).
- The volume of fixes going into the re-wrap nudge and guard seam areas suggests the team is **prioritizing stability and hardening** over new features, which should improve user satisfaction in the near term.

## Backlog Watch

**Items needing maintainer attention (based on duration without updates):**

- **[#2982 — fix(agent-runner): reconcile Claude tool allowlist with pinned CLI, add drift guard](https://github.com/nanocoai/nanoclaw/pull/2982)** — Open since July 8, updated July 12 with no recent reviewer activity. This fixes five non-existent tools in the allowlist (Task renamed to Agent, TodoWrite, TeamCreate, TeamDelete, ToolSearch). **Risk:** Drift between the allowlist and actual CLI tools could cause unexpected permission errors or tools silently failing.

- **[#2983 — feat: per-group harness capability toggles](https://github.com/nanocoai/nanoclaw/pull/2983)** — Open since July 8, updated July 12. While it has updates, it's a substantial structural change (per-group configuration with grandfathering) that may need broader review before merging.

- **[#2987 — feat: /add-audit skill](https://github.com/nanocoai/nanoclaw/pull/2987)** — Open since July 9, rebased and hardened per review but still awaiting final merge. This is a core-team, security-relevant feature that should be prioritized for the next release.

**No issues were found that are unassigned or lacking a response from maintainers.** All active issues have at least one corresponding fix PR in flight.

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw Project Digest — 2026-07-13

## 1. Today's Overview

The IronClaw project is in an **intense consolidation phase**, with 50 PRs updated in the last 24 hours (33 merged/closed) — the highest single-day PR throughput observed this month. However, **CI instability remains the dominant story**: the project's `main` branch has been **red ~70% of the time in July** (139/200 push runs failed) due to flaky non-hermetic tests, prompting a dedicated taxonomy effort (Issue #6011) and a set of hardening PRs (#6022, #6020). Nine issues were active in the last day, with six open and three closed — all three of those closed were high-severity `bug_bash` and `created_by_ironclaw` items, signaling that the team is prioritizing user-facing regression fixes. No new releases were cut today.

## 2. Releases

**No new releases today.** The last release candidate remains PR #5598 (`chore: release`), which is still open and proposes:
- `ironclaw_common`: 0.4.2 → 0.5.0 (⚠ breaking changes)
- `ironclaw_safety`: 0.2.2 → 0.2.3 (compatible)
- `ironclaw_skills`: 0.3.0 → 0.4.0 (⚠ breaking changes)
- `ironclaw`: 0.24.0 → 0.29.1

That release PR has been open since July 3 with no movement; the team appears to be holding the release until CI is stabilized.

## 3. Project Progress

**33 PRs were merged or closed today** — the highest single-day total since tracking began. Notable items:

- **Agent loop enhancements**: PR #6013 (`feat(agent-loop): tools-capable completion nudge for interactive coding`) by `pranavraja99` makes the agent loop's driver-specific completion nudge tools-capable and enables it for interactive coding — a quality-of-life improvement for developers using IronClaw interactively.

- **CI hardening**: PR #5991 (`test(ci): require Responses API coverage in PR checks`) by `serrrfirat` closed today, ensuring all 16 Responses API E2E cases run in Reborn PR CI. This is part of a broader push to catch regressions earlier.

- **Admin secrets scope fix**: PR #5934 by `serrrfirat` (still open) validates admin capability-secret scope fix, ensuring tenant/user identity is preserved in the WebUI.

- **QA expansion**: PR #5853 (`Add targeted QA 10/11 canary cases`) by `serrrfirat` closed, adding 10 new manually-targetable Reborn WebUI v2 QA cases covering custom-tool and Response API BTC analysis stories.

- **Read-only CLI migration**: PR #4379 (`feat: migrate read-only commands doctor, status and config list/get to Reborn`) by `denbite` closed — a milestone in the Reborn CLI migration effort.

- **Dependency updates**: Two large Dependabot PRs closed (#5926 with 20 updates, plus #4022's wasm group), and two more remain open (#6021 with 22 updates, #5664 with 16 actions updates).

## 4. Community Hot Topics

The most active discussion centers on **CI failure taxonomy and reliability**:

- **Issue #6011** (`Daily ironclaw failure taxonomy — 2026-07-12`) by `pranavraja99` — A systematic daily breakdown of CI failures. This is the most operationally significant open item, providing a shared vocabulary for the CI crisis. The `clawbench` suite shows 136 non-pass tests, dominated by a benchmark provisioning defect (~103/136 failures). [nearai/ironclaw Issue #6011](https://github.com/nearai/ironclaw/issues/6011)

- **Issue #6014** (`CI fragility: flaky non-hermetic tests abort the coverage matrix`) by `ilblackdragon` — Documents that Code Coverage is the single largest source of red on `main` (~70% of July push runs failed), with two full-red waves. The root cause is structural, not a bad commit. [nearai/ironclaw Issue #6014](https://github.com/nearai/ironclaw/issues/6014)

- **Issue #6018** (`CI hardening: add static pre-push checks`) by `ilblackdragon` — Proposes three static checks to catch deterministic breakages (the other ~30% of failures). Already has a companion PR (#6022) implementing the fix. [nearai/ironclaw Issue #6018](https://github.com/nearai/ironclaw/issues/6018)

- **PR #6022** (`ci: static pre-push checks — include_str/Docker-COPY + hermetic env`) by `ilblackdragon` — Direct implementation of Issue #6018. Adds `include_str!` path + Docker-COPY coverage, hermetic env guard, and libsql-only clippy checks. [nearai/ironclaw PR #6022](https://github.com/nearai/ironclaw/pull/6022)

- **Issue #6015** (`Flaky/isolation: build_runtime_input_production_* races on std::env`) — Identifies a genuine test-isolation defect in the all-features coverage leg. [nearai/ironclaw Issue #6015](https://github.com/nearai/ironclaw/issues/6015)

The underlying need is clear: **the team needs CI to be trustworthy before shipping the next release**, and the taxonomy effort (#6011) is the foundation for that work.

## 5. Bugs & Stability

| Severity | Issue | Summary | Fix PR? |
|----------|-------|---------|---------|
| **Critical** | #6010 [CLOSED] | NEAR AI inference (GLM-5.2) hangs for minutes during opencode usage — "unusable for real-time interactive development" | Closed as bug, fix presumed merged |
| **Critical** | #6009 [CLOSED] | GLM-5.2 not available in opencode default model list — must be manually added | Closed as bug, fix presumed merged |
| **High** | #6014 [OPEN] | CI fragility: 70% of main pushes red due to flaky non-hermetic tests aborting coverage matrix | #6022 addresses static checks |
| **High** | #5704 [CLOSED] | Image preview becomes transparent while chat is active (bug_bash P3) | Closed, fix presumed merged |
| **Medium** | #6015 [OPEN] | build_runtime_input_production_* races on std::env in all-features coverage leg | No fix PR yet |
| **Medium** | #6016 [OPEN] | Slack trigger-delivery e2e tests timeout / miss fired trigger (two most recent main failures) | #6020 addresses Slack determinism |
| **Medium** | #6017 [OPEN] | DB concurrency contract tests flake (Postgres delete/recreate race, libSQL concurrent writers) | No fix PR yet |

**Critical fixes were shipped today**: Three closed issues (#6010, #6009, #5704) were all high-severity user-facing bugs. The GLM-5.2 hang (#6010) was particularly concerning — the inference engine becoming unresponsive for minutes at a time blocked interactive development workflows.

The remaining **five open CI bugs** (#6014-#6018) form a coordinated attack on the CI red problem, with `ilblackdragon` authoring four of them as part of a systematic taxonomy-to-fix pipeline.

## 6. Feature Requests & Roadmap Signals

Two major feature tracks are advancing:

1. **MCP (Model Context Protocol) Registration Stack**: PR #5970 (`feat(reborn): per-user MCP registration store`) by `henrypark133` — Rebuilt on the new `InstallationOwner` machinery. This is the T1 foundation of the MCP registration stack; T2 (egress enforcement) and T3 (registration API) are still ahead. This is likely destined for the next major release.

2. **Extension Runtime Train**: A series of 8 PRs is in progress:
   - PR #5995 (`P1: manifest v3 + VendorId + recipes + resolved record`) — Phase P1, Workstream A
   - PR #6012 (`P5: delivery coordinator + Slack/Telegram outbound`) — Workstream F, still in draft

   The extension-runtime train is the most ambitious architectural change in flight, adding delivery coordination for Slack and Telegram outbound channels.

3. **CI Static Checks**: PR #6022's pre-push checks (`include_str!`/Docker-COPY coverage, hermetic env guard, libsql-only clippy) will likely land within days, as they directly address the deterministic CI failure classes.

4. **Doctor command enhancement**: PR #6019 (`feat(reborn-cli): add dependency readiness checks to doctor with --live flag`) adds LLM/provider credential readiness checks — a quality-of-life improvement for developers.

**Prediction for next release**: The MCP registration store (#5970) and extension runtime P1 (#5995) are the strongest candidates, but the team won't cut a release until the CI red problem is resolved — so #6022 is the key blocking PR.

## 7. User Feedback Summary

- **Positive signal**: The bug_bash process is working — Issue #5704 (image transparency) was fixed within 6 days of filing, and both GLM-5.2 issues (#6009, #6010) were closed within 24 hours. This suggests the team is responsive to structured bug reports from the community.

- **Pain point: CI trustworthiness**: Users are experiencing CI failures that obscure genuine regressions. The taxonomy effort (#6011) is a direct response to maintainers needing visibility into *why* CI is failing, not just *that* it's failing.

- **Pain point: GLM-5.2 availability**: Users having to manually add models (Issue #6009) and experiencing hangs (Issue #6010) indicates friction in the model-provisioning pipeline. Both were fixed today.

- **Developer experience**: The agent-loop completion nudge (#6013) and doctor enhancement (#6019) suggest the team is investing in interactive development UX — a sign of a maturing project that cares about developer onboarding.

## 8. Backlog Watch

- **PR #5598** (`chore: release`) — **Open since July 3, 9 days ago**. This release PR for `ironclaw_common 0.5.0`, `ironclaw_skills 0.4.0`, and `ironclaw 0.29.1` has breaking API changes but no movement. The team appears to be deliberately holding the release until CI is stabilized. [nearai/ironclaw PR #5598](https://github.com/nearai/ironclaw/pull/5598)

- **PR #5664** (`build(deps): bump the actions group with 16 updates`) — **Open since July 5, 8 days ago**. A Dependabot PR updating 16 GitHub Actions (including `actions/checkout` from v4 to v7, and `anthropics/claude-code-action` from 1.0.88 to 1.0.171). The size and risk rating (L, medium) suggest maintainers are cautious about merging many action updates simultaneously. [nearai/ironclaw PR #5664](https://github.com/nearai/ironclaw/pull/5664)

- **PR #4032** (`build(deps): bump the wasm group`) — **Open since May 25, 49 days ago**. Stale Dependabot PR for `wit-component` and `wit-parser` updates. This is the oldest open PR in the project and may have merge conflicts by now. [nearai/ironclaw PR #4032](https://github.com/nearai/ironclaw/pull/4032)

- **PR #5114** (`build(deps): bump the tokio-ecosystem group`) — **Open since June 21, 22 days ago**. Updates to `tokio-tungstenite`, `tokio-postgres-rustls`, `tower-http`, and `hyper`. Notable because `hyper` is a core dependency — keeping it on an old version may be a security concern. [nearai/ironclaw PR #5114](https://github.com/nearai/ironclaw/pull/5114)

**Verdict**: The release PR (#5598) and the `wasm` stale PR (#4032) are the most concerning backlog items. The release is effectively blocked by CI reliability, which is receiving coordinated attention — but the wasm dependency update has been ignored for 7 weeks.

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

# 🦞 LobsterAI Project Digest — 2026-07-13

**Project:** LobsterAI (github.com/netease-youdao/LobsterAI)  
**Analyst:** AI Agent / Personal AI Assistant OSS Tracker  
**Report date:** 2026-07-13

---

## 1. Today’s Overview

The project shows **low overall activity** in the past 24 hours, with 1 updated issue (open) and 2 updated PRs (1 open, 1 closed/merged). No new releases were published. The single active issue (#2293) is a **confirmed regression bug** affecting multi-agent workflows, which has gathered 4 comments and is now a week old. A long‑stale PR (#1325) was bumped with a UI enhancement, while a closed/marged PR (#2065) addresses a fundamental Agent ID generation problem. The overall health is **stable but quiet**, with community attention concentrated on a data‑corruption bug rather than new feature development.

---

## 2. Releases

*No new releases today.*  
(Last release data not available in this snapshot.)

---

## 3. Project Progress

- **#1325 [OPEN] [stale]** — `feat(ui): 为新建对话图标按钮添加悬停提示`  
  *Author: 0xFLX*  
  A pure‑UI enhancement adding `title` attributes to "New Conversation" icon buttons across four views. No comments yet, but the PR (created April 2) was updated yesterday, indicating it may be under review.  
  [View PR](https://github.com/netease-youdao/LobsterAI/pull/1325)

- **#2065 [CLOSED/merged]** — `fix(agent): 使用短 UUID 替代名称生成 Agent ID`  
  *Author: gongzhi-netease*  
  A significant **data‑integrity fix** that replaces name‑based Agent IDs with short UUIDs. This prevents "data resurrection" when users delete and recreate an agent with the same name. The PR also acknowledges a remaining issue (sessions not cleaned on deletion) as a future fix.  
  [View PR](https://github.com/netease-youdao/LobsterAI/pull/2065)

---

## 4. Community Hot Topics

### Most Active Issue
- **#2293 [OPEN]** — *「重启后，多个agent下的USER.md被覆盖替换的BUG？」*  
  *Author: yepcn | Comments: 4 | 👍: 0*  
  **Underlying need:** Multi‑agent users require **isolated, persistent per‑agent configuration files (USER.md)**. The current behavior forcibly copies the *main agent’s* USER.md to all other agents on restart, breaking personalized setups. The reporter suspects a recent update introduced this regression.  
  [View Issue](https://github.com/netease-youdao/LobsterAI/issues/2293)

No other issues or PRs in the snapshot show significant engagement (0–1 reactions).

---

## 5. Bugs & Stability

| ID | Bug | Severity | Status | Fix PR? |
|----|-----|----------|--------|---------|
| #2293 | USER.md data overwritten for all agents after restart | **High** — data loss, breaks core multi‑agent functionality | Open (4 days old, 4 comments) | No fix PR linked yet. Likely related to recent changes in config persistence. |
| #2065 | Agent ID collisions causing data resurrection | **Medium** — data corruption on delete/recreate | ✅ **Closed/merged** today | Fixed via UUID‑based IDs (PR #2065). |

**Analysis:** Bug #2293 is the top stability concern. It is a regression that destroys user‑defined per‑agent content. The merged PR #2065 indirectly improves the situation for agent lifecycle, but does not address the USER.md overwrite issue directly.

---

## 6. Feature Requests & Roadmap Signals

No explicit feature requests appear in today’s snapshot. However, from the **stale PR (#1325)**:
- Users desire **better UI affordances** (tooltips) for icon‑only buttons when sidebar is collapsed — a common UX‑quality request.

From the **merged PR (#2065)**:
- The acknowledgment of **incomplete cleanup of sessions on agent deletion** signals a known roadmap item to fully support agent lifecycle management.

**Prediction for next version:**  
- Multi‑agent USER.md isolation fix (likely hotfix).  
- Session cleanup when an agent is deleted.  
- Minor UI polishing (tooltips).

---

## 7. User Feedback Summary

**Key pain points expressed by real users:**

- **Multi‑agent workflow broken** — The reporter of #2293 describes a scenario where they maintain different agent configurations for distinct roles/tasks. The current bug makes this impossible, and the user explicitly asks whether others have encountered the issue, indicating **confusion and frustration** about a feature that was previously working.
- **Data integrity anxiety** — The user manually tested by editing USER.md offline, only to find it overwritten on restart, showing a lack of trust in data persistence.

**Overall sentiment:**  
One deeply engaged user experiencing a regression; no praise or positive feedback captured. The community’s need for **reliable multi‑agent isolation** is clear.

---

## 8. Backlog Watch

| Item | Age | Issue | Reason for attention |
|------|-----|-------|----------------------|
| #1325 (UI tooltip PR) | ~102 days (created Apr 2) | Open, stale | Very low‑impact but long unattended. Could be a good first issue to merge or close. |
| #2293 (USER.md bug) | 7 days | Open, no maintainer reply yet | **Critical** — data‑loss regression. Needs maintainer triage and a fix PR urgently. |
| #2065 (UUID fix, closed) | — | ✅ Merged | Good; but the acknowledged “sessions cleanup” gap remains on the backlog. |

**Maintainer attention needed:**  
1. ✅ Confirm fix for #2293 — highest priority.  
2. 👍 Merge or close #1325 after review — low effort, good UX win.  
3. 📋 Add tracking issue for session cleanup (referenced in #2065).

---

*Digest generated from GitHub API snapshot for 2026-07-13.*

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

# CoPaw Project Digest — 2026-07-13

## 1. Today's Overview
CoPaw has seen **moderate-to-high** activity in the last 24 hours, with **19 issues** and **10 pull requests** updated. However, the project is clearly in a **post-2.0.0 release stabilization phase**, evidenced by a large number of regression bugs and compatibility issues reported by users upgrading from v1.x. The community is actively reporting and attempting to fix problems, with **3 PRs merged/closed** today targeting critical regressions. No new releases were published. The project's health is **concerning but actively managed** — the volume of bug reports (14 open bugs) against v2.0.0 indicates the release may have been premature, but the maintainer and contributor response is visible.

## 2. Releases
**No new releases today.** The latest available version remains **v2.0.0**, which according to user reports appears to have introduced several regressions and missing features compared to v1.1.x.

## 3. Project Progress
**3 PRs merged/closed today:**

- [#5990](https://github.com/agentscope-ai/CoPaw/pull/5990) — **fix(compat): handle legacy 'file' block type in _coerce_block** (merged). A critical fix for v1.x → v2.0 session migration that was previously overlooked. This was a first-time contributor submission that went through multiple iterations (PRs #5988, #5990).
- [#5987](https://github.com/agentscope-ai/CoPaw/pull/5987) — **fix(scroll): sanitize unpaired tool messages after context compression** (merged). Addresses the root cause of orphaned `tool_result` messages causing 400 errors.
- [#5988](https://github.com/agentscope-ai/CoPaw/pull/5988) — Duplicate/fix of #5990 (closed in favor of #5990).

**Key advancement:** The context compression bug causing "400 BadRequestError: tool messages must follow tool_calls" has been patched via #5987, which is a critical stability fix.

## 4. Community Hot Topics

**Most Active Issues:**

1. [#5952](https://github.com/agentscope-ai/CoPaw/issues/5952) — *Auto-memory fails "No module named 'agentscope.tool._builtin._scripts'"*  
   **4 comments, open 3 days.** Root cause identified by the community and a fix PR [#5997](https://github.com/agentscope-ai/CoPaw/pull/5997) has been opened. This is blocking memory summarization for all agents.

2. [#5986](https://github.com/agentscope-ai/CoPaw/issues/5986) — *Context compression breaks tool_call/tool_result pairing → 400 BadRequestError*  
   **4 comments, opened today.** The most impactful bug — causes API-level failures on long sessions. Already has a fix PR merged (#5987) the same day.

3. [#5964](https://github.com/agentscope-ai/CoPaw/issues/5964) — *Upgrade to 2.0.0 breaks session mapping*  
   **2 comments, open 2 days.** Users unable to open existing conversations after upgrade. Major migration pain point.

4. [#6001](https://github.com/agentscope-ai/CoPaw/issues/6001) / [#6000](https://github.com/agentscope-ai/CoPaw/issues/6000) — *Skill pool broken for all new skills*  
   **User reported as "completely broken"** — the entire skill installation pipeline has regressed in v2.0.0.

**Underlying needs:** Users are demanding **stable backward compatibility** and **functional upgrade paths**. The volume of v1→v2 migration issues suggests insufficient testing of migration paths before release.

## 5. Bugs & Stability

### Critical (blocks core functionality):
| Issue | Description | Status |
|-------|-------------|--------|
| [#5986](https://github.com/agentscope-ai/CoPaw/issues/5986) | Context compression → 400 errors on long sessions | **Fix PR #5987 merged** ✅ |
| [#5952](https://github.com/agentscope-ai/CoPaw/issues/5952) | Auto-memory completely broken (missing module) | **Fix PR #5997 open** 🛠️ |
| [#6001](https://github.com/agentscope-ai/CoPaw/issues/6001) | Skill system broken for all new skills | No fix PR yet ❌ |
| [#5964](https://github.com/agentscope-ai/CoPaw/issues/5964) | Session mapping lost after upgrade | **Fix PR #5993 open** 🛠️ |

### High Severity:
- [#5996](https://github.com/agentscope-ai/CoPaw/issues/5996), [#5985](https://github.com/agentscope-ai/CoPaw/issues/5985) — MODEL_EXECUTION_ERROR caused by orphaned tool messages (multiple reports, related to #5986)
- [#5995](https://github.com/agentscope-ai/CoPaw/issues/5995) — Messages silently dropped when session busy (no queue, no error)
- [#5994](https://github.com/agentscope-ai/CoPaw/issues/5994) — Security governance fires on every operation in AUTO mode, blocking workflow
- [#5998](https://github.com/agentscope-ai/CoPaw/issues/5998) — Agent executes old plan after user confirms new plan (memory/context inconsistency)
- [#5982](https://github.com/agentscope-ai/CoPaw/issues/5982) — Shell execution demands user approval every time in v2.0.0

### Medium/Low Severity:
- [#5983](https://github.com/agentscope-ai/CoPaw/issues/5983) — `qwenpaw doctor` reports FAIL (hardcoded incorrect health endpoint)
- [#5981](https://github.com/agentscope-ai/CoPaw/issues/5981) — UI bug: model search field auto-filled with username
- [#5977](https://github.com/agentscope-ai/CoPaw/issues/5977) — Plugin HTTP routes lost after workspace hot-reload
- [#5980](https://github.com/agentscope-ai/CoPaw/issues/5980) — Missing v1.1.12 features (SSH Offline, profiles) returning 404
- [#5979](https://github.com/agentscope-ai/CoPaw/issues/5979) — Electron cli tool crashes in sandbox (root mapping issue)

## 6. Feature Requests & Roadmap Signals

**Today's feature requests:**

- [#5999](https://github.com/agentscope-ai/CoPaw/issues/5999) — **Cross-channel session continuity**: Allow users to hand off the same conversation across Console, Feishu, DingTalk, etc. *This is a high-value enterprise/team collaboration feature likely to be prioritized for v2.1+.*
- [#5984](https://github.com/agentscope-ai/CoPaw/issues/5984) — **Tool approval toggle for unsandboxed hosts**: Users on ARM/Raspberry Pi cannot disable shell approval prompts. *A UI fix for the governance system is likely coming soon given multiple related complaints.*
- [#5979](https://github.com/agentscope-ai/CoPaw/issues/5979) — **Electron/sandbox compatibility for CLI tools**: Linux users need a way to run electron-based tools without --no-sandbox workarounds.

**Under discussion (open PRs):**
- [#5869](https://github.com/agentscope-ai/CoPaw/pull/5869) — **Slash autocomplete for system commands across all UIs** (under review). This would improve discoverability for power users.
- [#5992](https://github.com/agentscope-ai/CoPaw/pull/5992) — **Per-session model overrides**: Users could assign different models per conversation. *This is a significant UX improvement and may land in v2.1.*

**Prediction for v2.1:** Cross-channel session handoff, per-session model overrides, and a functioning skill system will likely be the headline features, along with a stabilization patch release.

## 7. User Feedback Summary

**Pain Points (high frequency):**
1. **v1.x → v2.0 migration is painful** — Session mapping lost (#5964), media compatibility broken (#5993, #5991), missing features (#5980)
2. **Context compression causes API errors** — Multiple users hitting 400 errors on long sessions (#5986, #5985, #5996)
3. **Governance/security system is too aggressive** — Users report being prompted for every action even in AUTO mode (#5994) and permanent shell approval prompts (#5982, #5984)
4. **Skill system is non-functional** — Two users independently confirmed that *no* new skills can be added (#6001, #6000)
5. **Auto-memory is broken** — A core feature completely non-functional post-upgrade (#5952, #5978)

**Positive signals:**
- Fast maintainer response on critical issues (PR #5987 merged same day as bug report)
- First-time contributors actively submitting fixes (4 of 10 PRs today are from new contributors)
- Users are filing detailed, reproducible bug reports with version numbers, which suggests a technically engaged community willing to help improve the project

**Satisfaction assessment:** Dissatisfaction is high among users who upgraded to v2.0.0, with many expressing frustration that core features regressed. However, the active contribution pipeline indicates long-term community health is intact.

## 8. Backlog Watch

**Issues needing maintainer attention:**

| Issue | Age | Reason for Watch |
|-------|-----|------------------|
| [#6001](https://github.com/agentscope-ai/CoPaw/issues/6001) | 1 day | Skill system "completely broken" — highest priority user blocker, no maintainer response yet |
| [#6000](https://github.com/agentscope-ai/CoPaw/issues/6000) | 1 day | Duplicate of #6001, also unacknowledged |
| [#5999](https://github.com/agentscope-ai/CoPaw/issues/5999) | 1 day | Strategic feature request (cross-channel session) — needs roadmap clarification |
| [#5980](https://github.com/agentscope-ai/CoPaw/issues/5980) | 1 day | Missing v1.x features — indicates possible regression in feature parity |
| [#5952](https://github.com/agentscope-ai/CoPaw/issues/5952) | 3 days | Auto-memory broken — critical feature, has fix PR but no merge yet |

**PRs needing review:**
- [#5992](https://github.com/agentscope-ai/CoPaw/pull/5992) — Per-session model overrides (significant feature addition, first-time contributor)
- [#5869](https://github.com/agentscope-ai/CoPaw/pull/5869) — Slash autocomplete (under review, 5 days old)
- [#5791](https://github.com/agentscope-ai/CoPaw/pull/5791) — Format number rounding fix (under review, 8 days old — may need maintainer attention)

**Overall assessment:** The project is experiencing a **stabilization crisis** following the v2.0.0 release. The next 48-72 hours are critical for releasing a v2.0.1 patch to restore trust in the upgrade path. The most important fires to put out are: (1) skill system regression, (2) auto-memory module missing, (3) session mapping loss on upgrade, and (4) aggressive governance defaults. The community is engaged and providing high-quality bug reports, which is a strong asset for recovery.

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# ZeroClaw Project Digest — 2026-07-13

## 1. Today's Overview

ZeroClaw shows sustained **high activity** with 49 issues and 50 pull requests updated in the last 24 hours, signaling an active development cycle. Only 2 items were closed/merged during this period, consistent with a project deep in a milestone push (v0.8.3). The tracker infrastructure dominates the issue tracker, with at least eight coordinated tracker issues coordinating release, runtime, memory, and channel work. Notably, **no new releases** were cut today, suggesting the team is consolidating work before a release candidate. The project health is strong but carries **significant risk signals**: multiple S1 (workflow-blocked) bugs and several high-risk PRs remain open, and the open-to-closed ratio indicates the team is prioritizing new feature work over bug closure.

## 2. Releases

**No new releases** on 2026-07-12 or 2026-07-13. The v0.8.3 milestone tracker (#7320) remains open with 15 items, indicating a release is pending but not imminent.

## 3. Project Progress

**Merged/closed items today:** 2 total (1 issue, 1 PR).

- **Closed Issue #9016** — `[Bug]: OpenAI tool turns fail when Chat Completions rejects reasoning effort`. This was a critical S1 bug where OpenAI-compatible models failed when ZeroClaw sent function tools with non-`none` reasoning effort. Likely a documentation-only close or a quick config fix.

- **Merged/closed PR:** No merged PRs explicitly visible in the top-30 trackers; the single closed issue appears to be the volume of closure activity.

**Feature branches advancing (open PRs with recent updates):**
- **WASM channel plugins landing (#8852)** — JordanTheJet wired the first real caller for WASM channel plugins, moving from compile-only to runtime execution. Significant architecture milestone.
- **Memory subsystem overhaul (#8897, #8898, #8984)** — Nillth is actively landing the staged retrieval pipeline and memory content scanning. Multiple high-risk, extra-large PRs in flight.
- **Matrix single-message streaming (#8443)** — vrurg's work on progress drafts for Matrix is nearing the milestone.
- **OpenAI Chat Completions endpoint (#8486)** — REL-mame's large PR for an OpenAI-compatible HTTP endpoint continues to advance.
- **CLI config-dir fix (#9018)** — JordanTheJet submitted a targeted fix for locale detection order.
- **Quickstart capability-safe defaults (#8987)** — Audacity88 submitted recommended runtime defaults for new users.

## 4. Community Hot Topics

**Most active discussions (by comment count):**

1. **#8681 — Goal mode implementation split stack** (9 comments, 0 👍) — `[Tracker]`  
   *Coordinating the splitting of accepted goal-mode work into reviewable PRs. Critical for architectural progress but has zero community reacts—strictly a maintainer coordination issue.*  
   https://github.com/zeroclaw-labs/zeroclaw/issues/8681

2. **#5808 — Default 32k context budget exceeded by system prompt** (8 comments, 0 👍) — `[Bug] S1`  
   *The longest-running S1 bug (since April 2026). The default context budget is ~3.3x too small on first iteration alone. Community is frustrated that this high-severity issue remains unresolved after 3 months.*  
   https://github.com/zeroclaw-labs/zeroclaw/issues/5808

3. **#6055 — Slack: hydrate thread context from conversations.replies** (6 comments, 0 👍) — `[Feature]`  
   *Request to backfill prior thread history on first bot mention. Community member DengHaoke's feature has been accepted but "in-progress" for 2.5 months.*  
   https://github.com/zeroclaw-labs/zeroclaw/issues/6055

4. **#7952 — publish full-channel prebuilt assets** (6 comments, 0 👍) — `[Feature]`  
   *Users requesting a `channels-full` binary bundle alongside lean defaults. Blocked on maintainer review.*  
   https://github.com/zeroclaw-labs/zeroclaw/issues/7952

**Underlying needs analysis:** The most commented issues reveal a pattern of **usability and configuration friction**. Users want:
- Better defaults that work out of the box (#5808).
- Channel-specific quality-of-life improvements (#6055, #8445, #8442).
- Packaging that simplifies deployment (#7952).
- The community is **patient but persistent**—these issues have been open for weeks to months with no resolution.

## 5. Bugs & Stability

**New S1 (workflow-blocked) bugs reported today:**

- **#9019 — OpenAI Responses provider rejects vision-capable models** (0 comments) — `[Bug] S1`  
  *The `OpenAiResponsesModelProvider` hardcodes `vision = false`, rejecting image input. No fix PR yet.*  
  https://github.com/zeroclaw-labs/zeroclaw/issues/9019

- **#9021 — Not shown in top-30 but referenced in search**  
  *No S1 bugs beyond #9019 in the top-30 display.*

**Existing high-severity bugs (S1) still open:**

- **#5808 — Default 32k context budget exceeded** — *No fix PR in flight. 3 months open.*  
- **#8654 — skill-review fork panics (SIGSEGV)** — *"in-progress" but no linked fix PR. 10 days open.*  
- **#8642 — MCP/tool-schema cloning drives unbounded RSS growth** — *Split from OOM tracker. Known memory leak. No fix PR.*  
- **#8563 — SOPs not available through web dashboard** — *No fix PR.*  
- **#9016 — OpenAI tool turns fail (closed today)** — *Resolved.*

**Fix PRs in flight for open bugs:**

- **#9018** — Fix for `--config-dir` being ignored during locale detection (#9017). Submitted today by JordanTheJet.  
- **#8902** — Fix for bidirectional RPC in ZeroCode (#8578 related).  
- **#8951** — Fix for duplicating streamed narration on whitespace-only divergence.  
- **#8963** — Fix for Telegram bot command limit cap.  
- **#8353** — Error message context improvements (stale-candidate, needs author action).

**Risk assessment:** The project carries **five open S1 bugs**, three of which (#5808, #8642, #8654) are memory/stability critical and have no published fix PRs. This is a concerning pattern for production readiness.

## 6. Feature Requests & Roadmap Signals

**New feature requests today:**

- **#9022 — Slack Events API over HTTP for scale-to-zero deploys** (0 comments)  
  *User dakaii requests optional HTTP-based Slack Events API alongside polling and Socket Mode, enabling serverless deployments where only egress is available.*  
  https://github.com/zeroclaw-labs/zeroclaw/issues/9022

- **#9020 — Session rewind and fork-from-message in ZeroCode** (0 comments)  
  *Audacity88 filed this feature for recovery from bad session state. Strong signal this is a maintainer-prioritized UX improvement for v0.8.3.*  
  https://github.com/zeroclaw-labs/zeroclaw/issues/9020

**Roadmap signals from trackers:**
- **#9009 — Operator UX Onboarding, Pairing & Self-Service** — *New tracker (just created) for operator journey improvements.* Likely a post-v0.8.3 initiative.
- **#8891 — Persistent memory parity** — *Multi-PR rollout targeting full parity with mature peer runtimes.* Active Nillth PRs suggest this lands in v0.8.3.
- **#8832 — Gateway-local Kanban board for agent work** — *RFC stage. Low priority but signals future direction toward agent management UI.*
- **#7314 — WASM plugin program** — *Deferred tracker but #8852 PR shows WASM is actively landing.*

**Predictions for next version (v0.8.3):**
- WASM channel plugin execution (#8852, #8855, #8857)
- Memory staged retrieval pipeline (#8897, #8898)
- Memory content scanning (#8984)
- OpenAI Chat Completions endpoint (#8486)
- Quickstart capability-safe defaults (#8987)
- Matrix single-message streaming (#8443)
- ZeroCode Code pane consolidation (#8655)

## 7. User Feedback Summary

**Pain points expressed by users:**

- **"Default config doesn't work"** — JordanTheJet reports that the default 32k context budget is 3.3x too small on iteration 1 (#5808). This is a **fundamental onboarding friction** that has persisted for 3 months.
- **"I can't run cheap models for cron jobs"** — touhidurrr wants to run cron jobs on low-cost models like Gemma but finds no configuration path (#7762).
- **"Telegram bot registration fails"** — wangmiao0668000666 reports that Telegram `setMyCommands` fails with `BOT_COMMANDS_TOO_MUCH` when tools exceed 100 (#8950, fixed by #8963).
- **"SOPs don't work in web chat"** — susyabashti configured SOPs per StageHand examples but they're undetected by the runtime (#8563).
- **"Session history grows unbounded"** — jokewithme110 requests auto-truncation of stale session history to control token consumption (#8134).
- **"Matrix streaming is broken in two different ways"** — vrurg reports both current options (concat all turns, send each turn) are unsatisfactory and requests single-message drafts (#8442).

**Satisfaction signals:**
- Users are actively contributing features (JordanTheJet, vrurg, Nillth, Audacity88 are recurring contributors).
- The WASM plugin architecture is attracting community contributors (#8852, #8923).
- ZeroCode is getting active UX improvement work from external contributors.

**Dissatisfaction patterns:**
- Long-standing S1 bugs with no fix visibility (#5808, #8642, #8654).
- Features accepted weeks ago that are still "in-progress" with no milestone commitment (#6055, #6641).

## 8. Backlog Watch

**Issues needing maintainer attention (open >30 days, important):**

| Issue | Age | Severity | Status |
|-------|-----|----------|--------|
| #5808 — Default context budget exceeded | 88 days | S1 | `status:in-progress` but no fix PR |
| #6074 — 153 commits lost in bulk revert | 79 days | High | `status:in-progress`; needs recovery audit |
| #6055 — Slack thread hydration | 79 days | Medium | `status:in-progress`; 6 commenters waiting |
| #6641 — Turn-level OTel trace correlation | 60 days | Medium | `status:in-progress`; 5 commenters |
| #7952 — Full-channel prebuilt assets | 23 days | Medium | `status:blocked, needs-maintainer-review` |
| #7762 — Cron documentation + model selection | 26 days | Medium | `status:accepted`; no PR |

**PRs needing maintainer action:**

| PR | Age | Risk | Status |
|----|-----|------|--------|
| #8353 — Error message context improvements | 16 days | Low | `needs-author-action, stale-candidate` |
| #8486 — OpenAI chat completions endpoint | 13 days | High | `needs-author-action` |
| #8655 — ZeroCode Code pane consolidation | 9 days | High | `needs-author-action` |
| #8984 — Memory content scanning | 1 day | High | `needs-author-action` |
| #8443 — Matrix single-message streaming | 14 days | High | `needs-author-action` |
| #9015 — CLI bind verbs for WeChat/Line | 0 days | High | `needs-author-action` |

**Critical observation:** The `needs-maintainer-review` label appears on important items (#8134, #8832, #8891, #8963) suggesting the maintainer team may be bandwidth-constrained. The volume of `needs-author-action` PRs (at least 6) indicates contributors are waiting for feedback.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/kky-wollu/agents-radar).*