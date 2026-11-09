# Discovery plan: how users find the agent plugin

Plan only. No code in other repos until the owner approves.

1. Settings, "MCP setup" block (task-manager-ui `src/pages/Settings.vue`): add a second line under the `claude mcp add` snippet: "Better: install the plugin" with `/plugin marketplace add <owner>/<repo>` and `/plugin install tmgr@tmgr`, plus a copy button and a link to the docs page. The token generated there is the one the plugin asks for.
2. Onboarding "Connect my AI agent" step (TM-478 S3, connect-agent dialog): after the token step show the same two plugin commands for Claude Code, and a copy-AGENTS.md button for Codex and Cursor.
3. `tmgr setup agent` (new CLI command): detects Claude Code, Codex and Cursor; runs `claude plugin marketplace add` and `install`, or appends the AGENTS.md snippet after a diff and confirmation; never writes a token itself (points to the keychain prompt or an env var). Optionally offered at the end of `tmgr login` and by `tmgr hook install`.
4. Docs page `/docs/mcp` (and `public/llms.txt`): "Skills for your AI agent" section with install steps and the skill list; link the raw SKILL.md files so agents without plugins can read them.
5. CLI README and release notes: one paragraph and the two commands; mention the plugin in the next changelog and in the tmgr-notify/MCP server `instructions` ("install the tmgr plugin for the full guide").

Also: list the repo in Claude plugin directories after the owner decides on public hosting and licence.
