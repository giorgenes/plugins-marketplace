---
name: reproduce
description: Use this skill to generate a reproduction script for a bug or issue, based on the understanding captured under `understand/`.
params:
  - name: path
    description: Directory containing the `understand/*.md` notes (output from the `understand` skill). Defaults to the current directory if not provided.
---

# Steps

1. Read `<path>/understand/*.md`. If it does not exist, tell the user to run the `understand` skill first and stop.
2. Analyze the facts to determine the problem type and the right reproduction approach (see **Choosing a script** below).
3. Generate the script(s) and save it to `<path>/reproduce/<task>.<ext>`.
4. Write a short `<path>/reproduce/instructions.md` that explains: what the script(s) do(es), how to run it, and what the expected (broken) output looks like vs. what correct output would look like.

# Bugs vs Features

If the issue type is a bug, focus on reproducing the bug.
If the issue type is a new feature or change, focus on reproducing existing functionality or making steps that lead up to it.

## Examples

- *Adding a new UI feature*: the reproduce script should lead up to the screen where the feature should be.
- *Adding new APIs*: the reproduce script should call similar apis or functionality via the UI.
- *Fixing a bug*: the script should reproduce the bug

# Purpose

The purpose of the reproduce script is one of either:
a) reproduce a specific behaviour like a bug
b) reproduce an existing behaviour that needs to be expanded or changed
c) lead up to a place where change needs to happen

This should include manually setting up the data as needed.

# Choosing a script

Select the language and tools that best match the problem. Use the simplest thing that reliably triggers the issue.

| Problem type | Preferred approach |
|---|---|
| HTTP REST API | `bash` with `curl` |
| gRPC API | `bash` with `grpcurl` |
| Web UI / browser interaction | `javascript` with Playwright |
| CLI tool | `bash` |
| Data pipeline / scripted logic | `python` |
| Node.js service or SDK | `javascript` / `typescript` |
| Database query | `python` with the relevant DB driver, or `bash` with the CLI client |
| Queue / pub-sub | `python` or `bash` with the relevant CLI |
| Mixed / unclear | `python` (most portable) |

Do not limit yourself to this list — use whatever tool best reproduces the problem with the least friction. Prefer tools already present in the codebase.

# Script requirements

- The script must be **self-contained**: a single file that can be run from a clean checkout without manual steps beyond installing listed dependencies.
- Add a `# Requirements:` comment at the top listing any tools or packages needed (e.g. `curl`, `grpcurl`, `pip install httpx`).
- Add a `# Usage:` comment showing exactly how to run it.
- Target the **minimal input** that triggers the bug. Remove all unrelated steps.
- Include clear `echo` / `print` / `console.log` statements so the person running it can see: what it sent, what it got back, and what was wrong about the response.
- If credentials or environment variables are required, embed it in the script but allow to override with env vars. Document each with a comment. These are throw away local scripts so security isn't a concern.
- If the bug requires a specific data state (e.g. a database record), include setup and teardown steps inside the script.

# Output

Use `<path>/reproduce/` as the output directory. If no `path` was given, use the current directory (`.`).

- Save the script to `<path>/reproduce/<script>.<ext>` (choose the correct extension for the language: `.sh`, `.py`, `.js`, `.ts`).
- Save the explanation to `<path>/reproduce/instructions.md`.
- Make the script executable if it is a shell script (`chmod +x`).

# Other notes and rules

- DO NOT create any other files or subdirectories.
- DO NOT try to implement the requirements or find root cause.
- Read `${CLAUDE_PLUGIN_PATH}/shared/rules.md` and follow those rules too.