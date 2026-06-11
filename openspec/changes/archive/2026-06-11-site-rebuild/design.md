## Context

The repo currently holds a single `index.html` that is the raw Claude Design first
draft: EB Garamond, JetBrains Mono, hex colours, sidebar layout. A fully redesigned
reference file exists in `docs/_brief/design_handoff_rossouw_ie/index.html` — vanilla
HTML/CSS/JS, no dependencies, fonts commented out for local preview. That file is the
implementation target. The vault's `index-rebuild.md` is the content target.

GitHub Pages with Jekyll native build is the hosting model. No local build tooling is
required for deployment; `git push` to `main` is sufficient.

## Goals / Non-Goals

**Goals:**
- Ship the brief's design pixel-accurately, with fonts enabled
- Replace all copy with vault `index-rebuild.md` content
- Wrap in the minimum Jekyll structure GitHub Pages requires
- Keep the implementation a single HTML file with inline or co-located CSS

**Non-Goals:**
- Multi-page routing (single page only)
- Blog or writing section
- External CSS files / asset pipeline
- Node.js, npm, or any build tooling
- Sass, PostCSS, or CSS preprocessors
- Client-side framework

## Decisions

### D1 — Keep inline styles; do not extract to separate CSS files

The brief is self-contained by design. Extracting CSS would add complexity (asset
passthrough config, link tags, cache busting) with no benefit for a single-page site.
All styles stay in `<style>` blocks inside the layout template.

### D2 — Minimal Jekyll: one layout, front matter on index

`_layouts/default.html` holds the full HTML shell (head, header, footer, scripts).
`index.html` uses `layout: default` front matter and provides only the `<main>`
content via a `{{ content }}` block. This is the least-friction Jekyll structure —
no plugins, no gems beyond `github-pages`, no custom config needed.

### D3 — Jekyll `_config.yml` is minimal

Only the fields GitHub Pages needs: `title`, `description`, `url`, `baseurl` (empty),
and `exclude` for non-page files. No theme, no plugins beyond what `github-pages` gem
provides automatically.

### D4 — Google Fonts loaded in the layout head

The brief's fonts (`Newsreader`, `IBM Plex Mono`, `IBM Plex Sans`) are currently in
commented-out `<link>` tags. They move into `_layouts/default.html` uncommented.
The `preconnect` hints stay for performance.

### D5 — Dark mode script runs inline in `<head>`

The theme toggle reads `localStorage` before first paint to avoid flash-of-wrong-theme.
This inline script stays in the layout `<head>`, as designed in the brief.

### D6 — Content sourced verbatim from vault `index-rebuild.md`

The rebuild note is the authoritative source. Any divergence between it and the brief's
`index.html` is resolved in favour of the vault. Key reconciled facts:
- "remotely since 2004" (was 2003 in old site)
- Aegir 2007–2011 (was 2012 in old site)
- NearForm payroll project: "DevOps and build pipelines" (was "micro-services platform")
- Wake Forest dropped from EHR list
- DataRobot row dropped from résumé table
- Formicary referenced once in intro prose, not in a separate callout

## Risks / Trade-offs

- **OKLCH colour support**: requires Chrome 111+, Firefox 113+, Safari 15.4+. Older
  browsers will render unstyled colours. Acceptable given the audience; no fallback
  needed.
- **Google Fonts dependency**: external request on every load. Trade-off accepted —
  Newsreader and IBM Plex Mono are central to the design identity.
- **`prefers-reduced-motion`**: the brief includes a blanket `transition-duration:
  0.001ms` override for this media query — keep it.

## Migration Plan

1. Write `_config.yml` (minimal)
2. Write `_layouts/default.html` (full HTML shell from brief, fonts uncommented,
   `{{ content }}` block where `<main>` content goes)
3. Rewrite `index.html` with front matter + `<main>` content from vault
   `index-rebuild.md`, using brief's component CSS classes
4. Update `.gitignore` for `_site/` and `.jekyll-cache/`
5. Push to `main`; verify GitHub Pages build succeeds

No rollback complexity — old `index.html` is in git history.

## Open Questions

- Contact section "digital purge" tone: vault flags this as an open decision. Keep
  the current wording for now; Adrian can revise separately.
- Aegir end year: vault notes it may be 2011 or 2012. `index-rebuild.md` uses 2011;
  use that.
