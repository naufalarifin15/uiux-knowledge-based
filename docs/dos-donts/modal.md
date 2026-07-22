# Modal

## Function & When to Use
Modal displays an overlay dialog that blocks interaction with the content behind it — used for important action confirmations, short forms that need full focus, or details that don't need a separate page.

## Props Structure

| Prop | Type | Default | Description |
|---|---|---|---|
| `open` | `boolean` | `false` | Modal visibility (controlled), used with **`v-model:open`** |
| `title` | `string` | `'Title is lorem ipsum'` | Title in the modal header |
| `showCloseIcon` | `boolean` | `true` | Shows the close (×) button in the header |
| `showFooter` | `boolean` | `true` | Shows/hides the entire footer area |
| `primaryButtonText` | `string` | `'Ya, lanjutkan'` | Label for the built-in primary button |
| `secondaryButtonText` | `string` | `'Cek kembali'` | Label for the built-in secondary button |
| `size` | `'sm'` \| `'md'` \| `'lg'` | `'md'` | Modal size preset |
| `width` | `string` | — | Custom width (e.g. `'500px'`, `'80vw'`) — **overrides `size` for width when filled in** |
| `minHeight` | `string` | — | Custom min-height (e.g. `'400px'`, `'50vh'`) — **overrides `size` for min-height when filled in** |
| `primaryButtonDisabled` | `boolean` | `false` | Disables the built-in primary button |

**Slots**
| Slot | Description |
|---|---|
| `default` | Modal body content |
| `footer` | Custom footer — **when filled in, COMPLETELY REPLACES the built-in primary/secondary buttons**, used for custom button variants or complex conditional logic |

## Events
| Event | Payload | When It Fires |
|---|---|---|
| `update:open` | `boolean` | For `v-model:open` binding |
| `primaryClick` | — | Built-in primary button is clicked |
| `secondaryClick` | — | Built-in secondary button is clicked |

## ✅ Do
- Use `v-model:open` (not plain `v-model`) — the prop is named `open`, not `modelValue`.
- Use the `footer` slot **only** when you need more than the 2 built-in buttons, a different button variant, or complex conditional logic — for standard confirmation cases (2 buttons), just rely on the built-in `primaryButtonText`/`secondaryButtonText` without needing the `footer` slot.
- Combine `size` (preset) with custom `width`/`minHeight` only when the existing presets aren't enough — e.g. `size="lg"` as a base and then override `minHeight` for content that needs special height.
- Set `primaryButtonDisabled={true}` when the condition hasn't been met to proceed (e.g. a form inside the modal isn't valid yet), rather than leaving the button active but showing an error after it's clicked.
- Set `showCloseIcon={false}` for modals that genuinely must be answered via one of the action buttons (e.g. an important confirmation that shouldn't be casually dismissed) — don't let the user close the modal without picking a clear action if that's actually required.

## ❌ Don't
- Don't fill in `primaryButtonText`/`secondaryButtonText` and expect both to still appear if the `footer` slot is also filled in — the `footer` slot **completely replaces** the built-in buttons, making those props have no effect.
- Don't listen for `primaryClick`/`secondaryClick` if you're already using a custom `footer` slot — those events are only for the built-in buttons, which are no longer rendered once the `footer` slot is used; build your own handler inside the `footer` slot's content instead.
- Don't set `showFooter={false}` while still filling in the `footer` slot — the footer will most likely still not appear, since `showFooter` controls the visibility of the entire footer area regardless of its content (verify this against the actual behavior, but don't mix these two approaches together).
- Don't use Modal for content that's persistent/needs to stay open for a long time while the user keeps interacting with other parts of the page — Modal blocks background interaction, which isn't suitable for that.

## Additional Context
- Since `width`/`minHeight` can override `size`, if you customize either one, consider consistency with other modals in the application that still use the `size` preset — so there aren't modals with wildly different proportions for no clear reason.