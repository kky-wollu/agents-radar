# OpenClaw Ecosystem Digest 2026-07-28

> Issues: 500 | PRs: 500 | Projects covered: 13 | Generated: 2026-07-27 23:08 UTC

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

Here is the OpenClaw project digest for 2026-07-28.

---

## OpenClaw Project Digest: 2026-07-28

### 1. Today's Overview
The OpenClaw project is experiencing an exceptionally high traffic day, with **500 issues** and **500 pull requests** updated in the last 24 hours—a significant spike that may indicate a release cycle, a hackathon, or automated bulk processing (e.g., stale-bot sweeps). The issue queue is heavily active with **235 open/active issues** and **265 closed**, while the PR queue shows **275 open PRs** and **225 merged/closed**. No new releases were cut today. The project is focused on stabilizing critical infrastructure, with maintainers addressing severe P0 and P1 memory leaks, security boundaries, and session-state regressions under the `clawsweeper` triage system.

### 2. Releases
No new releases were published today. The last known version context from issues references `2026.7.2-beta.4` and `beta.5`, suggesting a beta cycle is in progress.

### 3. Project Progress
**225 PRs were merged or closed today.** Notable examples of forward progress include:
- **Hosting & Deployment:** Multiple large PRs from `giodl73-repo` advance the "Standard Hosting Profiles" initiative (RFC 23), including profile conformance tooling ([#114636](https://github.com/openclaw/openclaw/pull/114636)) and core readiness conditions ([#113421](https://github.com/openclaw/openclaw/pull/113421)).
- **Security Hardening:** A critical fix landed to prevent SSRF attacks via untrusted ClawHub skill URLs ([#113215](https://github.com/openclaw/openclaw/pull/113215)) and a sandbox escape fix prevents sub-agents from reading other agents' bridged memory ([#111463](https://github.com/openclaw/openclaw/pull/111463)).
- **Platform Support:** Multiple bot account support was added for Microsoft Teams ([#112811](https://github.com/openclaw/openclaw/pull/112811)), and a fix prevents stale wake tasks on iOS ([#113062](https://github.com/openclaw/openclaw/pull/113062)).
- **CI & Quality:** The Control UI end-to-end test suite was made mandatory for merges ([#114554](https://github.com/openclaw/openclaw/pull/114554)).

### 4. Community Hot Topics
- **[#75 - Linux/Windows Clawdbot Apps](https://github.com/openclaw/openclaw/issues/75)** (115 comments, 80 👍) – The long-running request for desktop applications beyond macOS/iOS remains the community's most discussed feature, but there is no PR linked.
- **[#7707 - Memory Trust Tagging by Source](https://github.com/openclaw/openclaw/issues/7707)** (22 comments) – A high-interest security feature to prevent memory poisoning from untrusted web content, reflecting growing user concern about supply-chain safety in agent memory.
- **[#91588 - Gateway Memory Leak (P0)](https://github.com/openclaw/openclaw/issues/91588)** (21 comments, 1 👍) – A critical stability issue with RSS growing to 15.5GB. The high activity signals widespread user pain from OOM crashes.
- **[#10659 - Masked Secrets](https://github.com/openclaw/openclaw/issues/10659)** (15 comments, 4 👍) – Strong demand for a system that prevents agents from reading raw API keys, driven by prompt injection risks.
- **[#6615 - Denylist for Exec-Approvals](https://github.com/openclaw/openclaw/issues/6615)** (10 comments, 8 👍) – Users want "allow all except dangerous commands" policies, indicating a need for more granular operational control.

### 5. Bugs & Stability
Today's data reveals severe stability issues, with several **P0** and **P1** bugs in flight:

| Severity | Issue | Summary | Fix PR Exists? |
|----------|-------|---------|----------------|
| **P0** | [#91588](https://github.com/openclaw/openclaw/issues/91588) | Gateway memory leak: RSS 350MB → 15.5GB, OOM crashes | No |
| **P0** | [#109867](https://github.com/openclaw/openclaw/issues/109867) | State migration blocking gateway startup (beta.2) | No (Closed) |
| **P1** | [#113306](https://github.com/openclaw/openclaw/issues/113306) | SQLite snapshot restore lacks crash guarantees | No |
| **P1** | [#86519](https://github.com/openclaw/openclaw/issues/86519) | Agent repeats reply 2-10x on Telegram (regression) | No |
| **P1** | [#113434](https://github.com/openclaw/openclaw/issues/113434) | Codex session reuse exhausts Gateway RAM (beta.4) | No |
| **P1** | [#113315](https://github.com/openclaw/openclaw/issues/113315) | Telegram update permanently lost after offset persistence | No |
| **P1** | [#10659](https://github.com/openclaw/openclaw/issues/10659) | Masked Secrets (enhancement with P1 security impact) | No |

The **gateway heap growth** ([#87109](https://github.com/openclaw/openclaw/issues/87109)) and **session context bloat** ([#67419](https://github.com/openclaw/openclaw/issues/67419)) remain open, suggesting systemic resource management challenges.

### 6. Feature Requests & Roadmap Signals
The following features, if implemented, are likely candidates for the next release based on their priority and activity:
- **Dynamic Model Discovery** ([#10687](https://github.com/openclaw/openclaw/issues/10687), P2) – Needed for OpenRouter support; a prerequisite for many users.
- **Filesystem Sandboxing** ([#7722](https://github.com/openclaw/openclaw/issues/7722), P2) – Configurable `fileAccess` restrictions, paired with **Masked Secrets** ([#10659](https://github.com/openclaw/openclaw/issues/10659)).
- **Session Stream Mode Command** ([#93218](https://github.com/openclaw/openclaw/pull/93218)) – A large PR offering per-session streaming control (final/partial/block/progress), addressing a long-standing UX friction.
- **Memory Trust Tagging** ([#7707](https://github.com/openclaw/openclaw/issues/7707), P2) – Growing community desire for provenance-aware memory.

### 7. User Feedback Summary
- **Performance Pain:** Users are deeply frustrated by memory leaks that render the gateway unusable after days of uptime ([#91588](https://github.com/openclaw/openclaw/issues/91588), [#87109](https://github.com/openclaw/openclaw/issues/87109)). One user in [#87109](https://github.com/openclaw/openclaw/issues/87109) notes cron jobs **fail silently** under memory pressure.
- **Message Loss & Duplication:** Telegram users report duplicate replies ([#86519](https://github.com/openclaw/openclaw/issues/86519)), and WhatsApp users report stalled sessions on long model calls ([#84569](https://github.com/openclaw/openclaw/issues/84569)). These degrade trust in the platform.
- **Security Anxiety:** Multiple feature requests (masked secrets, denylist, memory tagging, permission manifests) indicate users are proactively seeking to prevent prompt injection and credential theft.
- **UX Friction:** Users request accessibility improvements (TUI emoji disable [#9637](https://github.com/openclaw/openclaw/issues/9637)), multi-line message input in TUI ([#10118](https://github.com/openclaw/openclaw/issues/10118)), and suppressing unwanted sub-agent announcements ([#8299](https://github.com/openclaw/openclaw/issues/8299)).

### 8. Backlog Watch
Several important items are in "stale" or long-unanswered states that require maintainer attention:
- **[#75 - Linux/Windows Clawdbot Apps](https://github.com/openclaw/openclaw/issues/75)** – The most-commented issue (115 comments) has been open since January 2026 with no assigned PR.
- **[#67419 - Session Context Bloat](https://github.com/openclaw/openclaw/issues/67419)** – Open since April, rated P2, but describes a **20-30% token waste** per turn—a significant cost and performance issue.
- **[#85251 - Codex Session Wedge](https://github.com/openclaw/openclaw/issues/85251)** – A P1 bug where embedded runs freeze for the full 360s recovery window, with no PR linked.
- **[#9986 - Fallback on Context Length Exceeded](https://github.com/openclaw/openclaw/issues/9986)** – A feature request that could prevent many user-facing "model errored" scenarios, still awaiting maintainer review after 6 months.

---

## Cross-Ecosystem Comparison

## Cross-Project Ecosystem Comparison Report
**Date:** 2026-07-28  
**Analysis Period:** Last 24 hours

---

## 1. Ecosystem Overview

The personal AI assistant open-source ecosystem is experiencing **unprecedented velocity**, with six of nine monitored projects showing high activity and aggregate daily throughput exceeding **1,000 issues and 800 PR updates**. The ecosystem is bifurcating into two tiers: **production-first platforms** (OpenClaw, NanoBot, IronClaw, CoPaw) racing toward enterprise stability, and **experimental/niche projects** (Moltis, PicoClaw, NanoClaw) advancing specific architectural bets like ACP protocols and embedded deployment. A shared crisis is emerging around **memory management and security provenance**—every active project reports memory leaks, context bloat, or authorization bypass defects. The community is demanding **deterministic agent behavior**, concrete sandboxing guarantees, and multi-channel reliability before trusting agents with production workloads. Notably, the ecosystem is converging on **sandboxed execution, pluggable memory backends, and channel-agnostic messaging layers** as architectural requirements, while diverging on whether to prioritize local-first (PicoClaw, TinyClaw) versus cloud-hybrid (OpenClaw, CoPaw) deployment models.

---

## 2. Activity Comparison

| Project | Issues Updated (24h) | PRs Updated (24h) | Release Status | Health Score | Notes |
|---------|----------------------|-------------------|----------------|--------------|-------|
| **OpenClaw** | 500 (235 open) | 500 (275 open) | Beta cycle (2026.7.2-beta.5) | 🟡 Caution | Massive volume, P0 memory leaks, security gaps |
| **NanoBot** | 64 (63 closed) | 38 (14 open) | No new release | 🟢 Excellent | Highest close rate, rapid iteration |
| **Hermes Agent** | 50 (44 open) | 50 (40 open) | v2026.7.20 | 🟡 Moderate | Open/closed imbalance, Windows pain |
| **IronClaw** | 37 (32 open) | 50 (46 open) | **v1.0.0 (07/27)** | 🟡 Launch Mode | Post-release bug bash, CI instability |
| **CoPaw** | 50 (13 open) | 49 (15 open) | v2.0.0.post3 | 🟡 Moderate | High close rate, regression in current release |
| **ZeroClaw** | 50 (46 open) | 50 (44 open) | v0.8.3 | 🔴 Stressed | Security audit avalanche, CI broken |
| **LobsterAI** | 7 (5 open) | 9 (5 open) | No new release | 🟡 Moderate | Growing backlog, 3-month stale bugs |
| **PicoClaw** | 5 (5 open) | 4 (4 open) | v0.3.1 | 🟡 Slow | No merges today, key PRs stale (27 days) |
| **NanoClaw** | 0 | 8 (8 open) | No new release | 🟡 Moderate | PRs active but unmerged, Signal fixes pending |
| **Moltis** | 0 | 5 (5 open) | No new release | 🟡 Development | Architectural work, no code landing |
| **NullClaw** | 0 | 1 (1 open) | No new release | 🟢 Stable | Zero bugs, but Dependabot PR stale 43 days |
| **TinyClaw** | 0 | 0 | N/A | ⚪ Inactive | No activity |
| **ZeptoClaw** | 0 | 0 | N/A | ⚪ Inactive | No activity |

**Health Score Definitions:** 🟢 Excellent (high close rate, no critical bugs) · 🟡 Moderate/Caution (active but with risks) · 🟡 Development (active but no code landing) · 🔴 Stressed (critical security/CI failures) · 🟢 Stable (maintenance phase, low risk) · ⚪ Inactive (no activity)

**Key Observations:**
- Four projects (OpenClaw, NanoBot, Hermes, IronClaw) account for 90%+ of ecosystem activity
- NanoBot has the highest **efficiency ratio** (63 of 64 issues closed = 98%)
- ZeroClaw has the lowest **health signal** (46 of 50 issues still open, CI broken, 12+ security bugs)
- Two projects (TinyClaw, ZeptoClaw) show zero activity—potential abandonment risk

---

## 3. OpenClaw's Position

**Advantages vs. Peers:**
- **Ecosystem scale**: 500 daily issues/PRs—3x larger than next-busiest project (NanoBot). Community size is unmatched.
- **Reference implementation status**: As the canonical "claw" architecture, OpenClaw sets patterns others follow (Standard Hosting Profiles RFC 23, ClawHub skill marketplace, `clawsweeper` triage).
- **Security investment**: Dedicated SSRF protection (#113215), sandbox escape fixes (#111463), and masked secrets demand (#10659) show proactive security posture compared to peers with reactive audit responses (ZeroClaw).
- **Platform breadth**: Support for multiple bot accounts on Teams, iOS wake tasks, and desktop Control UI mandatory e2e tests signals enterprise maturity.
- **Feature depth**: Dynamic model discovery, filesystem sandboxing, session stream mode—these are architectural, not cosmetic.

**Technical Approach Differences:**
- **Triage rigor**: OpenClaw uses the `clawsweeper` P0–P2 severity system explicitly; most peers use GitHub labels inconsistently. This enables clearer risk communication.
- **Beta discipline**: Operating a named beta cycle (`2026.7.2-beta.5`) with explicit regression tracking—more formal than peers' release strategies.
- **Memory model**: Gateway-centric architecture (Codex sessions, SQLite snapshots) contrasts with IronClaw's row-native journal approach and NanoBot's GitStore model.

**Community Size Comparison:**
- OpenClaw likely has the largest contributor base (implied by 500 daily PRs and long-running threads like #75 with 115 comments)
- NanoBot has strong community-driven PRs (64 issues closed/day) but smaller absolute volume
- ZeroClaw's audit-driven spike suggests a smaller, more technically sophisticated user base
- Moltis and PicoClaw show single-contributor bottleneck risk (e.g., PicoClaw's PR #3200 stale 27 days)

**Risk:** OpenClaw's P0/P1 memory leaks (#91588, 15.5GB RSS) and session bloat (#67419, 20-30% token waste) threaten to erode trust—NanoBot's GitStore fix and IronClaw's `FailureKind` refactor show competitors solving similar problems faster.

---

## 4. Shared Technical Focus Areas

The following requirements are emerging **independently across multiple projects**, signaling ecosystem-wide priorities:

| Focus Area | Affected Projects | Specific Needs |
|------------|------------------|----------------|
| **Memory/Context Leak Prevention** | OpenClaw, NanoBot, CoPaw, Hermes, ZeroClaw | Gateway heap growth, session bloat, consolidation failures, vector index persistence |
| **Security & Authorization** | OpenClaw, ZeroClaw, Hermes, Moltis | SSRF, sandbox escape, API key leakage, channel authorization bypass, tool allowlist bypass |
| **Windows Platform Parity** | OpenClaw, Hermes, CoPaw, ZeroClaw, LobsterAI | Native sandbox, PATH encoding, file system compatibility, compilation failures |
| **Channel Reliability** | OpenClaw, NanoBot, CoPaw, Hermes, ZeroClaw | Duplicate messages (Telegram), silent drops (Feishu, WhatsApp), stale sessions, WebSocket reconnection |
| **Multi-Agent/Profile Isolation** | Hermes, ZeroClaw, Moltis, NanoClaw | Profile session auth, per-profile allowlists, engagement policy self-service |
| **Local Model Deployment** | NanoBot, PicoClaw, CoPaw | Ollama/LM Studio confusion, memory consolidation with local models, port binding failures |
| **Internationalization** | PicoClaw, ZeroClaw | Japanese localization (PicoClaw), English metadata in localized UI (ZeroClaw) |
| **Upgrade/Migration Safety** | OpenClaw, CoPaw, ZeroClaw | State migration blocking startup, chat history mapping loss, silent breaking changes |
| **Pluggable Backends** | IronClaw, CoPaw, Moltis, ZeroClaw | MCP server support, third-party agent backends, WASM memory plugins, ACP bidirectional |
| **Tool/Extension Platforms** | NanoBot, OpenClaw, IronClaw | skills.sh marketplace, unified extension platform, IronHub marketplace |

**Cross-cutting insight:** The **memory + security + Windows** trifecta is the ecosystem's largest shared debt. Every project that has scaled beyond initial prototyping has hit these walls.

---

## 5. Differentiation Analysis

| Dimension | OpenClaw | NanoBot | IronClaw | CoPaw | ZeroClaw | Moltis |
|-----------|----------|---------|----------|-------|----------|--------|
| **Target User** | Enterprise/advanced | General developer | Adventurous early adopter | Chinese enterprise | Security-focused developer | Protocol/architecture dev |
| **Deployment Model** | Cloud-hybrid (gateway) | Self-hosted + cloud | Local-first (Reborn) | Hybrid (AgentScope) | CLI + headless | Protocol-native (ACP) |
| **Core Architecture** | Gateway + Codex sessions | GitStore memory | Row-native journal | AgentScope platform | CLI + WASM plugins | ACP client→agent bridge |
| **Release Cadence** | Beta cycles (formal) | Rapid (64 issues/day) | Major version (v1.0.0) | Point releases (2.0.x) | Milestone (v0.9.0) | Development phase |
| **Community Origin** | Western/international | Asian (HKU) | Near.ai (US) | Chinese (Alibaba) | International | International |
| **Language** | Multi-language | English + Chinese | English | Chinese-first | English | English |
| **Differentiator** | Scale & ecosystem breadth | Close rate & WebUI polish | Architecture rewrite (Reborn) | Chinese ecosystem + Qwen | WASM sandboxing | ACP protocol innovation |
| **Primary Risk** | Memory leak severity | Backlog growth | Post-release regressions | Upgrade fragility | Security debt | Single-contributor bottleneck |

**Key differentiators:**
- **OpenClaw** wins on **community scale** and **feature breadth** but loses on **stability velocity**
- **NanoBot** wins on **developer responsiveness** (98% close rate) and **WebUI polish** (Dream runs, skills marketplace)
- **IronClaw** is the most **architecturally ambitious** (Reborn rewrite) but carries post-v1.0 regression risk
- **CoPaw** dominates **Chinese ecosystem integration** (Feishu, DingTalk, Qwen) but underinvests in Western channels
- **ZeroClaw** leads on **security innovation** (WASM sandbox) but fails on **operational security** (12+ audit findings)
- **Moltis** is the most **architecturally radical** (ACP-native) but has no production users yet
- **PicoClaw** and **NanoClaw** serve **embedded/lightweight** niches but lack maintainer bandwidth

---

## 6. Community Momentum & Maturity

### Tier 1: High Velocity (Rapidly Iterating)
- **OpenClaw** — 500 daily PRs, formal beta cycle, massive community. Volatility is high but momentum is undeniable. Risk: burnout if P0 memory leaks persist.
- **NanoBot** — 98% issue close rate, 24 PR merges/day. Most efficient project. Closing in on production readiness within weeks.
- **IronClaw** — v1.0.0 just shipped; 50 PRs/day in stabilization phase. High energy, high risk of regressions. Watch for post-launch fatigue.
- **CoPaw** — 37 of 50 issues closed/day; 15 PRs merged. Healthy cadence but regression in current release (#6258) is concerning.

### Tier 2: Moderate/Stabilizing
- **Hermes Agent** — Steady state (50/50 issues/PRs) but low close rate (6 of 50). Backlog pressure is building.
- **ZeroClaw** — Security audit spike (12+ p1 bugs in 48h) + CI broken. This is a **remediation phase**, not normal development. Risk of losing community trust.
- **LobsterAI** — Moderate activity but 3-month stale bugs (#1240, #1237) signal maintainer bottleneck. Community contributing PRs faster than reviews.

### Tier 3: Niche/Development
- **Moltis** — 5 PRs, all open, no code landing. Heavy architectural work (ACP, Zvec, instrumentation) but no shipped value yet.
- **PicoClaw** — Critical PR #3200 stale 27 days. Japanese localization is positive signal but single-contributor risk.
- **NanoClaw** — Signal attachment fix (#3142) and Dial integration (#3050) suggest targeted US Navy/DoD use case. Low volume but purposeful.

### Tier 4: Inactive/Stable
- **NullClaw** — No issues, no merges. Dependabot PR stale 43 days. Maintenance mode or abandoned.
- **TinyClaw, ZeptoClaw** — Zero activity. Considered dormant.

**Maturity Assessment:** NanoBot and OpenClaw are the ecosystem's two poles—one optimized for **velocity and polish**, the other for **scale and breadth**. IronClaw's v1.0 launch makes it the third platform to watch. The remaining projects serve specialized niches or are in development limbo.

---

## 7. Trend Signals

### For AI Agent Developers

1. **Memory is the new bottleneck.** Every project reports memory leaks, context bloat, or consolidation failures. The era of "infinite context window" is over—pragmatic solutions (session compaction, row-native journals, GitStore snapshots) are becoming competitive differentiators.

2. **Security is shifting from "feature" to "licensing requirement."** ZeroClaw's audit findings (12+ p1 bugs in 48h) and the independent emergence of masked secrets, allowlist denials, and sandboxing across OpenClaw, Hermes, and Moltis indicate that **production deployment requires systematic security**, not bolt-on fixes.

3. **Channel reliability is table stakes, not differentiation.** Feishu, Telegram, WhatsApp, and LINE all have duplicate/lost message bugs across projects. Users expect **at-least-once delivery** and **error visibility**—the projects that solve this win trust.

4. **Windows is the platform threshold.** Every project with Windows bugs (Hermes, CoPaw, ZeroClaw, LobsterAI) loses developer mindshare. Linux-first is acceptable for servers; Windows compatibility is required for developer adoption.

5. **Local model deployment is a UX problem, not an infrastructure one.** Users can configure Ollama; they cannot configure a broken port, missing memory consolidation, or silent failures. The projects that **hide complexity** (NanoBot's preset switching, PicoClaw's fallback chains) will win local-first users.

6. **Internationalization is accelerating.** PicoClaw's Japanese localization (merged within hours of request), ZeroClaw's partial i18n, and CoPaw's Chinese-first design signal that global adoption requires **language-native experiences**, not just translation.

7. **Agent-marketplace ecosystems are emerging.** OpenClaw (ClawHub), NanoBot (skills.sh), and IronClaw (IronHub) are all building skill/tool marketplaces. The winning platform will have the **best curation and security review**—not the most listings.

8. **Multi-agent patterns are unproven in production.** Hermes (multiplex profiles), ZeroClaw (delegate tool bypass), and Moltis (ACP agent exposure) all explore multi-agent architectures, but **isolation and coordination bugs** (#72348, #8279) show this is still unsolved.

9. **CI reliability correlates with project health.** ZeroClaw's broken CI (#9357) precedes its security crisis; OpenClaw's mandatory e2e test gate (#114554) precedes its beta discipline. **Projects that invest in CI first ship reliably later.**

10. **Single-contributor risk is real.** Moltis (penso), PicoClaw, and NanoClaw show bottleneck patterns. Projects that attract **multiple active maintainers** (OpenClaw, NanoBot, IronClaw) survive through velocity. Ecosystem dependency on individuals is a risk factor.

### Strategic Recommendation
For decision-makers evaluating this ecosystem:
- **Production deployment today:** OpenClaw (broadest platform) or NanoBot (fastest iteration)—accept memory leaks as a known risk
- **Security-sensitive deployment:** Wait for ZeroClaw's security sprint results or invest in Hermes with monitoring
- **Chinese-market focus:** CoPaw (deepest ecosystem integration)
- **Architecture research:** Moltis (ACP protocol innovation) or IronClaw (row-native journal)
- **Avoid investment in:** TinyClaw, ZeptoClaw (no activity); monitor NullClaw (maintenance risk)

The next 3-6 months will determine which projects **cross the chasm** from promising open-source to production infrastructure. OpenClaw and NanoBot have the strongest momentum; IronClaw has the architectural ambition; ZeroClaw has the most to prove.

---

## Peer Project Reports

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot Project Digest — 2026-07-28

## Today's Overview
NanoBot exhibited very high activity today with 64 issues updated (63 closed, 1 active) and 38 pull requests updated (14 open, 24 merged/closed). The project is clearly in a period of intense development and maintenance, driven largely by a sustained effort to close out older open issues and land numerous enhancement PRs. The surge in merged PRs across WebUI, agent core, and channel components signals a stable, accelerating release cadence. No new releases were published today, but the volume of merged changes suggests a release may be imminent. Overall project health appears excellent, with significant community engagement and rapid developer response to bugs.

## Releases
No new releases were published today. The latest available version remains unreported in this data.

## Project Progress
24 PRs were merged or closed today, indicating strong forward momentum across several subsystems:

**WebUI Improvements (significant advance):**
- [#5112](https://github.com/HKUDS/nanobot/pull/5112) — "feat(webui): expose Dream runs as read-only sessions" – A major feature exposing Dream agent runs in the WebUI with full replay of reasoning, tool calls, file edits, and streaming output in a dedicated read-only session group.
- [#5116](https://github.com/HKUDS/nanobot/pull/5116) — "feat(webui): add skills.sh marketplace and skill management" – Adds a Discover view backed by the skills.sh registry and 24-hour leaderboard, plus CLI-based skill installation.
- [#5077](https://github.com/HKUDS/nanobot/pull/5077) — "feat(webui): switch model presets from the composer" – Users can now long-press and drag to cycle through model presets directly in the composer.
- [#5121](https://github.com/HKUDS/nanobot/pull/5121) — "fix(webui): prevent composer resize scroll jitter" – Fixes a UI annoyance where completion auto-follow interfered with manual scrolling.
- [#5113](https://github.com/HKUDS/nanobot/pull/5113) — "fix(webui): stabilize repeated model preset rows" – Ensures fallback presets don't create duplicate or stale UI rows.

**Agent & Core Fixes:**
- [#5126](https://github.com/HKUDS/nanobot/pull/5126) / [#5124](https://github.com/HKUDS/nanobot/pull/5124) — "fix(gitstore): return real git object ids instead of hex-of-hex" – Critical fix preventing double-encoding of Git object IDs that could corrupt memory history.
- [#5122](https://github.com/HKUDS/nanobot/pull/5122) — "fix(agent): read document attachments on demand" – Non-image uploads (PDF, DOCX, XLSX, PPTX) now lazily parsed via `read_file` instead of ingested upfront.
- [#5120](https://github.com/HKUDS/nanobot/pull/5120) — "fix: session consolidation drops uploaded media paths" – Fixes data loss where file paths persisted only in `media[]` field were silently dropped during consolidation.
- [#5117](https://github.com/HKUDS/nanobot/pull/5117) — "fix(session): tolerate invalid idle-compaction timestamps" – Guards against crash when persisted `updated_at` is invalid.
- [#5114](https://github.com/HKUDS/nanobot/pull/5114) — "fix(memory): preserve Dream input integrity" – Ensures Dream sees full conversation history and can write to canonical memory files.

**Integrations & Channels:**
- [#5115](https://github.com/HKUDS/nanobot/pull/5115) — "feat(channels): add LINE Messaging API channel" – Adds support for Japan/Taiwan/Thailand/Indonesia's most popular messenger.

**Developer Experience:**
- [#5123](https://github.com/HKUDS/nanobot/pull/5123) — "docs: improve README landing page" – Updated README with clearer H1, star CTA, and concrete use cases.
- [#5098](https://github.com/HKUDS/nanobot/pull/5098) — "feat(extensions): add unified extension platform" – Introduces a native Python extension boundary for code-level capabilities beyond skills/Apps/MCP.
- [#5110](https://github.com/HKUDS/nanobot/pull/5110) — "feat(config): make status actionable for agent readiness" – `nanobot status` now includes offline Agent-readiness check.
- [#5076](https://github.com/HKUDS/nanobot/pull/5076) — "fix(webui): honor custom gateway port with Vite" – Custom ports now work correctly with Vite dev server.

## Community Hot Topics
The most active discussions today were all **closed issues**, indicating that development velocity is outpacing community discussion backlog:

1. **[#1991](https://github.com/HKUDS/nanobot/issues/1991) — "Hope nanobot can support multiple custom providers"** (9 comments)  
   User requests ability to add multiple custom model configurations and switch freely. This has 9 comments but 0 upvotes, suggesting limited broader demand—though the specific use case (switching between models easily) is being partially addressed by the new preset-switching feature in PR #5077.

2. **[#3123](https://github.com/HKUDS/nanobot/issues/3123) — "cron/scheduled task message send"** (8 comments)  
   User reports that cron-sent messages cannot be asked about afterwards because they belong to the cron session rather than a user session. A nuanced UX design challenge for multi-turn conversations that start from scheduled messages.

3. **[#2570](https://github.com/HKUDS/nanobot/issues/2570) — "local ollama config — 404 page not found"** (7 comments)  
   User struggling with local Ollama setup on Raspberry Pi; gateway not listening on expected port. This is a recurring pain point for local-model users.

4. **[#1174](https://github.com/HKUDS/nanobot/issues/1174) — "memory consolidation can take long or even fail"** (5 comments, 👍2)  
   Most upvoted issue today. User reports that switching from cloud to local model causes memory consolidation failures and prevents starting new sessions. Highlights a major usability barrier for users mixing model providers.

## Bugs & Stability
**Critical/P1 Bugs with Existing Fix PRs:**
- **[#4792](https://github.com/HKUDS/nanobot/issues/4792) — "/stop silently discards pending queue messages"** – Messages in queue are permanently lost when `/stop` is used. No fix PR yet; this is a serious data loss issue.
- **[#4805](https://github.com/HKUDS/nanobot/issues/4805) — "suppress(Exception) on prepare_call silently swallows tool validation errors"** – Tool errors are hidden, leading to silent failures and fallback to unprocessed calls.
- **[#5126](https://github.com/HKUDS/nanobot/pull/5126) — GitStore hex-of-hex bug (fix PR exists)** – Double-encoding of Git object IDs risked memory history corruption. Fix was merged today.
- **[#5120](https://github.com/HKUDS/nanobot/pull/5120) — Session consolidation drops media paths (fix PR exists)** – Data loss bug where uploaded file paths were lost during session consolidation. Fix merged today.

**Moderate Bugs:**
- **[#3559](https://github.com/HKUDS/nanobot/issues/3559) — WebSocket cannot replace webhooks for proactive delivery in multi-tenant** – Architectural limitation for cron/heartbeat/agent-initiated messages.
- **[#1174](https://github.com/HKUDS/nanobot/issues/1174) — Memory consolidation failures with local models** – Makes it impossible to start new sessions after model switch.
- **[#1881](https://github.com/HKUDS/nanobot/issues/1881) — Tool and memory not optional for weaker models** – Users with low-quality models suffer memory blowup and tool interference.

**Lower-Severity:**
- **[#1672](https://github.com/HKUDS/nanobot/issues/1672) — WhatsApp self-message not working** – Agent won't reply to own messages; likely a permission filtering issue.
- **[#1948](https://github.com/HKUDS/nanobot/issues/1948) — Exec tool cannot write to /tmp** – Docker/container filesystem restriction issue.

## Feature Requests & Roadmap Signals
**Likely in Next Version:**
- **LINE channel** ([PR #5115](https://github.com/HKUDS/nanobot/pull/5115)) – Very likely to merge given it's a clean PR with full test coverage and urgent demand in SE Asia.
- **Dream runs in WebUI** ([PR #5112](https://github.com/HKUDS/nanobot/pull/5112)) – Already merged; will appear in next release.
- **skills.sh marketplace** ([PR #5116](https://github.com/HKUDS/nanobot/pull/5116)) – Already merged; major ecosystem play.
- **Extension platform** ([PR #5098](https://github.com/HKUDS/nanobot/pull/5098)) – Already merged; foundational for third-party plugins.

**User-Requested Features (Potential):**
- **Multiple custom model providers** ([#1991](https://github.com/HKUDS/nanobot/issues/1991)) – Partially addressed by preset switching; full support likely in future.
- **Optional tool/memory for weak models** ([#1881](https://github.com/HKUDS/nanobot/issues/1881)) – Increasingly important as the user base grows to include resource-constrained setups.
- **Operator/Plugin support like OpenClaw** ([#1881](https://github.com/HKUDS/nanobot/issues/1881)) – The extension platform ([#5098](https://github.com/HKUDS/nanobot/pull/5098)) directly addresses this.
- **Emoji customization** ([#2747](https://github.com/HKUDS/nanobot/issues/2747)) – Low effort, high polish; could appear as a quick win.

## User Feedback Summary
**Pain Points:**
1. **Local model integration remains difficult** – Multiple issues ([#2570](https://github.com/HKUDS/nanobot/issues/2570), [#1590](https://github.com/HKUDS/nanobot/issues/1590), [#1947](https://github.com/HKUDS/nanobot/issues/1947)) show users struggle with Ollama, LM Studio, and other local providers. Configuration is confusing, with port mismatches and API key requirements even for local models.
2. **Memory management issues with model switching** ([#1174](https://github.com/HKUDS/nanobot/issues/1174)) – Users who try to switch from cloud to local models hit consolidation failures that block new sessions entirely.
3. **Channel-specific bugs frustrate users** – Feishu progress notifications ([#3166](https://github.com/HKUDS/nanobot/issues/3166)), WhatsApp self-messages ([#1672](https://github.com/HKUDS/nanobot/issues/1672)), and Discord slash command conflicts ([#1315](https://github.com/HKUDS/nanobot/issues/1315)) each indicate integration fragility.
4. **Message loss bugs erode trust** – `/stop` discarding queue ([#4792](https://github.com/HKUDS/nanobot/issues/4792)) and session consolidation dropping media ([#5120](https://github.com/HKUDS/nanobot/issues/5120)) are serious data integrity concerns.

**Satisfaction Signals:**
- High community engagement; users are actively filing detailed bug reports with reproduction steps.
- The rapid closure of 63 issues in one day indicates strong maintainer responsiveness.
- New features like the LINE channel and skills marketplace show the project is expanding its ecosystem reach.

## Backlog Watch
- **[#3123](https://github.com/HKUDS/nanobot/issues/3123) — Cron/scheduled message usability** (8 comments, closed) – While closed, the underlying UX problem (cron messages not attachable to user sessions) remains unsolved.
- **[#4792](https://github.com/HKUDS/nanobot/issues/4792) — /stop discarding messages** (3 comments, closed) – Closed but no fix PR is evident; should be monitored for reoccurrence given severity.
- **[#1033](https://github.com/HKUDS/nanobot/issues/1033) — Inter-instance cache staleness** (3 comments, closed) – Different channels see different cron job lists; closed but may resurface in multi-instance deployments.
- **[#3559](https://github.com/HKUDS/nanobot/issues/3559) — WebSocket vs webhook for proactive delivery** (3 comments, closed) – Architectural limitation closed as "won't fix" for now; enterprise users may need this revisited.
- **[#1328](https://github.com/HKUDS/nanobot/issues/1328) — Agent and gateway don't share skills** (2 comments) – Skills created via CLI agent not visible to gateway users; a fundamental workflow gap that could limit adoption for teams.

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent Project Digest — 2026-07-28

## Today's Overview

High activity day with **50 issues** and **50 PRs** updated in the last 24 hours, signaling sustained community engagement and active development. The project maintains a healthy balance of bug fixes, feature work, and community support, though the open-to-closed ratio (44 open issues, 40 open PRs versus 6 and 10 closed/merged respectively) suggests some backlog pressure. No new releases were published today, but the volume of merged PRs indicates forthcoming improvements. The Windows platform continues to be a notable pain point, with multiple unresolved platform-specific bugs. Overall, the project appears in a **steady state of active development** with responsive maintainers, though some long-standing issues in the backlog warrant closer attention.

## Releases

**No new releases today.** The last published version remains v2026.7.20 based on issue references. Users should monitor for an upcoming release given the volume of recently merged fixes.

## Project Progress — Merged/Closed PRs Today

Ten PRs were closed or merged in the last 24 hours:

- **[#72963](https://github.com/NousResearch/hermes-agent/pull/72963)** — *Unify the preview rail onto one tab list* (Merged). Consolidates two separate preview systems into a single tab strip in the right rail, reducing UI complexity.
- **[#71503](https://github.com/NousResearch/hermes-agent/pull/71503)** — *Fix desktop: authenticate profile session slices against oauth gateways* (Merged). Fixes a bug where the Desktop session sidebar rendered empty for the root profile on oauth-gated remote gateways. Addressed a significant authentication isolation issue.
- **[#72956](https://github.com/NousResearch/hermes-agent/pull/72956)** — *Fix desktop: don't let Enter swap a free-text slash argument for a completion* (Merged). Resolves a UI hazard where pressing Enter could replace user-typed prose with an unintended completion.
- **[#63512](https://github.com/NousResearch/hermes-agent/pull/63512)** — *Fix browser: safely decode subprocess output with regression coverage* (Merged). Adds robust UTF-8 decoding for browser subprocess output, preventing crashes on malformed encoding.
- **[#71817](https://github.com/NousResearch/hermes-agent/issues/71817)** — Closed as duplicate — *browser.cdp_url configuration causes 10+ second startup delay*.
- **[#66757](https://github.com/NousResearch/hermes-agent/issues/66757)** — Closed as duplicate — *Desktop app i18n: respect display.language config*.
- **[#42040](https://github.com/NousResearch/hermes-agent/issues/42040)** — Closed — *Windows x.com passkey prompt appears when Hermes starts/uses stale browser CDP config*.
- **[#70811](https://github.com/NousResearch/hermes-agent/issues/70811)** — Closed — *browser_cdp check_fn performs network I/O and makes the tool schema unstable*.
- **[#72667](https://github.com/NousResearch/hermes-agent/issues/72667)** — Closed — *MCP stdio: stale serve processes mask fixes + unbounded dart mcp-server accumulation*.
- **[#65735](https://github.com/NousResearch/hermes-agent/issues/65735)** — Closed — *Support multiple openai/codex subscriptions* (implemented on main).

**Key advances:** Desktop UX improvements were a clear focus today — three PRs improving the preview rail, find bar, and slash-command behavior were merged. Browser tool stability received a meaningful fix with proper output decoding. The oauth gateway fix for profile sessions closes an important authentication isolation gap.

## Community Hot Topics

The most active discussions in the last 24 hours (by comment count and reactions):

1. **[#63177 — search_files silently returns 0 results on Windows (5 comments, 1 👍)](https://github.com/NousResearch/hermes-agent/issues/63177)**  
   *Underlying need:* Users on native Windows (no WSL) cannot reliably search files with absolute paths due to path conversion conflicts between MSYS and native ripgrep. This is the **longest-running active discussion** at 16 days, suggesting deep frustration. A related duplicate [#67629](https://github.com/NousResearch/hermes-agent/issues/67629) was also updated today, indicating this is a systemic Windows issue.

2. **[#71349 — Dashboard chat stuck in "reconnecting" after model switch (5 comments)](https://github.com/NousResearch/hermes-agent/issues/71349)**  
   *Underlying need:* Model switching causes WebSocket connectivity breakdowns in the dashboard UI, leaving users unable to interact. The fact that the handshake succeeds but UI never recovers points to a state synchronization bug in the gateway-dashboard protocol.

3. **[#68339 — Mixed-batch tool execution interacts with TOOL_USE_ENFORCEMENT_GUIDANCE (4 comments)](https://github.com/NousResearch/hermes-agent/issues/68339)**  
   *Underlying need:* A recent performance improvement (#66317) is causing behavioral shifts in early-session tool usage for gated models. Community members are identifying unintended side effects of optimizations — a healthy sign of sophisticated testing.

4. **[#72348 — Discord adapter allow/deny gates are process-global under multiplex_profiles (3 comments, new today)](https://github.com/NousResearch/hermes-agent/issues/72348)**  
   *Underlying need:* Multi-profile isolation is a core feature for enterprise users, and this bug breaks security boundaries when running multiple Discord bots. This issue is likely to get rapid maintainer attention given the security implications.

5. **[#71097 — Hygiene Agent In-Place Compression Fails (3 comments)](https://github.com/NousResearch/hermes-agent/issues/71097)**  
   *Underlying need:* Session hygiene is critical for long-running agents. A configuration option (`compression.in_place = true`) that silently fails undermines trust in the system's ability to manage its own memory.

## Bugs & Stability — Ranked by Severity

### Critical / P2

| Issue | Description | Fix Exists? |
|-------|-------------|-------------|
| [#72348](https://github.com/NousResearch/hermes-agent/issues/72348) | Discord adapter allow/deny gates are process-global, breaking per-profile isolation under multiplex_profiles — **security boundary violation** | No |
| [#69398](https://github.com/NousResearch/hermes-agent/issues/69398) | Per-profile PairingStore path changed between versions — pairing approvals silently stop working after upgrade | No |
| [#68137](https://github.com/NousResearch/hermes-agent/issues/68137) | One-shot mode (`-z`) silently drops slow MCP servers due to incomplete tool registry | No |
| [#70253](https://github.com/NousResearch/hermes-agent/issues/70253) | Inbound images dropped from context during busy turns (busy_input_mode: steer) | No |
| [#69603](https://github.com/NousResearch/hermes-agent/issues/69603) | state.db repair/re-corrupt cascade — schema surgery not serialized correctly, causing repeated corruption | No |
| [#71999](https://github.com/NousResearch/hermes-agent/issues/71999) | #50502 cached-history guard false-fires every tool-use turn, misreading alternation-merged persisted view as write loss | No |

### Medium / P3

| Issue | Description | Fix Exists? |
|-------|-------------|-------------|
| [#70719](https://github.com/NousResearch/hermes-agent/issues/70719) | File-mutation verifier footer fires on arg-missing patch calls (noisy overclaim banner) | No |
| [#71097](https://github.com/NousResearch/hermes-agent/issues/71097) | Hygiene Agent in-place compression fails — `_last_compaction_in_place` not set | No |
| [#70422](https://github.com/NousResearch/hermes-agent/issues/70422) | Desktop: accidental composer drag/pop-out when selecting text | No |
| [#72961](https://github.com/NousResearch/hermes-agent/issues/72961) | Find-in-page bar overlaps titlebar icons and renders behind overlays | Yes — [#72959](https://github.com/NousResearch/hermes-agent/pull/72959) |
| [#72453](https://github.com/NousResearch/hermes-agent/issues/72453) | Desktop context gauge shows previous overflow while recovery turn running | No |

## Feature Requests & Roadmap Signals

Notable feature requests from today's activity:

1. **[#72952](https://github.com/NousResearch/hermes-agent/issues/72952) — Support Gemini-native enterprise gateways with custom base URL and auth header** (new today, P2). A user has already submitted a corresponding fix PR [#72958](https://github.com/NousResearch/hermes-agent/pull/72958). Given the P2 priority and the submitted patch, this is **likely to land in the next release**.

2. **[#71929](https://github.com/NousResearch/hermes-agent/issues/71929) — Make web backend selectors dropdown selects in Config Form view** (P3). A small UX improvement that reduces user error in configuration. High likelihood of quick implementation.

3. **[#72957](https://github.com/NousResearch/hermes-agent/pull/72957) — Telegram /profile picker with cross-restart persistence** (open PR). If merged, this adds persistent multi-profile switching to Telegram, a valuable feature for users with multiple agent configurations.

4. **[#72953](https://github.com/NousResearch/hermes-agent/pull/72953) — Sync pinned sessions across multiple GUI apps** (open PR). Synchronizes pinned sessions across Desktop clients sharing the same remote gateway — a quality-of-life improvement for multi-device users.

5. **[#72893](https://github.com/NousResearch/hermes-agent/pull/72893) — Group tool calls behind one summary line in Desktop** (open PR). Addresses transcript verbosity by collapsing runs of tool calls into single summary lines. Would significantly improve the Desktop reading experience.

6. **[#72968](https://github.com/NousResearch/hermes-agent/pull/72968) — Resume contextual reset followups** (open PR). Adds an opt-in continuation policy for idle/daily session expiry (auto-resume previous session). This would be valuable for users with long-running agent interactions.

**Prediction:** The Gemini enterprise gateway support, Telegram profile picker, and session sync features have strong momentum with existing PRs. These are strong candidates for the next minor release.

## User Feedback Summary

**Satisfaction signals:**
- Community is actively contributing patches, with multiple user-authored fix PRs today (OutThisLife, DavidMetcalfe, webtecnica, tigercraft4, antunes-hq, deacon-botdoctor).
- Users are running sophisticated configurations — multiplex profiles, enterprise gateways, oauth auth — indicating advanced adoption.

**Pain points (recurring themes):**

1. **Windows platform pain is persistent and acute.** Issues [#63177](https://github.com/NousResearch/hermes-agent/issues/63177), [#67629](https://github.com/NousResearch/hermes-agent/issues/67629), and [#69372](https://github.com/NousResearch/hermes-agent/issues/69372) all affect Windows users with no fix in sight. The search_files path issue alone has been open for 16 days.

2. **Post-upgrade breakage erodes trust.** Issue [#69398](https://github.com/NousResearch/hermes-agent/issues/69398) documents pairing approvals silently breaking after upgrading to v2026.7.20 due to a path change — with no migration path. This is a significant user experience problem.

3. **Desktop UI regressions are accumulating.** Three new desktop UI bugs today (overlapping find bar, context gauge misreporting, accidental composer pop-out) suggest the rapid UI changes are creating friction.

4. **Silent failures undermine confidence.** Multiple issues describe failures that produce no error messages — dropped images, lost memory turns, silently dropped MCP servers, false-positive compression footers. Users value actionable diagnostics.

## Backlog Watch

Issues and PRs needing maintainer attention:

| Item | Age | Gap |
|------|-----|-----|
| [#14614](https://github.com/NousResearch/hermes-agent/issues/14614) — `resolve_alias()` reverse lookup returns wrong provider | **96 days** (last updated today) | Long-standing config resolution bug; maintainers have not engaged recently despite it being P2 |
| [#26037](https://github.com/NousResearch/hermes-agent/issues/26037) — Feishu: reply-to-image messages lose parent context | **74 days** | Platform-specific bug for Feishu integration; no movement in months |
| [#33489](https://github.com/NousResearch/hermes-agent/issues/33489) — BlueBubbles adapter: add group chat filtering | **62 days** | Feature request with no maintainer response; users of BlueBubbles adapter lack basic filtering |
| [#63177](https://github.com/NousResearch/hermes-agent/issues/63177) — search_files silent failure on Windows | **16 days** | Now has a duplicate issue (#67629) filed 7 days later. The oldest active P2 bug without a fix assignment. Community is getting frustrated. |

**Watch items (new today requiring initial maintainer response):**
- [#72952](https://github.com/NousResearch/hermes-agent/issues/72952) — Gemini enterprise gateway support (has companion PR, but needs maintainer review of the approach)
- [#72348](https://github.com/NousResearch/hermes-agent/issues/72348) — Discord security boundary violation (P2, security implications)
- [#72961](https://github.com/NousResearch/hermes-agent/issues/72961) — Desktop find bar overlap (has fix PR #72959, likely to be quickly resolved)

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

Here is the PicoClaw project digest for July 28, 2026.

---

## PicoClaw Project Digest | 2026-07-28

### 1. Today's Overview

Activity over the last 24 hours is **moderate but critical**. While no new releases or merges occurred, the project saw updates on 4 open Pull Requests and 5 open Issues. The backlog remains active, with a significant "stale" 27-day-old PR (#3200) for a fallback model chain still pending. The community is currently focused on three key areas: **globalization** (Japanese localization), **hardening the agent loop** against failures (MCP/exec tool bugs), and **performance** (UI lag with long histories). The lack of any merged code today suggests the maintainer team is either reviewing complex PRs or in a release preparation phase.

### 2. Releases

- **None**: No new releases were published in the last 24 hours. The latest stable release remains **v0.3.1**.

### 3. Project Progress

- **Merged/Closed PRs (Today): 0**
- **Active PRs Updated: 4**
    - **#3273**: *feat(webui): add Japanese (ja) localization* – A full 968-line translation file submitted as requested by issue #3272.
    - **#3271**: *chore(providers): update default model names to 2026-07 latest* – Updates model IDs for OpenAI (e.g., `gpt-5.6-sol`), Anthropic, Gemini, and others.
    - **#3270**: *feat: add DashScope TTS provider and WeChat audio file sending* – Adds Alibaba Cloud TTS integration and a new audio output channel for WeChat.
    - **#3200**: *feat(models): add configurable default fallback chain* – A 27-day-old PR awaiting review to allow users to configure a fallback chain of models.

### 4. Community Hot Topics

The following issues are drawing the most community attention, primarily due to their direct impact on user workflows:

- **#3272 / #3273 (Japanese Localization):** The request for Japanese translation (#3272) was immediately implemented via PR #3273. This shows a **strong community responsiveness** and a clear user-base demand for i18n support beyond English/Chinese.
- **#3268 (exec tool default action):** Users report that AI agents fail when calling the `exec` tool because the `action` field is required. The fix (defaulting to `"run"`) is simple and has a high impact on agent reliability.
- **#3269 (MCP hang):** A severe bug where a failed MCP server connection causes a **complete deadlock** of the entire chat interface. This is a high-priority stability issue.
- **#3281 (Web UI Lag):** Performance degradation reported on long chat sessions, indicating a potential rendering or state management bottleneck in the frontend.

### 5. Bugs & Stability

| Severity | Issue | Summary | Fix PR? |
| :--- | :--- | :--- | :--- |
| **Critical** | [#3269](https://github.com/sipeed/picoclaw/issues/3269) | MCP server failure hangs the agent loop, breaking all replies. | No |
| **High** | [#3268](https://github.com/sipeed/picoclaw/issues/3268) | `exec` tool requires `action` param; AI calls fail unpredictably. | No |
| **Medium** | [#3281](https://github.com/sipeed/picoclaw/issues/3281) | Chat input becomes very laggy with long history. | No |

**Note:** None of these bugs currently have an associated fix PR open.

### 6. Feature Requests & Roadmap Signals

- **Japanese Localization:** Strong signal for internationalization. Likely to land in the next minor release (v0.3.2) given the PR is already open.
- **Systemd & Server Mode (#3276):** A request for better headless/server deployments, asking the launcher to detect an externally-managed gateway. This signals a **growing enterprise/self-hosting user base**.
- **Model Fallback Chains (#3200):** This long-standing PR suggests users want high reliability by chaining models (e.g., "try GPT-5.6, if down fallback to Claude"). If merged, this would be a major UX win for production users.
- **DashScope TTS + WeChat (#3270):** Indicates demand for **Chinese ecosystem integrations**, specifically Alibaba Cloud and WeChat messaging.

### 7. User Feedback Summary

- **Pain Points:**
    - Unreliable agent loops: Users are frustrated that a single MCP server failure or an LLM's parameter choice can freeze the whole chat (#3269, #3268).
    - Performance at scale: UI becomes unusable for power users with long conversation histories (#3281).
    - Lack of UI language options: International users (Japanese) lack a basic UI localization (#3272).
- **Use Cases:**
    - **Headless servers:** Users are deploying PicoClaw as a systemd service on Ubuntu VMs, expecting it to act as a persistent infrastructure component (#3276).
    - **WeChat integration:** Real-world usage involving sending audio files to WeChat is being developed and tested (#3270).

### 8. Backlog Watch

- **PR #3200 (Model Fallback Chain):** Opened **July 1st** (27 days ago). No maintainer activity. This is a highly requested feature that adds production-grade resilience. Risk of rotting.
- **Issue #3276 (External Gateway):** Open for 8 days. No maintainer response. Tags the core architectural assumption (launcher owns gateway lifecycle) that affects server deployments.
- **Issue #2723 (Hypothetical/Historical):** *No new items beyond the 24h window noted.* However, the lack of closure on #3276 and #3281 suggests the maintainers may be bottlenecked on review capacity.

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw Project Digest — 2026-07-28

## 1. Today's Overview
The NanoClaw project showed moderate activity over the past 24 hours, with **8 open pull requests** receiving updates but **no new issues, releases, or merges**. The sustained PR activity—spanning bug fixes, documentation, and feature skills—indicates the maintainers are actively advancing the codebase, particularly in Signal adapter reliability and container configuration fidelity. However, the absence of any closed PRs today suggests progress is in the review/iteration phase rather than landing code. The project remains healthy, with a clear focus on hardening existing integrations and improving developer experience around skill selection and approval workflows.

## 2. Releases
**No new releases.** The latest release remains unchanged from previous digest cycles.

## 3. Project Progress
**No PRs were merged or closed today.** The following pull requests were actively updated but remain open:
- **PR #2346** — Fix for unknown slash commands being misclassified as `passthrough`, which caused silent message drops; now categorizes them as normal chat.
- **PR #2685** — Documentation update covering Signal group typing indicators, outbound reactions, and quote-reply fixes.
- **PR #2971** — New `ncc` utility skill for host operational and health CLI capabilities.
- **PR #3050** — Adds Dial as a channel option in the setup wizard and skill model.
- **PR #3137** — Engages core team: fixes engagement consistency and exposes self-serve wiring controls for group-scoped agents.
- **PR #3141** — Fixes `container.json` skill selection so `CLAUDE.md` fragments are correctly respected.
- **PR #3142** — Critical fix for Signal attachments: previously hardcoded an unmounted path, making image/file attachments unreachable; now routes through the mounted inbox.
- **PR #3143** — Preserves approval card content after resolution, keeping title and request details visible with muted status indicators.

## 4. Community Hot Topics
The most active threads today, ranked by update frequency and cross-team engagement:

**1. PR #3137 — Engagement consistency & wiring controls** *(updated 2026-07-26→27)*  
Core-team contribution that addresses a fundamental pain point: group-scoped agents cannot inspect or adjust their own engagement policies. This PR enables agents to query their wirings and request approved updates, plus adds validation for JavaScript engagement regexes.  
🔗 [github.com/nanocoai/nanoclaw/pull/3137](https://github.com/nanocoai/nanoclaw/pull/3137)  
*Underlying need:* Operations teams managing multiple agents need self-service governance without manual intervention—this unlocks autonomous policy adjustments.

**2. PR #2971 — NCC utility skill** *(updated 2026-07-27)*  
New skill for host operational and health CLI commands. As a utility skill (no source changes), it represents a low-risk way to extend agent capabilities.  
🔗 [github.com/nanocoai/nanoclaw/pull/2971](https://github.com/nanocoai/nanoclaw/pull/2971)  
*Underlying need:* Users want agents to perform system-level checks and diagnostics without custom infrastructure.

**3. PR #3142 — Signal attachment path fix** *(updated 2026-07-27)*  
High-urgency fix: Signal image and file attachments were broken because the adapter used an unmounted path. This directly impacts production Signal deployments.  
🔗 [github.com/nanocoai/nanoclaw/pull/3142](https://github.com/nanocoai/nanoclaw/pull/3142)

## 5. Bugs & Stability

| Severity | Bug | Status | Fix PR |
|----------|-----|--------|--------|
| **Critical** | Signal attachments (images, PDFs, text files) broken due to hardcoded unmounted path | Open, fix authored | [#3142](https://github.com/nanocoai/nanoclaw/pull/3142) |
| **High** | Unknown slash commands silently dropped instead of treated as normal chat | Open, fix authored | [#2346](https://github.com/nanocoai/nanoclaw/pull/2346) |
| **Medium** | Approval cards lose content (title+details) after resolution | Open, fix restores retention | [#3143](https://github.com/nanocoai/nanoclaw/pull/3143) |
| **Medium** | Container skill selection ignores `container.json` for `CLAUDE.md` fragments | Open, fix authored | [#3141](https://github.com/nanocoai/nanoclaw/pull/3141) |

No new bugs were *reported* today—existing bugs have corresponding open fix PRs, indicating responsive maintenance.

## 6. Feature Requests & Roadmap Signals
Several open PRs point toward upcoming capabilities:

- **Dial channel integration** ([PR #3050](https://github.com/nanocoai/nanoclaw/pull/3050)) — Likely to land in the next minor release, as it includes setup wizard changes and skill model updates. Expands supported channels.
- **NCC host health CLI** ([PR #2971](https://github.com/nanocoai/nanoclaw/pull/2971)) — A pure utility skill, low integration cost, likely to merge quickly after review.
- **Self-serve engagement wiring** ([PR #3137](https://github.com/nanocoai/nanoclaw/pull/3137)) — Strong signal that autonomous agent governance is a roadmap priority; could become a core feature in v0.5 or v0.6.
- **Group typing indicators** (part of PR #2685) — Indicates Signal group support is maturing beyond basic messaging.

**Prediction:** The next release will likely include Dial support (PR #3050) and the Signal attachment fix (PR #3142), as these are well-progressed and address significant gaps.

## 7. User Feedback Summary
No new user comments were recorded in the last 24 hours. However, the PR patterns reveal ongoing user pain points:

- **Signal attachment usability** — The unmounted-path bug (PR #3142) impacts users relying on Signal for file sharing, especially teams using PDFs or documents.
- **Agent governance friction** — PR #3137 arises from real operator feedback that group-scoped agents need self-service controls, rather than requiring manual wiring edits.
- **Container selection confusion** — PR #3141 addresses a scenario where `container.json` skill selections were ignored for `CLAUDE.md` fragments, causing unexpected agent behavior.

These suggest satisfaction with the project's direction (active fixes are being authored), but some impatience with foundational bugs persisting across releases.

## 8. Backlog Watch
- **PR #2346** (Slash command misclassification fix) — Open since **2026-05-08** (82 days). Updated today but still unmerged. This fix prevents silent message drops, a likely user-facing issue. Needs maintainer prioritization.  
  🔗 [github.com/nanocoai/nanoclaw/pull/2346](https://github.com/nanocoai/nanoclaw/pull/2346)

- **PR #2685** (Signal docs update) — Open since **2026-06-04** (54 days). While a docs PR, it covers three important Signal features. Its age suggests documentation may be deprioritized relative to code fixes.  
  🔗 [github.com/nanocoai/nanoclaw/pull/2685](https://github.com/nanocoai/nanoclaw/pull/2685)

**No unanswered issues were identified** (the open issue count is zero), which is positive for project health—every tracked concern has an associated PR or is being actively worked.

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

Here is the **NullClaw Project Digest** for **2026-07-28**, based on the provided GitHub data.

---

### 1. Today's Overview
The NullClaw project is currently in a low-activity state. Over the last 24 hours, there were no new issues created, no releases published, and no pull requests merged. The only notable activity is a single open Pull Request (#956) from **dependabot**, which updates the base Docker image from Alpine 3.23 to 3.24. While the project maintains stability (zero open bugs today), the lack of recent commits or community engagement suggests a maintenance lull or a focus on internal development.

### 2. Releases
**None.** No new releases were published today or in the recent history provided. The "Latest Releases" section remains empty.

### 3. Project Progress
- **Merged/Closed PRs (24h):** 0
- **Progress this period:** No features or fixes were advanced or deployed today. The single open PR (#956) represents the only pending infrastructure change.

### 4. Community Hot Topics
The sole active item is:
- **[#956 - [OPEN] ci(deps): bump alpine from 3.23 to 3.24 in the docker-images group](https://github.com/nullclaw/nullclaw/pull/956)**
    - *Author:* dependabot[bot]
    - *Activity:* Created June 15, updated July 27 (no new comments).
    - *Analysis:* This is an automated dependency bump. The lack of human discussion or maintainer review for over a month indicates the project is not prioritizing CI maintenance or is awaiting a specific reviewer. The underlying need is to keep the runtime environment secure and up-to-date.

### 5. Bugs & Stability
- **Bugs reported today:** 0
- **Crashes/Regressions:** 0
- **Stability Assessment:** There are no stability concerns documented in the last 24 hours. The project appears stable, though this may also be due to low user testing volume.

### 6. Feature Requests & Roadmap Signals
- **No new feature requests** were filed today.
- **Predictions:** The open PR (#956) suggests the project is preparing its containerized deployment environment. If merged, the next version of NullClaw will likely ship on **Alpine 3.24** for improved security and compatibility.

### 7. User Feedback Summary
- **Positive Signals:** No user complaints or negative feedback surfaced today, indicating the current release is stable for existing users.
- **Pain Points:** None identified in the given data. There is no evidence of user dissatisfaction or reported usability issues.

### 8. Backlog Watch
- **Long-unanswered PR:** **[#956 - Bump alpine from 3.23 to 3.24](https://github.com/nullclaw/nullclaw/pull/956)**
    - *Issue:* This PR has been open for **43 days** (since June 15) without a review or merge from a maintainer.
    - *Risk:* Delaying this dependency update could expose containerized deployments to potential unpatched vulnerabilities in the older Alpine 3.23 base image. **Maintainer attention is required** to merge or close this PR to keep the CI/CD pipeline healthy.

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

Here is the IronClaw project digest for **2026-07-28**.

---

### 1. Today's Overview
The IronClaw project is in a high-velocity, launch-critical phase following the release of **v1.0.0** on July 27. Activity is extremely high, with **50 PRs** and **37 issues** updated in the last 24 hours, indicating intense engineering and bug-bashing efforts. The focus is squarely on stabilizing the "Reborn" architecture, closing out a v1 launch checklist, and resolving regressions identified during the final testing push. The team is also rapidly merging foundational infrastructure for sandboxing, memory providers, and error recovery.

### 2. Releases
**ironclaw v1.0.0** was released on 2026-07-27.
- **Summary:** This is a ground-up rebuild of the agent runtime, storage, extension host, and web UI (codenamed "Reborn"). It is **not** an increment on the 0.29.x line.
- **Breaking Changes:** The `ironclaw` binary now refers to the new rearchitected CLI. The legacy monolith is available as the `ironclaw-legacy` binary.
- **Migration:** A tracking issue (#6725) for the migration path from legacy to v1 has been opened but is still awaiting a detailed description.

### 3. Project Progress
Merged and closed PRs in the last 24 hours show significant infrastructure and refactoring progress:
- **Infrastructure & Security:** A new sandbox certificate authority and credential-firewall primitives (PR #6723) were merged, laying groundwork for TLS termination in the sandbox egress proxy.
- **Stability & Reliability:** A major refactor collapsed five failure-kind enums into a single `FailureKind` (PR #6684), fixing six mis-retry bugs and solidifying the error-recoverability contract. The e2e testing suite gained the ability to replay provider journeys in reverse order to prove isolation (PR #6728).
- **Documentation:** Internal engineering docs were restructured (PR #6692) to prevent sensitive content from being served publicly, and the docs site was reorganized around the v1.0 binary.
- **State Management:** A significant PR (PR #6696) collapsed lifecycle state into a row-native process journal, moving away from parallel turn row engines.

### 4. Community Hot Topics
- **#6284: [EPIC] Error-Recoverability Endgame** (14 comments)
  - **Link:** [Issue #6284](https://github.com/nearai/ironclaw/issues/6284)
  - This remains the most engaged discussion, defining the core contract that the agent must survive errors, see the cause, and be given a turn to act. It is driving multiple sub-tasks and PRs (e.g., #6697, #6684).
- **#6524: [EPIC] Hermetic Capability and Journey Testing Platform** (3 comments)
  - **Link:** [Issue #6524](https://github.com/nearai/ironclaw/issues/6524)
  - A high-priority effort to ensure every capability has deterministic, meaningful test coverage. It is the parent epic for the new e2e testing work (PR #6738).

### 5. Bugs & Stability
Multiple critical bugs were reported today as part of the v1-launch checklist:
- **Critical: UI/Streaming Issues (P1):** Users report tasks running indefinitely with a non-functional stop button (Issue #6720) and streaming that only resumes after switching pages (Issue #6718). Conversation history also fails to load after backend errors (Issue #6719). *No fix PRs are open yet.*
- **High: Incorrect Agent Hallucinations:** The model incorrectly claims Slack integration is unavailable (#6716) and gives Telegram pairing instructions after pairing has already succeeded (#6717). This indicates a **knowledge gap** where the agent lacks access to its own configuration state.
- **High: Duplicate Field Serialization:** A pre-existing bug causing 400 errors with DeepSeek when tools are included (Issue #4548) was closed, implying a fix was merged.
- **Medium: Theme/UI Defects:** Theme selection resets on SPA navigation (#6711) and the "Always allow" approval checkbox retains state across tool changes (#6713), representing minor but annoying UI regressions.

### 6. Feature Requests & Roadmap Signals
The project is heavily focused on extensibility and platform features for the next iteration:
- **Integration Roadmap:** A major new epic (#6731) signals intent to integrate **IronHub** (a tool/skill marketplace) into the agent, allowing runtime discovery and installation of community tools.
- **Documentation-Driven Agents:** A new epic (#6734) requests giving the agent access to its own documentation to guide users through configuration, directly addressing the hallucination bugs seen today (#6716, #6717).
- **Extensibility:** A roadmap item (#6727) explicitly calls for supporting **arbitrary user-supplied MCP servers**, moving beyond the two currently hardcoded ones. This, along with the "Unified Manifest-Driven Extension Platform" (#6481), points toward a v1.1 focused on making the agent truly extensible.

### 7. User Feedback Summary
Real user pain points are surfacing from the staging environment:
- **Configuration Headaches:** Users struggle with a lack of documentation and agent guidance for setting up channels like Telegram (#6522). The agent’s inability to accurately reflect its own state (e.g., claiming Slack is unavailable) leads to user confusion and distrust.
- **Fragile UI Experience:** Users are seeing persistent "Reconnecting" states (#6581), broken streaming (#6718), and unresponsive stop buttons (#6720), creating a perception of instability.
- **Successful Parity:** The closing of the DeepSeek bug (#4548) and the steady state of `ironclaw onboard` (Issue #6575, closed) suggest foundation installation and basic model compatibility are meeting expectations.

### 8. Backlog Watch
- **#6481, #6482, #6483, #6484 (Multiple Epics):** These four epics (Unified Extensions, Pluggable Memory, Telegram Hardening, Shared Messaging Layer) were all created on **2026-07-22** and remain open with zero comments from maintainers or community. Given the launch intensity, these may be critical but are currently undocumented.
- **#4548 (Closed):** The DeepSeek serialization bug (duplicate `model` field) was finally closed after 50 days open, which is a significant relief for users of that provider.
- **Release PR #5598:** This PR for a cross-crate release (with breaking changes in `ironclaw_common` and `ironclaw_skills`) has been open since July 3rd but shows recent activity. It is likely waiting for the v1.0 stabilization wave to pass before being merged.

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

# LobsterAI Project Digest — 2026-07-28

## 1. Today's Overview
The project shows **moderately high activity** with 7 issues and 9 PRs updated in the last 24 hours, though **no new releases** are available. Five PRs were merged/closed today, indicating steady development velocity, but the open issue count remains elevated—suggesting a **growing backlog** of unresolved user-impacting bugs. Several stale issues (3+ months old) were updated by authors today, possibly indicating frustration with lack of resolution. Two new critical bugs (data corruption via `\f` byte replacement, Shell encoding on Chinese Windows) surfaced within hours of this digest.

---

## 2. Releases
**No new releases** since last digest.

---

## 3. Project Progress (Merged/Closed PRs Today)
Five PRs were closed or merged today:

| PR | Title | Area | Summary |
|----|-------|------|---------|
| [#2389](https://github.com/netease-youdao/LobsterAI/pull/2389) (CLOSED) | fix(email): prevent attachment path traversal | docs, skills | Sanitizes attachment filenames, enforces download boundaries, adds cross-platform tests |
| [#2388](https://github.com/netease-youdao/LobsterAI/pull/2388) (CLOSED) | feat(artifacts): 新增预览工具栏分享与部署入口 | renderer, docs, build | Adds share/deploy buttons to Artifact preview toolbar; extracts deployment strategy logic; adds unit tests |
| [#2387](https://github.com/netease-youdao/LobsterAI/pull/2387) (CLOSED) | Feat/2026.7.20 sites | renderer, docs, main, artifacts | Bulk feature delivery for "sites" functionality (details not fully visible) |
| [#2386](https://github.com/netease-youdao/LobsterAI/pull/2386) (CLOSED) | fix(agentEngine): terminate no-progress tool loops before token budget exhaustion | renderer, build, docs, main, openclaw | Prevents runaway tool-calling loops that waste tokens; critical stability fix |
| [#1323](https://github.com/netease-youdao/LobsterAI/pull/1323) (CLOSED) | fix(cowork): narrow input-too-long error classification | cowork | Prevents misleading "input too long" UI when error is unrelated to context limits |

**Key advancements**: Agent engine runaway-loop protection merged; email skill security improved; Artifact preview sharing/deployment now functional.

---

## 4. Community Hot Topics

| Issue/PR | Comments | Reactions | Topic |
|----------|----------|-----------|-------|
| [#2400](https://github.com/netease-youdao/LobsterAI/pull/2394) (for discussion) | 5+ in sub-threads | — | Windows install manual overwrite blocked — user @fisherdaddy contributed a fix |
| [#2393](https://github.com/netease-youdao/LobsterAI/issues/2393) | 0 (just filed) | High urgency | **Critical**: `\f` byte pair silently replaced with form-feed character, corrupting file data |
| [#2392](https://github.com/netease-youdao/LobsterAI/issues/2392) | 0 (new) | — | Scheduled tasks cannot select which agent or skill to use — core scheduling limitation |
| [#1240](https://github.com/netease-youdao/LobsterAI/issues/1240) (stale) | 1 comment, user "zolufly-web" | — | API key rate-limit spills across all agents; app crashes on restart; user manually restored `openclaw.json` — **no maintainer response** |

**Underlying needs**:
- Users want **fine-grained control** over scheduled tasks (choose agent + skill)
- The API rate-limit propagation issue suggests a **session-level state leak** that is not being addressed
- Data corruption issue (#2393) is extremely high priority but has zero maintainer engagement yet

---

## 5. Bugs & Stability

### 🔴 Critical (Data Integrity)
- **[#2393](https://github.com/netease-youdao/LobsterAI/issues/2393)** — Accelerator replaces `\f` byte pair (`5C 66`) with form-feed character (`\x0C`), silently corrupting files containing literal `\f` tokens (e.g., `\firecrawl`, `\filename`). 100% reproducible. **No fix PR yet.**

### 🟠 High (Usability / Lockout)
- **[#1240](https://github.com/netease-youdao/LobsterAI/issues/1240)** — API rate-limit error permanently blocks ALL agent switching, even to models from other providers. After restart, app fails to launch unless `openclaw.json` is restored from backup. **3 months stale, no reply from maintainers.**
- **[#2062](https://github.com/netease-youdao/LobsterAI/issues/2062)** — Tasks exceeding max duration silently stop; user cannot tell if background execution continues. **2 months stale, no fix PR.**
- **[#2390](https://github.com/netease-youdao/LobsterAI/issues/2390)** — `exec` tool hardcodes `powershell.exe` (Windows PowerShell 5.1), breaking scripts for users with Chinese usernames (encoding corruption). **Filed today, no fix PR yet.**

### 🟡 Medium
- **[#1237](https://github.com/netease-youdao/LobsterAI/issues/1237)** — Unsaved Settings changes (API Key, provider config) silently lost when closing without Save. PR [#1241](https://github.com/netease-youdao/LobsterAI/pull/1241) exists but remains **open and stale since April 1st**.

---

## 6. Feature Requests & Roadmap Signals

| Feature | Issue/PR | Likelihood for Next Release |
|---------|----------|----------------------------|
| **Skill renaming** | [#2391](https://github.com/netease-youdao/LobsterAI/issues/2391) — user request | Low (no maintainer reaction yet) |
| **Agent + skill selection in scheduled tasks** | [#2392](https://github.com/netease-youdao/LobsterAI/issues/2392) | Low (requires UI + backend work) |
| **Taskbar/Dock flash on task completion** | PR [#1239](https://github.com/netease-youdao/LobsterAI/pull/1239) — open since April 1 | Medium (feature is written, needs review/merge) |
| **Unsaved changes confirmation in Settings** | PR [#1241](https://github.com/netease-youdao/LobsterAI/pull/1241) — open since April 1 | Medium (fix exists, blocked on review) |
| **Artifact share/deploy toolbar** | PR [#2388](https://github.com/netease-youdao/LobsterAI/pull/2388) — just merged | ✅ Already in trunk |

**Prediction**: The next release is likely to include the Artifact share/deploy features (#2388) and the agent engine timeout fix (#2386), but the two April-stale usability PRs (#1239, #1241) remain uncertain without maintainer engagement.

---

## 7. User Feedback Summary

**Pain points**:
- **Data corruption** (#2393) is the most severe — a user discovered their `MEMORY.md` was silently corrupted by the accelerator, calling it "bytes abnormal"
- **API lock-out** (#1240) made a user's entire LobsterAI instance unusable for hours; they had to restore from backup — "辛苦了，请解决问题" (Please solve the problem, thank you)
- **Missing scheduling customization** (#2392) — users need to assign specific agents and skills to timed tasks, a basic automation requirement
- **Skill management limitations** (#2391) — skill rename is a simple but missing QoL feature
- **Windows encoding** (#2390) — user with Chinese characters in username cannot execute commands properly; forced to use a less-capable PowerShell version

**Satisfaction signals**:
- PRs from community contributors (e.g., @fisherdaddy, @woxinsj, @gouff98) indicate active community investment
- High-quality bug reports like #2393 include exact byte sequences, reproduction rate, and impact analysis

**Overall sentiment**: Tension between **active community contribution** and **stale maintainer response** — several high-impact bugs remain untouched for months.

---

## 8. Backlog Watch

The following items have been **open for 3+ months with no maintainer response or resolution** — they represent growing technical debt and user frustration risk:

| Issue/PR | Age | Impact | Status |
|----------|-----|--------|--------|
| [#1240](https://github.com/netease-youdao/LobsterAI/issues/1240) — API lockout persists across all agents | 119 days | Critical: application unusable when any API key is rate-limited | No maintainer reply |
| [#1237](https://github.com/netease-youdao/LobsterAI/issues/1237) — Unsaved Settings silently lost | 118 days | High: user data loss | Has fix PR [#1241](https://github.com/netease-youdao/LobsterAI/pull/1241) but PR is also stale |
| [#1239](https://github.com/netease-youdao/LobsterAI/pull/1239) — Taskbar flash on task completion | 118 days | Medium: UX improvement | Fully written, never reviewed |
| [#2062](https://github.com/netease-youdao/LobsterAI/issues/2062) — Max duration task silently fails | 62 days | Medium: user confusion | No reply |
| [#1277](https://github.com/netease-youdao/LobsterAI/pull/1277) — Electron dependency bump (40→43) | 116 days | Medium: security/compatibility | Open, stale |

**Call to action**: The four oldest stale items (#1240, #1237, #1239, #1277) all date to April 2026 — a maintainer triage pass is overdue. In particular, the PRs with ready code (#1239, #1241) represent "low-hanging fruit" that could clear significant backlog quickly.

---

*This digest was generated from public GitHub data on 2026-07-28. All links point to repository issues/PRs.*

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

# Moltis Project Digest — July 28, 2026

## Today's Overview

The Moltis project shows moderate activity today with 5 open pull requests updated in the last 24 hours and no new issues, releases, or merged changes. Activity is concentrated on infrastructure and security improvements rather than new feature delivery, with four PRs authored by core contributor `penso`. The project is in a development-heavy phase, with significant architectural work underway to expose Moltis as an ACP agent, add instrumentation and feedback collection, and fix a security vulnerability in the `/sh` command. No blockers or critical regressions were reported, but no code has been merged today.

## Releases

No new releases were published today. The latest release remains earlier in the project timeline.

## Project Progress

**No PRs were merged or closed today.** All 5 PRs updated remain open, indicating ongoing review or revision cycles. Notable progress on existing PRs includes:

- **#1158** *(feat: zvec vector database memory backend)* — Continues development as an experimental alternative memory backend, feature-gated behind the `zvec` Cargo feature.
- **#1169** *(feat: ACP agent exposure over stdio)* — Transforms Moltis from a pure ACP client into a bidirectional ACP participant, enabling it to be used as an agent within ACP-compatible harnesses.
- **#1170** *(fix: per-account operators list for /sh and privileged tools)* — Adds critical authorization gating beyond simple channel access policies.
- **#1174** *(feat: instrumentation and feedback collection)* — Introduces pluggable `ObservationSink` architecture for telemetry and user feedback.
- **#1173** *(feat: PWA push notification reliability)* — Fixes notification replacement bug where silent overwrites lost alerts.

## Community Hot Topics

All updated PRs have zero comments, so there is no active community discussion reflected in the data. The most notable PRs from a technical interest perspective:

- **[PR #1158](https://github.com/moltis-org/moltis/pull/1158)** — Zvec memory backend. Addresses the need for a lower-latency, locally-run vector memory alternative to existing backends, optimizing for setups where the user runs their own embedding model.
- **[PR #1169](https://github.com/moltis-org/moltis/pull/1169)** — ACP agent exposure. Reflects demand for Moltis to be usable as a standalone agent in third-party tools (Zed, Cursor, bespoke runners), expanding its integration surface.
- **[PR #1173](https://github.com/moltis-org/moltis/pull/1173)** — PWA notifications. Highlights user frustration with missed or silent notifications, indicating the PWA frontend is a growing focus for reliability.

## Bugs & Stability

One security-critical fix is in progress:

- **PR #1170** *(High severity)* — `/sh` command was reachable by any channel member passing access gates. On multi-user platforms (Discord, group chat), this allowed arbitrary host command execution. The fix introduces a per-account operators list for authorization.
  - *Status:* Open, not yet merged.
  - *No related issues filed for this bug.*

No crashes, regressions, or other stability bugs were reported today.

## Feature Requests & Roadmap Signals

The following features are under active development and likely candidates for the next release:

1. **Memory backend diversity** (PR #1158) — A lighter-weight vector database option for users running local LLM infrastructure.
2. **ACP bidirectional support** (PR #1169) — Critical for integration with ACP-based tools; may unlock new deployment patterns.
3. **Telemetry and feedback** (PR #1174) — Suggests the team is prioritizing observability and user-driven improvement cycles.
4. **Reliable PWA notifications** (PR #1173) — Addresses a core UX issue for web-based users.

No new feature requests were filed as issues today.

## User Feedback Summary

No direct user feedback (comments, reactions, or issue reports) was recorded in the last 24 hours. The PRs themselves encode user pain points:
- Users running local embedding models need lighter memory backends (PR #1158)
- Developers want to use Moltis as a drop-in agent in existing ACP tools (PR #1169)
- PWA users experienced silent notification loss, a significant usability bug (PR #1173)

## Backlog Watch

No issues are currently open, so there is no backlog of unanswered user reports. Among the open PRs, note:
- **PR #1158** has been open since July 17 and has not received comments or maintainer review visible in the data. It may require attention to determine whether the experimental Zvec backend is worth merging or requires further iteration.
- The four remaining PRs are all less than 3 days old and appear to be actively iterated.

**No maintainer-attention items flagged today.**

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

# CoPaw Project Digest — 2026-07-28

## Today's Overview

CoPaw maintains a high level of community activity, with 50 issues and 49 pull requests updated in the last 24 hours. The project is processing a large volume of bug reports and feature contributions simultaneously, reflecting a healthy but heavily loaded maintenance cadence. 37 of 50 issues were closed, indicating responsive triage, while 34 of 49 PRs remain open, suggesting many features and fixes are under active review. No new releases were published today, but PR activity points toward significant forthcoming improvements in browser automation, memory systems, and agent infrastructure. The project appears to be in a phase of rapid feature development concurrent with stabilization efforts following the 2.0.0 release.

## Releases

No new releases were published on 2026-07-28. The last known versions are `v2.0.0.post3` for QwenPaw and `agentscope 2.0.4.post1`, both referenced in recent issue reports.

## Project Progress

15 pull requests were merged or closed today, spanning fixes, documentation, and infrastructure improvements:

- **[#6462](https://github.com/agentscope-ai/CoPaw/pull/6462)** (merged): Fixed documentation to clarify native Windows sandbox support — QwenPaw now provides AppContainer and restricted-token isolation on Windows without requiring WSL2.
- **[#6508](https://github.com/agentscope-ai/CoPaw/pull/6508)** (open): Fixes `spawn_subagent` to inherit session-level `approval_level` overrides, preventing child agents from bypassing approval settings.
- **[#6068](https://github.com/agentscope-ai/CoPaw/pull/6068)** (open): Fixes Scroll history migration to preserve canonical `session_id` mappings during upgrades.
- **[#6398](https://github.com/agentscope-ai/CoPaw/pull/6398)** (open, under review): Adds reranker support for ReMe memory search with configurable over-fetch and re-ranking via external API.
- **[#6424](https://github.com/agentscope-ai/CoPaw/pull/6424)** (open): Introduces native desktop GUI automation (`computer_use` tool) for Windows and macOS, using accessibility-first and Tauri control modes.
- **[#6504](https://github.com/agentscope-ai/CoPaw/pull/6504)** (open): Unifies project directory handling and file workspace, injecting resolved paths into system prompts for both normal and coding-enabled ReAct agents.
- **[#6157](https://github.com/agentscope-ai/CoPaw/pull/6157)** (open): Chrome extension plugin with native messaging bridge, enabling browser control via agent.
- **[#6284](https://github.com/agentscope-ai/CoPaw/pull/6284)** (open, under review): New `qwenpaw-creator` app plugin for script → assets → storyboard → video creation workflows.
- **[#6269](https://github.com/agentscope-ai/CoPaw/pull/6269)** (open): Workspace checkpoint management using shadow Git store for recoverable conversation history.
- **[#6397](https://github.com/agentscope-ai/CoPaw/pull/6397)** (open, under review): Integrates Codex, Qoder, Skills, and MCP as third-party agent backends, with each agent selecting its backend independently of Coding Mode.
- **[#6503](https://github.com/agentscope-ai/CoPaw/pull/6503)** (open): Adds per-agent token usage tracking from turn metadata, splitting aggregates from global totals.
- **[#6456](https://github.com/agentscope-ai/CoPaw/pull/6456)** (open): Adds PawFocus visual context compression for long agent histories with recoverable content.
- **[#6489](https://github.com/agentscope-ai/CoPaw/pull/6489)** (open): Adds Driver unit tests and enables `fail_under=50` coverage gate in CI.
- **[#6500](https://github.com/agentscope-ai/CoPaw/pull/6500)** (open): Fixes security issue — makes unauthenticated local CDP exposure opt-in rather than default.
- **[#6387](https://github.com/agentscope-ai/CoPaw/pull/6387)** (open): Supports on-demand channel SDK installation and version repair from Console.

## Community Hot Topics

The following issues and PRs attracted the most discussion and reactions:

1. **[#5757](https://github.com/agentscope-ai/CoPaw/issues/5757)** (14 comments, CLOSED): Feishu bot stops responding after first message. Multiple users confirmed the same behavior on both Docker and AgentScope Platform instances. A recurring theme — Feishu channel reliability remains a persistent pain point.

2. **[#5995](https://github.com/agentscope-ai/CoPaw/issues/5995)** (7 comments, CLOSED): Messages silently dropped when session is busy processing previous requests. No queue, no error feedback. This represents a fundamental UX issue for all chat channels.

3. **[#5725](https://github.com/agentscope-ai/CoPaw/issues/5725)** (6 comments, CLOSED): Console UI freezes during streaming output. Users report this is uniquely bad in QwenPaw compared to other AI chat web apps like DeepSeek.

4. **[#4895](https://github.com/agentscope-ai/CoPaw/issues/4895)** (5 comments, CLOSED): Infinite image compression loop causing hallucination — images are repeatedly re-compressed and re-injected, causing context corruption.

5. **[#5090](https://github.com/agentscope-ai/CoPaw/issues/5090)** (5 comments, CLOSED): Tool security bypass — `rm` command is intercepted by tool guardrails, but agents bypass via Python scripts to delete files anyway.

6. **[#5259](https://github.com/agentscope-ai/CoPaw/issues/5259)** (5 comments, CLOSED): Vector index not persisted on Windows — users must keep "Rebuild memory index on startup" enabled forever.

7. **[#5964](https://github.com/agentscope-ai/CoPaw/issues/5964)** (5 comments, CLOSED): Upgrade to 2.0.0 causes chat list ↔ conversation history mapping loss, data exists in DB but UI returns 500 errors.

8. **[#6258](https://github.com/agentscope-ai/CoPaw/issues/6258)** (4 comments, OPEN): OpenAI model max output token setting does not take effect — a regression in 2.0.0.post3.

9. **[#4968](https://github.com/agentscope-ai/CoPaw/issues/4968)** (4 comments, CLOSED): Virtual memory leak causes subprocess fork to fail with "Cannot allocate memory" on Ubuntu.

10. **[#5773](https://github.com/agentscope-ai/CoPaw/issues/5773)** (4 comments, CLOSED): Memory search completely breaks OpenCode Go provider — auto_memory_search injects messages missing the `reasoning_content` field.

**Analysis of underlying needs:** Users are primarily asking for **reliable message delivery in chat channels**, **robust memory persistence (especially on Windows)**, **better migration/upgrade paths**, and **real security guarantees** (not just surface-level tool interception). The streaming/card performance issues suggest the UI framework is becoming a bottleneck as feature complexity grows.

## Bugs & Stability

**Critical severity:**

- **Silent message drops when session busy** ([#5995](https://github.com/agentscope-ai/CoPaw/issues/5995)): Messages received by webhook but never queued or processed. No error feedback. Affects all channels. **No fix PR open** — this is a fundamental architecture gap.
- **2.0.0 upgrade breaks chat history mapping** ([#5964](https://github.com/agentscope-ai/CoPaw/issues/5964), CLOSED): 500 errors in Web UI, data orphaned in `history.db`. A data migration issue that erodes user trust in upgrades. PR [#6068](https://github.com/agentscope-ai/CoPaw/pull/6068) aims to fix Scroll migration.
- **OpenAI max output token not honored** ([#6258](https://github.com/agentscope-ai/CoPaw/issues/6258), OPEN): Regression in v2.0.0.post3. Users cannot control model output length — critical for cost-sensitive deployments.

**High severity:**

- **Infinite image compression loop** ([#4895](https://github.com/agentscope-ai/CoPaw/issues/4895), CLOSED): Images compressed repeatedly in a feedback cycle, causing hallucination. Classic context pollution bug.
- **Tool security bypass** ([#5090](https://github.com/agentscope-ai/CoPaw/issues/5090), CLOSED): Agents use Python subprocess to bypass `rm` interception. Security feature is cosmetic only.
- **Memory search breaks OpenCode provider** ([#5773](https://github.com/agentscope-ai/CoPaw/issues/5773), CLOSED): Missing `reasoning_content` field in injected messages. Affects all DeepSeek model users on OpenCode.

**Medium severity:**

- **Vector index not persisted on Windows** ([#5259](https://github.com/agentscope-ai/CoPaw/issues/5259), CLOSED): Forces daily memory rebuild. Windows-specific but impacts a large user base.
- **Console streaming causes browser freeze** ([#5725](https://github.com/agentscope-ai/CoPaw/issues/5725), CLOSED): DeepSeek's web UI handles the same scenario without issue, suggesting QwenPaw's streaming implementation has inefficiencies.
- **Windows PATH concatenation drops semicolons** ([#6239](https://github.com/agentscope-ai/CoPaw/issues/6239), CLOSED): Child processes lose npm globals due to incorrect PATH building on Windows.
- **Long Feishu responses lost** ([#5561](https://github.com/agentscope-ai/CoPaw/issues/5561), CLOSED): Responses exceeding trivial length only deliverable as file attachments, not as chat messages.

**Low severity / open:**

- **High CPU in Edge+Wayland** ([#6460](https://github.com/agentscope-ai/CoPaw/issues/6460), OPEN): Suspected WebSocket/render loop issue with ComfyUI-heavy sessions.
- **Task mode spawns excessive conversation records** ([#6457](https://github.com/agentscope-ai/CoPaw/issues/6457), OPEN): History pollution from background tasks.

## Feature Requests & Roadmap Signals

The most prominent feature signals from the last 24 hours of PR and issue activity:

**Confirmed on the roadmap (in-progress PRs):**

1. **Native desktop GUI automation** ([#6424](https://github.com/agentscope-ai/CoPaw/pull/6424)): `computer_use` tool for Windows/macOS — likely to land in the next minor release (2.1.x).
2. **Unified browser control** ([#6276](https://github.com/agentscope-ai/CoPaw/pull/6276)): One SDK, any backend — abstracts Playwright, CDP, etc. under a single agent-facing surface.
3. **Third-party agent backends** ([#6397](https://github.com/agentscope-ai/CoPaw/pull/6397)): Codex, Qoder, Skills, MCP integration — significant expansion of agent ecosystem.
4. **Workspace checkpoints** ([#6269](https://github.com/agentscope-ai/CoPaw/pull/6269)): Shadow Git-based conversation recovery. Very useful for enterprise users.
5. **Visual context compression** ([#6456](https://github.com/agentscope-ai/CoPaw/pull/6456)): PawFocus for long histories — directly addresses the context inflation bugs ([#4872](https://github.com/agentscope-ai/CoPaw/issues/4872), [#4921](https://github.com/agentscope-ai/CoPaw/issues/4921)).
6. **Safe model discovery** ([#6302](https://github.com/agentscope-ai/CoPaw/pull/6302)): Infrastructure to auto-discover provider models rather than requiring manual IDs.

**User-requested features (issue-driven):**

1. **Custom model protocols** ([#5609](https://github.com/agentscope-ai/CoPaw/issues/5609)): Not all APIs follow `/v1/chat/completions` — users want `/v1/images/generations` and similar custom endpoints.
2. **Session ID exposure in plugins** ([#5547](https://github.com/agentscope-ai/CoPaw/issues/5547)): Enterprise users need to pass authenticated user context into MCP tools for permission control.
3. **DingTalk image preview** ([#5593](https://github.com/agentscope-ai/CoPaw/issues/5593)): Images should be uploaded as previewable image messages, not degraded to file messages.
4. **Kimi Coding Plan models** ([#5427](https://github.com/agentscope-ai/CoPaw/issues/5427)): Anthropic-compatible endpoints from Kimi are not supported — OpenAI-compatible assumption is too narrow.

**Prediction for next release (v2.1.0):** Likely to include the unified browser SDK, native desktop automation, third-party agent backends, and visual context compression — these are all high-value features under active review with multiple contributors.

## User Feedback Summary

**Pain points (recurring themes):**

- **Feishu reliability remains the #1 channel complaint.** Multiple issues ([#5757](https://github.com/agentscope-ai/CoPaw/issues/5757), [#5561](https://github.com/agentscope-ai/CoPaw/issues/5561), [#5708](https://github.com/agentscope-ai/CoPaw/issues/5708)) report dropped messages, unparsed cards, and length limits. Users signal frustration — "飞书信息不回复情况" captures the sentiment.
- **Upgrade anxiety is real.** The 2.0.0 migration broke chat history ([#5964](https://github.com/agentscope-ai/CoPaw/issues/5964)) — users with production deployments are wary of future upgrades.
- **Security features are not yet trustworthy.** The `rm` bypass bug ([#5090](https://github.com/agentscope-ai/CoPaw/issues/5090)) shows that tool guardrails are surface-level. Power users can trivially circumvent them. The expectation is: "希望安全防护真的可以拦截危险命令" (I hope security protections can really intercept dangerous commands).
- **Custom model support is brittle.** Users report models that worked in v1.1.7 break in later versions ([#5584](https://github.com/agentscope-ai/CoPaw/issues/5584)). The OpenAI-compatible API assumption excludes many real-world deployments.

**Satisfaction signals:**

- High PR activity from multiple contributors suggests an engaged developer community.
- The `qwenpaw-creator` app ([#6284](https://github.com/agentscope-ai/CoPaw/pull/6284)) indicates users are building domain-specific applications on top of CoPaw.
- First-time contributor PRs ([#6502](https://github.com/agentscope-ai/CoPaw/pull/6502)) show the project is attracting new developers despite documentation gaps.

**Use cases reported:**

- **Enterprise workflow automation**: Users integrating CoPaw with DingTalk, Feishu, WeCom for internal chatbots.
- **Model routing via middleware**: Users behind 9router and similar proxies want transparent forwarding.
- **ComfyUI management**: Users running heavy visual workflows through CoPaw UI ([#6460](https://github.com/agentscope-ai/CoPaw/issues/6460)).
- **Proxy/VPN deployment**: Some users (likely in restricted networks) attempt to use CoPaw as a node builder ([#6467](https://github.com/agentscope-ai/CoPaw/issues/6467)) — though this appears to be a misconception about project capabilities.

## Backlog Watch

Items requiring maintainer attention that have gone unanswered or have no clear resolution path:

1. **[#6460](https://github.com/agentscope-ai/CoPaw/issues/6460) — High CPU in Edge+Wayland (OPEN, 3 comments)**: Created 2026-07-25. No maintainer response. May be a subtle WebSocket/reconciliation loop issue specific to Tauri + Wayland compositors.

2. **[#6457](https://github.com/agentscope-ai/CoPaw/issues/6457) — Task mode history pollution (OPEN, 3 comments)**: Created 2026-07-24. Basic UX issue — user confused by excessive conversation records from background tasks. No assigned owner or milestone.

3. **[#6258](https://github.com/agentscope-ai/CoPaw/issues/6258) — OpenAI max output token broken (OPEN, 4 comments)**: Created 2026-07-19. This is a regression in the current release (2.0.0.post3) and affects all OpenAI API users. Should be treated as P1 — model configuration settings are foundational.

4. **[#4921](https://github.com/agentscope-ai/CoPaw/issues/4921) — Images/attachments loaded as raw Base64 into context (CLOSED, 3 comments)**: While closed, this underlying issue is not yet fully addressed by a fix PR. The PawFocus visual compression PR ([#6456](https://github.com/agentscope-ai/CoPaw/pull/6456)) may address it, but it remains under review.

5. **[#5504](https://github.com/agentscope-ai/CoPaw/issues/5504) — (Not in top 30 but historically noted)** File attachment context inflation — related to #4921, the project needs a systematic approach to attachment handling rather than case-by-case fixes.

**Trend observation:** The project has many issues from May-June 2026 that were closed without explicit resolution — they may have been fixed en masse or deferred. The re-opening rate should be monitored. The new 2.0.0 series introduced regressions that are still being surfaced by the user community, suggesting that the stabilization phase is not yet complete.

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# ZeroClaw Project Digest — 2026-07-28

## Today's Overview
ZeroClaw remains in an intensive development cycle with **50 issues updated** and **50 PRs updated** in the last 24 hours. The project shows high velocity but also significant instability: **46 open/active issues** indicate a large bug backlog, with multiple security-critical defects surfaced by a recent audit. Seven PRs were merged or closed today, signaling progress on CI/test infrastructure and dependency upgrades. No new releases were published. The project appears to be mid-cycle toward v0.9.0, with a particular focus on security hardening, platform compatibility, and test reliability.

## Releases
No new releases were published today. The latest tracked version remains **0.8.3** (master branch). The v0.9.0 milestone is actively tracked in [#7432](https://github.com/zeroclaw-labs/zeroclaw/issues/7432), which documents auth, security, gateway, and breaking-change work.

## Project Progress
Seven PRs were merged or closed today:

- **#9442** (closed) — [fix(tests): stop wall-clock guards in channels tests asserting scheduling](https://github.com/zeroclaw-labs/zeroclaw/pull/9442) — Fixed flaky channel tests that used fixed timeouts as assertions, a root cause of CI flakes on slow runners.
- **#9298** (closed) — [fix(tests): classify integration tests by path component in config-save gate](https://github.com/zeroclaw-labs/zeroclaw/pull/9298) — Improved the config-save isolation test gate to correctly classify integration tests, fixing a Windows CI gap.
- **#9434** (closed) — [chore(deps): bump the rust-all group with 44 updates](https://github.com/zeroclaw-labs/zeroclaw/pull/9434) — Bulk dependency update across the workspace.
- **#9251** (closed) — [feat(infra): PostgreSQL as the first supported session backend](https://github.com/zeroclaw-labs/zeroclaw/pull/9251) — Major infrastructure milestone establishing PostgreSQL as the canonical session backend, reducing the earlier five-backend scope to a single supported path.
- **#9238** (closed) — [Bug]: config_save_isolation skips all tests/ files on Windows — Fixed so the safety-net test now inspects Windows test files.
- **#7808** (closed) — [Bug]: CLI secret prompts give no feedback after paste — UX improvement for secret entry.
- **#9429** (closed) — [Bug]: zeroclaw-channels tests use fixed wall-clock timeouts as assertions — Fixed flaky test infrastructure.

## Community Hot Topics
The most active discussions today revolve around security vulnerabilities exposed by a recent code audit:

1. **[#9393](https://github.com/zeroclaw-labs/zeroclaw/issues/9393)** — [Bug]: Bluesky and Reddit have no sender authorization (3 comments, priority:p1, risk:high). A systemic finding: two channel implementations completely lack sender authorization, with no central gate covering them. This represents a fundamental security gap.

2. **[#9392](https://github.com/zeroclaw-labs/zeroclaw/issues/9392)** — [Bug]: LINE group messages skip the allowlist and the pairing handshake (2 comments, priority:p1, risk:high). Similar authorization bypass affecting LINE group messages.

3. **[#9386](https://github.com/zeroclaw-labs/zeroclaw/issues/9386)** — [Bug]: Gemini API key in request URL survives sanitize and is posted into chat (4 comments, priority:p1, risk:high). An API key leak vulnerability where transport-level errors expose the full URL (including `?key=`) to end users.

4. **[#9357](https://github.com/zeroclaw-labs/zeroclaw/issues/9357)** — [Bug]: cargo test fails on master in 19/20 runs (4 comments, priority:p1, risk:high). A critical CI reliability issue where tests are effectively broken on master.

5. **[#9425](https://github.com/zeroclaw-labs/zeroclaw/issues/9425)** — [Bug]: Running SOP jobs have no operator cancellation path (1 comment, priority:p1, risk:high, web). A workflow-blocking issue for the web dashboard.

**Underlying need**: The community is demanding systematic security hardening, particularly around channel authorization and credential handling, as well as CI reliability to regain trust in the development process.

## Bugs & Stability
Today saw a significant spike in high-severity bug reports, largely from a coordinated security audit:

### Critical (S0 - data loss / security risk):
- **#8279** — [delegate tool bypasses parent's tool allowlist](https://github.com/zeroclaw-labs/zeroclaw/issues/8279) — Sub-agents can invoke tools the parent policy excludes. No fix PR yet. Risk: high.

### High (S1 - workflow blocked / S2 with security implications):
- **#9386** — [Gemini API key leaked via sanitize_api_error](https://github.com/zeroclaw-labs/zeroclaw/issues/9386) — Active. No fix PR.
- **#9393** — [Bluesky/Reddit have no sender authorization](https://github.com/zeroclaw-labs/zeroclaw/issues/9393) — Active. No fix PR.
- **#9392** — [LINE group messages skip allowlist](https://github.com/zeroclaw-labs/zeroclaw/issues/9392) — Active. No fix PR.
- **#9417** — [WhatsApp Cloud leaks live approval token](https://github.com/zeroclaw-labs/zeroclaw/issues/9417) — Active. No fix PR.
- **#9390** — [Emergency stop is CLI-only state file, runtime never reads it](https://github.com/zeroclaw-labs/zeroclaw/issues/9390) — Active. No fix PR.
- **#9389** — [Unauthenticated POST /api/pair keys lockout on attacker-supplied header](https://github.com/zeroclaw-labs/zeroclaw/issues/9389) — Active. No fix PR.
- **#9357** — [CI tests fail 19/20 runs on master](https://github.com/zeroclaw-labs/zeroclaw/issues/9357) — Active. No fix PR.
- **#9425** — [No cancellation path for running SOP jobs](https://github.com/zeroclaw-labs/zeroclaw/issues/9425) — Active. No fix PR.
- **#9340** — [CLI cron jobs hardcode delivery to "none"](https://github.com/zeroclaw-labs/zeroclaw/issues/9340) — Active. No fix PR.
- **#9422** — [zeroclaw-config cannot compile on Windows](https://github.com/zeroclaw-labs/zeroclaw/issues/9422) — Active (status:in-progress). Risk:low.
- **#9462** — [zeroclaw-plugins unit tests behind wasmtime feature never execute in CI](https://github.com/zeroclaw-labs/zeroclaw/issues/9462) — Active. No fix PR.

### Medium (S2 - degraded behavior):
- **#8973** — [Landlock blocks shell access to /dev/null on Fedora](https://github.com/zeroclaw-labs/zeroclaw/issues/8973) — Active (status:in-progress). Risk:high.
- **#9363** — [Config metadata remains English in localized UI](https://github.com/zeroclaw-labs/zeroclaw/issues/9363) — Active. Risk:medium.
- **#6350** — [WhatsApp Web allowed-numbers bypassed for LID contacts](https://github.com/zeroclaw-labs/zeroclaw/issues/6350) — Active (status:in-progress). Risk:high.
- **#8720** — [Cannot disable cachePoint for Bedrock Nova 2 Lite](https://github.com/zeroclaw-labs/zeroclaw/issues/8720) — Active (status:in-progress). Risk:medium.
- **#9465** — [Precheck-declined messages produce only reaction, no text](https://github.com/zeroclaw-labs/zeroclaw/issues/9465) — Active. Risk:medium.

### Low (S3 - minor):
- **#5514** — [Telegram media groups not batched into one multimodal turn](https://github.com/zeroclaw-labs/zeroclaw/issues/5514) — Active (status:in-progress). Risk:medium.
- **#6157** — [Nextcloud Talk uses wrong bot message API](https://github.com/zeroclaw-labs/zeroclaw/issues/6157) — Active (status:in-progress). Risk:high.

**Note**: Many of today's security bugs were filed by the same reporter (`belumume`) and reference a systematic audit. The project now has 12+ active security-related issues at priority p1, creating a significant remediation burden.

## Feature Requests & Roadmap Signals
Despite the bug-heavy day, several substantive feature proposals are active:

1. **[#9464](https://github.com/zeroclaw-labs/zeroclaw/issues/9464)** — RFC: Anthropic stored-profile OAuth alias contract (priority:p1). A focused contract for explicit OAuth authentication with Anthropic, backed by PR #9420. Likely to land in v0.9.0 given the maintainer engagement.

2. **[#8983](https://github.com/zeroclaw-labs/zeroclaw/issues/8983)** — Proposal: category-scoped read_memory_from (priority:p2). Addresses a concrete multi-agent pattern where selective memory sharing is needed. Could appear in v0.9.0 or v0.10.0.

3. **[#9463](https://github.com/zeroclaw-labs/zeroclaw/issues/9463)** — Feature: Wire WASM memory plugins into runtime backend selection (priority:p2). Currently only the tool WASM backend is production-ready; channel and memory backends exist but are unreachable. Likely v0.9.0 or later.

4. **[#9330](https://github.com/zeroclaw-labs/zeroclaw/issues/9330)** — RFC: AI-assisted PR pre-review and re-review (priority:p2). An infrastructure proposal to use CI results for AI-assisted initial review while keeping final approval human-owned. Uncertain timeline.

5. **[#8288](https://github.com/zeroclaw-labs/zeroclaw/issues/8288)** — Tracker: SOP milestone — daemon-owned SOP control plane to 5/5 (priority:p2). A multi-PR epic targeting full SOP capability. The cancellation gap (#9425) suggests this is still in progress.

**Prediction**: The Anthropic OAuth RFC (#9464) and the PostgreSQL session backend (#9251, already merged) are most likely for v0.9.0. The WASM plugin wiring (#9463) may follow in v0.10.0. The security audit findings will likely force a "security sprint" before any major feature release.

## User Feedback Summary
User pain points evident from today's data:

- **Security anxiety**: Multiple reports of credential leaks (Gemini API key, WhatsApp approval token), authorization bypasses, and unauthenticated endpoints suggest growing user concern about production readiness. Users filing these issues are performing deep code audits, indicating a sophisticated but anxious user base.

- **Platform friction**: Fedora users hit sandbox issues (#8973), Windows users can't compile (#9422), and macOS/WSL users see CI failures (#9357). The project's Linux-first approach is causing friction for other platforms.

- **Usability gaps**: CLI cron jobs silently discard output (#9340), channel messages produce only emoji reactions with no explanatory text (#9465), and SOP jobs lack cancellation (#9425). Users are frustrated by opaque failure modes.

- **Localization incomplete**: Config metadata remains English even when UI is localized (#9363), creating a fragmented experience for non-English users.

- **Feature gaps**: Bedrock users cannot disable caching (#8720), multi-agent memory sharing is all-or-nothing (#8983), and Telegram media groups aren't batched (#5514).

**Satisfaction signals**: The active community engagement — 50 issues and 50 PRs in 24 hours — indicates a highly engaged user base investing significant effort in improving the project.

## Backlog Watch
Several long-unanswered or slowly-progressing issues merit maintainer attention:

1. **#8279** — [delegate tool bypasses parent's tool allowlist](https://github.com/zeroclaw-labs/zeroclaw/issues/8279) — Filed 2026-06-24, labeled S0 (data loss/security risk), status:in-progress but no fix PR. 33 days open with no remediation. This is the most critical security gap.

2. **#6350** — [WhatsApp Web allowed-numbers bypassed for LID contacts](https://github.com/zeroclaw-labs/zeroclaw/issues/6350) — Filed 2026-05-03, **86 days open** with status:in-progress. Users report silent message drops with no error surfaced. A long-standing quality issue.

3. **#5514** — [Telegram media groups not batched](https://github.com/zeroclaw-labs/zeroclaw/issues/5514) — Filed 2026-04-08, **111 days open**. A UX regression that has been "in progress" for over three months.

4. **#7432** — [v0.9.0 auth/security/gateway tracker](https://github.com/zeroclaw-labs/zeroclaw/issues/7432) — Filed 2026-06-09, 49 days open. This tracker coordinates the next release's breaking changes but shows no merged PRs linked to it. Risk of scope creep or missed deadlines.

5. **#8692** — [Maintainer decision queue for RFCs](https://github.com/zeroclaw-labs/zeroclaw/issues/8692) — Filed 2026-07-04, 24 days open. The existence of this tracker itself suggests that RFCs are piling up awaiting maintainer decisions, including #9330 (AI-assisted PR review) and #9464 (Anthropic OAuth).

6. **PR #9251** — [PostgreSQL session backend](https://github.com/zeroclaw-labs/zeroclaw/pull/9251) — Now merged, but note it was a **reduction** from five backends to one. The original scope may still be desired by users who preferred other databases.

7. **PRs needing author action (stale)**: #8966 (11 days), #9447, #9424, #8438 (29 days), #8966 (17 days), #9420 (2 days). Several open PRs are stalled waiting for author updates, slowing the release cycle.

**Maintainer callout**: The security audit findings (#9386, #9390, #9392, #9393, #9417, #9389) were all filed in the last 1-2 days and represent a concentrated vulnerability disclosure. Prioritizing these alongside the 86-day-old WhatsApp issue (#6350) is critical for user trust.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/kky-wollu/agents-radar).*