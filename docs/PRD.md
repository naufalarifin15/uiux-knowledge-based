# PRD — [Project Name]

*Refilled each time this is used in a new project, so Claude Code understands the business context behind the UI being requested.*

---

## 1. Summary

| | |
|---|---|
| **Product name** | ... |
| **Problem being solved** | ... |
| **Target users** | ... |

---

## 2. User Roles

| Role | Description | Main Access |
|---|---|---|
| ... | ... | ... |

---

## 3. Sitemap

**Page list**

| Page | Route | Layout | Role |
|---|---|---|---|
| Login | `/login` | AuthLayout | All |
| Dashboard | `/dashboard` | DefaultLayout | All |
| ... | ... | ... | ... |

**Navigation (sidenav/navbar)**
```
Dashboard        → /dashboard
Menu A           → /menu-a
  Sub-menu A.1   → /menu-a/sub-1
Menu B           → /menu-b
```

**Key user flows**
```
1. Login → Dashboard
2. Dashboard → [action] → Page X
3. Page X → submit → Page Y (+ confirmation toast)
```

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

## 5. Non-Functional Requirements
| Aspect | Example Content |
|---|---|
| **Responsive** | Follows the default breakpoints of `@siloamhospitals/ui-vue`. Tables on list pages automatically switch to cards on mobile. |
| **Accessibility** | All interactive elements (icon-only buttons, etc.) must have an `aria-label`. Text color contrast must meet at least WCAG AA. |
| **Performance** | Lists/tables with more than 50 rows must use pagination or infinite scroll, not render everything at once. |
| **Language/Localization** | Indonesian as the default language. Date format `DD/MM/YYYY`. |
| **Offline/Loading state** | Every data fetch must have a skeleton/loading state, not a blank screen. |
| **Error handling** | Every form must show inline error messages below the field, not just a generic alert/toast. |

---

## 6. Additional Notes
Domain terms, abbreviations, or other project-specific details Claude Code needs to know.