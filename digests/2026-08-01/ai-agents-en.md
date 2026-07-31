# OpenClaw Ecosystem Digest 2026-08-01

> Issues: 500 | PRs: 500 | Projects covered: 13 | Generated: 2026-07-31 23:06 UTC

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

# OpenClaw Project Digest — 2026-08-01

## 1. Today's Overview

OpenClaw is experiencing **high activity** with 500 issues and 500 PRs updated in the last 24 hours, and no new releases today. While the issue volume is enormous (457 open active issues), the project is in a **heavy triage state**: the `clawsweeper` bot is actively processing items, no new releases were cut, and the vast majority of open issues carry labels like `needs-maintainer-review` and `needs-product-decision`. A significant volume of recent PRs — the #117084–#117095 series by `steipete` (15+ PRs in a single day) — signal a major internal refactoring push targeting gateway, memory, agents, and Discord/UI subsystems. The overarching theme is **reliability hardening**: the hottest issues cluster around message loss, crash-loop recovery, session-state wedging, and prompt-cache churn across Discord/WhatsApp/Telegram/Matrix channels, indicating the 2026.7.x track is facing significant stability challenges that are drawing maintainer and community attention.

## 2. Releases

**No new releases published today** (2026-08-01). The latest tracked release remains 2026.7.1/2026.7.2-beta.x, which is under active stabilization based on the bug reports referencing those versions.

## 3. Project Progress

Today's activity is dominated by **large-scale refactoring PRs** (many still open) rather than ground-breaking features. Key merged/closed items (n=112 merged/closed) include both bug fixes and internal cleanup by maintainers.

Top advanced areas:

