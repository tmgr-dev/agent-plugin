---
name: tmgr-time-tracking
description: Use when the user asks to track, start or stop time on a task, see tracked time or time per task, category or person, or asks why agent time is not in the task timer.
---

# Time tracking

Two separate clocks:

- Task timer: the HUMAN's own time. MCP `start_task_timer` / `stop_task_timer`; CLI `tmgr start`, `tmgr stop`, `tmgr switch`, `tmgr done`. `startTime > 0` on a task means a timer is running.
- Agent work: the agent's time, reported with `start_agent_work` / `finish_agent_work` (tmgr-task-workflow). `list_agent_work(taskId)` shows agent time next to the timer time.

## Rules

- Never start or stop the task timer for your own work. Use the timer tools only when the user asks to track their time.
- An agent running `tmgr start` uses `--no-timer` (and `--no-branch` if needed).
- Starting a timer on a backlog task may offer a move to an active status; that is a status change, so follow the workspace rules.

## Reading time

- `time_summary(workspaceId, from, to, groupBy)`: dates `YYYY-MM-DD`, `groupBy` `task`, `category` or `user`, includes running timers. A task is counted in the range when it was last updated inside it, so a long task can appear in a period where little work happened.
- CLI: `tmgr today [--date D]`, `tmgr status` (active task and today's time).
- `tmgr time` is something else: time spent inside `tmgr attach`, and whether it is sent to bound tasks (`tmgr time sync`).

Cost of the time: tmgr-ai-cost. Docs: https://tmgr.dev/docs/cli/the-start-done-cycle
