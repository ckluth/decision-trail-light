---
name: finalize-session
description: >-
    Close out a work session: write a brief, informal derived summary of what
    was done, and — the main goal — check ARCHITECTURE.md for entries this
    session's work has made obsolete or that now need updating. Use when the
    user asks to finalize, wrap up, or close out a session whose touched
    ADRs/Plans are settled.
---

# decision-trail-light: Finalizing a session

The closing step after `prompt → ADR → Plan` has run its course for this
session's work: produce a short trail-of-record for humans, and — the
**primary goal** — reconcile `ARCHITECTURE.md` against what actually changed.
It never restates or reinterprets what/why/how — those live in the ADRs/Plans;
this only derives a summary from them.

## Trigger

Activate when the user asks to finalize, close out, or wrap up the current
session's work. Do not activate it while any ADR/Plan touched this session is
still in flux — that's normal ADR/Plan work, not finalization.

## Precondition — do not skip

Every ADR touched this session is `Accepted`, `Rejected`, `Deprecated`, or
`Superseded` (none left `Proposed`), and every Plan touched this session that
implements an `Accepted` ADR is `Done` or deliberately `Abandoned`.

If a scan turns up any `Proposed` ADR or any `Draft`/`Active` Plan among the
ones touched this session, do not silently skip it and do not decide its
resolution yourself. Stop, list the unsettled document(s) by name/status, and
resolve each with the user — typically one of:

- **Withdraw finalization** — the work isn't actually done; the user continues
  the ADR/Plan work (via `decision-trail-adr`/`decision-trail-plan`) and
  finalization is deferred.
- **Set the ADR's `Status` to `Deprecated`** (or `Rejected`/`Superseded`, as
  fits) to consciously close it out without implementing it, and abandon any
  Plan that depended on it.

Only proceed to Step A once every document touched this session is in one of
the settled states above.

## Step A — brief session summary

Write a short, informal, derived summary of the session's outcome — a few
sentences or a handful of bullets, not a rigid multi-section report. Point at
the ADR(s)/Plan(s) involved (e.g. "ADR-04 / plan-03") rather than restating
their content. Ask the user where they'd like it recorded (e.g. posted in
chat only, appended to a changelog, or used as a PR/commit description) —
this skill does not mandate a fixed file or location for it, and skipping it
entirely is fine if the user doesn't want one.

## Step B — `ARCHITECTURE.md` reconciliation (the main goal)

1. Read `ARCHITECTURE.md` and compare it against this session's actual
   changes (the touched ADRs' Decisions/Consequences and Plans' outcomes).
2. If any documented statement is now stale, contradicted, or missing
   coverage of what this session introduced or removed, list the exact
   proposed edits (current statement → replacement) and ask the user for
   permission before touching the file.
3. Only after explicit approval, edit `ARCHITECTURE.md` — including its
   `Last updated` line.
4. If nothing is stale, say so explicitly and leave the file untouched — do
   not edit it just to have touched it.

## Confirmation guard

State the intended scope — writing the session summary (and where, if
anywhere); which `ARCHITECTURE.md` edits, if any, once identified — in one
line and wait for explicit approval before writing; see repo `AGENTS.md`.
