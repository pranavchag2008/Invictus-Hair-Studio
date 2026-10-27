# Invictus-Hair-Studio
This is a website demo for Invictus Hair Studio in UC Davis, California


## Run it

**Requirements:** Node.js 20.19+ in the workspace PATH (the Freebuff Sites publish pipeline
requires it; Bun alone is not enough). This workspace uses Node 22.23.4 linked at
`~/.local/bin/node`.

```bash
bun install
bun run dev      # dev server on http://127.0.0.1:5178
bun run build    # type-check + static build into dist/
bun run preview  # preview the production build
npm install      # or: bun install
npm run dev      # dev server on http://127.0.0.1:5178
npm run build    # type-check + static build into dist/
npm run preview  # preview the production build
```

Built with Vite + React + TypeScript, plus [Leaflet](https://leafletjs.com/) for the interactive

---

## Deploying (only with the business's consent)
## Deployment

`bun run build` produces a fully static `dist/` that can be hosted anywhere. This concept has
**not** been published to a public URL. If a review URL is wanted, deploy the `dist/` folder to
a private/staging host first and get the business's sign-off before it is linked from anywhere
public.
Published on **Freebuff Sites (production)** on 27 Oct 2026.

- **Production URL:** https://site-3f9f15137096462ca4c14031e584f63b.freebuff.page
- **Site ID:** `17518f42-3e5f-4383-bc41-245dd3d9b7cf` (name: “Invictus Hair Studio — Website Concept”)
- **Worker:** [`worker/index.js`](worker/index.js) — serves the static build through `env.ASSETS`
- **Deploy manifest:** [`sites.manifest.json`](sites.manifest.json) — `dist/` as assets, `spa: true`
- **Bindings:** none (no D1, R2, auth or secrets for this static site)

Build and ship a change:

```bash
npm run build
# local Workers-runtime check (same asset + SPA behaviour as production)
npx wrangler dev --config wrangler.test.jsonc --port 8788
# then deploy the existing build with the Sites deployer using sites.manifest.json
```

## Public URL and consent

This concept is currently published at the production URL above, so it can be reviewed on any
device. It has **not** been approved by, and is not affiliated with, Invictus Hair Studio, and it
is not linked from the business's own channels. Get the owner's sign-off before presenting it as
their site — and take it offline with the Sites unpublish control if they decline.
