# Activity View — Submit Pickup Request

```mermaid
flowchart TD
  A([Start]) --> B[Browse published menu]
  B --> C[Select items, options, and quantity]
  C --> D[Enter contact and review notices]
  D --> E{Input valid?}
  E -- no --> F[Show field errors]
  F --> D
  E -- yes --> G[Recheck item availability and price]
  G --> H{No material changes?}
  H -- no --> I[Show changes and require confirmation]
  I --> C
  H -- yes --> J[Create order with idempotency key]
  J --> K{Already processed key?}
  K -- yes --> L[Return existing order reference]
  K -- no --> M[Store snapshot; set AwaitingReview]
  M --> N[Display reference and pending explanation]
  L --> O([End])
  N --> O
```

## Activity notes

- Validation before persistence avoids creating partial orders.
- Final availability and price checks address the time gap between menu browsing and submission.
- Idempotency handles transport retries; it does not merge two intentional orders.
- The diagram omits internal authentication, logging, and notification retries to keep its focus on the customer goal.
