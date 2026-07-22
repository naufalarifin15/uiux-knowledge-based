# Input

## Function & When to Use
Input is a basic text field for forms — supports various HTML input types, prefix/suffix text, icons, and disabled/error states. Used for almost all text/number/email/password inputs in a form.

## Props Structure

| Prop | Type | Default | Description |
|---|---|---|---|
| `modelValue` | `string` | — | Current value, used with `v-model` (controlled) |
| `defaultValue` | `string` | — | Initial value for uncontrolled mode |
| `placeholder` | `string` | `'Placeholder'` | Placeholder text |
| `type` | `'text'` \| `'email'` \| `'password'` \| `'number'` \| `'tel'` \| `'url'` \| `'search'` | `'text'` | HTML input type, affects validation & mobile keyboard |
| `disabled` | `boolean` | `false` | Disables the input |
| `error` | `boolean` | `false` | Shows error styling |
| `labelLeft` | `string` | — | Prefix text inside the input (e.g. `https://`) |
| `labelRight` | `string` | — | Suffix text inside the input (e.g. `kg`, `%`) |
| `iconLeft` | `Component` | — | Icon on the left side |
| `iconRight` | `Component` | — | Icon on the right side |
| `className` | `string` | — | Additional CSS class |

## Events — Important Differences
| Event | Payload | When It Fires |
|---|---|---|
| `update:modelValue` | `string` | Every keystroke (real-time), used for `v-model` |
| `change` | `string` | When the input changes, intended for optional side effects (e.g. validation, API calls) |

> `update:modelValue` fires on **every keystroke**, while `change` is intended for **side effects** (not the main binding) — don't put heavy logic (e.g. an API call) in the `update:modelValue` listener; use `change` instead so it isn't called excessively on every keystroke.

## ✅ Do
- Choose `type` based on the kind of data requested (`email` for email, `tel` for phone numbers, `number` for numbers) — this triggers the correct mobile keyboard and basic HTML validation, not just decoration.
- Use `modelValue` + `v-model` for the general case (controlled); use `defaultValue` only for a deliberately uncontrolled case (e.g. a simple form with no reactive state).
- Use `labelLeft`/`labelRight` for prefixes/suffixes that visually blend with the input (e.g. `https://` before a URL, `kg` after a weight input) — not `placeholder`, since the placeholder disappears once the user starts typing while the left/right label stays visible.
- Use `error={true}` together with a separate error message outside the component (Input itself doesn't display error text, just styling).
- Put side-effect logic (async validation, tracking, etc.) in the `change` listener, not `update:modelValue`.

## ❌ Don't
- Don't use `modelValue` and `defaultValue` together — pick one (controlled or uncontrolled); mixing both creates ambiguity about the source of truth for the data.
- Don't use `placeholder` as a substitute for `labelLeft`/`labelRight` for a permanent unit/prefix — the placeholder disappears once the user starts typing, so context (e.g. the `kg` unit) disappears along with it.
- Don't put heavy operations (API calls, complex validation) in `update:modelValue` — this event fires on every keystroke and can cause excessive calls.
- Don't set `disabled={true}` and `error={true}` together without a clear reason — this combination rarely makes UX sense (a disabled field usually doesn't need to show an error state).

## Additional Context
- Native HTML `type="number"` has some quirks (e.g. the scroll wheel can accidentally change the value) — consider additional handling like disabling scroll-to-change if relevant for the form context (e.g. a number input in a medical form that needs precision).