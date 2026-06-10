---
description: Use this skill to decide what should be built — explore solutions, evaluate trade-offs, and pick the simplest approach that fits the architecture.
params:
  - name: path
    description: Directory containing faq.md and reproduce.md (outputs from the `understand` and `reproduce` skills), and optionally analysis.md (output from the `analyse` skill). Defaults to the current directory if not provided.
---

1. Read `<path>/faq.md`. If it does not exist, tell the user to run the `understand` skill first and stop.
2. Read `<path>/reproduce.md`. If it does not exist, tell the user to run the `reproduce` skill first and stop.
3. Read `<path>/analysis.md` if it exists and use it as additional context. It is optional — skip silently if absent.
4. Answer the **Design questions** below, then write the outputs.

# Design questions

Answer each question. Skip any that are clearly not applicable.

| Question | What to consider |
|---|---|
| What are the possible solutions? | At least two distinct approaches; include the simplest viable option |
| What are the trade-offs? | Complexity, performance, reliability, maintainability, reversibility for each option |
| What is the simplest solution? | The option with the smallest footprint that fully solves the problem |
| How does it fit the architecture? | Which existing patterns, layers, and contracts it follows or must change |

Prefer the simplest solution that fully addresses the problem. Avoid over-engineering.

# Output

Use `path` as the output directory. If no `path` was given, use the current directory (`.`).

## `<path>/design.md`

The main design document. Include:

- **Problem summary** — one paragraph recapping what needs to be solved and why (drawn from the input files)
- **Options considered** — for each option: a short description, pros, cons, and a verdict (chosen / rejected / fallback)
- **Chosen solution** — what will be built, in plain language; why this option over the others
- **Implementation outline** — the key steps or phases, in order; highlight any sequencing constraints
- **Fits the architecture** — how the solution aligns with existing patterns; any parts of the architecture it changes or extends
- **Open questions** — anything that needs a decision or more information before implementation starts

## Diagrams

Generate only the diagrams that add insight. Skip any that would be redundant or empty given the context.

For each diagram:
1. Write the Mermaid source to `<path>/diagrams/<name>.mmd`
2. Export to SVG: `npx --yes @mermaid-js/mermaid-cli -i <path>/diagrams/<name>.mmd -o <path>/diagrams/<name>.svg`

### Solution comparison

A side-by-side view of the options and their key dimensions (complexity, risk, scope). Use when there are three or more options or when the trade-offs are non-obvious.

```
flowchart LR
```

### Proposed architecture

How the components look after the change — new nodes, modified relationships, removed paths. Use when the solution adds, removes, or meaningfully changes a component or connection.

```
flowchart TD
```

### Sequence diagram

The new or corrected interaction between components. Use when the fix changes the order of calls, introduces async steps, or resolves a race condition.

```
sequenceDiagram
```

### Data model

The entity relationships affected by the change. Use when the solution modifies a schema, adds a table or field, or changes cardinality.

```
erDiagram
```

## `<path>/api-contracts.md`

API contracts for any new or changed interfaces. Include only what the solution introduces or modifies. Skip this file entirely if no API changes are needed.

For each endpoint or method:

- **Name / path / method**
- **Purpose** — one sentence
- **Request** — parameters, headers, body schema (use a concise JSON example)
- **Response** — status codes, body schema (use a concise JSON example)
- **Error cases** — the failure modes the caller must handle
- **Backwards compatibility** — breaking / non-breaking; migration notes if breaking

## `<path>/data-model.md`

Data model changes required by the solution. Skip this file entirely if no schema changes are needed.

- **Summary** — what is being added, removed, or changed and why
- **Schema changes** — new tables/collections, modified columns/fields, removed structures; include types and constraints
- **Migration strategy** — how existing data is handled; whether the migration is online or offline
- **Impact** — queries, indexes, or application code that must change as a result

DO NOT create any other files or subdirectories.
