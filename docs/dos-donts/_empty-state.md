# Empty State Pattern

## Function & When to Use
This document defines the **standard combination and sequencing of components** for common empty-content scenarios — situations where there's nothing to show, but nothing is actually broken. This is distinct from `_error-state.md`: empty means "there's genuinely nothing here yet," while error means "something failed." Illustration choice (see `illustration.md`) is the main signal that tells them apart, so getting the right illustration for the right cause matters more here than in most patterns.

Use this as the reference whenever a feature involves:
- A list, table, or collection with zero items
- A dashboard widget with no data to display
- A notification panel or chat/conversation list with nothing yet
- A search or filter query that returns zero results
- A file-upload area before anything has been added

---

## Scenario 1 — Empty List / Collection (never had content)

**Trigger:** A list, table, or collection genuinely has nothing in it yet — not because of a filter or search, but because nothing has been created (e.g. a new patient's visit history, a freshly created module).

**Component sequence:**
1. Illustration (`noItem` for a straightforward empty container, or `noData` if the absence is more about "no determinable data" than a simple empty list — see `illustration.md` for the distinction), size `medium` if within a page section, `large` if it's the entire page's content
2. Short message stating what's missing in plain terms (e.g. "No visits recorded yet")
3. Primary action button, if the user can do something about it right now (e.g. "Add Visit") — omit the button if creation happens elsewhere or requires a different flow

**✅ Do**
- Use `noItem` for the common case (a list that's just empty) and reserve `noData` for cases where the underlying data itself is unclear/unavailable rather than simply zero-count
- Word the message around the specific entity (e.g. "No lab results yet" rather than a generic "No data")

**❌ Don't**
- Don't use `dataFailed` here — that's for a failed fetch, not a successful fetch that legitimately returned nothing (see `_error-state.md` Scenario 2 for the failure case)
- Don't add a Retry button — there's nothing to retry when the fetch succeeded and simply found nothing

---

## Scenario 2 — Empty Dashboard Widget

**Trigger:** A specific widget/card on a dashboard has no data, while the rest of the page has content.

**Component sequence:**
1. Illustration (`emptyWidget`), size `small` or `medium` depending on the widget's footprint — never `large`, since a widget never occupies the full page
2. Short message scoped to that widget specifically (e.g. "No appointments today"), not a page-level message
3. Action button only if directly relevant to that widget's content and space allows — otherwise omit to avoid crowding a small card

**✅ Do**
- Keep the empty widget visually contained within its own card/section — it shouldn't imply the whole page is empty

**❌ Don't**
- Don't use `noData` or `noItem` for a widget-scoped empty state — `emptyWidget` exists specifically so widgets are visually distinguishable from page or section-level empty states

---

## Scenario 3 — Empty Notifications / Chat

**Trigger:** A notification panel or a chat/conversation list has no items yet.

**Component sequence:**
1. Illustration (`noNotif` for notifications, `noChat` for chat/conversation lists), size `small` or `medium` depending on whether it's a full panel/page or a compact dropdown
2. Short, friendly message (e.g. "You're all caught up", "No messages yet") — these are low-stakes, everyday empty states, so tone can be lighter than a clinical data empty state
3. No action button needed in most cases — these are typically passive states the user simply waits out

**✅ Do**
- Use `small` size when the notification/chat list appears in a dropdown or narrow panel rather than a full page

**❌ Don't**
- Don't reuse `noData`/`noItem` here — `noNotif`/`noChat` are semantically specific and should stay recognizable as their own scenario

---

## Scenario 4 — Search / Filter Returns No Results

**Trigger:** The user actively searched or applied a filter, and it returned zero results.

**Component sequence:**
1. Illustration (`searchNotFound`), size `medium` typically (rarely full-page, since a search bar/filter UI usually remains visible above it)
2. Message that references the search/filter context (e.g. "No results for '{query}'"), not a generic empty message
3. Suggest a recovery action in the message or as a button — e.g. "Try different keywords" or "Clear filters" — since unlike Scenario 1, the user caused this state and can undo it

**✅ Do**
- Always offer a way to clear the search/filter from this state, since the user may not remember which filter caused zero results

**❌ Don't**
- Don't use `noData`/`noItem` for this — the distinguishing detail is that the emptiness is a *result of user input*, which `searchNotFound`'s messaging and recovery action should reflect

---

## Scenario 5 — Empty Upload Area

**Trigger:** A file-upload zone before any file has been added.

**Component sequence:**
1. Illustration (`upload`), size `medium` for a dedicated upload section, `small` if it's a compact upload field within a larger form
2. Message with the accepted format/size guidance if applicable (e.g. "Drag and drop or click to upload — PDF, max 10MB")
3. This illustration typically sits inside an interactive drop-zone itself, rather than replacing a content area the way other empty states do — treat it as part of the upload control's default visual, not a standalone block

**✅ Do**
- Include file format/size constraints in the message when they exist, so the user doesn't fail on the first attempt

**❌ Don't**
- Don't pair `upload` with a Retry button — "retry" implies a prior failed attempt, which belongs to a separate upload-failure state, not this initial empty one

---

## Decision Summary

| Scenario | Illustration | Typical Size | Action Needed? |
|---|---|---|---|
| Empty list/collection (never had content) | `noItem` or `noData` | `medium`/`large` | Yes, if user can create content directly |
| Empty dashboard widget | `emptyWidget` | `small`/`medium` | Rarely |
| Empty notifications | `noNotif` | `small`/`medium` | No |
| Empty chat/conversation list | `noChat` | `small`/`medium` | No |
| Search/filter — zero results | `searchNotFound` | `medium` | Yes — clear search/filter |
| Empty upload area | `upload` | `small`/`medium` | No (not a failure state) |

---

## Open Items
- **(TBD)** Confirm final distinction between `noItem` and `noData` with design once more real usage examples exist — current guidance is based on illustration visuals only (see `illustration.md`)
- **(TBD)** `consultation` illustration is not assigned to any empty-state scenario — resolve its use case if/when a feature calls for it, per `illustration.md`
- This document assumes empty states never need Alert or Toast — if a future scenario seems to need one (e.g. an empty state caused indirectly by a permission restriction), check `_error-state.md` first, since that may actually be an error/access scenario rather than a true empty state