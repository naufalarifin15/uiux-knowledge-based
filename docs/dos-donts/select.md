# Select

## Function & When to Use
Select is for choosing 1 or more options from a dropdown list, with built-in search and support for option grouping. Used when there are too many options for a regular Radio/Checkbox, or when a search feature within the option list is needed.

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
| `emptyMessage` | `string` | `'No options found'` | Message shown when search results are empty |
| `disabled` | `boolean` | `false` | Disables the select |
| `error` | `boolean` | `false` | Shows error styling |

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

## ✅ Do
- **Always treat `value`/`modelValue` as an array**, even for single-select (`multiple=false`) — take the first element (`value[0]`) to get the single value, don't assume the data type is a plain `string`.
- Use `group` in `SelectOption` for long lists that have a natural category (e.g. a list of provinces grouped by island) — helps users scan faster.
- Turn off `searchable={false}` for short option lists (e.g. < 5 options) where the search field just adds noise with no benefit.
- Set `disabled` at the `SelectOption` level to disable specific options (e.g. an option already selected in another select, or unavailable given the current condition) — without needing to remove it from `items`.
- Adjust `emptyMessage` to a relevant search context (e.g. `"No matching province found"`) instead of leaving the generic default, if it aids clarity.

## ❌ Don't
- Don't assume `value` is a single `string` for the `multiple=false` case — its data type is still `string[]` (an array with 1 element); it will error if treated as a plain string.
- Don't mix `value` (controlled) and `defaultValue` (uncontrolled) at the same time — pick one approach.
- Don't place options with different `group` values randomly/unordered in `items` — it's better to sort by group so the dropdown display stays organized (depends on whether the component automatically re-groups them or follows the original array order — check the actual behavior before assuming).
- Don't turn off `searchable` for a long list of options (dozens+) — users will struggle to manually scroll to find an option without search.

## Additional Context
- The `change` event carries the exact same payload as `update:modelValue` — use `change` only for additional side effects (e.g. triggering validation/analytics), not as a separate primary data source from `v-model`.