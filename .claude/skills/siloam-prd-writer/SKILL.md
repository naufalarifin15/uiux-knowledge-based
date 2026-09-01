---
name: siloam-prd-writer
description: Write PRDs (Product Requirement Documents) containing background, problem statement, solution, user stories, acceptance criteria, edge cases, and success metrics — based strictly on what the user provides. Use this skill whenever the user asks for a PRD, user story, acceptance criteria, success metric, or any product requirement document. Trigger even on casual phrasing like "write a PRD for X", "I need user stories for Y", "create AC for this feature", "what are the success metrics for Z", or "add a problem statement". Do NOT add features, assumptions, or elaborations beyond what the user explicitly states.
---

# PRD Writer Skill

## Core Rule

**Only write what the user gives you. No additions, no sugar-coating, no "nice to have" extras.**

- Thin input → show thinking, ask via AskUserQuestion, then write.
- Rich input → show thinking, write directly.
- Never invent requirements, edge cases, metrics, evidence, or alternatives the user did not mention.
- Any field the user cannot or does not fill → mark **(TBD)** or **(TBC)**, then ask via AskUserQuestion to resolve.

---

## Process

### Step 1 — Show thinking (always first)

```
🧠 Analyzing your input...
- Feature: [name]
- Background / Problem: [found ✅ / not found ⚠️]
- Evidence & Data: [found ✅ / not found ⚠️]
- Context & History: [found ✅ / not found ⚠️]
- Cost of Inaction: [found ✅ / not found ⚠️]
- Role: [found ✅ / not found ⚠️]
- Action: [found ✅ / not found ⚠️]
- Outcome: [found ✅ / not found ⚠️]
- Expected behavior: [found ✅ / not found ⚠️]
- Solution / Approach: [found ✅ / not found ⚠️]
- Tech Specification: ✅ always included (Siloam standard stack)
- UI Style (design style, colors, references): [found ✅ / not found ⚠️]
- Design artifacts: [found ✅ / not found ⚠️]
- Alternatives considered: [found ✅ / not found ⚠️]
- Success metrics: [found ✅ / not found ⚠️]
- Edge cases: [derivable ✅ / not found ⚠️]

⚠️ Missing: [list] — asking now.
```

---

### Step 2 — Metadata (always, every time)

**Step 2a — AskUserQuestion:**
```
AskUserQuestion:
- header: "Status"
  question: "What is the current status of this PRD?"
  options: ["Draft", "In Review", "Final"]
  multiSelect: false

- header: "Stakeholders"
  question: "Who are the stakeholders involved?"
  options: [context-relevant roles]
  multiSelect: true

- header: "Version"
  question: "What version is this PRD?"
  options: ["v1.0", "v1.1", "v1.2", "v2.0"]
  multiSelect: false
```
(An "Other" free-text option is always available automatically — no need to add it manually.)

**Step 2b — Plain text follow-up (one message):**
> "Three quick details:
> 1. PRD title / name?
> 2. Creator / author?
> 3. Today's date?"

Missing fields → **(TBD)**.

---

### Step 3 — Background & Problem data (ask if missing)

For each sub-field below, if missing ask via AskUserQuestion before writing.

**Problem Statement** — if not provided:
```
AskUserQuestion:
- header: "Problem Type"
  question: "What type of problem does this feature solve?"
  options: ["User pain point", "Business inefficiency", "Compliance / regulatory",
            "Competitive gap", "Technical debt"]
  multiSelect: true
```
Then plain text follow-up: "Describe the problem: who is affected, how often, how severely?"

**Evidence & Data** — if not provided:
```
AskUserQuestion:
- header: "Evidence"
  question: "What evidence supports this problem?"
  options: ["User research / interviews", "Support tickets", "NPS / CSAT data",
            "Analytics / usage data", "Incident reports", "Stakeholder feedback",
            "None yet / TBD"]
  multiSelect: true
```

**Context & History** — if not provided:
```
AskUserQuestion:
- header: "Prior Work"
  question: "Has this been attempted or related to prior work?"
  options: ["Yes — I'll provide details", "No prior work", "Not sure / TBD"]
  multiSelect: false
```

