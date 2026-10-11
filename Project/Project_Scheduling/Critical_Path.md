# TutorBook - Exercise 7: Critical Path and Verification

## Critical path

**T1 → T2 → T5 → T9 → T10 → T12 → T14 → T15 → T16 → T17**

## Expected project duration

**48 working days** (assuming the estimated task durations and finish-to-start dependencies in the WBS).

## Calculation

| Critical activity | Duration (days) | ES | EF | Slack |
|---|---:|---:|---:|---:|
| T1 — Refine requirements and architecture | 3 | 0 | 3 | 0 |
| T2 — Design SQL data model | 4 | 3 | 7 | 0 |
| T5 — Build account and access functions | 6 | 7 | 13 | 0 |
| T9 — Build safe booking creation | 7 | 13 | 20 | 0 |
| T10 — Build tutor booking decisions | 5 | 20 | 25 | 0 |
| T12 — Build cancellation and rescheduling | 6 | 25 | 31 | 0 |
| T14 — Integrate all six user-facing processes | 4 | 31 | 35 | 0 |
| T15 — Run functional and security testing | 6 | 35 | 41 | 0 |
| T16 — Run UX and nonfunctional checks | 4 | 41 | 45 | 0 |
| T17 — Prepare deployment and handoff | 3 | 45 | 48 | 0 |

Sum of the critical-task durations = 3 + 4 + 6 + 7 + 5 + 6 + 4 + 6 + 4 + 3 = **48 days**.

## Why this is the critical path

Each critical task has **zero slack**: any delay to one of these activities (without an offsetting schedule change) pushes the planned finish beyond working day 48. By contrast, activities such as T3, T6, T8, T11 and T13 have positive slack. Critical branches meet at T9: T5 and T7 both finish at day 13, so **both T5 and T7 lie on critical paths**. The path written above is **one** valid critical path; the set of all zero-slack branches must be considered for delay control.

## Independent tool verification

A second analysis using **NetworkX** on a directed acyclic activity graph calculated the longest start-to-finish path duration as **48 days**, matching the manual forward/backward pass. Graphviz rendered the node network, and Matplotlib rendered the Gantt chart. Calculations and dependencies are also supplied as a CSV.

> Note: Multiple critical paths exist if there are parallel zero-slack branches with equal completion times. The network diagram highlights **all zero-slack tasks**, not only the single path stated above.

## Practical validity note

These are **planning estimates**, not observed task durations. The team should confirm the 4-person parallel-work assumption, actual course deadline and workday calendar with the instructor before describing this as a committed delivery schedule.
