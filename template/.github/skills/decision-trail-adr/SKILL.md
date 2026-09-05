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

## Template

```markdown
# ADR-NN: <Title>

- Status: Proposed
- Date: <YYYY-MM-DD>
- Amends: <ADR-NN, if any — omit line otherwise>

## Context

<Why this decision is needed. If promoted directly from a user prompt,
summarize the prompt's intent here (or point at the saved file in
docs\prompts\, if the user saved one) — no separate idea file is written.>

## Decision

<What was decided. Add "## Decision Drivers" / "## Considered Options"
sections above this one only when weighing real alternatives — skip them for
a straightforward call.>

## Consequences

<What follows — positive and negative. Split into "**Positive**" /
"**Negative / Risks**" sub-headings when both are non-trivial.>

## Open Questions

| ID | Question | Status |
| --- | --- | --- |
| — | — | — |

(Use "None." in place of the table when there are no open questions.)
```

- **Title line and filename slot must agree** (`ADR-03: ...` lives in
  `ADR-03-...md`).
- `Status` is one of `Proposed`, `Accepted`, `Rejected`, `Superseded`,
  `Deprecated`. ADRs are append-only: a superseded/rejected ADR is left in
  place, not deleted or rewritten; link forward/back (`Amends:` /
  `Amended by:`, `Superseded by:`).
- Accepting/rejecting an ADR is just flipping `Status:` in place — no new file.
- A bug found **after** this ADR is `Accepted` and its Plan is `Done`? That's
  not a new/amending ADR by default — see the `decision-trail-correction`
  skill for the lighter, explicitly user-demanded patch path.

## Two hard gates (do not skip)

1. **Status-flip gate.** An ADR may stay `Proposed` indefinitely if nothing
   builds on it — that's fine. But the moment any next step builds on it
   (writing its Plan, starting the work it authorizes, drafting an amending
   ADR that assumes it), flip it to `Accepted` **first**. Never proceed while
   the governing ADR is still `Proposed`.
2. **Open-questions gate.** Nothing may be built on an ADR (Plan, amending
   ADR, implementation) while its "Open Questions" table has any unresolved
   row. Walk each open question with the user one at a time, fold the
   resolution into Context/Decision/Consequences, mark it resolved, only then
   flip `Status` to `Accepted`.

## Confirmation guard

Before creating or editing an ADR, or flipping its status, state the intended
scope in one line and wait for explicit approval — see repo `AGENTS.md`.
