# TutorBook — Class Inventories and Approved Team Model

Source: COE420L Lab 5 report, Part A and Section 3.3. The first four inventories are individual, **pre-integration** candidates. The final table gives the **approved integrated model**.

## Individual contributors

| Team Member | AUS ID | Modelled Component | Use Cases | Individual Class IDs |
| --- | --- | --- | --- | --- |
| Hasan Omar | b00100248 | Accounts, authentication & profiles | UC-01–UC-05 | HO-01–HO-11 |
| Abdul Raffay | B00100018 | Tutor search & discovery | UC-06–UC-10 | AR-01–AR-10 |
| Mohammed Jabsheh | b00097438 | Booking lifecycle | UC-11–UC-15 | MJ-01–MJ-06 |
| Hassan Almahdawi | b00102063 | Availability, sessions & administration | UC-16–UC-21 | HA-01–HA-13 |

## Hasan Omar — individual classes

| Class ID | Class Name | Purpose / Responsibility | Related Use Case(s) | Contributor |
| --- | --- | --- | --- | --- |
| HO-01 | User {abstract} | Abstract account holding credentials, account status and lock-out state shared by every login. | UC-02, UC-03 | Hasan Omar |
| HO-02 | Student | AUS student account; can gain the Tutor role and switch views without logging out. | UC-01, UC-05 | Hasan Omar |
| HO-03 | Administrator | Staff account that signs in with the same credentials mechanism but has no student functions. | UC-02 | Hasan Omar |
| HO-04 | Profile | Editable personal details and courses of interest of a student account. | UC-04 | Hasan Omar |
| HO-05 | PasswordResetToken | Single-use reset link token that expires 30 minutes after it is issued. | UC-03 | Hasan Omar |
| HO-06 | TutorApplication | A student's application to tutor one course, with status and rejection reason. | UC-05 | Hasan Omar |
| HO-07 | AccountService «control» | Implements DFD process P1: registration rules, login lock-out, password reset, tutor applications. | UC-01–UC-05 | Hasan Omar |
| HO-08 | EmailSender «interface» | Sends the password-reset link e-mail. | UC-03 | Hasan Omar |
| HO-09 | AccountStatus «enumeration» | Account state used for lock-out and deactivation. | UC-02 | Hasan Omar |
| HO-10 | Role «enumeration» | View a student account is currently using. | UC-05 | Hasan Omar |
| HO-11 | ApplicationStatus «enumeration» | Tutor application state. | UC-05 | Hasan Omar |

## Abdul Raffay — individual classes

| Class ID | Class Name | Purpose / Responsibility | Related Use Case(s) | Contributor |
| --- | --- | --- | --- | --- |
| AR-01 | Course | AUS course (e.g., CMP 305) used for applications, approvals, interests and search. | UC-06, UC-10 | Abdul Raffay |
| AR-02 | TutorProfile | The Tutor role of a student account: approved courses, public calendar, completed-session count. | UC-06, UC-08, UC-09 | Abdul Raffay |
| AR-03 | SearchCriteria | One tutor search request: course code, optional filters and sort order; validated before use. | UC-06–UC-08 | Abdul Raffay |
| AR-04 | SearchFilter {abstract} | Generalisation of the optional result filters, so a new filter is one new subclass. | UC-07 | Abdul Raffay |
| AR-05 | DayOfWeekFilter | Keeps tutors with a free slot on the chosen weekday. | UC-07 | Abdul Raffay |
| AR-06 | TimeRangeFilter | Keeps tutors with a free slot inside the chosen time range. | UC-07 | Abdul Raffay |
| AR-07 | LocationFilter | Keeps tutors with a free slot at the chosen location. | UC-07 | Abdul Raffay |
| AR-08 | TimeSlot «dataType» | A dated free slot of a tutor shown on the 14-day calendar. | UC-09 | Abdul Raffay |
| AR-09 | TutorSearchService «control» | Implements DFD process P2: approved-tutor search, filtering, sorting and same-prefix suggestions. | UC-06–UC-10 | Abdul Raffay |
| AR-10 | SortOption «enumeration» | Search sort order. | UC-08 | Abdul Raffay |

## Mohammed Jabsheh — individual classes

