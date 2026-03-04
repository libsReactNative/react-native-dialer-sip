# Understanding: Call Management

> Call lifecycle handling, call UI state, and user interactions during calls.

## Phase: SPAWNING

## Hypothesis

This domain handles the call lifecycle from UI perspective - managing call state display, user actions during calls (hold, mute, transfer), and coordinating multiple simultaneous calls.

## Sources

- app/screens/CallScreen/index.js - Main call screen component
- app/screens/CallScreen/anim.js - Call animation logic
- app/components/call/** - Call UI components (controls, info, actions)
- app/modules/pjsip.js - Call operations (makeCall, answerCall, etc.)

## Validated Understanding

**Core Responsibilities:**
1. **Call Screen Lifecycle**: CallScreen component manages call state via Redux, handles Promise-based call initialization
2. **Call UI State**: Animated transitions between call states (incoming, active, terminated) using Animated API
3. **Call Actions**: Two-page ViewPager with actions (add, mute, speaker, transfer, hold, DTMF, park, merge, chat, record)
4. **Call Controls**: Answer/Hangup/Redirect buttons with animated positioning based on call state
5. **Multi-Call Handling**: Displays parallel call info strips, manages incoming call modal during active call
6. **Incoming Call Modal**: Full-screen modal for incoming calls with Answer/Decline actions

**Key Patterns:**
- Animated values for smooth UI transitions between call states
- Call state-based layout calculations (incoming vs active vs terminated)
- ViewPager for paging through action sets
- Platform-agnostic UI (same components for iOS/Android)
- Call object methods: `getState()`, `isMuted()`, `isSpeaker()`, `isHeld()`, `getRemoteNumber()`, `getRemoteName()`

**Call States (PJSIP):**
- `PJSIP_INV_STATE_NULL` - Initial state
- `PJSIP_INV_STATE_CALLING` - Outgoing call
- `PJSIP_INV_STATE_EARLY` - Early media
- `PJSIP_INV_STATE_CONNECTING` - Connecting
- `PJSIP_INV_STATE_CONFIRMED` - Active call
- `PJSIP_INV_STATE_INCOMING` - Incoming call
- `PJSIP_INV_STATE_DISCONNECTED` - Call ended

**UI Layout (animated):**
```
[Call Parallel Info] <- multiple calls
[Call Info]          <- remote name/number
[Call Avatar]        <- large avatar (fades in/out)
[Call State]         <- call status text
[Call Actions]       <- 2-page ViewPager (mute, speaker, hold, transfer, etc.)
[Call Controls]      <- answer/hangup/redirect buttons
```

## Children Identified

> Deeper concepts spawned during SPAWNING phase

| Child | Hypothesis | Status |
|-------|------------|--------|
| call-screen-lifecycle | CallScreen component lifecycle, Promise initialization, Redux connection | PENDING |
| call-ui-state | Animated transitions, state-based layouts, avatar visibility | PENDING |
| call-actions | ViewPager actions, toggle logic (mute/unmute, hold/unhold, speaker/earpiece) | PENDING |
| multi-call-handling | Parallel call info strips, call switching, incoming call during active call | PENDING |
| incoming-call-modal | Modal presentation, Answer/Decline handling | PENDING |

## Dependencies

- **Uses**: sip-core (call operations via Redux), navigation (screen transitions on call end)
- **Used by**: screens (CallScreen is the main screen), ui-components (reusable call components)

## Key Insights

1. **Promise-based call initialization**: Call can be a Promise, screen shows "Please wait" during initialization
2. **Animated state transitions**: All UI elements animate to different positions based on call state
3. **Incoming call overlay**: IncomingCallModal shows during active call for second incoming call
4. **Screen lock support**: `isScreenLocked` prop renders black overlay (privacy feature)
5. **Call end navigation**: After call ends, navigates back or to active call after 3 second delay
6. **ViewPager for actions**: Swipeable action pages, indicator shows current page
7. **Placeholder actions**: park, merge, record actions exist but may not be fully implemented

## ADR Candidates

1. **Animated UI for call states**: Choice to use Animated API vs state-based rendering
2. **ViewPager for actions**: Swipeable actions vs expandable menu
3. **Modal for incoming calls**: Full-screen modal vs inline notification
4. **CallKit single-call UI**: How UI handles CallKit limitation

## Flow Recommendation

- **Type**: VDD (Visual-Driven Development)
- **Confidence**: high
- **Rationale**: Call screen is primary user-facing feature, visual experience critical, heavy use of animations and UI components

## Synthesis

> Updated during SYNTHESIZING phase after children complete

### From Children
[pending]

### Combined Understanding
[pending]

## Bubble Up

> Summary to pass to parent during EXITING

- Manages call UI lifecycle with animated state transitions
- Handles multi-call scenarios with parallel call info and incoming call modal
- Provides comprehensive call actions via ViewPager (mute, hold, transfer, DTMF, etc.)
- Promise-based call initialization with loading state
- Screen lock feature for privacy

---

*Phase: SPAWNING | Depth: 1 | Parent: root*
