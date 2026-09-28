# TutorBook Functional Requirements

The table is the team-consolidated list. Each member contributed five requirements. The contributor and original requirement ID remain attached to every approved requirement. FR-03, FR-10, FR-13, FR-14, and FR-15 were revised during team consolidation.

| ID | Contributor | Source | Final requirement |
|---|---|---|---|
| FR-01 | Hasan Omar (b00100248) | S-01 | The system shall allow a student to register using an AUS email address and AUS ID, and shall reject registration if the email domain is not `aus.edu` or the AUS ID is already registered. |
| FR-02 | Hasan Omar (b00100248) | S-01 | The system shall authenticate a user by email and password, and shall lock the account for 15 minutes after 5 consecutive failed login attempts. |
| FR-03 | Hasan Omar (b00100248) | S-03, S-06 | The system shall allow a student to apply to tutor a specific course; once at least one application is approved (FR-19), the same account shall hold both Student and Tutor roles and the user shall be able to switch between views without logging out. |
| FR-04 | Hasan Omar (b00100248) | S-01 | The system shall allow a user to create and edit a profile with full name, major, academic year, courses of interest, and a biography of at most 300 characters. |
| FR-05 | Hasan Omar (b00100248) | S-01 | The system shall allow a password reset through a single-use link sent to the registered email address, valid for 30 minutes. |
| FR-06 | Abdul Raffay (B00100018) | S-02 | The system shall allow a student to search for tutors by course code and shall return only tutors approved to tutor that course. |
| FR-07 | Abdul Raffay (B00100018) | S-02 | The system shall allow filtering of search results by day of week, time range, and session location. |
| FR-08 | Abdul Raffay (B00100018) | S-02 | The system shall allow sorting of search results by earliest available slot or by the tutor's number of completed sessions. |
| FR-09 | Abdul Raffay (B00100018) | S-02 | The system shall display a tutor's public profile with courses tutored, biography, and an availability calendar covering the next 14 days. |
| FR-10 | Abdul Raffay (B00100018) | S-02 | The system shall display a "no tutors available" message on an empty search and list other courses with the same course-code prefix (e.g., COE) that have available tutors. |
| FR-11 | Mohammed Jabsheh (b00097438) | S-02 | The system shall allow a student to request a booking by selecting a free slot from a tutor's availability, creating the booking with status Pending. |
| FR-12 | Mohammed Jabsheh (b00097438) | S-07 | The system shall reject a booking if the slot is already booked or overlaps a session the student has already confirmed, and shall display the reason. |
| FR-13 | Mohammed Jabsheh (b00097438) | S-04 | The system shall allow a tutor to confirm or decline a pending request, and shall set it to Expired automatically if it is unanswered within 24 hours or by the slot's start time, whichever comes first. |
| FR-14 | Mohammed Jabsheh (b00097438) | S-05 | The system shall allow a student to cancel a confirmed booking up to 3 hours before its start time, returning the slot to the tutor's public availability. Administrator-initiated cancellations under FR-20 are exempt from the 3-hour limit. |
| FR-15 | Mohammed Jabsheh (b00097438) | S-05 | The system shall allow a student to reschedule a confirmed booking, up to 3 hours before its start time, to another free slot of the same tutor that passes the FR-12 checks; the booking shall retain its identifier, return to Pending for tutor confirmation (FR-13), and the change shall be logged. |
| FR-16 | Hassan Almahdawi (b00102063) | S-03 | The system shall allow a tutor to define recurring weekly availability slots of 30 or 60 minutes, each with a specified location. |
| FR-17 | Hassan Almahdawi (b00102063) | S-03 | The system shall allow a tutor to block a specific date or time range as unavailable without deleting the underlying recurring pattern. |
| FR-18 | Hassan Almahdawi (b00102063) | S-04 | The system shall provide each user a dashboard of upcoming and past sessions, and allow a tutor to mark a session Completed or No-show. |
| FR-19 | Hassan Almahdawi (b00102063) | S-06 | The system shall allow an administrator to approve or reject a tutor application per course, recording a written reason for each rejection. |
| FR-20 | Hassan Almahdawi (b00102063) | S-06 | The system shall allow an administrator to deactivate an account, automatically cancelling its future bookings and notifying the affected users. |

## Consolidation decisions

- FR-13 expires an unanswered request after 24 hours or at the slot start time, whichever occurs first.
- FR-15 applies the three-hour rescheduling limit, checks the new slot, and returns the booking to Pending.
- FR-14's three-hour limit applies to student cancellations, not administrator deactivation.
- FR-03 explains how approval of a course application grants the Tutor role.
- FR-10 defines related courses by their course-code prefix.
- FR-12 specifies double-booking behavior; NFR-11 specifies the concurrency guarantee.
