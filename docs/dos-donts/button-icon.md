# Icon Button

## Function & When to Use
Icon Button is a button variant that **only displays an icon with no text label**, usually shaped as a compact circle/square. Used for actions whose meaning is already clear from the icon alone (e.g. "+" for add, a trash icon for delete), in places with limited space (toolbars, table rows, floating action buttons).

**Difference from a regular Button:** Button displays a `label` (text) with optional left/right icons, while Icon Button is **icon-only, with no text at all** — which is why `ariaLabel` becomes mandatory (see below), unlike Button whose label is already automatically accessible via visible text.

## Variant Guide

**Dimension 1 — Variant (function/meaning of the action)**
Same as a regular Button — see `button.md` for a full explanation of each value (`primary`, `secondary`, `danger`, `safe`, `outline`, `ghost`, `caution`, `disabled`). The selection rules are identical: `primary` for main actions, `danger` for destructive actions, etc.

**Dimension 2 — Size**
| Value | When to Use |
|---|---|
| `lg` | Default — actions that are meant to stand out, e.g. a floating action button |
| `md` | General contexts, toolbars |
| `sm` | Dense contexts, e.g. inside a table row |

## ✅ Do
- **Always fill in `ariaLabel`** with a clear description of the button's function (e.g. `"Delete item"`, not `"Button"` or empty) — since there's no visible text, screen readers rely solely on this prop to explain the button's function to visually impaired users.
- Use icons that are already familiar/conventional for their function (e.g. trash for delete, pencil for edit) — avoid ambiguous icons that need a label to be understood.
- Choose the variant using the same rules as a regular Button (see `button.md`) — color meaning consistency must still be maintained even though the shape is different.
- Consider adding a tooltip with the same text as `ariaLabel` for sighted users (not just screen readers), so the button's function stays visually clear.

## ❌ Don't
- Don't leave `ariaLabel` empty — this isn't optional in practice, even if it's not technically required in the types. An Icon Button without `ariaLabel` isn't accessible at all.
- Don't use Icon Button for actions whose meaning isn't clear from the icon alone — if the user has to think "what is this button for," use a regular Button with a label, or add a tooltip.
- Don't use the same icon for different functions on the same page (e.g. a pencil icon used for "edit" in one place and "view detail" in another) — this will confuse users.

## Additional Context
- Icon Button's variant list and sizes are identical to the regular Button, so if there's a change to variant rules in `button.md`, also check its relevance for this file.