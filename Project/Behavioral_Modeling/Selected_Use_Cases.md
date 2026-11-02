# TutorBook — Lab 6 Selected Major Use Cases

The selected use cases were traced to the consolidated Lab 5 class inventory and use-case crosswalk. Each diagram represents a distinct Lab 3 use case.

| Use Case ID | Name | Primary Actor | Purpose | Reason for Selection |
|---|---|---|---|---|
| UC-06 | Search Tutors by Course | Student | Locate approved peer tutors for an AUS course. | Models search-criteria validation and the repeated approval check for candidate tutors. |
| UC-11 | Request Booking | Student | Request a PENDING session for a valid free slot. | Shows cross-service availability validation, atomic booking creation and request notification. |
| UC-12 | Respond to Booking Request | Peer Tutor (Student role) | Confirm or decline a booking while the request remains actionable. | Demonstrates booking status transitions, deadline guards and status-change notifications. |

## Modeling conventions

- The diagrams show actors, service/entity/interface lifelines, method calls, activation bars, returns, guarded `alt` branches and one `loop` fragment.
- Peer Tutor is a Student with a TutorProfile role, not a separate Tutor class in the consolidated model.
- The model excludes payment processing, video calls, AI tutoring, registration-system integration and native mobile apps.
- The PNG images and corresponding editable Mermaid `.mmd` sources are in `Sequence_Diagrams/`.
