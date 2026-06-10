# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Jekyll-based static website for Last Interactive, a two-person mobile app and indie game studio in Brooklyn. Hosted on GitHub Pages at `www.lastinteractive.com` via the `CNAME` file (do not remove).

## Build & Serve

```bash
bundle install                  # Install Ruby dependencies (first time)
bundle exec jekyll serve        # Local dev server at http://localhost:4000
bundle exec jekyll build        # Generate static files to _site/
```

No test suite, linter, or additional build tooling exists.

## Architecture

- **Works collection** (`_works/`): Each app/game is a Markdown file. Front matter drives all rendering — there is no shared catalog file. Adding a new work = new `.md` file with the conventions below.
- **Layouts**: `default.html` (base: navbar + footer) and `works.html` (individual work detail page with phone mockup + store buttons). `posts.html` exists but is unused (no `_posts/` directory).
- **Includes**: `head.html`, `navbar.html`, `footer.html` — all driven by `_config.yml`.
- **Styling**: Single `css/main.css`. Dark teal `#0c3734` + cream `#f5eddb`. Fonts: Playfair Display (headings), Rubik (body).

## Work front matter conventions

`index.html` and `_layouts/works.html` consume these keys — names matter:

- `name` — display title (used everywhere; `title` is for the HTML `<title>` tag).
- `summary` — short blurb shown on the work list and detail page.
- `meta` — short tag like `"iOS · 2025"` or `"In development"`. Defaults to `"iOS"` on the work list if absent.
- `icon`, `demo` — asset paths (PNG icon, GIF demo). Demo renders inside a phone mockup.
- `app-store-link`, `play-store-link` — optional store URLs. Detail page chooses "Available on:" vs "Exclusively available on:" based on which are present.
- `featured: true` — promotes the work into the homepage **Featured / "A closer look"** section. Only the first match is used.
- `unreleased: true` — excludes the work from the released list and renders it as a single **disabled** tile at the end of the homepage works list. Also drives the "Next up:" line in the hero. Only the first match is used.

## Homepage rendering rules (`index.html`)

- Lists the 3 most recent released works (`site.works | reverse | limit: 3`, filtering out `unreleased`).
- Appends one unreleased work (if any) as a disabled tile.
- Featured section only renders if some work has `featured: true`.
- "Currently shipping" copy in the hero is hardcoded — update `index.html` when changing the current shipping title.
