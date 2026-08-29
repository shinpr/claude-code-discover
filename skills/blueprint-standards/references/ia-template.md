# Information Architecture Template

## Product: {product-name}

### Site Map

Organize pages hierarchically. Mark each page with its primary role and target persona.

```
/ (Root)
├── {page-name} — {role} [{persona}]
│   ├── {sub-page} — {role} [{persona}]
│   └── {sub-page} — {role} [{persona}]
├── {page-name} — {role} [{persona}]
└── ...
```

**Role types**: Landing, Dashboard, Creation, Detail, Transaction, Settings, Discovery

### Labeling & Taxonomy

| Aspect | Decision |
|--------|----------|
| Navigation labels | {user-facing terminology for menu items — derived from user mental model, not internal naming} |
| Content categories | {how content is grouped for browsing — e.g., by type, by topic, by persona} |
| Search strategy | {primary discovery method: navigation-driven / search-driven / hybrid} |

### Navigation Model

Use step indicators for linear task flows such as onboarding or checkout; add navigation where it supports an evidenced route or exit.

| Element | Type | Visible To | Content |
|---------|------|-----------|---------|
| {nav-element} | Global / Contextual / Utility / Step indicator | {roles} | {items} |

### Page Inventory

For each page, define:

#### {Page Name}

- **URL pattern**: `/{path}`
- **Purpose**: {one sentence — what the user accomplishes here}
- **Primary persona**: {persona name}
- **Linked Opportunity**: {OPP-NNN or "Supporting function"}
- **Key content**: {what data is displayed or manipulated}
- **Entry points**: {how users arrive — navigation, link, redirect}
- **Exit points**: {where users go next}

### Multi-sided Considerations

For marketplace/platform products, define both sides:

| Aspect | Side A ({role}) | Side B ({role}) |
|--------|----------------|----------------|
| Entry page | | |
| Core loop | | |
| Connection points | | |
| Shared pages | | |

### IA Decisions Log

| Decision | Options Considered | Chosen | Rationale (linked to design principle) |
|----------|-------------------|--------|----------------------------------------|
| {decision} | {options} | {chosen} | {rationale} |
