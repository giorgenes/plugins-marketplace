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

### `sw-eng`

Skills for software engineering workflows, including closing issues from start to finish.

| Skill | Description |
|-------|-------------|
| `process` | Close a software development issue from start to finish. |
| `understand` | Deeply understand a codebase, module, or piece of code. |
| `reproduce` | Generate a reproduction script for a bug, based on the facts captured by the `understand` skill. |
| `analyse` | Find the root cause of a bug — answers why it happens, which component is responsible, and what evidence supports the theory. Produces a root cause analysis and architecture notes. Run after `reproduce`. |
| `design` | Decide what should be built — explores solutions, evaluates trade-offs, and picks the simplest approach that fits the architecture. Produces a design document, diagrams, API contracts, and data model changes. Run after `analyse`. |

### `brand-design`

Skills for brand design workflows: discovery interviews to define brand identity, and visual identity system generation for designers.

| Skill | Description |
|-------|-------------|
| `branding-questions` | Run a structured brand discovery interview covering purpose, audience, positioning, personality, voice, and visual direction. Saves a full brand brief to a local Markdown file. |
| `visual-identity` | Translate a completed brand brief into a full visual identity system. Asks targeted design questions, then produces a `visual-identity.md` specification for designers and a standalone HTML brand showcase page. Run after `branding-questions`. |
| `color-scheme` | Visualize and pick colors interactively. Given colors, builds shareable URLs for realtimecolors.com (live site preview) and coolors.co (palette editor). Given a URL from either site, extracts the colors for use by other skills. |

### `marketing`

Marketing strategy skills — website messaging architecture and brand copy guides.

| Skill | Description |
|-------|-------------|
| `website-messaging` | Design the messaging architecture of a website — IA, copy hierarchy, and section-by-section copy direction. Produces a `website-messaging.md` a designer or copywriter can execute from directly. Run after `branding-questions`. |
| `copy-guide` | Translate a brand brief into a practical copywriting guide — voice rules, tone by context, grammar preferences, "say this not that" examples, and CTA formulas. Produces a `copy-guide.md` any writer can use immediately. Run after `branding-questions`. |

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
