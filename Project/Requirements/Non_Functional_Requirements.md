# TutorBook Non-Functional Requirements

The table is the team-consolidated list. Each member contributed five requirements. NFR-03, NFR-10, and NFR-13 were revised during team consolidation.

| ID | Category | Contributor | Final requirement |
|---|---|---|---|
| NFR-01 | Security | Hasan Omar (b00100248) | Passwords shall be stored only as salted bcrypt hashes at work factor ≥ 12; no plaintext password shall be written to the database or any log file. |
| NFR-02 | Security | Hasan Omar (b00100248) | Role-based access control shall prevent a student account from reaching tutor availability-management or administrator functions, verified by a test suite covering every protected endpoint. |
| NFR-03 | Usability | Hasan Omar (b00100248) | A first-time student shall complete registration and submit a first booking request within 5 minutes unassisted, achieved by at least 8 of 10 usability-test participants. |
| NFR-04 | Portability | Hasan Omar (b00100248) | The interface shall function on current Chrome, Safari, Firefox and Edge, and remain usable without horizontal scrolling down to 360 px width. |
| NFR-05 | Maintainability | Hasan Omar (b00100248) | The system shall follow a three-layer architecture (presentation, logic, data access); adding a new search filter shall require changes to no more than two modules. |
| NFR-06 | Performance | Abdul Raffay (B00100018) | Tutor search shall return results within 2 seconds for 95% of requests, with 500 tutors and 5,000 availability slots in the database. |
| NFR-07 | Scalability | Abdul Raffay (B00100018) | The system shall support 200 concurrent active users with no more than 20% degradation in average response time. |
| NFR-08 | Performance | Abdul Raffay (B00100018) | A tutor's 14-day availability calendar shall render within 1.5 seconds of opening the profile page. |
| NFR-09 | Robustness | Abdul Raffay (B00100018) | Invalid or malformed search input shall never terminate a session; the system shall show a validation message, log the event, and stay operational. |
| NFR-10 | Size | Abdul Raffay (B00100018) | The initial client-side bundle shall not exceed 2 MB and shall load within 3 seconds on a 10 Mbps connection. |
| NFR-11 | Reliability | Mohammed Jabsheh (b00097438) | Booking creation shall be atomic; for concurrent requests on one slot exactly one shall be recorded, verified by a test issuing 100 simultaneous requests. |
| NFR-12 | Reliability | Mohammed Jabsheh (b00097438) | The system shall be available at least 99% of the time between 08:00 and 22:00 GST during the semester, with unplanned downtime ≤ 2 hours per month. |
| NFR-13 | Reliability | Mohammed Jabsheh (b00097438) | The database shall be backed up automatically every 24 hours and be restorable from the latest backup within 2 hours. |
| NFR-14 | Performance | Mohammed Jabsheh (b00097438) | A confirmed booking shall be persisted and visible in both dashboards within 3 seconds of confirmation. |
| NFR-15 | Usability | Mohammed Jabsheh (b00097438) | Every error message shall state the cause and next action in plain language; raw database errors, stack traces and internal codes shall never be displayed. |
| NFR-16 | Security | Hassan Almahdawi (b00102063) | All client–server communication shall use HTTPS with TLS 1.2 or higher; email addresses and AUS IDs shall never appear in URL query strings. |
| NFR-17 | Maintainability | Hassan Almahdawi (b00102063) | The booking and availability modules shall maintain at least 70% unit-test line coverage, with the suite running automatically on every push to the repository. |
| NFR-18 | Portability | Hassan Almahdawi (b00102063) | The system shall be deployable on any machine with the documented runtime and SQL database, reaching a working local instance within 30 minutes via the README. |
| NFR-19 | Robustness | Hassan Almahdawi (b00102063) | On loss of the database connection the system shall display a retry message and resume normal operation within 60 seconds of restoration, without a restart. |
| NFR-20 | Usability | Hassan Almahdawi (b00102063) | All text shall meet a minimum contrast ratio of 4.5:1, and the full booking flow shall be operable by keyboard alone. |

## Consolidation decisions

- NFR-03 measures the student's submission of a booking request, because tutor confirmation depends on someone else.
- NFR-10 uses a measurable 10 Mbps connection instead of an unspecified campus Wi-Fi connection.
- NFR-13 sets a two-hour restoration target consistent with the downtime target in NFR-12.
- NFR-09 concerns continued operation after invalid input; NFR-15 concerns the wording of error messages.
