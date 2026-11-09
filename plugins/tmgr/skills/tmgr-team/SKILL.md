---
name: tmgr-team
description: Use when the user asks who is in a TMGR workspace, to invite someone, about roles and what members can do, who a task should be assigned to, or what a team member has been working on.
---

# Team

## Read

- `list_members(workspaceId)` lists members. Assign tasks to people through the task tools with a member id from this list; personas are assigned with `assign_persona` (tmgr-personas).
- `time_summary(workspaceId, from, to, groupBy: "user")` shows tracked time per person. `search_tasks` / `list_tasks` filter by assignee. In the app, a member's page shows the period's tracked time, done tasks, comments and activity.

## Invite and roles

Invitations are sent in the app (List or Board: the + next to avatars, or Workspace settings, Invite), by email, to one or more addresses. The sender needs a verified email. An invitation works for one person and expires after 7 days; resend and revoke are in Workspace settings. Sending invitations to real people is the user's action: do not do it for them.

Two roles: the owner, and members. Both edit tasks and pages. Only the owner removes members, turns modules on or off for everyone (tmgr-workspace-modules) and deletes the workspace. Invitations are not available in a local workspace (tmgr-local-workspaces).

## Assigning

Do not assign a task to a person unasked. If a task is assigned to someone else or reserved in its comments, stop and ask the owner (tmgr-decisions).

Docs: https://tmgr.dev/docs/app/team
