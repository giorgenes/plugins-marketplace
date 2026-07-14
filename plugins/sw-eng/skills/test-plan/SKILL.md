---
name: test-plan
description: Use this to generate an end to end test plan for an issue, bug or feature
---

# Goal

The goal of this skill is to produce a test plan for an implementation.

# Steps

- Read `understand/*` documents.
- Read `reproduce/*` documents.
- Read `design/*` documents.
- Create a `test/` folder is non-existant.
- Create a `test/*.md` files containing the test plan.

# Test plan

The test plan should contain test scenarios for the feature or bug fix implementated. It should cover the steps to be able to be manually executed (though it will probably be automated in later steps).

# Generated Files

Break down the content of the test plan into separate files.
Think of the files as short notes instead of building one long document with multiple sections.

# Rules

Read `${CLAUDE_PLUGIN_PATH}/shared/rules.md` and follow those rules too.