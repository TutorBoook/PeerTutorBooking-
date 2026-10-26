# TutorBook — Class Model Consistency and Traceability Check

Source: COE420L Lab 5 report, Section 5.

## 1. Use cases and functional requirements

| Use case | FR | Realised by (class / operation) |
| --- | --- | --- |
| UC-01 Register Account | FR-01 | AccountService.register(), Student, User, Profile |
| UC-02 Log In | FR-02 | AccountService.login(), User.recordFailedLogin()/isLocked(), AccountStatus |
| UC-03 Reset Password | FR-05 | AccountService.requestPasswordReset()/resetPassword(), PasswordResetToken, NotificationService.sendResetLink(), EmailService |
| UC-04 Manage Profile | FR-04 | Profile.update()/addCourseOfInterest(), Course |
| UC-05 Apply to Tutor a Course | FR-03, FR-19 | Student.applyToTutor()/switchView(), TutorApplication, TutorProfile, Role |
| UC-06 Search Tutors by Course | FR-06 | TutorSearchService.searchTutors(), SearchCriteria, TutorProfile.isApprovedFor() |
| UC-07 Filter Search Results | FR-07 | SearchFilter, DayOfWeekFilter, TimeRangeFilter, LocationFilter |
| UC-08 Sort Search Results | FR-08 | SortOption, TutorSearchService.sortResults(), TutorProfile.getEarliestFreeSlot() |
| UC-09 View Tutor Profile | FR-09 | TutorSearchService.viewTutorProfile(), TutorProfile.getAvailabilityCalendar(), SlotOccurrence |
| UC-10 View Alternative Course Suggestions | FR-10 | TutorSearchService.suggestAlternativeCourses(), Course.hasSamePrefix() |
| UC-11 Request Booking | FR-11 | BookingService.requestBooking(), Booking, NotificationService.notifyBookingRequest() |
| UC-12 Respond to Booking Request | FR-13 | BookingService.respondToRequest()/expirePendingBookings(), Booking.confirm()/decline()/expire() |
| UC-13 Cancel Booking | FR-14 | BookingService.cancelBooking(), Booking.cancel()/canStudentModify() |
| UC-14 Reschedule Booking | FR-15 | BookingService.rescheduleBooking(), Booking.reschedule(), BookingChangeLog |
| UC-15 Validate Booking Slot | FR-12 | BookingService.validateSlot(), ValidationResult, Booking.overlaps(), AvailabilityService.getFreeOccurrences() |
| UC-16 Manage Weekly Availability | FR-16 | AvailabilityService.addRecurringSlot()/editRecurringSlot()/removeRecurringSlot(), AvailabilitySlot |
| UC-17 Block Unavailable Time | FR-17 | AvailabilityService.blockPeriod(), BlockedPeriod |
| UC-18 View Session Dashboard | FR-18 | BookingService.getDashboard(), Booking |
| UC-19 Record Session Outcome | FR-18 | BookingService.recordOutcome(), Booking.recordOutcome(), TutorProfile.incrementCompletedSessions() |
| UC-20 Review Tutor Application | FR-19 | AdminService.reviewApplication(), TutorApplication.approve()/reject(), Administrator |
| UC-21 Deactivate Account | FR-20 | AdminService.deactivateAccount(), User.deactivate(), BookingService.cancelAllFutureBookings(), NotificationService.notifyDeactivation() |

## 2. DFD processes, stores, and external entities

| Lab 4 DFD element | Class(es) |
| --- | --- |
| D1 User & Tutor Records | User, Student, Administrator, Profile, PasswordResetToken, TutorApplication, Course, TutorProfile |
| D2 Availability Records | AvailabilitySlot, BlockedPeriod (SlotOccurrence is computed, not stored) |
| D3 Booking / Session Records | Booking, BookingChangeLog |
| P1 Manage Accounts | AccountService |
| P2 Search Tutors | TutorSearchService (SearchCriteria, SearchFilter hierarchy) |
| P3 Manage Tutor Availability | AvailabilityService |
| P4 Book Tutoring Session | BookingService.requestBooking()/validateSlot() |
| P5 Manage Scheduled Sessions | BookingService.respondToRequest()/cancelBooking()/rescheduleBooking()/getDashboard()/recordOutcome() |
| P6 Administer Platform | AdminService |
| External entities | Student → Student; Peer Tutor → Student with TutorProfile; System Administrator → Administrator; Email Service → «interface» EmailService |

