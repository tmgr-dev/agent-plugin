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
