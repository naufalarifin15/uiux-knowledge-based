# UI/UX Knowledge Base

This repository contains documentation and context used by **Claude Code** during vibecoding sessions on Vue 3 projects built with `@siloamhospitals/ui-vue`. This repo is **universal** — designed to be reused across any project (not tied to a specific product), just adjust the contents of `docs/PRD/` to match the project you're working on. Since all UI needs reference the package, this repo **does not** manually document component tokens/props — the focus is on product context and correct usage patterns.

## Folder Structure
```
.
├── CLAUDE.md                      # Main instructions, automatically read by Claude Code
├── docs/
│   ├── PRD/
│   │   ├── README.md               # Index: product overview, global roles, sitemap, cross-module business rules
│   │   ├── _template.md            # Template for adding a new module's PRD
│   │   ├── module-a.md
│   │   ├── module-b.md
│   │   └── ...                     # one file per module/feature
│   ├── dos-donts/
│   │   ├── README.md               # Index of all components + their status
│   │   ├── _template.md            # Template for adding new documentation
│   │   ├── button.md
│   │   ├── input.md
│   │   ├── toast.md
│   │   └── ...                     # one file per component in the package
│   └── assets/                     # Visual references linked from PRD / dos-donts files (flat folder)
│       ├── mockup-*.png             # Figma/design references for features not yet built
│       ├── screenshot-*.png         # Bug captures, error states, existing UI conditions
│       └── ref-*.png                # Supporting visual references (inspiration, competitor UI, etc.)
└── .claude/
    └── skills/
        └── siloam-prd-writer/       # Interactive PRD-writing skill (auto-triggers on "write a PRD for X")
            ├── SKILL.md
            └── README.md
```

## How to Use
1. Place this folder in the root of your Vue 3 project (or symlink it if used across multiple projects).
2. Open VSCode with Claude Code active in the same project root.
3. Claude Code automatically reads `CLAUDE.md` as the base instruction for every session.
4. For component props/API, Claude Code refers directly to the types from `@siloamhospitals/ui-vue`.
5. For usage patterns & variant selection (do's & don'ts), Claude Code refers to `docs/dos-donts/`.
6. To generate a PRD, just ask: "write a PRD for [feature name]" — the `siloam-prd-writer` skill will guide you through it interactively and save the result as a new file in `docs/PRD/`.
7. For visual references (mockups, screenshots), save the image to the relevant `docs/assets/` subfolder, link it in the corresponding PRD or dos-donts file, and include its path explicitly when prompting Claude Code — see **Visual Assets** below.

## Coverage of `docs/dos-donts/`
**Every component in `@siloamhospitals/ui-vue` should ideally have a documentation file**, because the package's types only explain *what* props/variants are available, not *when* and *why* to use them. This matters especially for variants that carry functional meaning, for example:
- **Size** — when to use `sm` vs `md` vs `lg`
- **Color/variant** — colors that represent different functions (e.g. `danger` for destructive actions, not just an aesthetic choice)

Documentation can be built incrementally (starting with the most frequently used components), but the goal is to eventually cover all components — not just the ones that have caused issues.

## Adding New Documentation
1. Copy `docs/dos-donts/_template.md` → rename it to match the component name
2. Fill in the **Variant Guide** first (size, color/function, etc.)
3. Fill in the Do / Don't section with concrete examples
4. Add a row to `docs/dos-donts/README.md`

## Updating the PRD
Each module's PRD file in `docs/PRD/` should be updated whenever there's a new page/role for that module, so Claude Code always has accurate business context when generating new pages. When adding a new module, copy `docs/PRD/_template.md` and register it in the **Modules / Features** table in `docs/PRD/README.md`.

## Visual Assets
`docs/assets/` holds uploaded visual references (mockups, screenshots) used across PRD and dos-donts documentation — separate from `src/assets/` in the consuming project, which is for runtime application assets. References can also be **links** (Figma files/nodes, or any other external URL) instead of uploaded files — links stay current while exported images can go stale.

- **Uploaded images** — flat folder, distinguished by a type prefix in the filename: `[type]-[module]-[short-description]-[optional-version].png`, where `[type]` is `mockup`, `screenshot`, or `ref`
  e.g. `mockup-dashboard-emr-overview-v1.png`, `screenshot-patient-list-filter-bug.png`
- **Links** — referenced directly as a URL, labeled by source (e.g. `Figma`, `Ref`) so it's clear how Claude Code should use it

**Linking in docs**, use a `## Visual Reference` section that mixes both as needed:
```markdown
## Visual Reference
- ![Dashboard EMR Overview](../assets/mockup-dashboard-emr-overview-v1.png)
  **Path for Claude Code**: `docs/assets/mockup-dashboard-emr-overview-v1.png`
- **Figma**: https://www.figma.com/file/xxxxx/Dashboard-EMR?node-id=123-456
- **Ref**: https://dribbble.com/shots/xxxxx
```
Neither a rendered markdown image nor a plain URL gives Claude Code visual/design access on its own — the file path or link needs to be referenced directly in a prompt when analysis is needed. For Figma links, specify Vue 3 conversion explicitly, since `Figma:get_design_context` defaults to React output.
- Note that the rendered markdown image alone doesn't give Claude Code visual access — the path needs to be referenced directly in a prompt (e.g. "Read `docs/assets/mockups/dashboard-emr-overview-v1.png` and implement this using DS Pulse").

See `CLAUDE.md` → **Visual Assets Convention** for the full rules.