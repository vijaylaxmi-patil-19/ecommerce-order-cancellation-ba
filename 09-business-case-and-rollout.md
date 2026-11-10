# 09 · Business case, rollout and decision log

| Option | Benefit | Feasibility and trade-off | Decision |
|---|---|---|---|
| Low-stock reminders | Encourage timely replenishment | Easier to implement, depends on seller response | Later enhancement |
| Checkout reservation and reconciliation | Direct control over last-unit contention and checkout failure recovery | Requires authoritative stock writes, payment reconciliation and integration testing | Proposed MVP |
| Physical reconciliation and tighter seller sync | Addresses inventory accuracy outside checkout | Requires seller participation and stock-update observability | Pilot operational companion |

## Illustrative economics

At 10,000 monthly orders, a reduction from 6% to 4% implies 200 fewer cancellations per month. Assume ₹50 in incremental contribution and ₹30 in avoidable support cost per prevented cancellation, producing ₹16,000 monthly benefit. Assume ₹80,000 one-time build cost and ₹5,000 monthly operating cost.

- First-year benefit = ₹192,000. First-year cost = ₹140,000.
- First-year ROI = (₹192,000 − ₹140,000) / ₹140,000 = **37.1%**.
- Simple payback = ₹80,000 / (₹16,000 − ₹5,000) = **7.3 months**.
- At 100 prevented cancellations monthly, first-year ROI falls to **−31.4%**.

Validate contribution, operational savings and achievable reduction before funding. Gross merchandise value is tracked separately from realized contribution.

## Rollout and change management

1. Agree measurement rules and instrument a comparable baseline with mature cohorts.
2. Verify inventory and payment reconciliation in staging. Brief sellers and train support on customer messages and exception triage.
3. Enable a feature flag for a small seller cohort. Compare to its baseline and a comparable non-pilot cohort, accounting for promo mix, volume and seasonality.
4. Review results after four mature weekly cohorts. Proposed expansion gates are stock cancellations ≤4.0%, checkout conversion decline no more than 1 percentage point, and no critical unresolved ledger or refund defects.
5. If rollback is needed, stop new reservations via flag and keep existing holds, orders and refund queues under reconciliation until cleared. Ops owns communications and engineering owns recovery.

| Risk or decision | Owner | Action / status |
|---|---|---|
| Stale physical stock undermines hold accuracy | Ops | Audit pilot sellers and investigate discrepancies |
| Callback arrives after hold expiry | Payments | Reconcile late capture and deduplicate refunds |
| Checkout latency lowers conversion | Engineering | Load-test and monitor per cohort |
| 10-minute TTL conflicts with slow payment | Product and payments | Validate against completion-time distribution before launch |
| Seller-specific stock integration feasibility | Engineering | Confirm authoritative write path during discovery |
