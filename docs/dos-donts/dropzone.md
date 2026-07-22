# Dropzone

## Function & When to Use
Dropzone provides a drag-and-drop area (or click to browse) for file uploads, with file type/size validation and upload progress tracking. Used in forms that need document/image uploads (e.g. uploading lab results, patient photos, document attachments).

## Props Structure

| Prop | Type | Default | Description |
|---|---|---|---|
| `accept` | `Record<string, string[]>` | `{'image/*': ['.png','.jpg','.jpeg','.gif']}` | Accepted MIME types and extensions |
| `multiple` | `boolean` | `true` | Whether more than 1 file can be selected at once |
| `maxFiles` | `number` | `10` | Maximum number of files |
| `maxFileSize` | `number` | — (no default/unbounded) | Maximum size per file in bytes |
| `uploadProgress` | `Record<string, number>` | `{}` | Upload progress per file (key = filename, value 0-100) |
| `state` | `'default'` \| `'drop-hover'` | `'default'` | Visual state — **`drop-hover` is normally controlled automatically by the component when a file is dragged over it**, not set manually by the developer |

## Events
| Event | Payload | When It Fires |
|---|---|---|
| `filesChange` | `{ accepted: File[], rejected: DropzoneRejectedFile[] }` | When a file is dropped or selected via browse |
| `fileRemove` | `File` | When the user removes a file from the list |

## ✅ Do
- **Always explicitly set `accept`** based on the page's needs — don't rely on the default (`image/*`) if the use case is for documents (PDF, etc.).
- **Always explicitly set `maxFileSize`** — since there's no default (unbounded), leaving it empty means users can upload files of any size, which is risky for performance/storage costs.
- **Always handle `rejected` from the `filesChange` event** — show a clear error message to the user explaining why the file was rejected (wrong type, too large, etc.); don't just process `accepted` and silently ignore `rejected`.
- Use `uploadProgress` to show a progress bar per file while an upload is in progress (e.g. integrating with an XHR/fetch progress event).
- Set `multiple={false}` when the use case genuinely only needs 1 file (e.g. uploading a single profile photo) — reduces user confusion and simplifies validation.

## ❌ Don't
- Don't manually set `state="drop-hover"` outside of an actual drag interaction — this state represents a temporary visual condition during a drag, not a permanent status controlled externally.
- Don't ignore `rejected` files — a user whose file was rejected without a clear message will be confused about why the upload isn't working.
- Don't set `maxFiles` higher than actually needed "just in case" — align it with a clear business rule (e.g. a maximum of 5 attachments per submission).
- Don't forget to clear/reset `uploadProgress` after an upload finishes or fails, so old progress doesn't linger in the UI for a new file.

## Additional Context
- `uploadProgress` is keyed by `filename` — if there are 2 files with the same name in one batch, make sure there's special handling (e.g. automatic renaming) so progress tracking doesn't get mixed up between files.