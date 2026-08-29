---
name: hypothesis-discipline
description: Manages hypothesis lifecycle, enforces validation criteria, time budgets, and confidence scoring rules. Use when creating hypotheses, updating confidence scores, setting validation criteria, handling timeouts, or recording validation results.
disable-model-invocation: true
---

# Hypothesis Discipline

## Core Principle

A hypothesis is not a guess — it is a **structured statement with clear validation criteria and a time budget**. Every hypothesis must answer: "How will we know if this is true or false?"

## Hypothesis Characteristics

- Hypotheses exist at **every level** of the OST hierarchy (Outcome → Opportunity → Solution → Assumption)
- Each hypothesis has a **target level** attribute indicating which OST level it addresses
- Hypotheses follow an **ADR-style lifecycle** — a single file tracks the full journey from draft to conclusion
- **Rejected and invalidated hypotheses remain in their lifecycle file** as learning assets

## Hypothesis Lifecycle

```
draft → testing → validated → adopted
                            → rejected (validated but not adopted)
              → invalidated (disproven by evidence)
              → inconclusive (evidence gathered but insufficient to confirm or deny)
              → timeout (deadline passed, decision needed: continue or stop)
```

## Hypothesis File Schema

The authoritative schema is defined in `references/hypothesis-template.md`. Key fields:

- `id`: HYPO-NNN
- `level`: outcome / opportunity / solution / assumption
- `status`: draft / testing / validated / invalidated / inconclusive / adopted / rejected / timeout
- `confidence`: per-risk scores (value, usability, feasibility, viability) on 0-10 scale
- `time-budget` and `deadline`: validation time constraints

## Validation Criteria Requirements

Every hypothesis **must** define before testing begins:

1. **We believe that** — the hypothesis statement
2. **We'll know we're right when** — measurable success criteria
3. **We'll know we're wrong when** — measurable failure criteria
4. **Validation method** — how we will test (prototype, data analysis, interview, code spike, market research)
5. **Time budget** — maximum time investment before forced decision

## Time Budget and Cutoff

- Every hypothesis gets a **time budget** (e.g., 1d, 1w, 2w)
- A **deadline** sets the hard cutoff date
- When deadline passes without conclusion → status becomes `timeout`
- Timeout forces a decision: extend (with justification), pivot, or abandon
- **Bound every validation** with a time budget and deadline so exploration ends in an explicit decision

## Confidence Update Rules

- Confidence scores are updated **only when new evidence is gathered**
- Record the evidence that justified each score change
- Confidence can go **down** as well as up — negative evidence is valid evidence
- Different risk dimensions can have different confidence levels

## Result Recording

When a hypothesis reaches conclusion (validated/invalidated/inconclusive/adopted/rejected):

1. **Record the result** in the hypothesis file with evidence
2. **Update confidence scores** with final values
3. **Link to evidence** (data, screenshots, prototype results, interview notes)
4. **Record decision learning** — conclusions and evidence that can change confidence, the Opportunity, or a downstream decision
5. **Update the parent Opportunity** if the result changes its understanding

## Key Disciplines

- **Separate creation from evaluation**: Generate candidate hypotheses before evaluating them
- **Seek disconfirming evidence**: Actively look for reasons the hypothesis might be wrong
- **One hypothesis, one test**: Each validation produces an interpretable result for one hypothesis
- **Record decision evidence**: Preserve conclusions, evidence, and reasoning that can change confidence, the parent Opportunity, a downstream decision, or future validation. Omit working narration and baseline knowledge with no consumer
- **Rejected ≠ worthless**: A rejected hypothesis teaches what doesn't work and why
- **Inconclusive is honest**: When evidence is insufficient, say so instead of forcing a verdict
