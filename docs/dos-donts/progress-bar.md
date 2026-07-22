# Progress Bar

## Function & When to Use
Progress Bar displays a process with a **definite, measurable value** (0-100%), unlike Spinner, which is for indeterminate processes. Used when the progress can actually be calculated — e.g. a file upload with a percentage, a multi-step form completion progress, or a process whose backend reports a real percentage.

**Difference from Spinner:** Spinner is for processes of unknown duration (indeterminate), while Progress Bar is for processes whose percentage can genuinely be calculated (determinate). Don't use Progress Bar with a faked/estimated value if there's actually no real progress data — that situation is better suited to Spinner.

## Props Structure

| Prop | Type | Default | Description |
|---|---|---|---|
| `value` | `number` | `0` | Progress percentage, from `0` to `100` |

## ✅ Do
- Use Progress Bar only when there's a **real** progress value that can be calculated (e.g. `bytesUploaded / totalBytes * 100`), not an estimated/fake number just to give the impression of "in progress."
- Update `value` reactively to follow the actual progress (e.g. from an XHR/fetch progress event), not a static animation that doesn't reflect the real condition.
- Make sure `value` always stays within the 0-100 range — clamp the value at the application level if the data source could potentially return a value outside that range (e.g. rounding that produces 100.5).

## ❌ Don't
- Don't use Progress Bar for a process of unknown duration — use Spinner for that case instead of forcing Progress Bar with a value that's periodically fake-incremented.
- Don't let `value` sit at the same number for too long with no other indication that the process is actually still running (e.g. stuck at 99% because the last step is genuinely slow) — consider adding an extra status message outside this component.
- Don't forget to reset `value` to `0` when starting a new process, so it doesn't show leftover progress from a previous process.

## Additional Context
- Progress Bar doesn't have a prop to display a label/percentage text inside the component itself — if you need to display a percentage number (e.g. "45%"), it needs to be added as a separate text element outside/alongside this component.