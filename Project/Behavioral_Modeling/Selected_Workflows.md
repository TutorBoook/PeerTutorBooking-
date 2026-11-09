# Selected Workflows — TutorBook (Lab 7)

The activity models use exactly the same three use cases as the Lab 6 sequence diagrams. Each diagram presents the **workflow**, rather than the method-call chronology, and keeps the TutorBook scope defined in prior labs.

| Use case | Primary actor | Workflow and significant decisions | Related Lab 5 services |
|---|---|---|---|
| UC-06 — Search Tutors by Course | Student | Validate search input, examine candidate tutor approvals, return matching tutors or validation failure | TutorSearchService, SearchCriteria, TutorProfile |
| UC-11 — Request Booking | Student | Validate dated availability, check conflicts, create a PENDING booking atomically, notify tutor or reject | BookingService, AvailabilityService, Booking, NotificationService |
| UC-12 — Respond to Booking Request | Peer Tutor (Student role) | Check pending/unexpired request, confirm or decline, audit and notify; otherwise reject | BookingService, Booking, NotificationService |

## Modeling decisions

- Each model contains an initial node, final node, named actions, arrows and guard-labeled decisions.
- Alternative branches rejoin before the final node; UC-06 loops through candidate profiles.
- Responsibility groups distinguish the initiating actor from the services and domain objects.
- No concurrency is invented: UML fork/join bars are omitted because these selected flows do not establish genuinely parallel activities.
- UC-12's automatic-expiry sweep is not incorrectly placed inside the tutor's action; it is a separate system-triggered process represented in the corresponding Lab 6 model.
- Each PNG/PDF corresponds to the editable Graphviz DOT model stored alongside it.
