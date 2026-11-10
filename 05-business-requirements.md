# 05 · Business requirements document

**Owner:** Product manager. **Status:** Proposed. **Approvers:** Product and operations, with engineering feasibility review.

| ID | Business requirement | Success evidence |
|---|---|---|
| BR-01 | Prevent orders from being placed against unavailable inventory | UAT proves only one checkout can claim the final unit |
| BR-02 | Recover inventory and reconcile money when checkout or fulfilment fails | Failed, expired and cancelled flows clear holds or record an exception without duplicate refunds |
| BR-03 | Make cancellations measurable and actionable | Reason, actor, stage and timestamps support a reconciled KPI breakdown |
| BR-04 | Keep customers and operations informed about cancellations and refunds | Customer message and ops work item show the current status |

## Business success and sign-off

Pilot goal is ≤4.0% stock-related order cancellations against a comparable baseline. Monitor checkout conversion, false stock blocks, time to refund initiation and paid attempts without orders. Product approves KPI and rollout decisions. Operations approves business workflows. Engineering confirms consistency, observability and rollback controls.
