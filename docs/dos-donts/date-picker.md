# Date Picker (Family)

## Function & When to Use
Date Picker is **a family of 4 separate components** in the package, not 1 component with variants. The four are distinguished by a combination of 2 independent dimensions:

- **Range?** — selecting a single date, or a range (start–end)
- **Time?** — date only, or date + time

| Component | Range | Time | `modelValue` Type | Calendar Display |
|---|---|---|---|---|
| `DatePicker` | No | No | `string` (`"YYYY-MM-DD"`) | 1 calendar |
| `DateRangePicker` | Yes | No | `[string, string] \| null` | 2 calendars side by side |
| `DateTimePicker` | No | Yes | `string` (`"YYYY-MM-DD HH:mm"`) | 1 calendar + 1 time input |
| `DateTimeRangePicker` | Yes | Yes | `[string, string] \| null` (each `"YYYY-MM-DD HH:mm"`) | 2 calendars + 2 time inputs (Start Time, End Time) |

> Choose the component based on this combination — **don't** try to force one component to mimic the function of another (e.g. using `DatePicker` and then manually adding a separate time input; use `DateTimePicker` directly instead).

## Props (same across all 4 components)
| Prop | Type | When to Use |
|---|---|---|
| `v-model` / `modelValue` | Differs per component (see table above) | Binds the selected date/range value |
| `state` | `'default'` \| `'disabled'` \| `'error'` \| `'focus'` | Visual state — same pattern as in Checkbox/other components |
| `placeholder` | `string` | Default differs per component (see each format) |
| `className` | `string` | Additional CSS class on the root element |

## Events — Important Differences Between Components
All 4 components have an `update:modelValue` event (for `v-model`) and a `change` event, **but the `change` timing differs**:

| Component | When `change` Fires |
|---|---|
| `DatePicker` | Every time a date is selected |
| `DateRangePicker` | After the **end** date of the range is selected (not when the start date is selected) |
| `DateTimePicker` | Every time there's a change (either date or time) |
| `DateTimeRangePicker` | After the range is fully confirmed (date + start & end time) |

> For the Range variants, don't assume `change` fires twice (once per date) — this event only fires **after the full range has been selected**.

## ✅ Do
- Use `DatePicker` as the default for a single date input without time (the most common case, e.g. birth date, document date).
- Use `DateRangePicker` when the user needs to select a period (e.g. a "from–to" report filter).
- Use `DateTimePicker` when precise time is needed (e.g. an appointment schedule).
- Use `DateTimeRangePicker` when both a period AND precise time are needed at once (e.g. a shift schedule with start-end times).
- For the Range variants, listen for `change` (not `update:modelValue`) when the logic that runs should only fire after the full range has been selected (e.g. triggering a report data fetch).
- Set `state="error"` when validation fails (e.g. a required date field is empty), consistent with the `state` pattern in other form components (Checkbox, etc.).

## ❌ Don't
- Don't use `DatePicker` and then manually add a separate time input — use `DateTimePicker`, which already combines both with a consistent value format.
- Don't assume the `modelValue` format is the same across all components — variants with Time use `"YYYY-MM-DD HH:mm"`, while those without Time use just `"YYYY-MM-DD"`. Range variants wrap it as a `[string, string]` tuple.
- Don't listen for `update:modelValue` to trigger logic that should wait for a full range — in the Range variants, `update:modelValue` may fire earlier for v-model syncing purposes before the range is actually complete; use `change` for that instead.
- Don't mix in manual placeholder formats that differ from the package default — leave the default (`DD/MM/YYYY`, etc.) unless there's a specific localization requirement.

## Additional Context
- Note that **the placeholder uses a period separator for time** (e.g. `00.00`) while **the stored value uses ISO format with a colon** (`HH:mm`) — this is a difference between the placeholder's visual display and the actual data format; don't mix these up when parsing/formatting the value outside the component.
- For all variants, `state` is purely visual (same pattern as other components) — make sure actual form validation is still controlled by application logic, not relying on `state="error"` as the sole indicator.