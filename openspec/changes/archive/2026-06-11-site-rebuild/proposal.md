## Why

The live site is the original Claude Design draft: old fonts, old colours, old layout,
and several factual errors (remote since 2003, wrong Aegir end year, stale NearForm
project framing). The design brief produced a high-fidelity redesign with corrected
content that has never been published. This change ships that design and reconciles
all copy against the vault's authoritative `index-rebuild.md`.

Separately, the repo has no Jekyll structure — GitHub Pages is serving a raw HTML
file. Wrapping it in minimal Jekyll gives us front matter, a proper `_config.yml`,
and a foundation for any future templating without introducing a build step or
external tooling.

## What Changes

- **Design**: replace EB Garamond + JetBrains Mono palette and sidebar layout with
  the Newsreader + IBM Plex Mono redesign from `docs/_brief/` (OKLCH oxblood colours,
  sticky header, dark mode toggle, epistemic status callout)
- **Content**: apply all corrections from vault `index-rebuild.md` — remote since 2004,
  Aegir 2007–2011, NearForm payroll entry reframed as DevOps/build pipelines, Wake
  Forest dropped, DataRobot dropped from résumé, Formicary referenced once in intro
- **Jekyll**: add `_config.yml`, `_layouts/default.html`, convert `index.html` to a
  Jekyll page with front matter; update `.gitignore` for Jekyll artefacts (`_site/`,
  `.jekyll-cache/`)
- **Fonts**: uncomment the Google Fonts `<link>` tags (currently commented out in the
  brief's HTML, required for production)

## Capabilities

### New Capabilities

- `jekyll-structure`: minimal Jekyll scaffold (`_config.yml`, `_layouts/default.html`,
  front matter on `index.html`) enabling GitHub Pages native build
- `new-design`: full visual implementation of the brief — Newsreader + IBM Plex Mono,
  OKLCH tokens, dark mode, sticky header, epistemic callout replacing the status card

### Modified Capabilities

<!-- none — this is the first versioned implementation; no prior specs exist -->

## Impact

- `index.html` is rewritten entirely — old design and old copy are replaced
- `_config.yml` and `_layouts/default.html` are new files
- `.gitignore` gains Jekyll-specific entries
- `docs/_brief/` is read-only reference; not modified
- No URL changes; GitHub Pages continues to serve from repo root
- Visitors see the new design immediately on next deploy
