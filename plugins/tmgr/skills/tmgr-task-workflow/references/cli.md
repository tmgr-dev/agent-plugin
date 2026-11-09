# tmgr CLI cheat-sheet

Run `tmgr <command> --help` for the full flags. Add `--json` for machine output (schema tmgr.v1). `-y` accepts non-privileged confirmations. Some commands only run in a real terminal and ask you to type a confirmation; do not try to bypass that.

## References and workspaces

- `TM-512` (needs `--ws <code>` or a default set with `tmgr ws use <code>`), `#8974` / `8974` (global id). `tmgr help refs`.
- `--ws local:<code>`: a local workspace of the TMGR desktop app. No login, no network. Cloud and local task ids are different spaces.
- `tmgr ws list`, `tmgr whoami`, `tmgr status`.

## Tasks and the human timer

- `tmgr task list [-p CODE] [--status-type active]`, `tmgr task show TM-512 --comments 10`.
- `tmgr add "Title" [-p CODE] [-s STATUS] [--desc-file F]` (`-` reads title and description from stdin).
- `tmgr start TM-512` (branch, active status, human timer; `--no-timer` / `--no-branch`), `tmgr stop`, `tmgr switch TM-513`, `tmgr done [TM-512] [--comment T]` (stops the timer, moves to review, links the PR).
- These are the human's clock. An agent that only does the work uses `--no-timer`, or the agent-work commands below.

## Agent work (CLI form of start/update/finish_agent_work)

- `tmgr agent start TM-512 --agent claude-code --model <model> [--branch B]`
- `tmgr agent update [--run ID] --summary T --commit "sha subject" --pr URL --tests-passed N --tests-failed N --tests-cmd C` (also a heartbeat)
- `tmgr agent finish --status succeeded|failed|cancelled [same flags]`
- `tmgr log` lists runs of the workspace.

## Personas and the skills library

- Personas are named agent identities that can be assigned to tasks. MCP: `list_assignable_personas`, `assign_persona`, `unassign_persona`, `get_persona`, `get_persona_skill`.
- `tmgr skills list|show|put|delete|attach|detach`: a server-side library of skills attached to personas. Different from the plugin skills you are reading now. `tmgr skills put <slug> --file F.md` needs `slug:` in the front matter.

## Other

- Notes and pages: tmgr-pages skill. Decisions, notify, alarm: tmgr-decisions skill.
- `tmgr usage [--week] [--by task]`, `tmgr usage task TM-512`: local AI cost and tokens. Reading local agent logs needs consent (`tmgr usage consent`).
- Experimental: `tmgr runner`, `tmgr run`, `tmgr attach`, `tmgr autopilot`. Control is local only; the server never sends commands to the runner. Do not start these unless the user asks.
