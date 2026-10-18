# RailTrace — Reproducible Scenario Validation

> **Purpose:** a manual, repeatable product-quality check for the public prototype. This is a designed test set using synthetic records, not customer research, production validation, or proof of business impact.

## Files

- `validation/railtrace-scenarios.csv` — seven synthetic cases for import into the browser prototype.
- This protocol — expected evidence interpretation and safe next action for each scenario.

## Run the test

1. Open the RailTrace prototype in a browser.
2. Select **Reset demo data** if you want a clean baseline. This resets only this browser's local demo data.
3. Select **Import CSV**, choose `validation/railtrace-scenarios.csv` or paste its contents, then click **Import rows**.
4. Search each imported case by its order ID (`ORD-TEST-001` through `ORD-TEST-007`).
5. Compare the evidence rows, investigation summary and next action with the expected results below.
6. Record pass/fail, observed behavior, browser and date in the results table. Do not mark a scenario passed without running it.

## Scenario acceptance criteria

| Scenario | Expected interpretation | Safe next action | Failure condition |
|---|---|---|---|
| RTX-2001 — fee may explain difference | Expected ₹24,999.00 minus settlement ₹24,514.02 = ₹484.98; the supplied fee matches arithmetically, but validity is not proven | Verify against the provider fee schedule/report before resolving | Treats the matching fee as verified or auto-resolves |
| RTX-2002 — unexplained settlement gap | Expected ₹7,800.00 versus settlement ₹7,300.00; ₹500.00 remains unexplained and no fee evidence exists | Inspect itemised settlement/adjustment data; escalate only if still unexplained | Invents a fee/root cause or says the case is resolved |
| RTX-2003 — missing payment confirmation | Order exists but payment record is absent; payment outcome is unknown | Check authoritative provider status and export coverage | Labels payment definitively successful/failed from missing evidence |
| RTX-2004 — possible duplicate | Two successful-looking rows share an order reference; distinct provider transactions are not established | Compare unique transaction IDs/timestamps and reversal/refund evidence | Calls it a confirmed double charge without verification |
| RTX-2005 — refund completion absent | Refund request exists; completion record is absent from this sample | Check provider status and applicable provider timeline | Claims the provider missed an SLA without a timestamp/contract |
| RTX-2006 — settlement record absent | Current extract lacks settlement record; date-range issue is possible | Check settlement cycle and import the correct report period | Treats missing row as proof of failed settlement |
| RTX-2007 — conflicting statuses | Order/payment show success but a separate note says pending; timestamps/authority are unknown | Manual review against authoritative status and source timestamps | Selects one status as true or recommends resolution without reconciliation |

## Results log (fill only after execution)

| Scenario | Pass/Fail/Blocked | Observed result | Date / browser |
|---|---|---|---|
| RTX-2001 | Not run | — | — |
| RTX-2002 | Not run | — | — |
| RTX-2003 | Not run | — | — |
| RTX-2004 | Not run | — | — |
| RTX-2005 | Not run | — | — |
| RTX-2006 | Not run | — | — |
| RTX-2007 | Not run | — | — |

## Known limitations to keep visible

- The prototype uses deterministic rules and imported text; it does not call live payment providers or independently establish the truth of a status.
- A matching amount is not proof that a fee is contractually valid.
- Missing records can reflect delayed data, export-window problems, identifier mismatches or a real exception.
- Scenario coverage is intentionally small and synthetic. It does not represent real-world exception frequency or prove users need a separate product.
- Do not calculate savings or report recommendation accuracy until the scenarios are executed and reviewed; any user test requires a qualified reviewer and representative workflow.

## Suggested next validation with people

After the scripted checks, ask payment-operations/finance analysts to work through comparable cases using their current workflow and RailTrace. Measure task time, correct next action, missing-evidence detection and unsafe assumptions. Treat a small sample as directional and document the sample size and limitations.
