# Understanding: Navigation

> Custom navigation stack management, route handling, and screen transitions.

## Phase: EXPLORING

## Hypothesis

Navigation is handled via react-native-deprecated-custom-components (Facebook's Navigator) with Redux state management for route tracking.

## Sources

- app/modules/navigation.js - Navigation actions and reducer
- app/containers/AppScreen.js - Navigator component, scene rendering
- app/old/navigator/Navigator.js - Facebook's Navigator implementation (1380 lines)

## Validated Understanding

**Core Responsibilities:**
1. **Redux State Management**: Navigation state in Redux store (ref, current, previous, history, drawer)
2. **Navigator Wrapper**: Uses react-native-deprecated-custom-components Navigator
3. **Route Actions**: goTo, goBack, goAndReplace, reset, openDrawer, closeDrawer
4. **Scene Rendering**: renderScene switch statement maps route names to components
5. **Navigation Ref**: Stores reference to Navigator for imperative push/pop/replace

**Navigation Actions:**
- `ref(nav)` - Store Navigator reference
- `goTo(route)` - Push route to stack
- `goBack()` - Pop route with 500ms delay
- `goAndReplace(route)` - Replace current route (with tab logic)
- `openDrawer()` / `closeDrawer()` - Drawer visibility

**Route Structure:**
```javascript
{
  name: 'launch' | 'dialer' | 'call' | 'account' | 'network_settings' | 'media_settings' | 'conversations' | 'history' | 'settings',
  call?: Call object  // For call routes
}
```

**Scene Config:**
- Uses `Navigator.SceneConfigs.FadeAndroid` for all transitions

**Screens Registered:**
- LaunchScreen (initial)
- Viewport (conversations, contacts, history, settings, dialer)
- CallScreen
- AccountScreen
- NetworkSettingsScreen
- MediaSettingsScreen

**Navigation State:**
```javascript
{
  ref: null,              // Navigator reference
  init: {name: 'launch'}, // Initial route
  current: {},            // Current route
  previous: {},           // Previous route
  history: [],            // Route history
  drawer: false           // Drawer visibility
}
```

**Key Patterns:**
- Thunk actions for goTo (async) to access Navigator ref
- goBack has 500ms delay before dispatching action
- goAndReplace has special logic for tab routes (conversations, dialer, history, settings)
- Drawer navigation supported but may not be used

## Children Identified

> Deeper concepts spawned during SPAWNING phase

| Child | Hypothesis | Status |
|-------|------------|--------|
| navigation-actions | Redux actions for navigation operations | PENDING |
| navigator-component | Navigator wrapper, ref management | PENDING |
| scene-rendering | renderScene switch, route-to-component mapping | PENDING |
| navigation-state | Redux reducer, state transformations | PENDING |
| drawer-navigation | Drawer open/close functionality | PENDING |

## Dependencies

- **Uses**: react-native-deprecated-custom-components (Navigator)
- **Used by**: All screens, call-management (navigation on call end), app initialization

## Key Insights

1. **Deprecated library**: Uses react-native-deprecated-custom-components from GitHub (not maintained)
2. **Commented alternatives**: react-navigation imports commented out (considered migration?)
3. **Tab logic**: goAndReplace has special handling for tab routes (don't replace if same tab)
4. **500ms delay**: goBack has artificial delay (animation sync?)
5. **Full-screen detection**: CallScreen detected as full-screen (hides status bar)

## ADR Candidates

1. **react-native-deprecated-custom-components**: Why this vs react-navigation?
2. **FadeAndroid scene config**: Platform-specific choice
3. **Redux for navigation state**: Centralized vs Navigator's internal state

## Flow Recommendation

- **Type**: SDD (internal service logic)
- **Confidence**: high
- **Rationale**: Navigation is infrastructure, not stakeholder-facing

## Synthesis

> Updated during SYNTHESIZING phase after children complete

### From Children
[pending]

### Combined Understanding
[pending]

## Bubble Up

> Summary to pass to parent during EXITING

- Custom Navigator wrapper with Redux state management
- 5 navigation actions (goTo, goBack, goAndReplace, reset, drawer)
- Scene rendering via switch statement
- Deprecated library dependency (migration risk)

---

*Phase: EXPLORING | Depth: 1 | Parent: root*
