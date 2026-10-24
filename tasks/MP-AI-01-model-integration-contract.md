# MP-AI-01 — Gemini primary-provider specification (docs only)

**Owner decision:** Use Google Gemini 3.8 Flash with medium thinking.  
**Base:** the unmerged MP-A0 Draft PR #1 at `55bbde025ccbee8bffa43d8ffc99c35b45bc5845`.  
**Branch:** `docs/mp-ai-01-gemini-integration-contract`, Draft PR stacked on MP-A0.

**Objective:** Document the selected model, server-only AI contract, strict evidence-linked JSON schema, negative controls and implementation requirements without running or integrating a model.

**Allowed:** relevant docs, status/handoffs, project memory, `.env.example`, task specification. **Forbidden:** code/dependencies/credentials, provider calls, payment changes, any production operation, CI bypass, merge, deploy, UI shell.

**UI gate:** Not applicable, docs-only.

**Acceptance:** API model ID/medium thinking verified against official docs; no AI tool access; buyer capture authority unaffected; real evidence IDs and version checks mandatory; AI-01..AI-12 documented; 32 MP acceptance IDs and 18-day schedule preserved; Python profile validation and independent exact-head doc audit requested; no tests/CI falsely labeled PASS.

**Reviewer handoff:** independently examine full diff versus MP-A0, source docs, selection/terms, payment safety, status, schema and negative cases. Report PASS/PARTIAL/FIX REQUIRED and await owner approval. No automatic merge.
