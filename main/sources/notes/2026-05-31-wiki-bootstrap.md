---
created: 2026-05-31T16:12:00-04:00
source: slack-dm
sender: Job (U03FS8NVDH9)
tags:
  - meta
  - infrastructure
  - wiki
title: Wiki bootstrap — Quartz + GitHub Pages
---

# Wiki bootstrap — Quartz + GitHub Pages

First note filed to the wiki. Captures the setup so the system has a memory of how it came to exist.

## What was set up

- **Vault**: `/Users/clueo/.openclaw/wiki/main` (OpenClaw memory wiki)
- **Renderer**: [Quartz 5](https://quartz.jzhao.xyz/) at `/Users/clueo/.openclaw/wiki/quartz`
- **Hosting**: GitHub Pages at <https://propheticwrit.github.io>
- **Repo**: <https://github.com/propheticwrit/propheticwrit.github.io>, branch `master`
- **Deploy**: GitHub Actions workflow at `.github/workflows/deploy.yml` builds on every push to `master`

## How notes flow now

1. Job sends a note in this Slack DM (explicit triggers like `note:` / `save:` / `remember:`, or anything clearly substantive).
2. Medensclaw writes it to `wiki/main/sources/notes/YYYY-MM-DD-<slug>.md` with frontmatter.
3. `~/.openclaw/workspace/scripts/wiki-publish.sh` commits and pushes to GitHub.
4. GitHub Actions runs Quartz, deploys to <https://propheticwrit.github.io>.
5. Echo back `📝 filed: <title>` to confirm.

## Gotchas learned during setup

- Quartz 5 requires Node 22. Node 25 (currently global) breaks the build. Installed `node@22` via Homebrew and pinned its path in the serve script — global node untouched.
- `npm run install-plugins` is broken; use `./quartz/bootstrap-cli.mjs plugin install` instead.
- `baseUrl` must be a valid URL (empty string crashes the build).
- The `propheticwrit.github.io` repo is a **user site**, so it serves from the repo root on `master`.

## Related

- `~/.openclaw/workspace/TOOLS.md` — Wiki section with full command reference
- `~/.openclaw/workspace/MEMORY.md` — Note-capture convention
