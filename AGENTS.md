# AGENTS.md — Website

This repository is the public website project only.

When editing here:

- treat `_quarto.yml` as the site entrypoint
- keep session deck pages here separate from the runnable session source repo
- update `downloads/` only when the public downloadable bundles actually need to change
- do not add participant working files, generated session outputs, or personal helper skills here

Locally, this repo lives inside the session source folder as
`from-asking-to-doing-site/` (gitignored there). The runnable sessions are at
`../01_slidemaker/`, `../02_summarizer/` and `../03_multitudes/`; the folders
with the same names here are deck pages. Commit website changes in this repo,
never in the parent.
