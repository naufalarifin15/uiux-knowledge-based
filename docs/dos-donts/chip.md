# Chip

## Function & When to Use
Chip displays a compact unit of information, and can be used in 2 modes:
- **Static** — as a tag, status label, or category that's only displayed (no `closable`, no need to handle `click`)
- **Interactive** — as an active filter, a multi-select result, or an element that can be clicked/removed via the `click`/`close` event

Chip is more flexible than Badge because it has a richer variety of `appearance` (solid/outline) and `size` options, making it suitable for status/tags that need different visual emphasis even when not interactive at all.

## Variant Guide

**Dimension 1 — Variant (color function/meaning)**
| Value | Function | When to Use |
|---|---|---|
| `default` | Neutral | General tags/categories with no status meaning |
| `info` | Neutral information | Flags additional info |
| `success` | Positive status | Flags a successfully/actively positive condition |
| `warning` | Warning | Flags a condition that needs caution |
| `error` | Failure/critical condition | Flags a problematic condition |
| `disabled` | Visually inactive | A disabled chip — **see the note on overlap with the `disabled` prop below** |
| `custom` | Custom | For cases not covered by the other semantic variants — use with caution to avoid violating DS color consistency |

**Dimension 2 — Appearance (visual only, doesn't affect meaning)**
| Value | Visual | When to Use |
|---|---|---|
| `solid` | Full background color | Chip needs to stand out more, e.g. a currently active filter |
| `outline` | Border only, transparent/white background | Chip with lighter visual emphasis, e.g. a tag in a long list |

**Dimension 3 — Size**
| Value | When to Use |
|---|---|
| `sm` | Dense contexts, e.g. many chips lined up in one row |
| `md` | Default — general contexts |
| `lg` | Chip as an element that needs to stand out more |

**Dimension 4 — Composition**
| Element | Prop | When to Enable |
|---|---|---|
| Left icon | `iconLeft` | Extra visual context before the label, e.g. a category icon |
| Right icon | `iconRight` | Additional indication after the label |
| Close button (×) | `closable` | When the chip represents a selection the user can remove (e.g. an active filter, a selected tag) |

## ✅ Do
- Use Chip **without `closable`** when it only functions as a static tag/status/label (e.g. an "Active" status, an item category in a table) — not every Chip needs to be interactive.
- Use `closable` for chips that represent a user-cancellable selection (active filters, multi-select results) — listen for the `close` event to remove that item from the data, not the `click` event.
- Use the `click` event for actions other than removal, e.g. navigation or toggling detail — make sure the chip's click area and the close button don't overlap functionally.
- Choose the variant based on status meaning, same as Alert/Badge — `error` for problematic conditions, not just a color that happens to contrast.
- Use `outline` when many chips are lined up in a long list, so it doesn't get visually too busy compared to `solid`.

## ❌ Don't
- Don't use the `custom` variant as the default choice — it's for exception cases, not an alternative to the existing semantic variants.
- Don't enable `closable` for chips that are informational/static in nature (e.g. a read-only category label) — a non-functional close button will confuse users.
- Don't mix `solid` and `outline` within the same group of similar chips (e.g. a list of active filters) — appearance consistency matters for the same group.
- Don't use `className` to override a color that's already available via a variant — pick the matching variant, or use `custom` as a last resort.

## Additional Context
- `variant="disabled"` (color style) and the `disabled` prop (boolean, interaction) are 2 different things that can be combined — `disabled` (boolean) controls whether the chip can be interacted with, while `variant="disabled"` is just visual styling. Make sure they're consistent: if the chip really can't be interacted with, set `disabled=true` AND `variant="disabled"` together, not just one of them.
- The `click` and `close` events can occur independently — make sure the `close` handler doesn't also trigger logic that should only run on `click`, or vice versa.