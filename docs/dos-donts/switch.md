# Switch

## Function & When to Use
Switch is for an on/off toggle whose **effect takes place immediately** when clicked (with no separate submit needed) — unlike Checkbox, which is usually part of a form that's submitted together. Suitable for settings/preferences that change instantly (e.g. enabling notifications, dark mode).

## Props Structure

| Prop | Type | Default | Description |
|---|---|---|---|
| `modelValue` | `boolean` | — | On/off value (controlled), used with `v-model` |
| `defaultChecked` | `boolean` | `false` | Initial value (uncontrolled) |
| `disabled` | `boolean` | `false` | Disables interaction |
| `label` | `string` | — | Text next to the switch |
| `state` | `'Off'` \| `'On'` \| `'Off disabled'` \| `'On disabled'` \| `'Error'` | — | Visual state override, presentational — **see the note below** |

> `state` here combines the checked condition (`On`/`Off`) and the disabled condition (`Off disabled`/`On disabled`) together in 1 enum. For actual functional control, still use `modelValue` (checked/unchecked) and `disabled` (boolean) separately — `state` is more for overriding the appearance (including `'Error'`, which doesn't represent checked/unchecked but rather failed-validation styling).

## Events
| Event | Payload | When It Fires |
|---|---|---|
| `update:modelValue` | `boolean` | For `v-model` binding |
| `change` | `boolean` | Optional side effect, same value as `v-model` |

## ✅ Do
- Use `modelValue` + `v-model` as the functional source of truth for on/off — `state` is only for visual overrides (e.g. `state="Error"` when validation fails).
- Use Switch for changes whose **effect applies immediately** with no need for a separate submit button (e.g. toggling a setting that saves right away). If the change needs to be confirmed/submitted first, consider Checkbox inside a regular form instead.
- Include a `label` that clearly states what's being toggled (e.g. "Email notifications"), so the switch doesn't stand alone without context.
- Listen for `change` to trigger side effects (e.g. an API call to save the preference), ideally with an optimistic update and a fallback if the API fails (revert the switch to its previous position).

## ❌ Don't
- Don't use `state` as a substitute for `modelValue` to control the actual checked/unchecked value — `state` is presentational and doesn't guarantee the data value that gets submitted/saved.
- Don't use Switch for a choice that needs to be submitted together with other form fields (e.g. part of a long registration form) — use Checkbox instead for consistency with the regular form pattern.
- Don't forget to handle API failure when `change` fires for an action with a side effect (e.g. an API call) — if it fails, the switch should be reverted to its previous position; don't let the UI show a status that doesn't match the actual backend condition.

## Additional Context
- Since `state` can contain a combination of checked+disabled at once (`'On disabled'`, `'Off disabled'`), make sure the implementation doesn't rely on `state` for any logic — treat it purely as a visual reference/override, with `modelValue` and `disabled` as the sole sources of truth for behavior.