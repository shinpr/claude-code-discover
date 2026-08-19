# Prototype Construction Guide

## Purpose

Guide for constructing HTML prototypes with proper design context injection. Prototypes validate Usability and Value risks — without reading project context files, they validate nothing.

## Construction Principles

### Read Context First, Build Second

Before writing any code, read the project files specified in the parent skill. Extract:
- Design principles and their trade-off resolutions
- Persona characteristics (role, context, pains, JTBD)
- Hypothesis success/failure criteria
- Product vision and tone

### Be Specific in Implementation

Specific implementation produces testable prototypes.

| Aspect | Effective approach |
|--------|-------------------|
| Layout | Specific max-width, spacing, and composition derived from design principles |
| States | All relevant states with transitions (see State Coverage section) |
| Data | Realistic mock data in the product's language with concrete structure |
| Copy | Actual UI text matching persona's context and the product's language |

### Describe Interactions as State Transitions

Every interactive element has observable state behavior. Implement the states that can occur in the tested path and record the remaining state dispositions:
- Default state
- Hover / focus state
- Loading state (with animation)
- Success state (with feedback)
- Error state (with recovery path)

### One Prototype, One Hypothesis

Each prototype tests one hypothesis. If multiple things need testing, generate separate prototypes. Bundling reduces the validity of each test.

## Prototype Structure

### Minimum Observable Structure

Implement the interaction and source-backed entry/exit context needed to observe the hypothesis. Add product chrome, value-proposition copy, social proof, or related data only when a real user in the tested context would see it and it affects interpretation of the result.

### State Coverage

Apply the authoritative State Design rule from product-principles: record Loading, Empty, Error, Partial, and Success as `required` or `not_applicable` with a reason. Implement Success and every failure or absence state whose occurrence or recovery can distinguish the hypothesis's success, failure, or inconclusive criteria.

### Design Quality

Prototypes must be legible, accessible, and coherent with approved product evidence. Apply supplied visual decisions directly. Where evidence is silent, choose minimal readable typography, semantic color, and spatial hierarchy. Add motion or surface treatment only when it communicates a tested state or approved brand behavior; respect reduced-motion preferences. Resolve only visual properties that affect interpretation of the test.

### Mock Data Guidelines

- Simulate a deterministic delay only when loading behavior is required by the tested path
- Use data that matches the product's domain and language
- Handle edge cases in input (flexible parsing over strict validation)
- Include enough data to demonstrate the interaction pattern

## Prototype Scope Boundaries

**Include in prototypes:**
- UI/UX specifications (layout, components, interactions)
- User flows (step-by-step journeys)
- Visual design (colors, fonts, spacing)
- Mock data (inline JavaScript objects)
- State transitions required to observe the hypothesis; animation only when it communicates that transition
- Keyboard navigation and accessibility attributes

**Replace with mocks:**
- Backend → Hardcoded arrays and setTimeout
- Database → Inline JSON structures
- API endpoints → Mock functions with simulated delay
- Authentication → Mock state (boolean)
- Third-party APIs → Static placeholder data

## File Naming

Save prototypes as:
```
docs/discovery/prototypes/hypo-{id}-prototype.html
```

## Quality Checklist

- [ ] The product decisions that control the tested interaction were read from their source artifacts and reflected in the prototype
- [ ] The UI targets the evidenced persona or user context without invented behavior
- [ ] Hypothesis success/failure criteria are testable through the prototype
- [ ] User flow is implemented step-by-step (not separate pages)
- [ ] All five states have a disposition and every required state is implemented with its transition
- [ ] Mock data is realistic and in the product's language
- [ ] Accessibility: keyboard navigable, WCAG AA contrast, aria attributes
- [ ] Single self-contained HTML file, opens in browser without build step
- [ ] Saved to `docs/discovery/prototypes/`
