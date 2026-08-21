# Product Requirements Documentation — Index

## Overview
<!-- 1-2 paragraphs: product/app name, its main purpose, target users, brief business context -->

[Fill in here]

## Modules / Features

| File | Module | Status | Last Updated |
|------|--------|--------|---------------|
| [module-name.md](./module-name.md) | Module Name | 📝 Draft | YYYY-MM-DD |

<!-- 
Status legend:
📝 Draft        — still in initial drafting
🚧 In Progress  — reviewed, some parts still changing
✅ Complete     — final, ready to be used as a development reference
🔄 Needs Update — was complete, but requirements have changed
-->

## User Roles
<!-- List all roles/actors that interact with the system, with a short description of their access/responsibilities.
If a role is very specific to one module, just name it here and detail it in the relevant module file -->

- **[Role Name]** — [short description of access/authority]

## Global Business Rules
<!-- Business rules that apply ACROSS modules (not specific to a single module).
Examples: ID formats, general validation rules, role-based access policy, etc. -->

- [Rule 1]
- [Rule 2]

## Glossary (optional)
<!-- Domain-specific terms that may be unfamiliar, especially if the product is technical/niche -->

- **[Term]** — [short definition]

## How to Use This Documentation
- Each file in this folder represents one module/feature, containing: user stories, flow, business rules specific to that module, and wireframe/design references if available.
- When adding a new PRD:
  1. Use `_template.md` (if available) as the starting point
  2. Update the **Modules / Features** table above
  3. Update the **Status** whenever there is a significant change
- Business rules that apply to more than one module belong in the **Global Business Rules** section, not duplicated across module files.