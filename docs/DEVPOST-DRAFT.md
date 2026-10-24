# MilestonePay AI — Devpost Submission Draft

**Draft only, prepared October 24, 2026. DO NOT submit the present-tense claims until the working build, real sandbox captures, AI calls, and final exact-HEAD audit actually exist. Replace `[VERIFY]` placeholders with facts observed in the completed app.**

## Project title
MilestonePay AI

## Tagline
Verify the work. Approve the payment. Trust the process.

## Elevator pitch (short)
MilestonePay AI connects evidence-backed AI review to PayPal's real Sandbox authorization and capture flow. A buyer defines measurable milestone criteria, a contributor submits proof of delivery, and AI highlights supported, missing, and unverifiable claims. The buyer—not the AI—decides whether to capture or void the payment. It is a single-merchant, sandbox-only prototype, not escrow or a freelancer payout system.

## What inspired us?
Digital-service payments and delivery reviews are often disconnected. The payment happens in one place, while promises, deliverables, and acceptance conversations live across documents and messages. We wanted to explore a better interface: one that shows *why* someone is comfortable approving a payment, rather than asking AI to move money on someone's behalf.

## What it does
A buyer creates one fixed-price service milestone and reviews AI-suggested acceptance criteria. Once the criteria are frozen, the buyer approves a PayPal Sandbox authorization through PayPal Checkout. A contributor then submits criterion-linked evidence. MilestonePay AI generates a structured verification report with citations and explicit uncertainty. The buyer reviews the report and can request changes, capture the authorized payment, or void the authorization. An audit timeline links each important decision to the associated PayPal status and transaction identifiers.

The AI is advisory. It cannot capture money, update a payment state, or turn questionable evidence into an automatic payout. The app does not hold funds and does not provide escrow, arbitration, or independent contractor payouts.

## How we built it
We used **[VERIFY: actual Next.js and TypeScript versions]** for the user interface and server routes, **[VERIFY: Supabase configuration]** for authenticated contracts and event history, and the official **PayPal JavaScript SDK, Orders v2 and Payments v2 REST APIs** for the sandbox authorize/capture/void lifecycle. Our backend verifies role, amount, merchant, evidence-version freshness, and payment state before making each irreversible request. Webhook verification, idempotency reservations, and reconciliation protect against forged payment updates and duplicate capture attempts.

For AI, we used **[VERIFY: actual provider + exact model and version]** for criteria suggestions and evidence classification. The model returns structured, criterion-specific results referencing permitted evidence IDs. We reject invalid citations and treat uploads as untrusted input. The model has no direct access to the payment execution functions.

Our main frameworks/tools are **[VERIFY: actual versions and deployed stack]**. Optional sponsor tools: **[LIST ONLY IF ACTUALLY USED; describe meaningful, tested AG Studio/AG Grid integration if present]**.

## Challenges we ran into
The largest design challenge was separating a persuasive AI assessment from authority to move money. PayPal authorization is a temporary hold, not escrow, so we chose a fixed single-merchant model with explicit buyer-controlled capture instead of suggesting a marketplace service we could not responsibly implement during a short hackathon. We also designed for asynchronous payment results: a timed-out capture request must be reconciled, not blindly retried.

**[UPDATE BEFORE SUBMISSION with actual bugs, integration failures, and how they were resolved. Do not describe hypothetical issues as solved.]**

## Accomplishments we're proud of
**[FILL FROM REAL EVIDENCE]** An end-to-end sandbox order/authorization/capture; a separately voided authorization; criterion-linked, uncertainty-aware real AI analysis; role-separated consent; and an understandable audit trail. We especially value keeping AI judgment from becoming an autonomous money-moving instruction.

## What we learned
PayPal's approval, authorization, and capture stages are distinct; a clear UI must reflect those differences. We also learned that evidence-first AI systems become more trustworthy when they can say *unverifiable* instead of inventing certainty. **[Add specific learnings after implementation.]**

## What's next?
A post-hackathon research roadmap could evaluate merchant onboarding for multiple real sellers, clearer dispute-evidence exports, additional accessibility testing, customer validation, and legal/compliance review. Marketplace payments and escrow are **not** present in this prototype and would require separate product, partner, operational, and legal decisions. No production-money launch is committed.

## PayPal technology used
- PayPal Checkout JavaScript SDK with `intent=authorize`.
- Orders v2 REST API: create an `AUTHORIZE` order; authorize a buyer-approved order.
- Payments v2 REST API: full authorized-payment capture and void, with status retrieval.
- OAuth 2 client-credentials grant for server authentication; verified webhooks and idempotent requests.

**[Mark each as USED only after observing a real successful sandbox call; remove unused endpoints.]**

## AI tools used and what they do
**[VERIFY provider/model]** receives the buyer-approved criteria and a bounded synthetic evidence packet, suggests improvements to measurable acceptance wording, and returns a typed verdict per criterion (`SUPPORTED`, `GAP`, or `UNVERIFIABLE`) with cited evidence IDs. AI does not browse arbitrary websites, verify code by running it, decide disputes, change prices, or issue payments. **[Disclose any code-generation assistants if required by the form, and distinguish build-time tools from runtime AI.]**

## What makes it different?
MilestonePay AI does not start with “can an AI agent pay?” It asks “what evidence should a buyer see *before* approving a payment?” That shifts the center of the experience from autonomous settlement to explicit consent, evidence provenance, and uncertainty-aware assistance.

## Safety, limits, and honesty
This is a sandbox-only research prototype. It uses a single fixed merchant/payee and synthetic buyer/contributor personas. PayPal authorization is not escrow and does not guarantee eventual capture. The contributor is not automatically paid by the app. A human buyer makes every capture or void decision. The report is advisory and should not be represented as legal, financial, or professional certification.

## Repository / demo / video links
- GitHub: `[PENDING — do not invent URL]`
- Demo: `[PENDING — tested URL or runnable README]`
- YouTube: `[PENDING — public URL, duration under 3:00]`
- Audit report: `[PENDING — exact SHA and independent audit result]`

## Suggested demo video narration (target 2:45)

“Paying for digital work is easy. Knowing whether the work meets the agreement is harder. MilestonePay AI connects an evidence-based review to a real PayPal Sandbox payment. Here, a buyer creates a twenty-dollar website milestone and confirms three measurable acceptance checks. Next, the buyer approves a PayPal authorization—notice that it is authorized, not captured. A contributor supplies evidence for each criterion. Our AI evaluates that evidence, cites what supports each result, and flags anything it cannot verify. The model can recommend, but it can never move money. Now the buyer sees the exact amount, reviews the limitations, and explicitly chooses to capture. The backend verifies the payment and records the actual PayPal Sandbox transaction ID. Or the buyer can void an uncaptured authorization. Every decision remains traceable: what evidence was submitted, what AI concluded, what the buyer authorized, and what PayPal confirmed. No escrow, no fictional payouts, and no hidden agent controlling the funds. MilestonePay AI: verify the work, approve the payment, trust the process.”

## Submission quality check

- Confirm every past-tense accomplishment was actually demonstrated at the exact published Git SHA.
- Keep video below three minutes; show working browser app and genuine sandbox IDs.
- Publish public repo under valid open-source license; ensure README is runnable by judges.
- Explain AI runtime versus coding assistants accurately, verify sponsor eligibility claims.
- Provide free demo access or complete local setup and sandbox-account instructions through judging.
- Inspect video/images for unauthorized third-party copyright and trademarks.
- Submit before Nov 12, 2026, noon PST.

Official event: https://paypalaihackathon.devpost.com/