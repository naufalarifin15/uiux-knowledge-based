# Number Input

## Function & When to Use
Number Input is for entering numeric values with increment/decrement controls (a stepper), min/max limits, and a custom step. Used for fields that are semantically numbers with a clear boundary (e.g. item quantity, age, dosage, quantity) — not just a regular `Input` with `type="number"`.

## Props Structure

| Prop | Type | Default | Description |
|---|---|---|---|
| `modelValue` | `string` | — | Current value (controlled), used with `v-model` |
| `defaultValue` | `string` | — | Initial value (uncontrolled) |
| `placeholder` | `string` | `'Placeholder'` | Placeholder text |
| `min` | `number` | — | Minimum value limit |
| `max` | `number` | — | Maximum value limit |
| `step` | `number` | `1` | Increment/decrement amount per stepper click |
| `disabled` | `boolean` | `false` | Disables the input |
| `error` | `boolean` | `false` | Shows error styling |
| `state` | `'Default'` \| `'Disabled'` \| `'Error'` \| `'Focus'` | `'Default'` | Visual state — **overlaps with the `disabled`/`error` booleans, see note below** |
| `name` | `string` | — | Field name for the form |
| `className` | `string` | — | Additional CSS class |

## Events — Important Differences
| Event | Payload | When It Fires |
|---|---|---|
| `update:modelValue` | `string` | Every change, used for `v-model` |
| `change` | `{ value: string, valueAsNumber: number }` | Every change, with a ready-to-use numeric detail |

> For numeric calculation needs (summation, range validation, etc.), use **`valueAsNumber` from the `change` event**, not a manual `parseFloat`/`Number()` from `modelValue` (which is typed as a string) — the component already provides its numeric version directly.

## ✅ Do
- Always set `min`/`max` for fields with a reasonable business-driven value limit (e.g. quantity can't be negative, age has a sensible upper bound) — don't leave it unbounded by default when there's a clear business rule.
- Use `valueAsNumber` from the `change` event for logic that needs a number (calculations, comparisons), rather than manually converting from `modelValue`.
- Match `step` to a sensible unit for the context (e.g. `step={0.5}` for an input that needs decimal precision, `step={1}` for whole-number quantities).
- Keep `disabled`/`error` (booleans) consistent with `state` — if a field is disabled, set `disabled={true}` and `state="Disabled"` together, not just one of them.

## ❌ Don't
- Don't leave `min`/`max` empty for a field that has a clear business-driven limit — validating only at form submission is too late; it's better to prevent it right from the input.
- Don't manually parse `modelValue` (string) for calculations when `valueAsNumber` is already available in the `change` event — reduces the risk of parsing bugs (e.g. decimal locale, empty string, etc.).
- Don't set `state="Error"` without also setting `error={true}`, or vice versa — keep both error indicators in sync.
- Don't use Number Input for values that aren't actually pure numbers (e.g. phone numbers, postal codes that may start with 0) — use `Input` with `type="tel"`/`text` for that case, since Number Input normalizes the value into a number.

## Additional Context
- Since there are 2 props indicating error (`error` boolean and `state="Error"`) and 2 indicating disabled (`disabled` boolean and `state="Disabled"`), make sure the implementation always changes both together via 1 computed/helper, so no condition is forgotten to sync in one place.