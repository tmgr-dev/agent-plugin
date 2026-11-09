---
name: tmgr-agent-teams
description: Use when you orchestrate or join a team of agents on TMGR work (orchestrator, lead, worker), spawn sub-agents, need parentSessionId or role on agent work, or must put an agent persona on a task. Not for a single agent reporting its own run (tmgr-task-workflow).
---

# Agent teams in TMGR

Each agent in a team reports its own run on the task, so the owner sees who did what and for how long. Tool names are plain; your client may prefix them with `mcp__<server>__`.

## Roles

- `orchestrator`: delegates the task to other agents. It opens its own run, keeps `update_agent_work` going while it waits, and finishes it at the end.
- `lead`: drives the work for a task and its workers.
- `worker`: does one slice for a lead.

Pass `role` to `start_agent_work`. A spawned agent also passes `parentSessionId` = the session id of whoever spawned it. Use `sessionId` only when you really know it; never invent one.

## Rules

- One run per agent and role on a task. A second run of the same agent with the same role ends the first one, so workers of one agent type on one task should not each start a run with an identical role unless the earlier one is meant to end.
- Every run needs its own heartbeat: `update_agent_work` after each commit and at least every 15 minutes, with all commits so far.
- A worker that fails or is stopped: `finish_agent_work` with `failed` or `cancelled` and a summary of what is left.
- The orchestrator finishes last, with the PR url and the combined result, then does `update_task` and `add_comment`.
- If a tool answers "Agent work is disabled in workspace", skip reporting there.

## Assigning a persona

A persona is a named agent identity. `list_assignable_personas` for the workspace, then `assign_persona(taskId, persona)` with the uuid or the exact name. This puts the task on the persona's queue and starts nothing. Assigning is a decision for the user: do it when asked, not on your own.

An agent connected with a persona token works inside one workspace with that persona's permissions and sees its own queue with `list_my_queue`.

## More

Persona and skills library: tmgr-personas. Fully local agent sessions: tmgr-runner. Docs: https://tmgr.dev/docs/agents
