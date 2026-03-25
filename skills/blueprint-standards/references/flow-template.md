# User Flow Template

## Flow: {flow-name}

### Overview

- **Persona**: {persona name}
- **Goal**: {what the user is trying to accomplish}
- **Linked Opportunity**: {OPP-NNN}
- **Entry condition**: {how/why the user starts this flow}
- **Success outcome**: {what "done" looks like for the user}

### Steps

| # | Action | Page/Screen | System Response | Next Step |
|---|--------|-------------|----------------|-----------|
| 1 | {user action} | {page} | {what happens} | → 2 |
| 2 | {user action} | {page} | {what happens} | → 3 or → 2a |
| 2a | {alternative path} | {page} | {what happens} | → 3 |
| ... | | | | |

### Decision Points

| At Step | Condition | Path A | Path B |
|---------|-----------|--------|--------|
| {step#} | {condition} | {action → step} | {action → step} |

### Error Scenarios

| At Step | Error | User Sees | Recovery Path |
|---------|-------|-----------|--------------|
| {step#} | {what goes wrong} | {error message/state} | {how to recover} |

### Flow Diagram

```
[Entry] → [Step 1] → [Step 2] → [Decision?]
                                    ├─ Yes → [Step 3] → [Success]
                                    └─ No  → [Step 2a] → [Step 3]
```

### Notes

- **Assumptions**: {assumptions this flow makes about user state, data availability}
- **Open questions**: {unresolved design decisions}