| Class ID | Class Name | Purpose / Responsibility | Related Use Case(s) | Contributor |
| --- | --- | --- | --- | --- |
| MJ-01 | Booking | A requested or confirmed session between one student and one tutor slot, with its status. | UC-11–UC-14 | Mohammed Jabsheh |
| MJ-02 | BookingChangeLog | Audit entry for every status change or reschedule of a booking. | UC-12–UC-14 | Mohammed Jabsheh |
| MJ-03 | BookingService «control» | Atomic booking creation, tutor response, expiry, cancellation and rescheduling. | UC-11–UC-15 | Mohammed Jabsheh |
| MJ-04 | ValidationResult «dataType» | Outcome of slot validation, carrying the rejection reason shown to the student. | UC-15 | Mohammed Jabsheh |
| MJ-05 | BookingStatus «enumeration» | PENDING, CONFIRMED, DECLINED, EXPIRED, CANCELLED. | UC-11–UC-14 | Mohammed Jabsheh |
| MJ-06 | Tutor (subclass of Student) | A student who tutors; receives booking requests and responds to them. | UC-12 | Mohammed Jabsheh |

## Hassan Almahdawi — individual classes

| Class ID | Class Name | Purpose / Responsibility | Related Use Case(s) | Contributor |
| --- | --- | --- | --- | --- |
| HA-01 | AvailabilitySlot | A tutor's recurring weekly slot with fixed length and location. | UC-16 | Hassan Almahdawi |
| HA-02 | BlockedPeriod | A date/time range a tutor marks unavailable without deleting recurring slots. | UC-17 | Hassan Almahdawi |
| HA-03 | SlotOccurrence «dataType» | One dated instance of a recurring slot, as shown on the 14-day calendar and selected for booking. | UC-16, UC-17 | Hassan Almahdawi |
| HA-04 | AvailabilityService «control» | Implements DFD process P3: recurring slots, blocked periods and free-slot calculation. | UC-16, UC-17 | Hassan Almahdawi |
| HA-05 | Session | A held tutoring session with its outcome (Completed / No-show). | UC-18, UC-19 | Hassan Almahdawi |
| HA-06 | SessionOutcome «enumeration» | UPCOMING, COMPLETED, NO_SHOW. | UC-19 | Hassan Almahdawi |
| HA-07 | SessionService «control» | Upcoming/past session dashboards and outcome recording. | UC-18, UC-19 | Hassan Almahdawi |
| HA-08 | CourseApproval | An administrator's approve/reject decision for one tutor and course. | UC-20 | Hassan Almahdawi |
| HA-09 | Administrator | Staff account performing approvals and deactivations. | UC-20, UC-21 | Hassan Almahdawi |
| HA-10 | AdminService «control» | Implements DFD process P6: per-course tutor approval and account deactivation. | UC-20, UC-21 | Hassan Almahdawi |
| HA-11 | NotificationService «control» | Composes deactivation and cancellation notices. | UC-21 | Hassan Almahdawi |
| HA-12 | EmailService «interface» | Boundary to the external Email Service actor from the use case model. | UC-21 | Hassan Almahdawi |
| HA-13 | DayOfWeek «enumeration» | Weekday of a recurring slot or filter. | UC-16 | Hassan Almahdawi |

## Approved consolidated model

The report records **26 classes (C01–C26) and 6 enumerations (E01–E06)**, total 32 modeled elements.

