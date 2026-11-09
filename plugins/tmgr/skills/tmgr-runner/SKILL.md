---
name: tmgr-runner
description: Use when the user wants to start an agent in a managed terminal session with `tmgr run`, list or watch sessions, type into a session, stop, resume or rename one, or restart the background runner. Experimental CLI feature; do not start sessions unless asked.
---

# tmgr run, sessions and the runner

The runner is a background process that owns agent sessions. `tmgr run` starts it when needed. All of these commands are experimental, and control is local only: the TMGR server never sends commands to the runner. Start nothing unless the user asked. `send`, `halt`, `rm` and `runner stop|restart` act on sessions the user may be watching: only when asked. Never use `--no-sandbox` or a bypass permission mode unasked.

## Start

```
tmgr run --agent claude-code --worktree --checkpoints --name site-footer
```

`--worktree` gives the agent its own copy of the project on its own branch. `--checkpoints` saves the folder after every turn (see tmgr-supervision). Run `tmgr run --help` for the rest.

## Sessions

Anywhere a session is needed, an id or a name works.

- `tmgr agents`: list sessions and states (`starting`, `working`, `waiting`, `blocked`, `exited`, `failed`).
- `tmgr peek <session> --lines 100`: current screen as plain text. Prefer this over `attach`, which is an interactive full-screen view for a human.
- `tmgr send <session> "text" [--wait idle|exit] [--timeout 5m]`: type a line. With `--wait idle` the exit code is 8 if the agent ended up blocked. The state is guessed from the screen.
- `tmgr rename`, `tmgr halt <session> [--kill]`, `tmgr rm <session>` (exited only).
- `tmgr resume <session> [--fork]`: continue an exited session; it asks for confirmation. `tmgr agents restore` offers to restart sessions a reboot stopped.
- `tmgr session list [--search "text"]`, `tmgr session summary|export <session>`: past conversations. Needs usage-log consent; export scans for secrets first.

## Runner

`tmgr runner status|start|stop|restart`. Stopping the runner does not stop sessions. After `tmgr self-update`, run `tmgr runner restart` (it also stops a running autopilot). `tmgr runner gc --dry-run` shows finished task copies that can be cleaned. `tmgr runner trust <dir>` and `install-service` ask for terminal confirmation: leave those to the user.

## Docs

https://tmgr.dev/docs/cli/runner and https://tmgr.dev/docs/cli/sessions
