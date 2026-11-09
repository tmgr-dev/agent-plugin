# TMGR agent plugin

Skills and MCP configuration that teach AI coding agents to work with [TMGR](https://tmgr.dev): picking up tasks, reporting agent work, creating tasks, asking the owner through the Decisions inbox, and using pages.

## Skills

| Skill | Use when |
| :-- | :-- |
| `tmgr-setup` | connecting an agent to TMGR (MCP, token, CLI, hooks) |
| `tmgr-task-workflow` | working on, continuing or finishing a TMGR task; agent time vs human timer |
| `tmgr-create-tasks` | creating, splitting, relating or archiving tasks |
| `tmgr-decisions` | needing the owner's decision; phone notify and alarm |
| `tmgr-pages` | reading or writing pages and notes; Markdown sync |
| `tmgr-agent-teams` | orchestrator, lead and worker reporting; assigning a persona |
| `tmgr-runner` | `tmgr run`, agent sessions, the background runner |
| `tmgr-agent-queue` | approved tasks start on your machine and arrive as PRs |
| `tmgr-autopilot` | `tmgr autopilot`: backlog with agent teams, limits, pause and stop |
| `tmgr-supervision` | sandboxed agents, watching them, checkpoints and rollback |
| `tmgr-day-report` | what got done in a period; overdue and due-soon tasks |
| `tmgr-ai-cost` | `task_cost`, `tmgr usage`: tokens, cost, limits |
| `tmgr-time-tracking` | the human task timer vs agent time; time summaries |
| `tmgr-agent-work-reports` | reading who worked on a task, how long, commits, tests |
| `tmgr-personas` | personas, the shared skills library and its versions |
| `tmgr-graph` | what is connected, blocked, orphaned; paths between items |
| `tmgr-routines` | routines, recurring ones, done and skip |
| `tmgr-board` | statuses and their types, the board, the archive |
| `tmgr-workspace-modules` | turning modules on and off, presets |
| `tmgr-team` | members, invitations, roles, assignees |
| `tmgr-local-workspaces` | local (offline) workspaces and the CLI |
| `tmgr-plugin-authoring` | building TMGR desktop plugins |
| `tmgr-shell-prompt` | task and timer in the shell prompt, tmux, status line |
| `tmgr-troubleshooting` | 401, token scopes, signature errors, updating tmgr |

## Docs

- [AI agents](https://tmgr.dev/docs/agents): connect Claude Code, Codex, Cursor
- [Command line](https://tmgr.dev/docs/cli) and [troubleshooting](https://tmgr.dev/docs/cli/troubleshooting)
- [llms.txt](https://tmgr.dev/llms.txt): the docs index for agents

## Install (Claude Code)

```
/plugin marketplace add tmgr-dev/agent-plugin
/plugin install tmgr@tmgr
```

or from a local clone: `claude plugin marketplace add ./agent-plugin` then `claude plugin install tmgr@tmgr`.

On enable, Claude Code asks for the smart device token (TMGR web app: Settings, smart device token, Generate). It is stored in the OS keychain; change it with `claude plugin configure tmgr`. The plugin does not contain a token.

Try one session without installing: `claude --plugin-dir ./agent-plugin/plugins/tmgr`.

The plugin bundles only the cloud MCP server. The optional local `tmgr` CLI, its hooks and the stdio `tmgr mcp` server are set up by the `tmgr-setup` skill.

## Codex and Cursor

They do not read Claude plugins. Add the contents of [AGENTS.md](AGENTS.md) to your project's `AGENTS.md` and configure the MCP server as in `plugins/tmgr/skills/tmgr-setup/SKILL.md`.
