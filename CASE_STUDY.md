# RailTrace — Merchant Payment Exception Triage

> **Case-study status:** Prototype and product hypothesis. The problem and business impact still require validation with merchant finance/payment-operations users. All demo records are synthetic; no production payment integrations or measured customer outcomes are claimed.

## Executive summary

RailTrace explores a focused workflow for Indian omnichannel merchants to investigate payment exceptions across orders, payment confirmations, refunds and settlement records. The hypothesis is that finance and payment-operations analysts lose time switching between provider dashboards, order-management systems, spreadsheets and support records to determine what happened and who should act next.

The product is not a payment gateway, reconciliation ledger or money-movement system. It is an investigation and case-management layer for exceptions that need human review.

## 1. Problem framing

### Problem hypothesis

When an order, payment, refund or settlement record does not line up, a merchant analyst may need to gather evidence from several systems, identify the discrepancy, decide the next step, assign ownership and follow up until the case is resolved. Evidence and context can be fragmented across tools, while handoffs and follow-ups may be tracked manually.

This is a hypothesis to validate—not a claim that all merchants experience the same problem or that current tools cannot solve it.

### Why focus on exceptions?

The normal payment path is designed to complete transactions. Exceptions create a different operational task: explain a mismatch, establish what is known, identify what is missing, and decide whether to wait, investigate, contact a provider, or reconcile an amount. The product opportunity is to improve the investigation workflow rather than replace payment infrastructure.

### Target users

- **Primary:** Finance and payment-operations analysts at growing Indian omnichannel merchants.
- **Secondary:** Refund-operations analysts and operations managers responsible for case queues, ageing and escalation.
- **Potential buyers:** Finance or operations leaders, subject to discovery and willingness-to-pay validation.

## 2. Public evidence and validation (desk research)

This section adds externally observable signals to the problem framing. It is **secondary research**, not merchant interviews, a representative survey, or proof that RailTrace itself is needed. Sources establish the scale and operational mechanics of payment flows; they do not quantify merchant time lost to exception investigation.

### Signal A — Merchant payment flows operate at very large scale

NPCI's UPI ecosystem statistics report that in August 2025, UPI processed approximately **20.0 billion transactions** overall, including approximately **12.7 billion person-to-merchant (P2M) transactions**. The scale means even a small share of transactions requiring follow-up could create a meaningful absolute workload—but this is a sizing hypothesis, not a measured exception rate.

