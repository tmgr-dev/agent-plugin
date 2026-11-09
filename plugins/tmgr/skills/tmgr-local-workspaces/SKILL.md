---
name: tmgr-local-workspaces
description: Use when the user works in a local (offline) TMGR workspace of the desktop app, wants the CLI to act on it, or asks what a local workspace cannot do compared with a cloud one.
---

# Local workspaces

A local workspace lives in the TMGR desktop app on the user's machine. No login and no network.

## CLI

Add `--ws local:<code>` to a command: `tmgr task list --ws local:<code>`, `tmgr add "Title" --ws local:<code>`, `tmgr agent start ... --ws local:<code>`. The data is under the desktop's workspaces folder (`$TMGR_LOCAL_ROOT` overrides it).

- When the desktop is signed in, the CLI acts as that user; otherwise as the desktop's local account. `tmgr config set local_user_id <id>` overrides which user.
- Agent runs can only be updated by the user who started them. Only personas of that user (or of the local account) can be assigned.
- `tmgr task confirm` lets agents run on a local task: it shows the full text and needs a terminal; the user runs it.
- `tmgr queue` runs tasks of local workspaces (and, with `runner allow`, cloud ones); see tmgr-agent-queue.

## Differences from cloud

- Task ids of a local and a cloud workspace are different spaces; never mix them.
- The cloud MCP server (`api.tmgr.dev/mcp`) does not see local workspaces. Use the CLI with `--ws local:<code>`. The stdio `tmgr mcp` only does notifications and the Decisions inbox, not tasks.
- Email invitations are not available in a local workspace (tmgr-team).
- A cloud token or workspace rule does not apply to local data.

Moving a local workspace to the cloud is done in the desktop app. Ask the user to do it there; do not copy data by hand through the API.

Docs: https://tmgr.dev/docs/app/team (invitations) and https://tmgr.dev/docs/cli
