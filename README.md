# Claude Plugin Marketplace

A community registry of Claude Code skills (plugins).

## Structure

```
plugins-marketplace/
├── registry.json              # Index of all published plugins
├── schema/
│   ├── registry.schema.json   # Schema for registry.json
│   └── manifest.schema.json   # Schema for each plugin's manifest.json
└── plugins/
    └── <plugin-name>/
        ├── manifest.json      # Plugin metadata
        └── SKILL.md           # Skill instructions read by Claude
```

## Adding a plugin

1. Create a directory under `plugins/<your-plugin-name>/`.
2. Add a `manifest.json` (see `schema/manifest.schema.json` for the shape).
3. Add a `SKILL.md` with the skill instructions Claude will follow.
4. Register the plugin in `registry.json`.

## Using a plugin

Copy the plugin's `SKILL.md` content into your project's `.claude/` skills configuration, or reference it via the Claude Code skill loading mechanism.
