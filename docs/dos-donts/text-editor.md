# Text Editor

## Function & When to Use
Text Editor is a rich text editor with a formatting toolbar (bold, italic, list, heading, etc.), producing **HTML** as output — not plain text. Used for content that needs formatting (e.g. structured medical notes, richly formatted descriptions), not for simple text fields (use `Input`/`Textarea` for that).

## Props Structure

| Prop | Type | Default | Description |
|---|---|---|---|
| `modelValue` | `string` | `''` | Content in **HTML** format, used with `v-model` |
| `placeholder` | `string` | `'Start typing...'` | Placeholder text |
| `disabled` | `boolean` | `false` | **Read-only** mode — content still displays, but can't be edited |
| `minHeight` | `string` | `'200px'` | Minimum editor height, **a full CSS value with a unit** (not a plain number) |
| `showToolbar` | `boolean` | `true` | Shows/hides the formatting toolbar |

## Events
| Event | Payload | When It Fires |
|---|---|---|
| `update:modelValue` | `string` (HTML) | For `v-model` binding |
| `change` | `string` (HTML) | Fires when the content changes |
| `focus` | — | The editor gains focus |
| `blur` | — | The editor loses focus |

## ✅ Do
- **Always sanitize the HTML from `modelValue`** before re-rendering it elsewhere (e.g. displaying it to other users via `v-html`) or storing it directly to the database without validation — since this is rich text/HTML, it can potentially become an XSS vector if not handled properly, especially for content that other users may view (e.g. notes shared between staff).
- Set `minHeight` with a full CSS unit (e.g. `'150px'`, `'10rem'`), not a plain number (`'150'` without a unit isn't valid).
- Turn off `showToolbar={false}` for simple display contexts (e.g. a brief preview/read-only view) or when complex formatting isn't needed.
- Use `disabled={true}` for read-only mode when displaying content that's already finalized/shouldn't be edited anymore (e.g. a note that's already been submitted/locked).
- Use `focus`/`blur` for additional logic like auto-saving a draft when the editor loses focus.

## ❌ Don't
- Don't use Text Editor for simple fields that plain text would suffice for (e.g. name, a short address) — the toolbar overhead and HTML output aren't needed for that case; use `Input`/`Textarea` instead.
- Don't store/display raw `modelValue` without sanitization if there's a possibility of malicious content being injected (especially if the input source could come from a not-fully-trusted user).
- Don't assume `modelValue` is plain text when you need to count characters/words — the HTML tags need to be stripped first to get an accurate text count.
- Don't forget the CSS unit on `minHeight` — a unitless value may not be applied correctly by the browser.

## Additional Context
- Since the output is HTML, make sure the rendered result's styling (wherever `modelValue` is re-displayed, e.g. a detail/print page) stays consistent with the original styling in the editor — check whether additional CSS is needed outside of Text Editor to re-render that HTML with the same appearance.