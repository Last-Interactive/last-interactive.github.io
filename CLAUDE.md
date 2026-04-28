# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Jekyll-based static website for Last Interactive, a mobile app and indie game studio. Hosted on GitHub Pages at `www.lastinteractive.com`.

## Build & Serve

```bash
bundle install       # Install Ruby dependencies (first time)
jekyll serve         # Local dev server at http://localhost:4000
jekyll build         # Generate static files to _site/
```

No test suite, linter, or additional build tooling exists.

## Architecture

- **Jekyll collections**: Apps/games are entries in the `_works/` collection, each a Markdown file with front matter (title, subtitle, icon, demo image, store links). Adding a new work means adding a new `.md` file there.
- **Layouts**: `default.html` is the base layout (navbar + footer). `works.html` extends it for individual app detail pages with demo images and download buttons.
- **Includes**: `head.html` (meta/fonts/CSS), `navbar.html`, `footer.html` — all driven by `_config.yml` settings.
- **Styling**: Single `css/main.css` file. Dark teal (`#0c3734`) and cream (`#f5eddb`) color scheme. Fonts: Playfair Display (headings), Rubik (body).
- **Site config**: `_config.yml` controls navbar links, social media links, footer text, and the works collection definition.
- **CNAME**: Custom domain mapping — do not remove.
