# Radio (RadioGroup)

## Function & When to Use
RadioGroup is for selecting **exactly 1 option** from several mutually exclusive choices, with all options visible at once (unlike Select, which hides options inside a dropdown). Good for a small number of choices (usually 2-5 options) that are important to see all at once without needing to click open a dropdown.

**When to choose Radio vs. Select:** use Radio when there are few options and it matters that they're all shown at once (e.g. gender, payment method); use Select when there are many options (6+) so showing them all at once would take up too much space.

## Props Structure

**RadioGroup**
| Prop | Type | Default | Description |
|---|---|---|---|
| `options` | `RadioOption[]` | **required** | List of options |
| `name` | `string` | — | Form group name (important for native form grouping) |
| `value` | `string` | — | Selected value (controlled) |
| `defaultValue` | `string` | — | Initial value (uncontrolled) |
| `disabled` | `boolean` | `false` | Disables **the entire** group of radios |
| `error` | `boolean` | `false` | Shows error styling |
| `orientation` | `'horizontal'` \| `'vertical'` | `'vertical'` | Layout direction of the options |

**RadioOption**
| Field | Type | Description |
|---|---|---|
| `value` | `string` | Option value |
| `label` | `string` | Displayed text |
| `disabled` | `boolean` (optional) | Disables **only this option** (different from the `disabled` at the RadioGroup level) |

## Events
| Event | Payload | When It Fires |
|---|---|---|
| `update:modelValue` | `string \| null` | For `v-model` binding |
| `change` | `string \| null` | Optional side effect, same value as `v-model` |

> The payload can be `null` — meaning no option has been selected yet. Make sure application logic (especially form validation) handles this `null` condition as "not yet filled in," rather than assuming there's always a value as soon as RadioGroup is rendered.

## ✅ Do
- Use `orientation="horizontal"` for short options that fit side by side (e.g. "Yes"/"No"); use the default `'vertical'` for options with longer labels or a larger number of options.
- Use `disabled` at the `RadioOption` level (not at the RadioGroup level) when only certain options need to be disabled (e.g. an option that's currently unavailable), while other options remain selectable.
- Use `disabled` at the RadioGroup level only when the entire group genuinely needs to be disabled at once (e.g. a form in read-only mode).
- Set a unique `name` per RadioGroup within 1 page, especially when there are several RadioGroups at once, to avoid conflicting form semantics.
- Handle the condition `value === null` as an unfilled state, and validate accordingly (e.g. requiring 1 selection before submit).

## ❌ Don't
- Don't use RadioGroup for more than ~5-7 options — it will take up a lot of vertical/horizontal space; consider Select for that case.
- Don't set `disabled` at the RadioGroup level if the intent is only to disable 1-2 specific options — use `disabled` at the `RadioOption` level for that instead.
- Don't assume there's always 1 option automatically selected at the start — if no `value`/`defaultValue` is set, the initial state is `null` (no selection yet).

## Additional Context
- Since `value` can be `null`, make sure the UI (e.g. border/color) distinguishes the "no selection yet" state from a "validation error" state, so users aren't confused between not having chosen yet vs. having actually chosen incorrectly.