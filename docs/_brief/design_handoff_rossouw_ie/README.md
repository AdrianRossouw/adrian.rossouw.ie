# Handoff: adrian.rossouw.ie

## Overview

Personal portfolio and CV site for Adrian Rossouw — VP Information Systems & Product, Dublin. Single-page scrolling document: masthead, epistemic status callout, intro prose, practice list, project entries, career table, contact grid, footer. No blog, no CMS, no routing.

## About the Design Files

`index.html` in this bundle is a **high-fidelity design reference built in plain HTML/CSS/JS**. It is also essentially production-ready — there is no framework, no build step, no dependencies beyond two Google Font families. The implementation task is:

1. Uncomment the Google Fonts `<link>` tags (marked clearly in `<head>`)
2. Deploy to a static host (Netlify, Vercel, Cloudflare Pages, etc.)
3. Point `adrian.rossouw.ie` at it

If you want to port it to a static site generator (Eleventy, Astro, Hugo) or a framework, all the design tokens and component patterns are documented below so you can recreate them faithfully.

## Fidelity

**High-fidelity.** Every colour, typographic scale step, spacing value, interaction state, and piece of copy is final. Recreate pixel-accurately.

---

## Architecture

- **Stack:** Vanilla HTML5 + CSS custom properties + ~60 lines of vanilla JS (theme toggle only). No framework, no bundler, no npm.
- **Single file:** Everything lives in `index.html`. Two `<style>` blocks — the first holds design tokens and global primitives, the second holds page-specific component styles.
- **Dark mode:** Opt-in (light is default). Toggled by a button with `data-theme-toggle`. State persisted to `localStorage` under the key `rossouw-theme`. Applied by setting `data-theme="dark"` on `<html>`. The toggle script runs inline in `<head>` before paint to avoid flash.

---

## Design Tokens

### Typography

```
Serif:  Newsreader — Google Fonts
        ital,opsz,wght@0,6..72,400..600;1,6..72,400..500
Mono:   IBM Plex Mono — Google Fonts
        ital,wght@0,400;0,500;0,600;1,400
Sans:   IBM Plex Sans (minimal use — system fallback fine)
        wght@0,400;0,500;0,600
```

Font-size scale (all `rem`, base `16px`):

| Token          | Value       | px equiv |
|----------------|-------------|----------|
| `--fs-micro`   | `0.6875rem` | 11 px    |
| `--fs-mono`    | `0.75rem`   | 12 px    |
| `--fs-meta`    | `0.8125rem` | 13 px    |
| `--fs-sm`      | `0.9375rem` | 15 px    |
| `--fs-base`    | `1.1875rem` | 19 px    |
| `--fs-lead`    | `1.375rem`  | 22 px    |
| `--fs-h3`      | `1.5rem`    | 24 px    |
| `--fs-h2`      | `1.9375rem` | 31 px    |
| `--fs-h1`      | `2.75rem`   | 44 px    |
| `--fs-display` | `3.5rem`    | 56 px    |

The masthead `<h1>` uses a fluid size: `clamp(2.65rem, 6.4vw, 3.7rem)`.

Line-height tokens:

| Token        | Value |
|--------------|-------|
| `--lh-tight` | 1.18  |
| `--lh-snug`  | 1.35  |
| `--lh-body`  | 1.72  |
| `--lh-meta`  | 1.5   |

### Colour — Oxblood scheme

All colours use OKLCH. Modern browsers (Chrome 111+, Firefox 113+, Safari 15.4+) support this natively. If you need hex fallbacks, use `color-mix()` or a PostCSS plugin.

**Light mode** (default):

| Token            | OKLCH value              | Notes                        |
|------------------|--------------------------|------------------------------|
| `--paper`        | `oklch(0.988 0.004 40)`  | Warm off-white background    |
| `--paper-sunk`   | `oklch(0.968 0.006 40)`  | Recessed panels              |
| `--paper-raise`  | `oklch(0.998 0.002 40)`  | Elevated surfaces            |
| `--ink`          | `oklch(0.248 0.014 35)`  | Primary text                 |
| `--ink-soft`     | `oklch(0.398 0.012 35)`  | Secondary text               |
| `--ink-mute`     | `oklch(0.540 0.010 30)`  | Captions, bylines            |
| `--ink-faint`    | `oklch(0.660 0.008 30)`  | Disabled / very quiet        |
| `--rule`         | `oklch(0.888 0.008 40)`  | Standard dividers            |
| `--rule-soft`    | `oklch(0.928 0.005 40)`  | Lighter dividers             |
| `--accent`       | `oklch(0.405 0.135 22)`  | Oxblood red — primary accent |
| `--accent-deep`  | `oklch(0.335 0.130 22)`  | Hover / deeper accent        |
| `--accent-tint`  | `oklch(0.958 0.024 22)`  | Selection highlight          |
| `--accent-rule`  | `oklch(0.698 0.090 22)`  | Accent-toned dividers        |

