# Phone Input

## Function & When to Use
Phone Input is for entering a phone number with a separate country code dropdown (e.g. `ID +62`). Used for all phone number fields that need to support multiple countries — not a regular `Input` with `type="tel"`.

> **Important:** `modelValue` only contains the **phone number without the country code** (e.g. `"8123xxxxxxx"`). The country code is stored separately via the `countryCode` prop (e.g. `"+62"` or `"ID"`, check the actual format in the types). To get the full number (E.164), combine `countryCode` + `modelValue` manually.

## Props Structure

| Prop | Type | Default | Description |
|---|---|---|---|
| `modelValue` | `string` | — | Phone number (without country code), used with `v-model` |
| `defaultValue` | `string` | — | Initial value (uncontrolled) |
| `placeholder` | `string` | `'8123xxxxxxx'` | Placeholder text |
| `countryCode` | `string` | — | Selected country code (controlled) |
| `defaultCountryCode` | `string` | — | Initial country code (uncontrolled) |
| `disabled` | `boolean` | `false` | Disables the input |
| `error` | `boolean` | `false` | Shows error styling |
| `state` | `'Default'` \| `'Disabled'` \| `'Error'` \| `'Focus'` | `'Default'` | Visual state — keep in sync with the `disabled`/`error` booleans |
| `name` | `string` | — | Field name for the form |
| `className` | `string` | — | Additional CSS class |

## Events
| Event | Payload | When It Fires |
|---|---|---|
| `update:modelValue` | `string` | Phone number changes, used for `v-model` |
| `change` | `string` | When the phone number input changes |
| `country-code-change` | `string` | When the country code is changed — used for `v-model:country-code` when controlled behavior is needed |

## ✅ Do
- Store `modelValue` (the number) and `countryCode` (the country code) as **2 separate states** in the form data, matching how the component splits them — don't assume either one already covers both.
- Combine `countryCode` + `modelValue` into a full format (e.g. E.164: `+628123xxxxxxx`) **when submitting to the backend**, rather than storing them separately in the database if the system needs a single, complete phone number field.
- Use `v-model:country-code` (listen for `country-code-change`) if the default country needs to be set automatically based on other data (e.g. the patient's residence), rather than relying only on a static default.
- Set `state="Error"` together with `error={true}` for failed number format validation, with a separate error message outside the component.

## ❌ Don't
- Don't assume `modelValue` already includes the country code — sending `modelValue` alone to the backend without `countryCode` will produce incomplete/ambiguous phone number data.
- Don't hardcode a `defaultCountryCode` that doesn't match the application's context (e.g. always `+1` for an application whose users are mostly in Indonesia) — match the default to the primary target users.
- Don't use a regular `Input` for international phone numbers — Phone Input already handles the country-code complexity, which isn't easy to replicate manually.

## Additional Context
- Since `modelValue` and `countryCode` are 2 separate props, phone number format validation (e.g. digit length matching the country) should ideally also take `countryCode` into account, rather than only applying generic length validation to `modelValue` alone.