# Combobox

## Function & When to Use
Combobox is similar to Select — choosing a value from a list of options — but the search input lives **inside the field itself**, not inside the dropdown panel. Clicking/focusing the field turns it into a text input where the user types directly to filter options, and the option list appears as a dropdown below it.

**Difference from Select:** In Select, the search field is a separate input rendered inside the dropdown panel (see `select.md`) — the trigger itself is just a display button, not typeable. In Combobox, the trigger field *is* the search input — there's no separate search box inside the dropdown.

## Variant Guide

**Open Behavior (config for when the option list appears)**
| Value | Behavior | When to Use |
|---|---|---|
| `'immediate'` | Option list opens as soon as the field gets focus, before the user types anything | Short/medium option lists where browsing without typing is useful (e.g. picking from a known short list of statuses) |
| `'onType'` | Option list only appears after the user starts typing | Long option lists where showing everything on focus would be overwhelming |

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
| *(TBD: prop name)* | `boolean` | *(TBD)* | Toggles whether `create-option` is enabled — confirmed to exist and be toggleable, exact prop name and default not yet verified |

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
| `create-option` | `string` | Fires when the user submits a typed value that doesn't match any existing option. Handling is **manual** — the app must push the new value into `items` itself; the component does not add it automatically. Can be enabled/disabled via a dedicated prop (see Props Structure) |

## Shared Feature — Clear Button (Select & Combobox)
Both Select and Combobox support a **clear/remove button** that appears once a value is filled/selected, toggleable via `clearable`:
- `clearable={true}` (default) — shows an "×" affordance inside the field once there's a selected value, letting the user reset the field in one click without opening the dropdown first.
- `clearable={false}` — hides it; the user must open the dropdown/list and deselect manually, or the field simply can't be cleared once set (depending on other required-field rules).

## Shared Feature — Create Option (Combobox & Select)
Combobox supports letting the user add a new option by typing a value that doesn't exist in `items`, via the `create-option` event. This is **manually handled** — on receiving the event, the app must append the new value to `items` itself (e.g. `{ label: value, value }`); the component doesn't mutate `items` on its own. **Select has this same event too** (confirmed via the component's type signature) — see `select.md`.

## ✅ Do
- Use Combobox (instead of Select) when the interaction should feel like typing to filter, with the typed text staying visible in the field itself — e.g. searching a long list of doctors/patients by name.
- Use `openBehavior="onType"` for large option lists, so the dropdown doesn't try to render everything the moment the field is focused.
- Use `openBehavior="immediate"` for shorter, locally-available lists where letting the user browse without typing first is genuinely helpful.
- **Always treat `value`/`modelValue` as an array**, even for single selection — same rule as Select, take `value[0]` for the single value.
- Set `clearable={false}` only for fields where clearing to an empty state doesn't make sense (e.g. a required field that must always resolve to a valid value) — for most use cases, keep the default `clearable={true}` so users can easily reset their input.
- Enable the create-option toggle only in contexts where adding a new value on the fly is actually valid for that field (e.g. tags, free-form categories) — not for fields that must only accept a fixed, known set of values.
- On `create-option`, always update `items` manually (append the new value) — the component won't do this for you, so skipping it means the newly "created" option won't actually appear as selectable afterward.

## ❌ Don't
- Don't assume the search box is separate from the field like in Select — in Combobox, typing directly in the field *is* the search mechanism, there's no secondary search input inside the dropdown.
- Don't use `openBehavior="immediate"` for very large datasets — this can force rendering the full list before the user has typed anything to narrow it down.
- Don't mix `value` (controlled) and `defaultValue` (uncontrolled) at the same time.
- Don't set `clearable={false}` by default across the whole app "just in case" — this removes a convenience most users expect once a field has typeahead behavior.
- Don't leave the create-option toggle enabled for fields that must only accept predefined values (e.g. selecting from a fixed list of departments) — turn it off for those, since leaving it on would let users create invalid entries.

## Additional Context
- Because typing in the field doubles as both display value and search query, make sure the displayed text after selection (the option's `label`) doesn't get confused with leftover search text — clearing/re-focusing behavior should reset the field to show the selected label, not the last typed query.
- **(TBD)** There is no dedicated event for observing the raw typed query (no `search` event exists on this component, despite earlier assumptions). If remote/async filtering is needed, confirm how the app is meant to observe what the user is typing — e.g. by watching `value`, or another mechanism — before implementing that pattern.