---
name: tmgr-troubleshooting
description: Use when a TMGR call fails with 401, "session expired", "this login does not allow that (needs scope ...)", a signature or self-update error, a credential store error, or tmgr itself needs updating.
---

# TMGR troubleshooting

The full list is at https://tmgr.dev/docs/cli/troubleshooting. Do not paste tokens into chat while debugging.

## Sign-in

- `tmgr whoami` shows who is signed in. "not logged in", "session expired or revoked", "stored token is malformed": the user runs `tmgr login` (`--no-browser` if no browser; sign out first with `tmgr logout` to start clean).
- "this login does not allow that (needs scope ...)": the sign-in lacks a permission. The hint prints a `tmgr login --scopes ...` command with the scope added; the user runs it and approves in the browser. This also covers `agent-approvals:write` (autopilot, tmgr-autopilot).
- Keychain refused or missing: `TMGR_CREDENTIAL_STORE=file tmgr login` stores the token in a private file (mode 0600). A readable-by-others file is refused; run the `chmod 600` hint.

## MCP 401

The cloud MCP uses the smart device token from the plugin configuration or the `TMGR_TOKEN` environment variable. 401 means the token is missing, revoked or the header is not set. Regenerate it in the web app and reconfigure (tmgr-setup). A persona token only works in its own workspace.

## Updating tmgr

`tmgr self-update --check`, then `tmgr self-update` (`--channel beta` for beta). After updating, `tmgr runner restart` if the runner is used.

- Signature or checksum failures: nothing is installed and the current tmgr keeps working. Do not work around them; retry later or reinstall with the install script.
- "managed by ...": update with the package manager command shown. "no permission to write the install directory": tmgr never uses sudo; reinstall to a folder the user owns.
- "refusing to downgrade": only the user may override, with `--allow-downgrade` in a terminal.

## Server errors

HTTP 502 or "server unavailable": retry in a moment. "rate limited": wait a minute.