**Dark mode** (applied via `[data-theme="dark"]` on `<html>`):

| Token            | OKLCH value              |
|------------------|--------------------------|
| `--paper`        | `oklch(0.188 0.013 30)`  |
| `--paper-sunk`   | `oklch(0.228 0.015 30)`  |
| `--paper-raise`  | `oklch(0.218 0.014 30)`  |
| `--ink`          | `oklch(0.930 0.009 40)`  |
| `--ink-soft`     | `oklch(0.778 0.011 40)`  |
| `--ink-mute`     | `oklch(0.622 0.012 30)`  |
| `--ink-faint`    | `oklch(0.502 0.012 30)`  |
| `--rule`         | `oklch(0.322 0.018 30)`  |
| `--rule-soft`    | `oklch(0.272 0.015 30)`  |
| `--accent`       | `oklch(0.740 0.150 20)`  |
| `--accent-deep`  | `oklch(0.810 0.130 20)`  |
| `--accent-tint`  | `oklch(0.295 0.048 22)`  |
| `--accent-rule`  | `oklch(0.520 0.100 22)`  |

### Spacing

```
--space-1: 0.25rem    --space-2: 0.5rem    --space-3: 0.75rem
--space-4: 1rem       --space-5: 1.5rem    --space-6: 2rem
--space-7: 3rem       --space-8: 4.5rem    --space-9: 7rem
```

### Layout

```
--measure:      62ch           (max line width)
--measure-wide: 74ch
--page-pad:     clamp(1.25rem, 5vw, 3rem)
--radius:       3px
```

The `.shell` class centres content:
```css
max-width: calc(var(--measure) + var(--page-pad) * 2);
margin-inline: auto;
padding-inline: var(--page-pad);
```

---

## Sections

### 1. Sticky Header (`.site-head`)

- `position: sticky; top: 0; z-index: 20`
- `background: color-mix(in oklch, var(--paper) 88%, transparent)` with `backdrop-filter: saturate(1.1) blur(6px)`
- `border-bottom: 1px solid var(--rule)`
- Row: **wordmark** (serif, 500 weight, 1.35rem, `--ink`) left, **nav + theme toggle** right
- Nav links: IBM Plex Mono, `--fs-micro`, `letter-spacing: 0.16em`, uppercase, `--ink-faint` default, `--ink` on hover with a bottom border, `--ink` + `border-bottom: 1px solid var(--accent)` on active
- Theme toggle: 30×30px circle button, `border: 1px solid var(--rule)`, half-filled disc icon (`linear-gradient(90deg, var(--ink-soft) 50%, transparent 50%)`)

### 2. Masthead (`.masthead`)

- `padding-top: var(--space-8)` (desktop), `var(--space-5)` (≤640px)
- **Eyebrow** (`.masthead__eyebrow`): kicker class — IBM Plex Mono, `--fs-mono`, `letter-spacing: 0.13em`, uppercase, `--ink-mute`
- **H1** (`.masthead__title`): Newsreader, `clamp(2.65rem, 6.4vw, 3.7rem)`, weight 560, `lh-tight`, `letter-spacing: -0.022em`, `max-width: 16ch`, `text-wrap: balance`. The word **"seam"** is wrapped in `<span class="title-seam">` and coloured `var(--accent)` — this is intentional emphasis, not a link.
- **Deck** (`.masthead__deck`): Newsreader, `clamp(1.3rem, 2.5vw, 1.6rem)`, weight 400, `lh-snug`, `--ink-soft`. Has a `::before` pseudo-element: `3.5ch × 2px`, `background: var(--accent)`, `border-radius: 2px`, `position: absolute; top: 0; left: 0`. Wrap the deck in `position: relative; padding-top: var(--space-4)`.
- **Byline** (`.masthead__byline`): IBM Plex Mono, `--fs-meta`, `--ink-mute`, `letter-spacing: 0.02em`

