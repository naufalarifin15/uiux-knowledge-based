# Popover

## Purpose & When to Use
Popover displays floating content near a trigger element, visually similar to Tooltip (bubble shape + position relative to the trigger), but with **free-form content** — it can hold more than just a text label (e.g. a list of options, a small form, action buttons, or a combination of elements).

**Difference from Tooltip:** Tooltip only accepts short text via the `label` prop and automatically shows/hides on hover/focus (see `tooltip.md`). Popover accepts free-form content via a slot and is triggered by a click, with dismissal requiring an explicit user action (clicking outside the popover area, or a close button inside its content) — since its content is interactive, it shouldn't disappear automatically just because the mouse moved.

## Props Structure

| Prop | Type | Default | Description |
|---|---|---|---|
| `position` | `'Bottom'` \| `'Top'` \| `'Left'` \| `'Right'` | `'Bottom'` | Popover position relative to the trigger |

**Slots**
| Slot | Description |
|---|---|
| `default` | The trigger element that opens the popover when clicked |
| `content` | Free-form content shown inside the popover — can contain any element, not limited to text |

## ✅ Do
- Use Popover for content that needs **interaction** (clicking a button, selecting an option, filling a small form) — for short, passive explanatory text, use Tooltip instead.
- Provide an explicit way to close the popover (click outside the popover area, or a close button inside the `content` slot) — don't rely on hover-out like Tooltip.
- Choose a `position` that won't cause the popover content to get cut off at the viewport edge — avoid `position="Top"` for triggers at the very top of the page, or `position="Right"` for triggers near the right edge of the screen.
- Keep the content inside the `content` slot concise — Popover is not a replacement for Modal when it comes to long/complex content.
- Make sure the element in the `default` slot (trigger) can receive focus, so the Popover can also be opened via keyboard navigation.

## ❌ Don't
- Don't use Popover for a short, single-line label — that's Tooltip's use case, not Popover's.
- Don't put overly complex/long content in the `content` slot (e.g. a long multi-field form) — use Modal for that instead.
- Don't leave a Popover open without a clear way to close it — users can get stuck with a popover covering other content on the page.
- Don't use the same `position` for every trigger regardless of its location in the layout — adjust it per case so the popover doesn't get cut off or hidden behind other elements.

## Additional Context
- Since Popover is triggered by a click (not hover), make sure its trigger doesn't overlap with other elements that also respond to clicks in the same area — this can cause interaction conflicts.