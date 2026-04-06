---
name: recipe-refine-visuals
description: Optional side-workflow for design experts to refine auto-derived Visual Tokens in brand-direction.md with professional judgment
disable-model-invocation: true
---

**Context**: Refine the Visual Tokens section of `docs/product/design/brand-direction.md` with design expertise. This recipe reads the existing brand direction (including auto-derived tokens from `recipe-blueprint`) and lets a design expert override specific values with professional judgment. The output is the same `brand-direction.md` file — downstream consumers (prototype-generator, UI Spec) read it without knowing which path produced the tokens.

## When to Use

- After `recipe-blueprint` has completed and `brand-direction.md` exists with auto-derived Visual Tokens
- When a design expert is available and wants to refine the visual system
- **This recipe is entirely optional** — auto-derived tokens are sufficient for prototype generation

## Orchestrator Definition

**Execution Protocol**:
1. **Follow the refinement flow** defined below
2. **Stop at every `[STOP — BLOCKING]` marker** — present findings and CANNOT proceed until user explicitly confirms

## Workflow Overview

```
Input (existing brand-direction.md with auto-derived tokens)
    ↓
1. Context Reading → Read brand direction + design principles + personas
    ↓
2. Token Review → Present current tokens with their derivation rationale
    ↓
3. Expert Refinement → User specifies overrides [Stop: User confirms changes]
    ↓
Output: Updated Visual Tokens in docs/product/design/brand-direction.md
```

## Execution Decision Flow

### 1. Context Reading

**Gate: `docs/product/design/brand-direction.md` must exist with a Visual Tokens section. If missing → inform user to run `recipe-blueprint` first.**

Read:
- `docs/product/design/brand-direction.md` — current direction and auto-derived tokens
- `docs/product/design-principles.md` — trade-off context
- `docs/product/personas/` — audience context
- Reference Products listed in brand-direction — use WebSearch to inspect their current design if needed

### 2. Token Review

Present the current Visual Tokens organized by category, showing:
- Current value and its derivation source
- How it relates to the directional sections above it
- Any inconsistencies between tokens (e.g., contrast ratio issues between text and surface colors)

Highlight areas where expert judgment would have the most impact:
- Color harmony and palette coherence
- Font pairing quality
- Spacing scale appropriateness for the product's density target

### 3. Expert Refinement

Guide the expert through each token category:

#### Color Tokens
- Present current palette as a visual summary (hex values with role labels)
- Ask: which values to keep, which to override
- Validate contrast ratios: `--color-text` against `--color-surface` must meet WCAG AA (4.5:1 for body text)
- Validate color harmony across the full palette

#### Typography Tokens
- Present current font selections with Google Fonts links
- Ask: alternative font pairings, size adjustments, weight preferences
- Validate: heading/body contrast is sufficient for hierarchy
- Validate: selected fonts support the product's language(s)

#### Spacing Tokens
- Present current scale with the base unit
- Ask: base unit adjustment, scale ratio preferences
- Validate: scale produces enough differentiation between levels

For each override, record the expert's rationale in the Decisions Log.

**[STOP — BLOCKING]** Present the refined token set to user for confirmation:
- Side-by-side comparison: auto-derived vs. expert-refined values
- Rationale for each change
- Contrast and harmony validation results

**CANNOT update the file until user explicitly confirms.**

### 4. File Update

After user approval:
- Update the Visual Tokens section in `docs/product/design/brand-direction.md`
- Change Source field from `auto-derived` to `expert-refined`
- Add override entries to the Brand Direction Decisions Log

## Scope Boundaries

**Included**: Visual Token refinement (colors, typography, spacing) within the existing brand-direction.md
**Not included**: Changing directional sections (Tone & Voice, Color Direction, etc.), adding new sections, component-level specifications, responsive breakpoints

## Completion Criteria

- [ ] Existing brand-direction.md read with auto-derived tokens
- [ ] Current tokens reviewed with derivation context
- [ ] Expert overrides collected with rationale
- [ ] Contrast and harmony validated
- [ ] User confirmed refined tokens
- [ ] brand-direction.md updated with source marked as `expert-refined`
- [ ] Decisions logged in Brand Direction Decisions Log
