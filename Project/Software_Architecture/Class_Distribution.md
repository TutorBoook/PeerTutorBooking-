# Lab 5 class distribution

Record Access owns the persistent class definitions. The logic components load those objects and call their Lab 5 methods. For example, Booking.confirm() still belongs to Booking. Web Interface has no Lab 5 classifier because Lab 5 modeled services, domain objects and the mail boundary. EmailService is the contract owned by Notifications and implemented by the external provider.

| ID | Component | Responsibilities | Included classifiers |
| --- | --- | --- | --- |
| CO1 | Web Interface | Accepts input from students, peer tutors and administrators. Shows search results, booking status and validation reasons. Screens call the logic layer. | None (presentation screens) |
| CO2 | Accounts and Administration | Handles registration, login, password resets and role changes. Administrators review applications per course and deactivate accounts. Deactivation triggers cancellation of future bookings and a notice to affected users. | C07 AccountService, C24 AdminService |
| CO3 | Tutor Discovery | Validates the course and search criteria, checks course approval and applies optional filters and sorting. Uses dated free slots for calendar-based filters and returns same-prefix alternatives for an empty search. | C10 SearchCriteria, C11 SearchFilter, C12 DayOfWeekFilter, C13 TimeRangeFilter, C14 LocationFilter, C15 TutorSearchService, E04 SortOption |
| CO4 | Scheduling and Booking | Expands weekly slots into a 14-day calendar, subtracts blocked and occupied times, and manages requests, responses, expiry, cancellations, rescheduling and session outcomes. | C18 BookingService, C19 ValidationResult, C22 SlotOccurrence, C23 AvailabilityService, E05 BookingStatus, E06 DayOfWeek |
| CO5 | Notifications | Builds reset, booking and deactivation messages. Calls the external mail provider through the EmailService boundary. | C25 NotificationService, C26 EmailService |
| CO6 | Record Access | Loads and saves the D1 account and tutor records, D2 availability records and D3 bookings and history. Provides a transaction boundary shared by conflicting scheduling operations. | C01 User, C02 Student, C03 Administrator, C04 Profile, C05 PasswordResetToken, C06 TutorApplication, C08 Course, C09 TutorProfile, C16 Booking, C17 BookingChangeLog, C20 AvailabilitySlot, C21 BlockedPeriod, E01 AccountStatus, E02 Role, E03 ApplicationStatus |

| Lab 5 ID | Classifier | UML type | Primary component |
| --- | --- | --- | --- |
| C01 | User | abstract class | CO6 Record Access |
| C02 | Student | class | CO6 Record Access |
| C03 | Administrator | class | CO6 Record Access |
| C04 | Profile | class | CO6 Record Access |
| C05 | PasswordResetToken | class | CO6 Record Access |
| C06 | TutorApplication | class | CO6 Record Access |
| C07 | AccountService | control | CO2 Accounts and Administration |
| C08 | Course | class | CO6 Record Access |
| C09 | TutorProfile | class | CO6 Record Access |
| C10 | SearchCriteria | class | CO3 Tutor Discovery |
| C11 | SearchFilter | abstract class | CO3 Tutor Discovery |
| C12 | DayOfWeekFilter | class | CO3 Tutor Discovery |
| C13 | TimeRangeFilter | class | CO3 Tutor Discovery |
| C14 | LocationFilter | class | CO3 Tutor Discovery |
| C15 | TutorSearchService | control | CO3 Tutor Discovery |
| C16 | Booking | class | CO6 Record Access |
| C17 | BookingChangeLog | class | CO6 Record Access |
| C18 | BookingService | control | CO4 Scheduling and Booking |
| C19 | ValidationResult | dataType | CO4 Scheduling and Booking |
| C20 | AvailabilitySlot | class | CO6 Record Access |
| C21 | BlockedPeriod | class | CO6 Record Access |
| C22 | SlotOccurrence | dataType | CO4 Scheduling and Booking |
| C23 | AvailabilityService | control | CO4 Scheduling and Booking |
| C24 | AdminService | control | CO2 Accounts and Administration |
| C25 | NotificationService | control | CO5 Notifications |
| C26 | EmailService | interface | CO5 Notifications |
| E01 | AccountStatus | enumeration | CO6 Record Access |
| E02 | Role | enumeration | CO6 Record Access |
| E03 | ApplicationStatus | enumeration | CO6 Record Access |
| E04 | SortOption | enumeration | CO3 Tutor Discovery |
| E05 | BookingStatus | enumeration | CO4 Scheduling and Booking |
| E06 | DayOfWeek | enumeration | CO4 Scheduling and Booking |

The 26 C-series classifiers and six enumerations each have one primary component. SlotOccurrence is computed. Tutor is a Student role and each session remains a Booking.
