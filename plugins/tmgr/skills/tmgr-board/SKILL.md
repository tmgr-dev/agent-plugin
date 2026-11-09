---
name: tmgr-board
description: Use when the user asks about statuses, the board or kanban columns, status types, creating or renaming a status, archiving finished tasks, or why a task is missing from the board or list.
---

# Statuses, board and archive

Statuses belong to the workspace. The TYPE matters, not the name:

- `default`: the backlog; new tasks start here; only one per workspace, cannot be deleted.
- `active`: work in progress.
- `completed`: finished work, counted as done.
- `hidden`: parked tasks, in their own board column but left out of the list status filter.
- `archived`: no board column, not in the current list; found on the Archive page.

Statuses and the board belong to the Workflow module (the Board module needs Workflow). With Workflow off there is a Done checkbox and no board; statuses are kept and return when it is turned on.

## Tools

- `list_statuses(workspaceId)`: ids, names, types. Pick by type, never by remembered name or id.
- `list_tasks_by_status`: filter by type or id.
- `create_status(workspaceId, name, color)` and `update_status(statusId, name, color)` take a name and a hex color only. They cannot set the type; the type is chosen in the board UI (Filters, Add status, or a column's Edit status). Tell the user when a type has to be set.
- `update_task` with a status id moves a task.
- CLI: `tmgr board` (full-screen kanban), `tmgr task list --status-type active`.

## Gotchas

- Deleting a status moves its tasks to the default status. Moving all tasks of a column and "Archive all" are bulk actions: ask first.
- "Archive all" needs a status of type `archived` to exist; create it first.
- To bring an archived task back, set any other status.

Docs: https://tmgr.dev/docs/app/statuses-and-board
