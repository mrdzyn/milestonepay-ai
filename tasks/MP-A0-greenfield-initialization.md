# Task MP-A0 — Greenfield template initialization

**Goal:** Make `mrdzyn/milestonepay-ai` a project-mode, docs-first child of the AI-native engineering template without weakening its CI/security/human review gates.

**Allowed:** configuration profile, product/architecture/security/testing/release docs, design map, source spec/handoff/Devpost planning drafts, clean template inventory, appropriate LICENSE/.env.example/.gitignore hygiene, task and status.

**Forbidden:** implementing payment operations, new live credentials, escrow, payout features, UI shell before design signoff, production release or merge, bypassing CI or deleting reusable common validation.

## Acceptance
- `repositoryMode=project`, design enabled, web selected, store releases and integrations unselected.
- Master-only handoff/memory/task blocks and master-only workflow/validators removed; common-validation caller/callee and project-profile validator retained.
- Root README and canonical product architecture/status accurately describe the single fixed merchant and lack of implementation.
- AI output cannot be mistaken for payment authorization; explicit human capture constraint recorded in ADR and security policy.
- `docs/MILESTONEPAY-SPEC-v1.md` contains all 32 test IDs and 18 calendar milestones.
- `python3 scripts/validate_project_profile.py --repository mrdzyn/milestonepay-ai` actually passes at final branch head, or is explicitly NOT RUN with blocker recorded.
- No secrets, production host, real user data, deployment, or merge.

## Independent audit
Verify exact remote SHA; compare retained and pruned paths against `docs/REPOSITORY-SETUP.md`; check all referenced docs, source statements and workflow structure; run validator; report PASS/PARTIAL/FIX REQUIRED. Separate reviewer only. No claims of hosted CI execution without real GitHub run.

## Next task (not authorized here)
MP-A1: requirements refinement, interactive screen map, accessible web design proposals and explicit owner signoff; only later Next.js shell and integration.
