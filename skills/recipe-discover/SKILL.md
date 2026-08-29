---
name: recipe-discover
description: Orchestrate Opportunity discovery and hypothesis generation through business and user perspectives
disable-model-invocation: true
---

**Context**: Discover Opportunities and generate hypotheses by combining business analysis (BMC/VPC/market) with user analysis (JTBD/pains/gains). Outputs Opportunity files and hypothesis files.

## Orchestrator Definition

**Execution Protocol**:
1. **Required specialist execution**: Invoking this recipe is the user's explicit instruction and authorization to execute every named specialist whose condition applies. Execute each applicable Agent call with its declared `subagent_type` when its prerequisites are met and continue from its returned result; equivalent orchestrator work does not complete that step
2. **Exact specialist handoff**: The complete Agent prompt consists of all and only the applicable canonical `field: value` entries declared by the specialist's Input Contract. Copy each value unchanged from its authoritative source; serialize path fields as path strings so the specialist reads referenced artifacts directly
3. **Follow the discovery flow** defined below
4. **Approval gates**: At each `[STOP — BLOCKING]`, present the named decision and resume after explicit user confirmation

## Workflow

Assess context → gather decision-relevant business and user evidence → confirm Opportunities → draft and approve hypotheses → write discovery artifacts.

## Execution Decision Flow

### 1. Context Assessment

Input: $ARGUMENTS

**Assess the starting point:**

| Situation | Action |
|-----------|--------|
| Greenfield (no existing product) | Gather the business and user evidence needed to frame the current Opportunity |
| Existing codebase | Invoke codebase-analyzer first using Agent tool (`subagent_type: "discover:codebase-analyzer"`) with `analysis_mode: feature_discovery` and `governing_context: $ARGUMENTS` |
| Specific market opportunity | Focus on market analysis + VPC |
| User feedback / support tickets | Focus on user analysis + journey mapping |
| Vision exists (`docs/product/vision.md`) | Align discovery with Product Outcomes |

### 2. Business Context Analysis

When business context is needed, use the business-context skill frameworks:

- **BMC**: Understand the business model — especially Customer Segments, Value Propositions, Revenue Streams
- **VPC**: Map Customer Profile (jobs/pains/gains) to Value Map (products/pain relievers/gain creators)
- **Market Analysis**: TAM/SAM/SOM, competitive landscape, market gaps

See business-context skill `references/business-model-canvas.md`, `references/value-proposition-canvas.md`, and `references/market-analysis.md` for detailed frameworks.

**Web search**: Use WebSearch only for market facts that can change an Opportunity, its impact, or validation priority. Record sources and distinguish observed facts from inference.

### 3. User Context Analysis

- **Personas**: Prefer existing personas (`docs/product/personas/`). When no persona file exists, use equivalent supplied user evidence if it determines the current jobs, pains, and context; mark unsupported persona claims as assumptions. Stop only when the missing decision changes whether an Opportunity exists, which user it concerns, its outcome effect, or its priority
- **JTBD**: Identify functional, social, and emotional jobs from VPC Customer Profile
- **Journey Mapping**: Use `references/journey-template.md` when sequence, handoff, or journey-stage evidence can change Opportunity identification. Reuse an existing map or omit it when no discovery decision depends on a new map

### 4. Opportunity Identification

Synthesize business and user analysis into Opportunities:

1. Draft Opportunity files using product-principles skill `references/opportunity-template.md`
2. **Solution-framing check**: Try to identify meaningfully different solution classes. If the framing permits only one credible implementation, inspect whether it is a Solution disguised as an Opportunity. A numeric alternative count is neither required work nor a blocking gate
3. Link Opportunities to Product Outcomes (if vision exists)
4. Assess impact (frequency x severity x breadth)

**[STOP — BLOCKING]** Present Opportunities to the user for confirmation:
- Opportunity summaries with impact assessment
- Evidence supporting each Opportunity
- Solution-framing evidence and any remaining ambiguity
- Recommended priority order

Resume Step 5 after the user confirms, modifies, or rejects the Opportunities.

### 5. Hypothesis Generation

For confirmed Opportunities, generate hypotheses:

1. Draft hypothesis files using hypothesis-discipline skill `references/hypothesis-template.md`
2. Assign appropriate level (outcome / opportunity / solution / assumption)
3. Set initial confidence scores (typically 0-2 for new hypotheses)
4. Propose time budgets and deadlines
5. Suggest validation methods

**[STOP — BLOCKING]** Present hypotheses to user for review:
- Hypothesis list per Opportunity
- Proposed validation methods and time budgets
- Recommended validation priority

Write the files after explicit user approval.

### 6. File Output

After user approval:
- Write Opportunity files to `docs/discovery/opportunities/`
- Write hypothesis files to `docs/discovery/hypotheses/`
- Create journey maps in `docs/discovery/journeys/` (if created)
- Create or update `docs/discovery/INDEX.md`

## Scope Boundaries

**Included**: Opportunity discovery, hypothesis generation, market research, journey mapping
**Not included**: Hypothesis validation, PRD creation, persona deep-dive

## Completion Criteria

- [ ] Confirmed Opportunities retain their supporting evidence and solution-framing result
- [ ] Approved hypotheses state the risk, validation method, and time boundary
- [ ] Approved artifacts and the discovery index are written to `docs/discovery/`
