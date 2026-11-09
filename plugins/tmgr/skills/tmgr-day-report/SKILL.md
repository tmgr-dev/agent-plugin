---
name: tmgr-day-report
description: Use when the user asks what got done today, yesterday, this week or in a period, for a standup, summary or report of tasks, agent work and commits, or which tasks are overdue, due soon, unassigned or stale (deadline report).
---

# Reports: what got done, what is due

Build the report from TMGR data, not from memory. Use the workspace of the question (`list_workspaces`, `workspace_context`).

## What got done

1. `tmgr today [--yesterday | --date YYYY-MM-DD] [--mine]` (CLI) shows tracked time, agent time and routines for a day.
2. `list_tasks_by_status` with status type `completed`, or `search_tasks`, for tasks finished in the period; check dates on each task before listing it as done in the period.
3. `list_agent_work(taskId)` for the runs on those tasks: agent, duration, commits, tests, summary. CLI: `tmgr log --since 1d [--task REF] [--agent NAME]`.
4. `time_summary(workspaceId, from, to, groupBy)` for human time, grouped by `task`, `category` or `user`. A task counts in the range when it was last updated inside it.

Keep human time and agent time apart; they are different clocks (tmgr-time-tracking).

## Deadlines

`deadline_report(workspaceId, dueSoonDays, staleDays)` returns overdue, due-soon, unassigned, unestimated and stale open tasks. Defaults: 7 days ahead, 14 days stale. Report overdue first, with the task link from the `url` field.

## Shape of the answer

Short groups: Done, In progress, Blocked or overdue, Agent work. One line per item: key, title, link, one fact (PR, commits, time). Do not invent tasks or hours; say when a source returned nothing or agent work is disabled in the workspace.

Docs: https://tmgr.dev/docs/cli/agent-work-reports
