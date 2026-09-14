---
name: dawk-task
description: Turn a TODO, bug, or note from the editor into a Dawk task and link it to the code. Use when the user says "make this a task", "file this in Dawk", or asks to track something they found in the code.
---
# Dawk task from the editor

Needs the `dawk:write` scope for steps 2 and 3.

1. `list-workspaces` — pick the workspace (and project, if the repo maps to one). If it is not obvious, ask; do not guess.
2. `create-task` with a short imperative `title`, a `description` that states the problem and the expected outcome, and the workspace id. Priority only if the user gave one. The task enters planning; a human approves the plan before anything runs. Note the returned task id and `channel_id`.
3. `post-message` to that channel with the file path and line range (and the commit or branch if known) so the plan has a starting point. One message, no code dumps.
4. Report the task id and link, and confirm the message posted. If the create succeeded but the post failed, say exactly that.

Later edits: `update-task` changes title, description or priority. Status and approvals are not editable here. Never call `cancel-task` unless the user asks to cancel by name.
