---
name: recipe-define
description: Orchestrate PRD creation from validated hypotheses — standard PRD output with 4 Risks confidence and hypothesis traceability
disable-model-invocation: true
---

**Context**: Transform validated hypotheses into a reviewed PRD that preserves product evidence, exposes remaining risk, and can be consumed by downstream implementation workflows.

## Orchestrator Definition

**Execution Protocol**:
1. **Required specialist execution**: Invoking this recipe is the user's explicit instruction and authorization to execute every named specialist whose condition applies. Execute each applicable Agent call with its declared `subagent_type` when its prerequisites are met and continue from its returned result; equivalent orchestrator work does not complete that step
2. **Exact specialist handoff**: The complete Agent prompt consists of all and only the applicable canonical `field: value` entries declared by the specialist's Input Contract. Copy each value unchanged from its authoritative source; serialize path fields as path strings so the specialist reads referenced artifacts directly
3. **Complete finding coverage**: Record one evidence-backed disposition for every reviewer issue before correction or progression
4. **Follow the definition flow** below and stop at the final user approval gate

## Workflow

Assess readiness → draft the PRD → obtain independent review → resolve each finding → request final user approval.

## Execution Decision Flow

### 1. Readiness Assessment

Input: $ARGUMENTS

Read the relevant Opportunity and hypothesis files. For each hypothesis included in the PRD:

1. Check confidence evidence using prd-standards `references/user-story-guide.md`
2. Assess cost × risk × reversibility
3. Determine `validated enough` or `needs more validation`
4. Keep proceed, further validation, scope reduction, and explicit residual risk as valid results; choose further validation only when its evidence can change readiness or scope

Use product-principles `references/mvp-definition.md` to determine the smallest included capability set, explicit exclusions, and observable proof. A ranking aid is optional and applies only when credible candidates remain tied after direct boundary analysis.

Resolve the current outcome and included scope from confirmed product sources, their declared precedence, and cited evidence. Repository-local document structure and other reversible drafting choices remain with the workflow. Stop only when confirmed obligations are mutually exclusive and selecting the governing obligation requires a product choice absent from those sources; present the exact conflicting statements and the PRD decision they block.

### 2. PRD Drafting

Use prd-standards `references/prd-template.md` and write the draft to `docs/prd/[feature-name]-prd.md` so the reviewer reads the artifact directly.

The PRD includes:

1. **Overview**: Current outcome, Opportunity, cited hypotheses, and explicit exclusions
2. **User Stories**: Persona-grounded stories with all four Risks, evidence or explicit unknowns, remaining risk, and readiness rationale
3. **Functional Requirements**: Stable AC IDs and observable EARS-format behavior
4. **State Coverage**: For each user-facing requirement, specify applicable Loading, Empty, Error, Partial, or Success behavior and explain only ambiguous exclusions
5. **Design Context**: Reference existing design artifacts; copy only decisions the implementation consumer needs
6. **Success Criteria**: Trace to Product Outcomes
7. **Technical Considerations**: Include current dependencies, constraints, and unvalidated assumptions only when they can change implementation or verification

Verify an external API, library, or service with WebSearch only when a current availability or compatibility claim controls PRD scope, feasibility, or verification. Record the authoritative source and stop research when that decision is supported.

### 3. Independent Review

Invoke prd-reviewer using Agent tool (`subagent_type: "discover:prd-reviewer"`) exactly with:

```text
target_path: docs/prd/[feature-name]-prd.md
```

When the verdict is `rejected`, return the reported conflict to Readiness Assessment. Re-check source precedence, confirmed outcomes, explicit exclusions, and cited evidence. Resume drafting when they determine one coherent boundary. Stop only for the unresolved pair of confirmed obligations defined in Step 1.

### 4. Review Resolution

For every reviewer issue, inspect the cited PRD content, evidence, and governing product sources, then record exactly one disposition:

| Disposition | Condition |
|---|---|
| `apply` | Leaving the PRD unchanged would contradict the confirmed outcome or evidence, state an unsupported claim as fact, leave implementation non-executable, or leave required behavior non-verifiable |
| `decline` | The PRD still satisfies the confirmed outcome and required downstream boundary; the issue is template-only, optional hardening, added scope, a reversed exclusion, duplicate proof, or unsupported reviewer preference |

For each issue preserve the complete reviewer object unchanged and add only its disposition, plus governing reason and evidence for a decline. An orchestrator-authored paraphrase is not a correction requirement.

After every issue has an `apply` or `decline` disposition, apply the `apply` corrections inside the confirmed PRD scope. Then rerun prd-reviewer with the original `target_path` and a `prior_feedback` entry for every original issue:

```text
target_path: docs/prd/[feature-name]-prd.md
prior_feedback: [{issue: <complete unchanged reviewer issue object>, disposition, reason?, evidence}]
```

Every prior ID must return once as `resolved`, `withdrawn`, or `maintained`:

- `resolved` and `withdrawn` complete the item
- a maintained `apply` returns through correction using the complete original issue and reconciliation evidence; after the same issue survives two correction attempts, report it as incomplete instead of manufacturing further work
- a maintained `decline` remains in the reviewer's `issues` and keeps the reviewer verdict at `needs_revision`; retain the evidence-backed decline, skip another correction loop, and present the disagreement at final approval

Review Resolution converges when every issue is resolved, withdrawn, or retained as an evidence-backed decline and every new issue has a disposition. When retained declines are the only current issues, proceed to final approval with the reviewer verdict at `needs_revision` and list each disagreement in the approval presentation.

### 5. User Approval

**[STOP — BLOCKING]** Present the reviewed PRD once:

- PRD target path and current outcome/scope
- 4 Risks and remaining-risk summary
- prd-reviewer verdict and coverage
- applied corrections
- evidence-backed declined findings, if any

Finalize after explicit user approval. If the user changes the outcome, scope, or exclusion, resume from Step 1 with the complete changed decision. Otherwise keep the reviewed file unchanged.

## Scope Boundaries

**Included**: PRD creation, user story generation, mandatory independent review, review resolution, final user approval
**Not included**: Hypothesis validation, Design Doc/ADR creation, implementation, release or production operations

## Completion Criteria

- [ ] The PRD preserves the confirmed outcome, evidence, exclusions, remaining risk, and observable behavior
- [ ] prd-reviewer reviewed the artifact path and every issue has a traceable disposition
- [ ] The user approved the reviewed PRD at its final path
