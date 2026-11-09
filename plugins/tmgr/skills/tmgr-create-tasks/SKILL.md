---
name: tmgr-create-tasks
description: Use when the user asks to create, split, rename, move, relate or archive TMGR tasks, or to put follow-ups and findings into the TMGR backlog.
---

# Creating and editing TMGR tasks

1. `list_workspaces` for the workspace id and code. Statuses are per workspace: `list_statuses` returns id, name and TYPE (`default` = backlog, `active`, `completed`, `hidden`, `archived`).
2. Categories (projects): `tmgr_request` with `GET /api/project_categories?all` gives id, code, settings. Pick the category the work belongs to; ask if unclear.
3. `create_task` with `projectCategoryId` and `statusId` (the `default` type status unless told otherwise). The server does not choose a status for you.
4. Title: pass it WITHOUT a prefix. A category may add `TM-157: ` itself from its name pattern. When renaming with `update_task`, keep the existing prefix; titles are stored verbatim.
5. Description: goal, context, acceptance criteria, links. Small and checkable. One task per outcome; do not bundle.
6. Dedupe first: `search_tasks` with two or three keywords before creating a follow-up.
7. Relations: `tmgr_request` `POST /api/tasks/{id}/related-to/{otherId}/with/{relationTypeId}`; types from `GET /api/task-relation-types`.
8. Archive: `update_task` with the status whose type is `archived`. Deleting (`delete_task`) only when the user asked for it by name.
9. `update_task` changes only the fields you pass. Lists (`list_tasks`, `search_tasks`, `list_comments`) are paged: while `hasMore` is true, call again with `page + 1`.
10. Report links using each task's `url` field.

Do not assign a persona or another person unless asked; see `list_assignable_personas` and `assign_persona` when the user requests it.
