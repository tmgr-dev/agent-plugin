---
name: tmgr-plugin-authoring
description: Use when the user wants to build, change or debug a TMGR desktop plugin (commands, sidebar views, status bar and tray items, board badges, task menu items), its manifest or permissions.
---

# Building a TMGR desktop plugin

Plugins extend the TMGR desktop app and run in a sandbox with only the permissions their manifest declares. This is about plugins for TMGR, not about this Claude Code plugin.

## Where the truth is

1. Call the MCP tool `plugin_authoring_guide`: preconditions, the scaffold, test, lint and try loop, the manifest, permission groups and rules.
2. Full guide and API reference (Markdown): https://tmgr.dev/docs/plugins.md
3. Types: https://tmgr.dev/docs/plugin-sdk/tmgr.d.ts (global `tmgr` in `main.js`), https://tmgr.dev/docs/plugin-sdk/window.d.ts (`window.tmgr` inside a plugin page).
4. Permissions list: https://tmgr.dev/docs/plugin-sdk/permissions.json
5. Template, test harness and examples: https://github.com/tmgr-dev/frontend/tree/master/plugin-sdk
6. Index of all agent docs: https://tmgr.dev/llms.txt

Fetch these rather than relying on memory; the API changes.

## Working rules

- Start from the template, not from scratch. Run its tests and lint before telling the user it works.
- Declare the minimum permissions. Every extra permission is shown to the user at install.
- Never put tokens or private data in a plugin or its manifest.
- Try it in the desktop app with the user's consent; do not install plugins in their app unasked.
