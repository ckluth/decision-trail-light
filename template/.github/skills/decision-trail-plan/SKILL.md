---
name: decision-trail-plan
description: >-
    Write or execute an Implementation Plan that carries an Accepted ADR into
    action, in this repo's docs\plans\ folder. Use when the user asks to plan
    the execution of a decision, break an ADR into steps, or work through/tick
    off an existing plan's tasks.
---

# decision-trail-light: Plan authoring & execution

A Plan is the **how**: mechanical execution of an already-`Accepted` ADR (the
**decision** stage of `prompt → ADR → Plan`, see repo `AGENTS.md`). It never
restates what/why — that lives in the ADR.

## Trigger

Activate this skill when the user asks to:

- plan the execution of an (accepted) ADR / decision,
- break an ADR down into steps, write an implementation plan,
- work through, execute, or tick off an existing plan's tasks.

Do not activate it for a request that only wants a decision recorded (use
`decision-trail-adr` instead), or a brief outline/brainstorm with no intent to
execute step by step. If the user wants a small fix patched directly into an
already-`Done` plan for an already-`Accepted` ADR (not a fresh plan), use
`decision-trail-correction` instead.

## Precondition — do not skip

Before writing a Plan, confirm its governing ADR is `Accepted` **and** its
"Open Questions" table has zero unresolved rows. If not, stop and resolve that
in the ADR first (see the `decision-trail-adr` skill) — do not fold an
undecided question into the Plan as a task.

## Where it lives

`docs\plans\plan-NN-<slug>.md` — flat, directly under `docs\plans\`. `NN` is
zero-padded, sequential **across the whole folder**, independent of the ADR's
own numbering — a plan implementing `ADR-03` is not necessarily `plan-03`.
Pick the next free number (`max(existing) + 1`) in `docs\plans\`.

## Template

```markdown
# Plan-NN: <Title>

- Status: Draft
- Implements: ADR-NN (`docs\adr\ADR-NN-<slug>.md`)

## Facts this plan relies on

<Facts/inputs/decisions already established by the ADR (or verified by direct
inspection) that steps below may rely on without re-verifying — name exact
files, APIs, versions, config values. Nothing here may contradict or extend
the ADR; if a needed fact isn't settled, return to the decision stage first.>

## Execution Mode

- **Step-by-step mode:** execute one step, check its acceptance criteria,
  report the result, wait for explicit confirmation before the next step.
- **Batch mode:** execute all steps in order, checking each step's acceptance
  criteria before continuing.

State which mode is in use before starting execution.

## Tasks

- [ ] Step 1: <imperative, atomic goal>
      Action: <exact files/commands/edits — name them, don't paraphrase>
      Acceptance criteria: <objective, observable condition(s)>
      Stop and ask for clarification if: <specific ambiguity that would block this step>
- [ ] Step 2: <imperative, atomic goal>
      Action: <...>
      Acceptance criteria: <...>
      Stop and ask for clarification if: <...>

## Completion Criteria

- <end-to-end observable outcome>
- <required validation/tests have passed>
- <docs or handoff updated, when applicable>
```

- `Status` is one of `Draft`, `Active`, `Done`, `Abandoned`. Execution is the
  plan in motion: `Draft` → `Active` while ticking `- [ ]` → `- [x]`, → `Done`
  when all steps are done **and** Completion Criteria are met, or `Abandoned`
  if dropped (leave it in place — plans are append-only).
- Steps are numbered, atomic (one coherent outcome each), and normally
  sequential/strictly ordered; say so explicitly if a plan allows reordering
  or parallel steps. Do not include discovery/investigation/"determine" steps
  — unresolved facts belong in the ADR (decision stage), not the plan.
- A plan may be executed **step-by-confirmed-step or in one batch** — either
  is fine; the mode is recorded in the plan's own `## Execution Mode` section
  so a later, cold-started session can tell which was chosen.

## Hard rule — plans are mechanical execution only

A task is never "decide X" or "clarify open question Y". Each step's own
"Stop and ask for clarification if" is the mechanism for this: when it's met,
or an expected precondition/fact is absent, or a target differs from the
plan, **stop immediately** — do not improvise, guess, or fold a decision into
the plan. Return to the decision stage: patch, amend, or open a new ADR to
settle it (via the `decision-trail-adr` skill), then resume execution against
the updated spec.

When executing: re-read the step, its acceptance criteria, and its stop
condition before acting; ask one focused question naming the blocking
condition rather than proposing or assuming an answer.

## Confirmation guard

Before creating/editing a Plan, starting execution, or ticking off steps,
state the intended scope in one line (e.g. "this single step" vs. "the whole
batch") and wait for explicit approval — see repo `AGENTS.md`.
