---
name: decision-trail-adr
description: >-
    Write, update, accept, reject, amend, or supersede an Architecture Decision
    Record (ADR) in this repo's docs\adr\ folder. Use when the user asks to
    record a decision, write/update an ADR, turns a prompt/idea straight into a
    decision, or wants to accept/reject/amend an existing one.
---

# decision-trail-light: ADR authoring

An ADR is the **decision** stage of `prompt → ADR → Plan` (see repo `AGENTS.md`
for the overview). It is the spec: a Plan never restates *what/why*, only *how*.

## Where it lives

`docs\adr\ADR-NN-<slug>.md` — flat, directly under `docs\adr\`. `NN` is
zero-padded, sequential **across the whole folder**, starting at `01` — pick
the next free number (`max(existing) + 1`), never reuse or derive it from a
Plan's number.

**Number-collision guard.** Before writing, re-enumerate `docs\adr\` and
verify the chosen filename isn't already in use — protects against a stale
listing or a number picked from memory/an earlier turn. If it collides
(e.g. a concurrent write since you last listed the folder), take the next
free number instead; never overwrite an existing ADR by reusing its number.

## Template

```markdown
# ADR-NN: <Title>

- Status: Proposed
- Date: <YYYY-MM-DD>
- Amends: <ADR-NN, if any — omit line otherwise>
- Amended by: <ADR-NN, if any — omit line otherwise>
- Supersedes: <ADR-NN, if any — omit line otherwise>
- Superseded by: <ADR-NN, if any — omit line otherwise>

## Context

<Why this decision is needed. If promoted directly from a user prompt,
summarize the prompt's intent here (or point at the saved file in
docs\prompts\, if the user saved one) — no separate idea file is written.>

## Proposed decision

<What was decided. Add "## Decision Drivers" / "## Considered Options"
sections above this one only when weighing real alternatives — skip them for
a straightforward call. Rename this heading to "## Decision" the moment
`Status` flips to `Accepted` — see "Heading tracks status" below.>

## Consequences

<What follows — positive and negative. Split into "**Positive**" /
"**Negative / Risks**" sub-headings when both are non-trivial.>

## Open Questions

| ID | Question | Status |
| --- | --- | --- |
| — | — | — |

(Use "None." in place of the table when there are no open questions. Rename
this heading to "## Resolved Questions" the moment every row is resolved —
see "Heading tracks resolution" below.)
```

- **Title line and filename slot must agree** (`ADR-03: ...` lives in
  `ADR-03-...md`).
- ADRs are append-only: a rejected/superseded/deprecated ADR is left in place,
  not deleted or rewritten.
- Accepting/rejecting an ADR is just flipping `Status:` in place — no new file.
- Only include the cross-link fields that apply — omit `Amends:`/`Amended
  by:`/`Supersedes:`/`Superseded by:` entirely when unused, rather than
  leaving them blank.
- A bug found **after** this ADR is `Accepted` and its Plan is `Done`? That's
  not a new/amending ADR by default — see the `decision-trail-correction`
  skill for the lighter, explicitly user-demanded patch path.

## Status vocabulary and transitions

| From | To | When | Requires |
| --- | --- | --- | --- |
| Proposed | Accepted | Both hard gates below pass | — |
| Proposed | Rejected | Considered, turned down before acceptance | — |
| Accepted | Superseded | A later ADR **fully replaces** this decision | The new ADR carries `Supersedes:` back to this one; this one gets `Superseded by:` |
| Accepted | Deprecated | Decision no longer applies (e.g. what it governed was removed), but nothing replaces it | Optional one-line reason appended to Consequences; no `Superseded by:` needed |

`Rejected`, `Superseded`, and `Deprecated` are **terminal** — never transition
further. A change of mind about any of them is always a **new** ADR, never a
reopening of the old one (append-only).

Use `Amends:`/`Amended by:` (not a status change) when a later ADR only
**refines or extends** this one's decision without reversing it — the amended
ADR's own `Status` doesn't change, it just gains an `Amended by:` link.
Reserve `Supersedes:`/`Superseded by:` (paired with flipping `Status:
Superseded`) for when a later ADR makes this one's decision obsolete outright.

**Heading tracks status.** While `Status: Proposed`, the decision section is
headed `## Proposed decision`; the moment `Status` flips to `Accepted`, rename
the heading to `## Decision` in the same edit. Status and heading always move
together — if you ever find them disagreeing, treat it as a bug to fix on
sight, not a stylistic detail.

**Heading tracks resolution.** While the "Open Questions" table has any
unresolved row, the section is headed `## Open Questions`; the moment every
row's `Status` is marked resolved (each folded into Context/Decision/
Consequences per the "Open-questions gate" below), rename the heading to
`## Resolved Questions` in the same edit. This is independent of the ADR's
own `Status` field — an ADR may have all questions resolved yet still sit at
`Status: Proposed` by choice; the section heading tracks the questions'
resolution, not the ADR's acceptance.

## Two hard gates (do not skip)

1. **Status-flip gate.** An ADR may stay `Proposed` indefinitely if nothing
   builds on it — that's fine. But the moment any next step builds on it
   (writing its Plan, starting the work it authorizes, drafting an amending
   ADR that assumes it), flip it to `Accepted` **first**. Never proceed while
   the governing ADR is still `Proposed`.
2. **Open-questions gate.** Nothing may be built on an ADR (Plan, amending
   ADR, implementation) while its "Open Questions"/"Resolved Questions" table
   has any unresolved row. Walk each open question with the user one at a
   time, fold the resolution into Context/Decision/Consequences, mark it
   resolved, rename the section heading to `## Resolved Questions` once every
   row is resolved, and only then flip `Status` to `Accepted`.

## Confirmation guard

Before creating or editing an ADR, or flipping its status, state the intended
scope in one line and wait for explicit approval — see repo `AGENTS.md`.
