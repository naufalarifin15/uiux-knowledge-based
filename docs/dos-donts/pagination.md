# Pagination & Rows Per Page (Family)

## Function & When to Use
These 2 components **complement each other** and are usually used side by side in a table/list footer:
- **Pagination** — navigation between pages (page numbers, prev/next)
- **Rows Per Page** — selecting how many items are shown per page, plus "X-Y of Z rows" info

Both share the concept of `pageSize`/number of items per page, so they **must be kept in sync** — a change in one component affects the calculation in the other.

## Props Structure

**Pagination**
| Prop | Type | Default | Description |
|---|---|---|---|
| `count` | `number` | **required** | Total **number of items**, not the number of pages |
| `pageSize` | `number` | `10` | Number of items per page |
| `page` | `number` | — | Active page (controlled), used with **`v-model:page`** |
| `defaultPage` | `number` | `1` | Initial page (uncontrolled) |
| `siblingCount` | `number` | `1` | Number of page buttons on the left-right of the active page before truncating into `...` |
| `className` | `string` | `''` | Additional CSS class |

**Rows Per Page**
| Prop | Type | Default | Description |
|---|---|---|---|
| `modelValue` | `number` | **required** | Selected number of rows per page (controlled), used with `v-model` |
| `totalItems` | `number` | **required** | Total items in the dataset — **must be the same value as `count` in Pagination** |
| `currentPage` | `number` | `1` | The currently active page — used to compute the range text ("1-10 of 247 rows"), **must be in sync with `page` in Pagination** |
| `options` | `number[]` | `[5, 10, 20, 50, 100]` | Available rows-per-page choices |
| `showItemsInfo` | `boolean` | `true` | Shows the "X-Y of Z rows" text |

## Events
| Component | Event | Payload | When It Fires |
|---|---|---|---|
| Pagination | `update:page` | `number` | Page changes, used for `v-model:page` |
| Pagination | `page-change` | `{ page: number, pageSize: number }` | User navigates to a different page |
| Rows Per Page | `update:modelValue` | `number` | Value changes, used for `v-model` |
| Rows Per Page | `rows-per-page-change` | `number` | User selects a different rows-per-page |

## ✅ Do
- Use **1 source of truth** for `pageSize`/rows-per-page, then supply the same value to `pageSize` (Pagination) and `modelValue` (Rows Per Page) — don't let 2 separate states exist that could desync.
- Use **1 source of truth** for the total item count, supplying the same value to `count` (Pagination) and `totalItems` (Rows Per Page).
- Sync `page` (Pagination) and `currentPage` (Rows Per Page) — both represent the same page.
- **Reset the page to 1** every time `rows-per-page-change` fires — if the user switches from 10 to 50 rows per page while on page 5, page 5 with the new pageSize is very likely no longer valid.
- Listen for `page-change` and `rows-per-page-change` to trigger a new data fetch from the backend, using the latest `page`/`pageSize` parameters.
- Fill `count`/`totalItems` with the total item count **after filters/search** have been applied, and re-update it every time the filter changes.

## ❌ Don't
- Don't let `pageSize` (Pagination) and `modelValue` (Rows Per Page) be set from 2 separate states that don't update each other — this will produce inconsistent page-count calculations between the components.
- Don't fill `count`/`totalItems` with a manually calculated number of pages — both expect a total item **count**, not a total page count.
- Don't forget to reset the page to 1 when rows-per-page or a filter changes — the user could end up stranded on an empty page.
- Don't set `siblingCount` too large in narrow layouts (mobile) — it can potentially overflow.

## Additional Context
- The safest pattern: store `page` and `pageSize` as 2 reactive states at the parent level (e.g. a `usePagination` composable), then supply both to Pagination and Rows Per Page as props, and update that state via events from both components — so there's no possibility of drift between the values shown in the 2 different components.