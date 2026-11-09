---
name: tmgr-setup
description: Use when the user wants to connect an AI agent to TMGR, the tmgr MCP server is missing or fails ("401", "tool not found", no tmgr tools), or the tmgr CLI, hooks or Decisions inbox need installing. Covers token handling.
---

# Connect an agent to TMGR

## Rules for secrets

- The smart device token is a secret. Never ask the user to paste it into chat, never echo it, never write it into a tracked file, a task, a comment or a Decisions card.
- Give the user a place to put it themselves: the plugin prompt (below), a gitignored file such as `.env.local`, or their own shell profile.

## Cloud MCP (task tools)

1. Check first: call `whoami`. If it answers, the server is connected; stop.
2. Plugin install (preferred): the plugin ships the server. On enable, Claude Code asks for `tmgr_token` and stores it in the OS keychain. To set or change it later: `claude plugin configure tmgr`.
3. Token source: TMGR web app, Settings, "MCP setup" block, Generate. Self-hosted: use your own `/mcp` URL instead of `https://api.tmgr.dev/mcp`.
4. Without the plugin, the user runs this themselves (token from their own env var, not typed by you):
   `claude mcp add --transport http tmgr https://api.tmgr.dev/mcp --header "X-Smart-Device-Token: $TMGR_TOKEN"`
5. Codex (`~/.codex/config.toml`):
   ```toml
   [mcp_servers.tmgr]
   url = "https://api.tmgr.dev/mcp"
   env_http_headers = { "X-Smart-Device-Token" = "TMGR_TOKEN" }
   ```
   Cursor (`.cursor/mcp.json`): `{"mcpServers":{"tmgr":{"url":"https://api.tmgr.dev/mcp","headers":{"X-Smart-Device-Token":"${env:TMGR_TOKEN}"}}}}`
6. Rotate a leaked token by generating a new one in Settings and updating the stored value.
7. Server authenticates by header only (no OAuth), so claude.ai web connectors will not work.

## Local `tmgr` CLI (optional, adds timers, Decisions, hooks)

- Check: `tmgr version` and `tmgr whoami`. Install and sign-in: `tmgr login` (device code, opens a browser). Update: `tmgr self-update`.
- Hooks (ask the user before running; they edit agent config):
  - `tmgr hook install claude` (or `codex`): reports agent sessions and commits to the running agent-work run.
  - `tmgr hook install decisions`: routes permission prompts and stop events to the Decisions inbox.
  - Preview any of them with `--print`; undo with `tmgr hook uninstall <target>`. `--project` edits only the current repo.
- Local stdio MCP (Decisions tools, phone notify/alarm): `claude mcp add tmgr-notify -- tmgr mcp`. Only add it when the binary exists (`command -v tmgr`).

## Verify

`whoami` returns the account; `list_workspaces` returns workspaces. If a tool answers "Agent work is disabled in workspace", that workspace turned agent reporting off; it is not a setup error.
