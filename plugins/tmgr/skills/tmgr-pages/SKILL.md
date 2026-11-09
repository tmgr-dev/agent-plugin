---
name: tmgr-pages
description: Use when reading or writing TMGR pages (workspace docs, context pages, notes, specs), syncing pages with Markdown files, or saving a note, plan or finding for the team or the next agent session.
---

# TMGR pages

Pages are the workspace's shared memory (rules, architecture, notes) and can be linked to tasks. If a tool answers "Pages are disabled in this workspace", there are none; use task comments instead.

## Reading

- `workspace_context` returns all context pages as one Markdown document. Read it before working.
- `pages_for_task` returns pages linked to a task. `pages_search`, `pages_tree`, `pages_get` find and read the rest.

## Writing

- Context pages belong to the owner. You may write ONLY the section "Agent notes" (section id `agent-notes`): `pages_append` without a heading, or `pages_set_section` with `sectionId` `agent-notes`. Never edit another section.
- Put in Agent notes only durable facts the next agent needs: what shipped and where, a hold or gate, a gotcha, an open decision. Date each entry. No secrets, no chat narration, no progress logs (those go to agent-work updates).
- Your own pages (specs, plans, reports): `pages_create` with a parent and, when it belongs to a task, link it to that task. `pages_update` replaces content, so read first and change only what you mean to.
- Task-level progress belongs in task comments (tmgr-task-workflow), not pages.

## Markdown sync (CLI)

- `tmgr page pull DIR [--tree PAGE_ID] [--force]` writes pages as `.md` files; `tmgr page status` shows local vs remote changes; `tmgr page push [FILES...]` uploads changed files. Pull before editing, push only files you changed, and do not use `--force` over local edits.
- `tmgr note [TITLE] [--task REF] [--parent ID]` opens `$EDITOR` and saves a page.
- Block features the Markdown form cannot express may be simplified on round trip; check `tmgr page status` after a push.
