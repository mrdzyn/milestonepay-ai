# MP-AI-01 — Gemini AI interface and acceptance contract

**Status:** Draft implementation contract; NO runtime AI integration, no API invocation and no payment permission.

## Planned server-only provider adapter

```ts
type Criterion = { id: string; description: string };
type Evidence = { id: string; criterionIds: string[]; kind: "text" | "image"; sanitizedText?: string };
type Verdict = "SUPPORTED" | "GAP" | "UNVERIFIABLE";
type Assessment = { results: Array<{ criterionId: string; verdict: Verdict;
  evidenceIds: string[]; reason: string; limitations: string }>; summary: string };

interface VerificationProvider {
  suggestCriteria(input: { buyerDraft: string; requestId: string }):
    Promise<{ suggestions: Array<{ description: string }> }>;
  assessEvidence(input: {
    requestId: string;
    contractVersionHash: string; evidenceManifestHash: string;
    criteria: Criterion[]; evidence: Evidence[];
  }): Promise<Assessment>;
}
```

The verification service—not the model—calculates the trusted input snapshot hashes; assigns provider/model metadata, timestamps, schema/prompt version and user ownership; then stores read-only assessment history. The provider cannot write payment state.

## Wire-format example

```json
{
  "results": [
    {
      "criterionId": "criterion-1",
      "verdict": "SUPPORTED",
      "evidenceIds": ["evidence-1"],
      "reason": "The submitted screenshot shows a navigation menu.",
      "limitations": "It does not prove the menu works on a real mobile device."
    }
  ],
  "summary": "Additional manual verification is necessary."
}
```

The Gemini SDK should use `model: "gemini-3.8-flash"`, `generation_config.thinking_level: "medium"`, and schema-constrained `application/json` (`response_format`, Interactions API), without tools. Confirm installed SDK API/types before coding, since APIs evolve. Also validate with a strict runtime schema (e.g. Zod) and an independent semantic validator. JSON schema alone is not security verification.

## Mandatory validation

- Exactly one result for **each** frozen criterion; reject missing/extra/duplicate criterion IDs and invalid verdicts.
- Citation IDs must belong to the authenticated contract's **current frozen evidence manifest**; reject foreign, nonexistent or duplicate IDs. SUPPORTED and GAP require grounded source citations; otherwise downgrade or error.
- Reject malformed or extra fields, blank reason/limitations, oversized text and impossible claims of executed tests; keep caps for 2–5 criteria, max five evidence items, and one sanitized image.
- Recheck current contract/evidence hashes **after** the model call; stale results must not update the current review or change capture availability.
- Backend, not AI, supplies `contractVersionHash`, `evidenceManifestHash`, model identity and request IDs in the persisted report.
- On refusal, provider outage, timeout, quota failure, invalid schema, prompt injection or ungrounded evidence: show ERROR/UNVERIFIABLE and preserve payment restrictions. Do not fabricate a successful assessment.
- Model cannot call functions, Google Search/grounding, URL context, remote fetch, code execution, computer use or payment APIs. No secret values in prompts or model-visible metadata.
- Limit prompt contents to permitted evidence and criteria; do not fetch user-submitted URLs, run attachments or trust injected "instructions" embedded in screenshots/text.
- Store sanitized audit metadata (request ID, provider, exact model, prompt/schema versions, hashes, timestamps, token usage if provided, result category), not secrets/raw user content/reasoning traces by default.
- Suggestion outputs are editable **drafts** only. Explicit buyer acceptance is mandatory before freezing the contract.

`SUPPORTED` means *the submitted evidence supports the claim*, not that an implementation passed live testing. Buyer approval and PayPal capture are separately guarded; no AI score directly triggers payment.

## Additional AI-specific test scenarios

These supplement **without replacing or renumbering** the existing 32 MP acceptance tests.

| ID | Test | Expected |
|---|---|---|
| AI-01 | Real `gemini-3.8-flash` provider call | Redacted proof of real request, exact model ID |
| AI-02 | Criteria suggestions | 2–5; buyer explicitly confirms before freeze |
| AI-03 | Good text evidence | Grounded citation and qualified SUPPORTED |
| AI-04 | Screenshot claiming code execution | No fabricated execution proof |
| AI-05 | Forged evidence ID | No accepted citation; report rejected/downgraded |
| AI-06 | Duplicate/missing/extra criterion | Invalid report, no payment mutation |
| AI-07 | Malformed JSON, extra fields or bad enum | Fail closed, no positive report |
| AI-08 | Evidence says `capture_now`/ignore rules | Inert evidence; zero PayPal calls |
| AI-09 | Stale manifest and cross-user evidence | Reject and preserve permission gate |
| AI-10 | API error / 429 / timeout / refusal | Review unavailable, never auto-capture |
| AI-11 | Tool/URL fetch / secret exfiltration attack | No tools and no secrets exposed |
| AI-12 | Parallel assessment/duplicate requests | Bound quota; persisted snapshot consistent |

Map AI-05 through AI-11 to MP-011, MP-012, MP-013, MP-022 and MP-023 where applicable. For future feature implementation, add objective-based unit tests, a real model invocation and independent exact-HEAD audit evidence. Synthetic mock responses cannot substitute for the actual provider test.

## Implementation scope

MP-AI-01 is **docs only**. No frontend/backend scaffold, SDK install, live calls, paid API setup, schema migration, credential provisioning, CI exception, merge or deployment is authorized by this task. Separate implementation approval is required.
