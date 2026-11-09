---
name: tmgr-ai-cost
description: Use when the user asks what a task or their AI agents cost, how many tokens were used, how much of a rate limit is left, or about `task_cost` and `tmgr usage`.
---

# AI cost

Two sources, with different scope.

## Per task, from TMGR

`task_cost(taskId)` returns human timer time times the hourly rate, agent run time, and AI tokens and cost from usage that members synced. Money values are decimal strings. `totals` adds human and AI cost. The personal hourly rate is hidden from other members.

## Per machine, from local logs

`tmgr usage` reads the local logs of Claude Code and Codex. It needs consent first: `tmgr usage consent allow`. It keeps token counts, models, times and branches, never prompt text.

- `tmgr usage --week` (or other period flags, see `--help`), `--by day|project|branch|task`.
- `tmgr usage task TM-512`: cost, time, tokens and agent tree of one task. Task attribution works for agents started through `tmgr run` or `tmgr agent start`.
- `tmgr usage limits`: rate-limit windows, percent used, time to reset. For Claude Code it needs the status line hook (`tmgr usage statusline install` previews, `--install` applies).
- `tmgr usage sync`: upload per-task usage to TMGR, opt-in. That is what fills `task_cost`.

Costs are API list-price equivalents, not a subscription bill. Do not turn on consent or sync for the user; they are privacy choices.

Docs: https://tmgr.dev/docs/cli/what-ai-costs-you
