# Do's & Don'ts — Index

Usage documentation for each component in `@siloamhospitals/ui-vue` — supplementing the package's types/props with context that isn't reflected there, especially **when to use a given variant** (size, color/function, etc.) and anti-patterns to avoid.

| Component | File | Status |
|---|---|---|
| Accordion | [accordion.md](accordion.md) | ✅ |
| Alert | [alert.md](alert.md) | ✅ |
| Avatar | [avatar.md](avatar.md) | ✅ |
| Badge | [badge.md](badge.md) | ✅ |
| Breadcrumb | [breadcrumb.md](breadcrumb.md) | ✅ |
| Button | [button.md](button.md) | ✅ |
| Button Icon | [button-icon.md](icon-button.md) | ✅ |
| Card | [card.md](card.md) | ✅ |
| Chart | [chart.md](chart.md) | ✅ |
| Checkbox | [checkbox.md](checkbox.md) | ✅ |
| Chip | [chip.md](chip.md) | ✅ |
| Date Picker (Date Picker, Date Range Picker, Date Time Picker, Date Time Range Picker) | [date-picker.md](date-picker.md) | ✅ |
| Divider | [divider.md](divider.md) | ✅ |
| Drawer | [drawer.md](drawer.md) | ✅ |
| Dropzone | [dropzone.md](dropzone.md) | ✅ |
| File Upload | [file-upload.md](file-upload.md) | ✅ |
| Header | [header.md](header.md) | ✅ |
| Image | [image.md](image.md) | ✅ |
| Input | [input.md](input.md) | ✅ |
| Link | [link.md](link.md) | ✅ |
| Modal | [modal.md](modal.md) | ✅ |
| Notification | [notification.md](notification.md) | ✅ |
| Number Input | [number-input.md](number-input.md) | ✅ |
| Pagination & Rows Per Page | [pagination.md](pagination.md) | ✅ |
| Password Input | [password-input.md](password-input.md) | ✅ |
| Phone Input | [phone-input.md](phone-input.md) | ✅ |
| Popover | [popover.md](popover.md) | ✅ |
| Progress Bar | [progress-bar.md](progress-bar.md) | ✅ |
| Radio (RadioGroup) | [radio.md](radio.md) | ✅ |
| Select | [select.md](select.md) | ✅ |
| Sidenav | [sidenav.md](sidenav.md) | ✅ |
| Slider | [slider.md](slider.md) | ✅ |
| Spinner | [spinner.md](spinner.md) | ✅ |
| Switch | [switch.md](switch.md) | ✅ |
| Table | [table.md](table.md) | ✅ |
| Tabs | [tabs.md](tabs.md) | ✅ |
| Text Editor | [text-editor.md](text-editor.md) | ✅ |
| Textarea | [textarea.md](textarea.md) | ✅ |
| Timeline | [timeline.md](timeline.md) | ✅ |
| Toast | [toast.md](toast.md) | ✅ |
| Tooltip | [tooltip.md](tooltip.md) | ✅ |
| Typography | [typography.md](typography.md) | ✅ |

Status: ✅ Complete · 🚧 Incomplete (image references don't cover all details yet) · ⬜ Not created yet

## Adding New Documentation
1. Copy `_template.md` → rename it to match the component name (lowercase, kebab-case)
2. Fill in **Function & When to Use** and **Variant Guide** first — this is the most important part since it isn't reflected in the types
3. Fill in Do / Don't with concrete examples (can be filled in incrementally as new cases are found)
4. Add a new row to the table above