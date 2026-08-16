# Agent guidelines — cbrell.github.io

This is **Courtney Brell's personal academic website**, not a copy of the al-folio project. It was forked from the al-folio v1 starter and then stripped down. The upstream project's contributor rules do **not** apply here; an archived copy of them lives in `reference/` for lookup only.

Read this file before making changes.

## What the site is for

An academic job market site. The audience is hiring committee members and letter writers who will spend well under a minute on it. Priorities, in order:

1. **Never be broken.** A failed deploy or a dead PDF link is the worst outcome.
2. **Fast and readable on a phone.**
3. **Conventional.** This is not a site that should be visually interesting.

Prefer removing things over adding them. Every feature is a thing that can fail.

## Architecture in one paragraph

Layouts, includes, Sass and Liquid tags live in **gems** (`al_folio_core` and the other `al_*` gems in the `Gemfile`), not in this repo — which is why there is no `_layouts/` or `_includes/` directory. This repo holds content and configuration.

**Overriding a gem-owned file is allowed here.** Create `_layouts/page.liquid` (or `_includes/…`, `_sass/…`) locally and Jekyll will use your copy instead of the gem's. This has been tested and works. Copy the original out of the gem first:

```bash
cp "$(bundle info al_folio_core --path)/_layouts/page.liquid" _layouts/
```

Note that an override is a frozen copy: it will not pick up gem improvements later.

## The rule that matters most

**Do not run `bundle update`.** Every gem is pinned to an exact version in the `Gemfile`, with checksums in `Gemfile.lock`. That combination is why the build is reproducible. Leave it frozen for the duration of the job market; upgrade in the off-season, deliberately, with time to test.

## Two lists that must agree

Adding or removing a plugin means editing **both** the `Gemfile` and the `plugins:` list in `_config.yml`. A plugin present in only one of them is inert — the associated Liquid tag renders an empty string, with no warning and no error. This is the most common way to lose an hour here.

## No build-time network calls

The build must not depend on any third-party server being up, because that turns someone else's outage into a failed deploy. Deliberately disabled:

- `external_sources` — pulled RSS from Medium and blog.google at build time
- `jekyll_get_json` — fetched JSON Resume data
- the Google Scholar citation scraper and its workflow
- `enable_publication_badges` — Altmetric, Dimensions, Scholar, InspireHEP

`third_party_libraries.download: true` also vendors FontAwesome, Academicons, MathJax, Google Fonts and the rest into the build, so visitors' browsers make no CDN calls either. **Keep it that way.** If you need external data, fetch it once and commit the result.

## Commands

```bash
bundle install
bundle exec jekyll serve                      # http://localhost:4000
JEKYLL_ENV=production bundle exec jekyll build
```

Needs ImageMagick on `PATH`. On a machine with a non-UTF-8 locale, prefix with `LANG=C.UTF-8 LC_ALL=C.UTF-8`.

## Deployment

`main` → `.github/workflows/deploy.yml` → `gh-pages`. Only four workflows remain (`deploy`, `render-cv`, `axe`, `broken-links-site`); the rest were al-folio project CI and were removed. Don't add workflows back without a reason.

## Gotchas

- `baseurl` is intentionally **blank** (this is a user page at the domain root). Do not set it to `/al-folio` — the archived upstream docs say to, and that advice is wrong for this repo.
- `reference/` is excluded from the build and is disposable.
- The `Gemfile` still carries gems for features the site does not use (charts, distill, marimo, RTL, comments, newsletter). Harmless — they cost a couple of seconds of build time. Prune them later, once the content is settled, not before.
