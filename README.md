# clever-proxy

A real web proxy: type an address, and the page loads through this server instead of your browser talking to the destination site directly. Unlike [`clever`](https://github.com/birdyboyiyert/clever) (a plain iframe browser — simple, but blocked by any site that refuses to be framed, and blocked by any network filter that just blocks the destination domain), this one actually gets around both, because the destination site only ever sees a request from *this server*, not from your browser.

## What this actually is

This is proxy technology in the same family as **Ultraviolet** and **Rammerhead** — the tech behind most "unblocked site" tools. Concretely, it's built on **[Scramjet](https://github.com/MercuryWorkshop/scramjet)** + the **Wisp protocol** (both from Mercury Workshop), scaffolded with their official [`create-proxy-app`](https://www.npmjs.com/package/create-proxy-app) generator.

**How it works:**
1. A service worker registers on the page and intercepts every request the page makes.
2. Instead of your browser resolving `example.com` itself, the request gets rewritten and sent to *this server* over a WebSocket (the Wisp protocol).
3. The server makes the real request to `example.com`, gets the response, and hands it back through the same WebSocket. The service worker unwraps it and serves it to the page as if it came from `example.com` directly.
4. Your network only ever sees you talking to wherever this server is hosted — never the actual destination. That's what lets it load sites a domain-based filter blocks, and sites that set `X-Frame-Options`/CSP to refuse being iframed (which is what stopped the plain `clever` iframe browser on sites like Google).

**Be honest with yourself about what this is for.** This exact technology is legitimately used for privacy and getting around state-level censorship — and is also the standard way students bypass school/work network filters, which is very likely against whatever policy governs that network. Nothing here checks or cares which one you're doing. That's on you.

## Running it locally

```bash
npm install
node server.js
```

Then open `http://localhost:3030`.

## Deploying it as an actual website

Unlike `clever`, **this cannot be a static site** — the server component (the part that actually fetches pages on your behalf) has to run continuously somewhere. GitHub Pages can't do that. A `render.yaml` is included for a one-click deploy to [Render](https://render.com)'s free tier:

1. Push this repo to GitHub (already done if you're reading this from the repo).
2. On Render: **New +** → **Blueprint** → connect this repo → it reads `render.yaml` automatically → Deploy.
3. Render gives you a `https://clever-proxy-xxxx.onrender.com` URL. That's the live site.

Free-tier Render web services spin down after 15 minutes of no traffic and take ~30-60s to wake back up on the next request — normal for a free-tier demo, not a bug. Other free Node hosts (Railway, Fly.io, Cyclic) work the same way, just point them at `npm install` / `node server.js`.

## Credits

- [Scramjet](https://github.com/MercuryWorkshop/scramjet) & [`create-proxy-app`](https://www.npmjs.com/package/create-proxy-app) by [Mercury Workshop](https://github.com/MercuryWorkshop) — AGPL-3.0
- License headers in the scaffolded source files are kept as generated; this project as a whole is AGPL-3.0 to match.
