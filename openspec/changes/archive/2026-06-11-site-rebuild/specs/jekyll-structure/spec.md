## ADDED Requirements

### Requirement: REQ-001 Jekyll config exists
The repository SHALL contain a `_config.yml` at the root with at minimum `title`,
`description`, `url`, and an empty `baseurl`. No theme key SHALL be set.

#### Scenario: Config is valid
- **WHEN** GitHub Pages processes the repository
- **THEN** it finds `_config.yml` and builds without error

### Requirement: REQ-002 Default layout wraps all pages
A file at `_layouts/default.html` SHALL contain the full HTML shell: `<!doctype html>`,
`<head>` (meta, fonts, styles, theme script), sticky `<header>`, `{{ content }}`, and
`<footer>`. All pages SHALL reference it via `layout: default` front matter.

#### Scenario: Layout renders head correctly
- **WHEN** any page using `layout: default` is built
- **THEN** the output contains `<meta charset="utf-8">`, the Google Fonts `<link>`
  tags (uncommented), and the theme-toggle inline script

#### Scenario: Content block is injected
- **WHEN** `index.html` is built with `layout: default`
- **THEN** the `<main>` content from `index.html` appears inside the rendered shell

### Requirement: REQ-003 index.html uses front matter
`index.html` at the repo root SHALL have a YAML front matter block specifying at
minimum `layout: default`, `title`, and `description`.

#### Scenario: Front matter is present
- **WHEN** `index.html` is opened
- **THEN** the first line is `---` and a `layout: default` key is present

### Requirement: REQ-004 Jekyll artefacts are gitignored
`.gitignore` SHALL include `_site/` and `.jekyll-cache/` so build output is never
committed to the repository.

#### Scenario: Build output is not tracked
- **WHEN** `git status` is run after a local Jekyll build
- **THEN** files under `_site/` and `.jekyll-cache/` are not listed
