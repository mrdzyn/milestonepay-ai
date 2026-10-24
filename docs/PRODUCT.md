# MilestonePay AI — Product Definition

## Identity
- **Name:** MilestonePay AI
- **Tagline:** Verify the work. Approve the payment. Trust the process.
- **Owner:** Repository owner `mrdzyn`; product direction and risk approvals remain human-owned.
- **Stage:** Hackathon P0 specification / repository initialization, no running application yet.
- **Distribution:** Public open-source web demo; no live payment offering or app-store release; proposed MIT license.

## Problem and users
A buyer needs to decide whether agreed digital work meets measurable criteria before authorizing payment capture. A merchant's contributor submits evidence. Neither AI reasoning nor screenshots should be presented as guaranteed proof. Buyer and contributor accounts are fictional in the hackathon demo.

## Scope
A buyer freezes 2–5 criteria and a USD $1–$200 price; the buyer uses PayPal Sandbox to authorize for one configured merchant. The contributor submits at most five text entries and an optional safe image. A real AI model returns evidence IDs and criterion-level SUPPORTED/GAP/UNVERIFIABLE findings. The buyer explicitly approves capture or voids the active authorization; a verified PayPal response/webhook determines the payment status. Immutable audit history identifies each source.

## Hard boundaries
**No escrow, third-party seller payouts, partner fees, autonomous capture, automatic void, real-money mode, refunds, partial captures, multi-merchant onboarding or arbitration.** An authorization is not escrow and capture is not guaranteed; encourage a 48-hour workflow and disclose PayPal's recommended capture window. No agent or model directly calls payment APIs.

## Outcomes / acceptance
- A reproducible true Sandbox authorize → review → human-approved full capture demonstration.
- A separate true Sandbox authorization void example.
- Negative controls for cross-user access, stale evidence, forged webhooks, duplicate captures, prompt injection, and failing AI output.
- Exact-head independent audit and objective human QA prior to any submission claims.

## Plan and authority
The definitive detailed spec, 18-day milestones and 32 test IDs are in `docs/MILESTONEPAY-SPEC-v1.md`. Material scope, risk, AI provider, and release decisions require explicit owner approval.
