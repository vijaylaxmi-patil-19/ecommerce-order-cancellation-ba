# 08 · UAT and requirements traceability

**Execution status:** Planned. Use staging with seller stock fixtures, a payment sandbox and access to event logs. Record actual results, evidence, defect ID, tester, date and retest status at execution.

| Test | Trace | Setup and actions | Expected result |
|---|---|---|---|
| UAT-01 | BR-01 / FR-01 / US-01 / NFR-02 | Set stock to 1. Submit two simultaneous checkout attempts for 1. Retry the winning ID. | One active hold. Losing request unavailable. Retry returns the original hold. |
| UAT-02 | BR-01 / FR-02 / US-02 / NFR-02 | Create active hold, complete prepaid checkout, replay success twice. Repeat with a fresh COD attempt. | Each attempt creates one order and one allocation. |
| UAT-03 | BR-02 / FR-03 / US-03 | Create hold. Let TTL expire and send a delayed successful capture twice. | Stock released once, zero orders and one reconciliation task. |
| UAT-04 | BR-03 / FR-04 / US-04 / NFR-03 | Cancel with missing reason, then with a valid reason. Try correcting it as a seller, then as authorized Ops. | Missing reason rejected. Ops correction logged with old and new values. Seller correction rejected. |
| UAT-05 | BR-02, BR-04 / FR-05 / US-05 / NFR-02 | Cancel an unshipped prepaid order for missing stock. Retry cancellation and refund handoff. | One cancellation, one refund request, quarantined units, visible customer status. |
| UAT-06 | BR-02, BR-04 / FR-05 / US-05 | Cancel an unshipped COD order with confirmed sellable stock. | Allocation cleared, stock sellable, customer notified, zero refund requests. |
| UAT-07 | BR-03, BR-04 / FR-06 / US-06 / NFR-03 | Seed a stale hold and refund exception. Check queue as Ops and as an unrelated seller. Reconcile extract counts. | Ops sees correct age and state. Seller cannot see another seller's records. Extract matches cohort. |
| PERF-01 | BR-01 / FR-01 / NFR-01 | Run agreed staging load for 15 minutes. | p95 ≤500 ms with error rate captured. |

**Exit criteria.** All Must stories pass, no unresolved critical defects, refund and inventory evidence attached, operations and product sign off. US-07 is a future enhancement and has no MVP UAT gate.
