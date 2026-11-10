# 06 · Functional and system specification

| ID | System behavior |
|---|---|
| FR-01 | Reserve the requested quantity for the seller SKU at checkout using an atomic availability check and update. Return an unavailable outcome for insufficient stock and a retry outcome for service failure. Do not place an order on either outcome. |
| FR-02 | Give a hold a configurable TTL, initially 10 minutes. On valid checkout completion, atomically transition the active hold to allocation and create one order. For prepaid orders require verified payment success. For COD require confirmed checkout. |
| FR-03 | Release active holds on verified failure, abandonment expiry or explicit cancellation. Reject checkout completion after expiry. If prepaid capture arrives late, create a payment reconciliation task without creating an order. |
| FR-04 | Require primary reason, actor and detection stage for a placed-order cancellation. Keep timestamps and preserve reason corrections in audit history. |
| FR-05 | Cancel and deallocate before shipment. Return quantity to sellable stock only after inventory is confirmed sellable. For stock discrepancy, place it in a non-sellable bucket pending review. For captured payments, enqueue one refund request per eligible payment, and notify the customer of cancellation and refund status. |
| FR-06 | Provide an operations view of cancellations, stale holds, and payment/refund exceptions with order or attempt reference and age. Publish KPI extracts by order placement date. |

## State and data rules

- Hold states are ACTIVE, ALLOCATED, RELEASED and EXPIRED. Completion and expiry race through one conditional state transition. An expired or released hold cannot be allocated.
- Available to sell = max(0, recorded on-hand − active holds − unshipped allocations − non-sellable units). Shipment reduces on-hand and clears its allocation together.
- Seller updates use a version check. Flag a new stock count below existing commitments and block additional reservations until corrected. Preserve existing commitments for operations to reconcile.
- Checkout attempt ID is the retry key. Repeating the same request returns the existing result. A changed payload with the same ID returns a conflict. Refund operations use payment reference and cancellation ID as the retry key.
- Persist refund handoff with the cancellation transition, retry delivery, and reconcile provider state before reissuing ambiguous requests. Refund statuses are pending, submitted, completed, failed and review required.
- Keep payment tokens and customer PII out of analytics events. Include event time, actor role, reason, stage, seller SKU, attempt ID and order ID when available.

| ID | Non-functional requirement and verification |
|---|---|
| NFR-01 | Proposed reserve endpoint p95 ≤500 ms at 50 requests/sec for 15 minutes in staging. Measure latency and errors separately. |
| NFR-02 | No negative available stock or duplicate orders/refunds under concurrent requests and event replay. Verify ledger and provider sandbox. |
| NFR-03 | Restrict seller visibility to owned orders and restrict reason corrections to operations. Verify permissions and audit changes. |
