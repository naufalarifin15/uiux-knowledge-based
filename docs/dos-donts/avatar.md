# Avatar

## Function & When to Use
Avatar displays a visual representation of a user/entity (profile photo, initials, or a generic icon). Used in places that need quick identification of who/what a piece of data relates to — e.g. profile headers, user lists, comments, tables with an "assigned to" column.

## Variant Guide

**Dimension 1 — Size**
| Value | When to Use |
|---|---|
| `xs` | Very dense contexts, e.g. stacked avatars or inside a badge/notification |
| `sm` | Inside a list/table row, comment thread |
| `md` | Default — general contexts, e.g. item cards, user dropdowns |
| `lg` | Section headers, user detail cards |
| `xl` | Profile pages, user detail modals |
| `2xl` | Main profile page / hero section, as the main visual element on screen |

**Dimension 2 — Fallback Behavior**
| Value | Behavior | When to Use |
|---|---|---|
| `with fallback` | The fallback (e.g. initials/icon) is set manually via a prop, used when an image isn't available | When explicit control over the displayed fallback is needed (e.g. custom initials, a special icon per context) |
| `auto fallback` | The fallback is generated automatically by the component (e.g. from a given name) without needing an extra prop | When the available data is already sufficient (e.g. a name field exists) and manual fallback customization isn't needed |

> Note: make sure this understanding matches the package's actual implementation — if `auto fallback` generates initials from a specific prop (e.g. `name`), make sure that prop is always filled when using this mode, or the fallback may end up empty or incorrect.

## ✅ Do
- Be consistent and use one size within the same context (e.g. all avatars in the same list use `sm`, don't mix `sm` and `md` in one list).
- Use `auto fallback` as the default when name/identity data is already available from the data source — reduces manual work and keeps things consistent.
- Use `with fallback` when a fallback that can't be automatically derived is needed, e.g. a generic icon for non-user entities (e.g. an avatar for "System"/"Bot").
- Match the size to the page's visual hierarchy — elements with a more important/prominent focus role (e.g. a main profile) should use a larger size (`xl`/`2xl`).

## ❌ Don't
- Don't use large sizes (`xl`/`2xl`) inside a list/table — it will break the layout and look disproportionate to the other content.
- Don't mix `with fallback` and `auto fallback` for the exact same case (e.g. between items in the same user list) — pick one consistent approach.
- Don't let `auto fallback` be used without sufficient data (e.g. an empty name) — make sure there's data validation before rendering, so an empty/broken avatar doesn't appear.

## Additional Context
- Avatar size should stay consistent with the surrounding components (e.g. the size of an adjacent name text) to keep the visual ratio balanced.