# AI Interaction Model Template

## Product: {product-name}

Apply this template to in-scope AI-powered features. Include a section only when it records a decision needed by the current feature or downstream consumer.

### AI Features Inventory

| Feature | User Goal | AI Role | Interaction Pattern | Linked Opportunity |
|---------|----------|---------|--------------------|--------------------|
| {feature} | {what user wants to accomplish} | {generate/suggest/assist/automate} | {chat/form/inline/background} | {OPP-NNN} |

### Interaction Pattern Decisions

For each in-scope AI feature, define the decisions that affect user control or observable behavior:

#### {Feature Name}

**Pattern**: {Chat / Form / Inline Suggestion / Hybrid / Background}

**Rationale**: {why this pattern fits the user's mental model and the design principles}

**UI Placement**: {full-screen / side panel / inline / modal / overlay}

**User Control Model**:
- Input method: {free text / structured form / guided prompts / selection}
- Preview: {real-time / on-submit / staged}
- Edit: {direct manipulation / re-prompt / both}
- Undo: {step-by-step / full reset / version history}

### AI Capability Boundaries

Define what the AI reliably handles vs. what it struggles with:

| Capability | Confidence | Constraint | Fallback |
|-----------|-----------|------------|----------|
| {what AI does} | {high/medium/low} | {known limitation} | {what happens when AI fails} |

### Response Display Strategy

| Scenario | Display Method | Rationale |
|----------|---------------|-----------|
| {observed or required wait condition} | {instant / progress / streaming / background / other} | {user and system evidence} |

### Error & Edge Case Taxonomy

| Error Type | User Sees | Recovery Action |
|-----------|-----------|----------------|
| {failure that can occur in the confirmed interaction} | {observable behavior} | {available recovery} |

### Human-AI Handoff Pattern

Define the ownership boundary only when AI output enters a human-controlled artifact or decision:

| Phase | Who Controls | What Changes |
|-------|-------------|-------------|
| {phase} | {user / AI / system} | {permitted change and approval boundary} |

### Transparency & Confidence Communication

Record disclosures and reliability signals required by user risk, regulation, or the confirmed product decision:

| Aspect | Decision | Rationale |
|--------|----------|-----------|
| AI disclosure | {how users know AI is involved — label, icon, explanation, none} | {trust/regulatory requirement} |
| Confidence indication | {how output certainty is communicated — explicit score, visual cue, hedging language, none} | {user expectation for accuracy} |
| Source attribution | {whether AI-generated content is labeled as such after creation} | {content ownership clarity} |
| Limitation visibility | {where/how AI limitations are communicated — onboarding, inline, help, none} | {error prevention} |

### Guardrails

| Guardrail | Implementation | User-Visible Behavior |
|-----------|---------------|----------------------|
| {boundary activated by current risk or policy} | {smallest enforcement mechanism} | {observable behavior} |

### AI Interaction Decisions Log

| Decision | Options Considered | Chosen | Rationale |
|----------|-------------------|--------|-----------|
| {decision} | {options} | {chosen} | {rationale} |
