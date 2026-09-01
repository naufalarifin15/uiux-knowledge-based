# Combobox

## Function & When to Use
Combobox is similar to Select — choosing a value from a list of options — but the search input lives **inside the field itself**, not inside the dropdown panel. Clicking/focusing the field turns it into a text input where the user types directly to filter options, and the option list appears as a dropdown below it.

**Difference from Select:** In Select, the search field is a separate input rendered inside the dropdown panel (see `select.md`) — the trigger itself is just a display button, not typeable. In Combobox, the trigger field *is* the search input — there's no separate search box inside the dropdown.

## Variant Guide

**Open Behavior (config for when the option list appears)**
| Value | Behavior | When to Use |
|---|---|---|
| `'immediate'` | Option list opens as soon as the field gets focus, before the user types anything | Short/medium option lists where browsing without typing is useful (e.g. picking from a known short list of statuses) |
| `'onType'` | Option list only appears after the user starts typing | Long option lists or remote/async search, where showing everything on focus would be overwhelming or expensive to fetch |

## Props Structure

| Prop | Type | Default | Description |
|---|---|---|---|
| `items` | `ComboboxOption[]` | `[]` | List of options |
| `value` | `string[]` | — | Selected value (controlled) — **always an array, even for single selection**, consistent with Select's convention |
| `defaultValue` | `string[]` | — | Initial value (uncontrolled) |
| `placeholder` | `string` | `'Search or select...'` | Placeholder text shown in the field before typing/selecting |
| `openBehavior` | `'immediate'` \| `'onType'` | `'immediate'` | Controls when the option list appears — see Variant Guide |
| `multiple` | `boolean` | `false` | Allows selecting more than 1 option |
| `clearable` | `boolean` | `true` | Shows a clear/remove button once a value is selected — **shared behavior with Select, see note below** |
| `emptyMessage` | `string` | `'No options found'` | Message shown when there are no matching results |
| `disabled` | `boolean` | `false` | Disables the combobox |
| `error` | `boolean` | `false` | Shows error styling |

**ComboboxOption**
| Field | Type | Description |
|---|---|---|
| `label` | `string` | Displayed text |
| `value` | `string` | Option value |
| `disabled` | `boolean` (optional) | Disables only this option |
| `group` | `string` (optional) | Group header name — same grouping behavior as `SelectOption.group` |

## Events
| Event | Payload | When It Fires |
|---|---|---|
| `update:modelValue` | `string[]` | For `v-model` binding, fires on selection |
| `change` | `string[]` | Optional side effect, same value as `v-model` |
| `search` | `string` | Fires on every keystroke inside the field — the raw typed query, useful for async/remote filtering |

## Shared Feature — Clear Button (Select & Combobox)
Both Select and Combobox support a **clear/remove button** that appears once a value is filled/selected, toggleable via `clearable`:
- `clearable={true}` (default) — shows an "×" affordance inside the field once there's a selected value, letting the user reset the field in one click without opening the dropdown first.
- `clearable={false}` — hides it; the user must open the dropdown/list and deselect manually, or the field simply can't be cleared once set (depending on other required-field rules).

## ✅ Do
- Use Combobox (instead of Select) when the interaction should feel like typing to filter, with the typed text staying visible in the field itself — e.g. searching a long list of doctors/patients by name.
- Use `openBehavior="onType"` for large or remotely-fetched option lists, so the dropdown doesn't try to render everything (or fire a fetch) the moment the field is focused.
- Use `openBehavior="immediate"` for shorter, locally-available lists where letting the user browse without typing first is genuinely helpful.
- **Always treat `value`/`modelValue` as an array**, even for single selection — same rule as Select, take `value[0]` for the single value.
- Set `clearable={false}` only for fields where clearing to an empty state doesn't make sense (e.g. a required field that must always resolve to a valid value) — for most use cases, keep the default `clearable={true}` so users can easily reset their input.
- Listen to `search` for async/remote filtering (e.g. querying a backend as the user types), and debounce it at the application level — the component only emits the raw keystroke, it doesn't debounce for you.

## ❌ Don't
- Don't assume the search box is separate from the field like in Select — in Combobox, typing directly in the field *is* the search mechanism, there's no secondary search input inside the dropdown.
- Don't use `openBehavior="immediate"` for very large datasets — this can force rendering (or fetching) the full list before the user has typed anything to narrow it down.
- Don't mix `value` (controlled) and `defaultValue` (uncontrolled) at the same time.
- Don't ignore the `search` event when doing remote filtering and instead try to filter `items` locally if `items` doesn't actually contain the full dataset — for async search, `items` is expected to be updated externally based on the `search` payload.
- Don't set `clearable={false}` by default across the whole app "just in case" — this removes a convenience most users expect once a field has typeahead behavior.

## Additional Context
- Because typing in the field doubles as both display value and search query, make sure the displayed text after selection (the option's `label`) doesn't get confused with leftover search text — clearing/re-focusing behavior should reset the field to show the selected label, not the last typed query.