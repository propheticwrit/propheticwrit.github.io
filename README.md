# Medensclaw Wiki

OpenClaw memory wiki vault rendered with [Quartz 5](https://quartz.jzhao.xyz/).

## Layout

- `main/` — the wiki vault (raw markdown, ingested via `openclaw wiki ingest`)
- `quartz/` — the Quartz site generator that renders `main/` to HTML

## Local preview

```sh
cd quartz
PATH="/opt/homebrew/opt/node@22/bin:$PATH" ./quartz/bootstrap-cli.mjs build -d ../main --serve --watch
```

Open <http://localhost:8080>.

Or use the workspace helper script: `~/.openclaw/workspace/scripts/wiki-serve.sh`.

## Deploy (GitHub Pages)

1. Create a GitHub repo and push this directory.
2. In repo *Settings → Pages*, set *Source* to **GitHub Actions**.
3. Update `quartz/quartz.config.yaml`'s `baseUrl` to `<username>.github.io/<repo>` (or your custom domain).
4. Commit and push — `.github/workflows/deploy.yml` builds and deploys automatically.

## Notes

- Quartz requires Node.js 22+. Node 25 currently has issues with this codebase.
- The `_attachments`, `_views`, and `reports` folders are excluded from the rendered site (see `quartz.config.yaml` `ignorePatterns`).
- Plugin installs happen via `./quartz/bootstrap-cli.mjs plugin install` (don't use `npm run install-plugins`, it's broken on current Node versions).