| ID | Class | Type | Responsibility | Use Cases | Origin | Contributor |
| --- | --- | --- | --- | --- | --- | --- |
| C01 | User | Entity (abstract) | Abstract account holding credentials, account status and lock-out state shared by every login. | UC-02, UC-03, UC-21 | HO-01 | Hasan Omar |
| C02 | Student | Entity | AUS student account; can gain the Tutor role and switch views without logging out. | UC-01, UC-05, UC-06, UC-11 | HO-02 | Hasan Omar |
| C03 | Administrator | Entity | Staff account that reviews tutor applications and deactivates accounts; no student functions. | UC-02, UC-20, UC-21 | HO-03, HA-09 | Hasan Omar |
| C04 | Profile | Entity | Editable personal details and courses of interest of a student account. | UC-04 | HO-04 | Hasan Omar |
| C05 | PasswordResetToken | Entity | Single-use reset link token that expires 30 minutes after it is issued. | UC-03 | HO-05 | Hasan Omar |
| C06 | TutorApplication | Entity | A student's request to tutor one course; its approval is the per-course tutor approval record. | UC-05, UC-20 | HO-06, HA-08 | Hasan Omar |
| C07 | AccountService | Control | Implements DFD process P1: registration rules, login lock-out, password reset, tutor applications. | UC-01 – UC-05 | HO-07 | Hasan Omar |
| C08 | Course | Entity | AUS course (e.g., CMP 305) used for applications, approvals, interests and search. | UC-05, UC-06, UC-10 | AR-01 | Abdul Raffay |
| C09 | TutorProfile | Entity | The Tutor role of a student account: approved courses, public calendar, completed-session count. | UC-06, UC-08, UC-09, UC-16 | AR-02, MJ-06 | Abdul Raffay |
| C10 | SearchCriteria | Entity | One tutor search request: course code, optional filters and sort order; validated before use. | UC-06, UC-07, UC-08 | AR-03 | Abdul Raffay |
| C11 | SearchFilter | Entity (abstract) | Generalisation of the optional result filters, so a new filter is one new subclass. | UC-07 | AR-04 | Abdul Raffay |
| C12 | DayOfWeekFilter | Entity | Keeps tutors with a free slot on the chosen weekday. | UC-07 | AR-05 | Abdul Raffay |
| C13 | TimeRangeFilter | Entity | Keeps tutors with a free slot inside the chosen time range. | UC-07 | AR-06 | Abdul Raffay |
| C14 | LocationFilter | Entity | Keeps tutors with a free slot at the chosen location. | UC-07 | AR-07 | Abdul Raffay |
| C15 | TutorSearchService | Control | Implements DFD process P2: approved-tutor search, filtering, sorting and same-prefix suggestions. | UC-06 – UC-10 | AR-09 | Abdul Raffay |
| C16 | Booking | Entity | A requested/scheduled tutoring session and its full status lifecycle, including outcomes. | UC-11 – UC-14, UC-18, UC-19 | MJ-01, HA-05 | Mohammed Jabsheh |
| C17 | BookingChangeLog | Entity | Audit entry for every status change or reschedule of a booking. | UC-12, UC-13, UC-14 | MJ-02 | Mohammed Jabsheh |
| C18 | BookingService | Control | Implements DFD processes P4 and P5: atomic booking, tutor responses, expiry, cancel/reschedule, dashboards, outcomes. | UC-11 – UC-15, UC-18, UC-19 | MJ-03, HA-07 | Mohammed Jabsheh |
| C19 | ValidationResult | Data type | Outcome of slot validation, carrying the rejection reason shown to the student. | UC-15 | MJ-04 | Mohammed Jabsheh |
| C20 | AvailabilitySlot | Entity | A tutor's recurring weekly slot with fixed length and location. | UC-16 | HA-01 | Hassan Almahdawi |
| C21 | BlockedPeriod | Entity | A date/time range a tutor marks unavailable without deleting recurring slots. | UC-17 | HA-02 | Hassan Almahdawi |
| C22 | SlotOccurrence | Data type | One dated instance of a recurring slot, as shown on the 14-day calendar and selected for booking. | UC-09, UC-11, UC-14 | HA-03, AR-08 | Hassan Almahdawi |
| C23 | AvailabilityService | Control | Implements DFD process P3: recurring slots, blocked periods and free-slot calculation. | UC-16, UC-17 | HA-04 | Hassan Almahdawi |
| C24 | AdminService | Control | Implements DFD process P6: per-course tutor approval and account deactivation. | UC-20, UC-21 | HA-10 | Hassan Almahdawi |
| C25 | NotificationService | Control | Builds every outgoing message (reset link, booking request/status, deactivation notice). | UC-03, UC-12, UC-21 | HA-11 | Hassan Almahdawi |
| C26 | EmailService | Interface | Boundary to the external Email Service actor from the use case model. | UC-03, UC-21 | HA-12, HO-08 | Hassan Almahdawi |
| E01 | AccountStatus | Enumeration | Account state used for lock-out and deactivation. | UC-02, UC-21 | HO-09 | Hasan Omar |
| E02 | Role | Enumeration | View a student account is currently using. | UC-05 | HO-10 | Hasan Omar |
| E03 | ApplicationStatus | Enumeration | Tutor application state. | UC-05, UC-20 | HO-11 | Hasan Omar |
| E04 | SortOption | Enumeration | Search sort order. | UC-08 | AR-10 | Abdul Raffay |
| E05 | BookingStatus | Enumeration | Booking lifecycle states, including session outcomes. | UC-11 – UC-14, UC-19 | MJ-05, HA-06 | Mohammed Jabsheh |
| E06 | DayOfWeek | Enumeration | Weekday of a recurring slot or filter. | UC-07, UC-16 | HA-13 | Hassan Almahdawi |

See `Integration_Notes.md` for why certain individual candidates are no longer separate classes.
