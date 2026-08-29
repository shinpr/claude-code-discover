# Reflection Guide

## Purpose

Guide for structured reflection at three levels: PRD unit, Opportunity unit, and Vision unit. Reflection drives the feedback loop that makes the product development cycle learn from itself.

## Reflection Principles

- **Reflect on the artifact, not in a separate place**: Results are appended to the target file (hypothesis, Opportunity, vision.md)
- **ADR-style lifecycle**: Each artifact carries its full history
- **Decision-relevant learning**: Preserve success or failure evidence when it can change an Opportunity, product rule, or future validation decision
- **Distill outcomes**: Use knowledge-distiller to extract cross-result patterns and conditions

## Reflection Levels

### Level 1: Hypothesis Reflection (per hypothesis)
**Trigger**: Hypothesis reaches conclusion (validated / invalidated / inconclusive / adopted / rejected / timeout)
**Target file**: The hypothesis file itself

**Process**:
1. Record the result with evidence in the hypothesis file
2. Update confidence scores with final values
3. Document conclusions and evidence that can change a downstream decision
4. Identify next actions
5. Flag if this result changes understanding of the parent Opportunity

### Level 2: Opportunity Reflection (per Opportunity)
**Trigger**: After multiple hypotheses under an Opportunity reach conclusions, or when shifting focus away from an Opportunity
**Target file**: The Opportunity file (Tier 2 Learnings section)

**Process**:
1. Invoke knowledge-distiller to analyze all hypotheses under this Opportunity
2. Extract patterns: What worked? What didn't? What surprised us?
3. Update Tier 2 Learnings in the Opportunity file
4. Check if any Tier 2 learnings qualify for Tier 1 promotion
5. Update related hypotheses' status if Opportunity understanding changed

### Level 3: Vision Reflection
**Trigger**: New cross-Opportunity evidence can change a Product Outcome, NSM, strategic priority, or Tier 1 learning used by a current decision
**Target file**: `docs/product/vision.md` and `docs/product/learnings.md`

**Process**:
1. Review Product Outcomes — are they still the right targets?
2. Review NSM — is it still the right connecting metric?
3. Invoke knowledge-distiller to analyze cross-Opportunity patterns
4. Promote qualified learnings to Tier 1 (`docs/product/learnings.md`)
5. Update `docs/discovery/INDEX.md` with current status

## Distillation Quality Criteria

See product-principles skill for authoritative definitions of the Knowledge Pyramid and distillation criteria (Independent Evidence, Context Coverage, Contradiction Handling, Freshness Tags). knowledge-distiller enforces these criteria when proposing promotions.

## INDEX.md Update

recipe-reflect updates `docs/discovery/INDEX.md` with:
- Hypothesis status summary (draft / testing / validated / invalidated / inconclusive / adopted / rejected / timeout counts)
- Opportunity-to-hypothesis mapping
- Recent validation results
- Tier 1 learning changes

## Reflection Check

- [ ] The target artifact and index preserve decision-relevant results and confidence evidence
- [ ] Level 2+ patterns come from knowledge-distiller; contradictions retain their conditions
- [ ] Promotions meet the tier criteria and modified Tier 1 learnings carry freshness tags
