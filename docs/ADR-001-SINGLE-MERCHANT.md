# ADR-001 — Single-merchant PayPal Sandbox with human-controlled capture

**Status:** Accepted for hackathon specification; implementation pending. **Date:** 2026-10-24.

## Decision
Model one merchant's fixed-price, single-milestone Sandbox checkout, with separate buyer and contributor application roles. Contributor is not a PayPal payee. Buyer approves and authorizes the payment through PayPal; afterward an AI assessment supports (but never triggers) a distinct explicit buyer capture-or-void decision. Exactly one fixed-amount full capture is permitted. PayPal is the payment processor, not an app-controlled trust/escrow account.

## Why
Hackathon judges need visible, real PayPal integration and defensible AI value in 18 days. An escrow/multi-vendor implementation would require features, agreements, policies, and compliance outside this schedule and could misrepresent PayPal authorization.

## Controls
- `PAYPAL_ENV=sandbox`; host allowlist fails closed for live endpoints
- Merchant identity and USD amount loaded from trusted backend data; never from the browser, contributor, or model
- Authorization is a temporary provider state, not guaranteed settlement; recommend a 48-hour demo with no automatic capture
- Stable operation keys + DB reservation + verified webhook reconciliation
- No AI tool/function access to Orders authorize, Payments capture or void
- No partner payee/platform fee or payouts, refunds, escrow, disputes, production payments

## Rejected
Marketplace payouts, escrow custody, automatic AI clearance of funds, multiple captures, and live transactions. Each requires new product/security/legal approval; none is silently imported from the hackathon concept.

## Consequences
The demonstration is a single-merchant acceptance-and-payment workflow, not a payment marketplace. UI/copy must state this. Independent security review must verify no implementation path exceeds these boundaries.
