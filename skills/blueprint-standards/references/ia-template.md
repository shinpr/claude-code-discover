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

### Navigation Model

| Element | Type | Visible To | Content |
|---------|------|-----------|---------|
| {nav-element} | Global / Contextual / Utility | {roles} | {items} |

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
