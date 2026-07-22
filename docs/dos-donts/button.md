# Button

## Function & When to Use
Button triggers an action when clicked (`click` event) — form submit, navigation, triggering a modal, etc. Since it has many variants with different meanings, choosing the right variant matters so users understand the importance/consequence of each action just from its appearance.

## Variant Guide

**Dimension 1 — Variant (function/meaning of the action)**
| Value | Function | When to Use |
|---|---|---|
| `primary` | Main action | The action most expected to be clicked within a section/form. Ideally only 1 per section. |
| `secondary` | Secondary action | A companion action that isn't as critical as primary, e.g. "Cancel" next to "Save" |
| `danger` | Destructive action | Delete, permanently remove, actions that can't be/are hard to undo |
| `safe` | Positive/safe confirmation action | Confirmations that are safe/positive in nature, e.g. "Agree", "Done" |
| `outline` | Action with low visual emphasis | An available action that doesn't need to stand out, often used alongside `primary` |
| `ghost` | Action with the lowest visual emphasis | Minor actions, e.g. inside a toolbar or an area dense with elements |
| `caution` | Action requiring caution | Risky actions but not as destructive as `danger`, e.g. "Reset to default" |
| `disabled` | Inactive action | Disables the button due to a certain condition (e.g. the form isn't valid yet) |

**Dimension 2 — Size**
| Value | When to Use |
|---|---|
| `lg` | Default — main CTAs, forms with enough space |
| `md` | General contexts, toolbars, dialogs |
| `sm` | Dense contexts, e.g. inside a table row or a small card |

**Dimension 3 — Composition (additional elements)**
| Element | Prop | When to Enable |
|---|---|---|
| Left icon | `iconLShow` + `iconL` | To give quick visual context before the label (e.g. a "+" icon for "Add") |
| Right icon | `iconRShow` + `iconR` | To indicate direction/further action (e.g. an arrow icon for "Next," a chevron for a dropdown) |
| Badge | `badgeShow` + `badgeContent` | To display a small counter on top of the button (e.g. notification count), default content `'9+'` |

## ✅ Do
- Limit to only **1 `primary` button per section/form** — if there are multiple actions, use `secondary`/`outline`/`ghost` for the rest based on their level of importance.
- Use `danger` specifically for actions that are genuinely destructive/hard to undo — not just for actions that "feel important."
- Use the `disabled` variant (or a disabled state) to prevent double submission/invalid actions, rather than hiding the button entirely — users still need to know the action exists but isn't usable yet.
- Pair icons (`iconL`/`iconR`) only when they genuinely add clarity, not purely for decoration.
- Use `badgeShow` for brief additional information (a counter), not for long text.

## ❌ Don't
- Don't use more than 1 `primary` button within a single section — it will confuse users about which action is most expected.
- Don't use `danger` for actions that aren't actually destructive just because you want the button to look more prominent.
- Don't enable `iconLShow`/`iconRShow` without filling in `iconL`/`iconR` — these are interdependent pairs; enabling the show flag without an icon component will leave an empty slot.
- Don't enable `badgeShow` without relevant `badgeContent` — an empty/default badge (`'9+'`) that doesn't match the actual condition will mislead users.

## Additional Context
- `disabled` here is listed as one of the values of `variant`, not a separate boolean prop — make sure it's applied consistently (don't mix in an assumption that there's a separate boolean `disabled` prop if this state is actually purely controlled via `variant="disabled"`).
- The `click` event is the only event exposed — make sure action logic (loading state, disabling on submit, etc.) is controlled externally through changes to `variant`/props, rather than expecting other events like `mousedown`/`mouseup`.