# Illustration

## Function & When to Use
Illustration conveys the meaning of a state visually — used to reinforce empty, error, or success conditions, or to add visual context to informational moments (e.g. an upload area, a consultation screen). Illustration is decorative/supportive, not interactive — it should always be paired with a short supporting message, and with an action (e.g. Retry, Back) when the state calls for one. Illustration alone should never be the only signal a user gets about what happened.

## Variant Guide
Illustration has 2 independent dimensions: **Type** (which illustration / meaning) and **Size** (how much space it occupies).

### Dimension 1 — Type (meaning/context)

| Illustration | Category | When to Use |
|---|---|---|
| `error403` | Error | User doesn't have permission to view this page/resource |
| `error404` | Error | The page or resource doesn't exist or has been removed |
| `dataFailed` | Error | A data fetch/load operation failed (network or server error) |
| `noInternet` | Error | Device/app has lost network connectivity |
| `noData` | Empty | A data source/report/page has no determinable data — visually shown as documents with a "?", implying the data is unavailable rather than simply zero-count |
| `noItem` | Empty | A collection/list/container has nothing inside it — visually an empty open box, for a straightforward "zero items" case (e.g. empty cart, empty folder) |
| `emptyWidget` | Empty | A dashboard widget/card specifically has no data — visually depicts a widget/window shape itself with a "?", making it self-referential to widget context (distinct from a full-page `noData`) |
| `noNotif` | Empty | The notification list/panel is empty |
| `noChat` | Empty | A chat/conversation list or thread has no messages yet |
| `searchNotFound` | Empty | A search query returned zero results — distinct from `noData` because it implies "try different keywords" |
| `upload` | Empty | A file upload area with nothing uploaded yet — prompts the user to drag-and-drop or select a file |
| `dataSuccess` | Success | Confirms a significant operation completed successfully (beyond a routine save) |
| `emailSuccess` | Success | Confirms an email-related action succeeded (e.g. verification email sent, reset link sent) |
| `consultation` | Contextual/Flow | *(TBD — general-purpose illustration, exact scenario not yet defined; confirm intended use the first time a feature calls for it, rather than assuming a fit here)* |

### Dimension 2 — Size

| Value | When to Use |
|---|---|
| `large` | Full-page states, where nothing else on screen competes for attention |
| `medium` | Section/card-level states, where the illustration shares space with page chrome, nav, or other sections |
| `small` | Compact spaces — modal, drawer, inline widget — where a full illustration would overwhelm the container |

## ✅ Do
- Choose the illustration based on the **actual cause** of the state, not on which one looks nicer — e.g. never use `dataFailed` for a list that's simply, intentionally empty.
- Always pair the illustration with a short supporting text explaining the specific reason — the illustration signals the category (error/empty/success), the text explains the specifics.
- Match size to the surrounding space — a `large` illustration in a modal or drawer will look cramped or overwhelming; drop to `small` or `medium`.
- Use `searchNotFound` only when the empty result is caused by a user-entered search/filter query, not for a list that's empty by default.
- Distinguish `noItem` (a straightforward empty container — list, cart, folder) from `noData` (data is unavailable/undeterminable, broader than a single list) and from `emptyWidget` (specifically a dashboard widget/card with no data) — pick based on which one the scenario actually is, since they read differently to the user despite all being "empty."
- Use `upload` specifically for an empty file-upload area (before any file is added), not for a generic empty state.
- Keep usage of `noNotif` and `noChat` consistent with their specific scenario so users learn to recognize what each one means at a glance, rather than treating them as interchangeable "generic empty" assets.
- Reserve `dataSuccess`/`emailSuccess` for meaningful milestones (e.g. end of a multi-step flow, account verification) — not for routine saves, which belong to Toast instead.

## ❌ Don't
- Don't use an error illustration (`error403`, `error404`, `dataFailed`, `noInternet`) for an empty state, or vice versa — mixing categories makes it unclear to the user whether something is broken or simply has no content.
- Don't use `large` size inside a small container (modal, drawer, inline widget) — it will visually dominate and push out surrounding content.
- Don't use `dataSuccess`/`emailSuccess` as a substitute for Toast on routine confirmations (e.g. "field saved") — full illustration success states are for significant, page-level moments, not minor actions.
- Don't display an illustration without any accompanying text — even for a self-explanatory case, always include at least a short message.
- Don't assign `consultation` to a scenario preemptively — since it's general-purpose, confirm the actual use case (e.g. by asking during that feature's work) rather than guessing when a prototype seems to fit.

## Additional Context
- **`noData` vs `noItem` vs `emptyWidget`** — confirmed via visual reference: `noItem` uses an empty open box (a plain "container has nothing" metaphor), `noData` uses documents with a "?" (data is unavailable/undeterminable, not just zero), and `emptyWidget` depicts a widget/window shape itself with a "?" (scoped specifically to dashboard widgets). Use the one that matches the actual cause, not just "this list is empty."
- **`upload`** — confirmed as an Empty-category illustration (cloud + upload arrow), used for a file-upload area before any file has been added.
- **`consultation`** — **(TBD)** general-purpose, no fixed scenario defined yet. Rather than pre-assigning it here, resolve its use case the first time a feature genuinely needs it — e.g. by asking during that feature's PRD/prototype work — and update this table once a real usage establishes the pattern.
- Illustration should always be evaluated together with `_error-state.md` and any future `_empty-state.md` / success pattern doc — this file defines *which illustration and size to use*, while those pattern docs define *what other components (Alert, Toast, buttons) accompany it* for a full scenario.