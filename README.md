# UI/UX Knowledge Base

This repository contains documentation and context used by **Claude Code** during vibecoding sessions on Vue 3 projects built with `@siloamhospitals/ui-vue`. This repo is **universal** — designed to be reused across any project (not tied to a specific product), just adjust the contents of `docs/PRD.md` to match the project you're working on. Since all UI needs reference the package, this repo **does not** manually document component tokens/props — the focus is on product context and correct usage patterns.

## Folder Structure
```
.
├── CLAUDE.md                      # Main instructions, automatically read by Claude Code
├── docs/
│   ├── PRD.md                      # Product requirements: roles, sitemap, pages, business rules
│   └── dos-donts/
│       ├── README.md               # Index of all components + their status
│       ├── _template.md            # Template for adding new documentation
│       ├── button.md
│       ├── input.md
│       ├── toast.md
│       └── ...                     # one file per component in the package
└── .claude/
    └── skills/
        └── siloam-prd-writer/       # Interactive PRD-writing skill (auto-triggers on "write a PRD for X")
            ├── SKILL.md
            └── README.md
```

## Cloning This Repo
This repo is ready to use as-is — no sub-folder navigation needed.

1. Clone it:
   ```
   git clone https://github.com/naufalarifin15/uiux-knowledge-base-en.git
   ```
2. Open the cloned folder directly in VSCode / Claude Code.
3. That's it — Claude Code automatically reads `CLAUDE.md`, `docs/dos-donts/`, and activates the `siloam-prd-writer` skill.

## How to Use
1. Place this folder in the root of your Vue 3 project (or symlink it if used across multiple projects).
2. Open VSCode with Claude Code active in the same project root.
3. Claude Code automatically reads `CLAUDE.md` as the base instruction for every session.
4. For component props/API, Claude Code refers directly to the types from `@siloamhospitals/ui-vue`.
5. For usage patterns & variant selection (do's & don'ts), Claude Code refers to `docs/dos-donts/`.
6. To generate a PRD, just ask: "write a PRD for [feature name]" — the `siloam-prd-writer` skill will guide you through it interactively.

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
`docs/PRD.md` should be updated whenever there's a new page/role, so Claude Code always has accurate business context when generating new pages.
