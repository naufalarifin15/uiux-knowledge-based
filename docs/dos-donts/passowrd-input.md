# Password Input

## Function & When to Use
Password Input is a dedicated field for password entry, with a built-in show/hide toggle (eye icon). Used for **all** password fields — don't use a regular `Input` with a manual `type="password"`, since Password Input already provides a visibility toggle that's design-consistent across the whole application.

## Props Structure

| Prop | Type | Default | Description |
|---|---|---|---|
| `modelValue` | `string` | — | Password value, used with `v-model` |
| `placeholder` | `string` | `'Placeholder'` | Placeholder text — **generic default, should always be overridden** |
| `disabled` | `boolean` | `false` | Disables the input |
| `error` | `boolean` | `false` | Shows error styling |
| `showPassword` | `boolean` | — (uncontrolled if not set) | Controlled visibility state — used with `v-model:show-password` when external control is needed |
| `className` | `string` | `''` | Additional CSS class |

## Events
| Event | Payload | When It Fires |
|---|---|---|
| `update:modelValue` | `string` | Every keystroke, used for `v-model` |
| `update:showPassword` | `boolean` | When the visibility toggle is clicked, used for `v-model:show-password` |

## ✅ Do
- **Always override `placeholder`** with clear text matching the context (e.g. `"Enter password"`, `"Confirm password"`) — don't leave the uninformative generic default `'Placeholder'`.
- Leave `showPassword` **uncontrolled** (don't set/bind it) for the general case — the component already handles visibility toggling internally.
- Use `v-model:show-password` only when there's a special requirement needing external visibility syncing (e.g. a single "show all passwords" button that controls several password fields at once in the same form).
- Set `error={true}` together with a separate validation message (e.g. "Password must be at least 8 characters") — the component itself doesn't display error text, only styling.

## ❌ Don't
- Don't use a regular `Input` with a manual `type="password"` — always use this Password Input component so the visibility toggle stays consistent across all forms.
- Don't let the default `placeholder` (`'Placeholder'`) show up in production — this is clearly a temporary placeholder that should always be replaced.
- Don't forcibly control `showPassword` from outside for a case that doesn't actually need external syncing — leave it uncontrolled so the toggle behavior stays simple and matches user expectations (click the eye icon to toggle, nothing more).

## Additional Context
- Since there's no `type` prop, all format validation (e.g. minimum character count, letter-number combination) needs to be handled at the application/form validation level, not by this component.