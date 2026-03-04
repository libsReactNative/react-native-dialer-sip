# Understanding: React Native SIP Dialer

> Entry point for recursive understanding. Children are top-level logical domains.

## Phase: COMPLETE

## Project Overview

React Native SIP dialer application built with Redux state management and react-native-sip2 library for VoIP communication. The app provides calling functionality with support for multiple SIP accounts, call management, and settings configuration.

**Key Technologies:**
- React Native 0.61.5
- Redux + Redux Thunk for state management
- react-native-sip2 (PJSIP wrapper) for SIP/VoIP calls
- react-native-deprecated-custom-components for navigation
- Platform-specific implementations (iOS/Android)

## Identified Domains

> Logical domains discovered. Each becomes a child directory for deeper exploration.

| Domain | Hypothesis | Priority | Status |
|--------|------------|----------|--------|
| sip-core | SIP endpoint management, accounts, calls | high | ✅ COMPLETE |
| call-management | Call lifecycle, actions, state handling | high | ✅ COMPLETE |
| navigation | App routing, screen transitions, back stack | high | ✅ COMPLETE |
| ui-components | Reusable UI components for calls, settings, dialer | medium | ✅ COMPLETE |
| screens | Screen implementations (CallScreen, LaunchScreen, Settings) | medium | ✅ COMPLETE |
| state-management | Redux store, reducers, actions | high | ✅ COMPLETE |
| push-notifications | VoIP push notifications for incoming calls (iOS) | medium | ✅ COMPLETE |

## Source Mapping

> Which source paths map to which logical domains

| Source Path | -> Domain |
|-------------|----------|
| app/modules/pjsip.js | sip-core |
| app/modules/app.js | state-management |
| app/modules/navigation.js | navigation |
| app/modules/index.js | state-management |
| app/containers/** | screens |
| app/components/call/** | ui-components (call) |
| app/components/common/** | ui-components (common) |
| app/components/settings/** | ui-components (settings) |
| app/screens/** | screens |
| app/utils/** | ui-components |
| app/index.js | state-management |
| app/configureStore.js | state-management |

## Cross-Cutting Concerns

> Things that span multiple domains (may become ADRs)

- **Platform-specific behavior**: iOS vs Android differences in push notifications, Touchable components
- **State persistence**: Application state is not persistent when User close app
- **Multiple call handling**: Support for multiple SIP accounts but single active call (CallKit limitation)
- **Background registration**: VoIP push notifications trigger re-registration when app in background
- **Navigation deprecation**: Using deprecated Navigator library, migration risk

## Children Spawned

```
All 7 domains completed:
- sip-core ✅
- call-management ✅
- navigation ✅
- state-management ✅
- screens ✅
- ui-components ✅
- push-notifications ✅ (integrated with sip-core)
```

## Synthesis

> Updated after all children complete

### From sip-core (completed)
- Handles all SIP protocol operations via react-native-sip2
- Manages account lifecycle (create, delete, register) and call operations (make, answer, hold, transfer)
- Integrates with iOS VoIP push notifications for background incoming calls
- Uses Redux for centralized state management (accounts/calls maps)
- **Key insights**: State not persistent, CallKit single-call limitation, hardcoded credentials (security concern)
- **Flows generated**: SDD (sdd-sip-core), ADR (adr-001-sip-library)

### From call-management (completed)
- CallScreen manages call lifecycle with animated UI transitions
- ViewPager with call actions (mute, speaker, hold, transfer, DTMF)
- Multi-call handling with parallel call info strips and incoming call modal
- Promise-based call initialization with loading state
- **Flows generated**: VDD (vdd-call-ui)

### From navigation (completed)
- Custom Navigator wrapper (react-native-deprecated-custom-components) with Redux state
- 5 navigation actions (goTo, goBack, goAndReplace, open/closeDrawer)
- Scene rendering via switch statement mapping routes to components
- **Key insight**: Deprecated library (migration risk), commented react-navigation imports
- **Flows generated**: SDD (sdd-navigation)

### From state-management (completed)
- Simple Redux store with 3 reducers (navigation, app, pjsip)
- Thunk middleware for async actions
- app/DESTROY preserves navigation, clears other state
- No persistence layer (state lost on restart)

### From screens (completed)
- Viewport pattern: iOS-specific Screen + platform-agnostic Viewport
- 9 screens total: Launch, Call, Account, NetworkSettings, MediaSettings, Conversations, Dialer, History, Settings
- CallScreen most complex, others simpler configuration/display

### From ui-components (completed)
- Well-organized component library (call/, common/, settings/)
- Call components: Most sophisticated (analyzed in call-management)
- Common components: Header, List*, ViewPager, Touchable (platform-specific)

### From push-notifications (completed - integrated with sip-core)
- iOS VoIP push notifications via react-native-voip-push-notification
- Token management (voip, im) in Redux state
- Background registration on push received
- Documented in sdd-sip-core

---

*All domains analyzed | BFS Traversal Complete*
