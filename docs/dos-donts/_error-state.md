# Error State Pattern

## Function & When to Use
This document defines the **standard combination and sequencing of components** for common error scenarios. It does not replace `Alert.md`, `Toast.md`, or `Input.md` — those define *when to use a single component*. This pattern defines *which components work together, in what order*, for a given error scenario, so that error handling looks and behaves consistently across the product.

Use this as the reference whenever a feature involves:
- Form submission that can fail
- Data fetching that can fail
- Network/connection loss
- A destructive or important action that can fail (delete, update, approve)

---

## Scenario 1 — Form Validation Error (client-side)

**Trigger:** User submits a form with one or more invalid fields.

**Component sequence:**
1. Set `error={true}` on every invalid form field — confirmed uniform across all form components (`Input`, `PasswordInput`, `NumberInput`, `PhoneInput`, `Select`, `Combobox`, `DatePicker`, `TimePicker`, `TextArea`, `FileUpload`): all use the same `error: boolean` prop for visual styling (border/color change). None of them carry the error message text itself — *(TBD: confirm whether a wrapper component, e.g. `FormField`/`FormGroup`, owns the inline error message, or whether it must be a manually placed text element below each field)*
2. Auto-scroll and auto-focus to the **first** invalid field
3. Alert (`variant="error"`, `tone="soft"` unless the form is short/critical, then `default`) placed **above the form**, only when there are **3 or more** invalid fields — for 1–2 invalid fields, field-level indicators alone are sufficient and an Alert on top is redundant
4. Do **not** use Toast for this scenario — validation errors are not a one-off event, they need to stay visible until corrected

**✅ Do**
- Keep the Alert description generic ("Please check the fields below") — the specific error belongs to the field itself, not the top-level Alert
- Re-validate and clear the field error (`error={false}`) as soon as the user corrects it — don't wait for re-submit
- Apply `error={true}` the same way across every field type in a form — since the prop is uniform, there's no reason for inconsistent handling between, say, a `Select` and an `Input` in the same form

**❌ Don't**
- Don't show a Toast *and* an Alert for the same validation error — pick one (Alert)
- Don't show the top Alert when there's only 1 invalid field — it adds noise without new information
- Don't rely on `error={true}` alone to communicate *why* the field is invalid — since none of these components have a built-in message prop, forgetting the separate text element leaves the user with a red border and no explanation

---

## Scenario 2 — Data Fetch Failure (page/section load)

**Trigger:** A page or section fails to load data (e.g. patient list fails to fetch).

**Component sequence:**
1. Replace the expected content area with an **error state block**: Illustration (`dataFailed`) + short message + a **Retry** button
2. Illustration size: `medium` for a section within a page, `large` for a full-page failure — *(TBD: confirm against Illustration dos-donts once written)*
3. Use Alert (`variant="error"`, `default` tone) only if the failure affects the **entire page** (e.g. critical data the rest of the page depends on) rather than one section among several
4. Do **not** use Toast — this is a persistent state, not a momentary event

