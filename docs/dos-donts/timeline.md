# Timeline

## Function & When to Use
Timeline (per-item) displays 1 entry in chronological order with a connector line linking items together — used repeatedly (e.g. via `v-for`) to form a full timeline (e.g. patient visit history, activity log, process stages).

> This is a **per-item** component, not a full timeline wrapper — rendering the complete list means rendering many instances of this component in sequence, with `placement` set according to each one's position in the list.

## Variant Guide

**Dimension 1 — Placement (position in the list, controls the connector line)**
| Value | When to Use |
|---|---|
| `'start'` | The **first** item in the list — the connector line only connects downward |
| `'middle'` | An item in the **middle** of the list (default) — the connector line connects both upward and downward |
| `'end'` | The **last** item in the list — the connector line only connects upward |

> **Must be set according to the index position when looping** — if every item is left at the default `'middle'`, the connector line on the first and last items will look dangling/unnatural (a line that shouldn't exist at the ends of the list).

**Dimension 2 — Type (card style)**
| Value | Visual | When to Use |
|---|---|---|
| `'default'` | Plain card | A regular timeline item |
| `'active'` | Light blue background | The item currently the focus/most recent status (e.g. a process stage in progress) |
| `'custom'` | Custom | Exception cases not covered by the 2 styles above — use with caution |

**Dimension 3 — Icon Style (indicator shape)**
| Value | Visual | When to Use |
|---|---|---|
| `'default'` | A plain small dot | A regular timeline item with no special emphasis |
| `'icon'` | A 24px circle with a status icon | An item that needs clearer visual emphasis on its status (combined with the `status` prop) |

**Dimension 4 — Status (semantic meaning, used together with `icon='icon'`)**
| Value | Function |
|---|---|
| `'success'` | Stage completed/successful |
| `'info'` | Neutral information |
| `'warning'` | Needs caution |
| `'error'` | Failed/problematic |

## Props Structure

| Prop | Type | Default | Description |
|---|---|---|---|
| `placement` | `'start'` \| `'middle'` \| `'end'` | `'middle'` | See Dimension 1 |
| `type` | `'default'` \| `'active'` \| `'custom'` | `'default'` | See Dimension 2 |
| `icon` | `'default'` \| `'icon'` | `'default'` | See Dimension 3 |
| `status` | `'success'` \| `'info'` \| `'warning'` \| `'error'` | `'success'` | See Dimension 4 |
| `date` | `string` | `'DD/MM/YY'` | Date label |
| `time` | `string` | `'00:00'` | Time label |
| `title` | `string` | `'Timeline Title'` | Main title |
| `description` | `string` | `'Timeline Description'` | Supporting text |

## ✅ Do
- Set `placement` explicitly based on the index while looping: item 0 → `'start'`, the last item → `'end'`, the rest → `'middle'` (default).
- Use `type="active"` to highlight the item representing the **current** status/stage in a process (e.g. a visit status that's currently ongoing), not just any item.
- Use `icon="icon"` + the matching `status` for items that need clear status emphasis (e.g. `status="error"` for a failed stage); leave `icon="default"` (plain dot) for routine history items that don't need emphasis.
- Format `date`/`time` consistently with the format used across the whole application (refer to the localization convention in `docs/PRD.md`), rather than hardcoding different formats in different places.

## ❌ Don't
- Don't let every item use `placement="middle"` (default) when rendering the full list — the first and last items need `'start'`/`'end'` so the connector line doesn't look dangling.
- Don't use `type="custom"` as the default choice — it's for exceptions, not an alternative to `'default'`/`'active'`.
- Don't use `type="active"` for more than 1 item at once within the same timeline if its meaning is "current status" — it will confuse which one is actually the current state.
- Don't use `icon="icon"` without considering a matching `status` — this combination is designed to complement each other, with `status` determining the meaning of the displayed icon.

## Additional Context
- Since this is a per-item component, the logic for determining `placement` (start/middle/end) should ideally be computed automatically from the array index during rendering (e.g. `index === 0 ? 'start' : index === list.length - 1 ? 'end' : 'middle'`), rather than being manually hardcoded per item.