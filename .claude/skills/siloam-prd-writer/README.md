# siloam-prd-writer

A Claude skill for writing structured PRDs (Product Requirement Documents) — strictly based on what you provide. No sugar-coating, no invented requirements.

## What it does

Every time you ask for a PRD, the skill will:

1. **Show its thinking** — analyzes your input and flags what's missing
2. **Ask for PRD metadata** — title, version, status, creator, stakeholders, date
3. **Ask for missing feature data** — via interactive pill/button selections (multi-select supported)
4. **Write the PRD** with four sections:
   - User Story
   - Acceptance Criteria
   - Edge Cases
   - Success Metrics
5. **Resolve TBDs** — any unknown items are followed up with pill questions before finalizing

Items that can't be determined are marked **(TBD)** or **(TBC)** — never invented.

---

## Output example

```
─────────────────────────────────────────
📄 PRD: Lab Worklist Feature
─────────────────────────────────────────
Version     : v1.0
Status      : Draft
Date        : 26 May 2026
Created by  : John Doe
Stakeholders: Product Manager, Tech Lead, QA
─────────────────────────────────────────

### User Story
As a Lab Technician and Lab Analyst, I want to view and manage
doctor request orders in a single worklist, so that I can process
lab requests faster and reduce missed orders.

### Acceptance Criteria
1. The worklist displays all incoming doctor request orders.
2. The user can update the status of an order.
...

### Edge Cases
1. If there are no orders → display empty state message.
2. If data fails to load → show error with retry button.
...

### Success Metrics
- Single application usage: no external tool switching required.
- Time to process an order: (TBD) — confirm with stakeholders.
```

---

## Installation

Claude skills are installed **manually** — they cannot be auto-installed from GitHub.

### Step-by-step

1. **Download** the `.skill` file from this repository:
   [`siloam-prd-writer.skill`](./siloam-prd-writer.skill)

2. **Open Claude** at [claude.ai](https://claude.ai)

3. **Go to Settings**
   - Click your profile icon (top right)
   - Select **Settings**

4. **Open the Skills section**
   - Look for **"Skills"** in the left sidebar

5. **Install the skill**
   - Click **"Add skill"** or **"Install from file"**
   - Upload the `siloam-prd-writer.skill` file
   - Confirm installation

6. **Done** — the skill is now active in your Claude conversations.

> ⚠️ Skills are tied to your Claude account. Each team member who wants to use it needs to install it individually.

---

## How to use

Once installed, just describe the feature you want a PRD for — in plain language. No special command needed.

**Examples that trigger the skill:**

```
"Write a PRD for a login page"
"I need a PRD for the lab worklist feature"
"Create user stories for the patient registration flow"
"PRD for a notification system"
"Write acceptance criteria for the doctor appointment booking feature"
```

The skill will guide you through the rest using interactive buttons — no typing required for most fields.

---

## Updating the skill

When a new version is released:

1. Download the new `.skill` file
2. Go to **Settings → Skills**
3. Remove the old `siloam-prd-writer` skill
4. Install the new `.skill` file

Versioning follows `v[major].[minor]` — check the [releases page](../../releases) for changelogs.

---

## Contributing

This skill is maintained by the Siloam team. To suggest changes:

1. Open an issue describing what's missing or broken
2. Or submit a pull request with an updated `SKILL.md`

The skill logic lives entirely in `siloam-prd-writer/SKILL.md` — plain markdown, easy to read and edit.

---

## Repository structure

```
siloam-prd-writer/
├── SKILL.md                  # Skill instructions (the brain)
├── siloam-prd-writer.skill   # Packaged file — install this into Claude
└── README.md                 # This file
```

---

## License

Internal use — Siloam Hospitals Group.
