# Feature Idea: Demo state controls outside iframe preview

> **Status:** Submitted to Design OS Discussions (Ideas)
> **Implementation:** Ready in this repo - see files listed at bottom

---

## Problem & motivation

When building section previews with demo state controls (e.g., toggling between "loading", "error", "success" states), the controls currently live inside the preview component itself. Since `ScreenDesignPage` renders previews in an iframe for style isolation, these controls appear *inside* the device mockup, overlapping the actual design.

This makes it hard to evaluate the design at different states without the controls interfering visually.

## Proposed change & alternatives

**Proposed change:** Move demo state controls to `ScreenDesignPage.tsx` (outside the iframe) and communicate with the preview via `postMessage`.

This would involve:

1. A convention for sections to declare available demo states (e.g., `demo-config.json` or exported from the preview component)
2. `ScreenDesignPage` rendering controls based on that config
3. Preview components listening for `postMessage` to update their state

**Alternatives considered:**

- **Collapsible/hideable controls inside the iframe** — Still intrusive, requires extra UI chrome
- **Floating controls that can be dragged out of the way** — Complex to implement, still occupies viewport space
- **Keyboard shortcuts for state switching** — Not discoverable, poor UX for new users

## User experience impact

- Cleaner preview that accurately represents the actual user experience
- Controls are always accessible regardless of preview width or current state
- Works consistently across all sections without per-section customization
- Better for taking screenshots of designs

## Updating & compatibility considerations

- **Backward compatible** — Sections without demo config would simply show no controls (current behavior)
- **Opt-in per section** — Only sections that define a `demo-config.json` would get external controls
- **Minimal API surface** — Preview components just need to listen for a standard `postMessage` event
- **No breaking changes** — Existing preview components continue to work unchanged

---

## Implementation Reference (local)

Implementation is complete and tested in this repo:

| File | Purpose |
|------|---------|
| `src/lib/demo-config-loader.ts` | Config loader + TypeScript types |
| `src/components/ScreenDesignPage.tsx` | Dynamic controls rendering |
| `docs/patterns/demo-state-controls.md` | Pattern documentation |
| `product/sections/transform/demo-config.json` | Example config |

See `docs/contributions/README.md` for PR instructions when approved.
