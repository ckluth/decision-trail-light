# Adopting decision-trail-light in a new repo

Audience: an AI coding agent (or a human) about to adopt this workflow into a
target repository, on request from its owner. Read this fully before writing
anything into the target repo.

## 1. Confirm the shape the user wants

This template assumes the **flat** variant — everything under `docs\adr\` and
`docs\plans\`, no per-feature/per-PBI grouping. If the target project is
large enough that flat numbering will get unwieldy (many unrelated workstreams
sharing one `docs\adr\` sequence), say so and ask whether they'd rather nest
by feature/PBI instead (see "Provenance" below for the heavier variant this
was distilled from). Otherwise, proceed with flat.

Also confirm before writing:

- **Numbering scheme** — default is a global sequence per folder (`ADR-01,
  ADR-02, ...`; `plan-01, plan-02, ...`, independent of each other). This is
  almost always what's wanted; only ask if the user has hinted otherwise.
- **`docs\prompts\`** — optional and informal (a place to save a longer
  starter prompt as a file and point to it, instead of pasting it inline).
  Include it by default; drop it only if the user explicitly doesn't want it.

## 2. Files to place in the target repo

Copy from `template\` in this repo, preserving relative paths:

| Source | Target | Handling |
| --- | --- | --- |
| `template\AGENTS.md` | `AGENTS.md` (repo root) | Copy verbatim, then replace the `<Project Name>` title (first line) with the target repo's actual name. Nothing else needs changing — the rest is repo-agnostic. |
| `template\ARCHITECTURE.md` | `ARCHITECTURE.md` (repo root) | Only if the target repo doesn't already have one. Replace `<Project Name>` and `<YYYY-MM-DD>`, then fill in (or explicitly state "nothing built yet" for) the Overview/Components/Key conventions sections based on the target repo's actual current state. |
| `template\.github\copilot-instructions.md` | `.github\copilot-instructions.md` | Only if the target repo doesn't already have one (see step 3 if it does). Replace `<Project Name>` and every bracketed placeholder with real content reflecting the target codebase — build/test/lint commands, a short architecture summary, key conventions — before appending the "Working method" section as-is. |
| `template\.github\skills\decision-trail-adr\SKILL.md` | `.github\skills\decision-trail-adr\SKILL.md` | Copy verbatim, unmodified. |
| `template\.github\skills\decision-trail-plan\SKILL.md` | `.github\skills\decision-trail-plan\SKILL.md` | Copy verbatim, unmodified. |
| `template\.github\skills\decision-trail-correction\SKILL.md` | `.github\skills\decision-trail-correction\SKILL.md` | Copy verbatim, unmodified. |
| `template\.github\skills\finalize-session\SKILL.md` | `.github\skills\finalize-session\SKILL.md` | Copy verbatim, unmodified. |

Also ensure `docs\adr\`, `docs\plans\`, and (if wanted) `docs\prompts\` exist
in the target repo. Git doesn't track empty folders — it's fine to only
create them the first time a file is actually written into one; don't add
placeholder `.gitkeep` files unless the user asks for the folders to be
visible/tracked before that.

## 3. If the target repo already has some of these files

Never silently overwrite an existing `AGENTS.md`, `ARCHITECTURE.md`, or
`.github\copilot-instructions.md`. Instead:

- **Existing `AGENTS.md`** — show the user the "How we work" section from the
  template and ask whether to append it (as a new top-level section) or merge
  it with what's already there.
- **Existing `ARCHITECTURE.md`** — leave its content untouched; just confirm
  it has a `Last updated` line, and reference it from
  `copilot-instructions.md` as the source of truth.
- **Existing `copilot-instructions.md`** — leave the project-specific content
  (build/test/architecture) as-is; append the "Working method" section from
  the template so future sessions know about `AGENTS.md` and the skills.

Skills (`.github\skills\*`) are project-agnostic and safe to add outright; if
a skill of the same name already exists and differs, ask before replacing it.

## 4. After copying

- Sweep for any leftover `<...>` placeholder tokens and confirm none remain.
- Sanity-check the cross-references still make sense: `AGENTS.md` names the
  four skills, `copilot-instructions.md` points at `AGENTS.md` and
  `ARCHITECTURE.md`.
- Tell the user the workflow is installed and ready. A natural first real use
  is turning their next non-trivial request straight into an ADR.

## Provenance

This template was distilled from an internal `job-system` repo's heavier,
per-PBI decision-trail-light setup, which nests ADRs/Plans under
`docs\pbi-<nnnn>-<slug>\` (or `docs\feature-<nnnn>-<slug>\pbi-<nnnn>-<slug>\`
for cross-cutting work), numbers `NN` independently *within* each PBI's own
`adr\`/`plans\` folder, and includes a `finalize-pbi` skill that produces a
structured closing report (`final-summary.md`) for a specific backlog item.

This flattened variant removes PBI/feature grouping entirely — everything
lives directly under `docs\adr\` and `docs\plans\`, numbered as one global
sequence per folder — and renames `finalize-pbi` to `finalize-session`,
refocused on an informal summary plus keeping `ARCHITECTURE.md` current,
rather than a formal per-PBI closing document. If a target project later
grows enough workstreams that flat numbering becomes unwieldy, migrating to
the nested PBI/feature variant is a reasonable escalation — reintroduce
`docs\pbi-<nnnn>-<slug>\adr\`/`plans\` subfolders and restore a PBI-scoped
finalize skill at that point, rather than trying to shoehorn grouping into
the flat layout.
