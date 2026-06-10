---
description: Use this skill to generate a reproduction script for a bug or problem, based on the understanding captured in faq.md.
params:
  - name: path
    description: Directory containing faq.md (output from the `understand` skill). Defaults to the current directory if not provided.
---

1. Read `<path>/faq.md`. If it does not exist, tell the user to run the `understand` skill first and stop.
2. Analyze the facts to determine the problem type and the right reproduction approach (see **Choosing a script** below).
3. Generate the script and save it to `<path>/reproduce.<ext>`.
4. Write a short `<path>/reproduce.md` that explains: what the script does, how to run it, and what the expected (broken) output looks like vs. what correct output would look like.

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
- If credentials or environment variables are required, read them from env vars (never hardcode secrets). Document each with a comment.
- If the bug requires a specific data state (e.g. a database record), include setup and teardown steps inside the script.

# Output

Use `path` as the output directory. If no `path` was given, use the current directory (`.`).

- Save the script to `<path>/reproduce.<ext>` (choose the correct extension for the language: `.sh`, `.py`, `.js`, `.ts`).
- Save the explanation to `<path>/reproduce.md`.
- Make the script executable if it is a shell script: `chmod +x <path>/reproduce.sh`.

DO NOT create any other files or subdirectories.
