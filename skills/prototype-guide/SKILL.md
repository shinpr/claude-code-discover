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
- Use Tailwind CSS via CDN and Google Fonts for typography
- Include all CSS and JavaScript inline
- Use mock data instead of real APIs

## Design Context Injection

Before generating, read the relevant project files to understand the full context:

1. **Design Principles** — read `docs/product/design-principles.md`
2. **Persona** — read relevant file from `docs/product/personas/`
3. **Hypothesis Under Test** — read the target hypothesis file from `docs/discovery/hypotheses/`
4. **Vision** — read `docs/product/vision.md` for tone and value proposition

These files drive every design decision. A prototype built without reading them validates nothing.

### Blueprint Context (include when `docs/product/design/` exists)

Read all available artifacts from `docs/product/design/` (information architecture, brand direction, user flows, content model, AI interaction model). When present, brand direction overrides ad-hoc aesthetic inference from design principles.

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

- **Prototype to learn, not to ship**: Don't over-invest in polish
- **Context from files, not assumptions**: Read the project files rather than inventing context
- **One hypothesis per prototype**: Keep focused on a single question
- **One pattern per prototype**: When multiple patterns need validation, generate a separate prototype for each
- **Flows, not just screens**: Implement step-by-step user flows, not isolated UI states
- **States, not just features**: Implement all relevant state transitions (loading, error, empty, success)
- **Concrete data**: Use realistic sample data and actual UI copy in the product's language
- **Save everything**: Prototypes, screenshots, and learnings go to `docs/discovery/prototypes/`
- **Iterate, don't restart**: Build on previous prototypes

For detailed construction patterns, state design guidance, and scope boundaries, see `references/prototype-prompt-guide.md`.
