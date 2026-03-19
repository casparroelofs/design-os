# Screenshot Screen Design

You are helping the user capture screenshots of a screen design. Screenshots can be captured in multiple variants: light/dark mode and desktop/mobile viewports.

## Step 1: Identify the Screen Design

Read `/product/product-roadmap.md` to get the list of available sections, then check `src/sections/` for existing screen designs.

If only one screen design exists, auto-select it.

If multiple exist, ask the user which one to screenshot:

"Which screen design would you like to screenshot?"

Present options grouped by section:
- [Section Name] / [ScreenDesignName]

## Step 2: Ask Which Variants

Ask the user which variants to capture:

"Which variants should I capture?
- **All 4** — light desktop, dark desktop, light mobile, dark mobile
- **Desktop only** — light + dark at 1280x800
- **Mobile only** — light + dark at 375x812
- **Light only** — desktop + mobile in light mode
- **Dark only** — desktop + mobile in dark mode
- **Single** — just one specific combination"

## Step 3: Check for Demo States

Check if `product/sections/[section-id]/demo-config.json` exists, or if the screen design preview component has demo state controls (look for state buttons or a `DemoState` type in `src/sections/[section-id]/[ScreenDesignName].tsx`).

If demo states exist, capture the selected variants for each state.

## Step 4: Capture Screenshots

Use `agent-browser` (the CLI tool, via Bash) to capture screenshots.

### Setup

1. Start the dev server (`npm run dev`) in the background using Bash
2. Wait a few seconds for the server to be ready
3. Open the fullscreen URL:
   ```bash
   agent-browser open "http://localhost:3000/sections/[section-id]/screen-designs/[screen-design-name]/fullscreen"
   ```
4. Wait for the page to load:
   ```bash
   agent-browser wait --load networkidle
   ```

### Capture each variant

For each selected variant, set the viewport + theme, then capture:

```bash
# Set viewport (pick one)
agent-browser set viewport 1280 800   # desktop
agent-browser set viewport 375 812    # mobile

# Set theme (pick one)
agent-browser set media light
agent-browser storage local set theme light
# OR
agent-browser set media dark
agent-browser storage local set theme dark

# Reload to apply theme fully, then capture
agent-browser reload
agent-browser wait --load networkidle
agent-browser screenshot --full product/sections/[section-id]/[name]-[variant].png
```

### Demo states

If the section has demo states, use the snapshot to find and click state control buttons between captures:

```bash
agent-browser snapshot -i
agent-browser click @[ref]  # Click the state button
```

### Naming convention

`[screen-design-name]-[variant].png`

| Variant | Filename |
|---------|----------|
| Light desktop | `hero-light-desktop.png` |
| Dark desktop | `hero-dark-desktop.png` |
| Light mobile | `hero-light-mobile.png` |
| Dark mobile | `hero-dark-mobile.png` |

With demo states: `[name]-[state]-[variant].png` (e.g., `create-empty-light-desktop.png`)

### Screenshot specifications

- Desktop: 1280x800 viewport
- Mobile: 375x812 viewport (iPhone 14 equivalent)
- Full page screenshots (`--full`) to capture all scrollable content
- PNG format

## Step 5: Cleanup

Close the browser and kill the dev server when done.

```bash
agent-browser close
```

## Step 6: Confirm Completion

List all screenshots saved:

"I've saved screenshots to `product/sections/[section-id]/`:

[List each file with a brief description]

The screenshots capture the **[ScreenDesignName]** screen design for the **[Section Title]** section."

## Important Notes

- Start the dev server yourself — do not ask the user to do it
- Screenshots are saved to `product/sections/[section-id]/` alongside spec.md and data.json
- Always use the `/fullscreen` route — it renders the screen design without Design OS chrome
- Both `set media` and `storage local set theme` are needed — `set media` handles CSS `prefers-color-scheme`, `storage local` handles the app's theme state
- Reload after changing theme to ensure full re-render
- After you're done, kill the dev server if you started it
