# Typography

## Function & When to Use
Typography is a generic text component that provides a size/weight scale matching the design system, with a **separation between visual style (`variant`) and semantic HTML tag (`as`)**. Used for almost all text in the application to stay consistent with the type scale, instead of writing plain `<h1>`/`<p>` with manual styling.

## Variant Guide

**Dimension 1 — Variant (visual style: size & weight)**
| Value | When to Use |
|---|---|
| `'title1'` | Page title or main section title |
| `'title2'` | Sub-section title |
| `'subtitle1'` | Title-supporting text (larger) |
| `'subtitle2'` | Title-supporting text (smaller) |
| `'body1'` | Main paragraph text — default |
| `'caption1'` | Small labels and annotations |
| `'caption2'` | Smallest-sized detail text |

**Dimension 2 — `as` (semantic HTML tag, independent from `variant`)**
Determines the actual HTML element rendered (`h1`, `h2`, ..., `p`, `span`, `div`), **separate from its visual style**. This matters for document hierarchy/accessibility — a large visual appearance (`variant="title1"`) doesn't always have to be an `<h1>` semantically; it depends on its position within the page structure.

## Props Structure

| Prop | Type | Default | Description |
|---|---|---|---|
| `variant` | `'title1'` \| `'title2'` \| `'subtitle1'` \| `'subtitle2'` \| `'body1'` \| `'caption1'` \| `'caption2'` | `'body1'` | Visual style (size & weight) |
| `bold` | `boolean` | `false` | Applies additional bold weight on top of the chosen variant |
| `as` | `'h1'` \| `'h2'` \| ... \| `'p'` \| `'span'` \| `'div'` | — | The HTML tag rendered |

**Slot**
| Slot | Description |
|---|---|
| `default` | Text content |

## ✅ Do
- Choose `variant` based on **visual need** (how large/prominent the text should look).
- Choose `as` based on **the text's position within the document hierarchy** — make sure the heading order (`h1` → `h2` → `h3`, etc.) is logical and doesn't skip levels purely for visual reasons. Ideally there's only 1 `h1` per page.
- Combine both independently when needed — e.g. text that needs to look large (`variant="title1"`) but is semantically an `h3` level within the page structure (`as="h3"`) is valid and intentional by this component's design.
- Use `as="span"` or `as="div"` for text that isn't part of the heading hierarchy or a paragraph that needs to be read by screen readers as its own block (e.g. an inline label).
- Use `bold={true}` for extra emphasis within the same variant (e.g. 1 word that needs to stand out within a `body1` paragraph), rather than switching to a larger `variant` just for the bold effect.

## ❌ Don't
- Don't assume `variant="title1"` is automatically rendered as `<h1>` — these two props are independent; `as` must be set explicitly based on the actual document structure.
- Don't decide `as` based on the desired appearance (e.g. using `h1` just to "look big") — the heading order must follow the page's information structure, not visual preference. For visual needs, change `variant` instead.
- Don't skip heading levels for visual reasons (e.g. jumping straight to `as="h4"` after `h1` because `h2`/`h3` "look too big") — if the size doesn't fit, change `variant`, not `as`.
- Don't write native text elements (`<h1>`, `<p>`, etc.) with manual styling outside this component for content that should stay consistent with the type scale.

## Additional Context
- Since this `variant`/`as` separation is fairly unique compared to other components, make sure the team/Claude Code always fills in both deliberately (not just one) — if `as` isn't set, check the component's default behavior (it likely falls back to a generic element like `div`/`span`) before assuming it automatically follows `variant`.