- **Anthropic streaming & usage accounting unification** — [PR #117086](https://github.com/openclaw/openclaw/pull/117086) consolidates direct-provider/managed streaming policies, sharing token/context accounting and cache breakpoint placement.
- **Memory provider adaptation unification** — [PR #117094](https://github.com/openclaw/openclaw/pull/117094) unifies indexing, search config, and the Gateway `/v1/embeddings` endpoint; closes regression [#90786](https://github.com/openclaw/openclaw/issues/90786) (memory status fails on `google` provider).
- **Discord fixes** — [PR #117089](https://github.com/openclaw/openclaw/pull/117089) preserves fenced tool-call examples; [PR #117093](https://github.com/openclaw/openclaw/pull/117093) consolidates model picker navigation.
- **Gateway reliability fixes** — [PR #117036](https://github.com/openclaw/openclaw/pull/117036) adds 5s budget to stale-PID lsof scan (hotfix 2026.7.1 restart loop); [PR #117066](https://github.com/openclaw/openclaw/pull/117066) rejects sends on closing node sockets; [PR #117083](https://github.com/openclaw/openclaw/pull/117083) yields before post-ready background work; [PR #116997](https://github.com/openclaw/openclaw/pull/116997) protects Slack startup from plugin prewarm.
- **Telegram polling stall fix** — [PR #117081](https://github.com/openclaw/openclaw/pull/117081) prevents full thread-binding rewrites, addressing latency/polling stalls.
- **MS Teams multi-bot support** — [PR #112811](https://github.com/openclaw/openclaw/pull/112811) (open, ready for maintainer review) adds support for multiple Teams bot accounts.
- **UI queued-message restore fix** — [PR #117084](https://github.com/openclaw/openclaw/pull/117084) restores queued messages to the correct agent after reconnect.
- **Session SQLite lease unification** — [PR #117092](https://github.com/openclaw/openclaw/pull/117092) routes session-key writes through the canonical state lease owner.

## 4. Community Hot Topics

Most active/discussed Issues & PRs (top by comment count with signals of user pain):

- **#115326** — *Crash-loop breaker suppresses Discord/WhatsApp permanently* (`impact:message-loss`, `impact:crash-loop`, rated `platinum hermit`). 24 comments. Users can't recover channels even via documented `channels.start` path. Top pain point today. [Issue](https://github.com/openclaw/openclaw/issues/115326)
- **#79902** — *Companion-friendly SQLite transcript/session seams* (P2, 14 comments, 👍2). Power users want canonical runtime state to build on. [Issue](https://github.com/openclaw/openclaw/issues/79902)
- **#67288** — *amazon-bedrock-mantle lacks discovery gate, discovery runs every request* (13 comments). Unnecessary IAM token discovery per-request; friction for non-Bedrock users. [Issue](https://github.com/openclaw/openclaw/issues/67288)
- **#69208** — *Umbrella: duplicate transcript/replay/context assembly across channels* (P1, 12 comments). Meta-issue referencing #114137/#91564 etc.; clearly a cluster of recurring session-state bugs. [Issue](https://github.com/openclaw/openclaw/issues/114137)
- **#114137** — *Visible channel turns dispatch with no queued reply payloads — final text persisted, never delivered* (11 comments; `message-loss` P1) on Signal. [Issue](https://github.com/openclaw/openclaw/issues/114137)
- **#85251** — *Codex app-server silent after `turn/started`; embedded run wedges up to 360s* (11 comments). Session-state/performance issue. [Issue](https://github.com/openclaw/openclaw/issues/85251)
- **#109490** — *Codex turn interrupted after client-delegated tool result (`terminate:true`)* (P1, 10 comments). Promised work never executes after progress messages. [Issue](https://github.com/openclaw/openclaw/issues/109490)
- **#90414** — *agentmemory__memory_search returns "index metadata is missing" persistently* (P2, 10 comments). Persistent memory-core state cache failure. [Issue](https://github.com/openclaw/openclaw/issues/90414)
- **#10687** — *Fully dynamic model discovery (OpenRouter + beyond)* (P2, 9 comments, 👍3). High-demand feature; model catalogs move faster than baked-in lists. [Issue](https://github.com/openclaw/openclaw/issues/10687)
- **#107464** — *Telegram message(action=send) prematurely releases Codex turn in message_tool_only mode* (P1, 9 comments). [Issue](https://github.com/openclaw/openclaw/issues/107464)

**PR activity:** The top PRs (by size/immediacy) are #117089 (fix, P1), #117036 (fix, P1), and #117081 (fix, P1) — all flagged as needing proof or ready for maintainer look; several closed, including #117077 (`doctor` release inventory compaction) and #117076 (SQLite session compaction fix).

**Underlying need:** Community as a whole is grappling with **message delivery reliability** (messages sent but not delivered; transcripts persisted but channel output lost), **session-state corruption** (stuck `running`, stale claims, permanent black-holes), and **model/provider integration friction** (discovery, fallback silence, cache churn). These are being reported across Discord, WhatsApp, Telegram, Signal, Matrix, and Codex sidecar paths.

## 5. Bugs & Stability

**Critical/High severity (P1) bugs surfaced today or still active in the last 24h:**

| Bug | Impact | Fix PR? |
|---|---|---|
| [#115326](https://github.com/openclaw/openclaw/issues/115326) Crash-loop breaker suppresses Discord/WhatsApp permanently; `channels.start` fails (WebSocket 1006) | message-loss, crash-loop | No new fix PR |
| [#114137](https://github.com/openclaw/openclaw/issues/114137) Visible channel turns dispatch w/ no queued reply payloads — never delivered (Signal) | message-loss | No |
| [#114211](https://github.com/openclaw/openclaw/issues/114211) Matrix room agents loop on visible no-reply output, restart recovery, stale session replay | session-state, message-loss | No |
| [#114255](https://github.com/openclaw/openclaw/issues/114255) Restart mid-run leaves session `running` with live restart-recovery claim; Telegram spool retries forever | session-state | No |
| [#116418](https://github.com/openclaw/openclaw/issues/116418) Ollama provider never selected as primary in 2026.7.1; routing always falls back | auth-provider/session-state | No |
| [#114653](https://github.com/openclaw/openclaw/issues/114653) `sessions_send` transient failure in spawned-session visibility lookup indistinguishable from policy denial (silent catch) | security/session-state | No |
| [#116973](https://github.com/openclaw/openclaw/issues/116973) Docs vs code: `gateway.reload.debounceMs`/`deferralTimeoutMs` listed but retired in beta.5 | docs/config | Closed (docs issue) |
| [#114234](https://github.com/openclaw/openclaw/issues/114234) Usage-cost refresh lock never releasable after restart reuses owner PID (containers) | session-state | No |
| [#107464](https://github.com/openclaw/openclaw/issues/107464) Telegram premature Codex turn release with `message_tool_only` | message-loss | No |

**Medium severity regressions:**

- [#115001](https://github.com/openclaw/openclaw/issues/115001) — Hybrid memory search returns spurious 1.0 similarity scores via FTS LIKE-fallback hard-coded `textScore` (P2, regression).
- [#103198](https://github.com/openclaw/openclaw/issues/103198) — WebChat image attachments not mapped: `image_0` sent, not file path (P1, 👍3).
- [#115076](https://github.com/openclaw/openclaw/issues/115076) — Webchat text+image misclassified as `source_modality: image` (P2).
- [#109145](https://github.com/openclaw/openclaw/issues/109145) — Gateway HTTP server listens but doesn't accept connections (v2026.7.1-beta.5).
- [#108379](https://github.com/openclaw/openclaw/issues/108379) — Duplicate assistant generation attempts for Xiaomi MiMo (openai-completions).
- [#95610](https://github.com/openclaw/openclaw/issues/95610) — Prompt-cache prefix churn on OpenAI models defeats caching (P2, 7 comments).

**Bugs with linked/pr/open fix PRs:** #67288 (closed), #34528 (closed), #113403 (fix gated on review), #114234 (no PR), #117001 (closed), #117036 (PR up), #117081 (PR up), #117089 (PR up).

**Security-related:** [#7722](https://github.com/openclaw/openclaw/issues/7722) — Filesystem sandboxing config not implemented (P2, 👍4); [#64046](https://github.com/openclaw/openclaw/issues/64046) — Sensitive data masking (P1, 👍0, Chinese); [#114653](https://github.com/openclaw/openclaw/issues/114653) — Security-boundary confusion (looks like policy denial); [#117095](https://github.com/openclaw/openclaw/issues/?) — operator approval resolution refactor.

## 6. Feature Requests & Roadmap Signals

Requests that might land in 2026.8.x (based on volume, maintainer interest, and roadmap overlap):

- **FS Sandboxing** (`tools.fileAccess`) — [Issue #7722](https://github.com/openclaw/openclaw/issues/7722), P2, 👍4, oldest-standing feature request (Feb 2026). Likely to be picked up for a security pass.
- **Dynamic model discovery (OpenRouter + beyond)** — [Issue #10687](https://github.com/openclaw/openclaw/issues/10687), P1, 👍3. High traction; core model catalog being rebuilt.
- **Sensitive data masking/redaction** — [Issue #64046](https://github.com/openclaw/openclaw/issues/64046), P1, 👍0. Config/log/UI sanitization.
- **Per-spawn tool restrictions for sub-agents** — [Issue #15032](https://github.com/openclaw/openclaw/issues/15032), P2, security-review. Needed for DMZ-style isolation.
- **Multi-slot memory role architecture** — [PR #88504](https://github.com/openclaw/openclaw/pull/88504) open; big change, P2. Addresses factual recall vs. auto-capture vs. companion.
- **Remote reranker endpoint support** — [Issue #64438](https://github.com/openclaw/openclaw/issues/64438), P2. To complement remote embedding providers.
- **Anthropic advisor tool** (server-side tools) — [Issue #63930](https://github.com/openclaw/openclaw/pull/63930), P2. Adds generic server-tool-block handling.
- **Talks: Per-provider `baseUrl` for OAI-Realtime-compatible voice** — [Issue #114146](https://github.com/openclaw/openclaw/issues/114146), P2, 👍1. Echoes community build-outs on Alibaba/proxy endpoints.
- **Expose OpenRouter usage cost to agent runtime** — [Issue #9016](https://github.com/openclaw/openclaw/issues/9016), P2, 👍1.
- **Per-model generation timeout** — [Issue #8724](https://github.com/openclaw/openclaw/issues/8724), P2; google flash loops.
- **Telegram parseMode config** — [Issue #10944](https://github.com/openclaw/openclaw/issues/10944), P2; hardcoded Markdown.
- **WhatsApp sticker send support** — [Issue #7476](https://github.com/openclaw/openclaw/issues/7476), P2.
- **Azure Foundry GPT Realtime Talk** — [Issue #87325](https://github.com/openclaw/openclaw/issues/87325), P2.

Likely candidates for next releases: the `memory` refactor (#117094 / #88504) and the *dynamic discovery* work, given the number of provider-related issues (Ollama, OpenRouter, MiniMax, etc.).

## 7. User Feedback Summary

- **Reliability is the #1 dissatisfied area.** Users report that messages *appear* in the transcript/dashboard but are never delivered to Discord/WhatsApp/Signal/Telegram. This is the single most repeated, cross-channel complaint. Several users escalate with "permanent suppression," "black hole," "never delivered" language, showing confidence erosion in the delivery layer.
- **The crash-loop breaker + recovery path failing is painful.** #115326 explicitly documents the documented recovery failing; users cannot recover without manual DB edits. This is a P1 product-decision item.
- **Power users want canonical, stable runtime state.** Open requests for SQLite transcript seams (#79902, 👍2), stable plugin SDK for skills (#81913), and sharing usage cost to agents (#9016) show demand for programmatic composability and less "opaque blob scraping."
- **Model/provider fragmentation is growing.** Multiple issues around fallback silence (gpt-5.6-*, MiMo, Ollama routing), model discovery, and provider-specific bugs (MiniMax usage inversion, Bedrock discovery, Tencent source) indicate integration debt is mounting.
- **Cost/usage tracking is a consistent ask** (OpenRouter cost, MiniMax % used bug, usage-cost refresh lock bug) — users want transparent metering.
- **AI assistants in multi-channel group contexts are leaking replies.** The "foreground reply fence" issue (#92186) — replies shown in dashboard but not delivered to WhatsApp group — is a sharp edge case with high emotional impact.
- **Docs vs. runtime drift** (retired tuning paths, non-existent CLI flags) signals the docs pipeline is strained as 2026.7.x churns.

## 8. Backlog Watch

Items likely needing maintainer attention (long-lived, high-impact, no fix PR, not recently updated):

- **#69208 (Umbrella #114137)** — P1, 12 comments, no new fix PR, `needs-product-decision`. The entire cluster of duplicate transcript/replay/context assembly issues has no single fix yet. High risk.
- **#85251 (Codex silent turn)** — P1, 11 comments, no fix PR, `needs-maintainer-review`; can wedge sessions up to 360s.
- **#91564 (Telegram forum topic black hole)** — P1, 7 comments, no new PR, `needs-info`; inbound messages acked but never logged.
- **#70903 (Persistent file-based provider cooldown blocks users after billing recovery)** — P0, 6 comments, `stale`, no new PR. A claimed P0 with an old timestamp; severe availability impact if real.
- **#34528 (Feishu reaction suffix 400)** — Closed but only 7 comments; suggest fix is pending in another path.
- **#10687 (Dynamic model discovery)** — P1, 9 comments, 👍3, no PR; the catalog is baked in and users are hitting fallback confusion on gpt-5.6.
- **#90414 (agentmemory "index metadata is missing")** — P2, 10 comments, no fix PR; a memory-core issue that blocks all memory users on the affected setup.
- **#95610 (Prompt-cache prefix churn on OpenAI)** — P2, `platinum hermit`, 7 comments; affects cost/performance but not correctness; flagged for maintainer review.
- **#114234 (Usage-cost refresh lock forever)** — P1, 7 comments, PR open but `stale`; container-restart PID reuse means permanent cache freeze.
- **Long-idle but untouched P0/P1s** — #70903 is the only P0 on the list; verified stale.

**Open PRs needing maintainer review:** #117036 (5s lsof budget), #117089 (fenced tool-call examples), #112811 (MS Teams multi-bot), #113403 (explicit tool-less runs), #88504 (multi-slot memory architecture, XL), #116300 (tencent externalization, XL), #117040 (session list performance on large stores, XL).

---

*Generated from GitHub data for openclaw/openclaw, 2026-08-01.*

---

## Cross-Ecosystem Comparison

# Cross-Project Comparison Report: Personal AI Assistant Ecosystem
**Date:** 2026-08-01

---

## 1. Ecosystem Overview

The personal AI assistant open-source landscape is characterized by rapid iteration and a shared focus on **reliability hardening** across messaging channels. Projects are grappling with a common set of challenges: message delivery guarantees, session-state integrity, provider integration complexity, and the architectural shift toward multi-agent orchestration. A clear bifurcation is emerging between **core reference projects** (OpenClaw, ZeroClaw, IronClaw) investing heavily in architectural refactoring and contract extraction, and **end-user-focused projects** (NanoBot, CoPaw, PicoClaw) prioritizing UX polish and channel parity. The ecosystem is actively converging on SQLite as the standard session-storage layer, while security concerns (webhook authentication, path traversal, multi-tenant isolation) are surfacing as top-priority issues across multiple projects. Overall, the landscape is healthy but stretched thin, with many projects operating in "firefighting" mode post-major-migration.

---

## 2. Activity Comparison

| Project | Issues (24h) | PRs (24h) | Releases | Health Score | Primary Activity Type |
|---|---|---|---|---|---|
| **OpenClaw** | 500 updated | 500 updated | None | 🟡 **Moderate** — high volume, but heavy triage and stability churn | Reliability hardening & refactoring |
| **NanoBot** | 5 (3 open) | 17 (10 open, 7 merged) | None | 🟢 **Healthy** — high velocity, responsive maintainers | Feature development & bug fixes |
| **Hermes Agent** | 50 updated | 50 updated | v0.19.1 (July 30) | 🟢 **Healthy** — active but "firefighting" | Post-release stabilization |
| **PicoClaw** | 2 updated | 3 open | None (0.3.1 latest) | 🟢 **Healthy** — deliberative review cycle | Feature reviews & consolidation |
| **NanoClaw** | 8 updated | 9 updated (3 merged) | None (v2.1.54 blocked) | 🟡 **Moderate** — steady but strategic crossroads | Channel expansion & infrastructure |
| **NullClaw** | 0 | 1 open | None | 🟡 **Low activity** — maintenance phase | Minimal |
| **IronClaw** | 29 updated (22 open) | 50 updated (18 open, 32 merged) | None (release PR stalled 30d) | 🟡 **Moderate** — industrious but stretched | Architectural refactoring ("Reborn") |
| **LobsterAI** | 0 new (4 stale closed) | 12 updated (11 merged) | None | 🟢 **Healthy** — steady maintenance | Bug fixes & UX polish |
| **Moltis** | 2 (1 bug, 1 closed) | 8 updated (2 merged) | None | 🟢 **Healthy** — active security hardening | Security fixes & feature expansion |
| **CoPaw** | 21 updated | 43 updated (13 merged) | None (2.0.1 latest) | 🟡 **Moderate** — high-intensity stabilization | Post-migration regression fixes |
| **TinyClaw** | 0 | 0 | None | ⚪ **Inactive** | — |
| **ZeptoClaw** | 0 | 0 | None | ⚪ **Inactive** | — |
| **ZeroClaw** | 44 updated | 44 updated (6 merged) | None | 🟢 **Healthy** — high-velocity design phase | Security hardening & RFCs |

---

## 3. OpenClaw's Position

**Advantages vs. Peers:**
- **Scale:** With 500 issues/PRs updated in 24 hours, OpenClaw operates at 10x the activity volume of its nearest competitor (IronClaw, ZeroClaw at ~50). This scale drives faster bug discovery but also creates triage bottlenecks.
- **Channel breadth:** Supports Discord, WhatsApp, Telegram, Signal, Matrix, MS Teams, Slack, and WeChat — the widest channel coverage in the ecosystem. Competitors typically cover 2-4 channels.
- **Architectural maturity:** The gateway/memory/agent separation and the streaming/usage accounting unification (PR #117086) demonstrate a level of internal consistency that smaller projects (PicoClaw, NullClaw) have not yet reached.
- **Community investment:** Issues like #79902 (SQLite transcript seams) and #10687 (dynamic model discovery) show power users building on OpenClaw's foundation — a moat that smaller projects lack.

**Technical Approach Differences:**
- OpenClaw uses a **unified gateway** with per-channel adapters, while NanoClaw and CoPaw use container-first isolation models.
- OpenClaw's memory architecture (multi-provider, with embeddings) is more ambitious than NanoBot's JSONL→SQLite migration or Moltis's Zvec backend.

**Community Size Comparison:**
- OpenClaw's 457 open active issues dwarf all peers. NanoBot (5 issues) and NullClaw (0 issues) appear to serve niche communities by comparison.
- However, OpenClaw's **reliability reputation is under pressure** — the "message black hole" complaints (#115326, #114137) are the ecosystem's most severe user-facing pain points this week. Smaller projects like NanoBot are avoiding these issues by shipping fewer features more carefully.

---

## 4. Shared Technical Focus Areas

| Requirement | Projects | Specific Needs |
|---|---|---|
| **Message delivery guarantees** | OpenClaw, CoPaw, ZeroClaw | Persistent "sent but not delivered" failures; webhook auth bypass (ZeroClaw P0 #9565) |
| **Session-state integrity** | OpenClaw, Hermes, Moltis, CoPaw | Stuck `running` states, corrupted manifests (CoPaw #6520), session persistence across restarts |
| **SQLite as canonical storage** | OpenClaw (#79902), NanoBot (#5173), Hermes | Migration from JSONL, transcript seams for companion apps |
| **Provider/model discovery** | OpenClaw (#10687), CoPaw (#6302), ZeroClaw (#8603), NullClaw (#981) | Dynamic catalogs, CLI-based providers (grok-cli), OpenAI-compat adapters |
| **Memory separation** | OpenClaw (#88504), ZeroClaw (#9048), CoPaw (#6555) | Distinguishing conversation history from curated long-term memory |
| **Security hardening** | Moltis (#1180), ZeroClaw (#9565), IronClaw (#6900), NanoClaw (#2923) | Path traversal, webhook auth, multi-tenant isolation, signature verification |
| **Multi-agent orchestration** | OpenClaw, IronClaw, CoPaw, ZeroClaw | Sub-agent spawning, A2A protocols, delegate recursion caps |
| **Cost/usage transparency** | OpenClaw, Hermes, ZeroClaw, CoPaw | Token metering, usage-cost APIs, caching optimization |

---

## 5. Differentiation Analysis

| Project | Primary Focus | Target Users | Architectural Style |
|---|---|---|---|
| **OpenClaw** | Reliability & scale | Power users, self-hosters | Unified gateway, multi-provider memory |
| **NanoBot** | Lightweight UX | Individual users, mobile-first | SQLite storage, WebUI-forward |
| **Hermes Agent** | Multi-agent desktop | Advanced users, macOS/Windows | Desktop app + gateway, plugin ecosystem |
| **PicoClaw** | Protocol breadth | Niche protocol users (DeltaChat, Simplex, IRC) | Channel-adapter architecture |
| **NanoClaw** | Container-first security | Security-conscious users, restricted environments | Docker/K8s isolation, skill-based model |
| **NullClaw** | CLI-provider integration | Users of multiple AI CLIs (Codex, Gemini, Claude, Grok) | Minimal, modular provider pattern |
| **IronClaw** | Enterprise multi-tenant | Organizations, production deployments | Contract-crate extraction, MCP support |
| **LobsterAI** | Desktop UX & caching | End-users, Chinese-language market | OpenClaw-compatible, UI polish focus |
| **CoPaw** | Qwen ecosystem | Alibaba/AgentScope users, Desktop consumers | AgentScope 2.0 runtime, cross-platform |
| **Moltis** | Enterprise trust & observability | Teams, security-sensitive deployments | Rust core, NIP-29/Buzz, Langfuse OTel |
| **ZeroClaw** | Architectural innovation | Early adopters, RFC-engaged community | RFC-driven, wasmtime sandboxing |

**Key differentiators:**
- **Security posture:** IronClaw and Moltis lead with formal multi-tenant isolation (openat2, per-account operators). CoPaw's Windows manifest corruption (#6520) and ZeroClaw's webhook P0 highlight security debt in others.
- **Target user:** NanoBot and CoPaw target **consumer-grade desktop/mobile**, while IronClaw and ZeroClaw target **production enterprises**. OpenClaw sits in between, serving power users and self-hosters.
- **Innovation pace:** ZeroClaw's RFC volume (14 comments on memory separation) exceeds all peers, while NullClaw's sole PR reflects a niche but focused roadmap.

---

## 6. Community Momentum & Maturity

**Tier 1 — High-Velocity, Actively Refactoring (3+ PRs merged/day):**
- **OpenClaw** — Massive but in triage; stability churn is the narrative.
- **IronClaw** — Disciplined architecture migration (WS1.x contract extraction), but security issues piling up.
- **ZeroClaw** — Fast-moving RFC + security cycle; many accepted features likely in next release.
- **CoPaw** — Post-migration firefighting; 13 PRs merged but regression surface is broad.

**Tier 2 — Steady, Feature-Focused (1-7 PRs merged/day):**
- **NanoBot** — Healthy velocity, responsive to community (same-day fixes); SQLite migration is a milestones.
- **Hermes Agent** — Post-v0.19.1 stabilization; high community engagement on architectural issues.
- **LobsterAI** — Consistent maintenance cadence; UX polish phase after feature surge.
- **Moltis** — Active security hardening + feature expansion; moderate volume.

**Tier 3 — Deliberate / Low Activity:**
- **PicoClaw** — Consolidation phase; long PR review cycles (5 weeks for Simplex) suggest cautious maintainers.
- **NanoClaw** — Steady but strategically at a crossroads (K8s/native mode demands unanswered).
- **NullClaw** — Minimal; 1 PR, zero issues, maintenance mode.
- **TinyClaw & ZeptoClaw** — Inactive in the last 24 hours.

**Stabilizing vs. Iterating:**
- **Stabilizing:** Hermes (post-v0.19.1), CoPaw (post-2.0 migration), OpenClaw (2026.7.x stabilization track).
- **Rapidly iterating:** IronClaw (Reborn refactor), ZeroClaw (RFC-driven features), NanoBot (SQLite + WebUI).

---

## 7. Trend Signals

**1. Reliability is the #1 user demand across the board.**
OpenClaw's "message black hole" complaints, CoPaw's "silent failures," and ZeroClaw's webhook auth bypass all point to the same conclusion: users will tolerate missing features but not missing messages. **Implication:** Agent developers should treat delivery acknowledgments and fail-closed webhook design as non-negotiable requirements.

**2. SQLite is winning as the session-storage standard.**
NanoBot's JSONL→SQLite migration (#5173), OpenClaw's SQLite transcript seam request (#79902), and Hermes's state.db issues all converge on a single conclusion: SQLite offers the right balance of durability, queryability, and operational simplicity for agent runtime state. **Implication:** New projects should default to SQLite from day one rather than JSONL or in-memory stores.

**3. Memory separation is the next architectural battleground.**
ZeroClaw's memory-separation RFC (#9048), OpenClaw's multi-slot memory PR (#88504), and CoPaw's auto-memory flush fix (#6592) signal a shift from "one big context" to **explicitly layered memory** (conversation history vs. curated long-term vs. auto-captured recall). **Implication:** Building memory as a plugin with clear seams — rather than a monolithic feature — will become a competitive differentiator.

**4. Provider fragmentation is accelerating, and dynamic discovery is the answer.**
OpenClaw (#10687), CoPaw (#6302), ZeroClaw (#8603), and NullClaw (#981) all address the same problem: baked-in model catalogs are obsolete within weeks. The ecosystem is converging on **dynamic model discovery** (OpenRouter, CLI-based providers, OpenAI-compat adapters) and **configurable fallback chains** (PicoClaw #3200). **Implication:** Agent developers should design provider abstraction layers that treat model catalogs as external data, not code.

**5. Multi-agent orchestration is moving from experimental to production.**
Hermes's recursive-delegation meltdown (#52484), CoPaw's spawn_subagent schema fixes, IronClaw's admin-managed agents (#6578), and ZeroClaw's A2A outbound client RFC (#9106) all signal that **sub-agent delegation is entering mainstream use** — and that safety caps (max depth, timeout, billing limits) are the missing feature. **Implication:** Any agent that can spawn sub-agents must implement hard recursion limits and cost guardrails by default.

**6. Observability is becoming a core requirement, not a bolt-on.**
Moltis's instrumentation PR (#1174), ZeroClaw's OTel correlation RFC (#8933), and OpenClaw's cost/usage accounting unification all treat **structured, correlatable logs** as essential for debugging multi-turn, multi-channel agents. **Implication:** Adopt OpenTelemetry semantics (e.g., `gen_ai.conversation.id`) early to avoid painful retrofits.

**7. Security is the ecosystem's weak link, and it's being exposed.**
Path traversal (Moltis #1180), webhook auth bypass (ZeroClaw P0 #9565), multi-tenant memory leaks (IronClaw #6900), and absolute-path command bypasses (Hermes #71995) show that agent frameworks are reaching production scale before their security models have caught up. **Implication:** For developers, the safest architecture is **container-first isolation** (NanoClaw, IronClaw's openat2) combined with **fail-closed external interfaces** (webhooks, pairing signatures).

**8. Desktop UX is the new battleground for user adoption.**
CoPaw's quick-access button (#6083), Hermes's sidebar jitter fix, LobsterAI's scroll/copy polish, and NanoBot's scroll-preservation fix all indicate that **polished desktop/mobile UI is now a retention factor**, not just a nicety. **Implication:** Agent products that treat UI as secondary will lose to those that invest in interaction details (loading states, keyboard shortcuts, scroll behavior).

---

*Report generated from community digest summaries for 2026-08-01. Data reflects public GitHub activity and community discussions only.*

---

## Peer Project Reports

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot Project Digest
**Date: 2026-08-01**

---

## 1. Today's Overview

NanoBot is experiencing a **high-velocity development period** with 17 PRs updated in the last 24 hours (10 open, 7 merged/closed) and 5 issues tracked (3 open, 2 closed). The project shows **healthy momentum** across multiple fronts: a major architectural migration from JSONL to SQLite session storage was merged, multiple channel-specific bug fixes (Weixin, Slack, WhatsApp) landed, and contributions are coming from a diverse set of community members including first-time contributors. The maintainer team appears responsive, with several issues receiving same-day fixes. No new releases were published in this window.

---

## 2. Releases

**No new releases** in this reporting period.

---

## 3. Project Progress

Seven PRs were merged/closed today, showcasing significant advancement:

### Infrastructure & Architecture
- **[#5173 — feat(session): migrate session storage from JSONL to SQLite](https://github.com/HKUDS/nanobot/pull/5173)** *(merged)* — This is the most significant architectural change of the day. SQLite becomes the sole runtime session store with transactional import from existing JSONL files as rollback backups. This marks a major performance and scalability milestone for the project.

- **[#5145 — fix(ci): stabilize and speed up CI](https://github.com/HKUDS/nanobot/pull/5145)** *(merged)* — Replaced a timing-dependent timeout test with a stdin-gated readiness handshake and batched dependency installs, improving CI reliability and speed.

### Channel Fixes
- **[#5196 — fix(weixin): recover refreshed state after session expiry](https://github.com/HKUDS/nanobot/pull/5196)** *(merged)* — Fixes issue #5195; reloads persisted Weixin state after a session pause, preventing the 60-minute silent deadlock loop after token refresh.
- **[#4223 — fix(weixin): reload session state after pause expiry](https://github.com/HKUDS/nanobot/pull/4223)** *(merged)* — An older PR (June 2026) that resolved its merge conflicts and was finally landed alongside the newer Weixin fix.
- **[#5192 — fix(slack): scope channel thread openers to their own session](https://github.com/HKUDS/nanobot/pull/5192)** *(merged)* — Fixes a bug where top-level channel messages that open Slack threads shared a single channel-wide session, causing unrelated threads to see each other's messages.

### WebUI & Configuration
- **[#5193 — fix(webui): preserve user scroll ownership near tail](https://github.com/HKUDS/nanobot/pull/5193)** *(merged)* — Improves scroll behavior in the WebUI so the user's position is maintained when near the live tail.
- **[#5189 — fix(config): install timezone data on all platforms](https://github.com/HKUDS/nanobot/pull/5189)** *(merged)* — Fixes Termux compatibility by installing `tzdata` as a fallback for minimal Linux hosts, with strict timezone validation preserved.

---

## 4. Community Hot Topics

### Most Active Discussions

**1. Issue #5149 — "[bug] no audio ?"** (3 comments)
[GitHub Issue](https://github.com/HKUDS/nanobot/issues/5149)
- User reports that NanoBot receives but cannot send audio messages via WhatsApp.
- The underlying need appears to be **full multimodal messaging support**, particularly audio file transmission.
- This issue highlights the expectation that NanoBot should handle all message types symmetrically (send AND receive).

**2. Issue #5195 — "[bug] [weixin] Re-scan QR login overwrites new token"** (2 comments, now closed)
[GitHub Issue](https://github.com/HKUDS/nanobot/issues/5195)
- Root-caused by the community with a detailed analysis of the token overwrite race condition.
- Resolved same-day via PR #5196. Shows strong community debugging collaboration.

**3. Issue #5198 — "[bug] Not possible to change models in a specific session"** (0 comments, new)
[GitHub Issue](https://github.com/HKUDS/nanobot/issues/5198)
- User wants per-session model selection — clicking the model blip does nothing and `/model` command only uses fallback models.
- This is a **UX gap** versus Cloud SaaS AI interfaces. Likely to draw more attention.

---

## 5. Bugs & Stability

### Active Bugs by Severity

**🔴 High — Issue #5198: Cannot change models per-session**
[GitHub Issue](https://github.com/HKUDS/nanobot/issues/5198)
- No fix PR yet. User expectations from cloud SaaS UIs are unmet.
- Could be considered a **feature gap** rather than a bug, but impacts daily usability.

**🔴 High — Issue #5149: No audio sending on WhatsApp**
[GitHub Issue](https://github.com/HKUDS/nanobot/issues/5149)
- No fix PR yet. Incomplete messaging channel support.
- Requires investigation of the `neonize` FFmpeg integration.

**🟡 Medium — Issue #5190: Module script MIME type failure**
[GitHub Issue](https://github.com/HKUDS/nanobot/issues/5190)
- Windows-specific bug where `.js` files are served with `text/plain` due to Windows registry association overriding Python's mimetypes.
- **Fix PR exists**: [#5191 — Register correct MIME types for static assets on Windows](https://github.com/HKUDS/nanobot/pull/5191) (open).

**🟡 Medium — Issue #5195: Weixin re-login token overwrite (closed)**
- Fixed by PR #5196. Closed successfully.

### Stability Improvements
Several P1 priority fix PRs are waiting for review/merge:
- **[#5201 — tolerate malformed persisted session summary](https://github.com/HKUDS/nanobot/pull/5201)** *(P1, open)* — Session auto-compaction could crash on invalid persisted metadata.
- **[#5200 — preserve wait targets across response truncation](https://github.com/HKUDS/nanobot/pull/5200)** *(P1, open)* — Exec session `wait_for` could miss targets when output was truncated.

---

## 6. Feature Requests & Roadmap Signals

### Strong Signals (PRs Already Submitted)

**1. DeepSeek Responses API support** — [PR #5197](https://github.com/HKUDS/nanobot/pull/5197)
- Routes `deepseek-v4-flash` through the native Responses API with streaming and function-tool support.
- Indicates **active provider expansion** and model optimization.

**2. Quick Chat and Temporary Chat in WebUI** — [PR #5184](https://github.com/HKUDS/nanobot/pull/5184)
- Persistent Quick Chat as a first-class UI entry + opt-in Temporary Chat with in-memory-only history.
- This is a **consumer-grade UX feature** that often wins over new users.

### Emerging Requests
- **Per-session model switching** (Issue #5198) — likely to become a feature in the next version given the UX gap.
- **Audio sending across channels** (Issue #5149) — necessary for WhatsApp parity.

### Backlog Features (Older PRs, Still Open)
- **[Session management commands (export/import/search/stats)](https://github.com/HKUDS/nanobot/pull/1565)** — Waiting since March 2026.
- **[Skill status CLI command](https://github.com/HKUDS/nanobot/pull/1319)** — Waiting since February 2026.

---

## 7. User Feedback Summary

### Pain Points

| Theme | Evidence | Sentiment |
|-------|----------|-----------|
| **Channel messaging gaps** | WhatsApp audio send fails (#5149) | Negative — channel parity expected |
| **Session model control** | Cannot switch models per session (#5198) | Negative — UX falls short of cloud SaaS |
| **Cross-platform issues** | Termux timezone crash (#5187, fixed), Windows MIME (#5190) | Improving — responsive fixes |
| **WebUI polish** | Scroll behavior (fixed, #5193) | Positive trajectory |

### Satisfaction Signals
- **Weixin token bug** (#5195): Community root-caused and maintainer fixed same-day — strong confidence in the project's responsiveness.
- **SQLite migration** (#5173): Timely infrastructure improvement, likely to address session listing performance for heavy users.

---

## 8. Backlog Watch

### PRs Requiring Maintainer Attention

| PR | Age | Status | Notes |
|----|-----|--------|-------|
| **[#1656 — fix(validation): handle None value in string schema validation](https://github.com/HKUDS/nanobot/pull/1656)** | ~5 months | Conflict | Simple bugfix that prevents a TypeError; needs conflict resolution |
| **[#1565 — feat(session): add session export, import, search and stats commands](https://github.com/HKUDS/nanobot/pull/1565)** | ~5 months | Conflict | Significant feature set; likely superseded by SQLite migration (#5173) |
| **[#1319 — feat: add skill status command](https://github.com/HKUDS/nanobot/pull/1319)** | ~5 months | Conflict | Useful diagnostic for ClawHub skill issues; needs conflict resolution |

### Open P1 PRs Awaiting Review
- **[#5201 — fix(session): tolerate malformed persisted session summary](https://github.com/HKUDS/nanobot/pull/5201)** — crash fix, P1
- **[#5200 — fix(exec): preserve wait targets across response truncation](https://github.com/HKUDS/nanobot/pull/5200)** — regression fix, P1

All three long-open PRs are marked with `conflict` status, suggesting they need maintainer time to resolve merge conflicts rather than new code. The session-related PRs (#1565) may be fully superseded by the SQLite migration and could benefit from a maintainer decision (merge vs. close).

---

## Project Health Assessment

**Overall: 🟢 Healthy — High velocity, responsive maintainers, clear roadmap signals**

- **Velocity**: Very high — 17 PRs touched in 24h with 7 merged
- **Responsiveness**: Excellent for bugs; several issues fixed same-day
- **Backlog risk**: Three stale PRs with conflicts need triage decisions
- **Community engagement**: Active contributors including new names (KDB-Wind, chengyongru, pblocz, shixi-li)
- **Architecture evolution**: SQLite migration signals long-term scalability focus

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent Project Digest
**Date:** August 1, 2026

---

## 1. Today's Overview

Hermes Agent is experiencing an extremely high level of community engagement and development activity. With exactly 50 issues and 50 PRs updated in the last 24 hours, the project is operating at a healthy, fast-paced cadence. The release of v0.19.1 (v2026.7.30) as a stable patch tag consolidates over 1,000 merged PRs, signaling a period of maturation and stabilization after a major feature push. Community contributions are strong, with numerous drive-by fixes for regressions reported just days after the release. The backlog, however, is significant — several key architectural issues (recursive delegation, absolute-path security bypass, and session-state corruption) remain open and are attracting community concern, indicating that while velocity is high, deep-rooted technical debt persists.

---

## 2. Releases

**v0.19.1 (v2026.7.30)** — Released July 30, 2026 as a patch release.

- **Scope:** Rolls up approximately 1,000+ PRs merged since v0.19.0 into a stable tagged release for downstream consumers.
- **Audience:** Intended primarily for Docker images, hosted deployments, and fresh installs.
- **Notes:** Given the title and description, this is an aggregation tag rather than a feature-heavy minor release. No explicit breaking changes or migration steps were called out in the release notes excerpt, but given the sheer volume of PRs, downstream users should verify their plugin ecosystem and configuration schemas against the release notes for any silent API changes.

---

## 3. Project Progress

The last 24 hours saw four closed/merged PRs (out of 50 updated). The activity is dominated by **stabilization and hardening after the v0.19.1 tag**:

- **Thread-scoped output silencing fixes** (PRs [#72868](https://github.com/NousResearch/hermes-agent/pull/72868) and [#73012](https://github.com/NousResearch/hermes-agent/pull/73012)) address a class of `ValueError: I/O operation on closed file` errors on the gateway caused by global `sys.stdout` redirects poisoning concurrent threads. This was a real production incident (nine cron jobs failing in one tick, 328 errors during parallel delegation).
- **Gateway fixes:** Deep community PRs for Discord bot-loop suppression ([#53266](https://github.com/NousResearch/hermes-agent/pull/53266)), email cron report preservation ([#53264](https://github.com/NousResearch/hermes-agent/pull/53264)), and a WhatsApp command-prefix regression ([#75716](https://github.com/NousResearch/hermes-agent/pull/75716)).
- **Desktop jitter fix:** PR [#75714](https://github.com/NousResearch/hermes-agent/pull/75714) proposes memoization of sidebar rows to fix the Windows 11 scrolling jitter issue.
- **Agent/Delegate management:** PR [#75715](https://github.com/NousResearch/hermes-agent/pull/75715) prevents the Desktop WebSocket orphan reaper from tearing down sessions with live delegations.

---

## 4. Community Hot Topics

The most engaged issues highlight deep architectural concerns and feedback on UX safety:

- **[#64231 — Lifecycle-event catalog & hook taxonomy (12 comments)](https://github.com/NousResearch/hermes-agent/issues/64231)**
  This is a classic maintainer-led triage issue on the observer-hook PR cluster. The community is weighing in on how to standardize hooks rather than merge a dozen one-off additions. The underlying need is clear: the plugin system needs a defined extension model, and the community wants predictable, documented APIs.

- **[#66887 — Multiplexed gateway session persistence bug (6 comments)](https://github.com/NousResearch/hermes-agent/issues/66887)**
  Secondary Telegram profiles write to the default profile's `state.db`. This data-confusion issue is a P2 and has the "risk-session-state" sweeper tag. The 6 comments indicate deep investigation into a subtle scoping failure between config and storage.

- **[#52484 — Token Incinerator: Recursive delegation without max depth (5 comments)](https://github.com/NousResearch/hermes-agent/issues/52484)**
  (P2) This is a concerning structural flaw: open-ended prompts cause cascading sub-agent spawning with no depth cap, leading to "recursive delegation meltdown." This is cost-related and could be a future "runaway bill" story.

- **[#71995 — Absolute-path invocation bypasses hardline floor (5 comments)](https://github.com/NousResearch/hermes-agent/issues/71995)**
  (P2, Security) `shutdown` blocked, but `/sbin/shutdown` is allowed. This is a classic security flaw that underscores the difficulty of a "hardline" safety approach. The community urgency is high, and a fix PR ([#71996](https://github.com/NousResearch/hermes-agent/pull/71996)) is already open.

---

## 5. Bugs & Stability

**Critical/High Severity (P2):**

- **Infinite delegate recursion ([#52484](https://github.com/NousResearch/hermes-agent/issues/52484))** — Architectural flaw, potential runaway compute/billing. No fix PR yet.
- **Absolute-path hardline bypass ([#71995](https://github.com/NousResearch/hermes-agent/issues/71995))** — Security floor bypass. Fix PR [#71996](https://github.com/NousResearch/hermes-agent/pull/71996) is open.
- **Managed-runtime provisioning always fails ([#75655](https://github.com/NousResearch/hermes-agent/issues/75655))** — The `uv sync` command passes both `--locked` and `--no-config`, which are mutually exclusive. This means self-healing cannot recover; a broken venv becomes permanent. Reported today.
- **Compression tip projection hides sessions in WebUI ([#75625](https://github.com/NousResearch/hermes-agent/issues/75625))** — Session list disappears after cross-source compression chains. State-integrity issue.
- **Anthropic 429 then OAuth 400 retry cascade ([#75641](https://github.com/NousResearch/hermes-agent/issues/75641))** — Provider auth fallback is broken.

**Medium Severity (P2/P3) and UX:**

- **Desktop sidebar jitter ([#73629](https://github.com/NousResearch/hermes-agent/issues/73629))** — Win11 specific. PR fix available ([#75714](https://github.com/NousResearch/hermes-agent/pull/75714)).
- **macOS Tauri updater handoff failure ([#75278](https://github.com/NousResearch/hermes-agent/issues/75278))** — `HERMES_UPDATE_HANDOFF_PID` mismatch makes `--update` always fail.
- **TUI clipboard probe storm ([#75150](https://github.com/NousResearch/hermes-agent/issues/75150))** — Regression of #23984; now causing "infinite image auto-attach storm" on macOS.
- **`/status` shows wrong provider ([#75535](https://github.com/NousResearch/hermes-agent/issues/75535))** — Misleading billing/usage data.
- **Remote profile blocks sidebar for 45s ([#75712](https://github.com/NousResearch/hermes-agent/issues/75712))** — Timeout issue, no failure indication.

---

## 6. Feature Requests & Roadmap Signals

The community is pushing for features that make Hermes a more robust multi-agent and multi-platform hub:

- **Multi-Agent Telegram Groups ([#75711](https://github.com/NousResearch/hermes-agent/issues/75711))** — Requests to run "a fleet" of Hermes agents on NVIDIA edge hardware (DGX Spark, Jetson Thor) all in one Telegram group. This points to a strategic direction: orchestration and co-existence of multiple agent instances.
- **Lifecycle Event Catalog ([#64231](https://github.com/NousResearch/hermes-agent/issues/64231))** — Not a user feature but a maintainer necessity that will likely land in the next major. It is a prerequisite for a healthy plugin ecosystem.
- **`/refresh` Command ([#74622](https://github.com/NousResearch/hermes-agent/issues/74622))** — Reload system prompt without losing context. A UX request born out of prefix-cache warmth vs. developer iteration. Given the low complexity, this could land soon.
- **Browser Tab Management ([#71375](https://github.com/NousResearch/hermes-agent/issues/71375))** — List/switch/close browser tabs. Tool expansion.
- **LLM Execution Middleware Intentional Blocking ([#64662](https://github.com/NousResearch/hermes-agent/issues/64662))** — This is a subtle plugin-API request to allow middleware to abort execution intentionally, distinguishing from errors.

---

## 7. User Feedback Summary

**Big wins (positive signals):**
- Users are testing and reporting specific regressions with high fidelity (e.g., specific error logs for the managed-runtime provisioning bug), indicating a technically proficient and engaged user base.
- The ecosystem is expanding to ambitious hardware (DGX Spark) via Telegram fleet groups.

**Recurring pain points:**
- **Update/install loop regressions:** Both macOS (Tauri updater) and Windows (PowerShell wrapper fix) have broken update paths. The community is submitting thorough roots-cause analyses (e.g., [#75278](https://github.com/NousResearch/hermes-agent/issues/75278)).
- **Safety/cost boundaries:** Users are concerned about the YOLO mode and token incineration. The "Token Incinerator" title and "recursive meltdown" language in [#52484](https://github.com/NousResearch/hermes-agent/issues/52484) suggests frustration with runaway resource usage.
- **Config/state confusion:** The multiplexed-profile Docker sandbox issue ([#69575](https://github.com/NousResearch/hermes-agent/issues/69575), closed) and the persistent session-state bugs indicate that the profile system is still the most confusing area for advanced users.

---

## 8. Backlog Watch

These items have been open for over a month and are either silent or require maintainer decision:

- **[#27941 — codex_app_server Kanban workers cannot write artifacts (since May 18)](https://github.com/NousResearch/hermes-agent/issues/27941)** — 4 comments, still open. This indicates a long-standing plugin incompatibility that may need a dedicated maintainer.
- **[#23982 — Dashboard daily chart uses UTC instead of local timezone (since May 11)](https://github.com/NousResearch/hermes-agent/issues/23982)** — A simple-feeling fix that has been ignored for nearly 3 months. The community is likely frustrated by this.
- **[#46371 — Unlabeled YOLO bolt toggle in Desktop (since June 15)](https://github.com/NousResearch/hermes-agent/issues/46371)** — A UX safety issue with 3 comments. It has not been picked up by maintainers.
- **[#63306 — Skill-install trust derived from attacker-controlled identifier (since July 12)](https://github.com/NousResearch/hermes-agent/issues/63306)** — Security hardening report with no maintainer response.

---

**Project Health Assessment:** The project is in a healthy but "firefighting" state. Velocity is high, and the community is heavily invested. The v0.19.1 rollup has surfaced several configuration and update-path regressions that the team will need to prioritize against the deep architectural issues (recursion, security boundaries) that the community is flagging. The main backlog risk is low-priority UX and plugin-ecosystem issues left unaddressed for months, which can erode developer trust over time.

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw Project Digest — 2026-08-01

## 1. Today's Overview
PicoClaw shows **moderate activity** over the past 24 hours with 2 issues and 3 pull requests updated, though no new releases were published and no PRs were merged or closed. The project appears to be in a **consolidation phase** — the open PRs have been in review for 1–5 weeks, suggesting maintainers may be carefully evaluating substantial feature additions (Simplex channel, DeltaChat refactor, model fallback chains) rather than rushing integrations. Issue flow remains light, with one feature request and one bug report both pending attention for roughly a week. Overall, the project is **healthy but in a deliberate review cycle**, with no signs of regression churn or urgent stability concerns.

## 2. Releases
No new releases were published in the last 24 hours. The most recent user-facing version remains **0.3.1** (as referenced in Issue #3292). No release notes, migration guides, or breaking changes are available for this period.

## 3. Project Progress
No PRs were merged or closed in the last 24 hours. However, the following PRs remain open and actively being iterated on:

- **[#3222 — refactor(deltachat): cleanup implementation, documentation -200LOC](https://github.com/sipeed/picoclaw/pull/3222)** (open, by trufae) — significant cleanup: drops legacy features, removes hardcoded relay lists, eliminates password-based email configuration, and renames `invite_link` → `join_invite_link` while adding `show_invite_link`. This suggests the DeltaChat integration is being hardened for production use.
- **[#3193 — Added simplex channel type](https://github.com/sipeed/picoclaw/pull/3193)** (open, by dim) — adds a new channel type for the Simplex messaging protocol, expanding PicoClaw's multi-protocol reach.
- **[#3200 — feat(models): add configurable default fallback chain](https://github.com/sipeed/picoclaw/pull/3200)** (open, by lc6464) — introduces a dedicated workflow on the models page for setting default models, adding fallbacks, reordering, and persisting via the backend API.

## 4. Community Hot Topics
The most engaging discussions this week center on **long-message handling for IRC** and **performance concerns in the web interface**:

- **[Issue #3287 — Better support long messages in IRC](https://github.com/sipeed/picoclaw/issues/3287)** (2 comments): The community is asking PicoClaw to reassemble IRCv3 message fragments (split at the 512-byte limit) back into a single cohesive message. This is a genuine protocol-comprehension gap — users want PicoClaw to treat split messages semantically as one unit, not as separate chat turns. Underlying need: **fidelity of conversation context** in constrained protocols.
- **[Issue #3292 — CPU usage too high when focus on input box in chat interface](https://github.com/sipeed/picoclaw/issues/3292)** (1 comment): A user on Firefox (Debian/linux x64) with PicoClaw 0.3.1 and deepseek-v4-flash reports high CPU usage when focusing on the input box. The bilingual report (English/Chinese) indicates growing international adoption. Underlying need: **smooth, resource-efficient web UI** for daily chat use.

## 5. Bugs & Stability
One bug was active in the last 24 hours, ranked by severity:

1. **Medium — CPU spike in chat input (Issue #3292)** — High CPU usage when the input box is focused, on Firefox/Linux. Not a crash or data-loss bug, but a real usability and resource-efficiency concern for desktop users. No fix PR exists yet; maintainer attention may be needed to diagnose whether this is a rendering loop, excessive reactive updates, or a frontend framework issue.

No crashes, regressions, or data-integrity issues were reported in this period.

## 6. Feature Requests & Roadmap Signals
Two clear signals emerge for the near-term roadmap:

- **[IRC long-message reassembly (#3287)](https://github.com/sipeed/picoclaw/issues/3287)** — This is a well-specified, protocol-level feature that improves conversation coherence. Given that PicoClaw positions itself as a multi-channel AI agent, **this is a strong candidate for a next minor release** (0.3.x or 0.4.0), as it touches core message-handling logic.
- **[Configurable model fallback chain (#3200)](https://github.com/sipeed/picoclaw/pull/3200)** — Already in PR form and open for a month; if merged, this delivers resilience against model outages and user-controlled model routing, a highly requested capability in agent tools. **Likely for the next release if review completes.**

Additional signals: the open Simplex channel PR (#3193) and the DeltaChat overhaul (#3222) indicate the roadmap includes **protocol breadth** (Simplex) and **maintainability/security hardening** (DeltaChat secret management), likely targeting a 0.4.x milestone.

## 7. User Feedback Summary
- **Positive signals**: The DeltaChat refactor (dropping legacy features, enforcing JSON-RPC-only secrets) suggests the maintainers are addressing security and maintainability proactively — community feedback on simplifying configuration likely drove this. The model fallback chain feature directly responds to user need for **reliable model availability** in production.
- **Pain points**: (1) IRC users want PicoClaw to preserve message boundaries correctly; the current split behavior breaks conversational context. (2) Web UI performance on input focus is a real friction point for daily use, especially on Linux/Firefox. (3) The bilingual issue (#3292) indicates a growing non-English user base, which may warrant future i18n considerations.
- **Overall sentiment**: Constructive and feature-driven. No frustrated or blocked users; the community is actively submitting well-structured feature requests and fixes, indicating healthy engagement.

## 8. Backlog Watch
The following items have been open for extended periods and may need maintainer attention:

- **[PR #3193 — Simplex channel type](https://github.com/sipeed/picoclaw/pull/3193)** — Open since June 27 (~5 weeks), no comments. For a clean new-feature PR, this deserves a maintainer review or at least a status update to avoid silent rot.
- **[PR #3222 — DeltaChat refactor](https://github.com/sipeed/picoclaw/pull/3222)** — Open since July 3, no explicit comments. This is a large refactor (-200 LOC) touching security-sensitive code (secret handling); it should be prioritized for review to prevent conflicts with other channel work.
- **[PR #3200 — Model fallback chain](https://github.com/sipeed/picoclaw/pull/3200)** — Open since July 1. No maintainer comments; the feature is user-visible and would likely reduce support issues around model outages. Consider fast-tracking.

Additionally, a **stale-process check** of issues #3287 and #3292 would help set expectations — both have been idle for ~1 week after initial discussion.

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw Project Digest — 2026-08-01

## Today's Overview

NanoClaw is in a period of sustained, moderate activity driven primarily by the core team and a small cluster of recurring external contributors. In the last 24 hours, the project saw 8 issues updated (all still open) and 9 PRs updated, of which 3 were merged or closed. The primary themes are infrastructure flexibility (Kubernetes, Apple Container, non-Docker execution), channel expansion (iMessage, Dial, hosted services), and security hardening (log redaction, origin validation). While no new releases shipped today, the project maintains a steady cadence of feature work and fixes across its ~3160 issues and a mature contribution culture. A notable bottleneck is the slow progress on long-standing infrastructure requests like native host execution and Kubernetes support, which remain popular but unresolved for months, while maintainers focus on merging channel integrations and security patches.

## Releases

**No new releases** were published in the last 24 hours. The most recent release path (v2.1.54) is being restored via PR #3163, which was a closed fix PR, indicating the maintainers are actively clearing a release-blocking issue.

## Project Progress

Three PRs were merged or closed today, representing a mix of cleanups and feature completions:

- **[PR #3163 (Closed) — "fix(release): restore the v2.1.54 release path"** — a core-team fix to repair the release pipeline, unblocking future version bumps.
- **[PR #3076 (Closed) — "feat(imessage): unified local+hosted adapter targeting spectrum-ts v11"** — a feature skill merging local and hosted iMessage support, actively superseded by the newer PR #3164, suggesting iterative development on this channel.
- **[PR #1678 (Closed) — "docs(skills): update voice transcription skills for Telegram + Linux"** — a documentation update expanding `use-local-whisper` support beyond WhatsApp to Telegram and Linux, closing a three-month-old PR.

These closures indicate progress on channel integrations and docs, but no major new runtime features were merged today. The core-team focus appears to be on stabilizing the release pipeline and consolidating iMessage work.

## Community Hot Topics

The most active discussions are clustered around infrastructure limitations and security:

- **[Issue #1184 (3 comments, 1 👍) — "Challenges deploying nanoclaw in restricted K8s environments (Sealos)"** — The community's long-standing desire for Kubernetes support persists. Users want to run NanoClaw on managed clusters without Docker, but face networking and container-runtime barriers.
- **[Issue #1732 (3 comments, 0 👍) — "feat: native runner mode — bypass Docker for host-tool access"** — Another recurring ask: direct host integration (tmux, headed browsers, macOS APIs) without Docker. This reveals a fundamental tension between NanoClaw's security isolation and power-user needs, with no maintainer response visible yet.
- **[Issue #2588 (1 comment, 0 👍) — "skill/apple-container branch is substantially out of sync with mainline"** — The Apple Container (macOS microVM) story is actively broken for users: the documented `convert-to-apple-container` skill fails immediately due to divergence from `main`. This is a high-signal pain point that links to the in-flight PR #2809 attempting to fix it.

**Underlying need:** A significant segment of the community wants to run NanoClaw outside the default Docker model — either on K8s, natively on the host, or in Apple's lightweight Container runtime. The project's strict container-first security model is both a feature and a blocker, and the slow pace of resolution is generating user frustration.

## Bugs & Stability

Two bugs were reported or remain active today, with one clearly more urgent:

- **[Issue #3162 (High Priority, New today) — "Telegram pairing is silently broken for the whole process lifetime if the boot-time getMe fails"** — A resilient-path failure: one failed HTTP call at boot permanently locks out pairing, with no user-facing error. This is a stability and UX regression affecting the Telegram channel, a core communication pathway. No fix PR is linked yet.
- **[Issue #2923 (Security) — "ask_user_question card can be defaced by a forged click before origin authz"** — A display-integrity spoof where a forged click can alter card text even when the origin check correctly rejects the response. This is not a data-leak risk but a trust/integrity issue. A fix PR ( [#2651](https://github.com/nanocoai/nanoclaw/pull/2651) ) is open and aims to validate the response origin, though it has been open for over a month.

**Severity ranking:** (1) Telegram pairing lockout [#3162] — high impact, new. (2) Card defacement [#2923] — medium severity, fix in review. (3) Apple Container networking [#2589] — medium, blocks a supported runtime.

## Feature Requests & Roadmap Signals

The roadmap is clearly pointing toward a **multi-runtime, multi-channel future**:

- **Kubernetes runtime (Issue #2354)** — Spawning agents as K8s pods instead of Docker is an open feature request with community support. Given the related discussion in #1184, this is a persistent ask. *Prediction: likely targeted for a v3.0 timeframe, but no maintainer commitment visible yet.*
- **Native runner mode (Issue #1732)** — Direct host-tool access (tmux, macOS APIs) is a marked divergence from the container-first model. *Prediction: unlikely to be accepted as-is due to security implications; a middle-ground (like Apple Container) is more probable.*
- **Apple Container runtime + remote OneCLI gateway (PR #2809)** — An in-flight PR adding an env-gated `CONTAINER_RUNTIME=container` mode with remote gateway support. *Prediction: this is the most likely next major feature to land, as it has an active PR and addresses multiple open issues (#2588, #2589).*
- **Channel expansion** — Two new channel PRs are active: **Dial (SMS + AI voice) in PR #3041** and **Hosted iMessage (Photon) in PR #3164**. The iMessage work is iterating quickly (superseding #2999 and #3076), suggesting it is close to merge readiness.
- **Secrets redaction (PR #3161)** — A new fix to redact credentials from host logs, a welcomed security hardening step.

**Next version guess:** v2.1.54 (once the release path is restored) will likely include the security fixes (log redaction, origin validation) and possibly the iMessage adapter, while Apple Container support may land shortly after.

## User Feedback Summary

- **Positive sentiment:** Users explicitly appreciate NanoClaw's minimalist, lightweight approach versus "bloated agent frameworks" (Issue #1184), and the skill-based contribution model is thriving, with multiple community contributors (glifocat, invisicat, OmriBenShoham) submitting high-quality PRs.
- **Pain points:** Docker dependency is the #1 recurring friction. Both Windows and Linux users without Docker are blocked (Issue #1225), and even Docker users face K8s restrictions (Issue #1184) or seek host-level tool access (Issue #1732). The Apple Container fallback is currently broken, worsening this gap.
- **Satisfaction:** Medium. Contributors are engaged and responsive, but several popular feature requests remain unanswered for weeks to months, which risks alienating the power-user community that drives feature ideas.

## Backlog Watch

Two items remain prominently unanswered and are growing stale:

- **[Issue #1225 (since 2026-03-18) — "Run it without docker"** — A fundamental question from a non-Docker user with only 2 comments. This low-priority question has gone 4.5 months without a substantive maintainer answer, which is a poor sign for onboarding non-Docker users.
- **[Issue #1732 (since 2026-04-10) — "feat: native runner mode"** — A detailed feature proposal with a clear use-case backlog (tmux, headed browsers, macOS APIs), but no maintainer acknowledgment. As the community's most ambitious infrastructure ask, it deserves a formal "won't fix" or roadmap allocation.
- **[Issue #2588 (since 2026-05-22) — "Apple Container branch out of sync"** — An actively broken skill for a supported runtime. While PR #2809 aims to fix it, the issue itself has only 1 comment and no triage label, leaving users in the dark.

---

**Project Health Summary:** NanoClaw is functionally healthy — releases, active channels, and a growing contributor base — but strategically at a crossroads on infrastructure. The core team is responsive on security and channel work, yet the long tail of "run it anywhere" requests (#Docker, #K8s, #native) risks fragmenting the community if not addressed with clear direction. The immediate priorities are restoring the release path (PR #3163) and landing the Apple Container runtime (PR #2809), which would unblock a significant portion of the current friction.

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

# NullClaw Project Digest — 2026-08-01

## 1. Today's Overview

NullClaw is in a **low-activity maintenance phase** as of August 1, 2026, with no new releases, no issue updates, and zero open/closed issue activity in the last 24 hours. The project’s only movement is a single open PR (#981) introducing a `grok-cli` provider, which was last updated two days ago but shows no recent commits or comments. While the repository remains functional and stable (no bug reports or regression chatter), the absence of maintainer responses and merged work suggests a **slowed development cadence** that could benefit from renewed attention. The active PR signals continued interest in expanding provider support, but overall community engagement metrics are minimal this week.

## 2. Releases

**None.** No new releases were published in the last 24 hours (or in the preceding period tracked for this digest). There are no changelog entries, breaking changes, or migration notes to report.

## 3. Project Progress

**No PRs were merged or closed in the last 24 hours.** The sole PR in motion remains open:

- **[#981 [OPEN] feat(provider): add grok-cli provider for xAI Grok CLI](https://github.com/nullclaw/nullclaw/pull/981)** — Authored by `valonmulolli` (created 2026-07-29, updated 2026-07-31). This PR extends NullClaw’s provider architecture by adding a **CLI-based provider** that spawns the local `grok` CLI per request, following the established pattern from `codex-cli`, `gemini-cli`, and `claude-cli`. It is designed as an **optional provider** requiring local installation and authentication of the `grok` CLI.

While not merged, this PR represents the only feature advancement in flight and demonstrates continued architectural consistency in how external CLI tools are integrated.

## 4. Community Hot Topics

With zero comments and zero reactions across all tracked items, there are **no active community discussions** to surface this week. The single open PR (#981) has no comment thread, indicating it is either waiting for maintainer review or lacks community visibility. The underlying need expressed by this PR is clear: **users want parity with a growing ecosystem of AI CLIs** — after support for Codex, Gemini, and Claude CLIs, xAI’s Grok is the natural next addition. The lack of dialogue around it may suggest the community is small, patient, or awaiting a maintainer’s green light to begin discussion.

## 5. Bugs & Stability

**No bugs, crashes, or regressions were reported in the last 24 hours.** The issue tracker is empty (0 total items), indicating that the current codebase is either stable in the eyes of its users or that usage is too low to surface problems. No severity-ranked items can be listed this period, and no fix PRs are pending for stability concerns.

## 6. Feature Requests & Roadmap Signals

The only feature signal in the current window is **PR #981**, which proposes a `grok-cli` provider. If merged, this would complete NullClaw’s coverage of major AI CLI tools (OpenAI, Anthropic, Google, xAI). 

Looking ahead, it is **moderately likely** this PR will be merged into the next minor version (e.g., v0.x.y), given it follows a well-trodden implementation pattern and requires no core refactoring. Beyond this, there are no new feature requests or roadmap signals in the data — suggesting the maintainers may be focusing on stability or internal work not visible in public channels.

## 7. User Feedback Summary

No explicit user feedback (comments, reactions, issue reports, or PR reviews) was recorded in the last 24 hours. The implicit signal from the community is **demand for broader provider integration**, as evidenced by the existence of PR #981. There is no data to assess satisfaction or dissatisfaction directly, but the absence of complaints suggests no acute pain points are being voiced. The project appears to serve a niche audience that values **modularity and optionality** in provider selection.

## 8. Backlog Watch

**No long-unanswered items are currently visible** — the issue tracker is empty, and the sole PR (#981) is only 3 days old, which is well within a normal review window. However, given the **zero-activity pattern over the past day**, maintainers should be mindful of PR #981 drifting into "stale" territory. If no review comment appears within the next week, the PR would become a candidate for a gentle nudge to keep contributor momentum alive. No other items require maintainer attention this period.

---

*Data source: [github.com/nullclaw/nullclaw](https://github.com/nullclaw/nullclaw) — snapshot taken 2026-08-01.*

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw Project Digest — 2026-08-01

## 1. Today's Overview

IronClaw is in a period of intense architectural refactoring and stabilization. The project saw **29 issues updated** (22 open, 7 closed) and **50 PRs updated** (18 open, 32 merged/closed) in the last 24 hours — a high-velocity day driven primarily by the "Reborn" target-architecture workstream. The dominant theme is the **systematic extraction of neutral contract crates** (`ironclaw_loop_contracts`, `ironclaw_extension_contracts`, `ironclaw_product_contracts`) from monolithic modules, with a stacked PR chain (WS1.1→WS1.4) advancing steadily. Concurrently, **security and privacy bugs** are surfacing at an elevated rate (cross-user memory leaks, shared home directories, catalog metadata exposure), suggesting the refactoring is exposing latent multi-tenant isolation gaps. **No releases** were published today. The project is healthy but under significant load: a macro-epic (#6284) on error-recoverability sets an ambitious "100% recovery" goal, while CI infrastructure is being reworked to keep pace.

---

## 2. Releases

**No new releases published today.** The last release PR (#5598, opened 2026-07-03) remains open, previewing a future release with breaking changes in `ironclaw_common` (0.4.2→0.5.0, new `Copy` impl added) and `ironclaw_skills` (0.3.0→0.4.0).

---

## 3. Project Progress

The "Reborn" target-architecture refactoring dominated today's merged work. Key closed PRs:

| PR | Description | Significance |
|----|-------------|--------------|
| [#6967](https://nearai/ironclaw PR #6967) | **WS1.1**: Complete turn vocabulary in `host_api`, retire turns shims | Foundation for contract extraction; notes 6 pre-existing CI blockers |
| [#6975](https://nearai/ironclaw PR #6975) | **WS1.2**: Extract `ironclaw_loop_contracts`, flip `agent_loop` onto it | First dedicated contract crate; includes enforcement + CI registration |
| [#6979](https://nearai/ironclaw PR #6979) | Docs reconciliation with hosted-MCP registration (#6930) | Five markdown files, +27/−11; keeps docs in sync with 153-file merge |
| [#6930](https://nearai/ironclaw PR #6930) | **feat(extensions):** Register hosted MCP servers (+15,002/−1,818) | Large feature: tenant-runtime MCP registration, auto auth detection, full lifecycle integration |
| [#6932](https://nearai/ironclaw PR #6932) | Dependabot: 34 dependency updates | Routine maintenance |
| [#4022](https://nearai/ironclaw PR #4022) | Fix: HTTP response errors recoverable, not run-aborting | **Important regression fix** from May — restores model-visible recovery for tool HTTP errors |
| [#3952](https://nearai/ironclaw PR #3952) | TOCTOU-harden LocalFilesystem (openat2/O_NOFOLLOW) | High-leverage security hardening for multi-tenant FS isolation |

**Still open and advancing:** WS1.3 ([#6977](https://nearai/ironclaw PR #6977)) and WS1.4 ([#6980](https://nearai/ironclaw PR #6980)) continue the contract-crate extraction chain. The "model chooses skills" fix ([#6938](https://nearai/ironclaw PR #6938)) and skills-selectability overhaul ([#6745](https://nearai/ironclaw PR #6745)) target epic #6941.

---

## 4. Community Hot Topics

Most-commented items reveal two concentrated debate zones:

**1. Error-Recoverability Macro-Epic — [#6284](https://nearai/ironclaw Issue #6284)** (15 comments)
- **Underlying need:** A hard contract that every mid-run error is survivable, model-visible, actionable, and carries cause + fix hints. This is the project's north-star quality goal ("100% recovery") but is enormous in scope. It has spawned sub-epics, suggesting the team is decomposing it pragmatically.

**2. Path-Keyed CI Gates — [#6963](https://nearai/ironclaw Issue #6963)** (5 comments)
- **Underlying need:** Eight discovered defects where CI gates resolve scope from the literal flat `crates/ironclaw_*` tree shape, breaking after the product-crate merge. Filed as a tracking issue because "a checklist row is weak tracking." Community pressure is for durable, path-independent CI.

**3. Hosted-MCP Catalog Exposure — [#6778](https://nearai/ironclaw Issue #6778)** (1 comment)
- **Underlying need:** Cross-user metadata exposure on multi-principal servers — discovered tool catalogs are published per extension *id*, not per *installation*. This is a privacy-relevant design flaw in the new MCP registration path.

**Notable PR activity:** The stacked WS1.x contract-extraction chain (4 PRs in sequence) is drawing attention as the team's flagship refactoring effort, but comments are tracked separately per PR.

---

## 5. Bugs & Stability

Ranked by severity:

| Severity | Issue | Description | Fix PR? |
|----------|-------|-------------|---------|
| **P0** | [#6900](https://nearai/ironclaw Issue #6900) | **Cross-user memory leak**: Shared-channel default subject collapses all users into operator's memory namespace | No |
| **P0** | [#6897](https://nearai/ironclaw Issue #6897) (closed) | Model gateway retries deterministic LLM errors as "Unavailable" for ~7 minutes — terminal errors should fail fast | Fixed via retry-classification rework |
| **P1** | [#6976](https://nearai/ironclaw Issue #6976) | Linux service install doesn't enable user lingering → unreliable unattended operation (headless servers) | No |
| **P1** | [#6972](https://nearai/ironclaw Issue #6972) | New-account email authentication not working | No |
| **P2** | [#6940](https://nearai/ironclaw Issue #6940) | IronHub skill CTA returns 404 across all skills | No |
| **P2** | [#6866](https://nearai/ironclaw Issue #6866) | Same home directory shared across all users; workspaces visible to others (privacy) | No |
| **P2** | [#6947](https://nearai/ironclaw Issue #6947) | `classify-test-scope.sh` mis-buckets `ironclaw_product` as legacy-only (glob predates merge) | No |
| **CI** | [#6978](https://nearai/ironclaw Issue #6978) | `workflow_dispatch` runs structurally fail the Tests (Reborn) roll-up — CI red despite clean run | No |
| **Perf** | [#6974](https://nearai/ironclaw Issue #6974) | libSQL `thread_store_writes` pathology: tool-heavy stress p95 at 37–135s (target 2.5s) post-#6696 | [#6973](https://nearai/ironclaw PR #6973) (open) |
| **Perf** | [#6973](https://nearai/ironclaw PR #6973) (open) | Postgres API capacity regressed: p95 3.74s→12.0s, `send_message` 275ms→4.78s | This PR itself |

**Notable:** The performance regressions (#6973/#6974) are directly attributed to the #6696 row-native process journal change, and the fix is already in flight. The `#6978` CI structural failure means even clean runs report red — a morale and trust issue.

---

## 6. Feature Requests & Roadmap Signals

User-driven requests today:

1. **[#6939](https://nearai/ironclaw Issue #6939) — Migration tool from legacy agents**: Users of Hermes/Openclaw face high switching costs; no way to port setup/configuration/memory. *Strong adoption barrier — likely a high-value near-term feature.*
2. **[#6971](https://nearai/ironclaw Issue #6971) — Clarify "Tools" vs "Extensions" terminology**: Product naming confusion. *Quick win — a terminology decision, not code.*
3. **[#6939-related] Migration from legacy**: Pairs with the "Reborn" branding cleanup ([#6854](https://nearai/ironclaw Issue #6854)) — the team is actively renaming "Reborn" → "Ironclaw 1.0" in external docs.

**Roadmap signals from internal epics:**
- **Admin-Managed Agents ([#6578](https://nearai/ironclaw Issue #6578), #6578)** — non-human identity subjects for automation/integrations.
- **Hermetic capability testing ([#6524](https://nearai/ironclaw Issue #6524))** — deterministic coverage proof for all capabilities/journeys.
- **New `/new`, `/stop`, `/interrupt` commands ([#6969](https://nearai/ironclaw PR #6969), open)** — registry-backed task lifecycle across all channels.

**Predicted next-version features:** The three stacked contract-extraction PRs (WS1.3, WS1.4) will land soon; the messaging framework PR ([#6831](https://nearai/ironclaw PR #6831)) with 16 canonical operations is large and likely close. The migration tool request is a candidate for community-driven adoption growth.

---

## 7. User Feedback Summary

Real user pain points reported this week:

- **Adoption friction**: "Several users would resist starting over with a clean slate" for legacy agent migration (from [#6939](https://nearai/ironclaw Issue #6939)).
- **Broken onboarding**: New-account email auth failure blocks first-run experience ([#6972](https://nearai/ironclaw Issue #6972)); IronHub skill CTA 404s ([#6940](https://nearai/ironclaw Issue #6940)).
- **Privacy violations**: Shared home directory across users — "Which is a privacy concern" ([#6866](https://nearai/ironclaw Issue #6866)); cross-user memory namespace collapse ([#6900](https://nearai/ironclaw Issue #6900)).
- **Branding inconsistency**: "Reborn" appears in external-facing extension descriptions; users expect "Ironclaw 1.0" ([#6854](https://nearai/ironclaw Issue #6854)).
- **Deployment reliability**: Unattended installs fail without user lingering — a blocker for headless/VM setups ([#6976](https://nearai/ironclaw Issue #6976)).

**Satisfaction signals:** The "model chooses the skill" philosophy change ([#6938](https://nearai/ironclaw PR #6938)) aligns with user expectations that the agent should be in control — a positive architectural direction. The fast PR turnaround on the Postgres regression suggests a responsive team.

---

## 8. Backlog Watch

Items needing maintainer attention:

1. **[#5598](https://nearai/ironclaw PR #5598) — Release PR open since 2026-07-03** (30 days). The release train appears stalled; `ironclaw_common` and `ironclaw_skills` breaking changes are waiting. This blocks downstream consumers.
2. **[#6284](https://nearai/ironclaw Issue #6284) — Error-recoverability epic** (15 comments, updated daily). The largest strategic item; while active, it's unclear if it has an owner or a breakdown plan beyond sub-epics.
3. **[#6780](https://nearai/ironclaw PR #6780) — IronHub deep-link register/install gateway** (open since 07-28, no comments). Substantial feature (re-port of #5409) with zero review engagement — a stall risk.
4. **[#6945](https://nearai/ironclaw Issue #6945) — Hook-isolation semantic has no regression test** — documentation cited tests that never existed; the gap is now tracked but unassigned.
5. **Open security issues without PRs**: #6900 (P0 memory leak), #6778 (MCP metadata exposure), #6866 (shared home) — all have clear repro paths but no fix in flight. These are multi-tenant isolation fundamentals that should be prioritized before scale.

**Health assessment:** The project is executing a disciplined architecture migration while backfilling regressions it caused. The main risks are (a) security isolation issues piling up without assigned fixes, and (b) a 30-day-old release with breaking changes still unshipped. CI is currently noisy (structural failures reported as red even on clean runs), which will erode confidence if not fixed promptly. Overall: industrious, transparent, but stretched thin.

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

# LobsterAI Project Digest — 2026-08-01

## 1. Today's Overview

LobsterAI shows steady maintenance momentum with 12 PRs updated in the last 24 hours, of which 11 were merged or closed and 1 remains open. The project closed 4 stale issues, primarily feature requests from April that were addressed over the intervening months. Today's merged work focuses heavily on the OpenClaw subsystem (prompt-cache stability, tool-protocol hygiene, cron yield handling) alongside UI polish items (copy feedback, settings overlay dismissal). One potentially impactful open PR (#2234) addresses core orchestration logic around cron-based multi-agent finalization and is approaching one month of inactivity. Overall, the project displays a healthy mix of bug-fixing, performance engineering, and UX refinement, though the presence of stale-labelled items suggests some backlog aging. No new releases shipped today.

## 2. Releases

No new releases published in the last 24 hours.

## 3. Project Progress

**OpenClaw / Core Agent Engine (3 merged PRs):**
- **[#2413](https://github.com/netease-youdao/LobsterAI/pull/2413)** — `fix(openclaw): keep live prompt tool-result history byte-stable across turns` — Prevents re-applying a fixed 4x aggregate character cap on every request, which previously rewrote already-cached history and collapsed DeepSeek prefix-cache hit rates. This is a significant performance/context-caching fix.
- **[#2415](https://github.com/netease-youdao/LobsterAI/pull/2415)** — `fix(openclaw): drop aggregate cap in live tool-result prompt projection` — Companion fix to #2413; passes `aggregateMaxCharsOverride=null` so unchanged history stays byte-stable. Reported to recover DeepSeek long-session hit rates from ~57% back to ~100%.
- **[#2414](https://github.com/netease-youdao/LobsterAI/pull/2414)** — `fix(cowork): prevent BTW tool protocol leakage` — Sanitizes provider tool-call markup from side-chat results, returns stable guidance when a side question requires tools, and preserves error metadata through the OpenClaw gateway.

**UI / Renderer Improvements (2 merged PRs):**
- **[#2417](https://github.com/netease-youdao/LobsterAI/pull/2417)** — `fix(sites): add copy success feedback` — Reuses the conversation copy icon and interaction for site URLs and share codes, improving affordance consistency.
- **[#1321](https://github.com/netease-youdao/LobsterAI/pull/1321)** — `fix(settings): dismiss overlays when switching settings tabs` — Fixes a bug where cowork memory editor or model connection-test modals remained as full-window overlay layers after navigating to another settings tab, making the UI appear read-only.

**Release Infrastructure:**
- **[#2416](https://github.com/netease-youdao/LobsterAI/pull/2416)** — `Release/2026.7.31` — Release branch merged (closed).

**Stale PRs Closed (likely merged earlier, now formally closed):**
- **[#172](https://github.com/netease-youdao/LobsterAI/pull/172)** — Antigravity OAuth integration and proxy compatibility (main process OAuth subsystem, SQLite persistence, OpenAI-compatible proxy support).
- **[#1308](https://github.com/netease-youdao/LobsterAI/pull/1308)** — Isolate home-screen input draft per agent.
- **[#1315](https://github.com/netease-youdao/LobsterAI/pull/1315)** — Draggable sidebar width (180–480px range, global mousemove/mouseup binding).
- **[#1318](https://github.com/netease-youdao/LobsterAI/pull/1318)** — Keyboard shortcut `<kbd>` badges for sidebar buttons (platform-aware: ⌘/⌥/⇧ on macOS, Ctrl/Alt/Shift elsewhere).
- **[#1320](https://github.com/netease-youdao/LobsterAI/pull/1320)** — Skeleton loading state for session list; added `sessionsLoaded` flag to `coworkSlice` to distinguish "loading" from "empty".

## 4. Community Hot Topics

The most-discussed items carried 2 comments each and were exclusively the April-era feature requests that have since been implemented:

- **[Issue #1311](https://github.com/netease-youdao/LobsterAI/issues/1311)** — Table content wrap showing raw tags; hover tooltip for truncated long text in tables.
- **[Issue #1314](https://github.com/netease-youdao/LobsterAI/issues/1314)** — Draggable sidebar width adjustment (implemented in PR #1315).
- **[Issue #1317](https://github.com/netease-youdao/LobsterAI/issues/1317)** — Keyboard shortcut hints in sidebar (implemented in PR #1318).
- **[Issue #1319](https://github.com/netease-youdao/LobsterAI/issues/1319)** — Skeleton loading for session list to prevent "empty state" flash (implemented in PR #1320).

**Analysis:** These issues cluster around UX discoverability and latency perception. Users want the UI to communicate more (shortcut hints, loading states, hover previews) and be more adaptable (adjustable sidebar). The pattern suggests strong interest in making the desktop client feel more polished and responsive on first launch and during interaction. All were authored by two recurring contributors (MaoQianTu authored three of the four), indicating a dedicated community member driving UI polish.

## 5. Bugs & Stability

| Severity | Issue / PR | Description | Status |
|----------|-----------|-------------|--------|
| **High** | [PR #2413](https://github.com/netease-youdao/LobsterAI/pull/2413) / [PR #2415](https://github.com/netease-youdao/LobsterAI/pull/2415) | Live prompt projection re-applied a 4x aggregate cap on every request, rewriting cached history and dropping DeepSeek long-session cache hit rates from ~100% to ~57% — a severe performance regression for long sessions | **Fixed** (merged today) |
| **Medium** | [Issue #1319](https://github.com/netease-youdao/LobsterAI/issues/1319) | Empty-state flash on startup: session list showed "暂无会话" before data loaded, misleading users into thinking history was lost | **Fixed** (PR #1320, stale-closed) |
| **Low** | [PR #2414](https://github.com/netease-youdao/LobsterAI/pull/2414) | BTW tool protocol leakage: provider tool-call markup leaked from side-chat results into the main conversation | **Fixed** (merged today) |
| **Low** | [PR #1321](https://github.com/netease-youdao/LobsterAI/pull/1321) | Settings tab switch left overlays mounted (`absolute inset-0`), causing UI to appear read-only after navigating | **Fixed** (stale-closed) |

No new critical regressions reported today. The DeepSeek cache-hit-rate issue was the most serious stability/performance item and has been resolved.

## 6. Feature Requests & Roadmap Signals

**Implemented (closed this cycle):**
- Draggable sidebar width ([#1314](https://github.com/netease-youdao/LobsterAI/issues/1314) → [#1315](https://github.com/netease-youdao/LobsterAI/pull/1315))
- Keyboard shortcut `<kbd>` badges ([#1317](https://github.com/netease-youdao/LobsterAI/issues/1317) → [#1318](https://github.com/netease-youdao/LobsterAI/pull/1318))
- Session-list skeleton loading ([#1319](https://github.com/netease-youdao/LobsterAI/issues/1319) → [#1320](https://github.com/netease-youdao/LobsterAI/pull/1320))
- Table content rendering: preserve raw tags on wrap, add hover full-text preview ([#1311](https://github.com/netease-youdao/LobsterAI/issues/1311))

**Predicted for next minor release (2026.8.x):**
- **Cron yield finalization** ([PR #2234](https://github.com/netease-youdao/LobsterAI/pull/2234)) — multi-round descendant-completion driving for parent agents in cron scenarios; if merged, it addresses a significant orchestration gap.
- **Antigravity OAuth** ([PR #172](https://github.com/netease-youdao/LobsterAI/pull/172)) — provider integration with profile persistence; likely to be stabilized further before official release notes.

## 7. User Feedback Summary

**Pain points expressed (direct or inferred):**

- **UX discoverability:** Users were unaware of existing keyboard shortcuts; the interface provided no visual hints ([#1317](https://github.com/netease-youdao/LobsterAI/issues/1317)).
- **Perceived data loss:** On startup, the empty-state text made users think their conversation history was gone before data finished loading ([#1319](https://github.com/netease-youdao/LobsterAI/issues/1319)).
- **Layout rigidity:** Fixed 240px sidebar width penalized both small-screen users (content squeezed) and large-screen users (long titles truncated) ([#1314](https://github.com/netease-youdao/LobsterAI/issues/1314)).
- **Table readability:** Raw HTML tags appearing in wrapped table cells and truncated long text without hover preview degraded information scanning ([#1311](https://github.com/netease-youdao/LobsterAI/issues/1311)).

**Satisfaction indicators:** All four feature requests were addressed through PRs with direct issue links (Closes #xxxx), demonstrating a responsive maintainers-to-community loop. The DeepSeek cache fix signals attention to power-user real-world workloads (long sessions, context persistence).

## 8. Backlog Watch

| Item | Type | Age | Why it matters |
|------|------|-----|----------------|
| **[PR #2234](https://github.com/netease-youdao/LobsterAI/pull/2234)** — `fix(openclaw): cron yield descendant finalization` (btc69m979y-dotcom) | Open PR | created 2026-06-30, stale-labelled | Fixes a core orchestration issue: after `sessions_yield`, child-agent completion events fail to drive the parent agent forward in cron scenarios. Includes test coverage for three scenarios (normal/cron-parallel/cron-serial). The `[area: docs]` label suggests it may be blocked on documentation updates. One month of dormancy on a correctness fix in the agent engine is a risk worth maintainer attention. |

**Also of note:** The "stale" label is being applied aggressively (all 24h-updated items carry it), which may indicate an automated staleness bot that could prematurely close genuinely valuable items. Maintainers may want to review threshold settings.

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

# Moltis Project Digest — 2026-08-01

## 1. Today's Overview

Moltis is in a phase of active security hardening and feature expansion. The project saw 2 issues updated (1 bug, 1 feature that was closed) and 8 pull requests updated, with 2 PRs merged/closed (Markdown export and Slack improvements). The immediate priority is clearly security: a contributor (`tsauvajon`) submitted two urgent fixes for path traversal vulnerabilities and signature verification gaps, suggesting external security review is surfacing issues. Concurrently, maintainers are advancing significant architectural features—Nostr NIP-29 group chat, a new vector database backend, and full instrumentation infrastructure—indicating healthy, broad development across channels, memory, and observability. Overall health appears solid, though the open security PRs should be prioritized for merge.

## 2. Releases

No new releases were published in the last 24 hours. The most recent changes are available on the `main` branch only.

## 3. Project Progress

Two pull requests were merged/closed in the last 24 hours:

- **[#1176 - feat(web): add Markdown copy and session export](https://github.com/moltis-org/moltis/pull/1176)** (closed/merged): Delivers the ability to copy assistant replies in original Markdown format and export the full session history as a Markdown file, including image references. This directly addresses the long-standing feature request in issue [#1131](https://github.com/moltis-org/moltis/issues/1131), which was also closed today.
- **[#1166 - feat(slack): per-message acknowledgment reactions, phases, reconnect supervision, and Block Kit](https://github.com/moltis-org/moltis/pull/1166)** (closed/merged): Implements and makes safe the acknowledgment reaction lifecycle for Slack bots under queueing, cancellation, retries, and delivery failures, adding phase tracking and Block Kit support. Builds on previously merged work in #1165.

## 4. Community Hot Topics

The most active items reflect a strong focus on trusting the system with sensitive data and expanding integration surface:

- **[PR #1174 - Instrumentation and feedback collection infrastructure](https://github.com/moltis-org/moltis/pull/1174)**: Adds Langfuse v4 export, OTLP backends, and end-user reaction feedback; treats "observability as a core platform capability" rather than a bolt-on.
- **[PR #1168 - NIP-29 group chat support for Buzz channels](https://github.com/moltis-org/moltis/pull/1168)**: Integrates Moltis with Block's open-source Nostr-based workspace Buzz, where AI agents and humans share team channels. This signals a push toward agent-human hybrid team workflows.
- **[PR #1170 - Privilege separation via per-account operators list](https://github.com/moltis-org/moltis/pull/1170)**: Addresses a real security concern: channel senders on the access allowlist could previously reach privileged commands/host tools; this PR enforces an explicit `operators` boundary across all execution paths.

The underlying need across these threads is enterprise/team readiness: secure multi-tenant operations, auditable agent behavior, and interoperability with existing collaboration platforms.

## 5. Bugs & Stability

One bug was reported in the last 24 hours:

- **[Issue #1181 - [Bug]: Issue with GPT 5.6 Luna](https://github.com/moltis-org/moltis/issues/1181)** — Severity: **High** (blocks use of a specific model family); 0 comments, no fix PR referenced yet. The report is recent and diagnostic context is pending.

Two security vulnerability classes were addressed via PRs, both considered **Critical** severity due to potential arbitrary code execution:

- **[PR #1180 - fix(security): harden model and zip paths](https://github.com/moltis-org/moltis/pull/1180)**: Fixes two bug classes leading to arbitrary file write outside the intended directory via malicious zip extraction or HuggingFace repo paths, which could overwrite user config/credentials/scripts and yield code execution.
- **[PR #1179 - fix(gateway): verify node pairing signatures](https://github.com/moltis-org/moltis/pull/1179)**: Binds `node.pair.verify` to the server-issued pending request, preventing callers from supplying their own key or challenge.

These PRs are **open and awaiting review/merge** — they should be treated as top priority for maintainers.

## 6. Feature Requests & Roadmap Signals

- **Markdown copy & session export** (originally requested in [#1131](https://github.com/moltis-org/moltis/issues/1131)) was implemented in PR #1176 and closed — **shipped**.
- **Vector database memory backend (Zvec + redb)**: PR [#1158](https://github.com/moltis-org/moltis/pull/1158) offers a lightweight alternative to existing memory backends, optional via the `zvec` cargo feature. Likely to be merged as opt-in.
- **Agent instrumentation & observability**: PR #1174 is broad and may land soon given the strong commit activity.
- **Nostr NIP-29 group chat**: PR #1168 — likely to land in the next minor version as Buzz integration is a notable ecosystem play.

**Predictions for next release:** The next release will likely wrap in the security fixes (#1179, #1180), Markdown export, Slack lifecycle improvements, and possibly the `zvec` memory backend.

## 7. User Feedback Summary

- **Pain point — privilege separation**: PR #1170 highlights that current access allowlists are insufficient to protect privileged commands and host tools. This is a trust and safety issue for users running Moltis on shared channels.
- **Pain point — security of model/path handling**: PR #1180 stems from genuine risk of remote code execution through malicious model repos or zip files. Users handling untrusted model data should apply these patches promptly.
- **Satisfaction signal**: Issue #1131 (Markdown export) received a 👍 and was picked up and closed within 6 weeks — a sign of responsive development to user requests.
- **Use case insight**: The Buzz/NIP-29 integration indicates real demand for AI agents as **first-class members of human team channels**, not just backend tools.

## 8. Backlog Watch

- **[Issue #1181 (GPT 5.6 Luna bug)](https://github.com/moltis-org/moltis/issues/1181)** — Open, 0 comments; could use triage from a maintainer to reproduce or request context.
- **[PR #1180 (zip/model path hardening)](https://github.com/moltis-org/moltis/pull/1180)** — High-impact security fix, waiting on review; should not sit in the backlog.
- **[PR #1179 (pairing signature verification)](https://github.com/moltis-org/moltis/pull/1179)** — Security fix for a trust gap in gateway pairing; should be reviewed alongside #1180.
- No long-unanswered issues were identified beyond the above; the project appears actively maintained with a responsive core team.

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

# CoPaw Project Digest
**Date:** 2026-08-01  
**Repository:** [agentscope-ai/CoPaw](https://github.com/agentscope-ai/CoPaw)

---

## 1. Today's Overview

CoPaw (QwenPaw) is in a period of **high-intensity bug-fixing and stabilization** following the 2.0.1 release. With **21 issues and 43 PRs updated in the last 24 hours**, the project demonstrates strong community engagement and active maintainer response. Notably, a **significant cohort of first-time contributors** (mohitdebian, Yigtwxx, and others) is submitting targeted fixes for critical bugs. The most pressing themes are **shell command execution reliability**, **memory/context compression integrity**, and **AgentScope 2.0 compatibility**, suggesting the team is working through migration-related regressions. While no new releases were published today, the volume of merged PRs (13) indicates substantial progress is being made on the stabilization front.

---

## 2. Releases

**No new releases** were published in the last 24 hours. The latest available version remains **QwenPaw 2.0.1** (Desktop). Several issues reference version **2.0.4.post1** of the `agentscope` dependency, and a compatibility issue (#6612) between QwenPaw 2.0.1 and agentscope 2.0.4.post1 was identified, indicating a pending patch release may be in the works.

---

## 3. Project Progress

Thirteen PRs were merged or closed in the last 24 hours. Key merged/closed PRs include:

| PR | Title | Summary |
|----|-------|---------|
| [#6573](https://github.com/agentscope-ai/QwenPaw/pull/6573) | fix(audio): restore transcription for channel audio messages | Fixes silent transcription failure for Feishu audio messages after AgentScope 2.0 migration. |
| [#6602](https://github.com/agentscope-ai/QwenPaw/pull/6602) | Fix/issue 6558 session integrity | Resolves multi-session UI data integrity issues including message loss on switch and instructions drift. Preserves across Coding/Chat mode switches. |
| [#6606](https://github.com/agentscope-ai/QwenPaw/pull/6606) | fix(read_file): accept numeric string line ranges | Fixes `read_file` tool to accept line range values provided as strings. |
| [#6604](https://github.com/agentscope-ai/QwenPaw/pull/6604) | docs(memory): explain ReMe self-evolving knowledge base | Documentation for ReMe memory lifecycle. |
| [#6592](https://github.com/agentscope-ai/QwenPaw/pull/6592) | fix(memory): flush Auto-Memory before Scroll context eviction | Fixes memory loss (issue #6555) where early-session events were dropped when context scrolled out. |

**Notable first-time contributor activity:** A cluster of PRs from **mohitdebian** addresses multiple critical issues simultaneously — agent.json corruption (#6528), shell command hangs (#6610), spawn_subagent schema (#6609), and AgentScope compatibility (#6615). This is a promising sign for the sustainability of the contributor pipeline.

---

## 4. Community Hot Topics

The most active discussions in the last 24 hours:

1. **[#6537 — Skill tags disappear on restart (regression of #3270)](https://github.com/agentscope-ai/QwenPaw/issues/6537)**
   - **10 comments**, authored by Ra-M497
   - Tags persist to disk but are lost during manifest reconciliation at startup. This is a regression that affects core configuration persistence.
   - **Signal:** High importance — configuration data loss on restart is a critical flaw that erodes user trust.

2. **[#6601 — 不报空响应错误 (Empty response errors not reported)](https://github.com/agentscope-ai/QwenPaw/issues/6601)**
   - **5 comments**, authored by rerbin
   - Long sessions approach the context window limit, and the model returns empty responses without QwenPaw reporting an error. The session loses all responsiveness.
   - **Signal:** Long-context session handling is a pain point, especially for models that silently hit context limits.

3. **[#6563 — CI 'Real behavior proof' workflow blocks all fork PRs](https://github.com/agentscope-ai/QwenPaw/issues/6563)**
   - **5 comments**, CLOSED, authored by BlackBox-Labs
   - CI workflow fails on all fork PRs with `Resource not accessible by integration`, blocking all external contributions.
   - **Signal:** Closed — good, but this directly impacts the sustainability of the open-source ecosystem. Its resolution is worth monitoring.

Also notable: **#6083** (workspace output quick access button) received 4 comments and 0 reactions, and **#6588** (spawn_subagent single-task unusable) received 4 comments, indicating these are areas users are actively engaging with.

---

## 5. Bugs & Stability

Eight new issues were reported in the last 24 hours. Ranked by severity:

**🔴 Critical — Session unresponsiveness due to shell command blocking:**
- [#6608](https://github.com/agentscope-ai/QwenPaw/issues/6608) — Long-running shell commands bypass `shell_command_timeout` and block Feishu session indefinitely. Orphan subprocess on cancel. No per-channel total timeout.
  - **Fix PR exists:** [#6610](https://github.com/agentscope-ai/QwenPaw/pull/6610) caps timeout against the configured max (default 600s).
- Also related: [#6589](https://github.com/agentscope-ai/QwenPaw/issues/6589) — `execute_shell_command` with massive output (>10k lines) freezes UI; single-threaded rendering blocks everything.

**🔴 Critical — Manifest corruption on Windows:**
- [#6520](https://github.com/agentscope-ai/QwenPaw/issues/6520) — `agent.json` suffers systemic, distributed corruption: BOM header, missing quotes, double-encoded Chinese text. Causes complete system failure. Update: no new manifestation, but fix PR [#6528](https://github.com/agentscope-ai/QwenPaw/pull/6528) is open.

**🟠 High — Silent failures:**
- [#6614](https://github.com/agentscope-ai/QwenPaw/issues/6614) — WeChat cron scheduled push silently fails — task reports `success` but messages never delivered (`ret=-2`, context_token invalid). User reports ~44M tokens burned on retries.
- [#6544](https://github.com/agentscope-ai/QwenPaw/issues/6544) — Feishu audio messages silently fail transcription in 2.x (CLOSED, fix PR merged).

**🟠 High — Compatibility breakage:**
- [#6612](https://github.com/agentscope-ai/QwenPaw/issues/6612) — QwenPaw 2.0.1 + agentscope 2.0.4.post1 → proactive crashes (Msg.content type) and tool-permission deadlock. This is a direct dependency breakage.
  - **Fix PR exists:** [#6615](https://github.com/agentscope-ai/QwenPaw/pull/6615).

**🟡 Medium:**
- [#6588](https://github.com/agentscope-ai/QwenPaw/issues/6588) — `spawn_subagent` single-task mode unusable — `batch` exposed as required in schema (fix PR open).
- [#6601](https://github.com/agentscope-ai/QwenPaw/issues/6601) — No error reported on empty model responses near context limit.

**🟢 Lower severity:**
- [#6589](https://github.com/agentscope-ai/QwenPaw/issues/6589) — Massive shell output freezes UI (fix PR open).

**Overall stability trend:** The project is actively addressing its stability gap from the 2.0 migration, but the breadth of issues (config corruption, session deadlock, silent channel failures) suggests the regression surface from the AgentScope 2.0 rewrite was substantial.

---

## 6. Feature Requests & Roadmap Signals

Active feature requests and user needs:

1. **[#6083 — Desktop workspace output quick-access button](https://github.com/agentscope-ai/QwenPaw/issues/6083)** (4 comments)
   - Users want a one-click button in the Desktop window to access generated artifacts (reports, CSVs, images) without navigating to the file system. Requested for Windows Tauri users.
   - **Signals a user segment** — non-technical desktop users without file-system navigation comfort.

2. **[#6160 — Bundled Python runtime for Desktop](https://github.com/agentscope-ai/QwenPaw/issues/6160)** (4 comments)
   - Users on Windows without a global Python interpreter (e.g., using Conda) can't execute generated scripts. They request a bundled runtime.
   - Related to the Desktop product's "it just works" value proposition.

3. **[#6593 — Unified, professional cleanup page](https://github.com/agentscope-ai/QwenPaw/issues/6593)** (1 comment)
   - Agent runtime data bloat (auto-memory, temp files, backup, session history) has no management. Users want a global cleanup page with manual and automated options.
   - **Signals product maturity requirement** — the "garbage collection" feature that long-running personal AI users start needing.

4. **[#6559 — Session fork grouping / hierarchy](https://github.com/agentscope-ai/QwenPaw/issues/6559)** (2 comments)
   - Unwanted session forks are flat-listed and indistinguishable from user-created sessions. Users request tree/grouping structure with trigger-cause labels.

5. **[#6587 — Rename "QwenPaw Desktop" to "QwenPaw"](https://github.com/agentscope-ai/QwenPaw/issues/6587)** (1 comment)
   - Cosmetic naming nit for the Windows desktop app.

**Prediction for next version:** Desktop UX polish (quick-access, bundled Python, UI folding) is likely to be prioritized as feature asks cluster around the desktop experience. The flush/cleanup page is a stronger 2.1 candidate due to space-bloat complaints appearing across issues.

---

## 7. User Feedback Summary

Overall, user feedback paints a picture of a **powerful product with rough edges exposed after a major migration**:

**Pain points:**
- **UI/UX friction:** Tool-call output overwhelms results ([#6260](https://github.com/agentscope-ai/QwenPaw/issues/6260), 👍1) — one user explicitly says "thinking and tool calls take up the full screen, burying results." Session list chaos from unwanted forks ([#6559](https://github.com/agentscope-ai/QwenPaw/issues/6559)).
- **Reliability:** Silent failures are deeply frustrating — WeChat push "success" without delivery ([#6614](https://github.com/agentscope-ai/QwenPaw/issues/6614)), empty model responses with no error ([#6601](https://github.com/agentscope-ai/QwenPaw/issues/6601)), audio transcription failing silently ([#6544](https://github.com/agentscope-ai/QwenPaw/issues/6544), now fixed).
- **Windows-specific bugs:** `agent.json` corruption ([#6520](https://github.com/agentscope-ai/QwenPaw/issues/6520)), UI input box occlusion ([#6549](https://github.com/agentscope-ai/QwenPaw/issues/6549), now closed), Python environment requirements ([#6160](https://github.com/agentscope-ai/QwenPaw/issues/6160)).
- **Session continuity:** Switching sessions/modes loses messages or re-renders from scratch ([#6558](https://github.com/agentscope-ai/QwenPaw/issues/6558), fixed in PR #6602); Dream memory-loss window ([#6555](https://github.com/agentscope-ai/QwenPaw/issues/6555), fixed in PR #6592).

**Positive signals:**
- The **community is actively self-modulating**: issue #6563 (CI blocking all fork PRs) was raised by a first-time contributor and quickly addressed — a sign that maintainers are responsive to meta-issues.

---

## 8. Backlog Watch

Issues/PRs needing maintainer attention:

| Issue/PR | Age (days) | Status | Why it matters |
|----------|------------|--------|----------------|
| [#6203](https://github.com/agentscope-ai/QwenPaw/pull/6203) — fix(utils): bound and hide the Windows `tasklist` liveness probe | 16 days | Open, Under Review | The PR itself adds a timeout to `tasklist` probing. Key because Windows-based hangs are a recurring theme (see #6608, #6589). It's small but impactful — it has been sitting for 16 days. |
| [#6302](https://github.com/agentscope-ai/QwenPaw/pull/6302) — feat: unify provider discovery, model metadata, routing | 11 days | Open | A large feature PR that touches provider management. Unresolved, it technically conflicts with #6526 (NVIDIA provider) and #6167. Prioritize to avoid merge-conflict bloat. |
| [#6526](https://github.com/agentscope-ai/QwenPaw/pull/6526) — feat: Add NVIDIA NIM provider support | 4 days | Open | Blocked on review. Not critical but adds a backend users are asking for (NVIDIA on-prem). |
| [#6608](https://github.com/agentscope-ai/QwenPaw/issues/6608) — Long-running shell commands bypass timeout, block sessions | 1 day | Open | With a fix pending (#6610), this needs fast determination to include in the next release; this is the kind of bug that contributes to a poor "reliability" reputation. |
| [#6612](https://github.com/agentscope-ai/QwenPaw/issues/6612) — Proactive crashes with agentscope 2.0.4.post1 | 1 day | Open | This is a compatibility landmine — the pinned dependency broke features. It should get design-level attention since fix PR #6615 is a stopgap. |
| [#6537](https://github.com/agentscope-ai/QwenPaw/issues/6537) — Skill tags disappear on restart (regression) | 4 days | Open, 10 comments | The most-discussed issue. Users already hit this once (#3270) and now it's back. Regression of this type suggests the configuration-reconciliation logic changed subtly during 2.0 migration. Needs investigation and a regression test attached to the fix. |

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# ZeroClaw Project Digest
**Date:** 2026-08-01

---

## 1. Today's Overview

ZeroClaw is in a period of **exceptional architectural transformation and security hardening**. With 44 active issues and 44 open PRs updated in the last 24 hours, the project is experiencing a high-velocity design phase dominated by RFCs for major architectural changes. The maintainer community is actively reviewing numerous proposals on session ownership, memory separation, and transport adapters, with a concurrent focus on critical security fixes (including a P0 webhook authentication vulnerability and a P1 wasmtime CVE). While no new release was cut today, the high volume of merged security patches and accepted architectural RFCs signals a significant release may be imminent. Project health is strong but the sheer volume of RFCs awaiting maintainer review indicates a decision bottleneck that needs attention.

---

## 2. Releases

No new releases were published in the last 24 hours.

---

## 3. Project Progress

Six PRs were merged or closed today, including critical security and documentation fixes:

| PR | Description | Classification |
|---|---|---|
| [#9585](https://github.com/zeroclaw-labs/zeroclaw/pull/9585) | Fixed dead SLSA provenance link in release-verification docs | Documentation |
| [#9553](https://github.com/zeroclaw-labs/zeroclaw/pull/9553) | Added glob pattern matching for allowed commands (e.g., `docker-*`) | Feature |
| [#9075](https://github.com/zeroclaw-labs/zeroclaw/pull/9075) | Fixed `models_cache.json` persistence on models refresh (closes #9046) | Bug Fix |
| [#9552](https://github.com/zeroclaw-labs/zeroclaw/pull/9552) | Added TLS certificate verification skip option for MCP servers | Feature |
| [#9586](https://github.com/zeroclaw-labs/zeroclaw/pull/9586) | Waived RUSTSEC-2026-0222 (wasmtime) pending patch | Security |

The wasmtime vulnerability waiver was short-lived: [#9589](https://github.com/zeroclaw-labs/zeroclaw/pull/9589) has already been opened to bump the wasmtime stack to 47.0.3 with the actual fix.

---

## 4. Community Hot Topics

The most active discussions center on architectural RFCs:

1. **[#9048](https://github.com/zeroclaw-labs/zeroclaw/issues/9048) (14 comments)** — "RFC: Separate conversation history from agent-curated long-term memory" by Audacity88. The community is strongly debating the distinction between ephemeral conversation history and curated long-term memory, suggesting current implementation conflates the two.

2. **[#9127](https://github.com/zeroclaw-labs/zeroclaw/issues/9127) (11 comments)** — "RFC: Abstract a `KeySource` trait — classify master-key material by source / deployment form" by REL-mame. Security-focused discussion on how master key material should be sourced based on deployment context.

3. **[#8933](https://github.com/zeroclaw-labs/zeroclaw/issues/8933) (9 comments)** — "RFC: Add cross-turn conversation correlation to OTel export" by FTDGRT. The community wants better observability with `gen_ai.conversation.id` for tracing multi-turn interactions.

4. **[#9106](https://github.com/zeroclaw-labs/zeroclaw/issues/9106) (8 comments)** — "RFC: A2A outbound client (A2ATool)" by kingstar001. Significant interest in enabling ZeroClaw agents to proactively call external A2A-compliant agents.

5. **[#8603](https://github.com/zeroclaw-labs/zeroclaw/issues/8603) (8 comments)** — "RFC: OpenAI Chat Completions compatibility adapter" by REL-mame. Multiple related issues track this feature, indicating high demand for OpenAI-compatible API support among the community.

**Underlying needs:** The community is pushing for architectural maturity around memory separation, agent-to-agent communication, and tool ecosystem extensibility. The OpenAI compatibility adapter appears twice in the top-issues list, signaling strong demand for interoperability with existing tooling.

---

## 5. Bugs & Stability

Several high-severity bugs were reported or updated in the last 24 hours:

| Severity | Issue | Description | Fix Status |
|---|---|---|---|
| **P0** | [#9565](https://github.com/zeroclaw-labs/zeroclaw/issues/9565) | Gateway webhook handlers do not fail closed (WhatsApp Cloud, Linq, WATI). Attacker-controllable messages dispatched without caller authentication. | No fix PR yet — actively needs maintainer attention |
| **P1** | [#9596](https://github.com/zeroclaw-labs/zeroclaw/issues/9596) | Anthropic tool-result images inlined as base64 text instead of delivered as images — causes excessive token billing | No fix PR yet |
| **P1** | [#9572](https://github.com/zeroclaw-labs/zeroclaw/issues/9572) | Debug gateway WebSocket turns can overflow default Tokio worker stack | No fix PR yet |
| **P1** | [#9573](https://github.com/zeroclaw-labs/zeroclaw/issues/9573) | Cost pricing lookup fails for multiple aliases of the same provider type | No fix PR yet |
| **P2** | [#9590](https://github.com/zeroclaw-labs/zeroclaw/issues/9590) | Concurrent models refresh runs can lose cache entries (read-modify-write race) | No fix PR yet |
| **P2** | [#9562](https://github.com/zeroclaw-labs/zeroclaw/issues/9562) | WebChat auto-scroll overrides manual scrolling during streaming | No fix PR yet |

The **P0 webhook authentication bypass** (#9565) is the most critical stability/security issue, declared as S0 severity with data-loss/security implications. The wasmtime CVE (RUSTSEC-2026-0222) is being actively patched in [#9589](https://github.com/zeroclaw-labs/zeroclaw/pull/9589).

---

## 6. Feature Requests & Roadmap Signals

Strong signals point toward a comprehensive architectural overhaul in upcoming releases:

**High-probability features for next release (v0.8.4+):**
1. **OpenAI Chat Completions compatibility adapter** ([#8603](https://github.com/zeroclaw-labs/zeroclaw/issues/8603), [#8550](https://github.com/zeroclaw-labs/zeroclaw/issues/8550)) — Accepted, in-progress, multiple related issues suggest high priority.
2. **Separate conversation history from long-term memory** ([#9048](https://github.com/zeroclaw-labs/zeroclaw/issues/9048)) — Needs maintainer review but with 14 comments, this is a hot topic.
3. **Runtime-owned conversation sessions** ([#9487](https://github.com/zeroclaw-labs/zeroclaw/issues/9487)) — Proposed July 28, recent and fast-moving with a tracking issue (#9600) already opened.
4. **Mixture-of-Agents (MoA) virtual model provider** ([#8568](https://github.com/zeroclaw-labs/zeroclaw/issues/8568)) — Accepted pattern (from OpenClaw), reasonable for near-term.
5. **A2A outbound client tool** ([#9106](https://github.com/zeroclaw-labs/zeroclaw/issues/9106)) — Would follow the A2A server shipped in v0.8.2.

**SOP capability permission contract** ([#9598](https://github.com/zeroclaw-labs/zeroclaw/issues/9598)) and **Glob pattern matching for allowed commands** (merged PR #9553) suggest a continued emphasis on security and privacy controls.

---

## 7. User Feedback Summary

**Positive Signals:**
- The community actively engages in RFCs, demonstrating strong investment in the project's direction. The detailed, well-structured proposals (e.g., #9048, #9106) indicate sophisticated users with production deployment needs.
- Users are requesting enterprise-grade features (OTel correlation, A2A interop, OpenAI compatibility) — a positive sign of production adoption.
- Contributor diversity is high: 12+ distinct contributors active in the last 24h, including "principal contributors" and "distinguished contributors," suggesting a healthy contributor funnel.

**Pain Points:**
- **Onboarding friction:** Users reported broken LinkedIn link on org profile ([#9550](https://github.com/zeroclaw-labs/zeroclaw/issues/9550)) and documentation pointing to non-existent files (#9585 fix).
- **Quality-of-life issues:** WebChat auto-scroll during streaming (#9562), models_cache.json never written (#9046 closed but users may still be affected until release).
- **Security concerns:** P0 webhook issue suggests users deploying channel integrations (WhatsApp, WATI, Linq) may be at risk.
- **Configuration confusion:** Users are hitting edge cases with provider aliases (#9573) and MCP TLS connections (#9552).
- **Performance:** Token billing inflation for Anthropic image tools (#9596) and worker stack overflows (#9572) suggest real-world load issues.

---

## 8. Backlog Watch

Issues/PRs needing maintainer attention:

1. **[#9565](https://github.com/zeroclaw-labs/zeroclaw/issues/9565) (P0, S0)** — Webhook handlers do not fail closed. This is the highest-priority item needing immediate maintainer review.
2. **[#8519](https://github.com/zeroclaw-labs/zeroclaw/issues/8519) (P1, accepted)** — Reconcile cargo-audit/deny.toml drift. Open since June 30; security-sensitive dependencies cleanup that is being indirectly addressed by #9589 but still needs full closure.
3. **[#8996](https://github.com/zeroclaw-labs/zeroclaw/pull/8996)** — "fix(goal): preserve running goals across daemon reload." Open since July 11, marked with `needs-author-action`. High-risk, size XL — blocking goal feature stability.
4. **[#9109](https://github.com/zeroclaw-labs/zeroclaw/pull/9109)** — "feat(providers): add native Hailo-Ollama support." Open since July 17, high-risk, size XL. Hardware-specific but represents growing edge-hardware use cases.
5. **[#9598](https://github.com/zeroclaw-labs/zeroclaw/issues/9598)** — "RFC: Define SOP capability permission contract." Opened yesterday, already critical for security posture (required_permissions is not evaluated).
6. **[#9101](https://github.com/zeroclaw-labs/zeroclaw/issues/9101)** — Consolidate release attestation. Accepted P1 but open since July 16; the three-parallel-signing redundancy is a release-engineering debt point.
7. **RFCs nearing decision:** #9127 (KeySource trait), #9103 (memory separation), and #8933 (OTel correlation) all have `needs-maintainer-review` and are at risk of staleness if not addressed in the next maintainer decision pass.

**Build/CI debt:** PRs #9527 (toolchain bump), #9547 (CPAL upgrade), and #9548 (Codex CLI warning) have `needs-author-action` and risk blocking future CI/security releases.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/kky-wollu/agents-radar).*