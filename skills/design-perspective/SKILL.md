---
name: design-perspective
description: Integrates design principles, WCAG 2.2 AA accessibility, persona context, and state design into product decisions. Use when reviewing UX decisions, checking accessibility, applying design principles, or ensuring state coverage in acceptance criteria.
disable-model-invocation: true
---

# Design Perspective

## Core Philosophy

Design is not a phase — it is a **perspective applied across all product processes**.

| Process | Design's Role |
|---------|--------------|
| Opportunity Discovery | Journey maps, pain point visualization |
| Solution Generation | Design principle-driven ideation |
| Assumption Validation | Prototype generation → usability testing |
| PRD Definition | Usability risk confirmation for user stories |
| Reflection | UX learning accumulation |

## Design Principles Reference

Reference only the product-specific principles from `docs/product/design-principles.md` that can change the current design decision.

Design principles are **product-specific guardrails** that guide all design decisions. They are not generic best practices but choices that reflect this product's values and trade-offs.

## State Design

State Design checks Loading, Empty, Error, Partial, and Success, then specifies the states that can change observable behavior or verification.

In practice:
- PRDs specify applicable state behavior and preserve an exclusion reason when omission would be ambiguous
- Prototypes implement the states needed to test the hypothesis
- User stories addressing Usability risk should consider all relevant states

## Accessibility Standards

**Baseline: WCAG 2.2 AA compliance**

Key requirements:
- **Perceivable**: Text alternatives for non-text content, sufficient color contrast (4.5:1 for normal text, 3:1 for large text), content adaptable to different presentations
- **Operable**: All functionality available via keyboard, sufficient time for interactions, no content that causes seizures, clear navigation mechanisms
- **Understandable**: Readable text, predictable behavior, input assistance for error prevention
- **Robust**: Compatible with assistive technologies, valid markup

Accessibility is a **Usability risk** dimension — factor it into confidence scoring.

## Persona and Context Integration

When they can change the current design decision, reference:
- **Personas** (`docs/product/personas/`) — Who is using this? What's their context, skill level, environment?
- **Journey Maps** (`docs/discovery/journeys/`) — Where in their journey does this interaction happen?

When creating or updating personas, use `references/persona-template.md` for the standard structure (demographics, JTBD, pains/gains, behavioral patterns, validation status).

Design decisions without persona/context grounding are assumptions that need validation.

## Blueprint Integration

When `docs/product/design/` exists, applicable blueprint artifacts provide shared structural context (information architecture, brand direction, content model, user flows, AI interaction model) for prototypes that depend on those decisions.

## Design in Hypothesis Validation

When validating Usability risk through prototypes:
1. Define what "usable" means for this specific user story (tied to persona/context)
2. Identify the interaction path that exposes the hypothesis's success and failure criteria
3. Specify success criteria (task completion rate, time-on-task, error rate)
4. Generate prototype with design context injected (design principles, persona, vision, blueprint artifacts)
5. Record results with specific UX learnings

## Decision Boundary

Apply product-specific principles, applicable state behavior, WCAG 2.2 AA, and evidenced user context. Treat any remaining design choice that can change the validation result or user outcome as an explicit assumption.
