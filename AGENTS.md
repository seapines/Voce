# AGENTS.md — instructions for AI agents working in this repository

## Project
VOCE Audio dealer-facing one-page website. Static HTML/CSS, deployed to GitHub
Pages via `.github/workflows/pages.yml`. The site deliberately uses no build
tooling or framework — keep it that way.

## Structure
- `index.html` — English page (default)
- `ru/index.html` — Russian page
- `it/index.html` — Italian page
- `style.css` — single shared stylesheet, linked by all three pages
- `img/` — logos (included in the repo; do not hotlink third-party images)
- `.github/workflows/pages.yml` — GitHub Pages deploy workflow. At build time it
  fingerprints `style.css` (hash-renamed) and rewrites the stylesheet link in
  **all three** `index.html` files, so translated pages must never be excluded
  from that step.

## The single most important rule: keep the three pages in sync
The three language pages must always mirror each other:

- Every content change (copy, products, sections, structure, attributes,
  accessibility labels) MUST be applied to `index.html`, `ru/index.html`, and
  `it/index.html` in the same commit.
- English is the source of truth. Translate into natural, marketing-grade
  Russian and Italian — not word by word. Product names ("VOCE Matrix-4",
  "VOCE Amp-Pro", "VOCE Aqua-8") and brand terms (Control4, Home Assistant,
  KNX, Hi-Res, DLNA, AirPlay, Dealer Kit, B2B) stay untranslated.
- The language switcher (`nav.lang`, top right) must appear on every page with
  the current language marked by `span.current` — EN/RU/IT links comparing to
  `../` / `../ru/` / `../it/` relative to the page.

## Styling conventions
- All colors are CSS variables in `:root` in `style.css`. Add new colors there.
- Design language: quiet luxury / high-tech (Sonos, Basalte). Dark palette,
  thin type, wide letter-spacing, generous whitespace. Do not add ornaments.
- Mobile first. Sections are full-screen splashes (`min-height: 100svh`).
- Keep CSS simple — plain, no frameworks, no preprocessors.

## Deploy
- Only push/commit when the user explicitly asks.
- Deploy happens automatically on push to `main`; a manual commit is not needed
  for a deploy.
- The email CTA is a `mailto:` with URL-encoded subject/body — copy its format
  between the language pages, only translating visible link text.
