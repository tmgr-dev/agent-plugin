---
name: tmgr-shell-prompt
description: Use when the user wants the active TMGR task and timer in their shell prompt, tmux, Starship or the Claude Code status line.
---

# Task in the prompt

`tmgr init` prints a snippet; `--install` applies it.

```
tmgr init bash            # or zsh, fish, tmux, starship, claude
tmgr init bash --install  # shows the change, asks for confirmation, keeps a backup
```

Then reload the shell (for example `source ~/.bashrc`). The segment is read from a local state file with no server calls, so the prompt stays fast. `tmgr prompt` prints the segment and `tmgr statusline` prints output for other tools. With a task running the prompt shows its key and the timer; `tmgr stop` shows it as paused. `tmgr status` shows the same in full.

## Notes

- Print the snippet first (`tmgr init <target>` without `--install`) and let the user read it. Never pass `--yes` to `--install`. Editing their shell config is their decision.
- `tmgr init claude` is the Claude Code status line. Rate-limit data for it is a different thing (`tmgr usage statusline install`, tmgr-ai-cost); do not mix them up and do not overwrite an existing status line without asking.
- The timer in the prompt is the human's task timer (tmgr-time-tracking). An agent should start tasks with `--no-timer`.

Docs: https://tmgr.dev/docs/cli/your-task-in-the-shell-prompt
