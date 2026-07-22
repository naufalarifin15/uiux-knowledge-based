# Alert

## Function & When to Use
Alert displays contextual, **persistent/static** messages — attached to the layout (e.g. above a form, within a page section) and doesn't disappear automatically. Used to convey status, warnings, or information that needs to stay visible until the user consciously dismisses it (if `iconRshow` is enabled) or the underlying condition changes.

**Don't confuse it with Toast** — Toast is temporary (appears then disappears automatically, usually floating in a corner of the screen), while Alert stays permanently within the layout. If the need is a brief notification (e.g. "successfully saved"), Toast is the right choice, not Alert.

## Variant Guide
Alert has 3 independent dimensions: **Semantic variant** (color/function), **Tone** (visual), and **Composition** (which elements are displayed).

**Dimension 1 — Semantic Variant (function/meaning)**
| Value | Function | When to Use |
|---|---|---|
| `info` | Neutral information | Informing about something with no good/bad implication |
| `success` | Positive confirmation | An operation completed successfully |
| `warning` | Warning | User needs to be cautious before proceeding, but there's no error yet |
| `error` | Failure/error | Something failed or is invalid, needs the user's attention/action |
| `default` | Neutral, no semantic color | General messages that don't fit info/success/warning/error |

**Dimension 2 — Tone (visual only, doesn't affect meaning)**
| Value | Visual | When to Use |
|---|---|---|
| `default` | Solid/filled color, high contrast | Important messages that must grab attention immediately |
| `soft` | Soft/pastel background color, colored text | Messages that still need to be visible but shouldn't be too dominant/distracting from other surrounding content |

**Dimension 3 — Composition (elements displayed)**
| Element | Default | Can Be Turned Off? |
|---|---|---|
| Left icon (`iconL`) | Shown | Yes — can be hidden |
| Description | Shown | Yes — can be hidden |
| Title (`titleShow`) | Hidden | Can be enabled to give a short label before the description |
| Right icon (`iconRshow`) | Hidden | Can be enabled, typically for actions like dismiss/close |

## ✅ Do
- Choose the semantic variant based on **the meaning of the message**, not based on a color that "looks right" aesthetically — `error` should always be used for failures, not a manually red-styled `warning`.
- Use the `soft` tone when the alert appears in a visually dense context (e.g. inside a form, among many other elements) so it doesn't dominate too much.
- Use the `default` (solid) tone for alerts that are blocking/important and need immediate user attention, e.g. at the top of a page.
- Enable `titleShow` when the message is long enough or needs to be split into a summary (title) + detail (description) — helps users scan the alert quickly.
- Enable `iconRshow` only when there's an actual related action (e.g. dismiss) — don't show the right icon without a function, as it will look clickable when it isn't.

## ❌ Don't
- Don't use the `default` variant for a message that actually has a clear semantic meaning (e.g. error) just because the color is considered visually more "neutral" — this removes an important signal for the user.
- Don't mix `default` and `soft` tones within the same group of similar alerts (e.g. a notification list) — it will look inconsistent.
- Don't enable `titleShow` for a short one-line message — the title becomes redundant and adds height to the alert with no benefit.
- Don't use the `soft` tone for a critical/blocking `error` alert — low contrast can make the user unaware there's a serious error.

## Additional Context
- Composition (title/iconR) applies the same way across all variant × tone combinations — don't assume the title is only available for certain tones.
- If the alert is used as a notification the user can dismiss, make sure `iconRshow` is enabled as the dismiss trigger, rather than adding a separate close button outside the component.
- Since `iconL` and the description can both be turned off, make sure there's at least **a title or a description shown** — don't let the alert end up with no text content at all (e.g. iconL off, titleShow not enabled, description empty).