# TutorBook components

## CO1 Web Interface

Presentation layer. Accepts input from students, peer tutors and administrators. Shows search results, booking status and validation reasons. Screens call the logic layer.

- Coverage: UC-01–UC-21 (screens)
- Provides: Human-facing screens
- Requires: IAccounts, IAdministration, IDiscovery, ICalendar, IBookings

## CO2 Accounts and Administration

Logic layer. Handles registration, login, password resets and role changes. Administrators review applications per course and deactivate accounts. Deactivation triggers cancellation of future bookings and a notice to affected users.

- Coverage: UC-01–05, UC-20–21
- Provides: IAccounts, IAdministration
- Requires: IBookingCleanup, INotifications, IRecords

## CO3 Tutor Discovery

Logic layer. Validates the course and search criteria, checks course approval and applies optional filters and sorting. Uses dated free slots for calendar-based filters and returns same-prefix alternatives for an empty search.

- Coverage: UC-06–10
- Provides: IDiscovery
- Requires: ICalendar, IRecords

## CO4 Scheduling and Booking

Logic layer. Expands weekly slots into a 14-day calendar, subtracts blocked and occupied times, and manages requests, responses, expiry, cancellations, rescheduling and session outcomes.

- Coverage: UC-11–19
- Provides: ICalendar, IBookings, IBookingCleanup
- Requires: INotifications, IRecords

## CO5 Notifications

Logic layer. Builds reset, booking and deactivation messages. Calls the external mail provider through the EmailService boundary.

- Coverage: UC-03, UC-11–14, UC-21
- Provides: INotifications
- Requires: EmailService

## CO6 Record Access

Data access layer. Loads and saves the D1 account and tutor records, D2 availability records and D3 bookings and history. Provides a transaction boundary shared by conflicting scheduling operations.

- Coverage: D1, D2 and D3
- Provides: IRecords
- Requires: None

## Interface contracts

IAccounts.updateProfile and switchView wrap Profile.update and Student.switchView. IRecords is a proposed Lab 8 storage contract. T denotes a stored record type, Predicate<T> a typed selection condition, and R the transaction result. Other contracts expose Lab 5 operations. Filtering and sorting run inside searchTutors. A system timer invokes BookingService.expirePendingBookings(now: DateTime): int internally.

### IAccounts

Provider: CO2 Accounts and Administration. Consumers: CO1 Web Interface.

```text
register(email: String, ausId: String, password: String): Student
login(email: String, password: String): User
requestPasswordReset(email: String): void
resetPassword(token: String, newPassword: String): boolean
submitTutorApplication(studentId: int, courseCode: String): TutorApplication
updateProfile(studentId: int, fullName: String, major: String, year: int, bio: String): void
switchView(studentId: int, role: Role): void
```

### IAdministration

Provider: CO2 Accounts and Administration. Consumers: CO1 Web Interface.

```text
listPendingApplications(): List<TutorApplication>
reviewApplication(adminId: int, applicationId: int, approve: boolean, reason: String): void
deactivateAccount(adminId: int, userId: int): int
```

### IDiscovery

Provider: CO3 Tutor Discovery. Consumers: CO1 Web Interface.

```text
searchTutors(criteria: SearchCriteria): List<TutorProfile>
viewTutorProfile(tutorProfileId: int): TutorProfile
suggestAlternativeCourses(courseCode: String): List<Course>
```

### ICalendar

Provider: CO4 Scheduling and Booking. Consumers: CO1 Web Interface, CO3 Tutor Discovery.

```text
getFreeOccurrences(tutorId: int, from: Date, days: int): List<SlotOccurrence>
addRecurringSlot(tutorId: int, day: DayOfWeek, start: Time, minutes: int, location: String): AvailabilitySlot
editRecurringSlot(slotId: int, day: DayOfWeek, start: Time, minutes: int, location: String): void
removeRecurringSlot(slotId: int): void
blockPeriod(tutorId: int, start: DateTime, end: DateTime, reason: String): BlockedPeriod
```

### IBookings

Provider: CO4 Scheduling and Booking. Consumers: CO1 Web Interface.

```text
requestBooking(studentId: int, slot: SlotOccurrence): Booking
validateSlot(studentId: int, slot: SlotOccurrence): ValidationResult
respondToRequest(tutorId: int, bookingId: String, accept: boolean): void
cancelBooking(studentId: int, bookingId: String): void
rescheduleBooking(studentId: int, bookingId: String, newSlot: SlotOccurrence): Booking
getDashboard(userId: int, upcoming: boolean): List<Booking>
recordOutcome(tutorId: int, bookingId: String, outcome: BookingStatus): void
```

### IBookingCleanup

Provider: CO4 Scheduling and Booking. Consumers: CO2 Accounts and Administration.

```text
cancelAllFutureBookings(userId: int): List<Booking>
```

### INotifications

Provider: CO5 Notifications. Consumers: CO2 Accounts and Administration, CO4 Scheduling and Booking.

```text
sendResetLink(user: User, token: String): void
notifyBookingRequest(booking: Booking): void
notifyBookingStatusChange(booking: Booking): void
notifyDeactivation(users: List<User>, cancelled: List<Booking>): void
```

### IRecords

Provider: CO6 Record Access. Consumers: CO2 Accounts and Administration, CO3 Tutor Discovery, CO4 Scheduling and Booking.

```text
find<T>(where: Predicate<T>): List<T>
save<T>(record: T): void
inTransaction<R>(work: () → R): R
```

### EmailService

Provider: External mail provider. Consumers: CO5 Notifications.

```text
sendEmail(to: String, subject: String, body: String): boolean
```

## Workflow checks

| Use case | Path through the architecture |
| --- | --- |
| UC-06 · FR-06 | Web Interface calls IDiscovery.searchTutors. Invalid criteria stop the search. For valid input, Tutor Discovery calls TutorProfile.isApprovedFor(course) for each candidate. Only approved tutors appear. |
| UC-11 · FR-11, FR-12, NFR-11 | Scheduling and Booking computes free occurrences and rechecks the tutor slot and the student’s confirmed sessions under one serializable transaction. Success writes a PENDING Booking and its first log entry, then notifies the tutor. A conflict returns its reason. |
| UC-12 · FR-13 | The assigned tutor can confirm or decline a PENDING request before the earlier of 24 hours after the request and the session start. The service records the change and notifies the student after commit. A late response is refused. The separate expiry sweep sets outstanding overdue requests to EXPIRED. |
| UC-14 · FR-15 | Rescheduling keeps the booking ID, obeys the three-hour student cutoff, revalidates the new slot for the same tutor, logs the change and returns the booking to PENDING. |
| UC-20/21 · FR-19/20 | Approval comes from the reviewed TutorApplication for that course. On deactivation, the admin service calls IBookingCleanup even for future sessions inside the student cutoff, then requests a deactivation notice. |
