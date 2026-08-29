---
name: recipe-vision
description: Define or update product vision, strategy, outcomes, and NSM
disable-model-invocation: true
---

**Context**: Create or update `docs/product/vision.md` with Product Outcomes, Business Outcomes, NSM, design principles, and strategic priorities.

## Orchestrator Definition

**Execution Protocol**:
1. **Follow the vision flow** defined below
2. **Approval gate**: At `[STOP — BLOCKING]`, present the vision decision and resume after explicit user confirmation

## Workflow

Assess create/update context → define the outcome structure and necessary principles → confirm current priorities → write vision artifacts.

## Execution Decision Flow

### 1. Context Assessment

Input: $ARGUMENTS

| Situation | Mode | Action |
|-----------|------|--------|
| No `docs/product/vision.md` exists | Create | Full vision definition |
| Vision exists, triggered by reflection | Update | Review and update specific sections |
| Vision exists, strategic pivot | Update | Re-evaluate outcomes and priorities |

### 2. Vision Definition

Use `references/vision-template.md` to structure the vision:

#### New Product (Create Mode)
1. **Product Vision**: What does this product aspire to become? Use the shortest statement that preserves the decision
2. **Design Vision**: How should the product feel to users?
3. **Business Outcomes**: What business results does the product contribute to?
4. **Product Outcomes**: What team-controllable product goals drive those business results?
5. **NSM**: What single metric connects Product Outcomes to Business Outcomes?

#### Existing Product (Update Mode)
1. Review current vision against recent learnings (`docs/product/learnings.md`)
2. Assess whether Product Outcomes are still the right targets
3. Evaluate NSM — still the right connecting metric?
4. Update specific sections based on trigger

### 3. Design Principles

Define or review the smallest non-overlapping set of product-specific design principles needed to resolve recurring trade-offs:
- Each principle should resolve a specific design trade-off
- Principles guide all design decisions across the product
- Write to `docs/product/design-principles.md`

### 4. Strategic Priorities

Define current cycle priorities:
- Map priorities to Product Outcomes
- Identify key Opportunities per priority
- Document strategic bets (outcome-level hypotheses)

**[STOP — BLOCKING]** Present complete vision to user for confirmation:
- Product vision and design vision
- Outcome structure (Business → Product → NSM)
- Design principles
- Strategic priorities for current cycle
- Strategic bets with confidence levels

Write the files after explicit user confirmation.

### 5. File Output

After user approval:
- Write or update `docs/product/vision.md`
- Write or update `docs/product/design-principles.md`
- Create `docs/product/learnings.md` when the first learning is ready to record

## Scope Boundaries

**Included**: Vision definition, outcome structure, NSM, design principles, strategic priorities
**Not included**: Opportunity discovery, persona definition, reflection/distillation

## Completion Criteria

- [ ] The confirmed vision connects Business Outcomes, Product Outcomes, and the NSM
- [ ] Design principles resolve distinct recurring trade-offs and priorities trace to Product Outcomes
- [ ] User-confirmed artifacts are written to `docs/product/`
