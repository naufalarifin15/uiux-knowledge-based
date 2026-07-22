# Sidenav

## Function & When to Use
Sidenav is the application's main left-side navigation, supporting collapse/expand, tiered menus (a parent with a submenu), per-item notification badges, and active-item highlighting. Used once per application as part of the main layout (e.g. `DefaultLayout`), alongside Header.

## Props Structure

| Prop | Type | Default | Description |
|---|---|---|---|
| `defaultExpanded` | `boolean` | `false` | Initial expanded/collapsed state |
| `items` | `SidenavMenuItem[]` | `[]` | Menu list, supports nesting (a parent with a submenu) |
| `activeItemId` | `string` | — | ID of the currently active item (controlled) — **see the special rules below for items with a submenu** |

## Events
| Event | Payload | When It Fires |
|---|---|---|
| `itemClick` | `string` (item id) | A menu item is clicked |
| `expandToggle` | `boolean` | Collapse/expand state changes |

## Special Behavior — Menus with a Submenu
This is the most important rule for this component:

1. **A parent item with a submenu CANNOT have an active status.** The parent only functions as a dropdown toggle (open/close the submenu) — see the "Patient" example in Image 3, which is never highlighted as active even when its submenu (e.g. "New patient") is active.
2. **Only a child/submenu item can be set as active** via `activeItemId` — never set `activeItemId` to the id of a parent that has children, since the parent has no active visual state at all.
3. **When the sidenav is collapsed**, submenus aren't visible (only the top-level icons are shown). In this condition, **the parent's icon automatically gets highlighted as active** if one of its children is active — this is automatic component behavior, not something that needs to be manually configured.

## ✅ Do
- Set `activeItemId` **only to the id of an item with no submenu** (a leaf item) — for items with children, let one of its children be the active one instead.
- Update `activeItemId` dynamically based on the active route (e.g. computed from `route.name`/`route.path`), so the highlight always stays in sync with the currently open page.
- Listen for `itemClick` to perform navigation (e.g. `router.push`) — Sidenav itself likely doesn't perform navigation automatically, it only reports which item was clicked.
- Listen for `expandToggle` if the user's collapse/expand preference needs to be saved (e.g. to localStorage) so the state persists across sessions.
- Trust the parent-highlight-when-collapsed logic to the component — don't try to manually override it by setting `activeItemId` to a parent's id.

## ❌ Don't
- Don't set `activeItemId` to the id of a parent that has a submenu — the parent won't show any active status, and this can confuse developers about why the highlight "isn't appearing."
- Don't assume submenu items stay individually visible when the sidenav is collapsed — in collapsed mode, the active-state granularity "rolls up" to just the parent icon level.
- Don't implement routing navigation inside Sidenav itself — use the `itemClick` event and handle routing at the application level (composable/router).
- Don't mix a count badge (a number, e.g. "9" on "New patient") and a dot badge (a plain dot, e.g. on "Health Tracker") inconsistently for the same meaning — align with the Badge convention (`badge.md`): count for a definite number, dot for merely flagging "there's something new."

## Additional Context
- Since `activeItemId` is a controlled prop with no visible `update:activeItemId` event, determining the active item is most likely entirely the application's responsibility (not managed internally by Sidenav) — make sure there's 1 source of truth (e.g. computed from the current route) consistently used for this prop across the application.