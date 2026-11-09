# Sequence View — Staff Accepts an Order

```mermaid
sequenceDiagram
  actor Lead as Shift lead
  participant Browser as Staff browser
  participant Service as Order service
  participant Store as Order store
  participant Worker as Notification worker
  Lead->>Browser: Select Accept
  Browser->>Service: Transition(order, expected=AwaitingReview, target=Accepted)
  Service->>Store: Compare state and append transition event
  alt State still AwaitingReview
    Store-->>Service: Commit Accepted and event
    Service-->>Browser: Accepted with current state
    Service->>Worker: Enqueue customer update
    Worker-->>Service: Delivery result later
  else Another staff member already acted
    Store-->>Service: State conflict
    Service-->>Browser: Conflict plus current state
  end
```

## Sequence notes

The store performs a compare-and-transition so two staff actions cannot both win based on stale screens. The customer notification is queued only after the state is committed. Delivery failure requires retry and staff visibility; it does not revert the accepted state.
