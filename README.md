# From Asking to Doing Website

This repository contains the Quarto source for the public website for the
Jacobs Foundation "From Asking to Doing" training.

The site is deployed from the GitHub repository
`nelsonamayad-jf/from-asking-to-doing-site` and published at:

- <https://nelsonamayad-jf.github.io/from-asking-to-doing-site/>

This repository is intentionally separate from the validated runnable session
source repo `nelsonamayad-jf/from-asking-to-doing` (private). Maintainers keep it cloned
inside that repo's folder as `from-asking-to-doing-site/`, where it is
gitignored, so sessions and site sit side by side while each keeps its own
history and remote.

## Purpose

Use this repository for the public-facing website only:

- landing pages and navigation
- published session deck pages and their wrapper pages
- shared styling, images, and Quarto extensions
- downloadable public bundles under `downloads/`
- GitHub Pages deployment configuration

Do not use this repository for:

- participant working files
- generated session outputs
- personal helper skills
- source-of-truth runnable session development

## Repository Layout

- `_quarto.yml`: site entrypoint and render list
- `index.qmd`, `about.qmd`, `intro.qmd`, `tips.qmd`, `thesaurus.qmd`:
  top-level website pages
- `01_slidemaker/`, `02_summarizer/`, `03_multitudes/`: session wrapper pages,
  revealjs decks, and related assets
- `downloads/`: curated downloadable bundles that are meant to be public,
  each one a zip of a session folder from the session source repo
- `docs/`: repository and deployment notes
- `_website/`: rendered output directory created by Quarto; do not commit it

## Local Development

Prerequisite:

- Quarto CLI installed locally

Preview the site:

```bash
quarto preview
```

Render the full site:

```bash
quarto render
```

Quarto writes the rendered site to `_website/`.

## Deployment

GitHub Pages deployment is handled by
[`.github/workflows/deploy.yml`](.github/workflows/deploy.yml).

On every push to `main`, the workflow:

1. checks out the repository
2. installs Quarto
3. renders the site into `_website/`
4. uploads the rendered artifact
5. deploys the artifact to GitHub Pages

Repository setting required:

- `Settings -> Pages -> Source -> GitHub Actions`

The canonical site URL is also set in `_quarto.yml` as
`website.site-url`.

## Working Rules

- Treat `_quarto.yml` as the site entrypoint.
- Keep session deck pages here separate from the runnable session source repo.
- Update `downloads/` only when the public downloadable bundles actually
  change.
- Do not add generated site output or temporary helper files.

## License

Workshop content is licensed under CC BY 4.0.

Website code and configuration are licensed under MIT.

See `LICENSE`, `LICENSE-CONTENT`, and `LICENSE-CODE` for the exact split,
including exclusions for Jacobs Foundation brand assets.
