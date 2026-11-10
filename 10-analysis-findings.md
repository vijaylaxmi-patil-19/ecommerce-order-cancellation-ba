# 10 · Demo analysis and findings

![Synthetic cancellation analysis](../assets/demo-analysis.png)

| Metric | Calculation | Demo result |
|---|---|---:|
| Orders placed | Count unique placed orders | 1,000 |
| Total cancellation rate | 120 cancelled / 1,000 placed | 12.0% |
| Stock cancellation rate | 60 stock cancelled / 1,000 placed | 6.0% |
| Stock share of cancellations | 60 stock cancelled / 120 cancelled | 50.0% |

The 120 cancellations include 60 stock, 20 customer, 15 payment, 10 delivery, 8 seller processing, 5 platform and 2 unknown. Among stock cancellations, the simulated labels are 30 stale stock, 20 concurrent oversell and 10 physical mismatch. A reservation addresses concurrent oversell directly. Stale counts and physical mismatches also require reliable seller updates and reconciliation. The 20 oversell cases make the 4% target a useful hypothesis to test if the same 1,000-order denominator and other reasons held constant.

## How to investigate with real data

Join order headers to cancellation events, inventory history and payment events using order and attempt IDs. Reduce cancellation events to the latest audited primary reason per order before aggregation. Use placement date to define cohort membership. Apply the same follow-up window to each cohort and separately report still-open orders and events outside the window. Compare rates by seller, category, fulfilment location and checkout flow, with counts alongside rates and a minimum volume rule for seller ranking. Compare event sequences for both cancelled and completed orders to validate causal hypotheses.

Track checkout blocks, checkout conversion, late payments, time to refund initiation and stock reconciliation age as separate metrics. A drop in stock cancellations alongside a large conversion decline could indicate that checkout is blocking valid orders.
