# MilestonePay AI

**Verify the work. Approve the payment. Trust the process.**

MilestonePay AI is a hackathon prototype: AI evaluates evidence against the acceptance criteria of one digital-service milestone; the **buyer** makes the final decision on a **PayPal Sandbox** authorization/capture.

> **Not escrow.** This is single-merchant, sandbox-only delayed capture; no funds custody, marketplace, third-party freelancer payouts, payment guarantees, or autonomous settlement. The contributor persona submits evidence but does not receive a payout.

## Current state

**Phase MP-A0: greenfield repository initialization, documentation only.** No Next.js app, real PayPal Sandbox transaction, AI verification, independent audit, deployment, or Devpost submission has been implemented or verified. Do not portray the specification as working code.

The first PR is intentionally docs/configuration-only under the inherited human-gated AI-native engineering model. Product UI development must follow requirements → screen map → screen designs → explicit owner visual approval → shell → integration.

## Architecture direction

- **Web:** Next.js + TypeScript and an accessible, responsive UI (after design approval)
- **Auth/data:** Supabase Auth, Postgres + row-level security, private evidence storage
- **AI:** Gemini 3.8 Flash (`gemini-3.8-flash`, planned server-only `@google/genai`), structured/citation-validated output; advisory only. See [ADR-002](docs/ADR-002-GEMINI-PRIMARY.md) and [AI contract](docs/AI-VERIFICATION-CONTRACT.md).
- **Payments:** fixed PayPal Sandbox merchant, Orders v2 AUTHORIZE; Payments v2 capture/void; verified webhooks and durable idempotency
- **QA:** unit/integration tests, Playwright, real Sandbox evidence, separate exact-head security review

No provider credentials belong in Git or client bundles. Local setup values are documented in [`.env.example`](.env.example); they are **not** active integrations yet.

## Start here

1. Read [`AGENTS.md`](AGENTS.md), [`docs/STATUS.md`](docs/STATUS.md) and [`config/project-profile.json`](config/project-profile.json).
2. Read [`docs/MILESTONEPAY-SPEC-v1.md`](docs/MILESTONEPAY-SPEC-v1.md) and [`docs/ADR-001-SINGLE-MERCHANT.md`](docs/ADR-001-SINGLE-MERCHANT.md).
3. Follow [`tasks/MP-A0-greenfield-initialization.md`](tasks/MP-A0-greenfield-initialization.md), [`docs/UI-MAP.md`](docs/UI-MAP.md) and the [`docs/IMPLEMENTATION-HANDOFF.md`](docs/IMPLEMENTATION-HANDOFF.md).
4. Check repository profile validity with `python3 scripts/validate_project_profile.py --repository mrdzyn/milestonepay-ai` after cloning this proposed branch.
5. Only after independent review and owner approval, begin the separate implementation/UI milestone. App-specific `npm ci`, build and tests are **not yet configured**, and must not be claimed as PASS.

## Repo quality and safety

The inherited `.github/workflows/ci.yml` and `common-validation.yml` are retained. Hosted GitHub Actions should be treated as **NOT PASS** until a real run completes; if blocked by account credits, collect equivalent local evidence and seek a narrowly scoped owner exception rather than weakening checks. A public demo must not include real money or real customer data.

## Hackathon

Planned build window: Oct 25–Nov 11, 2026. Submission deadline: **Nov 12, 2026, 12:00 PST / Nov 13, 04:00 PHT**. Final Devpost copy must describe verified implementation rather than aspirations.

**License:** MIT (subject to third-party license review before release).
