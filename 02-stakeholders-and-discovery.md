# 02 · Stakeholders and discovery

| Stakeholder | Interest / influence | Evidence to request | Engagement |
|---|---|---|---|
| Product manager | High / high | KPI priorities and pilot tolerances | Approve scope and launch gates |
| Marketplace operations | High / high | Seller escalations and exception logs | Weekly design review |
| Sellers | High / varies | Stock update cadence, off-platform sales, stock checks | Interview pilot sellers and observe fulfilment |
| Engineering | High / high | Inventory writes, locks, retries, payment events | Technical discovery and feasibility review |
| Support and payments | High / medium | Tickets, refund timestamps and failure cases | Review exception workflow |
| QA | High / medium | Test environment and failure fixtures | Review acceptance criteria and run UAT with owners |

| Activity | Accountable | Responsible | Consulted | Informed |
|---|---|---|---|---|
| Define problem and scope | Product | BA | Ops, sellers, support | QA |
| Define reservation behavior | Engineering | Engineering, BA | Product, payments, QA | Ops |
| Validate cancellation codes | Ops | BA, support | Sellers, payments | Product |
| Run business acceptance | Ops | QA, BA | Engineering, sellers | Product |
| Approve rollout | Product | Ops, engineering | QA, payments | Sellers, support |

## Discovery questions and outputs

- Sellers: How do you record store sales? When does marketplace stock update? Walk through a rejected order and show the stock history.
- Engineering: Which inventory write is authoritative? Can two checkouts claim the final unit? How are late payment callbacks reconciled?
- Support: Who chooses a cancellation reason? Which codes are ambiguous? When is refund status visible?
- Operations: Which sellers show repeated mismatches? How do you verify a stock correction?
- Product: What checkout conversion loss would trigger rollback? Who owns the go/no-go decision?

Capture date, role, evidence link, finding, confidence, decision owner and follow-up in discovery notes. Sample cancellations and successful orders before confirming a root cause. Proposed decisions and open questions belong in the rollout log.
