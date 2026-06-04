---
description: Use this skill to deeply understand what needs to be done when given a task, issue or bug.
params:
  - name: issue-id
    description: The issue id to understand.
---

1. Read the questions in @questions.md
2. For each question, try to answer it from the context given.
3. Generate diagrams (see below) and save them to the output folder.


# Output

Save an md file with the answers in `$CONTEXT_PATH/Projects/$0/faq.md`

Save SVG diagrams to `$CONTEXT_PATH/Projects/$0/diagrams/`


# Diagrams

Generate only the diagrams that are relevant to the issue. Skip any that add no insight given the context.

For each diagram:
1. Write the Mermaid source to a temp file (e.g. `/tmp/<name>.mmd`)
2. Export to SVG: `npx --yes @mermaid-js/mermaid-cli -i /tmp/<name>.mmd -o $CONTEXT_PATH/Projects/$0/diagrams/<name>.svg`
3. Delete the temp file

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
