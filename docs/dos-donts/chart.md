# Chart

## Function & When to Use
Chart visualizes numeric data in several forms (`line`, `bar`, `pie`, `doughnut`). Since each chart `type` has *different relevant props* (many props here only apply to a specific type), choosing the right type determines which props need to/can be filled in.

## Variant Guide

**Dimension 1 — Type (chart shape)**
| Value | When to Use |
|---|---|
| `line` | Shows trends/changes in data along a continuous axis, e.g. data over time |
| `bar` | Compares values across discrete categories, e.g. comparing across days/groups |
| `pie` | Shows the proportion/composition of parts relative to a whole, with few segments |
| `doughnut` | Same as `pie`, a version with a hole in the middle — a visual style choice, not a functional difference |

**Dimension 2 — Props Applicability (which props apply to which type)**
| Prop | Applies to | Description |
|---|---|---|
| `labels` | All (different meaning) | X-axis labels for `line`/`bar`; segment names for `pie`/`doughnut` |
| `datasets` | All | 1+ data series for `line`/`bar`. **`pie`/`doughnut` only accept 1 dataset** |
| `showLegend` | All | Clickable legend below the chart |
| `showGrid` | `line`, `bar` only | Horizontal grid lines |
| `showDataLabels` | All (different context) | Value labels above bars or data points |
| `dropLines` | `line` only | Vertical dashed lines from a data point to the X axis |
| `fill` | `line` only | Fills the area under the line |
| `xTitle` / `yTitle` | `line`, `bar` only | X/Y axis title — **not relevant for `pie`/`doughnut`** since they have no axes |
| `height` | All | Canvas height in px, default `300` |

**Dimension 3 — ChartDataset Fields (per data series)**
| Field | Applies to | Description |
|---|---|---|
| `label` | All | Series name, appears in legend/tooltip |
| `data` | All | Numeric values |
| `color` | `line`, `bar` | Overrides the color of 1 series. Fill with a DS primary hex so it's automatically paired with the DS secondary as the fill |
| `colors` | `pie`, `doughnut` | Array of colors per segment. If fewer than the number of segments, lightness variations are auto-generated |
| `pointColor` | `line` only | Color of the point/dot, independent from the line color. Defaults to follow `color` |

## ✅ Do
- Choose `type` based on **the nature of the data**, not visual preference — trend/time → `line`, category comparison → `bar`, proportion/composition → `pie`/`doughnut`.
- For `pie`/`doughnut`, make sure `datasets` contains only **1 dataset** — sending more than that violates the component's expectations.
- Fill in `xTitle`/`yTitle` only for `line`/`bar` — don't fill them in for `pie`/`doughnut` since there's no axis to explain.
- Use `color` (singular) to override 1 series in `line`/`bar`, and `colors` (plural/array) for per-segment coloring in `pie`/`doughnut` — don't mix these up since they apply to different fields.
- Use `pointColor` in `line` when the point color needs to differ from the line color (e.g. a darker point for contrast), rather than relying on the same `color` for both.

## ❌ Don't
- Don't use `dropLines`/`fill` for `bar`/`pie`/`doughnut` — these props are only relevant for `line` and won't have an effect (or may error) on other types.
- Don't send multiple `datasets` for `pie`/`doughnut` — the component only expects a single series for these types.
- Don't enable `showGrid` for `pie`/`doughnut` — there's no concept of a grid on a chart without axes.
- Don't let the length of `labels` mismatch the length of `data` in each dataset — this will cause a mismatch between categories and values.
- Don't use `pie`/`doughnut` for data with many segments (more than ~6-7) — the proportions become hard to read; consider `bar` as an alternative for that case.

## Additional Context
- Since many props are conditional on `type`, when generating a new chart make sure `type` is determined first before filling in other props, so you don't add props that are irrelevant/have no effect.