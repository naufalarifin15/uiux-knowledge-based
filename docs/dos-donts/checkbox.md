# Checkbox

## Function & When to Use
Checkbox is for selecting one or more independent options (can check more than one, unlike Radio which only allows 1 selection). Supports a third `indeterminate` state — used specifically for "select all" checkboxes that represent a condition where some (but not all, and not none) child items are selected.

## Variant Guide

**Dimension 1 — Functional State (`modelValue`, used with `v-model`)**
| Value | Meaning |
|---|---|
| `false` | Not selected |
| `true` | Selected |
| `'indeterminate'` | Partially selected — specifically for a parent checkbox representing a group with some child items checked |

**Dimension 2 — Visual State Preset (`state`)**
A prop separate from `modelValue`, used to override the visual appearance presentationally — including states that **don't represent checked/unchecked**, such as `'Error'` for failed-validation styling.

| Value | When to Use |
|---|---|
| `'Uncheck'` | Default, synced with `modelValue = false` |
| `'Checked'` | Synced with `modelValue = true` |
| `'Indeterminate'` | Synced with `modelValue = 'indeterminate'` |
| `'Error'` | Shows error styling (e.g. red border) when form validation fails, regardless of its checked value |

> The `state` list has other options not fully covered here (marked with `...` in the props table) — check the package types directly for the complete list before using a value outside what's documented here.

## ✅ Do
- Use `modelValue` + `v-model` as the **functional source of truth** — this determines the actual data value, not `state`.
- Use `'indeterminate'` specifically for a "select all" checkbox when some (not all) child items are checked.
- Use `state="Error"` to show failed-validation styling, while still keeping `modelValue` at its actual value (checked/unchecked) — these two props are independent and can be combined.
- Use the `update:modelValue` event for `v-model` binding; use `change` only if you need an additional side effect outside of the data binding (e.g. triggering validation, analytics).
- Disable interaction via the `disabled` prop, not by manipulating `state`.

## ❌ Don't
- Don't use `state` as a substitute for `modelValue` to control the actual checkbox value — `state` is purely visual/presentational, changing it doesn't change the data that gets submitted.
- Don't let `state` and `modelValue` fall out of sync without reason (e.g. `state="Checked"` but `modelValue=false`) except for special cases like `state="Error"`, which is independent from the checked value.
- Don't use `'indeterminate'` for a regular standalone checkbox (not a group's parent checkbox) — this state only makes semantic sense for representing a group.

## Additional Context
- Checkbox emits 2 events for the same condition (`update:modelValue` and `change`) — make sure you're not duplicating logic in both at once for the same action; pick one based on your need (v-model vs. a manual listener).