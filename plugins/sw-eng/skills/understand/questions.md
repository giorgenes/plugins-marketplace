# Issue Clarification Questions

Use these to build a shared understanding of WHAT needs to be done before writing any code.
Skip questions that are clearly irrelevant to the issue type.

---

## 1. The Problem

- What is the current behavior? What is the expected behavior?
- Is this a **bug** (something broken) or a **feature** (something new or changed)?
- If a bug: when did it start? Was it ever working correctly?
- Who is affected? (all users, specific roles, specific conditions?)
- How was this discovered? (user report, monitoring alert, manual testing, code review?)

## 2. The Goal

- What specific outcome signals that this issue is resolved?
- What are the **acceptance criteria** (definition of done)?
- Are there explicit scenarios or examples that must work after the change?

## 3. Scope

- What is explicitly **in scope**?
- What is explicitly **out of scope** for this issue?
- Which systems, services, or components are involved?
- What must **not** change or break?
- Are there related issues or follow-up work that is intentionally deferred?

## 4. Context & Background

- What is the business or user value behind this issue?
- Who is the primary stakeholder or requester?
- Are there linked issues, PRs, design docs, or prior discussions to read?
- What is the **priority** and **deadline**, if any?
- Are there blockers or dependencies on other teams or issues?

## 5. Requirements & Edge Cases

- What should happen with **invalid or unexpected input**?
- What are the **error states** and how should they behave?
- Are there **edge cases** the issue description does not cover but that are likely to arise?
- Are there **permissions** or **role-based** differences in behavior?
- Are there **localization**, **timezone**, or **encoding** concerns?

## 6. Non-Functional Requirements

- Are there **performance** requirements (latency, throughput, limits)?
- Are there **security** constraints or data sensitivity concerns?
- Are there **accessibility** requirements (a11y standards, screen reader support)?
- Are there **compliance** or **regulatory** rules that apply?
- Does this need to be **backward-compatible** with existing data or APIs?

## 7. Design & UX (if applicable)

- Are there **mockups**, **wireframes**, or a design spec linked to this issue?
- Are there exact **copy/text** requirements (labels, error messages, notifications)?
- What is the expected behavior on **mobile** vs. **desktop**?
- Are there **loading**, **empty**, and **error** states that need design?

## 8. Testing & Validation

- How should this be **manually tested** to verify correctness?
- Are there **automated tests** that need to be added or updated?
- Is there a **staging environment** or **test dataset** available?
- Should this be **feature-flagged** to allow safe rollout or A/B testing?

## 9. Rollout & Observability

- Does this require a **data migration** or schema change?
- Are there **rollback** concerns if the change causes issues in production?
- Should success be tracked with **metrics**, **logs**, or **alerts**?
- Is a **gradual rollout** or **dark launch** expected?
