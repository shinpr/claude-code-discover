# Brand Direction Template

## Product: {product-name}

### Design Vision

{1-2 sentences from docs/product/vision.md Design Vision section — how the product should feel}

### Tone & Voice

| Dimension | Position | Rationale (design principle) |
|-----------|----------|------------------------------|
| Formal ↔ Casual | {position} | {which principle drives this} |
| Serious ↔ Playful | {position} | {which principle drives this} |
| Expert ↔ Approachable | {position} | {which principle drives this} |
| Technical ↔ Plain | {position} | {which principle drives this} |

### Color Direction

| Role | Intention | Reference | Traced To |
|------|-----------|-----------|-----------|
| Primary | {what action/meaning} | {color family or reference} | {design principle} |
| Surface | {background feel} | {warm/cool/neutral} | {design principle} |
| Accent | {emphasis/highlight} | {color family or reference} | {design principle} |
| Success | {positive feedback} | {color family} | Standard |
| Error | {negative feedback} | {color family} | Standard |

This is **directional**, not a final token system. Concrete values for prototype consistency are derived in Visual Tokens below. Final production values are determined during UI Spec.

### Typography Direction

| Role | Intention | Reference |
|------|-----------|-----------|
| Heading | {personality, weight} | {font family or style reference} |
| Body | {readability, density} | {font family or style reference} |
| UI / Label | {clarity, compactness} | {font family or style reference} |

**Language consideration**: {product's primary language and implications for font selection}

### Motion Tendency

| Dimension | Direction | Rationale |
|-----------|-----------|-----------|
| Transitions | {none / subtle fade / spring animations} | {tone & voice alignment} |
| Micro-interactions | {none / hover feedback only / expressive on all interactions} | {persona context — expertise, device} |
| Loading states | {static spinner / skeleton screens / progressive reveal} | {perceived performance priority} |

### Visual Density

| Dimension | Direction | Rationale |
|-----------|-----------|-----------|
| Whitespace | {generous / moderate / compact} | {persona context — device, environment} |
| Information density | {sparse / balanced / dense} | {persona expertise level} |
| Card / Surface elevation | {flat / subtle / layered} | {design principle} |

### Reference Products

Products whose visual approach aligns with the intended direction:

| Product | What to Reference | What to Avoid |
|---------|------------------|---------------|
| {product} | {specific aspect} | {specific aspect} |

### Visual Tokens

Concrete values derived from the direction above. Auto-generated during blueprint, optionally refined by a design expert via `recipe-refine-visuals`.

**Source**: {`auto-derived` | `expert-refined`}

#### Color Tokens

| Token | Value | Derived From |
|-------|-------|-------------|
| `--color-primary` | {hex} | Color Direction → Primary |
| `--color-primary-hover` | {hex} | Primary darkened 10% |
| `--color-surface` | {hex} | Color Direction → Surface |
| `--color-surface-elevated` | {hex} | Surface lightened/darkened for elevation |
| `--color-accent` | {hex} | Color Direction → Accent |
| `--color-text` | {hex} | Contrast against surface |
| `--color-text-secondary` | {hex} | Reduced emphasis text |
| `--color-success` | {hex} | Color Direction → Success |
| `--color-error` | {hex} | Color Direction → Error |
| `--color-border` | {hex} | Surface-derived, low opacity |

#### Typography Tokens

| Token | Value | Derived From |
|-------|-------|-------------|
| `--font-heading` | {font family} | Typography Direction → Heading |
| `--font-body` | {font family} | Typography Direction → Body |
| `--font-ui` | {font family} | Typography Direction → UI / Label |
| `--font-size-base` | {px/rem} | Visual Density → Information density |
| `--font-weight-normal` | {weight} | Body readability |
| `--font-weight-bold` | {weight} | Heading emphasis |
| `--line-height-body` | {ratio} | Body readability |

#### Spacing Tokens

| Token | Value | Derived From |
|-------|-------|-------------|
| `--space-unit` | {px} | Visual Density → Whitespace |
| `--space-xs` | {px} | unit × 0.5 |
| `--space-sm` | {px} | unit × 1 |
| `--space-md` | {px} | unit × 2 |
| `--space-lg` | {px} | unit × 3 |
| `--space-xl` | {px} | unit × 5 |
| `--radius-sm` | {px} | Visual Density → Surface elevation |
| `--radius-md` | {px} | Visual Density → Surface elevation |
| `--shadow-sm` | {value} | Visual Density → Card elevation |
| `--shadow-md` | {value} | Visual Density → Card elevation |

### Brand Direction Decisions Log

| Decision | Options Considered | Chosen | Rationale |
|----------|-------------------|--------|-----------|
| {decision} | {options} | {chosen} | {rationale} |
