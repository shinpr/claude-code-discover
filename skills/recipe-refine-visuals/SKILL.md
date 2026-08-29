---
name: recipe-refine-visuals
description: Optional side-workflow for design experts to refine Concrete Tokens in brand-direction.md when a named downstream consumer needs reproducible values
disable-model-invocation: true
---

**Context**: Refine the concrete tokens used by a named prototype or downstream design consumer. The output remains `docs/product/design/brand-direction.md` so consumers read one approved source.

## When to Use

- `brand-direction.md` contains concrete tokens, or the user names a consumer that now requires them
- A design expert wants to refine the values that affect that consumer

## Orchestrator Definition

**Execution Protocol**:
1. **Follow the refinement flow** defined below
2. **Approval gate**: At `[STOP — BLOCKING]`, present the token decision and resume after explicit user confirmation

## Workflow

Read the approved direction and named consumer → review affected tokens → confirm retain/refine decisions → update the shared brand direction when values change.

## Execution Decision Flow

### 1. Context Reading

**Gate: Approved brand direction and a named consumer requiring concrete values must be inspectable. Existing tokens may be refined; absent tokens may be added only for that consumer. Return the exact missing decision when either input is unavailable.**

Read:
- `docs/product/design/brand-direction.md` — Design Intent, Decision-Relevant Direction, and current Concrete Tokens when present
- `docs/product/design-principles.md` — trade-off context
- `docs/product/personas/` — audience context
- A referenced product only when its current design can change a token under review

### 2. Token Review

Present the current or required tokens that affect the named consumer, showing:
- Current value and its derivation source
- How it traces to a Decision-Relevant Direction row or other governing evidence
- Any inconsistencies between tokens (e.g., contrast ratio issues between text and surface colors)

Stop the review when remaining token changes cannot affect accessibility, approved direction, or the named consumer.

### 3. Expert Refinement

Guide the expert through only the token categories selected for refinement:

#### Color Tokens
- Present current palette as a visual summary (hex values with role labels)
- Ask: which values to keep, which to override
- Validate applicable text and surface token pairs against the WCAG AA contrast boundary
- Validate color harmony across the full palette

#### Typography Tokens
- Present current font selections with their source and language availability
- Ask for font, size, or weight changes that affect the consumer
- Validate: heading/body contrast is sufficient for hierarchy
- Validate: selected fonts support the product's language(s)

#### Spacing Tokens
- Present current scale with the base unit
- Ask for spacing changes that affect the consumer
- Validate: scale produces enough differentiation between levels

For each override, record the expert's rationale in the Decisions Log.

**[STOP — BLOCKING]** Present the refined token set to user for confirmation:
- Side-by-side comparison: previous vs. proposed values
- Rationale for each change
- Contrast and harmony validation results

Update the file after explicit user confirmation.

### 4. File Update

After user approval:
- Keep `brand-direction.md` unchanged when the expert confirms the current tokens already satisfy the named consumer
- When values change:
  - Update or add the `Concrete Tokens — Only When a Consumer Requires Them` section in `docs/product/design/brand-direction.md`
  - Record `expert-refined` and the governing direction in each refined token's `Derived From` value
  - Add override entries to the `Decisions Log`

## Scope Boundaries

**Included**: Consumer-required Concrete Token refinement within the existing brand-direction.md
**Not included**: Changing Design Intent or Decision-Relevant Direction, component-level specifications, responsive breakpoints

## Completion Criteria

- [ ] Reviewed tokens affect the named consumer and retain their derivation context
- [ ] Applicable accessibility and coherence checks pass; an evidence-backed no-change result is valid
- [ ] User-confirmed changes carry `expert-refined` provenance and appear in the Decisions Log
