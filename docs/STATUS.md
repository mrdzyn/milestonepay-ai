# MilestonePay AI — Project Status

## Project
- **Current phase:** MP-A0 — greenfield template initialization
- **Status:** Draft initialization change, **not** independently audited; no running app
- **Primary branch:** `main`
- **Working branch:** `chore/mp-a0-greenfield-bootstrap`
- **Base SHA:** `01de15e4a847f3536c6957853882705f54d714f6`
- **PR:** Draft PR to be opened after bootstrap commit
- **Active task:** `tasks/MP-A0-greenfield-initialization.md`
- **Active handoff:** None

## Completed
- Existing repository was created from `mrdzyn/ai-native-project-template`.
- MilestonePay product specification and owner-selected scope exist as planning artifacts.
- A bootstrap change is proposed on a dedicated branch.

## NOT DONE / NOT TESTED
- Greenfield pruning and project profile validation: pending final exact-head validation.
- Independent project initialization audit: pending.
- Next.js scaffolding, Supabase schema, payment controller, real PayPal Sandbox operations, AI calls, design approval, QA, public deployment, and Devpost submission: NOT IMPLEMENTED.
- GitHub branch protection/rulesets and hosted CI on this repository: NOT VERIFIED. No CI exception has been granted for this PR.

## Next actions
1. Run the project-profile validator against the exact bootstrap branch; independently confirm pruned inventory and locked payment boundaries.
2. Audit the Draft PR independently at exact remote HEAD, mark PASS / FIX REQUIRED without inventing tests.
3. Obtain explicit owner approval to merge the initialization PR.
4. Begin screen map/mockup design review, then separate bounded implementation milestones only after owner design approval.

## Locked boundaries
PayPal Sandbox only; one fixed merchant; human-approved capture; no escrow, third-party payouts, live payments or AI-initiated money movement.
