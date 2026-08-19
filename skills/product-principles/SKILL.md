---
name: product-principles
description: Defines 4 Risks confidence thresholds, OST hierarchy levels, Knowledge Pyramid tiers, and state design requirements. Use when evaluating user stories, setting confidence scores, referencing OST levels, scoping MVP, or determining validation sufficiency.
disable-model-invocation: true
---

# Product Management Principles

## Core Philosophy

1. **Hypothesis Until Proven**: Every assumption is a hypothesis until validated with evidence. Treat unvalidated ideas as hypotheses, not facts
2. **Value Traceability**: From hypothesis to validation to user story to PRD to implementation to test — maintain traceability across the entire chain
3. **Feedback Accumulation**: Every outcome (including failures) remains a learning asset. Preserve invalidated hypotheses for future decisions
4. **Validated Enough**: Use cost x risk x reversibility to determine the sufficient confidence threshold
5. **Artifacts Over Notes**: Intermediate analysis (market research, competitive landscape, brainstorming) is conducted within the conversation and synthesized into the designated artifact. Each recipe defines its output locations

## Opportunity Solution Tree (OST) Hierarchy

All product work follows this hierarchy:

```
Outcome
  ├── Product Outcome (team-controllable product goals)
  │     NSM connects Product Outcome ↔ Business Outcome
  └── Business Outcome (business results Product Outcome contributes to)

Product Outcome
  └── Opportunity (user problems, needs, desires)
        └── Solution (approaches to address the opportunity = feature candidates)
              └── Assumption (premises underlying the solution = hypotheses)
                    └── Experiment (methods to validate the hypothesis)
```

### Level Definitions

| Level | Granularity | Artifact | Description |
|-------|-------------|----------|-------------|
| Business Outcome | Largest | `docs/product/vision.md` | Business results the product contributes to |
| Product Outcome | Large | `docs/product/vision.md` | Team-controllable product goals |
| Opportunity | Large | `docs/discovery/opportunities/` | User problems, needs, desires |
| Solution | Medium | PRD (`docs/prd/`) | Feature candidates addressing an Opportunity |
| Assumption | Small | `docs/discovery/hypotheses/` | Premises underlying a Solution |
| User Story | Smallest | Within PRD | Minimum unit of value with all 4 Risks validated |

## 4 Risks (Authoritative Definition)

A user story is the **minimum unit of value**. All four risks must be **sufficiently validated**:

- **Value** — Will users use/buy this? Does it solve their problem?
- **Usability** — Can users figure out how to use it? Does the UX work?
- **Feasibility** — Can we build it technically? Is the effort realistic?
- **Viability** — Does it work as a business? Can we explain why we're building it?

## Confidence Meter (Authoritative Definition)

Track confidence per risk dimension (0-10):

| Score | Meaning | Typical Evidence |
|-------|---------|------------------|
| 0-2 | Gut feeling / no evidence | Assumption only |
| 3-4 | Structured evaluation | Expert review, competitive analysis, scoring |
| 5-7 | Data-backed | Analytics, surveys, interview patterns |
| 8-10 | Tested and confirmed | Prototype validation, A/B test, beta results |

### Threshold by Cost x Risk x Reversibility

| Condition | Confidence Needed | Evidence Level |
|-----------|-------------------|----------------|
| Low-cost, reversible (feature flag, gradual rollout) | 3-4 | Structured evaluation |
| Medium cost | 5-7 | Data |
| High-cost, irreversible (platform change, pricing change) | 8+ | Test results |

PRDs must show each user story's **current confidence and remaining risks**. Enable PO/DRI to judge "validated enough for delivery", not just "fully validated".

## Knowledge Pyramid (Authoritative Definition)

Knowledge is organized in three tiers to manage context as hypotheses accumulate:

| Tier | Scope | Location | Loading |
|------|-------|----------|---------|
| **Tier 1** | Distilled product principles | `docs/product/learnings.md` | Always (via this skill) |
| **Tier 2** | Opportunity-level learnings | Each Opportunity file's "Tier 2 Learnings" section | When working on that Opportunity |
| **Tier 3** | Individual hypothesis files | `docs/discovery/hypotheses/` | On demand |

Tier 1 learnings are validated patterns supported by independent evidence across the contexts in which the principle claims to hold. Treat them as established only within those recorded conditions.

Distillation criteria (enforced by knowledge-distiller):
- **Independent evidence**: Promotion requires more than one retelling of the same observation; evidence independence and quality matter more than a fixed count
- **Context coverage**: Evidence must cover the segments or conditions named by the proposed learning; additional segment research requires a current decision it can change
- **Contradiction handling**: Conflicting evidence remains recorded with its conditions
- **Freshness tags**: Tier 1 learnings record `last-validated`; re-check when a changed environment or current decision makes staleness consequential, not merely because a timer elapsed

## State Design (Authoritative Definition)

Every user-facing interaction must account for each state as `required` or `not_applicable`. A `not_applicable` result includes the scope or behavior reason so omission remains visible without manufacturing irrelevant UI work:

| State | Description |
|-------|-------------|
| **Loading** | Data is being fetched/processed — show progress indicator |
| **Empty** | No data exists yet — guide user to first action |
| **Error** | Something went wrong — explain what happened, offer recovery |
| **Partial** | Some data available, some not — show available, indicate missing |
| **Success** | Normal state with data — primary design focus |

PRDs record all five states for each user-facing requirement and specify behavior for every required state. Prototypes implement Success and every failure or absence state whose occurrence or recovery can distinguish the hypothesis's success, failure, or inconclusive criteria; they record every other state as `not_applicable` with a reason.

## Key Principles for Daily Decisions

- **Solution-Framing Check**: Seek meaningfully different solution classes to test whether an Opportunity is solution-shaped. Stop when further alternatives cannot change that framing judgment. See `references/opportunity-template.md` for Opportunity file structure
- **Outcome Connection**: Preserve the connection to business outcomes while using NSM to balance pure metric-chasing pressure
- **Design is a Perspective, Not a Phase**: Design thinking applies across all processes — discovery, validation, definition, delivery, and reflection
- **Cycle, Not Phases**: Discovery → Validation → Definition → Delivery → Reflection is a continuous cycle. Start from anywhere
- **MVP Scoping**: When transitioning validated hypotheses to a PRD or blueprint, use `references/mvp-definition.md` for the inclusion boundary, explicit exclusions, observable proof, and scope reduction. Use an optional ranking aid only when direct boundary analysis leaves credible candidates tied

## Common Pitfalls (Why These Principles Exist)

These principles exist to counter natural tendencies in product thinking:

- **Solution-Framing Check** counters the tendency to treat the first Solution idea as the Opportunity itself without turning brainstorming volume into required work
- **Confidence Meter (0-10)** counters all-or-nothing thinking about validation. The threshold varies by cost x risk x reversibility because not everything needs the same evidence level
- **Knowledge Pyramid tiers** counter both context overload and knowledge loss. Independent, condition-matched evidence keeps Tier 1 principles grounded without treating observation counts as proof quality
- **State Design** counters the tendency to design only for the happy path. Acceptance criteria that cover only Success state miss the states users encounter most during onboarding