Source: [NPCI — UPI Ecosystem Statistics](https://www.npci.org.in/what-we-do/upi/upi-ecosystem-statistics) (August 2025 table).

### Signal B — Payment status outcomes vary across participants

NPCI's August 2025 remitter-member table reports different approved and technical/business-decline rates across banks. For example, the published table shows SBI remitter approved at 93.66% and HDFC Bank at 95.37%; the same page also distinguishes technical declines, business declines and debit reversals. These are ecosystem-level measures, not merchant checkout conversion rates and not all declines are operational exceptions. They nevertheless show why status, participant and reversal context matter when diagnosing a payment outcome.

Source: [NPCI — UPI Ecosystem Statistics](https://www.npci.org.in/what-we-do/upi/upi-ecosystem-statistics) (remitter-member performance, August 2025).

### Signal C — Reconciliation requires linking transaction and settlement records

Razorpay's documentation describes settlement reports that map transactions to settlement IDs and documents APIs that expose settlement IDs, transaction/payment sources, statuses, fees and amounts. Its published product material also describes a single-view reconciliation workflow across payment gateways, including settlement information such as UTR, settlement ID and aggregator. This validates that transaction-to-settlement matching and consolidated visibility are recognized product workflows in the market. It does **not** prove that every merchant lacks these capabilities or that a new standalone product would outperform existing tools.

Sources:
- [Razorpay — Settlement reports and reconciliation](https://razorpay.com/blog/how-to-use-razorpay-dashboard/)
- [Razorpay — Single-view reconciliation across payment gateways](https://razorpay.com/blog/single-view-recon/)
- [Razorpay Docs — Fetch transfers for a settlement](https://razorpay.com/docs/api/payments/route/fetch-transfers-for-a-settlement/?preferred-country=IN)

### What this evidence does—and does not—validate

| Claim | Evidence status | Interpretation |
|---|---|---|
| India has a very large merchant-payment flow | Supported by NPCI aggregate transaction data | Establishes scale, not the size of the exception-management market |
| Payment outcomes and reversals require status context | Supported by NPCI participant-level statistics | Supports evidence-aware triage, but does not establish the cause of any individual transaction |
| Transaction-to-settlement mapping and consolidated reconciliation are real workflows | Supported by payment-provider documentation and product materials | Confirms adjacent capabilities already exist; competitive differentiation must be demonstrated |
| Merchants routinely switch between tools and lose significant time | **Not validated by the sources reviewed** | Keep as a hypothesis until credible merchant research or a reliable study quantifies it |
| RailTrace reduces investigation time, losses or unresolved cases | **Not measured** | Do not claim business impact until a controlled usability test or pilot measures it |

### Revised problem statement

For merchants processing payments across one or more providers, payment and settlement evidence can be spread across transaction views, settlement reports and internal order/accounting records. When records do not match or statuses are unclear, the analyst needs to reconcile identifiers and amounts, determine what is known versus missing, and track a next action. Provider documentation confirms these records and reconciliation workflows exist; public sources reviewed here do not establish how painful this is for a particular merchant segment. RailTrace therefore targets a **testable workflow hypothesis**, not a proven market gap.

### Competitive implication

Razorpay and other payment providers already offer settlement details and reconciliation features. RailTrace should **not** position itself as a replacement for those dashboards or claim that the market lacks reconciliation. A more defensible potential wedge to test is an **exception-first, cross-provider investigation queue** that combines evidence from multiple systems, explains mismatches, records ownership and makes follow-up auditable. Whether that wedge is differentiated enough—and whether target merchants would adopt or pay for it—remains unvalidated.

## 3. Initial use cases

1. **Settlement mismatch:** order/payment evidence exists, but the expected and reported settlement amounts differ.
2. **Payment confirmation missing:** an order appears paid or pending while confirmation evidence is incomplete or delayed.
3. **Refund pending:** a refund has been initiated but its status or settlement evidence needs follow-up.
4. **Duplicate payment:** records suggest more than one payment for an order and require verification before action.
5. **Fee variance:** reported settlement net amount differs from the expected amount after fees or adjustments.

These categories are illustrative. Real terminology, frequency and handling differ by gateway, payment method, merchant stack and provider contract.

## 4. Product goal and non-goals

### Goal

Help an analyst reach a defensible next action for a payment exception, with the supporting evidence, owner and follow-up recorded in one case view.

### Non-goals

- Processing payments or initiating refunds
- Replacing a payment gateway, PSP dashboard, bank statement or accounting ledger
- Making final financial or regulatory determinations
- Claiming live access to UPI, NPCI, card networks, banks or payment providers
- Automatically resolving exceptions without verification

## 5. Proposed workflow

1. **Surface:** show a searchable queue with status, exception type, priority, merchant/order reference and age.
2. **Inspect:** bring available order, transaction, refund and settlement fields into one evidence view.
3. **Explain:** show which values match, conflict or are missing, and why the case was flagged.
4. **Recommend:** offer a rule-based next step with the reason and the evidence required before action.
5. **Assign:** record the responsible person/team, status and follow-up deadline.
6. **Resolve:** capture the resolution reason and activity history so the next analyst can understand what happened.

The current prototype explores the queue, synthetic cases, evidence review, transparent rule-based recommendations, ownership/status, activity history, CSV import/export and browser-local persistence. These are prototype capabilities, not evidence of production readiness.

## 6. Decision principles

- **Evidence before recommendation:** distinguish observed fields from assumptions and missing information.
- **Explain uncertainty:** use a needs-review state when evidence is incomplete or contradictory; do not present a guess as a confirmed root cause.
- **Human confirmation for financial actions:** recommendations organize investigation; they do not move money.
- **Auditable handoffs:** retain status changes, notes, owner and resolution rationale.
- **Safe data handling:** use synthetic data in the portfolio demo and avoid storing real payment credentials or customer-sensitive records.

## 7. MVP boundaries and trade-offs

| Decision | Rationale | Trade-off / risk |
|---|---|---|
| Standalone browser prototype | Makes the workflow easy to review without paid services or setup | No multi-user collaboration or server-side audit trail |
| Synthetic cases | Safe for public demonstration | Cannot establish real exception distributions or impact |
| Transparent rules | Reviewers can inspect why a next action is suggested | Rules may be incomplete and need provider-specific validation |
| CSV import/export | Allows a basic workflow without integrations | Data mapping, duplicate detection and file quality need testing |
| Case tracking, not money movement | Keeps the scope narrow and safer | Analysts still need the source system to verify evidence and execute actions |

## 8. Success metrics to validate

Do not report improvements until a baseline and a test have been run with representative users.

- **Primary:** median time from opening an exception to selecting a correct, evidence-supported next action.
- **Quality guardrail:** percentage of next-action selections judged correct by a qualified reviewer.
- **Workflow metric:** percentage of cases with a named owner, next step and follow-up date.
- **Resolution metric:** median age of exceptions and percentage unresolved beyond the agreed service target.
- **Usability metric:** task completion rate and number of context switches needed during a scripted investigation.
- **Safety guardrail:** rate of recommendations that overstate certainty or suggest an action without required evidence.

### Suggested usability test

Ask 5–8 payment/finance operators (a discovery sample, not a statistically representative study) to work through matched scripted scenarios using their current process and the prototype. Capture baseline and prototype task times, correct next actions, missed evidence and user confidence. Record the sample size, scenario mix and limitations. Treat results as directional.

## 9. Discovery plan: what must be proven

Before expanding the build, interview payment-operations and finance analysts at growing omnichannel merchants. Ask them to walk through the last real exception they handled, with sensitive details removed.

Questions:
- Which exception types recur most often, and roughly how many cases arrive per day or week?
- Which systems or reports must be checked to investigate one case?
- What evidence is hardest to obtain, and where do handoffs or follow-ups break down?
- How are ownership, ageing, escalation and resolution reason tracked today?
- Which existing gateway, reconciliation or ERP tools already cover this workflow well?
- What is the operational cost of delay or rework, and how is it measured?
- Which data could be exported safely, and what security/compliance constraints apply?
- Would a cross-provider investigation layer fit the workflow, or would integration and process changes make it impractical?

**Disconfirming evidence to look for:** existing tools already provide a trusted consolidated queue; exception volume is too low; analysts have no access to required data; integration/security costs exceed the value; or the main bottleneck is provider resolution time rather than investigation.

## 10. Risks and mitigations

- **False diagnosis:** display evidence and rule rationale, label missing/contradictory fields, require human confirmation.
- **Provider-specific semantics:** validate statuses, settlement cycles and fee treatment with each provider before encoding rules.
- **Sensitive financial data:** keep public demos synthetic; define access, retention and audit requirements before any real-data pilot.
- **Duplicate or stale records:** validate imports and design idempotent identifiers before integrating data feeds.
- **Unclear ownership:** require an owner or explicit unassigned state and record handoffs.
- **Overstated impact:** publish only measured results with method, sample size and baseline.

## 11. Current prototype vs. next milestones

### Built in the prototype

- Exception queue, search and filters
- Synthetic cases for common exception categories
- Evidence/discrepancy review and rule-based next-action guidance
- Status, ownership, notes and activity history
- CSV import/export and manual case creation
- Overview metrics and browser-local persistence

### Next milestones

1. Complete and document a one-case CSV export/import round trip, including validation failures.
2. Improve the evidence explanation so each discrepancy identifies the observed values, missing evidence and reason for the suggested action.
3. Test the workflow with representative users and compare task time and next-action accuracy with their current process.
4. Refine the product scope based on discovery; only then consider read-only integrations and multi-user auditability.

## Portfolio positioning

RailTrace is an independent product experiment demonstrating problem framing, workflow design, transparent decision rules, MVP trade-offs and validation planning. It is not professional merchant payments experience, a live integration, or proof of quantified business impact.
