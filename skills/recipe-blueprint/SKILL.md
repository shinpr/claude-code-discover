---
name: recipe-blueprint
description: Define structural design foundation — information architecture, user flows, content model, brand direction, and AI interaction model — from validated opportunities and hypotheses
disable-model-invocation: true
---

**Context**: Create or update structural design artifacts in `docs/product/design/` that provide shared context for prototype generation and downstream UI specification. Blueprint bridges the gap between "what problems to solve" (discovery) and "what the product looks and works like" (prototypes).

## Orchestrator Definition

**Execution Protocol**:
1. **Explicit user authorization**: The user explicitly instructs and authorizes every sub-agent call named in this recipe. Invoke each named specialist whenever its stated condition applies; the orchestrator does not replace that call with its own analysis
2. **Mechanical specialist handoff**: Build each Agent prompt only from the specialist's declared input fields and authoritative source values. Preserve those values unchanged; do not summarize, paraphrase, supplement, or turn them into narrative instructions
3. **Follow the blueprint flow** defined below
4. **Stop at every `[STOP — BLOCKING]` marker** — present findings and CANNOT proceed until user explicitly confirms

The authorization and mechanical-handoff rules are intentional redundancy against model and system defaults that substitute orchestrator work or fluent restatements for an approved specialist call. Retain them until fresh execution evidence shows the failure no longer occurs.

## Workflow Overview

```
Input (validated opportunities / discovery outputs / strategic update)
    ↓
1. Context Assessment → Determine scope and mode (create vs. update)
    ↓
2. MVP Scope Definition → Feature prioritization from validated hypotheses
    ↓
3. Information Architecture → Page structure, navigation, multi-sided layout [Stop: User confirms IA]
    ↓
4. Content Model → Entity types, relationships, states
    ↓
5. Core User Flows → Smallest set covering the core value loop and confirmed structural boundaries [Stop: User confirms structure]
    ↓
6. Brand Direction → Visual tone, color/typography direction, reference products
    ↓
7. AI Interaction Model → Interaction patterns, capability boundaries, guardrails (if applicable) [Stop: User confirms design direction]
    ↓
Output: docs/product/design/ artifacts
```

## Execution Decision Flow

### 1. Context Assessment

Input: $ARGUMENTS

**Read project context to determine scope:**

| File | Extract |
|------|---------|
| `docs/product/vision.md` | Product vision, design vision, outcomes, NSM, strategic priorities |
| `docs/product/design-principles.md` | Trade-off resolutions that constrain all design decisions |
| `docs/product/personas/` | All persona files — roles, JTBD, pains, behavioral patterns |
| `docs/discovery/INDEX.md` | Opportunity and hypothesis status overview |
| `docs/discovery/opportunities/` | Validated opportunities with impact assessment |
| `docs/discovery/hypotheses/` | Hypothesis status, confidence scores, learnings |
| `docs/discovery/journeys/` | Journey maps (if available) |
| `docs/product/learnings.md` | Tier 1 learnings from reflection cycles |

**Gate: The product vision, design trade-offs, target-user context, and at least one identified Opportunity must be inspectable. Prefer the canonical files above, and treat equivalent supplied or repository evidence as satisfying the same decision. Stop only when a missing product decision changes the IA, content model, user flow, included capability, or brand direction.**

| Situation | Mode | Action |
|-----------|------|--------|
| No `docs/product/design/` exists | Create | Full blueprint definition |
| Blueprint exists, new Opportunities discovered | Update | Extend IA, flows, content model for new scope |
| Blueprint exists, new learnings in `docs/product/learnings.md` | Update | Revise based on new learnings |
| Existing codebase | Create/Update | Invoke codebase-analyzer with `analysis_mode: structural_design` and the relevant Opportunity or blueprint update request as `governing_context` |

### 2. MVP Scope Definition

Use product-principles `references/mvp-definition.md` to select the smallest feature scope that preserves the confirmed outcome, core value loop, required boundary, and observable proof:

1. Inspect only Opportunities and hypotheses that can change the current blueprint
2. Map their candidate capabilities against existing behavior
3. Record the evidence, outcome effect, rough cost, risk, and reversibility for each inclusion
4. Record explicit exclusions and why removing each included capability would break the MVP boundary
5. Use a ranking framework only if credible candidates remain tied and the ranking can change scope

Record the scope in the IA artifact header (Step 3).

### 3. Information Architecture

Use blueprint-standards skill `references/ia-template.md` to structure the IA:

1. **Site map**: Organize pages hierarchically based on MVP scope
   - Every page traces to an Opportunity or a supporting function (authentication, settings, onboarding)
   - Mark each page with its primary persona
2. **Navigation model**: Define global navigation, contextual navigation, and utility navigation
3. **Multi-sided considerations**: For marketplace/platform products, define both sides of the market with their entry pages, core loops, and connection points
4. **Page inventory**: For each page, define purpose, primary persona, key content, entry/exit points

