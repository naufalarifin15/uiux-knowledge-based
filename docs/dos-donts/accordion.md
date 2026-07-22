# Accordion

## Function & When to Use
Accordion hides/shows content vertically to save space, with a title that's always visible and content that can be toggled. Good for content that doesn't all need to be seen at once (FAQ, additional details, optional form sections).

**Don't confuse it with Tabs** — Tabs are for equivalent/parallel content where the user only needs to see one at a time without long scroll history, while Accordion is for content that naturally stacks vertically and can be collapsed.

## Variant Guide
Accordion has 2 independent variant dimensions — combining them gives 4 variants: `semi-single`, `semi-multiple`, `full-single`, `full-multiple`.

**Dimension 1 — Behavior (open/close interaction)**
| Value | Behavior | When to Use |
|---|---|---|
| `single` | Only 1 item can be open at a time. Opening another item automatically closes the currently open one. | Content between items is mutually exclusive / doesn't need to be compared side by side. Good for FAQs, step-by-step. |
| `multiple` | All items can be open at the same time, independent of each other. Opening a new item doesn't close others. | Content between items needs to be compared/viewed together. Good for form sections, filter groups. |

**Dimension 2 — Border style (visual only, doesn't affect behavior)**
| Value | Visual | When to Use |
|---|---|---|
| `semi` | Only a divider line between items, no border surrounding the whole component | Accordion blends in with other surrounding sections/cards, needs a lighter look |
| `full` | Each item has a full border/stroke surrounding it | Accordion stands alone as a clearly defined visual block, separate from surrounding elements |

> Border style (`semi`/`full`) is purely a visual choice — **it must not be used as a reason to pick a behavior** (`single`/`multiple`). These two dimensions are independent and should be decided based on different needs: border from the surrounding visual context, behavior from the nature of the content.

## ✅ Do
- Use `single` as the default when there's no explicit requirement for comparing items — this behavior is more common and easier for users to follow (reduces long scrolling caused by many items being open at once).
- Use `multiple` when the user needs to compare the contents of several items at once, e.g. several related form sections.
- Choose `full` when the accordion needs to stand on its own and be clearly separated from other surrounding content (e.g. within a page that has many other elements).
- Choose `semi` when the accordion is already inside another container/card, to avoid stacked (double) borders.
- Example: FAQ (mutually exclusive questions, no need to compare) → `behavior="single"` + `border="semi"`. A form with several sections that need to be viewed together → `behavior="multiple"` + `border="full"`.

## ❌ Don't
- Don't use `multiple` for content that's naturally exclusive (e.g. a step-by-step wizard) — users can get confused if several steps are open at once when they should be sequential.
- Don't use `full` inside a card/container that already has its own border — this results in stacked (double) borders that look untidy.
- Don't assume `single` = `semi` or `multiple` = `full`. All four combinations are valid and independent; don't pick a border style based on behavior or vice versa.

## Additional Context
- The default state (which item is open on first render) needs to be set explicitly based on the page's needs — don't leave everything closed if one of the items contains important information that should be visible right away.
- For `behavior="single"`, make sure the open/close transition (collapse animation) doesn't cause a disruptive layout shift if the accordion is above the fold/viewport.