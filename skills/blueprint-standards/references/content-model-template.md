# Content Model Template

## Product: {product-name}

### Entity Overview

List all content types the product manages.

| Entity | Description | Created By | Visible To | Linked Opportunity |
|--------|-------------|-----------|------------|-------------------|
| {entity} | {what it represents} | {persona/system} | {who sees it} | {OPP-NNN} |

### Entity Definitions

#### {Entity Name}

**Purpose**: {why this entity exists in the product}

**Attributes**:

| Attribute | Type | Required | Description |
|-----------|------|----------|-------------|
| {name} | {text/number/date/enum/reference} | {yes/no} | {what it represents} |

**Relationships**:

| Related Entity | Relationship | Cardinality | Description |
|---------------|-------------|-------------|-------------|
| {entity} | {has-many/belongs-to/has-one} | {1:N/N:M/1:1} | {context} |

**States** (if stateful):

| State | Meaning | Transitions To | Trigger |
|-------|---------|---------------|---------|
| {state} | {description} | {next states} | {what causes transition} |

### Entity Relationship Diagram

```
[Entity A] 1──N [Entity B] N──M [Entity C]
                     │
                     1
                     │
                     N
               [Entity D]
```

### Display Contexts

Where and how each entity appears in the IA:

| Entity | List View | Detail View | Creation | Embedded In |
|--------|----------|------------|----------|-------------|
| {entity} | {page} | {page} | {page/flow} | {other entity's detail} |

### Content Model Decisions Log

| Decision | Options Considered | Chosen | Rationale |
|----------|-------------------|--------|-----------|
| {decision} | {options} | {chosen} | {rationale} |