**Cost of Inaction** — if not provided:
```
AskUserQuestion:
- header: "Risk"
  question: "What is at risk if this is not built?"
  options: ["Revenue loss", "User churn", "Compliance / legal risk",
            "Competitive disadvantage", "Operational inefficiency",
            "Patient safety risk", "Skip / TBD"]
  multiSelect: true
```

---

### Step 4 — Feature data (ask if missing)

Max 4 questions per `AskUserQuestion` call. Prioritize: Role → Outcome → Behavior.

**Role** (`multiSelect: true`)
**Expected behavior** (`multiSelect: true`)
**Edge cases** (`multiSelect: true`) — include "Skip / TBD" as an option
**Outcome** (`multiSelect: true`) — "Save time", "Reduce errors", "Replace another tool", "Improve visibility"
**Success metrics** (`multiSelect: true`) — "Task completion rate", "Time saved", "Error reduction", "User adoption", "Skip / TBD"

(Free-text "Other" is always available automatically for every question.)

---

### Step 4b — Tech Specification (always, no need to ask)

The Siloam standard tech stack is fixed and must always be included in the PRD without asking the user. Insert it as a section at the very top of the output, before everything else — above the PRD Header.

Ask only if the user wants to **override or extend** the defaults:

```
AskUserQuestion:
- header: "Stack Override"
  question: "Are there any additions or overrides to the standard Siloam tech stack?"
  options: ["Add GraphQL layer", "Add WebSocket / real-time layer",
            "Custom state management (Pinia extension)", "No changes — use standard stack"]
  multiSelect: true
```

If user selects "No changes" → skip and use defaults as-is.
If user selects other options → append those to the Tech Spec output.

---

### Step 5 — Solution data (ask if missing)

**Proposed Approach** — if not provided, plain text prompt:
> "Describe the proposed solution at a product level. Reference designs if available — do not describe UI in prose."

**UI Style** — always ask, even if user described the UI:
```
AskUserQuestion:
- header: "Design Style"
  question: "What is the design style for this feature?"
  options: ["Modern SaaS dashboard", "Minimal / clean", "Mobile-first",
            "Enterprise / CRM style", "Healthcare / clinical (Pulse DS default)",
            "Follow existing product style"]
  multiSelect: false

- header: "Primary Color"
  question: "What is the primary color style?"
  options: ["Indigo", "Blue", "Emerald", "Teal", "Red / Rose",
            "Neutral grayscale", "Follow Pulse DS tokens"]
  multiSelect: false

- header: "Secondary Color"
  question: "What is the secondary color style?"
  options: ["Soft gray", "White / minimal", "Amber / warm", "Slate",
            "Complement primary", "Follow Pulse DS tokens"]
  multiSelect: false
```
After the questions, ask plain text follow-up:
> "Do you have a design reference (e.g. Figma link, website, product name)? If yes, paste it. If no, type 'none'."

If user skips any UI Style field → mark **(TBD)**.

**Design Artifacts** — if not provided:
```
AskUserQuestion:
- header: "Artifacts"
  question: "Which design artifacts are available?"
  options: ["User Flow", "Wireframes", "Mockups", "Prototype", "None yet / TBD"]
  multiSelect: true
```
For each selected artifact, ask plain text: "Paste the link and status (Draft/Final) for [artifact]."

**Considered Alternatives** — always mandatory, ask if missing:
> "What alternatives were considered and why were they rejected? List at least one option."

**Technical Constraints** — if not provided:
```
AskUserQuestion:
- header: "Constraints"
  question: "Are there technical constraints shaping this solution?"
  options: ["Existing architecture limits", "Third-party dependencies",
            "Performance requirements", "Security / compliance constraints", "None"]
  multiSelect: true
```

---

### Step 6 — Write the PRD

Write all sections in order. After writing, scan every **(TBD)** item — for any that can be resolved by asking the user, call `AskUserQuestion` with relevant options + "Skip / Leave as TBD". Max 4 per call.

If user picks "Skip / Leave as TBD" → keep **(TBD)**, annotate: *to be confirmed with stakeholders.*
Do NOT ask about TBDs that are purely stakeholder/business decisions (e.g. exact revenue targets).

---

