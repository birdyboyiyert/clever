# clever

Type an address, it loads — even sites that are otherwise blocked or unavailable to you directly.

## How it works

Instead of your browser going straight to the site, the request is routed through this server first. The server fetches the real page and hands it back. Because your device only ever talks to this server (not the destination site directly), it works in situations where the direct connection wouldn't — a blocked domain, a site that refuses to be shown inside another page, etc.

Built on **[Scramjet](https://github.com/MercuryWorkshop/scramjet)** and the **Wisp protocol** (both from Mercury Workshop), scaffolded with their official [`create-proxy-app`](https://www.npmjs.com/package/create-proxy-app) generator.

**Be honest with yourself about what you're using this for.** This kind of tool gets used for legitimate things (privacy, getting around state-level censorship) and also to get around rules your school or workplace has set on their own network. Nothing here checks or cares which one you're doing — that's on you.

## Running it locally

```bash
npm install
node server.js
```

Then open `http://localhost:3030`.

[![Deploy to Render](https://render.com/images/deploy-to-render-button.svg)](https://render.com/deploy?repo=https://github.com/birdyboyiyert/clever)

## Deploying it as an actual website

This needs a real server running continuously — it can't be a static site (GitHub Pages, etc. won't work). A `render.yaml` is included for a one-click deploy to [Render](https://render.com)'s free tier:

1. Push this repo to GitHub (already done if you're reading this from the repo).
2. On Render: **New +** → **Blueprint** → connect this repo → it reads `render.yaml` automatically → Deploy.
3. Render gives you a live `https://clever-xxxx.onrender.com` URL.

Free-tier Render services spin down after 15 minutes of no traffic and take ~30-60s to wake back up on the next request — normal for a free-tier demo, not a bug.

## Credits

- [Scramjet](https://github.com/MercuryWorkshop/scramjet) & [`create-proxy-app`](https://www.npmjs.com/package/create-proxy-app) by [Mercury Workshop](https://github.com/MercuryWorkshop) — AGPL-3.0
- License headers in the scaffolded source files are kept as generated; this project as a whole is AGPL-3.0 to match.
