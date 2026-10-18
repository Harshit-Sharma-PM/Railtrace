# RailTrace — Payment Exception Triage Prototype

**Product concept · Payments operations · Workflow design**

RailTrace is an independently built, browser-based prototype exploring how finance and payment-operations analysts could investigate payment exceptions in one place. It is a portfolio concept for testing a product hypothesis—not a production payment service.

**[View my Product Management portfolio](https://harshit-sharma-product-portfolio.pages.dev)**

## The problem hypothesis

Payment operations teams may need to compare order, payment, refund and settlement records across systems to understand discrepancies. This can create repetitive investigation work and make it harder to see what evidence is missing or what action should happen next.

RailTrace explores a focused workflow: surface an exception, review its evidence, understand a transparent rule-based recommendation, assign ownership, and track resolution.

This problem statement is a hypothesis for discovery and validation, not a claim that the prototype has demonstrated measurable operational savings.

## Product case study

Read the detailed [RailTrace merchant payment exception triage case study](CASE_STUDY.md) for the problem hypothesis, target users, proposed workflow, product decisions, success metrics, discovery plan and open validation risks. The [reproducible validation protocol](VALIDATION_PROTOCOL.md) and [seven synthetic test scenarios](validation/railtrace-scenarios.csv) document expected safe behavior; results are marked not run until actually executed.

## Product scope

- Exception queue with search and filters
- Synthetic cases for settlement mismatches, missing payment confirmations, pending refunds, duplicate payments and fee variance
- Evidence review and transparent rule-based recommendations
- Case assignment, status updates and activity history
- CSV import/export and manual case creation
- Overview metrics and exception mix
- Browser local storage for demo persistence

## Try the prototype

Open `index.html` directly in a browser. No Node.js, package installation, paid API, server or database is required.

The app is static HTML, CSS and JavaScript. To deploy it on Cloudflare Pages, create a separate repository and use:
- Framework preset: **None**
- Build command: **leave blank**
- Build output directory: `/` (root)

## Product decisions and trade-offs

- **Transparent recommendations over opaque AI:** the prototype uses explicit rules so a reviewer can understand why a next action is suggested.
- **Synthetic data over live payment integrations:** this keeps the demo safe and independently runnable.
- **Case tracking over money movement:** the product helps organize investigation; it does not initiate refunds or move funds.
- **CSV as an entry point:** file import/export allows a basic workflow without requiring integrations before the core problem is validated.

## Limits and safety

- No live bank, UPI, NPCI, card-network or gateway integrations
- No payment credentials or real customer data
- No automatic refunds, money movement or regulatory determinations
- Deadlines are illustrative reminders only; confirm applicable provider terms and rules
- All seeded records are synthetic. Dashboard amounts represent sample case values, not verified financial losses or real customer outcomes

## CSV import format

```csv
order_id,transaction_id,merchant,amount,expected_amount,rail,exception_type
ORD-123,UPI-123,Example Store,1500,1450,UPI,Settlement mismatch
```

## Next validation steps

1. Interview payment-operations or finance analysts about the frequency and cost of exception investigation.
2. Map the current investigation workflow, systems involved, handoffs and evidence gaps.
3. Test whether the queue and evidence view help users identify the next action faster.
4. Measure task completion time, correct next-action selection and unresolved-case rate before making impact claims.

## Tech

Vanilla JavaScript, HTML, CSS, browser local storage. No runtime dependencies.

This prototype demonstrates a product hypothesis and workflow exploration; it does not establish production readiness or validated business impact.
