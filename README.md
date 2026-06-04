# Claude Plugin Marketplace

A community plugin marketplace for Claude Code by giorgenes.

## Install

Add this marketplace to Claude Code once:

```
/plugin marketplace add giorgenes/plugins-marketplace
```

Then install any plugin by name:

```
/plugin install sw-eng@giorgenes-plugins
```

## Available plugins

| Plugin | Description |
|--------|-------------|
| `sw-eng` | Placeholder — skill text coming soon. |

## Keeping up to date

> **Tip:** This marketplace and its plugins are updated independently — remember to refresh both periodically so you get the latest skills and fixes.

Update the marketplace catalog (fetches the latest plugin list):

```
/plugin marketplace update giorgenes-plugins
```

Update an installed plugin to its latest version:

```
/plugin update sw-eng
```

To update all marketplaces and all plugins in one go, you can run both commands without arguments:

```
/plugin marketplace update
/plugin update sw-eng
```

A restart of Claude Code is required after updating plugins for the changes to take effect.

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md) for how to add plugins and validate the marketplace.
