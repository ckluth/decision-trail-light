# decision-trail-light (template)

A minimal, repo-local **`prompt → ADR → Plan`** documentation workflow for
agent-driven development — lightweight enough to actually get used,
structured enough to leave a real decision trail behind.

This repo is **not** a GitHub template repo to fork or generate from. It's a
reference package for an AI agent (or a human) to read and *adopt into a
target project* by copying/adapting its files there. Point an agent at this
repo plus `GUIDE.md` and ask it to adopt the workflow into your project.

## Contents

- **`GUIDE.md`** — step-by-step adoption instructions for the agent doing the
  adopting, including what to customize vs. copy verbatim, and how to handle
  a target repo that already has some of these files.
- **`template\AGENTS.md`** — the method itself: `docs\` layout, numbering,
  the confirmation guard.
- **`template\ARCHITECTURE.md`** — architecture-doc stub.
- **`template\.github\copilot-instructions.md`** — Copilot entry-point
  template.
- **`template\.github\skills\`** — the five skills: `decision-trail-adr`,
  `decision-trail-plan`, `decision-trail-correction`, `finalize-session`,
  `travel-diary`.

## The method, in one paragraph

Non-trivial requests become an ADR (`docs\adr\ADR-NN-<slug>.md`, `Status:
Proposed` → `Accepted`), which is then carried into action by an
Implementation Plan (`docs\plans\plan-NN-<slug>.md`) once the ADR is
`Accepted` and has no open questions. Both live **flat** under `docs\` — no
per-feature/per-PBI folders. A confirmation guard requires stating the exact
scope before writing, editing, or executing any step.

See **`GUIDE.md`** for how to adopt this into a new repo.
