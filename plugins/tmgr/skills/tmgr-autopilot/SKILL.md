---
name: tmgr-autopilot
description: Use when the user wants to let `tmgr autopilot` work through a workspace backlog with agent teams, set its limits (teams, hours, tasks, cost, plan usage), check progress, or pause, resume and stop it. Experimental.
---

# tmgr autopilot

Autopilot reads the backlog, lists the tasks it can run, asks for one typed confirmation, then runs agent teams on this machine through the agent queue (tmgr-agent-queue; it needs a queue rule for a cloud workspace). Every task ends as a pull request; nothing is merged. Starting it is the owner's decision: prepare the command, let them confirm.

## Start

```
tmgr autopilot start --max-teams 2 --max-hours 4 [--rule NAME] [--dry-run] [--review]
```

- `--dry-run` plans and starts nothing; read it with `tmgr autopilot status`. Turn the queue's background loop off first.
- `--review` shows the full text of each task before signing. `--tasks`, `--only`, `--skip`, `--order` take comma-separated task keys.
- Limits: `--max-teams`, `--max-hours`, `--max-tasks`, `--max-cost USD` (only runs paid by an API key), `--usage-soft PCT` (no new tasks), `--usage-hard PCT` (running agents pause), `--no-usage-limit`. `none` removes a numeric limit.
- Usage limits and the cost cap need `tmgr usage consent allow`; without readable usage, no new task starts.

## Control

- `tmgr autopilot status [--watch]`, `tmgr autopilot log --tail 100`.
- `tmgr autopilot pause` stops new tasks; running ones finish. `resume` is refused inside an agent session, so the user runs it in a normal terminal. `stop` ends it and turns the queue off, or puts it back to its background loop if that was running before.

## If it does not start

"no queue rule for workspace": add a rule or pass `--rule`. A 403 mentioning `agent-approvals:write`: sign in again with the scopes command from the hint (tmgr-troubleshooting).

Docs: https://tmgr.dev/docs/cli/autopilot
