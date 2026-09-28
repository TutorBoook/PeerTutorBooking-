# TutorBook Use Cases

All 21 use cases contributed by the team were approved. Student and Tutor are specializations of User. A tutor retains a student account and can also search for tutors and book sessions. Administrator is a separate actor. Email Service is a secondary external actor.

| ID | Use case | Primary actor | Description | FR trace | Contributor |
|---|---|---|---|---|---|
| UC-01 | Register Account | Student | Register with an AUS email and AUS ID; reject other domains and duplicate IDs. | FR-01 | Hasan Omar (b00100248) |
| UC-02 | Log In | User, Administrator | Sign in with email and password; lock the account for 15 minutes after five consecutive failures. | FR-02 | Hasan Omar (b00100248) |
| UC-03 | Reset Password | User; Email Service is secondary | Request a single-use password-reset link valid for 30 minutes and set a new password. | FR-05 | Hasan Omar (b00100248) |
| UC-04 | Manage Profile | User | View and edit name, major, academic year, courses of interest, and a biography of up to 300 characters. | FR-04 | Hasan Omar (b00100248) |
| UC-05 | Apply to Tutor a Course | Student | Apply to tutor a course; an approved application grants the Tutor role on the same account. | FR-03, FR-19 | Hasan Omar (b00100248) |
| UC-06 | Search Tutors by Course | Student | Enter a course code and see tutors approved for that course. | FR-06 | Abdul Raffay (B00100018) |
| UC-07 | Filter Search Results | Student | Narrow results by day, time range, and location. | FR-07 | Abdul Raffay (B00100018) |
| UC-08 | Sort Search Results | Student | Order results by earliest available slot or number of completed sessions. | FR-08 | Abdul Raffay (B00100018) |
| UC-09 | View Tutor Profile | Student | See courses tutored, biography, and a 14-day availability calendar. | FR-09 | Abdul Raffay (B00100018) |
| UC-10 | View Alternative Course Suggestions | Student | When no tutors match, see available courses with the same course-code prefix. | FR-10 | Abdul Raffay (B00100018) |
| UC-11 | Request Booking | Student | Select a free tutor slot and create a Pending booking. | FR-11 | Mohammed Jabsheh (b00097438) |
| UC-12 | Respond to Booking Request | Tutor | Confirm or decline a pending request; unanswered requests expire at the applicable deadline. | FR-13 | Mohammed Jabsheh (b00097438) |
| UC-13 | Cancel Booking | Student | Cancel a confirmed booking at least three hours before it starts and release the slot. | FR-14 | Mohammed Jabsheh (b00097438) |
| UC-14 | Reschedule Booking | Student | Move a confirmed booking to a free slot of the same tutor, keeping its ID, logging the change, and returning it to Pending. | FR-15 | Mohammed Jabsheh (b00097438) |
| UC-15 | Validate Booking Slot | Included by UC-11 and UC-14 | Check that the slot is free and does not overlap a confirmed student session; reserve it atomically or report why it cannot be booked. | FR-12 | Mohammed Jabsheh (b00097438) |
| UC-16 | Manage Weekly Availability | Tutor | Create, edit, or remove recurring 30- or 60-minute weekly slots with locations. | FR-16 | Hassan Almahdawi (b00102063) |
| UC-17 | Block Unavailable Time | Tutor | Block a date or time range without deleting the recurring availability pattern. | FR-17 | Hassan Almahdawi (b00102063) |
| UC-18 | View Session Dashboard | User | See upcoming and past sessions and their statuses. | FR-18 | Hassan Almahdawi (b00102063) |
| UC-19 | Record Session Outcome | Tutor | Mark an ended session Completed or No-show. | FR-18 | Hassan Almahdawi (b00102063) |
| UC-20 | Review Tutor Application | Administrator | Approve or reject an application for a particular course, recording a reason for rejection. | FR-19 | Hassan Almahdawi (b00102063) |
| UC-21 | Deactivate Account | Administrator; Email Service is secondary | Deactivate an account, cancel its future bookings, and email affected users. | FR-20 | Hassan Almahdawi (b00102063) |

## Use case relationships

For `<<include>>`, the base use case always performs the related use case. For `<<extend>>`, the related use case adds optional or conditional behavior to the base use case.

| ID | Base use case | Related use case | Relationship | Reason |
|---|---|---|---|---|
| R-01 | UC-11 Request Booking | UC-15 Validate Booking Slot | `<<include>>` | Every booking request must check and reserve the slot before the booking is created. |
| R-02 | UC-14 Reschedule Booking | UC-15 Validate Booking Slot | `<<include>>` | Every reschedule must check and reserve the proposed new slot. |
| R-03 | UC-02 Log In | UC-03 Reset Password | `<<extend>>` | Reset is triggered only when the user selects “Forgot password.” |
| R-04 | UC-06 Search Tutors by Course | UC-07 Filter Search Results | `<<extend>>` | Filtering is optional after a search. |
| R-05 | UC-06 Search Tutors by Course | UC-08 Sort Search Results | `<<extend>>` | Choosing a different sort order is optional. |
| R-06 | UC-06 Search Tutors by Course | UC-10 View Alternative Course Suggestions | `<<extend>>` | Suggestions appear only when the search finds no tutors. |
| R-07 | UC-16 Manage Weekly Availability | UC-17 Block Unavailable Time | `<<extend>>` | The tutor may optionally add an exception to recurring availability. |
| R-08 | UC-18 View Session Dashboard | UC-19 Record Session Outcome | `<<extend>>` | A tutor can record an outcome only after the session has ended. |

Logging in is a precondition for protected functions; it is not modeled as an `<<include>>` relationship for every use case.
