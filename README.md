# UML Diagrams Practice

> **Self-initiated portfolio case study.** Fictional online pickup ordering domain; no client or employment claim is implied.

This repository explains how three UML views communicate different questions about one bounded workflow: customer submits an order, staff make a decision, and kitchen staff update fulfilment. Each diagram is paired with assumptions and a reading guide so it can be discussed in an interview.

## Views

- [Use-case diagram](diagrams/use-case.md): actors, goals, and system boundary.
- [Activity diagram](diagrams/activity.md): decisions and alternate paths during submission.
- [Sequence diagram](diagrams/sequence.md): message order and responsibility during staff acceptance.

## Modeling choices

The customer, staff user, ordering service, and notification provider have distinct roles. A submitted request is `AwaitingReview`, not automatically accepted. Availability and price are rechecked before order creation. Notification delivery is asynchronous and does not undo an accepted order. These choices expose important business behavior without pretending that the diagrams describe a deployed system.

## How to read and discuss

Start with the use-case view to establish scope, then use the activity view to explain branching behavior, and finally use the sequence view to discuss ordering and failure boundaries. The models are intentionally complementary, not three independent specifications. Mermaid renders on GitHub; its notation is a readable lightweight representation rather than a claim of formal UML tool validation.
