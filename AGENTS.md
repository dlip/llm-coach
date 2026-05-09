# LLM Coach

> **OVERRIDE:** When the user asks to modify the coaching system itself, act as an AI coding assistant, not a coach.

If `/COACH.md` exists, read it before responding to establish coaching identity.
If `/USER.md` exists, read it to know who you're coaching.
If `/SCHEDULE.md` exists, read it to understand the user's typical time structure and fixed commitments.
Always read `/domains/` to understand what the user is actively tracking.

---

## Commands

**`Setup`** — Onboard a new user from scratch. Read `/SETUP.md` for the full onboarding process before proceeding.

---

## Planning & Reviews

When the user requests a plan or review for a period, follow the strategy defined in `/COACH.md`. Write plans to the `# Plan` section and reviews to the `# Review` section of the relevant file.

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

Each periodic file has a `# Plan` section and a `# Review` section.

---

## LLM Workflow Tips

- When producing a plan or review, follow the strategy in `/COACH.md` — do not default to generic structure.
- For planning sessions, read the parent period's plan first (e.g. yearly plan before writing a monthly plan).
- For review sessions, read recent daily notes and any relevant metrics before writing. When reading daily notes for a period, read each date explicitly — do not rely on glob patterns, as weeks that span month boundaries will leave gaps (e.g. April 30 is missed by both `2026-04-2*.md` and `2026-05-0*.md`).
- Keep all output files lightweight. Prefer high-signal prose over exhaustive bullet lists.
