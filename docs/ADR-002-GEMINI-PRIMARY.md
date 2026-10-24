# ADR-002 — Select Google Gemini 3.8 Flash

**Decision date:** October 24, 2026 | **Status:** Owner-selected specification, not implemented.

## Choice and constraints

MilestonePay's single MVP AI model is **Google Gemini 3.8 Flash**, stable API ID `gemini-3.8-flash`, called from the **server** using the official **`@google/genai`** TypeScript SDK. Default thinking level is **medium** (available: low, medium, high; minimal is unsupported). Do not use preview/latest aliases or silently substitute another model. A provider-neutral adapter is permitted for maintainability, but there is **no automatic model fallback**. Changing the model/provider requires an approved ADR revision.

Official sources checked October 24, 2026:
- https://ai.google.dev/gemini-api/docs/models/gemini-3.8-flash
- https://ai.google.dev/gemini-api/docs/thinking
- https://ai.google.dev/gemini-api/docs/structured-output
- https://ai.google.dev/gemini-api/terms

Configuration for future code (not a working integration): `AI_PROVIDER=google`, `AI_MODEL=gemini-3.8-flash`, `AI_THINKING_LEVEL=medium`, and server-only `GEMINI_API_KEY`. SDK version/endpoint compatibility, project availability, quotas, and actual model execution must be verified during implementation.

## Exactly two authorized AI capabilities

1. **Criteria suggestion:** transform a buyer's draft into 2–5 *proposed* measurable acceptance criteria. The buyer manually confirms and the backend freezes the resulting contract; AI cannot modify it later.
2. **Evidence assessment:** interpret frozen criteria and versioned evidence (text, optional sanitized PNG/JPEG) and produce citation-linked `SUPPORTED` / `GAP` / `UNVERIFIABLE` per criterion. A screenshot cannot independently prove code execution, accessibility, security, uptime, or feature correctness.

**The AI is an advisory subsystem only.** It never receives PayPal OAuth tokens, merchant credentials, Supabase privileged keys, or payment controller tools. Do not enable search, URL context, function calling, code execution, computer use, file search or web retrieval. User-submitted evidence and model output are untrusted; provider output does **not** make any payment decision or mutate payment state.

Only authenticated, explicitly consenting buyer actions, followed by independent backend checks, can invoke sandbox capture/void. No escrow, autonomous settlement, external payouts, or live PayPal configuration.

## Output, failures and privacy

Ask for schema-constrained JSON; then independently revalidate in server code: required types/enums, exact frozen criterion IDs, actual current evidence citations, uniqueness, length bounds and manifest hash freshness. Server assigns the model ID, prompt/schema version and input hashes; never trust those values from the model. Refusals, invalid output, stale data, 429s and timeouts become **unavailable/unverifiable**, not fabricated passes. Separate buyer and payment authorization conditions remain required even when evidence is marked SUPPORTED.

Transmit only consented/minimized synthetic hackathon evidence; no buyer credentials, payment IDs, personal contact details or private URLs. Images require consent. API terms differ by free/paid tier; verify the actual account's permitted data use before ingesting personal information. Set spend caps, timeout, size limits, request budgets and redacted logging on implementation. Do not assert a pricing plan or model service is already configured.

## Verification and follow-on work

`docs/AI-VERIFICATION-CONTRACT.md` defines implementation schema, fixture tests and fail-closed guarantees. MP-AI-01 records the decision only. An eventual implementation requires one **real** Gemini call with redacted evidence plus independent tests, separate exact-head audit, and a human merge gate. No package, server route, SDK dependency, API key, or PayPal configuration is added by this ADR.
