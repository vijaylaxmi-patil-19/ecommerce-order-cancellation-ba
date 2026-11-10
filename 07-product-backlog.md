# 07 · Product backlog

**Epic:** Stock-safe marketplace checkout. Use these issues as a Jira-style backlog. Status for every issue is Proposed.

| Story | Priority | User story | Acceptance criteria | Dependency |
|---|---|---|---|---|
| US-01 | Must | As a shopper, I want checkout to secure my item before I pay. | Given one unit and two concurrent requests, when both reserve it, then exactly one active hold exists. An unavailable response explains that stock has changed. | Versioned inventory |
| US-02 | Must | As a shopper, I want one order even if my payment callback repeats. | Given an active hold and verified capture, when callbacks replay, then one order and one allocation exist. A valid COD attempt also places one order. | US-01 |
| US-03 | Must | As operations, I want abandoned holds and late payments resolved. | Given an expired hold, when capture arrives, then stock stays released, no order is created and one exception is recorded. | US-01, US-02 |
| US-04 | Must | As operations, I want consistent cancellation reasons. | Given an attempted cancellation with a missing reason, when submitted, then validation fails. A valid submission records actor, stage and audit time. | Order states |
| US-05 | Must | As a shopper, I want refund status after cancellation. | Given a captured payment and accepted cancellation, when the cancellation repeats, then one refund handoff exists and status is visible. Suspect stock stays unavailable pending review. | US-04 |
| US-06 | Should | As operations, I want to monitor exceptions by age. | Given expired holds and refund exceptions, when opening the queue, then the correct references, states and age appear. | US-03, US-05 |
| US-07 | Could | As a seller, I want low-stock reminders. | Given available stock crosses the agreed threshold, when the job runs, then one reminder is sent per threshold crossing. | Reliable inventory |