**✅ Do**
- Always pair a fetch-failure state with a Retry action — never leave the user with no way to recover without a page refresh
- Scope the failure to the smallest affected area (a section failing shouldn't block sections that loaded fine)

**❌ Don't**
- Don't silently show an empty state when the cause is actually an error — empty state and error state must look visually distinct
- Don't rely on Toast alone for a failed fetch, since the user may not be looking at the screen when it appears, and the broken state has no other explanation left on screen

---

## Scenario 3 — Network / Connection Loss

**Trigger:** The app detects the user has lost connectivity (not a specific request failing, but connectivity itself).

**Component sequence:**
1. Alert (`variant="warning"`, `default` tone, `titleShow` enabled) — persistent, typically pinned near the top of the layout, since this affects the whole session, not one action
2. If the connection loss blocks an entire page/screen (not just a background action), replace the content area with Illustration (`noInternet`, size `large`) + short message + Retry, following the same block pattern as Scenario 2
3. Once connection is restored, dismiss the Alert automatically (don't require manual dismissal for a condition that resolved itself)
4. Toast (`variant="success"`) may optionally confirm "Connection restored" — brief, not required to persist

**✅ Do**
- Use `warning`, not `error`, for connection loss itself — the loss of connection is a caution, the *failed actions that result from it* are what warrant `error`

**❌ Don't**
- Don't stack a new Alert every time connectivity flickers — debounce/throttle so the user isn't seeing the Alert appear and disappear repeatedly

---

## Scenario 4 — Action Failure (submit / delete / update)

**Trigger:** A user-initiated action completes but fails server-side (distinct from Scenario 1, which is client-side validation before the request is even sent).

**Component sequence:**
1. Toast (`variant="error"`) confirming the specific action failed (e.g. "Failed to update patient record")
2. The page/form state must **not** change as if the action succeeded — the data that failed to save must remain visibly unsaved (per `Toast.md`: don't let critical information exist only in the Toast)
3. Use `showButton` on the Toast only if there's an immediate, relevant recovery action (e.g. "Retry") — don't add a button for the sake of it

**✅ Do**
- Keep the form/inputs exactly as the user left them on failure, so they don't lose their input and can retry without re-typing

**❌ Don't**
- Don't use Alert for this scenario — it's a one-off action result, not a persistent condition (per `Alert.md` vs `Toast.md` distinction)
- Don't show a generic "Something went wrong" Toast when a more specific reason is available — specificity helps the user decide what to do next

---

## Scenario 5 — Access Denied / Not Found (page-level)

**Trigger:** User navigates to a page they don't have permission for (403), or a resource that doesn't exist (404) — e.g. a direct link to a deleted patient record.

**Component sequence:**
1. Full-page replacement: Illustration (`error403` or `error404`, size `large`) + short message explaining the reason (avoid exposing technical detail like raw status codes to end users) + a single clear action (e.g. "Back to Dashboard")
2. No Alert or Toast needed — this is not a transient failure, it's the entire page's state
3. Do not show a Retry button here — retrying won't change a permission or existence problem, unlike Scenario 2's fetch failure

**✅ Do**
- Keep the message role-appropriate — a nurse and an admin may need different next-step guidance for a 403

**❌ Don't**
- Don't reuse `dataFailed` for this — 403/404 are distinct causes from a network/fetch failure and should look visually distinct so users (and support staff reading screenshots) can tell them apart

---

## Illustration Reference (Error Scenarios Only)

| Scenario | Illustration | Typical Size |
|---|---|---|
| Data fetch failure (section) | `dataFailed` | `medium` |
| Data fetch failure (full page) | `dataFailed` | `large` |
| Network/connection loss (blocking) | `noInternet` | `large` |
| Access denied | `error403` | `large` |
| Resource not found | `error404` | `large` |

**Note:** The following illustrations from your set are **not** error-state assets and are out of scope for this document — flagging them here so they aren't accidentally misapplied to an error scenario:
- `noData`, `noItem`, `emptyWidget`, `noNotif`, `noChat`, `searchNotFound` → belong in a future `_empty-state.md` (zero-content states, not failures)
- `dataSuccess`, `emailSuccess` → belong in a success/confirmation pattern doc
- `upload`, `consultation` → appear to be contextual/flow illustrations rather than state illustrations; **(TBD)** confirm their actual use case before categorizing

**(TBD) Illustration size guidance (draft, unconfirmed):**
- `large` — full-page states (nothing else on screen competes for attention)
- `medium` — section/card-level states (illustration shares space with page chrome, nav, other sections)
- `small` — compact spaces (modal, drawer, inline widget) where a full illustration would overwhelm the container
This sizing logic is not yet backed by an Illustration dos-donts document — recommend writing one, since this file currently borrows illustration usage rules from inference rather than a source of truth.

---

## Decision Summary

| Scenario | Primary Component | Illustration | Persistent? | Retry/Recovery Action |
|---|---|---|---|---|
| Form validation (client-side) | Field-level + Alert (if 3+ fields) | None | Yes, until corrected | Implicit — fix the field |
| Data fetch failure | In-place error block (+ Alert if page-wide) | `dataFailed` | Yes, until retried | Explicit Retry button |
| Network/connection loss | Alert (`warning`) (+ full block if blocking) | `noInternet` (if blocking) | Yes, until reconnected | Automatic (dismisses on reconnect) |
| Action failure (submit/delete/update) | Toast (`error`) | None | No — but form state must reflect the failure | Optional, only if relevant |
| Access denied / not found | Full-page illustration block | `error403` / `error404` | Yes, until user navigates away | None (retry doesn't apply) |

---

## Open Items
- **(TBD)** Whether an inline error-message text is rendered by a wrapper component (e.g. `FormField`/`FormGroup`) or must be placed manually alongside each field — confirmed that `error: boolean` is uniform across all form components for styling only, with no message prop anywhere in that set
- **(TBD)** `consultation` illustration still has no assigned scenario — resolve if/when a feature calls for it, per `illustration.md`