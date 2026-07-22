# Card

## Function & When to Use
Card is a generic container for visually grouping related content (border + padding + border-radius), with free-form content via the `default` slot. Used to wrap a standalone unit of information — e.g. an item in a dashboard grid, a data summary, or a form section grouping.

> Card doesn't have a fixed content structure (there's no separate `title`/`description` prop) — all content (title, description, etc. inside it) is manually composed within the `default` slot using other components (Typography, etc.).

## Variant Guide

**Density** — the only variant dimension, controlling padding, gap, and border-radius all at once (not 3 separate props).

| Value | Padding | Gap | Border Radius | When to Use |
|---|---|---|---|---|
| `xs` | 8px | 8px | 4px | Very small/dense cards, e.g. in a grid with many items at once |
| `small` | 12px | 8px | 6px | Dense contexts, compact list cards |
| `regular` | 16px | 8px | 8px | Default — general contexts |
| `medium` | 20px | 8px | 12px | Cards with slightly more detailed content |
| `large` | 24px | 8px | 16px | Card as the main visual element on the page |
| `xl` | 32px | 8px | 16px | Hero/highlight cards, generous spacing |

> Note that `gap` stays consistent at 8px across all densities — what changes significantly is only padding and border-radius.

## ✅ Do
- Choose `density` based on **the density of surrounding content** — grids with many cards at once (e.g. a dashboard) should use a smaller density (`xs`/`small`), while a single/highlight card should use a larger density (`large`/`xl`).
- Compose content inside the slot consistently across similar cards (e.g. all cards in one grid have the same title + description structure), so the grid looks tidy.
- Use `density` to control spacing, rather than adding manual padding via `className`.

## ❌ Don't
- Don't override padding/gap/border-radius via `className` when `density` already provides a matching option — this creates inconsistency with other cards using a standard density.
- Don't mix different densities for cards that sit side by side in the same grid/list — it will look uneven.
- Don't nest Card inside Card without a clear reason — stacked borders and padding will make the appearance heavy and confuse the visual hierarchy.
- Don't use `className` to change Card's fundamental structure/layout — this prop is for minor adjustments (e.g. extra outer spacing), not for significantly altering Card's visual character.

## Additional Context
- Since the `default` slot is free-form, consistency of content structure (e.g. the order of title → description → action) is the implementation's responsibility, not guaranteed by the component. It's best to establish a standard pattern per context (e.g. "Patient Info Card" always has a bold title + 1 line of description) and document it as a separate composition pattern if it's used repeatedly.