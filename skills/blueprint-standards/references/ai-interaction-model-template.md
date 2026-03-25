# AI Interaction Model Template

## Product: {product-name}

This template is for products that include AI-powered features (LLM chat, generative UI, AI-assisted creation, etc.). Skip this artifact if the product has no AI interaction.

### AI Features Inventory

| Feature | User Goal | AI Role | Interaction Pattern | Linked Opportunity |
|---------|----------|---------|--------------------|--------------------|
| {feature} | {what user wants to accomplish} | {generate/suggest/assist/automate} | {chat/form/inline/background} | {OPP-NNN} |

### Interaction Pattern Decisions

For each AI feature, define the interaction model:

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
| Short response (< 3s) | {spinner / skeleton / instant} | {user expectation} |
| Long generation (3-30s) | {streaming / progressive / staged reveal} | {perceived performance} |
| Very long (> 30s) | {background + notification / chunked delivery} | {user can do other things} |

### Error & Edge Case Taxonomy

| Error Type | User Sees | Recovery Action |
|-----------|-----------|----------------|
| Generation failure | {message} | {retry / fallback / manual entry} |
| Inappropriate output | {message} | {regenerate / report / edit} |
| Timeout | {message} | {retry / queue / simplify request} |
| Low confidence output | {message} | {review prompt / accept with warning} |
| Rate limit | {message} | {wait indicator / queue position} |

### Human-AI Handoff Pattern

Define the boundary between AI-generated and human-edited content:

```
[User Input] → [AI Generation] → [Preview/Review] → [User Edit] → [Publish/Save]
                                        ↑                   │
                                        └── Re-generate ────┘
```

| Phase | Who Controls | What Changes |
|-------|-------------|-------------|
| Input | User | Request / prompt |
| Generation | AI | Draft output |
| Review | User | Accept / reject / modify |
| Edit | User | Fine-tune details |
| Re-generate | User triggers, AI executes | Partial or full regeneration |

### Guardrails

| Guardrail | Implementation | User-Visible Behavior |
|-----------|---------------|----------------------|
| Content safety | {moderation layer / output filtering} | {message when triggered} |
| Scope limitation | {prompt constraints / output validation} | {what AI refuses to do} |
| Quality gate | {validation rules / confidence threshold} | {warning or block} |

### AI Interaction Decisions Log

| Decision | Options Considered | Chosen | Rationale |
|----------|-------------------|--------|-----------|
| {decision} | {options} | {chosen} | {rationale} |
