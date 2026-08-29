---
name: recipe-validate
description: Orchestrate hypothesis validation through type-appropriate methods — prototypes, code analysis, market research, and expert review
disable-model-invocation: true
---

**Context**: Validate hypotheses using appropriate methods based on risk type. Always invoke hypothesis-verifier for an independent disconfirming pass. Record results in hypothesis files.

## Orchestrator Definition

**Execution Protocol**:
1. **Required specialist execution**: Invoking this recipe is the user's explicit instruction and authorization to execute every named specialist whose condition applies. Execute each applicable Agent call with its declared `subagent_type` when its prerequisites are met and continue from its returned result; equivalent orchestrator work does not complete that step
2. **Exact specialist handoff**: The complete Agent prompt consists of all and only the applicable canonical `field: value` entries declared by the specialist's Input Contract or, for a built-in specialist, by the call site's inline contract. Copy each value unchanged from its authoritative source; serialize path fields as path strings so the specialist reads referenced artifacts directly
3. **Follow the validation flow** defined below
4. **Approval gates**: At each `[STOP — BLOCKING]`, present the named decision and resume after explicit user confirmation

## Workflow

Assess the hypothesis → independently design and approve the smallest disconfirming test → execute it → record and review the result.

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

**Invoke hypothesis-verifier** using Agent tool (subagent_type: "discover:hypothesis-verifier") with `hypothesis_path: <target hypothesis path>` to design the validation:
- hypothesis-verifier operates in a separate context to preserve an independent disconfirming pass
- It defines success/failure criteria independently

**[STOP — BLOCKING]** Present validation design to user for confirmation:
- Proposed validation method
- Success and failure criteria
- Required resources and time estimate
- Risk of the validation approach itself

Execute the validation after the user confirms the design.

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
1. Pass only `hypothesis_path` and `output_path` using their canonical path values
2. prototype-generator operates in a separate context and reads design sources directly
3. Use one prototype unless the confirmed hypothesis explicitly compares patterns
4. Output: `docs/discovery/prototypes/hypo-{id}-prototype.html` (or `hypo-{id}-{pattern}-prototype.html` for multiple)
5. User opens the completed `output_path` in a browser for verification

#### Worktree Code Spike (for Feasibility validation)
When repository inspection cannot resolve a Feasibility decision and executable proof can change the verdict:
1. Invoke codebase-analyzer (via Agent tool, subagent_type: "discover:codebase-analyzer") with `analysis_mode: feasibility` and the hypothesis path as `governing_context`
2. Invoke a fresh Agent call with `subagent_type: "general-purpose"` and `isolation: "worktree"` using exactly:

   ```text
   action: execute the smallest disposable code spike that can resolve the target hypothesis's feasibility uncertainty; return feasibility, complexity, blockers, and inspectable evidence
   hypothesis_path: <canonical hypothesis path>
   ```

3. The worktree is automatically cleaned up — no code persists in the main branch

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

Proceed to the next hypothesis or close the workflow after the user reviews the result.

### 5. Timeout Handling

When a hypothesis reaches its deadline without conclusion:
1. Set status to `timeout`
2. Present options to user:
   - **Extend**: Add more time with justification
   - **Pivot**: Modify the hypothesis based on partial evidence
   - **Abandon**: Stop validation, record learnings from partial evidence

## Scope Boundaries

**Included**: Hypothesis validation design, validation execution, result recording
**Not included**: Hypothesis generation, PRD creation, reflection/distillation

## Completion Criteria

- [ ] hypothesis-verifier supplied the independent, smallest disconfirming design
- [ ] The confirmed method produced decision-relevant evidence or an explicit inconclusive result
- [ ] The hypothesis file records the reviewed result, confidence change, evidence, and next decision
