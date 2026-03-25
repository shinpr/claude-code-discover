---
name: blueprint-standards
description: Defines structural design artifact formats — information architecture, user flows, content model, brand direction, and AI interaction model. Use when creating or reviewing structural design documents that precede prototype generation.
disable-model-invocation: true
---

# Blueprint Standards

## Purpose

Blueprint artifacts define the **structural foundation** that prototypes and UI specifications build upon. They bridge the gap between validated opportunities and tangible product design.

Blueprint artifacts answer: "What pages exist, how do users move between them, what data lives where, and what does the product feel like?"

## Artifact Overview

| Artifact | Question It Answers | Template |
|----------|-------------------|----------|
| Information Architecture | What pages exist and how are they organized? | `references/ia-template.md` |
| User Flows | How do users move through the product to achieve goals? | `references/flow-template.md` |
| Content Model | What data types exist and how do they relate? | `references/content-model-template.md` |
| Brand Direction | What does the product look and feel like? | `references/brand-direction-template.md` |
| AI Interaction Model | How does the user interact with AI features? | `references/ai-interaction-model-template.md` |

## When Blueprint Artifacts Are Required

Blueprint artifacts provide the structural context that makes prototypes coherent across multiple hypotheses. Create them before generating prototypes.

## Relationship to Other Artifacts

```
docs/product/vision.md              ← Strategic intent
docs/product/design-principles.md   ← Trade-off resolutions
docs/product/personas/              ← Who uses it
docs/discovery/opportunities/       ← What problems to solve
docs/discovery/hypotheses/          ← How to solve them
                ↓
docs/product/design/                        ← Blueprint (structural design)
                ↓
docs/discovery/prototypes/          ← Tangible validation artifacts
                ↓
docs/prd/                           ← Implementation specification
```

## Blueprint Scope

**Blueprint defines**: Structure, navigation, data relationships, visual direction, interaction patterns
**Blueprint defers**: Pixel-level specifications, component APIs, responsive breakpoint details, design token values → these belong to UI Spec (implementation phase)

## Key Principles

- **Opportunity-grounded**: Every page in the IA traces to a validated Opportunity or a supporting function
- **Persona-informed**: Flows are written from the perspective of specific personas
- **Consistent across prototypes**: Brand direction and IA provide shared context that all prototypes reference
- **Updatable through reflection**: Blueprint artifacts evolve as new learnings surface in `docs/product/learnings.md`
- **Minimal viable structure**: Define enough to make prototypes coherent, defer details that require implementation-phase decisions
