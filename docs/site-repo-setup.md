# Dedicated site repo setup

This workshop uses a two-repository publishing model:

- `Jacobs-Foundation/From-asking-to-doing` is the source repo
- `Jacobs-Foundation/from-asking-to-doing-site` is the public website repo

The source repo renders the site from `website/`. GitHub Actions then copies only `website/_website/`
into the site repo.

## Why this model

- The workshop repo keeps the replicable session folders.
- The site repo carries only rendered HTML, CSS, JS, images, and curated downloads.
- Public website hosting no longer forces the source repo itself to become the website repo.

## One-time GitHub setup

1. Create the repository `Jacobs-Foundation/from-asking-to-doing-site`.
2. Add a minimal `README.md` so the repo has a `main` branch from the start.
3. In that repo, go to `Settings -> Pages`.
4. Under `Build and deployment`, choose `Deploy from a branch`.
5. Set branch to `main` and folder to `/(root)`.
6. In the source repo `Jacobs-Foundation/From-asking-to-doing`, add these Actions settings:
   - Variable: `SITE_REPO_ENABLED` = `true`
   - Variable: `SITE_REPO` = `Jacobs-Foundation/from-asking-to-doing-site`
   - Secret: `SITE_REPO_TOKEN` = token with write access to the site repo
7. Push to `main` in the source repo or run the `Publish website` workflow manually.

## Token guidance

Use a token that can push commits into `Jacobs-Foundation/from-asking-to-doing-site`.

Practical minimum:

- Fine-grained personal access token
- Repository access limited to `from-asking-to-doing-site`
- Repository permission: `Contents` set to `Read and write`

## What the workflow syncs

The publish workflow force-syncs the site repo to match the rendered `website/_website/`
folder from the source repo.

That means:

- keep the site repo dedicated to published output
- do not hand-edit HTML in the site repo
- make content changes in the source repo, then republish

## Current URL assumption

The Quarto project is configured for:

`https://jacobs-foundation.github.io/from-asking-to-doing-site/`

If you choose a different site repo name, update:

- `website/_quarto.yml` `website.site-url`
- `SITE_REPO` in the source repo variables
