# Form Layout — Responsive Grid Rules

## Function & When to Use
Defines how many form fields are allowed per row at each breakpoint. Applies to any form or filter layout containing 2+ fields. Referenced by all form-related components — `input.md`, `password-input.md`, `number-input.md`, `phone-input.md`, `select.md`, `combobox.md`, `date-picker.md`, `time-picker.md`, `text-area.md`, `file-upload.md`, `button.md` — instead of each one defining its own grid rule.

> Breakpoints: see `_breakpoints.md`

## Field Categories

Rather than listing every component individually, fields fall into one of these behavioral categories. When a new form component is added, match it to the closest category below instead of adding a new row.

| Category | Includes | Behavior summary |
|---|---|---|
| **Standard field** | Input, Password, Number, Select, Combobox, Date Picker, Time Picker | Single value, single control. Default grid behavior. |
| **Compact field** | Select/Combobox with short options (e.g. Ward, Status, Category — 1-2 word values) | Same as Standard, but narrow enough to pair with another compact field on mobile. |
| **Composite field** | Phone Input (country code + number), Date Range, Time Range | Internally made of 2+ sub-controls. Always treated as ONE grid unit — never split across the grid. |
| **Full-row field** | Text Area, File Upload | Always spans the full row width at every breakpoint, regardless of how much horizontal space is available. |
| **Action element** | Button (primary/submit, e.g. Search) | Not a data field — follows its own placement rule, see `button.md`. |

## Max Fields Per Row

| Category | Desktop | Tablet | Mobile |
|---|---|---|---|
| Standard field | 3–4 per row | 2 per row | 1 per row (full-width) |
| Compact field | 4+ per row | 2 per row | 2 per row max, only if each retains min-width 140px |
| Composite field | 1 per row (sub-controls inline) | 1 per row (sub-controls inline) | 1 per row; sub-controls stack vertically if combined width < 280px |
| Full-row field | Always full-width, own row | Always full-width, own row | Always full-width, own row |
| Action element | Inline with fields, right-aligned | Full-width, own row below fields | Full-width, own row, placed after all fields |

## Rule of Thumb
- **Desktop:** fit Standard/Compact fields by container width, no fixed count — never let a field's rendered width fall below its category's min-width. Full-row fields (Text Area, File Upload) still take their own row even on desktop.
- **Tablet:** default to 2 Standard fields per row unless both are Compact.
- **Mobile:** default to 1 field per row for Standard fields. Exception: 2 Compact fields may sit side-by-side if each retains at least 140px width. Composite and Full-row fields never share a row with anything else, at any breakpoint.

## ✅ Do
- Do default to 1 Standard field per row on mobile — prevents label/value truncation.
- Do allow 2 Compact fields per row on mobile only when both qualify as short-option fields (e.g. Ward / Room, not Ward / Patient Name).
- Do treat Composite fields (Phone Input, Date Range, Time Range) as one grid unit that reflows internally (inline → stacked) rather than splitting sub-controls into separate grid fields.
- Do keep Full-row fields (Text Area, File Upload) at full width on every breakpoint, including desktop, unless the form explicitly places them in a 2-column layout by design.
- Do place the primary action button as its own full-width row, after all fields, on mobile.
- Do reduce progressively: 3–4 fields/row (desktop) → 2 (tablet) → 1 (mobile) for Standard fields — don't skip the tablet step.

## ❌ Don't
- Don't put more than 2 fields per row on mobile under any circumstance, even for Compact fields.
- Don't mix a Compact field and a Standard/long field (e.g. Ward dropdown + Patient Name input) in the same mobile row.
- Don't split a Composite field's sub-controls (e.g. phone country code + number, or date/time range) into 2 independent grid fields — they must move and wrap together.
- Don't shrink a Full-row field (Text Area, File Upload) to fit alongside another field just to save vertical space.
- Don't keep the action button inline with the last field on mobile — give it a dedicated full-width row.

## Additional Context
This rule set governs layout/grid placement only. For behavior of each field type itself (label position, width handling, tap targets, internal validation states), refer to that component's own Responsive Behavior section in its individual doc file.