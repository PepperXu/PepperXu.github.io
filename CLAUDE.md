# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Personal academic portfolio website for Xu Peisen (PhD candidate in HCI at NUS), built with Jekyll and hosted on GitHub Pages.

The repository is intentionally minimal and one-page focused:
- Single homepage layout only (`_layouts/one-page.html`)
- Light-theme-only behavior
- Content collections rendered inline on homepage (`publications`, `teaching`, `talks`)
- No multi-page post/archive/comment/analytics template stack

## Development Commands

### Local Development
```bash
bundle install          # Install Ruby gems
bundle exec jekyll serve -l -H localhost
```

### Docker Development
```bash
# Standard compose command (may fail if lockfile gems are not yet materialized in container)
docker compose up --build

# Reliable verification flow for this repo state
docker compose run --service-ports --rm jekyll-site sh -lc "bundle install; bundle exec jekyll serve -H 0.0.0.0 -w --config _config.yml,_config_docker.yml --livereload --force_polling"
```

### JavaScript Build
```bash
npm install             # Install Node.js dependencies
npm run build:js        # Minify JS (outputs to assets/js/main.min.js)
npm run watch:js        # Watch and rebuild on changes
```

## Architecture

### One-Page Layout (Homepage)
The site uses a custom one-page layout (`_layouts/one-page.html`) that renders all sections — About, Publications, Experience, Teaching, Talks, Resources — on a single scrolling page. `_pages/about.md` (permalink `/`) uses `layout: one-page`. The layout bypasses the standard masthead and sidebar, using its own sticky nav instead.

Styles for the one-page layout live in `_sass/layout/_one-page.scss`, imported last in `assets/css/main.scss`.

### Content Structure
- **`_publications/`** — Academic papers. Key front matter: `title`, `venue`, `date`, `category` (`conferences`/`manuscripts`/`books`), `paperurl`, `videourl`, `codeurl`, `demourl`, `slidesurl`. Set `featured: true` to appear in the highlighted grid. Set `award:` for an award badge. Add `header: { teaser: "images/filename.jpg" }` for a feature figure.
- **`_teaching/`** — Teaching entries rendered as a list on the homepage.
- **`_talks/`** — Talks rendered as a list on the homepage.
- **`_data/experience.yml`** — Education/work timeline data for the Experience section.
- **`_data/resources.yml`** — External links for the Resources section (`external` key, each with `title`, `url`, `icon`, `description`).
- **`_data/`** — Also includes `authors.yml` and `ui-text.yml`.
- **`_layouts/`** — Minimal set: `compress.html`, `one-page.html`.
- **`_includes/`** — Minimal set used by one-page: `base_path`, `head.html`, `head/custom.html`, `browser-upgrade.html`, `footer.html`, `footer/custom.html`, `scripts.html`, `seo.html`.
- **`_sass/`** — SCSS source; compiled CSS lives in `assets/css/`.

### Jekyll Collections
Three collections in `_config.yml`: `publications`, `teaching`, `talks` (all `output: false`). The one-page layout pulls these collections inline.

### JavaScript
Source files are `assets/js/_main.js` and `assets/js/theme.js`. The npm build concatenates and minifies them into `assets/js/main.min.js`.

Notes:
- Never edit `assets/js/main.min.js` directly.
- The one-page nav behavior is inlined at the bottom of `_layouts/one-page.html`.
- Site behavior is light-only; dark-theme branches were removed.

### Styling
Theme is set via `site_theme: "default"` in `_config.yml` and the implementation is light-only. Custom styles go in `_sass/`. Changes to SCSS require a Jekyll rebuild to take effect locally.

### Adding Publications
1. Create a `.md` file in `_publications/` named `YYYY-MM-DD-slug.md`
2. Required: `title`, `collection: publications`, `category`, `date`, `venue`
3. For featured highlight card: add `featured: true`, `description:`, and optionally `header: { teaser: "images/filename.jpg" }`
4. For award badge: add `award: "Best Paper Honorable Mention (Top 5%)"`

### Static Files
Upload PDFs and other files to `/files/` — accessible at `https://pepperxu.github.io/files/<filename>`.

## Key Config Files
- **`_config.yml`** — One-page settings, collections, plugin config (`jekyll-feed`, `jekyll-sitemap`, `jekyll-redirect-from`)
- **`_config_docker.yml`** — Overrides for Docker environment
- **`Gemfile`** — Ruby dependencies (uses `github-pages` gem for compatibility)
- **`package.json`** — JS build toolchain only; not a Node.js app

## Generated/Ignored Files
`_site/`, `.sass-cache/`, `node_modules/`, `Gemfile.lock`, `vendor/` are generated/ignored and should not be edited directly.
