# Loading State Pattern

## Function & When to Use
This document defines the **standard approach for indicating that content or an action is in progress**, before a result (success, error, or empty) is known. Loading state is always temporary and resolves into one of the other three patterns — `_error-state.md`, `_empty-state.md`, or a successful render of real content — so it should never look like a dead end on its own.

## Component Guide
Two loading components are available: **Spinner** (indeterminate, sizes `16`/`20`/`24`/`32`/`40`) and **Progress Bar** (determinate, driven by a `value` 0–100 prop). Full component-level rules live in `Spinner.md` and `Progress Bar.md` — this document only covers *which one, at what size, in which scenario*.

| Component | When to Use |
|---|---|
| `Spinner` | Loading with **no measurable progress** — duration unknown (most data fetches, most actions) |
| `Progress Bar` | Loading with **measurable progress** — a real, calculable percentage exists (e.g. file upload bytes, not a faked estimate) |

No Skeleton component exists in this library — do not reference skeleton loaders in prototypes or specs; use `Spinner` for cases that might otherwise call for a skeleton.

Two rules from the component docs carry directly into every scenario below:
- Per `Spinner.md`: never let a Spinner spin indefinitely with no fallback — if a process times out or fails, it must resolve into `_error-state.md`, not spin forever.
- Per `Progress Bar.md`: the `value` prop has no built-in label — any percentage or filename text shown alongside it (e.g. "45%", "report.pdf") must be added as a separate text element.

Use this as the reference whenever a feature involves:
- Initial page load
- A section/widget loading independently of the rest of the page
- An action in progress (submit, delete, save)
- Loading more items (pagination / infinite scroll)
- A search-in-progress state

---

## Scenario 1 — Initial Page Load

**Trigger:** The page is fetching the data it needs before it can render anything meaningful.

**Component sequence:**
1. Centered `Spinner`, size `40` (full-page/large focal area, per `Spinner.md`), with `ariaLabel` describing what's loading (e.g. `"Loading patient data"`) rather than the generic default
2. Once data resolves: replace with real content, or transition to `_empty-state.md` / `_error-state.md` as appropriate — per `Spinner.md`, never leave it spinning indefinitely with no fallback if the load times out or fails

**✅ Do**
- Always show the Spinner immediately on navigation — never a blank white page, even briefly, since the EMR context includes users on older/slower hospital hardware where load time can be noticeable

**❌ Don't**
- Don't use `Progress Bar` here unless the page load genuinely has a measurable percentage (e.g. a multi-step data sync) — most page loads are indeterminate and should use `Spinner`

---

## Scenario 2 — Section / Widget Load (independent of page)

**Trigger:** One section or dashboard widget is still loading while the rest of the page has already rendered.

**Component sequence:**
1. `Spinner`, size `24` (default) for a typical card/section, or `32` if the widget occupies a notably larger area — scoped to that section/widget only, not the whole page
2. The rest of the already-loaded page must remain interactive — a loading section should never block interaction elsewhere

**✅ Do**
- Let each widget resolve independently — a slow widget shouldn't hold up ones that already loaded (this pairs with `_empty-state.md` Scenario 2 and `_error-state.md` Scenario 2, which are the two possible outcomes once loading finishes)

**❌ Don't**
- Don't use a page-level Spinner (`40`) or overlay for a single section's load — that incorrectly signals the whole page is blocked

---

## Scenario 3 — Action in Progress (submit / save / delete)

**Trigger:** The user triggered an action and is waiting for the result.

**Component sequence:**
1. `Spinner`, size `16` (small inline, per `Spinner.md`), replacing the button's label — the button becomes disabled during this state
2. Disable the rest of the form/related controls during the action to prevent duplicate submissions, especially relevant for actions that shouldn't be triggered twice (e.g. submitting a clinical note)
3. On resolution: Toast confirms success/failure per `_error-state.md` Scenario 4 and `Toast.md` — the button returns to its normal state either way

**✅ Do**
- Keep the button's width stable when it switches to its loading state (spinner replacing text) so the layout doesn't shift

**❌ Don't**
- Don't use a full-page loading overlay for a single button's action unless the action is genuinely page-blocking (e.g. a navigation-triggering save) — most actions should feel local to where the user clicked
- Don't use a Spinner size larger than `16`/`20` inside a button — per `Spinner.md`, an oversized Spinner in a small element looks disproportionate

