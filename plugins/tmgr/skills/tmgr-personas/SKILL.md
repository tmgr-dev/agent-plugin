---
name: tmgr-personas
description: Use when the user wants to create or assign a persona, give it skills, work with the shared skills library and its versions, or asks what a persona is. Not for the plugin skills you are reading now.
---

# Personas and the skills library

A persona is an AI teammate with a name, a role, a system prompt, permissions per workspace and skills. Tasks can be assigned to it like to a person.

## Personas

- Create in the web app: Settings, Personas. Choose who can assign it (only me, or this workspace), the system prompt, and what it may do in each workspace. An agent connects as the persona with its own token, limited to one workspace and to those permissions.
- MCP: `list_assignable_personas(workspaceId)`, `assign_persona(taskId, persona)` / `unassign_persona`. Only assign when the user asks. A persona token also has `get_persona` (system prompt and skills index), `get_persona_skill(slug)` and `list_my_queue`.

## Skills library

Skills here are server-side Markdown files for personas. They are different from the plugin skills in this repo.

- Front matter: `slug` (lowercase letters, digits, `-`, up to 60), `title` (up to 120), `when` (required), `actions`. Up to 16384 bytes, 100 skills per library, 20 per persona.
- CLI: `tmgr skills list|show|put|delete|attach|detach`. `tmgr skills put <slug> --file F.md` uploads and every change is a new version. `tmgr skills attach <persona-id> <slug>`.
- A persona gets the latest version unless pinned to one. A persona's own skill with the same slug wins over the library one. Deleting a skill detaches it everywhere; deleted skills can be restored from their versions for 30 days, but attachments are not restored.
- Never put secrets or private data into a skill: it is shared with every persona it is attached to.

Docs: https://tmgr.dev/docs/web/personas-and-skills, https://tmgr.dev/docs/app/skills-library, https://tmgr.dev/docs/cli/personas-and-skills
