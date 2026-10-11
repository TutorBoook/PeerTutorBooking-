# TutorBook - Exercise 4: Work Breakdown Structure (WBS)

**Project:** TutorBook Peer-Tutoring Booking System  
**Development approach:** Incremental model (existing project process model)  
**Estimate basis:** 4-person team; working-day durations; multiple tasks may run in parallel.  
**Status:** Proposed project plan for Lab 4, **not** a record of actual implementation dates or commits.

The activities implement TutorBook's real system scope: account management, approved tutor searching, availability, Pending requests, tutor decisions, session changes and administrator actions. Online payments, native applications and video tutoring are excluded.

## Work packages

| ID | Task name | Description | Predecessor(s) | Duration (days) |
| --- | --- | --- | --- | --- |
| T1 | Refine requirements and architecture | Confirm Lab 1-3 scope, FR/NFR traceability, three-layer module boundaries and acceptance criteria. | — | 3 |
| T2 | Design SQL data model | Define accounts, per-course tutor approvals, recurring slots, blocked dates, bookings and status history. | T1 | 4 |
| T3 | Design interfaces and navigation | Prototype student search/booking, tutor availability/dashboard, admin review and keyboard-accessible layouts. | T1 | 4 |
| T4 | Set up application and automation | Create presentation, business-logic and data-access skeleton; configure local SQL setup and CI test workflow. | T1 | 3 |
| T5 | Build account and access functions | Implement AUS email and ID checks, login, reset link, profile basics and protected role access. | T2, T4 | 6 |
| T6 | Build tutor application and approval | Handle course-specific tutor applications, approval/rejection and same-account role switching. | T5 | 5 |
| T7 | Build tutor availability management | Create 30/60-minute weekly slots with locations and date/time blocking without deleting recurrence. | T2, T4 | 6 |
| T8 | Build tutor search and calendar | Implement approved-course search, filters/sorting, fallback suggestions and 14-day availability view. | T3, T6, T7 | 6 |
| T9 | Build safe booking creation | Create Pending bookings; validate free slots and student overlap; enforce one winner for concurrent slot requests. | T5, T7 | 7 |
| T10 | Build tutor booking decisions | Handle confirm/decline responses, status changes and automatic Pending expiry. | T9 | 5 |
| T11 | Build session dashboards and outcomes | Show current/past appointments and enable tutors to record Completed or No-show. | T10, T6 | 5 |
| T12 | Build cancellation and rescheduling | Enforce three-hour student cutoff, release slots, retain IDs and re-request tutor confirmation. | T10, T7 | 6 |
| T13 | Build admin deactivation workflows | Deactivate accounts; cancel future bookings and prepare affected-user notifications. | T6, T10 | 4 |
| T14 | Integrate all six user-facing processes | Connect interfaces, APIs, SQL transactions and transitions across accounts, search, booking and admin modules. | T8, T11, T12, T13 | 4 |
| T15 | Run functional and security testing | Test requirements, status rules, atomic double-booking, role authorization and automated module coverage. | T14 | 6 |
| T16 | Run UX and nonfunctional checks | Check search latency, 14-day calendar, browser/mobile UI, keyboard access and recovery behavior. | T15 | 4 |
| T17 | Prepare deployment and handoff | Document SQL setup, HTTPS, backup/restore procedure, smoke test and repeatable local setup in README guidance. | T16 | 3 |

**Total project length with parallel dependencies:** 48 working days (not the sum of all task durations).

## Scheduling assumptions

- Every dependency is finish-to-start; each task can begin only when **all** listed predecessors have finished.
- Day 1 is the first planned working day, since the team has not supplied a calendar start date.
- The estimates are illustrative team-planning values to validate and approve before committing.
- Features use existing requirements FR-01 through FR-20; acceptance testing also covers NFR-01 through NFR-20.
- The final integration and verification phases require completed modules, and parallel work is possible during development.
- Expected time **E** in the task network equals the WBS single-point task duration (this assignment does not supply PERT three-point estimates).

## Requirements traceability

| Activities | Relevant requirements / use cases |
|---|---|
| T1-T4 | Project scope, incremental process model, NFR-05, NFR-18 |
| T5-T6 | FR-01 to FR-05, FR-19; UC-01 to UC-05, UC-20 |
| T7-T8 | FR-06 to FR-10, FR-16, FR-17; UC-06 to UC-10, UC-16, UC-17 |
| T9-T10 | FR-11 to FR-13; UC-11, UC-12, UC-15; NFR-11 |
| T11-T13 | FR-14, FR-15, FR-18, FR-20; UC-13, UC-14, UC-18, UC-19, UC-21 |
| T14-T17 | Integration; NFR-01 to NFR-20, release preparation |