### 3. Epistemic Status Callout (`.epistemic`)

Deliberately low-key — **no background box, no accent border**. Just a top hairline rule:

```css
border-top: 1px solid var(--rule);
padding-block: var(--es-pad);  /* clamp(1.1rem, 3vw, 1.75rem) */
```

Contains:
- **Label** (`.epistemic__label`): IBM Plex Mono, `--fs-mono`, `letter-spacing: 0.14em`, uppercase, `--accent-deep`, weight 600. Has a `::before` 6×6px circle in `var(--accent)`.
- **Fields** (`.epistemic__fields`): CSS grid `max-content 1fr`, IBM Plex Mono, `--fs-meta`. `<dt>` in `--ink-faint`, uppercase, `--fs-micro`. `<dd>` in `--ink`. Separated from the note below by `border-bottom: 1px solid var(--rule)`.
- **Note** (`.epistemic__note`): Serif, `--fs-sm`, `lh: 1.6`, `--ink-soft`. Italics are `--ink-mute`.

### 4. Intro Prose

Five paragraphs of Newsreader body text (`--fs-base`, `lh-body`, `--ink`). `max-width: var(--measure)`. Separated from the epistemic callout by `<hr class="rule-mark">`: a `4ch` wide, `1px` top-border rule with `margin-block: var(--space-7)`.

Links: underline, `text-decoration-thickness: 1px`, `text-underline-offset: 0.18em`, `text-decoration-color: var(--accent-rule)`. Hover: `color: var(--accent-deep)`, `text-decoration-color: var(--accent)`.

### 5. Practice (`.practice-list`)

Section opener: kicker + h2 (`section-head` pattern below).

Numbered `<ol>`, rendered as flex rows:
- `border-top: 1px solid var(--rule)` on each item; `border-bottom` on last
- `padding-block: var(--space-4)`
- **Number**: IBM Plex Mono, `--fs-mono`, `var(--accent)`, weight 500, `letter-spacing: 0.04em`, `flex-shrink: 0`, `width: 1.6rem`
- **Text**: Newsreader, `--fs-base`, `--ink`, `lh-snug`

### 6. Work (`.project-list`)

Four project entries. Each is a CSS grid: `2.5rem 1fr` columns.

- `border-top: 1px solid var(--rule)`, `padding-block: var(--space-7)`
- **Number** col: IBM Plex Mono, `--fs-micro`, `var(--accent)`, weight 600, `letter-spacing: 0.08em`, `padding-top: 0.4em`
- **Content** col:
  - `project__name`: Newsreader, `--fs-h3`, weight 500, `--ink`, `letter-spacing: -0.012em`
  - `project__meta`: IBM Plex Mono, `--fs-meta`, `--ink-mute`. `.org` in `--ink-soft`, `.sep` in `var(--rule)`
  - `project__oneliner`: Newsreader italic, `--fs-sm`, `--ink-soft`, `lh: 1.55`. `border-left: 1.5px solid var(--accent-rule)`, `padding-left: var(--space-4)`, `margin-block: var(--space-4)`
  - `project__body`: Newsreader, `--fs-sm`, `--ink-soft`, `lh-body`
  - `project__tags`: flex-wrap, `gap: var(--space-2)`. Tag: IBM Plex Mono, `--fs-micro`, `--ink-mute`, `border: 1px solid var(--rule-soft)`, `border-radius: 3px`, `padding: 0.1rem 0.45rem`. `::before` content `#` in `--ink-faint`.

### 7. Career (`.career-list`)

Grid table: `8.5rem 1fr 5rem` columns (collapses to `6rem 1fr` on mobile, location hidden).

- `border-top: 1px solid var(--rule-soft)`, `padding-block: var(--space-3)`
- **Years**: IBM Plex Mono, `--fs-meta`, `--ink-mute`, `letter-spacing: 0.02em`, `white-space: nowrap`
- **Role**: Newsreader, `1rem`, `--ink`. `.career-org` is italic, `--ink-soft`, prepended with ` · ` separator in `--ink-faint`.
- **Location**: IBM Plex Mono, `--fs-micro`, `--ink-faint`, `letter-spacing: 0.04em`, `text-align: right`

