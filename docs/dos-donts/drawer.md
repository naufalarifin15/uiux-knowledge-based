# Drawer

## Purpose & When to Use
Drawer displays a panel that slides in from one edge of the screen, covering part of the viewport while still leaving the page context visible behind it (partial overlay, unlike Modal which is usually centered and feels more fully "blocking"). Used for supplementary content that's fairly substantial (a form, item detail, filter panel) but doesn't need to fully take the user's focus away from the main page.

**Difference from Modal:** Modal appears centered on screen and feels more "blocking" (suited for critical confirmations); Drawer slides in from an edge and feels lighter/more contextual (suited for detail panels, additional forms, filters). See `modal.md` for further comparison.

**Difference from Popover:** Popover is small and positioned relative to a specific trigger element; Drawer covers a significant portion of the screen and its position is relative to the **viewport** (which edge it slides in from), not relative to a single small trigger element. See `popover.md`.

## Variant Guide

**Position (which edge of the screen the Drawer appears from)**
| Value | When to Use |
|---|---|
| `'Right'` | Default — most common for detail panels/additional forms (follows left-to-right reading flow, the drawer appears from a direction that doesn't disrupt the main reading path) |
| `'Left'` | Alternative for secondary navigation/filters, especially when `'Right'` is already used by another element on the same screen |
| `'Bottom'` | Mobile/responsive context — an action sheet or short form that feels more natural appearing from the bottom on narrow screens |
| `'Top'` | Rarely used — for special cases like a temporary notification/announcement panel |

## Props Structure

| Prop | Type | Default | Description |
|---|---|---|---|
| `open` | `boolean` | `false` | Drawer visibility (controlled), used with `v-model:open` (consistent with the pattern in `modal.md`) |
| `position` | `'Bottom'` \| `'Top'` \| `'Left'` \| `'Right'` | `'Right'` | Which edge of the screen the drawer appears from |
| `showHeader` | `boolean` | `true` | Show/hide the drawer header (title + close button) |

**Slots**
| Slot | Description |
|---|---|
| `default` | Free-form content inside the drawer body — can contain any element (form, list, detail info, etc.) |
| `header` (optional) | Custom header content, used when the default header (title + close) isn't flexible enough for a particular need |

## ✅ Do
- Use `v-model:open` for visibility control, consistent with the Modal pattern.
- Choose `position="Right"`/`"Left"` for panels that logically sit alongside the main content (e.g. an item's detail next to its list); choose `"Bottom"` for mobile contexts or quick actions.
- Set `showHeader={false}` only when the content in the `default` slot already manages its own header/title — for most cases, leave `showHeader={true}` (default) so the user always has a clear way to close the drawer and understands the title context.
- Use Drawer (not Modal) when the user still needs to sense the page context behind it (e.g. glancing at a list while filling out a detail form in the drawer) — if the task needs full, distraction-free focus, consider Modal instead.
- Keep Drawer content from growing too long without clear scroll behavior — make sure the drawer body scrolls properly for content that exceeds the viewport height.

## ❌ Don't
- Don't set `showHeader={false}` without providing another way to close the drawer (e.g. a custom close button inside the `default` slot) — the user must always have a clear way out.
- Don't use `position="Top"` for fairly long content — a drawer from the top is usually less natural for content that needs a lot of scrolling compared to one from the side.
- Don't use Drawer for critical confirmations that truly need to block the user's attention (e.g. confirming a permanent data deletion) — use Modal for that, since its more "blocking" feel is psychologically better suited to important decisions.
- Don't mix different `position` values for drawers with similar functions within the same app (e.g. all "detail panels" should consistently use `'Right'`) — inconsistent positioning makes the experience feel unpredictable.

## Additional Context
- Since Drawer can cover a significant portion of the screen, especially with `position="Bottom"` on mobile, make sure to handle the virtual keyboard properly (e.g. when there's an input inside the drawer) so the drawer doesn't get covered by the keyboard or become inaccessible.