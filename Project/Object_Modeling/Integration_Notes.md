# TutorBook — Integration and Consolidation Notes

Source: COE420L Lab 5 report, Part B, Sections 3.1–3.2. Each member first modeled their assigned component; the team reviewed duplicate responsibilities, data ownership, associations, multiplicities, inheritance, and the prior DFD.

## Duplicate classes and consolidation resolutions

| Individual classes | Problem found | Resolution | Final |
| --- | --- | --- | --- |
| HO-03 Administrator / HA-09 Administrator | Same class modelled twice. | Merged into one Administrator subclass of User; Hassan Almahdawi's "deactivates" association kept. | C03 |
| HO-06 TutorApplication / HA-08 CourseApproval | Both represent the per-course tutor approval stored in D1; keeping both would store the decision twice. | Merged into TutorApplication (status + reviewedAt + rejectionReason, reviewed by Administrator). | C06 |
| MJ-01 Booking / HA-05 Session | Both represent the same D3 record; a separate Session would duplicate start/end and need syncing. | Merged into Booking; COMPLETED and NO_SHOW added to BookingStatus; recordOutcome() moved to Booking. | C16, E05 |
| MJ-05 BookingStatus / HA-06 SessionOutcome | Two enumerations for one lifecycle. | Single BookingStatus with seven values; UPCOMING dropped (it equals CONFIRMED before start). | E05 |
| MJ-03 BookingService / HA-07 SessionService | Both implement DFD process P5 (Manage Scheduled Sessions). | Merged into BookingService: getDashboard() and recordOutcome() added. | C18 |
| AR-08 TimeSlot / HA-03 SlotOccurrence | Same concept: one dated instance of a recurring slot. | Kept SlotOccurrence (name makes clear it is derived, not stored); TimeSlot.isFree() dropped because AvailabilityService computes free occurrences. | C22 |
| HO-08 EmailSender / HA-12 EmailService | Two boundaries to the same external Email Service actor. | One «interface» EmailService named after the Lab 3 actor; message text moved to NotificationService. | C25, C26 |

The individual models contain **40 candidate classes** in total, while the approved model contains **26 classes and 6 enumerations**. These are not identical sets: the approved model has merged or removed several redundant individual candidates. The final diagram is the authoritative team model.

## Design decisions (D-01–D-08)

| ID | Issue | Reason | Decision |
| --- | --- | --- | --- |
| D-01 | Tutor as a subclass of Student (MJ-06) vs. Tutor as a role (HO-02, AR-02) | FR-03 requires one account to hold both roles and switch without logging out, and the role is gained only after an approval (FR-19). An object cannot change class at runtime, so a subclass cannot model this. | Student 1 ◆— 0..1 TutorProfile. MJ-06 removed; the Lab 3 actor generalisation stays valid in the use case diagram. |
| D-02 | Where a tutor's approved courses live (MJ-06 approvedCourses: List<String>) | A second copy of approvals could disagree with the administrator's decision. | Derived association TutorProfile "/approved for" Course, computed from APPROVED TutorApplications (single source of truth). |
| D-03 | How booking operations receive a slot (MJ: slotId + date, HA: SlotOccurrence) | Two parameter styles for the same thing across services. | All booking/search operations take a SlotOccurrence; SearchFilter.matches() also uses it. |
| D-04 | Admin cancellation after the Session merge | AdminService previously cancelled sessions through SessionService, which no longer exists. | BookingService.cancelAllFutureBookings(userId) added; Booking.cancel(byAdmin = true) skips the 3-hour check (FR-14 clarification, FR-20). |
| D-05 | Notifications to tutors on new requests (missing class responsibility) | The Level-0 DFD sends a "request to tutor" from P4, but no booking class sent it. | NotificationService widened to all outgoing messages: reset link, booking request, status change, deactivation. |
| D-06 | Completed-session count used for sorting (missing link) | FR-08 sorts by completed sessions, but recording an outcome (Hassan Almahdawi) did not update the count used by search (Abdul Raffay). | Booking.recordOutcome(COMPLETED) calls TutorProfile.incrementCompletedSessions(). |
| D-07 | Who performs an automatic expiry | BookingChangeLog required exactly one User, but expiry (FR-13) is done by the system. | Multiplicity changed to 0..1 (empty for automatic expiry). |
| D-08 | Type of DayOfWeekFilter.day (AR: String, HA: DayOfWeek) | A String allows invalid days (NFR-09). | Uses the DayOfWeek enumeration. |

## Important final-model implications

- `Tutor` is **not** a subclass of `Student` in the consolidated class diagram. `Student` owns an optional `TutorProfile` (D-01).
- `CourseApproval` merges into `TutorApplication`; approved courses derive from approved applications (D-02).
- `Session` and `SessionOutcome` merge into `Booking` and `BookingStatus`; `SessionService` merges into `BookingService`.
- `TimeSlot` and `SlotOccurrence` merge into the computed `SlotOccurrence` data type, not a stored data record.
- `EmailSender` and `EmailService` merge into the one external `EmailService` interface.
- `BookingService` handles administrative cancellation of all future bookings without the usual three-hour restriction (D-04).
- Booking expiry has no acting `User` in its change log (D-07).

**Traceability:** The approved model links each retained C/E identifier back to its individual contributor and origin in `Class_Inventory.md`.
