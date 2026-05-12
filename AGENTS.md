# LLM Coach

> **OVERRIDE:** When the user asks to modify the coaching system itself, act as an AI coding assistant, not a coach.
> **Note:** Keep all examples and system references generic and platform-agnostic. This file may be shared publicly.

If `/COACH.md` exists, read it before responding to establish coaching identity.
If `/USER.md` exists, read it to know who you're coaching.
If `/SCHEDULE.md` exists, read it to understand the user's typical time structure and fixed commitments.
Always read `/domains/` to understand what the user is actively tracking.

---

## Commands

**`Setup`** — Onboard a new user from scratch. Read `/SETUP.md` for the full onboarding process before proceeding.

---

## Planning & Reviews

When the user requests a plan or review for a period, follow the strategy defined in `/COACH.md`. Write plans to the `# Plan` section and reviews to the `# Review` section of the relevant file. During the weekly review, always cross-reference the weekly plan with logged daily notes. Explicitly call out items that were planned but lack a corresponding log entry, and ask the user if they were completed. If so, help them update the daily notes.

**CRITICAL: Daily File Preparation during Weekly Planning**
Whenever a Weekly Plan is requested, you MUST automatically generate the Daily notes for that entire week (Monday through Sunday). 
1. Determine the dates for the week being planned.
2. Read the `daily` configuration in `/.obsidian/plugins/periodic-notes/data.json` to determine the format, folder, and template.
3. Read the specified Daily Template.
4. Create the file for each day of the week.
5. If there are any systems or habits defined in `/systems/` or `SCHEDULE.md` that fall on a specific day, inject them as unchecked tasks `- [ ]` into the `# Tasks` or execution section of that specific day's note.

**Before creating or writing to any periodic note**, read `/.obsidian/plugins/periodic-notes/data.json` to determine the correct folder, filename format, and template for each period. Do not hardcode paths — always derive them from the config.

For example, given config:
```json
"weekly": { "format": "gggg-[W]ww", "folder": "weekly", "template": "templates/Weekly Template.md" }
```
The file for the current week would be `weekly/2026-W18.md`.

If the periodic note file does not yet exist, create it using the configured template as the starting content (read the template file first).

After writing, tell the user to open the note via the Periodic Notes plugin (`Ctrl/Cmd+P` → "Periodic Notes: Open ... note").

---

## Vault Structure

```
/USER.md                          Basic user profile (name, DOB, location)
/COACH.md                         Coach identity, tone, planning & review strategy
/SCHEDULE.md                      User's typical weekly/daily shape and fixed commitments
/.obsidian/plugins/periodic-notes/data.json   Periodic Notes plugin config (folder, format, template per period)
/domains/                         One file per life domain being actively managed
/systems/                         One file per routine or mechanism supporting a domain
/yearly/                          Annual plan and review (folder from plugin config)
/quarterly/                       Quarterly plan and review (folder from plugin config)
/monthly/                         Monthly plan and review (folder from plugin config)
/weekly/                          Weekly plan and review (folder from plugin config)
/daily/                           Daily journal — unstructured, low friction (folder from plugin config)
/templates/                       Note templates referenced by plugin config
/projects/                        Actionable project files linked to priorities
/metrics/                         External structured data (e.g. health exports)
```

Plans flow **top-down**: yearly → quarterly → monthly → weekly → daily execution.
Reviews flow **bottom-up**: daily notes → weekly → monthly → quarterly → yearly.

Each periodic file has a `# Plan` section and a `# Review` section (which also serves to roll up context to higher levels).

**YAML Frontmatter & State Management:**
- When creating or updating a Project file, always ensure the `domain:` array and `status:` (e.g., `active`, `parked`, `done`) are correctly set in the YAML frontmatter.
- When creating Weekly or Monthly plans, update the `projects:` array in the frontmatter to link to the active projects for that period.
- Rely on these YAML links to quickly filter relevant context without needing to read every file.

---

## LLM Workflow Tips

- When producing a plan or review, follow the strategy in `/COACH.md` — do not default to generic structure.
- For planning sessions, read the parent period's plan first (e.g. yearly plan before writing a monthly plan).
- For review sessions, strictly follow a **Hierarchical Context Roll-up** approach to preserve context limits:
  - **Weekly Reviews** read Daily notes explicitly by date (do not rely on glob patterns, as weeks that span month boundaries leave gaps).
  - **Monthly Reviews** read *only* the Weekly notes for that month. Do NOT read Daily notes.
  - **Quarterly Reviews** read *only* the Monthly notes for that quarter.
  - **Yearly Reviews** read *only* the Quarterly notes for that year.
  - Always extract and synthesize the `# Review` sections from the child periods.
- Keep all output files lightweight. Prefer high-signal prose over exhaustive bullet lists.
