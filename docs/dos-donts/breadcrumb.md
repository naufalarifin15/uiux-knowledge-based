# Breadcrumb

## Function & When to Use
Breadcrumb displays a hierarchical navigation trail (e.g. `Home > Category > Current Page`), helping users know their position within the page structure and letting them quickly go back to a previous level. Used on pages with more than 1 level of navigation depth (not on top-level pages like Dashboard).

> Breadcrumb doesn't have size/color variants like other components — its structure is determined more by **props** (`items`, `separator`), so this documentation focuses on how to fill in the props correctly rather than variant selection.

## Props Structure

**Breadcrumb**
| Prop | Type | Default | Description |
|---|---|---|---|
| `items` | `BreadcrumbItem[]` | `[]` | Array of breadcrumb items, ordered from the topmost level to the current level |
| `separator` | `any` | chevron icon (default) | Custom separator between items, can be a string or a Component |

**BreadcrumbItem**
| Field | Type | Description |
|---|---|---|
| `label` | `string` | The displayed text |
| `href` | `string` (optional) | Destination URL — **must be left empty for the last item (current page)** |

## ✅ Do
- Always order `items` from the topmost level (root) to the current level, matching the actual navigation hierarchy — don't shuffle or reverse it.
- Leave `href` empty (omit it) on the last item, since that item represents the currently active page and shouldn't be clickable/navigate to itself.
- Fill in `href` for all items before the last one, so users can click back to any level above.
- Use a custom `separator` only if there's a specific visual requirement — the default (chevron icon) is sufficient for most cases.

## ❌ Don't
- Don't fill in `href` on the last item — it will make the current page look like a clickable link, when it should be static/non-interactive.
- Don't use Breadcrumb for pages with a flat/1-level hierarchy (e.g. directly under Dashboard) — it adds no extra navigational value and only adds visual noise.
- Don't hardcode a `label` that differs from the actual page/menu title — the breadcrumb must stay consistent with the related page title so it doesn't confuse the user.

## Additional Context
- Since `items` is a dynamic array, make sure it's generated consistently with the routing structure (`docs/PRD.md` Sitemap section) — the breadcrumb should ideally be derived automatically from the route path, not written manually per page.