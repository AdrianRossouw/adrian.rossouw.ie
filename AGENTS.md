# adrian.rossouw.ie — agent guidance

## Project

Personal site and blog for Adrian Rossouw at `https://adrian.rossouw.ie`.
Currently a single-page HTML/CSS site — no build step, no Jekyll, no framework.
Deploy: push to `main`; GitHub Pages serves from root.

Primary file: `index.html` — all markup and styles live here.

Design tokens are defined in the `:root` block inside `index.html`'s `<style>` tag.
Do not hardcode colour, spacing, or type values elsewhere; always use CSS variables.
Typefaces: EB Garamond (serif body) and JetBrains Mono (labels, metadata, code).

Requirements are in `docs/requirements.md` (REQ-001 onwards).
Traceability is in `docs/traceability.md`.

Specs for new pages or significant components go in `docs/specs/` before
implementation. Specs are plain Markdown: intent, structure, states, and API shape
if relevant. Spec-first applies to anything non-trivial.

## Commit convention

Every commit that **implements or modifies** a requirement must reference the
relevant REQ-IDs in the subject scope. This applies to **all** commit types —
`feat`, `fix`, `refactor`, `test`, `docs` — not only `feat`.

```
feat(REQ-003,REQ-004): add writing section with post listing
fix(REQ-007): correct scrollspy offset on mobile
refactor(REQ-002,REQ-010): extract design tokens to shared file
```

**chore:** commits that touch only task-tracking files (tasks.md, AGENTS.md,
CLAUDE.md, .gitignore) do not need REQ-IDs.

**Finding the right REQ-IDs:** scan the diff — every file you touch maps to one
or more requirements. Cross-reference `docs/requirements.md` for the IDs. Err
on the side of including more rather than fewer; missing an ID is a traceability
gap, an extra one is not.

**Subjects describe the change, not the tool.** Never write "per /simplify
findings" or "via /code-review" in a subject line — those are session artefacts,
not meaningful history.

## Branch discipline

Every change goes on a named branch. Merge to `main` with `--no-ff`.

```
git checkout -b feat/writing-section
# ... make changes ...
git checkout main
git merge --no-ff feat/writing-section
```

Branch prefix matches the commit type: `feat/`, `fix/`, `refactor/`, `docs/`,
`test/`, `chore/`.

Direct commits to `main` are only permitted for the repository's very first
commit and for single-line chore entries that touch only task-tracking files.
Maintenance work (refactors, simplification passes, test additions) still gets
a branch and a merge commit — the branch name is what links the work to a unit
of intent in the log.

## Pre-commit checklist

Before every `git commit` that touches implementation files:

1. Am I on a named branch (not `main`)?
2. Does the subject follow `type(REQ-NNN,...): imperative description`?
3. Does the REQ-ID list cover every requirement whose implementing files appear
   in `git diff --stat`? (grep `docs/requirements.md` if unsure)
4. Is the subject under ~72 characters?
5. Does the subject describe the *what*, not the tool or session that prompted it?
