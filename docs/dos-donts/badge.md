# Badge

## Function & When to Use
Badge displays a short indicator — either a number (counter) or a small status marker — usually attached to the corner of another element (icon, avatar, menu item) to flag the count/presence of something that needs attention (e.g. unread notifications, number of new items).

## Variant Guide

**Dimension 1 — Size**
| Value | Shape | When to Use |
|---|---|---|
| `lg` | Pill with a number, large size | Counter with an important value that needs to stand out, e.g. a badge in the main navigation |
| `md` | Pill with a number, medium size | Default — general contexts |
| `sm` | Pill with a number, small size | Dense contexts, e.g. a small badge inside a list item |
| `dot-xs` | Plain dot with no number, small size | Only needs to flag "there's something new/unread" without needing to know the exact count |
| `dot-2xs` | Plain dot with no number, smallest size | Same as `dot-xs`, used when space is very limited (e.g. attached to a small icon) |

> `lg`/`md`/`sm` sizes display a number/counter (e.g. `99+`, `9+`, `5`), while `dot-xs`/`dot-2xs` **don't display a number at all** — just a dot as a presence indicator.

**Dimension 2 — Semantic Variant (function/meaning)**
| Value | Function | When to Use |
|---|---|---|
| `error` | Failure/critical condition | Flags an item that needs immediate attention |
| `warning` | Warning | Flags a condition that needs caution but isn't critical yet |
| `success` | Positive status | Flags a successful/completed condition |
| `info` | Neutral information | Flags additional info with no good/bad implication |
| `default` | Neutral, no semantic color | A general counter with no specific status meaning (e.g. a regular message count) |

**Dimension 3 — Tone (visual only, doesn't affect meaning)**
| Value | Visual | When to Use |
|---|---|---|
| `solid` | Full background color, high contrast | Badge needs to grab attention immediately (default for important notifications) |
| `soft` | Soft/pastel background color | Badge in a visually dense context, shouldn't be too dominant |

## ✅ Do
- Use `dot-xs`/`dot-2xs` when the exact count doesn't matter to the user — it's enough to know "there's something new," e.g. a red dot on a notification icon.
- Use sizes with a number (`lg`/`md`/`sm`) when the exact count is relevant to the user's decision, e.g. the number of unread messages they need to know.
- Match the badge size to the size of the element it's attached to — an `lg` badge on top of a small icon will look disproportionate.
- Choose the semantic variant based on meaning, just like Alert — `error` for critical conditions, not just a color that happens to look contrasting.

## ❌ Don't
- Don't use dot sizes (`dot-xs`/`dot-2xs`) in places that need to display a number — a dot has no slot for text/numbers at all.
- Don't mix `solid` and `soft` tones for similar badges within the same UI group (e.g. several notification badges side by side).
- Don't use the `default` variant for a condition that actually has a clear semantic meaning (e.g. error) — it removes an important signal for the user.

## Additional Context
- For counters with large values, make sure the number truncation format (e.g. `99+`) follows the limit already defined in the package — don't hardcode it manually at the page implementation level.