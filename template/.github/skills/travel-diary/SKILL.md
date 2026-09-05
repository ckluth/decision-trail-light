---
name: travel-diary
description: >-
    Add a dated chapter to docs\travel-diary.md — a guard-free, human-facing
    continuity log for handing a session off to a future one. Use when the
    user asks to log progress, add a travel-diary/log entry, or record where
    things stand — regardless of whether any ADR/Plan touched this session is
    settled.
---

# decision-trail-light: Travel diary

A single running, human-facing log for session-to-session continuity —
independent of ADR/Plan state. Unlike every other skill in this method, this
one is **guard-free**: no confirmation guard, no precondition, usable even
mid-work or on a purely exploratory session where nothing was decided.

This is not `finalize-session` in miniature: `finalize-session` closes out
**settled** decision-trail work (and keeps `ARCHITECTURE.md` current); the
travel diary is a cheap, forward-looking "where we left off" note that works
even when nothing is settled yet — or nothing was a decision at all.

## Trigger

Activate only when the user explicitly asks — e.g. "add a chapter to the
travel diary", "log this", "note where we are for next time". Never write to
it unprompted; it's not a task the agent volunteers on its own.

## Where it lives

`docs\travel-diary.md` — a single flat file directly under `docs\` (create it
on first use if it doesn't exist yet).

## Format

Prepend a new section at the **top** of the file (most recent first):

```markdown
## [YYYY-MM-DD]

- **Where we are:** <one or two sentences>
- **What we achieved:** <bullets, this session>
- **What is left:** <bullets, still open>
- **What is next:** <the immediate next step>

<Optional continuation brief: a short paragraph a cold-started future
session can read first to pick up with full context.>
```

Same-day entries are disambiguated `## [YYYY-MM-DD] (2)`, `(3)`, … in the
order they were added — never overwrite or merge same-day entries.

## Rules

- Append-only, like every other artifact in this method — never edit or
  delete a past chapter, only prepend a new one.
- No status, no cross-links, no numbering — it isn't part of the ADR/Plan
  family and has none of their machinery.
- It may reference an ADR/plan by name/number for context, but never carries
  decision content itself — a decision surfacing here belongs in an ADR, not
  in the diary.

Since it's guard-free, just write the chapter once asked — no need to state
intent and wait for approval first, unlike every other skill here.