## Output Format

### ⚙️ TECHNICAL SPECIFICATION
> This section is always placed at the very top of every PRD output — before the PRD Header.

```
══════════════════════════════════════════
⚙️  TECHNICAL SPECIFICATION — SILOAM STANDARD
══════════════════════════════════════════

STACK
─────────────────────────────────────────
Framework         : Vue 3 (Composition API)
UI Framework      : @siloamhospitals/ui-vue (Pulse DS — sole source of truth)
Language          : TypeScript
State Management  : Pinia

ARCHITECTURE
─────────────────────────────────────────
Layout Pattern    : Sidebar + Topbar (Dashboard layout)
Architecture      : Component-based architecture
Data Fetching     : API-based (REST / fetch / composables)
Responsive        : See docs/dos-donts/_breakpoints.md
                    Mobile   → 0–500px
                    Tablet   → 501–1023px
                    Desktop  → 1024px and up
Dark Mode         : Per Pulse DS tokens (if supported)
Pattern           : Clinical EMR dashboard pattern

DESIGN SYSTEM PRIORITY
─────────────────────────────────────────
1. @siloamhospitals/ui-vue (Pulse DS) — exclusive source for all visual concerns
2. No new package installations without explicit confirmation
3. No custom Tailwind / improvised styling — use exact Pulse DS tokens only

OVERRIDES / ADDITIONS
─────────────────────────────────────────
[Populated from user selections — or "None" if standard stack]
══════════════════════════════════════════
```

Rules:
- This section is **always generated** — do not skip, do not ask permission.
- The stack values above are Siloam defaults — never change them unless the user explicitly overrides.
- The Responsive breakpoint values must always match `docs/dos-donts/_breakpoints.md`. If that file is ever updated, update this section too — do not let the two drift apart.
- The OVERRIDES row is populated from Step 4b user selection. If "No changes" → write "None".
- Place this before the PRD Header in every output.

---

### PRD Header

```
─────────────────────────────────────────
📄 PRD: [Title]
─────────────────────────────────────────
Version     : [v1.0]
Status      : [Draft / In Review / Final]
Date        : [DD MMM YYYY]
Created by  : [Name]
Stakeholders: [List]
─────────────────────────────────────────
```

---

### Section 1 — Background

#### Problem Statement
> Lead with the problem — never the solution.

[Describe the user or business pain. Who is affected? How often? How severely?]

If not provided → **(TBD)**

#### Evidence & Data
> No unsubstantiated claims.

[Cite data, research, support tickets, NPS feedback, or incidents.]

If not provided → **(TBD)** — annotate: *No evidence provided. Confirm before finalizing.*

#### Context & History
[Prior work, failed attempts, or related initiatives. Link to prior PRDs or post-mortems.]

If not provided → **(TBD)**

#### Cost of Inaction
[What is lost if this is not pursued — revenue, users, compliance, competitive position?]

If not provided → **(TBD)**

---

### Section 2 — User Story

> As a **[role(s)]**, I want **[action]**, so that **[outcome]**.

- Multiple roles → list them.
- Missing parts → **(TBD)**.
- Assign ID: **US-001**, **US-002**, etc. (increment per story if multiple).

---

### Section 3 — Acceptance Criteria

Numbered list using "Given / When / Then" or plain declarative statements.
- Traces directly to user input or selections.
- Incomplete → **(TBD)** or **(TBC)** inline.
- No padding.

---

### Section 4 — Edge Cases

Numbered list, condition + expected behavior.
- Derive logically from described behavior (empty state, failure, session expiry).
- Include only what user confirmed or what is derivable.
- Unknown behavior → **(TBD)**.

---

### Section 5 — Solution

#### Proposed Approach
[Product-level description. Reference designs — do not describe UI in prose.]

If not provided → **(TBD)**

#### UI Style

| Property              | Value                     |
|-----------------------|---------------------------|
| Design Style          | [e.g. Modern SaaS dashboard] |
| Primary Color Style   | [e.g. Indigo]             |
| Secondary Color Style | [e.g. Soft gray]          |

