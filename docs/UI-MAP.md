# MP-A1 — UI planning gate (not yet approved)

**Status:** Screen inventory only. There are no approved Figma designs or implementation shells.

## Screens and journeys
1. Landing + explicit Sandbox-only disclaimer, links to buyer/contributor sign-in.
2. Buyer overview: draft/authorized/review-ready/captured/voided/reconciling milestones.
3. Create/freeze one milestone: title, USD integer cents $1–$200, 2–5 criteria, AI suggestions marked advisory.
4. PayPal authorization screen: exact merchant/amount confirmation, JS SDK buyer approval, pending/cancel/failure states.
5. Contributor evidence form: criteria-bound entries and safe optional image; read-only frozen criteria.
6. AI verification report: criterion result + actual evidence IDs, uncertainty, model metadata and missing evidence.
7. Buyer decision: explicit capture checkbox with exact fixed merchant/amount, separate request revision and void actions; guard against stale/unknown states.
8. Audit timeline: verifiable provider IDs/statuses, approval actor, hashes, revision history, redacted downloadable data only if authorized.

## Required states
Empty, loading, success, network retry, disconnected/UNKNOWN payment state, denied permissions, expired authorization, stale evidence, evidence validation failures, incomplete AI response, mobile reflow and disabled destructive controls.

## Visual/accessibility gate
Use inherited web design profile, semantic tokens, WCAG 2.2 AA target and keyboard-first flows. Produce reviewable mockups and get explicit owner visual approval **before building the material UI shell**. No payment features may be inferred from visual mockups.
