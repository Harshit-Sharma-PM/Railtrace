# RailTrace MVP

A zero-dependency, browser-based prototype for payment-exception triage. This is a portfolio product, not a production payment service.

## Run it

Open `index.html` in a browser. No Node.js, package installation, paid API, server, or database is required.

## Deploy free using Cloudflare Pages

Create a **separate repository** for RailTrace and upload these files. In Cloudflare Pages, connect that repository and set:
- Framework preset: **None**
- Build command: **leave blank**
- Build output directory: `/` (root)

The app is static HTML, CSS and JavaScript. This avoids paid build services and keeps hosting requirements simple. Do not put it inside the existing product portfolio repository unless you explicitly decide to do so.

## Features

- Exception queue with search and filters
- Synthetic cases for settlement mismatches, missing payment confirmations, pending refunds, duplicate payments and fee variance
- Evidence review and transparent rule-based recommendations
- Case assignment, status updates and activity history
- CSV import and export; manual case creation
- Overview metrics and exception mix
- Browser local storage for demo persistence

## Limits and safety

- No live bank, UPI, NPCI, card-network or gateway integrations
- No payment credentials or real customer data
- No automatic refunds, money movement or regulatory determinations
- Deadlines are illustrative reminders only; confirm the applicable provider terms and rules
- All seeded records are synthetic. Dashboard amounts represent sample case values, not verified financial losses or real customer outcomes

## CSV import format

```csv
order_id,transaction_id,merchant,amount,expected_amount,rail,exception_type
ORD-123,UPI-123,Example Store,1500,1450,UPI,Settlement mismatch
```

## Product hypothesis

**Target user:** Finance or payment-operations analyst at a growing Indian online or omnichannel merchant.

**Problem hypothesis:** Investigating discrepancies across order, payment, refund and settlement records can require repetitive manual effort.

**Value proposition to test:** Help analysts understand why an exception exists, see missing evidence, choose a next action and track the case through resolution.
