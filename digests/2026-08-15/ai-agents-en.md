# OpenClaw Ecosystem Digest 2026-08-15

> Issues: 500 | PRs: 500 | Projects covered: 13 | Generated: 2026-08-14 22:28 UTC

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

# OpenClaw Project Digest — 2026-08-15

## 1. Today's Overview

OpenClaw is exhibiting **extremely high issue and PR velocity**, with 500 issues and 500 PRs updated in the last 24 hours — indicating a very active community and a heavily engaged maintenance team. However, the project appears to be **stabilizing its core after a prolonged period of bug reports**, with only 9 of 500 issues closed in the last day and 98 PRs merged/closed. The surge of UI-focused PRs from a single contributor (vyctorbrzezowski) suggests an active design-system overhaul of the web dashboard is underway. No new releases were published today, so recent fixes remain on the `main` branch, awaiting a release train. The most significant ongoing problems remain clustered around **session-state integrity and silent message loss** across multiple channels (Telegram, WhatsApp, Discord), which continues to be a source of user frustration.

## 2. Releases

**None.** No new versions of OpenClaw were published in the last 24 hours. The last notable release mentioned in the issue tracker is `2026.7.1`, which introduced a regression affecting gateway startup on some systems (issue #108435). Users remain on the `2026.6.x` / `2026.7.x` line, with the maintainers apparently focusing on landing a batch of fixes before cutting a new release.

## 3. Project Progress

No PRs were explicitly marked as merged/closed today in the top-30 list (most remain open awaiting review, proof, or author action), but 98 PRs were closed/merged overall in the last 24h, indicating steady maintenance churn. Noteworthy PRs advanced for review in the last 24h include:

- **Security/Policy UX (#116489, closed)** — A large, XL-sized PR from jesse-merhi that is now closed. It introduced mandatory acknowledgement for install-policy warnings in the CLI, a security boundary improvement. Its companion UI PR (#120900) is still open and ready for a maintainer look.
- **Control UI Design System Overhaul** — A series of seven PRs from vyctorbrzezowski (#123603, #123594, #123586, #123655, #123566, #123626, #123613, #123681) are all waiting on author or review. They progressively unify the sidebar iconography, typography, transient surfaces, and session layout — a massive, systematic improvement to the web UI's polish and consistency.
- **Cloud Workers for Codex Runtime (#123743)** — An XL-sized feature PR from steipete which removes the hard gate that limited cloud worker deployments to the OpenClaw runtime, enabling them for the Codex harness, with security and availability flags.
- **Memory System Fixes** — PR #121115 from arhxam avoids repeating recall from context, and PR #121044 from IlyaKuprov fixes a bug where zero-hit memory search triggers a full index rebuild (which stalls on larger histories).
- **Platform/Provider Maintenance** — PRs were advanced for fixing legacy plugin crashes post-lifecycle-guard (#121096), Bedrock image capability preservation (#120919), Mattermost progress-post separation (#120854), and sandbox provisioning timeouts (#120861).

## 4. Community Hot Topics

The most active issue, and a clear sign of a resurfacing bug, is:

- **#121058 — "Silent reply failures still recurring"** — 94 comments, created and updated within the last 24h. This is a continuation of a long-plaguing bug where the gateway silently drops messages without ever queuing a reply payload. The monitoring cron for this failure mode is still logging new occurrences. This is the **highest-priority community concern** at the moment.

Other heavily-discussed issues, indicating long-standing pain points:

- **#44925 — "Subagent completion silently lost"** (28 comments, 2 👍) — P1 bug about subagent results being lost without retry, notification, or restart on timeout. It's a persistent problem impacting core reliability.
- **#91588 — "Gateway Memory Leak"** (24 comments, 1 👍) — P0 issue where RSS grows from 350MB to 15.5GB over days, causing OOM crashes, with no fix PR in sight.
- **#80319 — "QA tool-defaults suite conflates tools"** (18 comments) — A maintainer-heavy discussion about test harness architecture, not user-facing, but blocking closure on that front.
- **#96834 — "WhatsApp inbound image wedges lane"** (15 comments) — P1 bug where multimodal messages wedge the main lane for ~3 minutes.

The sheer volume of comments on #121058 suggests that a previously "closed" issue is resurfacing, which is a strong signal that the underlying fix was incomplete.

## 5. Bugs & Stability

The project is under significant stability pressure. Reported issues are ranked by severity (P0, P1, P2). The most critical, with no fix PRs yet, are:

**P0 (Critical)**
- **#91588 — Gateway Memory Leak** — RSS grows to 15.5GB, repeated OOM crashes. No fix PR. (High severity, affects all long-running users).
- **#108435 — Gateway fails to start after update to 2026.7.1** — A regression blocking gateway startup with systemd, ollama, and manual launch. 14 comments, 3 👍.
- **#119270 — File tools strip leading `@` from paths** — Data-loss bug where write/edit/apply_patch silently operates on the wrong file. 6 comments, no fix PR yet.

**P1 (High)** — With a heavy concentration on "silent message loss" and session-state corruption:
- **#121058** — Silent reply failures recurring (94 comments, most active issue).
- **#62505 — "Coding Agent never completes anything"** (15 comments) — A severe regression for coding-use-case users.
- **#86215 — Codex OAuth refresh failures wedge agent** (11 comments) — Authentication loops lasting hours.
- **#83959 — Codex app-server startup retries exhaust** (11 comments).
- **#96834 — WhatsApp image wedge** (15 comments).
- **#96975 — Subagent completion context overload** (12 comments).
- **#120563 — Conversation history not sent on Ollama/custom provider** (9 comments) — Core context-loss bug.
- **#98435 — MCP loopback not auto-reconnecting** (10 comments).
- **#47975 — Subagent sessions persist, main unresponsive** (10 comments).
- **#87109 — Gateway heap growth + silent cron failures** (9 comments).

**P1, with Fix PRs in the pipeline:**
- **#99910 — Memory dreaming run pegs event loop** — The PR "avoid repeating recall" (#121115) and zero-hit rebuild (#121044) address related memory-system stalls.
- **#121083 — Docs: SecretRef `provider: "default"` undocumented** (6 comments) — Has a clear fix shape and is queueable.

The three **most severe systemic problems** are: (1) the silent reply/loss failure mode, (2) memory leaks in the gateway process, and (3) session-state corruption after subagent/multiturn operations.

## 6. Feature Requests & Roadmap Signals

Several feature requests point at the future direction of OpenClaw:

- **UI/UX Polish (likely in next release):** The massive series of sidebar and design-system PRs from vyctorbrzezowski are explicitly "ready for maintainer look." These are cosmetic but high-visibility improvements that will likely be merged into the next minor release.
- **Cloud workers for Codex (#123743)** — A significant feature unlocking the Codex harness for cloud deployments. Awaiting author action, but likely to land soon.
- **Reaction-triggered agent turns (#17840)** — An opt-in mechanism to let reactions (e.g., emoji) wake the agent. 6 comments, low priority (P2) but a nice interactive pattern for future bots.
- **Slack Modal Support (#88154)** — First-class support for Slack modals for structured input. P2, with a clear use case for form-style workflows.
- **Per-model usage logging (#13219)** — A highly-requested feature for cost tracking. 8 comments, 1 👍.
- **Fully dynamic model discovery (#10687)** — Needed for OpenRouter's fast-moving catalog. 10 comments, 3 👍 — this is a strong roadmap signal as more users adopt multi-provider setups.
- **Pre-routing inbound hook (#81061)** — Requested for channel bridging/proxying. 8 comments, 3 👍.
- **Mattermost progress-post isolation (#120854)** — An opt-in feature to separate transient progress from final replies, a UX improvement likely to be replicated to other channels.

**Prediction:** The next release (likely `2026.8.x`) will include the full UI sidebar unification series, the Memory fix PRs (#121115, #121044), and possibly the cloud-workers-for-Codex feature. It is also likely to include targeted fixes for the most egregious P1 regressions (#62505, #120563).

## 7. User Feedback Summary

User sentiment is a **mix of high satisfaction and deep frustration with reliability**:

- **High Engagement / Satisfaction:** The community is extremely active, with users following up on issues with detailed context (e.g., #121058 with 94 comments), running monitoring crons, and contributing well-crafted bug reports. The feature request #73537 ("Add production-readiness stability label") openly thanks the maintainer, "Peter 👋," saying OpenClaw "has genuinely become part of our daily workflow" (Telegram integration, automations, cron, Home Assistant). This indicates strong product-market fit for personal/family assistants.
- **Deep Frustration with Reliability:** P1 issues consistently describe "silently lost" messages and session corruption, which erodes trust. Users describe "apologies for the vagueness" from the agent (#62505), "wedged" lanes (#96834), and "silent failures" with "no output, no push, no error report" (#87109). The recurring nature of #121058 ("still recurring after #116277 was closed") suggests the fix loop is not closing cleanly, leading to user fatigue.
- **Platinum Hermit Rating as a Proxy for Frustration:** The project's own "issue-rating" taxonomy assigns "platinum hermit" to the most impactful bugs. Many P0/P1 bugs carry this rating (e.g., #91588, #86215, #83959, #38327, #92241), signaling that the community feels these core issues with "crash-loop" or "data-loss" impact are the most significant blockers to daily use.

## 8. Backlog Watch

Several issues of high impact remain open and appear to lack attention from maintainers or a concrete fix plan ("clawsweeper:no-new-fix-pr", "clawsweeper:needs-maintainer-review"). The most concerning are:

- **#91588 (P0, Memory Leak)** — Open for over 2 months (June 9), 24 comments, tagged as `clawsweeper:no-new-fix-pr`. This is a **critical issue that is being ignored** by the autosweeper bot and likely requires manual maintainer intervention.
- **#62505 (P1, Coding Agent never completes)** — Open since April 7, 15 comments, no new fix PR. This is a **fundamental regression for the coding use case** and has been pending for over 4 months.
- **#38327 (P1, "Cannot convert undefined or null to object")** — Open since March 6, 14 comments, no fix PR. A long-standing auth-provider regression.
- **#44925 (P1, Subagent completion silently lost)** — Open since March 13, 28 comments, no fix PR. Core reliability issue.
- **#86214 (P1, Codex app-server client closes mid-turn)** — Open since May 24, 8 comments, no fix PR.

**Maintainer attention needed:** The "clawsweeper" bot appears to be cycling these issues into "needs-maintainer-review" states without a clear path forward. The **memory leak (#91588)** and the **coding agent regression (#62505)** stand out as the highest-priority items, with the most at stake in terms of user trust and core functionality. The maintainers should prioritize these to restore confidence in the platform's stability.

---

## Cross-Ecosystem Comparison

# Cross-Project Comparison Report: Personal AI Agent Open-Source Ecosystem
**Date:** 2026-08-15 | **Data Window:** Last 24 hours | **Projects Analyzed:** 13

---

## 1. Ecosystem Overview

The personal AI assistant open-source landscape is **highly active but fragmented**, with projects at varying stages of maturity and focus. The ecosystem is characterized by **rapid iteration on reliability** (silent message loss, session-state corruption, memory leaks) rather than purely feature-driven development, signaling a maturation phase where production-readiness is the primary competitive battleground. Projects cluster into three archetypes: **core agent frameworks** (OpenClaw, OpenClaw, Hermes Agent), **specialized/niche implementations** (PicoClaw for resource-constrained hardware, NanoClaw for supply-chain hardening), and **commercial-backed frontends** (CoPaw, LobsterAI). Cross-project convergence is visible around **MCP integration, provider-agnostic model routing, session-state integrity, and multi-channel UX parity** — indicating that the community has identified shared pain points that transcend individual implementations.

---

## 2. Activity Comparison

| Project | Issues (24h) | PRs (24h) | Merged/Closed PRs | Release Status | Health Score* |
|---|---|---|---|---|---|
| **OpenClaw** | 500 updated | 500 updated | 98 merged/closed | None (≥2026.7.1) | 🟠 **High activity, stability pressure** |
| **Hermes Agent** | 50 updated | 50 updated | 20 closed issues | None (v2026.8.13) | 🟡 **Stable w/ Windows risk** |
| **CoPaw** | 50 updated (38 closed) | 41 updated | 15 merged/closed | None (2.1.0 beta) | 🟠 **Feature-rich, review bottleneck** |
| **ZeroClaw** | 33 updated | 50 updated | 0 merged (all in-review) | None (v0.8.5 weekly) | 🟠 **Stabilizing, RFC-heavy** |
| **IronClaw** | 25 updated (9 closed) | 48 updated | 23 merged/closed | **✅ v1.2.0 stable** | 🟢 **Strong, disciplined** |
| **LobsterAI** | 2 updated | 27 updated | 22 merged/closed | **✅ v2026.8.14** | 🟢 **Healthy, shipping fast** |
| **NanoBot** | 3 updated (2 closed) | 23 updated | 8 merged/closed | None | 🟢 **Efficient, responsive** |
| **PicoClaw** | 3 updated | 8 updated | 5 closed (stale-tagged) | None (nightly only) | 🟠 **Maintenance, review lag** |
| **NanoClaw** | 2 new | 9 updated | 3 closed (2 intentional) | None | 🟢 **Stable, CI-focused** |
| **Moltis** | 0 updated | 1 updated | 0 | None | 🟡 **Stalled, single-PR** |
| **NullClaw** | 0 updated | 1 updated | 1 merged | None | 🟢 **Quiet, stable** |
| **TinyClaw** | 0 | 0 | 0 | — | ⚪ **Idle** |
| **ZeptoClaw** | 0 | 0 | 0 | — | ⚪ **Idle** |

*\*Health score is a qualitative synthesis of activity level, response efficiency, bug severity, and release cadence. 🟢 = healthy momentum; 🟠 = active but under strain; 🟡 = stable with noted risk; ⚪ = dormant.*

---

## 3. OpenClaw's Position

**Advantages vs. Peers:**

- **Unmatched community scale** — 500 issues/500 PRs in 24h is 10x the nearest competitor (Hermes, CoPaw at 50). OpenClaw is the de facto **community standard** for personal AI assistants.
- **Platform breadth** — Supports Telegram, WhatsApp, Discord, Slack, Mattermost, and more, with active work across all channels. Competitors (CoPaw, PicoClaw) are still catching up on per-channel parity.
- **UI/UX investment** — A dedicated design-system overhaul (7 PRs from vyctorbrzezowski) signals commitment to polish that most peers lack.
- **Roadmap vitality** — Cloud workers for Codex, memory-system fixes, and a P1-fix pipeline demonstrate a forward-looking trajectory.
- **Strong user loyalty** — Explicit user testimonials ("genuinely become part of our daily workflow") indicate deep product-market fit for personal/family use cases.

**Technical Approach Differences:**

- **Gateway-centric architecture** — OpenClaw centralizes multi-channel delivery through a gateway process. This enables broad channel support but creates concentrated risk: memory leaks (#91588, 350MB→15.5GB RSS) and silent reply failures (#121058) are gateway-level failures with wide blast radius.
- **Rust-based core (inferred from "Codex runtime" and "cloud workers" references)** — Performance-oriented but slower to iterate than Python-based competitors (NanoBot, CoPaw/AgentScope).
- **AI-powered issue triage** — The "clawsweeper" bot automates bug classification, but the bot's failure to address the P0 memory leak (open 2+ months) indicates **automation cannot replace maintainer judgment**.

**Community Size Comparison:**

| Metric | OpenClaw | Hermes Agent | CoPaw | IronClaw |
|---|---|---|---|---|
| Issues (24h) | 500 | 50 | 50 | 25 |
| PRs (24h) | 500 | 50 | 41 | 48 |
| Comments on top issue | 94 | 16 | 8 | 1 |
| Contributor diversity | High | High | Moderate | Core-team-centric |

**OpenClaw's disadvantage:** The sheer issue volume means individual bugs receive diluted attention. The most-commented issue (#121058, 94 comments) is a resurfaced bug, suggesting the **fix loop is not closing cleanly** — a trust-eroding pattern that smaller, more responsive projects (NanoBot at 2 issues closed same-day) avoid.

---

## 4. Shared Technical Focus Areas

| Focus Area | Projects | Specific Needs |
|---|---|---|
| **Session-state integrity** | OpenClaw (#44925 subagent loss), Hermes (#67442 cross-process serialization), NanoBot (#5271 stale saves), CoPaw (#7011 cross-session pollution) | Prevent silent data loss; deterministic behavior under concurrency; reliable session resume across clients |
| **Provider-agnostic model routing** | OpenClaw (#10687 dynamic discovery), ZeroClaw (#8603 Chat Completions profile), CoPaw (#6302 unified provider), IronClaw (#7183 per-user LLM) | Dynamic model catalogs; per-session overrides; OpenAI-compatible protocol for ecosystem tooling |
| **MCP reliability & compatibility** | OpenClaw (#98435 loopback), NanoBot (#5179 SDK v2 migration), PicoClaw (#3269 connection hang), IronClaw (#7661 memory provider), Moltis (#1190 connectors) | Reconnection, auth flows, error handling, v2 migration |
| **Multi-channel UX parity** | PicoClaw (#3307 sessions on Telegram), CoPaw (Feishu/DingTalk/QQ), ZeroClaw (Telegram model picker), OpenClaw (design-system UI overhaul) | Consistent session management, media support, and interaction patterns across all channels |
| **Memory system robustness** | OpenClaw (#121115 recall), NanoBot (#5018 skill context), Hermes (#85622 provider contract), ZeroClaw (#9919 fallback silent) | Pluggable backends, explicit context loading, no silent degradation |
| **Windows support** | Hermes (#86223 P1 desktop broken), NanoBot (#5382 PermissionError), NanoClaw (#3246 orphan cleanup), ZeroClaw (#7462 74 test failures), IronClaw (smoke fixes in v1.2.0) | First-class desktop client, no crashes, test parity |
| **Supply-chain / security hardening** | NanoClaw (#3243 signature approver), ZeroClaw (RFC #6971 ingress policy), Hermes (#77472 redaction), OpenClaw (#116489 install policy) | Verified builds, secrets redaction, permission boundaries |

**Key insight:** Session-state integrity and MCP reliability are **universal pain points** — every active project has at least one open issue in each category. This is the ecosystem's shared "tax" for building agent frameworks, and solving it well is the fastest path to differentiation.

---

## 5. Differentiation Analysis

| Project | Target User | Architecture | Key Differentiator |
|---|---|---|---|
| **OpenClaw** | Personal/family assistant, power users | Gateway-centric, Rust core | **Breadth** — channel count, plugin ecosystem, community scale |
| **Hermes Agent** | Desktop-first, multi-platform | Desktop client + gateway, session serialization | **Desktop UX polish** + i18n/state hooks |
| **IronClaw** | Self-hosted, structured automations | Release-disciplined, v1.2.0 stable, QA dogfooding | **Deterministic automations** + MCP-backed pluggable memory |
| **CoPaw** | Enterprise/China-market, multi-channel | AgentScope-based, Python | **Enterprise channel breadth** (Feishu, DingTalk, QQ) + desktop/mobile |
| **ZeroClaw** | Security-conscious self-hosters | RFC-driven architecture, Rust | **Security posture** (redaction, auth RFCs, universal ingress) |
| **NanoBot** | Developer/API-first users | Python, WebUI + CLI | **Type safety** (pyright suppressions) + WebUI collaboration features |
| **LobsterAI** | Consumer desktop app (China) | Electron-style frontend, OpenAI-compatible | **Polished desktop UX** + cowork multi-agent chat |
| **PicoClaw** | Resource-constrained hardware (IoT/edge) | Go, 10MB RAM target | **Extreme efficiency** (sub-second boot, $10 hardware) |
| **NanoClaw** | CI/CD-focused self-hosters | Node.js heritage, supply-chain verification | **Verified builds** (cosign signatures, auto-merge gates) |
| **Moltis** | Offline-first, privacy-focused | Connector-based (CalDAV, Gmail, Slack) | **Durable external connectors** + local full-text search |

---

## 6. Community Momentum & Maturity

### Tier 1: Rapidly Iterating (high velocity, high responsiveness)
- **NanoBot** — 8 PRs merged/closed in 24h, 2/3 issues closed, bug-to-fix same-day (#5391→#5392). **Most efficient per-issue throughput.**
- **LobsterAI** — 22 PRs merged/closed, release shipped yesterday. **Highest release cadence.**
- **IronClaw** — 23 PRs merged, v1.2.0 stable, disciplined RC validation. **Most structured development process.**

### Tier 2: High Activity, Moderate Velocity (engaged but under strain)
- **OpenClaw** — 98 PRs merged/closed but 500+ open; critical P0s (memory leak) unaddressed for 2+ months. **Volume without proportional closure.**
- **CoPaw** — 15 PRs merged, 38 issues closed, but 26 PRs awaiting review and a critical cross-session bug without fix. **Review bottleneck.**
- **Hermes Agent** — 20 issues closed, steady PR cadence, but P1 Windows blocker unaddressed and needs-decision backlog. **Stable but at risk.**
- **ZeroClaw** — 50 PRs in-review but **zero merged in 24h**; 5+ RFCs awaiting maintainer decisions. **Deliberate but slow — consolidation phase.**

### Tier 3: Stabilizing / Consolidating
- **NanoClaw** — Low issue/PR volume, but CI/supply-chain hardening is progressing. **Quiet, reliable.**
- **PicoClaw** — Stale-bot sweep, 3 substantive PRs waiting (1 for 45 days). **Review velocity is the bottleneck.**

### Tier 4: Dormant / Single-Threaded
- **NullClaw** — 1 PR merged, 0 issues. **Maintenance-only.**
- **Moltis** — 1 open PR (4 days, no comments). **Stalled or internally reviewing.**
- **TinyClaw / ZeptoClaw** — **No activity at all.**

---

## 7. Trend Signals

### 1. "Silent failure" is the #1 trust-killer
Across OpenClaw (#121058), CoPaw (#7016), Hermes (#67442), and NanoBot (#5271), users consistently report **messages lost without error or retry**. Agents that fail loudly and recover cleanly will win user trust. **Action for developers:** instrument for detection, add retry/notification on failure, and make failure modes visible in UI.

### 2. Protocol interoperability is a strategic unlock
ZeroClaw's Chat Completions RFC (#8603) and Hermes' Grok/xAI parity campaign (#80424) show users want **drop-in compatibility with existing OpenAI-ecosystem tooling** (Open WebUI, LobeChat, Continue.dev). Being a "citizen of the OpenAI protocol world" is table-stakes; building proprietary protocols is a dead-end.

### 3. MCP is becoming the universal integration bus
From OpenClaw's loopback to IronClaw's pluggable memory to PicoClaw's connection handling, **MCP is the chosen abstraction for external tools and memory**. The ecosystem is moving from "how to connect tools" to "how to make MCP connections reliable, secure, and reconnecting."

### 4. Deterministic automations over probabilistic agents
IronClaw's structured-automation spec, ZeroClaw's goal-mode RFC (#8303), and OpenClaw's cron fixes all point to the same need: **users want scheduled/bounded execution that produces predictable results**, not "hit-or-miss" outcomes. The "hit-or-miss" complaint (IronClaw #6879) is the clearest articulation: *trust requires determinism*.

### 5. Windows is the weakest link everywhere
Windows is **not a first-class platform** in most projects' test suites (ZeroClaw 74 failures, Hermes P1 desktop broken, NanoBot PermissionError, NanoClaw orphan cleanup). With Windows being the dominant desktop OS, projects that make Windows reliable first will capture the widest desktop user base.

### 6. Security hardening is moving from bolt-on to built-in
NanoClaw's supply-chain verification, ZeroClaw's ingress-policy RFCs, Hermes' dump-redaction issue, and OpenClaw's install-policy acknowledgment all signal a maturation from "works" to "works *securely*." Expect security certifications and signed releases to become marketing differentiators.

### 7. Memory is becoming pluggable and provider-neutral
IronClaw's MCP-backed memory provider, OpenClaw's memory fixes, Hermes' standalone memory-provider PR, and Moltis' durable connectors all point toward **memory as a configurable subsystem**, not a hard-coded feature. The closed "hosted memory" wontfix on ZeroClaw confirms: memory is core, not an add-on.

### 8. Multi-channel UX parity is a feature race
Users increasingly run agents across Telegram, Discord, Feishu, WeChat, and web — and expect **identical session management, media handling, and interaction patterns** on every channel. PicoClaw's session-management request, CoPaw's Feishu bugs, and ZeroClaw's Telegram model picker all signal that channel feature parity is a differentiator.

---

## Executive Summary

| Dimension | Top Performers | At-Risk Areas |
|---|---|---|
| **Velocity** | LobsterAI, IronClaw, NanoBot | OpenClaw (volume without closure), ZeroClaw (0 merges) |
| **Reliability** | IronClaw (v1.2.0 stable), NanoBot (same-day fixes) | OpenClaw (P0 leak, silent failures), CoPaw (cross-session bug) |
| **Community Health** | OpenClaw (unmatched scale), Hermes (engaged contributors) | Review bottlenecks in CoPaw, PicoClaw; decision backlog in ZeroClaw |
| **Strategic Direction** | IronClaw (deterministic automations), ZeroClaw (security RFCs), NanoBot (MCP v2) | Moltis, NullClaw (dormant/stalled) |

**Biggest emerging opportunity:** The universal pain points — session integrity, MCP reliability, deterministic execution, and Windows parity — are **unowned by any single project**. A project that solves these four comprehensively will set the ecosystem standard.

---

## Peer Project Reports

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot Project Digest
**Date:** 2026-08-15

---

## 1. Today's Overview

NanoBot is experiencing a period of high development velocity, with 23 PRs updated in the last 24 hours and a healthy mix of opens (15) and merges/closures (8). The project is also processing issues efficiently, closing 2 of the 3 active issues within a day, demonstrating a responsive maintainer team. The most significant technical activity centers on infrastructure hardening—ranging from a critical session overwrite bug to an Anthropic streaming timeout regression—alongside substantial WebUI feature development. No releases were published today, indicating the project is likely consolidating code before the next version bump. Momentum is clearly positive, with multiple contributors (at least 10 distinct authors) actively engaged.

---

## 2. Releases

No new releases were published on 2026-08-15. The project appears to be in an active development phase, with the backlog of merged changes likely preparing for a future release candidate.

---

## 3. Project Progress

A total of **8 PRs** were merged or closed in the last 24 hours, covering a diverse range of improvements:

- **Bug Fix — Anthropic Streaming Timeout (`#5392`)** — Closed PR that fixes issue [#5391](https://github.com/HKUDS/nanobot/issues/5391) where `NANOBOT_STREAM_IDLE_TIMEOUT_S` incorrectly acted as a total timeout rather than an inactivity timeout on the no-callback path of `AnthropicProvider.chat_stream`. This prevented long but active generations from being killed prematurely.

- **Bug Fix — File-cap Archive Failure (`#5378`)** — Closed issue resolved where `Session.enforce_file_cap()` mutated the live session before the archive callback, leading to a corrupted in-memory state if the callback raised. A fix is included in the merged changes.

- **WebUI Polish — Sidebar and Session Transitions (`#5393`)** — Merged a UI-only history that improves sidebar hierarchy, connector lines, tab treatment, and folder presentation, split cleanly from the collaboration PR for independent review.

- **WebUI Polish — Conversation Groups and Shared Shapes (`#5395`)** — Merged refinements for consistent group terminology, full localization of the grouping workflow, simplified delete confirmation styling, and a shared shape scale across WebUI controls.

- **Provider Feature — OAuth Status and Expiry Warnings (`#4689`)** — Closed after updates; adds shared OAuth provider status helpers and proactive token expiry warnings across CLI, WebUI, and runtime sessions. This brings long-awaited provider UX visibility.

- **Skills Enhancement — Explicit Context Loading (`#5018`)** — Closed after updates; fixes the critical gap where `skill_names` input on `ContextBuilder` was ignored, preventing direct callers from preloading explicitly requested skills.

---

## 4. Community Hot Topics

The most active discussions (by comment count) reveal a strong focus on **quality engineering** and **session concurrency correctness**:

1. **Refactor: Narrow File-Level Pyright Suppressions (`#5396`)** — [Open PR](https://github.com/HKUDS/nanobot/pull/5396) (Fixes [#5161](https://github.com/HKUDS/nanobot/issues/5161))
   Actively working to remove 31 file-level type suppression directives in favor of precise, file-local suppressions. This signal reflects a growing commitment to type correctness across the codebase—a sign of project maturity.

2. **Prevent Stale Background Task Saves (`#5271`)** — [Open PR](https://github.com/HKUDS/nanobot/pull/5271) (priority: p0)
   This is the highest severity PR currently open. It addresses a serious concurrency issue where stale background work can overwrite session data after `/new` or lifecycle replacement. The extended lifespan (8+ days) of this p0 suggests it's a complex fix under active review.

3. **Skills: Allow Marketplace Skills to Shadow Builtins (`#5309`)** — [Open PR](https://github.com/HKUDS/nanobot/pull/5309)
   The marketplace currently prevents installing workspace skills that share names with bundled skills (e.g., `github`), returning without installing the workspace copy. Users are likely frustrated by this silent failure when they intend to customize built-in functionality.

**Underlying Need Analysis:** The community is pushing for two things: (a) strict type safety as the codebase scales and (b) deterministic session/state behavior under concurrency. Long-running PRs on p0 issues signal that maintainers are prioritizing correctness over shipping speed.

---

## 5. Bugs & Stability

Ranked by severity:

| Severity | Bug | Status |
| --- | --- | --- |
| **High (p0)** | **Stale background task saves overwrite session data** ([PR #5271](https://github.com/HKUDS/nanobot/pull/5271)) — `JsonlSessionStore` can lose data when background work completes after a `/new` command. | Fix open, under active development |
| **Medium (p2)** | **Anthropic stream timeout kills active generations** ([Issue #5391](https://github.com/HKUDS/nanobot/issues/5391)) — Idle timeout (default 90s) applied as total timeout on no-callback path, killing long but active generations. | **Fixed** — merged in PR [#5392](https://github.com/HKUDS/nanobot/pull/5392) |
| **Medium** | **File-cap archive failure corrupts session before persistence** ([Issue #5378](https://github.com/HKUDS/nanobot/issues/5378)) — Session mutates before archive callback; if the callback raises, a later save can't recover the lost overflow data. | Fixed (addressed in merged changes) |
| **Medium (p2)** | **Windows transient `PermissionError` crash** ([PR #5382](https://github.com/HKUDS/nanobot/pull/5382)) — `os.replace()` crashes the entire gateway on transient Access Denied during heartbeat cron saves (confirmed twice in 2026-08-11 logs). | Fix open, add retry logic |

**Notable:** No new crashes or data-loss-level regressions were opened today. Windows compatibility remains a recurring focus.

---

## 6. Feature Requests & Roadmap Signals

Several features are in flight or recently merged, indicating likely coming in the next minor release:

- **WebUI Collaboration via Mentions (`#5358`)** — [Open PR](https://github.com/HKUDS/nanobot/pull/5358) — Adds stable server-owned `@name` identifiers for persisted WebUI sessions and extends the composer mention picker for peer session selection. This is a foundational step toward collaborative agent usage.

- **Drag-and-Drop Session Organization (`#5389`)** — [Open PR](https://github.com/HKUDS/nanobot/pull/5389) — Includes reordering, grouping by drag, and support for the latest pane-based session layout. Combined with #5358, WebUI session UX is being significantly upgraded.

- **Interactive Particle Hero Background (`#5340`)** — [Open PR](https://github.com/HKUDS/nanobot/pull/5340) — Lazy-loaded Canvas background with spring motion for empty threads. A major aesthetic passing, indicating the team is investing in first-time user experience.

- **Native TypeScript Terminal UI (`#4329`)** — [Open PR (June)](https://github.com/HKUDS/nanobot/pull/4329) — Rebuilds `nanobot agent` as a native TypeScript/OpenTUI client, keeping the Python gateway as the backend. This long-lived PR (2 months) signals a strategic move toward a modern terminal client.

- **MCP SDK v2 Migration with Legacy Compatibility (`#5179`)** — [Open PR](https://github.com/HKUDS/nanobot/pull/5179) — Migrates to MCP v2 high-level `Client` API while preserving SSRF validation, redirect checks, DNS pinning, proxy routing, and finite timeouts. This is critical for ecosystem compatibility.

**Prediction:** The WebUI collaboration and session organization features (#5358, #5389) plus session stale-save fix (#5271) are the most likely to ship in the next release.

---

## 7. User Feedback Summary

- **Happiness around quick bug fixes:** The Anthropic streaming timeout bug (#5391) was reported and fixed within the same day. Users encountering this would have seen active generations killed at 90s falsely; this fix will materially improve long-generation workflows.

- **Frustration with marketplace skill overrides:** There is clear user pain around not being able to define their own skill implementations for built-ins like `github` (PR #5309). This is a permissions/usability issue—the install button is non-functional and the system silently returns without installing the workspace copy.

- **Session data loss concerns:** The p0 stale save issue (#5271) likely causes infrequent but highly damaging data loss, undermining trust in sessions. Its extended fix timeline may frustrate affected users.

- **Positive signal on OAuth experience:** The merged OAuth status/expiry feature (#4689) should improve user visibility into when tokens are about to expire—a common source of mid-session failure.

---

## 8. Backlog Watch

Items requiring maintainer attention due to their importance, complexity, or longevity:

1. **Prevent Stale Background Task Saves (`#5271`, p0)** — [Open PR](https://github.com/HKUDS/nanobot/pull/5271) (created Aug 6, open 9 days) — Highest severity production issue, could cause silent data loss. Needs decisive review/merge.

2. **Subagent Partial Completion Results (`#5152`)** — [Open PR](https://github.com/HKUDS/nanobot/pull/5152) (created Jul 28, open 18 days) — Addresses logical correctness in runnner: the model currently infers unfinished subagent results as complete. A known issue with a tested fix.

3. **Weather Skill (`#4145`)** — [Open PR](https://github.com/HKUDS/nanobot/pull/4145) (created Jun 1, open 75 days) — A long-standing, uncontroversial multi-file skill + tests + docs contribution that appears stalled. May need a rebase and maintainer check.

4. **Native TypeScript Terminal UI (`#4329`)** — [Open PR](https://github.com/HKUDS/nanobot/pull/4329) (created Jun 13, open 63 days) — Ambitious frontend rewrite. While active, its very long lifespan risks divergence from the Python gateway. Maintainers should decide direction promptly.

5. **Marketplace Skills Shadowing (`#5309`)** — [Open PR](https://github.com/HKUDS/nanobot/pull/5309) (created Aug 9, open 6 days) — The silent install failure is user-visible and should be prioritized.

---

*Data source: [HKUDS/nanobot](https://github.com/HKUDS/nanobot) on GitHub. Digest generated 2026-08-15.*

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent Project Digest
**Digest Date:** 2026-08-15
**Data Window:** Issues/PRs updated in last 24h

---

## 1. Today's Overview

Hermes Agent is showing a moderate-high level of community activity, with 50 issues and 50 PRs updated in the last 24 hours. The project is in an active development phase with a steady influx of new bug reports (notably a P1 Windows desktop update blocker) and a healthy stream of feature contributions, particularly around i18n localization (Brazilian Portuguese, Persian) and desktop UX polish.

The triage pipeline is functioning, though a significant portion of open issues carry `needs-decision` or `needs-repro` labels, indicating a bottleneck in maintainer decision-making and prioritization. A notable cluster of issues focuses on session state management (`sweeper:risk-session-state`), specifically around profile overrides, session resumption, and state serialization—a complex area that continues to generate regressions and deep architectural discussions.

While there are no new releases today, the high number of open PRs (45) and closed issues (20) suggests a "fix-forward" cadence, with community members actively submitting patches for reported bugs (e.g., Telegram flood control, browser tab recovery, terminal output archival).

---

## 2. Releases

**No new releases were published in the last 24 hours.**

*The most recent stable version referenced in issues is `v2026.8.13`, with the next patch expected to address the critical Windows desktop update failure (see Bugs & Stability).*

---

## 3. Project Progress

**Merged/Closed PRs & Implemented Fixes:**

The following high-impact fixes were closed in the last 24 hours, deviating from the 20 closed issues:

1. **Desktop Profile Socket Reuse Fixed** — [#85777](https://github.com/NousResearch/hermes-agent/issues/85777): A critical bug where switching local named profiles after an update would leave the Desktop app attached to the default profile's socket was resolved. This was a P2 regression affecting multi-profile users.

2. **TUI Stale Session Content Fixed** — [#62170](https://github.com/NousResearch/hermes-agent/issues/62170): Resolved a v0.18.1 issue where the TUI displayed stale session content after switching sessions, a common usability pain point.

3. **Profile Override Reset Bug Fix** — [#50233](https://github.com/NousResearch/hermes-agent/issues/50233): Fixed a P2 bug where `SOUL.md` and skills resolved to the root profile instead of the user's selected profile due to a premature reset of the profile override.

4. **Dashboard Session Resume Fixes** — [#64425](https://github.com/NousResearch/hermes-agent/issues/64425) & [#63701](https://github.com/NousResearch/hermes-agent/issues/63701): Both addressed regressions where clicking a past session in the dashboard opened a blank or empty session instead of the conversation transcript.

5. **Gateway Crash on List Config** — [#83185](https://github.com/NousResearch/hermes-agent/issues/83185): A P1 crash affecting all gateway platforms (Telegram, Discord) when `gateway.platforms` was defined as a standard list format was resolved.

6. **CLI Updater Diverged Install Fix** — [#53479](https://github.com/NousResearch/hermes-agent/issues/53479): Fixed shallow/diverged `git rev-list` count logic in the CLI updater, preventing misleading "Found N new commits" messages.

---

## 4. Community Hot Topics

**Most Discussed Issues (by comment count):**

1. **Cross-Process Session Serialization ([#67442](https://github.com/NousResearch/hermes-agent/issues/67442))** — 16 comments, `needs-decision`
   - **Analysis:** This is the most active technical discussion. It addresses an architectural edge case where CLI-continuity sessions sharing a gateway session across OS processes lack a DB-level lease, risking race conditions for turn serialization. The need for a maintainer decision here indicates a design crossroads that could impact session reliability significantly.

2. **GUI Zoom Intermittent Reset ([#60693](https://github.com/NousResearch/hermes-agent/issues/60693))** — 13 comments, **Closed**
   - **Analysis:** Despite being closed, this issue drew significant engagement. The root cause appears to be a host of related Electron window-focus issues (see #84274, #82713, #81879, #50837). The community is clearly frustrated by UI zoom instability across different triggers (RDP, Alt-Tab, launching other Electron apps), suggesting this should have been prioritized earlier as a UX-critical bug family.

3. **Grok/xAI Feature Parity Campaign ([#80424](https://github.com/NousResearch/hermes-agent/issues/80424))** — 10 comments, `needs-decision`
   - **Analysis:** A meta-issue advocating for full alignment with the official xAI developer platform, covering Models, Function calling, Reasoning, Streaming, and Imagine image/video. This signals a strong community desire for Hermes to be a first-class citizen for all major provider APIs.

4. **External Memory Provider "Additive" Contract Breach ([#85622](https://github.com/NousResearch/hermes-agent/issues/85622))** — 9 comments, P3
   - **Analysis:** Users are invoking the documented "additive, never replacing" contract for external memory providers. The bug, where built-in MEMORY.md/USER.md injection is suppressed on new chats, is a clear documentation-vs-implementation mismatch that erodes trust in feature contracts.

---

## 5. Bugs & Stability

**Ranked by Severity:**

1. **[P1] Windows Desktop Client Broken After Updates** — [#86223](https://github.com/NousResearch/hermes-agent/issues/86223)
   - **Impact:** The desktop client is completely broken on Windows after the last 2 updates. Backend exits with code 1, cannot self-restart, and hits WinError 32 lock chains. This is a blocker for all Windows desktop users and should be the top priority for a hotfix release.

2. **[P1] Gateway Crash with List Platform Config** — [#83185](https://github.com/NousResearch/hermes-agent/issues/83185) **(Closed)**
   - **Impact:** Was breaking all gateway messages (Telegram, Discord) for users with standard config. Already fixed, highlighting a regression from a `perf(gateway)` commit.

3. **[P2] Persistent Unredacted Tool Content in Dumps** — [#77472](https://github.com/NousResearch/hermes-agent/issues/77472)
   - **Impact:** Security issue (HIGH severity controlled residuals). Request dumps, trajectory JSONL, `pending_messages`, and `/save` persist tool content unredacted (only regex-redacted with `force=True`). 11 live dumps up to 166 KB exist, potentially containing sensitive data.

4. **[P2] External Memory Provider Suppresses Built-in Memory** — [#85622](https://github.com/NousResearch/hermes-agent/issues/85622)
   - **Impact:** Breaks documented "additive" contract, leading to loss of context for users relying on both external and built-in memory.

5. **[P2, Needs-Repro] Xiaomi MiMo v2.5 Pro Tool Calling Broken** — [#86403](https://github.com/NousResearch/hermes-agent/issues/86403)
   - **Impact:** Enabled tools are not exposed to the model for a major provider, making the agent useless for any tool-based task with this model.

6. **[P2] macOS Screen Recording Permission Loop** — [#86385](https://github.com/NousResearch/hermes-agent/issues/86385)
   - **Impact:** Post-update, users with a stale TCC grant are stuck in a loop where the toggle is ON but cannot be re-granted, breaking screen recording capabilities.

**Fix PRs Available:** PR [#86414](https://github.com/NousResearch/hermes-agent/pull/86414) fixes a desktop model-pick persistence bug. PR [#86406](https://github.com/NousResearch/hermes-agent/pull/86406) fixes terminal output archival. PR [#86216](https://github.com/NousResearch/hermes-agent/pull/86216) hardens tool-call arg schema validation.

---

## 6. Feature Requests & Roadmap Signals

**Active Feature Work (Open PRs):**

1. **i18n Expansion is Hot** — The community is actively filling localization gaps:
   - **Brazilian Portuguese** ([#86292](https://github.com/NousResearch/hermes-agent/pull/86292))
   - **Persian (Farsi) with RTL** ([#86335](https://github.com/NousResearch/hermes-agent/pull/86335))
   - *Prediction:* Multi-language support is a clear near-term roadmap item, with these PRs likely to be merged into the next minor release.

2. **"Freemaxxing" No-Auth Provider Pool** ([#85631](https://github.com/NousResearch/hermes-agent/pull/85631)) — A feature PR to add a failover pool of no-auth OpenAI-compatible providers. This addresses cost-sensitivity and reliability, though `needs-decision` suggests maintainers are weighing policy implications.

3. **State Transformation Plugin Hooks** ([#86298](https://github.com/NousResearch/hermes-agent/pull/86298)) — Adds `transform_message_store`/`transform_message_load` hooks to the sqlite boundary, enabling encryption or custom serialization. This is a powerful plugin API extension.

4. **Standalone Memory Providers End-to-End** ([#82649](https://github.com/NousResearch/hermes-agent/pull/82649)) —A draft PR to make GBrain a true memory provider, coordinated with other ecosystem changes. Signals deep work on memory architecture.

5. **A2A Streaming Message Support** ([#86369](https://github.com/NousResearch/hermes-agent/pull/86369)) — Implements client-side `SendStreamingMessage` with card-gated fallback, improving inter-agent communication.

6. **Desktop UX Polish** — PRs for matte glass translucency ([#84329](https://github.com/NousResearch/hermes-agent/pull/84329)) and stripping ANSI decoration on copy ([#86301](https://github.com/NousResearch/hermes-agent/pull/86301)) are small but high-quality quality-of-life improvements.

**Meta-Architecture Signals:**
- **Unified Deadline Layer** ([#85125](https://github.com/NousResearch/hermes-agent/issues/85125)): A proposed 4-phase architectural fix to eliminate the 400+ timeout/hang bugs. This is a major roadmap signal that maintainers should evaluate carefully.

---

## 7. User Feedback Summary

**Recurring Pain Points:**

1. **Session Resume Fidelity (High Dissatisfaction):** Multiple issues across TUI, Dashboard, and Web clients ([#62170](https://github.com/NousResearch/hermes-agent/issues/62170), [#64425](https://github.com/NousResearch/hermes-agent/issues/64425), [#63701](https://github.com/NousResearch/hermes-agent/issues/63701)) where resuming a session shows blank content or stale state. This is a core trust-breaking bug for daily users.

2. **UI Zoom Instability (Medium Dissatisfaction):** A cluster of 4+ issues ([#60693](https://github.com/NousResearch/hermes-agent/issues/60693), [#84274](https://github.com/NousResearch/hermes-agent/issues/84274), [#82713](https://github.com/NousResearch/hermes-agent/issues/82713)) across Windows and macOS contexts where UI zoom resets to 100% after focus changes or external events. Users expect persistent settings.

3. **Windows Platform Instability (High Dissatisfaction):** The P1 desktop update failure ([#86223](https://github.com/NousResearch/hermes-agent/issues/86223)) is a significant negative signal for the Windows user base, who are being left with a broken client for extended periods.

4. **Configuration Format Friction (Medium):** Issues like the gateway list-config crash ([#83185](https://github.com/NousResearch/hermes-agent/issues/83185)) and deprecated `.env` misreporting ([#86393](https://github.com/NousResearch/hermes-agent/issues/86393)) indicate that configuration parsing edge cases still bite users.

**Positive Signals:**
- **Eager Contributors:** The number of high-quality, well-scoped PRs from community members (not just maintainers) is a strong positive indicator for project health. Contributors like `andrexibiza`, `lxman`, and `veltri-23` are consistently delivering valuable code.
- **Clear Documentation of Bugs:** Reports like the memory provider contract breach ([#85622](https://github.com/NousResearch/hermes-agent/issues/85622)) show users are reading and enforcing documented guarantees.

---

## 8. Backlog Watch

**Items Requiring Maintainer Attention (Unanswered or Aging):**

1. **[#80233] Long-running config:** The "Agentic coding via the Hermes GUI" feature request has been open since June with activity through August 14. It proposes a plugin architecture for running tasks across different GUIs/IDEs. This is a major feature request that seems to have stalled in triage.

2. **[#77472] Security Dump Redaction:** Open since Aug 3, this HIGH-severity security issue about unredacted tool content persists. While there is a PR ([#86216](https://github.com/NousResearch/hermes-agent/pull/86216)) to harden tool-call args, the broader dump redaction issue needs a committed fix. The `needs-repro` label on a security issue of this magnitude is concerning.

3. **[#63892] WebRTC streaming for the dashboard:** Open since July 12, this feature request for in-memory WebRTC streaming has gone unanswered by maintainers. With the dashboard's known session-resume bugs, improving its underlying streaming architecture is a logical next step.

4. **[#60119] "Hermes on Laptop / Desktop is inefficient":** A discussion about local resource usage and GPU acceleration. This is an important "quality of life" and "cost of operation" topic that could influence the project's local-first positioning.

5. **[#58404] ACP state store + recovery replay:** Open since July 1, this protocol feature suggestion has not received a maintainer response. In light of the two open bug-fix PRs for ACP mode ([#74243](https://github.com/NousResearch/hermes-agent/pull/74243), [#74242](https://github.com/NousResearch/hermes-agent/pull/74242)), this feature could improve robustness.

---

## Project Health Assessment

| Metric | Status | Notes |
| :--- | :--- | :--- |
| **Activity Level** | 🟢 High | 50 issues + 50 PRs updated in 24h, 20 issues closed. |
| **Bug Response Time** | 🟠 Moderate | P1 issues get attention, but P2/P3 `needs-repro` bottlenecks exist. |
| **Community Engagement** | 🟢 Excellent | Standardized issue templates, detailed bug reports, and high-quality community PRs. |
| **Maintainer Bandwidth** | 🟠 Limited | `needs-decision` on key architecture issues (#67442, #80424, #85125) indicates a decision backlog. |
| **Risk Areas** | 🔴 Windows Release, Session State | The P1 Windows update bug is a critical hotfix candidate. Session-state regressions repeat. |
| **Roadmap Vitality** | 🟢 Promising | i18n, A2A streaming, state hooks, and memory provider work indicate a feature-rich next release. |
| **Overall** | **🟡 Stable with noted exceptions** | The project is shipping and community-driven, but Windows desktop stability and a persistent session-state bug class need decisive fixes. |

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw Project Digest — 2026-08-15

## 1. Today's Overview

PicoClaw shows moderate activity with 8 PRs and 3 issues touched in the last 24 hours, though no new releases were published. The project is in a "stale sweep" phase — the majority of closed items carry `[stale]` tags triggered by the recently bumped `actions/stale` bot, suggesting maintainers are doing housekeeping rather than pushing major features. One critical bug fix PR (#3337) targeting an MCP-server connection hang is actively open and represents the most significant work in flight. Three older PRs (one from July 1st) remain open without merged status, indicating a possible backlog in review velocity. Overall, the project appears healthy but in a consolidation/maintenance period rather than active feature development.

## 2. Releases

No new releases were published in the last 24 hours. The most recent tagged version remains the nightly build referenced in issue #3269 (`git: 2cf030d2`).

## 3. Project Progress

Five PRs were closed/merged in the last 24 hours (all tagged `[stale]`, suggesting they were auto-closed by the bot rather than actively reviewed):

- **[#3303 — `build(deps): bump actions/stale from 10 to 11`](https://github.com/sipeed/picoclaw/pull/3303)** (dependabot): Infrastructure dependency bump; likely merged to enable the stale-bot sweep.
- **[#3283 — `fix(dingtalk): support picture/image message inbound`](https://github.com/sipeed/picoclaw/pull/3283)** (MrTreasure): DingTalk channel now supports receiving images with graceful degradation; added access-token caching.
- **[#3279 — `fix(seahorse): prevent tool-call format leakage into LLM summaries`](https://github.com/sipeed/picoclaw/pull/3279)** (MrTreasure): Fixed a bug where raw tool-call formatting leaked into user-visible messages via `partsToReadableContent`.
- **[#3271 — `chore(providers): update default model names to 2026-07 latest`](https://github.com/sipeed/picoclaw/pull/3271)** (LeaderOnePro): Model IDs refreshed across 9 providers (OpenAI `gpt-5.6*` family, Anthropic updates, etc.).
- **[#3270 — `feat: add DashScope TTS provider and WeChat audio file sending`](https://github.com/sipeed/picoclaw/pull/3270)** (MrTreasure): New Alibaba DashScope TTS provider plus WeChat audio send capability.

Notably, three substantive features (DingTalk images, DashScope TTS, model updates) appear to have been implemented over the past two weeks but only now closed — suggesting review came in a batch. However, the `[stale]` tag on all of them raises a question: **were these merged, or auto-closed without merging?** Their content suggests real features; maintainers should verify merge status.

## 4. Community Hot Topics

- **[#3269 — [BUG] MCP server connection failure hangs agent loop](https://github.com/sipeed/picoclaw/issues/3269)** — 5 comments, 1 👍
  The most active discussion: when an MCP server becomes unreachable, the agent loop errors out and the entire chat interface stops responding. Users effectively lose the assistant until restart. A fix PR (#3337, see below) is already open.

- **[#3308 — Code Review: concurrency hazards, goroutine leaks, memory/speed optimizations](https://github.com/sipeed/picoclaw/issues/3308)** — 2 comments
  A community code review of the SeaHorse, Channel Manager, and Hooks subsystems, citing goroutine leaks and concurrency hazards. Given the project's focus on extreme resource constraints (10MB RAM, sub-second boot on $10 hardware), this is technically substantive feedback but appears to have been closed as stale — worth reassessing for engineering value.

- **[#3307 — Session list/switch command for Telegram and other channels](https://github.com/sipeed/picoclaw/issues/3307)** — 2 comments
  Feature request highlighting a UX gap: session management exists in the Web UI but is absent from Telegram and other chat channels. No linked implementation PR exists.

**Underlying signal:** The community is actively using PicoClaw in multi-channel setups (Telegram, DingTalk, WeChat) and encountering real-world reliability and UX gaps. The MCP hang is the highest-priority pain point.

## 5. Bugs & Stability

| Severity | Issue | Status | Fix PR | Notes |
|----------|-------|--------|--------|-------|
| **High** | [#3269 — MCP failure hangs agent loop; chat stops replying entirely](https://github.com/sipeed/picoclaw/issues/3269) | Open, active (1 👍) | **Yes: [#3337](https://github.com/sipeed/picoclaw/pull/3337) (open, created yesterday)** | Complete agent stall requiring restart — critical reliability issue for production users |
| **Medium** | [#3279 — Tool-call format leaking into LLM summaries](https://github.com/sipeed/picoclaw/pull/3279) | PR closed | — | Fix was in the PR; `seahorse` summaries leaked raw tool-call syntax into user-visible messages |
| **Medium** | [#3319 — `exec` tool ignores per-run timeout; `background`/`pty` typed as strings](https://github.com/sipeed/picoclaw/pull/3319) | PR open | — | Schema mismatch and silently-ignored timeout could lead to runaway processes |

**Assessment:** The MCP hang (#3269) is the headline bug. PR #3337 proposes changing `AgentLoop.Run` to internally handle `ensureMCPInitialized` failures and continue the loop with degraded functionality instead of propagating the error to exit. This is the right approach; the PR should be prioritized for review and merge.

## 6. Feature Requests & Roadmap Signals

- **Session management for non-web channels** ([#3307](https://github.com/sipeed/picoclaw/issues/3307)): Users want `/sessions list`, `/switch`, `/delete` from Telegram and other channels. The Web UI implementation exists, so a backend SSE command layer would extend it.
- **Configurable default model fallback chain** ([#3200](https://github.com/sipeed/picoclaw/pull/3200)): A UI-driven default model + fallback priority chain, persisted via backend API. Open since July 1st — likely the next substantial UX feature if merged.
- **DashScope TTS + WeChat audio** ([#3270](https://github.com/sipeed/picoclaw/pull/3270)): Already implemented, adds multimodal voice capability to a major Chinese messaging channel.

**Prediction:** The fallback chain (#3200) and session management (#3307) are the most likely candidates for the next minor release, alongside the MCP hang fix. Multi-channel parity (DingTalk images, WeChat audio) suggests the maintainers are pushing channel-feature parity as a theme.

## 7. User Feedback Summary

- **Pain point (critical):** MCP server flakiness can completely brick the assistant (#3269). Users on unreliable networks or with self-hosted MCP endpoints will hit this daily. The one 👍 is understated for its severity.
- **Pain point (medium):** Session continuity is broken across channels — users on Telegram cannot return to a previous conversation, forcing context loss and re-explanation in every interaction (#3307).
- **Positive signal:** Community members are contributing code reviews on concurrency/memory (#3308) and directly proposing PRs (multiple by MrTreasure across DingTalk, WeChat, DashScope, and seahorse) — indicating a technical user base invested in the project's reliability.
- **Satisfaction:** The volume of channel-specific feature contributions (DingTalk images, WeChat audio, Telegram session features) suggests active real-world deployment and satisfaction with the core product; the complaints are about edge-case reliability, not fundamental capability.

## 8. Backlog Watch

- **[#3200 — Configurable default fallback chain (PR)](https://github.com/sipeed/picoclaw/pull/3200)**: Open since **July 1** (45+ days). A fully-scoped feature with backend persistence. Stalled without maintainer comments. High user value.
- **[#3319 — `exec` tool timeout/option fixes (PR)](https://github.com/sipeed/picoclaw/pull/3319)**: Open since August 7, addresses a real correctness bug in a core tool. Needs review.
- **[#3337 — MCP hang fix (PR)](https://github.com/sipeed/picoclaw/pull/3337)**: Only 1 day old but critical; should be fast-tracked.
- **[#3308 — Community concurrency code review (Issue)](https://github.com/sipeed/picoclaw/issues/3308)**: Auto-closed as stale. Given the project's resource-constrained target (10MB RAM, goroutine hygiene matters), this review deserves resurrection and a maintainer response.

---

**Overall health:** Stable and active, with a small but engaged contributor base. The primary risk is review velocity: 3 substantive PRs (including one 45-day-old feature) are waiting on maintainer attention, while the stale-bot may be prematurely closing technically valuable community input (#3308). The MCP hang fix should be merged this week to address the most severe reported bug.

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw Project Digest — 2026-08-15

## 1. Today's Overview

NanoClaw is in a **moderate-activity maintenance and stabilization phase**. The project saw **2 open issues** and **9 pull requests** updated in the last 24 hours, with **3 PRs closed/merged** (including two intentional "DO NOT MERGE" live-fire tests for the signature-approval pipeline). Core-team activity is focused on **CI/CD reliability** (supply-chain verification), while community contributors are submitting **targeted bug fixes** around setup scripting, cron scheduling, and Windows compatibility. No new releases were published today. Overall, the project shows **healthy contributor diversity** (5 distinct authors active) but is **not currently shipping net-new features**, suggesting a focus on hardening existing infrastructure.

## 2. Releases

**No new releases** were published in this 24-hour window. (No changelog, breaking changes, or migration notes to report.)

---

## 3. Project Progress — Merged/Closed PRs & Advanced Work

Three PRs were closed/merged today, all from core-team member **gavrielc**:

| PR | Title | Status |
|----|-------|--------|
| [#3244](https://github.com/nanocoai/nanoclaw/pull/3244) | `[core-team] DO NOT MERGE — live-fire the signature approver (take 2)` | **Closed unmerged** (intentional test) |
| [#3243](https://github.com/nanocoai/nanoclaw/pull/3243) | `verify-agent-image: arming auto-merge is not a verdict` | **Closed/merged** — fixes CI logic where `Enable auto-merge` failure (e.g., on draft PRs) was incorrectly treated as a verification verdict |
| [#3242](https://github.com/nanocoai/nanoclaw/pull/3242) | `[core-team] DO NOT MERGE — live-fire test of the signature approver` | **Closed unmerged** (intentional test) |

**Key takeaway:** PR #3243 is the substantive win — it decouples *auto-merge state* from *image-verification verdict* in CI, making the supply-chain check more honest and less flaky. The two closed-unmerged PRs confirm the approval chain now completes end-to-end (verify → approve → independent cosign verify → approving review) even on draft PRs, which was the goal.

**Open PRs advanced today (no merge yet):**
- [#3249](https://github.com/nanocoai/nanoclaw/pull/3249) — `fix(setup): handle an existing Node that is too old` (fixes #3248)
- [#3247](https://github.com/nanocoai/nanoclaw/pull/3247) — `fix(scheduling): retire a malformed cron string instead of re-erroring every sweep tick`
- [#3246](https://github.com/nanocoai/nanoclaw/pull/3246) — `fix(container-runtime): stop orphan cleanup from silently no-oping on Windows`

---

## 4. Community Hot Topics

*None of today's items have comments or reactions yet* — this is a low-social-engagement window. However, the **highest-signal items** by author activity and recency are:

1. **[#3248 — [bug] setup.sh "Node missing or too old" branch cannot handle too old](https://github.com/nanocoai/nanoclaw/issues/3248)**  
   Filed by `glifocat`, this is a **logic-gap bug** in setup: the version check routes failures to `install-node.sh`, but that script short-circuits if *any* node exists — so a user with Node v18 (too old) gets **neither a working setup nor a clear error**. The author immediately submitted **PR #3249** to fix it, showing engaged, solution-oriented community contribution.

2. **[#3245 — Prebuilt agent image: Bun binary requires AVX2 — SIGILL on CPUs without it](https://github.com/nanocoai/nanoclaw/issues/3245)**  
   Filed by `sergeykad` — affects **low-power/Atom-class CPUs** (Celeron J6413/N5105, Elkhart Lake/Tremont). The default hardened image ships a **non-baseline x64 Bun binary** that crashes with SIGILL on AVX2-less CPUs. **No fix PR exists yet.**

3. **Dial channel PRs (two, from `OmriBenShoham`)** — [#3050 (wizard/skills)](https://github.com/nanocoai/nanoclaw/pull/3050) and [#3041 (adapter)](https://github.com/nanocoai/nanoclaw/pull/3041). Both are **open for ~1 month** and have been updated recently but **not yet reviewed/merged** — this is the most likely "stuck waiting on maintainers" item.

---

## 5. Bugs & Stability

Ranked by severity:

**🟥 High — [#3245](https://github.com/nanocoai/nanoclaw/issues/3245): Bun binary requires AVX2 → SIGILL on older CPUs**  
- **Impact:** Default wizard-recommended setup crashes immediately on a real hardware class (Atom/Tremont). No workaround documented, **no fix PR open**.  
- **Signal:** Hardware-compat issue; may need an `x64-baseline` build variant or a fallback image.

**🟧 Medium — [#3248](https://github.com/nanocoai/nanoclaw/issues/3248): setup.sh cannot handle "too-old" Node (only "missing")**  
- **Impact:** Silent misconfiguration; user thinks setup failed, no actionable message.  
- **Fix:** PR [#3249](https://github.com/nanocoai/nanoclaw/pull/3249) open — needs review/merge.

**🟨 Low-Medium — [#3247](https://github.com/nanocoai/nanoclaw/pull/3247): Malformed cron strings cause repeated error spam every sweep tick**  
- **Impact:** Log noise + wasted DB writes; potential infinite re-erroring. Fix PR open (`retire` bad rows).

**🟨 Low — [#3246](https://github.com/nanocoai/nanoclaw/pull/3246): Orphan cleanup silently no-ops on Windows**  
- **Impact:** Docker orphans accumulate; users on Windows see no effect and no error. Fix PR open (removes POSIX-only quoting).

---

## 6. Feature Requests & Roadmap Signals

1. **Dial channel integration (SMS + AI voice calls)** — [PR #3050](https://github.com/nanocoai/nanoclaw/pull/3050) and [PR #3041](https://github.com/nanocoai/nanoclaw/pull/3041). Both are mature, feature-complete PRs (channel adapter + wizard integration) that have been open **~1 month**. **If maintainers approve this week, Dial could land in the next minor release.** This is the strongest near-term feature signal.

2. **CI/CD supply-chain hardening (signature approver)** — While technically internal, #3243's merged fix advances the project's **verification/audit story**, which often precedes a public "verified builds" feature or certification.

3. **No new user-facing feature requests** were filed in the last 24h.

---

## 7. User Feedback Summary

- **Pain point — Onboarding on modest hardware:** [#3245](https://github.com/nanocoai/nanoclaw/issues/3245) reveals the default path **breaks for a real CPU class** — user expectation is "wizard recommends → it works," but instead they get a hard crash. This was reported by a user likely setting up on a home-server/NUC-type device.
- **Pain point — Setup error messages are misleading:** [#3248](https://github.com/nanocoai/nanoclaw/issues/3248) indicates users with an old Node are left confused (branch thinks "no node" when in fact "old node"). Reporter went beyond filing — **provided a fix PR**, indicating a power-user persona who wants to stay productive.
- **Positive signal:** No "this is broken and unusable" complaints; both issues are **specific, technical, well-articulated** — typical of a technically-sophisticated user base.
- **Satisfaction proxy:** The live-fire CI tests (#3242/#3244) were closed successfully, meaning *maintainer-side* confidence in the release pipeline is improving.

---

## 8. Backlog Watch

| Item | Age | Why it matters |
|------|-----|----------------|
| [PR #3050](https://github.com/nanocoai/nanoclaw/pull/3050) + [PR #3041](https://github.com/nanocoai/nanoclaw/pull/3041) — Dial channel | **~32 days** | Feature-complete, updated as recently as today, **zero maintainer review comments observed**. Risk of bit-rot and contributor burnout. **High-priority for maintainer attention.** |
| [PR #3230](https://github.com/nanocoai/nanoclaw/pull/3230) — `fix(skills): stop removal docs pointing at the retired data/env mirror` | **~3 days** | Docs-only fix, but touches user-facing removal instructions; low-risk, should be fast to merge. |
| **No long-unanswered issues** detected — the two new issues (#3248, #3245) were filed within 24h, so no stale issues are blocking. | — | Healthy signal: maintainers are keeping up with issue triage. |

---

### Overall Health Verdict
**Stable-to-positive.** Community is active, bug reports are high-quality, and contributors are pairing issues with fix PRs. Two actionable risks: (1) the **AVX2 SIGILL issue has no fix yet** and affects real hardware, and (2) the **Dial channel PRs risk stagnation** after a month without maintainer review. The CI supply-chain hardening (merged #3243) is a quiet but important reliability win.

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

# NullClaw Project Digest
**2026-08-15**

---

## 1. Today's Overview

NullClaw is in a low-activity maintenance window. Over the past 24 hours, zero issues were updated or opened, and no new releases were published. Activity was limited to a single pull request, which was merged, indicating ongoing incremental development rather than large-scale feature work. The repository appears to be in a stable state with no open defects reported, and the merged PR suggests a continued commitment to configuration flexibility for deployment scenarios.

---

## 2. Releases

No new releases were published in the last 24 hours. The most recent release remains unavailable in this reporting window, and as such there are no breaking changes or migration notes to relay.

---

## 3. Project Progress

**Merged/Closed PRs:**

- **[#986 — GEN-548: make SQLite memory database path configurable](https://github.com/nullclaw/nullclaw/pull/986)** — *merged, closed*
  - **Author:** gently-whitesnow
  - **Summary:** This change adds a `memory.database_path` setting for SQLite-backed primary memory engines. The existing default location (`<workspace>/memory.db`) is preserved when the setting is empty. Relative paths are resolved from the workspace, while absolute paths are supported for read-only workspace deployments. The setting is documented in the example configuration.
  - **Significance:** The merge brings operational flexibility to deployment environments where workspace paths are immutable. This is the first code merge in this digest window and signals progress on configurability of persistence layers.

---

## 4. Community Hot Topics

Currently, there are no active issues or pull requests generating discussion. The sole PR of the day (#986) received no comments or reactions during the reporting window. The repository exhibits low community engagement in this period, likely reflecting a quiet period rather than a lack of interest. There are no underlying community needs to analyze from discussion data today.

- [#986 (merged, no discussion)](https://github.com/nullclaw/nullclaw/pull/986)

---

## 5. Bugs & Stability

No new bugs, crashes, or regressions were reported in the last 24 hours. The repository shows zero open issues, indicating a clean bill of health in terms of reported defects. No fix PRs were necessary as the only PR merged was a feature enhancement rather than a bug remedy.

*Note: While zero reported issues is a positive signal, it may also reflect lower usage-volume or community reporting activity, which is typical for a project in a maintenance phase.*

---

## 6. Feature Requests & Roadmap Signals

The only feature signal in this window is the **configurable SQLite memory database path** (PR #986), driven by a use-case for read-only workspace deployments. While not a user *request* in the traditional sense (it was implemented as an internal ticket, GEN-548), it addresses a real deployment pain point.

**Prediction for next version:** Given the focus on configuration flexibility in this merge, future releases may expand on the theme of deployment adaptability — including but not limited to: custom storage backends, environment-variable-driven configuration overrides, or support for external/networked persistence layers. Watch for continued work on `memory.*` configuration options.

---

## 7. User Feedback Summary

With zero open issues, no comments on the merged PR, and no release activity, direct user feedback is unavailable in this window. The absence of complaints suggests no acute dissatisfaction. The merged PR itself is a response to a legitimate use case: deployments where the workspace is mounted read-only. This indicates that NullClaw users are actively running the project in production-like, restricted environments, and the maintainers are responsive to those operational needs.

**Indirect signal:** The successful merge of a configuration enhancement suggests maintainers are listening to deployment-related friction and prioritizing operational robustness over new experimental features.

---

## 8. Backlog Watch

There are no long-unanswered issues or pull requests requiring maintainer attention in this reporting window. The issues queue is completely empty, and the sole PR was promptly merged the day after creation. While this is a sign of a well-maintained repo, contributors or users waiting on bug fixes or enhancements should note that we found no pending items to flag. If any critical items exist in the broader backlog, they are not surfacing as open issues in this window.

---

**Overall Health Assessment:** *Stable, quiet, and maintenance-focused.* The project shows no signs of decay but is not in an active development sprint. The merged configuration feature is a solid increment and speaks to thoughtful engineering for varied deployment footprints.

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw Project Digest — 2026-08-15

## 1. Today's Overview

IronClaw shows high-velocity development with 25 issues and 48 PRs updated in the last 24 hours, and the v1.2.0 stable release is now officially out (RC3 promotion). The project is deep into v1.3.0 planning with significant architectural work around **structured automations**, **unbound/prepared-context turns**, and **pluggable memory via MCP**, plus a parallel effort on **DB write-pressure reduction**. The QA dogfooding epic continues to surface real bugs (Telegram 2FA, Slack UI states, extension leakage), which are being triaged and fixed quickly — 9 issues closed and 23 PRs merged/closed in the window. The team is also investing in doc-truth testing and CI coverage ratchets to prevent regressions and documentation drift.

## 2. Releases

**ironclaw-v1.2.0** (2026-08-13) — stable promotion of `1.2.0-rc.3`.

Key fixes validated in RC2/RC3:
- **Runtime `curl` installation** — container images now include `curl` so in-container HTTP healthchecks can execute (orchestrators probe workers with it).
- Thread-index projection repair (forward-ported via PR #7663).
- Windows filesystem/smoke reliability fixes.
- Clean Windows JSON output.

Migration notes: PR #7657 merged the release line back into main, carrying **state-preserving 1.0/1.1→1.2 startup migrations**, backend/domain contract coverage, and release artifact upgrade canaries. Existing users should upgrade through the standard path; migrations are forward-only and preserve state.

## 3. Project Progress

**Merged/Closed PRs (23 total):**

- **#7668** *(fix)*: Surface GitHub provider auth diagnostics through the full stack — WASM, extension-tool ABI, capability, runtime-gate, and durable gate-record paths.
- **#7652** *(perf)*: Production DB write workload measurement — canonical agent turn (10 tool calls) and idle process benchmarks; complements the `pg_stat_statements` harness from #7592.
- **#7665** *(fix)*: Origin-scoped hosted MCP OAuth support — admit MKT1's `/mcp` endpoint shape with RFC 9728 resource binding, persisted through DCR/token exchange/refresh.
- **#7658** *(fix)*: Telegram 2FA gate recognition on migrated DCs + login-code delivery messaging (QR scan defect).
- **#7666** *(fix)*: Extension-card truth batch — device-link installs now direct users to the Web UI link step; fixes the "Reconnect/Finish Setup" false state.
- **#7657** *(chore)*: 1.2.0 release line merged back into main with migrations.
- **#7655** *(ci)*: Re-pinned slack/telegram integration coverage floors to observed reality.
- **#7569**, **#7565**, **#7532**, **#7414**, **#7183**, **#7520**, **#6869**: Closed issues covering shared SearchField component, i18n coverage, structured execution specs, dogfooding epic, per-user LLM selection, frontend surface retirement, and DOCX corruption.

**Advanced but still open:**
- **#7634** *(open)*: Complete switchover to prepared-context "unbound turns" — every follow-up documented in #7562 ships, 71-clause conformance audit passed.
- **#7651** *(open)*: Deterministic no-result suppression for automations (`deliver` vs `suppress_when_nothing_to_report` contract).
- **#7650** *(open)*: Persist semantic execution outcomes — replaces hidden reconciler with exact-run terminal settlement events.
- **#7661** *(open)*: MCP-backed memory provider — bind memory systems by configuration (Mnesis Core as first consumer).

## 4. Community Hot Topics

**#6879 — Automation runs are hit-or-miss** (open, epic, 1 comment)
Central reliability epic: same stored prompt sometimes succeeds, sometimes produces nothing useful, especially on DeepSeek V4 Flash. Audit shows structural issue: trigger fires execute as plain interactive chat turns. This spawns the entire structured-automation work-stream (#7644–#7647, #7532, PRs #7650/#7651). **Signal:** Determined push toward determinism in scheduled execution — the community/team wants automations to be *reliable*, not probabilistic.

**#7664 — Pluggable memory over MCP** (open, enhancement)
Tracks wiring the `ironclaw_memory_mcp` provider crate so external memory systems bind by configuration. First consumer is Mnesis Core. PR #7661 is the draft implementation. **Signal:** Memory is becoming a first-class pluggable subsystem — expect third-party memory backends.

**#7624 — ACP harness executor (claude-code as loop)** (open, feature)
Only pluggable-loops work item to build now; the consolidated ladder (#7621–#7623) is deferred until v0 validates the slot. **Signal:** IronClaw is exploring alternative loop executors beyond the canonical Rust one — architecture is trending toward swappable run executors.

**#7183 — Per-user LLM model selection** (closed)
Admin-only model selection was a long-standing user pain point (raised at Champions check-in by marketing). Closed in this window. **Signal:** Multi-tenant flexibility is a recurring demand.

## 5. Bugs & Stability

Ranked by severity:

1. **#7662 — MP4 attachment fails with `invalid_value (attachments.mime_type)` in Telegram** *(open, P2)* — Uploading `.mp4` video fails despite correct MIME detection. Functional blocker for media workflows. No fix PR yet.
2. **#7659 — Extensions installed by other users visible on Registry page** *(open, P2)* — Extension state leaks between users; **tenant-isolation concern**, not just UI bug. No fix PR yet.
3. **#7660 — Slack shows "Reconnect"/"Finish Setup" despite active connection** *(open, P2)* — UI state mismatch; connection works but UI lies. Fix shipped in #7666.
4. **#7667 — Telegram phone-mode login code hint ignores `sentCode.type_`** *(open)* — Raw-TL send path: user received no code after `PHONE_MIGRATE_1` re-send. Fix in #7658/PR #7658 (closed).
5. **#7626 — Custom MCP requiring browser/email auth gets stuck** *(open)* — Auth flow hangs when MCP needs interactive verification (MKT1 case). No fix PR yet.
6. **#6869 — Generated DOCX files unreadable by Word** *(closed)* — Corruption bug resolved (closed in window).

**Stability efforts:** PR #7628 removes heartbeat journal churn (fewer DB writes), PR #7652 establishes write benchmarks, and #7592 builds the regression harness. Regression risk is actively managed via coverage ratchets (#7655) and doc-fact contract tests (#7378).

## 6. Feature Requests & Roadmap Signals

**Strong signals for v1.3.0:**
- **Structured automations** (#7532 closed, #7644–#7647 open): Spec with goals, criteria, capability allowlists, model pinning, preflight grants, and deterministic suppression — nearly every piece has an open PR.
- **Unbound turns** (#7562, #7634): Prepared-context turns with kernel binding-ref deletion — architectural shift to context management.
- **Pluggable memory** (#7664, #7661): MCP-backed memory provider.
- **Ask User cards** (#7653): OMP-inspired structured `ask` tool for WebUI with `LoopCompletionKind::AskUserReply`.
- **Slack-to-Console bridge** (#7656 closed): Deep links and run metadata.
- **Per-user LLM selection** (#7183 closed): Now available.

**Likely landing in v1.3.0:** Deterministic automations, unbound turns (phase 1), ACP harness v0 (experimental). Pluggable memory is plausible if #7661 merges cleanly.

## 7. User Feedback Summary

- **Frustration with reliability:** #6879 and #7647 reflect users' core complaint — scheduled automation is unpredictable. The "hit-or-miss" phrasing signals trust erosion; the team's structured-spec response is exactly right.
- **Tool-call ergonomics:** #7636 (`builtin.shell` description now says "command line, not one primitive per call") addresses model confusion — small but user-visible quality-of-life fix.
- **Auth flows are painful:** Telegram 2FA/migration (#7658, #7667), custom MCP browser/email verification (#7626), and Slack re-connect states (#7660) all represent friction points where integrations break the "it just works" promise.
- **DOCX corruption is fixed:** #6869 closed — users reported ChatGPT/Claude handle this trivially; good to see this resolved.
- **Design-system debt:** Multiple issues (#7637, #7638, #7639, #7569) show the team is proactively consolidating frontend patterns — less *user* feedback, more *developer* experience, but it improves consistency.

## 8. Backlog Watch

- **#7626 — Custom MCP auth gets stuck** (opened 2026-08-13, open, no comments): No fix PR yet. Blocking for MKT1-style paid-access MCPs. This is a **user-facing blocker** that should be prioritized.
- **#7662 — MP4 Telegram attachment failure** (opened 2026-08-14, open, no comments): P2 QA bug, no fix PR. Media sharing is core daily-driver functionality.
- **#7659 — Cross-user extension leakage** (opened 2026-08-14, open, no comments): Potential tenant-isolation bug — **security-adjacent**. Needs immediate triage.
- **#7379/#7378 — Doc-truth PRs** (opened 2026-08-07, open, 1 week old): docs-live branch deployment and doc-fact contract tests — important for the docs↔release skew problem, but no movement in 24h despite being part of a 4/5 PR train (looks like #7317's static gate).
- **#7255 — APDD governance kit evaluation** (opened 2026-08-05, open, 10 days): Docs-only PR proposing scoped integration of an external governance framework. Low urgency but shows process maturity interest.
- **#7456 — Durable storage profile-agnostic** (opened 2026-08-10, open): Large refactor with security envelope persistence — several days without merges may indicate review bottleneck.

---

**Project health assessment:** Strong. Release-1.2.0 shipped cleanly with disciplined RC validation, the team is executing on a well-scoped v1.3.0 roadmap, and QA is actively catching real bugs. The main risks are (a) tenant-isolation bugs like #7659, (b) auth-flow friction where third-party services are involved, and (c) the growing size of open structural PRs that will require careful sequencing to land cleanly.

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

# LobsterAI Project Digest — 2026-08-15

## 1. Today's Overview

LobsterAI is in a **high-velocity release cycle**, with 27 PRs touched in the last 24 hours (22 merged/closed vs. 5 open) and a fresh release shipped yesterday (v2026.8.14). The project shows strong contributor momentum: a major release merge (v2026.7.30, 67 commits, +24,736/-4,253 lines) landed into main, alongside a burst of UI/UX polish PRs in the cowork (multi-agent chat) and account modules. Activity is heavily concentrated on renderer/frontend work and OpenClaw integration fixes rather than core architecture changes. Only 2 issues were updated in the period—both open—and one is a user requesting a new "v4pro" model update. Overall, the project is **healthy and actively shipping**, though the backlog shows several stale PRs from March/April that have not been resolved or explicitly closed.

## 2. Releases

**LobsterAI 2026.8.14** (released 2026-08-14)

The release notes are truncated in the data, but the visible changes include:
- **feat(sidebar):** support check-in and banner carousel ([PR #2411](https://github.com/netease-youdao/LobsterAI/pull/2411))
- **feat(sidebar):** add multi-agent task activity filter ([PR #2418](https://github.com/netease-youdao/LobsterAI/pull/2418))
- The notes are cut off (`feat(sidebar): mov...`), so additional changes may be present.

**Notable:** The **2026.7.30 release branch** (67 commits ahead of main at merge time) was merged into main today via [PR #2498](https://github.com/netease-youdao/LobsterAI/pull/2498), introducing:
- **Team Edition account and quota flows** (likely a significant new commercial tier)
- **Refreshed Skills and Connectors experiences**

**Breaking changes / migration notes:** Not explicitly documented in the data. The font-size bump PR ([#2495](https://github.com/netease-youdao/LobsterAI/pull/2495)) includes a "one-time migration" for typography defaults, which may affect custom UI theming. No migration guide was referenced.

## 3. Project Progress

**22 PRs were merged/closed today.** Key advances:

| Area | Change | PR |
|------|--------|----|
| **Release management** | 2026.7.30 branch merged to main (Team Edition, Skills/Connectors refresh) | [#2498](https://github.com/netease-youdao/LobsterAI/pull/2498) |
| **OpenClaw/skills** | Fixed skill toggles being silently ineffective — key `skills.entries` by frontmatter `name` (main fix) | [#2491](https://github.com/netease-youdao/LobsterAI/pull/2491), duplicate [#2483](https://github.com/netease-youdao/LobsterAI/pull/2483) |
| **Cowork UX** | Keep turn process expanded until an answer exists (avoids false "failure" collapse after `sessions_yield`) | [#2499](https://github.com/netease-youdao/LobsterAI/pull/2499) |
| **Cowork UX** | Keep badge popovers within viewport | [#2496](https://github.com/netease-youdao/LobsterAI/pull/2496) |
| **Artifacts** | Browser annotation screenshots now render as numbered attachment cards in artifact panel | [#2490](https://github.com/netease-youdao/LobsterAI/pull/2490) |
| **UI** | Default font sizes bumped with one-time migration | [#2495](https://github.com/netease-youdao/LobsterAI/pull/2495) |
| **Account** | Credits icon restyled (stacked-points SVG, `currentColor` theming) and color aligned | [#2494](https://github.com/netease-youdao/LobsterAI/pull/2494), [#2492](https://github.com/netease-youdao/LobsterAI/pull/2492) |
| **i18n** | Improved cowork goal/steer copy wording | [#2497](https://github.com/netease-youdao/LobsterAI/pull/2497) |
| **Session export** | Fixed session export image and card toggle UI | [#2493](https://github.com/netease-youdao/LobsterAI/pull/2493) |
| **DX** | Dependabot updates for rimraf & vite (open) | [#2460](https://github.com/netease-youdao/LobsterAI/pull/2460), [#2465](https://github.com/netease-youdao/LobsterAI/pull/2465) |

## 4. Community Hot Topics

Only 2 issues were updated in the last 24h, which limits reactive signals, but the most notable items are:

- **[Issue #2489](https://github.com/netease-youdao/LobsterAI/issues/2489) — "快更新v4pro！"** (Update v4pro now!) — Created 2026-08-14, 1 comment. User is pressing for a new model (likely a specific LLM version) support. High urgency from user perspective; a clear roadmap signal.

- **[Issue #1154](https://github.com/netease-youdao/LobsterAI/issues/1154) — Vitest test coverage for `commandSafety` and `coworkMemoryJudge`** — Stale (created 2026-03-31) but still open. This is a **safety-critical gap**: no tests for dangerous-command detection or memory-quality scoring. The issue itself is the community signal — it has only 1 comment and 0 reactions, but the subject matter is high-stakes.

The most activie PR by **comment count** is **#2374** ([hide sidebar ad banner - permanent toggle](https://github.com/netease-youdao/LobsterAI/pull/2374)), still open since 2026-07-21. It directly answers user complaints about intrusive ads (referenced issue #2342). This is a community-driven feature request that predates the release branch work—possibly deferred due to the Team Edition launch.

## 5. Bugs & Stability

No new bug reports were filed in the last 24h (the only two issues updated are stale + feature request). However, several fixed bugs were merged today, ranked by severity:

| Severity | Bug | Fix PR |
|----------|-----|--------|
| **High** | OpenClaw skill toggle silently ineffective when directory/frontmatter names mismatch (users thought enable/disable worked; actually no-op) | [#2491](https://github.com/netease-youdao/LobsterAI/pull/2491) |
| **Medium** | Cowork turn that ends mid-wait (e.g. after `sessions_yield`) collapses into an empty duration line reading as failure | [#2499](https://github.com/netease-youdao/LobsterAI/pull/2499) |
| **Medium** | Badge popovers render outside viewport or behind later messages | [#2496](https://github.com/netease-youdao/LobsterAI/pull/2496) |
| **Low** | Session export image and card toggle UI broken | [#2493](https://github.com/netease-youdao/LobsterAI/pull/2493) |

No crashes or regressions were reported in the analyzed window.

## 6. Feature Requests & Roadmap Signals

- **New model support (v4pro)** — [Issue #2489](https://github.com/netease-youdao/LobsterAI/issues/2489): User demand for latest LLM (likely Claude/GPT-class). Given the project's release cadence, this is likely to land within 1–2 weeks.

- **Permanent ad-banner hiding** — [PR #2374](https://github.com/netease-youdao/LobsterAI/pull/2374): User-facing setting to permanently disable sidebar ads. The PR is ready (addresses #2342) but not merged in 3+ weeks — possibly **blocked by product decisions** regarding ad revenue vs. UX (the "check-in and banner carousel" feature in the latest release suggests active ad-system development).

- **Team Edition** (from merge of release/2026.7.30): Now in main; likely to be the headline feature of the next minor release, with account/quota UI already polished.

- **Backlog signals from stale PRs**: Ctrl+F in-session search ([\#1155](https://github.com/netease-youdao/LobsterAI/pull/1155)), "mark as unread" for sessions ([\#1228](https://github.com/netease-youdao/LobsterAI/pull/1228)), AgentCreateModal Escape-key close/reset ([\#1231](https://github.com/netease-youdao/LobsterAI/pull/1231)) — all merged/closed recently despite being stale-labeled, suggesting old PRs are being **swept and committed** while the team focuses on release readiness.

## 7. User Feedback Summary

Few direct complaints were logged in the last 24 hours, but the data reveals consistent themes:

- **Ad fatigue:** The release added check-in/banner carousel ([\#2411](https://github.com/netease-youdao/LobsterAI/pull/2411)) at the same time users request an off-switch ([\#2374](https://github.com/netease-youdao/LobsterAI/pull/2374)). This tension suggests **monetization pressure is colliding with desktop-app UX expectations**.

- **Model freshness anxiety:** "快更新v4pro！" ([#2489](https://github.com/netease-youdao/LobsterAI/issues/2489)) is the second request of this style; users treat the app as **front-end for frontier models** and expect rapid adaptation.

- **Silent configuration failures:** The skill-toggle bug (directory vs. frontmatter name mismatch) frustrated users who believed settings worked when they were no-ops. The duplicate PRs ([#2483](https://github.com/netease-youdao/LobsterAI/pull/2483) & [#2491](https://github.com/netease-youdao/LobsterAI/pull/2491)) suggest two contributors independently found and fixed this—likely a hot pain point.

- **Testing debt acknowledged internally:** The stale safety-module test issue ([#1154](https://github.com/netease-youdao/LobsterAI/issues/1154)) has not been acted on in ~5 months, signaling that **safety module confidence is likely lower than ideal** for production AI-agent workloads, even as new features (Team Edition) ship.

## 8. Backlog Watch

| Item | Age | Type | Concern |
|------|-----|------|---------|
| [**Issue #1154**](https://github.com/netease-youdao/LobsterAI/issues/1154) — Vitest tests for `commandSafety`/`coworkMemoryJudge` | 4.5 months, stale | Issue (safety) | No maintainer response; unguarded dangerous-command detection is a **latent risk** for enterprise adoption |
| [**PR #1153**](https://github.com/netease-youdao/LobsterAI/pull/1153) — Fix Gemini `/v1` baseURL join bug (extra `/` missing) | 4.5 months, stale | PR (bug fix) | Google Gemini endpoint currently produces **malformed URLs** (`...googleapis.comv1beta/...`) for some user configurations; fix unattended |
| [**PR #1155**](https://github.com/netease-youdao/LobsterAI/pull/1155) — In-session Ctrl+F search | 4.5 months, stale | PR (feature) | Conflicting with global search; needs design decision |
| [**PR #2465**](https://github.com/netease-youdao/LobsterAI/pull/2465) — vite 5→8 major bump | 5 days | PR (deps) | Major-version upgrade needs careful review; not yet merged |
| [**PR #2374**](https://github.com/netease-youdao/LobsterAI/pull/2374) — Permanent ad-banner hide | 25 days | PR (feature) | Community-requested; product decision likely blocking |

**Maintainer attention needed:** The two stale PRs from March (Gemini URL bug, Ctrl+F search) deserve explicit closure or fast-tracking — their "stale" label masks the fact that #1153 is a **correctness bug** in a supported provider path.

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

Based on the provided GitHub data for Moltis (moltis-org/moltis), here is the project digest for **2026-08-15**.

---

# Moltis Project Digest — August 15, 2026

## 1. Today's Overview
The project is currently in a low-activity phase, with **zero issues** updated in the last 24 hours and no new releases cut. The primary focus is a **single, highly substantive open Pull Request (#1190)** that aims to introduce a robust layer of durable external connectors (calendar, email, and channel history). While the merge rate appears stalled this week, the scope of the pending PR suggests significant internal development or review is underway. Overall, the project health is stable, but the pipeline indicates a bottleneck at the review/merge stage rather than a lack of feature development.

## 2. Releases
**None.** No new versions or tags were released within the last 24 hours (or the immediate reporting window). There are no changelogs, breaking changes, or migration notes to report.

## 3. Project Progress
- **No Merged/Closed PRs** were recorded in the last 24 hours.
- **Active Development:** The sole activity is PR **#1190** (Open), which proposes a major architectural upgrade. While not merged, it represents the primary vector for advancing the project. The PR adds provider-neutral connector persistence, atomic snapshots, and bounded local full-text search. This signals progress toward making Moltis a more resilient offline-first assistant with long-term memory capabilities.

## 4. Community Hot Topics
- **[PR #1190] Add durable calendar, channel, and email connectors** (Open)
  - *Author:* penso | *Last Updated:* 2026-08-14
  - **Analysis:** Despite having only **0 comments** and **0 reactions** listed, this is the single most active thread in the repository. The lack of public comments suggests the discussion is happening internally or the PR is awaiting maintainer review. The underlying need here is clear: users require **reliable, long-term storage** for third-party data (CalDAV, Gmail, Slack/Discord history) without duplicating credentials or violating provider trust boundaries. This reflects a demand for Moltis to function as a standalone archive rather than just a real-time assistant.

## 5. Bugs & Stability
**No new bugs, crashes, or regressions** were reported in the last 24 hours. The repository shows **0 open/active issues** and **0 closed issues** in this window. Consequently, there is no severity ranking to provide, and no fix PRs are pending in this category. The absence of bug reports is a positive indicator for baseline stability, though it is likely correlated with the general lack of recent user activity.

## 6. Feature Requests & Roadmap Signals
While there are no explicit user-submitted feature requests today, the content of **PR #1190** serves as a strong **roadmap signal** for the project’s direction. The PR specifically targets:
- **Provider-scoped trust** and read-only access.
- **Scheduling and projections** for calendar data.
- **Bounded local full-text search** for email history.

**Prediction:** The next minor version of Moltis will likely center on **"Bring Your Own Data" (BYOD)** capabilities, allowing users to connect existing accounts (Gmail, CalDAV) to the assistant without requiring them to migrate into a proprietary cloud. Expect this PR to be the v0.x or v1.x headline feature once merged.

## 7. User Feedback Summary
Due to the absence of issues and comments on the PR, there is **no qualitative user feedback** to analyze in this reporting window. The silence on public channels could indicate:
- Users are satisfied with the current build and have no critical pain points to report.
- Or, the community is waiting on the features proposed in #1190 before providing deeper feedback.

The lack of dissatisfaction is positive, but the lack of positive reinforcement makes it difficult to gauge sentiment definitively.

## 8. Backlog Watch
- **[PR #1190] (Open since 2026-08-11)** — Currently 4 days old without public comments or a merge. Given the size and complexity of this PR (connectors, persistence, search), it requires urgent maintainer attention to either:
  - Provide approval and merge it to unblock the roadmap, or
  - Request changes to prevent the branch from going stale.

There are **no other** long-unanswered issues or PRs in the backlog, indicating that the maintainers have handled previous requests efficiently. The entire backlog watch rests on this single PR.

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

# CoPaw Project Digest - 2026-08-15

## 1. Today's Overview

CoPaw is exhibiting **high community engagement** with 50 issues and 41 PRs updated in the last 24 hours, though the majority of issues (38) were closed, indicating rapid triage. The project is **mid-feature-cycle**, with no new releases today but a significant influx of new feature PRs (skill system lifecycle, computer use window surfaces, media download controls, subagent grouping) submitted by both first-time contributors and regulars. The activity mix—a large backlog of closed items from previous weeks alongside fresh PRs—suggests the maintainers are **processing accumulated community feedback while actively advancing the v2.x roadmap**. The high open-PR count (26) relative to closures (15) indicates a **build-up of contributions awaiting review**, particularly with several PRs flagged as "[Under Review]."

## 2. Releases

No new releases were published on 2026-08-14. The most recent versions referenced in community discussions are **QwenPaw 2.1.0** (current beta) and **2.0.x** (stable line). Users are reporting issues in 2.1.0, suggesting it is actively being tested while 2.0.x still receives support.

## 3. Project Progress

Today saw **15 merged/closed PRs**, advancing several key areas:

**Skill System (New Feature):**
- [#7029](https://github.com/agentscope-ai/QwenPaw/pull/7029) & [#7031](https://github.com/agentscope-ai/QwenPaw/pull/7031): Dynamic skill loading/unloading with `AutoUnloadHook` (every 5 turns). This directly addresses the community's long-standing request for runtime skill management. Note: #7031 is the English duplicate of #7029; #7033 is the updated/re-opened version.

**Channel Infrastructure:**
- [#6943](https://github.com/agentscope-ai/QwenPaw/pull/6943): Restored plugin channel `get_configurator()` support for interactive channel configuration.
- [#6715](https://github.com/agentscope-ai/QwenPaw/pull/6715): OneBot inbound media (image/audio/video/file) localization before agent processing.

**Bug Fixes:**
- [#6969](https://github.com/agentscope-ai/QwenPaw/pull/6969): Fix for duplicate tool result writing when MCP returns both `content` and `structuredContent` (fixes #6958).
- [#7024](https://github.com/agentscope-ai/QwenPaw/pull/7024): DashScope audio formatting fix with fallback retry.
- [#6908](https://github.com/agentscope-ai/QwenPaw/pull/6908): Dependencies bumped to agentscope 2.0.6.

**Docs:**
- [#2105](https://github.com/agentscope-ai/QwenPaw/pull/2105): Whisper installation documentation.
- [#6997](https://github.com/agentscope-ai/QwenPaw/pull/6997): Long-term memory guides rewritten and expanded agent memory prompt.

## 4. Community Hot Topics

1. **[#7011](https://github.com/agentscope-ai/QwenPaw/issues/7011)** (OPEN, 5 comments): Console stop request can cancel an active Feishu session under multiple UI sessions. The updated findings provide direct evidence of cross-session identity pollution. This is a **serious reliability issue** affecting multi-channel users.

2. **[#7010](https://github.com/agentscope-ai/QwenPaw/issues/7010)** (CLOSED, 6 comments): QwenPaw lacks true daemon/background mode; SSH-launched commands hang. **High demand** from server-side users who want non-blocking startup.

3. **[#6405](https://github.com/agentscope-ai/QwenPaw/issues/6405)** (CLOSED, 6 comments): After upgrading to 2.0, MCP tools always report "Tool not found" even though names follow `[mcp-key]__[tool_name]` format. Docker version 2.0.0post3. This points to **MCP adapter regression** in the 2.0 line.

4. **[#7025](https://github.com/agentscope-ai/QwenPaw/issues/7025)** (OPEN, 4 comments): QwenPaw Creator plugin conflicts and disables all other plugins when installed. A **plugin isolation problem** that undermines the plugin ecosystem.

5. **[#2303](https://github.com/agentscope-ai/QwenPaw/issues/2303)** (CLOSED, 6 comments): MiniMax provider fails `check_connection()` with 404 on unsupported `/models` endpoint. This is an **Anthropic-compatible provider compatibility issue** that should have been caught earlier.

6. **[#2846](https://github.com/agentscope-ai/QwenPaw/issues/2846)** (CLOSED, 6 comments): Desktop auto-update feature + fix Windows taskbar icon showing Python instead of CoPaw. **High annoyance factor** for Windows desktop users.

7. **[#3045](https://github.com/agentscope-ai/QwenPaw/issues/3045)** (CLOSED, 8 comments): [Bug]: 自动获取模型为什么不可用 - Auto model discovery unavailable in v1.0.1 Windows. This is a **recurring provider discovery issue**.

## 5. Bugs & Stability

**High Severity (reported today, still open):**

| Severity | Issue | Description | Fix PR? |
|---|---|---|---|
| **Critical** | [#7011](https://github.com/agentscope-ai/QwenPaw/issues/7011) | Console stop cancels active Feishu session (cross-UI session identity bug) in 2.1.0. **Active production sessions can be terminated by mistake.** | None yet |
| **High** | [#7025](https://github.com/agentscope-ai/QwenPaw/issues/7025) | Creator plugin disables all other plugins. **Entire plugin ecosystem fails.** | None yet |
| **High** | [#7016](https://github.com/agentscope-ai/QwenPaw/issues/7016) | Tool calls return 404 ("Tool call not found") in streaming sessions on `/api/tool-calls/...` endpoint. **Streaming tool use broken in 2.1.0.** | None yet |
| **Medium** | [#6958](https://github.com/agentscope-ai/QwenPaw/issues/6958) | FastMCP tool results written twice (duplicate data in tool result files) when truncation threshold exceeded in 2.1.0b4. | **Yes—[#6969](https://github.com/agentscope-ai/QwenPaw/pull/6969)** (open) |

**Root-Cause Analysis:**
- Issue #7016 (404 on tool calls) is particularly concerning—it indicates a **matching/state issue in the tool-call registry during streaming**, likely related to recent session model changes ([#6302](https://github.com/agentscope-ai/QwenPaw/pull/6302)).
- The duplicated tool results (#6958) stem from the adapter writing both unstructured `content` and formatted `structuredContent` fields. The fix in #6969 correctly avoids duplication.

**Fixed/Closed bugs today:**
- #6951: Scroll compression hides pre-compression chat history; only eviction index visible. Fixed.
- #7040: Numerous typo issues ("Stopp Running")—closed as invalid but highlights **QA/typo pass needed**.
- #6972: Chrome extension WebSocket disconnects after `tab.create`—closed.
- #6612: QwenPaw 2.0.1+agentscope 2.0.4.post1 compatibility crash—closed.

## 6. Feature Requests & Roadmap Signals

**Strong signals for next version (2.2.0 likely):**

1. **Dynamic Skill Lifecycle** (from [#7033](https://github.com/agentscope-ai/QwenPaw/pull/7033)): load/unload skills at runtime with auto-unload. This is a direct answer to [#2418](https://github.com/agentscope-ai/QwenPaw/issues/2418) ("skills-hub management page") and was just merged (via #7029). **Landing in 2.2.**

2. **Per-Session Model Overrides** ([#5992](https://github.com/agentscope-ai/QwenPaw/pull/5992), open, under review): opt-in ability to use different LLMs per conversation. This addresses core "provider-agnostic switching" requests (#2314). Likely in **2.2**.

3. **Unified Provider Discovery/Model Routing** ([#6302](https://github.com/agentscope-ai/QwenPaw/pull/6302), open): catalog-driven provider model system with runtime discovery and capability-aware routing. This is the **architectural fix** for the miniMax/Azure Responses API issues. Could be **2.2+**.

4. **Computer Use Window Surfaces** ([#7037](https://github.com/agentscope-ai/QwenPaw/pull/7037), open): observe related window surfaces (native menus, dialogs) in Computer Use. Direct answer to [#5551](https://github.com/agentscope-ai/QwenPaw/issues/5551) ("plan to support computer use?"). **2.2.**

5. **Desktop Auto-Update** ([#2846](https://github.com/agentscope-ai/QwenPaw/issues/2846), closed today—may be implemented): user demand is loud; expect this soon.

6. **Conversation Splitting** ([#4436](https://github.com/agentscope-ai/QwenPaw/issues/4436), open): ability to move selected messages to a new session to avoid token waste. **Backlog.**

7. **GGUF Local Model Runner** ([#6433](https://github.com/agentscope-ai/QwenPaw/issues/6433), closed today): bundled llama.cpp runtime with model browser—a bold feature that would make QwenPaw standalone.

## 7. User Feedback Summary

**Pain Points:**
1. **Windows desktop friction**: No auto-update; manual uninstall/reinstall each time (#2846, #3464). This is the **most-repeated complaint** among Windows users.
2. **MCP tool reliability**: After 2.0 upgrade, tools "not found" in Docker (#6405); tool calls 404 in streaming (#7016); duplicate results (#6958). **The MCP experience is regressing**, not improving.
3. **Provider compatibility**: OpenAI Responses API (Azure gateway) fails 400 (#3002); MiniMax check_connection broken (#2303); and even after closed, users still want Responses support (#944, #2737). This is a **long-standing architectural gap**.
4. **Desktop polish**: Python icon in taskbar, browser launch failures (Edge exit code 21), nvidia-smi hang at startup (#6197), cmd window flashing on Windows (#4832). Small but **visible quality-of-life problems**.
5. **State-management issues**: Scroll compression hides history (#6951); session identity cross-contamination between UI and Feishu (#7011).

**Positive Signals:**
- The typo issue (#7040) being closed as invalid suggests users care about **product polish**—a sign they value the craft.
- The demand for daemon mode (#7010) indicates **production/server usage** is growing.
- Requests for "like WeChat" single-message deletion (#4001) and "like lobster (龙虾)" timer-task delivery control (#2554) show users are **mixing personal and enterprise workflows**.

**Satisfaction Indicators:**
- Low 👍 counts across top issues (mostly 0) suggests users are **driven by problems, not praise**.
- The range of plugins, channels (Feishu, DingTalk, QQ, Discord, iMessage), and desktop/mobile clients being discussed indicates **broad platform adoption**.

## 8. Backlog Watch

These items need maintainer attention:

| Item | Age | Why it matters |
|---|---|---|
| **[#4001](https://github.com/agentscope-ai/QwenPaw/issues/4001)** (OPEN, 4 comments, May 2) | 3.5 months | Delete single messages in conversation UI. High-value UX feature, no PR yet. |
| **[#4436](https://github.com/agentscope-ai/QwenPaw/issues/4436)** (OPEN, 2 comments, May 16) | 3 months | Conversation splitting to avoid token waste. Community wants it; no traction. |
| **[#944](https://github.com/agentscope-ai/QwenPaw/issues/944)** (closed, Mar 8) | 5 months | Responses-API-only provider support. Even though closed, it was **never implemented**; users still asking (#3002). **Sign of unresolved architectural debt.** |
| **[#2314](https://github.com/agentscope-ai/QwenPaw/issues/2314)** (closed, Mar 26) | 5 months | Provider-agnostic conversation history. Closed but no implementation merged—**risk of user-facing regression**. |
| **[#5551](https://github.com/agentscope-ai/QwenPaw/issues/5551)** (closed, Jun 26) | 7 weeks | Computer use support. PR #7037 now addresses it, but **needs review**. |
| **[#5992](https://github.com/agentscope-ai/QwenPaw/pull/5992)** (OPEN, Under Review, Jul 12) | 1 month | Per-session model overrides. Stalled in review—**high-demand feature, low-review velocity**. |
| **[#6302](https://github.com/agentscope-ai/QwenPaw/pull/6302)** (OPEN, Jul 21) | 3.5 weeks | Unified provider discovery & routing. Large PR, **needs architectural review**; but it's the **fix for the entire class of provider issues**. |

**Maintainer risk:** The list above shows several PRs that are "[Under Review]" for extended periods. With 26 open PRs and a large issue backlog (12 active open issues), the **review bottleneck is the critical path** to community satisfaction. The 38 closed issues in 24h is good, but much of that is likely bulk-closing stale items rather than deep triage.

---

*Report generated: 2026-08-15 from CoPaw data (github.com/agentscope-ai/CoPaw).*

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# ZeroClaw Project Digest — 2026-08-15

## Today's Overview

ZeroClaw shows a high-velocity stabilization phase with 33 issues and 50 PRs updated in the last 24 hours. The project is deep in its v0.8.5 finite weekly stabilization line (tracker #9459), with maintenance heavily focused on hardening security posture, config reliability, and cross-platform test stability. Activity is unusually concentrated on RFC-driven architecture work — at least four high-risk RFCs (chat completions profile, goal mode, runtime-owned sessions, unified attachments) are converging toward ratification, while a substantial bug backlog (Windows test failures, Solana wallet address redaction, token accounting) is being actively fixed. There were no new releases this period, and no merged PRs in the last day, suggesting a "polish and review" cadence rather than a pushing cadence.

## Releases

No new releases were published in this digest window. The project continues to operate on its v0.8.5 weekly stabilization line (tracker [#9459](https://github.com/zeroclaw-labs/zeroclaw/issues/9459)), with weekly cuts shipping ready work without waiting for every milestone item.

## Project Progress

No PRs were merged or closed in the last 24 hours; the 50 updated PRs are all currently in-review or awaiting author action. That said, several long-running initiatives are visibly converging:

- **Security hardening is the dominant theme.** [#9996](https://github.com/zeroclaw-labs/zeroclaw/pull/9996) makes action-budget accounting atomic, [#9839](https://github.com/zeroclaw-labs/zeroclaw/pull/9839) blocks direct spellings of irreversible destructive commands, and [#9580](https://github.com/zeroclaw-labs/zeroclaw/pull/9580) hardens HTTP egress on the shared network guard. These sit alongside accepted RFCs for pluggable inbound authentication (#7141), a runtime-owned security decision pipeline (#7142), and a universal ingress policy (#6971) — all of which have been recently revised and are converging on maintainer ratification.
- **Config correctness and reliability.** [#9707](https://github.com/zeroclaw-labs/zeroclaw/pull/9707) fixes bare `vision_model_provider` migration to dotted alias refs, [#9281](https://github.com/zeroclaw-labs/zeroclaw/pull/9281) rolls back auto-created map aliases when `config set` fails, and [#10002](https://github.com/zeroclaw-labs/zeroclaw/pull/10002) fixes camelCase segment validation in `google_workspace` tool config.
- **Provider correctness.** [#9999](https://github.com/zeroclaw-labs/zeroclaw/pull/9999) classifies output-limited terminal responses for OpenAI-compatible providers — a direct follow-up to the S1 bug #9421 where incomplete terminal responses could be reported as successful. [#9420](https://github.com/zeroclaw-labs/zeroclaw/pull/9420) adds support for stored Anthropic OAuth profiles.
- **CI modernization.** [#9962](https://github.com/zeroclaw-labs/zeroclaw/pull/9962) routes rust-cache through a provider-aware composite action, and [#9985](https://github.com/zeroclaw-labs/zeroclaw/pull/9985) extends Blacksmith runners to msrv, parallel-runtime-test, and installer-drift jobs. These are likely part of the response to the ETXTBSY cron test race (#9965).

## Community Hot Topics

The most active threads reveal the community's deepest structural concerns:

1. **RFC: Goal mode v1 — bounded foreground Matrix work** ([#8303](https://github.com/zeroclaw-labs/zeroclaw/issues/8303), 22 comments) — The most-commented issue. @vrurg is proposing a durable way to pursue bounded user objectives across multiple agent turns, explicitly de-scoping restart handoff, Web, and async child work from the first delivery. The need: users want multi-turn goal pursuit without full autonomous-agent complexity.

2. **RFC: Per-execution confirmation tier for high-risk shell commands** ([#7155](https://github.com/zeroclaw-labs/zeroclaw/issues/7155), 20 comments) — @NiuBlibing has revised this three times, narrowing the normative scope to a reconciled shell-policy contract (allow/ask/deny). This is clearly a high-priority request: users want Claude Code-style command confirmation patterns, and the maintainer has pushed back twice on scope.

3. **RFC: ZeroClaw Chat Completions profile** ([#8603](https://github.com/zeroclaw-labs/zeroclaw/issues/8603), 19 comments) — The community wants OpenAI Chat Completions protocol compatibility to unlock Open WebUI, LobeChat, Continue.dev, Aider, LangChain, and the OpenAI SDK as clients. This is a major ecosystem-integration signal.

4. **RFC: Pluggable inbound authentication and canonical principals** ([#7141](https://github.com/zeroclaw-labs/zeroclaw/issues/7141), 16 comments) — Rev 8 of the identity & access milestone proposal. OIDC and pluggable-provider support has been in discussion since June 3.

5. **Windows test failures** ([#7462](https://github.com/zeroclaw-labs/zeroclaw/issues/7462), 15 comments) — 74 failing tests on Windows 11 (Chinese locale, cp936). CI only runs Linux, so this is invisible until users hit it. High frustration potential.

6. **RFC: Runtime-owned conversation sessions and transport surface adapters** ([#9487](https://github.com/zeroclaw-labs/zeroclaw/issues/9487), 14 comments) and **Unified attachment architecture** ([#9488](https://github.com/zeroclaw-labs/zeroclaw/issues/9488), 14 comments) — both by @NiuBlibing, both marked `needs-maintainer-review`, this is a coherent architecture push for web chat and channel parity.

## Bugs & Stability

No new crash-level regressions were reported today, but several significant bugs are in flight:

- **[S1, in-progress] Incomplete terminal responses reported as successful** ([#9421](https://github.com/zeroclaw-labs/zeroclaw/issues/9421)) — A provider can end a turn without a trustworthy final answer, yet runtime reports success. Fix PR [#9999](https://github.com/zeroclaw-labs/zeroclaw/pull/9999) classifies OpenAI-compatible `finish_reason: "length"` and rejects incomplete non-streaming text — PR is open and recent.
- **[S2] Windows test failures** ([#7462](https://github.com/zeroclaw-labs/zeroclaw/issues/7462)) — 74 failures due to Unix-only test commands, path semantics, and console encoding (cp936). CI gap: Test job only runs on Linux. PR [#10001](https://github.com/zeroclaw-labs/zeroclaw/pull/10001) fixes non-UTF-8 browser path fixtures to be Linux-gated, a partial step.
- **[S2] High-entropy detector redacts Solana wallet addresses** ([#9486](https://github.com/zeroclaw-labs/zeroclaw/issues/9486)) — Telegram channel messages replace every Solana address with `[REDACTED_HIGH_ENTROPY_TOKEN]`, and `high_entropy_tokens=false` does not stop it on the channel path. This breaks a legitimate use case (Solana MCP server users cannot state their wallet). No fix PR seen yet.
- **[S2] Duplicate webhook ports not rejected in Quickstart** ([#9759](https://github.com/zeroclaw-labs/zeroclaw/issues/9759)) — staging multiple fresh channel entries with the same port slips through; accepted but no fix PR yet.
- **[Medium] cron custom-shell test hits ETXTBSY** ([#9965](https://github.com/zeroclaw-labs/zeroclaw/issues/9965)) — A flaky test under the parallel runtime gate is red-lighting unrelated PRs; tracker exists but no fix PR yet.
- **[Medium] Qdrant silently routed to MarkdownMemory fallback** ([#9919](https://github.com/zeroclaw-labs/zeroclaw/issues/9919)) — builder-only factory silently selects the wrong persistence layer when storage config is unavailable. PR exists (per issue labels) but is not in the top-20 list.
- **[S3] Fallback model without vision misreports error cause** ([#9983](https://github.com/zeroclaw-labs/zeroclaw/issues/9983)) — Error messaging does not explain that the failure is due to the fallback lacking vision support.

## Feature Requests & Roadmap Signals

Clear signals for what lands next:

- **Telegram UX is underserved.** New feature requests: provider-grouped paginated `/model` picker ([#9895](https://github.com/zeroclaw-labs/zeroclaw/issues/9895)), tool-call progress during partial streaming ([#6663](https://github.com/zeroclaw-labs/zeroclaw/issues/6663), closed — likely shipped), and Discord role-based authorization ([#9970](https://github.com/zeroclaw-labs/zeroclaw/issues/9970)). A PR for the Telegram model picker is already open ([#9997](https://github.com/zeroclaw-labs/zeroclaw/pull/9997)).
- **Agent evaluation is a priority.** [#7065](https://github.com/zeroclaw-labs/zeroclaw/issues/7065) (zeroclaw eval harness, replay + live modes) and its tracker [#9967](https://github.com/zeroclaw-labs/zeroclaw/issues/9967) both show activity — the project wants a first-class way to evaluate agent behavior and model/prompt quality at scale.
- **Web research is coming.** PR [#9833](https://github.com/zeroclaw-labs/zeroclaw/pull/9833) adds a `web_research` delegate tool (bounded sub-agent loop: search → fetch → distill) and scopes raw `web_search` to it. This is a direct response to "the main agent does too many tool calls and burns tokens" — a very common user pain point.
- **Portable agent export/import** ([#9986](https://github.com/zeroclaw-labs/zeroclaw/pull/9986)) — `zeroclaw agents export <alias> --out <dir>` writes a manifest, config closure, and workspace tree. Useful for moving agents between installs.
- **Shell dialect in system prompt** ([#9788](https://github.com/zeroclaw-labs/zeroclaw/issues/9788)) — the model should know which shell language to write for, instead of guessing from the OS name. Small but high-leverage for tool-calling quality.
- **Localization enforcement** ([#9972](https://github.com/zeroclaw-labs/zeroclaw/issues/9972)) — tracker to eliminate user-facing literal output outside Fluent/ZeroCode boundaries.

Prediction: the **web_research delegate** (PR #9833) and the **Telegram paginated model picker** (PR #9997) are most likely to land in the next v0.8.5 weekly cut. The **Chat Completions profile RFC** (#8603) has 19 comments and `needs-maintainer-review` — expect either ratification or a scope-narrowing revision in the coming days.

## User Feedback Summary

- **Power users want protocol interoperability.** The Chat Completions profile RFC (#8603) is the clearest signal: users want to plug ZeroClaw into the OpenAI ecosystem (Open WebUI, LobeChat, Continue.dev, Aider, LangChain). This is an "unlock our existing tooling" request, not a "give us new features" request.
- **Users run into Windows-specific pain** — #7462 (74 test failures) and #10001 (non-UTF-8 fixture paths) show that Windows is not a first-class platform in the test suite, and users with Chinese/Japanese/Korean locales hit the worst of it. These are S2 bugs (degraded behavior) but the silent CI gap means users discover them on their own.
- **High-entropy redaction is too aggressive** — #9486 shows a real production workflow broken: an agent with a Solana MCP server cannot state a wallet address in Telegram. This is a security-vs-usability training problem; the `high_entropy_tokens=false` escape hatch does not work on the channel path.
- **Users want bounded, reliable multi-turn execution** — RFC #8303 (goal mode) and the cron/heartbeat delivery-contract PR (#9842) both come from the same need: "the model should know what will happen to its output and how long it can work." The community is pushing for explicit, bounded foreground work rather than implicit long-running agents.
- **Tool-call accounting and output limit handling matter** — the S1 bug #9421 (incomplete terminal responses reported as success) and the fix PR #9999 (classify `finish_reason: "length"`) address a failure mode that breaks trust in the system. Users are clearly hitting token-limit truncation that is silently misreported.
- **A hosted memory vendor pitch (#9982) was closed as `wontfix`** in 1 day — the maintainers are not interested in third-party hosted memory layers; they are building their own stateful/persistent AI and treat memory infrastructure as core.

## Backlog Watch

Several long-running, high-comment-count RFCs sit in `needs-maintainer-review` or `status:accepted` without visible merge activity. These are the "big rocks" the project must resolve:

1. **RFC: ZeroClaw Chat Completions profile** ([#8603](https://github.com/zeroclaw-labs/zeroclaw/issues/8603)) — 19 comments, `needs-maintainer-review` since 2026-07-02. This unlocks significant ecosystem value and has direct competition implications (LobeChat, Open WebUI are default client choices for many self-hosters).
2. **RFC: Runtime-owned conversation sessions and transport surface adapters** ([#9487](https://github.com/zeroclaw-labs/zeroclaw/issues/9487)) and **Unified attachment architecture** ([#9488](https://github.com/zeroclaw-labs/zeroclaw/issues/9488)) — both `needs-maintainer-review` since 2026-07-28. This is a coherent architecture push but a large one; without maintainer review, it will stall.
3. **RFC: Security posture, credential boundaries, and universal ingress policy** ([#6971](https://github.com/zeroclaw-labs/zeroclaw/issues/6971)) — 11 comments, `needs-maintainer-review` since 2026-05-27. This is the umbrella security RFC; its sub-RFCs (#7141, #7142) have been revised more recently and show more life.
4. **RFC: Provenance, conversation binding, and reply contract for internally initiated agent turns** ([#6954](https://github.com/zeroclaw-labs/zeroclaw/issues/6954)) — 11 comments, `needs-maintainer-review` since 2026-05-26. Tied to cron/heartbeat work; the delivery-contract PR #9842 may be a step toward this.
5. **74 Windows test failures** ([#7462](https://github.com/zeroclaw-labs/zeroclaw/issues/7462)) — 15 comments, `status:accepted` since 2026-06-10, still no full fix. This is the longest-running visible quality debt.
6. **Maintainer decision queue tracker** ([#8692](https://github.com/zeroclaw-labs/zeroclaw/issues/8692)) — the project uses a tracker to manage the decision queue; the queue is visibly full (5+ RFCs awaiting decisions).

**Overall health assessment:** ZeroClaw is in a healthy but stormy stabilization phase. The RFC churn is unusually high (11 high-risk RFCs in flight), which signals a deliberate architecture push before v0.9.0 — but it also risks decision fatigue. The security-hardening PR wave is excellent and directly addresses the S1/S2 bug reports. The biggest near-term risks are: (a) the Windows test gap with no full fix, (b) 5+ RFCs waiting on maintainer decisions with `needs-maintainer-review` flags, and (c) the growing `needs-author-action` count on major PRs (at least 8 of the top-20 PRs are blocked on author revision). The project is not stalled — it is consolidating.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/kky-wollu/agents-radar).*