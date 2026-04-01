# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Personal academic portfolio website for Xu Peisen (PhD candidate in HCI at NUS), built with Jekyll and hosted on GitHub Pages. The site showcases research (Mixed Reality, Human-Drone Interaction), publications, teaching, and blog posts.

## Development Commands

### Local Development
```bash
bundle install          # Install Ruby gems
jekyll serve -l -H localhost  # Serve with live reload at http://localhost:4000
# or
bundle exec jekyll serve -l -H localhost
```

### Docker Development
```bash
docker compose up       # Build and run (port 4000, LiveReload on 35729)
```

### JavaScript Build
```bash
npm install             # Install Node.js dependencies
npm run build:js        # Minify JS (outputs to assets/js/main.min.js)
npm run watch:js        # Watch and rebuild on changes
```

### Content Generation (Python tools in `markdown_generator/`)
```bash
python publications.py  # Generate publication .md files from publications.tsv
python talks.py         # Generate talk .md files from talks.tsv
python pubsFromBib.py   # Generate publications from a BibTeX file
```

### CV Update
```bash
./scripts/update_cv_json.sh  # Convert CV markdown to _data/cv.json
```

## Architecture

### One-Page Layout (Homepage)
The site uses a custom one-page layout (`_layouts/one-page.html`) that renders all sections — About, Publications, Experience, Teaching, Talks, Resources — on a single scrolling page. `_pages/about.md` (permalink `/`) uses `layout: one-page`. The layout bypasses the standard masthead and sidebar, using its own sticky nav instead.

Styles for the one-page layout live in `_sass/layout/_one-page.scss`, imported last in `assets/css/main.scss`.

### Content Structure
- **`_publications/`** — Academic papers. Key front matter: `title`, `venue`, `date`, `category` (`conferences`/`manuscripts`/`books`), `paperurl`, `videourl`, `codeurl`, `demourl`, `slidesurl`. Set `featured: true` to appear in the highlighted grid. Set `award:` for an award badge. Add `header: { teaser: "images/filename.jpg" }` for a feature figure.
- **`_teaching/`** — Teaching entries rendered as a list on the homepage.
- **`_posts/`** — Blog posts, shown as cards in the Resources section.
- **`_data/experience.yml`** — Education/work timeline data for the Experience section.
- **`_data/resources.yml`** — External links for the Resources section (`external` key, each with `title`, `url`, `icon`, `description`).
- **`_data/`** — Also: `navigation.yml`, `cv.json`, `authors.yml`, `ui-text.yml`.
- **`_layouts/`** and **`_includes/`** — Liquid HTML templates; `default.html` wraps `compress.html`; `one-page.html` extends `compress.html` directly.
- **`_sass/`** — SCSS source; compiled CSS lives in `assets/css/`.

### Jekyll Collections
Four collections in `_config.yml`: `publications`, `teaching`, `portfolio`, `talks`. The one-page layout pulls from `site.publications`, `site.teaching`, `site.talks`, and `site.posts` directly.

### JavaScript
Source files in `assets/js/_main.js` and `assets/js/plugins/`. The npm build concatenates and minifies them into `assets/js/main.min.js`. Never edit `main.min.js` directly — edit source files and run `npm run build:js`. The one-page nav/scroll JS is inlined at the bottom of `one-page.html`.

### Styling
Theme is set via `site_theme: "default"` in `_config.yml` (alternative: `"air"`). Custom styles go in `_sass/`. Changes to SCSS require a Jekyll rebuild to take effect locally.

### Adding Publications
1. Create a `.md` file in `_publications/` named `YYYY-MM-DD-slug.md`
2. Required: `title`, `collection: publications`, `category`, `date`, `venue`
3. For featured highlight card: add `featured: true`, `description:`, and optionally `header: { teaser: "images/filename.jpg" }`
4. For award badge: add `award: "Best Paper Honorable Mention (Top 5%)"`

### Static Files
Upload PDFs and other files to `/files/` — accessible at `https://pepperxu.github.io/files/<filename>`.

## Key Config Files
- **`_config.yml`** — Jekyll settings, author profile, social links, plugin config
- **`_config_docker.yml`** — Overrides for Docker environment
- **`Gemfile`** — Ruby dependencies (uses `github-pages` gem for compatibility)
- **`package.json`** — JS build toolchain only; not a Node.js app

## Generated/Ignored Files
`_site/`, `.sass-cache/`, `node_modules/`, `Gemfile.lock`, `vendor/` are gitignored and should not be edited directly.
