# Contributions to Design OS

This folder tracks potential contributions back to the Design OS open source project.

## Pending Contributions

### 1. Demo State Controls Outside Iframe

**Status:** Proposal submitted, awaiting approval
**Discussion:** https://github.com/buildermethods/design-os/discussions (Ideas section)
**Proposal file:** `demo-controls-outside-iframe.md`

#### Summary

Moves demo state controls (for testing different UI states) outside the iframe preview so they don't overlap the design being reviewed.

#### Implementation (ready to contribute)

| File | Location | Description |
|------|----------|-------------|
| `demo-config-loader.ts` | `src/lib/` | Loader function and TypeScript types |
| `demo-config.json` | `product/sections/[section]/` | Per-section config schema |
| `ScreenDesignPage.tsx` | `src/components/` | Updated to read config dynamically |
| `demo-state-controls.md` | `docs/patterns/` | Pattern documentation |

#### Files to include in PR

```
src/lib/demo-config-loader.ts        # New file
src/components/ScreenDesignPage.tsx  # Modified (demo controls section)
docs/patterns/demo-state-controls.md # New file
```

#### Example config to include

```
product/sections/transform/demo-config.json  # Example implementation
```

#### When approved

1. Fork the Design OS repo
2. Create branch `feature/demo-controls-outside-iframe`
3. Copy the files listed above
4. Remove any Animira-specific references
5. Submit PR referencing the approved discussion

---

## Contributing Process (Design OS)

From their CONTRIBUTING.md:

1. **Start with a Discussion** in the Ideas section
2. Wait for maintainer to label it `approved`
3. Only then submit a PR
4. Include `[feature]` in PR title for new features

Note: "New features rarely enter core" - so discussion approval is important before investing time in a PR.
