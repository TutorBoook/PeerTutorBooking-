# TutorBook - DFD Consistency and Balancing Check (Lab 4)

## 1. Existing model preserved

The supplied student work identifies three primary external entities (**Student**, **Peer Tutor**, **System Administrator**); six Level-0 processes (**P1-P6**); and three data stores (**D1-D3**). The original team images (AI-refined from handwritten diagrams) have been restored to the package unchanged in content.

## 2. External flow balancing: Context vs. Level-0

| External entity | Context input to TutorBook | Corresponding Level-0 process(es) | Context output from TutorBook | Corresponding Level-0 process(es) |
|---|---|---|---|---|
| Student | Register/login/profile, tutor application, search, booking and session-change requests | P1, P2, P4, P5 | Account status, search results, booking status, session details | P1, P2, P4, P5; administrative notices via P6 |
| Peer Tutor | Register/login/profile, recurring availability, exceptions, booking decisions, session outcomes | P1, P3, P5 | Account status, booking requests, schedule/session information | P1, P3, P4, P5; admin notices via P6 |
| System Administrator | Login, tutor application review, account deactivation | P1, P6 | Login status, applications, user/booking information and action results | P1, P6 |

**Balancing status:** The same three modeled external entities occur in both diagrams, and the data-flow *categories* above can be mapped conceptually. However, the original Context Diagram appears to reverse the Student arrow directions relative to the labels: the registration/search/booking information is shown on an arrow toward the Student, and account confirmation/search results are shown on an arrow toward the system. These need confirmation/correction for formal directional balancing. This file does not claim the images have passed a full flow-by-flow verification.

## 3. Data flow logic and store checks

- **D1** stores user, profile and course tutor-approval records. P1 reads/writes D1, while P2 and P6 consume tutor or account information.
- **D2** stores weekly availability and blocked times. P3 maintains it, P2 searches it, P4 checks it and P5 updates slot state.
- **D3** stores bookings and session status. P4 creates Pending bookings, P5 changes bookings and P6 cancels future bookings on deactivation.
- In the diagram, no external actor communicates directly with a data store; data crosses through a named process.
- Process inputs and outputs are covered by the six matrix rows; process IDs and names match the Level-0 DFD exactly.

## 4. Requirements traceability

| Process | Linked use cases / functional requirements |
|---|---|
| P1 Manage Accounts | UC-01..UC-05, FR-01..FR-05 |
| P2 Search Tutors | UC-06..UC-10, FR-06..FR-10 |
| P3 Manage Tutor Availability | UC-16..UC-17, FR-16..FR-17 |
| P4 Book Tutoring Session | UC-11, UC-15, FR-11..FR-12 |
| P5 Manage Scheduled Sessions | UC-12..UC-14, UC-18..UC-19, FR-13..FR-15, FR-18 |
| P6 Administer Platform | UC-20..UC-21, FR-19..FR-20 |
