# Site Notes

## Repo Overview

Jekyll-based personal/teaching website deployed to `dandrake.github.io` via GitHub Pages.

**Theme:** `jekyll-theme-minimal` (GitHub Pages built-in), with two custom layouts in `_layouts/` — `page.html` (generic) and `course.html` (adds course header with title, semester, meeting time, location, and nav links).

## Content Structure

- `index.md` — Homepage (lists current courses, bio, CV link)
- `courses/` — Course materials organized by semester:
  - `courses/2026-1-spring/112_intro_to_data_sci/`
  - `courses/2026-1-spring/123_core_concepts_in_cs/`
  - `courses/2025-2-fall/...`
- `dan-drake-cv.pdf` — CV
- `_config.yaml` — Jekyll config defining collections for each course (e.g., `"123"` outputs to `/courses/2026-1-spring/123_core_concepts_in_cs/`)

## How to Update

1. Edit/add Markdown or HTML files in the appropriate directory. Course pages use `layout: course` front matter with fields like `title`, `semester`, `meeting_time`, `location`, `course_nav`.
2. Syllabi are HTML files generated from source docs in Google Drive. Git hooks (`.git-hooks/pre-commit` and `pre-push`) validate that the HTML isn't stale relative to the source.

## How to Build and Preview Locally

```bash
bundle install            # install gems (one-time, uses .bundle/vendor)
bundle exec jekyll serve   # serve locally at localhost:4000
```

Jekyll watches for changes and rebuilds automatically. Requires Ruby 3.4.5 (see `.ruby-version`; managed via rbenv per `README.org`).

## CSS Styling

Custom styles live in `assets/css/style.scss`. This file overrides the theme's default stylesheet. It must start with empty front matter (`---`/`---`) for Jekyll to process it.

Currently it imports the base theme and adds a background image (an SVG "endless constellation" pattern from SVGBackgrounds.com) as an inline data URI on `body`. To change the background, replace the `background-image` data URI or update `background-color`.

## How to Deploy

Automatic. Push to the `pages-site` branch and a GitHub Actions workflow (`.github/workflows/jekyll-gh-pages.yml`) builds the site with `jekyll build` and deploys it to GitHub Pages. No manual deploy step needed.

**Branch note:** `pages-site` is the deploy branch. `gh-pages-test` appears to be the default remote HEAD / main branch for PRs.
