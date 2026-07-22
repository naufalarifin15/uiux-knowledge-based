# Toast

## Function & When to Use
Toast displays a **temporary** notification that appears then disappears automatically, usually floating in a corner of the screen — used for brief feedback about an action (e.g. "Successfully saved," "Failed to send data").

**Difference from Alert:** Alert is persistent/attached to the layout (see `alert.md`), while Toast is temporary and not attached to the page's content flow. If a message needs to stay visible until the user consciously dismisses it or the condition changes, use Alert, not Toast.

## Props Structure

| Prop | Type | Default | Description |
|---|---|---|---|
| `variant` | `'primary'` \| `'info'` \| `'success'` \| `'warning'` \| `'error'` | `'success'` | Visual style and icon |
| `title` | `string` | `'Title'` | Notification title (bold) |
| `description` | `string` | — | Supporting text |
| `showButton` | `boolean` | `false` | Shows an additional action button |
| `buttonText` | `string` | `'Accept'` | Action button label |

> Toast also has a close (×) button that's **always visible** regardless of `showButton` — `showButton` controls the **additional** action button (e.g. "Undo," "View"), not the close button.

## Events
| Event | Payload | When It Fires |
|---|---|---|
| `buttonClick` | — | When the action button (`buttonText`) is clicked |

## ✅ Do
- Choose `variant` based on the meaning of the action's result — `success` for a successful action, `error` for a failed action, `warning` for a result with a caveat, `info` for a neutral notification.
- Keep `title` and `description` **brief** — Toast has a limited display duration, and a long message risks not being fully read before the toast disappears.
- Use `showButton` only for actions that are genuinely actionable and relevant right at that moment (e.g. "Undo" after deleting data, "View" to jump directly to a related page) — don't use it for purely informational notifications.
- Use Toast for feedback on the result of a user action (submit, delete, update), not for information that needs to stay visible for a long time.

## ❌ Don't
- Don't use Toast for a message that needs to stay visible until the user consciously closes it (e.g. an important warning that must be read) — use Alert for that instead.
- Don't stack many Toasts at once for actions that happen in quick succession — consider combining messages or throttling how often toasts appear.
- Don't put crucial information that **only** exists in the Toast with no other way to access it again — since it's temporary and can be missed, especially for important results that ideally should also be reflected in the page's state (e.g. successfully saved data should still show as updated on the page, not just briefly mentioned in a toast).
- Don't use `showButton` for actions unrelated to the context of that notification.

## Additional Context
- No prop for auto-dismiss duration (e.g. `duration`/`autoCloseDelay`) is visible in this table — the duration is likely already fixed by default in the component's implementation, or controlled by a higher-level toast/notification manager system (rather than per-instance on this Toast).