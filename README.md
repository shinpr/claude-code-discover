# Claude Code Discover

[![Claude Code](https://img.shields.io/badge/Claude%20Code-Plugin-purple)](https://claude.ai/code)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

A Claude Code plugin that turns a feature idea or product question into an evidence-backed product requirements document (PRD) before implementation begins. It helps you decide what to build, test the assumptions that could change that decision, and carry the evidence into implementation.

Use it to:

- turn user research, product ideas, or an existing codebase into Opportunities and testable hypotheses
- validate value, usability, feasibility, and viability with a method suited to the risk
- define shared product structure when prototypes or downstream design need it
- produce a reviewed PRD with explicit scope, exclusions, remaining assumptions, and traceable evidence

The resulting artifacts live under `docs/` beside the code, so rejected alternatives and unresolved risks remain available when implementation starts.

Works standalone, or paired with [claude-code-workflows](https://github.com/shinpr/claude-code-workflows) for a full discovery-to-implementation cycle:

```
[claude-code-discover]  →  Reviewed PRD + validation evidence  →  [claude-code-workflows]
   Discovery                                                     Implementation
```

## Quick Start

> Requires Claude Code with plugin marketplace and Skills support.

```bash
# Start Claude Code
claude

# Add the marketplace and install the plugin
/plugin marketplace add shinpr/claude-code-discover
/plugin install discover@claude-code-discover
/reload-plugins

# Start from a user problem, feature idea, or existing evidence
/discover:recipe-discover "Describe the problem or feature idea"
```

For a new product or strategic reset, start with `/discover:recipe-vision` instead. You can also begin from an existing Opportunity or hypothesis; the recipes are entry points, not a mandatory sequence.

## Choose Where to Start

```
Idea or existing evidence
          ↓
Discover → Opportunities + hypotheses
          ↓
     Validate by risk ↔ Blueprint when shared structure is needed
          ↓
 Reflect completed evidence or Define a reviewed PRD
```

| Recipe | Use it when | Result |
|--------|-------------|--------|
| `/discover:recipe-vision` | You are starting a product or revisiting its direction | Vision, outcomes, and product principles |
| `/discover:recipe-persona` | You need a grounded view of who uses the product and in what context | Evidence-backed personas |
| `/discover:recipe-discover` | You have a problem, idea, research, or an existing product to examine | Opportunities, hypotheses, and validation priorities |
| `/discover:recipe-validate` | A hypothesis could change readiness or scope | Validation evidence and an updated hypothesis |
| `/discover:recipe-blueprint` | Prototypes or downstream design need shared product structure | IA, user flows, content model, and brand direction |
| `/discover:recipe-refine-visuals` | A prototype or downstream design workflow needs reproducible visual values | Concrete tokens in `brand-direction.md` |
| `/discover:recipe-reflect` | Validation results or product evidence should become reusable learning | Updated evidence, learnings, and discovery index |
| `/discover:recipe-define` | You are ready to make an implementation decision | An independently reviewed PRD |

## How Validation Works

Validation starts by identifying the assumption most likely to change the current product decision, then selects the smallest useful test for that uncertainty.

| Risk | Typical validation |
|------|--------------------|
| **Value** | Market research, interviews, competitive analysis, or a demand test |
| **Usability** | A self-contained HTML prototype and user testing |
| **Feasibility** | Repository analysis, dependency review, or an isolated code spike |
| **Viability** | Business-model, financial, or regulatory analysis |

Every validation updates the hypothesis with its result and evidence. A prototype is produced only when the selected usability test needs one.

## Connecting to Implementation

`recipe-define` compares the proposed work's cost, risk, and reversibility with the available evidence. It asks for more validation only when the result could change implementation readiness or scope. It then writes the PRD to `docs/prd/` and runs an independent review before asking for approval. Prototypes from usability validation can accompany the PRD as design references.

The PRD can be handed to [claude-code-workflows](https://github.com/shinpr/claude-code-workflows) for design and implementation:

```bash
/dev-workflows:recipe-implement "docs/prd/feature-prd.md"
```

See the linked project for current installation instructions and workflow options.

## Repo Structure

Recipes create or update the relevant files under `docs/`:

```
docs/
├── product/             # Vision, personas, design principles, learnings
│   └── design/          # Blueprint: IA, user flows, content model, brand direction
├── discovery/           # Opportunities, hypotheses, prototypes, journeys
│   └── INDEX.md         # Auto-maintained summary of discovery status
└── prd/                 # PRDs ready for implementation
```

## Agents

Five agents run in separate contexts for independent analysis:

| Agent | What it does | Why it runs in a separate context |
|-------|-------------|----------------------------------|
| `prd-reviewer` | Checks each PRD against its outcome, evidence, scope, and downstream needs | Re-checks evidence and boundaries outside the authoring conversation |
| `codebase-analyzer` | Maps decision-relevant features, user roles, and architecture from code | Separates what the product currently does from evidence about what users need |
| `hypothesis-verifier` | Decomposes hypotheses into assumptions and designs falsifiable tests | Challenges the hypothesis outside the authoring conversation before validation begins |
| `knowledge-distiller` | Extracts patterns across multiple hypothesis results | Finds cross-cutting learnings without being anchored to any single hypothesis |
| `prototype-generator` | Generates HTML prototypes from design context files | Builds product UIs isolated from test design details |

## License

MIT
