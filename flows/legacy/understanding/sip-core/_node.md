# Understanding: SIP Core

> PJSIP endpoint management, account lifecycle, and SIP protocol integration.

## Phase: SPAWNING

## Hypothesis

This module handles the core SIP functionality using react-native-sip2 library. Manages:
- Endpoint initialization and lifecycle
- SIP account creation/deletion/registration
- Network connectivity handling
- Service configuration (UA string, STUN servers)

## Sources

- app/modules/pjsip.js - Main SIP logic, endpoint management
- app/modules/app.js - App initialization calling PjSip.init()

## Validated Understanding

**Core Responsibilities:**
1. **Endpoint Management**: Creates new Endpoint instance from react-native-sip2, starts it with configuration
2. **Account Lifecycle**: createAccount, deleteAccount, replaceAccount (not implemented)
3. **Call Operations**: makeCall, hangupCall, answerCall, declineCall, hold/unhold, mute/unmute, transfer, redirect
4. **Event Subscription**: Listens to registration_changed, connectivity_changed, call_received, call_changed, call_terminated, call_screen_locked
5. **Push Notification Integration**: VoIP push notifications for iOS, token management
6. **CallKit Integration**: iOS CallKit for native call UI (partially implemented, commented out)
7. **Network Configuration**: WiFi/3G/Edge/GPRS/Roaming settings
8. **State Persistence**: Redux store for accounts, calls, tokens, connectivity

**Key Patterns:**
- Thunk actions for async operations (dispatch/getState pattern)
- Event-driven architecture (endpoint.on() for SIP events)
- Account map stored in Redux state (keyed by account ID)
- Call map stored in Redux state (keyed by call ID)
- Platform-specific behavior (iOS push notifications, Android simpler flow)

**Configuration Defaults:**
- Transport: UDP (default)
- Registration timeout: 3600 seconds
- Registration on add: true (auto-register)
- Network: useWifi=true, useOtherNetworks=true

## Children Identified

> Deeper concepts spawned during SPAWNING phase

| Child | Hypothesis | Status |
|-------|------------|--------|
| endpoint-lifecycle | Endpoint creation, start, destroy, event subscription | PENDING |
| account-management | Create/delete/replace SIP accounts, contact URI params | PENDING |
| call-operations | Make/answer/hangup/hold/transfer call operations | PENDING |
| registration-handling | Account registration state changes, background registration | PENDING |
| network-configuration | Network settings, connectivity events, useAnyway flag | PENDING |
| push-notification-integration | VoIP tokens, iOS push notification handling | PENDING |

## Dependencies

- **Uses**: react-native-sip2 (Endpoint class), VoipPushNotification, PushNotificationIOS, uuid
- **Used by**: call-management, state-management, screens (CallScreen, DialerViewport)

## Key Insights

1. **State is not persistent**: Application state is lost when app closes (commented in pjsip.js line ~67)
2. **Multiple accounts, single active call**: CallKit limitation noted in code
3. **Background registration**: App re-registers accounts when receiving VoIP push in background
4. **Platform divergence**: iOS has extensive push/CallKit integration, Android simpler
5. **Hardcoded credentials**: Development credentials visible in init() (username: 50363, domain: 172.16.104.17)

## ADR Candidates

1. **react-native-sip2 choice**: Fork/replacement of react-native-pjsip (imported but commented out)
2. **UDP transport default**: Choice over TCP/TLS
3. **Registration timeout**: 3600 seconds (1 hour)
4. **CallKit single-call limitation**: Architecture accepts this constraint
5. **Redux for SIP state**: Centralized state management for accounts/calls

## Flow Recommendation

- **Type**: SDD (internal service logic, no stakeholder-facing docs)
- **Confidence**: high
- **Rationale**: Core infrastructure module, handles SIP protocol internally, no direct stakeholder interaction

## Synthesis

> Updated during SYNTHESIZING phase after children complete

### From Children
[pending]

### Combined Understanding
[pending]

## Bubble Up

> Summary to pass to parent during EXITING

- Handles all SIP protocol operations via react-native-sip2
- Manages account lifecycle and registration
- Provides call control operations (make/answer/hangup/transfer)
- Integrates with iOS VoIP push notifications for incoming calls
- Uses Redux for centralized state management

---

*Phase: SPAWNING | Depth: 1 | Parent: root*
