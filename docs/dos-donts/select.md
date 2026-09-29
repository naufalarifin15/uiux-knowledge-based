# Select

## Function & When to Use
Select is for choosing 1 or more options from a dropdown list, with built-in search and support for option grouping. Used when there are too many options for a regular Radio/Checkbox, or when a search feature within the option list is needed.

**Difference from Combobox:** Select has a separate search field inside the dropdown panel (the main trigger is just a display button, not directly typeable). Combobox's search field is merged into the trigger itself (you type directly in the field). See `combobox.md` for details.

## Props Structure

| Prop | Type | Default | Description |
|---|---|---|---|
| `items` | `SelectOption[]` | `[]` | List of options |
| `value` | `string[]` | — | Selected value (controlled) — **always an array, even when `multiple=false`** |
| `defaultValue` | `string[]` | — | Initial value (uncontrolled) |
| `placeholder` | `string` | `'Select an option'` | Placeholder text |
| `multiple` | `boolean` | `false` | Allows selecting more than 1 option |
| `searchable` | `boolean` | `true` | Shows the search field inside the dropdown |
| `searchPlaceholder` | `string` | `'Search...'` | Placeholder for the search field |
| `clearable` | `boolean` | `true` | Shows a clear/remove button once a value is selected — **same shared feature also in Combobox, see `combobox.md`** |
| `emptyMessage` | `string` | `'No options found'` | Message shown when search results are empty |
| `disabled` | `boolean` | `false` | Disables the select |
| `error` | `boolean` | `false` | Shows error styling |
| *(TBD: prop name)* | `boolean` | *(TBD)* | Toggles whether `create-option` is enabled — confirmed to exist (same as Combobox) via the component's type signature, but exact prop name and default not yet verified |

**SelectOption**
| Field | Type | Description |
|---|---|---|
| `label` | `string` | Displayed text |
| `value` | `string` | Option value |
| `disabled` | `boolean` (optional) | Disables only this option |
| `group` | `string` (optional) | Group header name — options sharing the same `group` are grouped together in the dropdown |

## Events
| Event | Payload | When It Fires |
|---|---|---|
| `update:modelValue` | `string[]` | For `v-model` binding |
| `change` | `string[]` | Optional side effect, same value as `v-model` |
| `create-option` | `string` | Fires when the user submits a typed search query that doesn't match any existing option — same mechanism as Combobox, see `combobox.md`'s Shared Feature section. Handling is manual — the app must push the new value into `items` itself |

## Shared Feature — Clear Button (Select & Combobox)
See `combobox.md` for the full explanation — `clearable` behaves identically in both components.

## Shared Feature — Create Option (Select & Combobox)
Select supports the same create-option pattern as Combobox: typing a search query that doesn't match any option and submitting it fires `create-option`. This is **manually handled** — on receiving the event, the app must append the new value to `items` itself (e.g. `{ label: value, value }`); the component doesn't mutate `items` on its own. See `combobox.md` for the full explanation of this shared feature — the behavior is the same in both components, only the entry point differs (typed directly in the field for Combobox, typed into the dropdown's search field for Select).

## ✅ Do
- **Always treat `value`/`modelValue` as an array**, even for single-select (`multiple=false`) — take the first element (`value[0]`) to get the single value, don't assume the data type is a plain `string`.
- Use `group` in `SelectOption` for long lists that have a natural category (e.g. a list of provinces grouped by island) — helps users scan faster.
- Turn off `searchable={false}` for short option lists (e.g. < 5 options) where the search field just adds noise with no benefit.
- Set `disabled` at the `SelectOption` level to disable specific options (e.g. an option already selected in another select, or unavailable given the current condition) — without needing to remove it from `items`.
- Adjust `emptyMessage` to a relevant search context (e.g. `"No matching province found"`) instead of leaving the generic default, if it aids clarity.
- Set `clearable={false}` only for fields that must always hold a valid value (can never be empty) — for most cases, keep the default `clearable={true}` so users can easily reset their selection.
- Enable the create-option toggle only in contexts where adding a new value on the fly is actually valid for that field (e.g. tags, free-form categories) — not for fields that must only accept a fixed, known set of values.
- On `create-option`, always update `items` manually (append the new value) — the component won't do this for you, so skipping it means the newly "created" option won't actually appear as selectable afterward.

## ❌ Don't
- Don't assume `value` is a single `string` for the `multiple=false` case — its data type is still `string[]` (an array with 1 element); it will error if treated as a plain string.
- Don't mix `value` (controlled) and `defaultValue` (uncontrolled) at the same time — pick one approach.
- Don't place options with different `group` values randomly/unordered in `items` — it's better to sort by group so the dropdown display stays organized (depends on whether the component automatically re-groups them or follows the original array order — check the actual behavior before assuming).
- Don't turn off `searchable` for a long list of options (dozens+) — users will struggle to manually scroll to find an option without search.
- Don't leave the create-option toggle enabled for fields that must only accept predefined values (e.g. selecting from a fixed list of departments) — turn it off for those, since leaving it on would let users create invalid entries.

## Additional Context
- The `change` event carries the exact same payload as `update:modelValue` — use `change` only for additional side effects (e.g. triggering validation/analytics), not as a separate primary data source from `v-model`.