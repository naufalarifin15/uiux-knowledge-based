# Textarea

## Function & When to Use
Textarea is for multi-line text input (plain text, not HTML like Text Editor). Used for notes/descriptions longer than 1 line that don't need rich formatting (e.g. patient complaints, short notes) — if formatting is needed (bold, lists, etc.), use Text Editor instead of Textarea.

## Props Structure

| Prop | Type | Default | Description |
|---|---|---|---|
| `modelValue` | `string` | — | Current value, used with `v-model` |
| `label` | `string` | — | Label above the textarea |
| `placeholder` | `string` | — | Placeholder text |
| `error` | `boolean` | `false` | Shows error styling |
| `errorMessage` | `string` | — | Error message displayed **below the field** — different from most other form components, which don't have a built-in error message slot |
| `disabled` | `boolean` | `false` | Disables interaction |
| `resize` | `'none'` \| `'both'` \| `'horizontal'` \| `'vertical'` | `'vertical'` | Resize behavior (CSS `resize` property) |
| `rows` | `number` | `4` | Number of visible lines initially |
| `maxLength` | `number` | — | Character count limit |
| `autoFocus` | `boolean` | — | Auto-focuses when the component mounts |

## Events
| Event | Payload | When It Fires |
|---|---|---|
| `update:modelValue` | `string` | For `v-model` binding |
| `input` | `Event` | Every keystroke — the payload is a native Event, useful when extra detail is needed (e.g. cursor position) |
| `focus` | `FocusEvent` | The field gains focus |
| `blur` | `FocusEvent` | The field loses focus |

## ✅ Do
- Use `errorMessage` (not just the `error` boolean) to always include a clear error message — this component **already has a built-in slot** for that, so there's no need to manually build a separate error message element like in some other components.
- Set `resize="none"` when the textarea sits in a tight/fixed layout (e.g. inside a small card) so the user can't resize it in a way that breaks the layout; leave the default `'vertical'` for most general cases.
- Set `maxLength` for fields with a clear business limit (e.g. a short note capped at 500 characters) — and consider manually showing a remaining-character counter in the UI when `maxLength` is set, since the component doesn't show an automatic counter.
- Match `rows` to the expected content length (e.g. `rows={2}` for a short note, `rows={6}` for a long description) — don't always use the default `4` without considering the context.
- Use `autoFocus` carefully, only for pages/modals genuinely dedicated to this field as the main focus (e.g. an "Add Note" modal with just 1 main field) — don't use it carelessly in a form with many fields, as it can disrupt the user's navigation flow (especially for screen reader users).

## ❌ Don't
- Don't use Textarea for content that needs formatting (bold, lists, headings) — use Text Editor for that instead, Textarea is purely plain text.
- Don't set `error={true}` without `errorMessage` — the component already provides a place for the error message, so take advantage of it to let the user know what's wrong, rather than just red styling with no explanation.
- Don't set `maxLength` without giving the user a visual indication of the remaining character count — the user could type a long entry and be caught off guard when it gets cut off without warning.
- Don't use `autoFocus` on more than 1 element within the same page — only 1 element should be auto-focused per page/modal.

## Additional Context
- The `input` and `update:modelValue` events both fire on every keystroke — use `update:modelValue` for regular data binding (`v-model`), and `input` only when you need access to the native Event (e.g. for more advanced cursor/text-selection logic).