## 3. Class relationships and multiplicities

| Relationship | Justification |
| --- | --- |
| User 1 — 0..* PasswordResetToken (requests) | Single-use links: a user may request several over time; each token belongs to one account (FR-05). |
| Student 1 ◆— 1 Profile (has) | Every student account has exactly one profile, deleted with the account (FR-04). |
| Profile 0..* — 0..* Course (interested in) | A profile lists any number of courses; a course interests many students (FR-04). |
| Student 1 — 0..* TutorApplication (submits) | One application per course; a student may apply for several courses (FR-03). |
| TutorApplication 0..* — 1 Course (for) | Approval is per course, so each application names exactly one course (FR-19). |
| Administrator 0..1 — 0..* TutorApplication (reviews) | A pending application has no reviewer yet; one admin reviews many (FR-19). |
| Administrator 0..1 — 0..* User (deactivates) | Active accounts have no deactivating admin; one admin may deactivate many (FR-20). |
| Student 1 ◆— 0..1 TutorProfile (holds tutor role) | At most one tutor role per account, none until an approval (FR-03). |
| TutorProfile 0..* — 1..* Course (/approved for, derived) | A tutor exists only after at least one approval; derived from APPROVED applications (FR-06, FR-19). |
| TutorProfile 1 ◆— 0..* AvailabilitySlot (offers) | Slots belong to one tutor; a new tutor may have none yet (FR-16). |
| TutorProfile 1 ◆— 0..* BlockedPeriod (blocks) | Blocks belong to one tutor and are optional (FR-17). |
| Student 1 — 0..* Booking (requests) | Each booking has exactly one requesting student (FR-11). |
| Booking 0..* — 1 AvailabilitySlot (reserves) | A weekly slot is booked on many dates in a semester; each booking reserves one slot (FR-11, FR-15). |
| Booking 1 ◆— 1..* BookingChangeLog (history) | Creation is the first entry; every change is logged (FR-15). |
| BookingChangeLog 0..* — 0..1 User (performed by) | Student, tutor or admin changes name the user; automatic expiry has none (FR-13). |
| SearchCriteria 1 ◆— 0..* SearchFilter (narrowed by) | Filters are optional and exist only for one search (UC-07 «extend»). |
| Student, Administrator ⟶ User (inheritance) | Both are accounts with shared login, lock-out and deactivation; Administrator has no student functions (NFR-02). |
| DayOfWeek/TimeRange/LocationFilter ⟶ SearchFilter (inheritance) | Each is a kind of result filter with its own matches() rule (NFR-05). |

## 4. Quality and scope checklist

| Area | Check | Status | Evidence |
| --- | --- | --- | --- |
| Individual work | Each member submitted an inventory and a tool-made class diagram | Yes | Sections 1.1–1.4 and Figures 1–4; 11 / 10 / 6 / 13 classes. |
| Individual work | Attributes, methods, visibility, types, parameters, return types | Yes | All classes use +, −, # with typed attributes and full signatures. |
| Individual work | Associations named with multiplicities; inheritance present | Yes | Every diagram has named associations with multiplicities and at least one inheritance. |
| Integration | Duplicates and conflicts resolved and recorded | Yes | 7 duplicates (Section 3.1) and 8 decisions D-01–D-08 (Section 3.2). |
| Requirements | Every use case realised by at least one class/operation | Yes | UC-01–UC-21 all mapped in Section 5.1. |
| Requirements | Key NFRs reflected in the structure | Yes | NFR-01 hashPassword(); NFR-02 separate Administrator class; NFR-05 SearchFilter + service layer; NFR-09 SearchCriteria.isValid(); NFR-11 validateSlot note; NFR-15 ValidationResult.reason. |
| DFD | Every data store and process has corresponding classes | Yes | D1–D3 and P1–P6 mapped in Section 5.2. |
| Relationships | Multiplicities justified; inheritance only for real specialisation | Yes | 18 relationships justified in Section 5.3; Tutor-as-subclass rejected (D-01). |
| Out of scope | No classes for payments, video calls, AI tutoring or registration integration | Yes | None present. |

## Consolidation traceability

The approved class inventory in `Class_Inventory.md` maps every element to use cases, individual origin identifiers, and the contributor. `Integration_Notes.md` records seven consolidation items and eight explicit decisions.

**Scope exclusions (as reported):** payments, video calls, AI tutoring, integration with registration systems, and native mobile apps.
