# Claude Plugin Marketplace

A community plugin marketplace for Claude Code by giorgenes.

## Install

Add this marketplace to Claude Code once:

```
/plugin marketplace add giorgenes/plugins-marketplace
```

Then install any plugin by name:

```
/plugin install dev-issue@giorgenes-plugins
```

## Available plugins

| Plugin | Description |
|--------|-------------|
| `dev-issue` | Placeholder — skill text coming soon. |

## Repository structure

```
plugins-marketplace/
├── .claude-plugin/
│   └── marketplace.json          # Marketplace catalog
└── plugins/
    └── <plugin-name>/
        ├── .claude-plugin/
        │   └── plugin.json       # Plugin metadata and version
        └── skills/
            └── <skill-name>/
                └── SKILL.md      # Skill instructions read by Claude
```

## Adding a plugin

1. Create `plugins/<your-plugin>/` following the structure above.
2. Add `.claude-plugin/plugin.json` with `name`, `description`, and `version`.
3. Add `skills/<skill-name>/SKILL.md` with the skill instructions (frontmatter `description:` field controls the trigger).
4. Register it in `.claude-plugin/marketplace.json` under `plugins`.

## Validating

```
/plugin validate .
```
