# Website

This folder is the Quarto project for the published workshop site.

It is not the runnable workshop package. The runnable sessions live at the repo
root in:

- `../01_slidemaker/`
- `../02_summarizer/`
- `../03_multitudes/`

## What Lives Here

- public pages such as `index.qmd`, `about.qmd`, and `intro.qmd`
- the published session decks and wrappers under `01_slidemaker/`, `02_summarizer/`, and `03_multitudes/`
- styles, images, and Quarto extensions
- curated downloadable session zip files under `downloads/`
- publish setup notes under `docs/`

## Build Locally

```bash
cd website
quarto preview
quarto render
```

Render output goes to `website/_website/` and should never be committed.
