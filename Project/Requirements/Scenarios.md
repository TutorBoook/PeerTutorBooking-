# TutorBook Scenarios

TutorBook connects AUS students with approved peer tutors. Payments, video calls, AI tutoring, university registration-system integration, and native mobile apps are outside the project scope.

| ID | Scenario | Actor | Description |
|---|---|---|---|
| S-01 | First-time registration and profile setup | Student | Sara tries to register with a personal Gmail address, which TutorBook rejects. She registers with `b00101234@aus.edu` and AUS ID `b00101234`, logs in, and adds her major, academic year, courses of interest, and biography. |
| S-02 | Searching for a tutor and requesting a session | Student | Omar searches for `CMP 305`, filters for Tuesday 14:00–17:00 at the Library, sorts by earliest available slot, and checks Layla's profile and 14-day calendar. He requests Tuesday 15:00–16:00; booking `BK-1042` is created as Pending. |
| S-03 | Tutor sets up weekly availability | Tutor | Layla creates recurring 60-minute slots on Sunday, Tuesday, and Thursday from 15:00–17:00 in Library Room L-204. She blocks 12–16 October for midterms without deleting the recurring pattern. |
| S-04 | Tutor handles requests and records outcomes | Tutor | Layla confirms `BK-1042`, declines a conflicting request, and leaves a third request unanswered until it expires. After the sessions, she records one as Completed and another as No-show. |
| S-05 | Student reschedules and attempts a late cancellation | Student | Omar moves `BK-1042` to Thursday 16:00. The booking keeps its ID, returns to Pending, and the change is logged. When he later tries to cancel another session only two hours before it starts, the system rejects the late cancellation. |
| S-06 | Administrator reviews applications and deactivates an account | Administrator | An administrator approves Khalid to tutor MTH 203, rejects his COE 420 application with a written reason, and deactivates an account reported for repeated no-shows. Its future bookings are cancelled and affected users are emailed. |
| S-07 | Two students try to book the same slot | Student | Two students request Layla's Sunday 15:00 slot at almost the same time. Exactly one booking is recorded. The other student sees that the slot was just booked and is returned to the updated calendar. |
