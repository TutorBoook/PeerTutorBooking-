# TutorBook - Exercise 3: Core Processes Matrix

This completed table follows the **six processes P1-P6 and three data stores D1-D3** in the supplied Level-0 DFD. It makes each process's inputs, outputs and specific transformation rules explicit. Rules trace to the existing project Functional and Non-Functional Requirements.

| Process no. and name | Input data | Output data | Rules |
|---|---|---|---|
| P1 — Manage Accounts | Registration/login, AUS ID/email, profiles, password reset, tutor applications | Account/profile status; stored accounts; course tutor applications | AUS email required; unique AUS ID (FR-01); lock account after 5 failed logins for 15 minutes (FR-02); 30-minute single-use reset (FR-05); profile bio max 300 chars (FR-04). |
| P2 — Search Tutors | Course code; filters for weekday, time and location; D1 approved tutor records; D2 free slots | Approved matching tutor profiles; availability calendar; sorted results; suggestions | Return only approved course tutors (FR-06); optional filters/sorts (FR-07/08); show 14-day calendar (FR-09); suggest same-prefix courses when empty (FR-10). |
| P3 — Manage Tutor Availability | Recurring weekly slot specifications; exception date/time; existing D2 records | Updated D2 availability; tutor confirmation; available slots for search/booking | Only authorized tutor can manage slots; each slot is 30 or 60 minutes and has a location (FR-16); blocking dates must preserve recurring pattern (FR-17). |
| P4 — Book Tutoring Session | Student booking request; selected slot; D2 availability; D3 existing sessions | New Pending booking in D3; request to tutor; status or rejection reason to student | Only a free slot may be requested (FR-11); reject already booked slots and overlapping confirmed student sessions with reason (FR-12); concurrent requests must commit atomically (NFR-11). |
| P5 — Manage Scheduled Sessions | Pending booking decision; cancellation/reschedule; dashboard query; outcome updates | Updated D3 bookings; D2 slot releases/reallocations; notifications; dashboard data | Tutor can confirm/decline; pending expires within 24h or by start (FR-13). Student can cancel/reschedule ≥3h before start; reschedule keeps ID and returns to Pending (FR-14/15). Tutor marks ended sessions Completed/No-show (FR-18). |
| P6 — Administer Platform | Admin course-approval decisions; account deactivation; D1 applications; D3 future bookings | Approval/rejection and reason; deactivated account; cancelled future bookings; affected-user notices | Approve/reject tutors per course and record rejection reason (FR-19). Deactivation cancels future bookings regardless of 3h cutoff and notifies affected users (FR-20, FR-14). |

**Data stores:** D1 = User & Tutor Records; D2 = Availability Records; D3 = Booking / Session Records.  
**Scope:** No payment processing, video-call tutoring, AI-generated tutoring or native mobile app features.

Source: [TutorBook Functional Requirements](https://github.com/TutorBoook/PeerTutorBooking-/blob/master/Project/Requirements/Functional_Requirements.md) and [Use Cases](https://github.com/TutorBoook/PeerTutorBooking-/blob/master/Project/Requirements/Use_Cases.md).