### 8. Contact

Two-column grid (`repeat(auto-fit, minmax(170px, 1fr))`), `border-top` and `border-bottom: 1px solid var(--rule)`. Each cell:
- `padding-block: var(--space-5)`
- `border-right: 1px solid var(--rule)` (except last)
- **Label**: IBM Plex Mono, `--fs-micro`, `var(--accent)`, uppercase, `letter-spacing: 0.12em`, weight 500
- **Value**: Newsreader, `--fs-lead`, `--ink`, `letter-spacing: -0.01em`. Turns `var(--accent)` on hover.

Below the grid: `.also-at` — IBM Plex Mono, `--fs-meta`, `--ink-mute`. Links in `--ink-soft` with a bottom border rule.

### 9. Footer

`border-top: 1px solid var(--rule)`, `padding-block: var(--space-6) var(--space-8)`. Three-column flex row (wraps): site name / typeset credit / copyright. All IBM Plex Mono, `--fs-mono`, `--ink-mute`.

---

## Section Header Pattern

Used for Practice, Work, Career, Contact sections:

```html
<div class="section-head">
  <p class="kicker">Label</p>
  <h2>Heading text.</h2>
  <p class="section-lede">Optional italic lead.</p>  <!-- only some sections -->
</div>
```

- `.kicker`: IBM Plex Mono, `--fs-mono`, `letter-spacing: 0.13em`, uppercase, `--ink-mute`, weight 500
- `h2`: Newsreader, `clamp(1.85rem, 4vw, 1.9375rem)`, weight 560, `lh-tight`, `letter-spacing: -0.018em`, `max-width: 26ch`, `text-wrap: balance`
- `.section-lede`: Newsreader italic, `--fs-lead`, `--ink-soft`, `lh: 1.45`, `max-width: 44ch`

---

## Interactions & Behaviour

### Theme Toggle
```js
localStorage.setItem('rossouw-theme', 'dark' | 'light');
document.documentElement.setAttribute('data-theme', 'dark'); // or removeAttribute
```
Script runs in `<head>` — reads saved theme before first paint. All transitions: `background-color 240ms ease`, `color 240ms ease`.

### Navigation
All nav links are simple `<a href="#section-id">` anchor links. No JS scroll handling needed — native browser behaviour is sufficient.

### Hover states
- Nav links: `color → --ink`, `border-bottom-color → var(--rule)`
- Active nav: `color: --ink`, `border-bottom: 1px solid var(--accent)`
- Prose links: `color → --accent-deep`, `text-decoration-color → --accent`
- Contact cells: value text `→ var(--accent)`
- Tags: `color → --ink`, `border-color → --ink-faint`

### Text selection
```css
::selection { background: var(--accent-tint); color: var(--ink); }
```

---

## Responsive Breakpoints

One breakpoint: `max-width: 640px`

- Masthead: reduced top padding (`--space-5`)
- **Nav: hidden entirely** (`display: none`) — header collapses to wordmark + theme toggle only
- H1: smaller fluid size `clamp(1.85rem, 8vw, 2.6rem)` with `overflow-wrap: break-word`
- Career: grid collapses to `max-content 1fr` (years column auto-sizes to content), location column hidden
- Project: gutter column `2.5rem → 1.75rem`, gap reduced
- Contact grid: stacks to single column, borders reflow
- Nav: gap reduced

No horizontal scroll at any viewport width.

---

## Assets

None. The site is text-only. No images, no icons, no SVGs.

---

## Files in This Bundle

| File | Purpose |
|------|---------|
| `index.html` | Complete production-ready site — design reference AND deployable output |

---

## Deployment Checklist

1. **Uncomment Google Fonts** — in `<head>`, three `<link>` tags are commented out. Uncomment them for production.
2. **Deploy to static host** — drop `index.html` on Netlify / Vercel / Cloudflare Pages.
3. **DNS** — point `adrian.rossouw.ie` at the host. Add `www` redirect if desired.
4. **Meta tags** — `<title>` and `<meta name="description">` are already set correctly.
5. **Optional:** Add `<link rel="canonical" href="https://adrian.rossouw.ie/" />` once the domain is live.
