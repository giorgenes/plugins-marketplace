---
description: Use this skill to deeply understand what needs to be done when given a task, issue or bug.
params:
  - name: context
    description: What to understand — a free-form description, an issue ID, a feature name, or any combination.
  - name: path
    description: Directory to save output. Defaults to the current directory if not provided.
---

1. If the context mentions an issue ID, fetch the issue details from the relevant tracker (Linear, GitHub, Jira, etc.) and use that as additional context.
2. Read the questions in @questions.md.
3. For each question, answer it from the context given. Skip questions that are clearly irrelevant or already answered.
4. Generate `faq.md`: This should be a comprehensive FAQ for reference with the key information and decisions.
5. Generate diagrams (see below) and save them alongside the FAQ.

# Output

Use the `path` param as the output directory. If no `path` was given, use the current directory (`.`).

- Save the FAQ to `<path>/faq.md`.
- Save diagrams to `<path>/diagrams/`.

DO NOT invent a subfolder structure beyond what is specified above.

# Diagrams

Generate only the diagrams that are relevant to the issue. Skip any that add no insight given the context.

For each diagram:
1. Write the Mermaid source to `<path>/diagrams/<name>.mmd`
2. Export to SVG: `npx --yes @mermaid-js/mermaid-cli -i <path>/diagrams/<name>.mmd -o <path>/diagrams/<name>.svg`

## Flowchart

The main process or business logic flow. Include decision points and branching paths.
Covers the happy path and the most important edge cases identified in the FAQ.

```
flowchart TD
```

## Swimlane diagram

Which actor (user, system, external service) is responsible for each step.
Use this when the issue involves multiple actors or cross-system handoffs.

```
flowchart LR (with subgraph per actor as swimlanes)
```

## State diagram

The lifecycle of the main entity involved — what states it can be in and what triggers transitions.
Use this when the issue involves status, approval flows, or any kind of state change.

```
stateDiagram-v2
```

## Context diagram

The boundary of the feature: what's in scope, what systems it touches, what it does not touch.
Use this when scope is ambiguous or the feature interacts with multiple systems.

```
flowchart TB (system as central node, external actors/systems around it)
```

## User journey

The end-to-end experience around the feature, from the user's perspective.
Include steps before and after the feature itself to capture upstream/downstream effects.
Use this for user-facing features.

```
journey
```
