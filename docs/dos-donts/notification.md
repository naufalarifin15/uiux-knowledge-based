# Notification

## Function & When to Use
Notification is a panel/dropdown containing a list of notifications with an "Unread" filter toggle, per-item options, and a footer button to load older notifications. Used as a dropdown from the notification icon in Header (see `header.md` — the `notificationClick` event in Header typically triggers showing/hiding this panel).

## Props Structure

| Prop | Type | Default | Description |
|---|---|---|---|
| `showFooter` | `boolean` | `true` | Shows the "Show Previous Notifications" footer button |
| `footerText` | `string` | `'Show Previous Notifications'` | Custom footer button label |
| `showUnreadOnly` | `boolean` | `false` | Filters to show only unread notifications |

> The API documented here only covers the footer control and "Unread" filter — **there's no prop for supplying the list of notification items itself** (e.g. an `items`/`notifications` array). This suggests notification content is likely injected via a **slot** (not a prop), following the pattern of several other components in this package (e.g. the `default` slot in Card). Check the package's types/Storybook for the exact slot name before implementing — this documentation doesn't cover that detail.

## Events
| Event | Payload | When It Fires |
|---|---|---|
| `update:showUnreadOnly` | `boolean` | For `v-model:show-unread-only` on the "Unread" toggle |
| `notificationClick` | union (type depends on the clicked item) | When a notification card is clicked |
| `footerClick` | — | The footer button is clicked |
| `optionClick` | union | When an action from the options menu (`...` icon) is selected |

## Built-in Behavior (from design reference)
- **The notification title has a different hover state than the default** — on hover, the title displays with an underline; the default has no underline. This is built-in behavior with no prop to change it.
- **The component's height adjusts to its content** (hugs content) — if a notification description is more than 2 lines, the list height increases automatically, rather than being truncated/a fixed height per item.
- **There's a content height limit (around 600px)**, after which additional notifications are loaded via **lazy load** — not a regular, unbounded infinite scroll.

## ✅ Do
- Use `v-model:show-unread-only` to sync the "Unread" toggle with filter state in the parent, if that filter needs to affect other logic (e.g. re-querying the backend).
- Listen for `notificationClick` to navigate to the notification's related detail (e.g. a related patient page) or to mark it as read.
- Listen for `optionClick` to implement per-item actions (e.g. "Mark as read," "Delete") — the union payload means its type needs to be narrowed/checked before further processing.
- Adjust `footerText` if the usage context isn't literally "old notifications" (e.g. "Load more") to better match the need.
- Take advantage of the built-in lazy load for long notification lists — don't fetch all notification data at once upfront if the component already handles incremental loading.

## ❌ Don't
- Don't expect a prop to change the title's hover state (underline) — this is fixed by design and isn't customizable via props.
- Don't manually set a fixed container height smaller than needed — the component is designed to hug content up to a certain limit, and forcing a different height could improperly cut off content.
- Don't assume all notifications are loaded at once without accounting for lazy load — make sure the data source/API supports pagination/incremental loading matching this built-in behavior.
- Don't ignore the union-typed `optionClick`/`notificationClick` payload — make sure there's type narrowing/validation before branching logic, so you don't make wrong assumptions about the received data structure.

## Additional Context
- Since notification data doesn't come in through a documented prop here, make sure the content supplied (via a slot or other mechanism) stays consistent with the built-in behavior described above (hover underline, hug content, lazy load at ~600px) — don't manually override the notification item's structure/styling to the point of ignoring that built-in behavior.