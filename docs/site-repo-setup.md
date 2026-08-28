# GitHub Pages Setup

This repository is both the website source repo and the GitHub Pages deploy
repo for the public workshop site.

The validated runnable sessions live separately in
`Jacobs-Foundation/From-asking-to-doing`.

## Why this model

- The session repo stays easy to browse and replicate in Claude or Codex.
- The website repo contains only public website source and downloadable bundles.
- GitHub Pages deployment no longer depends on cross-repo sync or personal tokens.

## One-time GitHub setup

1. Create or open `nelsonamayad-jf/from-asking-to-doing-site`.
2. Push this repository so `main` exists.
3. In `Settings -> Pages`, set `Source` to `GitHub Actions`.
4. Ensure GitHub Actions is enabled for the repository.
5. Push to `main` or run the `Deploy site` workflow manually.

## What the workflow does

`.github/workflows/deploy.yml`:

- checks out this repo
- installs Quarto 1.10.8
- renders the site into `_website/`
- uploads the rendered artifact
- deploys it to GitHub Pages

No PAT or cross-repo secret is required.

## Current URL assumption

The Quarto project is configured for:

`https://nelsonamayad-jf.github.io/from-asking-to-doing-site/`

If the repository name changes, update `_quarto.yml` `website.site-url`.
