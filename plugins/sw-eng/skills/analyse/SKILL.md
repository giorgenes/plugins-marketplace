---
description: Use this skill to find the root cause of a bug, based on faq.md and reproduce.md from previous skills.
params:
  - name: path
    description: Directory containing faq.md and reproduce.md (outputs from the `understand` and `reproduce` skills). Defaults to the current directory if not provided.
---

1. Read `<path>/faq.md`. If it does not exist, tell the user to run the `understand` skill first and stop.
2. Read `<path>/reproduce.md`. If it does not exist, tell the user to run the `reproduce` skill first and stop.
3. Answer the **Root cause questions** below using the techniques listed, then write the outputs.

# Root cause questions

Answer each question with evidence. Skip any that are clearly not applicable.

| Question | What to look for |
|---|---|
| Why is this happening? | The specific condition, input, or state that triggers the failure |
| Which component is responsible? | The file, function, service, or layer where the fault originates |
| What assumptions are wrong? | Implicit invariants in the code that the bug violates |
| What evidence supports the theory? | Logs, traces, stack traces, data values, or code paths that confirm the cause |

# Techniques

Use whatever combination of these best fits the problem:

| Technique | When to use |
|---|---|
| Logging | Add or read log statements around the failure path to confirm control flow and variable state |
| Tracing | Follow a request or call chain end-to-end across services or layers |
| Debugging | Step through the reproduction script or test with a debugger or strategic print statements |
| Reading code | Trace the execution path statically; look for off-by-ones, wrong conditions, missing guards |
| Examining data | Inspect database records, queue messages, API payloads, or config values for unexpected values |

For code tracing: start at the entry point identified in `reproduce.md`, follow the call chain to the point of failure, and note each function and file along the way.

# Output

Use `path` as the output directory. If no `path` was given, use the current directory (`.`).

Write two files:

## `<path>/analysis.md`

Root cause analysis document. Include:

- **Root cause** — one clear sentence stating what is wrong and where
- **Why it happens** — the chain of events or conditions that lead to the failure
- **Responsible component** — file(s) and function(s) where the fault lives, with line references where possible
- **Wrong assumptions** — the invariants or expectations the code has that the bug breaks
- **Evidence** — the specific logs, traces, data, or code excerpts that confirm the theory
- **Confidence** — High / Medium / Low, with a note on what would increase confidence if not High

## `<path>/architecture.md`

Architecture notes relevant to the fix. Include:

- The components involved and how they relate (a short description or Mermaid diagram if it adds clarity)
- Data flow through the affected path
- Any constraints, contracts, or invariants that a fix must preserve
- Known risks or side-effects to consider when fixing

DO NOT create any other files or subdirectories.
