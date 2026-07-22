# Link

## Function & When to Use
Link is for **navigation** — moving to another page/resource (internal or external) via `href`. Used when the main action is "go somewhere," not performing an action on the same page.

**Difference from Button:** Button is for actions (submit, delete, toggle, etc.) with no URL-based navigation; Link always has an `href` as its destination. If the element being built has no destination URL, it should be a Button, not a Link — even though visually the two can be made to look similar (e.g. both as blue-colored text).

## Props Structure

| Prop | Type | Default | Description |
|---|---|---|---|
| `label` | `string` | `'Link Button'` | Link text |
| `href` | `string` | — | Destination URL |
| `target` | `'_blank'` \| `'_self'` \| `'_parent'` \| `'_top'` | `'_self'` | Where the link opens |
| `size` | `'lg'` \| `'md'` \| `'sm'` | `'lg'` | Text size |
| `showIcon` | `boolean` | `true` | Shows an arrow icon next to the label |
| `disabled` | `boolean` | `false` | Disables the link |

## Events
| Event | Payload | When It Fires |
|---|---|---|
| `click` | `MouseEvent` | When the link is clicked |

## ✅ Do
- Use `target="_blank"` only for links that open an **external domain/resource** or a document that needs to keep the origin page open (e.g. a PDF, a link to another site) — so the user doesn't lose context of the current page.
- Use the default `target="_self"` for internal navigation within the same application.
- Leave `showIcon` enabled (default `true`) for links that are clearly navigation/CTAs (e.g. "View all," "Read more") — the arrow icon helps users recognize this as a link, not regular text.
- Disable `showIcon` for inline links within a text paragraph, where the arrow icon would actually disrupt the reading flow.
- Use a `size` consistent with the surrounding text — inline links within body text paragraphs should use a size that matches that text.

## ❌ Don't
- Don't use Link for actions that aren't navigation (e.g. submitting a form, deleting data) — use Button instead, even if you want it to visually resemble a link (there's a Button variant/appearance that can mimic a link's style if needed).
- Don't use `target="_blank"` for internal navigation within the same application — it will open a new tab for no reason and confuse users about the application's state (e.g. a form they're currently filling out).
- Don't leave `href` empty/unfilled — if there's no real destination, this isn't a Link use case.
- Don't rely on the `click` event for custom navigation logic that should already be handled by `href` — use `click` only for additional side effects (e.g. analytics tracking), not as a substitute for the navigation itself.

## Additional Context
- For `target="_blank"`, consider standard security aspects (`rel="noopener noreferrer"`) — check whether the component already handles this internally or if it needs to be added manually at the implementation level.