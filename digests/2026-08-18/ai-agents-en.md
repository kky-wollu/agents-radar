# OpenClaw Ecosystem Digest 2026-08-18

> Issues: 500 | PRs: 500 | Projects covered: 13 | Generated: 2026-08-17 22:28 UTC

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

# OpenClaw Project Digest — 2026-08-18

## 1. Today's Overview

OpenClaw maintains a **high-velocity development cadence** with 500 issues and 500 PRs updated in the last 24 hours, reflecting a very active maintainer and contributor ecosystem. The project shows **moderate triage bottleneck**: 409 open PRs and 489 open issues indicate a large backlog awaiting maintainer review, with 91 PRs merged/closed in the period demonstrating steady throughput. No new releases shipped today, suggesting work is consolidating on a next-version milestone rather than patch releases. The issue tracker shows heavy concentration on **reliability and state-management bugs** (session-state, message-loss, crash-loop impacts dominate top issues), indicating the project is prioritizing hardening of the core runtime over new features. The presence of `clawsweeper` automation labels on nearly every top issue confirms an active bot-assisted triage pipeline.

## 2. Releases

**No new releases published in the last 24 hours.**

The project is between release cycles; the last referenced version is `2026.6.10` (mentioned in issue #96834). Based on PR activity, the next release is likely to focus on reliability fixes for session state, message delivery, and the Codex integration.

## 3. Project Progress

91 PRs were merged/closed in the last 24 hours. Notable items from the closed/merged set:

- **[#120900 — feat(ui): review install policy warnings](https://github.com/openclaw/openclaw/pull/120900)** — Closed. Adds an authenticated admin review flow for install-policy warnings in the Control UI, accepting the new `acknowledgeInstallPolicyWarning: true` option in `plugins.install`. Complements the earlier security-boundary work in #116489.
- **[#116489 — feat(security): require acknowledgement for install policy warnings](https://github.com/openclaw/openclaw/pull/116489)** — Closed. Introduces the `security.installPolicy` `warn` level, requiring an authorized operator to acknowledge a suspicious plugin/skill install before it proceeds. Interactive CLI installs show bounded reasons and require the exact target name.

Open PRs with strong progress signals (ready for maintainer look):
- **[#125412 — fix(gateway): restore external Tailscale Serve and Funnel proxies](https://github.com/openclaw/openclaw/pull/125412)** — P0, fixes `proxy_attribution_required` rejection for external Tailscale routes.
- **[#125407 — fix(agents): stop canceled subagents reporting timeouts](https://github.com/openclaw/openclaw/pull/125407)** — Fixes erroneous timeout reporting when a subagent is canceled with a bare `aborted: true`.
- **[#123482 — fix: session list stalls while loading workspace state](https://github.com/openclaw/openclaw/pull/123482)** — Fixes Control UI stalls from scanning hidden workspace transcripts under load.
- **[#123535 — fix(ui): avoid session catalog refresh storms](https://github.com/openclaw/openclaw/pull/123535)** — Limits native session-catalog scans to real node changes, reducing CPU/network churn.
- **[#125384 — refactor(workers): make worker turns node-only](https://github.com/openclaw/openclaw/pull/125384)** — Removes the deprecated reverse-worker carrier from provider configuration.

## 4. Community Hot Topics

- **[#77598 — Track live dev agent behavior and trajectory](https://github.com/openclaw/openclaw/issues/77598)** — 23 comments. A running-notes observational watch on a maintainer dev agent. Signals the community's deep interest in how OpenClaw agents behave in real dev workflows; likely a transparency/fidelity issue.
- **[#91009 — Codex PreToolUse native hook relay spawns CPU-bound processes and stalls gateway RPC](https://github.com/openclaw/openclaw/issues/91009)** — 20 comments, 2 👍. Critical reliability issue with the Codex integration, burning CPU and stalling RPC. **P1 platinum hermit** rating; needs live repro and product decision.
- **[#68596 — Feature Request: Configurable streaming watchdog timeout threshold](https://github.com/openclaw/openclaw/issues/68596)** — 15 comments, 8 👍. Users running long-reasoning models (kimi-k2.5, DeepSeek-R1) hit false-positive watchdog resets. Indicates a real mismatch between model behavior and OpenClaw's timeouts.
- **[#62505 — Coding Agent never completes anything (regression)](https://github.com/openclaw/openclaw/issues/62505)** — 15 comments, 1 👍. The agent "just doesn't do _anything_ apart from vague status updates." A **P1 diamond lobster** regression: user frustration with a formerly-working core workflow.
- **[#96834 — WhatsApp image wedge: multimodal run strands active work](https://github.com/openclaw/openclaw/issues/96834)** — 15 comments. Image messages wedge the main lane for ~3 minutes pre-processing. **P1 platinum hermit**; reproducible on 2026.6.10.
- **[#38327 — "Cannot convert undefined or null to object" with google-vertex/gemini-3.1-pro-preview](https://github.com/openclaw/openclaw/issues/38327)** — 14 comments, 3 👍. **P1 platinum hermit** regression in 2026.3.2; auth-provider impact.

## 5. Bugs & Stability

**Critical (P0):**
- **[#70903 — Persistent file-based provider cooldown blocks user for hours after billing recovery](https://github.com/openclaw/openclaw/issues/70903)** — **P0 diamond lobster**. A 402 triggers a persistent `disabledUntil` timestamp that survives restarts, locking the user out even after topping up. No fix PR linked.
- **[#125412 (PR)](https://github.com/openclaw/openclaw/pull/125412)** — **P0 security-boundary** PR fixes external Tailscale proxy rejection, currently waiting on author.

**High (P1):**
- **[#91009 — Codex PreToolUse hook CPU-bound processes / gateway RPC stall](https://github.com/openclaw/openclaw/issues/91009)** — platinum hermit; needs live repro.
- **[#96834 — WhatsApp image wedge / multimodal run strand](https://github.com/openclaw/openclaw/issues/96834)** — platinum hermit; reproducible.
- **[#38327 — "Cannot convert undefined or null to object" (Gemini 3.1-pro-preview)](https://github.com/openclaw/openclaw/issues/38327)** — platinum hermit; needs live repro.
- **[#78493 — `sudo openclaw update` mixed ownership → doctor overwrites config](https://github.com/openclaw/openclaw/issues/78493)** — platinum hermit; macOS/LaunchAgent specific.
- **[#62505 — Coding Agent never completes anything](https://github.com/openclaw/openclaw/issues/62505)** — diamond lobster; regression, source repro available.
- **[#97616 — Leaked unreaped hook/tool child processes (zombies)](https://github.com/openclaw/openclaw/issues/97616)** — gold shrimp, crash-loop impact.
- **[#53408 — Write/exec tool parameters silently dropped after long conversations](https://github.com/openclaw/openclaw/issues/53408)** — platinum hermit; 15+ turn heavy tool usage triggers empty arguments.
- **[#86215 — Codex OAuth refresh failures wedge agent for hours](https://github.com/openclaw/openclaw/issues/86215)** — platinum hermit; no alerting or profile rotation.

**Medium (P2) — notable:**
- **[#77930 — Discord channel not loaded regression in 2026.5.4](https://github.com/openclaw/openclaw/issues/77930)** — silver shellfish; linked PR open.
- **[#51429 — Hardcoded work path (`/Users/wangtao`) merged and published](https://github.com/openclaw/openclaw/issues/51429)** — diamond lobster; user-facing config bug.
- **[#62328 — node:sqlite missing FTS5 → memory search keyword fallback broken](https://github.com/openclaw/openclaw/issues/62328)** — diamond lobster.

**Fix PRs in flight:** #125407 (subagent timeout), #125015 (Copilot Claude auto-compaction silence), #120443 (Codex compaction binding), #125432 (Matrix case-sensitivity), #125290 (macOS Bash CI), #125377 (configure system agent), #125403 (plugin artifact reload).

## 6. Feature Requests & Roadmap Signals

Next-version candidates based on community demand and maintainer attention:

- **Streaming watchdog configurability** ([#68596](https://github.com/openclaw/openclaw/issues/68596), 8 👍) — highly requested for long-reasoning model support.
- **Configurable upload size limit for Control UI** ([#71142](https://github.com/openclaw/openclaw/issues/71142)) — hardcoded 5MB cap is a usability blocker.
- **Multi-model embedding / memory architecture** ([#63990](https://github.com/openclaw/openclaw/issues/63990), [#60572](https://github.com/openclaw/openclaw/issues/60572) — 3 👍) — both propose multi-index/slot memory; signals a possible memory refactor.
- **Fallback model chains for compaction/LCM** ([#56781](https://github.com/openclaw/openclaw/issues/56781)) — resilience for model rate-limits.
- **Per-agent dreaming configuration** ([#67413](https://github.com/openclaw/openclaw/issues/67413), 5 👍) — OOM risk in multi-agent setups.
- **MathJax/LaTeX support in Control UI** ([#42840](https://github.com/openclaw/openclaw/issues/42840), 10 👍) — highest community demand in the feature set.
- **Multiple Teams bots per gateway** ([#71058](https://github.com/openclaw/openclaw/issues/71058)) — active PR **#112811** is in "needs proof" state, showing real implementation effort.
- **YAML config support** ([#45758](https://github.com/openclaw/openclaw/issues/45758), 2 👍) — DX/readability win.
- **Session context bloat reduction** ([#67419](https://github.com/openclaw/openclaw/issues/67419), 2 👍) — 20–30% token waste on bootstrap file re-injection is a strong cost-savings signal.

## 7. User Feedback Summary

**Satisfaction signals:**
- Users are running OpenClaw as "family and business assistant" (Telegram, automations, cron, Home Assistant) and describe it as "genuinely part of our daily workflow" ([#73537](https://github.com/openclaw/openclaw/issues/73537)).
- Developers rely on the coding agent for "pumping out work for weeks" until a regression broke it ([#62505](https://github.com/openclaw/openclaw/issues/62505)).

**Key pain points:**

1. **Session-state reliability is the #1 user concern.** Multiple platinum-hermit bugs around `session-state` and `message-loss` impacts: WhatsApp image wedges, subagent completion loss, A2A duplicate messages, and tool-parameter drops after long conversations. Users report silent failures that degrade trust.

2. **The Codex integration is a double-edged sword.** OAuth refresh failures ([#86215](https://github.com/openclaw/openclaw/issues/86215)) and CPU-bound hook processes ([#91009](https://github.com/openclaw/openclaw/issues/91009)) suggest the native Codex path needs serious hardening before it can be considered production-grade.

3. **Config usability friction.** Hardcoded paths ([#51429](https://github.com/openclaw/openclaw/issues/51429)), hardcoded 5MB upload limits ([#71142](https://github.com/openclaw/openclaw/issues/71142)), and hardcoded 25-item message list caps ([#71452](https://github.com/openclaw/openclaw/issues/71452)) frustrate power users.

4. **UI/UX criticism is growing.** "The UI is hard to navigate," "feels dense," "looks too much like AI-generated code" ([#75947](https://github.com/openclaw/openclaw/issues/75947)). The UI improvement PRs from `vyctorbrzezowski` (#125242, #125241) and `jesse-merhi` (#123535) show the team is listening.

5. **Watchdog false positives at scale.** Users with long-reasoning models (DeepSeek-R1, Kimi) report the 30s watchdog fires too aggressively, killing legitimate runs.

**Dissatisfaction signals:**
- A user reported a **hardcoded personal path** (`/Users/wangtao`) merged to production ([#51429](https://github.com/openclaw/openclaw/issues/51429)) — a process/QA failure.
- Silent failures (model switch with large context, compaction failures without fallback) erode confidence.

## 8. Backlog Watch

Long-unanswered issues needing maintainer attention (marked `needs-maintainer-review` / `needs-product-decision`):

- **[#62505 — Coding Agent never completes anything](https://github.com/openclaw/openclaw/issues/62505)** — Created 2026-04-07, P1 diamond lobster regression, 15 comments, **no fix PR since April**. A core workflow is broken for weeks — this should be a priority.
- **[#51429 — Hardcoded work path merged](https://github.com/openclaw/openclaw/issues/51429)** — Created 2026-03-21, P2 diamond lobster, 12 comments, open for nearly 5 months. Self-inflicted config bug.
- **[#53540 — "Network connection lost" on large tool-call parameters](https://github.com/openclaw/openclaw/issues/53540)** — Created 2026-03-24, P1 diamond lobster, 8 comments, no fix PR.
- **[#53408 — Write/exec tool parameters silently dropped](https://github.com/openclaw/openclaw/issues/53408)** — Created 2026-03-24, P1 platinum hermit, 11 comments, no fix PR.
- **[#67777 — Subagent completion delivery can be lost](https://github.com/openclaw/openclaw/issues/67777)** — Created 2026-04-16, P1 diamond lobster, 12 comments, `clawsweeper-recovery-stuck` label applied — the bot itself is stuck.
- **[#51429 — WhatsApp backfill after reconnection](https://github.com/openclaw/openclaw/issues/50093)** — Created 2026-03-19, P1 platinum hermit, 13 comments, message-loss impact, no linked PR.
- **[#39476 — A2A sessions_send duplicate messages](https://github.com/openclaw/openclaw/issues/39476)** — Created 2026-03-08, P1 diamond lobster, 13 comments; a `linked-pr-open` label exists but the PR status is unclear.
- **[#71058 — Multiple Teams bots](https://github.com/openclaw/openclaw/issues/71058)** — Created 2026-04-24, P2; active PR #112811 is in "needs proof" for weeks, suggesting the maintainer-review pipeline is slow for large PRs.

**Blocked automation:** 12 of the top issues carry the `clawsweeper-recovery-stuck` label, meaning the auto-triage bot cannot make progress — these need human intervention to break the loop.

---

## Cross-Ecosystem Comparison

# Cross-Project Ecosystem Comparison Report
**Date:** 2026-08-18

---

## 1. Ecosystem Overview

The personal AI assistant/agent open-source landscape is in a period of intense maturation, marked by a shift from greenfield feature development to **reliability hardening, extensibility, and operational scalability**. Projects are converging on common pain points: session-state integrity, cross-platform compatibility (especially Windows), provider resilience, and architectural seams for third-party extensions. The ecosystem shows **healthy contributor engagement** across tiers, from high-velocity core projects (OpenClaw, NanoBot, IronClaw) to community-driven stabilization efforts (PicoClaw, Moltis, CoPaw). Notably, **security and governance** are now first-class concerns, with multiple projects implementing install-policy acknowledgements, log redaction, and per-execution confirmation tiers. The emergence of **cross-agent orchestration** (LobsterAI, NanoBot session mentions, ZeroClaw goal-mode RFC) suggests the next architectural frontier is inter-agent communication and federated workflows. However, maintainer bandwidth remains the critical constraint across nearly all projects, with significant PR/issue backlogs and RFCs awaiting decisions.

---

## 2. Activity Comparison

| Project | Issues Updated (24h) | PRs Updated (24h) | Merged/Closed PRs (24h) | Release Status | Health Score |
|---|---|---|---|---|---|
| **OpenClaw** | 500 | 500 | 91 | Between cycles (last: 2026.6.10) | **7.5/10** — High velocity, but 489 open issues + 409 open PRs indicate triage bottleneck |
| **NanoBot** | 3 | 15 | 5 | Accumulating (no tag) | **8/10** — Responsive merges, active stabilization sprint, low backlog |
| **Hermes Agent** | 50 | 50 | 9 | v0.20.3 (Aug 16, patch) | **6.5/10** — Fast shipping (125 PRs in patch) but P1 install/update regressions |
| **PicoClaw** | 4 | 4 | 3 | Between cycles | **7.5/10** — Same-day bug-fix turnaround, responsive maintainers |
| **NanoClaw** | 4 | 34 | 21 | v2.1.48 (recent) | **8/10** — Massive merge wave, healthy community contribution, 2 high-severity bugs with fix PRs pending |
| **NullClaw** | 0 | 1 | 0 | None | **3/10** — Effectively dormant; 64-day-old dependency PR unmerged |
| **IronClaw** | 28 | 44 | 16 | Between cycles | **8.5/10** — High throughput, responsive bug-to-fix pipeline (#7714→#7717 in 24h), strategic epics |
| **LobsterAI** | 7 | 21 | 17 | None | **6/10** — Backlog-clearance wave (stale PRs), but core bugs from April unresolved |
| **Moltis** | 0 | 11 | 6 | Accumulating | **8/10** — Steady, clean merges, responsive issue closure |
| **CoPaw** | 14 | 35 | 22 | v2.1.0 | **8/10** — Rapid triage (6 issues closed), active UI/UX polish, 3 first-time contributors |
| **TinyClaw** | 0 | 0 | 0 | — | **N/A** (dormant) |
| **ZeptoClaw** | 0 | 0 | 0 | — | **N/A** (dormant) |
| **ZeroClaw** | 50 | 50 | 9 | v0.8.4 (pre-0.9.0) | **7/10** — Architecturally active (RFC-heavy), but maintainer bandwidth is critical constraint |

---

## 3. OpenClaw's Position

### Advantages vs. Peers
- **Dominant community mass:** 500+ issues and PRs updated in 24h — an order of magnitude more engagement than any peer. This translates to faster bug discovery and a larger contributor pool.
- **Comprehensive platform breadth:** Multi-channel (Telegram, WhatsApp, Discord, Matrix), Codex integration, Control UI, plugin system, and enterprise-grade security features (install-policy warnings, authenticated admin review) — a "full-stack" assistant.
- **Bot-assisted triage:** The `clawsweeper` automation pipeline (though stuck on 12 items) signals a level of tooling maturity peers lack.
- **Real-world trust:** Users describe OpenClaw as "genuinely part of our daily workflow" — a level of production dependence not yet seen in smaller projects.

### Technical Approach Differences
- **Monolithic core + plugin ecosystem:** Unlike NanoBot's lighter agent framework or IronClaw's durable-runtime focus, OpenClaw ships a batteries-included runtime with enterprise-oriented security boundaries.
- **Runtime-owned state:** OpenClaw's session/state management is centralized, and the cluster of session-state bugs indicates the complexity cost of this approach. IronClaw and ZeroClaw are architecting around runtime-ownership as a first-principle; OpenClaw is retrofitting reliability.

### Community Size Comparison
| Project | Approximate Community Signal |
|---|---|
| OpenClaw | **Very Large** (4× the daily activity of next closest) |
| IronClaw / ZeroClaw | Large (50+ issues and PRs daily, core-team driven) |
| NanoClaw / CoPaw | Medium (30+ PRs daily, balanced core/community) |
| NanoBot / Moltis / PicoClaw | Small but engaged (5–15 PRs daily, responsive) |
| LobsterAI / Hermes Agent | Medium (20–50 PRs) but with stale-bug risk |
| NullClaw / TinyClaw / ZeptoClaw | Dormant |

**Bottom line:** OpenClaw is the ecosystem's reference implementation and community hub. Its reliability bugs are the ecosystem's biggest pain points; its fixes will set the template for others. The competitive risk is IronClaw (near-enterprise durability) and ZeroClaw (OpenAI-protocol interop) executing faster on architecture.

---

## 4. Shared Technical Focus Areas

| Focus Area | Projects | Specific Needs |
|---|---|---|
| **Session/State Reliability** | OpenClaw, Hermes Agent, NanoBot, IronClaw | Message-loss prevention, session-state corruption fixes, cross-session context, session catalog stalls |
| **Provider Resilience & Fallbacks** | OpenClaw, NanoBot, Hermes Agent, IronClaw | Fallback model chains, provider exception handling, OAuth refresh failures, codex integration hardening, fallback diagnostics transparency |
| **Cross-Platform Parity (esp. Windows)** | NanoBot, Hermes Agent, ZeroClaw, LobsterAI | Windows-safe commands (curl/Invoke-WebRequest), update executable locks, CI coverage, EMFILE errors, console encoding |
| **Configuration Usability** | OpenClaw, Hermes Agent, NanoClaw, Moltis, LobsterAI | YAML support, configurable timeouts/limits (upload size, message caps), env-override priority, config-write conflicts, silent overwrites |
| **Goal-Directed Agent Loops** | NanoBot, ZeroClaw, CoPaw | Avoiding repeated clarification loops, goal-mode multi-turn execution, complete_goal serialization bugs, bounded agent turns |
| **Observability & Telemetry** | OpenClaw (dev trajectory), NanoClaw (ClawMetry dashboard), IronClaw (failure taxonomy), CoPaw (task telemetry) | Session history queryability, live agent-behavior tracking, failure-cause diagnostics, benchmark-driven stability |
| **Interoperability & Extensibility** | ZeroClaw (Chat Completions profile), LobsterAI (A2A/orchestration), NanoBot (session mentions), CoPaw (MCP 2.0), IronClaw (ACP serve) | OpenAI-protocol APIs, agent-to-agent communication, standardized tool contracts, protocol-level integrations |
| **Watchdog/Timeout Tuning** | OpenClaw (streaming watchdog), NanoBot (Telegram polling) | Configurable thresholds, false-positive suppression for long-reasoning models |

---

## 5. Differentiation Analysis

| Project | Feature Focus | Target Users | Technical Architecture |
|---|---|---|---|
| **OpenClaw** | Full-stack personal assistant, enterprise security, multi-channel | Power users, families, small businesses, dev-agent coders | Monolithic runtime + plugins, centralized session-state, Control UI, Codex integration |
| **NanoBot** | Lightweight agent framework, goal management, WebUI features | Developers embedding agents in workflows, cost-conscious users | Modular framework, gateway/client lease model, TypeScript TUI, WebUI (side convos, mentions) |
| **Hermes Agent** | Cross-platform desktop client, BOTS (multi-bot) support, stable releases | Desktop-first users, Windows/Mac/Linux, downstream Docker consumers | Desktop app + gateway, session-based bots, SQLite DB (with known leak), Desktop BOTS sidebar |
| **PicoClaw** | Minimal, channel-focused (Telegram, Slack, IRC, Weixin) | Hobbyists, self-hosters, channel-specific deployments | Lightweight Go-based agent, per-channel integrations, config via JSON/env |
| **NanoClaw** | **Extensibility via hooks/seams** (channels, router, delivery, tools), cross-session context | Developers building custom channel/skill integrations | Modular Node.js, hook-based extension architecture, MCP tools, cross-session context groups |
| **NullClaw** | (Dormant) | — | Docker-based, Alpine image |
| **IronClaw** | **Durable runtime**, write-pressure optimization, automation, notification inbox | Enterprise/ops teams running scheduled automations at scale | Rust-based durable store, libSQL, WASM tools, resource governor, notification contracts |
| **LobsterAI** | Desktop client w/ rich UX (Cowork), multi-agent orchestration, dsh engine provider | GUI users, Chinese-market (netease-youdao), multi-agent workflows | Electron app, OpenClaw runtime base, per-agent directories, DeepSeek Harness/dsh engine |
| **Moltis** | Steady reliability (heartbeats, browser shadow DOM, Files library) | Scheduler/automation users, browser automation needs | Rust-based, cargo registry, ACP-based external agents (MiniMax Code) |
| **CoPaw** | Charm UI/UX polish, MCP integration, media handling, per-channel config (requested) | Console-first users, multi-channel (DingTalk, WeChat, Feishu), Chinese-dominant | Agent console (PawApps), AnySearch integration, MCP 2.0, compact background task panel |
| **ZeroClaw** | **Architecture-first**: RFC-driven 0.9.0, runtime-owned conversations, security pipelines, Chat Completions interop | Developers adopting ZeroClaw as an agent backend, personal coding assistant via ZeroCode | Runtime-owned state, WASM plugins, SOP contracts, security decision overlays, goal-mode |

---

## 6. Community Momentum & Maturity

### Activity Tiers

| Tier | Projects | Characteristics |
|---|---|---|
| **Rapid Iteration (High Velocity)** | OpenClaw, IronClaw, ZeroClaw, CoPaw, NanoClaw | 30+ PRs daily, active epic/RFC pipeline, large maintainer teams or strong contributor base |
| **Stabilizing (Moderate Velocity)** | NanoBot, Moltis, PicoClaw, Hermes Agent | 5–15 PRs daily, focused on bug fixes, dependency bumps, incremental features; Hermes in "fix regressions" phase |
| **Dormant/Stagnant** | NullClaw, TinyClaw, ZeptoClaw | Zero or near-zero activity; dependency hygiene unresolved |

### Maturity Assessment
- **Most mature (operationally):** **IronClaw** — 8.5/10 health; strategic epics (write-pressure reduction), benchmark-driven testing (daily failure taxonomy), and responsive bug-to-fix pipeline indicate a project scaling toward production-enterprise use.
- **Most mature (community):** **OpenClaw** — 7.5/10; though backlog-heavy, the sheer community mass provides resilience. The 12 `clawsweeper-recovery-stuck` items are a human-intervention red flag.
- **Most architecturally ambitious:** **ZeroClaw** — Pre-0.9.0 RFC-driven hardening of runtime-owned security/state is the boldest architectural bet. Execution risk on maintainer bandwidth is high.
- **Most contributor-friendly:** **NanoClaw & CoPaw** — First-time contributor PRs merged rapidly; healthy balance of core-team and community work.

---

## 7. Trend Signals

**1. Reliability is the new feature.** Across projects, "silent failures" are the loudest negative signal: cron jobs dying silently (Hermes), watchdog false-positives (OpenClaw), silent Telegram outages (NanoBot), dropped tool parameters (OpenClaw), misleading fallback logs (ZeroClaw). Users would trade new features for deterministic, self-explanatory behavior.

**2. Cross-platform is non-negotiable.** Windows-specific failures (Hermes update lock, NanoBot curl alias, ZeroClaw test suite, LobsterAI Electron context menu) indicate the user base has moved beyond Linux-only. Scheduled CI for Windows/macOS (ZeroClaw #9398) will become a universal pattern.

**3. Provider resilience and cost control are converging.** Users are demanding fallback chains, configurable timeouts, and spend firewalls (NanoBot #5409). The era of "vibe-coding" on a single model is over; production agents need provider-agnostic routing and cost governance.

**4. Agent interoperability is the next battleground.** ZeroClaw's Chat Completions profile, LobsterAI's A2A advocacy, NanoBot's session mentions, and IronClaw's ACP serve command all point to a future where agents speak standard protocols to each other and existing tools. The "walled garden" assistant is losing to the "protocol-backed" agent.

**5. Configuration wants to be code.** Users are asking for YAML support (OpenClaw), env-override priority (PicoClaw), patch-style config updates (Moltis), and are being burned by silent overwrites (LobsterAI, Hermes). The message: configuration should be **diffable, reviewable, and reproducible** — treat it like infrastructure-as-code.

**6. Observability is a decision-making input.** IronClaw's daily failure taxonomy, NanoClaw's ClawMetry dashboard, OpenClaw's dev-trajectory issue — these signal a shift from "does it work?" to "how does it work, and why did it fail?" Agent systems need forensic tooling.

**7. Security is becoming a proactive practice.** Install-policy acknowledgements (OpenClaw), log redaction (LobsterAI), Slack redirect validation (NanoBot), allowlist-vs-ask-deny shell policies (ZeroClaw), bearer-auth for MCP (IronClaw) — security is moving from reactive patching to preventative defaults.

**8. The "agent as employee" use case is expanding.** From "coding agent that pumps out work" (OpenClaw #62505) to goal-mode multi-turn execution (ZeroClaw #8303) to "main agent orchestrating sibling agents" (LobsterAI #1644), users are treating agents as semi-autonomous workers that need robust task-scoping, budget governance, and inter-agent communication.

---

*Report generated 2026-08-18 from community digest data.*

---

## Peer Project Reports

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot Project Digest — 2026-08-18

## 1. Today's Overview

NanoBot saw a flurry of activity on **August 17-18, 2026**, with **15 pull requests** updated in the last 24 hours (10 still open, 5 merged/closed), alongside **3 issues** (2 active, 1 closed). This is a notably high-velocity day, with **5 PR merges clustered around gateway, CLI, Telegram, and goal-handling fixes**, signaling an active stabilization sprint. The project is clearly approaching a maturity phase where infrastructure concerns — Windows compatibility, process lifecycle, logging, and provider resilience — dominate over greenfield feature work. Notably, the `#4864` **complete_goal tool-call infinite loop bug** remains open with 7 comments, suggesting persistent pain in agent goal-management. New WebUI features (side conversations, follow-up suggestions, session mentions) are also in review, indicating ongoing UX investment.

## 2. Releases

**No new releases** were published in the last 24 hours. The project appears to be accumulating a substantial body of PRs (5 merged today alone) without a tagged release, suggesting a significant version bump may be imminent. Users tracking stable builds should watch for a flurry of these fixes to land in the next tag.

## 3. Project Progress

Five PRs were merged/closed, indicating concrete progress:

- **[PR #5416 (merged) — fix(gateway): stabilize process identities](https://github.com/HKUDS/nanobot/pull/5416)** by Re-bin: Replaces locale-dependent `ps lstart` with native macOS `proc_pidinfo` birth timestamps for reliable process identity comparison — a cross-platform fix for gateway client lease management.
- **[PR #5301 (merged) — fix(telegram): bridge stdlib logging and detect stalled polling](https://github.com/HKUDS/nanobot/pull/5301)** by QQQ300kuai: Splits low-risk observability from #5156 — bridges stdlib logging into loguru and adds a liveness check (logs-only, no teardown). Addresses the silently-stalled Telegram polling issue.
- **[PR #5156 (merged) — fix(telegram): recover from silently stalled polling](https://github.com/HKUDS/nanobot/pull/5156)** by QQQ300kuai: The full watchdog fix for #5171 — rebuilds stalled Telegram polling connection pools after transient network failures (e.g., unstable proxies).
- **[PR #5410 (merged) — fix(goal): stop repeating clarification replies](https://github.com/HKUDS/nanobot/pull/5410)** by linz12306: **Important behavioral fix** — stops auto-re-injecting sustained-goal continuation after a normal model response, preserving it only at the actual tool-call budget boundary. Directly mitigates the **endless loop** seen in #4864.
- **[PR #5406 (merged) — feat(cli): add native TypeScript terminal UI](https://github.com/HKUDS/nanobot/pull/5406)** by Re-bin: Re-lands the native TUI (replacing #4329's mistaken merge) with contiguous commit history plus cross-terminal fixes. **New feature:** modern terminal UI for `nanobot agent`.

**Key advancement:** The merged Telegram PRs **close issue #5171**, resolving a critical reliability gap where the bot could permanently stop responding after network blips.

## 4. Community Hot Topics

- **[Issue #4864: Endless loop for `<tool_call> <function=complete_goal>`](https://github.com/HKUDS/nanobot/issues/4864)** — 7 comments, 1 👍, open for **over 5 weeks**. This is the highest-engagement item in the digest. The bug causes the `complete_goal` tool to error repeatedly when the gateway serializes the recap parameter as a bare string instead of JSON. While PR #5410 (merged today) narrows the loop trigger, the root parsing/serialization mismatch remains unfixed — **the community is likely waiting for a follow-up on the gateway serialization contract**.

- **[PR #5364: feat(webui): add temporary side conversations](https://github.com/HKUDS/nanobot/pull/5364)** — Tied with #4864 as the most symbolically significant. Users want **parallel, ephemeral conversations** alongside the main topic (`/side` command, tab switching, parallel sending). This suggests multi-tasking needs in a single session.

- **New feature race on WebUI:** Three concurrent PRs (#5408 follow-up suggestions, #5358 session mentions, #5364 side conversations) show strong community investment in WebUI interactivity. These are **not conflicting** but complementary; likely all land in the next release window.

**Underlying need:** The #4864 persistence + the goal-continuation fix (PR #5410) reveal that **goal-directed agent loops are a fragile experience** — users are burning tokens on repeated clarification replies. The community wants deterministic, non-repeating tool-call behavior.

## 5. Bugs & Stability

Bugs reported/active today, by severity:

| Severity | Issue | Status | Fix PR |
|---|---|---|---|
| **High** | [#5171 Telegram polling stalls silently (closed)](https://github.com/HKUDS/nanobot/issues/5171) — permanent loss of message reception after transient network failure; process alive, logs silent. | **Closed** | [#5156 merged](https://github.com/HKUDS/nanobot/pull/5156) — watchdog rebuilds polling pools |
| **High** | [#4864 complete_goal endless loop (still open)](https://github.com/HKUDS/nanobot/issues/4864) — recap parsed as bare string, not JSON; tool errors perpetually. | Open | Partial: [#5410 merged](https://github.com/HKUDS/nanobot/pull/5410) stops repeat replies, but **gateway param serialization fix not yet visible** |
| **Medium** | **[PR #5413 — fix(providers): apply fallback policy to raised errors](https://github.com/HKUDS/nanobot/pull/5413)** (open) — provider exceptions escape the fallback loop entirely; only `LLMResponse(finish_reason="error")` was handled. | PR open | This PR |
| **Medium** | **[PR #5407 — fix(cron): retired persisted heartbeat/dream jobs keep firing](https://github.com/HKUDS/nanobot/pull/5407)** (open, bug) — `heartbeat.enabled=false` doesn't stop already-persisted jobs in `cron/jobs.json`; continues burning tokens. | PR open | This PR |
| **Low/Medium** | **[PR #5341 — fix(skills): make weather workflow Windows-safe](https://github.com/HKUDS/nanobot/pull/5341)** (open, p2, conflict) — bare `curl` resolves to `Invoke-WebRequest` alias on Windows PowerShell, breaking first weather command. | PR open | This PR |
| **Low** | **[PR #5414 — fix(slack): validate file downloads across redirects](https://github.com/HKUDS/nanobot/pull/5414)** (open) — Slack private download URLs are remote input; crafted URLs could redirect toward unintended targets. | Security-hardening | This PR |

**Stability theme:** Today's merges directly resolve the Telegram outage bug and one source of the goal-loop. The remaining **cron-job token leak** (#5407) and **provider exception escape** (#5413) are both actively being patched; likely merge within 48h.

## 6. Feature Requests & Roadmap Signals

Three concurrent WebUI feature PRs are the strongest roadmap signal:

- **[PR #5408 — follow-up suggestions](https://github.com/HKUDS/nanobot/pull/5408)**: Ephemeral, chat-scoped follow-ups after turns; provider-neutral. Matches the documented "DeerFlow interaction" pattern.
- **[PR #5358 — session messaging via mentions](https://github.com/HKUDS/nanobot/pull/5358)**: Persistent `@name` for WebUI sessions; `list_sessions`/`send_session_message` APIs. This hints at **agent-to-agent communication** within the same workspace — a significant architectural direction.
- **[PR #5364 — temporary side conversations](https://github.com/HKUDS/nanobot/pull/5364)**: Parallel ephemeral conversations with tab switching; careful isolation of drafts/streaming.

Also open: **[Issue #5409 — Hybrid Spend Firewall](https://github.com/HKUDS/nanobot/issues/5409)** (opened by `sophieamoure2026-ui`): A request for budget-control and loop-detection mechanisms to prevent "power users running infinite loops and bankrupting LLM budget." While not yet a PR, this aligns with the commercial transition of the project and is a **high-probability roadmap item** given today's goal-loop fixes.

**Prediction:** The next minor release will likely include **all three WebUI features** (they are independent) plus the **TypeScript TUI** (#5406). The spend firewall is the most likely next major feature.

## 7. User Feedback Summary

- **Pain: repeated goal replies = wasted tokens.** PR #5410's fix description explicitly notes that "AgentRunner treated every plain-text final response as a reason to re-inject sustained-goal continuation," causing repeated clarification spam. This likely caused several support threads and frustrates users of long-running agents.
- **Pain: silent Telegram outages.** Issue #5171's description ("permanently stop receiving messages while process keeps running") is the classic "zombie service" failure — particularly dangerous for a chat agent that users rely on. Closure with a watchdog is a positive outcome.
- **Pain: Windows is a second-class citizen.** PR #5341 (weather skill breaking on PowerShell's `curl` alias) plus #5415 (Windows venv child-process adoption) and #5416 (macOS process identity), show the maintainers actively closing platform gaps.
- **Safety-concerned users:** PR #5414 (Slack redirect validation) indicates users expect **defense-in-depth** on remote download URLs — a sign that the user base now includes security-conscious adopters.
- **Satisfaction indicator:** The request volume for WebUI features (3 concurrent PRs) shows high engagement; but the **4-week-old #4864 with 7 comments** is the most likely candidate for "users waiting for maintainers to respond" sentiment.

## 8. Backlog Watch

- **[Issue #4864 (open, 5.5 weeks) — complete_goal endless loop](https://github.com/HKUDS/nanobot/issues/4864)**: Commenced 2026-07-09, last updated 2026-08-17. While the merge of #5410 mitigates repeat-reply behavior, **no PR addresses the root gateway param serialization bug**. Maintainers should either identify the fix or explicitly scope it into a release milestone; this is the oldest open high-severity bug.
- **[PR #5341 (open, 7 days, p2, "conflict" label) — Windows-safe weather skill](https://github.com/HKUDS/nanobot/pull/5341)**: Updated today, still open. The "conflict" label (plus #5415's Windows work) suggests the maintainer is prioritizing platform fixes carefully; but **7 days for a simple, well-understood `curl` alias fix is slower than the rest of the board** and may block other Windows users.
- **[PR #5407 (open, 1 day) — cron heartbeat/dream jobs token leak](https://github.com/HKUDS/nanobot/pull/5407)**: Labelled p2 with bug+regression+priority tags. Because this is a **token-cost leak** (jobs fire when disabled, "burning tokens"), it may deserve higher than p2 priority in the cost-conscious climate of the project.
- **No Python/backlog PRs** need maintainer attention today; all closed items merged within a day of posting — the project is healthy on triage cadence.

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent Project Digest — 2026-08-18

## 1. Today's Overview

Hermes Agent is in a high-velocity release cycle, with **50 issues** and **50 PRs** updated in the last 24 hours — a strong indicator of active maintenance and community engagement. The project shipped a patch release (**v0.20.3**) on August 16, consolidating ~125 PRs, but the current focus is clearly on **stabilization of the Desktop client** and **hardening the update/install pipeline**. A notable cluster of issues around the **Desktop BOTS sidebar**, **session state corruption**, and **Windows-specific update failures** suggests the team is actively addressing regressions introduced in recent feature work. The presence of **multiple `sweeper:risk-*` labels** indicates automated triage is working, but the volume of P1 bugs (setup failures, cron silent deaths, mixed-version gateways) signals that **update reliability** remains a top concern. Overall, this is a project that is shipping fast, but is currently in a **"fix the regressions" phase** following a large release.

---

## 2. Releases

**New Release: v0.20.3 (v2026.8.16.2)**

- **Date:** August 16, 2026
- **Type:** Patch release
- **Scope:** Rolls up ~125 PRs merged since v0.20.2 into a stable tagged release for downstream consumers (Docker images, hosted deployments, fresh installs).

**Key implications:**
- This is a **stabilization release**, not a feature release. The large PR count rolled up suggests a significant delta, but the patch designation implies no intentional breaking changes.
- **No migration notes** were included in the release body snippet, suggesting the data store and config formats remained stable.
- **Downstream consumers** (Docker, hosted) are the primary audience; the rollup is critical for production parity.

**Risk:** The sheer volume of changes (~125 PRs) in a single patch release increases the risk of subtle regressions, which is consistent with the elevated bug volume observed in today's data (e.g., #88654 mixed-version gateway, #86093 Windows update failures).

---

## 3. Project Progress

Today saw **9 closed/merged PRs** and **41 still-open PRs**. The closed PRs focus heavily on **Desktop BOTS session consistency** and **message delivery reliability**:

- **Desktop BOTS Roster & Canonical Chat Fixes (Merged):**
  - `#88678` [merged]: Cross-machine bot DMs now work end-to-end (canonical chat, sender attribution, reply relay). *Tags: `type/feature`, `sweeper:risk-session-state`.*
  - `#88292` [merged]: Aligns BOTS roster preview with the session its click opens — fixes a confusing mismatch where the preview showed one session but clicking opened another.
  - `#88148` [merged]: Fixes a bug where a failed intro or missing pin could replace the Bot Chat; now preserves the canonical pin.
  - `#88699` [merged]: Fixes "mid-switch 404" being treated as session deletion, which caused users to land on a blank `#/` route (#88540).
  - `#88690` [merged]: Salvages the above two fixes (#88148 + #88292) into a unified fix making the Bots pane always open the pinned canonical chat.

- **Platform Updates & Cleanup:**
  - `#88702` [merged]: Preserves Telegram DM outbound correlation metadata even without a thread ID.
  - `#88675` [merged]: Makes maintenance cleanup and notices update-safe (Kanban workspace cleanup, worktree preservation, terminal leak fixes).

- **New Open Feature/Enhancement PRs:**
  - `#88705` [open]: **MiniMax music generation plugin** — promotes a battle-tested user plugin to in-tree as `plugins/music_gen/minimax`. Signal of growing "media studio" ambitions.
  - `#88704` [open]: **Project-trust sidecar** — machine-written `~/.hermes/project-trust.json` with per-skill sha256 fingerprints for sticky deny. Addresses the ongoing project-local skills EPIC (#48970).
  - `#88701` [open]: Sanitized activity read model — new `GET /api/sessions/{session_id}/activity` endpoint for external consumers.

---

## 4. Community Hot Topics

The most engaged issues reveal deep concerns about **data integrity, extensibility, and update safety**:

1.  **#66616 — Skills index is stale or degraded** (47 comments, open, bug). The automated freshness probe is failing, and the index is degrading. This is a **core infrastructure concern** for anyone using the Skills Hub. The prolonged thread (since July 18) suggests this may be a chronic, hard-to-diagnose issue. [Link](https://github.com/NousResearch/hermes-agent/issues/66616)
2.  **#23717 — RFC: Pluggable SessionDB Provider** (17 comments, 7👍). The community is deeply interested in **PostgreSQL/MySQL as a backend**, driven by pain around the "Hot-Update Death Spiral" with SQLite. This is a major architectural request that maintainers have likely not committed to yet (`needs-decision` label). [Link](https://github.com/NousResearch/hermes-agent/issues/23717)
3.  **#87093 — Debian installation broken** (12 comments, P1). A fresh install fails on Debian 13.6 due to `uv.lock` and `npm install` issues. A high-severity onboarding bug that will affect adoption. [Link](https://github.com/NousResearch/hermes-agent/issues/87093)
4.  **#86093 — Windows: update always fails** (8 comments, 2👍, P1). The live `hermes.exe` cannot be renamed, and the quarantine mechanism fails, polluting the registry. A **critical platform-specific reliability issue**. [Link](https://github.com/NousResearch/hermes-agent/issues/86093)

---

## 5. Bugs & Stability

Bug reports are currently dominated by **install/update failures** and **session-state corruption**. Ranked by severity:

- **P1 (Critical — Blocks Adoption/Correctness):**
  - **#87093** — Debian setup broken (`uv.lock`/`npm install` failure). *No fix PR yet.* [Link](https://github.com/NousResearch/hermes-agent/issues/87093)
  - **#86093** — Windows update always fails (executable lock). *No fix PR.* [Link](https://github.com/NousResearch/hermes-agent/issues/86093)
  - **#88655** — Scheduler-level cron errors bypass failure_nudge alerting — jobs die silently. *Linked to #88654.* [Link](https://github.com/NousResearch/hermes-agent/issues/88655)
  - **#88654** — Gateway auto-restart fails after update, leaving mixed-version gateway. **Fix PR #88703 exists (open).** [Link](https://github.com/NousResearch/hermes-agent/issues/88654)

- **P2 (Major — Impairs Workflows):**
  - **#88595** — Provider fallback never re-evaluates mid-turn; one 429 pins the run to fallback. *No fix PR.* [Link](https://github.com/NousResearch/hermes-agent/issues/88595)
  - **#79742** — SQLite session DB leaks per-thread WAL connections → EMFILE (file-descriptor exhaustion). *No fix PR; a deep-dive is needed.* [Link](https://github.com/NousResearch/hermes-agent/issues/79742)
  - **#72716** — `optimize-storage` stamps empty FTS on interrupted demote → permanent search loss. **Fix PR #88696 exists (open).** [Link](https://github.com/NousResearch/hermes-agent/issues/72716)
  - **#88607** — Dashboard WebSocket rejection codes are lost (5401 becomes 403), making auth failure UX broken. *No fix PR.* [Link](https://github.com/NousResearch/hermes-agent/issues/88607)
  - **#88695** — Codex OAuth context window raised to 900K, but compaction still triggers at 200K. *Behavior bug.* [Link](https://github.com/NousResearch/hermes-agent/issues/88695)

- **P3 (Minor — Friction/UX):**
  - **#86601 / #87823** — Desktop auto-TTS speech duplication (2 comments each). *These are duplicates; #87823 is marked as such.* [Link1](https://github.com/NousResearch/hermes-agent/issues/86601) [Link2](https://github.com/NousResearch/hermes-agent/issues/87823)
  - **#53666** — `clarify` tool prompts invisible in Desktop chat UI (user sees no question). *Open for >1 month.* [Link](https://github.com/NousResearch/hermes-agent/issues/53666)

---

## 6. Feature Requests & Roadmap Signals

High-activity feature requests point to clear roadmap signals:

- **Pluggable SessionDB (#23717):** The most upvoted open feature (7👍). The community is vocally demanding an escape from the single-file SQLite model. Given the architectural weight, this won't land quickly, but the `needs-decision` label suggests active maintainer review. Expect *discussion* to be forwarded but no code soon. **Roadmap Signal: High**.
- **Project-local `.hermes/` EPIC (#48970):** This is progressing in pieces. Today, we saw **two PRs** advancing this initiative: `#88700` (canonicalize project trust identity across git worktrees) and `#88704` (project-trust sidecar with fingerprints). This is likely to ship in a future minor version (v0.20.x).
- **MiniMax Music Generation (#88705 PR):** This is a new in-tree plugin for music generation. It signals a push into richer media generation capabilities beyond text. **Roadmap Signal: Medium** (likely in v0.21).
- **Custom Provider Reasoning Effort (#66543):** The community wants per-model reasoning-effort mapping for custom endpoints. `needs-decision` label, but low complexity. **Roadmap Signal: Medium**.

---

## 7. User Feedback Summary

The friction points are concrete and painful:

- **Installation & Update Pain:** Users are **failing fresh installs** (Debian #87093) and **cannot update on Windows** (#86093). There's also a report that the install script **masks failures** and reports success after a hard failure (#61828). This undermines trust in the core lifecycle.
- **Session & Data Integrity:** The pain around session state is severe. Users face **permanent search loss** (#72716), **file-descriptor exhaustion** causing crashes (#79742), and **wrong session content opening** (#88200). The underlying need is simple: "Don't lose my data, and show me the right chat." The high velocity of fixes around the BOTS sidebar (#88292, #88148) suggests the team is actively listening and fixing these fast.
- **Configuration Conflicts:** Users are frustrated by **Desktop/Gateway double-writes** corrupting config (#37751) and **silent config rewrites** (#4775). This indicates a need for a more robust and intentional configuration-management strategy.
- **Silent Failure Modes:** The recurring theme of **silent failures** is the loudest negative signal: cron jobs dying silently (#88655), update failures leaving mixed-version gateways (#88654), and TTS double-speaks (#87823). Users are not getting clear feedback when things go wrong.

Overall sentiment is a mix of **excitement about the feature set** but **frustration with the reliability of the update path and the silent behavior of the system**.

---

## 8. Backlog Watch

- **#23717 (RFC: Pluggable SessionDB)** — High community demand (7👍, 17 comments), stale since May. Maintainer decision is needed. [Link](https://github.com/NousResearch/hermes-agent/issues/23717)
- **#79742 (SQLite FD Leak → EMFILE)** — Long-standing (since Aug 5), complex concurrency bug, in-code comment assumption is identified as wrong. Needs a maintainer's deep-dive to scope a fix. [Link](https://github.com/NousResearch/hermes-agent/issues/79742)
- **#53666 (Desktop `clarify` tool hidden)** — Open since June 27, active comments, but no fix PR. It's been over a month. [Link](https://github.com/NousResearch/hermes-agent/issues/53666)
- **#49354 (PR: repair sqlite wal state handling)** — Open since June 20, updated today. A critical P2 fix for WAL state that remains in review. [Link](https://github.com/NousResearch/hermes-agent/pull/49354)
- **#61828 (Install script masks failures)** — Open since July 10, directly contributes to the bad install experience. It would benefit from maintainer attention to prevent onboarding roadblocks. [Link](https://github.com/NousResearch/hermes-agent/issues/61828)

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw Project Digest — 2026-08-18

## Today's Overview

PicoClaw is in a moderately active maintenance phase with 4 issues and 4 PRs updated in the last 24 hours. The project shows healthy community engagement: a bug report (#3338) was quickly addressed by a same-day fix PR (#3340), while an older critical failure loop issue (#3311) saw its fix merged. Notable activity includes the closure of a long-stale Weixin channel enhancement PR (#2606) and a config-priority fix for Fly deployments (#271). No new releases were published today, suggesting development is accumulating toward a future release.

## Releases

No new releases on 2026-08-18.

## Project Progress

Three PRs were merged or closed today:

- **[PR #3312 — fix(agent): stop turn early on repeated identical tool failure](https://github.com/sipeed/picoclaw/pull/3312)** (closed/merged): Fixes a critical UX issue where a turn would silently spin to `max_tool_iterations` when a tool fails repeatedly with the same error (e.g., git without credentials). The agent now stops early instead of wasting cycles and leaving the user without an answer.
- **[PR #271 — fix: env overrides when config.json is missing and add regression test](https://github.com/sipeed/picoclaw/pull/271)** (closed/merged): Resolves a gap where env vars (commonly used in Fly deployments) were not applied when config.json was absent, causing the app to fall back to default model `glm-4.7` and fail on missing credentials. Now `env.Parse(cfg)` always runs.
- **[PR #2606 — feat: enhance Weixin channel support and configuration](https://github.com/sipeed/picoclaw/pull/2606)** (closed, stale): Long-awaiting merge (opened April 21) — adds multi-instance Weixin channel support, dynamic instance handling, illegal-name validation, and improved error handling across backend, frontend, and docs.

## Community Hot Topics

- **[Issue #3287 — Better support long messages in IRC](https://github.com/sipeed/picoclaw/issues/3287)** (6 comments, open): The most-discussed issue. Users want PicoClaw to coalesce IRCv3 messages split at 512 bytes into a single cohesive message. This touches core message-parsing logic and affects IRC channel usability for anyone using PicoClaw over IRC with verbose output.
- **[Issue #3311 — Repeated identical tool failure loops silently to max_tool_iterations](https://github.com/sipeed/picoclaw/issues/3311)** (2 comments, resolved via PR #3312): A production-affecting bug over Telegram where git commands without credentials caused minutes-long silent spins. The fix merged today directly addresses this; users should verify in the next release.

## Bugs & Stability

Ranked by severity:

1. **[High — Issue #3338: Slack does not attach image media content](https://github.com/sipeed/picoclaw/issues/3338)** (open, new today): `SendMedia` omits `FileSize` in `slack.UploadFileParameters`, causing the slack-go SDK to reject all uploads with `file.upload.v2: file size cannot be 0`. **Fix exists:** [PR #3340](https://github.com/sipeed/picoclaw/pull/3340) sets the field; awaiting merge.
2. **[Medium — Issue #3339: Antigravity generation returns generic 429 despite valid OAuth scopes](https://github.com/sipeed/picoclaw/issues/3339)** (open, new today): Google Antigravity auth and model discovery succeed, but every generation returns `RESOURCE_EXHAUSTED`. The response lacks quota details, making diagnosis difficult. No known fix PR yet.
3. **[Medium — Issue #3311: Silent tool failure loop](https://github.com/sipeed/picoclaw/issues/3311)** (closed): Fixed in PR #3312 — no longer silently loops to max iterations; agent stops early on repeated identical tool failures.

## Feature Requests & Roadmap Signals

- **IRC long-message coalescing (#3287):** Active request with 6 comments; likely to be considered if IRC is a supported channel in the next milestone. Needs protocol-aware message buffering.
- **Weixin channel enhancements (#2606):** Merged — a long-pending feature suggesting community interest in WeChat routing. Expect it in the next release.

**Prediction for next version:** The Slack fix (PR #3340) is a near-certain inclusion, alongside the agent loop fix (#3312) and config env fix (#271). IRC long-message support may surface as an experimental improvement if maintainers pick it up.

## User Feedback Summary

- **Pain point — silent failures:** Users are dissatisfied when the agent spins without producing an answer (production Telegram issue, #3311). The fix restores confidence but needs regression tests to prevent recurrence.
- **Pain point — channel media support:** Slack uploads fundamentally broken (#3338) — a core integration failure; fix PR is ready but needs review. ️
- **Pain point — deployment configurability:** Fly.io-style env-only deployments were failing (#271) because env overrides were ignored without config.json; fixed and now regression-tested.
- **Satisfaction signal:** Positive community engagement — users report bugs with detailed stack traces and promptly submit PRs (e.g., octavioturra for Slack, lucapette for agent loop).

## Backlog Watch

- **[PR #2606 (Weixin)](https://github.com/sipeed/picoclaw/pull/2606) — closed today after ~4 months:** Raises flag that large, well-tested features can take months to merge; maintainers may want to revisit PR review velocity.
- **[Issue #3287 (IRC long messages)](https://github.com/sipeed/picoclaw/issues/3287):** Inboxed since 2026-07-22 with committers engaged, but no maintainer response visible yet — worth a triage comment.
- **No new unaddressed issues** from today’s batch, but #3339 (Antigravity 429) has zero comments and needs maintainer investigation for quota-handling clarity.

*Overall: Healthy project with responsive maintainers, clear community-driven bug fixes, and a steady drip of feature work. Watch for Slack fix merge (PR #3340) and Antigravity 429 diagnosis in the next 48h.*

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw Project Digest — 2026-08-18

## 1. Today's Overview

NanoClaw is in a period of intense development velocity, with **34 pull requests updated in the last 24 hours** — a very high activity level — alongside 4 issues and zero new releases. The vast majority of PR activity (21 of 34) is merge or close events, indicating a significant merge wave is underway. Most merged work comes from core-team members (gavrielc, glifocat) and focuses on architectural seams, hooks, and extension points for the platform. The project is also experiencing a burst of community-contributed fixes (wakqasahmed, torbenstruever, chiptoe-svg) addressing practical operational issues, suggesting a healthy balance between platform maturation and user-driven hardening.

## 2. Releases

No new releases were published in the last 24 hours. The most recent release remains **v2.1.48** (referenced in Issue #3301 as introducing the "one-door task delivery" behavior).

---

## 3. Project Progress

A substantial merge wave occurred today, dominated by **gavrielc's** architectural contributions, which were all merged:

- **[PR #3292](https://github.com/nanocoai/nanoclaw/pull/3292) — Channels: bridge inbound-policy registration seam.** Adds a single-point interception point on the Chat SDK bridge for inbound dispatch, allowing modules to wrap `ChannelSetup` without editing bridge source.
- **[PR #3293](https://github.com/nanocoai/nanoclaw/pull/3293) — Router: session-created hook.** Notifies registered modules when an engaged message creates a brand-new session, enabling platform-specific conversation bootstrap (thread naming, etc.).
- **[PR #3294](https://github.com/nanocoai/nanoclaw/pull/3294) — Delivery: post-delivery hook.** Adds a first-delivery flag hook to the outbound drain loop for one-time follow-through (e.g., onboarding affordances).
- **[PR #3295](https://github.com/nanocoai/nanoclaw/pull/3295) — Channels: generic membership-event hook.** Forwards `onMemberJoinedChannel` events to a per-channel-type handler, enabling adopt-on-invite behavior without bridge source edits.
- **[PR #3296](https://github.com/nanocoai/nanoclaw/pull/3296) — Agent-runner: `extendTool`.** Allows modules to additively extend MCP tool schemas, descriptions, and passthrough keys without touching base tool source.
- **[PR #3297](https://github.com/nanocoai/nanoclaw/pull/3297) — Setup: per-channel pre-step and companion-skill declarations.** Two generic extension points for the wizard: pre-step input binding and companion-skill declaration.
- **[PR #3285](https://github.com/nanocoai/nanoclaw/pull/3285)** (merged, superseding #3254–#3257) — **Cross-session context** for multi-session agent groups, including fan-out, DM backfill, echo pruning, and `ncl sessions history`.

**Key theme:** The platform is consolidating its extension architecture — hooks and seams are being baked into core subsystems (router, delivery, bridge, setup, tool registry) so that channels and skills can be built without forking the bridge source.

---

## 4. Community Hot Topics

The most active discussion items today:

- **[Issue #1143](https://github.com/nanocoai/nanoclaw/issues/1143) — Skills docs reference `/data/env` path that no longer exists** (2 comments). A documentation bug flagged by the triage bot, opened in March but only closed today. Users following skill instructions hit a dead path for environment variable configuration. **Underlying need:** Documentation must track the current env-var mechanism; this is a trust issue — stale docs erode user confidence.

- **[Issue #3203](https://github.com/nanocoai/nanoclaw/issues/3203) — Codex provider emits undeclared `file` `ProviderEvent`.** `/add-codex` fails typecheck on `main`; generated images are silently dropped. **Underlying need:** The Codex provider integration is incomplete (event type undeclared, no consumer for the emitted event). This is both a type-safety violation and a silent data-loss bug.

- **[PR #3288](https://github.com/nanocoai/nanoclaw/pull/3288) — Add `/add-clawmetry` skill** (open). Community member `vivekchand` proposes a read-only local dashboard with a NanoClaw session adapter. The motivation: the FAQ's debugging answer ("ask Claude Code") is insufficient for reading sessions and scanning overnight activity. **Underlying need:** Operational observability — users want queryable session history, not just conversational debugging.

- The **cross-session context work** (PR #3285 and its predecessors) is the single largest architectural topic, folding four PRs into one. Multiple comment threads across the superseded PRs indicate active review discussion about fan-out semantics and session-echo behavior.

---

## 5. Bugs & Stability

Ranked by severity:

**High — [Issue #3301](https://github.com/nanocoai/nanoclaw/issues/3301) — Tasks firing in chat sessions run one-door: logs dropped, replies eaten, series unlisted.** Regression introduced in v2.1.48 (#2988). When a `kind='task'` row fires inside a chat session, the entire query switches to task mode, causing dropped logs and eaten replies. **Note:** This is currently the single most impactful open bug — it affects existing installs with pre-2.1.48 task rows. **Fix PR exists:** [#3303](https://github.com/nanocoai/nanoclaw/pull/3303) (fix: keep run logs for task rows firing in chat sessions) — open, not yet merged.

**High — [Issue #3289](https://github.com/nanocoai/nanoclaw/issues/3289) — Bound pending-message polling for accumulated backlogs.** `getPendingMessages()` loads every due pending row into JS memory before applying batch limits — an O(n) memory hazard as backlogs accumulate. **Fix PR exists:** [#3291](https://github.com/nanocoai/nanoclaw/pull/3291) — open, not yet merged.

**Medium — [Issue #3203](https://github.com/nanocoai/nanoclaw/issues/3203) — Codex provider typecheck failure and silent image drops.** `/add-codex` fails on `main`; images silently dropped. Related fix PR [#3299](https://github.com/nanocoai/nanoclaw/pull/3299) also bumps the `@openai/codex` pin ahead of **GPT-5.4 retirement from Codex on 2026-08-31** — a time-boxed risk (13 days).

**Low — [PR #3300](https://github.com/nanocoai/nanoclaw/pull/3300) — Attachment type not escaped in agent-facing XML.** `formatAttachments` escapes every field except `type` — a subtle injection/parsing hazard.

**Low — [PR #3286](https://github.com/nanocoai/nanoclaw/pull/3286) — Skip image rebuild when no packages configured.** `ncl groups restart --rebuild` unconditionally rebuilds even when `packages_apt`/`packages_npm` are empty — wasted cycles.

---

## 6. Feature Requests & Roadmap Signals

**Strong signals for next release:**

- **Web chat channels (two competing implementations):** [PR #3298](https://github.com/nanocoai/nanoclaw/pull/3298) by `amit-shafnir` (loopback-only Local Web adapter with browser UI) and [PR #3290](https://github.com/nanocoai/nanoclaw/pull/3290) by `viiluxx` (self-contained page on native HTTP bridge, no dependencies). Two community members independently built web chat in the same 24-hour window — this is a clear demand signal. Expect maintainers to pick one or reconcile both.

- **ClawMetry dashboard skill ([PR #3288](https://github.com/nanocoai/nanoclaw/pull/3288)):** Read-only local dashboard with session adapter. Aligns with the observation that users want structural visibility, not just conversational debugging.

- **Bounded stdin JSON ([PR #3218](https://github.com/nanocoai/nanoclaw/pull/3218)):** Generic `--stdin-json` input mode for both host and container clients. A clean, backwards-compatible extension to the CLI.

- **OneCLI gateway bind address fix ([PR #3302](https://github.com/nanocoai/nanoclaw/pull/3302)):** Fixes install-time misconfiguration where the gateway's own `docker-compose` never receives the discovered `api-host`.

**The through-line:** channel extensibility, observability, and operational correctness — the platform is past "spike" phase and into "operational hardening" phase.

---

## 7. User Feedback Summary

- **Frustration with task/chat interaction** (Issue #3301): Users with pre-2.1.48 installs are effectively trapped — their task rows stay in chat sessions and now break log delivery, reply visibility, and series listing. This is a migration/backward-compatibility concern.

- **Documentation drift** (Issue #1143): Users following skill docs hit removed paths (`/data/env`), breaking skill setup flows. Closed today, but the underlying process issue (docs not kept in sync with path changes) remains.

- **Silent data loss** (Issue #3203): Codex-generated images being dropped without any consumer signal is the kind of bug that erodes trust — the typecheck failure is a red flag, but the silence is the real problem.

- **Community is building on the platform:** The volume of community-contributed fixes (wakqasahmed contributing three separate fixes in one day; torbenstruever's XML escaping fix; chiptoe-svg's dependency-pin urgency) indicates a healthy, engaged contributor base that understands the codebase well.

- **Latent demand for web UI:** Two independent web-chat implementations in one day is the strongest possible signal that users want a browser-based interface. The project's current "every conversational surface except the one-shot CLI routes through an external service" (per PR #3290) is evidently a felt gap.

---

## 8. Backlog Watch

Items needing maintainer attention:

- **[PR #3249](https://github.com/nanocoai/nanoclaw/pull/3249) — fix(setup): handle an existing Node that is too old** (open since 2026-08-14, 4 days). A core-team fix from `glifocat`, still unmerged. Setup wizard Node-version handling is a first-run experience issue — long wait on a "getting started" fix.

- **[PR #3218](https://github.com/nanocoai/nanoclaw/pull/3218) — feat(cli): accept bounded JSON from stdin** (open since 2026-08-09, 9 days). A well-scoped feature with minimal invasiveness; still awaiting review.

- **[Issue #3203](https://github.com/nanocoai/nanoclaw/issues/3203) — Codex provider typecheck failure** (open since 2026-08-08, 10 days). The associated fix PRs (#3299, and any type-declaration fix) need attention — the GPT-5.4 retirement deadline (2026-08-31) adds time pressure.

- **PRs #3287, #3286, #3300, #3302** — all community-contributed fixes from today's batch. Several are small, well-scoped, and address real operational bugs; they should not languish. The project would benefit from explicitly acknowledging contribution velocity to keep the momentum.

- **[Issue #1143](https://github.com/nanocoai/nanoclaw/issues/1143)** was closed today after 5 months open — the long gap between report (March) and closure (August) suggests documentation issues receive lower triage priority, which contradicts their outsized impact on user experience.

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

Here is the NullClaw project digest for **2026-08-18**, based on the provided repository activity data.

---

# NullClaw Project Digest — 2026-08-18

## 1. Today's Overview
NullClaw's repository activity remains extremely low, indicating a period of maintainer hibernation or a stable, uncommitted codebase. Over the past 24 hours, there were **zero issues updated** (no new bugs, no new feature requests) and **zero new releases** published. The only activity recorded was a single **open dependency pull request** (PR #956) aiming to bump the base Alpine image from 3.23 to 3.24. While the project does not appear to be in active feature development at this moment, the upkeep of patch-level dependencies (if merged) suggests the project is technically alive, though it may require maintainer intervention to keep the momentum going.

## 2. Releases
**No new releases were published in the last 24 hours.** There are no changelogs, breaking changes, or migration notes to report for this digest period.

## 3. Project Progress
**None.** No pull requests were merged or closed in the last 24 hours. There is no new feature development, refactoring, or bug-fix activity to report as "complete."

- **Open (Awaiting Merge):** [#956 - ci(deps): bump alpine from 3.23 to 3.24](https://github.com/nullclaw/nullclaw/pull/956) — A minor infrastructure hygiene update for Docker images.

## 4. Community Hot Topics
Despite the low volume, the single PR currently open represents the **most active item**:

- **[#956 [dependencies, docker] ci(deps): bump alpine from 3.23 to 3.24](https://github.com/nullclaw/nullclaw/pull/956)** — *Author: dependabot[bot] | Updated: 2026-08-17 | Comments: 0 | 👍: 0*

**Underlying Analysis:** While this is an automated bot-driven update, its prolonged open status (created over two months ago on 2026-06-15) is notable. The "need" here is not user-driven but signals a **maintainer bottleneck**. The community relies on maintainers to approve dependency security patching (Alpine bumps typically include security fixes). The lack of engagement on this PR could indicate a risk of outdated security infrastructure in the Docker images.

## 5. Bugs & Stability
**No new bugs, crashes, or regressions were reported in the last 24 hours.** The issue tracker remains at zero active items.

- **Severity Ranking:** N/A (No active reports).

## 6. Feature Requests & Roadmap Signals
**No user-submitted feature requests were logged today.** The roadmap is silent. 

**Prediction:** Given the current stagnation, it is unlikely that any new features are in the immediate pipeline. The next "version" milestone will likely simply consist of the dependency upgrade currently sitting in PR #956 (Alpine 3.24) once merged, rather than user-facing functional changes.

## 7. User Feedback Summary
There is **no direct user feedback** (comments, 👍s, or issues) to analyze in the last 24 hours. The absence of complaints could suggest user satisfaction, but it is more likely an indication of low user engagement or a dormant community. The only implicit "user" feedback comes from the bot: the system believes a Docker base image is out of date and is requesting a refresh, which remains unaddressed.

## 8. Backlog Watch
**High Priority:** **[#956 - Bump Alpine (Open for 64 days)](https://github.com/nullclaw/nullclaw/pull/956)**

This PR requires immediate maintainer attention. It has been open for over two months without a merge or close. This is a critical signal for project health:

- **Risk:** Keeping the base image on Alpine 3.23 exposes the Docker images to potential security vulnerabilities that have been patched in 3.24.
- **Action:** The maintainers should either approve and merge this change or explicitly close it with a reason to prevent future bot spam. The lack of activity here suggests that the project either lacks a designated maintainer or the CI process is not adequately staffed.

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw Project Digest — 2026-08-18

## 1. Today's Overview

IronClaw is in a period of intense engineering activity focused on two dominant themes: **durable database write-pressure reduction** (epic #7591) and **durable notification/UI infrastructure**. The project saw 28 issues and 44 PRs updated in the last 24 hours, with 6 issues closed and 16 PRs merged/closed — indicating healthy throughput. A dedicated QA/dogfooding epic (#7685) opened for the week, and a daily failure-taxonomy report (#7704) was published, suggesting the team is running regular benchmark suites against the codebase. Notably, the write-pressure epic has spawned multiple Tier 2/Tier 3 sub-issues and at least one critical bug discovery (#7714) with an immediate fix PR (#7717), demonstrating a responsive bug-to-fix pipeline. The notification inbox workstream (#7687–#7691) represents a substantial product-surface investment, with four related issues opened on the same day. No releases were cut in this window.

**Activity assessment: Very high.** Dozens of opened issues and PRs, multiple interdependent workstreams, and significant architectural discussions around write amplification.

---

## 2. Releases

No new releases were published in the last 24 hours. The most recent release work appears to be the forward-port PR #7663 (closed), which carried 1.2-fixes onto `main` — including Windows filesystem/release-smoke reliability, clean Windows JSON output, and runtime curl for healthchecks — but that is a code-merge, not a tagged release.

---

## 3. Project Progress

**16 PRs were merged or closed** in the last 24 hours. Notable items:

### Merged/Closed and Folded

- **#7710 (closed)** — `fix(slack): address multi-agent review findings on #7682` — A multi-agent code review produced 7+ findings on the Slack unlinked-user connect flow (private nudge + one-click connect link); this PR addressed them on the source branch so author @sergeiest can fold them into #7682.
- **#7663 (closed)** — `fix(release): forward-port 1.2 fixes and thread repair` — Brought independently validated 1.2 fixes onto `main`, plus a thread-index projection repair.
- **#7703 (closed)** — `feat(wasm): typed WIT tool response and bundled guest migration` — Superseded by #7711 to avoid add-then-remove churn of a compatibility shim.
- **#7637 / #7647 (closed issues)** — Additional design-system typing and automation no-delivery outcome work.

### Issues Closed

- **#7637** — Type the design-system component boundary (frontend strictness improvement).
- **#7647** — Deterministic no-delivery outcome for scheduled runs (automation reliability).
- **#7275** — Reborn persistence verification across conversations (user-reported issue closed).
- **#7594, #7598, #7605** — Three Tier 1–3 write-pressure sub-issues closed, indicating the epic is making steady progress.

### Key Open PRs (in review)

- **#7717** — Fix for libSQL write-lane starvation (#7714), resource-governor cascade.
- **#7712** — Opt-in `BeforeModel` checkpoint batching, side-effect-safe via checkpoint-kind gating.
- **#7709** — Bounded lease fence reads (memoized, capped at 30s).
- **#7711** — WASM typed tool responses + guest migration (supersedes #7703).
- **#7708** — Run-now capability across trigger domain and WebUI.
- **#7694 / #7693** — Durable backend suggestions and native structured output finalization.

---

## 4. Community Hot Topics

The most actively discussed items (by comments/reactions) in this window:

1. **#7275 — Verification of persistent memory across conversations** (CLOSED, 4 comments)
   - [nearai/ironclaw Issue #7275](https://github.com/nearai/ironclaw/issues/7275)
   - A user-facing reliability concern: info established in one conversation not reliably recalled later. Closed, but the underlying issue (#7185) triggered a verification pass.

2. **#7591 — Epic: reduce durable DB write pressure ~60%** (3 comments)
   - [nearai/ironclaw Issue #7591](https://github.com/nearai/ironclaw/issues/7591)
   - The largest architectural effort this week. 7+ sub-issues have been scoped across Tier 1–3, with substantial analysis (per-row savings for each).

3. **#7701 — Collapse resource-governor reserve+reconcile into one post-call spend write** (2 comments)
   - [nearai/ironclaw Issue #7701](https://github.com/nearai/ironclaw/issues/7701)
   - Gap found after epic creation; est. −11 rows/turn.

4. **#7603 / #7604 — Tier 3 batching and paired-row collapse** (2 comments each)
   - [nearai/ironclaw Issue #7603](https://github.com/nearai/ironclaw/issues/7603), [Issue #7604](https://github.com/nearai/ironclaw/issues/7604)
   - #7603's original approach was proven unsafe via integration test → spawned #7707 for a safer path.

**Underlying needs:** The community (largely core-team driven) is deeply concerned with **operational scalability** — the cost of durable storage per turn is now a first-class product problem. The team is investing heavily in reducing row-writes while preserving multi-worker lease safety, which suggests IronClaw is being tested at higher concurrency/load than before.

---

## 5. Bugs & Stability

Ranked by severity:

### High Severity

- **#7714 — libSQL single shared write connection starves resource-governor journal** (OPEN, bug)
  - [nearai/ironclaw Issue #7714](https://github.com/nearai/ironclaw/issues/7714)
  - During PinchBench (147 tasks), the resource governor's delta journal stalled ~40s, causing repeated cascade (authority invalidated → journal replacement → durable-state reload), permanently leaked reservations, and mislabeled `process in use` deaths.
  - **Fix PR exists: #7717** (open, XL size) — stops write-lane starvation from cascading through the resource governor.

### Medium Severity

- **#7716 — Add MCP server flow missing bearer key auth and transport options** (OPEN, qa-bug)
  - [nearai/ironclaw Issue #7716](https://github.com/nearai/ironclaw/issues/7716)
  - Cannot configure authenticated MCP servers or choose STDIO/HTTP transports from the UI.

- **#7705 — Shutdown hang and latching `pending_flush_error` in CoalescingEventSink** (OPEN)
  - [nearai/ironclaw Issue #7705](https://github.com/nearai/ironclaw/issues/7705)
  - Two non-blocking findings from PR #7631: shutdown can hang on a wedged event backend; flush errors latch permanently.

- **#7702 — Obligation audit records never attached in production** (OPEN, contract violation)
  - [nearai/ironclaw Issue #7702](https://github.com/nearai/ironclaw/issues/7702)
  - Opposite of a write-pressure problem: required `AuditBefore/AuditAfter` records are not being written at all, violating documented host-api contract.

### Low/UX Severity

- **#7715 — Telegram connection flow lacks bot-vs-personal consent** (OPEN, qa-bug)
  - [nearai/ironclaw Issue #7715](https://github.com/nearai/ironclaw/issues/7715)
  - Users can't choose between bot and personal account mode.
- **#7681 — Slack unlinked-user connect message is public** (OPEN, UX)
  - [nearai/ironclaw Issue #7681](https://github.com/nearai/ironclaw/issues/7681)
  - Fix PR #7682 in review.

### Stability Signals from Benchmarks

- **#7704 — Daily failure taxonomy (2026-08-17)** (OPEN)
  - [nearai/ironclaw Issue #7704](https://github.com/nearai/ironclaw/issues/7704)
  - Clawbench: 84 non-pass cases; largest fixable defect is a storage write-lane concurrency issue (matches #7714).

---

## 6. Feature Requests & Roadmap Signals

Signals that are likely to land in upcoming versions:

1. **Durable notification inbox (#7687–#7691)** — A full user-scoped notification system with typed kinds, severities, lifecycle states, dedup keys, and server-backed persistence. Replaces the current automation-approval-only center. Expected to land in phases across v1.3/v1.4.

2. **OOBE / onboarding automation-tasks prototype (#6994)** — Carousel, inline cards, agent-mode pill, gated behind `oobe_suggestions` flag. Design + integration plan committed to `docs/internal/design/oobe/`.

3. **Run-now for automations (#7708)** — Manual fire preserving schedule + domain-separated fire identity. Atlassian-style manual trigger for scheduled automations.

4. **Evidence-backed run outcomes (#7650)** — Replace answer-only semantic judging with deterministic, evidence-backed assessment using runtime data and `required_capability_ids`.

5. **Semantic Google Docs tools (#7718)** — Anchored batch edits, structured inspection, table population, deterministic verification (all legacy tools preserved).

6. **Structured output finalization (#7693)** — Provider-neutral immutable output contract, host-owned and tools-disabled after terminal candidate.

7. **Durable backend suggestions (#7694)** — Product-surface-neutral `suggestions.*` operations, asynchronous generation via canonical runner.

8. **GitHub Projects v2 field manipulation (#7719)** — Community requested (Main backlog priority field); currently missing from GitHub tooling.

9. **ACP CLI serve command (#7513)** — Agent Communication Protocol over stdio; enables external clients (Copilot CLI, VS Code).

---

## 7. User Feedback Summary

- **Persistent memory across conversations (#7275)** — A user reported that explicitly established information is not reliably recalled in later conversations. IronClaw already had persistent memory tools and cross-thread integration coverage, so this was a verification/QA issue. Resulted in closure after verification work; watch for regressions.

- **AGENTS.md edits not picked up (#3762, OPEN since 2026-05-18)** — Editing identity files in the web UI doesn't update the system prompt for current/future conversations. This is a long-standing (3-month-old) user-facing issue, still open. Suggested P1, tagged for v1.4.0.

- **MCP bearer auth + transport options (#7716)** — A QA tester found the Add-MCP-server flow too limited. Real-world signal: enterprise users need authenticated MCP endpoints.

- **Telegram bot vs. personal account (#7715)** — Connection flow doesn't explain which mode is used. Onboarding clarity issue.

- **Slack connect nudges are public (#7681)** — In shared channels, unlinked users get a public reply to connect, creating a privacy leak and manual round trip. Teams using Slack at scale will hit this daily.

- **Write/performance pain at scale (#7714, #7704)** — Operator-feedback via benchmarks: IronClaw is hitting storage bottlenecks during heavy automation runs. The team's rapid response (fix PR within 24h) is a positive signal.

---

## 8. Backlog Watch

Items needing maintainer attention (older / unanswered):

1. **#3762 — Editing AGENTS.md in web UI does not update system prompt** (OPEN since 2026-05-18, suggested_P1, v1.4.0)
   - [nearai/ironclaw Issue #3762](https://github.com/nearai/ironclaw/issues/3762)
   - 3 months old, 2 comments; core onboarding/identity flow.

2. **#7406 — Dependabot PR: actions group, 4 updates** (OPEN since 2026-08-09, 8 days old)
   - [nearai/ironclaw PR #7406](https://github.com/nearai/ironclaw/pull/7406)
   - Bumps `anthropics/claude-code-action`, `actions/setup-node`, `Swatinem/rust-cache`, `docker/login-action`.

3. **#7513 — ACP serve command (new contributor)** (OPEN since 2026-08-11, 7 days old)
   - [nearai/ironclaw PR #7513](https://github.com/nearai/ironclaw/pull/7513)
   - Large PR (XL) from a new contributor; no comments in the last 24h.

4. **#7184 — Nostr host functions for WASM tools** (OPEN since 2026-08-04, 14 days old)
   - [nearai/ironclaw PR #7184](https://github.com/nearai/ironclaw/pull/7184)
   - Third-party contribution (Nostr integration, Schnorr signing); no maintainer comments in the last 24h.

5. **#6994 — OOBE automation-tasks prototype** (OPEN since 2026-08-01, 17 days old)
   - [nearai/ironclaw PR #6994](https://github.com/nearai/ironclaw/pull/6994)
   - Large design+implementation PR; older than the active week's PRs but part of the deliberate OOBE workstream.

---

*Digest generated 2026-08-18 from GitHub data (nearai/ironclaw).*

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

# LobsterAI Project Digest — 2026-08-18

## 1. Today's Overview

LobsterAI shows a **high-velocity development day**, with 21 PRs touched in the last 24 hours (17 merged/closed, 4 open) and 7 issues updated. Notably, the majority of merged PRs (#1636–#1675) carry the `stale` label, appearing to be a **large backlog-clearance wave** — historical contributions from April being merged or closed simultaneously. This suggests maintainers executed a reconciliation pass over accumulated contributions. Only one genuinely new contribution is present (PRs #2502–#2506, a DeepSeek Harness / "dsh" engine integration). No new releases were cut today; activity is concentrated in the main branch. All 7 issues updated are **open** (0 closed), with most (~6/7) being stale/older issues receiving automated or maintenance touches rather than new complaints.

---

## 2. Releases

**None.** No new versions were published in the reporting window.

---

## 3. Project Progress

Several feature/merge clusters cleared today (labels mirror historical PRs from April):

| PR | Title | Notes |
|----|-------|-------|
| [#1636](https://github.com/netease-youdao/LobsterAI/pull/1636) | Cowork: floating "scroll to bottom" button | Chat UX — merged |
| [#1637](https://github.com/netease-youdao/LobsterAI/pull/1637) | Cowork: "Regenerate" button for AI replies | Chat UX — merged |
| [#1639](https://github.com/netease-youdao/LobsterAI/pull/1639) | i18n: fix hardcoded English tooltips | L10n fix across Windows titlebar, skills, schema — merged |
| [#1640](https://github.com/netease-youdao/LobsterAI/pull/1640) | Tool results: one-click copy button | Adds copy to bash/diff/standard tool outputs — merged |
| [#1641](https://github.com/netease-youdao/LobsterAI/pull/1641) | Modal: Esc-to-close everywhere | Unified modal behavior — merged |
| [#1642](https://github.com/netease-youdao/LobsterAI/pull/1642) | Windows: right-click context menu ("Open with LobsterAI") | Registry-based shell integration — added |
| [#1661](https://github.com/netease-youdao/LobsterAI/pull/1661) | Log redaction for sensitive data (API keys, tokens) | Security/privacy hardening — merged |
| [#1663](https://github.com/netease-youdao/LobsterAI/pull/1663) | OpenClaw runtime upgrade → v2026.4.12 + weixin plugin 2.1.8 | Dependency/Runtime bump — merged |
| [#1667](https://github.com/netease-youdao/LobsterAI/pull/1667) | Qwen console links migrated (DashScope → Bailian) | Config/docs fix — merged |
| [#1668](https://github.com/netease-youdao/LobsterAI/pull/1668) | Per-agent working directories | Data-layer migration + persist — merged |
| [#1669](https://github.com/netease-youdao/LobsterAI/pull/1669) | Settings: provider test-connection UX fixes | Disable logic + display-name — merged |
| [#1675](https://github.com/netease-youdao/LobsterAI/pull/1675) | Cowork: session list grouped by time buckets (Today/Yesterday/7d/30d/monthly) | UI/UX — merged |

**Fresh contributions (Aug 17):**
- [#2503](https://github.com/netease-youdao/LobsterAI/pull/2503) — Electron edit context menu for text inputs (cut/copy/paste) — *closed*
- [#2501](https://github.com/netease-youdao/LobsterAI/pull/2501) — Skill upgrade progress overlay fix + focused renderer logs — *closed*
- [#2505](https://github.com/netease-youdao/LobsterAI/pull/2505) & [#2502](https://github.com/netease-youdao/LobsterAI/pull/2502) — **dsh** (DeepSeek Harness) process launcher + engine integration — *closed (merged, platform: macos, area: renderer/build/main)*
- [#2506](https://github.com/netease-youdao/LobsterAI/pull/2506) — docs: dsh runtime setup instructions — *open*
- [#2504](https://github.com/netease-youdao/LobsterAI/pull/2504) — **OrcaRouter** provider integration (Anthropic/OpenAI-compatible gateway) — *open*

---

## 4. Community Hot Topics

**VOKO Cross-Platform Agent Communication — Issue [\#2500](https://github.com/netease-youdao/LobsterAI/issues/2500)** *(1 comment, new, Aug 17)*  
Author is promoting **VOKO**, an open-source "AI-agent communication layer" aiming to interconnect different agent frameworks/IM channels (OpenClaw, VOKO IM, AstrBot). Proposes A2A standardization and group-collaboration features. This is the **only genuinely "reactive" issue** today — a community outreach. *Signal: users want federation/interop between agent frameworks and IM — echoes Issue #1644.*

**Stale-groupPolicy overwrite — Issue [\#1653](https://github.com/netease-youdao/LobsterAI/issues/1653)** *(2 comments — highest in issues)*  
User reports `groupPolicy` being silently reverted to `allowlist` repeatedly. No maintainer attention visible in comments. Persisted unresolved since April.

---

## 5. Bugs & Stability

Only one new bug-adjacent item surfaced today (PR, not issue): **Electron text-field edit menu missing** — addressed by [#2503](https://github.com/netease-youdao/LobsterAI/pull/2503) (Cut/Copy/Paste/Select All scoped to text inputs).

Severity ranking of open, recurring bug reports (all stale, untouched by maintainers recently):

| # | Issue | Severity | Status |
|---|-------|----------|--------|
| 1 | [#1635](https://github.com/netease-youdao/LobsterAI/issues/1635) — Ollama local models (qwen3, gemma4) unusable; error on call despite working in other clients | **High** — core model-provider functionality broken | Open since Apr 12 |
| 2 | [#1662](https://github.com/netease-youdao/LobsterAI/issues/1662) — MCP engines other than SSE not discoverable/usable | **High** — tooling integration broken | Open since Apr 14 |
| 3 | [#1653](https://github.com/netease-youdao/LobsterAI/issues/1653) — `groupPolicy` repeatedly overwritten to `allowlist` | Medium — silent misconfiguration | Open since Apr 13 |
| 4 | [#1671](https://github.com/netease-youdao/LobsterAI/issues/1671) — MD→Word conversion stops midway with `sse response finish reason: full` | Medium — truncation in long outputs | Open since Apr 14 |
| 5 | [#1643](https://github.com/netease-youdao/LobsterAI/issues/1643) — False "content unsaved" warning when saving scheduled tasks (4.8, Win11) | Low | Open since Apr 12 |

---

## 6. Feature Requests & Roadmap Signals

**Strong signal — agent orchestration & MD-based workflows:** Issue [#1644](https://github.com/netease-youdao/LobsterAI/issues/1644) asks that the main agent be able to organize other agents (and its own spawned sub-agents) to complete complex tasks defined in Markdown. Today, agents are **mutually unaware**; the main agent cannot "see" or invoke sibling agents. This intersects with VOKO's outreach (#2500) — expect cross-agent orchestration to be a **future architectural focus**. Given PR #1660 (displaying non-main agents on the home screen) is still open, visibility into agent topology is clearly being built toward.

**Other signals:**
- **OrcaRouter provider** (PR #2504, open) — third-party LLM gateway integration, similar to OpenRouter; likely lands soon as a first-class provider.
- **dsh engine** (DeepSeek Harness) — new runtime/launcher added across build/renderer/main, with setup docs (PRs #2502/#2505/#2506). A new execution back-end is being folded in.
- **Per-agent working directories** (PR #1668, merged) — indicates a push toward multi-agent isolation and independent state management.

---

## 7. User Feedback Summary

**Pain points (persisting, from April):**
- **Local model integration friction (Ollama)** — users expect drop-in usage with local models; failures here cause frustration and push users to alternative clients ("cherrystudio works fine").
- **MCP protocol incompleteness** — beyond SSE is not working; limits tool-ecosystem reach.
- **Configuration gets silently overwritten** (`groupPolicy`) — erodes trust in settings persistence.
- **Long-context truncation** (`finish reason: full`) — blocks real-world document conversion tasks (MD→Word).
- **Minor UX inconsistencies** — unsaved-changes false positives; missing right-click menus (now addressed in PR #2503).

**Positive signals:**
- The stale-PR merge wave shows the maintainers are **actively clearing accumulated community contributions** — including significant UX polish (scroll-to-bottom, regenerate button, copy buttons, Esc-to-close, session grouping).
- Log redaction (PR #1661) addresses a real privacy concern (plaintext API keys in exported logs) — professionalism signal.

---

## 8. Backlog Watch

These require maintainer eyes — all are open, unresolved since **April**, and did **not** receive maintainer responses today:

| Item | Type | Age (days) | Why it matters |
|------|------|-----------|----------------|
| [#1635](https://github.com/netease-youdao/LobsterAI/issues/1635) — Ollama local models broken | Bug | ~128 | Core provider; pushes users to other products |
| [#1662](https://github.com/netease-youdao/LobsterAI/issues/1662) — non-SSE MCP unusable | Bug | ~126 | Tooling ecosystem limited |
| [#1644](https://github.com/netease-youdao/LobsterAI/issues/1644) — MD-based workflow / main-agent orchestration | Feature request | ~128 | Blocks advanced multi-agent use cases; high strategic value |
| [#1653](https://github.com/netease-youdao/LobsterAI/issues/1653) — `groupPolicy` silently overwritten | Bug | ~127 | Silent config corruption; confusing |
| [#1643](https://github.com/netease-youdao/LobsterAI/issues/1643) — False "unsaved" warning in scheduler | Bug | ~128 | UX annoyance on Windows |
| [#1671](https://github.com/netease-youdao/LobsterAI/issues/1671) — MD→Word truncation at SSE full | Bug | ~126 | Blocks practical document workflows |
| PR [#1277](https://github.com/netease-youdao/LobsterAI/pull/1277) — dependabot electron group bump (40.2.1 → 43.4.0) | Dependabot PR | ~138 | Long-pending dependency update; no comments |

**Project-health assessment:** Active maintainer effort today is high, but it's primarily **backlog administration** rather than new feature development or bug triage. Core-provider issues (Ollama, MCP) are dangerously old — the `stale` label on many issues suggests bot-based closure was considered but not executed. The community remains engaged (VOKO outreach, dsh contributions), but the **bug-response latency for April-era critical issues is the main health risk.**

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

# Moltis Project Digest — 2026-08-18

## 1. Today's Overview

Moltis shows solid, steady activity with 11 items updated in the last 24 hours, highlighting a healthy balance of maintenance and feature work. The project closed 6 pull requests while keeping 3 open, and resolved 2 issues including a CI formatting gate failure and a long-standing feature request for configurable RPC timeouts. Notably, the merge of PR #1130 (configurable webui RPC timeout) closes the two-month-old issue #1127, demonstrating sustained follow-through on community-driven improvements. The active work is concentrated on heartbeat configuration semantics (PRs #1208, #1209) and a substantial new Files library feature (PR #1206), indicating both bug-fixing rigor and forward-looking feature development. No new releases were published this period, suggesting the team may be consolidating changes before a version cut.

## 2. Releases

No new releases were published in the last 24 hours. The project appears to be in an accumulation phase, with multiple merged PRs (including dependency bumps, the shadow DOM fix, and the MiniMax Code agent) likely queued for an upcoming version.

## 3. Project Progress

Six pull requests were merged or closed today, moving several initiatives forward:

- **[PR #1130](https://github.com/moltis-org/moltis/pull/1130)** — **feat: make webui rpc timeout configurable** (merged, closes #1127): Adds configuration support for webui RPC timeouts, resolving a two-month-old enhancement request.
- **[PR #1103](https://github.com/moltis-org/moltis/pull/1103)** — **fix(browser): pierce shadow DOM lookups efficiently** (merged): Improves browser snapshot and ref-based lookup paths to efficiently pierce shadow DOM boundaries — a long-running fix (opened June 4) that addresses a previously blocked PR (#1100).
- **[PR #1207](https://github.com/moltis-org/moltis/pull/1207)** — **chore(deps): bump the cargo group across 1 directory with 4 updates** (merged): Updates `wasmtime-wasi`, `cmov`, `quinn-proto`, and `serde_with`.
- **[PR #1204](https://github.com/moltis-org/moltis/pull/1204)** — **feat: add MiniMax Code ACP agent** (merged): Adds a new `acp-minimax-code` external-agent kind backed by `mcode acp`, including default executable detection and registry updates.
- **[PR #1087](https://github.com/moltis-org/moltis/pull/1087)** — **chore(deps): bump tar from 0.4.45 to 0.4.46** (merged): Minor dependency update.
- **[PR #1125](https://github.com/moltis-org/moltis/pull/1125)** — **Support model and effort selection for external agents** (closed): Long-running PR (opened June 15) closed without merge, likely superseded or iterated elsewhere.

## 4. Community Hot Topics

Activity centers on heartbeat configuration and external agent support, with two active PRs from the same author:

- **[PR #1209](https://github.com/moltis-org/moltis/pull/1209)** (open): Fixes `heartbeat.update` to treat params as a patch rather than replacing the entire config — a correctness fix that addresses surprising behavior where unset keys reset to defaults.
- **[PR #1208](https://github.com/moltis-org/moltis/pull/1208)** (open): Makes the scheduler actually honor `heartbeat.active_hours` — a documented-and-tested feature that was never wired into the cron execution path.
- **[PR #1206](https://github.com/moltis-org/moltis/pull/1206)** (open): A substantial feature adding a managed Files library with authenticated streamed APIs and a Finder-style Settings browser, plus `MOLTIS_FILES_DIR` discovery support across container runtimes.

The underlying need across #1208 and #1209 is the same: users expect heartbeat configuration to be *semantic* (respecting active hours, preserving unspecified keys) rather than mechanical, suggesting maturing expectations around what "configuration" means for a cron-triggered agent system.

## 5. Bugs & Stability

One regression was identified and already closed:

- **[Issue #1202](https://github.com/moltis-org/moltis/issues/1202)** — **Format CI gate is red on main** (closed): The file-size check fails on `main` because `crates/memory-zvec/src/store.rs` (1799 lines) and `crates/gateway/src/methods/services/admin.rs` (1531 lines) exceed the 1500-line limit. Both files originate from commit `9b47001a`. **Severity: Low** — CI-only, not a runtime issue; closed within 24 hours, demonstrating responsive housekeeping.

No runtime crashes, data corruption, or user-facing regressions were reported today. The open heartbeat PRs (#1208, #1209) address functional bugs but are not marked as urgent regressions.

## 6. Feature Requests & Roadmap Signals

The two-month-old **[issue #1127](https://github.com/moltis-org/moltis/issues/1127)** — *allow to configure rpc timeout* — was closed with the merge of PR #1130, signaling that configurable timeouts are now available and the maintainers are listening to configuration-related asks.

Looking forward, the most likely next-version features are:

- **Heartbeat configuration fixes** (PRs #1208, #1209): Both are small, well-scoped, and address clear bug behaviors. Probability: very high.
- **Managed Files library** (PR #1206): This is a larger feature, but its detailed design (streamed APIs, container mount defaults, settings browser) suggests significant investment. Probability: medium-to-high, possibly the headline feature of the next minor release.
- **MiniMax Code ACP agent** (PR #1204, merged): Already in, will ship with the next release.
- **External agent model/effort selection** (PR #1125, closed): The closure without merge suggests this may still be in flux; watch for a revised approach to `/model` selection.

## 7. User Feedback Summary

No new user comments or reactions were recorded in the last 24 hours, but the merged items speak to persistent user needs:

- **Configurability**: Issue #1127 (RPC timeout) reflects a demand for operational control — users want to tune timeouts for slow or high-latency environments. The feature author, `khimaros`, filed both the issue and the PR, indicating a self-service contributor loop that works well.
- **Correctness expectations**: The heartbeat PRs (#1208, #1209) point to an underlying user pain: cron-scheduled agents firing outside configured active hours, and `heartbeat.update` silently resetting config keys. These are the kind of "quietly wrong" bugs that erode trust, and the author (`Lstarsky0`) filed both PRs with test references, suggesting a detail-oriented contributor.
- **External agent ecosystem growth**: The MiniMax Code agent addition (PR #1204) and the earlier model/effort selection work show that users are actively evaluating and integrating multiple external agent backends, making registry breadth a competitive factor.

## 8. Backlog Watch

- **[PR #1125](https://github.com/moltis-org/moltis/pull/1125)** — **Support model and effort selection for external agents** (closed June 15, closed 2026-08-17): After two months of activity, this PR was closed without a clear replacement PR linked. The feature (model/effort selection in `/model`) is important for external-agent UX; contributors and users will want a definitive statement on when or whether it will be reworked.
- **[PR #1103](https://github.com/moltis-org/moltis/pull/1103)** — **fix(browser): pierce shadow DOM lookups** (opened June 4, merged today): This aged PR finally merged, but the fact that it took 2.5 months — and notably that the original author (`s-salamatov`) could not push to the original PR head (`resumeparseeval/mycelium`) — points to a contributor-handoff friction worth watching. Consider whether a maintainer can help unblock follow-up work faster next time.
- **No long-dormant issues** currently demand urgent maintainer attention; the open items in registry are recent and being actively worked.

---

*All data reflects the 24-hour window ending 2026-08-18. Project health: strong — active community, responsive maintainers, and a clear release pipeline building toward a notable update.*

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

# CoPaw Project Digest
**Date: 2026-08-18**

---

## 1. Today's Overview

CoPaw (QwenPaw) shows a **high-activity day** with 14 issues and 35 PRs updated in the last 24 hours, indicating an actively maintained project. Six issues were closed and 22 PRs were merged/closed, demonstrating healthy throughput. The project is currently at **v2.1.0** (no new releases today), with ongoing work focused on **MCP tool integration fixes**, **media handling improvements** (image URLs, downloads, token counting), and **UI/UX polish** across the Console. Several **first-time contributor PRs** are in the queue, suggesting a welcoming community. No new releases were published today, but the volume of merged PRs suggests a **2.1.1 patch or 2.2.0 feature release may be brewing soon**.

---

## 2. Releases

**No new releases published today.** The project remains on **v2.1.0**, with the maintenance focus shifting to bug fixes and feature enhancements likely destined for the next patch release.

---

## 3. Project Progress

**22 PRs merged/closed today** — notable highlights:

| PR | Description | Status |
|---|---|---|
| [#7083](https://github.com/agentscope-ai/CoPaw/pull/7083) | **Compact background task list** — Console panel cap at ~3 rows with scroll, prevents chat input pushing | ✅ Merged |
| [#7017](https://github.com/agentscope-ai/CoPaw/pull/7017) | **PawApps open without reload** — newly installed apps activate immediately; page reload only for updates | ✅ Merged |
| [#5151](https://github.com/agentscope-ai/CoPaw/pull/5151) | **GitPanel tab style fix** — `ant-` prefix vs `qwenpaw` prefixCls mismatch resolved | ✅ Merged |
| [#7036](https://github.com/agentscope-ai/CoPaw/pull/7036) | **Media download controls** — unified audio/video download buttons in player bar | ✅ Merged |
| [#6975](https://github.com/agentscope-ai/CoPaw/pull/6975) | **Context-usage ring fix** — now updates after `/compact` (SSE flush issue) | ✅ Merged |
| [#6968](https://github.com/agentscope-ai/CoPaw/pull/6968) | **Token counting fix** — image base64 no longer counted as text tokens; prevents false 100% context | ✅ Merged |
| [#6940](https://github.com/agentscope-ai/CoPaw/pull/6940) | **DataPaw app runtime** — native data analysis PawApp with durable workspace | ✅ Merged |
| [#6981](https://github.com/agentscope-ai/CoPaw/pull/6981) | **i18n placeholder cleanup** — `/approve`/`/deny` hints removed from all 7 locales | ✅ Merged |
| [#6817](https://github.com/agentscope-ai/CoPaw/pull/6817) | **AnySearch web search integration** — replaces Tavily; MCP env-ref header fix | ✅ Merged (superseded by #7081) |

**Key feature advancement:** The [AnySearch integration](https://github.com/agentscope-ai/CoPaw/pull/7081) continues to evolve — a new open PR (#7081) supersedes the merged #6817, adding per-agent Console configuration and improved MCP client support.

---

## 4. Community Hot Topics

### 🔥 Most Active Issues

1. **[#6405 — MCP 2.0 migration: "Tool not found"](https://github.com/agentscope-ai/CoPaw/issues/6405)** *(7 comments, CLOSED)*
   - **User pain:** After upgrading to 2.0, MCP tools renamed to `[mcp-key]__[tool_name]` but consistently throw "Tool not found" (Docker 2.0.0post3)
   - **Analysis:** Migration compatibility issue; naming convention change may not be propagated through all code paths

2. **[#7011 — Console stop cancels active Feishu session](https://github.com/agentscope-ai/CoPaw/issues/7011)** *(6 comments, OPEN)*
   - **User pain:** Cross-session identity collision — Console UI stop request terminates an unrelated active Feishu conversation (v2.1.0)
   - **Analysis:** Session isolation bug; UI session IDs likely shared globally instead of per-channel

3. **[#7085 — Per-channel model configuration](https://github.com/agentscope-ai/CoPaw/issues/7085)** *(3 comments, OPEN)*
   - **User pain:** Model config is global/agent-level; users want per-channel models (e.g., 钉钉→gpt-4o, 微信→qwen-max, 控制台→llama.cpp)
   - **Analysis:** Strong feature demand from multi-channel users; roadmap likely

### 🔥 Most Active PRs

- [#7089 — DataPaw standalone release pipeline](https://github.com/agentscope-ai/CoPaw/pull/7089) — Infrastructure for independent plugin CDN publishing
- [#7087 — Localize remote media URLs before model requests](https://github.com/agentscope-ai/CoPaw/pull/7087) — Fixes hotlink-protected image failures (HTTP 403)
- [#7086 — Unify language options between settings gear/dropdown](https://github.com/agentscope-ai/CoPaw/pull/7086) — Missing Bahasa Indonesia & Vietnamese in settings gear (first-time contributor)

---

## 5. Bugs & Stability

Ranked by severity:

### 🔴 High Severity

| Issue | Description | Status |
|---|---|---|
| [#7082](https://github.com/agentscope-ai/CoPaw/issues/7082) | **`_StructuredOutputDynamicClass` not fully defined** — Pydantic error kills agent/toolkit initialization on console channel (v2.1.0) | OPEN, no fix PR |
| [#7063](https://github.com/agentscope-ai/CoPaw/issues/7063) | **Tool call crash** — `async for` on coroutine instead of async generator in `_execute_tool_call` (TypeError) | CLOSED (invalid; user code issue) |
| [#7011](https://github.com/agentscope-ai/CoPaw/issues/7011) | **Session identity collision** — Console stop cancels active Feishu session | OPEN |

### 🟡 Medium Severity

| Issue | Description | Status |
|---|---|---|
| [#7088](https://github.com/agentscope-ai/CoPaw/issues/7088) | **QQ image URLs expire (~2h rkey)** — model provider gets HTTP 400, stale URL poisons session history | CLOSED (bug confirmed) — Fix PR [#7087](https://github.com/agentscope-ai/CoPaw/pull/7087) open |
| [#7051](https://github.com/agentscope-ai/CoPaw/issues/7051) | **Console images lost on session reload** — backend serves data URL, frontend shows broken thumbnail | CLOSED |
| [#7084](https://github.com/agentscope-ai/CoPaw/issues/7084) | **Single-history navigation bug** — clicking historical conversation does nothing when only one exists | OPEN |

### 🟢 Low Severity

| Issue | Description | Status |
|---|---|---|
| [#7077](https://github.com/agentscope-ai/CoPaw/issues/7077) | **Plugin runtime hooks lost after workspace reload** — `workspace_created` callback not re-fired | CLOSED |
| [#7048](https://github.com/agentscope-ai/CoPaw/issues/7048) | **cron update `--text` returns success but prompt unchanged** | CLOSED (invalid) |
| [#7076](https://github.com/agentscope-ai/CoPaw/issues/7076) | **qwenpaw-creator: LLM model config 404 error** (v2.1.0) | OPEN |

**Positive signal:** Most bugs have been triaged quickly; merged fixes for token counting (#6968), context ring (#6975), and media downloads (#7036) address previously reported issues.

---

## 6. Feature Requests & Roadmap Signals

| Feature | Issue/PR | Community Interest | Likelihood for Next Version |
|---|---|---|---|
| **Per-channel model configuration** | [#7085](https://github.com/agentscope-ai/CoPaw/issues/7085) | High (multiple use cases listed) | 🟢 High — clean extension of `agent.json` |
| **PowerContext long-term memory backend** | [#7079](https://github.com/agentscope-ai/CoPaw/issues/7079) + [PR #7080](https://github.com/agentscope-ai/CoPaw/pull/7080) | Medium (first-time contributor) | 🟡 Medium — needs maintainer review |
| **Agent collaboration in a single session window** | [#6925](https://github.com/agentscope-ai/CoPaw/issues/6925) | Medium — UX friction | 🟡 Medium — significant UX refactor |
| **Detailed scheduled task telemetry** | [#7075](https://github.com/agentscope-ai/CoPaw/issues/7075) | Low-Medium — start time, duration, results | 🟡 Medium — straightforward backend addition |
| **AnySearch as first-class web search** | [PR #7081](https://github.com/agentscope-ai/CoPaw/pull/7081) | Low (vendor-driven) | 🟢 High — supersedes merged #6817 |
| **Session-scoped multi project directories** | [PR #6976](https://github.com/agentscope-ai/CoPaw/pull/6976) | Medium — power users | 🟡 Medium — large feature, still OPEN |
| **Persistent workspace artifact cards** | [PR #6719](https://github.com/agentscope-ai/CoPaw/pull/6719) | Medium — WorkBuddy-style UX | 🟡 Medium — OPEN for 2+ weeks |
| **Volcengine Agent Plan + Xiaomi MiMo V2.5 providers** | [PR #6515](https://github.com/agentscope-ai/CoPaw/pull/6515) | Low-Medium — provider coverage | 🟢 High — OPEN for 3 weeks, no conflicts |

**Prediction:** Next minor release (2.1.x) likely includes **AnySearch integration**, **DaraPaw release pipeline**, and **media URL localization** (#7087). A future 2.2.0 could bring **per-channel models** and **unified provider/model metadata** (#6302 — still OPEN).

---

## 7. User Feedback Summary

### Pain Points
- **MCP tool migration friction** (≥1 user): v2.0 upgrade breaks tool resolution (`Tool not found`); naming convention change reported as confusing
- **Session/history reliability** (multiple users): Images lost on reload (#7051), single-history navigation broken (#7084), cross-session cancellation (#7011), QQ image URL expiry (#7088)
- **Model configuration inflexibility** (≥1 user): Global-only model settings frustrate multi-channel deployments
- **English/Chinese language balance**: Issues submitted in both languages; Chinese-dominant support requests suggest a strong zh-CN user base

### Satisfaction Indicators
- **Rapid issue triage**: 6 closed issues today; most closed within 1–3 days of creation
- **Active community contributors**: 3 first-time contributor PRs today (#7086, #7080, #7081)
- **Vendor participation**: External teams (AnySearch, DataPaw) building on CoPaw — signals healthy ecosystem

### Dissatisfaction Signals
- **Issue #6405** suggests v2.0 upgrade path caused silent breakage for MCP-heavy users; resolution unclear
- **Issue #7076** (qwenpaw-creator 404) — tool-specific regression in latest version

---

## 8. Backlog Watch

### Issues Needing Maintainer Attention

| Issue | Age | Why It Matters |
|---|---|---|
| [#6515 — Volcengine/MiMo providers](https://github.com/agentscope-ai/CoPaw/pull/6515) | 3 weeks (OPEN PR) | Two commonly requested providers; no conflicts; straightforward addition |
| [#6302 — Unified provider/routing system](https://github.com/agentscope-ai/CoPaw/pull/6302) | 4 weeks (OPEN PR) | Large architectural refactor; sets direction for model management; needs review |
| [#6719 — Persistent workspace artifact cards](https://github.com/agentscope-ai/CoPaw/pull/6719) | 2 weeks (OPEN PR) | Major UX feature; no maintainer comments visible |
| [#6976 — Session-scoped multi project dirs](https://github.com/agentscope-ai/CoPaw/pull/6976) | 5 days (OPEN PR) | Power-user feature; needs design review |
| [#6925 — Single-window agent collaboration](https://github.com/agentscope-ai/CoPaw/issues/6925) | 6 days (OPEN) | UX pain point with no maintainer response |

### Risk Watch
- **PR #7080 (PowerContext memory)** and **PR #7081 (AnySearch)** are both **first-time contributor** PRs — they need maintainer mentorship to avoid stall
- **Issue #7082 (Pydantic crash)** is a hard blocker for console users on v2.1.0 — no fix PR yet; requires priority triage

---

*Data source: GitHub (agentscope-ai/CoPaw), retrieved 2026-08-18*

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# ZeroClaw Project Digest — 2026-08-18

## 1. Today's Overview

ZeroClaw remains in a period of high architectural activity, with the repository's governance and design processes dominating public discourse. Activity is intense: 50 issues and 50 pull requests were updated in the last 24 hours, with the vast majority remaining open and active. The project is clearly in a pre-0.9.0 hardening phase, with broad RFC ratification across security, gateway, runtime, and channel boundaries. The emergent theme is consolidation: migrating from per-channel ad-hoc logic (WhatsApp group admission, Email attachment handling, Telegram long-polling) toward unified, runtime-owned security and architecture contracts. A secondary but significant effort focuses on cross-platform test reliability, with an ongoing battle against Windows-specific failures and test fixtures that violate runtime gates. Maintainer bandwidth appears to be the most critical constraint, given the volume of high-risk, needs-maintainer-review PRs and a large accepted-RFC implementation backlog.

## 2. Releases

No new releases were published in the last 24 hours. The current version appears to be **0.8.4** (referenced in the "Work Lanes" RFC tracker), with the next milestone being **v0.9.0**, which is described in issue #7432 as a coordinated breaking-change release centered on auth, security, gateway boundaries, and tool policy. Expect a major release announcement in the coming weeks as that tracker's items are completed.

## 3. Project Progress

9 PRs were merged or closed in the last 24 hours, reflecting a blend of targeted security fixes and foundational infrastructure work:

- **[#9993]** `fix(email): stop implicit attachment file reads` — Closes a serious exfiltration vulnerability where an empty attachment payload could cause the system to spontaneously read arbitrary local files based purely on a display filename. (S-size, privacy fix)
- **[#9612]** `fix(channels): tie the WhatsApp Cloud approval token to a guard so no exit orphans it` — Fixes a credential-orphan bug that could leave pending approval tokens as dangling bearer credentials in the process-global map.
- **[#9765]** `fix(sop): load SOP definitions from the shared workspace, not data_dir` — Corrects a split-brain architecture bug where SOP definitions were loaded from the per-install data directory instead of the configurable, shared workspace.
- **[#9398]** `ci(tests): add scheduled macOS and Windows tests` — Adds a nightly scheduled CI job for macOS and Windows platform test suites, addressing the gap that let Windows-specific test failures into the wild (see #7462).
- **[#9544]** `fix(delegate): honor configured provider fallbacks` — Reconciled delegation with session-based provider routing, ensuring delegated targets use the same alias, routing, retry, and fallback logic as the main session (via the canonical session provider builder).

## 4. Community Hot Topics

The most active discussions (measured by comment count) reveal a community focused on governance, breaking architecture changes, and security hardening, all in the RFC stage:

- **[#6808]** `RFC: Work Lanes, Board Automation, and Label Cleanup` (24 comments) — This meta-governance RFC is about routing maintainer work more efficiently through automated labels and lanes. It signals a community stretched thin by maintenance load and seeking process relief.
- **[#8603]** `RFC: ZeroClaw Chat Completions profile` (24 comments) — Massive community signal: users want to plug ZeroClaw into existing OpenAI-protocol clients (Open WebUI, LobeChat, Continue.dev, Aider, LangChain). This is the highest-demand interoperability request in the tracker.
- **[#8303]** `RFC: Goal mode v1 — bounded foreground Matrix work` (22 comments) — Users want a durable user-objective loop that spans multiple agent turns, moving beyond single-turn prompting toward goal-oriented execution. High complexity, as it touches restart handoff and channel admission.
- **[#7155]** `RFC: Add a per-execution confirmation tier for high-risk shell commands` (20 comments) — Strong user interest in Claude Code-style command allowed/ask/deny policies, signaling a growing adoption of ZeroClaw as a personal-coding assistant rather than pure chat metaprogram.
- **[#9487]** `RFC: Runtime-owned conversation sessions and transport surface adapters` (19 comments) — A deep architectural RFC that seeks to make the runtime (rather than agents or channels) own conversation state and admissions. This is the linchpin architectural decision enabling the future "Runtime-owned" pattern visible across many other RFCs.

## 5. Bugs & Stability

Several concrete, high-severity bugs are being actively addressed:

- **[#7462]** `[Bug]: 74 test failures on Windows` (Open, S2) — The test suite has historically only run on Linux, masking a systemic Windows compatibility problem: Unix-only commands, path semantics issues, and console encoding failures. A fix PR ([#9398]) adding scheduled macOS/Windows CI was merged; remediation of the underlying test failures is ongoing and a major stability priority.
- **[#9965]** `[Task]: runtime-written executable test fixtures hit ETXTBSY` (Open, P1) — A Windows-specific race condition where test fixtures write, chmod, and execute a file after the test process is multithreaded, causing ETXTBSY failures. An interim fix ([#10010]) using symlinks is in review, with follow-up tasks planned for broader fixture cleanup (#10011).
- **[#10023]** `Failure logs claim the requested model, not the pinned fallback model` (Open, P2) — Misleading diagnostics in the reliable provider layer when a fallback model serves a request. A fix exists in the large, "XL" PR **[#10003]** ("account Reliable rejected attempts exactly"), which is pending maintainer review.
- **[#10059]** `Support Option-Backspace word deletion in ZeroCode text inputs` (Open, Low Risk) — This is a UX gap for macOS users in the ZeroCode editor (satisfyingly, the contributor also noted it in the digest!).
- **[#6586 / #9397 interplay]** — The Empty WhatsApp allowed_groups permit-none RFC (#9397) is flagging a security-misconfiguration default. While it is still in RFC status, the fix PR [#9612] (WhatsApp approval token guard) was merged, indicating focused token security work in this channel.

## 6. Feature Requests & Roadmap Signals

The RFC-heavy tracker signals a well-defined roadmap toward 0.9.0 and beyond:

- This period strongly indicates the **next major version (0.9.0) is centered on a runtime-owned architecture**: Runtime-owned conversations (#9487), runtime-owned security decision pipelines (#7142), unified attachment contracts (#9488), and platform-bound telemetry (#9621). Expect these to land together as coordinated breaking changes.
- **[Chat Completions Profile (#8603)]** is a "ratified" RFC with a dedicated tracker; this is the most significant feature signal for the developer ecosystem, as it positions ZeroClaw as a backend AI agent protocol service.
- Users are actively requesting **SOP (Standard Operating Procedure) capability contracts** (#9598) and **security decision overlays** (#7142), indicating a desire to run ZeroClaw as a governed, policy-enforcing agent inside organizational workflows, not just a personal assistant.
- **[#6653]** `[Feature]: Define host-architecture policy for emulated installs` — The community sees a use case for emulated installs (e.g., x86_64 on aarch64), which currently lacks a defined policy and is unresolved.

(Note: #6586 has no context in the digest; if it exists, it may be low-traffic or dormant; a "WhatsApp empty allowed_groups" topic was assumed via #9397.)

## 7. User Feedback Summary

- **Pain Point — Cross-Platform Parity (Windows):** The most persistent source of user friction is the Windows test failure backlog (#7462), indicating ZeroClaw's development has been heavily Linux-primary. The community is actively pioneering fixes (e.g., ETXTBSY workaround #10010) but is awaiting maintainer-driven design consensus on the “right” cross-platform test pattern.
- **Pain Point — Diagnosis & Transparency:**
  [#10023], [#9056] — Users report that failure logs are often misleading, obscuring whether a fallback provider or models are actually failing. They want exact, cause-specific diagnostics, a frustration echoed by the push for better telemetry (#9621).
- **Use Case — AI Coding Assistant:** The most active user-facing development work centers on vim/editor-style inputs in ZeroCode (#10059) and shell policy (#7155). This indicates a rapidly growing cohort is using ZeroClaw as a terminal-based AI operator, not just a chat App.
- **Desire — Ecosystem Interop:** High demand for the OpenAI protocol compatibility (#8603) shows that Chaser-Along users want to bring ZeroClaw into their existing LLM tooling landscape rather than fight a walled garden.

## 8. Backlog Watch

Several long-running, high-stakes items continue to require maintainer attention or review:

- **[RFC #6808 — Work Lanes and Board Automation]** (23 comments, started May 2026): This RFC directly targets the "process burden" that is a recurring pain point. Maintainers actively discussing this are effectively processing their own repair; action on it remains the highest-leverage governance move.
- **[RFC #6165 — Prefer a lighter ZeroClaw core through external integrations]** (15 comments, started April 2026): An architecture shift toward a leaner core by moving long-tail integrations (e.g., MCP, Lucid, Qdrant) to ext via WASM plugins. While slowing, it remains a pivotal direction decision that affects the core's complexity budget.
- **[PR #9314 — Telegram long-poll offset fix]** (Large PR, 26 days open, flagged 'needs-maintainer-review'): A currently-open fix for potential message loss (offset skip) in Telegram after transient failures. It is a high-risk, high-value fixing PR waiting for maintainer time.
- **[RFC #8692 — Maintainer decision queue for RFCs and design issues]** (30 days, open): This tracker is the very backlog of RFCs awaiting maintainer decision. Its existence documents the storage of the decisions that will shape v0.9.0, including key architecture bids from [#9487, #9488, #7141, #7142]. Fast-track this queue or 0.9.0 will slip.

---

*Data as of 2026-08-17; links are references to the ZeroClaw GitHub repository (zeroclaw-labs/zeroclaw).*

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/kky-wollu/agents-radar).*