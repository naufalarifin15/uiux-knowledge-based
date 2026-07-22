# Divider

## Function & When to Use
Divider is a horizontal separator line for visually separating sections/groups of content, without needing a separate container/card. Used when you need a light separator between sections within the same page/card.

## Variant Guide

**Dimension 1 — Size (line height in px)**
| Value | Height | When to Use |
|---|---|---|
| `'1'` | 1px | Default — standard/thin separator, suitable for most cases |
| `'2'` | 2px | A slightly more pronounced separator |
| `'4'` | 4px | Separator between large sections that need stronger visual distance |
| `'8'` | 8px | The thickest separator, used for major section separation (rarely used) |

**Dimension 2 — Type (stroke color)**
| Value | Color | When to Use |
|---|---|---|
| `'soft'` | Lighter (`#f5f5f4`) | Default — a subtle separator that doesn't draw too much attention |
| `'hard'` | Darker (`#e7e5e4`) | A separator that needs to be a bit more visible/pronounced |

## ✅ Do
- Use size `'1'` + type `'soft'` (default) for most cases of separating regular sections.
- Only increase the size when you genuinely need significant visual emphasis on the distance between sections — don't make a large size the default without reason.
- Use type `'hard'` when the divider needs to stay clearly visible against a background that's also light (e.g. a white card on a white background).

## ❌ Don't
- Don't use Divider as a substitute for spacing/margin — if the goal is just to add distance without needing a visible line, use a spacing token, not a divider with a large size whose color is disguised.
- Don't mix different sizes for separators at the same level (e.g. between similar list items) — size consistency matters for a clear visual hierarchy.
- Don't override the color via `className` — use the already-available `type` (`soft`/`hard`) instead.

## Additional Context
- Size and type are independent of each other — any combination (e.g. size `'8'` with type `'soft'`) is still valid; choose both based on their respective needs (thickness vs. color contrast).