# 04 · Root-cause analysis

## Cancellation taxonomy

Use one primary reason per cancelled order. Keep actor, detection stage and secondary contributing factors as separate fields.

| Reason | Meaning | Evidence example |
|---|---|---|
| Stock unavailable | Seller cannot supply the ordered SKU | Inventory history, hold history, physical count |
| Customer request | Customer initiated cancellation | Customer event or support record |
| Payment exception | A placed order was later invalidated by payment reconciliation | Gateway transaction and order audit |
| Delivery exception | Order cancelled because serviceability or dispatch failed | Carrier event and postcode check |
| Seller processing | Seller missed confirmation or processing deadline for a reason unrelated to stock | Seller timestamps and SLA record |
| Platform error | An order workflow or integration failure caused cancellation | Incident and correlated event logs |
| Unknown | Evidence is insufficient | Queue for operations review |

Pre-placement payment declines and checkout stock blocks belong to checkout telemetry, outside the order cancellation denominator. Returns after delivery belong to returns reporting.

## Fishbone categories

| Branch | Possible contributor | How to validate |
|---|---|---|
| People | Seller forgets to enter offline sales | Interview and compare offline sales with stock updates |
| Process | Seller checks inventory only after order placement | Walk through confirmation timestamps |
| Systems | Concurrent attempts can claim the same unit | Replay two concurrent checkouts |
| Data | SKU mappings or counts are incorrect | Compare physical count with seller SKU ledger |
| Policy | Confirmation SLA expires without escalation | Compare SLA and alert history |
| External partners | Gateway or courier event is delayed | Compare provider and internal timestamps |

## 5 Whys · Concurrent oversell hypothesis

1. Why did the order cancel? The seller could fulfil only one of two orders.
2. Why were two orders accepted? Both checkouts saw one available unit.
3. Why did both see the same unit? The availability reads occurred before either order allocated it.
4. Why could placement proceed after a shared read? Stock checking and allocation were separate operations.
5. Why was the gap possible? The checkout design lacked an atomic reservation guarantee.

Validate with order timestamps, stock ledger versions and a concurrency reproduction. If checkout holds exist and the ledger matches, investigate delayed updates and physical stock mismatch next.