Rules:
- Always include this table in the Solution section.
- Populate from user's selections or typed input.
- Unknown fields → **(TBD)**.
- If user provided a design reference link → include it here and reference it in Design Artifacts table.
- All colors/spacing must ultimately resolve to Pulse DS tokens — see `docs/dos-donts/` for exact token values per component.
- Any responsive/breakpoint behavior mentioned must match `docs/dos-donts/_breakpoints.md` and `docs/dos-donts/_form-layout.md` — do not invent different breakpoint values.

#### Design Artifacts

| Artifact   | Link    | Status         |
|------------|---------|----------------|
| User Flow  | [Link]  | Draft / Final  |
| Wireframes | [Link]  | Draft / Final  |
| Mockups    | [Link]  | Draft / Final  |

Rules:
- Links are required. If not yet available → write **(TBD)** in Link column.
- Do not describe UI elements in prose — reference the design artifact instead.

#### User Story Coverage Map

| User Story | Solution Component | Design Reference      |
|------------|--------------------|-----------------------|
| US-001     | [Component]        | [Screen name / link]  |
| US-002     | [Component]        | [Screen name / link]  |

Rules:
- Every user story written in Section 2 must appear here.
- If design reference is not yet available → **(TBD)**.

#### Considered Alternatives

| Option   | Description     | Why Rejected |
|----------|-----------------|--------------|
| Option A | [Description]   | [Reason]     |
| Option B | [Description]   | [Reason]     |

Rules:
- **Mandatory** — always include at least one alternative.
- If user provided none → ask before writing. Do not invent alternatives.
- If user explicitly has no alternatives → write one row: "No alternatives considered" + note **(TBD — confirm with team)**.

#### Technical Constraints & Decisions
[Architectural decisions or constraints that shaped the solution.]

If not provided → **(TBD)**

---

### Section 6 — Success Metrics

| Metric | Target | Notes |
|--------|--------|-------|
| [Metric name] | [Target value] | [Context] |

- Only metrics the user provided or selected.
- Unknown target → **(TBD)**.
- No fabricated KPIs.

---

## TBD / TBC Resolution (after writing)

After the PRD is written, scan all **(TBD)** and **(TBC)** items.

For each resolvable TBD → use `AskUserQuestion`:
```
options: [relevant options for that field] + "Skip / Leave as TBD"
```

For each resolvable TBC → use `AskUserQuestion`:
```
options: [relevant options] + "Leave as TBC"
```
(Free-text custom answer is always available automatically — no need to add "I'll type it" manually.)

Max 4 questions per call. After user responds → update PRD in place.

---

## Relationship to this knowledge base

- This skill produces PRDs for **new features**. For component-level implementation details (exact tokens, spacing, do's/don'ts), always cross-check `docs/dos-donts/` before writing the Tech Spec or UI Style sections.
- Breakpoint and responsive grid values used anywhere in a PRD must come from `docs/dos-donts/_breakpoints.md` and `docs/dos-donts/_form-layout.md` — never hardcode different values (e.g. do not use generic Tailwind breakpoints like `sm/md/lg/xl/2xl`; this project uses Mobile 0–500px, Tablet 501–1023px, Desktop 1024px+).
- `docs/PRD/` contains the static reference templates (`README.md` for the index, `_template.md` for the module structure) — this skill is the interactive way to actually generate a PRD. Keep the templates in `docs/PRD/` as a manual fallback/reference; this skill is the primary workflow.

---

## What NOT to do

- Do not skip the thinking block.
- Do not skip metadata — mandatory every time.
- Do not write plain text question lists — always use `AskUserQuestion`.
- Do not use `multiSelect: false` for role, behaviors, or edge cases.
- Do not write the PRD before collecting metadata, background, and feature data.
- Do not invent evidence, alternatives, metrics, or constraints.
- Do not describe UI in prose in the Solution section — reference design artifacts.
- Do not skip the Alternatives section — it is mandatory.
- Do not leave all user stories out of the Coverage Map.
- Do not leave TBDs unaddressed — always follow up via AskUserQuestion.
- Do not introduce React/Next.js/Tailwind — this project's stack is Vue 3 + @siloamhospitals/ui-vue only.
- Do not hardcode breakpoint values that diverge from `docs/dos-donts/_breakpoints.md`.