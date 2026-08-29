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
| 2 | {user action} | {page} | {what happens} | {next step or success} |

### Decision Points

Include decision points that change the route or observable outcome.

| At Step | Condition | Path A | Path B |
|---------|-----------|--------|--------|
| {step#} | {condition} | {action → step} | {action → step} |

### Error Scenarios

Include failures that can occur in the confirmed flow and require user-visible recovery.

| At Step | Error | User Sees | Recovery Path |
|---------|-------|-----------|--------------|
| {step#} | {what goes wrong} | {error message/state} | {how to recover} |

### Flow Diagram

```
[Entry] → [required steps and decision branches] → [Success or recovery]
```

### Notes

- **Assumptions**: {assumptions this flow makes about user state, data availability}
- **Open questions**: {unresolved design decisions}
