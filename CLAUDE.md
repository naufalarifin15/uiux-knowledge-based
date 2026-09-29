# CLAUDE.md — Project Instructions

## Project Context
- Framework: Vue 3 (Composition API, `<script setup>`)
- Design System: `@siloamhospitals/ui-vue` package — the **single source of truth** for UI components, styling, fonts, spacing, and icons
- Domain/product: see `docs/PRD/` (this file is universal and reused across multiple projects — product details always reference the PRD, not hardcoded here)

## Before You Start
- Always check the current git branch and working directory status before creating or editing files (`git status`). Never assume you are on `main` — collaborators may be working from a different branch.
- If the working directory is not clean (uncommitted changes present) or the branch doesn't match the current task, **stop and ask the user** before proceeding, instead of assuming it's safe to continue.

## Hard Rules
1. **All visual needs must use components from `@siloamhospitals/ui-vue`.** Do not build custom components if an equivalent already exists in the package.
2. **Do not install new packages** (including other UI libraries, CSS frameworks, icon sets) without explicit confirmation from the user.
3. Do not write inline styles or custom CSS classes to mimic components that are already available in the package.
4. Before creating a new component/page, always check:
   - **Props/API** → directly from the package's types/JSDoc (`node_modules/@siloamhospitals/ui-vue`), not from manual documentation.
   - **Variant choices (size, color/function, etc.) and usage patterns** → `docs/dos-donts/[component-name].md`. This MUST be checked, especially for variants that carry functional meaning (e.g. color for destructive vs. primary actions), since the types don't explain when each value should be used.
   - If the dos-donts file for that component doesn't exist yet or is incomplete, don't assume — ask the user.

## Documentation References
- `docs/PRD/` — product requirements per module (see `docs/PRD/README.md` for index, global roles, sitemap, and cross-module business rules)
- `docs/dos-donts/` — usage guide for each component: when to use a given variant, anti-patterns, context not reflected in the types
- `docs/assets/` — visual references (mockups, screenshots, design exports) linked from PRD and dos-donts files — see **Visual Assets Convention** below
- **New PRDs must be generated using the `siloam-prd-writer` skill** — this enforces the correct structure, breakpoint system, and tech-stack constraints. Do not write a PRD manually without invoking the skill first.

## Visual Assets Convention
Visual references (mockups, bug screenshots, Figma exports, or external links) used in documentation are **distinct from `src/assets/`**, which holds runtime application assets. References come in two forms:

**A. Uploaded images** (screenshots, exported mockups, saved reference images)
- Stored as files in a single flat folder: `docs/assets/`
- **Naming pattern:** `[type]-[module]-[short-description]-[optional-version].png`, where `[type]` is `mockup`, `screenshot`, or `ref`
  - `mockup-dashboard-emr-overview-v1.png`
  - `screenshot-patient-list-filter-bug.png`
  - `ref-appointment-scheduler-inspiration.png`
- lowercase, dash-separated, no underscores; use `-v2`, `-v3` suffixes for revisions instead of overwriting

**B. Links** (Figma files/nodes, or any other external URL — Dribbble, competitor site, etc.)
- Not downloaded as images — referenced directly as a URL, since links (especially Figma) stay up to date while exported images can go stale
- Labeled by source so Claude Code knows how to handle it (Figma links can be read via the Figma MCP integration for exact tokens/spacing, not just visually)

**Linking in markdown docs** (e.g. `docs/PRD/[module].md` or `docs/dos-donts/[component].md`), use a `## Visual Reference` section that can mix both forms as needed:
```markdown
## Visual Reference
- ![Dashboard EMR Overview](../assets/mockup-dashboard-emr-overview-v1.png)
  **Path for Claude Code**: `docs/assets/mockup-dashboard-emr-overview-v1.png`
- **Figma**: https://www.figma.com/file/xxxxx/Dashboard-EMR?node-id=123-456
- **Ref**: https://dribbble.com/shots/xxxxx
```
Notes:
- A rendered markdown image or a plain URL does **not** give Claude Code visual/design access on its own — always reference the explicit file path or link directly in a prompt (e.g. "Read `docs/assets/mockup-dashboard-emr-overview-v1.png`..." or "Get the design from [Figma link]...").
- For Figma links specifically, remember to specify Vue 3 conversion explicitly, since `Figma:get_design_context` defaults to React output.

## Code Conventions
- `src/` folder structure:
  - `assets/` — static files used at runtime (images, local fonts, etc.) — **not** for documentation references, see Visual Assets Convention above
  - `components/` — custom Vue components (outside the UI package)
  - `composables/` — reusable composition functions (`useXxx`)
  - `layouts/` — page layout wrappers (e.g. `DefaultLayout.vue`, `AuthLayout.vue`)
  - `mocks/` — mock/dummy data for development (see Mock Data Convention below)
  - `pages/` — page/route-level components
  - `plugins/` — Vue plugin configuration (router, pinia, etc.)
  - `services/` — API calls / backend integration
  - `stores/` — state management (Pinia)
  - `types/` — TypeScript types/interfaces
  - `utils/` — pure helper functions
  - `App.vue`, `main.ts` — entry point
- File naming: PascalCase for `.vue` components, camelCase for composables/utils/services
- Always import UI components from `@siloamhospitals/ui-vue`; don't re-export or re-wrap them without a clear reason
- New components only go into `src/components/` if they're genuinely not available in `@siloamhospitals/ui-vue` (see rules above)

## Mock Data Convention
- All mock data MUST live in `mocks/`, NEVER hardcoded directly inside a component's `<script setup>`.
- File naming: `[entity-name].mock.ts` (e.g. `patients.mock.ts`, `appointments.mock.ts`)
- Location:
  - Flat/small projects → `src/mocks/`
  - Feature-based projects → `src/features/[feature-name]/mocks/`
- Define the TypeScript interface in `src/types/` first, before generating mock data, so the structure stays consistent across components. Cross-check field names/types against the **Data Requirements** table in the relevant `docs/PRD/[module].md` file when one exists.
- Use factory functions, not static arrays, so different states (empty, loading, error, populated) are easy to generate:
```ts
  export function createMockPatient(overrides?: Partial<PatientRecord>): PatientRecord {
    return {
      id: crypto.randomUUID(),
      mrn: 'MRN-0001',
      name: 'Budi Santoso',
      // ...other default fields
      ...overrides
    }
  }
```
- Mock data must be easy to swap for real API calls — only import mocks from the `services/`/`composables/` layer, never import them directly in a component.
- Ensure the `mocks/` folder is excluded from the production build, or at minimum clearly commented as dummy data.

## Output Format
- Vue 3 Composition API code (`<script setup>`)
- Include brief comments only for non-trivial logic
- Don't add new dependencies without permission
- If a UI need isn't covered by an existing component in the package, **notify the user** before building a custom solution — don't improvise on your own