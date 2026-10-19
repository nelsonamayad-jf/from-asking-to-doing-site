# CLAUDE.md — Website

This repository contains the Quarto source for the published workshop website.

Focus here on website concerns only:

- page structure and navigation
- presentation deck pages and wrappers
- styling, images, and Quarto extensions
- curated downloadable zip files
- GitHub Pages publishing setup

Do not treat this repo as the runnable workshop package. The validated session
source is the separate repository `nelsonamayad-jf/from-asking-to-doing`.

## Where This Repo Sits

Locally, this repo is checked out inside the session source folder, as
`from-asking-to-doing-site/`, and is gitignored there. It is still its own git
repository with its own remote; commit website changes here, never in the
parent.

Because Claude Code loads `CLAUDE.md` files from parent folders too, the session
repo's `../CLAUDE.md` is also in context when this folder is opened directly.
Its rules about not adding website files apply to that repo, not this one. For
website work, this file governs.

- `01_slidemaker/`, `02_summarizer/`, `03_multitudes/` here are deck pages and
  slide assets. The runnable sessions with the same names are at `../`.
- `downloads/*.zip` are bundles of those session folders. Rebuild one from the
  session repo's committed files rather than by hand, e.g. from `..`:
  `git archive --format=zip -o from-asking-to-doing-site/downloads/session-1-introduction.zip HEAD 01_slidemaker`
  (`02_summarizer` → `session-2-skills-and-agents.zip`, `03_multitudes` →
  `session-3-workflow.zip`).
- Run `quarto preview` / `quarto render` from this folder. Pushing to `main`
  deploys the site, so commit and push only when the change should go live.
