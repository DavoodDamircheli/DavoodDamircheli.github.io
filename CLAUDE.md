# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this repository is

A personal academic website for Davood Damircheli (LSU), built with **Jekyll 4.3** on a **vendored copy** of the [Minimal Mistakes](https://mmistakes.github.io/minimal-mistakes/) theme (v4.26.2). The theme's source (`_layouts`, `_includes`, `_sass`, `assets/js`) lives directly in the repo rather than being pulled from the gem, so theme internals can be edited in place — but see "What to edit vs. leave alone" below.

## Commands

```bash
bundle install                 # install Ruby gem dependencies (first run)
bundle exec jekyll serve       # local dev server with live reload at http://localhost:4000
bundle exec jekyll build       # build the static site into _site/
bundle exec jekyll serve --drafts   # include draft posts while previewing
```

Note: `_config.yml` is NOT reloaded by `jekyll serve` — restart the server after editing it. `Gemfile.lock` is gitignored but committed-adjacent; run `bundle install` if gems are missing.

## Content architecture

This site diverges from a stock Minimal Mistakes install: instead of using `_pages/`, each top-level nav section is its own directory whose main page (`index.md`, or `research.md`/`personal.md`) sets the section URL — some via an explicit `permalink`, others (`teaching/`, `cv/`) via Jekyll's default directory-based path. The nav bar is wired up in `_data/navigation.yml`, and each URL there must match a page's resolved URL:

| Directory      | Page              | `permalink`   |
| -------------- | ----------------- | ------------- |
| `Home/`        | `index.md`        | `/Home/`      |
| `research/`    | `research.md`     | `/research/`  |
| `teaching/`    | `index.md`        | `/teaching/`  |
| `besides/`     | `personal.md`     | `/besides/`   |
| `cv/`          | `index.md`        | `/cv/`        |

- **Blog posts** go in `_posts/` as `YYYY-MM-DD-title.md` with YAML front matter (`title`, `date`, `layout: single`, optional `categories`/`tags`). Post images live in `_posts/img/`. Permalink pattern is `/:categories/:title/` (set in `_config.yml`), and the home page paginates posts 5 at a time.
- **Site-wide assets**: user content images in `assets/img/`, videos in `assets/videos/`, plus the theme's `assets/css` and `assets/js`. The author avatar and bio are configured under `author:` in `_config.yml`.
- `content/` holds downloadable files (e.g. the CV PDF). `draft/` and `Home/` are content, not Jekyll's `_drafts`.

Pages use theme layouts referenced by `layout:` in front matter — commonly `single`, `archive`, or `splash`. Available layouts are in `_layouts/`.

## What to edit vs. leave alone

- **Edit for site content/config**: the top-level content directories above, `_posts/`, `_data/navigation.yml`, `_config.yml` (site title, author, nav, plugins), and `assets/img`/`assets/videos`.
- **Theme internals** (`_layouts/`, `_includes/`, `_sass/`, `assets/js/_main.js`): only touch when intentionally customizing the theme's appearance/behavior. These are upstream theme files.
- **Ignore / do not treat as site content**: `docs/` and `test/` are the upstream Minimal Mistakes demo site and test suite — both are excluded from the build via `_config.yml` and are not part of this website. `CHANGELOG.md`, `Rakefile`, `README.md`, and `package.json` are upstream theme-maintenance files, not site files.

## Config notes

- Plugins in use (`_config.yml` → `plugins`): `jekyll-paginate`, `jekyll-sitemap`, `jekyll-gist`, `jekyll-feed`, `jekyll-include-cache`. The `jekyll-include-cache` plugin is required — removing it causes `Unknown tag 'include_cached'` build errors.
- Markdown is kramdown with GFM input; syntax highlighting via rouge.
- Skin is set with `minimal_mistakes_skin` in `_config.yml` (`default`, `air`, `dark`, etc.).
