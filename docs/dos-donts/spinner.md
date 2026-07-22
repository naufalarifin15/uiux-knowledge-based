# Spinner

## Function & When to Use
Spinner indicates a loading process in progress with no precisely measurable progress (indeterminate) — e.g. while fetching data, submitting a form, or another async process whose duration isn't known for certain.

## Variant Guide

**Size (diameter in px)**
| Value | When to Use |
|---|---|
| `16` | Small inline, e.g. inside a button during submit ("Saving..." with a small spinner next to the text) |
| `20` | Dense contexts, e.g. inside a small input/field |
| `24` | Default — general contexts, section/card loading |
| `32` | A larger loading area, e.g. in the middle of an empty card |
| `40` | Full-page loading or a large area that's the focal point |

## ✅ Do
- Match `size` to the element that's loading — a spinner inside a button uses a small size (`16`/`20`), full-page loading uses a large size (`32`/`40`).
- Always fill in `ariaLabel` with descriptive text matching the context (e.g. `"Loading patient data"`) instead of leaving the generic default `"Loading"` when the context is specific — helps screen reader users understand what process is running.
- Use Spinner for processes whose **duration can't be predicted** — for processes with measurable progress (e.g. a file upload with a percentage), consider a more informative progress bar/indicator instead of a plain Spinner.

## ❌ Don't
- Don't let Spinner display indefinitely with no fallback — if the process fails/times out, make sure there's an error state/message that replaces the Spinner, don't let it spin forever.
- Don't use a large Spinner (`32`/`40`) for a small loading state (e.g. inside 1 table row) — it will break the layout and look disproportionate.
- Don't show more than 1 Spinner at once for the same process on the same page — it can confuse users about how many processes are actually running.

## Additional Context
- Spinner has no color/theme variant in its props — if you need to adjust the color to match the context (e.g. a Spinner inside an area with a dark background), check whether the color automatically adjusts for contrast or needs a manual override.