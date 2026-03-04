# Understanding: Screens

> Screen components and viewport pattern for main app screens.

## Phase: EXPLORING

## Sources

- app/screens/** - Screen implementations
- app/containers/** - Container components with Viewport pattern
- app/containers/AppScreen.js - Main app container (already analyzed in navigation)

## Validated Understanding

**Screen Structure:**
```
app/
├── screens/
│   ├── LaunchScreen/
│   ├── CallScreen/          ← Analyzed in call-management
│   ├── AccountScreen/
│   ├── NetworkSettingsScreen/
│   ├── MediaSettingsScreen/
│   └── ...
└── containers/
    ├── conversations/
    │   ├── ConversationsScreen.ios.js
    │   └── ConversationsViewport.js
    ├── dialer/
    │   └── DialerViewport.js  ← Analyzed in call-management
    ├── history/
    │   ├── HistoryScreen.ios.js
    │   └── HistoryViewport.js
    └── settings/
        ├── SettingsScreen.ios.js
        └── SettingsViewport.js
```

**Viewport Pattern:**
```javascript
// Screen component (e.g., SettingsScreen.ios.js)
// - Handles iOS-specific logic
// - Renders Viewport

// Viewport component (e.g., SettingsViewport.js)
// - Platform-agnostic
// - Connected to Redux
// - Contains business logic
```

**Screens Identified:**

| Screen | Container | Purpose |
|--------|-----------|---------|
| LaunchScreen | - | Initial screen, app bootstrap |
| CallScreen | - | Active call UI (analyzed in call-management) |
| AccountScreen | - | SIP account configuration |
| NetworkSettingsScreen | - | Network settings (transport, WiFi, etc.) |
| MediaSettingsScreen | - | Media/audio settings |
| ConversationsScreen | ConversationsViewport | Chat/conversations list |
| DialerViewport | - | Dialer keypad (analyzed in call-management) |
| HistoryScreen | HistoryViewport | Call history |
| SettingsScreen | SettingsViewport | App settings |

**Navigation Integration:**
```javascript
// In AppScreen.js renderScene
switch (route.name) {
  case 'launch': return (<LaunchScreen />)
  case 'dialer': return (<Viewport navigator={navigator}/>)
  case 'call': return (<CallScreen />)
  // ... etc
}
```

## Key Insights

1. **Viewport pattern**: Separation of iOS-specific and platform-agnostic logic
2. **Navigator prop**: Viewports receive navigator for navigation
3. **Redux connected**: Viewports use connect() for state/actions
4. **CallScreen dominant**: Most complex screen, rest are simpler

## Flow Recommendation

- **Type**: VDD (user-facing screens)
- **Confidence**: medium
- **Rationale**: Screens are user-facing, but Viewport pattern suggests internal logic separation

---

*Phase: EXPLORING | Depth: 1 | Parent: root*
