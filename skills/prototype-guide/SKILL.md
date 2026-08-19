---
name: prototype-guide
description: Generates self-contained HTML prototypes with design context from project files. Read design principles, personas, and hypothesis files, then produce a working prototype for Usability and Value risk validation. Use when creating prototypes or validating through tangible artifacts.
disable-model-invocation: true
---

# Prototype Generation Guide

## Purpose

Prototypes are **hypothesis validation tools**, not final implementations. They test Usability and Value risks by making ideas tangible enough for evaluation.

## Output Format

Generate a **single self-contained HTML file** in `docs/discovery/prototypes/`. The file must:
- Open directly in a browser (double-click) with no build step
- Include all CSS and JavaScript inline
- Use mock data instead of real APIs

Choose the smallest browser-native implementation that makes the validation boundary observable. Use an external CSS or font resource only when a supplied design decision requires it and the prototype remains directly openable; a library choice is not part of the validation outcome.

## Design Context Injection

Before generating, read the target hypothesis and the source artifacts whose decisions can change the tested flow:

1. **Design Principles** — read `docs/product/design-principles.md`
2. **Persona** — read relevant file from `docs/product/personas/`
3. **Hypothesis Under Test** — read the target hypothesis file from `docs/discovery/hypotheses/`
4. **Vision** — read `docs/product/vision.md` for tone and value proposition

Prefer these canonical paths but accept equivalent supplied evidence. These sources drive only the decisions they actually govern. Use their content directly; do not replace missing evidence with plausible product prose. Inspect another artifact only when it can change the tested interaction.

### Blueprint Context (include when `docs/product/design/` exists)

Read only artifacts from `docs/product/design/` that can change the tested navigation, entities, flow, interaction, or visual direction. When present and relevant, an approved brand decision overrides ad-hoc aesthetic inference.

### Additional Context (include when available)

5. **State Design** — which states to demonstrate (Loading / Empty / Error / Partial / Success)
6. **Accessibility Requirements** — WCAG 2.2 AA baseline
7. **Existing Components** — use codebase-analyzer to identify reusable components if a codebase exists
8. **Journey Position** — where in the user journey this interaction occurs

## Design System Integration

How to connect prototypes with your design system depends on your setup:

- **In-Repository Components**: Use codebase-analyzer to identify existing components, reference their visual patterns
- **Tailwind Config / Design Tokens**: Apply existing token definitions
- **No DS Yet**: Define constraints (palette, typography, spacing) — record decisions for future DS

## Key Principles

- **Prototype to learn**: Stop polishing when the hypothesis is observable and the UI is credible enough to interpret the result
- **Context from files, not assumptions**: Read the project files rather than inventing context
- **One hypothesis per prototype**: Keep focused on a single question
- **One validation question per prototype**: One artifact is sufficient unless the hypothesis explicitly requires a pattern comparison
- **Flows, not just screens**: Implement step-by-step user flows, not isolated UI states
- **States, not just features**: Apply the authoritative State Design rule from product-principles and the prototype implementation boundary in `references/prototype-prompt-guide.md`
- **Concrete data**: Use realistic sample data and actual UI copy in the product's language
- **Save validation evidence**: Store the prototype and evidence required to interpret its result; add a screenshot or auxiliary artifact only for a named validation consumer
- **Iterate from evidence**: Reuse a previous prototype when it preserves the current validation boundary

For detailed construction patterns, state design guidance, and scope boundaries, see `references/prototype-prompt-guide.md`.
