# TutorBook - Exercise 5: Gantt Chart

![TutorBook 48-working-day Gantt chart](Gantt_Chart/Gantt_Chart.png)

- Source activities and durations: [`WBS.md`](WBS.md).
- Schedule starts at planning **day 1**, not a fixed calendar date; this avoids inventing an agreed start date.
- Horizontal bars represent the task's earliest-start scheduling window. Labels inside bars are durations.
- The scheduling model treats dependencies as finish-to-start and allows independent tasks in parallel.
- Orange bars show zero-slack activities; see [`Critical_Path.md`](Critical_Path.md).
- Exact earliest/latest calculations: [`Network_Schedule/CPM_Calculations.csv`](Network_Schedule/CPM_Calculations.csv).
- **Estimated completion:** End of working day **48**.

The Gantt chart was created with Matplotlib from the **same data table** used to construct the WBS and network diagram.
