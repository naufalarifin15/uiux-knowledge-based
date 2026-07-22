# Tabs

## Function & When to Use
Tabs group several equivalent/parallel content panels, showing only 1 panel at a time. Good for content at the same level (e.g. "General Info" / "History" / "Documents" within 1 detail page).

**Difference from Accordion:** Tabs are for parallel content where the user only needs to see 1 at a time without a long scroll history; Accordion is for content that naturally stacks vertically and can be summarized/hidden together (see `accordion.md`).

## Variant Guide

**Dimension 1 — Variant (visual style)**
| Value | Visual | When to Use |
|---|---|---|
| `'inner'` | Tab triggers inside a container/pill with a background (segmented control) | Default — tabs inside a card/section that already has its own container, a more compact context |
| `'outer'` | Tabs with an underline (indicator) and no container, similar to traditional tabs | Tabs as the main page-level navigation, with clear separation from the content below |

**Dimension 2 — Full Width**
| Value | When to Use |
|---|---|
| `false` (default) | Many tabs or long labels — tabs adjust to their own content width |
| `true` | Few tabs (2-4) that need to evenly fill the container width, e.g. in a mobile layout |

## Props Structure

**Tabs**
| Prop | Type | Default | Description |
|---|---|---|---|
| `items` | `TabItem[]` | **required** | Array of tab items |
| `defaultValue` | `string` | — | The tab value that's active initially |
| `variant` | `'inner'` \| `'outer'` | `'inner'` | Visual style |
| `fullWidth` | `boolean` | `false` | Stretches tabs to fill the container width |

**TabItem**
| Field | Type | Description |
|---|---|---|
| `value` | `string` | Unique tab identifier |
| `label` | `string` | Tab header text |
| `icon` | `Component` (optional) | Icon before the label |
| `badge` | `string \| number` (optional) | Badge count on the tab (e.g. number of new items) |
| `content` | `any` (optional) | Content rendered in that tab's panel |

## Events
| Event | Payload | When It Fires |
|---|---|---|
| `change` | `string` (new tab value) | When the active tab changes |

## ✅ Do
- Use `variant="outer"` for tabs that serve as the page's main navigation (e.g. switching between large sections); use `variant="inner"` (default) for tabs inside a smaller card/container.
- Consistently use `icon` for all `TabItem`s in 1 group, or none at all — don't mix some tabs with icons and some without within the same group.
- Use `badge` for genuinely relevant information (e.g. the number of unread items in that tab), not as decoration.
- Listen for the `change` event when there's logic that needs to run on tab switch (e.g. lazy-loading data for the newly active tab, so you don't fetch all data for every tab at once).
- Use `fullWidth={true}` for cases with few tabs in a narrow layout (mobile) so the tabs look proportionally sized to fill the screen width.

## ❌ Don't
- Don't use Tabs for content whose count could be very large (more than ~6-7 tabs) — consider other navigation (e.g. Select or a sidebar) when there are too many options to show side by side.
- Don't use `fullWidth={true}` when there are many tabs — each tab will become too narrow and labels could get truncated.
- Don't place content that's interdependent between tabs (e.g. a multi-step form that must be sequential) — Tabs are for independent/equivalent content, not a sequential flow (for that, consider a step/wizard component if available).

## Additional Context
- No controlled prop (e.g. `value`/`modelValue`) is visible for Tabs in this reference, only `defaultValue` (uncontrolled) and the `change` event — if you need to programmatically switch the active tab from outside (e.g. navigating to a specific tab via code), check whether the component provides another way to do that before assuming it can simply be re-set like a typical controlled component.