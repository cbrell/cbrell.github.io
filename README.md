# cbrell.github.io

Personal academic website for Courtney Brell, published at <https://cbrell.github.io>.

Built with [Jekyll](https://jekyllrb.com/) on the [al-folio](https://github.com/alshedivat/al-folio) v1 starter. The site's layouts, styles and Liquid tags come from the `al_folio_core` gem and friends rather than living in this repo — see `AGENTS.md`.

## Local preview

```bash
bundle install
bundle exec jekyll serve      # http://localhost:4000
```

The production build is what CI runs:

```bash
JEKYLL_ENV=production bundle exec jekyll build
```

ImageMagick must be on `PATH` for responsive image generation (`sudo apt-get install imagemagick`).

## Where content lives

| What | Where |
|---|---|
| Landing page / bio | `_pages/about.md` |
| Publications & working papers | `_bibliography/papers.bib` |
| CV data (rendered to PDF by CI) | `_data/cv.yml` |
| Teaching | `_pages/teaching.md`, `_teachings/` |
| News items | `_news/` |
| Contact & social links | `_data/socials.yml` |
| Site-wide settings | `_config.yml` |
| PDFs, images | `assets/pdf/`, `assets/img/` |

## Deployment

Pushing to `main` triggers `.github/workflows/deploy.yml`, which builds the site and publishes it to the `gh-pages` branch. Work on a branch and merge to `main` to publish.

`reference/` holds an archived copy of the upstream al-folio documentation for convenience while the site is being built. It is not part of the published site and can be deleted once things settle.
