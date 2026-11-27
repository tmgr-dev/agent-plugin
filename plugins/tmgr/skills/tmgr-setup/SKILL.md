---
name: tmgr-setup
description: Use when the user wants to connect an AI agent to TMGR, the tmgr MCP server is missing or fails ("401", "tool not found", no tmgr tools), or the tmgr CLI, hooks or Decisions inbox need installing. Covers token handling.
---

# Connect an agent to TMGR

## Rules for secrets

- Treat persona and smart device tokens as secrets. Have the operator provide them through the MCP client's environment or a secret manager. Keep token values out of chat, source files, task comments and logs.

## Cloud MCP for coding agents

1. Check the connected identity with `whoami`. On a persona connection, `get_persona` returns its instructions and skills.
2. In **Settings → Personas**, choose the persona, then **Agent connections → Connect an agent**. Choose its workspace and expiry. Inspect the grants returned by `whoami`. Reading task context pages needs `pages:read`, and updating a task needs `tasks:write`. If a required grant is missing, the operator can enable it for this persona in that workspace. The connection acts as this persona with its granted permissions in that workspace.
3. The operator supplies the issued token as `TMGR_PERSONA_TOKEN` in the environment that launches the client, then restarts it. The Claude plugin includes this HTTP server configuration. For manual Claude setup, a project `.mcp.json` can contain the same variable reference:

   ```json
   {"mcpServers":{"tmgr":{"type":"http","url":"https://api.tmgr.dev/mcp","headers":{"X-Persona-Token":"${TMGR_PERSONA_TOKEN}"}}}}
   ```

4. For Codex, put the following in `~/.codex/config.toml`:

   ```toml
   [mcp_servers.tmgr]
   url = "https://api.tmgr.dev/mcp"
   env_http_headers = { "X-Persona-Token" = "TMGR_PERSONA_TOKEN" }
   ```

   Cursor uses `${env:TMGR_PERSONA_TOKEN}` for the header value in `.cursor/mcp.json`. For self-hosted TMGR, use the installation's own HTTPS MCP URL.

## User-level smart device connection

Use this mode when the operator needs the agent to act as their user across their workspaces. Generate a smart device token under **Settings → Smart device token** and supply it as `TMGR_TOKEN`. In a manual MCP configuration use `X-Smart-Device-Token` as the sole auth header and reference that variable using the client's syntax above. Use one connection mode per server entry. An existing 0.2.x plugin keychain value is a device token. Issue a persona token for the new bundled configuration.

## Local `tmgr` CLI (optional, adds timers, Decisions, hooks)

- Check: `tmgr version` and `tmgr whoami`. Install and sign-in: `tmgr login` (device code, opens a browser). Update: `tmgr self-update`.
- Hooks (ask the user before running; they edit agent config):
  - `tmgr hook install claude` (or `codex`): reports agent sessions and commits to the running agent-work run.
  - `tmgr hook install decisions`: routes permission prompts and stop events to the Decisions inbox.
  - Preview any of them with `--print`; undo with `tmgr hook uninstall <target>`. `--project` edits only the current repo.
- Local stdio MCP (Decisions tools, phone notify/alarm): `claude mcp add tmgr-notify -- tmgr mcp`. Only add it when the binary exists (`command -v tmgr`).

## Verify

`whoami` returns the account; `list_workspaces` returns workspaces. If a tool answers "Agent work is disabled in workspace", that workspace turned agent reporting off; it is not a setup error.
