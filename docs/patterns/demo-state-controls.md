# Demo State Controls

This pattern allows section previews to have external demo state controls that appear outside the iframe preview in `ScreenDesignPage`. This keeps the preview clean while still allowing easy state switching for design review.

## How it works

1. **Config file**: Section defines available demo states in `demo-config.json`
2. **ScreenDesignPage**: Reads config and renders controls outside the iframe
3. **Preview component**: Listens for `postMessage` events to update its state

## Adding demo states to a section

### Step 1: Create demo-config.json

Create `product/sections/[section-id]/demo-config.json`:

```json
{
  "states": [
    { "id": "loading", "label": "Loading" },
    { "id": "empty", "label": "Empty" },
    { "id": "populated", "label": "Populated" },
    { "id": "error", "label": "Error" }
  ],
  "defaultState": "populated",
  "toggles": [
    {
      "id": "isLoggedIn",
      "label": "Logged In",
      "defaultValue": true,
      "messageType": "setAuthState",
      "messageKey": "isLoggedIn"
    }
  ]
}
```

### Step 2: Add postMessage listener to preview component

In your preview component (e.g., `src/sections/[section-id]/[Name]Preview.tsx`):

```tsx
import { useState, useEffect } from 'react'

type DemoState = 'loading' | 'empty' | 'populated' | 'error'

export default function MyPreview() {
  // Read initial state from URL params
  const getInitialState = (): DemoState => {
    const params = new URLSearchParams(window.location.search)
    const state = params.get('state') as DemoState
    return ['loading', 'empty', 'populated', 'error'].includes(state)
      ? state
      : 'populated'
  }

  const [demoState, setDemoState] = useState<DemoState>(getInitialState)
  const [isLoggedIn, setIsLoggedIn] = useState(() => {
    const params = new URLSearchParams(window.location.search)
    return params.get('isLoggedIn') !== 'false'
  })

  // Listen for postMessage from parent (ScreenDesignPage)
  useEffect(() => {
    const handleMessage = (event: MessageEvent) => {
      if (event.data?.type === 'setDemoState') {
        setDemoState(event.data.state)
      }
      if (event.data?.type === 'setAuthState') {
        setIsLoggedIn(event.data.isLoggedIn)
      }
    }
    window.addEventListener('message', handleMessage)
    return () => window.removeEventListener('message', handleMessage)
  }, [])

  // Use demoState and isLoggedIn to derive component props...
}
```

## Config schema reference

### DemoConfig

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| `states` | `DemoState[]` | Yes | Available demo states |
| `defaultState` | `string` | Yes | ID of the default state |
| `toggles` | `DemoToggle[]` | No | Boolean toggles (e.g., logged in/out) |

### DemoState

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| `id` | `string` | Yes | Unique identifier, sent via postMessage |
| `label` | `string` | Yes | Display label in the controls UI |

### DemoToggle

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| `id` | `string` | Yes | Unique identifier |
| `label` | `string` | Yes | Display label (shown when active) |
| `defaultValue` | `boolean` | Yes | Initial toggle state |
| `messageType` | `string` | No | postMessage type (default: `'setToggle'`) |
| `messageKey` | `string` | No | Key in message payload (default: `'value'`) |

## postMessage API

### State changes

```typescript
// Sent when user clicks a state button
{ type: 'setDemoState', state: string }
```

### Toggle changes

```typescript
// Sent when user clicks a toggle button
// messageType and messageKey come from config
{ type: '<messageType>', [messageKey]: boolean, toggleId: string }

// Default (if no messageType/messageKey specified):
{ type: 'setToggle', value: boolean, toggleId: string }
```

## Example: Transform section

See `product/sections/transform/demo-config.json` and `src/sections/transform/TransformPreview.tsx` for a complete implementation example.
