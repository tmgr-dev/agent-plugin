---
name: tmgr-supervision
description: Use when the user wants to run an agent in a sandbox, watch what it does, undo what it changed, or asks about checkpoints, restore points and rolling back an agent session. Experimental CLI feature.
---

# Supervising an agent

`tmgr run` starts an agent in a sandbox: its own home folder and only the environment it needs. With `--worktree` it works in a separate copy on its own branch, so two agents never write to the same files. With `--checkpoints` the folder is saved after every turn.

```
tmgr run --agent claude-code --worktree --checkpoints --name site-footer
```

Detach from the live view with Ctrl+], then D; the agent keeps working.

## Watch

- `tmgr agents`: sessions and states (working, waiting, blocked).
- `tmgr peek <session>`: current screen as text. `tmgr attach` is the interactive view for a human.
- `tmgr questions`: unanswered questions agents asked in `tmgr attach` sessions.

## Roll back

- `tmgr checkpoints list <session>`: each turn is a restore point.
- `tmgr checkpoints diff <session> <n>`: what changed in that step, or what a restore would change.
- `tmgr checkpoints restore <session> <n>`: puts the folder back. It asks for confirmation and saves the current state first, so the rollback can be undone. Restoring is the user's call: show the diff, then let them confirm.
- `tmgr halt <session>` stops the session (`--kill` if it will not stop).

## Related

Sessions, resume and the runner: tmgr-runner. Questions from agents to the owner: tmgr-decisions. Docs: https://tmgr.dev/docs/cli/ai-agents-under-supervision
