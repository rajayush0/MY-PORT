# WARP.md

This file provides guidance to WARP (warp.dev) when working with code in this repository.

## Project type
This is a static, single-page portfolio site (no build step / framework). The entry point is `index.html`, which loads `styles.css` + `script.js` and uses CDN-hosted Google Fonts + Font Awesome.

## Common commands

### Serve locally (recommended)
Use a small static file server so relative paths and fetches behave like a real site.

```bash
python3 -m http.server 8000
```

Then open:

```bash
brave-browser http://localhost:8000/
```

### Open directly in Brave (no server)

```bash
brave-browser index.html
```

### Lint / format / tests
No lint/test tooling is configured in this repo (no `package.json`). Validate changes by loading the page in a browser.

## High-level architecture

### `index.html`
Single-page layout with anchor navigation.
- Top-level sections are keyed by IDs that match navbar links: `#home`, `#about`, `#skills`, `#projects`, `#certifications`, `#connect`.
- Imports `styles.css` and `script.js` from the repo root.
- Uses `assets/BS.png` for the About profile image.

### `styles.css`
All styling lives in one stylesheet.
- Theme is driven by CSS variables in `:root`.
- Light theme overrides are applied when the root element has `[data-theme="light"]`.
- Most of the UI (layout, hover effects, typography, section styling) is CSS-driven.

### `script.js`
Behavior/interaction layer:
- Custom cursor: updates `.cursor-dot` and animates `.cursor-outline` on `mousemove`.
- Mobile menu: toggles `.active` on `.hamburger` and `.nav-links`.
  - Note: if the menu doesn’t visually change, add/update CSS for `.nav-links.active` / `.hamburger.active`.
- Smooth scrolling: intercepts `a[href^="#"]` and calls `scrollIntoView({ behavior: "smooth" })`.
- Contact form: demo-only; blocks submission and shows an `alert()`.
- Theme toggle: `#theme-toggle` toggles `data-theme` on `<html>` and persists the choice to `localStorage`.
- Projects: clicking the element with `id="proj2"` opens an external site (`flashhubby.netlify.app`).

## Assets
- `assets/BS.png`: profile image used in About section.
