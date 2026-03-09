# CLAUDE.md — AI Assistant Guide for cloudsecurity.github.io

This file provides context and conventions for AI assistants (such as Claude) working in this repository.

## Repository Overview

This is a minimal **GitHub Pages** static site using **Jekyll** and the `jekyll-theme-hacker` theme. The site is hosted directly from the repository via GitHub Pages, with no custom build pipeline or CI/CD configuration.

## Tech Stack

| Component | Technology |
|-----------|------------|
| Static Site Generator | Jekyll |
| Theme | `jekyll-theme-hacker` |
| Content Format | Markdown (`.md`) with YAML front matter |
| Templating | Jekyll Liquid (via theme layouts) |
| Hosting | GitHub Pages (automatic Jekyll builds) |
| Ruby Dependency Manager | Bundler |

## Repository Structure

```
cloudsecurity.github.io/
├── _config.yml     # Jekyll site configuration
├── Gemfile         # Ruby/Bundler dependency file
├── index.md        # Main landing page (site content)
└── CLAUDE.md       # This file
```

There are no subdirectories, custom layouts, includes, plugins, or assets beyond what the theme provides.

## Key Files

### `_config.yml`
Jekyll site-wide configuration:
```yaml
title: Hacker theme
description: Hacker is a theme for GitHub Pages.
show_downloads: true
google_analytics:          # currently empty — add a UA/G- tracking ID here if needed
theme: jekyll-theme-hacker
```

### `index.md`
The sole content page. Uses the `default` layout (provided by the theme):
```yaml
---
layout: default
---
```
All content is standard Markdown, rendered by Jekyll via the hacker theme.

### `Gemfile`
Minimal Ruby dependency file using `gemspec`. Bundler resolves the actual gems from the theme and GitHub Pages environment.

## Development Workflow

### Local Development
To preview the site locally with Jekyll:

```bash
# Install dependencies
bundle install

# Serve locally with live reload
bundle exec jekyll serve

# Site will be available at http://localhost:4000
```

### Content Editing
- All site content lives in `index.md`.
- Add new pages as top-level `.md` files with the appropriate YAML front matter:
  ```yaml
  ---
  layout: default
  title: Page Title
  ---
  ```
- Jekyll will automatically build them into HTML on deploy.

### Deployment
- Push to the default branch (typically `main` or `master`).
- GitHub Pages detects the push and automatically rebuilds and publishes the site.
- No manual build or deployment step is needed.

## Conventions and Guidelines

### Markdown Style
- Use standard GitHub-Flavored Markdown (GFM).
- Fenced code blocks with language identifiers for syntax highlighting (e.g., ` ```js `, ` ```ruby `).
- Use `*` for unordered lists and `1.` for ordered lists.
- Wrap inline code in backticks: `` `keyword` ``.

### Front Matter
Every page **must** include a YAML front matter block at the top:
```yaml
---
layout: default
---
```
Optional fields: `title`, `description`, `permalink`.

### File Naming
- Lowercase filenames with hyphens for spaces: `my-new-page.md`
- Configuration and special Jekyll files use underscores: `_config.yml`

### Configuration Changes
- Site-wide settings go in `_config.yml`.
- Do not commit secrets (API keys, tokens) to `_config.yml` or any tracked file.
- The `google_analytics` field accepts a Google Analytics tracking ID (e.g., `G-XXXXXXXXXX`).

## Adding New Content

1. Create a new `.md` file at the repo root (e.g., `about.md`).
2. Add YAML front matter with at minimum `layout: default`.
3. Write content in Markdown below the front matter.
4. Commit and push — GitHub Pages will publish the new page automatically.

## What This Repository Does Not Have

- No custom `_layouts/`, `_includes/`, or `_sass/` directories — all inherited from theme.
- No JavaScript build tooling (webpack, vite, npm scripts).
- No automated tests or linters.
- No CI/CD workflows (`.github/workflows/`).
- No `Gemfile.lock` committed (lock file is not tracked).
- No `.gitignore` (consider adding one to exclude `_site/`, `.jekyll-cache/`, etc.).

## Suggested `.gitignore`

If working locally, add a `.gitignore` to avoid committing generated files:
```
_site/
.jekyll-cache/
.jekyll-metadata
.bundle/
vendor/
```
