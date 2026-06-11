## ADDED Requirements

### Requirement: REQ-005 Design tokens match the brief exactly
The CSS custom properties in the layout `<style>` block SHALL match the values in
`docs/_brief/design_handoff_rossouw_ie/README.md` exactly: OKLCH colour tokens,
spacing scale (`--space-1` through `--space-9`), font stacks, font-size scale, and
line-height tokens.

#### Scenario: Accent colour is oxblood
- **WHEN** the rendered page is inspected
- **THEN** `--accent` resolves to `oklch(0.405 0.135 22)` in light mode

#### Scenario: Dark mode tokens are applied
- **WHEN** `data-theme="dark"` is set on `<html>`
- **THEN** `--paper` resolves to `oklch(0.188 0.013 30)`

### Requirement: REQ-006 Newsreader and IBM Plex Mono are loaded
The layout `<head>` SHALL include uncommented `<link rel="preconnect">` and
`<link rel="stylesheet">` tags for Newsreader, IBM Plex Mono, and IBM Plex Sans
from Google Fonts, with the axes and weights specified in the brief.

#### Scenario: Font links are present and enabled
- **WHEN** the page HTML is inspected
- **THEN** three font `<link>` tags pointing to `fonts.googleapis.com` are present
  and not commented out

### Requirement: REQ-007 Sticky header with wordmark and nav
The page SHALL have a `<header class="site-head">` that is `position: sticky; top: 0`
containing the wordmark (serif, links to `#intro`) and a `<nav>` with anchor links to
`#practice`, `#work`, `#career`, and `#contact`. The nav SHALL be hidden on viewports
≤ 640px.

#### Scenario: Header sticks on scroll
- **WHEN** the user scrolls past the masthead
- **THEN** the header remains visible at the top of the viewport

#### Scenario: Nav hidden on mobile
- **WHEN** viewport width is ≤ 640px
- **THEN** the `.nav` element has `display: none`

### Requirement: REQ-008 Dark mode toggle is functional
A `<button data-theme-toggle>` SHALL appear in the header. Clicking it SHALL toggle
`data-theme="dark"` on `<html>` and persist the preference to `localStorage` under
the key `rossouw-theme`. An inline script in `<head>` SHALL restore the saved
preference before first paint.

#### Scenario: Toggle persists across reload
- **WHEN** the user activates dark mode and reloads the page
- **THEN** dark mode is applied before any paint (no flash)

#### Scenario: Toggle button reflects current state
- **WHEN** light mode is active
- **THEN** the button's `aria-label` is "Switch to dark theme"

### Requirement: REQ-009 Masthead matches brief
The masthead SHALL contain: eyebrow kicker (IBM Plex Mono, role + location), `<h1>`
with fluid size `clamp(2.65rem, 6.4vw, 3.7rem)` and the word "seam" in
`<span class="title-seam">` coloured `var(--accent)`, deck paragraph with `::before`
accent rule, and byline in IBM Plex Mono.

#### Scenario: Seam is accented
- **WHEN** the page is rendered
- **THEN** the word "seam" in the h1 is wrapped in `.title-seam` and coloured `var(--accent)`

### Requirement: REQ-010 Epistemic status callout replaces status card
The intro section SHALL contain an `<aside class="epistemic">` with a label, a `<dl>`
of structured fields (Role, Location, Focus), and a note paragraph. It SHALL NOT use
the old `.status-card` pattern.

#### Scenario: Epistemic aside is present
- **WHEN** the intro section is rendered
- **THEN** an element with class `epistemic` exists containing a `<dl>` with at least
  three `<dt>`/`<dd>` pairs

### Requirement: REQ-011 Text selection uses accent tint
The `::selection` pseudo-element SHALL use `background: var(--accent-tint)` and
`color: var(--ink)`.

#### Scenario: Selection styling is defined
- **WHEN** the page CSS is inspected
- **THEN** a `::selection` rule with `background: var(--accent-tint)` is present

### Requirement: REQ-012 Reduced motion respected
A `@media (prefers-reduced-motion: reduce)` block SHALL set
`animation-duration: 0.001ms` and `transition-duration: 0.001ms` on all elements.

#### Scenario: Reduced motion rule exists
- **WHEN** the page CSS is inspected
- **THEN** a `prefers-reduced-motion: reduce` media query is present
