---
name: recipe-blueprint
description: Define structural design foundation — information architecture, user flows, content model, brand direction, and AI interaction model — from validated opportunities and hypotheses
disable-model-invocation: true
---

**Context**: Create or update structural design artifacts in `docs/product/design/` that provide shared context for prototype generation and downstream UI specification. Blueprint bridges the gap between "what problems to solve" (discovery) and "what the product looks and works like" (prototypes).

## Orchestrator Definition

**Execution Protocol**:
1. **Delegate analysis work** to sub-agents (via Agent tool) when context separation benefits accuracy
2. **Follow the blueprint flow** defined below
3. **Stop at every `[STOP — BLOCKING]` marker** — present findings and CANNOT proceed until user explicitly confirms

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
5. Core User Flows → 5-10 primary flows across personas [Stop: User confirms structure]
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

**Gate: Vision, design principles, and at least one persona file must exist. At least one Opportunity must be identified (draft status is sufficient — validation is not required). If missing → inform user which prerequisite files are needed before proceeding.**

| Situation | Mode | Action |
|-----------|------|--------|
| No `docs/product/design/` exists | Create | Full blueprint definition |
| Blueprint exists, new Opportunities discovered | Update | Extend IA, flows, content model for new scope |
| Blueprint exists, new learnings in `docs/product/learnings.md` | Update | Revise based on new learnings |
| Existing codebase | Create/Update | Invoke codebase-analyzer for current architecture understanding |

### 2. MVP Scope Definition

Synthesize validated opportunities and hypotheses into a feature scope:

1. List all validated and in-progress Opportunities with their confidence scores
2. Map each Opportunity to candidate features (from hypothesis Solutions)
3. Apply MVP prioritization — see product-principles skill `references/mvp-definition.md` for MoSCoW/RICE frameworks
4. Produce a feature priority matrix:
   - **Must Have**: Validated Opportunities with confidence 5+ across Value and Usability
   - **Should Have**: Validated Opportunities with confidence 3-4
   - **Could Have**: Opportunities with partial validation
   - **Won't Have (this cycle)**: Explicitly deferred scope

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

Use blueprint-standards skill `references/flow-template.md` to define 5-10 primary flows:

1. Identify the highest-impact flows from validated Opportunities and journey maps
2. Write each flow from a specific persona's perspective
3. Include decision points, error scenarios, and alternative paths
4. Reference IA pages — each step maps to a page in the site map

Prioritize flows that:
- Cover the core value loop (the primary reason users return)
- Span both sides of the marketplace (if applicable)
- Address the highest-confidence Opportunities first

**[STOP — BLOCKING]** Present content model and user flows to user for confirmation:
- Entity overview with relationships
- Core flow list with persona assignments
- Flow details for the top 3 highest-priority flows

**CANNOT proceed to Step 6 until user explicitly confirms the structural design.**

### 6. Brand Direction

Use blueprint-standards skill `references/brand-direction-template.md` to define visual direction:

1. **Tone & Voice**: Position along key dimensions (formal↔casual, expert↔approachable), traced to design principles
2. **Color direction**: Primary, surface, accent color families with intentional rationale — directional, not final hex values
3. **Typography direction**: Heading, body, UI font style intentions with language considerations
4. **Visual density**: Whitespace, information density, surface elevation — informed by persona context
5. **Reference products**: Products whose visual approach aligns, with specific aspects to reference and avoid
6. **Visual Tokens (auto-derived)**: Derive concrete values from the direction defined above:
   - **Color tokens**: Select specific hex values from Reference Products' palettes and the Color Direction families. Use WebSearch to inspect Reference Products' public sites when no color values are stated in the Color Direction
   - **Typography tokens**: Select Google Fonts families that match the Typography Direction intentions and language considerations
   - **Spacing tokens**: Determine base unit from the Visual Density → Whitespace value (generous → 8px, moderate → 6px, compact → 4px) and derive scale
   - Mark source as `auto-derived` in the template
   - These tokens ensure prototype consistency. They are not final production values — those are determined during UI Spec

Reference the competitive landscape research (if available in `research/`) for visual benchmarking.

> **Note**: Design experts can refine Visual Tokens after blueprint completion using `recipe-refine-visuals`. The refinement updates the same `brand-direction.md` file.

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
- Color and typography direction
- Visual Tokens (auto-derived color, typography, spacing values)
- AI interaction pattern decisions
- Capability boundaries and guardrails

**CANNOT write files until user explicitly confirms the design direction.**

### 8. File Output

After user approval, write all artifacts to `docs/product/design/`:

- `docs/product/design/information-architecture.md`
- `docs/product/design/content-model.md`
- `docs/product/design/brand-direction.md`
- `docs/product/design/ai-interaction-model.md` (if applicable)
- `docs/product/design/flows/flow-{name}.md` (one file per flow)

## Sub-agent Usage

| Agent | When | Why (context separation benefit) |
|-------|------|----------------------------------|
| codebase-analyzer (via Agent tool, subagent_type: "discover:codebase-analyzer") | Existing codebase exists | Objective assessment of current architecture, routes, and components without hypothesis bias |

## Scope Boundaries

**Included**: Information architecture, user flows, content model, brand direction, AI interaction model, MVP scope synthesis
**Not included**: Opportunity discovery, hypothesis validation, pixel-level design specifications (UI Spec scope), component APIs and final production token values (UI Spec scope), PRD creation

## Completion Criteria

- [ ] Project context read (vision, principles, personas, opportunities)
- [ ] MVP scope synthesized from validated hypotheses
- [ ] Information architecture defined with Opportunity traceability
- [ ] User confirmed IA
- [ ] Content model defined with entity relationships
- [ ] Core user flows defined (5-10 flows)
- [ ] User confirmed structural design
- [ ] Brand direction defined with design principle traceability
- [ ] Visual Tokens auto-derived from brand direction
- [ ] AI interaction model defined (if applicable)
- [ ] User confirmed design direction
- [ ] All artifacts written to `docs/product/design/`
