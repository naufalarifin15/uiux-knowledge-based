# Table

## Function & When to Use
Table displays tabular data with customizable column rendering, optionally sortable. **Table doesn't handle pagination itself** — for large datasets, pair it separately with the Pagination component (see `pagination.md`).

## Props Structure

**Table**
| Prop | Type | Default | Description |
|---|---|---|---|
| `columns` | `Column[]` | **required** | Column definitions |
| `data` | `any[]` | **required** | Array of row data |
| `size` | `'md'` \| `'sm'` | `'md'` | Row height |
| `border` | `'all'` \| `'top-bottom'` | `'all'` | Border style |
| `zebra` | `boolean` | `false` | Alternating row background color |
| `hoverable` | `boolean` | `true` | Highlights the row on hover |

**Column Definition**
| Field | Type | Description |
|---|---|---|
| `key` | `string` | Must match the field name in the row data |
| `label` | `string` | Column header text |
| `sortable` | `boolean` (optional) | Shows a sort icon, emits the `sort` event when the header is clicked |
| `render` | `(value, row) => any` (optional) | Custom render for the cell content (e.g. currency formatting, a status badge, a date) |

## Events
| Event | Payload | When It Fires |
|---|---|---|
| `sort` | `string` (column `key`) | When a sortable column header is clicked |

> **Table doesn't perform sorting itself** — the `sort` event only reports which column was clicked. The ordering logic (ascending/descending, sorting the `data` array) is entirely the implementation's responsibility: store the sort direction state, re-sort `data` at the parent level, then send the already-sorted array back into the `data` prop.

## ✅ Do
- Use `render` for columns that need special formatting (e.g. Status becomes a colored Badge, a number becomes a currency format, a date becomes a localized format) — don't pre-format the raw data in the `data` prop; let `data` keep its raw/original values and handle formatting in `render`.
- Manage the sort direction state (`asc`/`desc`) manually at the parent level when listening for the `sort` event — toggle the direction each time the same column is clicked again, then re-sort `data` according to that direction.
- Pair it with a **Pagination** component (see `pagination.md`) for large datasets — don't render hundreds/thousands of rows at once without pagination.
- Use `zebra` for tables with many columns that need visual help scanning rows horizontally.
- Set `size="sm"` for tables with many columns/dense data, `size="md"` (default) for most cases.

## ❌ Don't
- Don't expect `data` to be automatically sorted after the `sort` event fires — the component only sends the `key` of the clicked column, it doesn't perform any actual sorting.
- Don't use a `key` that doesn't match an actual field in `data` — this will result in an empty cell since `key` is used to match the field.
- Don't put heavy logic/side effects (e.g. an API call) inside the `render` function — this function is called repeatedly for every cell/re-render and should be a pure display transformation only.
- Don't render an entire large dataset without Pagination — it will impact render performance, especially for tables with many custom `render` columns.

## Additional Context
- Since Table and Pagination are 2 separate components, make sure the `data` sent to Table is already **sliced to the current page** (not the entire dataset) — Table only renders what's given to the `data` prop, it doesn't do its own slicing based on the page.