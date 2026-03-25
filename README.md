# Claude Code Discover

[![Claude Code](https://img.shields.io/badge/Claude%20Code-Plugin-purple)](https://claude.ai/code)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

A Claude Code plugin that structures product context in your repo before implementation begins. Hypotheses, validation results, and PRDs live alongside your code — so when Claude builds your feature, it has access to rejected alternatives, unvalidated assumptions, and the evidence behind each decision.

Works standalone, or paired with [claude-code-workflows](https://github.com/shinpr/claude-code-workflows) for a full discovery-to-implementation cycle:

```
[claude-code-discover]  →  PRD + Prototypes  →  [claude-code-workflows]
   Discovery phase                                Implementation phase
```

## The Problem

When you ask an AI coding assistant to build a feature, it generates code without knowing what alternatives were ruled out, which assumptions are untested, or what user research shaped the requirements. Discovery artifacts typically live in Notion, Figma, or Slack — invisible to your coding tools. This plugin brings them into the repo where Claude can read them.

## What It Does

```
Vision & Personas        ← who you're building for and why
      ↓
  Opportunities          ← your hypotheses structured with validation plans
      ↓
  Blueprint              ← IA, user flows, content model, brand direction
      ↓
  Hypothesis Files       ← testable assumptions with success/failure criteria
      ↓
  Validation             ← assumption decomposition + HTML prototypes
      ↓
     PRD                 ← each user story traced to evidence
```

Each recipe is a step in this cycle. Run them in order or jump to where you need:

| Recipe | What it does |
|--------|-------------|
| `/discover:recipe-vision` | Define product vision, outcomes, and North Star Metric |
| `/discover:recipe-persona` | Create personas with JTBD, pains/gains, and behavioral data |
| `/discover:recipe-discover` | Structure your hypotheses into Opportunities with validation plans |
| `/discover:recipe-blueprint` | Define structural design foundation — IA, user flows, content model, brand direction, AI interaction model |
| `/discover:recipe-validate` | Decompose assumptions, design falsifiable tests, generate HTML prototypes |
| `/discover:recipe-reflect` | Extract learnings, promote knowledge across the hierarchy |
| `/discover:recipe-define` | Generate a PRD from validated hypotheses with confidence scores |

### What each recipe produces

- **Hypothesis file**: Markdown with assumption statement, success/failure criteria, confidence scores per risk dimension, time budget, and validation results
- **Blueprint artifacts**: Information architecture, user flows, content model, brand direction, and AI interaction model — shared structural context that prototypes reference for consistency
- **Prototype**: Single self-contained HTML file (~800-1200 lines) that opens in a browser. Deterministic mock data, all UI states implemented, design context applied from blueprint and project files
- **PRD**: 200-400 line document with user stories (each with 4 Risks confidence table), EARS-format acceptance criteria, unvalidated assumptions section, and references to hypothesis files

## How Validation Works

Each validation produces:
- Assumption breakdown (ranked by risk type and level)
- Test design per assumption (smallest test that could disprove it)
- HTML prototype (for user testing)

Two agents work in separate contexts:

1. **hypothesis-verifier** decomposes your hypothesis into assumptions, ranks them by risk, and designs the smallest test that could disprove each one — without seeing your expectations
2. **prototype-generator** reads your design principles, persona, hypothesis files, and blueprint artifacts (when available), then generates a self-contained HTML prototype with deterministic mock data and all UI states

The context separation is deliberate. The verifier designs tests that can fail. The prototype generator builds a product UI without test infrastructure leaking in.

## Connecting to Implementation

The PRD that `recipe-define` produces follows the standard structure that [claude-code-workflows](https://github.com/shinpr/claude-code-workflows) expects. Discovery extensions (hypothesis references, 4 Risks confidence per user story, unvalidated assumptions) are additive — they provide context without breaking compatibility. Prototypes generated during validation can be passed to the UI Spec designer as design references.

```bash
# Discovery phase (this plugin)
/discover:recipe-define → docs/prd/feature-prd.md

# Implementation phase (dev-workflows)
# UI Spec designer accepts PRD + optional prototype as input
/dev-workflows:recipe-implement "docs/prd/feature-prd.md"
```

The implementation workflow picks up the PRD, runs requirement analysis, creates design docs, and proceeds through the full development lifecycle with the discovery context preserved.

## Installation

> Requires [Claude Code](https://claude.ai/code)

```bash
# Start Claude Code
claude

# Install the marketplace
/plugin marketplace add shinpr/claude-code-discover

# Install plugin
/plugin install discover@claude-code-discover

# Reload plugins
/reload-plugins

# Start discovering
/discover:recipe-vision <your product>
```

### With claude-code-workflows

Install dev-workflows to get the full cycle from discovery to implementation. For projects with a frontend, install both backend and frontend plugins — dev-workflows handles backend logic and orchestration, while dev-workflows-frontend adds UI Spec generation and React-specific task execution:

```bash
/plugin marketplace add shinpr/claude-code-workflows

# Backend or general development
/plugin install dev-workflows@claude-code-workflows

# Frontend (install alongside dev-workflows for fullstack)
/plugin install dev-workflows-frontend@claude-code-workflows
```

## Repo Structure

As you use the recipes, artifacts accumulate in `docs/`:

```
docs/
├── product/             # Vision, personas, design principles, learnings
│   └── design/          # Blueprint: IA, user flows, content model, brand direction
├── discovery/           # Opportunities, hypotheses, prototypes, journeys
│   └── INDEX.md         # Auto-maintained summary of discovery status
└── prd/                 # PRDs ready for implementation
```

## Agents

Five specialized agents handle tasks where context separation matters:

| Agent | What it does | Why it runs in a separate context |
|-------|-------------|----------------------------------|
| `prd-reviewer` | Checks PRD completeness, consistency, and technical currency of dependencies | Catches gaps the author misses. Verifies external APIs are still available via web search |
| `codebase-analyzer` | Maps existing features, user roles, and architecture from code | Reports facts without hypothesis bias coloring the analysis |
| `hypothesis-verifier` | Decomposes hypotheses into assumptions, designs falsifiable tests | Designs tests that can actually fail, without seeing the author's expectations |
| `knowledge-distiller` | Extracts patterns across multiple hypothesis results | Finds cross-cutting learnings without being anchored to any single hypothesis |
| `prototype-generator` | Generates HTML prototypes from design context files | Builds product UIs isolated from test design details |

## Requirements

- Claude Code 1.0.33+

## License

MIT
