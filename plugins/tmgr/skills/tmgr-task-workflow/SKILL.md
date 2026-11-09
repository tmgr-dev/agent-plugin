---
name: tmgr-task-workflow
description: Use when the user asks to work on, pick up, continue or finish a TMGR task (TM-123, #8974, a tmgr.dev/.../tasks/N link), or to report agent work, track time on a task, or comment on a task. Not for creating new tasks (tmgr-create-tasks) or pages (tmgr-pages).
---

# Working a TMGR task

The TMGR MCP server sends its own WORKFLOW rules on connect (order of calls, 15-minute updates, finish order). Follow them; they are authoritative. This skill adds what they leave out. Tool names are plain (`start_agent_work`); your client may show them with an `mcp__<server>__` prefix. With only the CLI, use the equivalents in `references/cli.md`.

## Before you start

1. Resolve the task: id from a link, or `search_tasks` / `get_task`. References: `TM-512` (category key, needs the workspace), `#8974` or `8974` (global id). Always link to the task with the `url` field of the response, never a hand-built URL.
2. Call `workspace_context` for the task's workspace, then `pages_for_task`. They hold the team rules (branches, releases, what not to touch). Obey them over your defaults. If they answer "Pages are disabled", there are none.
3. Statuses are per workspace and names differ. Get ids from `list_statuses`; pick by TYPE (`active`, `completed`, `archived`), never by a remembered name.
4. If the task has an assignee or persona that is not you, or the comments say it is reserved, stop and ask the owner (see tmgr-decisions).

## Agent time vs human time

- Your work is reported with `start_agent_work` / `update_agent_work` / `finish_agent_work`. Pass `role` (`orchestrator`, `lead`, `worker`), `model`, `branch`, and `parentSessionId` when another session spawned you.
- Never use `start_task_timer` / `stop_task_timer` for yourself. Those are the human's clock; use them only when the user asks to track their time.
- If your run was marked abandoned, keep using the same run id; do not start a second run.
- Pausing or handing back: `finish_agent_work` with `cancelled` or `failed` and a summary that says what is left. Do not leave a run open.
- "Agent work is disabled in workspace X": skip reporting there. Not an error.

## While working

- Send commits as `<real sha> <subject>`; `update_agent_work` replaces the whole list, so always send all commits of the run.
- Put test results in `testsPassed` / `testsFailed` / `testsCommand`, other checks in `checks`.
- Do not paste secrets, tokens or env dumps into comments, summaries or descriptions.

## Finishing

1. `finish_agent_work` (succeeded) with summary, PR url, commits, tests.
2. `update_task` to the review or completed status of that workspace; follow the workspace rules on which one (many teams want Review until the owner confirms).
3. `add_comment`: what changed, where (commit, PR, deploy tag), what was verified, what is left. Plain text, links from `url`.
4. Record durable knowledge for the next agent only in the "Agent notes" section of a context page (see tmgr-pages).

## Descriptions and comments

Write for a reader who has not seen the chat: goal, what changed, how verified. Keep it short. Match the language the task is written in unless the workspace rules say otherwise.

## Related

CLI cheat-sheet (timers, `tmgr start/done`, `--ws local:<code>`, personas and the skills library): `references/cli.md`.
