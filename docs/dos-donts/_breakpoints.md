# Breakpoints

## Function & When to Use
Single source of truth for responsive breakpoint values used across all components. Every component's "Responsive Behavior" section should reference this file instead of redefining breakpoint numbers.

## Values

| Name | Range |
|---|---|
| Mobile | 0–500px |
| Tablet | 501–1023px |
| Desktop | 1024px+ |

> These values are intended to mirror the Storybook viewport config in `@siloamhospitals/ui-vue`. If that config file is accessible in the project you're working in, treat it as the actual source of truth and flag here if it ever diverges from the table above.

## Rationale
1024px is kept as the desktop threshold to continue supporting older institutional hardware still running at 1280px CSS width in some Siloam hospital sites.

## ✅ Do
- Do reference these three breakpoint values from this file in every component's Responsive Behavior section.
- Do use `min-width` media queries (mobile-first) so styles cascade upward, matching the ranges above.
- Do double-check against the actual Storybook viewport config if/when it becomes accessible, and update this file if values differ.

## ❌ Don't
- Don't redefine breakpoint pixel values inside individual component docs — reference this file instead.
- Don't use 767px as the mobile/tablet boundary — this project uses 500px.

## Additional Context
This file exists as a fallback source of truth for breakpoint values when the Storybook config isn't directly accessible in the working context. If the Storybook config path becomes known, add it here as a note.