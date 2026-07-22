# OpenClaw Ecosystem Digest 2026-07-23

> Issues: 406 | PRs: 500 | Projects covered: 13 | Generated: 2026-07-22 23:09 UTC

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

Here is the OpenClaw project digest for July 23, 2026.

---

## OpenClaw Project Digest — 2026-07-23

### 1. Today's Overview

This was an exceptionally high-activity day for OpenClaw, with **406 issues** and **500 pull requests** updated in the last 24 hours, indicating a very healthy and responsive open-source project. The maintainers showed strong velocity, merging or closing **186 PRs** and resolving **150 issues**, while actively driving a significant refactoring campaign focusing on channel plugins, session management, and developer experience. No new releases were cut today, but the volume of code change suggests a major weekly release is imminent. Community engagement remains high, with several long-standing P1 bugs seeing renewed attention.

### 2. Releases

No new releases were published today.

### 3. Project Progress

Today saw substantial merged/closed activity (186 PRs), with key architectural advances:
- **Plugin Schema Refactoring**: PR [#112792](https://github.com/openclaw/openclaw/pull/112792) moved Slack and Signal Zod schemas out of the core into the plugins themselves, improving ownership boundaries.
- **Telegram Forum Topic Fixes**: PR [#112794](https://github.com/openclaw/openclaw/pull/112794) fixed an issue where Telegram forum-topic users could not edit/delete/react to messages in their topic.
- **Gateway Logging Hygiene**: PR [#112777](https://github.com/openclaw/openclaw/pull/112777) ensures non-default profiles (e.g., `--dev`) get their own log files instead of interleaving with the primary gateway.
- **Onboarding Stability**: PR [#112738](https://github.com/openclaw/openclaw/pull/112738) fixed a critical onboarding bug where setup could mis-route through a non-`main` agent.
- **Session Visibility & Participation**: PR [#112787](https://github.com/openclaw/openclaw/pull/112787) introduced session visibility states and server-enforced participation, part of a multi-operator collaboration feature.
- **Android Settings Chat**: PR [#112788](https://github.com/openclaw/openclaw/pull/112788) added a native OpenClaw settings chat for Android operators, addressing a long-requested usability gap.
- **Wear OS Tile**: PR [#112721](https://github.com/openclaw/openclaw/pull/112721) added an instant talk tile for Wear OS devices.

### 4. Community Hot Topics

- **Linux/Windows Clawdbot Apps (Issue #75)** — [Link](https://github.com/openclaw/openclaw/issues/75)
    - **Comments:** 115 | **Reactions:** 80 👍
    - The single most active issue. Users are demanding parity with macOS/iOS/Android apps. This remains the top community request and a clear product roadmap signal.

- **Feature: Pre-response enforcement hooks (Issue #13583)** — [Link](https://github.com/openclaw/openclaw/issues/13583)
    - **Comments:** 16 | **Reactions:** 2 👍
    - High-stakes users (quant/finance, ops) are demanding *hard gates* on tool-call policies, as soft prompt instructions are unreliable.

- **Feature: Masked Secrets (Issue #10659)** — [Link](https://github.com/openclaw/openclaw/issues/10659)
    - **Comments:** 15 | **Reactions:** 4 👍
    - Security-conscious users want agents to *use* API keys without *seeing* them, to prevent prompt injection leaks.

- **Normal tool text degraded to “(see attached image)” (Issue #96857)** — [Link](https://github.com/openclaw/openclaw/issues/96857)
    - **Comments:** 13 | **Reactions:** 4 👍
    - A perplexing UX bug where agents go "blind" to command outputs, seeing only image placeholder text.

### 5. Bugs & Stability

**Active (Open) High-Severity:**

- **P0 (Release Blocker): Gateway fails to start on v2026.7.1 (Issue #108435)** — [Link](https://github.com/openclaw/openclaw/issues/108435). A regression update preventing gateway startup on systemd/ollama/manual launch. **No fix PR linked.**
- **P1 (Diamond Lobster): Codex PreToolUse hook relay spawns CPU-bound processes (Issue #91009)** — [Link](https://github.com/openclaw/openclaw/issues/91009). Causes RPC stalls. **Linked open PR.**
- **P1 (Diamond Lobster): Compaction timeout is single wall-clock, no partial-progress reuse (Issue #92043)** — [Link](https://github.com/openclaw/openclaw/issues/92043). Long-standing sessions get stuck in a fail loop. **Linked open PR.**
- **P1 (Diamond Lobster): Subagent raw output sent to chat instead of parent summary (Issue #90840)** — [Link](https://github.com/openclaw/openclaw/issues/90840). A regression breaking subagent workflows.
- **P1 (Diamond Lobster): Externalized channel plugins fail on self-hosted (Issue #92516)** — [Link](https://github.com/openclaw/openclaw/issues/92516). Blocks containerized deployments from using MS Teams/Slack plugins.
- **P1 (Silver Shellfish): Session list performance crash with 4900+ sessions (PR #112273)** — [Link](https://github.com/openclaw/openclaw/pull/112273). A fix is in review for the reported 140% CPU stall.

**Recently Closed / Fixed:**
- **P0 (Mac App): Install icon unclickable in DMG (Issue #98674)** — [Link](https://github.com/openclaw/openclaw/issues/98674). Closed today.
- **P1: WhatsApp channel drops long responses (Issue #84092)** — [Link](https://github.com/openclaw/openclaw/issues/84092). Closed, likely fixed by subsequent channel refactoring.

### 6. Feature Requests & Roadmap Signals

The following in-progress PRs point to upcoming features likely in the next major release:
- **Claw Manifest (CLAW.md) Support (PR #111391)** — [Link](https://github.com/openclaw/openclaw/pull/111391). A new manifest format for project-level agent configuration.
- **Localization & i18n Infrastructure (PR #112784)** — [Link](https://github.com/openclaw/openclaw/pull/112784). Proves a catalog authoring loop, suggesting internationalization is nearing public beta.
- **Consented Grouped Claw Updates (PR #102982)** — [Link](https://github.com/openclaw/openclaw/pull/102982). Moves from read-only plans to actual mutation of agent configs and workspace files.
- **Context Window % Injection (Issue #38568)** — [Link](https://github.com/openclaw/openclaw/issues/38568). A community request to inject "context=49%" into system prompts is gaining support.
- **Session End Hook Event (Issue #10142)** — [Link](https://github.com/openclaw/openclaw/issues/10142). Requested for Temporal workflow orchestration integration.

### 7. User Feedback Summary

- **Positive:** The rapid pace of fixes (150 issues closed today) and the massive refactoring effort (PR #112769, #112753, #112789) signal a mature project investing in code quality and debt reduction. The Wear OS tile and Android settings chat show responsiveness to platform-specific feedback.
- **Pain Points:**
    - **Performance Regressions:** Multiple users reported specific version-to-version slowdowns (Issue #85333: 4-5x slower `doctor --fix` on v2026.5.20).
    - **Channel Reliability:** Telegram, LINE, WhatsApp, and qqbot all had distinct issues with message delivery, reconnection, or silent drops.
    - **Security & Access Control:** The "masked secrets" and "pre-response enforcement hooks" requests indicate users feel current security is trust-based rather than mechanical.
    - **Session Management:** Users are frustrated by stale memories that cannot be deleted (Issue #95606) and sessions surviving app removal (Issue #99054).

### 8. Backlog Watch

Several high-severity issues from earlier months remain open without clear resolution:
- **Issue #39807 (P1, Mar 8): Billing error 402 causes infinite retry death spiral** — [Link](https://github.com/openclaw/openclaw/issues/39807). No backoff logic for provider billing errors. Still needs product decision.
- **Issue #41199 (P1, Mar 9): Agent-to-Agent communication tool parameter conflicts** — [Link](https://github.com/openclaw/openclaw/issues/41199). Structural flaw in `sessions_send` tool causing LLMs to generate invalid params. Linked PR open but stale.
- **Issue #87318 (P2, May 27): Amazon Bedrock Haiku 4.5 inference profile ARN not supported** — [Link](https://github.com/openclaw/openclaw/issues/87318). Directly blocks AWS enterprise adopters.
- **Issue #99773 (P1, Jul 4): Hot reload drops include-defined models from registry** — [Link](https://github.com/openclaw/openclaw/issues/99773). Requires a gateway restart as a workaround, defeating the purpose of hot reload.

---

## Cross-Ecosystem Comparison

# Cross-Project Comparison Report: AI Agent Open-Source Ecosystem
**Date: 2026-07-23**

---

## 1. Ecosystem Overview

The personal AI assistant open-source ecosystem is experiencing a **coordinated surge in architectural maturity**, with projects prioritizing multi-agent collaboration, channel reliability, and security hardening over raw feature expansion. Activity is heavily concentrated in the "Claw" lineage (OpenClaw, IronClaw, ZeroClaw, NanoClaw, PicoClaw), which together account for over 600 active issues and 650 active PRs—indicating a shared platform ecosystem undergoing simultaneous refactoring. A clear bifurcation is emerging: high-velocity projects (IronClaw, OpenClaw, ZeroClaw) are racing toward v1/v0.9 releases, while smaller projects (Moltis, ZeptoClaw, TinyClaw) are in maintenance or low-activity phases. The dominant technical themes are **session persistence across channels**, **multi-tenant security models**, and **model fallback reliability**—all signals of a maturing ecosystem shifting from prototyping to production deployments.

---

## 2. Activity Comparison

| Project | Active Issues | Active PRs | Release Today | Health Score* |
|---------|-------------|-----------|---------------|---------------|
| **OpenClaw** | 406 | 500 | No | 9/10 — High velocity, strong fix rate |
| **IronClaw** | 36 (+14 closed) | 26 (+22 merged) | No | 8/10 — Launch checkpoint focus, deep retro |
| **ZeroClaw** | 50 | 50 | No | 7/10 — Broad RFC activity, Windows CI gap drags |
| **NanoBot** | 4 (+2 closed) | 62 (+40 merged) | No | 7/10 — Extremely high PR throughput, critical bugs found |
| **PicoClaw** | 4 | 4 (+1 merged) | No | 5/10 — Moderate, single matrix bug is critical |
| **Hermes Agent** | 50 | 50 | No | 6/10 — High activity but regressions mounting |
| **CoPaw** | 31 | 50 (+15 merged) | **v2.0.0.post4** | 6/10 — High fix velocity, v2.0.0 stability issues |
| **NullClaw** | 1 (closed) | 1 (closed) | No | 4/10 — Minimal activity, one critical fix |
| **NanoClaw** | 1 | 3 | No | 4/10 — Low activity, SECURITY.md issue pending |
| **LobsterAI** | 1 (closed) | 5 (all merged) | No | 5/10 — Clean maintenance, no forward momentum |
| **Moltis** | 1 | 1 | No | 3/10 — Near-dormant, single feature discussion |
| **ZeptoClaw** | 0 | 0 | No | 1/10 — Inactive |
| **TinyClaw** | 0 | 0 | No | 1/10 — Inactive |

*Health Score: Composite of activity volume, fix rate, severity of open bugs, and community engagement.*

---

## 3. OpenClaw's Position

**Advantages vs Peers:**
- **Scale:** OpenClaw's 406 open issues and 500 active PRs dwarf every other project. This is a mature, heavily resourced project with a large maintainer team capable of processing 150+ issues and 186 PRs in a single day.
- **Platform Breadth:** Native apps for macOS, iOS, Android (including Wear OS), with Linux/Windows app as the #1 community request—indicating near-complete platform coverage.
- **Plugin Architecture:** The channel plugin schema refactoring (moving Zod schemas out of core) demonstrates a clean microkernel design, unlike IronClaw's monolithic approach or NanoBot's tight provider coupling.
- **Session Management:** Introduced session visibility states and server-enforced participation—none of the other projects have similar multi-operator collaboration primitives.

**Technical Approach Differences:**
- OpenClaw uses **Zod-based runtime validation** for plugins; ZeroClaw uses **Pydantic models**; IronClaw uses **Rust-style trait boundaries** via its `ProductSurface` refactor.
- OpenClaw is the only project with explicit **CI for fixed issues** (186 PRs merged/closed in 24h) and a clear **multi-operator session model**.
- Gateway logging hygiene (non-default profiles get separate log files) shows operational maturity peers lack.

**Community Size Comparison:**
- OpenClaw's #1 issue (75 comments on Linux/Windows app request) has more engagement than *any whole project* in the Moltis, NanoClaw, or PicoClaw ecosystems.
- The "pre-response enforcement hooks" (16 comments) and "masked secrets" (15 comments) requests indicate security-conscious, enterprise-grade user expectations.

---

## 4. Shared Technical Focus Areas

| Focus Area | Projects Involved | Specific Needs |
|-----------|-------------------|----------------|
| **Multi-Agent Collaboration** | OpenClaw, NanoBot, ZeroClaw, IronClaw | OpenClaw: session visibility/participation; NanoBot: subagent→multi-agent evolution (#5000); ZeroClaw: A2A agent discovery RFC (#7218); IronClaw: generic extension runtime |
| **Channel Reliability** | All "Claw" projects + Hermes Agent | OpenClaw: Telegram forum fix, LINE/WhatsApp drops; NullClaw: Discord deaf bug; IronClaw: Telegram P1 pairing loop; ZeroClaw: Signal crashloop; PicoClaw: Matrix no-reconnect |
| **Model Fallback & Provider Interop** | OpenClaw, NanoBot, CoPaw, ZeroClaw | OpenClaw: Diamond Lobster CPU-bound hook; NanoBot: MCP $ref blocks Kimi; CoPaw: GLM/DeepSeek tool call wrapping; ZeroClaw: model fallback notices (#8684) |
| **Security & Credential Isolation** | OpenClaw, IronClaw, ZeroClaw, NanoClaw | OpenClaw: masked secrets (#10659); IronClaw: secret-lease + egress-proxy (#6472); ZeroClaw: OIDC RFC, pairing code weakness; NanoClaw: SECURITY.md overclaim (#3118) |
| **Session/Memory Persistence** | OpenClaw, ZeroClaw, LobsterAI | OpenClaw: compaction timeout; ZeroClaw: MySQL/PostgreSQL backends (+4 DB PRs); LobsterAI: OOM crash fix |
| **Performance & Scalability** | OpenClaw, NanoBot, CoPaw, Hermes Agent | OpenClaw: 4900+ session stall; NanoBot: WebUI SQLite indexing; CoPaw: 2s overhead per reply; Hermes: Desktop resource leaks |
| **Localization & i18n** | OpenClaw, ZeroClaw | OpenClaw: PR #112784 (catalog authoring); ZeroClaw: channel bypass (#6548) |
| **Desktop/App Ecosystem** | OpenClaw, Hermes Agent, NanoClaw | OpenClaw: Wear OS tile, Android chat; Hermes: desktop session switching broken; NanoClaw: Waybar status indicator |

---

## 5. Differentiation Analysis

| Dimension | OpenClaw | IronClaw | ZeroClaw | NanoBot | CoPaw | Hermes Agent |
|-----------|----------|----------|----------|---------|-------|--------------|
| **Target User** | Power users, developers, multi-platform | Enterprise, production deployments | Developers, self-hosters, tinkerers | Researchers, LLM experimenters | Enterprise RAG/workflows | Consumer desktop users |
| **Primary Architecture** | Plugin microkernel (Zod schemas) | WASM extension runtime (Rust) | RFC-driven modular (Python/Pydantic) | Monolithic Python (provider-coupled) | Python agent framework | Node.js desktop app |
| **Key Differentiator** | Multi-operator session model, platform breadth | Error recoverability endgame, secret leasing | Database backends, OIDC, observability | High PR throughput, model preset scoping | v2.0.0 stability push, cron model override | Streaming TTS with barge-in, WhatsApp isolation |
| **Weakest Area** | Performance regressions (doctor 4-5x slower) | Telegram UX (pairing loop, routing confusion) | Windows CI completely broken (74 failures) | MCP $ref forwarding blocks providers | Process crashes, 2s overhead regression | Desktop app fragility, regressions in core UX |
| **Release Maturity** | Pre-major (weekly releases) | Pre-v1 launch (breaking API changes pending) | Pre-v0.9 (RFC cycle active) | Pre-v1 (no release in 24h) | v2.0.0.post4 (stabilizing) | No release today |
| **Community Contribution** | Very high (115-comment issue) | Moderate (4-comment epic) | High (11-comment Windows bug) | Moderate (4-comment proposal) | High (first-time contributor surge) | Moderate (translations, but regression reports) |

---

## 6. Community Momentum & Maturity

**High Velocity / Rapidly Iterating (active daily refactoring):**
- **OpenClaw** — Exceptional velocity; 406 issues, 500 PRs updated. Mature project investing in code quality. Clear platform leader.
- **IronClaw** — Launch checkpoint urgency; 12 retroactively closed "completed foundation" issues. Deep architectural consolidation.
- **ZeroClaw** — High RFC throughput; 13 PRs merged today. Windows CI gap is the single biggest risk.
- **NanoBot** — 40 PRs merged in 24h, but critical null-pointer bugs found today. High throughput yet fragile.

**Moderate / Stabilizing:**
- **CoPaw** — v2.0.0.post4 released; large number of first-time contributor fixes. Stability issues from v2.0.0 are being resolved.
- **Hermes Agent** — High bug report volume; team handling regressions but stretched. Desktop app is the weakest point.
- **PicoClaw** — Moderate activity; Matrix reconnection bug is critical but maintainer unresponsive since July 2.
- **LobsterAI** — Clean but low momentum; 5 PRs merged, all maintenance fixes. No forward-looking features.

**Low Activity / Maintenance:**
- **NullClaw** — One critical fix (Discord deaf bug) merged today; otherwise dormant.
- **NanoClaw** — One SECURITY.md issue, three stale PRs. Minimal community engagement.
- **Moltis** — One feature discussion (model routing) with no maintainer response in months. Near-dormant.
- **ZeptoClaw, TinyClaw** — No activity at all. Effectively inactive.

**Maturity Assessment:**
- **OpenClaw** is the most mature—production-grade plugin system, multi-platform apps, multi-operator features.
- **IronClaw** is building toward v1 with disciplined architectural refactoring and security foundations.
- **ZeroClaw** is ambitious (multiple DB backends, OIDC, A2A discovery) but the Windows gap undermines cross-platform credibility.
- **NanoBot** and **CoPaw** are growing rapidly but still fixing fundamental stability issues from recent releases.

---

## 7. Trend Signals

**1. Security is Shifting from Trust-Based to Mechanical Enforcement**
OpenClaw (#13583: pre-response enforcement hooks), IronClaw (#6472: secret-lease daemon), and ZeroClaw (#6613: weak pairing code, #7141: OIDC) all show users demanding hard gates, not soft prompts. Expect **WASM sandboxing**, **secret leasing**, and **OAuth-based credential management** to become minimum requirements for production AI agents.

**2. Multi-Agent Collaboration is the Next Frontier**
OpenClaw launched session visibility states; NanoBot is evolving subagents into multi-agent systems (#5000); ZeroClaw has A2A discovery RFC (#7218); IronClaw completed its generic extension runtime. The industry is moving toward **persistent agent identities, shared state, and inter-agent communication**—far beyond simple task delegation.

**3. Channel Reliability is Still the Hardest Problem**
Every project with a channel integration has at least one critical reliability bug: Telegram pairing loops (IronClaw), Matrix silent sync death (PicoClaw), Discord deaf bug (NullClaw), WhatsApp drops (OpenClaw), Signal crashloops (ZeroClaw). **WebSocket reconnection, rate limiting, and media upload handling** are universal pain points.

**4. Desktop App Fragility is a Recurring Theme**
Hermes Agent (session switching broken, image reconnection loops) and OpenClaw (DMG install icon unclickable) both struggled with desktop app quality. Users expect **mobile-grade UX on desktop**, and projects that deprioritize desktop testing (ZeroClaw's 74 Windows failures) risk losing developer trust.

**5. Performance Regressions Follow Major Refactors**
CoPaw (2s overhead per reply in v2.0.0), OpenClaw (4-5x slower doctor --fix), and ZeroClaw (140% CPU at 4900 sessions) all saw performance degrade after architecture changes. **Benchmark-driven CI** (which ZeroClaw's #7065 eval harness and IronClaw's hermetic testing platform aim to solve) is an emerging priority.

**6. Localization is Becoming a Competitive Differentiator**
OpenClaw (i18n catalog PR) and ZeroClaw (Fluent localization bug #6548) are investing in internationalization. The active community discussions in Chinese (CoPaw's WeChat ecosystem, PicoClaw's DingTalk support) confirm that **non-English-first UX is table stakes for global adoption**.

**Key Insight for Developers:**
The ecosystem is converging on a **three-layer architecture**: (1) a **multi-operator session layer** with visibility and participation controls, (2) a **channel-agnostic runtime** with WASM/MCP extensions, and (3) a **security layer** with secret leasing and OAuth-based credential isolation. Projects that invest in all three (OpenClaw, IronClaw, ZeroClaw) are well-positioned; those missing any layer risk being leapfrogged.

---

## Peer Project Reports

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot Project Digest — 2026-07-23

## 1. Today's Overview

NanoBot shows **heavy development activity** today, with 62 pull requests updated in the last 24 hours—40 of which were merged or closed. The project is clearly in a **high-velocity integration phase** after a previous week of churn. Six issues were updated, with two closed and four remaining open. However, **no new releases were published**, suggesting these changes are still baking or awaiting further validation. The PR velocity (62 updates) is unusually high and may indicate a coordinated sprint or release preparation.

## 2. Releases

**No new releases today.** The project has not published a release in the observed window. This is notable given the high volume of merged PRs; users awaiting a stable cut may need to track the `main` branch or await an upcoming tag.

## 3. Project Progress

**40 PRs were merged or closed today**, representing substantial codebase advancement. Key highlights among closed PRs:

- **PR #4866** — `feat(agent): make model presets session-scoped` (merged, priority p1) — This is a significant architectural change that makes named model-preset selection per-session, admits one immutable `LLMRuntime` per turn, and ensures consistency across provider calls, prompt sizing, tools/subagents, and compaction.

- **PR #4439** — `feat(tools): add read-only search_history tool` (open, 0 comments) — A new tool for recalling memory, though still open with conflicts.

- Multiple bug-fix PRs were merged today (see Section 5), including fixes for cron loading, pairing channel validation, and Markdown table rendering in Feishu and Slack.

Active development areas visible from open PRs include:
- **WebUI performance** (PR #5003) — Indexing conversation history in SQLite, moving disk work off the event loop
- **Multi-agent collaboration** (Issue #5000) — Proposal to evolve subagents into a true multi-agent system
- **New provider integrations** (PR #5035) — xAI Grok OAuth with capability-gated X Search
- **Channel improvements** (PR #5009, #5033) — Feishu group listen mode, Telegram multi-bot support
- **Mobile and accessibility** (PR #4494) — PWA support and mobile swipe gestures

## 4. Community Hot Topics

| Item | Type | Comments | Summary |
|------|------|----------|---------|
| [#5000](https://github.com/HKUDS/nanobot/issues/5000) | Issue (open) | 4 | Proposal to evolve subagent system toward multi-agent collaboration |
| [#4934](https://github.com/HKUDS/nanobot/issues/4934) | Issue (closed) | 2 | Qwen models exposing thinking/reasoning content in chat responses |

**Analysis:**
- **Issue #5000** (`[enhancement] Proposal: evolve the current subagent system toward multi-agent collaboration`) is the most discussed issue by comment count. This signals growing community interest in more sophisticated agent coordination—moving beyond simple task delegation toward persistent identities, shared state, and collaborative workflows. This could become a major feature for the next major release.
- **Issue #4934** (closed) regarding Qwen models leaking reasoning content indicates that provider-level content sanitization remains a concern, particularly as more models expose internal chain-of-thought.

The highest-activity PRs (all with 0 comments but large teams and cross-references visible) include:
- [#5017](https://github.com/HKUDS/nanobot/pull/5017) — WebUI fallback model display
- [#5003](https://github.com/HKUDS/nanobot/pull/5003) — SQLite indexing for WebUI history
- [#5035](https://github.com/HKUDS/nanobot/pull/5035) — xAI Grok OAuth integration

## 5. Bugs & Stability

**Severity: HIGH** — Multiple critical bugs reported and fixed today:

| Bug | Issue/PR | Severity | Status | Fix |
|-----|----------|----------|--------|-----|
| Null `schedule` crashes cron store | [#5042](https://github.com/HKUDS/nanobot/issues/5042) via PR #5042 | **CRITICAL** | Fix PR open | Fallback to `kind=every` on null |
| Null `runHistory` elements quarantine cron store | [#5043](https://github.com/HKUDS/nanobot/issues/5043) via PR #5043 | **CRITICAL** | Fix PR open | Skip non-dict elements |
| Null approved channel lists crash pairing loader | [#5044](https://github.com/HKUDS/nanobot/issues/5044) via PR #5044 | **HIGH** | Fix PR open | Treat non-list as empty allow-list |
| Dream batches starve later history (no cursor advance) | [#5041](https://github.com/HKUDS/nanobot/issues/5041) | **HIGH** | Open, no fix yet | — |
| MCP tool schema with non-standard `$ref` disables strict providers | [#5040](https://github.com/HKUDS/nanobot/issues/5040) | **HIGH** | Open, no fix yet | — |
| Qwen models leak reasoning content | [#4934](https://github.com/HKUDS/nanobot/issues/4934) | **MEDIUM** | Closed (fixed) | Fixed in prior merges |
| Fenced Markdown tables break in Feishu/Slack cards | [#5046](https://github.com/HKUDS/nanobot/pull/5046), [#5045](https://github.com/HKUDS/nanobot/pull/5045) | **LOW-MEDIUM** | Fix PRs open | Stash/restore code fences before table scan |
| Media path vs workspace path conflict | [#5028](https://github.com/HKUDS/nanobot/issues/5028) | **MEDIUM** | Open, no fix yet | — |
| WebUI loses visibility on late subagent completions | [#4948](https://github.com/HKUDS/nanobot/issues/4948) | **MEDIUM** | Closed (fixed) | Fixed |

**Notable:** Three null-pointer/serialization bugs were reported and immediately addressed with fix PRs on the same day (#5042, #5043, #5044), indicating strong maintainer responsiveness. The Dream cursor starvation (#5041) and MCP `$ref` forwarding (#5040) bugs lack fixes and could cause data loss or complete provider unavailability respectively.

## 6. Feature Requests & Roadmap Signals

| Feature | Issue/PR | Likelihood for Next Release |
|---------|----------|---------------------------|
| Multi-agent collaboration system | [#5000](https://github.com/HKUDS/nanobot/issues/5000) | **Medium** — conceptual, needs spec |
| xAI Grok OAuth + X Search | [#5035](https://github.com/HKUDS/nanobot/pull/5035) | **High** — PR open, priority p1 |
| Parallel Search MCP preset | [#5047](https://github.com/HKUDS/nanobot/pull/5047) | **High** — simple, low risk, documented |
| WebUI SQLite history indexing | [#5003](https://github.com/HKUDS/nanobot/pull/5003) | **High** — priority p1, PR open |
| Telegram multi-bot support | [#5033](https://github.com/HKUDS/nanobot/pull/5033) | **High** — priority p1, PR open |
| Feishu group listen mode | [#5009](https://github.com/HKUDS/nanobot/pull/5009) | **High** — priority p1, PR open |
| OAuth status/expiry warnings | [#4689](https://github.com/HKUDS/nanobot/pull/4689) | **Medium** — open since July 3, needs attention |
| Idle compaction interval config | [#5036](https://github.com/HKUDS/nanobot/pull/5036) | **Medium** — Raspberry Pi use case |
| PWA + mobile swipe gestures | [#4494](https://github.com/HKUDS/nanobot/pull/4494) | **Low** — open since June 24, conflicts |
| Explicit skill context loading | [#5018](https://github.com/HKUDS/nanobot/pull/5018) | **High** — PR open, resolved ignored feature |

**Prediction:** The next release will likely include xAI Grok support, WebUI SQLite indexing, Telegram multi-bot, Feishu group listen, and the Parallel Search MCP preset—all high-priority PRs with active work today.

## 7. User Feedback Summary

- **Performance concern (Raspberry Pi):** One user reports 30-40% CPU usage on idle, traced to aggressive compaction scan interval. This is addressed by PR #5036, which makes the interval configurable. This is a real pain point for edge/IoT deployments.

- **Dream system reliability:** User reports that no-op Dream runs don't advance the cursor, starving later history entries (Issue #5041). This suggests the memory consolidation pipeline has a silent correctness bug that could cause data loss in long-running agents.

- **Provider compatibility frustration:** The MCP `$ref` forwarding issue (#5040) blocks Kimi/Moonshot providers entirely when a single tool uses non-standard schema references. This is a hard failure that kills the entire model for those providers.

- **Multi-agent expectations:** The community is pushing for more sophisticated collaboration beyond simple subagent task delegation (Issue #5000). Users want persistent identities, shared state, and inter-agent communication.

- **Media/workspace path conflict:** A Feishu-integration user reports that uploaded files become inaccessible when workspace restrictions are enabled (Issue #5028), pointing to incomplete path isolation logic.

## 8. Backlog Watch

| Item | Issue/PR | Age | Status | Concern |
|------|----------|-----|--------|---------|
| OAuth status and expiry warnings | [#4689](https://github.com/HKUDS/nanobot/pull/4689) | 20 days (July 3) | Open, priority p1 | Unmerged despite p1; may indicate design review bottleneck |
| PWA + mobile swipe gestures | [#4494](https://github.com/HKUDS/nanobot/pull/4494) | 29 days (June 24) | Open, conflicts | Long-standing with conflicts; mobile users waiting |
| DingTalk private chat gate | [#4446](https://github.com/HKUDS/nanobot/pull/4446) | 31 days (June 22) | Open | Unaddressed for over a month; channel parity gap |
| Search history tool (memory recall) | [#4439](https://github.com/HKUDS/nanobot/pull/4439) | 32 days (June 21) | Open, conflicts | Longest open PR with memory recall implications; conflicts need resolution |
| Dream cursor starvation | [#5041](https://github.com/HKUDS/nanobot/issues/5041) | 1 day | Open, no fix | Recent but critical; no fix PR yet |
| MCP `$ref` forwarding | [#5040](https://github.com/HKUDS/nanobot/issues/5040) | 1 day | Open, no fix | Recent but blocks entire provider category; needs urgent fix |

**Maintainer attention needed:** PR #4439 (search history tool) and PR #4689 (OAuth status) are both p1 priority but have languished for weeks. While today's 40 merged PRs show high throughput, these longer-standing items may indicate that maintainers are prioritizing newer work over resolving open conflicts on existing PRs.

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

Here is the Hermes Agent project digest for July 23, 2026.

---

## Hermes Agent Project Digest — 2026-07-23

### 1. Today's Overview

The Hermes Agent project is experiencing **very high activity**, with 50 active Issues and 50 active PRs updated in the last 24 hours. This is a significant spike, driven by major feature integration (streaming TTS, WhatsApp isolation) and a surge of incoming bug reports, including critical regressions in the Desktop app. The community is highly engaged, but the maintainer team appears stretched, as several high-priority (P1/P2) bugs and long-standing feature requests remain open. There were no new releases today.

### 2. Releases

None.

### 3. Project Progress

Six pull requests were **merged or closed** today. Notable changes include:

- **Desktop E2E Testing:** A PR adding visual end-to-end session lifecycle tests for the desktop app was merged ([#69580](https://github.com/NousResearch/hermes-agent/pull/69580)). A follow-up PR now runs these tests offscreen on macOS ([#69668](https://github.com/NousResearch/hermes-agent/pull/69668)).
- **Automated Formatting:** A bot-driven PR for auto-fixing JS linting/formatting was auto-merged ([#69669](https://github.com/NousResearch/hermes-agent/pull/69669)).
- **Snapshot Restore Bug:** A fix for a regression where snapshot restoration could leave a stale state.db connection was closed (linked to [#65942](https://github.com/NousResearch/hermes-agent/pull/65942)).

### 4. Community Hot Topics

The most active discussions this week highlight two major pain points:

- **Dashboard Chat UX Regression (Issue #24860):** The most commented issue (12 comments) reports that `Ctrl+V` text paste is broken in the Dashboard Chat tab, and image paste is unsupported. Users are frustrated by a basic productivity function being non-functional. [Link](https://github.com/NousResearch/hermes-agent/issue/24860)
- **Desktop Session Switching Broken (Issue #66875):** A critical P2 bug (6 comments) shows that clicking the most recent session in the Desktop app does nothing after visiting another tab. Users cannot navigate back to their current conversation. [Link](https://github.com/NousResearch/hermes-agent/issue/66875)
- **Data Backup Concern (#12238):** With 19 upvotes, this is the highest-reacted feature request. Users are anxious about losing their agent's learned state and memory, signaling a strong demand for built-in version control and data safety. [Link](https://github.com/NousResearch/hermes-agent/issue/12238)

### 5. Bugs & Stability

A large volume of regressions and high-impact bugs were reported today. The most critical include:

- **Desktop: Queued Image Reconnect Loop (P2, #69638):** Large image attachments in the Desktop app cause a persistent WebSocket reconnect loop and persist massive amounts of data (up to 49MB) in localStorage. A fix PR ([#69666](https://github.com/NousResearch/hermes-agent/pull/69666)) has been opened to raise the WebSocket limit and strip the preview URLs.
- **Desktop SSH Remote Mode Broken with Profiles (P2, #69551):** The Desktop SSH remote session token path is hardcoded, causing complete failure when a non-default profile is active. A fix PR ([#69664](https://github.com/NousResearch/hermes-agent/pull/69664)) is open to anchor the token directory to the user's home directory.
- **Model Picker Groups Everything as "CUSTOM ENDPOINT" (P2, #66329):** The model picker in the CLI incorrectly groups models under a generic label instead of their correct named provider section. A configuration UI issue affecting user confidence.
- **Agent Conversational Hang (P1, #69467):** A critical fix was proposed for a bug where the agent's conversation loop goes completely silent after a tool-call error, requiring a gateway timeout to kill the session. Fix PR: [#69467](https://github.com/NousResearch/hermes-agent/pull/69467).
- **Telegram Upload Timeout (P2, #62936):** Uploads over ~15MB fail consistently because the Python Telegram Bot's media upload timeout is never set, ignoring the `HERMES_TELEGRAM_HTTP_WRITE_TIMEOUT` env variable. No fix PR is yet linked.

### 6. Feature Requests & Roadmap Signals

The pipeline for the next version appears to be heavily focused on **voice interactivity** and **multi-channel isolation**.

- **Streaming TTS with Barge-In (PR #69511):** A major feature is being finalized that enables sentence-by-sentence voice streaming with the ability to interrupt (barge-in) by talking or typing. This is a significant UX upgrade for voice mode.
- **Model Knowledge of Interruption (PR #69602):** A companion PR builds on the barge-in feature by informing the model that it was interrupted, allowing for more natural conversational flow.
- **WhatsApp Sender Isolation (PR #69665):** A security-focused PR aims to restrict toolsets for non-owner senders on shared WhatsApp lines, addressing a growing need for multi-tenant safety.
- **Shared Out-of-Credits UX (PR #69655):** A new feature standardizes the "out of credits" message across CLI, TUI, and Desktop, indicating a focus on billing UX maturity.

### 7. User Feedback Summary

- **Pain Points:**
    - *Desktop App Fragility:* Multiple reports (issues #69638, #66875, #69660) describe the Desktop app as having regressive behavior, such as broken session switching, message queueing failures, and resource leaks. This suggests a need for more rigorous desktop regression testing.
    - *Configuration & Platform Friction:* Users continue to face problems with macOS-specific toolchain shadowing (#45279) and missing environment paths for Linuxbrew (#69625).
    - *Provider/Delivery Inconsistency:* Reports of matrix adapter crashes (#63395) and FIFO queue media loss (#18539) indicate ongoing instability in the gateway and message delivery pipeline.

- **Satisfaction:** The high number of feature PRs (e.g., TTS, billing UX, WhatsApp isolation) suggests a team actively shipping new functionality, which keeps the community engaged. The community is also contributing valuable documentation translations (e.g., Russian README in PR #69658).

### 8. Backlog Watch

Several long-standing, important items remain unresolved and need maintainer attention:

- **Critical (P1):** The "vision bricking session" bug (Issue #25837) has been open for over two months. It can permanently break a session by sending oversized images to Anthropic. No fix PR is attached.
- **High-Value Feature (19 👍):** The built-in backup/version control request (Issue #12238) was created in April and remains open. It is the most popular feature request and is a major appeal for professional users.
- **High-Value Feature (7 Comments):** Per-cron reasoning effort overrides (Issue #23524) is a well-discussed request from May that lacks a PR.
- **Open Regressions:** The installer shadowing issue on macOS (Issue #45279) and the `.env` sanitizer bug (Issue #12651) have been open for over a month and could affect setup for new users.

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw Project Digest — 2026-07-23

## Today's Overview

PicoClaw shows moderate activity with 4 issues and 4 open pull requests updated in the last 24 hours. No new releases were published today, and only one PR was merged/closed. The project has several open bugs and feature requests advancing, alongside some long-stale items needing maintainer attention. Community engagement remains steady, with new contributors submitting fixes and feature implementations across multiple channels.

## Releases

No new releases were published today. The latest available version remains **v0.3.1** (referenced in Issue #3258).

## Project Progress

One pull request was merged and closed today:
- **#3285** — `docs: remove picopaw` — A documentation cleanup reverting an earlier PR, merged by imguoguo. This is a minor housekeeping change with no functional impact.

Three other PRs remain open and were updated today, none yet merged:
- **#3286** — `fix: update Go and x/text for govulncheck` — A bug fix addressing security vulnerability scanning issues by updating dependencies.
- **#3283** — `fix(dingtalk): support picture/image message inbound` — New feature adding image message support for the DingTalk channel, including token caching and media download logic.
- **#3222** (stale) — `refactor(deltachat): cleanup implementation, documentation -200LOC` — Significant cleanup of the DeltaChat implementation, removing legacy features and outdated tests.
- **#3163** (stale) — `feat(bedrock): leverage Converse prompt caching via cache points` — AWS Bedrock optimization that introduces prompt caching for cost reduction.

## Community Hot Topics

**Most active issue:**
- **#3203** — `[BUG] Matrix sync loop has no reconnection logic` — 5 comments, 2 👍 reactions. Created by weissfl, this issue describes a critical reliability bug where the Matrix `/sync` long-polling dies silently after network disruption, with no auto-reconnect. Users express concern about systemd's `Restart=on-failure` not triggering because the main process stays alive.

**Other notable items:**
- **#3258** — `[BUG] Process Hook before_tool modify not working: decision field discarded` — 1 comment. A user reports a deserialization defect in v0.3.1 that breaks tool hooks.
- **#3257** — `[stale] Add stateless/no-history mode for gateway sessions` — 1 comment. User lisiying requests a stateless session mode for CLI users who want fresh conversations without manual session key management.
- **#3287** — `[Feature] Better support long messages in IRC` — 0 comments yet, but opened today by superuser-does. Describes the IRCv3 message splitting issue where PicoClaw treats split messages as separate entities.

## Bugs & Stability

**Critical (silent failure, no recovery):**
- **#3203** — Matrix sync loop has no reconnection logic. Network disruption or homeserver restart kills the sync loop permanently. No fix PR exists yet. **Severity: High** — users could lose all Matrix functionality without noticing until manual restart.

**Medium Severity:**
- **#3258** — Process Hook `before_tool` modify not working. The decision field is discarded and args are misparsed due to a deserialization defect in v0.3.1. No fix PR linked. **Severity: Medium** — breaks custom tool workflows for users relying on hooks.

**Low Severity:**
- **#3286** — Go and x/text dependency updates to pass `govulncheck`. A fix PR is already open (same number) by imguoguo. **Severity: Low** — security compliance issue, not a runtime bug.

## Feature Requests & Roadmap Signals

**Likely candidates for next release:**
- **DingTalk image support** (#3283) — Already implemented as a PR, merges soon after review. This adds a long-requested media type for DingTalk users.
- **AWS Bedrock prompt caching** (#3163) — The PR has been open since June 23 and is stale, but the feature is well-documented and valuable for cost-sensitive production deployments.

**Community-requested features:**
- **Stateless/no-history gateway sessions** (#3257) — Suggested for CLI users needing fresh conversations without manual session key management. Could be implemented as a `--no-history` flag.
- **IRC long message support** (#3287) — Requests that PicoClaw treat split IRCv3 messages as a single cohesive message. Should be relatively straightforward to implement by buffering split messages with a timeout.

## User Feedback Summary

**Pain points:**
- **Matrix reliability** is the strongest negative signal — the silent death of the sync loop (#3203) can leave users unaware they've lost Matrix connectivity.
- **Tool hook bugs** (#3258) affect users who customize workflows via `before_tool` hooks, reducing trust in the hook system's reliability.
- **Session management friction** (#3257) — CLI users find the gateway mode's session key derivation inflexible for fresh conversations.

**Positive signals:**
- Community members are contributing real fixes (imguoguo, MrTreasure) and cleanups (trufae), indicating a healthy contributor base.
- Feature requests are well-specified with concrete use cases, suggesting users are actively integrating PicoClaw in production.

## Backlog Watch

**Critical attention needed:**
- **#3203** — Matrix reconnection bug (no response from maintainers since July 2). This leaves a core channel unreliable. **Needs immediate maintainer triage.**

**Long-stale items requiring maintainer attention:**
- **#3258** — Tool hook deserialization bug (stale since July 15, last updated July 22). Still unconfirmed by maintainers.
- **#3163** — Bedrock prompt caching PR (stale since June 23). Full implementation exists, needs review and merge.
- **#3222** — DeltaChat refactor PR (stale since July 3). Cleanup of -200LOC, tests dropped, needs review to merge or close.

These stale items risk becoming community friction points — contributors may lose motivation if their work remains unmerged for weeks.

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

**NanoClaw Project Digest — 2026-07-23**

---

## 1. Today’s Overview
NanoClaw sees moderate activity today, driven primarily by three open Pull Requests and one active security-related Issue. No releases were published in the last 24 hours. The project’s pulse remains steady, with ongoing community contributions focused on correctness (WhatsApp identity handling), feature expansion (Telegram rich messages, a Waybar status indicator), and a critical security documentation correction. Maintainer attention is spread across these open items, with none yet merged or closed today.

---

## 2. Releases
No new releases were published in the last 24 hours. The latest stable release remains unchanged.

---

## 3. Project Progress
No Pull Requests were merged or closed in the last 24 hours. All three PRs remain open:
- **#3070** (WhatsApp sender identity divergence fix) — author QuantumBreakz — addresses a cross-path discrepancy between Baileys and Cloud channel user IDs, directly resolving issue #3069. Continued review/feedback pending.
- **#3117** (new skill: `add-omarchy-statusbar`) — a Waybar status indicator for monitoring NanoClaw, contributed as a utility skill. Awaiting merge.
- **#2877** (Telegram native rich rendering via Bot API 10.1 `sendRichMessage`) — an older feature PR (opened 2026-06-28) still in review, updated yesterday.

No substantive feature or bugfix commits were landed today.

---

## 4. Community Hot Topics
- **Issue #3118** (SECURITY.md overclaims) — The only issue updated in the last 24h and the sole open/active issue. It highlights a material inaccuracy in the project’s security documentation regarding per-group credential isolation for OAuth connections on self-hosted OneCLI gateways. Zero comments yet, but the topic touches trust and correct deployment posture — potential for high community interest.
- **PR #2877** (Telegram rich rendering) — An older but active PR that continues to receive updates. Telegram integration is a frequently requested channel, and native rich message support via Bot API 10.1 would be a significant UX improvement. Underlying need: better cross-platform message formatting parity.

No PRs or issues have accumulated significant comment threads or reactions today.

---

## 5. Bugs & Stability
- **Issue #3118** (misleading security documentation) — Severity: Medium-High. While not a code bug, the overclaim of credential isolation could lead users to adopt a false sense of security on self-hosted deployments. No fix PR exists yet. Maintainers should prioritize correcting `docs/SECURITY.md` and/or issuing a clarifying note.
- No crashes, regressions, or runtime bugs were reported in the last 24h.

---

## 6. Feature Requests & Roadmap Signals
- **PR #3117** (Waybar status indicator) — A user-contributed utility skill for Linux desktop monitoring. Signals demand for local system integration and observability beyond chat channels.
- **PR #2877** (Telegram sendRichMessage) — If merged, this would likely land in the next minor release. Telegram channel users are a strong constituency; native rich formatting is a natural progression.
- **PR #3070** (WhatsApp identity normalization) — A correctness fix rather than a new feature, but necessary for multi-path WhatsApp reliability. Likely to be backported or included in next patch.
- No explicit feature requests were filed as issues today; however, the SECURITY.md issue may indirectly trigger a demand for clearer multi-tenant credential documentation or implementation guarantees.

---

## 7. User Feedback Summary
Today’s data reveals limited direct user feedback in issues or PR comments, but the following pain points and use cases are implicitly expressed:
- **Self-hosted deployment confusion**: Issue #3118 highlights that OAuth credential isolation is not as granular as documented, which could frustrate or mislead operators managing multi-agent setups.
- **Cross-path identity consistency**: PR #3070 points to an ongoing challenge when running both Baileys and Cloud WhatsApp paths — users expect a unified identity model.
- **Desktop integration demand**: The Waybar skill PR suggests a user segment that wants NanoClaw status visible without opening a chat interface.
- **Telegram feature parity**: PR #2877 signals user desire for richer Telegram messages, similar to what other platforms already support.

No explicit satisfaction or dissatisfaction signals were recorded.

---

## 8. Backlog Watch
- **PR #2877** (Telegram rich rendering) — Opened 2026-06-28, last updated 2026-07-22. Nearly a month old with no merge decision. This PR is technically ready (follows guidelines) but has been in review limbo. If maintainers intend to accept it, a decision (merge or explicit rejection with rationale) is overdue.
- **Issue #3118** (SECURITY.md overclaim) — Only 1 day old, but given its security implications, it should not languish. It requires a fast maintainer response to correct documentation or explain the actual isolation model.
- No other issues or PRs appear abandoned or unanswered beyond reasonable timeframes.

---

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

# NullClaw Project Digest — 2026-07-23

## 1. Today's Overview
Project activity was minimal today, with only one issue and one pull request updated in the last 24 hours, both of which were closed. No new releases were published. The closed issue (#977) reported a critical Discord connectivity bug affecting all gateway connections, while the closed PR (#978) fixed a related thread crash caused by insufficient stack size. Overall, the project is in a maintenance-focused state, with a high-severity bug resolved but no forward-looking feature work visible in today's data.

## 2. Releases
No new releases were published in the last 24 hours. The latest available release remains unchanged.

## 3. Project Progress
One pull request was merged/closed today:

- **#978 [CLOSED] discord: run typing thread on the heavy runtime stack** — *Author: Tetraslam*  
  Summary: The Discord typing-indicator thread was using `AUXILIARY_LOOP_STACK_SIZE` (512KB), which was insufficient for full HTTPS requests via `std.http.Client` and `std.crypto.tls`. The fix moves the typing thread to a larger stack, preventing process aborts when a turn triggers typing.  
  🔗 [PR #978](https://github.com/nullclaw/nullclaw/pull/978)

This PR directly addresses the crash described in issue #977 (see Bugs section), effectively resolving a critical stability issue.

## 4. Community Hot Topics
Only one issue and one PR were active today, both authored by Tetraslam:

- **#977 [CLOSED] Discord gateway goes permanently deaf after exactly one MESSAGE_CREATE** — *Comments: 1*  
  Users reported a reproducible bug where the Discord gateway becomes unresponsive after processing exactly one message. This generated significant urgency due to its 100% reproducibility and bot-disabling nature.  
  🔗 [Issue #977](https://github.com/nullclaw/nullclaw/issues/977)

- **#978 [CLOSED] discord: run typing thread on the heavy runtime stack** — *Comments: 0*  
  The fix for the above crash was deployed and merged without additional discussion.  

No other issues or PRs generated discussion today.

## 5. Bugs & Stability
One critical bug was identified and fixed today:

- **Bug: Discord gateway becomes permanently deaf after one MESSAGE_CREATE (Issue #977)**  
  **Severity: Critical** — The bot appears online but stops processing any events, making it fully non-functional until restart. Underlying cause: the typing-indicator thread stack overflowed during HTTPS requests, crashing the process.  
  **Fix: PR #978** — Merged and closed on the same day. The fix moves the typing thread to a heavier runtime stack, preventing the overflow.  
  🔗 [Issue #977](https://github.com/nullclaw/nullclaw/issues/977) | [PR #978](https://github.com/nullclaw/nullclaw/pull/978)

No other regressions or crashes were reported today.

## 6. Feature Requests & Roadmap Signals
No new feature requests were visible in today's data. The community energy was entirely focused on resolving a critical connectivity bug. Predictions for next release:  
- The stack-size fix from PR #978 is likely to be rolled into the next patch release.
- No new feature signals were present.

## 7. User Feedback Summary
- **Pain Points:** The primary user complaint is the Discord gateway becoming permanently deaf after a single message — a reliable, bot-breaking failure that forces full restarts. This was the only user-facing issue today.
- **Satisfaction:** The quick turnaround (issue report → fix merge within 24 hours) likely mitigates frustration for affected users.
- **Use Cases:** Users are actively running NullClaw as Discord bots, relying on gateway event processing for core bot functionality.

## 8. Backlog Watch
No long-unanswered issues or PRs were identified in today's data. The only open items were addressed and closed promptly. No stagnation signals detected.

---

*Data source: GitHub data from NullClaw (github.com/nullclaw/nullclaw) for 2026-07-23.*

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw Project Digest — July 23, 2026

## 1. Today's Overview

IronClaw activity is **very high** heading into a launch checkpoint. 50 issues were updated in the last 24 hours (36 open, 14 closed), and 48 PRs were active (26 open, 22 merged/closed). The team is executing a significant **"Completed foundation" retrospective push**, with 12 cleanly closed issues that document major feature deliveries from the past weeks. The most intense focus is on **Reborn error recoverability**, **Telegram channel reliability**, and the **ProductSurface boundary refactor** — the latter suggesting a deep architectural consolidation before a v1 launch. No new releases were cut today, but the release automation PR (#5598) has been open for 20 days, which may indicate a deliberate freeze before the next cut.

## 2. Releases

**No new releases today.** The last pending release PR (#5598) — updating `ironclaw_common` from 0.4.2 → 0.5.0 with breaking changes and `ironclaw_skills` from 0.3.0 → 0.4.0 — remains open and unmerged. Users should be aware that the next release is expected to contain breaking API changes in these crates.

## 3. Project Progress

22 PRs were merged or closed today. Key deliveries:

- **Error Recoverability (#6467, merged):** The first phase of the recoverability contract landed. Typed, host-authored model-error observations now allow recoverable provider failures to be shown to the model without exposing raw diagnostics. Context overflow, invalid model output, and content filtering each get one bounded observation-assisted retry.
- **ProductSurface conversion (#6442, merged):** Local and production runtime assembly collapsed onto the single production-shaped composition path. The dead `build_local_runtime` path and `RuntimeSubstrate::Local` profile predicates were removed.
- **Run failure classification (#6449, merged):** A runner-owned facade now returns lane, retry disposition, and user-facing messages from terminal run failures.
- **CI stabilization (#6452, merged):** Test extension manifests were updated to comply with origin-gate policy, and private-tool installation/dispatch E2E coverage was restored.
- **QA provider journey replay (#6466, merged):** Every harvested QA journey containing a provider call can now be replayed through standalone Reborn, first-party extensions, and Emulate, with deterministic provider ID binding.
- **12 "Completed foundation" issues closed:** These are retrospective records of prior deliveries including generic extension runtime (#6116, merged Jul 22), Telegram production image (#6217, Jul 18), Slack routing/reference (#5898, Jul 10), OAuth hardening (#5957, Jul 13), operator config write plane (#6246, Jul 19), host-managed memory lifecycle (#5327, Jul 20), and more.

## 4. Community Hot Topics

- **[#6284 – Error-Recoverability Endgame Epic](https://github.com/nearai/ironclaw/issues/6284)** (4 comments, 0 👍)  
  The most commented issue defines a high-bar contract: every mid-run error must survive, be visible to the model with both cause and fix, and give the model a turn. This is the project's most ambitious reliability goal. The first PR (#6467) landed today, suggesting strong maintainer commitment.

- **[#6105 – Extension/Channel Lifecycle State-Machine Test](https://github.com/nearai/ironclaw/issues/6105)** (3 comments, 0 👍)  
  The #1 user-facing bug family of the past two weeks — Slack lifecycle regressions across four QA bug-bash waves despite multiple fixes. The issue calls for adding cron-based canary lanes. No PR yet; the signal is that this is a known, painful gap.

- **[#5459 – Configurable Skills and Tools](https://github.com/nearai/ironclaw/issues/5459)** (2 comments, 0 👍)  
  An admin/user permission model for WASM tools and skills. This has been open since June 30 and has no linked PR. It directly relates to the retroactively closed generic extension runtime foundation, suggesting the ability exists but the UX for admin/user configuration may not be exposed yet.

- **[#6472 – Secret-Lease + Egress-Proxy Daemon](https://github.com/nearai/ironclaw/issues/6472)** (1 comment, 0 👍)  
  A brand-new issue describing an in-app daemon for sandbox security: an egress allowlist proxy and secret lease mechanism. Part of a larger secret management epic (#6468). This signals a major security architecture addition.

## 5. Bugs & Stability

**Severity P1 — Telegram:**  
- **[#6475 – `/pair` command not recognized](https://github.com/nearai/ironclaw/issues/6475)** (Telegram P1) — Users trapped in pairing loop. The agent instructs `/pair` but treats it as text. No fix PR linked yet.  
- **[#6474 – Telegram not configurable in Delivery Defaults](https://github.com/nearai/ironclaw/issues/6474)** (P1) — Delivery Defaults page only offers "Web app only." Users cannot configure Telegram or Slack externally.

**Severity P2 — Telegram & WebUI:**  
- **[#6478 – Agent incorrectly redirects to Slack authorization](https://github.com/nearai/ironclaw/issues/6478)** (P2) — Agent doesn't recognize connected Telegram channel.  
- **[#6349 – Telegram chat history rendered inconsistently in WebUI](https://github.com/nearai/ironclaw/issues/6349)** (P2) — Fragmented layout, duplicated prompts, large gaps.

**Launch-blocking checklist bugs:**  
- **[#6521 – CLI not available on agent staging](https://github.com/nearai/ironclaw/issues/6521)** — `ironclaw service restart` command not found when SSO'd into agent.  
- **[#6523 – Agent fails during onboarding with test flag](https://github.com/nearai/ironclaw/issues/6523)** — Setting the "test build" flag causes deployment error.  
- **[#6522 – No instructions for Telegram setup](https://github.com/nearai/ironclaw/issues/6522)** — Missing documentation for Telegram configuration on agent.near.ai.

**Notable:** No fix PRs are linked to these specific bugs yet, but the ongoing PRs on extension readiness (#6520) and OAuth denial lifecycle (#6251) are directly relevant to the channel routing issues.

## 6. Feature Requests & Roadmap Signals

- **Error-Recoverability Endgame (#6284):** This is the highest-priority feature in flight. The first PR (#6467) merged today, bringing typed model-error observations. Expect Phase B (bounded pre-termination warning turns, PR #6530) to merge soon.
- **Secret-Lease + Egress-Proxy Daemon (#6472):** A foundational security capability — sandboxed egress control and secret leasing. Part of epic #6468. Likely Phase A for a v1+ security review.
- **Hermetic Capability Testing Platform (#6524):** Brand new epic today — wants deterministic coverage for every supported capability and critical user journey. This indicates the project is prioritizing test automation as a launch gate.
- **Attested-Signing Stack + Ledger Hardware Wallet (#6532):** A design document for blockchain transaction safety — AI agents that can transact without unilateral money movement. This is a forward-looking roadmap item, likely post-v1.
- **Per-user extension lifecycle and OAuth hardening** has been retroactively marked as "completed foundation" (#6513). The admin-managed user security foundation PR (#6527) is now open, extending this to tenant-admin managed users.

## 7. User Feedback Summary

- **Telegram is the most painful surface:** Three P1/P2 bugs filed today around pairing loops, unreachable configuration, and channel misidentification. Users are clearly trying to use Telegram as a delivery channel and hitting hard UX failures.
- **Onboarding friction:** Launch-checklist issues show that new users cannot deploy an agent without documentation for Telegram setup, and the "test build" flag breaks creation entirely. This suggests confidence in the self-service flow is low.
- **Channel awareness broken:** The agent actively confuses channels — telling users to authorize Slack when Telegram is connected (#6478). This is a fundamental cognitive model problem, not just a UI glitch.
- **Delivery configuration invisible:** Users cannot see or set Telegram/Slack as a delivery default in the WebUI (#6474). The feature exists on the backend but is not surfaced, creating a UX trust gap.

## 8. Backlog Watch

- **[#5459 – Configurable Skills and Tools](https://github.com/nearai/ironclaw/issues/5459)** (23 days open, 2 comments) — No PR linked. The generic extension runtime is now merged, but the admin/user permission model for tool installation remains undocumented.  
- **[#2246 – Unify extension model: MCP tools as single-tool extensions](https://github.com/nearai/ironclaw/issues/2246)** (104 days open, 1 comment) — A core architectural issue. MCP servers still flood the tool list, and provider deduplication is absent. Given that the generic extension runtime is now merged, this issue may be closer to resolution than the comment count suggests.  
- **[#1519 – Routine notifications lack context in chat thread](https://github.com/nearai/ironclaw/issues/1519)** (124 days open, 1 comment) — Notifications are isolated in dedicated routine conversations rather than user chat threads. No recent activity.  
- **[#1330 – Tool schema: expose message routing and attachment semantics](https://github.com/nearai/ironclaw/issues/1330)** (127 days open, 1 comment) — The `message` schema is opaque to models. Runtime routing rules are undocumented. No movement despite being tagged as both bug and enhancement.  
- **[#5598 – Release PR](https://github.com/nearai/ironclaw/pull/5598)** (20 days open) — Blocked by breaking API changes in `ironclaw_common` and `ironclaw_skills`. Community and downstream consumers are waiting. No update since July 3.

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

Here is the LobsterAI project digest for 2026-07-23.

---

## LobsterAI Project Digest — 2026-07-23

### 1. Today's Overview
The project saw moderate maintenance activity with 5 pull requests merged and 1 issue closed in the last 24 hours, indicating a stable, low-bug period. The development focus was on security, UI rendering fixes, and crash prevention, alongside the final closure of several long-standing PRs that had been marked as stale. No new releases were published today, suggesting the team is consolidating recent features rather than packaging them for distribution. Overall, project health appears solid with a healthy throughput of non-trivial fixes.

### 2. Releases
**None.** No new versions were published today.

### 3. Project Progress
All 5 PRs updated today were merged or closed, covering three distinct areas of improvement:

- **Security (Windows):** PR #2377 (`feat: windows update installer hardening`) was merged. This strengthens the Windows installer update pipeline against potential tampering, likely adding digital signature verification or sandboxing.
- **UI/UX Fix:** PR #2376 (`fix(cowork): render export modal above sidebar`) was merged. This resolves a z-index stacking context issue where export modals could appear *behind* the sidebar, using a body portal to guarantee correct layering.
- **Crash Prevention:** PR #2375 (`fix(openclaw): guard against oversized transcript OOM crashes`) was merged. This introduces memory pressure guards to block large transcripts from causing out-of-memory (OOM) crashes, handles OOM-recovery cleanup, and prevents zombie reconnections after a heap restart.
- **Feature Backlog Cleanup:** Two stale PRs ( #1346 – Skills management, #1347 – Cron scheduling enhancement) were closed without merging, likely after being superseded by later work.

### 4. Community Hot Topics
The only active discussion this period was on **Issue #1348** (closed, 2 comments). This issue, raised in April by `xuzx-code`, concerns a missing validation for duplicate names in scheduled tasks. Even though it was closed as stale, the 2 comments indicate a user workflow pain point that may resurface. The linked screenshot suggests a UI dialog where duplicate names are silently accepted (no community link—internal GitHub).

### 5. Bugs & Stability
No new bugs were opened today. One notable stability fix was merged:
- **High Severity – OOM Crash:** PR #2375 fixes an out-of-memory crash caused by loading oversized transcripts in the OpenClaw component. The fix includes blocking oversized payloads *before* they hit the gateway, classifying Heap-OOM crash types, and cleaning up stale connections after a restart. This directly addresses a crash scenario, making it the most critical fix of the day.

### 6. Feature Requests & Roadmap Signals
No new feature requests were filed today. However, the **closure of PR #1347** (Cron custom scheduling, Agent/Model binding, form UX) suggests that a large scheduled-task feature set may have been implemented elsewhere and is no longer pending. The **Skills management** PR (#1346) closure similarly signals that the skills framework is likely already in a newer form. Neither feature appears to be stalled—rather, they appear to have been delivered or supplanted by a later version.

### 7. User Feedback Summary
No explicit user feedback comments were recorded today. The closing of Issue #1348 (duplicate task name validation) suggests a minor but lingering UX annoyance. The fix in PR #2375 indicates that some users were hitting OOM crashes with large transcripts—these users should now see improved stability upon the next release.

### 8. Backlog Watch
- **Issue #1348 (`定时任务名称重复没有校验`)** — Although closed as stale today, this issue about duplicate task name validation had 2 comments and zero reactions. If the validation gap is still present in the live product, it may need a fresh ticket. **No maintainer response was visible in the data.**
- **No other long-unanswered items** were identified in the 24-hour window. The project appears to have a clean backlog for this period.

---

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

Here is the Moltis project digest for **2026-07-23**.

---

## Moltis Project Digest: 2026-07-23

### 1. Today's Overview
Project activity is currently at a low ebb, with only one new Issue and one open Pull Request updated in the last 24 hours, and no new releases. While the single PR indicates continued development (specifically on the web UI), the absence of merged/closed items suggests a slowing of the release cycle. The community remains engaged in a long-running feature discussion regarding model routing, but the overall pace of actionable work is minimal today. The project appears to be in a maintenance or planning phase rather than a rapid development sprint.

### 2. Releases
**None.**
No new releases were created in the reporting period. There are no version changes, breaking changes, or migration notes to report.

### 3. Project Progress
No Pull Requests were merged or closed in the last 24 hours. The only active PR is still open:
- **[PR #1162]** *fix(web): show dates for older sessions* — This is a UI/UX fix aimed at improving session history readability. It introduces localized date labels (e.g., "yesterday", weekday names) for recent sessions and full calendar dates for older ones, including the year when necessary. This fix is still in the review process. 
  [View PR](https://github.com/moltis-org/moltis/pull/1162)

### 4. Community Hot Topics
The most active discussion remains a single long-standing feature request:
- **[Issue #574]** *[Feature]: Model Routing Per topic* (5 comments, 1 👍) — This issue, opened in April, continues to be a focal point. The request is to allow users to route specific conversational topics to different AI models automatically. The high comment count (relative to other issues) suggests significant interest in making multi-model setups more intelligent and context-aware.
  [View Issue](https://github.com/moltis-org/moltis/issues/574)

### 5. Bugs & Stability
No new bugs, crashes, or regressions were reported in the last 24 hours. The one active PR (PR #1162) addresses a user-visible UI issue (poor date formatting for older sessions), but it is a cosmetic fix rather than a critical stability patch. The project is currently stable with no high-severity defects under active investigation.

### 6. Feature Requests & Roadmap Signals
The sole feature request actively discussed today is **Model Routing Per topic** (Issue #574). Given the sustained interest (5 comments spread over months), this is a strong candidate for inclusion in a future minor or major release. Users are looking for dynamic model selection based on conversation context—similar to a routing layer for LLMs. Predicting the next version, this feature is likely to be considered for Q3 or Q4 2026, especially if the community demand grows.

### 7. User Feedback Summary
The user feedback visible in the data centers on a desire for greater intelligent automation in model selection. The primary pain point is that current multi-model setups likely require manual switching or static assignment, whereas users want the system to automatically determine the best model for a given topic. There is no evidence of satisfaction or dissatisfaction with recent releases (as none exist), but the continued interest in Issue #574 implies a latent need for more sophisticated AI orchestration.

### 8. Backlog Watch
The only item requiring attention is **Issue #574** (Model Routing Per topic). While it is actively commented on by users, it has been open for over three months without any official maintainer response or labeling (e.g., "under consideration" or "milestone"). This silence could lead to user frustration. A maintainer update acknowledging the request and outlining potential design considerations would help validate community engagement and manage expectations.
  [View Issue](https://github.com/moltis-org/moltis/issues/574)

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

Here is the project digest for CoPaw (github.com/agentscope-ai/CoPaw) based on the data provided for **2026-07-23**.

---

## CoPaw Project Digest – July 23, 2026

### 1. Today's Overview
CoPaw saw an extremely high activity level in the last 24 hours, with 31 issues and 50 PRs updated. While the team released a minor patch (v2.0.0.post4), the bulk of activity indicates a major stabilization and bug-fixing sprint, driven largely by regressions introduced in the v2.0.0 release. A large number of "first-time contributor" PRs from a single developer (patrick-andstar) targeting system reliability suggests a focused effort to harden the core infrastructure. Despite the high velocity of fixes, a significant number of open bugs related to model compatibility and performance overhead remain.

### 2. Releases
- **New Version:** [v2.0.0.post4](https://github.com/agentscope-ai/QwenPaw/releases/tag/v2.0.0.post4)
- **Changes:** This patch focuses on optimizing agent reasoning to mitigate redundant thinking loops and duplicate tool invocations.
- **Migration Notes:** No breaking changes are documented for this release. Users are advised to update from previous v2.0.0.x versions to resolve the noted loop issues.

### 3. Project Progress
Today, 15 PRs were merged or closed. Key fixes and features that landed include:
- **Context Injection Fixed:** PR [#6359](https://github.com/agentscope-ai/QwenPaw/pull/6359) was merged, changing the context injection role from `system` to `user` to resolve `ValueError` issues on GLM and OpenAI APIs.
- **Token Usage Persistence:** PR [#6375](https://github.com/agentscope-ai/QwenPaw/pull/6375) was closed, fixing a bug where transient write failures could cause token usage data to be lost.
- **Tool Call Robustness:** A fix for tool_call arguments, stripping markdown fences and XML tags, is proposed in PR [#6364](https://github.com/agentscope-ai/QwenPaw/pull/6364).
- **Safety & Governance:** A PR ([#6369](https://github.com/agentscope-ai/QwenPaw/pull/6369)) to honor the `audit_level: none` setting and a PR ([#6357](https://github.com/agentscope-ai/QwenPaw/pull/6357)) to improve the UI for one-time approval permissions are in review.

### 4. Community Hot Topics
The most active discussions are concentrated on critical bugs and feature gaps in the new v2.0.0 architecture:
- **[Performance Regression] Issue #6307** (4 comments): Users are reporting a ~2-second fixed overhead per reply in v2.0.0 compared to v1.x. This is a high-priority concern as it directly impacts user experience for even trivial queries.
- **[Model Compatibility] Issue #6363** (1 comment): A detailed bug report on how models like GLM-5-Turbo and DeepSeek-V3 wrap tool calls in markdown, breaking all tool execution. A fix PR ([#6364](https://github.com/agentscope-ai/QwenPaw/pull/6364)) is already open.
- **[Config Flexibility] Issue #6318** (6 comments): Users are requesting the ability to assign different AI models per conversation, rather than being locked into a single model per agent. This indicates a need for more granular control in multi-use-case setups.
- **[User Onboarding] Issue #6335** (2 comments): A user queries about multi-user support for company deployments, highlighting a gap in the personal-assistant default configuration vs. enterprise needs.

### 5. Bugs & Stability
Bug reports are the dominant topic today, with several critical issues identified:
- **High Severity:** **Process Crashes (Issue #6376)** - A user reports that the new loop feature causes the main process to crash entirely, suggesting inadequate stress testing. **Process Freeze (Issue #5218)** - Sub-agent context compaction freezes the app.
- **High Severity:** **Model Interoperability (Issues #6363, #6358)** - Multiple models (MiniMax-M3, GLM-5-Turbo, DeepSeek-V3) have critical failures with tool calling and context injection. These are cross-cutting issues affecting user choice.
- **Medium Severity:** **Connection Errors (Issue #6314)** - The `RemoteProtocolError` points to an issue with QwenPaw prematurely closing connections to the model backend. **Performance Overhead (Issue #6307)** - The 2-second overhead is a notable regression.
- **Low Severity:** **LaTex Rendering (Issue #6320)** - Fails on Docker deployments. **Windows Test Scripts (Issue #6361)** - Console tests fail on Windows, blocking a segment of contributors.

*Fix PRs exist for issues #6363 (PR #6364), #6358 (PR #6359), and #6374 (PR #6375).*

### 6. Feature Requests & Roadmap Signals
The community is signaling a need for more enterprise and workflow-oriented features. Key requests which are likely candidates for the next minor release include:
- **Per-Conversation Model Selection (Issue #6318):** Following the cron job model override (#6316), this is a logical next step for config flexibility. PRs like [#6353](https://github.com/agentscope-ai/QwenPaw/pull/6353) show the pattern is being explored.
- **Multi-User/Multi-Tenant Support (Issue #6335):** A clear signal of demand for enterprise deployment scenarios.
- **Drag-and-Drop File Upload (Issue #6297):** A high-utility feature for document-centric workflows like contract review. This is likely to be prioritized.
- **Docker Hot-Reload (Issue #6344):** A specific technical request to avoid losing runtime environments during updates, indicating a power-user base.

### 7. User Feedback Summary
User sentiment is currently mixed. While the team is praised for rapid iteration, the stability of the v2.0.0 release is causing significant friction. The primary pain points are:
- **Stability & Reliability:** The crashes (#6376), freezes (#5218), and dropped connections (#6314) are the loudest complaints.
- **Model Compatibility:** Users feel locked out by incompatibilities with non-standard model providers (#6363, #6362).
- **Performance Regression:** The 2-second overhead (#6307) is a tangible downgrade from v1.x for a core action like replying.
- **Lack of Enterprise Features:** Users looking to deploy within companies are hitting walls around multi-user support (#6335).

### 8. Backlog Watch
- **Issue #5135** (Open since 2026-06-11): A long-standing visual capability bug with the MiniMax-M3 model. Despite being raised over a month ago and having a duplicate report today (#6362), it has only one comment. This requires maintainer attention as it affects a specific provider entirely.
- **Issue #6176** (Closed): While closed, the issue regarding the `cron CLI update` command resetting runtime fields is a design flaw that may re-emerge. The fix should be monitored.

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# ZeroClaw Project Digest — 2026-07-23

## 1. Today's Overview

ZeroClaw remains highly active, with 50 issues and 50 PRs updated in the last 24 hours, indicating sustained development velocity. The project is tackling a broad range of architectural improvements, with major infrastructure work on session persistence (adding multiple database backends) and significant proposals around OIDC authentication and observability. The community continues to contribute actively, though a notable Windows-specific CI gap (74 test failures) remains a pressing stability concern. The project shows strong momentum toward v0.9.0, with multiple RFC-tracked features moving through the pipeline.

## 2. Releases

No new releases were published today. The last tracked release target remains v0.9.0.

## 3. Project Progress

**13 PRs were merged or closed today**, representing meaningful progress across several areas:

- **Observability significantly advanced**: PR [#8752](https://github.com/zeroclaw-labs/zeroclaw/pull/8752) (merged) nests memory and RAG spans under the turn trace, closing the remaining slice of [Issue #6641](https://github.com/zeroclaw-labs/zeroclaw/issues/6641) — a key observability enhancement.
- **Firmware/embedded**: PR [#8447](https://github.com/zeroclaw-labs/zeroclaw/pull/8447) (closed) shares protocol parsing with ESP32, reducing code duplication across Pico, Nucleo, and ESP32 firmware.
- **Model reliability improved**: PR [#8684](https://github.com/zeroclaw-labs/zeroclaw/pull/8684) (closed) surfaces model fallback notices on direct-turn surfaces in the runtime reliability layer.
- **Memory system hardened**: PR [#9105](https://github.com/zeroclaw-labs/zeroclaw/pull/9105) (closed) fixes Lucid ARM cold starts by making timeouts configurable and raising defaults.
- **CI/CD enhancements**: PR [#9174](https://github.com/zeroclaw-labs/zeroclaw/pull/9174) (closed) adds broad-channel measurement builds for pre-release validation.
- **ZeroCode initialization**: PR [#9169](https://github.com/zeroclaw-labs/zeroclaw/pull/9169) (closed) adds a 10-second timeout to stalled daemon initialization.
- **Documentation**: PR [#8991](https://github.com/zeroclaw-labs/zeroclaw/pull/8991) (closed) clarifies Bedrock credential profiles and systemd env setup.
- **ZeroCode fixes**: PR [#8779](https://github.com/zeroclaw-labs/zeroclaw/pull/8779) (closed) uses daemon final text when no streaming text was accumulated during a turn.
- **Skill system refactored**: PR [#8638](https://github.com/zeroclaw-labs/zeroclaw/pull/8638) (closed) replaces the built-in ClawHub source with a git-catalog-based skill selector, a breaking change removing `clawhub:slug` support.

## 4. Community Hot Topics

| Item | Type | Comments | Summary |
|------|------|----------|---------|
| [#7462](https://github.com/zeroclaw-labs/zeroclaw/issues/7462) | Issue (Open) | 11 | **74 test failures on Windows** — Unix-only test commands, path semantics, console encoding issues |
| [#6641](https://github.com/zeroclaw-labs/zeroclaw/issues/6641) | Issue (Closed) | 8 | **Turn-level OTel trace correlation** — now resolved via PR #8752 |
| [#7141](https://github.com/zeroclaw-labs/zeroclaw/issues/7141) | Issue (Open) | 7 | **RFC: OIDC authentication provider support** — high-priority security feature for v0.9.0 |
| [#7184](https://github.com/zeroclaw-labs/zeroclaw/issues/7184) | Issue (Closed) | 7 | **RFC: Move translation files to git submodule** — accepted but risk:medium |
| [#7218](https://github.com/zeroclaw-labs/zeroclaw/issues/7218) | Issue (Closed) | 7 | **RFC: A2A agent discovery** — multi-agent interoperability groundwork |

**Analysis**: The highest-engagement threads reveal the community's deep interest in three areas: cross-platform reliability (Windows testing gap), enterprise-grade security (OIDC integration), and multi-agent interoperability (A2A discovery). The volume of RFCs from contributor `singlerider` suggests sustained architectural leadership.

## 5. Bugs & Stability

**Critical/High Severity:**

- **[CRITICAL] Issue #7462** ([Windows CI](https://github.com/zeroclaw-labs/zeroclaw/issues/7462)): **74 test failures on Windows 11** — Unix-only commands in test scripts, path separator assumptions, and console encoding issues. **No fix PR exists yet**; currently unhandled. This represents a major portability gap since CI only runs on Linux.

- **[HIGH] Issue #8837** ([history trimming bug](https://github.com/zeroclaw-labs/zeroclaw/issues/8837)) (now closed): History trimming occurred silently even with pruning disabled, causing agents to lose context mid-session. **Fix appears to have been merged** (closed status).

- **[HIGH] Issue #6724** ([Signal/Voice crashloop](https://github.com/zeroclaw-labs/zeroclaw/issues/6724)): Empty credentials in Signal/Voice Call channels cause supervisor crashloops every ~2 seconds. **Open, no fix PR**.

- **[HIGH] Issue #6916** ([OOM in shell subprocesses](https://github.com/zeroclaw-labs/zeroclaw/issues/6916)): Shell/skill tool subprocesses can allocate unbounded memory, OOMing containers in production. **Open, no fix PR**.

- **[MEDIUM] Issue #6548** ([localization bypass](https://github.com/zeroclaw-labs/zeroclaw/issues/6548)): Channel runtime command replies bypass Fluent localization, breaking non-English locales. **Open, no fix PR**.

**Recently fixed bugs**:
- PR [#9075](https://github.com/zeroclaw-labs/zeroclaw/pull/9075) (open) aims to fix `models_cache.json` not being persisted after refresh.
- PR [#8781](https://github.com/zeroclaw-labs/zeroclaw/pull/8781) (open) removes stale advisory ignores for security advisories on removed dependencies.
- PR [#8996](https://github.com/zeroclaw-labs/zeroclaw/pull/8996) (open) fixes running goals not being preserved across daemon reload.

## 6. Feature Requests & Roadmap Signals

**Likely for v0.9.0** (highly active RFC-tracked items):

1. **OIDC Authentication** ([#7141](https://github.com/zeroclaw-labs/zeroclaw/issues/7141)) — high-priority security feature with defined delivery breakdown. Likely to land in next major release.

2. **Per-model capability configuration** ([#7100](https://github.com/zeroclaw-labs/zeroclaw/issues/7100)) — vision/context_window config per model, with UI indicators. Priority P1.

3. **Agent evaluation harness** ([#7065](https://github.com/zeroclaw-labs/zeroclaw/issues/7065)) — `zeroclaw eval` command for replay + live model evaluation. Priority P2, in-progress.

4. **Structured observability** ([#7232](https://github.com/zeroclaw-labs/zeroclaw/issues/7232)) — rich events, trace correlation, bridge refactoring. Priority P2.

5. **Session persistence backends** ([PR #9250](https://github.com/zeroclaw-labs/zeroclaw/pull/9250), [#9251](https://github.com/zeroclaw-labs/zeroclaw/pull/9251), [#9252](https://github.com/zeroclaw-labs/zeroclaw/pull/9252), [#9254](https://github.com/zeroclaw-labs/zeroclaw/pull/9254)) — massive infrastructure PR series adding MySQL, MariaDB, PostgreSQL, Oracle, and (deferred) IBM Db2 backends.

**User-requested channels** (all P2, high engagement):
- [#6423](https://github.com/zeroclaw-labs/zeroclaw/issues/6423) — Mastodon (ActivityPub) channel
- [#6427](https://github.com/zeroclaw-labs/zeroclaw/issues/6427) — Twilio SMS channel
- [#6435](https://github.com/zeroclaw-labs/zeroclaw/issues/6435) — Rocket.Chat channel
- [#6437](https://github.com/zeroclaw-labs/zeroclaw/issues/6437) — Zulip channel

## 7. User Feedback Summary

**Positive signals**: Community engagement remains high with 11-comment threads and active RFC discussion. Contributors like `Project516`, `Audacity88`, and `IftekharUddin` are driving significant quality improvements.

**Pain points expressed**:

1. **Windows portability gap** ([#7462](https://github.com/zeroclaw-labs/zeroclaw/issues/7462)): A Chinese Windows user reported 74 failures, highlighting that the project's CI only tests on Linux. This is the loudest user complaint today.

2. **Configuration/debugging friction**: Multiple users reported difficulty with config validation ([#6416](https://github.com/zeroclaw-labs/zeroclaw/issues/6416)), model switching confusion ([#6557](https://github.com/zeroclaw-labs/zeroclaw/issues/6557)), and missing state persistence after commands ([PR #9075](https://github.com/zeroclaw-labs/zeroclaw/pull/9075)).

3. **Security concerns**: User `sken130` ([#6613](https://github.com/zeroclaw-labs/zeroclaw/issues/6613)) explicitly flagged the 6-digit pairing code as "too weak," requesting alphanumeric + longer defaults.

4. **Documentation gaps**: User `ngamradt` ([#8925](https://github.com/zeroclaw-labs/zeroclaw/issues/8925)) struggled with Bedrock credential configuration and systemd service setup, prompting a documentation fix (PR #8991).

5. **Context loss**: User `susyabashti` ([#8837](https://github.com/zeroclaw-labs/zeroclaw/issues/8837), now closed) reported silent history trimming causing agents to "do something else completely" mid-session — a significant UX degradation.

## 8. Backlog Watch

**High-risk items needing maintainer attention:**

1. **Issue #7462** ([Windows CI](https://github.com/zeroclaw-labs/zeroclaw/issues/7462)) — 74 test failures on Windows, **no fix PR**. Last updated 2026-07-22. Risk: high, Priority P1. The most critical unaddressed item.

2. **Issue #6916** ([OOM in shell subprocesses](https://github.com/zeroclaw-labs/zeroclaw/issues/6916)) — Production OOM scenario, last updated 2026-07-22, **no fix PR**. Risk: high, Priority P1.

3. **Issue #6613** ([weak pairing code](https://github.com/zeroclaw-labs/zeroclaw/issues/6613)) — Security concern open since 2026-05-13, last updated 2026-07-22, **high risk, no fix PR**. Priority P1.

4. **Issue #6391** ([real heartbeat tracking](https://github.com/zeroclaw-labs/zeroclaw/issues/6391)) — Daemon node liveness detection open since 2026-05-05, **no fix PR** despite "no-stale" label. Risk: high.

5. **Issue #6917** ([Composio action-scope filter](https://github.com/zeroclaw-labs/zeroclaw/issues/6917)) — Security gap in tool dispatch, open since 2026-05-25, **no fix PR**. Risk: high.

6. **PR #8781** ([advisory ignore cleanup](https://github.com/zeroclaw-labs/zeroclaw/pull/8781)) — Labeled `needs-author-action` since 2026-07-06 — stale advisory ignores could mask real vulnerabilities.

7. **PR #8996** ([goal preservation](https://github.com/zeroclaw-labs/zeroclaw/pull/8996)) — Labeled `needs-author-action` since 2026-07-11 — a large fix affecting runtime stability across many channels.

**Long-stale high-priority items**: Issues #6390, #6416, #6548, #6724, #6346 are all marked `no-stale` but have open status with no fix PRs, despite being opened in early May 2026 — now over 2.5 months old.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/kky-wollu/agents-radar).*