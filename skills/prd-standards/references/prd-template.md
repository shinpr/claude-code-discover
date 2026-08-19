# PRD: [Feature Name]

## Overview

### One-line Summary
[Describe this feature in one line]

### Background
[Why is this feature needed? What problem does it solve?]

**Hypothesis & Validation References:**
- Opportunity: [OPP-NNN](../../../docs/discovery/opportunities/OPP-NNN.md)
- Key hypotheses validated:
  - [HYPO-NNN](../../../docs/discovery/hypotheses/HYPO-NNN.md) — [status, key finding]
  - [HYPO-NNN](../../../docs/discovery/hypotheses/HYPO-NNN.md) — [status, key finding]

## User Stories

### Primary Users
[Define the main target users. Reference personas from `docs/product/personas/`]

### User Stories

Each user story includes 4 Risks confidence assessment:

#### US-1: [Story Title]

```
As a [user type]
I want to [goal/desire]
So that [expected value/benefit]
```

**4 Risks Confidence (0-10):**
| Risk | Score | Evidence | Remaining Risk |
|------|-------|----------|----------------|
| Value | - | [what validated this] | [what's still uncertain] |
| Usability | - | [what validated this] | [what's still uncertain] |
| Feasibility | - | [what validated this] | [what's still uncertain] |
| Viability | - | [what validated this] | [what's still uncertain] |

**Delivery readiness**: [validated enough / needs more validation]
**Rationale**: [Why this confidence level is sufficient — cost x risk x reversibility]

#### US-2: [Story Title]

[Repeat the same structure]

### Use Cases
[Include only scenarios that add execution or verification context not already supplied by the stories and acceptance criteria; otherwise omit this subsection]

## Functional Requirements

### Must Have (MVP)
- [ ] Requirement 1: [Detailed description]
  - AC-001: [Acceptance criteria — EARS format: When/While/If-then]
  - AC-002: [Additional acceptance criteria if needed]
  - State Coverage: [Loading / Empty / Error / Partial / Success — mark each required or not_applicable; include expected behavior or the not-applicable reason]
- [ ] Requirement 2: [Detailed description]
  - AC-003: [Acceptance criteria]
  - State Coverage: [Loading / Empty / Error / Partial / Success — mark each required or not_applicable; include expected behavior or the not-applicable reason]
- [ ] Requirement 3: [Detailed description]
  - AC-004: [Acceptance criteria]
  - State Coverage: [Loading / Empty / Error / Partial / Success — mark each required or not_applicable; include expected behavior or the not-applicable reason]

### Nice to Have
- [ ] Requirement 1: [Detailed description]
  - AC-005: [Acceptance criteria]
  - State Coverage: [If user-facing, record all five states and define every required behavior]
- [ ] Requirement 2: [Detailed description]
  - AC-006: [Acceptance criteria]
  - State Coverage: [If user-facing, record all five states and define every required behavior]

### Out of Scope
- Item 1: [Description and reason]
- Item 2: [Description and reason]

## Design Context

Context for downstream UI specification. Prototypes show concrete examples; this section carries the intent behind them.

### Design Principles

[Include only principles from `docs/product/design-principles.md` that resolve an implementation-relevant trade-off. Omit this subsection when none applies.]

- **[Principle name]**: [Implementation-relevant trade-off resolution and rationale]

### Decision-Relevant Direction

[Copy only rows from `docs/product/design/brand-direction.md` whose Consumer / Effect changes implementation. Preserve the approved direction and governing evidence. Omit this subsection when none applies.]

| Property | Direction | Governing Evidence | Consumer / Effect |
|----------|-----------|--------------------|-------------------|
| [property] | [approved direction] | [source] | [implementation decision affected] |

### Design Guardrails

**Do:**
- [Positive pattern traced to a design principle]

**Transform:**
- [Anti-pattern → required alternative, traced to a design principle]

### Visual Reference

- Brand direction: `docs/product/design/brand-direction.md` (include concrete tokens only when present and relevant)
- Prototypes: [list relevant prototype files from `docs/discovery/prototypes/`]

## Non-Functional Requirements

[Include only categories activated by the current outcome, repository/product rules, observable behavior, compatibility contract, or required proof. Omit inactive placeholder categories.]

### Performance
- Response Time: [Target value]
- Throughput: [Target value]
- Concurrency: [Target value]

### Reliability
- Availability: [Target value]
- Error Rate: [Target value]

### Security
- [Security requirements details]

### Scalability
- [Considerations for future scaling]

### Accessibility (when feature includes UI)
- Compliance standard: WCAG 2.2 AA
- Target assistive technologies: [Screen reader, keyboard operation, voice control, etc.]
- Platform requirements: [e.g., app store review requirements]
- Known constraints: [e.g., external library limitations]

## Success Criteria

### Quantitative Metrics
[Smallest metric set needed to observe the Product Outcome]

### Qualitative Metrics
[Only decision-relevant qualitative evidence not covered by quantitative criteria]

### UI Quality Metrics (when feature includes UI)
[Only sourced UI quality or accessibility outcomes needed for acceptance]

## Technical Considerations

### Dependencies
- [Dependencies on existing systems]
- [Dependencies on external services]

### Constraints
- [Technical constraints]
- [Resource constraints]

### Assumptions (Unvalidated)
[Hypotheses that are NOT yet validated but the PRD proceeds with. These are explicit risks.]
- [ ] [Assumption 1 — confidence level, plan to validate]
- [ ] [Assumption 2 — confidence level, plan to validate]

### Risks and Mitigation
| Risk | Impact | Probability | Mitigation |
|------|--------|-------------|------------|
| [Only a current risk whose treatment changes scope, observable behavior, compatibility, or acceptance] | High/Medium/Low | High/Medium/Low | [Smallest sufficient treatment] |

## Undetermined Items

- [ ] [Question 1]: [Description of options or impacts]
- [ ] [Question 2]: [Description of options or impacts]

*Include only decisions whose answer can change the current outcome, included scope, exclusion, or acceptance criterion. Approval blocks only on an unresolved decision in that set; other unknowns remain in their owning section.*

## Appendix

### References
- [Related document 1]
- [Related document 2]
- [Prototype references from `docs/discovery/prototypes/`]

### Glossary
- **Term 1**: [Definition]
- **Term 2**: [Definition]
