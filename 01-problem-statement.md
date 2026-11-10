# 01 · Problem statement and scope

## Problem statement

Customers place marketplace orders based on displayed availability. The seller may later discover that the item has already sold, the available quantity is stale, or the shelf count differs from the system count. The platform cancels the order, customer support handles the complaint, and prepaid orders may require a refund. Operations lacks a consistent way to identify where and why the order failed.

## Objective

Reduce the share of placed orders cancelled for stock-related reasons. For the demo, 60 of 1,000 orders cancel for stock reasons. Use 4.0% as an illustrative pilot target and establish a comparable production baseline before launch.

| In scope | Out of scope |
|---|---|
| Single-item, single-seller orders, one fulfilment location per seller SKU | Multi-seller carts, substitutions and partial cancellation |
| Checkout reservation, inventory updates, seller confirmation, cancellation reason and refund handoff | Warehouse redesign, payment provider replacement and automated replenishment |
| Analysis of all demo cancellation categories | Implementation of fixes for every category |

**Constraints and assumptions.** Seller stock and payment events can arrive late or be duplicated. Available-to-sell inventory can be protected within the platform, while physical inventory accuracy still depends on sellers. All data and stakeholder roles are illustrative.
