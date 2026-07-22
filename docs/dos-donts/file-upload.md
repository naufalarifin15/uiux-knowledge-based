# File Upload

## Function & When to Use
File Upload is a **compact** file upload trigger — a "Choose File" button + filename label, with no drag-and-drop area or progress bar. Used for simple upload needs (usually 1 file) within a form, without needing visuals as large as Dropzone.

**Difference from Dropzone:**
| | File Upload | Dropzone |
|---|---|---|
| Interaction | Click button only | Drag-and-drop + click to browse |
| Default `multiple` | `false` (1 file) | `true` (many files) |
| Upload progress | None | Yes (`uploadProgress`) |
| Rejected file feedback | None (see note below) | Yes (`rejected` in the `filesChange` event) |
| Visual size | Small, inline | Large, separate area |

Use File Upload for simple cases (1 document within a long form); use Dropzone for uploads that are the page's main focus or that need many files at once with progress tracking.

## Props Structure

| Prop | Type | Default | Description |
|---|---|---|---|
| `state` | `'default'` \| `'disabled'` \| `'error'` \| `'focus'` | `'default'` | Visual state, same pattern as other form components |
| `placeholder` | `string` | `'No file chosen'` | Text shown before a file is chosen |
| `accept` | `Record<string, string[]>` | `{'*': []}` (accepts all types) | Accepted MIME types and extensions |
| `multiple` | `boolean` | `false` | Whether more than 1 file can be selected |
| `maxFiles` | `number` | `1` | Maximum number of files |
| `className` | `string` | `''` | Additional CSS class |

> There's no `maxFileSize` or `uploadProgress` prop on this component (unlike Dropzone) — file size validation and upload progress tracking need to be handled manually at the application level if needed.

## Events
| Event | Payload | When It Fires |
|---|---|---|
| `fileChange` | `File[]` | When a file is selected |

> The payload is just `File[]` with no `accepted`/`rejected` split (unlike Dropzone) — it's unclear whether `accept` actually filters out non-matching files or merely acts as a filter in the OS's file selection dialog. Manual validation on the application side (checking file type/size from the `fileChange` result) is needed to ensure the accepted file is actually valid.

## ✅ Do
- Use it for simple, single-file upload cases within a form that already has many other fields — so you don't need large visual space like Dropzone.
- Set `accept` explicitly based on the need (the default accepts all file types, which may be too permissive for most use cases).
- Set `state="error"` when file validation fails (e.g. wrong type, required but empty), and show a separate error message since this component doesn't attach a built-in error message.
- Perform additional validation (file size, actual MIME type) manually in the `fileChange` handler, since the component doesn't provide rejected-file feedback or a built-in size limit.

## ❌ Don't
- Don't use File Upload for use cases needing multiple files with progress tracking — use Dropzone instead, which already has `uploadProgress`.
- Don't assume a file that passes through to `fileChange` is automatically valid according to `accept` — still validate manually, especially for file size, which this component doesn't limit at all.
- Don't use this component as the page's main upload area (e.g. a dedicated document-upload page) — its visuals are too minimal to be a focal point; use Dropzone for that.

## Additional Context
- Since there's no built-in file size limit, make sure there's size validation at the application/backend level to prevent overly large file uploads.