# Design OS Features & Improvements

This document tracks features and improvements made to the Design OS tooling while building products. These are reusable across any project using Design OS.

---

## Demo State Controls (Outside Iframe)

**Added:** 2026-01-16
**Status:** Implemented locally, pending upstream contribution
**Docs:** [`docs/patterns/demo-state-controls.md`](./docs/patterns/demo-state-controls.md)

### What it does
Renders demo state controls (state switcher, toggles) outside the iframe preview in `ScreenDesignPage`, keeping the design preview clean and unobstructed.

### Why it matters
- Preview accurately represents the actual user experience
- Controls are always accessible regardless of viewport size
- Better screenshots without UI controls overlapping the design
- Works consistently across all sections

### Files involved
| File | Purpose |
|------|---------|
| `src/lib/demo-config-loader.ts` | Dynamic config loader + TypeScript types |
| `src/components/ScreenDesignPage.tsx` | Renders controls based on section config |
| `product/sections/[section]/demo-config.json` | Per-section demo state configuration |

### How to use
1. Create `demo-config.json` in your section's product folder
2. Add `postMessage` listener in your preview component
3. Controls automatically appear in ScreenDesignPage

See full guide: [`docs/patterns/demo-state-controls.md`](./docs/patterns/demo-state-controls.md)

### Contribution status
- Proposal: [`docs/contributions/demo-controls-outside-iframe.md`](./docs/contributions/demo-controls-outside-iframe.md)
- PR instructions: [`docs/contributions/README.md`](./docs/contributions/README.md)

---

## URL-Based State Control

**Added:** 2026-01-16
**Status:** Implemented

### What it does
Allows direct linking to specific demo states via URL parameters (e.g., `?state=error&user=guest`).

### Why it matters
- Shareable links to specific states for review/feedback
- Bookmarkable states during development
- Works with fullscreen mode for screenshots

### How to use
Preview components read initial state from URL params:
```tsx
const getInitialState = () => {
  const params = new URLSearchParams(window.location.search)
  return params.get('state') || 'default'
}
```

---

## Future Ideas

- [ ] Dark mode toggle in ScreenDesignPage controls
- [ ] Viewport size presets beyond mobile/tablet/desktop
- [ ] Animation speed controls for testing transitions
- [ ] Export demo config as Storybook stories
