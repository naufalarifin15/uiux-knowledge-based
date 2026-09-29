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

**Dimension 3 — Initial Length (for initials fallback)**
| Value | When to Use |
|---|---|
| `1 letter` | Very tight/dense contexts (typically paired with `xs` size), or when only a single identifiable word exists (e.g. a one-word entity name) |
| `2 letters` | Default — most common case, e.g. first name + last name initials |
| `3 letters` | When more differentiation is needed between similar users/entities (e.g. avoiding collisions when several people share the same 2-letter initials), or for a name/entity with three distinguishing words |

Available at all sizes, same as Dimension 1 — this dimension controls how many characters are shown, not how large the avatar is.

The number of letters is a **per-project choice**, not something automatically derived from name data (e.g. don't assume 2-word names always get `2 letters`) — pick the length that fits that project's context and space constraints, and apply it consistently within that project/context once chosen.

## ✅ Do
- Be consistent and use one size within the same context (e.g. all avatars in the same list use `sm`, don't mix `sm` and `md` in one list).
- Use `auto fallback` as the default when name/identity data is already available from the data source — reduces manual work and keeps things consistent.
- Use `with fallback` when a fallback that can't be automatically derived is needed, e.g. a generic icon for non-user entities (e.g. an avatar for "System"/"Bot").
- Match the size to the page's visual hierarchy — elements with a more important/prominent focus role (e.g. a main profile) should use a larger size (`xl`/`2xl`).
- Keep initial length consistent within the same context (e.g. all avatars in one user list use `2 letters`) — don't let it vary per row for no reason.
- Reserve `3 letters` for cases with a genuine need for differentiation, not as a default — it reads as more crowded than `1`/`2 letters`.

## ❌ Don't
- Don't use large sizes (`xl`/`2xl`) inside a list/table — it will break the layout and look disproportionate to the other content.
- Don't mix `with fallback` and `auto fallback` for the exact same case (e.g. between items in the same user list) — pick one consistent approach.
- Don't let `auto fallback` be used without sufficient data (e.g. an empty name) — make sure there's data validation before rendering, so an empty/broken avatar doesn't appear.
- Don't use `3 letters` at `xs` size — three characters in the smallest size become illegible; if that combination seems needed, drop to `2 letters` or increase the size instead.
- Don't mix different initial lengths within the same list/group (e.g. some avatars showing 2 letters, others showing 3) — pick one length for that context and apply it uniformly.

## Additional Context
- Avatar size should stay consistent with the surrounding components (e.g. the size of an adjacent name text) to keep the visual ratio balanced.
- Initial length (Dimension 3) and Fallback Behavior (Dimension 2) work together: initial length only applies when the fallback being shown is text-based initials — it has no effect when the fallback is a generic icon or when an actual image is loaded successfully.