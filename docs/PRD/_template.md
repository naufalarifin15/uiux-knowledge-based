# PRD — [Module Name]

> Status: 📝 Draft | 🚧 In Progress | ✅ Complete | 🔄 Needs Update
> Last Updated: YYYY-MM-DD
>
> *Refilled each time this module is documented, so Claude Code understands the business context behind the UI being requested. Global info (product summary, all user roles, full sitemap) lives in `README.md` — this file covers only what's specific to this module.*

---

## 1. Summary

| | |
|---|---|
| **Module name** | ... |
| **Problem being solved** | ... |
| **Target users (roles involved)** | ... |

---

## 2. User Roles Involved

<!-- Only roles relevant to this module. Full role list/definitions live in README.md — reference them here, only add detail if this module grants role-specific access not covered globally -->

| Role | Access Within This Module |
|---|---|
| ... | ... |

---

## 3. Pages in This Module

**Page list**

| Page | Route | Layout | Role |
|---|---|---|---|
| ... | ... | ... | ... |

**Key user flows (within this module)**
```
1. Entry point → [action] → Page X
2. Page X → submit → Page Y (+ confirmation toast)
```

> Full app-wide sitemap and cross-module navigation live in `README.md`.

---

## 4. Page Content Details

Top-to-bottom breakdown of each page's content — so Claude Code knows which sections must exist, not just the page name.

### [Page Name] — `/route`
| Section | Content/Component | Notes / Business Rules |
|---|---|---|
| Header | Page title + "Add New" button | Button only appears for certain roles |
| Filter bar | Search input, status dropdown, date range | Filter applies automatically (no submit button) |
| Main content | Table with columns: Name, Status, Date, Action | Clicking a row → goes to detail page |
| Footer | Pagination | 10 items per page |

> Duplicate the table above for each page that needs a breakdown (usually main/complex pages; simple pages like short forms can be skipped).

---

## 5. Business Rules

<!-- Rules SPECIFIC to this module, not already captured inline in the Page Content Details table above. Global cross-module rules live in README.md -->

- [Rule 1]
- [Rule 2]

---

## 6. Data Requirements

<!-- Fields/data this module needs. Serves as the reference for building the TypeScript interface (src/types/) and mock data (src/mocks/) -->

| Field | Type | Required | Notes |
|-------|------|----------|-------|
| [field_name] | string / number / etc. | Yes/No | [additional notes] |

---

## 7. Non-Functional Requirements

<!-- Only include rows that differ from or add to the global defaults in README.md -->

| Aspect | Example Content |
|---|---|
| **Responsive** | Follows the default breakpoints of `@siloamhospitals/ui-vue`. Tables on list pages automatically switch to cards on mobile. |
| **Accessibility** | All interactive elements (icon-only buttons, etc.) must have an `aria-label`. Text color contrast must meet at least WCAG AA. |
| **Performance** | Lists/tables with more than 50 rows must use pagination or infinite scroll, not render everything at once. |
| **Language/Localization** | Indonesian as the default language. Date format `DD/MM/YYYY`. |
| **Offline/Loading state** | Every data fetch must have a skeleton/loading state, not a blank screen. |
| **Error handling** | Every form must show inline error messages below the field, not just a generic alert/toast. |

---

## 8. Edge Cases / Error Handling

<!-- Special conditions beyond the table above: empty state, permission denied, network failure, etc. -->

- [Edge case 1]: [expected behavior]
- [Edge case 2]: [expected behavior]

---

## 9. Open Questions

<!-- Things still unclear/needing stakeholder confirmation, so Claude Code doesn't assume on its own -->

- [ ] [Question 1]
- [ ] [Question 2]

---

## 10. Related Components

<!-- Reference docs/dos-donts/ for UI components relevant to this module -->

- [component-name.md](../dos-donts/component-name.md)

---

## 11. Additional Notes

Domain terms, abbreviations, or other module-specific details Claude Code needs to know.