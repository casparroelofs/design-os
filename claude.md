# design-os

Visual product design tool for rapidly prototyping ideas.

Refer to @agents.md for detailed directives.

## Multi-Product Workflow

This is ONE instance for ONE product. The repo name should be `[product-name]-design-os`.

### Current Product

Check `product/product-overview.md` to see which product this instance is for.

### Starting Fresh

If this is a template clone, run `/design-os/product-vision` to begin.

### Resuming Work

1. Check `product/product-overview.md` for product context
2. Check `product/product-roadmap.md` for section progress
3. Run appropriate command to continue

### Exporting

After `/design-os/export-product`, copy `product-plan/` to your actual product codebase.

---

## Code Structure

```
[product-name]-design-os/
├── src/              # Source code
├── product/          # Product sections and configuration
├── public/           # Static assets
└── dist/             # Build output
```

## Tech Stack

| Layer | Technology |
|-------|------------|
| Framework | React, Vite |
| Styling | Tailwind CSS |

## Development

```bash
bun install           # Install dependencies
bun run dev           # Start dev server
bun run build         # Production build
```

## Project-Specific Commands

This project has custom commands in `.claude/commands/design-os/`:
- `/design-os/product-vision` - Product vision
- `/design-os/product-roadmap` - Product roadmap
- `/design-os/data-model` - Data model
- `/design-os/design-tokens` - Design tokens
- `/design-os/design-shell` - Application shell
- `/design-os/shape-section` - Define section specification
- `/design-os/sample-data` - Create sample data
- `/design-os/design-screen` - Design a screen
- `/design-os/screenshot-design` - Capture screenshots
- `/design-os/export-product` - Generate export package

## Documentation

See `docs/` folder for:
- `getting-started.md` - Setup instructions
- `usage.md` - How to use the workflow
- `product-planning.md` - Product planning guide
- `design-section.md` - Section design guide
- `export.md` - Export workflow
- `patterns/` - Design patterns (e.g., demo state controls)
- `contributions/` - Upstream contribution tracking
