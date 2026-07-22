# Image

## Function & When to Use
Image displays an image/placeholder area with a preset ratio (following the Figma design spec), used to ensure the image (or placeholder before the image loads) is always proportional according to the design standard, rather than a free-form ratio determined manually per implementation.

## Props Structure

| Prop | Type | Default | Description |
|---|---|---|---|
| `aspectRatio` | See preset table below | `'1:1'` | Placeholder ratio, following the Figma design spec |
| `orientation` | `'Landscape'` \| `'Portrait'` | `'Landscape'` | Ratio orientation — flips the ratio without needing to manually swap the numbers |
| `className` | `string` | `''` | Additional custom styling |

**Full `aspectRatio` preset list**
| Ratio | Category |
|---|---|
| `'1:1'` | Square |
| `'5:4'`, `'4:5'` | Near-square |
| `'4:3'`, `'3:4'` | Classic standard photo |
| `'7:5'`, `'5:7'` | Print photo |
| `'3:2'`, `'2:3'` | Standard DSLR photo |
| `'16:10'`, `'10:16'` | Screen/monitor |
| `'5:3'`, `'3:5'` | Medium wide |
| `'16:9'`, `'9:16'` | Video/widescreen (including vertical format for mobile/reels) |
| `'2:1'`, `'1:2'` | Panorama |
| `'21:9'`, `'9:21'` | Ultra-wide/cinematic |
| `'Golden'` | Golden ratio (~1.618:1) |

> Naming pattern: paired ratios (e.g. `'16:9'` and `'9:16'`) represent landscape vs. portrait of the same ratio — but **use the `orientation` prop to flip it**, rather than manually picking the inverse preset, to stay consistent with how this component was designed.

**Slot**
| Slot | Description |
|---|---|
| `default` | Content rendered inside the placeholder (e.g. the actual `<img>` once the image has loaded) |

## ✅ Do
- Choose `aspectRatio` from the preset table above based on the design spec in Figma — every ratio used by designers should already be covered by this preset.
- Use `orientation="Portrait"` to flip a landscape ratio into portrait (e.g. `'4:3'` + `orientation="Portrait"` to get the effect of `3:4`), rather than picking the `'3:4'` preset separately when both can be achieved via the same ratio + orientation combination.
- Use `'16:9'` for landscape video/banners, `'9:16'` for vertical content (e.g. story/reels-style), `'1:1'` for profile photos/square thumbnails, `'Golden'` for compositions that need a special aesthetic proportion.
- Use the `default` slot to render the actual `<img>` once the image data is available, so the placeholder automatically becomes a container with a consistent ratio.

## ❌ Don't
- Don't hardcode `width`/`height` via `className` to force a certain ratio — all common ratios are already covered by the preset, so use that instead.
- Don't guess an `aspectRatio` value outside the 20 available presets (e.g. `'18:9'`, which isn't in the list) — only values from the preset table above are valid.
- Don't pick 2 paired presets (e.g. `'16:9'` and `'9:16'`) for a case that could actually be achieved with just 1 preset + `orientation` — pick a consistent approach (base ratio + orientation) across the whole application.

## Additional Context
- The `default` slot is typed as `other` (flexible/generic) — make sure the content rendered inside it (usually `<img>` or another image component) follows the container dimensions already established by `aspectRatio`, rather than overriding with its own size that could break the proportions.