# Code to Flow Mapping

## Overview

Maps analyzed code modules to generated flows.

## Flow Type Detection Rules

| Indicator | Flow Type |
|-----------|-----------|
| `*.test.*`, `*.spec.*`, `__tests__/` | TDD |
| `components/`, `*.tsx`, `*.vue`, `templates/` | VDD |
| `README.md`, public exports, API docs | DDD |
| Internal logic, no UI, no public API | SDD |

## Mapping Table

| Code Path | Flow | Type | Action | Status | Notes |
|-----------|------|------|--------|--------|-------|
| app/modules/pjsip.js | flows/sdd-sip-core/ | SDD | CREATED | DRAFT | Core SIP logic, internal service |
| app/modules/pjsip.js | flows/adr-001-sip-library/ | ADR | CREATED | DRAFT | Library selection decision |
| app/modules/app.js | flows/sdd-sip-core/ | SDD | UPDATED | DRAFT | App initialization references |
| app/screens/CallScreen/ | flows/sdd-sip-core/ | SDD | UPDATED | DRAFT | Call UI integration |
| app/components/call/** | flows/sdd-sip-core/ | SDD | UPDATED | DRAFT | Call action components |

### Action Values
- **CREATED** - New flow created
- **UPDATED** - Existing flow appended to (additive changes only)
- **UNCHANGED** - Flow exists, no new information found
- **CONFLICT** - Analysis contradicts existing documentation (needs reconciliation)

## ADR Mapping

| Code Pattern | ADR | Type | Status |
|--------------|-----|------|--------|
| react-native-sip2 import | flows/adr-001-sip-library/ | constraining | DRAFT |
| UDP transport default | (pending) | constraining | - |
| Redux for SIP state | (pending) | enabling | - |
| CallKit single-call limitation | (pending) | constraining | - |

## Unmapped (needs manual review)

| Code Path | Reason |
|-----------|--------|
| app/containers/dialer/ | Navigation flow, user-facing |
| app/containers/history/ | Navigation flow, user-facing |
| app/containers/settings/ | Settings UI, user-facing |
| app/components/common/ | Reusable UI components |
| app/assets/ | Styles, images - VDD candidate |
| app/utils/ | Utility functions - low priority |

---

*Auto-generated. Update as analysis progresses.*
