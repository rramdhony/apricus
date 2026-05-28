# Apricus

Single-page site for apricus-mu.com.
Apricus is a food distribution and supply company based in Mauritius.

## Deployment

- **Type:** Cloudflare Worker (name: `apricus`)
- **Live URL:** https://www.apricus-mu.com
- **Pipeline:** push to `main` → GitHub Actions → `wrangler deploy` → live in ~60s
- **Config:** `wrangler.toml` at repo root, deploys only the `public/` directory

## Architecture

The deployable file is `public/index.html` — this is what Wrangler serves.
`wrangler.toml` uses `[assets] directory = "./public"`.

### Assets — NOT in this repo

All images on the live site are served from a separate CDN:
**https://assets.apricus-mu.com/**

Referenced in `public/index.html` as absolute URLs, e.g.:
`https://assets.apricus-mu.com/hero-harbour.jpg`

Do not move these to the repo or change them to relative paths.
To update an image, upload the new file to `assets.apricus-mu.com` directly.

### Reference files in repo root (not deployed)

The root folder contains source/reference images with numeric prefixes
(e.g. `04-hero-harbour.jpg`) and planning docs in `apricus files/`.
These are version-controlled for reference but are **not served** by the Worker.

The outdated `index.html` at root is also kept for reference — the live
version is always `public/index.html`.

## What to avoid

- Do not edit the root `index.html` — edit `public/index.html` instead
- Do not add assets to `public/` — images are on `assets.apricus-mu.com`
- This is a Worker, not Cloudflare Pages — do not use `wrangler pages deploy`
