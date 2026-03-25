---
name: recipe-validate
description: Orchestrate hypothesis validation through type-appropriate methods — prototypes, code analysis, market research, and expert review
disable-model-invocation: true
---

**Context**: Validate hypotheses using appropriate methods based on risk type. Invoke hypothesis-verifier for bias-free validation design. Record results in hypothesis files.

## Orchestrator Definition

**Execution Protocol**:
1. **Delegate verification design** to hypothesis-verifier (via Agent tool, subagent_type: "discover:hypothesis-verifier") for bias-free assessment
2. **Follow the validation flow** defined below
3. **Stop at every `[STOP — BLOCKING]` marker** — present findings and CANNOT proceed until user explicitly confirms

## Workflow Overview

```
Input (hypothesis file or hypothesis ID)
    ↓
1. Hypothesis Assessment → Read and understand the hypothesis
    ↓
2. Validation Design → hypothesis-verifier designs the test [Stop: User confirms design]
    ↓
3. Validation Execution → Type-appropriate method
    ↓
4. Result Recording → Update hypothesis file [Stop: User reviews results]
    ↓
Output: Updated hypothesis file with validation results
```

## Execution Decision Flow

### 1. Hypothesis Assessment

Input: $ARGUMENTS

Read the target hypothesis file(s). Understand:
- What is being tested (the hypothesis statement)
- Which risk dimension is primary (Value / Usability / Feasibility / Viability)
- Current confidence scores
- Time budget and deadline
- Parent Opportunity context

### 2. Validation Design

**Invoke hypothesis-verifier** using Agent tool (subagent_type: "discover:hypothesis-verifier") to design the validation:
- hypothesis-verifier operates in a separate context to prevent confirmation bias
- It designs the test without knowing the orchestrator's expectations
- It defines success/failure criteria independently

**[STOP — BLOCKING]** Present validation design to user for confirmation:
- Proposed validation method
- Success and failure criteria
- Required resources and time estimate
- Risk of the validation approach itself

**CANNOT proceed to validation execution until user explicitly confirms the design.**

### 3. Validation Execution

Execute validation based on the risk type and method:

| Risk Type | Validation Methods | Tools |
|-----------|-------------------|-------|
| **Value** | Market research, user interviews, competitive analysis, landing page test | WebSearch tool, survey analysis |
| **Usability** | Prototype testing, usability study, interaction analysis | prototype-generator agent (context-separated) |
| **Feasibility** | Code spike, architecture review, dependency analysis | codebase-analyzer, **worktree code spike** |
| **Viability** | Business model analysis, ROI calculation, regulatory review | WebSearch tool, BMC/VPC analysis |

#### Prototype Generation (for Usability validation)
Invoke prototype-generator using Agent tool (subagent_type: "discover:prototype-generator"):
1. Pass the hypothesis file path and output path in the prompt
2. prototype-generator operates in a **separate context** — it reads design context files independently and produces a natural product UI
3. When multiple patterns need validation, invoke prototype-generator separately for each pattern
4. Output: `docs/discovery/prototypes/hypo-{id}-prototype.html` (or `hypo-{id}-{pattern}-prototype.html` for multiple)
5. User opens in browser for verification

#### Worktree Code Spike (for Feasibility validation)
When validating Feasibility through code:
1. Invoke codebase-analyzer (via Agent tool, subagent_type: "discover:codebase-analyzer") for current architecture understanding
2. Use Agent tool with `isolation: "worktree"` to run a code spike in an isolated environment
3. The spike agent implements a minimal proof-of-concept
4. Results (feasibility assessment, complexity, blockers) are reported back
5. The worktree is automatically cleaned up — no code persists in the main branch

#### Market Research (for Value/Viability validation)
Use WebSearch tool to gather market data. See product-principles skill `references/mvp-definition.md` for scope assessment.

### 4. Result Recording

After validation execution:

1. Update the hypothesis file:
   - Change status (validated / invalidated / inconclusive / timeout)
   - Update confidence scores with evidence
   - Record evidence and artifacts
   - Document learnings
2. Link to validation artifacts (prototypes, data, interview notes)

**[STOP — BLOCKING]** Present results to user for review:
- Validation outcome (validated / invalidated / inconclusive)
- Updated confidence scores with evidence
- Key learnings
- Recommended next actions

**CANNOT proceed to next hypothesis or close the workflow until user explicitly reviews.**

### 5. Timeout Handling

When a hypothesis reaches its deadline without conclusion:
1. Set status to `timeout`
2. Present options to user:
   - **Extend**: Add more time with justification
   - **Pivot**: Modify the hypothesis based on partial evidence
   - **Abandon**: Stop validation, record learnings from partial evidence

## Sub-agent Usage

| Agent | When | Why (context separation benefit) |
|-------|------|----------------------------------|
| hypothesis-verifier (subagent_type: "discover:hypothesis-verifier") | Always (validation design) | Eliminates confirmation bias in test design |
| prototype-generator (subagent_type: "discover:prototype-generator") | Usability validation | Produces natural product UI without test infrastructure contamination |
| codebase-analyzer (subagent_type: "discover:codebase-analyzer") | Feasibility validation | Objective code analysis without hypothesis bias |

## Scope Boundaries

**Included**: Hypothesis validation design, validation execution, result recording
**Not included**: Hypothesis generation, PRD creation, reflection/distillation

## Completion Criteria

- [ ] Hypothesis assessed and understood
- [ ] hypothesis-verifier designed the validation (bias-free)
- [ ] User confirmed validation design
- [ ] Validation executed with appropriate method
- [ ] Hypothesis file updated with results and evidence
- [ ] User reviewed results
- [ ] Next actions identified
