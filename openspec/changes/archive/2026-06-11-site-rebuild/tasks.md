## 1. Jekyll scaffold (REQ-001 – REQ-004)

- [x] 1.1 Write `_config.yml` with `title`, `description`, `url: https://adrian.rossouw.ie`, `baseurl: ""`, and `exclude` list
- [x] 1.2 Write `_layouts/default.html` containing the full HTML shell from the brief: `<head>` (meta, uncommented Google Fonts links, both `<style>` blocks, theme-toggle inline script), sticky `<header>` with wordmark + nav + theme toggle button, `{{ content }}` block, and `<footer>`
- [x] 1.3 Add `_site/` and `.jekyll-cache/` to `.gitignore`

## 2. New design in layout (REQ-005 – REQ-012)

- [x] 2.1 Copy design-token `<style>` block from brief into `_layouts/default.html` — all OKLCH variables, spacing scale, font stacks, font-size scale, line-height tokens, dark mode `[data-theme="dark"]` overrides
- [x] 2.2 Copy page-component `<style>` block from brief into `_layouts/default.html` — site-head, masthead, prose, epistemic, practice-list, project-list, career-list, contact-grid, site-foot, responsive breakpoints, reduced-motion rule
- [x] 2.3 Copy theme-toggle inline script from brief into `_layouts/default.html` `<head>` (reads `localStorage`, sets `data-theme` before paint, wires click handler on DOMContentLoaded)
- [x] 2.4 Implement sticky `<header class="site-head">` in layout: wordmark link (`#intro`), nav links (`#practice`, `#work`, `#career`, `#contact`), theme-toggle button with disc icon

## 3. Page content

- [x] 3.1 Add front matter to `index.html`: `layout: default`, `title`, `description`
- [x] 3.2 Write intro section (`#intro`): masthead with eyebrow, h1 with `.title-seam` span on "seam", deck with `::before` accent rule, byline; epistemic aside with Role/Location/Focus dl and note; `<hr class="rule-mark">`; intro prose from vault `index-rebuild.md`
- [x] 3.3 Write practice section (`#practice`): section-head kicker + h2; five-item `<ol class="practice-list">` from vault `index-rebuild.md`
- [x] 3.4 Write work section (`#work`): section-head with lede; four `<li class="project">` entries from vault `index-rebuild.md`
- [x] 3.5 Write career section (`#career`): section-head with lede; `<ul class="career-list">` from vault `index-rebuild.md`
- [x] 3.6 Write contact section (`#contact`): section-head; prose; `<div class="contact-grid">` with LinkedIn and GitHub cells
- [x] 3.7 Write `<footer class="site-foot">`: site name, typeset credit (Newsreader & IBM Plex Mono), copyright

## 4. Verify

- [x] 4.1 Confirm Google Fonts `<link>` tags are uncommented in `_layouts/default.html`
- [x] 4.2 Confirm `.gitignore` includes `_site/` and `.jekyll-cache/`
