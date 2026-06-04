---
description: Use this skill to deeply understand a codebase, module, or piece of code
params:
  - name: target
    description: The file, directory, module, or concept to understand (defaults to the whole project)
---

# understand

Your goal is to build and communicate a clear mental model of the target code. Explore thoroughly, then explain in a way that lets the user reason about the code confidently.

## Workflow

1. **Orient** — Identify the target. If no target is given, start from the project root: read `CLAUDE.md`, `README.md`, and any top-level config files to understand the project's purpose and structure.
2. **Map** — Walk the relevant directory tree. Note key directories, entry points, and the overall shape of the code.
3. **Trace** — For the most important modules or flows, read the source. Follow call chains, data flow, and dependency edges far enough to understand behaviour, not just structure.
4. **Synthesise** — Produce a structured summary (see Output below). Prioritise insight over completeness: surface the non-obvious, skip the self-evident.

## Output

Structure your response as follows:

### Purpose
One or two sentences on what this code does and why it exists.

### Structure
How the code is organised — key directories, modules, or layers. A short bullet list is fine.

### Key concepts
The domain concepts, patterns, or abstractions a reader must understand to work with this code. Explain each in one or two sentences.

### Entry points
Where execution starts, or where the most important public interfaces live.

### Gotchas
Non-obvious constraints, sharp edges, or things that will surprise a reader. Omit this section if there are none.

## Rules

- Read as much source as needed, but summarise — do not dump raw file contents at the user.
- Prefer concrete examples (function names, file paths, data shapes) over abstract generalisations.
- If the target is ambiguous, ask the user to clarify before proceeding.
- If the target is too large to fully explore, say so and offer to focus on a specific sub-area.
