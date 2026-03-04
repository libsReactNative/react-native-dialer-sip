# Understanding: UI Components

> Reusable component library for call, settings, and common UI elements.

## Phase: EXPLORING

## Sources

- app/components/call/** - Call-specific components (analyzed in call-management)
- app/components/common/** - Reusable components
- app/components/settings/** - Settings-specific components
- app/components/viewport/** - Viewport wrappers

## Validated Understanding

**Component Structure:**
```
app/components/
├── call/                    ← Analyzed in call-management
│   ├── CallActions/
│   ├── CallControls/
│   ├── CallInfo/
│   ├── CallAvatar/
│   ├── CallState/
│   ├── Keypad/
│   ├── KeypadWithActions/
│   ├── TransferModal/
│   ├── DtmfModal/
│   ├── IncomingCallModal/
│   └── ...
├── common/
│   ├── Header/
│   ├── ListCheckbox/
│   ├── ListCustomField/
│   ├── ListFieldSeparator/
│   ├── ListSection/
│   ├── ListSelectField/
│   ├── ListTextField/
│   ├── ViewPager/
│   ├── Touchable.android.js
│   └── Touchable.ios.js
├── settings/
│   ├── ListAccountInfo/
│   └── ListConfigurationInfo/
└── viewport/
    └── ...
```

**Common Components:**

| Component | Purpose |
|-----------|---------|
| Header | Screen header with title, back button |
| List* | List form components for settings screens |
| ViewPager | Swipeable pager (used in CallActions) |
| Touchable | Platform-specific touchable wrapper |

**Settings Components:**

| Component | Purpose |
|-----------|---------|
| ListAccountInfo | Display SIP account info in list |
| ListConfigurationInfo | Display configuration info |

**Component Pattern:**
```javascript
// Typical component structure
import React, {Component} from 'react'
import PropTypes from 'prop-types'
import {View, Text, TouchableOpacity, Image} from 'react-native'
import s from './styles'

export default class ComponentName extends Component {
  // ... props, state, handlers
  
  render() {
    return (
      <View style={s.container}>
        {/* ... */}
      </View>
    )
  }
}

ComponentName.propTypes = {
  // ... prop types
}
```

**Styling:**
- Per-component styles (styles.js or s.js)
- Global container styles in app/assets/styles/containers.js

## Key Insights

1. **Component library**: Well-organized reusable components
2. **Platform-specific**: Touchable has .android.js and .ios.js variants
3. **List pattern**: Settings use consistent List* components
4. **Call component richness**: Most sophisticated components are for call UI

## Flow Recommendation

- **Type**: VDD (component library documentation)
- **Confidence**: medium
- **Rationale**: Reusable components benefit from visual documentation

---

*Phase: EXPLORING | Depth: 1 | Parent: root*
