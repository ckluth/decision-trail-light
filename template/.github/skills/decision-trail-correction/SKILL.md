---
name: decision-trail-correction
description: >-
    Patch a small correction directly into an already-Accepted ADR and its
    already-Done Plan, after implementation, without reopening the decision,
    flipping status, or writing a new amending ADR/fix-plan. Use only when the
    user explicitly demands a "correction"/"patch" to a settled ADR/Plan pair
    — typically after a real bug surfaced in already-shipped work that ADR
    governs.
---

# decision-trail-light: Post-Implementation Correction

A lightweight escape hatch for **settled** documents: when an `Accepted` ADR's
`Done` Plan turns out to have a real defect, patch both files in place instead
of paying for a full amending-ADR + new fix-plan cycle.

## Trigger

Activate **only** when the user explicitly asks to patch/correct a settled
ADR/Plan directly (e.g. "just patch the ADR", "correct this in place", "fix
the plan without a new plan"). Never activate this on your own initiative
just because a bug was found — by default, ask whether the user wants an
amending ADR + its own plan (the normal, heavier path) or this lighter patch;
use this skill only once they've explicitly chosen the patch.

## Precondition

- Governing ADR: `Status: Accepted`.
- Every Plan implementing it (`Implements: ADR-NN`) that this correction
  touches: `Status: Done`.

If either isn't settled yet (ADR still `Proposed`, or its Plan still `Draft`/
`Active`), this is not a correction — just edit the ADR/Plan directly through
the `decision-trail-adr` / `decision-trail-plan` skills instead.

## Scope boundary — what actually qualifies

A correction fixes an **execution or description defect** in what was already
decided — a bug, an inaccurate implementation detail, a wrongly-assumed fact —
**without** changing the substance of any `Decision` bullet. If the real fix
would mean deciding something differently (a different approach, not just a
more faithful execution of the same one), say so and recommend an amending
ADR + its own plan instead. Patch anyway only if the user insists after
hearing that.

## What to change — the ADR

Append a new section — never insert mid-document — directly after
`## Consequences` (and after any earlier corrections), and before any
`## Non-Goals` / `## Open Questions` / `## Resolved Questions` trailer:

```markdown
## Post-Implementation Correction #N (YYYY-MM-DD)

<What was wrong — name the specific Decision # it relates to.>

<How it surfaced — the concrete symptom/failure that revealed it.>

**Resolution**: <the fix — name exact files/methods changed>. No other
Decision in this ADR is affected.
```

- `N` is sequential per ADR, starting at 1.
- `Status`, `Date`, and every existing `Decision`/`Consequences` bullet stay
  untouched — a correction is strictly additive.

## What to change — the Plan

Find the step whose `Action` produced the now-corrected behavior. Append an
inline callout directly under that step's existing content — its checkbox
stays `[x]`, unchanged:

```markdown
**Post-Implementation Correction (YYYY-MM-DD)**: <what changed and why, in
1-3 sentences>. See ADR-NN's "Post-Implementation Correction #N" for the full
record.
```

Do not add a new task, uncheck the step, or reopen the plan's `Status`
(`Done` stays `Done`).

## Confirmation guard

State the intended scope — which ADR, which correction number, which plan
step — in one line and wait for explicit approval before patching; see repo
`AGENTS.md`.
