# Acceptance Criteria Guide (EARS Format)

## Purpose

Guide for writing clear, testable acceptance criteria using EARS (Easy Approach to Requirements Syntax) patterns. ACs define when a user story is "done".

## EARS Patterns

### When (Event-driven)
Triggered by a specific event or user action.

```
When [trigger event],
the system shall [expected behavior].
```

**Example:**
```
When the user clicks the "Save" button,
the system shall persist the form data and display a success notification within 2 seconds.
```

### While (State-driven)
Active during a specific system state or condition.

```
While [system state],
the system shall [expected behavior].
```

**Example:**
```
While the application is loading data,
the system shall display a skeleton screen with animated placeholders.
```

### If-Then (Conditional)
Behavior depends on a condition being true or false.

```
If [condition],
then the system shall [expected behavior].
```

**Example:**
```
If the user has not completed onboarding,
then the system shall display the onboarding wizard on login.
```

### Combined Patterns
Complex ACs can combine patterns:

```
When [trigger] while [state],
if [condition],
then the system shall [behavior].
```

**Example:**
```
When the user submits the search form while offline,
if cached results exist,
then the system shall display cached results with a "Results may be outdated" banner.
```

## State-Aware ACs

Check the standard states below and write an AC for each state that can occur and change observable behavior or recovery. Record an exclusion reason only when omission would leave the requirement ambiguous:

| State | AC Pattern |
|-------|-----------|
| **Loading** | While [data is loading], the system shall [show progress indicator] |
| **Empty** | If [no data exists], then the system shall [show empty state with guidance] |
| **Error** | When [operation fails], the system shall [show error with recovery action] |
| **Partial** | While [some data is unavailable], the system shall [show available data and indicate missing] |
| **Success** | When [operation completes], the system shall [confirm and show result] |

## Writing Good ACs

### Characteristics
- **Testable**: Can be verified with a clear pass/fail
- **Specific**: One observable interpretation of expected behavior
- **Independent**: Each AC tests one behavior
- **Complete**: Covers the requirement's applicable state and contract boundaries

### Required Form
- Use concrete values when supplied by governing evidence; otherwise state the observable boundary or unresolved value
- Specify error handling, recovery, accessibility, and design states when activated by the requirement

### Transform Before Use
- Replace vague terms ("quickly", "user-friendly", "intuitive") with an observable threshold or behavior
- Translate implementation details ("using REST API", "with Redux") into the user-visible or contract boundary they serve
- Split multiple behaviors into independently verifiable ACs
- Add only edge and error behavior that can occur within the requirement's state dispositions

## AC in PRD Format

```markdown
- [ ] Requirement: [Description]
  - AC-1: When [trigger], the system shall [behavior]
  - AC-2: If [condition], then the system shall [behavior]
  - AC-3: While [state], the system shall [behavior]
```

## Accessibility ACs

Include accessibility ACs for UI features:

```
When the user navigates using keyboard only,
the system shall support Tab/Shift+Tab for focus movement
and Enter/Space for activation of all interactive elements.

While a screen reader is active,
the system shall announce [component] with role [role]
and accessible name [name].

If the user has set "prefers-reduced-motion",
then the system shall disable all non-essential animations.
```

## Traceability

Each AC should be traceable:
- **User Story** → AC tests a specific aspect of the story's value
- **Design States** → ACs specify every applicable state behavior and any decision-relevant exclusion
