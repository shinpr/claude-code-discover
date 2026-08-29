# User Story Guide

## Purpose

Guide for writing user stories with 4 Risks assessment and Confidence Meter integration. User stories are the **minimum unit of value** in Discover.

## User Story Format

```
As a [user type]
I want to [goal/desire]
So that [expected value/benefit]
```

### Writing Good User Stories

- **User type**: Reference an evidenced persona or explicit user context that distinguishes the behavior
- **Goal/desire**: What the user wants to accomplish, not how the system works
- **Value/benefit**: Why this matters to the user. Must connect to an Opportunity

### INVEST Criteria

| Criterion | Description |
|-----------|-------------|
| **Independent** | Can be developed and delivered independently |
| **Negotiable** | Details can be discussed, not a rigid contract |
| **Valuable** | Delivers value to the user or business |
| **Estimable** | Team can estimate the effort |
| **Small** | Small enough to be delivered in a single iteration |
| **Testable** | Has clear acceptance criteria |

## 4 Risks Assessment

Every user story must assess Cagan's 4 Risks:

### Value Risk
- **Question**: Will users use this? Does it solve their problem?
- **Evidence types**: User interviews, usage data, prototype testing, competitive analysis
- **Low confidence indicators**: No user evidence, only stakeholder opinion, untested assumption

### Usability Risk
- **Question**: Can users figure out how to use it? Does the UX work?
- **Evidence types**: Prototype testing, usability studies, interaction patterns, accessibility audit
- **Low confidence indicators**: No prototype tested, complex interaction, new paradigm

### Feasibility Risk
- **Question**: Can we build it? Is the effort realistic?
- **Evidence types**: Code spike, architecture review, team expertise, dependency analysis
- **Low confidence indicators**: Unknown technology, complex integration, tight timeline

### Viability Risk
- **Question**: Does it work as a business? Can we explain why we're building it?
- **Evidence types**: Market analysis, business model fit, regulatory review, ROI analysis
- **Low confidence indicators**: Unclear revenue impact, regulatory uncertainty, misaligned with strategy

## Confidence Meter (0-10) per Risk

| Score | Meaning | Typical Evidence |
|-------|---------|------------------|
| 0-2 | Gut feeling / no evidence | Assumption only |
| 3-4 | Structured evaluation | Expert review, competitive analysis, scoring |
| 5-7 | Data-backed | Analytics, surveys, interview patterns |
| 8-10 | Tested and confirmed | Prototype validation, A/B test, beta results |

## "Validated Enough" Judgment

Not all stories need 8+ on every risk. The threshold depends on **cost x risk x reversibility**:

| Condition | Calibration Guide | Example |
|-----------|--------------------|---------|
| Low-cost, reversible | 3-4 on each risk | Feature flag experiment, UI tweak |
| Medium cost | 5-7 on each risk | New feature requiring 1-2 sprints |
| High-cost, irreversible | 8+ on each risk | Platform migration, pricing model change |

Use these ranges as calibration, not a fixed threshold. For each story, record current evidence and remaining uncertainty, reduce scope or increase reversibility where useful, and request further validation only when its result can change delivery readiness.

## User Story in PRD

In the PRD, each user story includes:

```markdown
#### US-N: [Story Title]

As a [persona name]
I want to [goal]
So that [benefit]

**4 Risks Confidence (0-10):**
| Risk | Score | Evidence | Remaining Risk |
|------|-------|----------|----------------|
| Value | N | [evidence] | [what's uncertain] |
| Usability | N | [evidence] | [what's uncertain] |
| Feasibility | N | [evidence] | [what's uncertain] |
| Viability | N | [evidence] | [what's uncertain] |

**Delivery readiness**: [validated enough / needs more validation]
**Rationale**: [cost x risk x reversibility justification]
```
