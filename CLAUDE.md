# CLAUDE.md

@AGENTS.md

`AGENTS.md` (imported above) is the authoritative guide for this repo: what the site is for, where the layouts actually live, the `bundle update` freeze, the Gemfile/`_config.yml` pairing rule, and the no-build-time-network-calls rule. Read it first and don't restate it here.

## Claude-specific notes

- **`reference/` is archived upstream al-folio documentation.** It describes the al-folio *project*, not this site, and parts of it are actively wrong here — most importantly the claim that `baseurl` is `/al-folio` and the prohibition on creating `_layouts/`, `_includes/` and `_sass/`. Use it to look up how a feature works, never as a source of rules.
- **Ask before adding a feature.** The default answer for anything that adds a moving part to a job market site is no.
- **Content questions belong to Courtney.** Don't invent affiliations, paper titles, dates, coauthors, course names or numbers. If a fact isn't supplied, leave a clearly marked placeholder and ask.
- **Verify by building.** `JEKYLL_ENV=production bundle exec jekyll build` catches most breakage. A green build plus a look at the rendered HTML beats reasoning about Liquid.
