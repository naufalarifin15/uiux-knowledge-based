# Header

## Function & When to Use
Header is the application's top-level topbar — displaying the logo (based on the product), a timestamp, dropdown triggers for hospital/doctor/language, and notification/help icons. Used once per application as part of the main layout (e.g. inside `DefaultLayout`), not a component repeated in many places.

> This Header is purely **display + event trigger** — it has no internal state/option list for the dropdowns (e.g. a list of selectable hospitals/doctors). When `hospitalClick`/`doctorClick`/`languageClick` is emitted, the implementation outside the component is responsible for showing the actual selection dropdown/modal and updating the related prop (`hospitalName`, `doctorName`, `language`) after the user makes a selection.

## Props Structure

| Prop | Type | Default | Description |
|---|---|---|---|
| `product` | `'Siloam'` \| `'CDMS'` \| `'EMR'` | `'Siloam'` | Determines which logo is displayed |
| `timestamp` | `string` | current date/time string | Timestamp text in the badge — **a static string, not an automatic live clock** |
| `timestampShow` | `boolean` | `true` | Show/hide the timestamp badge |
| `hospitalName` | `string` | `'Siloam Hospitals Semanggi'` | Hospital name shown on the dropdown button |
| `hospitalShow` | `boolean` | `true` | Show/hide the hospital dropdown button |
| `doctorName` | `string` | default doctor name | Doctor name shown on the dropdown button |
| `doctorShow` | `boolean` | `true` | Show/hide the doctor dropdown button |
| `language` | `string` | `'EN'` | Language code shown on the dropdown |
| `notificationCount` | `number` | `0` | Number of unread notifications |
| `showNotificationBadge` | `boolean` | `false` | Show/hide the notification count badge |

**Slot**
| Slot | Description |
|---|---|
| `logo` | Overrides the default logo — if not filled in, the logo is determined automatically from the `product` prop |

## Events
| Event | When It Fires |
|---|---|
| `hospitalClick` | The hospital dropdown button is clicked |
| `doctorClick` | The doctor dropdown button is clicked |
| `languageClick` | The language dropdown button is clicked |
| `notificationClick` | The notification icon is clicked |
| `helpClick` | The help icon is clicked |

## ✅ Do
- Choose `product` based on the application being built (`'EMR'` for an EMR system, etc.) — this determines the correct logo without needing a manual override.
- Use the `logo` slot **only** for white-label/custom logo cases not covered by the 3 existing `product` presets — for general cases, just rely on the `product` prop.
- If a live-updating timestamp (a running clock) is needed, build your own interval/timer at the application level that periodically updates the `timestamp` prop — this component receives a static string and doesn't auto-tick on its own.
- Listen for `hospitalClick`/`doctorClick`/`languageClick` to open a selection dropdown/modal implemented separately (Header itself doesn't provide the option list), then update the related prop (`hospitalName`, etc.) after the user makes a selection.
- Show `showNotificationBadge` based on the condition `notificationCount > 0` (computed), not hardcoded to `true` — so the badge doesn't appear showing an uninformative `0`.
- Hide elements that aren't relevant for a given role/context via the `*Show` props (e.g. `doctorShow={false}` for an Admin role not associated with a specific doctor).

## ❌ Don't
- Don't assume Header has a built-in dropdown menu for hospital/doctor/language — the emitted events are only triggers; the dropdown implementation (option list, search, etc.) must be built separately using other components (e.g. Select or a custom dropdown).
- Don't leave `timestamp` static without updates if the expected UX is a real-time clock — this string doesn't change on its own without an external interval.
- Don't set `showNotificationBadge={true}` without considering `notificationCount` — combine the two logically.
- Don't render more than 1 Header on the same page — this is an application-level component, not one meant to be repeated.

## Additional Context
- Since `hospitalName`/`doctorName` are purely display strings (not objects with an id), make sure there's separate application-level state storing the full id/data of the selected hospital/doctor (not just the name) if that data is needed for other logic (e.g. filtering data based on the active hospital).