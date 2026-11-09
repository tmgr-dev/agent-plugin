---
name: tmgr-routines
description: Use when the user talks about routines, daily or recurring habits, reminders, or asks to add a routine, mark one done or skip an occurrence in TMGR.
---

# Routines

Routines are things repeated on a schedule: once, daily, weekly, monthly or yearly, with an optional time, category and a reminder (reminders work for repeating routines). They show on the Daily routines page and in week and month calendars.

## Tools

- `list_routines(workspaceId, page, perPage)`: compact rows (id, title, category, recurring, scheduled date and time); `hasMore` says if there is another page.
- `expand_routines(from, to)`: the occurrences in a date range (`YYYY-MM-DD`).
- `create_routine(title, description, workspaceId)`: a one-off routine.
- `create_recurring_routine(title, description, workspaceId)`: a recurring one. The tool takes only title and description; set the repeat, time and reminder in the app afterwards and tell the user so.
- `complete_routine(taskId, date)`: mark done for one date. `skip_instance(instanceId)`: skip one occurrence.
- CLI: `tmgr routine list [--date D]`, `tmgr routine done <id>`, and `tmgr today` includes routines.

Marking a routine done or skipping it changes the user's own record: do it when asked, and for the date they mean. Do not create routines as a way to remember things for yourself; use task comments or the Agent notes section (tmgr-pages).

Docs: https://tmgr.dev/docs/web/routines
