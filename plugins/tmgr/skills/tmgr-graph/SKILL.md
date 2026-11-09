---
name: tmgr-graph
description: Use when the user asks what is connected to a task or page, what blocks what, which tasks to unblock first, what is forgotten or unlinked, or how two items are related; also for a workspace overview for planning or review.
---

# The workspace graph

Tasks and pages are linked (relations: blocks, depends on, duplicates, relates to; page links and mentions). These tools read that graph in one call instead of chaining many lookups.

- `graph_related(entity, depth, include)`: everything around one item, up to 2 hops. `entity` is `task:<id>`, `page:<id>`, `page:<slug>` or a task key like `TM-418`. Use it when you start a task or estimate impact. `include` is a comma list from tasks, pages, people, personas, agent_runs, comments.
- `graph_path(from, to, maxDepth)`: the shortest chain of links between two items (max 4 hops); empty nodes mean no path.
- `graph_hubs(workspaceId)`: the most connected items and the bottlenecks, the tasks blocking the most open work. Start unblocking there.
- `graph_orphans(workspaceId)`: open tasks and pages with no links. Forgotten work, or pages that should be connected.
- `graph_map(workspaceId, from, to, limit)`: the whole workspace in one call with clusters, bridges and insights. For reviews and planning only; the default is 500 nodes and `truncated=true` means the most connected were kept.

The graph needs the Graph module, which needs Pages; if a tool says it is off, see tmgr-workspace-modules.

Answers carry `url`s and keys; link with them. If `truncated` or `capsHit` is set, narrow `depth`, `include` or the dates before concluding something is missing.

To add a relation, use the task tools (tmgr-create-tasks). Docs: https://tmgr.dev/docs/app/pages
