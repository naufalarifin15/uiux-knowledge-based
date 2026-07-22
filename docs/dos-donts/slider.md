# Slider

## Function & When to Use
Slider is for selecting a numeric value within a range by dragging a thumb, supporting either single-thumb mode (1 value) or range mode (2 values/a range). Used for numeric input that's more visually intuitive than Number Input, e.g. a price range filter, volume/percentage settings.

## Variant Guide

**Dimension — Type**
| Value | Shape | `value`/`defaultValue` |
|---|---|---|
| `'Default'` | 1 thumb | `number` (single value) |
| `'Range'` | 2 thumbs | `number[]` (2 elements: [lower value, upper value]) |

## Props Structure

| Prop | Type | Default | Description |
|---|---|---|---|
| `value` | `number \| number[]` | — | Current value (controlled) — its shape follows `type` (see Variant Guide) |
| `defaultValue` | `number \| number[]` | — | Initial value (uncontrolled) |
| `min` | `number` | `0` | Minimum value |
| `max` | `number` | `100` | Maximum value |
| `step` | `number` | `1` | Increment amount per movement |
| `disabled` | `boolean` | `false` | Disables the slider |
| `type` | `'Default'` \| `'Range'` | `'Default'` | Single thumb or range (2 thumbs) |
| `label` | `string` | — | Label above the slider |
| `showValue` | `boolean` | `true` | Shows the current value next to the thumb |

## Events
| Event | Payload | When It Fires |
|---|---|---|
| `update:modelValue` | `number[]` | For `v-model` binding |
| `change` | `number[]` | Optional side effect, same value as `v-model` |

## ✅ Do
- Use `type="Default"` for single-value cases (e.g. setting volume, a 1-10 satisfaction level).
- Use `type="Range"` for range cases (e.g. a min-max price filter, an age range).
- Match `min`/`max`/`step` to the actual data unit (e.g. `step={5}` for a price filter in thousand/ten-thousand increments, rather than the default `step={1}`, which may be too fine-grained).
- Show `showValue={true}` (default) for most cases so users know the exact value currently selected, especially when `step` isn't granular (e.g. a large step).
- Include a `label` that clearly states the unit (e.g. "Price (Rp)," "Age (years)") so the slider's context is clear without needing to guess from the number alone.

## ❌ Don't
- Don't use `type="Range"` while giving `value`/`defaultValue` as a single `number` (not a 2-element array) — this will mismatch the component's expectation of 2 thumbs.
- Don't mix `value` (controlled) and `defaultValue` (uncontrolled) at the same time.
- Don't use Slider for input that needs high precision/exact values (e.g. a medication dose with a specific digit) — use Number Input for that case instead; Slider is better suited for estimation/rough ranges that rely more on visual interaction.

## Additional Context
- Make sure the data shape consumed from the `update:modelValue`/`change` event matches the `type` being used — a single `number` for `'Default'`, a `number[]` (2 elements) for `'Range'`.