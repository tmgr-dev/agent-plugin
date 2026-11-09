---
name: tmgr-workspace-modules
description: Use when the user asks to turn TMGR features on or off for a workspace, apply a preset, hide a module, or a feature (board, pages, agent runs, routines) is missing from the menu or a tool says it is disabled.
---

# Workspace modules

Each workspace turns on only the parts of TMGR it needs. Modules are in Workspace settings, Modules, grouped into time and focus, planning, knowledge, AI agents, integrations and notifications. There are no MCP tools for this; it is done in the app.

- Preset: Apply a preset (for example Personal) shows a preview of what changes before anything is applied.
- One module: switch it on or off individually. Some depend on others (Board needs Workflow).
- Hide for me removes a module only for the current user.
- Only the workspace owner can turn modules on or off for everyone; a member can only hide one for themselves.

## When something looks missing

"Pages are disabled in this workspace" and "Agent work is disabled in workspace X" mean the module is off. These are not errors: skip pages or agent-work reporting there (use task comments instead). Do not ask to turn a module on just to make your own reporting easier. Agent runs and the agent queue need the Agent runs module (tmgr-agent-queue); statuses and the board need Workflow (tmgr-board).

Docs: https://tmgr.dev/docs/web/workspace-modules
