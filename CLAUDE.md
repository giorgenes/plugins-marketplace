# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this is

A Claude Code plugin marketplace. Users add this marketplace once, then install individual plugins from it.

## Key commands

```
# Validate the marketplace and all plugins
! /plugin validate .

# (User-side) Add this marketplace
/plugin marketplace add giorgenes/plugins-marketplace

# (User-side) Install a plugin
/plugin install sw-eng@giorgenes-plugins
```

## Structure

```
.claude-plugin/marketplace.json       # Marketplace catalog — lists all plugins
plugins/<plugin-name>/
  .claude-plugin/plugin.json          # Plugin metadata: name, description, version
  skills/<skill-name>/SKILL.md        # Skill instructions; frontmatter description: controls trigger
```

## Adding a plugin

1. Create `plugins/<name>/` with `.claude-plugin/plugin.json` (`name`, `description`, `version`) and `skills/<skill-name>/SKILL.md`.
2. Register it in `.claude-plugin/marketplace.json` under `"plugins"`.
3. Update the plugins table in `README.md`.

## Conventions

- Plugin names use kebab-case.
- Each plugin can contain multiple skills under `skills/`.
- `plugin.json` `name` must match the directory name and the entry in `marketplace.json`.

## Before commit

Before commiting the code to git, make sure the following is met:
- plugin is validated
- README.md is updated to reflect any changes.

