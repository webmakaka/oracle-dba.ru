# AGENTS.md

Russian-language Oracle DBA knowledge base, built as a static Jekyll 4.2.2 site (kramdown markdown, jekyll-sitemap plugin). All content is in Russian — write new content in Russian.

## Layout

- `website/` — all site content as Markdown. Directories are numbered (`00-nav/`, `01-docs/...`), section indexes are `00-index.md`, articles `01-*.md`. This directory exists only to organize files; URLs never derive from paths.
- `website/01-index.md` — homepage (`permalink: /`), `website/02-sitemap.md` — sitemap (`/sitemap/`).
- `files/` — downloadable assets, referenced from docs with absolute URLs like `/files/golden-gate/...`.
- `_includes/header.html` — hand-maintained nav. New top-level sections must be added here manually.
- `_layouts/`, `css/`, `img/` — templates and static assets.

## Every page's front matter

Each Markdown page must explicitly declare its URL; Jekyll's path-based URLs are never used:

```yaml
---
layout: page
title: ...
description: ...
keywords: ...
permalink: /some/path/
---
```

- `permalink` must end with `/` (only exception: `00-nav/404.md` uses `/404.html`).
- The page body starts with an H1 `#` matching `title`.
- Articles use kramdown-only syntax (e.g. `{: .center-image }` attribute lists) — GFM is not active.

## Build and verify

There is no Makefile/Rakefile. The Dockerfile is the source of truth for verification: it runs `bundle exec jekyll build` then `htmlproofer ./_site` (only 4xx statuses, `--check-html`, hash hrefs allowed, `_site/404.html` ignored). CI (`.github/workflows/build.yml`) only runs `docker build ./` on push/PR to `main` — a green docker build is the equivalent of passing lint+link checks locally.

Recommended verification before finishing work:

```
docker build ./ -f ./Dockerfile -t oracle-dba:check
```

Broken internal links or invalid HTML inside new pages will fail the htmlproofer step.

Local dev server (port 80 on host):

```
docker-compose up   # jekyll serve --watch --incremental, host 80 -> container 4000
```

Quirks:
- `Dockerfile` pins ancient `ruby:2.6` + bundler 2.4.22; `Gemfile` pins jekyll 4.2.2, jekyll-sitemap 1.4.0, html-proofer 3.19.4. No `Gemfile.lock` is committed. Keep these pinned versions consistent if you touch them.
- Remote default branch is `main` (CI only runs there). A stale `master` branch and `imgbot` branch exist upstream — do not push to them; old docs mentioning "master" are outdated.

## Style

- HTML in `_includes/` is Prettier-formatted (`.prettierrc`: `singleQuote: true`) — keep formatting consistent when editing.
- Existing pages use `<br/>` separators, `: .center-image` classes on images, and plain HTML tables where needed — follow the pattern of the section you edit.
