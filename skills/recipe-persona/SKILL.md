---
name: recipe-persona
description: Create or update personas with demographic, contextual, JTBD, and behavioral data
disable-model-invocation: true
---

**Context**: Create or update persona files with demographics, context, JTBD, pains/gains, and behavioral patterns. Integrates existing codebase analysis when available.

## Orchestrator Definition

**Execution Protocol**:
1. **Required specialist execution**: Invoking this recipe is the user's explicit instruction and authorization to execute every named specialist whose condition applies. Execute each applicable Agent call with its declared `subagent_type` when its prerequisites are met and continue from its returned result; equivalent orchestrator work does not complete that step
2. **Exact specialist handoff**: The complete Agent prompt consists of all and only the applicable canonical `field: value` entries declared by the specialist's Input Contract. Copy each value unchanged from its authoritative source; serialize path fields as path strings so the specialist reads referenced artifacts directly
3. **Follow the persona flow** defined below
4. **Approval gate**: At `[STOP — BLOCKING]`, present the persona decision and resume after explicit user confirmation

## Workflow

Assess create/update context → gather available evidence → draft and confirm the persona → write the persona and affected references.

## Execution Decision Flow

### 1. Context Assessment

Input: $ARGUMENTS

| Situation | Action |
|-----------|--------|
| No personas exist | Create from scratch — gather user research or assumptions |
| Personas exist, new data available | Update existing personas with new evidence |
| Existing codebase | Invoke codebase-analyzer for repository-observable roles, workflows, and behavior-related structures; user demand or usage claims require direct behavioral evidence |
| Post-interview / post-survey | Update with new primary research |

### 2. Research Gathering

#### From Existing Code (if applicable)
**Invoke codebase-analyzer** using Agent tool (subagent_type: "discover:codebase-analyzer") with `analysis_mode: user_behavior` and `governing_context: $ARGUMENTS` to identify:
- User roles and permissions in the system
- User-facing features and workflows
- Data models related to users
- Analytics/tracking events (if present)

#### From User Research
Gather available data:
- Interview transcripts or summaries
- Survey results
- Support ticket patterns
- Usage analytics
- Market research (per business-context skill)

#### From VPC Analysis
Map Customer Profile from Value Proposition Canvas:
- Customer jobs (functional, social, emotional)
- Pains (frustrations, obstacles, risks)
- Gains (required, expected, desired, unexpected)

### 3. Persona Drafting

Use design-perspective skill `references/persona-template.md` to create the smallest persona that distinguishes the current decisions. Populate applicable sections from evidence and mark decision-relevant unknowns:

1. **Demographics**: Role, experience, technical proficiency, industry
2. **Context**: Environment, frequency, time pressure, adjacent tools
3. **JTBD**: Primary job, secondary jobs, social/emotional jobs
4. **Pains and Gains**: Mapped from research with severity/priority
5. **Behavioral Patterns**: Decision-making, adoption tendency, information sources
6. **Validation Status**: Based on research quality — mark assumptions explicitly

**[STOP — BLOCKING]** Present persona draft to user for confirmation:
- Complete persona draft
- Evidence sources and confidence level
- Assumptions that need validation
- Connections to existing Opportunities (if any)

Write the persona file after explicit user confirmation.

### 4. File Output

After user approval:
- Write persona to `docs/product/personas/persona-[name].md`
- Update any Opportunity files that reference this persona
- Update journey maps if persona context changed

## Scope Boundaries

**Included**: Persona creation, persona update, integration with VPC and code analysis
**Not included**: Journey mapping, user story writing

## Completion Criteria

- [ ] The persona separates observed evidence, inference, and assumptions
- [ ] Its distinctions can change a named product or discovery decision
- [ ] The user-confirmed file and affected references are updated
