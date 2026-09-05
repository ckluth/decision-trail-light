# <Project Name>

## How we work: decision-trail-light

Non-trivial work is carried **prompt → ADR → Plan**, in plain markdown under
`docs\`. This is a light, repo-local method — a deliberately-shrunk relative of
[decision-trail](https://github.com/haevg-rz/decision-trail), keeping only what
earns its overhead: an **ADR**, an **Implementation Plan**, and the
**confirmation guard** below. No idea files, no derived index, no travel diary.

- **A prompt that asks for a decision goes straight to an ADR.** There is no
  separate "idea" artifact — if the user demands a decision, write the ADR
  directly (`Status: Proposed`), summarizing the prompt's intent in its Context.
- **An ADR is the spec; a Plan carries it into action.** A Plan may only be
  written against an ADR that is `Accepted` with zero unresolved rows in its
  "Open Questions" table.
- How-to and templates are in the skills below — loaded only when the task
  actually needs them:
  - **`decision-trail-adr`** — writing, updating, accepting/rejecting an ADR.
  - **`decision-trail-plan`** — writing/executing an Implementation Plan.
  - **`decision-trail-correction`** — patching a small, post-implementation
    fix directly into an already-settled (Accepted ADR + Done Plan) pair,
    when the user explicitly demands it instead of a full amending ADR.
  - **`finalize-session`** — closing out a session's work: a brief, informal
    derived summary, plus keeping `ARCHITECTURE.md` up to date (the main goal).

### `docs\` layout

Everything lives **flat**, directly under `docs\` — no per-PBI or per-feature
subfolders:

```
docs\
    adr\ADR-NN-<slug>.md
    plans\plan-NN-<slug>.md
    prompts\<slug>.md        (optional, informal — see below)
```

`NN` is a zero-padded, **global** sequence per folder (`docs\adr\`,
`docs\plans\`) — ADRs and Plans are numbered independently of each other:
pick the next free number (`max(existing) + 1`) in that folder. Numbers are
never reused or derived from the other folder's numbering.

`docs\prompts\` is informal and optional, purely for the user's convenience: a
session may start directly from a quick typed/pasted prompt, or the user may
instead save a longer starter prompt as `docs\prompts\<slug>.md` and point to
that file. In most cases the goal is still to turn it into a clean ADR — but a
starter prompt may also be a quick side-task with no decision-trail overhead
at all; don't force one where the user didn't ask for it.

### Confirmation guard

Never write, edit, or implement an ADR/Plan step without saying first — in one
short sentence — exactly what you're about to do, then waiting for explicit
approval. A bare "yes"/"ok" approves only the named scope, not a larger batch;
if in doubt, ask which.
