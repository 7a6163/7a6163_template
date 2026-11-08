# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this repo is

A GitHub profile README template built on [github-profile-summary-cards](https://github.com/vn7n24fzkq/github-profile-summary-cards). There is no source code, build, lint, or test step. The only logic is one GitHub Actions workflow; everything else is generated SVG output plus `README.md`.

## How it works

- The repo was created from the template `vn7n24fzkq/github-profile-summary-cards-example`. It is not a fork, so there is no upstream to sync. `@release` always pulls the newest version of the action, so only the workflow file can fall behind. Compare its options with the action's README.
- `.github/workflows/profile-summary-cards.yml` runs the `vn7n24fzkq/github-profile-summary-cards@release` action for `github.repository_owner`. It runs daily at 00:00 UTC and on `workflow_dispatch`. Its options: `BRANCH_NAME` must be `master` (the action defaults to `main`), `TIME_ZONE` sets the timezone for the productive-time card, and `THEME` empty means every theme.
- The action authenticates with the repo secret `SUMARRY_CARDS_TOKEN` (the misspelling is the real secret name, so don't "fix" it unless the secret is renamed too). It writes SVGs to `profile-summary-card-output/<theme>/` and commits them as `profile-summary-cards[bot]` with the message "Generate profile summary cards".
- Each theme directory holds `0-profile-details.svg`, `1-repos-per-language.svg`, `2-most-commit-language.svg`, `3-stats.svg`, `4-productive-time.svg`, plus a `README.md` preview.
- `README.md` embeds the cards by absolute `raw.githubusercontent.com` URLs. These still point at the upstream example repo (`vn7n24fzkq/github-profile-summary-cards-example`, `vue` theme), not this repo (`7a6163/7a6163_template`). Change the URLs to show this account's own cards.

## Working here

- Don't hand-edit files under `profile-summary-card-output/`. The bot regenerates them on every run, and most of the git history is bot commits.
- Run the workflow manually: `gh workflow run profile-summary-cards.yml`.
- Don't copy the upstream README's cron `"* */24 * * *"`. It fires every minute of hour 0 UTC, not once a day.
- GitHub only shows the README on the profile page when the repo is named after the user (here that would be `7a6163/7a6163`).
