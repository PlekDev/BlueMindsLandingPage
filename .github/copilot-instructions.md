# Copilot instructions — BlueMindsLandingPage

Purpose
- Quickly orient code-writing agents to the structure, conventions, and developer workflows so they can be productive immediately.

Repository snapshot (big picture)
- Single-page static landing site: fully client-side HTML/CSS/JS.
- Main entry: `index.html` (contains markup, minimal custom CSS, and inline scripts for SPA navigation and charts).
- Assets: `Media/` (images, webp assets) and `site.webmanifest`.
- No build system, bundler, or automated tests present.

Run / preview / deploy
- Local preview: open `index.html` in any browser or run a simple static server from repo root: `python3 -m http.server 8080` (then visit `http://localhost:8080`).
- Deployment is performed via GitHub Pages (site meta points to `plekdev.github.io/BlueMindsLandingPage`). Push to the repository and configure GitHub Pages (root / `gh-pages` / `docs` depending on repo setup).

Key conventions & patterns (code agents should follow)
- SPA navigation: pages are `section` elements with ids of the form `view-<name>` and classes `page-view` (+ `hidden-view` / `active-view` to toggle visibility).
  - Use `showPage('<name>')` pattern (defined inline) when adding nav buttons. Example: add `section id="view-faq" class="page-view hidden-view">...</section>` and `button onclick="showPage('faq')">FAQ</button>`.
- Mobile menu: `id="mobile-menu"` with `toggleMobileMenu()` used to open/close.
- Charts: Chart.js is included via CDN. Chart canvases use `id="mainChart"` and `id="techChart"`. JS chart initialization lives at the bottom of `index.html`—follow existing pattern (guard with `?.getContext('2d')` if optional).
- Styling: Tailwind is used via CDN + small custom CSS in `<head>` (custom classes: `.blue-gradient`, `.nav-glass`, `.page-view`, `.stat-card`, etc.). Prefer using Tailwind classes and keep small custom CSS for page-wide utility styles.
- External libs & links: Tailwind, Font Awesome, Chart.js are CDN dependencies; external links include `https://app.neuroblueminds.com`, social links, and mailto for contact.
- Language & copy: site content is Spanish (`<html lang="es">`)—preserve locale when editing copy.

Files to look at when working on a change
- `index.html` — source of truth for behavior and layout. Most edits should touch this file.
- `Media/` — images and assets (optimize and keep consistent formats; OG image is referenced in meta tags).
- `site.webmanifest` — update if icons or theme colors change.
- `README.md` — minimal; consider updating when adding developer workflows or build steps.

Behavior & troubleshooting notes
- SPA state is purely DOM-class based; ensure `showPage()` toggles the right classes and call `toggleMobileMenu(false)` to close mobile menu after navigation.
- If adding charts, follow existing data and color patterns and declare them after the canvas element so query selectors find them.
- No automated tests: for visual changes, validate locally in multiple viewport sizes and in a browser to check Tailwind utilities render correctly.

Guidelines for PRs (practical scope)
- Keep changes small and focused; provide screenshots for visual changes.
- If adding new assets, put optimized WebP/PNG in `Media/` and update OG meta tags if the social preview should change.
- If introducing a build step (e.g., Tailwind compilation), update `README.md` with exact commands and add a `docs/` or `gh-pages` deployment note.

Examples of task-specific instructions
- Add new SPA page: create `section id="view-<name>" class="page-view hidden-view">`, add a nav button using `onclick="showPage('<name>')"`, and include content + tests via local preview.
- Add a new Chart: add `<canvas id="myChart"></canvas>` and initialize it in the inline script at the bottom; follow existing Chart.js options for responsiveness.

If anything here is unclear or missing, please point out specifics (e.g., desired CI, preferred deploy branch, or testing tools) and I will update this guidance. 

---
