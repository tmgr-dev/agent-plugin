---
name: tmgr-agent-work-reports
description: Use when the user asks which agent worked on a task, for how long, with which commits, PR and tests, or wants to read, audit or follow agent work reports.
---

# Reading agent work reports

An agent work run records one agent on one task: agent, model, role, branch, start and end, duration, summary, PR url, commits, tests, checks, releases and deploy.

## Read

- One task: `list_agent_work(taskId)`, newest first, with total agent time next to the timer time. `get_task` and `graph_related` (tmgr-graph) show runs next to the rest of the task.
- Whole workspace (CLI): `tmgr log [--task REF] [--since 2h|1d] [--agent claude-code] [--follow]`, `--json` for scripts.
- If it answers "Agent work is disabled in workspace", the owner turned it off there; say so.

## Interpreting

- `status`: `running`, `succeeded`, `failed`, `cancelled`. A run with no update for 45 minutes is marked abandoned; its agent may still resume it with the same run id.
- Roles and `parentSessionId` show who spawned whom (tmgr-agent-teams).
- Trust commits and tests that are in the run; do not assume work happened that the run does not show. Check the PR if it matters.
- Agent time and human timer time are separate; do not add them up unless asked (tmgr-time-tracking).

## Writing

Reporting your own run: tmgr-task-workflow. CLI hooks that notify and link commits: `tmgr hook install claude|codex` (asks for confirmation).

Docs: https://tmgr.dev/docs/cli/agent-work-reports
