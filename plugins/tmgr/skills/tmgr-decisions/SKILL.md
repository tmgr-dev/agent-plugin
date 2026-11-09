---
name: tmgr-decisions
description: Use when you need the owner's decision, approval, review or check result before going on, when the work is blocked, or when you must notify the user's phone or raise an alarm. Covers the TMGR Decisions inbox (tmgr ask, ask_owner, get_answer) and notify/alarm.
---

# Asking the owner

The owner answers from the phone or the TMGR desktop. A question that needs a decision goes out as a Decisions card, not as a chat line they may not see.

## When to ask

- Hard-to-undo actions: deletes, force-push, schema changes, production config, releases.
- A real choice between options, or a missing fact only the owner has.
- A review or check the owner must do (`--kind review|release|check`).
- Do not ask what you can decide yourself, what a file or the workspace rules already answer, or anything involving a secret. Never put secrets in a card.

## Make a card

MCP tool `ask_owner`, or CLI:

```
tmgr ask --title "Ship 1.4 now?" --question "..." --option "Ship" --option "Wait" --recommended 1 \
  --context "short Markdown background" --task TM-512 [--kind decision] [--blocking]
```

- Title is a headline, question is one decision. 2 to 4 options, mark `--recommended`. Context is short Markdown in the owner's language.
- For a diff review add `--repo DIR --base REF --head REF` and `--pr URL`; add `--fact ok|bad|wait:TEXT` / `--check ok|bad|todo:TEXT` for status lines.
- In chat, write one line: what you asked and the card id.

## Read the answer

- `get_answer` with `waitSeconds` of 60 or less, repeated. Do not hold one long wait. `find_answers` or `tmgr decisions answers [--task TM-512]` looks up answers already given. `tmgr decisions pending-delivery` shows answers nobody picked up.
- Few cards. Every pending wait can mean a live `tmgr mcp` process; many long waits caused high CPU. Batch related questions into one card, and do not poll in a tight loop.
- Keep working on unblocked parts while a card is open. Without `--blocking`, do not stop.
- `reply_owner` answers a message the owner sent you.

## Phone

- `notify_user` / `tmgr notify "text" [--priority low|normal|high] [--link URL]`: a push. Use for "done" or "needs a look", at most a few per session.
- `alarm` / `tmgr alarm "what happened and what is needed"`: push, then a voice call if not acknowledged. Only for an outage or something that cannot wait. `alarm_status` / `tmgr alarm status` checks it; `--no-call` skips the call.
- Do not use either to report routine progress; that goes to `update_agent_work` and task comments.