---

## Scenario 4 — Loading More Items (pagination / infinite scroll)

**Trigger:** The user is loading additional items into a list that already has content.

**Component sequence:**
1. `Spinner`, size `20` or `16`, at the bottom of the existing list — the user already sees real content and only needs a cue that more is coming
2. Existing items remain untouched and interactive while more load

**✅ Do**
- Keep this indicator small and inline — it should read as "more is loading," not compete with the content already on screen

**❌ Don't**
- Don't use a larger Spinner size (`24`+) here — per `Spinner.md`, an oversized indicator for a small loading cue breaks the layout

---

## Scenario 5 — Search-in-Progress

**Trigger:** The user typed a search query and results are being fetched (distinct from `_empty-state.md` Scenario 4, which is the *result* of a completed search).

**Component sequence:**
1. `Spinner`, size `20` (dense context, per `Spinner.md`), near the search input (e.g. trailing icon position) rather than replacing the results area immediately
2. Debounce the search trigger so a loading state doesn't flicker on every keystroke — only show it once a search is actually in flight

**✅ Do**
- Keep prior results visible (perhaps dimmed) while a new search is in flight, rather than clearing them immediately — reduces jarring empty flashes between queries

**❌ Don't**
- Don't show `searchNotFound` (from `illustration.md`) while the search is still in progress — that's a premature/incorrect signal until the request actually resolves with zero results

---

## Scenario 6 — File Upload in Progress

**Trigger:** A file is actively being uploaded, following the empty upload state described in `_empty-state.md` Scenario 5.

**Component sequence:**
1. `Progress Bar` replacing the `upload` illustration once a file is selected/dropped, with `value` bound to a real, calculated percentage (e.g. `bytesUploaded / totalBytes * 100`) — per `Progress Bar.md`, never fake or estimate this value
2. Since `Progress Bar` has no built-in label prop, add the filename and percentage as **separate text elements** alongside the bar (e.g. "report.pdf — 45%")
3. On completion: transition to a success indicator (e.g. checkmark, or `dataSuccess`/`emailSuccess` per `illustration.md` if the upload is a significant milestone) or to an upload-specific error state if it fails
4. Reset `value` to `0` before starting a new upload, per `Progress Bar.md`, so no leftover progress from a previous file is shown

**✅ Do**
- Use `Progress Bar` specifically because upload progress is measurable — this is the clearest case distinguishing it from `Spinner`
- If the upload stalls near 100% for a genuinely slow final step, add a status message outside the component (e.g. "Finalizing...") per `Progress Bar.md`, rather than leaving the bar looking frozen with no explanation

**❌ Don't**
- Don't use `Spinner` for file upload — even though the exact time remaining isn't precisely known, byte progress is measurable and `Progress Bar` conveys real advancement, which matters for larger files (e.g. medical imaging attachments)
- Don't rely on the component to show percentage text itself — it doesn't have that prop; forgetting the separate label leaves the user with a bar and no number

---

## Decision Summary

| Scenario | Indicator | Size | Blocks Interaction? | Resolves To |
|---|---|---|---|---|
| Initial page load | `Spinner` | `40` | Yes, for that page | Real content, `_empty-state.md`, or `_error-state.md` |
| Section/widget load | `Spinner` | `24` (or `32` for larger widgets) | No — rest of page stays interactive | Real content, `_empty-state.md`, or `_error-state.md` |
| Action in progress | `Spinner` (inline, in button) | `16` | Related controls only, not the page | Toast (`_error-state.md` Scenario 4) |
| Loading more items | `Spinner` (list footer) | `16`/`20` | No | Appended content |
| Search-in-progress | `Spinner` (input) | `20` | No | Real results or `_empty-state.md` Scenario 4 |
| File upload in progress | `Progress Bar` + separate label text | — (value-driven) | The upload control only | Success indicator or upload-error state |

---

## Open Items
- **(TBD)** Confirm what the upload-failure state (Scenario 6, if the upload fails mid-progress) should look like — likely belongs in `_error-state.md` as a new scenario once defined
- **(TBD)** Confirm whether Spinner's default `ariaLabel` should be overridden project-wide with a standard set of context-specific labels, or left to be written per-feature