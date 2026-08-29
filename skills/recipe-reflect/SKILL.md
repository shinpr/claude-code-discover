---
name: recipe-reflect
description: Orchestrate structured reflection — update target artifacts with learnings, distill knowledge across hypotheses, and maintain INDEX.md
disable-model-invocation: true
---

**Context**: Drive the feedback loop by reflecting on outcomes, updating target artifacts, and distilling learnings across the knowledge pyramid (see product-principles skill for Tier definitions).

## Orchestrator Definition

**Execution Protocol**:
1. **Required specialist execution**: Invoking this recipe is the user's explicit instruction and authorization to execute every named specialist whose condition applies. Execute each applicable Agent call with its declared `subagent_type` when its prerequisites are met and continue from its returned result; equivalent orchestrator work does not complete that step
2. **Exact specialist handoff**: The complete Agent prompt consists of all and only the applicable canonical `field: value` entries declared by the specialist's Input Contract. Copy each value unchanged from its authoritative source; serialize path fields as path strings so the specialist reads referenced artifacts directly
3. **Follow the reflection flow** defined below
4. **Approval gate**: At `[STOP — BLOCKING]`, present the distillation decision and resume after explicit user confirmation

## Workflow

Determine the reflection level → record results → independently distill applicable evidence → confirm promotions → update artifacts and index.

## Execution Decision Flow

### 1. Scope Assessment

Input: $ARGUMENTS

**Determine the reflection level** (see `references/reflection-guide.md`):

| Trigger | Level | Target Files |
|---------|-------|-------------|
| Hypothesis concluded | Level 1: Hypothesis | The hypothesis file |
| Multiple hypotheses concluded under an Opportunity | Level 2: Opportunity | Opportunity file (Tier 2 Learnings section) |
| PRD delivered, quarterly review, strategic pivot | Level 3: Vision | `docs/product/vision.md`, `docs/product/learnings.md` |

### 2. Result Recording

#### Level 1: Hypothesis Reflection
1. Verify the hypothesis file has been updated with results (validation results, confidence scores, evidence)
2. Document learnings: What did we learn regardless of outcome?
3. Check if this result changes understanding of the parent Opportunity

#### Level 2: Opportunity Reflection
1. Gather all hypotheses under the target Opportunity

#### Level 3: Vision Reflection
1. Gather cross-Opportunity data
2. Review Product Outcomes — are targets still correct?
3. Review NSM — still the right connecting metric?

### 3. Knowledge Distillation

**Invoke knowledge-distiller** using Agent tool (subagent_type: "discover:knowledge-distiller") with exact `scope_type`, `opportunity_ids`, and `hypothesis_paths` fields for pattern extraction:
- knowledge-distiller operates in a separate context so orchestrator synthesis does not replace direct source inspection
- It analyzes multiple hypotheses to find patterns, contradictions, and trends
- It proposes Tier 2 learnings (for Opportunity) or Tier 1 promotions (for Vision)
- It enforces distillation quality criteria (per product-principles skill)

**[STOP — BLOCKING]** Present distillation results to user for review:
- Extracted patterns and trends
- Proposed learnings (Tier 2 or Tier 1)
- Contradictions found (these become priority Discovery targets)
- Tier promotion proposals with supporting evidence

Write learnings and apply Tier promotions after explicit user confirmation.

### 4. Knowledge Promotion

After user approval:

#### Tier 3 → Tier 2
- Write learnings to the Opportunity file's "Tier 2 Learnings" section
- Include hypothesis references that support each learning

#### Tier 2 → Tier 1
- Write to `docs/product/learnings.md`
- Include freshness tag (`last-validated: YYYY-MM-DD`)
- Include independent supporting evidence strong enough for a product-level rule
- State the exact segments or conditions covered by that evidence

### 5. Index Update

Update `docs/discovery/INDEX.md` with:
- Hypothesis status summary (counts by status)
- Opportunity-to-hypothesis mapping
- Recent validation results
- Tier 1 learning changes (if any)
- Last updated timestamp

## Scope Boundaries

**Included**: Result recording, knowledge distillation, Tier promotion, INDEX.md maintenance
**Not included**: Hypothesis validation, new hypothesis generation

## Completion Criteria

- [ ] Result evidence is recorded at the applicable reflection level
- [ ] Level 2/3 patterns and promotions come from knowledge-distiller and user confirmation
- [ ] Modified learnings have current freshness tags and `docs/discovery/INDEX.md` reflects the result
