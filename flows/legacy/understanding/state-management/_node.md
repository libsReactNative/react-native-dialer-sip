# Understanding: State Management

> Redux store configuration, reducer composition, and state architecture.

## Phase: EXPLORING

## Sources

- app/modules/index.js - Root reducer with combineReducers
- app/configureStore.js - Store creation with thunk middleware
- app/index.js - App bootstrap, store dispatch

## Validated Understanding

**Architecture:**
```
Redux Store
├── navigation (navigation.js) - Route state, Navigator ref
├── pjsip (pjsip.js) - SIP state, accounts, calls, tokens
└── app (app.js) - App lifecycle (minimal, mostly delegates to pjsip)
```

**Store Configuration:**
```javascript
// configureStore.js
import {createStore, applyMiddleware} from 'redux'
import thunkMiddleware from 'redux-thunk'
import rootReducer from './modules'

export default function configureStore(initialState) {
  const finalCreateStore = applyMiddleware(thunkMiddleware)(createStore)
  return finalCreateStore(rootReducer, initialState)
}
```

**Root Reducer:**
```javascript
const appReducer = combineReducers({
  navigation,
  app,
  pjsip,
})

const rootReducer = (state, action) => {
  if (action.type === 'app/DESTROY') {
    state = { navigation: state.navigation }
  }
  return appReducer(state, action)
}
```

**Key Pattern:** app/DESTROY action preserves navigation state but clears app and pjsip state

**Middleware:**
- redux-thunk: Async actions via dispatch/getState
- redux-logger: Available in dev (in package.json)
- redux-devtools: Available (in package.json)

**State Persistence:**
- No persistence layer configured
- State lost on app restart
- Must re-initialize SIP on every start

## Dependencies

- **Uses**: redux, redux-thunk
- **Used by**: All components via react-redux connect()

## Key Insights

1. **Simple store**: Single store with 3 reducers
2. **Thunk only**: No saga/observable, just thunk for async
3. **No persistence**: In-memory state only
4. **Partial reset**: app/DESTROY preserves navigation
5. **Dev tools**: redux-devtools and redux-logger available

## Flow Recommendation

- **Type**: SDD (infrastructure)
- **Confidence**: high
- **Rationale**: Core infrastructure, internal implementation

---

*Phase: EXPLORING | Depth: 1 | Parent: root*
