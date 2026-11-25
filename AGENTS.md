## TMGR (task manager) for coding agents

This project tracks work in TMGR (https://tmgr.dev). When the user mentions a task (TM-123, #1234 or a tmgr.dev link):

1. Connect: the `tmgr` MCP server (Streamable HTTP, `https://api.tmgr.dev/mcp`, header `X-Smart-Device-Token` from the env var `TMGR_TOKEN`). Never print, store or commit the token. Check with `whoami`.
2. Before working: `workspace_context` and `pages_for_task`; follow the workspace rules. Statuses differ per workspace: choose by type via `list_statuses`.
3. Report your work: `update_task` to a status of type `active` and `start_agent_work` (agent "codex" or "cursor", with `role`, model, branch, `sessionId`/`parentSessionId` when known) when you begin, `update_agent_work` after each commit and every 15 minutes, `finish_agent_work` when done, then `update_task` and `add_comment` (what changed, where). Do not use `start_task_timer`; it is the human's clock.
4. Need a decision from the owner: ask once with `tmgr ask` (CLI) or `ask_owner` (only exists on the local `tmgr mcp` stdio server), 2 to 4 options with a recommendation; read the answer with `get_answer` or `tmgr decisions answers`, `waitSeconds` 60 or less.
5. You may create and edit context pages in your own workspace, except sections owned by someone else and system sections. What you write reaches every agent's `workspace_context`: write only workspace-wide rules, durable facts go in "Agent notes".
6. If a tool says "Agent work is disabled in workspace", skip step 3 for that workspace.

Detailed guides (raw files): `plugins/tmgr/skills/*/SKILL.md` in the TMGR agent plugin repo.
