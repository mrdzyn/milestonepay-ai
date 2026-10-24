# MilestonePay AI — Codex Implementation Handoff

**Task:** Implement the 18-day PayPal AI Hackathon P0 product using `MilestonePay_AI_Product_Spec_v1.md` as the source of truth.  
**Status:** Implementation has not started. This is a ready-to-paste task description, not an executed instruction.

## Owner direction (copy/paste into coding agent)

Initialize and build the existing public repository `mrdzyn/milestonepay-ai` from its AI-native project template. Preserve the core operating model and project profile; greenfield bootstrap is proposed in a Draft PR.  Work in focused branches and Draft PRs; do not merge, deploy, connect live payments, publish submission materials, or make discretionary product-direction changes without explicit owner approval. Read the full product spec first.

**Absolute payment scope:** PayPal **Sandbox only**; single fixed business merchant/payee; buyer uses a different personal sandbox account; one USD milestone and full-amount authorization/capture; NO escrow, marketplace, multi-seller payouts, partner fee features, refunds, delayed disbursement, autonomous capture, or live mode. Contributor persona submits evidence but is not a payee. PayPal authorization is a temporary hold with 3-day recommended capture window, not guaranteed money or escrow. Design for a 48-hour demonstration lifecycle.

**Stack:** TypeScript/Next.js, Supabase Auth/Postgres with RLS, official PayPal JS SDK + REST Orders v2/Payments v2, actual selected AI model with strict schema, Vitest/Playwright. Use synthetic data and explicit `PayPal Sandbox — no real money` labels throughout.

**Implementation order and staged deliverables:**

1. `MP-A0`: Repo, README, MIT LICENSE, branch policy, threat model and ADR single-merchant; environment placeholders, clean install, schema + seed + role denial tests.
2. `MP-A1`: Contract draft/criteria/freeze, precise USD cents, immutable hash, buyer/contributor secure screens and accessibility.
3. `MP-A2`: **REAL sandbox integration** for create AUTHORIZE order, PayPal SDK approval, server authorization, explicit buyer-led capture, alternate void, reconciliation and signature-verified webhooks. Record redacted actual IDs; no mocks counted as sandbox success.
4. `MP-A3`: Evidence entry, hashes, private data; AI criteria suggestion and evidence-level verification with source IDs, uncertainty, invalid-output guards, prompt-injection negative controls.
5. `MP-A4`: Buyer review, consent/freshness guard, audit timeline, responsive UI and complete test suite including concurrency/timeouts.
6. `MP-A5`: Fresh-clone independent audit, owner manual QA, remediation/re-audit at exact remote HEAD, judge-ready instructions, 165-second demo script, Devpost draft and release evidence.

**Every increment must:** show exact branch/HEAD, changed paths, real commands + exit codes, tests passed/failed/not run, new evidence, follow-up risks, and owner decision needed. Always update `docs/STATUS.md` and `docs/HANDOFFS.md`; leave Draft PR until owner instructs otherwise. Do not present an implementation as audit PASS without a separate auditor's explicit verified verdict.

**Nonnegotiable acceptance gates:**
- Correct real PayPal order, authorization, and capture IDs in sandbox; separate void flow.
- Server-side buyer permission and immutable amount/merchant checks at every payment step.
- Double capture, stale report, forged webhook, contributor-initiated capture, cross-user contract ID, and AI-injected commands fail safely.
- Idempotent requests persisted before PayPal network request; timeout reconciliation instead of blind replay.
- No AI/model interface can call capture or void; AI only returns strict criterion evidence JSON.
- Invalid AI results become `UNVERIFIABLE` / error, never acceptance proof.
- Security credentials never committed, echoed, or exposed to JS bundle.
- Payment status is grounded in PayPal verified data; app status cannot falsely claim paid.
- Tests have actual outputs and negative controls. Record `NOT TESTED` explicitly.
- Public open source repo + real runtime instructions + under-three-minute YouTube recording are checked against exact final SHA.

**Stop conditions:** If a real sandbox transaction cannot be made, stop downstream feature claiming and report blocking PayPal setup evidence. If an audit reveals a payment authorization vulnerability, capture duplication, leaked secrets, unauthenticated webhook mutation, or false payment proof, mark `FIX REQUIRED`; no merge/deploy/submission claims. If hosted CI cannot run, run and retain local equivalents with a scoped exception request; never relabel hosted CI as passed.

## Recommended first deliverable / handoff

Produce a docs-only PR containing the product specification, `ADR-001-SANDBOX-SINGLE-MERCHANT.md`, threat model, machine-readable acceptance matrix, 18-day plan and evidence conventions; run lint/validation that applies to docs; request an independent *spec audit* before writing the payment integration. Ask for approval to begin actual implementation only after scope is understood. Never block progress to ask questions whose answers are already in the source spec.

## Expected status report format

```text
MilestonePay AI / [increment] — PASS | PARTIAL | FIX REQUIRED
Branch:
Exact local HEAD / remote HEAD:
Changed files:
Implemented:
Real PayPal evidence (redacted IDs/status):
Real AI evidence (provider/model, schema result):
Commands and observed exit codes:
Tests PASS / FAIL / NOT RUN:
Security boundary checks:
Independent audit (reviewer, scope, exact SHA, verdict):
Risks/blockers:
Next smallest handoff:
Owner decision (if needed):
```

**References:** See the main spec's official PayPal and Devpost URLs; check docs again before implementing requests that affect funds.