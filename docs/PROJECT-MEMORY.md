# Project Memory

## Purpose

This file preserves **durable project knowledge** across chats, archived threads, AI agents, and team handoffs.

It is primarily a continuity contract between the project owner and the project orchestrator.

It is **not**:
- a chat transcript;
- a changelog;
- a backlog;
- meeting notes;
- a duplicate of `docs/STATUS.md`;
- default startup context for every coding agent.

## Coding-agent policy

Coding agents should **not** read this file by default.

The normal startup order remains:

1. `AGENTS.md`
2. `docs/STATUS.md`
3. `config/project-profile.json`
4. task-specific design/docs
5. relevant code/tests

Agents may consult this file only when:
- explicitly directed by the project owner or orchestrator;
- durable historical rationale is genuinely needed for the task; or
- the assigned task specifically involves updating project memory.

## What belongs here

Record information that is likely to remain useful for months or across major phases:

### Locked product decisions
- Product identity, audience, platform scope, or behavior that has been deliberately settled.

### Architecture decisions and rationale
- Important architectural choices and the reasons behind them.
- Meaningful rejected alternatives when that context prevents future rework.

### Implementation and testing lessons
- Non-obvious lessons that future agents would otherwise rediscover.
- Important platform/toolchain limitations.

### Integration constraints
- Stable external API, store, infrastructure, protocol, or vendor constraints.

### Security and privacy boundaries
- Durable trust boundaries, data-handling rules, offline/online boundaries, authentication principles, or compliance constraints.

### Commercialization and launch decisions
- Stable licensing, pricing-model, distribution-channel, store, or launch decisions.

### Stable terminology
- Canonical names for products, modules, roles, flows, and domain concepts.

## What does not belong here

Do not add:
- every completed ticket;
- transient debugging notes;
- temporary blockers;
- daily progress;
- raw agent output;
- build logs;
- routine version bumps;
- duplicate architecture text already maintained elsewhere.

## Durable memory entries

### MP-M001 — Human-controlled PayPal Sandbox settlement
**Decision:** This is one fixed Sandbox merchant, one USD milestone, full capture only, explicit buyer decision, no escrow, no third-party payouts, no live payments and no AI-initiated capture/void.

**Rationale:** Preserve meaningful PayPal API proof without misrepresenting payment authorization as custody or asking an unreliable AI to settle funds.

### MP-M002 — Evidence-limited AI
**Decision:** Model output is advisory, evidence-referenced, strictly validated, and never granted payment-tool permissions.

**Rationale:** Evidence quality and unverifiable observations must remain visible to the buyer rather than being converted into guarantees.

### MP-M003 — Repo and review gates
**Decision:** Preserve the AI-native template's independent exact-head audit, objective tests, design-first approval and human merge/release gates.

**Rationale:** A short hackathon schedule does not justify silently bypassing controls.


### MP-M004 — Primary AI model decision (October 24, 2026)
**Decision:** Select Google Gemini 3.8 Flash (`gemini-3.8-flash`) via an official server-side adapter and medium thinking as the sole hackathon MVP model. AI output is citation-validated, advisory only; no automatic model fallback or PayPal tools.

**Rationale:** Multimodal structured evidence review is feasible for the 18-day prototype while maintaining human-approved PayPal payment control. ADR-002 contains the binding technical contract.

## Maintenance rule

When adding an entry:
- assign the next memory ID;
- describe the decision/lesson clearly;
- include rationale;
- avoid temporary implementation detail;
- update an existing entry rather than creating contradictory duplicates when a durable decision changes.
