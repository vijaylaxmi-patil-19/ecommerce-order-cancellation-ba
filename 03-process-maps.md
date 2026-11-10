# 03 · Current and proposed process

## AS-IS hypothesis

```mermaid
flowchart TD
 A["Customer checks out"] --> B["Platform places order"]
 B --> C{"Seller can fulfil?"}
 C -->|Yes| D["Seller ships order"]
 C -->|No| E["Ops records cancellation reason"]
 E --> F{"Payment captured?"}
 F -->|Yes| G["Payments processes refund"]
 F -->|No| H["Support communicates status"]
 G --> H
```

## TO-BE proposal

```mermaid
flowchart TD
 A["Customer submits checkout"] --> B{"Platform reserves stock?"}
 B -->|No| C["Show unavailable or retry"]
 B -->|Yes| D{"Checkout completes before expiry?"}
 D -->|No| E["Release hold and reconcile payment"]
 D -->|Yes| F["Place order and allocate stock"]
 F --> G{"Seller can fulfil?"}
 G -->|Yes| H["Ship and consume allocation"]
 G -->|No| I["Cancel and reconcile stock"]
 I --> J["Queue refund if captured"]
 J --> K["Notify customer of status"]
```

| Handoff | Current gap | Proposed control |
|---|---|---|
| Listing to checkout | Display may lag stock | Check authoritative availability when reserving |
| Checkout to payment | Final unit can be promised twice | Atomic hold keyed to checkout attempt |
| Payment to order | Callback may arrive after expiry | Reconcile late payment and prevent order resurrection |
| Seller to operations | Reason can be unclear | Require reason and isolate suspected missing inventory |
| Operations to support | Refund state can be unclear | Separate cancellation and refund statuses |