**[STOP — BLOCKING]** Present IA to user for confirmation:
- Site map with page-to-Opportunity traceability
- Navigation model
- Multi-sided structure (if applicable)
- MVP scope summary

**CANNOT proceed to Step 4 until user explicitly confirms the IA structure.**

### 4. Content Model

Use blueprint-standards skill `references/content-model-template.md` to define the data structure:

1. **Entity inventory**: List all content types the product manages, mapped to Opportunities
2. **Entity definitions**: For each entity, define attributes, relationships, and states
3. **Entity relationship diagram**: Show how entities connect
4. **Display contexts**: Where each entity appears in the IA (list view, detail, creation, embedded)

### 5. Core User Flows

Use blueprint-standards skill `references/flow-template.md` to define the smallest flow set that covers the confirmed MVP structure:

1. Identify the highest-impact flows from validated Opportunities and journey maps
2. Write each flow from a specific persona's perspective
3. Include decision points, error scenarios, and alternative paths
4. Reference IA pages — each step maps to a page in the site map

Create a flow only when it changes navigation, entity/state behavior, a persona-specific path, or observable validation. Record each confirmed MVP Opportunity as covered by a flow or as not requiring a distinct flow with a reason. The flow set stops when these boundaries are covered.

Prioritize flows that:
- Cover the core value loop (the primary reason users return)
- Span both sides of the marketplace (if applicable)
- Address the highest-confidence Opportunities first

**[STOP — BLOCKING]** Present content model and user flows to user for confirmation:
- Entity overview with relationships
- Core flow list with persona assignments
- Flow details sized by the confirmed structural boundaries

**CANNOT proceed to Step 6 until user explicitly confirms the structural design.**

### 6. Brand Direction

Use blueprint-standards skill `references/brand-direction-template.md` to record only visual decisions a prototype or downstream design consumer needs. Start with tone, semantic color, readable type hierarchy, and density when those decisions are not already supplied. Add motion, texture, reference products, or concrete tokens only when product evidence or a real consumer makes them decision-relevant. Browse or derive a token system only when it can change a current decision for that consumer.

> **Note**: When a named downstream consumer requires concrete values, design experts can add or refine Concrete Tokens using `recipe-refine-visuals`. The refinement updates the same `brand-direction.md` file.

### 7. AI Interaction Model

Skip this step if the product has no AI-powered features.

Use blueprint-standards skill `references/ai-interaction-model-template.md` to define:

1. **AI features inventory**: Map each AI feature to its user goal, AI role, interaction pattern, and linked Opportunity
2. **Interaction pattern decisions**: For each feature — chat vs. form vs. inline vs. hybrid, UI placement, user control model
3. **Capability boundaries**: What AI reliably handles vs. known limitations, with fallbacks
4. **Response display strategy**: How to show AI output based on response time (streaming, progressive, staged)
5. **Error taxonomy**: Generation failure, inappropriate output, timeout, low confidence — each with user-visible behavior and recovery
6. **Human-AI handoff**: The boundary between AI-generated and human-edited content
7. **Guardrails**: Content safety, scope limitation, quality gates

**[STOP — BLOCKING]** Present brand direction and AI interaction model to user for confirmation:
- Tone & voice positioning
- Current decision-relevant visual direction
- Concrete tokens only when a downstream consumer requires reproducible values
- AI interaction pattern decisions
- Capability boundaries and guardrails

**CANNOT write files until user explicitly confirms the design direction.**

### 8. File Output

After user approval, write the confirmed artifact set to `docs/product/design/`:

- `docs/product/design/information-architecture.md`
- `docs/product/design/content-model.md`
- `docs/product/design/brand-direction.md`
- `docs/product/design/ai-interaction-model.md` (if applicable)
- `docs/product/design/flows/flow-{name}.md` (one file per flow)

## Sub-agent Usage

| Agent | When | Why (context separation benefit) |
|-------|------|----------------------------------|
| codebase-analyzer (via Agent tool, subagent_type: "discover:codebase-analyzer") | Existing codebase exists | Independent evidence about current architecture, routes, and components |

## Scope Boundaries

**Included**: Information architecture, user flows, content model, brand direction, AI interaction model, MVP scope synthesis
**Not included**: Opportunity discovery, hypothesis validation, pixel-level design specifications (UI Spec scope), component APIs and final production token values (UI Spec scope), PRD creation

## Completion Criteria

- [ ] Project context read (vision, principles, personas, opportunities)
- [ ] MVP scope synthesized from validated hypotheses
- [ ] Information architecture defined with Opportunity traceability
- [ ] User confirmed IA
- [ ] Content model defined with entity relationships
- [ ] Core user flows cover the core value loop and each structurally distinct confirmed MVP path without a fixed count
- [ ] User confirmed structural design
- [ ] Brand direction defined with design principle traceability
- [ ] Any concrete tokens have an identified consumer and trace to the approved direction
- [ ] AI interaction model defined (if applicable)
- [ ] User confirmed design direction
- [ ] All artifacts written to `docs/product/design/`
