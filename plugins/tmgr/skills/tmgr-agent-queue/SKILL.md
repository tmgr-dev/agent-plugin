---
name: tmgr-agent-queue
description: Use when the user wants approved TMGR tasks to start on their own machine and come back as pull requests, asks how the agent queue, queue rules or `tmgr queue` work, or why an assigned task did not start. Experimental.
---

# The agent queue

Tasks assigned to a persona and approved by the owner start on the owner's machine without a chat session, each in its own copy of the project, and finish as a pull request. Nothing is merged for you.

## How it fits together

1. Web: turn on the Agent runs module (workspace modules), assign the task to a persona, and use Confirm for agent runs. The confirmation signs the exact task text; editing the task drops the signature.
2. Machine: `tmgr runner allow <workspace>` trusts the workspace and pins the signing keys. `tmgr runner bind <workspace>:<project> <path-to-clone>` links a project to a local clone.
3. Rule: `tmgr queue rules add <name> --workspace W --persona P --profile claude-code --repo DIR --project PRJ --auto --max-concurrent 2`. A cloud rule only starts tasks the owner signed.
4. Switch: `tmgr queue enable`, or one pass with `tmgr queue run-once`. `tmgr queue status`, `pause`, `resume`, `disable`.
5. Follow: `tmgr agents`, `tmgr peek <session>`.

Adding rules, enabling, approving and `runner allow/bind` need a real terminal and a typed confirmation. They are the owner's decisions: show the command and let them run it. Do not try to bypass the prompt.

## When a task does not start

Check in order: Agent runs module on, the task is assigned to the persona and confirmed, `runner allowed` lists the workspace, a rule matches workspace, project and persona, `tmgr queue status` shows the queue enabled and not paused, and the concurrency limit is not reached.

`tmgr runner gc --dry-run` lists finished task copies; `tmgr runner gc` removes them.

## Related

Backlog automation on top of the queue: tmgr-autopilot. Runner and sessions: tmgr-runner. Docs: https://tmgr.dev/docs/cli/the-agent-queue
