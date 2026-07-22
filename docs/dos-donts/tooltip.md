# Tooltip

## Function & When to Use
Tooltip shows a short explanatory text when the trigger element is hovered/focused. Used to give extra context for an element whose meaning isn't fully clear from its appearance alone (e.g. an Icon Button with no label, an abbreviation, a status icon).

## Props Structure

| Prop | Type | Default | Description |
|---|---|---|---|
| `label` | `string` | `'This is tooltip'` | Tooltip text |
| `position` | `'Bottom'` \| `'Top'` \| `'Left'` \| `'Right'` | `'Bottom'` | Tooltip position relative to the trigger |

**Slot**
| Slot | Description |
|---|---|
| `default` | The trigger element that activates the tooltip on hover/focus |

## ✅ Do
- Use Tooltip to complement **Icon Button** (see `button-icon.md`) — since Icon Button has no visible text, Tooltip helps sighted users (not just screen reader users via `ariaLabel`) understand its function.
- Choose a `position` that isn't obstructed by other surrounding elements (e.g. avoid `position="Top"` for a trigger at the very top of the viewport, since the tooltip could get cut off).
- Keep `label` **brief** (1 short line) — Tooltip isn't the place for a long explanation; if more detail is needed, consider a Popover or separate documentation instead.
- Since Tooltip relies on the `default` slot as its trigger, make sure the element inside the slot can receive focus (e.g. a button, a link) so the tooltip also appears during keyboard navigation, not just on mouse hover.

## ❌ Don't
- Don't use Tooltip as the only way to convey important/must-read information — since it only appears on hover/focus, a tooltip is easy to miss (especially on touch devices with no hover concept).
- Don't put long text in `label` — an overly long tooltip becomes hard to read and could get cut off on narrow screens.
- Don't use Tooltip for elements whose meaning is already clear enough without extra explanation — overusing tooltips makes the interface feel noisy/excessive.
- Don't put a non-focusable element (e.g. a plain `<div>` with no `tabindex`) as the trigger in the `default` slot if the tooltip also needs to appear via keyboard navigation — make sure the trigger element is accessible.

## Additional Context
- Since this is purely hover/focus-triggered with no explicit touch-device support in the props table, consider that Tooltip might **not appear on mobile/tablet devices** (no hover concept) — for information that must be conveyed on all devices, don't rely on Tooltip alone.