# Setup Guide

Run `Setup` to onboard a new user from scratch. Work through the three phases below in order. **Ask one question at a time throughout.**

---

## Phase 0 — User Profile

Collect basic details about the user:
- Full name
- Date of birth
- Location (city/country)

Write this to `/USER.md` before proceeding. Keep it simple — just the facts.

---

## Phase 1 — Coach Identity

Interview the user to define their coach:
- Preferred style, tone, and values
- What they most want from a coaching relationship
- How the coach approaches **planning** (e.g. vision-first, outcome-focused, obstacle-aware)
- How the coach approaches **reviews** (e.g. celebration-first, honest reflection, single key insight)

Suggest a name but let them choose.

Once agreed, write `/COACH.md` before proceeding. Include:
- Identity, tone, core values
- How the coach shows up
- `## Planning & Review Strategy` section (planning approach + review approach)

This coach identity shapes everything that follows. Do not proceed to Phase 2 without writing this file.

---

## Phase 2 — Domains

Domains are areas of life the user actively manages and wants to improve.

### Step 1 — Propose domains

Suggest 5–10 domains drawn from this list (plus any that fit the user's situation):

- Health & Energy
- Career & Work
- Finance
- Relationships
- Personal Growth
- Parenting *(if they have children)*
- Home & Environment
- Fun & Recreation
- Creativity
- Spirituality / Purpose
- Community & Contribution

Present the list, explain briefly why each was included, and invite the user to add, remove, or rename any. Get explicit approval before proceeding.

### Step 2 — Create placeholder files

Immediately after approval, create `/domains/{name}.md` for every approved domain with a minimal placeholder:

```markdown
---
title: {Domain Name}
tags:
  - domain
  - todo
status: todo
---

# {Domain Name}

*To be completed during setup.*
```

This ensures progress is preserved if the session is interrupted.

### Step 3 — Go deep on each domain

For every domain, interview the user to understand their *specific* situation — not generic goals. Ask about:
- Current state: what's actually going on right now?
- Goals or desired direction
- Struggles, blockers, or things being avoided
- Any relevant context (conditions, constraints, history)

Ask one domain at a time. **After each response, immediately write the full domain file** before moving to the next. Remove the `todo` tag and `status: todo` once written.

If setup is resumed after an interruption, check for any domain files still marked `status: todo` and continue from there.

### Step 4 — Write domain files

Each completed `/domains/{name}.md` should:
- Reflect the user's actual situation, not a generic template
- Describe where they are now and what the coach is watching for
- Be written in the coach's voice
- Stay lightweight — high-signal prose, not exhaustive bullet lists

---

## Phase 3 — Systems

Systems are routines and mechanisms that support Domains (e.g. `morning-routine`, `weekly-review`, `monthly-finance-check`).

### Step 1 — Propose systems

For each domain, propose systems that would meaningfully support it, drawing on the coach's philosophy and what you now know about the user. Present the full proposed list and refine with the user. Get explicit approval before proceeding.

### Step 2 — Create placeholder files

Immediately after approval, create `/systems/{name}.md` for every approved system with a minimal placeholder:

```markdown
---
title: {System Name}
tags:
  - system
  - todo
status: todo
---

# {System Name}

*To be completed during setup.*
```

### Step 3 — Go deep on each system

For every system, ask the user about their current habits and context relevant to that system — enough to write something specific and actionable, not generic.

Ask one system at a time. **After each response, immediately write the full system file** before moving to the next. Remove the `todo` tag and `status: todo` once written.

If setup is resumed after an interruption, check for any system files still marked `status: todo` and continue from there.

Each completed `/systems/{name}.md` should:
- Reflect the user's actual routine and constraints
- Be practical and specific — not a generic template
- Be written in the coach's voice
- Stay lightweight — high-signal only
