# From Asking to Doing Website

This repository contains the Quarto source for the public workshop website.

It is published from the personal repository
`nelsonamayad-jf/from-asking-to-doing-site` and stays separate from the
validated session source repo `Jacobs-Foundation/From-asking-to-doing`.

## What Lives Here

- public pages such as `index.qmd`, `about.qmd`, `intro.qmd`, and `tips.qmd`
- published session decks and wrapper pages under `01_slidemaker/`, `02_summarizer/`, and `03_multitudes/`
- styles, images, and Quarto extensions
- curated downloadable session bundles under `downloads/`
- GitHub Pages setup notes under `docs/`

## Build Locally

```bash
quarto preview
quarto render
```

Render output goes to `_website/` and should never be committed.

## Deployment

This repo deploys itself to GitHub Pages from `.github/workflows/deploy.yml`.

One-time GitHub setup:

1. Push this repository to GitHub.
2. In `Settings -> Pages`, set `Source` to `GitHub Actions`.
3. Push to `main` to trigger the first deployment.

## License

Workshop content in this repo is licensed under CC BY 4.0. Website code and
configuration are licensed under MIT. See `LICENSE`, `LICENSE-CONTENT`, and
`LICENSE-CODE` for the exact split and exclusions for Jacobs Foundation brand
assets.
