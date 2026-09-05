# Copilot Instructions for <Project Name>

## Build, test & lint

<Replace this section with the project's real build/test/lint commands,
including how to run a single test — not just the full suite. If the project
has no code yet, say so explicitly instead of leaving this placeholder.>

## Architecture

<Replace with a short "big picture" summary — the parts of the system that
require reading multiple files to understand. `ARCHITECTURE.md` at the repo
root is the detailed, authoritative reference; this section is just a
pointer/teaser, kept in sync with it.>

## Key conventions

<Patterns specific to this codebase that aren't obvious from reading a single
file.>

## Working method: decision-trail-light (`prompt → ADR → Plan`)

The repo root **`AGENTS.md`** is the entry point for how work here is carried
out: non-trivial requests are turned into an **ADR** (`docs\adr\`) and then an
**Implementation Plan** (`docs\plans\`), both flat markdown files directly
under `docs\` (no per-feature/per-PBI subfolders). Read `AGENTS.md` first —
it also defines the confirmation guard that governs writing/editing these
documents.

The how-to and templates live in skills under `.github\skills\` — read the
relevant one before creating or editing any ADR, Plan, correction, or session
summary:

- **`decision-trail-adr`** — writing/updating/accepting/rejecting an ADR.
- **`decision-trail-plan`** — writing or executing an Implementation Plan.
- **`decision-trail-correction`** — patching a small fix directly into an
  already-settled (Accepted ADR + Done Plan) pair, only when the user
  explicitly asks for a patch instead of a full amending ADR.
- **`finalize-session`** — closing out a session: a brief informal summary,
  plus reconciling `ARCHITECTURE.md` (the main goal of finalizing).
- **`travel-diary`** — a guard-free, dated continuity log for handing a
  session off to the next one, independent of ADR/Plan status.

`ARCHITECTURE.md` at the repo root is the authoritative architecture
reference — keep it in sync with any change that affects a statement it
documents.
