# OpenClaw Ecosystem Digest 2026-08-06

> Issues: 500 | PRs: 500 | Projects covered: 13 | Generated: 2026-08-05 23:05 UTC

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

# OpenClaw Project Digest — 2026-08-06

## 1. Today's Overview

OpenClaw is experiencing a period of intense, sustained activity with **500 issues and 500 PRs updated in the last 24 hours** — signaling a deeply engaged community but also a potentially straining support backlog. Of those, **466 issues remain open/active** while only 34 closed, suggesting the maintainer team is heavily triaging new reports. The PR pipeline is healthier: **79 PRs were merged or closed today** against a backlog of 421 open. Notably, the **Clawsweeper autonomous fix bot is actively generating and submitting patches** (e.g., `#119737` Slack, `#119735` WhatsApp), indicating an automated remediation pipeline is operational alongside manual maintainer work. The "Latest Releases" field is empty, indicating no new tagged versions were published in the window, though pre-release betas (e.g., `2026.7.2-beta.7`) remain active in the wild. With several **P0 and P1 severity bugs** open (DB migration failure, media data loss), the project's health is characterized by extremely high community engagement paired with significant stability challenges under active remediation.

---

## 2. Releases

**None published in the last 24 hours.** No new stable, beta, or release-candidate versions were tagged during the reporting window. However, the presence of high-severity bugs reported against `2026.7.2` and `2026.7.2-beta.*` (like the `v14→v15` DB migration failure in `#119263`) suggests the maintainers are likely focused on stabilization and a patch release may follow. Users are urged to monitor the [Releases page](https://github.com/openclaw/openclaw/releases) for an imminent update, and to exercise caution with auto-update while the DB migration issue is open.

---

## 3. Project Progress

**79 PRs were merged or closed in the last 24 hours**, signaling strong throughput from both maintainers and the Clawsweeper bot. Key merged/closed items among the surfaced data:

| PR | Title | Status | Significance |
|----|-------|--------|--------------|
| [#119328](https://github.com/openclaw/openclaw/pull/119328) | docs(slack): document retired Socket Mode tuning cleanup | Closed | Documentation housekeeping; aligns Slack guide with current Socket Mode contract. |
| [#119147](https://github.com/openclaw/openclaw/pull/119147) | fix(auth): limit inline key cooldowns to credential failures | Closed | **Important fix:** prevents transient timeouts from disabling inline API keys for all subsequent sessions — reduces auth friction. |
| [#119727](https://github.com/openclaw/openclaw/pull/119727) | fix(qa): report cleanup failures truthfully | Closed | Improves QA Lab reliability by preventing false success signals when cleanup fails. |
| [#119749](https://github.com/openclaw/openclaw/pull/119749) | improve(agents): isolate concurrency benchmark workers | Closed | Maintainer tooling improvement; reduces "hot" session data from being mixed into benchmarks. |

Additionally, **Clawsweeper-bot-generated fixes** were authored today for the community:
- [#119737](https://github.com/openclaw/openclaw/pull/119737) — fix(slack): require confirmed thread placement for terminal receipts
- [#119735](https://github.com/openclaw/openclaw/pull/119735) — fix(whatsapp): refresh activity for pending inbound work (prevents false health-restarts)

Areas with active, unmerged fix PRs in review/proof include **agent run snapshots** (privacy leak fix `#117569`), **TUI picker lifecycle** (`#117285`), **session history restore** (`#116259`), and **general `in`-operator false-positive config lookups** (`#104511`, `#104510`).

---

## 4. Community Hot Topics

The following topics are generating the most traffic (comments + reactions), highlighting deep concern over **data loss, session reliability, and core UX**:

### 1. Realtime voice retaining unbounded provider/consult state
**[Issue #116201](https://github.com/openclaw/openclaw/issues/116201) — 58 comments — 🐚 Platinum Hermit (P1)**
Users reporting realtime voice sessions hold onto superseded state, potentially causing unbounded memory growth in bursty conditions. This is a high-visibility, high-complexity session-state bug with no fix PR yet.

### 2. Silent subagent completion loss
**[Issue #44925](https://github.com/openclaw/openclaw/issues/44925) — 25 comments — 🦞 Diamond Lobster (P1, 2 👍)**
Represents a systemic reliability issue: subagent orchestration can silently lose results when provider announcements fail, blocking downstream automation. Users emphasize this destroys trust in autonomous workflows.

### 3. Gateway main thread saturated from boot
**[Issue #118846](https://github.com/openclaw/openclaw/issues/118846) — 19 comments — CLOSED (P1)**
A crash-loop and local RPC death caused by plugin-metadata snapshotting and fs statting starving the accept loop. *Closed—indicating a fix exists or was re-triaged.*

### 4. Duplicate Telegram replies after 5.20 update
**[Issue #86519](https://github.com/openclaw/openclaw/issues/86519) — 14 comments — 🦞 Diamond Lobster (P1, 1 👍)**
A regression persisted from `2026.5.20` into `2026.5.22`; users report 2–3x duplicate replies per message. High frustration channel-level bug.

### 5. Hardcoded dev workspace path merged into code
**[Issue #51429](https://github.com/openclaw/openclaw/issues/51429) — 13 comments — 🦞 Diamond Lobster (P2)**
Chinese-language report: a developer "wangtao" seemingly hardcoded his local working directory (`/Users/wangtao`) into the released binary. Rustles engineering-confidence feathers.

**Underlying needs detected:** Across hot topics, the community is calling for **stronger session-state guarantees, reliable async task execution, and better CI/test gatekeeping to prevent regressions and environment-specific leaks**.

---

## 5. Bugs & Stability

Bugs dominate the open issues, with severity and fix-PR availability tracked below.

### 🔴 P0 (Critical / Release-Blockers)
| Issue | Summary | Fix PR? |
|-------|---------|---------|
| [#119263](https://github.com/openclaw/openclaw/issues/119263) | **Agent DB v14→v15 migration fails with `no such column: entry_valid`; gateway refuses to start** — bricks existing installations post-update. | No, awaiting maintainer (linked PR open but not shown) |
| [#119090](https://github.com/openclaw/openclaw/issues/119090) | **Managed media cleanup fails OPEN** — deletes session's generated media permanently if store unreadable (`CLOSED`, fix likely in progress) | Closed (fix in pipeline) |
| [#119088](https://github.com/openclaw/openclaw/issues/119088) | **`attachments.ttlHours` sweeps the entire media tree**, deleting durable chat-history media. (Closed—notably by same reporter as above) | Closed (fix in pipeline) |
| [#70903](https://github.com/openclaw/openclaw/issues/70903) | **Persistent file-based provider cooldown** blocks users for hours after billing recovery. | No (needs product decision) |

### 🟠 P1 (High)
| Issue | Summary | Fix PR? |
|-------|---------|---------|
| [#116201](https://github.com/openclaw/openclaw/issues/116201) | Unbounded provider/consult state in realtime voice. | **No** |
| [#44925](https://github.com/openclaw/openclaw/issues/44925) | Silent subagent completion loss on timeout. | **No** |
| [#86519](https://github.com/openclaw/openclaw/issues/86519) | Duplicate Telegram replies (regression, still present). | **No** |
| [#112423](https://github.com/openclaw/openclaw/issues/112423) | SQLite transcript cleanup blocks gateway event loop. | **No** |
| [#85251](https://github.com/openclaw/openclaw/issues/85251) | Codex app-server sends turn/started then goes silent; wedges for 360s. | **No** |
| [#106231](https://github.com/openclaw/openclaw/issues/106231) | Loop detection blocks exec but never terminates agent; burns resources. | **Yes — [#117884](https://github.com/openclaw/openclaw/pull/117884)** (related, quiet-turn fix) |
| [#84583](https://github.com/openclaw/openclaw/issues/84583) | Cron announce triggers `EmbeddedAttemptSessionTakeoverError` during active chat. | **No** |
| [#85844](https://github.com/openclaw/openclaw/issues/85844) | Auto-update leaves gateway using stale hashed bundle imports. | **No** |
| [#91982](https://github.com/openclaw/openclaw/issues/91892) | Cron jobs stall during model calls (`stream_progress` never completes). | **No** |
| [#117609](https://github.com/openclaw/openclaw/issues/117609) | Transient LLM errors kill whole embedded-assistant turns (no retry). | **No** |
| [#115700](https://github.com/openclaw/openclaw/issues/115700) | `chat.send` rejected "thread switched branches" after model completes; stale leaf ID. | **No** |
| [#97616](https://github.com/openclaw/openclaw/issues/97616) | Leaks unreaped child processes → zombie accumulation. | **No** |

### 🟡 Notable P2 Durability & Data-Loss Risks
- [#113306](https://github.com/openclaw/openclaw/issues/113306) — SQLite snapshot restore lacks end-to-end crash and identity guarantees.
- [#119557](https://github.com/openclaw/openclaw/issues/119557) — Chat delta throttle has no trailing flush; chunks get dropped silently.

**Key takeaway:** The preponderance of unresolved P1 bug reports related to **session-state corruption and message loss** suggests a systemic race involving session lock files, context deltas, and the SQLite transition, which is the primary threat to platform trust right now. The migration blocker `#119263` directly prevents users from moving forward.

---

## 6. Feature Requests & Roadmap Signals

Many open issues are effectively feature requests with strong signals:

| Issue | Ask | Outlook |
|-------|-----|---------|
| [#79902](https://github.com/openclaw/openclaw/issues/79902) | **Companion-friendly SQLite transcript/session seams** — expose canonical state as a public data model. | High value, moderate complexity; could be a v2026.8 candidate. |
| [#53654](https://github.com/openclaw/openclaw/issues/53654) | **Discord support for message edits→re-process and deletes→cancel.** (3 👍) | Likely roadmap item—an open PR `#96793` exists for Telegram topics (related), suggesting momentum. |
| [#50205](https://github.com/openclaw/openclaw/issues/50205) | **Configurable request labels for Gemini API calls** (for billing attribution). | Small, easy win—likely in next sprint. |
| [#50798](https://github.com/openclaw/openclaw/issues/50798) | **Visible agent-to-agent messaging for ACP thread-bound sessions** (proxy-only delivery). | Niche but highly requested by power users. |
| [#8892](https://github.com/openclaw/openclaw/issues/8892) | **`--agent` flag for TUI** to select a specific agent (3 👍). | Simple lookup fix; good first-contributor candidate. |
| [#44289](https://github.com/openclaw/openclaw/issues/44289) | **Generate secretref reference docs from registry metadata** (reduce manual sync). | Internal DX improvement; likely if maintainers feel the pain. |
| [#119256](https://github.com/openclaw/openclaw/pull/119256) | **WhatsApp poll vote hook** (live PR exists for review). | Likely in next release if merged. |

**Prediction:** The next minor/major version will prioritize: 1) SQLite migration/durability fixes (unblock `#119263`), 2) session-state concurrency hardening, and 3) small-affordance UX additions (TUI agent flag, Gemini labels).

---

## 7. User Feedback Summary

**Real pains being voiced strongly this week:**
- **"Migration hell"** — `v14→v15` DB failure makes a normal update turn into an outage; some users may be stuck on old versions.
- **"Silent failures"** — Subagents complete invisibly or don't complete at all, and errors are swallowed, eroding trust for automation users (repeated across `#44925`, `#85251`, `#109490`).
- **"Duplicate spam"** — Telegram/QQ/Discord duplicate deliveries frustrate end-users in public channels and give a "buggy bot" impression.
- **"The wangtao incident"** (`#51429`) — Symbolic for users: hardcoded personal paths and prototype-chain bugs make code look fragile and QA-less.
- **"Cooldowns out of thin air"** — Users express anger when they are temporarily locked out of providers due to billing/cooldown logic misconfigurations (`#70903`, `#115642`).

**Satisfaction signals:** The heavy volume of feature requests, Clawsweeper activity, and detailed bug reports suggests an *extremely engaged, technically sophisticated user base* who see OpenClaw as a critical infrastructure and care deeply about hardening it. The prompt generation of N-of-1 bugs and the maintainer's quick closure of bulk-filed media cleanup bugs (`#119088/#119090`) are positive signals for responsiveness.

---

## 8. Backlog Watch

Items of importance that appear **stale or unanswered** (no recent maintainer fix visible, older than a month):

| Issue | Age | Concern |
|-------|-----|---------|
| [#70903](https://github.com/openclaw/openclaw/issues/70903) (P0) | Apr 24 | Persistent billing cooldown blocks users for hours. Despite P0, it lacks a clear fix PR and sits in "needs product decision." **This is a dark spot.** |
| [#67419](https://github.com/openclaw/openclaw/issues/67419) (P2) | Apr 15 | Bootstrap files re-injected every turn wasting 20–30% tokens. Has a clear fix shape ("fix-shape-clear") but no PR yet. |
| [#53654](https://github.com/openclaw/openclaw/issues/53654) (P2) | Mar 24 | Discord edit/cancel events. Community requested for months. |
| [#8892](https://github.com/openclaw/openclaw/issues/8892) (P3) | Feb 4 | TUI `--agent` flag. Small, easy, still unaddressed for 6 months. |
| [#50165](https://github.com/openclaw/openclaw/issues/50165) (P2) | Mar 19 | Subagents appear completed before actual work finished—critical semantics issue for orchestration builders. |
| [#44289](https://github.com/openclaw/openclaw/issues/44289) (P2) | Mar 12 | Secretref docs generation. |

**Maintainers should prioritize:**
1. **(P0) Resolve DB migration `#119263` and cooldown exhaustion `#70903`** — both are direct platform blockers.
2. **(P1) Provide a definitive answer or merge PR** for session-state/message-loss cluster (`#44925`, `#86519`, `#85251`). The community is clearly converging on this being a systemic fault, not isolated bugs.
3. **(P2) Close the loop on easy UX wins** (`#8892`, `#50205`) to show responsiveness and encourage the volunteer contributor pipeline.

---

*Digest generated via analysis of raw GitHub data from `openclaw/openclaw` for the 24h window ending 2026-08-06. All links refer to the [OpenClaw repository](https://github.com/openclaw/openclaw).*

---

## Cross-Ecosystem Comparison

# Cross-Project Ecosystem Comparison Report
**Date:** 2026-08-06
**Period:** 24-hour window ending 2026-08-06

---

## 1. Ecosystem Overview

The personal AI assistant/agent open-source landscape is experiencing intense, bifurcated activity. A core cluster of projects (OpenClaw, Hermes Agent, IronClaw, ZeroClaw, CoPaw) operates at extreme velocity with 40-500 issues and PRs touched daily, while smaller projects (NanoBot, NanoClaw, NullClaw, PicoClaw, LobsterAI) show focused, steady iteration on specific stability and feature goals. The dominant concerns across all active projects converge on **session-state integrity, message delivery reliability, and multi-channel robustness**, with a clear shift toward **architectural hardening** (god-file decomposition, canonical messaging contracts, unified provider layers) over new feature velocity. Community feedback consistently highlights **silent failures and data loss** as the primary trust-eroding bugs—whether database migrations, subagent completion drops, or attachment handling—suggesting the ecosystem is transitioning from prototype excitement to production-grade reliability demands.

---

## 2. Activity Comparison

| Project | Issues (24h) | PRs (24h) | Merged/Closed PRs | Release Status | Health Score* |
|---|---|---|---|---|---|
| **OpenClaw** | 500 (466 open) | 500 | 79 | None; P0 blockers active | 🟡 **7/10** — Extreme engagement, stability risks |
| **Hermes Agent** | 50 | 50 | 10 | None; P0 fix merged today | 🟢 **8/10** — Fast iteration, critical gap remains |
| **IronClaw** | 43 (33% closed) | 50 | 21 (42%) | **v1.1.0-rc.1** (3d ago) | 🟢 **8/10** — Release-focused, agent-honesty P1s |
| **CoPaw** | 23 (26% closed) | 50 | 21 | v2.1.0-beta.2 | 🟡 **6/10** — High merge rate, critical regressions |
| **ZeroClaw** | 50 | 50 | 1 | None; v0.8.5 freeze | 🟡 **6/10** — Design-heavy, review bottleneck |
| **LobsterAI** | 3 (new bugs) | 12 | 12 | **2026.8.5** (yesterday) | 🟢 **8/10** — Clean release, fast bug intake |
| **NanoBot** | 4 | 16 | 8 (50%) | None; release imminent | 🟢 **8/10** — Balanced velocity, responsive |
| **NanoClaw** | 2 (revived) | 10 | 1 | None | 🟡 **7/10** — Active but stability PRs stalled |
| **PicoClaw** | 0 | 3 | 0 | None | 🟡 **5/10** — Low activity, lockfile blocker |
| **NullClaw** | 0 | 2 | 0 | None | 🟢 **7/10** — Small, focused, root-cause fixes |
| **TinyClaw** | — | — | — | — | ⚪ Inactive |
| **Moltis** | — | — | — | — | ⚪ Inactive |
| **ZeptoClaw** | — | — | — | — | ⚪ Inactive |

*Health Score is a qualitative composite of velocity, responsiveness, release progress, and severity of open blockers.

---

## 3. OpenClaw's Position

**Advantages:**
- **Scale & Reach:** 500 issues/PRs in 24h is 10x the nearest peers (Hermes, IronClaw, ZeroClaw at 50 each), indicating an order-of-magnitude larger install base and community.
- **Automated Remediation:** Clawsweeper bot autonomously generates and submits fixes (e.g., Slack receipts, WhatsApp health-restart), a unique operational capability.
- **Swarming Speed:** Maintainers close issues within hours (e.g., media cleanup bugs #119088/#119090), showing high triage discipline.

**Technical Approach Differences:**
- Unlike IronClaw's Rust (compiled, architecture-first) or NanoBot's Go (middleweight, single-binary), OpenClaw's JS/TS (Node) monorepo enables faster plugin/contribution velocity but appears to be a **primary source of systemic session-state races** (P1 cluster: #44925, #86519, #85251) and DB migration fragility.
- Relies on a versioned "reference" status with ecosystem forks, amplifying both its reach and its bugs.

**Community Size Comparison:**
- OpenClaw's issue volume (466 open) dwarfs the others combined; this is both a testament to adoption and a support-backlog risk signaling the need for a **stability-focused release quarter** to restore trust.

---

## 4. Shared Technical Focus Areas

Across multiple projects, these requirements are emerging (bolded = strongest cross-project signal):

**A. Session-State Integrity & Data Loss Prevention**
- OpenClaw: SQLite migration failure (#119263), realtime voice state leak (#116201), silent subagent loss (#44925)
- Hermes Agent: Interrupted compaction deletes history (#79391), LIKE-wildcard injection deletes sessions (#79722, fixed)
- IronClaw: Lossless 1.0→1.1 migration (#7256), state-honesty bugs (#7246, #7247)
- LobsterAI: Gateway lock poisoning (fixed #2436)
- CoPaw: Long-session 400 tool-role errors (#6726), shell background hangs (#6480)

**B. Message Delivery Reliability (Silent Failures)**
- OpenClaw: Duplicate Telegram replies (#86519), thread-switch staleness (#115700)
- NanoBot: MCP business-error envelopes ignored (#5237) — leads to agent waiting
- ZeroClaw: Signal sourceUuid drops (#9774), OpenRouter streaming loses provider config (#9775)
- IronClaw: Slack DM delivered to Telegram (#7249), attachments MIME-type rejection (#6257)
- CoPaw: WeChat context_token conflict (#6696), SSE 503 not retried (#6708)

**C. Config-as-Code & User-Controllable Prompts**
- OpenClaw: Secretref generator (#44289), configurable request labels (#50205)
- IronClaw: Config-as-Code epic (#3036, `reborn`)
- ZeroClaw: `cron update` discards changes (#9770)
- LobsterAI: System prompt bloat/duplication (#2440), config surface gaps (#2441)

**D. Agent-to-Agent & Multi-Agent Orchestration**
- OpenClaw: ACP thread-bound messaging (#50798)
- NanoClaw: SendMessage interop fix (#3187, merged)
- Hermes Agent: Multi-tenant isolation (#34352, most-commented)
- ZeroClaw: Goal mode RFC (#8303), ZeroCode multi-agent sidebar (#9727)

**E. Ephemeral/Privacy-Preserving Sessions**
- NanoBot: Temporary Chat (#5252), memory-ignore PR
- OpenClaw: Privacy leak in run snapshots (#117569)
- Hermes Agent: Session deletion hazards (P0 #79722)

---

## 5. Differentiation Analysis

| Project | Primary Target | Technical Core | Key Differentiator |
|---|---|---|---|
| **OpenClaw** | General users, enthusiasts | TypeScript/Node, plugin ecosystem | Largest community; Clawsweeper bot; channel breadth |
| **Hermes Agent** | Power users, DevOps | Python (OpenAI codex lineage) | Deep session/tooling control; multi-platform (Windows/Desktop); fast security cadence |
| **IronClaw** | Enterprise, platform builders | Rust, WebAssembly | Release discipline (Rust toolchain); 1.1 RC focus; durable attachments |
| **ZeroClaw** | Security-conscious, architects | Rust (gateway), plugin/WASM sandbox | RFC-driven design; threat-modeling rigor; Windows/Task Scheduler support |
| **CoPaw** | Mainstream, low-code | Python, multi-channel (WeChat-first) | Middleweight deployment (v2.1.0-beta); LLM fallback just shipped |
| **NanoBot** | Lightweight deployments | Go, single-binary | Model metaprogramming; temporary chat; MCP host ambitions |
| **NanoClaw** | Hardware-focused, edge? | Go | Container/edge focus; channel diversity (Signal, WhatsApp) |
| **NullClaw** | Minimalist, existing infrastructure | Go | Empty-issue queue; root-cause RPM (turn-stack fix, supervision loop) |
| **PicoClaw** | Lightweight, Sipeed HW | Go | Low-resource; install reliability |
| **LobsterAI** | Enterprise NIM-based | Electron desktop + NestJS/TypeScript | Native UI polish; enterprise auth isolation; activity/engagement focus |

---

## 6. Community Momentum & Maturity

**Tier 1 — Extreme Velocity, High Stress (Stabilizing):**
- **OpenClaw** — 500 issues/PRs daily; 466 open issues; P0 blockers; needs dedicated stabilization window
- **IronClaw** — High merge rate (21 PRs); RC-1; active bug-bash; pre-release hardening

**Tier 2 — Fast, Balanced, Healthy:**
- **Hermes Agent** — 50 issues/PRs; 10 merged, including P0 session fix
- **ZeroClaw** — 50 issues/PRs; 1 merged (review bottleneck); deep RFC design work
- **CoPaw** — 50 PRs/23 issues; 21 merged; but critical PYTHONHOME regression and WeChat bugs

**Tier 3 — Focused, Steady, Mature:**
- **NanoBot** — 16 PRs/4 issues; 8 merged; model metaprogramming features
- **NanoClaw** — 10 PRs/2 issues; 1 merged; container-edge focus
- **LobsterAI** — 12 PRs/3 issues; 12 merged; clean daily release cadence

**Tier 4 — Low-Key / Maintenance / Inactive:**
- **PicoClaw** — 0 issues, 3 open PRs; needs lockfile fix
- **NullClaw** — 0 issues, 2 active PRs closing long-standing bugs
- **TinyClaw, Moltis, ZeptoClaw** — No activity; wait-and-see or dormant

**Rapid Iteration Signal:** OpenClaw, Hermes Agent, IronClaw, CoPaw
**Stabilizing Signal:** ZeroClaw (v0.8.5 freeze), IronClaw (RC-1), LobsterAI (daily releases)

---

## 7. Trend Signals

**Signal 1: The "Agent Ecosystem" Is Crowding In**
- **The Ask:** MCP hosts (NanoBot wants MCP *UI* apps; IronClaw registers arbitrary MCP servers), agent-to-agent messaging (NanoClaw, OpenClaw), multi-agent sidebars (ZeroClaw).
- **The Value:** Seamless interoperability with a growing MCP/agent tool landscape; empowering users to compose, not just chat. This is the fastest-moving feature direction across the ecosystem.

**Signal 2: **"State Honesty" Is the New Trust Metric****
- **The Bug:** Agents claiming "GitHub connected" when it isn't (IronClaw #7247), "automation running" when it's empty (#7246), "work completed" when Git hooks rejected (CoPaw #6722), or silently never completing (OpenClaw #44925).
- **The Value:** For any delegation, the single most corrosive failure is an agent that *lies about its own state.* Users are structuring workflows around this. Building verification, not assumption, into tool results is now the defining differentiator between "demo" and "production."

**Signal 3: "Silent Failure" Is More Damaging Than a Crash**
- **The Pattern:** A crash is loud and triggers a retry; a silent drop (Telegram duplicates, Signal sourceUuid, MCP business-error envelopes, cron update discarding changes) is invisible until a downstream task fails or users notice a missed reply.
- **The Value:** The next quality bar is a comprehensive failure-surface audit: honest error propagation, mandatory retries on known-transient errors (503s), and eliminating swallows. This is bigger than bug-fixing; it's a design principle.

**Signal 4: "Developer-First Ops" Is the Adoption Driver**
- **The Rigor:** ZeroClaw's RFC discipline and WASM deadlines; IronClaw's workspace-slice decomposition and frozen doc boundaries; Hermes Agent's god-file sharding epic; NullClaw's root-cause stack fix.
- **The Value:** Contributors choose projects that are governed like software. Projects that implement formal change management (RFC trackers, release trains, architecture trackers) are attracting a higher-quality contributor pool (labeled "distinguished contributors", "principal contributors"), which becomes a self-fulfilling signal of long-term viability.

**Signal 5: "LLM Gateway Governance" Is Becoming Central**
- **The Thread:** CoPaw's LLM fallback system (just landed) + ZeroClaw's OpenRouter prompt caching/stable session_id + NanoBot's provider-native request switches + OpenClaw's cooldown exhaustion fix.
- **The Value:** As users run multi-provider, multi-model, multi-tenant deployments, the "model routing / gateway" layer is evolving from a config-file nuisance into a critical reliability and cost optimization surface. Products that make this surface transparent, testable, and self-optimizing will win the ops-user market.

**Signal 6: Quant Compute Is Creeping into Agents**
- **The Trajectory:** NanoClaw (edge), PicoClaw (Sipeed hardware), ZeroClaw (Hailo-Ollama provider).
- **The Implication:** The next wave of differentiation may be the ability to run small-model agents on local quantized hardware — for privacy, cost, and offline resilience. This is nascent but a genuine long-term architectural direction distinguishing the "edge" forks from the "cloud-scale" monoliths.

---

## Peer Project Reports

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot Project Digest — 2026-08-06

## 1. Today's Overview
NanoBot shows a **high-velocity development day** with 16 pull requests updated in the last 24 hours (8 open, 8 merged/closed) and 4 active issues. The project is clearly in a **feature-expansion and hardening phase**: the dominant themes are WebUI enhancements (temporary chat, interactive terminal, visual consistency), provider integrations (metasearch, request switches), and critical bug fixes (WhatsApp media, Matrix compatibility, goal-loop runaway). No new releases were cut today, but the volume and quality of merged PRs suggest a significant release is imminent. The maintainer team appears highly responsive, with several PRs addressing issues filed just 1–2 days ago.

## 2. Releases
**No new releases** were published in the last 24 hours. The last release remains the current published version; given the 8 merged PRs today (including security and P1-priority fixes), a minor or patch release is likely within the next few days.

## 3. Project Progress
Eight PRs were merged/closed today, advancing several fronts:

**WebUI Polish & UX:**
- **[#5249 — refactor(webui): improve visual consistency](https://github.com/HKUDS/nanobot/pull/5249)** — Introduced a two-level elevation system for menus/dialogs, flattened Skills/Channels layouts, removed replay animations, and added automatic timezone detection.
- **[#5250 — fix(webui): feather clipped activity edges](https://github.com/HKUDS/nanobot/pull/5250)** — Direction-aware fading for clipped activity panes, keeping the latest row clear during auto-follow.

**Provider & Channel Integrations:**
- **[#5234 — feat(agent): integrate mst-python as a metasearch provider](https://github.com/HKUDS/nanobot/pull/5234)** — A new Meta-Search Tool aggregating DuckDuckGo, Google, Brave, Bing with Reciprocal Rank Fusion for richer search coverage.
- **[#5233 — feat(mattermost): separate group policy for threads](https://github.com/HKUDS/nanobot/pull/5233)** — Adds `groupPolicyInThread` config so mention requirements differ between threads and main channels, exposed in WebUI.
- **[#5254 — feat: add provider-native request switches](https://github.com/HKUDS/nanobot/pull/5254)** — WebUI switches for OpenAI Codex Fast mode, OpenAI/DeepSeek web search, and xAI Grok X Search via `extraBody` modifications.

**Critical Fixes:**
- **[#5238 — refactor(session): remove request-scoped access grants](https://github.com/HKUDS/nanobot/pull/5238)** — Reverts a P1 regression, simplifying session tools to use construction-time `Tool.enabled()` only.
- **[#5203 — fix(whatsapp): detect outbound media content before dispatch](https://github.com/HKUDS/nanobot/pull/5203)** — Uses libmagic content detection instead of filename extensions; unsupported audio goes as documents.
- **[#5184 — feat(webui): add Quick Chat and Temporary Chat](https://github.com/HKUDS/nanobot/pull/5184)** — Merged foundational work for persistent Quick Chat and opt-in temporary sessions (superseded by newer PRs #5252/#5259).

## 4. Community Hot Topics
**Most Active Issue:**
- **[#5149 — [bug] no audio? (WhatsApp)](https://github.com/HKUDS/nanobot/issues/5149)** — 4 comments. Users report NanoBot receives audio but fails to *send* audio files on WhatsApp; logs point to a neonize/ffmpeg warning. This is an older issue (created 2026-07-28) and has a **targeted fix already merged today** (PR #5203), which should resolve it. The user's frustration is understandable given the 8-day wait.

**Most Active PRs (by attention):**
- **[#5252 — feat(webui): add temporary chat mode](https://github.com/HKUDS/nanobot/pull/5252)** — A highly requested privacy feature; part of a stacked chain with #5259. The merged #5184 (Quick Chat/Temporary Chat) shows this direction is confirmed.
- **[#5238 — refactor(session): remove request-scoped access grants](https://github.com/HKUDS/nanobot/pull/5238)** — A P1 regression fix that reverts an over-engineered permission layer from #5211; merged quickly, indicating strong maintainer priority on session stability.

**Underlying needs:** The cluster of PRs around *Temporary Chat* and *Quick Chat* reveals a real user desire for **privacy-preserving, ephemeral interactions** that don't pollute session history or persistent memory. Combined with the memory-ignore PR (#5260), users are pushing for cleaner separation between transient work and long-term stored state.

## 5. Bugs & Stability
Two open bugs reported today, plus one critical fix merged:

| Severity | Issue | Status | Fix Available? |
|----------|-------|--------|----------------|
| **High (P1)** | [#5237 — MCP tool "data not found" envelope → agent ignores it, waits for tool_timeout](https://github.com/HKUDS/nanobot/issues/5237) | Open | No PR yet. The agent treats `isError=False` business-error envelopes as success, wasting timeout cycles and confusing the LLM. This is a **design flaw in MCP error handling** — arguably the most impactful open bug. |
| **Medium (P2)** | [#5256 — /goal message produces dozens of repeated replies](https://github.com/HKUDS/nanobot/issues/5256) | Open | **Fix PR ready: [#5257](https://github.com/HKUDS/nanobot/pull/5257)** — Bounds sustained-goal continuation when idle. The loop only ended when the model self-detected the system loop. |
| **Medium (P2)** | [#5149 — no audio on WhatsApp (older)](https://github.com/HKUDS/nanobot/issues/5149) | Open | **Fix merged today: [#5203](https://github.com/HKUDS/nanobot/pull/5203)** — Content-based media detection should resolve this. |
| **Medium (P2)** | [#5258 — security: credential-bearing URLs sent to remote Jina reader](https://github.com/HKUDS/nanobot/pull/5258) | PR open | **PR #5258 itself is the fix** — routes `user:pass@` and token-style URLs through local readability instead. |

**Regression watch:** PR #5238 was explicitly labeled `[regression]` — it rolled back the request-scoped access grants from #5211, indicating that earlier permission model caused real problems. This has been successfully reverted.

## 6. Feature Requests & Roadmap Signals
**New requests today:**
- **[#5251 — Feature: Add MCP Apps host support to WebUI](https://github.com/HKUDS/nanobot/issues/5251)** — User `yuklcool` asks for support of the official `io.modelcontextprotocol/ui` extension, enabling MCP servers to attach interactive UIs inside the WebUI (beyond text/image artifacts). This is a **forward-looking, high-value request** that would make NanoBot a true MCP *host* platform, not just a client. Given the strong MCP momentum in the project, this is a plausible next-version candidate.

**Trending themes visible in PRs:**
- **Ephemeral privacy mode** (Temporary Chat, memory-only sessions) — very likely in next release.
- **Interactive project terminal** (shared PTY in WebUI, #5253) — a major power-user feature.
- **Self-hosted search aggregation** (MST integration, #5234) — reducing dependence on single search providers.

## 7. User Feedback Summary
- **Pain point (MCP reliability):** The #5237 complaint is sharp: "the LLM never learns the call failed, so it cannot re-i..." This indicates production users depend on MCP tools and need **trustworthy error propagation**. The current silent-failure behavior wastes tokens and time.
- **Pain point (agent loops):** #5256's "dozens of near-identical replies" describes a **runaway loop** that required user intervention — a high-frustration scenario. The project responded with a fix PR in under a day, showing good responsiveness.
- **Positive signal (feature velocity):** Users are asking for advanced capabilities (MCP Apps host, PTY terminal) — evidence of a sophisticated, engaged user base treating NanoBot as a serious platform.
- **Satisfaction indicator:** The maintainers' ability to merge 8 PRs in one day (including P1 fixes with tests) suggests healthy project governance and strong contributor throughput.

## 8. Backlog Watch
- **[#5149 — no audio on WhatsApp](https://github.com/HKUDS/nanobot/issues/5149)** — Open for 8 days despite fix #5203 merged today. **Maintainers should verify and close immediately** to avoid prolonged user frustration.

- **No other stale issues observed** in the 24-hour window. The project's triage velocity is excellent; issues are being addressed in days, not weeks.

---

*Digest generated 2026-08-06. All data sourced from HKUDS/nanobot GitHub activity in the preceding 24 hours.*

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent Project Digest
**Date:** 2026-08-06

---

## 1. Today's Overview

Hermes Agent is experiencing a high-velocity development cycle with **50 issues and 50 PRs updated in the last 24 hours** — a very active period driven largely by a cross-cutting **session-state stability initiative** and a **repo-wide "god-file" decomposition epic**. Activity clusters around three themes: schema-breaking bug fixes (the `exit(1)` gateway compaction crash, an `hermes update` regression, and session-deletion hazards), a large refactoring effort to break apart monolithic adapter files, and a wave of duplicate reports surfacing the same lifecycle-guard crash. The project shows **healthy, fast-paced iteration** — several P0/P1 bugs filed today already have fix PRs open within hours. Notably, **10 PRs were merged/closed today**, including a **P0 session-deletion fix** (#79722), while **zero new releases** were cut, indicating the project is consolidating a large batch of changes for the next version.

---

## 2. Releases

**No new releases in the last 24 hours.** The latest public version referenced in issues is **Hermes Agent v0.8.0** (2026.4.8) for the stable channel and **v0.20.0** (git install, Aug 2026) for the dev channel. Given the cluster of P0/P1 fixes merged today, a patch or minor release appears imminent.

---

## 3. Project Progress

The following PRs were **merged or closed today**, representing concrete forward progress:

| PR | Title | Type | Impact |
|----|-------|------|--------|
| [#79722](https://github.com/NousResearch/hermes-agent/pull/79722) | `fix(sessions): escape LIKE wildcards in prune/archive filters and the cwd-prefix clause` | **P0 bugfix** | Fixes a data-loss bug where `_` and `%` in session-title filters matched wildcards and **permanently deleted** unintended sessions (e.g. `user_auth` matched `user-auth`, `userXauth`). |
| [#78927](https://github.com/NousResearch/hermes-agent/pull/78927) | `fix(sessions): escape LIKE wildcards in the cwd-prefix clause` | **P1 bugfix** | Closes the same class of wildcard-injection bug in the cwd-prefix query. |
| [#78681](https://github.com/NousResearch/hermes-agent/pull/78681) | `fix(sessions): escape LIKE wildcards in prune/archive substring filters` | **P1 bugfix** | Consolidates filter-escape contract in `SessionDB`. |
| [#79737](https://github.com/NousResearch/hermes-agent/pull/79737) | `refactor(state): consolidate SQL LIKE escaping onto one shared helper` | Refactor | Consolidates 7 duplicate inline escape implementations into one `escape_like()` helper (net −50 LOC). |
| [#57867](https://github.com/NousResearch/hermes-agent/pull/57867) | `fix(environments): portable per-writer PID for atomic snapshot writes on bash 3.2` | Bugfix | Resolves macOS `/bin/bash` 3.2 `$BASHPID` empty-string issue that caused concurrent env-snapshot writers to share one temp file. |
| [#79736](https://github.com/NousResearch/hermes-agent/pull/79736) | `fix(desktop): don't persist zoom fallback on a transient read failure` | Bugfix | Stops desktop zoom resetting to 90% default when reading state transiently fails. |
| [#8576](https://github.com/NousResearch/hermes-agent/issues/8576) | `[security] WhatsApp bridge npm vulnerabilities` | Security | Closed — npm vulnerabilities fixed. |
| [#3230](https://github.com/NousResearch/hermes-agent/pull/3230) | `feat(skills): add Pi Coding Agent support` | Feature | New skill added for Pi Coding Agent CLI integration. |
| [#79642](https://github.com/NousResearch/hermes-agent/issues/79642) | Guest Task Drop: TaskMarket delegation | — | Closed as invalid (spam/promotional). |
| [#15951](https://github.com/NousResearch/hermes-agent/issues/15951) | doctor reports agent-browser not installed when globally installed | Bug | Closed — likely fixed by the new bundled-installer work. |

**Emerging trend:** The session-data-integrity trio (#79722, #78927, #78681) merged today signals a **coordinated hardening of `SessionDB`** against SQL wildcard injection — a significant reliability milestone for the session/prune/archive pipeline.

---

## 4. Community Hot Topics

The most actively-discussed items (by comment count and reactions):

**[#34352 — Multi-Tenant Hermes Problem** (15 comments, 2 👍)](https://github.com/NousResearch/hermes-agent/issues/34352)
> **Analysis:** The most-commented open issue, this long-running (since May) design discussion argues that memory operations bypass the hook system entirely, making tenant isolation impossible without forking core. The author claims to have **run a fix in production for months** with multiple concurrent multi-tenant agents. This is a **strategic architectural signal** — the community sees multiplayer agentic AI as the future and wants Hermes to lead. It remains open with `needs-decision` — the maintainers have not yet committed to an isolation architecture.

**[#77780 — lifecycle_guard crashes on `ValueError: embedded null byte`** (11 comments)](https://github.com/NousResearch/hermes-agent/issues/77780)
> **Analysis:** The most-replicated bug today — **two duplicate issues** (#79704) were filed. The `cron/lifecycle_guard.py` guard crashes on `os.open` when tokenizing heredoc/`-c` payloads, breaking **all terminal commands**. This is a **P2 stability blocker** affecting core terminal-tool functionality. Duplicate reports suggest broad user touch.

**[#78647 — Epic: Shard all 20 god files** (10 comments)](https://github.com/NousResearch/hermes-agent/issues/78647)
> **Analysis:** The repo-wide refactoring epic currently targets 20 god files (e.g. `slack/adapter.py` at 9,088 lines, `discord/adapter.py` at 10,114 lines). This has spawned multiple child issues (#78634, #78638) and two companion PRs today (#79662, #79731). The community is actively driving this maintainability campaign.

**[#8576 — WhatsApp bridge npm vulnerabilities** (7 comments, 2 👍)]
> Closed today — the community's security concern was addressed.

**[#68927 — Desktop: after long tasks Enter reaches backend but bubble not rendered** (6 comments)](https://github.com/NousResearch/hermes-agent/issues/68927)
> **Analysis:** P2 Desktop UI regression — user inputs are being lost visually though they reach the backend. Related to session-state sync issues (#68876) also filed by the same user. Desktop UX reliability is a recurring community theme.

---

## 5. Bugs & Stability

Ranked by severity, the **newly reported or actively-updated bugs today**:

| Sev | Issue | Summary | Fix PR? |
|-----|-------|---------|---------|
| **P0** | [#79391](https://github.com/NousResearch/hermes-agent/issues/79391) | **Interrupted auto-compaction permanently deletes session history** — no summary, no archive, hard ID gap (explicit_interrupt) | ⚠ **None open** — urgent gap |
| **P1** | [#79624](https://github.com/NousResearch/hermes-agent/issues/79624) | **Gateway crashes exit(1) during preflight compaction on restart** — oversized session (98k+ tokens) kills the process | ✅ [#79741](https://github.com/NousResearch/hermes-agent/pull/79741) open |
| **P1** | [#79678](https://github.com/NousResearch/hermes-agent/issues/79678) | **`hermes update` re-detaches HEAD after successful pull** — silently discards the update | ✅ [#79734](https://github.com/NousResearch/hermes-agent/pull/79734) open |
| **P1** | [#78541](https://github.com/NousResearch/hermes-agent/issues/78541) (closed) | Telegram group/forum: suppressing normal final send **swallows complete replies** (stale content_delivered) | Closed — fixed |
| **P2** | [#77780](https://github.com/NousResearch/hermes-agent/issues/77780) | **lifecycle_guard crashes on `ValueError: embedded null byte`** — breaks all terminal commands | ⚠ **None open** — most-replicated bug, fix urgently needed |
| **P2** | [#68927](https://github.com/NousResearch/hermes-agent/issues/68927) | Desktop: after long tasks, Enter reaches backend but **user bubble not rendered**, text stays in composer | ⚠ None |
| **P2** | [#76901](https://github.com/NousResearch/hermes-agent/issues/76901) | **Termux installation script error** | ⚠ None — affects mobile users |
| **P2** | [#79562](https://github.com/NousResearch/hermes-agent/issues/79562) | WeChat/Weixin `/approve` text fallback stops working after first approval (timing race) | ⚠ None |
| **P2** | [#79677](https://github.com/NousResearch/hermes-agent/issues/79677) | QQ Bot cron deliveries **never render markdown** (hardcoded msg_type 0) | ⚠ None |
| **P2** | [#5254](https://github.com/NousResearch/hermes-agent/issues/5254) | Tool calls repeating/fragmenting with LM-Studio (long-standing since April, 6 comments) | ⚠ None — aging |

**Security advisories** — two PRs today address the same dependency-vulnerability surface:
- [#79618](https://github.com/NousResearch/hermes-agent/pull/79618): clears `uv audit` findings (cryptography 48.0.1 with 3 advisories), closes two regression paths
- [#79740](https://github.com/NousResearch/hermes-agent/pull/79740): bumps aiohttp, cryptography, brace-expansion, undici, electron (40→41)

**Critical gap warning:** The **P0 session-deletion bug** (#79391) — interrupted auto-compaction permanently destroying session history — has **no fix PR** yet. Given its severity (permanent data loss) and platform coverage (Windows + Desktop), this should be prioritized.

---

## 6. Feature Requests & Roadmap Signals

**Strong roadmap signals (with active PRs):**

1. **Self-contained desktop installers** — [#79599](https://github.com/NousResearch/hermes-agent/pull/79599): bundles agent source, uv, CPython, wheelhouse, node, prebuilt JS; no first-launch downloads. This is a **major distribution improvement** likely to land in the next release.

2. **Auto-title API sessions** — [#63672](https://github.com/NousResearch/hermes-agent/pull/63672): backports CLI/gateway session-titling to `/v1/chat/completions` and `/v1/runs`. Small but high-QoL for API users.

3. **Durable reconnectable runs for Desktop/Web Dashboard** — [#53839](https://github.com/NousResearch/hermes-agent/issues/53839): decouples chat lifecycle from live client transports. This addresses the recurring Desktop session-state complaints and is likely **being actively worked on** given the session-state sweep.

4. **/background inactivity timeout** — [#8298](https://github.com/NousResearch/hermes-agent/pull/8298) (open since April): adds configurable inactivity timeout to prevent stuck background tasks silently dropping results.

**Community-requested but no PR yet:**

5. **Multi-tenant isolation** — [#34352](https://github.com/NousResearch/hermes-agent/issues/34352): the most-commented open issue; requires architectural change (memory hooks). Maintainers marked `needs-decision`.

6. **Discord `disable_link_previews` toggle** — [#60942](https://github.com/NousResearch/hermes-agent/issues/60942): parity with Telegram's existing config option. Simple feature, likely to be picked up.

7. **Expose decoded Codex usage payload on account snapshots** — [#79695](https://github.com/NousResearch/hermes-agent/issues/79695): enables downstream billing/usage integrations.

8. **Long-running autonomy gaps tracker** — [#79686](https://github.com/NousResearch/hermes-agent/issues/79686): consolidates requests for retained subagents, goal gates, self-edit audit/rollback, session heartbeats, inline shell.

---

## 7. User Feedback Summary

**Pain points (recurring themes):**

- **Session data integrity is the #1 concern.** Users report: permanent history deletion on interrupted compaction (#79391), LIKE-wildcard session deletion (#79722 — fixed), oversized-session process crash (#79624), and compression runs that never complete (#79741 context). Trust in the session store is the biggest reliability friction.

- **Update process fragility.** "hermes update silently discards the update" (#79678) and the Vite `configLoader: 'native'` warning (#79664) suggest the self-update path is confusing and unreliable for users on detached/pinned checkouts.

- **Platform parity gaps.** macOS bash 3.2 compatibility (#57867 — fixed), Termux install failure (#76901), macOS immutable-flag profile deletion (#43339), WeChat approval races (#79562), and QQ Bot markdown absence (#79677) show the multi-platform story is not yet seamless.

- **Desktop UI sync issues.** Two related bugs filed by the same user (Enter-not-rendering #68927, provider-switch desync #68876) indicate the Desktop surface needs a session-state synchronization pass.

**Positive signals:**
- The community is **actively contributing** — many PRs today come from external contributors (ethernet8023, kshitijk4poor, Drexuxux, thatssoheil, etc.), suggesting a healthy contributor base.
- The **god-file decomposition epic** has strong community buy-in — multiple contributors volunteered shards.
- Security fixes are landing quickly (two dependency-audit PRs in one day).

---

## 8. Backlog Watch

Issues/PRs needing maintainer attention:

| Item | Age | Why it matters |
|------|-----|----------------|
| [#5254 — Tool calls repeating with LM-Studio](https://github.com/NousResearch/hermes-agent/issues/5254) | **~4 months** (since Apr 5) | Long-standing tool-call fragmentation bug affecting local-model users; 6 comments, no resolution. Same class of bug as openai/codex#7517. Directly impacts local/private LLM users — a key Hermes audience. |
| [#8298 — /background inactivity timeout](https://github.com/NousResearch/hermes-agent/pull/8298) | **~4 months** (since Apr 12) | PR is open with substantive bugfix value (background tasks silently drop results); needs review/merge. |
| [#8290 — Protect cron tick loop from cascading failures](https://github.com/NousResearch/hermes-agent/pull/8290) | **~4 months** (since Apr 12) | Companion PR: a single bad cron schedule can permanently disable a job (next_run_at = null). Low-risk fix, long idle. |
| [#34352 — Multi-Tenant Hermes](https://github.com/NousResearch/hermes-agent/issues/34352) | **~2 months** (since May 29) | Most-commented open issue (15), marked `needs-decision`. The author claims a production-grade solution exists — a strategic decision here could unlock a major use case. |
| [#15951 — doctor reports agent-browser missing when global](https://github.com/NousResearch/hermes-agent/issues/15951) | **~3 months** (since Apr 26) | Closed today, but highlights that `hermes doctor` only checks local node_modules — a small, user-friction-y diagnostic bug. |
| [#60942 — Discord disable_link_previews](https://github.com/NousResearch/hermes-agent/issues/60942) | **~1 month** (since Jul 8) | Simple parity feature (Telegram already supports it); likely a quick win for platform consistency. |

---

## Summary Assessment

**Project health: Strong but stressed.** Hermes Agent is iterating at exceptional velocity — critical session-integrity bugs are being found *and* fixed within the same day (P0 #79722 filed and merged). The maintainer team appears responsive, with P1/P2 fixes typically receiving PRs within hours. The top risks are: (1) the **unfixed P0 session-deletion bug** (#79391) with no open PR, (2) the **most-replicated lifecycle_guard crash** (#77780) with no fix, and (3) the **aging LM-Studio tool-call fragmentation** issue (4 months). The community is deeply engaged in both feature work (multi-tenancy, god-file sharding) and reliability work — confidence in the project's trajectory is high, pending the next release to consolidate today's large batch of merged fixes.

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw Project Digest — 2026-08-06

## 1. Today's Overview
The PicoClaw project shows a low-activity day with no new releases, no issues filed or updated in the last 24 hours, and no merged pull requests. Three pull requests remain open, all receiving recent updates, indicating ongoing collaborative work rather than stalled development. The most significant development is a fix for a broken `pnpm-lock.yaml` file that is blocking frontend builds, which was submitted yesterday and is awaiting review. A long-standing enhancement to add configurable model fallback chains (PR #3200) has progressed with a recent update, suggesting active iteration on this feature. Overall, the project appears to be in a maintenance and refinement phase with moderate community contribution momentum.

## 2. Releases
No new releases were published in the reporting window. The project has not shipped a new version in the past 24 hours; the most recent release history is not available from the provided data, and no changelog, migration notes, or breaking-change announcements were issued.

## 3. Project Progress
No pull requests were merged or closed in the last 24 hours. The three open PRs all received updates, indicating active development work in progress:

- **PR #3318** — A fix for `web/frontend/pnpm-lock.yaml`, which currently contains duplicate mapping keys (semver@7.8.5 listed twice) and causes `ERR_PNPM_BROKEN_LOCKFILE` errors. This is a critical build-blocking fix needed for all frontend contributors.
- **PR #3200** — Enhancement adding a configurable default model fallback chain, allowing users to set a default model, add fallbacks, reorder the chain, and persist the configuration through the backend API. The recent update suggests the author (lc6464) is actively refining this work.
- **PR #1951** — A long-running effort to migrate installation scripts from the separate `picoclaw_docs` repository into the main codebase, consolidating documentation-related build tooling.

## 4. Community Hot Topics
There is no significant community engagement in the reporting window — no new issues were filed, and none of the open PRs have accumulated reactions or comments beyond API-level metadata. The most active items by recency of update are:

- **[PR #3318: fix(web): repair unparseable pnpm-lock.yaml](https://github.com/sipeed/picoclaw/pull/3318)** — While not heavily commented, this PR addresses an urgent build blocker that affects any developer attempting to install or build the frontend. The need is clear: the project's frontend install workflow is broken, and maintainer review is required to unblock contributors.
- **[PR #3200: feat(models): add configurable default fallback chain](https://github.com/sipeed/picoclaw/pull/3200)** — This feature targets a common user need for resilient model invocation quality; the absence of community comments may indicate the PR is not yet widely known, but the capability is foundational for production deployments where a single model may be unreliable or rate-limited.

## 5. Bugs & Stability
One active issue impacts project stability:

- **Broken `pnpm-lock.yaml` (Web Frontend Install Failure)** — Severity: **High** (build-blocking for all frontend contributors and CI). The lockfile at `web/frontend/pnpm-lock.yaml` fails parsing due to a duplicated mapping key for `semver@7.8.5` in the `snapshots:` section. pnpm rejects the file with `ERR_PNPM_BROKEN_LOCKFILE`. Fix PR: **[#3318](https://github.com/sipeed/picoclaw/pull/3318)** is open but unmerged. Until merged, any fresh clone running `pnpm install` in the frontend directory will fail.

No other crashes, regressions, or runtime bugs were reported in the last 24 hours.

## 6. Feature Requests & Roadmap Signals
The following feature work is in flight and likely to land in a future release:

- **Configurable Default Model Fallback Chain (PR #3200)** — This is the most substantive roadmap signal. The feature adds a dedicated workflow on the models page (set default model, add fallbacks, reorder, save) and persists the chain via the backend API. This addresses a core reliability need for multi-model inference setups and is likely planned for inclusion in the next minor release.
- **Consolidation of Installation Scripts (PR #1951)** — Moving installation scripts from the docs repo into the main repo indicates a move toward self-contained, testable installation tooling, likely accompanying the next release to simplify onboarding.

No new feature requests were filed today. Given the recent update activity on PR #3200, expect that feature to be merged first, followed by the build fix (#3318) as a hotfix.

## 7. User Feedback Summary
Direct user feedback is sparse in this window (no new issues). However, the open PRs reveal underlying pain points:

- **Onboarding friction**: The broken lockfile (#3318) is a clear developer pain point — new contributors cannot run the frontend without manual workarounds. The project's health would improve by establishing CI lockfile validation.
- **Model reliability / degradation**: The fallback chain feature (PR #3200) addresses a real operational need: users require automatic failover between models to ensure service continuity. The dedicated UI for managing the chain suggests the team is prioritizing user-friendly configuration over raw config files.
- **Repo self-sufficiency**: The migration of install scripts (PR #1951) signals that users were confused by split documentation/installation locations, and the project is responding by centralizing essential operational knowledge.

Overall, sentiment appears neutral-to-positive — contributors are actively working on improvements, but the broken lockfile is causing avoidable friction.

## 8. Backlog Watch
The following items require maintainer attention:

- **[PR #1951: chore: move installation scripts from docs repo to here](https://github.com/sipeed/picoclaw/pull/1951)** — Open since 2026-03-24 (over 4 months), this PR has not been merged or closed. Its long dormancy blocks the project from achieving self-contained installation documentation. This should be either merged, or explicitly closed with a rationale, as it affects onboarding discoverability.
- **[PR #3200: feat(models): add configurable default fallback chain](https://github.com/sipeed/picoclaw/pull/3200)** — Open since 2026-07-01 and receiving intermittent updates. Maintainer review is needed to ensure this feature lands before it goes stale; the design is complete and it has clear user value.

No issues are pending maintainer response at this time.

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw Project Digest - 2026-08-06

## 1. Today's Overview

NanoClaw shows steady, active development with a strong focus on channel integration robustness, container-environment improvements, and skill ecosystem expansion. The project saw 10 pull requests updated in the last 24 hours (1 merged, 9 open), indicating a healthy flow of community contributions and active maintainer engagement. Two long-standing issues—one from May and one from April—received new attention, suggesting ongoing triage of backlogged concerns. The majority of activity clusters around fixing infrastructure stability (WhatsApp session hangs, MCP server environments, attachment handling) and adding new utility skills. No releases were published today, so recent improvements are not yet in any stable release channel.

## 2. Releases

None in the last 24 hours.

## 3. Project Progress

One pull request was merged/closed during this window:

- **[#3187 - fix(agent-runner): disallow built-in SendMessage so agent-to-agent messaging works](https://github.com/nanocoai/nanoclaw/pull/3187)** — Merged. This fix addresses a critical interop issue: the built-in `SendMessage` tool was interfering with agent-to-agent messaging. By disallowing the built-in variant, the agent-runner now permits proper agent-to-agent communication, which is fundamental to multi-agent workflows.

Beyond the merge, multiple open PRs show meaningful forward progress with updated activity today:

- **#3156 (fix):** Carrying channel attachments (e.g., images, PDFs) to providers as structured parts — actively updated, likely paired with the #2528 bug report.
- **#3186 (refactor):** Adding host seams for skill-owned capabilities — architectural improvement to separate host vs. container responsibilities.
- **#3172 (chore):** Removing stale qodo and Google MCP skills — cleanup of outdated integrations.
- **#3191 (fix):** WhatsApp channel session timeout to prevent host startup hangs — directly addresses a user-facing stability bug.

## 4. Community Hot Topics

Both currently open issues received fresh comments today, indicating renewed maintainer or community attention:

- **[#2528 - Signal channel: image/PDF attachments unreachable from agent container](https://github.com/nanocoai/nanoclaw/issues/2528)** — Revived with new activity. This bug breaks a core user workflow (sending images to the agent for analysis). Note the related open PR #3156 focused on carrying channel attachments as structured parts is likely targeted at this exact issue, suggesting a coordinated fix effort in flight.

- **[#2006 - Fresh install on Debian 12 LXC: docker socket permission denied](https://github.com/nanocoai/nanoclaw/issues/2006)** — Two-month-old high-friction install blocker. The setup path adds the user to the `docker` group but fails to apply the new group membership within the same session, so subsequent steps can't access the Docker daemon. These installation pain points have outsized impact on first-time adoption and were given attention again today.

## 5. Bugs & Stability

Ranked by severity:

1. **High — Docker socket permission denied on fresh Debian 12 LXC installs** ([#2006](https://github.com/nanocoai/nanoclaw/issues/2006)): Complete blocker for installation on a common configuration (Debian 12 + LXC in Proxmox). The recovery path reportedly "doesn't fire," making this a first-run funnel problem. Growing in age (April 25) without a fix PR attached.

2. **High — Signal attachments unreachable from agent container** ([#2528](https://github.com/nanocoai/nanoclaw/issues/2528)): File attachments (images/PDFs) arrive at the host but cannot be read from inside the agent container. Directly disrupts core agent capabilities on Signal. Fix appears in-flight via PR #3156.

3. **Medium — WhatsApp session log-out hangs host startup** (PR [#3191](https://github.com/nanocoai/nanoclaw/pull/3191)): An unbounded promise in `WhatsApp ChannelAdapter.setup()` waits forever for a connection-open event that will never fire for logged-out sessions, preventing host startup. A fix PR was submitted and is open—this is actively being addressed.

4. **Medium — MCP servers spawned with bare environment** (PR [#3188](https://github.com/nanocoai/nanoclaw/pull/3188)): Stdio-spawned MCP servers miss proxy and CA-trust variables, breaking them in containerized or enterprise network setups. Fix open.

5. **Medium — Agent-to-agent messaging broken by built-in SendMessage** ([#3187](https://github.com/nanocoai/nanoclaw/pull/3187)): **Resolved** by merge today.

6. **Low — Unknown slash commands cause silent response drops** ([#2346](https://github.com/nanocoai/nanoclaw/pull/2346)): The formatter misclassified unknown slash commands as `passthrough`, causing the Agent SDK to produce output without `<message>` blocks that silently vanished. Open fix PR awaits review. Still, users may observe silent failures with unsupported slash commands.

## 6. Feature Requests & Roadmap Signals

Several PRs signal where the ecosystem is heading:

- **New skill submissions are accelerating.** Three of the ten PRs today are new utility skills: **Tavily MCP tool skill** ([#3190](https://github.com/nanocoai/nanoclaw/pull/3190)), **add-why—explain what happened to one message** ([#3189](https://github.com/nanocoai/nanoclaw/pull/3189)), and a **Dial channel integration** ([#3050](https://github.com/nanocoai/nanoclaw/pull/3050)). This indicates the skill builder ecosystem is becoming a primary extension vector, and the team is actively supporting external skill contributions.

- **Multi-agent and A2A patterns are emerging as a focus area.** The #3187 merge (agent-to-agent messaging fix) alongside early refactoring PRs (host seams for skill-owned capabilities, #3186) suggests architecture is stabilizing to support more complex multi-agent workflows in the next release.

- **Channel robustness is a recurring theme.** WhatsApp timeouts, Signal attachments, and new channel additions (Dial) suggest channel count is expanding while quality hardening of existing channels is the near-term blocking priority.

- **Environment-parity work** (MCP env vars, host seams) points at the team preparing the container/host boundary for richer integrations ahead of the next stable release.

## 7. User Feedback Summary

User pain points from this window:

- **Attachment handling is unreliable across channels.** Image/PDF attachments sent over Signal are unusable by the agent (issue #2528). A user's core ask—*"can you see this image?"*—fails with the current setup. This is likely generalized beyond Signal to all media-rich channels given the PR work in the agent-runner.

- **Fresh installs on Debian/LXC remain brittle.** A user on a clean Debian 12 LXC reports a Docker-permission failure with no recovery path. First-time users on Proxmox LXC setups are overrepresented in installation bug reports, suggesting this path needs automation attention in the installer itself.

- **Users rely on chat channels for multimodal workflows.** The bug reports (images, PDFs in containers) confirm users are sending media for the agent to process, not just text. This usage pattern is core to the project's value proposition and is a priority area for reliability.

Overall satisfaction appears high when channels work correctly, but frustration concentrates on two moments: first install and file-bearing messages.

## 8. Backlog Watch

Items that need maintainer attention:

- **[#2006 - Fresh Debian 12 LXC: docker socket permission denied](https://github.com/nanocoai/nanoclaw/issues/2006)** — 104 days old, opened April 25. This is the oldest active bug and a first-run blocker. A fix PR does not exist. Requires visibility from core maintainers.

- **[#2528 - Signal channel attachments unreachable in container](https://github.com/nanocoai/nanoclaw/issues/2528)** — 81 days old, opened May 18. Fix PR #3156 has been open for seven days; needs review and merge.

- **[#2346 - Unknown slash commands dropped silently](https://github.com/nanocoai/nanoclaw/pull/2346)** — Open since May 8, updated today. This fix closes a silent-failure mode. It has been waiting ~90 days for review.

- **[#3050 - Dial channel integration](https://github.com/nanocoai/nanoclaw/pull/3050)** — Open since July 14 (23 days). A sizable feature PR that includes wizard and skill changes; otherwise healthy, but needs active maintainer review to keep momentum.

**Overall:** NanoClaw is a healthy, actively maintained project with strong community contribution flow. The critical path is clearing the review backlog on stability-focused PRs, which are currently blocking fixes for user-facing bugs in channels and installs.

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

# NullClaw Project Digest
**Date:** 2026-08-06  
**Period:** 2026-08-05 → 2026-08-06

---

## 1. Today's Overview

NullClaw is in a low-activity but focused development phase. No new issues were opened or updated in the last 24 hours, and no releases were published. The project's momentum is concentrated entirely in two open pull requests, both authored by `raskevichai` and both targeting critical runtime stability concerns: one addresses a stack-size misconfiguration in the agent turn loop, and the other fixes a structural flaw in the supervisor that causes Telegram/Matrix channels to silently go silent. While the issue queue is empty, the presence of two substantive, root-cause-driven PRs suggests maintainers are actively working through a backlog of technical debt rather than iterating on user-facing features.

---

## 2. Releases

No new releases were published in the last 24 hours. The most recent release remains unchanged; users should continue using existing binaries or build from `main`.

---

## 3. Project Progress

No PRs were merged or closed in the last 24 hours. However, two significant open PRs are awaiting review/merge:

- **[#985 — fix(runtime): give the agent turn path a 16 MiB stack](https://github.com/nullclaw/nullclaw/pull/985)** — Fixes a root-cause issue where `SESSION_TURN_STACK_SIZE` was incorrectly aliased to `HEAVY_RUNTIME_STACK_SIZE` (2 MiB), leading to potential stack overflows in `SessionManager.processMessage*()` and `Agent.turn()`. The fix scales the turn-path stack to 16 MiB.
- **[#984 — fix(channels): let poll failures age out a dead polling thread](https://github.com/nullclaw/nullclaw/pull/984)** — Addresses a structural blind spot in `supervisionLoop` that prevented the supervisor from detecting and restarting dead polling threads in Telegram and Matrix channels after prolonged idle periods.

Both PRs close long-standing issues (#976 and #972 respectively), indicating that previously reported stability bugs are being actively resolved.

---

## 4. Community Hot Topics

There are currently **no Issues** open in the repository, and both active PRs have zero comments and zero reactions. This indicates either:

- The community is small and conversation happens elsewhere (e.g., Discord, Matrix),
- Or the maintainers are operating in a ticketing model where discussion is internal.

The two open PRs are the only items generating activity. Because they address user-facing failures (silent channels, potential crashes), these are likely the topics with the most implicit community interest, even if tacit.

---

## 5. Bugs & Stability

Two stability issues are addressed by the open PRs, ranked by severity:

1. **[High] Silent channel death (Telegram/Matrix) — PR #984 closes #972**  
   Channels go quiet after idle periods; only a full gateway restart restores functionality. This is a production-critical bug for any user relying on asynchronous channel polling. The PR fixes the supervisor's failure detection logic so dead polling threads age out and are restarted.

2. **[Medium] Stack overflow risk in agent turn path — PR #985 closes #976**  
   The agent turn path was sized at 2 MiB (aliased to the heavy runtime stack), which is insufficient for deep recursion or complex agent processing. The PR raises this to 16 MiB, preventing intermittent crashes (likely stack-overflow segfaults) during agent turns.

Both are actively addressed by open PRs; no new bugs were reported in the last 24 hours.

---

## 6. Feature Requests & Roadmap Signals

No explicit feature requests were opened or updated in the last 24 hours. The signal from the current PRs is not feature-focused but stability-oriented.

**Prediction for next release:** Given the focus on runtime robustness (stack sizing and supervision loop correctness), the next version of NullClaw will likely include:

- More generous and configurable stack sizing for agent execution paths,
- A hardened supervisor that correctly detects and recovers from dead polling threads,
- Possible adoption of a more defensive runtime configuration pattern (e.g., avoiding aliasing constants for unrelated purposes).

No new user-facing features are signaled in this window.

---

## 7. User Feedback Summary

There were **no new user comments, reactions, or issue reports** in the last 24 hours. Inferred pain points from the current PRs:

- **Reliability dissatisfaction:** Users experiencing silent channel failures (Telegram/Matrix) after idle periods likely face significant operational disruption, especially in always-on assistant deployments.
- **Stability expectations:** The stack-size fix suggests users or the maintainer encountered intermittent crashes during complex agent turns, implying usage scenarios are pushing the current default limits.

Satisfaction signals are neutral—no complaints, no praise—but the existence of PRs closing long-standing bugs suggests maintainers are responsive to reported issues.

---

## 8. Backlog Watch

**None.** The issue queue is empty. Both open PRs are recent (August 5) and belong to the same author; they are actively maintained and not stale. There are no unanswered issues or abandoned PRs requiring maintainer attention.

**Note:** While the issue queue being empty is positive, it may also reflect a limited community reporting structure. If issues are being logged elsewhere or not at all, maintainers may want to consider a more visible feedback channel (e.g., discussion forum, Discord bot, or inline feedback widget) to surface user needs.

---

*Digest generated from GitHub data retrieved 2026-08-06. All linked items are from the NullClaw repository.*

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw Project Digest — 2026-08-06

## 1. Today's Overview

IronClaw is deep into its **v1.1.0 release candidate cycle**, with `1.1.0-rc.1` shipped three days ago and the team actively stabilizing through bug-bash QA, CI fixes, and architecture refactoring. Activity is **very high**: 43 issues and 50 PRs touched in the last 24 hours, with ~24% of issues closed and ~42% of PRs merged or closed. The main themes are **extension reach** (MCP server registration, IronHub marketplace integration), **skills infrastructure** (DB-backed skill mounting, model-driven skill selection), and **web UI/UX polish** (composer focus fixes, dead code removal). Multiple bug-bash P1/P2 issues from a Railway QA instance indicate the project is in an aggressive test-and-fix loop leading up to the next RC. The codebase is also undergoing significant decomposition (a 6,400-line file flagged) and architectural consolidation (standardized messaging framework, capability policy unification).

---

## 2. Releases

### ironclaw-v1.1.0-rc.1 — 2026-08-03

- **Extension reach** — registering arbitrary hosted MCP servers
- **IronHub deep link installation** — install extensions via deep links
- **Durable file attachments** — attachments that persist across channels
- **Slack `/ironclaw` slash commands**
- Broad pass on making failures more legible

**No breaking changes or migration notes** were listed in the release notes. The RC is actively being validated; a backport PR (#7260) patches MCP egress and readable log fixes onto the release branch.

---

## 3. Project Progress

**Merged/closed PRs today (21 total)** focused on:

| Area | Key PRs |
|---|---|
| **Release hardening** | [#7256](https://github.com/nearai/ironclaw/pull/7256) — lossless 1.0→1.1 startup migration preserving threads, routines, channel bindings, extensions, and ledgers. [#7260](https://github.com/nearai/ironclaw/pull/7260) — backport of MCP egress + readable-log fixes to the RC branch. |
| **Migration / state preservation** | [#7256](https://github.com/nearai/ironclaw/pull/7256) as above; also a large batch of work-slice closures [#7258](https://github.com/nearai/ironclaw/pull/7258) spanning WS5/WS6/WS8/WS10 and both crate dissolutions. |
| **Coding tools** | [#7133](https://github.com/nearai/ironclaw/pull/7133) — bounded JSON file queries (explicit file paths, JSONPath `$` roots). [#7227](https://github.com/nearai/ironclaw/pull/7227) — keep readable text logs writable after read-before-edit checks. |
| **Architecture decomposition** | [#7258](https://github.com/nearai/ironclaw/pull/7258) — 7-slice batch closing workspace slices and dissolving crates toward the target architecture. |
| **E2E coverage** | [#7056](https://github.com/nearai/ironclaw/issues/7056) — automation lifecycle E2E (create → rename → pause → resume → delete) across the real API. |

**Open PRs in flight** — the top priority open PRs include: **standardized messaging framework** ([#6831](https://github.com/nearai/ironclaw/pull/6831)) defining 16 canonical host operations; **explicit channel delivery tool** ([#7157](https://github.com/nearai/ironclaw/pull/7157)) with a two-lane model (conversation lifecycle + notification lanes); **skills DB-backed tree** ([#7171](https://github.com/nearai/ironclaw/pull/7171)) so installed skills actually persist and run.

---

## 4. Community Hot Topics

The most active discussions (by comments/reactions) reveal three underlying drivers: **declarative configuration**, **extension discoverability**, and **skills trust**:

1. **#3036 — Configuration-as-Code Epic** (7 comments, 1 👍) — [link](https://github.com/nearai/ironclaw/issues/3036)
   Tenants want a schema-driven, auditable way to configure IronClaw instead of hand-editing `.env`, settings JSON, and runtime flags. This has been open since **April** and is marked `reborn` — a strong signal it's a long-lived architectural priority that may land post-1.1.

2. **#7194 — Admin-allowed shared channel as outbound delivery target** (3 comments) — [link](https://github.com/nearai/ironclaw/issues/7194)
   Agents can post to channels but cannot designate them as outbound delivery targets — a gap between agent capability and host routing that frustrates multi-channel workflows.

3. **Multiple bug-bash issues from the same QA instance** (each 1 comment, but high density):
   - #7249 — Slack DM result delivered to Telegram [link](https://github.com/nearai/ironclaw/issues/7249)
   - #7251 — agent *guesses* MCP auth type instead of discovering it [link](https://github.com/nearai/ironclaw/issues/7251)
   - #7246 — agent hallucinates automation status ("running") when state is actually "empty" [link](https://github.com/nearai/ironclaw/issues/7246)
   - #7247 — agent falsely claims GitHub is already connected [link](https://github.com/nearai/ironclaw/issues/7247)

   **Underlying need**: the model layer needs honest, verified state reporting — agents must check, not assume. This is the strongest thematic signal of the week.

---

## 5. Bugs & Stability

Ranked by severity (P1 = critical, P2 = significant):

| Severity | Issue | Description | Fix PR? |
|---|---|---|---|
| **P1** | [#7246](https://github.com/nearai/ironclaw/issues/7246) | Agent hallucinates automation status; claims an automation is running when none exists | ❌ None yet |
| **P1** | [#7247](https://github.com/nearai/ironclaw/issues/7247) | Agent falsely claims GitHub is connected without verifying auth; next GitHub call fails | ❌ None yet |
| **P2** | [#7248](https://github.com/nearai/ironclaw/issues/7248) | Invalid custom MCP endpoint accepted, then poisons the run — agent loops on tool discovery | ✅ [#7253](https://github.com/nearai/ironclaw/pull/7253) — keep registration definition-only, no installation/activation |
| **P2** | [#7249](https://github.com/nearai/ironclaw/issues/7249) | Slack DM execution result delivered to Telegram with Slack-specific metadata | ❌ None yet |
| **P2** | [#7250](https://github.com/nearai/ironclaw/issues/7250) | DeepWiki MCP reports misleading auth guidance on network errors | ❌ None yet |
| **P2** | [#7251](https://github.com/nearai/ironclaw/issues/7251) | Agent asks user to guess MCP auth type instead of discovering/initiating auth | ❌ None yet |
| **—** | [#6257](https://github.com/nearai/ironclaw/issues/6257) | `Invalid value (attachments.mime_type)` when sending/generating PDFs — reported via product feedback | ❌ Unknown |
| **—** | [#7254](https://github.com/nearai/ironclaw/issues/7254) | Cannot access files attached to Slack feedback threads | ❌ Unknown |
| **—** | [#7209](https://github.com/nearai/ironclaw/issues/7209) | CI regression gate cannot see `node:assert` style — wrongly fails valid frontend PRs | ❌ Open |

**Notable cross-cutting theme**: the bug-bash cluster (#7246–#7251) all come from a single Railway QA instance and share a root cause — **agents fabricating state instead of verifying it**. That is a systemic reliability issue for the 1.1 RC.

---

## 6. Feature Requests & Roadmap Signals

Strong roadmap signals for **post-1.1** (likely 1.2 or later):

| Signal | Signal Strength | Notes |
|---|---|---|
| **Configuration-as-Code** (#3036) | ★★★★★ | Epic open since April; `reborn`-tagged; no PR yet. Likely the next big architectural push. |
| **IronHub marketplace integration** (#6731, tagged `v1.1.0`) | ★★★★☆ | Already partially in RC-1 (deep-link install); the full marketplace (discover/install at runtime, signed & provenance-checked) is still in flight. |
| **Storybook + AI-first Design System** (#7038, `suggested_P0`) | ★★★★☆ | Full proposal package (PR #7257); design-system governance is being set up. Likely lands after web-UI stabilization. |
| **Web Debug Inspector** (#7218) | ★★★☆☆ | Operator-only `?debug=true` views for prompt construction, model usage, tool execution. Fresh epic (Aug 5). |
| **Admin-Managed Agents as UserId Subjects** (#6578) | ★★★☆☆ | Epic for tenant-admin non-human subjects (automations, inbound channels, delegated integrations) without a second identity hierarchy. |
| **Skills self-creation/selection** (#6941, tagged `v1.1.0`) | ★★★★★ | Multi-PR stack already in flight (#6745, #6938, #7171). This is *the* active epic right now. |

**Prediction**: the **skills** epic is the nearest to completion (multiple XL PRs open), and the **MCP registration definition-only** fix (#7253) will land in the next RC. The **config-as-code** epic will be scoped after 1.1 stabilizes — it is the biggest architectural debt item.

---

## 7. User Feedback Summary

**Pain points (direct from users via Slack/product feedback):**

- **PDF attachments break** — `Invalid value (attachments.mime_type)` prevents sending/generating PDFs (reported via #x-ai-product-feedback, tracked in #6257). ⚠️ This is a file-format edge case that shipped in the multi-type attachment work.
- **Slack feedback-thread files unreadable** — the triage workflow cannot download/read files attached to Slack feedback threads (#7254). Breaks a supported feedback loop.
- **Cross-channel delivery confusion** — Slack DM results appearing in Telegram (#7249) is a delivery-routing bug that erodes trust in multi-channel setups.
- **Agent dishonesty about state** — repeated P1 reports of the agent claiming things ("GitHub connected", "automation running") that are not true. This is the single most corrosive UX failure for trust in an autonomous agent.

**Positive signal**: the release-candidate cadence, active bug-bash, and fast backport of fixes to the RC branch indicate a responsive maintainer team.

---

## 8. Backlog Watch

Issues needing maintainer attention (long-unanswered, high-impact, or stale):

| Issue | Age | Why it matters |
|---|---|---|
| **#3036 — Config-as-Code epic** | 3.5 months (since Apr 28) | Still open, no implementation PR despite 7 comments and being `reborn`-tagged. High architectural leverage. |
| **#741 — Bedrock streaming via `converse_stream()`** | 5 months (since Mar 8) | Closed today — but was open since March; streaming parity for AWS Bedrock is a competitive feature. (Closed as part of today's cleanup? Verify.) |
| **#5598 — `chore: release` (ironclaw_common 0.5.0, ironclaw_skills 0.4.0)** | 1 month+ (since Jul 3) | Open release PR with **breaking API changes** (`copy_impl_added`, `enum_variant_added`). If this has been sitting for a month, downstream crates are blocked on breaking-change migration. |
| **#6892 / #6394 — previous dogfooding epics** | 1–2 weeks stale, closed today | Closed — good hygiene; but they indicate recurring QA cycles are the norm, not the exception. |
| **#7231 — Reviews that say "APPROVE" but never submit GitHub approval** | 1 day | Real workflow hazard: PRs appear approved but stay merge-blocked. This is a process/tooling defect in the review pipeline. |

**Maintainer attention needed most on**: #5598 (stale release PR with breaking changes), #6257 (PDF mime-type bug, affects real users), and the cluster of P1/P2 state-honesty bugs (#7246, #7247) — these are release-blocker candidates for RC-2.

---

## Project Health Assessment

| Dimension | Status |
|---|---|
| **Velocity** | 🟢 Very high — 50 PRs + 43 issues touched in 24h |
| **Release maturity** | 🟡 RC-1 shipped; active bug-bash with multiple P1s still open |
| **Architecture discipline** | 🟢 Strong — decomposition trackers, frozen doc boundaries (#7259), canonical contracts (#6831) |
| **User trust** | 🔴 Agent state-honesty issues (P1 cluster) need urgent attention |
| **Process hygiene** | 🟢 Good — epics closed, coverage gaps tracked, backports flowing |

**Bottom line**: IronClaw is shipping fast and iterating on real feedback, but the **agent-honesty bug cluster** is the top risk to 1.1 RC quality. The skills epic remains the most significant feature investment, and config-as-code is the clear next architectural horizon.

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

# LobsterAI Project Digest - 2026-08-06

## 1. Today's Overview
LobsterAI is in a high-velocity release cycle with a strong focus on stability hardening and activity feature polish. The project shipped a new release (2026.8.5) featuring a native daily check-in experience and enterprise-scoped auth isolation. Twelve pull requests were merged or closed today, including critical fixes for window lifecycle hangs, OpenClaw gateway lock poisoning, and system prompt deduplication issues. Three open issues remain, with two newly filed bugs around prompt injection duplication and skill toggle mismatches. Overall, the project shows a healthy balance of feature development, bug fixing, and infrastructure dependency maintenance.

## 2. Releases
**LobsterAI 2026.8.5** (released 2026-08-05)

Key changes:
- **New daily check-in experience**: Native activity check-in UI added to the renderer
- **Enterprise auth isolation**: Account-scoped authentication and service flows separated from the main application, enabling better multi-tenant deployments
- **Style updates**: Miscellaneous visual refinements

No breaking changes or migration notes were included in the release notes. The release was authored by `btc69m979y-dotcom` (PR #2408) and `liuzhq1986` (PR #2409).

## 3. Project Progress
Twelve PRs were merged or closed today, spanning both feature work and fixes:

**Activity & Campaign Features:**
- **Startup credit poster improvements** (PRs #2432, #2433, #2438, #2439): Removed white gutters, added close icon to poster, disabled final reward auto popup, refined claim failure messaging, and refreshed campaign binding on retry
- **Title-bar conversation search** (PR #2435): Added a search button beside the artifact panel toggle, reusing the sidebar search workflow with responsive styling

**Stability & Reliability Fixes:**
- **Window lifecycle hardening** (PR #2437): Server shutdown now uses a drain timer plus hard deadline to prevent lingering keep-alive sockets from stalling app quit; main window activation is gated on first render
- **OpenClaw gateway lock poisoning fix** (PR #2436): Two races that left corrupted lock files (causing 30s gateway respawn failures) were fixed—one from force-killing mid-write, one from gateway-initiated restart races

**Dependency Maintenance:**
- Bumped cross-env to 10.1.0, react-dom to 19.2.4, and vite to 8.0.9 (PRs #1279, #1280, #1281) via Dependabot

The volume and mix of merged PRs indicate a well-maintained codebase with active community contribution alongside core team work.

## 4. Community Hot Topics
The most actively discussed items today are newly filed bugs from user `fujingzhai`:

- **Issue #2440 — System prompt duplication (new, zero comments yet)**: A detailed analysis showing the desktop client injects a 4,425-character `[LobsterAI system instructions]` block where 78% is verbatim duplicate of `AGENTS.md`. This points to a prompt-bloat problem that could degrade model performance and increase token costs.

- **Issue #2441 — Skill toggle silent failure (new, zero comments yet)**: A two-part report: (1) a reproducible bug where skill toggles are written by directory name but OpenClaw matches by frontmatter `name`, causing silent toggle failure, and (2) a design gap where `openclaw.json` gets fully overwritten with no persistent user configuration surface.

The lack of comments on these issues suggests they were filed very recently (today), but their specificity and reproducibility indicate an experienced user deeply familiar with the codebase. The underlying need is improving the desktop client's configuration model to be more transparent and user-controllable.

## 5. Bugs & Stability
**High Severity:**
- **Issue #1200/PR #1201 — NIM teamTypeNum hardcoded incorrectly (stale, 4 months old)**: `fetchTeamName` passes wrong type numbers for V2NIM SDK enums, causing group names to fail in both super teams and normal groups when @-mentioned. A one-line fix PR (#1201) exists but remains open. This is the oldest unresolved bug.

**Medium Severity:**
- **Issue #2441 — Skill toggle silent failure**: Toggle config written under directory names but resolved by frontmatter name means users believe skills are disabled when they're actually still active. No fix PR yet.

**Low-Medium Severity:**
- **Issue #2440 — System prompt duplication**: Prompt bloat wastes tokens and potentially degrades instruction clarity. No fix PR yet.

**Fixed Today (high severity):**
- Gateway lock poisoning (PR #2436) and window shutdown hangs (PR #2437) were both proactively fixed before affecting end users.

## 6. Feature Requests & Roadmap Signals
The following signals indicate where the project may be heading:

- **Enterprise multi-account isolation** (PR #2409 in release): The auth/service flow separation suggests enterprise deployment is becoming a priority—expect further enterprise features (SSO, org-scoped configs) in upcoming releases.
- **Native activity gamification** (PR #2408): The daily check-in and startup credit campaigns with reward flows indicate an active focus on user engagement. The World Cup reward poster work (#2432) shows seasonal/sports-adjacent campaigns.
- **Conversation UX improvements** (PR #2435): Title-bar search indicates a workflow-quality push for power users navigating many conversations.
- **User-configurable prompt management**: Issues #2440 and #2441 both demand a user-facing surface to control what goes into system prompts—this is a strong candidate for a near-term feature (likely a "prompt management" or "configurable AGENTS.md" panel).

## 7. User Feedback Summary
Today's feedback comes from `fujingzhai`, whose two bug reports reveal real pain points:

- **Power users are hitting prompt-blown limits**: "There is no way for users to persistently reduce the system prompt injected into every new conversation." This is a sign the default prompt is too verbose or redundant for advanced usage.
- **Configuration visibility matters**: The skill toggle bug shows users aren't just okay with toggles that "mostly work"—they need deterministic, inspectable configuration. The `openclaw.json` being overwritten is seen as a loss of control.
- **The project lacks a persistent "minimal" config path**: Users want a way to prune default instructions without fighting the tool.

No direct satisfaction signals (positive or negative) other than the level of detail in the bug reports, which suggests users are technically engaged and invested in improving the product.

## 8. Backlog Watch
- **Issue #1200 / PR #1201 — NIM teamTypeNum bug (open since 2026-04-01)**: The oldest unresolved item. A one-line fix is ready in PR #1201 but hasn't been merged for 4 months. This should be a priority—the fix is trivial, low-risk, and affects group messaging reliability in cloud messaging scenarios.

- **Dependabot PRs #1279-1281 (open since 2026-04-02)**: React 19 and Vite 8 are major version bumps that were closed today after 4 months of staleness. Their long shelf life suggests maintainer caution around major dependency upgrades—worth checking if they were merged or closed without merge.

- **No other long-unanswered items** observed in the active dataset; the project appears responsive to new issues within the same day.

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

# CoPaw Project Digest
**Date: 2026-08-06**

---

## 1. Today's Overview

CoPaw is exhibiting high-velocity development activity this cycle, with **50 PRs updated (21 merged/closed)** and **23 issues updated (6 closed)** in the past 24 hours. The project is processing a significant volume of community contributions; notably, 3 of the 12 recently authored PRs are from first-time contributors, indicating healthy external engagement. The backlog is heavily focused on **stability fixes** — WeChat channel bugs, desktop/PyInstaller packaging regressions in the 2.1.0-beta.1 release, and a series of provider-level retry/logic issues are dominating the issue tracker. No new release was cut today, but the volume of merged fixes (including a large LLM fallback feature) suggests a consolidation release is imminent.

---

## 2. Releases

No new releases were published in the last 24 hours. The most recent tagged version remains **v2.1.0-beta.2**, which is currently the subject of several open bug reports (see Bugs & Stability).

---

## 3. Project Progress

Despite no release, significant code has merged, driving feature completion and bug fixes.

**Major Features Merged:**
- **[LLM Model Fallback System (#5597, #5598):** The long-running feature for per-agent and global LLM model fallback has finally closed. With "safe retry boundaries," the system will automatically switch to a configured backup model list after exhausting retries on transient/permission failures. This was a two-part PR including the backend logic and the Console UI configuration panel.

**Stability & Fixes:**
- **[fix: Force relay `reasoning_content` for DeepSeek (#6675):** A high-impact fix addressing upstream API rejections (`400`) in multi-turn conversations when context compaction strips historical thinking blocks. The fix forces the relay of `reasoning_content` for DeepSeek thinking-mode APIs.
- **[fix(channel): Yield failed AgentResponse (#5447):** Fixes the console channel leaving the UI in a perpetual "waiting" state when a model or runtime error occurs (e.g., `ModelQuotaExceededException`). This has been merged, preventing UI lock-ups.
- **[feat(privacy): Audit visibility for sensitive directory exclusion (#6713):** Merged to add audit logs for when the router excludes sensitive directories.
- **[fix(router): Retry logic refinement (#3874):** A long-standing PR refining model retry logic has been closed.

**On-Going Work (Highlights):**
- **[Unify App Market Listings (#6718):** Closed (but not merged), likely ready for integration.
- **[Unify Provider Discovery (#6302):** Still open; a massive PR unifying provider discovery, model metadata, and routing. This is a core architecture shift.

---

## 4. Community Hot Topics

The following Issues and PRs drew the most attention and discussion this cycle.

- **[Issue #6684: [Feature]: 增加频道的重试功能 (Add channel retry feature)]** (4 comments, Open)
  - *Link:* [agentscope-ai/QwenPaw Issue #6684](https://github.com/agentscope-ai/QwenPaw/issues/6684)
  - *Analysis:* Users using custom Matrix servers face race conditions where QwenPaw auto-starts faster than the external service. The lack of automatic retry or health checks forces manual re-saves after every boot. This highlights a need for more robust channel resilience and handle health validation.

- **[Issue #6436: The Right Model for Every Message: Automatic Model Routing]** (3 comments, Open)
  - *Link:* [agentscope-ai/QwenPaw Issue #6436](https://github.com/agentscope-ai/QwenPaw/issues/6436)
  - *Analysis:* A high-level feature desire to route requests dynamically (small/local models for simple tasks, vision models for images). This ties directly into the massive "Unify Provider Discovery" PR (#6302), suggesting the community is eager for smarter, automated model orchestration beyond static pinning.

- **[Issue #6480: `execute_shell_command`: shell process detached via &/nohup never returns to idle]** (2 comments, Open)
  - *Link:* [agentscope-ai/QwenPaw Issue #6480](https://github.com/agentscope-ai/QwenPaw/issues/6480)
  - *Analysis:* A confusing UX bug where launching background processes (`nohup`/`&`) via the agent hangs the agent thread, preventing it from returning to an idle state. This blocks a common use case of starting long-running daemons.

---

## 5. Bugs & Stability

The project is seeing a surge in stability reports affecting various channels and platforms.

| Severity | Bug | Description | Fix Status |
| :--- | :--- | :--- | :--- |
| **Critical** | **[Bug #6697: `PYTHONHOME` injection crashes Python subprocesses]** | v2.1.0b1 desktop injects `PYTHONHOME` into child env, causing every Python subprocess to crash with `encodings ModuleNotFoundError`. Breaks the core functionality of agents running code. | **No fix PR yet.** |
| **Critical** | **[Bug #6675 (Merged): DeepSeek reasoning-content relay failure]** | 400 errors on multi-turn conversations when historical thinking blocks are stripped during compaction. | **Resolved** by [PR #6675](https://github.com/agentscope-ai/QwenPaw/pull/6675). |
| **High** | **[Issue #6696: WeChat context_token consumed by typing indicator]** | The one-time token is used for both the "typing" indicator and sending replies, causing `ret=-2` rejection and a stuck "working" indicator. (Also related to [Issue #6695](https://github.com/agentscope-ai/QwenPaw/issues/6695) which prevents approval prompts entirely) | **No fix PR yet.** |
| **High** | **[Issue #6722: Background subagent reports completed on failure]** | A forked background subagent reports success even when the worktree finalization fails (due to rejected Git hooks). | **Fix PR submitted:** [PR #6725](https://github.com/agentscope-ai/QwenPaw/pull/6725). |
| **High** | **[Issue #6708: 503 from upstream gateway in SSE retried?]** | In-stream SSE error events carrying a `503` status are not retried, immediately failing the request. | **Fix PR submitted:** [PR #6714](https://github.com/agentscope-ai/QwenPaw/pull/6714). |
| **Medium** | **[Issue #6726: Console session fails with 400 'tool' role error]** | Long sessions with 20-30+ tool call/result pairs fail, implying a problem with history windowing or message aggregation. | **No fix PR yet.** |
| **Medium** | **[Issue #6698: Browser SDK `open()` fails with Target crashed]** | v2.1.0b1 regression breaking the browser tool. | **No fix PR yet.** |

---

## 6. Feature Requests & Roadmap Signals

The following signals suggest where CoPaw is heading next.

- **"Artifact Canvas" (Live Rendering):** [#6730](https://github.com/agentscope-ai/QwenPaw/issues/6730) proposes rendering agent-generated HTML (dashboards, reports) in a side panel within the Console. This is a strong UX signal for moving from text-only interaction to a more "app-like" agent output paradigm. Note that [PR #6719](https://github.com/agentscope-ai/QwenPaw/pull/6719) just added "persistent artifact cards" for files created/modified—suggesting this area is actively in development.
- **On-Demand Skill Loading:** [#6699](https://github.com/agentscope-ai/QwenPaw/issues/6699) requests loading skills on-demand to reduce token bloat in system prompts (users report 8-10k tokens wasted with 27+ skills). This addresses a major cost/performance issue for power users.
- **Dynamic Model Routing:** [#6436](https://github.com/agentscope-ai/QwenPaw/issues/6436) is a more advanced form of the routing logic just merged for fallback. While the fallback feature is reactive, this request is proactive routing. Together they signal a push toward a more "Agent OS"-level model management layer.
- **WeChat Approval UX:** [#6728](https://github.com/agentscope-ai/QwenPaw/issues/6728) requests localized Chinese labels for approve/deny actions in the WeChat channel, following the fix for the console-only dialog bug.

**Prediction:** The next minor version will likely focus on **Channel Reliability (retries/health checks)** and **Memory/Token Management** (addressing the long-history tool-call crash and on-demand skills), as these are the most common pain points currently.

---

## 7. User Feedback Summary

- **Frustration with v2.1.0.b1 Desktop:** The `PYTHONHOME` crash is a severe regression breaking core functionality, and the "browser SDK" failure makes a headline feature unusable.
- **Channel Reliability is a Top Pain Point:** Users are actively working around flaky connections to external systems (Matrix, WeChat). The request for retries and health checks is a direct plea to stop requiring manual interventions and restarts.
- **Desire for Simpler UX:** There is visible friction with the "Full Mode" vs. "Simple Mode" UI concept in the Console ([#6413](https://github.com/agentscope-ai/QwenPaw/issues/6413)). Users find it confusing and want a more conventional settings icon.
- **Performance Issues with Heavy Tool Use:** Users are hitting context window limits and UI freezes when large tool outputs are loaded into the session history ([#6700](https://github.com/agentscope-ai/QwenPaw/issues/6700)). This points to a need for preemptive output truncation and pagination for history.

---

## 8. Backlog Watch

The following issues or PRs are open, have seen some maintainer activity or are high-impact, but are still awaiting resolution.

- **[PR #6302: feat: unify provider discovery, model metadata, routing, and agent controls](https://github.com/agentscope-ai/QwenPaw/pull/6302)** — **(8 days old)** This massive, core-architecture PR has been open for over two weeks and is central to several user-requested features. It requires attention to prevent it from becoming a stale mega-branch that conflicts significantly with the mainline.
- **[Issue #6634: (from previous cycles)]:** No specific issue, but the patch-bomb pattern of "first-time-contributor" PRs landing without explicit issue links (e.g. #6725, #6723) could burden maintainers reviewing them without context; encouraging issue-linking protocols would help clear the backlog.
- **[Feature: Configurable MCP tool-call timeout (#6724)](https://github.com/agentscope-ai/QwenPaw/issues/6724):** A simple, high-value feature request (adding a `timeout` field to MCP client config) that affects reliability significantly but remains unaddressed by maintainers.

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# ZeroClaw Project Digest — 2026-08-06

## Today's Overview

ZeroClaw is in a period of intense architectural activity, with 50 issues and 50 PRs updated in the last 24 hours. The project is converging on several major RFCs touching security, authentication, session management, and shell policy — all flagged high risk and mostly awaiting maintainer review. Notably, only 1 PR was merged/closed, indicating a review bottleneck rather than a delivery burst. The v0.8.5 finite stabilization line (tracker #9459, intake frozen Aug 4) is in its third week, and many older RFCs are receiving significant revisions (e.g. #7155 Rev 3, #6954 Rev 2, #7141 Rev 8), showing active design iteration despite the low merge count. New issues filed today are sharp, well-scoped bugs and small tasks, suggesting a maturing project with strong contributor discipline.

## Releases

No new releases in the last 24 hours.

## Project Progress

Only one PR was merged/closed in the last 24 hours, **PR #9750** (`fix(service): bound launcher-owned daemon logs`, `size: XL`, closed). This is a substantial fix that replaces unbounded fixed-file daemon redirection on the launcher-owned path with a shared service supervisor, capping each capture file at 8 MiB while retaining recent output via bounded nonblocking queues. This likely resolves a long-standing disk-exhaustion class of bug. A follow-up for macOS launchd logs (**PR #9773**) was opened today, showing iterative hardening of the same subsystem.

Active PRs with clear progress signals (but not yet merged):
- **PR #9403** (`fix(plugins): bound WASM exports by a wall-clock deadline`) — daily-updated, adds `plugins.limits.call_timeout_ms` (30s default) with host-owned deadlines across all guest exports. Critical for runtime safety.
- **PR #9737** (`fix(tools): enforce agent policy in pipelines`) — builds `execute_pipeline` only after effective per-agent tool policy is known; applies memory and ACP delivery predicates to eager children and builtin skills.
- **PR #9428** (`fix(channels): require sender authorization for Bluesky and Reddit`) — closes a security gap where these two inbound channels never consulted `peer_groups` / `allowlist::is_user_allowed`.
- **PR #9701** (`feat(gateway): keep chat WebSockets alive`) — adds configurable server-side Ping frames to prevent idle disconnects.
- **PR #9223** (`feat(eval): junit xml report format`) — hand-rolled JUnit XML output for CI test reporters.

## Community Hot Topics

1. **Issue #8303** — *RFC: Goal mode v1 — bounded foreground Matrix work* (18 comments, 👍 1). Author `vrurg`. The most commented issue. Proposal for durable multi-turn user objectives; the revision explicitly narrows scope (dropping restart handoff and Web). The core dilemma: how to deliver a bounded-user-goal runtime without coupling to channel admission and child-work complexity.

2. **Issue #8603** — *RFC: ZeroClaw Chat Completions profile* (16 comments). Author `REL-mame`. Requests an OpenAI Chat Completions–compatible API surface on top of the existing WS/ACP/webhook stack, targeting Open WebUI, LobeChat, Continue.dev, Aider, LangChain. Adoption-driven demand.

3. **Issue #7155** — *RFC: per-execution confirmation tier for high-risk shell commands + Claude Code–style policy* (16 comments). Author `NiuBlibing`. Rev 3 narrowed the normative scope to a reconciled shell-policy contract per maintainer review. Clear signal that security-policy surfaces are being iterated carefully.

4. **Issue #7141** — *RFC: Pluggable inbound authentication and canonical principals* (12 comments). Author `singlerider`. Rev 8 targets an Identity & Access milestone; OIDC + pluggable providers. This is a foundational architecture piece.

5. **Issue #9487** — *RFC: Runtime-owned conversation sessions and transport surface adapters* (10 comments). Author `NiuBlibing`. Rev 2 ratifies the #9487/#9488/#9600 ownership boundary; all migrated entry points submit `InboundAction`.

Underlying need: The project is simultaneously (a) standardizing on a single inbound action model, (b) building an auth/principal layer, and (c) attempting OpenAI-protocol compatibility — all high-stakes, all awaiting maintainer decisions. The community is disciplined (revisions, scope reviews) but hungry for decisions; tracker #8692 exists precisely for that queue.

## Bugs & Stability

New high-severity bugs filed today (2026-08-05 creation):

| Severity | Issue | Summary | Fix PR? |
|---|---|---|---|
| **S1 blocked** | #9775 — `[Bug]: OpenRouter streaming requests drop provider_extra` | `stream_chat` serializes `NativeChatRequest` directly and never calls `merge_extra_body`, so every configured provider extra is lost on streaming. | None yet |
| **S1 blocked** | #9774 — `[Bug]: Signal channel silently drops sourceUuid-only senders` | SSE envelopes with only `sourceUuid` (privacy mode) are silently dropped; breaks inbound messages. | None yet |
| **S1 blocked** | #9697 (still open, p1 accepted) — ZeroCode cannot connect to daemon launched by Windows Task Scheduler | Regression persists from #9117; daemon never becomes ready. | None |
| **S2 degraded** | #9768 — `[Bug]: daemon reload is not on SIGUSR1, and the degraded-security warning tells operators to send a signal that kills the daemon` | Two doc/implementation mismatches; operators are actively told to kill the daemon. | None yet |
| **S2 degraded** | #6350 — WhatsApp Web allowed-numbers bypassed for LID-based contacts (silent drops) | Closed today; long-running issue finally resolved. | Closed |

Other notable items:
- **#8642** (p1 accepted) — MCP/tool-schema cloning drives unbounded RSS growth in agent loop (WSL2 OOM path, split from #5542). Still open, 3 comments.
- **#9328** (accepted, high) — `verifiable-intent` evaluates constraints without verifying the credential chain. Mitigated by task #9432 (closed today: stop registering `vi_verify` until verifier exists + startup warning).

Follow-up tasks filed today include #9771 (clippy -D warnings on default feature surface for `zeroclaw-gateway`), #9770 (`cron update` silently discards declarative job changes — six columns), and #9769 (`vi_verify` withheld-capability notice invisible when log persistence is off).

## Feature Requests & Roadmap Signals

- **OpenAI Chat Completions profile (#8603)** — highest-signal feature request. Given the ecosystem (Open WebUI, LobeChat, Continue.dev, Aider), this is likely planned for a near-term gateway milestone; watch for RFC acceptance.
- **OpenRouter prompt caching via stable `session_id` (#9631)** — a cost-saving, low-risk enhancement; likely to land in v0.8.5 or v0.9.0 given provider-focus.
- **Per-user Telegram session toggle (#PR 9772)** — `per_user_session` for shared group chats; this is a small, well-scoped UX fix likely to merge quickly.
- **Hailo-Ollama native provider (#PR 9109)** — large PR (XL) adding hardware-specific provider; actively maintained (latest activity today).
- **ZeroCode multi-agent sidebar (#9727 epic)** — run/monitor multiple agents side-by-side from TUI. A product-direction signal toward heavier local orchestration.
- **Structured localization boundary for provider errors (#9716)** — p3, new today; long-term architecture work.

Prediction for the next release (likely v0.8.5): the pragmatic, high-value items — WASM call deadline (#9403), gateway WebSocket keepalive (#9701), JUnit eval output (#9223), Telegram session toggle (#9772), launchd log bounding (#9773), and the OpenRouter streaming `provider_extra` fix once a PR lands. The big RFCs (#7141, #8303, #9487) are v0.9.0+ material.

## User Feedback Summary

- **Direct pain**: Users report daily-cost pain with OpenRouter (prompt-cache misses due to no stable session_id, #9631), silent message drops (Signal #9774, WhatsApp LID #6350), and configuration traps (`cron update` discards changes #9770).
- **Satisfaction indicators**: "help wanted" and "good first issue" labels are scarce; instead we see many `needs-author-action` flags — contributors are engaged and iterating. The presence of multiple `principal contributor` / `distinguished contributor` labels on active PRs (wangmiao0668000666, IftekharUddin, Audacity88, vrurg) indicates a stable core team.
- **Frustration points**: Bugs in Windows/WSL2 daemon startup persist (#9697); the clippy task (#9771) suggests CI hygiene gaps for the default feature surface. The S1 OpenRouter streaming bug (#9775) could erode trust in a core provider path.

## Backlog Watch

Items needing maintainer decision or reopening attention:

- **Issue #7422** — (not visible today, but the v0.9.0 tracker #7432 references "blocked prereqs"; worth checking for stalled security RFCs upstream.)
- **Issue #9328** — *verifiable-intent evaluates constraints without verifying the credential chain*. Accepted but the underlying chain-verifier gap remains; #9432 closed gives only a mitigation. This should stay on the critical path.
- **Issue #8642** — MCP/tool-schema cloning RSS growth (p1). Still open with only 3 comments; a `size:L` PR would be expected soon.
- **PR #9109** — Hailo-Ollama provider (`size:XL`). Active but large; risk of staleness.
- **PR #9403** — WASM deadline (`size:XL`, p1). Daily updates, but merging this would unblock plugin-safety concerns.
- **Issue #8303** — *RFC: Goal mode v1*. 18 comments, high risk, no maintainer review stamp yet despite a 6-week age. Tracker #8692 exists but is itself awaiting decisions.
- **PR #9420** — Anthropic stored OAuth profiles (`size:XL`). Large surface change; needs careful review for security implications (auth_mode = "oauth" vs legacy api_key paths).

**Overall health**: Good. The project is well-governed (trackers for RFCs, release stabilization, v0.9.0 queue), contributor quality is high, and today's bug intake shows healthy self-testing. The immediate risk is decision latency: 39 open issues and 49 open PRs with many `needs-maintainer-review` flags. The maintainer queue (#8692) is the gating factor.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/kky-wollu/agents-radar).*