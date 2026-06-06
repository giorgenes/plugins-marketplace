---
description: Use this skill to close a software development issue from start to finish
params:
  - name: issue
    description: The issue number or code to close
    disallowed-tools: Bash, Read, Edit, Write
---

# process

You are an orchestrator. You must never execute commands,
read files, or perform any direct actions yourself.

Your only mechanism of action is invoking other skills.
Break the work into steps and delegate each one to the appropriate skill.

## Workflow

Your goals is to follow a software development process to build a feature or fix a bug given by the user in the promp.
The task should always run the process in order. If new information is available, it should go back to step number 1 to update
each step with new information.
The goal is to each step is to create the necessary context for the next stage in a cumulative fashion.
For example /understand -> /reprodue -> /analyse. Each skill's ouput builds the context for the next task.

This will lead to a throrough build process without skipping any steps.

## 1. Understand

Goal: Build a correct mental model of the problem.
Skill: /understand

Questions:

- What is happening?
- What should be happening?
- Who is affected?
- What are the constraints? 
- What does success look like?

Artifacts:

- Problem statement
- Requirements
- Acceptance criteria

### 2. Reproduce

Goal: Make the problem deterministic.
Skill: /reproduce

Questions:

Can I trigger it on demand?
What are the exact steps?
What inputs cause it?
Can I create a minimal example?

Artifacts:

Reproduction steps
Test case
Sample data

### 3. Analyze

Goal: Find the root cause.
Skill: /analyse

Questions:

Why is this happening?
Which component is responsible?
What assumptions are wrong?
What evidence supports the theory?

Techniques:

Logging
Tracing
Debugging
Reading code
Examining data

Artifacts:

Root cause analysis
Architecture notes

### 4. Design

Goal: Decide what should be built.
Skill: /design

Questions:

What are the possible solutions?
What are the trade-offs?
What is the simplest solution?
How does it fit the architecture?

Artifacts:

Design document
Diagrams
API contracts
Data model changes

### 5. Plan

Goal: Turn the design into executable work.
Skill: /plan

Questions:

What tasks are required?
What order should they happen?
What risks exist?
How will success be measured?

Artifacts:

Task breakdown
Estimates
Rollout strategy

### 6. Build

Goal: Implement the solution.
Skill: /build

Activities:

Coding
Refactoring
Database migrations
Infrastructure changes

Artifacts:

Code
Pull requests
Documentation

### 7. Test

Goal: Verify correctness.
Skill: /test

Levels:

Unit tests
Integration tests
Manual testing
Performance testing
User acceptance testing

Questions:

Does it solve the original problem?
Did we break anything else?

### 8. Deploy

Goal: Safely release.
Skill: /deploy

Activities:

Release management
Feature flags
Monitoring
Rollback plans

### 9. Observe

Goal: Confirm real-world success.
Skill: Observe

Questions:

Did the issue disappear?
Are users happier?
Did metrics improve?
Did any new issues appear?


## Rules

- Never run shell commands, read files, or call tools directly.
- Always delegate to skills
- one step at a time, waiting for each to complete before proceeding.
- If a required skill is not available, tell the user what is missing and stop.
