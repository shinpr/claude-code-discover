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

Every user-facing requirement records each state as `required` or `not_applicable` with a scope-based reason. Write an AC for every required state:

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
- **Complete**: Covers the full behavior including edge cases

### Required Form
- Use concrete values ("within 2 seconds", "maximum 50 characters")
- Specify error handling and recovery
- Include accessibility requirements where relevant
- Reference design states (loading, empty, error)

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
- **4 Risks** → ACs collectively cover all four risk dimensions
- **Design States** → the requirement records all five dispositions and ACs specify behavior for each required state
