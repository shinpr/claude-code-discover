# MVP Definition Reference

## Purpose

Define the smallest current scope that can deliver and observe the confirmed Product Outcome. Use this when validated hypotheses transition into a PRD or structural blueprint.

## Inclusion Boundary

A capability belongs in the MVP when removing it would break at least one of these:

- the confirmed user outcome or core value loop;
- an explicit product, accessibility, security, or compatibility boundary;
- the observable proof needed to decide whether the outcome works; or
- a dependency required by another included capability.

Every inclusion records its governing evidence and effect. Every candidate outside this boundary is deferred or excluded with a reason. Reuse and no-change remain valid when existing behavior already satisfies the boundary.

## Scope Decision

1. State the current Product Outcome and user context.
2. Inspect the active Opportunities and hypothesis evidence that can change this outcome.
3. Identify candidate capabilities and existing behavior that may satisfy them.
4. For each candidate, assess outcome effect, evidence, rough cost, risk, and reversibility.
5. Keep the smallest set that preserves the inclusion boundary.
6. Record explicit exclusions and remaining assumptions.
7. Define the observable result that will show the MVP boundary is satisfied.

Resolve candidate choices from the confirmed outcome, governing evidence, rough cost, risk, and reversibility. When several candidates satisfy the same boundary, select the smallest lower-cost reversible set and record the rationale. Reversible implementation choices remain with the downstream workflow. Stop only when confirmed governing obligations are mutually exclusive and their declared precedence and evidence leave the governing obligation unresolved; report the exact conflict and the scope decision it blocks.

## Optional Ranking Aids

MoSCoW, RICE, or ICE may help when credible candidates remain tied after direct boundary analysis. Use one only when its result can change inclusion or order, and record the evidence behind its inputs. The score is decision support rather than an inclusion gate.

## Scope Reduction Options

Use the first option that preserves the observable outcome:

- reuse existing behavior;
- remove a candidate outside the inclusion boundary;
- narrow the user context or use case to the confirmed evidence;
- replace automation with a reversible manual step when the test remains valid;
- reduce implementation depth while preserving the public and user-visible contract.

## Validation Patterns

Choose a pattern only when it is the smallest proof for the active uncertainty:

| Pattern | Proof Boundary |
|---------|----------------|
| **Concierge** | Demand or workflow value before automation |
| **Wizard of Oz** | User interaction before backend investment |
| **Single capability** | One core value loop without adjacent scope |
| **Landing page** | Interest or problem recognition before product implementation |

## Completion Check

- The MVP has one current observable outcome.
- Every included capability has evidence and a named effect on that outcome or its required boundary.
- Existing behavior, exclusions, and residual assumptions are explicit.
- The scope stops where additional work cannot change the current outcome or its proof.
