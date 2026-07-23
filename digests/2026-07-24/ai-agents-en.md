# OpenClaw Ecosystem Digest 2026-07-24

> Issues: 351 | PRs: 500 | Projects covered: 13 | Generated: 2026-07-23 23:01 UTC

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

# OpenClaw Project Digest — 2026-07-24

## Today's Overview

The project is experiencing **sustained high activity** with 351 issues and 500 pull requests updated in the last 24 hours. The open-to-closed ratio (254:97 issues, 316:184 PRs) indicates a **heavy review and triage workload**, with approximately 37% of PRs being merged or closed. No new releases were published today, but the large number of merged PRs (184) suggests preparations for a near-future release. Multiple P0 and P1 regressions remain open, including a critical gateway startup failure from the 2026.7.1 update that continues to block some users.

## Releases

No new releases were published in the last 24 hours. The latest available version remains **2026.7.2-beta.3** (referenced in bug reports). Users are reporting regressions in the 2026.7.x line, particularly around gateway startup, Telegram DM handling, and tool schema compatibility.

## Project Progress

**184 PRs were merged or closed today.** Notable merged changes include:

- **[PR #113155](https://github.com/openclaw/openclaw/pull/113155)** — Fixed CI sticky module rebuild for snapshot refresh (maintainer fix)
- **[PR #113157](https://github.com/openclaw/openclaw/pull/113157)** — Refactored gateway chat run state to unify parallel state maps (maintainer work by steipete)
- **[PR #113158](https://github.com/openclaw/openclaw/pull/113158)** — Telegram now renders rich Markdown lists natively (bullets, ordered, nested, checkbox)
- **[PR #113163](https://github.com/openclaw/openclaw/pull/113163)** — Fixed managed image replies rendering under base paths in Control UI
- **[PR #113154](https://github.com/openclaw/openclaw/pull/113154)** — Split the 2,821-line `dispatchReplyFromConfigInner` function into a config dispatch pipeline (significant maintainability improvement)
- **[PR #113088](https://github.com/openclaw/openclaw/pull/113088)** — Fixed benign same-generation session update claims for cron runs
- **[PR #113151](https://github.com/openclaw/openclaw/pull/113151)** — Fixed v13 agent databases failing to open on supported Node 22.22.3 and Node 24.15.0
- **[PR #113150](https://github.com/openclaw/openclaw/pull/113150)** — Merged creator avatar into sidebar leading slot, moved creator filter into Threads menu (UI cleanup)

**Open PRs advancing major features:**
- **[PR #113165](https://github.com/openclaw/openclaw/pull/113165)** — Converts heartbeat `tasks:` entries into independent cron jobs (Stage 4 of "everything is a cron" initiative)
- **[PR #113167](https://github.com/openclaw/openclaw/pull/113167)** — Prepares hot-path runtime facts to reduce redundant metadata rediscovery

## Community Hot Topics

The most active discussions today reflect **deep frustration with session reliability and silent failures**:

1. **[Issue #44925](https://github.com/openclaw/openclaw/issues/44925) — "Subagent completion silently lost"** (22 comments, Diamond Lobster rating)  
   This is the highest-traffic issue. Users report subagent orchestration has **multiple silent failure modes** where results are lost with no retry, notification, or auto-restart. Marked as stable branch impact with session-state and message-loss tags. The underlying need is for **observability and resilience in multi-agent workflows**.

2. **[Issue #102020](https://github.com/openclaw/openclaw/issues/102020) — "Second message in a session fails"** (15 comments)  
   A cross-channel regression where the second message always hits "reply session initialization conflicted." Users are hitting this on both Signal and other channels. This represents a **fundamental session lifecycle bug** that breaks the core user experience.

3. **[Issue #94228](https://github.com/openclaw/openclaw/issues/94228) — "Invalid signature in thinking block" on native Anthropic** (14 comments, Platinum Hermit)  
   Long tool-use threads permanently brick with HTTP 400 on the Anthropic provider path. This is a **critical blocking issue** for any users running multi-turn tool-use sessions on Anthropic's native API.

4. **[Issue #92043](https://github.com/openclaw/openclaw/issues/92043) — "180s compaction timeout bricks entire pipeline"** (13 comments, Diamond Lobster)  
   A wall-clock timeout with no partial-progress reuse causes legitimate long compactions to fail identically every turn. Users with long histories or slow providers are trapped in **crash loops**.

5. **[Issue #108435](https://github.com/openclaw/openclaw/issues/108435) — "Gateway fails to start w/ error"** (10 comments, P0, UX release blocker)  
   This regression from the 2026.7.1 update is currently the **highest-severity open issue**, preventing users from starting the gateway at all on systemd, Ollama, or manual launch.

## Bugs & Stability

**Critical (P0) open bugs:**

| Issue | Summary | Fix PR? |
|-------|---------|---------|
| [#108435](https://github.com/openclaw/openclaw/issues/108435) | Gateway fails to start on 2026.7.1 (systemd, Ollama, manual) | No open fix PR |
| [#90378](https://github.com/openclaw/openclaw/issues/90378) | Cron store migration from JSON to SQLite silently breaks channel delivery (P0, Platinum Hermit) | Linked PR open |

**High-severity (P1) open bugs:**

- **[#44925](https://github.com/openclaw/openclaw/issues/44925)** — Subagent completion silently lost (linked PR open, no fix PR)
- **[#94228](https://github.com/openclaw/openclaw/issues/94228)** — Native Anthropic "Invalid signature in thinking block" (linked PR open, needs live repro)
- **[#92043](https://github.com/openclaw/openclaw/issues/92043)** — Compaction timeout bricks entire pipeline (linked PR open)
- **[#108580](https://github.com/openclaw/openclaw/issues/108580)** — Cron tool schema incompatible with llama.cpp grammar-constrained tool calling (linked PR open)
- **[#111519](https://github.com/openclaw/openclaw/issues/111519)** — Telegram DM replies fall back after stale DM-scope cleanup on 2026.7.2-beta.3 (needs info)
- **[#98435](https://github.com/openclaw/openclaw/issues/98435)** — MCP loopback transport does not auto-reconnect after gateway restart (needs product decision)
- **[#101814](https://github.com/openclaw/openclaw/issues/101814)** — All channels enter broken state after 2026.6.11 update, one message per session then silence (needs live repro)

**Regressions reported today (all channels affected):**
- Control UI agent avatar + session list regressions in multi-agent setup ([#112696](https://github.com/openclaw/openclaw/issues/112696))
- Discord agents cannot access MCP tools ([#91799](https://github.com/openclaw/openclaw/issues/91799))
- Tool result channel becomes empty after several calls on 2026.7.1-beta.1 ([#99481](https://github.com/openclaw/openclaw/issues/99481))
- OpenAI model resolution bug: `opencode-go/kimi-k2.6` resolves to `deepseek-v4-pro` ([#98713](https://github.com/openclaw/openclaw/issues/98713))

## Feature Requests & Roadmap Signals

**High-community-support features likely in next release:**

1. **[#110950](https://github.com/openclaw/openclaw/issues/110950) "Everything is a cron"** (P2, 8 comments, 2 👍)  
   *Today's merged PR #113165* is Stage 4 of this unification. The maintainer (steipete) is actively building this, making it **very likely for the next release**. This is a fundamental architecture change.

2. **[#67419](https://github.com/openclaw/openclaw/issues/67419) Session context bloat — bootstrap files re-injected every turn** (P2, Diamond Lobster)  
   20-30% token waste on every turn is a high-impact fix that would benefit all users. Product decision pending.

3. **[#38568](https://github.com/openclaw/openclaw/issues/38568) Inject context window % into system prompt** (P3, 6 comments, 2 👍)  
   Agents that self-monitor context usage could dramatically improve behavior. Low complexity, high value.

4. **[#49259](https://github.com/openclaw/openclaw/issues/49259) Prune stale orphaned sessions from dashboard** (P2, stable branch)  
   Long-standing UX friction issue that would improve dashboard usability significantly.

5. **[#7524](https://github.com/openclaw/openclaw/issues/7524) groupScope option to consolidate group sessions into main** (P2, 5 comments, 4 👍)  
   Strong community demand (highest 👍 count of all feature requests this update).

**Prediction:** The "everything is a cron" unification (#110950) will likely land fully in 2026.7.x or 2026.8.x. Context bloat (#67419) and orphaned session cleanup (#49259) are candidates for the next minor release.

## User Feedback Summary

**Pain points (most frequently reported):**
- **Session reliability degradation**: Multiple users report sessions breaking after one message, silent failures, or permanent silence until restart — affects all major channels (Telegram, WhatsApp, Discord, WebChat)
- **Upgrade regressions**: Users consistently report that 2026.7.x updates break previously working configurations, particularly around gateway startup and message delivery
- **Lack of observability**: Multiple issues highlight silent failures with no logging, retries, or user notifications (subagent loss, compaction timeouts, MCP disconnect)
- **Local/self-hosted friction**: Users on non-systemd Linux, macOS, and resource-constrained VPS report crashes, stalls, and missing platform support

**Satisfaction signals:**
- Active community engagement with 851 total updated items in 24 hours demonstrates **high adoption and usage**
- Multiple users contributing detailed bug reports with reproduction steps, logs, and even fixing code (e.g., PRs from community members LavyaTandel, MatthewSynthia, Sanjays2402)
- The project is being used in production environments (VPS deployments, team/org setups, multi-agent Telegram bots)

**Notable use case: Self-hosted production deployments**
- User [#41372](https://github.com/openclaw/openclaw/issues/41372) contributed 25 findings from 4 weeks of production use on a 2GB VPS with Telegram, Discord, and cron jobs — indicating real-world production adoption with specific pain points around resource limits and automated tasks.

## Backlog Watch

**Critical long-unanswered issues needing maintainer attention:**

| Issue | Age | Duration | Urgency |
|-------|-----|----------|---------|
| [#42820](https://github.com/openclaw/openclaw/issues/42820) Feishu message tool pollution | 2026-03-11 | ~4.5 months | P1, Platinum Hermit — needs live repro |
| [#43374](https://github.com/openclaw/openclaw/issues/43374) All LLM API calls time out simultaneously | 2026-03-11 | ~4.5 months | P1, Platinum Hermit — multi-agent concurrency bug |
| [#42273](https://github.com/openclaw/openclaw/issues/42273) backup create stalls on large installations | 2026-03-10 | ~4.5 months | P2, Platinum Hermit — affects production users |
| [#41372](https://github.com/openclaw/openclaw/issues/41372) 25 findings from 4 weeks production use | 2026-03-09 | ~4.5 months | P2, Platinum Hermit — comprehensive field report |
| [#48641](https://github.com/openclaw/openclaw/issues/48641) Discord DMs silently dropped | 2026-03-17 | ~4 months | P2, Platinum Hermit — inbound messages lost |
| [#49205](https://github.com/openclaw/openclaw/issues/49205) Control UI messages not appearing in Open WebUI | 2026-03-17 | ~4 months | P2, Platinum Hermit — shared context inconsistency |

**Watch list — open PRs that have stalled:**
- **[#101981](https://github.com/openclaw/openclaw/issues/101981) Signed ClawHub default feed trust** — P2, needs proof, open since 2026-07-08
- **[#111541](https://github.com/openclaw/openclaw/issues/111541) Localization context and message rendering** — P2, needs proof, open since 2026-07-19

**Next steps for maintainers:** The backlog contains several **4+ month old P1/P2 issues** with Platinum Hermit ratings covering session loss, silent failures, and multi-agent concurrency — these represent systemic stability concerns that compound as adoption grows.

---

## Cross-Ecosystem Comparison

# Cross-Project Ecosystem Comparison Report
**Date:** 2026-07-24

## 1. Ecosystem Overview

The personal AI assistant open-source ecosystem is experiencing **explosive growth**, with the seven tracked projects collectively processing over 500 issues and 650 pull requests in a single 24-hour period. The landscape is bifurcating into **two tiers**: mature, community-driven platforms (OpenClaw, ZeroClaw) that are grappling with scale and regression management, and newer or more focused projects (Moltis, NanoBot, PicoClaw) that are iterating rapidly on security and channel integration. A notable shift is underway from single-agent architectures toward **multi-agent orchestration**, with every project that has published metrics showing user demand for subagent delegation, cron-based automation, and cross-channel reliability. The core tension across the ecosystem is between **feature velocity and stability**—users consistently report frustration with regressions introduced by rapid release cycles, particularly around session lifecycle management and message delivery guarantees.

## 2. Activity Comparison

| Project | Issues Updated | PRs Updated | Release Status | Health Signal |
|---------|---------------|-------------|----------------|---------------|
| **OpenClaw** | 351 (254 open) | 500 (316 open) | Latest: 2026.7.2-beta.3 | **High activity, strained** — 37% PR closure rate, critical P0 regressions, high community engagement |
| **ZeroClaw** | 50 (39 open) | 50 (47 open) | Latest: v0.8.3 | **Intense sprint** — 3 S0 data-loss bugs with immediate fix PRs, 11 issues closed, major feature completions |
| **Hermes Agent** | 50 (43 open) | 50 (47 open) | No new release | **High volume, moderate throughput** — only 3 PRs merged vs 50 updated, maintainer bandwidth concern |
| **CoPaw** | 35 (14 open) | 50 (29 open) | Latest: v2.0.1-beta.2 | **Healthy post-release** — 21 PRs merged, strong fix velocity, but v2.0 performance regression is top complaint |
| **NanoBot** | 8 (4 open) | 38 (8 open) | No new release | **Strong maintenance push** — 30 PRs merged, security hardening focus, likely pre-release |
| **PicoClaw** | 1 (triggered) | 15 (8 open) | No new release | **Moderate, dependency-heavy** — 7 PRs merged but mostly automated bumps; 2 human-authored features |
| **IronClaw** | 32 (22 open) | 50 (40 open) | No new release | **Pre-v1 launch sprint** — 10 PRs merged, 10+ v1-launch checklist items, high engineering intensity |
| **Moltis** | 2 (1 open) | 5 (0 open) | Released: 20260723.02/.03 | **Stable, low activity** — 5 PRs merged, 2 releases, only 1 open bug (Podman) |
| **NanoClaw** | 1 (1 open) | 10 (6 open) | No new release | **Stable with fix velocity** — 4 PRs merged, Matrix E2EE is major architectural win |
| **LobsterAI** | 3 (3 open) | 3 (2 merged) | Latest: v2026.7.20 | **Maintenance phase** — 3 stale issues since April 2, no maintainer responses; community concern |
| **ZeptoClaw** | 2 (2 open) | 1 (1 open) | No new release | **Maintenance cycle** — focused on 2 critical bugs (credential leak, CI restoration) |
| **TinyClaw** | — | — | — | **Inactive** — no activity in 24h |
| **NullClaw** | — | — | — | **Inactive** — no activity in 24h |

## 3. OpenClaw's Position

**Advantages over peers:**
- **Unmatched scale**: 851 total updated items in 24 hours—over **3x the next largest project** (ZeroClaw at ~100). This reflects the largest user base, most active contributor ecosystem, and richest integration ecosystem (Telegram, Discord, WhatsApp, Signal, WebChat, cron)
- **Architecture maturity**: The "everything is a cron" initiative (Stage 4 merging today) represents a fundamental architecture unification that no other project has attempted. The 2,821-line function refactor into a config dispatch pipeline demonstrates engineering discipline at scale
- **Channel diversity**: Telegram rich Markdown native rendering, Control UI agent avatar overhaul, and managed image replies—OpenClaw leads in channel polish

**Technical approach differences:**
- OpenClaw uses a **gateway-based architecture** with pluggable channels, whereas NanoBot and CoPaw use **sidecar/backend process models**. This gives OpenClaw more flexibility but introduces the session lifecycle bugs that are its top pain point
- Unlike ZeroClaw's Rust-based core or IronClaw's WASM-focused approach, OpenClaw maintains a **JavaScript/TypeScript ecosystem**, which lowers the barrier for community contributions but creates performance ceiling concerns

**Community size comparison:**
- OpenClaw dominates by raw volume: 351 issues vs next-highest 50 (ZeroClaw, Hermes Agent). PR volume is 10x the median project
- However, **satisfaction signals are mixed**: the #1 issue (subagent completion silently lost, 22 comments) reflects deep frustration with reliability that smaller projects like Moltis and NanoBot have avoided by being more conservative with releases

## 4. Shared Technical Focus Areas

The following requirements are emerging across **three or more projects** simultaneously:

| Requirement | Affected Projects | Specific Need |
|-------------|------------------|---------------|
| **Multi-agent orchestration reliability** | OpenClaw (#44925), Hermes Agent (#70294), ZeroClaw (#2767), LobsterAI (#1265) | Subagent results silently lost, delegation reliability, per-agent model binding |
| **Session lifecycle correctness** | OpenClaw (#102020), CoPaw (#6401), Hermes Agent (#64488), LobsterAI (#1273) | Session initialization conflicts, history overwrites by cron, leaked TUI sessions, database corruption |
| **Security hardening & credential isolation** | NanoBot (PR #4594, #4987), Hermes Agent (#69449), ZeptoClaw (#644), ZeroClaw (#9127), IronClaw (#6596) | Shell injection bypass, plaintext API keys, subprocess credential leaks, TOCTOU race conditions |
| **Container/docker deployment UX** | CoPaw (#6344), Moltis (#1095), NanoClaw (#2466), OpenClaw (#108435) | Long update cycles, Podman support, duplicate container spawns, gateway startup failures |
| **Multi-platform WebUI parity** | Hermes Agent (#63679, #69687), ZeroClaw (#9198), OpenClaw (#112696), CoPaw (#6307) | Desktop rendering regressions, webhook management, typing indicator bugs, v2.0 performance overhead |
| **Agent tool reliability (MCP/Llama)** | OpenClaw (#108580), NanoBot (PR #5057), CoPaw (#6405), ZeroClaw (#9207) | Schema incompatibility, MCP tool not found, compressed responses not decoded |
| **Observability & diagnostics** | OpenClaw (#44925), Hermes Agent (#70058), ZeroClaw (#9228), CoPaw (#6392) | Silent failures, no warning on compression blocking, per-agent token stats, eval dashboards |

## 5. Differentiation Analysis

| Dimension | OpenClaw | ZeroClaw | Hermes Agent | CoPaw | NanoBot | IronClaw | Moltis |
|-----------|----------|----------|--------------|-------|---------|----------|--------|
| **Core language** | TypeScript/JS | Rust | TypeScript | TypeScript | Python | Rust + WASM | Go |
| **Target user** | Hobbyist to production | Power user, enterprise | Developer, researcher | End-user, desktop | Developer, security-aware | Early adopter | Sysadmin, team |
| **Deployment model** | Gateway + channels | Daemon + channels | Desktop + CLI | Desktop + Docker | CLI + WebUI | Cloud + local | Docker, binary |
| **Multi-agent model** | Subagent orchestration | Profile routing, A2A | Async delegation | CoWork sessions | Agent loop | Skill routing | Per-agent config |
| **Memory system** | Session context | File-based, ReMe | Hindsight + Honcho | ReMe memory | Simple context | Runtime facts | Context command |
| **Release cadence** | Weekly betas | Milestone-based | Irregular | Bi-weekly patches | Pre-release spikes | Pre-v1 sprint | Daily patches |
| **Security posture** | Moderate (P0 bugs open) | Strong (sprint-focused) | Improving (campaign) | Governance policies | Hardening (shell guards) | Early stage | Strong (OTP allowlists) |

**Key architectural differences:**
- **ZeroClaw** is the only project building Agent-to-Agent (A2A) protocol interoperability, positioning it as the most future-proof for multi-agent ecosystems
- **IronClaw** takes a unique WASM-first approach with "attested signing" for skill verification, targeting a more trust-oriented deployment model
- **NanoBot** prioritizes workspace isolation with multiple layers of shell injection protection—no other project has this depth of security-by-boundary design
- **Moltis** ships daily patches and has the cleanest bug dashboard (1 open bug), reflecting a conservative, ops-first philosophy that prizes stability over features

## 6. Community Momentum & Maturity

**Tier 1 — High Velocity, Scaling Challenges:**
- **OpenClaw** (851 items/day) is the ecosystem anchor. Activity is **10x median**, but the open-to-closed ratio (37% PR closure, 28% issue closure) indicates **triage is a bottleneck**. Multiple P0/P1 bugs are 4+ months old. The project is in danger of "growth implosion" unless maintainer bandwidth scales.
- **ZeroClaw** (~100 items/day) is in a **security sprint** with rapid fix creation (3 S0 bugs → immediate PRs). The close of 11 long-standing issues (Multi-Agent Routing, Discord filtering) shows strong project leadership. The main risk is PR review queue (47 open vs limited merging).

**Tier 2 — Active Development, Specific Focus:**
- **CoPaw** (85 items/day) is in a **healthy post-v2.0 iteration cycle** (21 PRs merged) but the 2s performance regression (#6307) is the #1 user complaint—a fix is critical to prevent user exodus.
- **Hermes Agent** (100 items/day) has **high volume but low throughput** (only 3 PRs merged from 50 updated). This signals either code complexity slowing reviews or maintainer bandwidth issues.
- **IronClaw** (82 items/day) is in an **intense pre-v1 launch sprint** with 10 PRs merged. The "Remove Reborn" branding initiative and signature substrate revival suggest a major announcement is imminent.

**Tier 3 — Stable, Conservative Iteration:**
- **NanoBot** (46 items/day) shows **high merge efficiency** (30/38 PRs closed), indicating disciplined project management. Likely near a release.
- **Moltis** (7 items/day) is the **most stable project**—5 PRs merged, 2 releases, 1 open bug. Low noise but steady improvement.
- **PicoClaw** (16 items/day) is **dependency-driven**—most activity is automated bumps. The 23-day-old unreviewed fallback chain feature PR risks contributor demotivation.

**Tier 4 — Stalled/Maintenance:**
- **LobsterAI** (6 items/day) has **3 stale issues since April 2 with zero maintainer response**. The WASM memory corruption bug (#1273) is a critical risk that's being ignored. Contributor trust is likely eroding.
- **ZeptoClaw**, **TinyClaw**, **NullClaw** show minimal to no activity—these projects may be in hibernation or winding down.

## 7. Trend Signals

**1. Security is the #1 cross-cutting concern** — Seven of ten active projects have security-related items in their top-priority lists. The pattern is consistent: shell injection, credential leakage, TOCTOU races, SSRF vulnerabilities. For AI agent developers, **sandboxing is no longer optional**—every project that ships tool execution capabilities is being forced to harden boundaries.

**2. Session lifecycle is the reliability bottleneck** — OpenClaw (#102020), CoPaw (#6401), Hermes Agent (#64488), and LobsterAI (#1273) all report bugs where sessions fail, duplicate, or corrupt. This is the **Achilles' heel of multi-turn AI agents**. Developers building on these frameworks should invest in idempotent session handling and crash recovery from day one.

**3. Multi-agent orchestration is becoming table-stakes** — Four projects (OpenClaw, ZeroClaw, Hermes Agent, LobsterAI) have active feature work or blocking bugs around subagent delegation, routing, or per-agent model binding. The community is moving from "one agent that does everything" to "many specialized agents." The A2A protocol work in ZeroClaw (#3566) and the "everything is a cron" initiative in OpenClaw are the most ambitious architectural responses.

**4. Docker deployment friction is a growth limiter** — CoPaw's 1.5-hour HDD update cycles, NanoClaw's duplicate container spawns, OpenClaw's gateway startup regression—these are not niche complaints. **Self-hosted agent deployments are going mainstream**, and projects that don't invest in Docker/container ergonomics will lose users to those that do.

**5. The "fast releases, break frequently" model is generating backlash** — CoPaw users (#6376) explicitly complain about insufficient testing before patches. OpenClaw users report 2026.7.x upgrades breaking previously working setups. LobsterAI's stale issues suggest users have stopped reporting bugs because they don't expect fixes. **The ecosystem is sending a clear signal: stability > features for production users.**

**6. Memory/persistence architecture is diversifying** — Projects are pursuing different memory strategies: ZeroClaw adds PostgreSQL backend for HA deployments, CoPaw introduces ReMe with reranking, Hermes Agent debates synchronous vs async recall, OpenClaw works on "hot-path runtime facts." This is a **healthy experimentation phase**—the approaches that emerge will define best practices for the next generation of AI agents.

**7. Desktop/CLI parity is an emerging battleground** — Hermes Agent's CLI code copy-to-clipboard (PR #4883, 4 months in the making), ZeroClaw's logging stream fix (#4721), and CoPaw's console performance work (#6393) all reflect a growing community that **uses these agents as daily drivers**, not just demos. The quality of the command-line and desktop experience is becoming a retention factor.

---

## Peer Project Reports

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

Here is the NanoBot project digest for July 24, 2026.

---

## NanoBot Project Digest for 2026-07-24

### 1. Today's Overview
NanoBot experienced a high volume of development activity today, with 38 Pull Requests updated (30 merged/closed) and 8 Issues updated (4 closed). This indicates a strong maintenance and feature push by the core team. Key areas of focus included security hardening for file system and command execution boundaries, simplification of the WebUI model preset settings, and stability fixes for session management and channel connectivity. The project currently has no new formal releases, but the volume of merged PRs suggests a significant release may be imminent.

### 2. Releases
**None.**
No new releases were published today. However, the high merge velocity (30 PRs) strongly suggests a release candidate is building.

### 3. Project Progress
The following significant PRs were merged or closed today, representing concrete improvements to the codebase:

- **WebUI Model Settings Overhaul:** PR [#5061 (CLOSED)](https://github.com/HKUDS/nanobot/pull/5061) (chengyongru) replaced the confusing "current configuration" workflow with reusable model presets and explicit call ordering, simplifying the user experience.
- **Security & Workspace Guarding:**
    - PR [#4594 (CLOSED)](https://github.com/HKUDS/nanobot/pull/4594) (axelray-dev) fixed a critical shell injection bypass where absolute paths after an `=` sign (e.g., `--output=/etc/passwd`) were not checked against workspace boundaries.
    - PR [#4889 (CLOSED)](https://github.com/HKUDS/nanobot/pull/4889) (hamb1y) added an allowlist for destructive priority commands (`/restart`, `/stop`) to prevent non-admin chat users from executing them.
    - PR [#4987 (OPEN)](https://github.com/HKUDS/nanobot/pull/4987) (KDB-Wind) is an open but crucial "P0" security fix that binds workspace checks to opened file handles to prevent TOCTOU (time-of-check time-of-use) attacks.
- **Session & Stability Fixes:**
    - PR [#5068 (CLOSED)](https://github.com/HKUDS/nanobot/pull/5068) (KDB-Wind) fixed a `FileNotFoundError` crash in `SessionManager.list_sessions()` when files are removed concurrently.
    - PR [#5066 (CLOSED)](https://github.com/KDB-Wind) (KDB-Wind) ensures stale exec sessions are retained after a cleanup failure, allowing for a later retry instead of data loss.
    - PR [#5055 (CLOSED)](https://github.com/HKUDS/nanobot/pull/5055) (santhreal) fixed a hang in the Telegram channel when splitting long single-line code fences.
- **Agent Functionality:**
    - PR [#5056 (OPEN)](https://github.com/HKUDS/nanobot/pull/5056) (chengyongru) addresses a critical bug where output was lost during "length recovery" (when a model response is truncated by token limits).
- **Document Handling:** PR [#5039 (CLOSED)](https://github.com/HKUDS/nanobot/pull/5039) (Re-bin) fixed DOCX parsing to preserve table content, making table-based forms accessible to the agent.
- **MCP Compatibility:** PR [#5057 (OPEN)](https://github.com/HKUDS/nanobot/pull/5057) (amplifierplus) fixes an issue where MCP tools with non-standard JSON Schema references would cause providers like Kimi/Moonshot to reject entire requests.

### 4. Community Hot Topics
- **Issue #4253** (CLOSED, 6 comments): "Support overriding model per conversation" by rombert. This was a highly requested feature to allow users to switch between a fast cloud model (OpenRouter) and a private local model (llamacpp) within the same conversation. While closed, it signals a strong desire for flexible model routing. [Link](https://github.com/HKUDS/nanobot/issues/4253)
- **Issue #5059** (CLOSED, 4 comments): "都支持各个浏览器的什么版本" by qteamo. A Chinese-language request asking for explicit browser version compatibility for the WebUI. The user expressed a desire for better documentation or wider testing. [Link](https://github.com/HKUDS/nanobot/issues/5059)
- **PR #5069 (OPEN)**: "fix(channels): ignore confirmations after connect cancellation" by KDB-Wind. This addresses a security concern where a cancelled WeChat/Feishu QR code connection could still save credentials if a late confirmation arrived. This touches on user trust and security. [Link](https://github.com/HKUDS/nanobot/pull/5069)

### 5. Bugs & Stability
- **[HIGH] Security: Shell Guard Bypass (PR #4594, CLOSED):** Commands like `curl --output=/etc/passwd` could bypass workspace restrictions. **Fixed.**
- **[HIGH] Security: TOCTOU File Access (PR #4987, OPEN):** A "P0" priority fix that prevents a race condition where a file path could be checked against the workspace and then swapped with a symlink before being opened. **Fix is in review.**
- **[MEDIUM] Data Loss: Agent Length Recovery (PR #5056, OPEN, Issue #5051):** When a model's response was truncated, only the last segment of the continuation was preserved, losing earlier parts of the output. **Open fix available.**
- **[MEDIUM] Crash: Concurrent Session Removal (PR #5068, CLOSED):** A `FileNotFoundError` could crash the agent loop if a session file was deleted by another process. **Fixed.**
- **[LOW] Test Failure: Missing `python` command (Issue #5062, PR #5064/5063, OPEN):** Unit tests fail on Debian/Ubuntu systems that only have `python3`. **Open fix available.**

### 6. Feature Requests & Roadmap Signals
- **Per-Conversation Model Override (Issue #4253):** Although closed, the underlying need for flexible, context-aware model selection is clear. The recent massive WebUI model settings refactor (PR #5061) suggests the team is moving toward a "model preset" concept, which could be a stepping stone to per-conversation overrides.
- **Per-Turn Model Fallback (PR #5017, CLOSED):** This merged feature already allows the WebUI to indicate when a fallback model is handling a turn. This shows the infrastructure for dynamic model selection is actively being built.
- **Browser Compatibility (Issue #5059):** This request for explicit browser support lists indicates that as WebUI usage grows, users are demanding clearer compatibility matrices.

### 7. User Feedback Summary
- **Pain Point: Workspace/Media Conflict (Issue #5028):** A user reported that when integrating with Feishu (Lark), uploaded files placed in the `media` directory become inaccessible when `restrictToWorkspace` is enabled. This is a real friction point for enterprise users mixing file uploads with workspace security.
- **Feature Need: Privacy/Performance Switching (Issue #4253):** A user demonstrated a clear, dual-use case: wanting to switch between a fast public API and a private, slower local model. The user's workflow is blocked by the inability to switch models per-conversation.
- **Satisfaction Signal:** The high number of closed bugs (4) and merged fixes (30) suggests the maintainers are responsive to user-reported issues, which likely contributes to overall satisfaction despite ongoing bugs.

### 8. Backlog Watch
- **Issue #4858 (OPEN):** "Refactor dynamic tool provider lifecycle out of AgentLoop" by chengyongru. This architectural issue, flagged as P2, has been open since July 9. It critiques the current architecture where MCP-specific code is leaking into the core `AgentLoop`, suggesting a deeper refactor is needed for long-term maintainability. [Link](https://github.com/HKUDS/nanobot/issues/4858)
- **PR #5042 (OPEN):** "fix(cron): default null schedule when loading jobs.json" by santhreal. A null schedule value in the cron store can orphan all other cron jobs. This has been open for 2 days and is flagged as P1, suggesting it could block users relying on scheduled tasks. [Link](https://github.com/HKUDS/nanobot/pull/5042)

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent Project Digest — 2026-07-24

## Today's Overview

Hermes Agent is experiencing a **high-activity day** with 50 issues and 50 PRs updated in the last 24 hours, reflecting a healthy but strained development cycle. The project has **43 open/active issues** and **47 open PRs**, suggesting a significant queue of work-in-progress that may indicate maintainer bandwidth pressure. Seven issues were closed and three PRs were merged today, showing steady but modest throughput relative to the volume of incoming work. The most active areas are **session state management**, **security hardening**, and **async delegation/task execution**, with a particular concentration of bugs around TUI/dashboard session leaks and provider integration edge cases. No new releases were published today.

## Releases

**None** — No new releases were published in the last 24 hours. The last release date is not available from the provided data.

## Project Progress

Three PRs were merged/closed today:

- **#69512 (CLOSED)** — `fix(anthropic): sanitize empty/whitespace-only text blocks to prevent permanent HTTP 400 after compression` — A critical fix for Anthropic provider integration where context compression could produce empty text blocks, causing hard API failures.
- **#4883 (CLOSED)** — `[UX] CLI code blocks have no copy-to-clipboard shortcut` — A long-standing UX enhancement (opened April 3) finally closed, improving CLI/TUI usability.
- **#62708 (CLOSED)** — `Silent context-overflow: no warning when compression is blocked (cooldown/anti-thrash)` — A P1 bug fix addressing a critical usability issue where users received no warning before hitting provider token limits.

Several significant open PRs advanced in review:
- **#70364** — `fix(tui): finalize delegate child live TUI runtimes on completion when never user-focused` — Direct fix for the orphaned TUI session bug (#70258).
- **#70363** — `fix(update): guard live venvs on POSIX` — Extending Windows-only venv protection to macOS and Linux.
- **#70343** — `fix(security): SSRF-safe GitHub Skills Hub API fetches` — Part of a broader security hardening campaign.

## Community Hot Topics

### Most Commented Issues

1. **#63679** (7 comments, CLOSED) — [Desktop App: every assistant message renders twice after recent update](https://github.com/NousResearch/hermes-agent/issues/63679)
   - A Windows-specific rendering regression where every assistant response appears duplicated. Closed, suggesting a fix was deployed. High visibility for Desktop users.

2. **#5820** (7 comments, OPEN since April) — [feat(memory): Allow synchronous recall for current turn as option for honcho and hindsight](https://github.com/NousResearch/hermes-agent/issues/5820)
   - Long-running feature request for memory plugins. The `prefetch` mechanism ignores the current query, causing irrelevant recalls. Community member @noctuid is pushing for architectural change.

3. **#70294** (6 comments, OPEN) — [cron: top-level delegate_task results are silently dropped](https://github.com/NousResearch/hermes-agent/issues/70294)
   - A critical cron job bug where delegation results vanish—users get only "I'm waiting for the subagents…" narration. Filed yesterday, already drawing significant attention.

4. **#30640** (6 comments, CLOSED) — [RFC: Cursor SDK (Composer 2.5) as cursor_agent tool](https://github.com/NousResearch/hermes-agent/issues/30640)
   - An ambitious integration proposal for Cursor's AI coding capabilities. Closed—potentially merged or deferred.

5. **#69449** (5 comments, OPEN) — [[Security] Custom endpoint API key stored in plaintext in config.yaml](https://github.com/NousResearch/hermes-agent/issues/69449)
   - A security concern: API keys for custom providers are stored unencrypted. Filed two days ago, rapidly gaining attention.

### Most Active Pull Requests

- **#70347** and **#70348** — Dependabot PRs for `body-parser` and `tar` updates (security dependencies in WhatsApp bridge and dev tooling).
- **#35040** (long-running since May) — `feat(api): add native voice turn stream endpoint` — A significant feature for voice interaction that's been open for nearly two months.

**Underlying need**: The community is expressing strong demand for **reliable async execution** (delegation, cron jobs), **memory system improvements** (synchronous recall, hindsight best practices), and **security hardening** (plaintext API keys, SSRF protection). These three themes dominate the most active discussions.

## Bugs & Stability

### Critical/High Severity (P1-P2)

| Issue | Severity | Description | Status | Fix PR |
|-------|----------|-------------|--------|--------|
| #70294 | **P2** | Cron delegate_task results silently dropped | OPEN, 6 comments | None yet |
| #64488 | **P2** | Dashboard TUI sessions leak processes/memory/DB rows | OPEN, 4 comments | None |
| #70258 | **P2** | Completed async delegations leave orphan live TUI runtimes | OPEN, 2 comments | #70364 (OPEN) |
| #70328 | **P2** | Compression triggers price images at flat 1500 tokens, causing 400s on 64K local models | OPEN, 1 comment | None |
| #69424 | **P2** | Slow LLM backend causes auto retry loop (140K+ token contexts) | OPEN, 4 comments | None |
| #69442 | **P2** | Doubao streaming tool_call JSON truncated — write_file silently fails | OPEN, 3 comments | None |
| #70131 | **P2** | Emoji truncation loop misses Dingbats (✨✅) | OPEN, 2 comments | None |
| #70203 | **P3** | xAI spending-limit 403 doesn't trigger fallback_providers | OPEN, 2 comments | None |
| #70245 | **P2** | fallback_providers context_length field silently discarded on activation | OPEN, 1 comment | None |
| #70097 | **P2** | openai-codex pool replays consumed refresh_token, goes terminally DEAD | OPEN, 1 comment | None |

### Medium Severity (P3)

| Issue | Description | Status |
|-------|-------------|--------|
| #70146 | `hermes sessions optimize-storage` reports negative "reclaimed" size | OPEN |
| #70058 | `reasoning_effort: "ultra"` rejected by GLM API, silent fallback to Claude | OPEN |
| #70153 | Persisted `/model` override rehydrates wrong `api_mode` after gateway restart | OPEN |
| #70116 | Mattermost adapter ignores HTTP proxy settings | OPEN |
| #70031 | TUI/CLI status lines repeat mid-turn even with streaming=false | OPEN |
| #53581 | Settings modal close button sits too close to window close button (Desktop) | OPEN |

### Security Concerns

| Issue | Description | Status |
|-------|-------------|--------|
| #69449 | **Plaintext API keys in config.yaml** | OPEN (P3, 5 comments) |
| #70343 | PR: SSRF-safe GitHub Skills Hub API fetches | OPEN |
| #70358 | PR: Reject always-blocked OpenViking endpoints | OPEN |
| #70357 | PR: Scrub credentials from voice playback subprocesses | OPEN |
| #70356 | PR: Route LobeHub skills fetches through guarded HTTP | OPEN |
| #70355 | PR: Reject always-blocked Supermemory BASE_URL | OPEN |
| #70354 | PR: Reject always-blocked RetainDB BASE_URL | OPEN |
| #70353 | PR: Mattermost media redirect SSRF hardening | OPEN |

**Analysis**: The project is experiencing a **wave of session/state management bugs** (leaks, orphans, dropped results) that suggest underlying architectural strain in the async delegation and TUI systems. The security PRs by @zapabob represent a **coordinated security hardening campaign** across multiple provider integrations (Skills Hub, Mattermost, voice playback, memory backends). The emoji truncation loop (#70131) is a particularly user-visible regression for Ollama users.

## Feature Requests & Roadmap Signals

### Community-Requested Features (Active)

1. **#5820** — Synchronous memory recall for honcho/hindsight (OPEN since April, 7 comments) — Would improve relevance of memory retrieval in real-time conversations. **Prediction**: Likely to be merged in next 1-2 releases given sustained community interest.

2. **#16168** — Allow the agent to send stickers (Telegram outbound) (OPEN since April, 3 comments, 5 👍) — A quality-of-life feature for Telegram users. Low complexity, high user satisfaction potential.

3. **#5237** — Hindsight memory: follow retain guidelines correctly (OPEN since April, 4 comments) — Aligns with best practices for memory performance. Could be bundled with #5820.

4. **#30640** — Cursor SDK integration (CLOSED) — The RFC was resolved; may appear in a future release as a tool or bridge.

### PRs Indicating Roadmap Direction

- **#35040** — Native voice turn stream endpoint (OPEN since May 29) — A significant voice interaction capability, potentially tied to HAL Voice integration.
- **#69437** — Relay setup and first-use metrics (OPEN, by @afourniernv) — Telemetry infrastructure for observability.
- **#69416** — Relay active install metrics (OPEN, by @afourniernv) — Continuation of telemetry stack.
- **#64094** — Surface async process/delegation results in Desktop chat (OPEN since July 14) — Improving visibility of background tasks.
- **#69687** — Desktop Webhooks page for subscription CRUD (OPEN, by @austinpickett) — Desktop parity with dashboard.

**Prediction**: The next release is likely to include **native voice streaming** (#35040), **Desktop Webhooks management** (#69687), and potentially the **memory recall improvements** (#5820/#5237). The security hardening PRs (#70343-#70358) are likely to land as a batch given their coordinated nature.

## User Feedback Summary

### Pain Points (Real User Reports)

- **Duplicate assistant messages** (#63679): A Windows Desktop user reported responses rendered twice after an update. **High frustration** for a rendering regression.
- **Silent delegation failures** (#70294): Cron job users lose subagent results without any error. Reported by @miltonleon-hero-software; the "job reports ok" behavior is especially misleading.
- **Plaintext API keys** (#69449): @asorry75 reported a security concern where custom endpoint API keys are stored unencrypted. **Trust and compliance risk** for enterprise or proxy-enforced environments.
- **Slow local LLM auto-retry loops** (#69424): @stuartbrand reported that slow 122B models on high-end AMD hardware enter infinite retry loops with 140K+ token contexts. **Productivity blocker** for users running local models.
- **Emoji truncation regression** (#70131): @yeounhyeok reported that the Dingbats emoji fix is incomplete, causing sparkles (✨) and checkmarks (✅) to trigger truncation loops. **Regression that breaks common model outputs**.
- **Mattermost proxy failure** (#70116): @rcarrata reported that the Mattermost adapter ignores HTTP proxy settings, blocking deployments in OpenShift/proxied environments. **Deployment blocker** for enterprise users.
- **Negative storage reporting** (#70146): @hussainjee found `optimize-storage` reports confusing negative "reclaimed" values when databases grow. **Usability issue** for power users managing storage.

### Satisfaction Signals

- Three issues were closed today, suggesting maintainers are responsive to user reports.
- The security PRs indicate proactive investment in hardening, which should improve trust.
- The Desktop Webhooks feature (#69687) shows parity improvements between dashboard and desktop clients.

## Backlog Watch

### Long-Open Issues Needing Maintainer Attention

| Issue | Age | Status | Reason for Concern |
|-------|-----|--------|--------------------|
| #2765 | **~4 months** (March 24) | OPEN, P3, 4 comments | Hindsight plugin silently skips tool registration when env var is missing — debugging nightmare for users, seemingly low complexity to fix |
| #7718 | **~3.5 months** (April 11) | OPEN, P3, 4 comments, 4 👍 | Hindsight plugin fails silently in `local_embedded` mode due to wrong dependency in plugin.yaml — significant user impact for local deployments |
| #5820 | **~3.5 months** (April 7) | OPEN, P3, 7 comments | Memory recall feature request — the most-commented open issue, sustained interest, no maintainer response visible |
| #5237 | **~3.5 months** (April 5) | OPEN, P3, 4 comments | Hindsight memory retain guidelines not followed — companion to #5820 |
| #16168 | **~3 months** (April 26) | OPEN, P3, 5 👍 | Telegram sticker sending — moderate community interest, low complexity feature |
| #46649 | **~5 weeks** (June 15) | OPEN, P3 | Desktop renderer blank window from ASAR path issue — affects packaged app users |

### Long-Open PRs Needing Attention

| PR | Age | Status | Reason for Concern |
|----|-----|--------|--------------------|
| #35040 | **~8 weeks** (May 29) | OPEN | Native voice turn stream endpoint — significant feature, potential merge conflicts growing |
| #49266 | **~5 weeks** (June 19) | OPEN | TUI colour parser replacement for nested tags — UX improvement for CLI/TUI users |

**Recommendation**: The **memory plugin issues** (#2765, #7718, #5820, #5237) represent the longest-standing and most user-impacting backlog. These four issues span 3-4 months and touch the same subsystem. A coordinated fix or refactor for the Hindsight memory plugin would provide outsized community benefit.

---

*Data sourced from NousResearch/hermes-agent GitHub repository. Generated 2026-07-24.*

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw Project Digest — 2026-07-24

## 1. Today's Overview
PicoClaw shows **moderate maintenance activity** today, with 15 pull requests updated in the last 24 hours—though the majority are automated dependency bumps. The project closed one stale bug issue and merged 7 PRs, including a vulnerability fix and two feature PRs that had been pending since June. No new releases were published. Activity is healthy but heavily skewed toward dependency housekeeping, with only two human-authored PRs among the 15. The open PR count (8) slightly exceeds closed/merged (7), suggesting a small accumulation of pending work.

## 2. Releases
**No new releases** were published in the last 24 hours. The latest release remains unchanged.

## 3. Project Progress
Today’s merged/closed PRs (7 total) advanced the project in several areas:

- **Security fix**: PR #3286 (closed) — *fix: update Go and x/text for govulncheck* — A user-authored fix addressing Go vulnerability scanner findings by updating the Go toolchain and `x/text` dependency. This is the most impactful merge today.
- **New feature (closed)**: PR #3118 — *Add remote Pico WebSocket mode to picoclaw agent* — Adds `--remote ws://...` mode to the agent CLI, enabling WebSocket-based remote control while preserving local behavior.
- **Bug fix (closed)**: PR #3115 — *Fix inline data URL media extraction for generic tool output* — Fixes a session-history corruption bug where base64-encoded media strings in plain text tool output were incorrectly treated as real attachments.
- **Dependency updates (closed, stale)**: PRs #3235, #3236, #3237, #3238 — Bumps for `pion/rtp`, `copilot-sdk/go`, `golang.org/x/sync`, and `aws-sdk-go-v2/config`.

A notable open feature PR remains under active development:
- PR #3200 (open) — *feat(models): add configurable default fallback chain* — Adds a UI and backend API for setting a default model with fallback chain, allowing reordering and persistence. This has been open for 23 days without maintainer response.

## 4. Community Hot Topics
Only one issue had any discussion activity in the last 24 hours:

- **#3195** [CLOSED — stale] *OpenAI GPT does not work on NanoKVM with default config* — 4 comments. The reporter found that PicoClaw on NanoKVM 2.4.0 fails to work with `gpt-5.4` despite following the configuration docs. This was closed as stale, meaning no fix or resolution was provided. The underlying need is better documentation or compatibility handling for the NanoKVM platform, which is a relatively new deployment target.

No PRs had comments or reactions in the last 24 hours.

## 5. Bugs & Stability
**One bug was actively addressed today:**

- **Medium severity**: PR #3115 (merged) — *Fix inline data URL media extraction for generic tool output* — A session-history corruption bug where tools like `read_file` and `exec` returning base64 image strings in output would be incorrectly parsed as media attachments. Now fixed.

**One unresolved platform compatibility issue:**

- **Low severity** (closed stale): Issue #3195 — OpenAI GPT not working on NanoKVM with default config. Closed without resolution. May re-emerge if more NanoKVM users encounter the problem.

**One vulnerability fix merged today:**

- PR #3286 — Go vulnerability scanner fixes, updated Go and `x/text` dependencies.

No crashes, regressions, or new bugs were reported today.

## 6. Feature Requests & Roadmap Signals
Two substantial features were merged/closed today, indicating they may land in the next release:

- **Remote WebSocket agent mode** (PR #3118) — Enables `picoclaw agent --remote ws://...` for remote control. Likely targeting developers who want to integrate PicoClaw into external workflows or manage agents from CI/CD pipelines.
- **Configurable default fallback chain** (PR #3200, still open) — Adds model fallback configuration in the web UI. This addresses a long-standing user need for graceful degradation when primary models are unavailable or rate-limited.

**Prediction**: The fallback chain feature (PR #3200) is the most likely candidate for inclusion in the next release, as it has been open for 23 days with no visible maintainer pushback. The remote WebSocket mode (already merged) will likely ship as well.

## 7. User Feedback Summary
Minimal direct user feedback was captured today. The single closed issue (#3195) reflects:

- **Pain point**: Configuration friction for new deployment targets (NanoKVM). The user followed official docs but encountered silent failures, suggesting either a documentation gap or a compatibility regression.
- **Use case**: Running PicoClaw on edge hardware (NanoKVM) with OpenAI GPT models. This is a growing niche as NanoKVM adoption increases.
- **Satisfaction level**: The issue was closed stale without a solution, which may leave the user dissatisfied. No follow-up or workaround was provided by maintainers.

No positive feedback, testimonials, or satisfaction signals were recorded today.

## 8. Backlog Watch
The following items require maintainer attention:

| Item | Status | Days Open | Why It Matters |
|------|--------|-----------|----------------|
| **PR #3200** — Configurable fallback chain | Open, no maintainer response | 23 days | Directly requested feature; has code but no review |
| **Issue #3195** — NanoKVM + OpenAI not working | Closed stale, unresolved | 24 days | Platform compatibility issue; may recur |
| **PR #3222** — DeltaChat refactor | Open, no maintainer response | 21 days | Significant cleanup (-200 LOC), documentation updates |
| **Dependency PRs #3262, #3263** — GitHub Actions setup-* bumps (v6→v7) | Open, stale | 8 days | Minor but blocking if CI relies on deprecated action versions |

**Most critical**: PR #3200 (fallback chain) is the highest-impact open item—it has no maintainer review despite being open for 23 days. If this feature is valuable to the roadmap, it should be reviewed and merged or provided with guidance to the contributor.

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw Project Digest — 2026-07-24

## 1. Today's Overview

NanoClaw saw moderate activity today with 4 merged/closed PRs and 6 still open, alongside one open bug issue. The project team focused on fixing container lifecycle bugs, improving Telegram and Matrix integration stability, and hardening the CLI against legacy API routes. No new releases were published. Overall project health is stable, with maintenance velocity picking up after a quieter June, though one high-priority race condition in container orchestration remains unresolved.

## 2. Releases

*No new releases today.*

## 3. Project Progress

Four pull requests were merged or closed today:

- **#2892 — Telegram thread support (merged)**  
  Enables `supportsThreads: true` for the Telegram adapter, allowing forum/topic threads to be properly tracked.  
  [GitHub](https://github.com/nanocoai/nanoclaw/pull/2892)

- **#2844 — Native Matrix E2EE adapter (merged)**  
  Replaces the legacy Chat SDK bridge with a native `matrix-bot-sdk` + Rust-crypto adapter for persistent end-to-end encryption support. A significant infrastructure improvement for privacy-conscious deployments.  
  [GitHub](https://github.com/nanocoai/nanoclaw/pull/2844)

- **#3120 — Keep typing indicator alive during long tool calls (merged)**  
  User-facing UX fix: prevents the typing indicator from prematurely disappearing when a single tool call takes more than a few seconds.  
  [GitHub](https://github.com/nanocoai/nanoclaw/pull/3120)

- **#3115 — Block legacy Gmail API routes (merged)**  
  Idempotent blocks for obsolete Gmail API endpoints through `www.googleapis.com` to prevent accidental policy bypasses.  
  [GitHub](https://github.com/nanocoai/nanoclaw/pull/3115)

## 4. Community Hot Topics

The most active discussion today centers around the duplicate container race condition:

- **#2466 — Duplicate container spawn race on `wakeContainer`**  
  *Comments: 2 | Last updated: 2026-07-23*  
  This 10-week-old bug remains the most significant unresolved issue. A race between script-based and host-service calls to `wakeContainer` can cause two identical agent containers to spawn, both processing the same message independently. The community seems to be waiting on a fix — notably, PR #3119 explicitly addresses this root cause (orphan reconciliation).  
  [GitHub](https://github.com/nanocoai/nanoclaw/issues/2466)

- **#3119 — Orphan container reconciliation (open PR)**  
  Directly targets the duplicate spawn problem by reconciling untracked orphan containers. If merged, this would likely close #2466.  
  [GitHub](https://github.com/nanocoai/nanoclaw/pull/3119)

## 5. Bugs & Stability

| Severity | Issue | Status | Fix PR? |
|----------|-------|--------|---------|
| **High** | #2466 — Duplicate container spawn race on concurrent `wakeContainer` calls | Open (2 comments) | PR #3119 open |
| Low | #3121 — Reaction delivery not best-effort (open PR) | Open | Being addressed in PR #3121 |
| Low | #2346 — Unknown slash commands silently dropped (open PR) | Open (since May) | PR #2346 open |

**Key finding:** The duplicate container race (#2466) is the most impactful bug. It causes duplicated agent work and potential data inconsistency. PR #3119 (orphan reconciliation) is the likely fix. The other open bug-related PRs are lower severity.

## 6. Feature Requests & Roadmap Signals

- **Matrix native E2EE (#2844)** — Now merged, this opens the door for enterprise/security-conscious deployments using Matrix. Likely to be included in the next stable release.
- **Typing indicator UX (#3120)** — Small but meaningful user-facing improvement; now merged.
- **`ncc` utility skill (#2971)** — A new standalone CLI for host operations and health checks (still open). Signals growing interest in better operator tooling for production deployments.

**Prediction for next minor release:** The orphan container fix (PR #3119) and the `ncc` utility skill could land in a v2.x release within 1–2 weeks, alongside the already-merged Matrix E2EE and Telegram thread support.

## 7. User Feedback Summary

- **Pain point:** The duplicate container race (#2466) is causing real operational problems for long-running hosts — users report seeing 3 concurrent containers for a single agent group, wasting resources and processing the same session DB entries.
- **Positive:** The merged Telegram thread support (#2892) and Matrix E2EE (#2844) respond to long-standing community requests for better multi-platform support and privacy.
- **Neutral/under discussion:** The `ncc` utility CLI (#2971) reflects user desire for better production observability, but has been open for 17 days without merge.

## 8. Backlog Watch

- **#2466 — Duplicate container spawn race**  
  Created 2026-05-14, last updated 2026-07-23 — 71 days open. This is the longest-running active bug. PR #3119 is the proposed fix. Attention needed: merge review.  
  [GitHub](https://github.com/nanocoai/nanoclaw/issues/2466)

- **#2346 — Unknown slash commands treated as `passthrough`**  
  Created 2026-05-08, last updated 2026-07-23 — 77 days open. Low priority but may confuse users who type `/unknown` expecting an error message and instead get silence.  
  [GitHub](https://github.com/nanocoai/nanoclaw/pull/2346)

- **#3090 — Prepend all top-level context Markdown**  
  Created 2026-07-19, open for 5 days. Core-team fix awaiting review/maintainer attention.  
  [GitHub](https://github.com/nanocoai/nanoclaw/pull/3090)

---

**Project health summary:** Stable with healthy fix velocity. The orphan container bug (#2466) is the single biggest risk to production reliability. The merged Matrix E2EE work is the most significant architectural improvement this week.

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw Project Digest — 2026-07-24

## Today's Overview
IronClaw is in an intense pre-v1 launch sprint with **50 PRs and 32 issues updated in the last 24 hours**, indicating peak engineering activity. The project shows a healthy balance of feature work (heartbeat scheduling, signing substrate revival, deployment renaming), bug fixes (WebChat disconnect, Windows serve crash, 429 rate limiting), and infrastructure cleanup (legacy test removal, extension source retirement). The v1-launch-checklist tag dominates open issues with 10+ items covering CLI availability, OAuth configuration, webhook delivery, and UI polish. Three closed issues today reflect steady progress on the architecture simplification roadmap (§5.11 runtime collapse). No new releases were cut today, suggesting the team is consolidating changes ahead of an imminent RC.

## Releases
**No new releases today.** The last automated release PR (#5598) remains open and has been updating since July 3, 2026. The release pipeline is blocked on pending changes, likely waiting for the v1 launch checklist items to clear.

## Project Progress
**10 PRs merged/closed today** (out of 50 total PRs updated). Key completions:

- **PR #6596** (Closed) — Clean deployment-mode local naming: renamed `RebornLocal*` and `LocalInvocationServicesResolver` to deployment-neutral vocabulary. A critical step in the "Remove Reborn from codebase" initiative.
- **PR #6589** (Closed) — test(e2e): Added reusable provider fault profiles (HTTP 400/401/403/404/409/429/5xx, timeouts, connection resets) with a resettable loopback fault proxy for standalone Reborn-to-Emulate testing.
- **Issue #6543** (Closed) — Move `ProductSurface` contract to `host_api` and collapse product crates into `ironclaw_product`. This completes a key architecture boundary cleanup.
- **Issue #6462** (Closed) — Sidebar thread list pagination bug fixed (frontend now consumes `nextCursor` for multi-page thread loading).

Notably, the **attested-signing substrate stack** (PRs #3996, #3997, #4015) was re-ported onto current `main`—1184 commits behind—indicating a major revival of the signing feature after dormancy.

## Community Hot Topics
**Most active discussions (by comments):**

- **Issue #6389** — [CLOSED] "Phase 4 (§5.11): collapse build_local_runtime + build_production_shaped" (11 comments). The highest-traffic issue. Discussion centered on reconciling the two runtime assembly paths into one `build_runtime(cfg)`. This is the final piece of the architecture simplification DTO and was closed successfully.
- **Issue #6274** — [CLOSED] "Finish DeploymentConfig as the main composition config" (5 comments). A follow-up to ensure `DeploymentConfig` fully replaces legacy config paths. Closed with the merge of the runtime collapse work.
- **Issue #6524** — [OPEN] "Epic: Hermetic capability and journey testing platform" (3 comments). A broad testing infrastructure epic. The underlying need is deterministic, reproducible coverage for all capabilities and critical user journeys—a foundation for CI reliability.

**Underlying need analysis:** The hot topics reveal a project in transition from "Reborn" prototyping to production IronClaw branding. The runtime collapse (high comments) is the last architectural debt before launch. The testing epic signals recognition that current E2E coverage is insufficient for v1 quality.

## Bugs & Stability
**New bugs reported today (ranked by severity):**

| Severity | Issue | Description | Fix PR? |
|----------|-------|-------------|---------|
| **Critical** | #6590 | `ironclaw serve` fails on Windows: "workspace root must not overlap default skill root /skills". Blocks all Windows local development. | Not yet |
| **High** | #6581 | 429 Too Many Requests on agent-stg SSE endpoint causes permanent "Disconnected" badge. | **PR #6592** (open, fixes both backend rate-limit budget and frontend navigation-race thrash) |
| **High** | #6548 | Hosted staging preview-auth wall blocks webhook delivery (Telegram, Slack). External services cannot reach staging. | Not yet |
| **High** | #6544 | No UI/CLI to configure `IRONCLAW_REBORN_SLACK_PERSONAL_OAUTH_REDIRECT_URI` — Slack auth returns 503. | Not yet |
| **Medium** | #6575 | `systemd` service error immediately after `ironclaw onboard` on Ubuntu. Service fails to start. | Not yet |
| **Medium** | #6541 | WebUI constantly showing "Reconnecting" despite agent working. Confusing user experience. | **PR #6592** (partial fix) |
| **Low** | #6523 | Agent creation fails during onboarding if testing flag is set. | Not yet |

**Observations:** The 429/WebChat disconnect bug (#6581) has a fix PR in review (#6592) that addresses both backend rate-limiting and frontend SSE race conditions. The Windows crash (#6590) is a path validation issue specific to local-dev profiles—likely a configuration default mismatch for Windows filesystem conventions.

**Regression risk:** The legacy extension source retirement (PR #6594, open) removes `tools-src/` and `channels-src/` trees. While WIT runtime support is preserved, any uncaught dependency on the old source layout could break CI or community forks.

## Feature Requests & Roadmap Signals
**Notable feature signals from today's issues:**

1. **Heartbeat scheduling** (Issues #6569, #6570, #6571) — A three-issue MVP chain defining heartbeat contract, durable scheduling, and delivery suppression. This is likely for monitoring agent liveness in production—a launch requirement.
2. **Reliable Skill Discovery, Routing, and Activation** (Issue #6565, epic) — The current model-directed skill selection is brittle. The epic proposes structured skill catalogs with deterministic routing, which would reduce model hallucination and improve task completion reliability.
3. **Admin-Managed Agents as UserId Subjects** (Issue #6578, epic) — Tenant administrators need to create non-human subjects for automations and integrations without breaking user isolation. This signals enterprise multi-tenant requirements coming soon.
4. **Default IronClaw Configuration and Runtime Contracts** (Issue #6551) — Part of the "Remove Reborn" branding effort. Suggests the next release will have cleaner env var naming (`IRONCLAW_*` with fallback to `IRONCLAW_REBORN_*`).

**Predictions for next release:**
- The heartbeat MVP (3 issues today) is a strong candidate for inclusion—it's scoped as MVP and addresses a blocking production need.
- The attested-signing substrate revival (3 PRs re-ported today) may land as the signing feature has been dormant for weeks.
- The "Remove Reborn" renaming work (issues #6550, #6551, #6552) will likely be bundled as a single UX-facing release.

## User Feedback Summary
**Real pain points captured today:**

- **User sergeiest** reported multiple v1-launch blockers across hosted staging: CLI unavailable on SSH (#6521), Telegram setup requires documentation (#6522), and Slack OAuth redirect URL cannot be configured (#6544). Core complaint: "IronClaw is not aware how to setup Telegram locally or on agent.near.ai" — requesting guided onboarding similar to Google's.
- **User mperkins0155** hit an immediate blocker on Windows: `ironclaw serve` crashes with a path overlap error. This is a platform-specific regression likely from recent workspace root changes.
- **User fadeevab** reported that `systemctl` service status shows errors immediately after `ironclaw onboard` on Ubuntu, indicating the onboarding process doesn't validate the systemd configuration.
- **Multiple users** (sergeiest, sergeiest again on #6541) express confusion about WebChat's "Reconnecting" banner, which appears constantly despite functional agents. The 429 rate limit (PR #6592 fix) is the root cause.

**Satisfaction signals:** No explicit praise, but the volume of activity suggests engaged early adopters willing to report bugs. The team's responsiveness (fix PRs within hours for #6581, #6590) is good.

## Backlog Watch
**Long-unanswered items needing maintainer attention:**

1. **Issue #4548** (Open since 2026-06-08, 47 days) — "Bug: Chat completion request serializes duplicate top-level `model` field when tools are included (DeepSeek 400)". **2 comments total, no maintainer response.** This blocks DeepSeek provider usage with tools. Given the v1 launch focus, this provider-specific bug may be deprioritized, but it still has zero maintainer engagement after 6+ weeks.

2. **PR #5598** (Open since 2026-07-03, 21 days) — Automated release PR that's been updating continuously. The release pipeline appears stalled. This is important because `ironclaw_common` 0.5.0 has breaking API changes that downstream consumers (if any) need to prepare for.

3. **PR #3997** (Open since 2026-05-24, 61 days) — attested-signing PR13, re-ported today after 1184 commits behind. This PR has been dormant for two months. The re-port today signals renewed attention, but it remains open—the signing feature has been in development for over 60 days.

**Recommendation:** The DeepSeek bug (#4548) should receive at minimum a triage label or a "planned for post-v1" comment. The silent gap is poor for community trust, especially since the issue has clear reproduction steps and a known provider.

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

# LobsterAI Project Digest — 2026-07-24

**Project**: LobsterAI (github.com/netease-youdao/LobsterAI)  
**Analysis Date**: 2026-07-24  

---

## Today's Overview

LobsterAI shows moderate activity over the past 24 hours, with three open issues and three pull requests updated. No new releases were tagged. Two PRs were merged or closed, including a feature polish for AI skin appearance and a larger release branch (v2026.7.20). All three currently open issues are stale (created April 2, 2026, with no recent maintainer response), indicating possible community frustration with unresolved bugs and feature requests. The repository appears to be in a maintenance phase following the latest release cut, with Dependabot dependency bumps and cosmetic feature work being the primary merged contributions.

---

## Releases

No new releases were published in the last 24 hours. The latest cut appears to be the release branch merged in PR #2379 (Release/2026.7.20, merged 2026-07-23). Users and contributors should refer to that release for recent changes.

---

## Project Progress

Two pull requests were merged/closed today:

- **[PR #2379 (CLOSED) — Release/2026.7.20](https://github.com/netease-youdao/LobsterAI/pull/2379)**: A release branch touching renderer, build, docs, main, OpenClaw, Cowork, Windows platform, and artifacts areas. This is the most recent version cut.
- **[PR #2378 (CLOSED) — feat(skin): polish AI skin appearance behavior](https://github.com/netease-youdao/LobsterAI/pull/2378)**: Aligned artifact add-tab and task-search surfaces with AI skin presentation, applied saved skins via card selection with newest-first ordering, made standard themes mutually exclusive with AI skins, and simplified the AI skin settings. This represents a user-facing UI polish for the skin system.

One PR remains open:

- **[PR #1277 (OPEN) — chore(deps-dev): bump the electron group across 1 directory with 2 updates](https://github.com/netease-youdao/LobsterAI/pull/1277)**: A Dependabot PR bumping Electron from 40.2.1 to 43.1.1 and electron-builder. This is a significant Electron version jump (40→43) and should be reviewed for compatibility before merging.

---

## Community Hot Topics

All three open issues are stale (last updated April 2, 2026, no recent maintainer replies). Despite low comment counts, they represent persistent community pain points:

- **[Issue #1263 (OPEN, stale) — Duplicate scheduled tasks showing identical content with API rate limit errors](https://github.com/netease-youdao/LobsterAI/issues/1263)**  
  *Need*: User reports UI displaying duplicate scheduled tasks with identical content, both triggering "API rate limit reached" errors. Only one session is found when checking internally. Likely a UI rendering or task scheduling duplication bug combined with insufficient API quota handling.

- **[Issue #1265 (OPEN, stale) — Per-agent IM bot and model binding](https://github.com/netease-youdao/LobsterAI/issues/1265)**  
  *Need*: User requests the ability to bind different IM bots and models to different agents (e.g., a dispatcher agent vs. a PPT generator). Arguments for team-based agent workflows and model specialization (e.g., coding vs. reasoning models). This is a multi-agent orchestration enhancement.

- **[Issue #1273 (OPEN, stale) — sql.js WASM memory corruption & database corruption risk](https://github.com/netease-youdao/LobsterAI/issues/1273)**  
  *Need*: Critical stability report describing `memory access out of bounds` crashes under high-frequency writes (Cowork sessions, message streams). Non-atomic `fs.writeFileSync` save operations risk database file corruption on interrupted writes. File describes an **irrecoverable crash** requiring app force-quit.

---

## Bugs & Stability

| Issue | Severity | Description | Fix PR? |
|-------|----------|-------------|---------|
| [#1273 — sql.js WASM memory corruption & DB corruption](https://github.com/netease-youdao/LobsterAI/issues/1273) | **CRITICAL** | `memory access out of bounds` crash under high Cowork/message load; non-atomic save risks permanent DB corruption | None identified |
| [#1263 — Duplicate scheduled tasks with API rate limits](https://github.com/netease-youdao/LobsterAI/issues/1263) | **HIGH** | UI shows duplicate tasks, both fail with rate limit errors; leads to user confusion and degraded automation | None identified |

The WASM memory corruption bug (#1273) is the most severe open stability issue, as it causes application hard-crashes and potential data loss. The duplicate tasks bug (#1263) degrades usability for automation workflows. No fix PRs are associated with either issue.

---

## Feature Requests & Roadmap Signals

The most notable feature request is **[Issue #1265 — Per-agent IM bot and model binding](https://github.com/netease-youdao/LobsterAI/issues/1265)**. This signals strong community interest in multi-agent orchestration where different agents take on distinct roles (dispatcher, PPT generator, coder) and can be assigned different models optimized for those roles. Given the PR #2378's focus on AI skin polish (which touches the CoWork area), multi-agent customization may be a candidate for the next minor release.

The Dependabot PR #1277 bumping Electron from 40→43 is notable. If merged, this would bring significant Chromium and Node.js improvements but may introduce breaking changes. Its long open duration (since April 2) suggests maintainers are cautious or have compatibility concerns.

---

## User Feedback Summary

- **Pain Points**:  
  - Duplicate scheduled tasks and API rate limit failures undermine automation reliability (Issue #1263).  
  - High-frequency CoWork sessions cause application crashes and database corruption risk (Issue #1273).  
  - Inability to assign different bots/models per agent limits team-based multi-agent workflows (Issue #1265).

- **Satisfaction Signals**:  
  - Recent cosmetic and UX improvements (AI skin polish, PR #2378) show maintainers are investing in visual polish.  
  - Regular release cadence (v2026.7.20 merged) suggests active development.

- **Dissatisfaction Indicators**:  
  - Three critical/stale issues with zero maintainer replies since April 2 — the community is likely frustrated by lack of acknowledgment for stability and feature enhancement requests.  
  - No fix PRs exist for the highest-severity bug (WASM memory corruption).

---

## Backlog Watch

The following items require maintainer attention:

- **Issue #1273 (CRITICAL, stale since April 2)** — WASM memory corruption and DB crash. No response from maintainers. This is the highest-priority stability issue in the backlog.
- **Issue #1265 (MEDIUM, stale since April 2)** — Per-agent bot/model binding. No response. This feature request has clear, well-articulated use cases.
- **Issue #1263 (HIGH, stale since April 2)** — Duplicate tasks + rate limit errors. No response. Affects core automation functionality.
- **PR #1277 (OPEN since April 2)** — Electron major version bump (40→43). Long unaddressed — risk of accumulating version debt and security vulnerabilities in the Electron dependency.

All three issues and the Dependabot PR have been open since 2026-04-02 without maintainer interaction. This suggests a significant gap in community issue triage that should be addressed to maintain contributor trust.

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

# Moltis Project Digest — 2026-07-24

## 1. Today's Overview
Moltis saw moderate activity over the past 24 hours, with 5 pull requests merged/closed and 2 issues updated. The project released two new patch versions (20260723.02 and 20260723.03), indicating ongoing iterative polishing. Bug-fixing and security hardening dominated the day's merged work, particularly around Slack integration and web UI usability. No new open issues were filed in the last 24 hours, and the open issue count remains low (1 active bug), suggesting a relatively stable state.

## 2. Releases
Two new releases were published today:
- **20260723.03** and **20260723.02**

No release notes, changelogs, or migration guides were provided in the data. Given the PRs merged just prior, these releases likely include the fixes described below (Slack allowlist OTP improvements, web UI date formatting, and Slack API base host validation). Users running earlier builds should upgrade to benefit from these patches. No breaking changes or migration steps are evident from the context.

## 3. Project Progress
All 5 pull requests active in the last 24 hours were merged or closed:

- **#1162** — *fix(web): show dates for older sessions* (merged). Fixes Issue #1108 by adding localized date labels for sessions older than today, including "yesterday," weekday names, and calendar dates with years for very old sessions.
- **#1164** — *fix(slack): allow operator-approved api base hosts* (merged). Adds `MOLTIS_SLACK_API_BASE_URL_ALLOWLIST` environment variable and moves validation into the channels crate, enabling internal Slack proxy setups while blocking cloud metadata endpoints.
- **#1163** — *fix(slack): challenge unknown allowlist DMs with OTP* (merged). Closes bypass vulnerabilities in Slack, Microsoft Teams, Signal group access, and Matrix DM allowlists; adds OTP-based self-approval for non-allowlisted Slack DM users.
- **#1161** — *chore(deps): bump astro from 7.0.9 to 7.1.3 in /docs* (merged). Routine dependency update for the documentation site.
- **#1124** — *Add context command support for chat turns* (merged). New feature allowing an optional `chat.context_command` config that runs before each turn and appends stdout to the prompt context, useful for deployments that need automatic runtime context injection.

## 4. Community Hot Topics
No issues or PRs in the last 24 hours generated significant community discussion (all have 0 reactions, and comments were limited to author/maintainer interactions).

- **Issue #1095** — [Bug]: Podman is not working via Moltis (1 comment). This remains the only active open bug and continues to represent an unmet user need for container engine diversity beyond Docker. URL: [Issue #1095](https://github.com/moltis-org/moltis/issues/1095)

The underlying need appears to be support for Podman as an alternative to Docker, which is important for users on systems without Docker Desktop or those preferring rootless containers.

## 5. Bugs & Stability
Two bug fixes were merged today, both addressing specific issues:

| Bug | Severity | Status | Fix PR |
|-----|----------|--------|--------|
| Web UI session list shows times but not dates for past-day sessions | Low (UI usability) | **Fixed** — merged today | [#1162](https://github.com/moltis-org/moltis/pull/1162) |
| Slack allowlist semantics: empty DM/channel allowlists granted access instead of denying | **High** (security bypass) | **Fixed** — merged today | [#1163](https://github.com/moltis-org/moltis/pull/1163) |
| Slack API base URL validation missing: cloud metadata endpoints potentially reachable via Slack client | **Medium** (security hardening) | **Fixed** — merged today | [#1164](https://github.com/moltis-org/moltis/pull/1164) |

No new bugs were reported today. The one open bug (Podman) continues without a fix in progress.

## 6. Feature Requests & Roadmap Signals
One significant feature was merged today:
- **Context command support** ([PR #1124](https://github.com/moltis-org/moltis/pull/1124)) — Adds `chat.context_command` config, enabling automatic runtime context injection before each chat turn. This signals the team's focus on making Moltis more useful in automated/CI deployment scenarios where dynamic context is needed.

Likely next version candidates:
- Podman support (based on open Issue #1095)
- Further Slack integration improvements (based on multiple recent Slack-related PRs)

## 7. User Feedback Summary
- **Pain point addressed (today):** Users reporting that the web UI session list lacked date context for older sessions — fixed via PR #1162.
- **Pain point unaddressed:** Podman container engine support remains broken for at least one user (Issue #1095).
- **Security concern (addressed):** An operator-controllable allowlist (`MOLTIS_SLACK_API_BASE_URL_ALLOWLIST`) was added, addressing potential security risks from internal Slack proxy configurations.
- **Satisfaction indicators:** The high merge rate (5 PRs closed) and two releases suggest maintainers are actively responding to community needs.

## 8. Backlog Watch
- **#1095** — [Bug]: Podman is not working via Moltis (open since 2026-06-03, last updated 2026-07-23, 1 comment). This is the longest-standing open bug with no fix PR attached. It has received no reactions or maintainer assignment. If Podman support is important to the project's roadmap, this should be prioritized. URL: [Issue #1095](https://github.com/moltis-org/moltis/issues/1095)

No other issues or PRs appear to be languishing without maintainer attention. All other tracked items have been closed or have recent activity.

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

Here is the project digest for **CoPaw (agentscope-ai/CoPaw)** covering activity on **2026-07-24**.

---

## CoPaw Project Digest — 2026-07-24

### 1. Today's Overview
This was a **high-activity day** for the CoPaw project, driven by the recent release of **v2.0.1-beta.2**. There were **35 Issues** and **50 PRs** updated in the last 24 hours, indicating a strong maintenance and development cadence. While the project is shipping many fixes (21 merged/closed PRs), there is significant user friction around the **v2.0 migration**, specifically regarding performance overhead, Docker update workflows, and MCP tool compatibility. The core team is actively addressing regressions, with several critical bug-fix PRs already in the review pipeline.

### 2. Releases
- **Latest Release:** [v2.0.1-beta.2](https://github.com/agentscope-ai/CoPaw/releases/tag/v2.0.1-beta.2)
- **Key Changes:**
    - **ci:** Unified release orchestrator now gates the Web build on success of the Desktop build (PR [#6329](https://github.com/agentscope-ai/CoPaw/pull/6329)).
    - **fix(runtime):** Rotates the text message display when a new reasoning block is generated (PR [#6310](https://github.com/agentscope-ai/CoPaw/pull/6310)).
- **Migration Notes:** None required for this patch version. This release appears to focus on CI reliability and minor UI runtime fixes.

### 3. Project Progress
- **Merged/Closed PRs (21):** The team closed several high-priority items:
    - **Governance:** [PR #6368](https://github.com/agentscope-ai/CoPaw/pull/6368) fixed a bug where the `audit_level=none` setting was ignored, always writing to the SQLite audit log. [PR #6390](https://github.com/agentscope-ai/CoPaw/pull/6390) bridges tool guard detection rules into the governance policy (Phase 1).
    - **Desktop Stability:** [PR #6225](https://github.com/agentscope-ai/CoPaw/pull/6225) replaced the force-kill of the backend sidecar with a graceful shutdown sequence (SIGTERM + wait).
    - **Console Performance:** [PR #6393](https://github.com/agentscope-ai/CoPaw/pull/6393) stabilized React memoization by creating a stable `EMPTY_QUEUE` constant, reducing unnecessary re-renders and SSE re-parsing.
    - **Memory:** [PR #6351](https://github.com/agentscope-ai/CoPaw/pull/6351) added recovery guidance to prompts, teaching the agent to reload and rewrite `MEMORY.md` instead of retrying failed edits.
- **Active PRs in Review:**
    - **Unified Browser:** [PR #6276](https://github.com/agentscope-ai/CoPaw/pull/6276) introduces a new architecture splitting browser control into a control-plane and execution-plane.
    - **Third-Party Agents:** [PR #6397](https://github.com/agentscope-ai/CoPaw/pull/6397) builds an extensible backend for Codex and Qoder agents, decoupling them from Coding Mode.
    - **QwenPaw Creator:** [PR #6284](https://github.com/agentscope-ai/CoPaw/pull/6284) adds a new app plugin for a script-to-video creation workflow.

### 4. Community Hot Topics
- **[Issue #6307](https://github.com/agentscope-ai/CoPaw/issues/6307) (6 comments):** **v2.0 performance overhead.** Users report a ~2s fixed latency on simple replies in v2.0 that didn't exist in v1.x. This is the highest-comment issue and represents the primary pain point for the v2.0 upgrade path.
    - *Analysis:* The community is highly sensitive to regression in base latency. A fix is likely a top priority for the next patch.
- **[Issue #6344](https://github.com/agentscope-ai/CoPaw/issues/6344) (3 comments):** **Docker hot-reload.** A user requests a "one-click update" button in the web UI to avoid destroying and rebuilding containers, which loses custom runtime environments (Node, ffmpeg).
    - *Analysis:* This reveals a growing base of power users running CoPaw on servers/NAS that need long-lived, stable deployments.
- **[Issue #6342](https://github.com/agentscope-ai/CoPaw/issues/6342) (3 comments):** **ReMe embedding validation.** A user cannot verify if ReMe's vector storage is working after configuring an embedding model.
    - *Analysis:* Indicates a documentation or UX gap—users need a clear signal that advanced features are active.

### 5. Bugs & Stability
- **High Severity:**
    - **[Issue #6307](https://github.com/agentscope-ai/CoPaw/issues/6307): v2.0 performance regression.** A core architectural issue causing ~2s overhead per reply. Fix status: **Open** (no linked PR yet).
- **Medium Severity:**
    - **[Issue #6363](https://github.com/agentscope-ai/CoPaw/issues/6363): Tool call JSON pollution.** Models (GLM, DeepSeek) wrap tool args in markdown fences, breaking all tool execution. Fix status: **Closed** (resolved).
    - **[Issue #6401](https://github.com/agentscope-ai/CoPaw/issues/6401): Cron jobs overwriting session history.** Scheduled tasks configured with `share_session: true` wipe out the target session’s history. Fix status: **Open**.
    - **[Issue #6405](https://github.com/agentscope-ai/CoPaw/issues/6405): MCP Tool not found.** Post v2.0 upgrade, MCP tools fail with "Tool not found". Fix status: **Open**.
- **Low Severity:**
    - **[Issue #6406](https://github.com/agentscope-ai/CoPaw/issues/6406): Windows multiline commands broken.** `execute_shell_command` collapses newlines for PowerShell, breaking here-strings. Fix PR exists: **[#6412](https://github.com/agentscope-ai/CoPaw/pull/6412)** (Open).
    - **[Issue #6379](https://github.com/agentscope-ai/CoPaw/issues/6379): Official plugin blocked by own security policy.** The `GenerateImageGpt` tool is denied by the Governance Policy. Fix status: **Closed**.

### 6. Feature Requests & Roadmap Signals
- **Likely in v2.0.2 / v2.1:**
    - **Multi-line Shell Fix (Windows):** PR [#6412](https://github.com/agentscope-ai/CoPaw/pull/6412) is already open, so this will land soon.
    - **ReMe with Reranking:** PRs [#6398](https://github.com/agentscope-ai/CoPaw/pull/6398) and [#6399](https://github.com/agentscope-ai/CoPaw/pull/6399) are reviewing a backend + UI for re-ranking memory search results.
    - **Dependency on-demand:** PR [#6387](https://github.com/agentscope-ai/CoPaw/pull/6387) is a strong candidate, removing heavy SDKs from core and installing them only when a channel is enabled.
- **Predicted for Future (Backlog Signals):**
    - **Agent-level Token Stats:** [Issue #6392](https://github.com/agentscope-ai/CoPaw/issues/6392) asks for granular per-conversation and per-agent token usage. This is a common enterprise requirement.
    - **Undo Command (/undo):** [Issue #6408](https://github.com/agentscope-ai/CoPaw/issues/6408) requesting the ability to delete/rewrite last conversation turn (like Cherry Studio).

### 7. User Feedback Summary
- **Satisfaction Drivers:**
    - Users appreciate the rapid iteration speed, but this is a double-edged sword (see pain points).
    - The community is building advanced integrations (NAS deployments, specific APIs).
- **Dissatisfaction / Pain Points:**
    - **"Moving Too Fast, Breaking Too Much":** Several users [Issue #6376](https://github.com/agentscope-ai/CoPaw/issues/6376) are frustrated that v2.0 patches are released without sufficient stress testing, causing process crashes due to the new `loop` feature.
    - **"Upgrade is Punishing for Self-Hosters":** Docker users on HDDs ([Issue #6380](https://github.com/agentscope-ai/CoPaw/issues/6380)) face 1.5-hour update cycles, while others lose their custom runtime on every container rebuild.
    - **"Hard to Validate Configuration":** Users find it difficult to confirm if features like ReMe, MCP tools, or the governance policy are actually working as configured.

### 8. Backlog Watch
- **[Issue #6239](https://github.com/agentscope-ai/CoPaw/issues/6239) (Updated 7/23): Windows PATH separator dropped.** Child processes on Windows lose npm globals because the ';' separator is lost when concatenating User + Machine PATH. **Severity: Medium.** This is a subtle but disruptive Windows-only bug that has gone unfixed for 5 days.
- **[Issue #5187](https://github.com/agentscope-ai/CoPaw/pull/5187) (Open since 6/14): Windows Desktop GUI Automation.** A massive feature PR (UIA + Tauri Control Mode) has been open for over a month with significant review activity. It is a major unmerged feature that would unlock powerful Windows desktop automation.

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

```markdown
# ZeptoClaw Project Digest — 2026-07-24

## Today's Overview
ZeptoClaw has had a low-activity day overall, with no new releases and no merged pull requests. Two critical issues remain open and actively tracked, both related to security and stability. One pull request is at the center of the day’s work, targeting subprocess credential exposure and process-reaping problems. The project appears to be in a focused maintenance and hardening phase rather than adding new features. No community engagement (comments or reactions) was recorded on any of today’s items.

## Releases
None. No new releases were published today.

## Project Progress
No pull requests were merged or closed today. The only active PR is:

- [#645 [OPEN] fix(runtime): scrub subprocess secrets and reap timed-out process trees](https://github.com/qhkm/zeptoclaw/pull/645) – This PR aims to fix the subprocess environment credential leak and add proper process-tree termination on timeout. It is the implementation branch for Issue #644. No reviewer comments or CI results are visible yet.

## Community Hot Topics
No issues or PRs received comments or reactions in the last 24 hours. The most actively worked-on items are both reported by the core maintainer, indicating an internal push rather than community-driven discussion.

## Bugs & Stability

### Critical severity (P1-critical)

1. **#644 – bug(safety): scrub subprocess environments and terminate process trees on timeout**  
   [Issue link](https://github.com/qhkm/zeptoclaw/issues/644)  
   **Summary:** Runtime subprocesses inherit the full ZeptoClaw environment, exposing credentials to shell commands. Timeout logic in several runtimes does not ensure spawned process trees are terminated and properly reaped.  
   **Fix:** PR #645 is open and directly addresses this.

2. **#646 – chore(ci): restore Clippy and cargo-deny checks on current toolchain**  
   [Issue link](https://github.com/qhkm/zeptoclaw/issues/646)  
   **Summary:** PR #645 uncovered two CI baseline failures: Rust 1.97.1 introduces 5 new Clippy warnings in existing code, and cargo-deny blocks vulnerable versions of `quick-xml 0.39.2` and `lopdf 0.40.0`. These are not directly caused by the subprocess changes but must be resolved to unblock CI.  
   **Status:** No fix PR yet. This is a blocking chore for safety and toolchain compatibility.

## Feature Requests & Roadmap Signals
No new feature requests were filed today. The project’s current focus is entirely on security hardening (credential isolation) and technical debt (CI restoration). No user-requested features were visible in today’s data.

## User Feedback Summary
No direct user feedback, comments, or reactions were recorded in the last 24 hours. The only activity is from the core team addressing internal technical debt and a safety vulnerability. No indicators of user satisfaction or dissatisfaction are available.

## Backlog Watch
No long-unanswered issues or PRs were identified in today’s snapshot. All open items have been recently touched (created/updated within the last 24 hours). The maintainer appears to be actively handling all current work.

**Project health assessment:** The project is in a quiet, focused maintenance cycle. Two critical safety/CI issues are at the top of the queue, with an implementation PR already submitted for one. The lack of community engagement is notable, but it may simply reflect a low-traffic day rather than a broader trend.
```

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

Here is the project digest for **ZeroClaw** based on the activity snapshot from **2026-07-24**.

---

## ZeroClaw Project Digest — 2026-07-24

### 1. Today's Overview
The ZeroClaw project is experiencing an **extraordinarily high volume of activity**, with 50 updated issues and 50 updated pull requests in the last 24 hours. This signals a major sprint or patch cycle, likely leading toward a **v0.9.0** milestone. The project is heavily focused on **security hardening**, **data integrity**, and **infrastructure scaling**, with three notable S0 (data loss) bugs reported and immediate fix PRs created. While there were no new releases today, the closure of long-standing issues like **Multi-Agent Routing (#2767)** and the progression of the **PostgreSQL session backend PR (#9251)** indicate significant architectural advances.

### 2. Releases
**None.** No new versions were published in the last 24 hours. The last release remains v0.8.3.

### 3. Project Progress
**Merged/Closed PRs (3):**
No specific merges were highlighted in the top 20, but the close of **11 issues** indicates active cleanup and stabilization.

**Key Advances:**
- **Multi-Agent Routing (#2767)** was closed, marking the completion of a major feature allowing isolated agents and multiple channel accounts to run in a single gateway.
- **Discord Channel Filtering (#6378)** was resolved, allowing operators to restrict bot responses to specific channels via an `allowed_channels` config field.
- **Logging Stream Fix (#4721)** was resolved: ZeroClaw now correctly logs to stderr instead of stdout, fixing CLI pipe issues.
- **Cached Token Cost Accounting (#7248)** was closed, meaning provider-reported cached input tokens are now persisted and included in billing data.
- **High-Entropy Token Redaction Toggle (#4832)** was resolved, adding a config option to disable false-positive redactions in the LeakDetector.
- **Message Channel Delivery Tool (#5145)** was closed, adding a `send_channel_message` tool for direct user delivery.
- **Cron Announce Mode (#6510)** was closed, adding an opt-in flag to deliver only the final assistant message from cron jobs.

### 4. Community Hot Topics
The community is deeply engaged in **security and architecture discussions**, with the following items receiving the most attention:

- **A2A Protocol Interoperability (#3566)** (9 comments, 7 👍) — This tracker is the most popular open item, reflecting strong demand for ZeroClaw to speak the Agent2Agent protocol. It is a high-risk, accepted tracker that will define v0.9.0’s multi-agent capabilities. [Link](https://github.com/zeroclaw-labs/zeroclaw/issues/3566)
- **KeySource Trait RFC (#9127)** (7 comments) — A security RFC proposing classification of master-key material by deployment form. This is a foundational architecture discussion likely to shape the credential encryption framework. [Link](https://github.com/zeroclaw-labs/zeroclaw/issues/9127)
- **Multi-Agent Routing (#2767)** (7 comments, 9 👍) — Now closed, but it was the most "liked" issue, showing strong community desire for multi-profile/multi-account support. [Link](https://github.com/zeroclaw-labs/zeroclaw/issues/2767)
- **PostgreSQL Session Backend PR (#9251)** — The largest PR (size:XL), this is a major infrastructure shift from SQLite-only to PostgreSQL support, with an in-depth design discussion. [Link](https://github.com/zeroclaw-labs/zeroclaw/pull/9251)

**Underlying Needs:** The community is demanding enterprise-grade features: **multi-agent orchestration**, **secure credential handling**, and **database scalability**. The high engagement on the A2A tracker suggests users want ZeroClaw to be an interoperable node in a broader agent ecosystem.

### 5. Bugs & Stability
**Today’s bug landscape is critical, with three S0 (data loss) reports:**

| Severity | Issue | Component | Fix PR Exists? |
|----------|-------|-----------|----------------|
| **S0** | **Telegram long-poll advancement before delivery (#9188)** — Crash can lose inbound voice/attachments. | `channel:telegram` | ✅ **Yes** — PR #9314 advances offset only after delivery or permanent skip. |
| **S0** | **WeChat sync cursor persisted before enqueue (#9187)** — Crash loses inbound messages. | `channel:wechat` | ✅ **Yes** — PR #9313 persists cursor only after batch is enqueued. |
| **S1** | **Cron jobs lack wall-clock timeout (#9191)** — No kill switch for stuck agent jobs. | `runtime/cron` | ❌ No PR yet. |
| **S1** | **Landlock sandbox locks the daemon itself (#9204)** — Breaks SQLite and system access. | `security/sandbox` | ❌ No PR yet. |
| **S1** | **Desktop installer fails on Windows (#9290)** — Missing `TaskDialogIndirect` API. | `desktop/tauri` | ❌ No PR yet. |
| **S1** | **Config flush can overwrite concurrent writes (#9284)** — Race condition corrupts config. | `runtime/daemon` | ✅ **Yes** — PR #9312 serializes RPC config writes. |
| **S2** | **Web fetch returns garbage for compressed responses (#9207)** — gzip/brotli not decoded. | `tool:web` | ❌ No PR yet. |
| **S2** | **Telegram aliases dropped after config reload (#9236)** — Fresh config lost silently. | `config` | ✅ **Yes** — PR #9309 keeps partial channel aliases through salvage. |
| **S3** | **Nested set_prop masks invalid values (#9285)** — Confusing error messages. | `config/onboarding` | ❌ No PR yet. |
| **S3** | **Discord typing indicator stuck after reload (#9198)** — UI bug. | `channel:discord` | ❌ No PR yet. |

**Critical Stability Signal:** The three S0 bugs are all in **channel message processing** (Telegram, WeChat), indicating a systemic issue with the `get_updates` → `save_sync_data` → `enqueue` ordering. The team has responded rapidly with matching fix PRs, which is a strong sign of project health.

### 6. Feature Requests & Roadmap Signals
**High-Confidence Next-Release Features (likely v0.9.0):**
- **PostgreSQL Session Backend (#9251)** — A massive shift from SQLite, enabling multi-process and HA deployments. This is the top infrastructure PR.
- **Telegram Multi-Message Streaming (#8561)** — Adds paced multi-message delivery to Telegram, matching Discord/Matrix.
- **Goal Command Admission (#8689)** — A shared `/goal` command across all channels for starting, pausing, and managing objectives.
- **Authenticated HTTP SOP Fan-in (#9203)** — Enables webhook-triggered SOP execution over HTTP.
- **ScopedToolRegistry Refactor (#9319)** — Seals the engine tool registry for better security and test isolation.

**Longer-Term Signals:**
- **TOTP for Cross-Channel Approval (#3767)** — Requesting 2FA for destructive shell commands across all channels. Given the security focus, this is likely for v0.9.0 or v0.9.1.
- **Message Lifecycle Hooks (#3696)** — Shell hooks before/after agent message processing. High interest for integration workflows.
- **Eval Results Dashboard (#9228)** — Longitudinal pass-rate trends for capability suites. A "nice-to-have" facing increasing community pressure.

### 7. User Feedback Summary
**Common Pain Points:**
- **Tool reliability:** The `web_fetch` bug (#9207) returning binary garbage for compressed responses is a workflow blocker for users relying on web scraping.
- **Data integrity fears:** The three S0 bugs (Telegram/WeChat message loss, cron timeout) erode trust in message reliability. Users are reporting "stuck typing indicators" and "lost inbound voice."
- **Windows deployment:** The desktop installer failure (#9290) is blocking new Windows adopters entirely.
- **Telegram alias setup:** The config reload bug (#9236) is causing frustration during initial bot setup on Telegram.

**Positive Signals:**
- Users are actively contributing features (e.g., `send_channel_message` tool, cron announce mode), indicating a healthy contributor ecosystem.
- The community is engaging in high-level architecture discussions (A2A, KeySource trait), suggesting experienced developers are invested in ZeroClaw’s long-term direction.

### 8. Backlog Watch
The following items require maintainer attention:

- **Browser Screenshot Path Validation PR (#8741)** — Open since 2026-07-05, needs review. This is a security fix for arbitrary path writes. [Link](https://github.com/zeroclaw-labs/zeroclaw/pull/8741)
- **File Download SSRF Gate PR (#8713)** — Open since 2026-07-04, needs author action. Closes the last SSRF surface from a July security audit. [Link](https://github.com/zeroclaw-labs/zeroclaw/pull/8713)
- **npm Audit Failure (#9235)** — Open since 2026-07-21, with 3 high/critical vulnerabilities in `@redocly/openapi-core`. This is a CI pipeline blocker that could affect web asset security. [Link](https://github.com/zeroclaw-labs/zeroclaw/issues/9235)
- **TOTP Enforcement (#3767)** — Open since March 2026, accepted but no PR. Given the current security sprint, this should be a priority for v0.9.0. [Link](https://github.com/zeroclaw-labs/zeroclaw/issues/3767)
- **Memory Change History (#3672)** — Open since March 2026, no PR. Users want version control for agent workspace files. [Link](https://github.com/zeroclaw-labs/zeroclaw/issues/3672)

---

**Project Health Conclusion:** ZeroClaw is in a **high-velocity security and stability cycle**. The rapid creation of fix PRs for S0 bugs is commendable, but the volume of open PRs (47) requiring review is a bottleneck. The project is clearly maturing toward enterprise readiness, but the next release should prioritize resolving the backlog of high-severity bugs before shipping new features.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/kky-wollu/agents-radar).*