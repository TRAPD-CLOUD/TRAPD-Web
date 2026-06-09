# TRAPD — Homepage

Marketing homepage for **TRAPD**, a modular, API-first, self-hosted security
operations platform — from a single homelab box to a full enterprise SOC.

It is a single static page (`index.html`) with no build step and no runtime
dependencies. Everything it needs ships in `assets/`. That makes it trivial to
host anywhere — Vercel, IONOS, or your own machine.

## Structure

```
.
├── index.html              # the homepage (entry point)
├── assets/
│   ├── tokens.css          # TRAPD design system — colors, type, radius (OKLCH)
│   ├── logo_white.svg      # wordmark/logo (light, used on dark surfaces)
│   ├── logo_black.svg      # wordmark/logo (dark, used on light surfaces / favicon)
│   └── integrations/       # integration logos (ClickHouse, Supabase, Redis, …)
├── vercel.json             # Vercel hosting config (headers + caching)
├── .htaccess               # Apache config for IONOS classic webspace
└── .gitignore
```

Fonts (Outfit + JetBrains Mono) are pulled from Google Fonts via an `@import`
in `tokens.css`, so an internet connection is needed for the exact typefaces;
the page falls back to system fonts gracefully if offline.

## Run locally

The page is plain HTML/CSS/JS — no toolchain required.

**Option A — just open it**

Open `index.html` in your browser. (Some browsers restrict relative paths on
the `file://` protocol; if assets don't load, use Option B.)

**Option B — a tiny local server** (recommended)

```bash
# Python 3 (preinstalled on macOS/Linux)
python3 -m http.server 8000

# …or Node, if you have it
npx serve .
```

Then visit <http://localhost:8000>.

## Deploy to Vercel

This repo is a zero-config static deployment.

- **Via the dashboard:** import the repo at <https://vercel.com/new>. Leave the
  framework preset as **Other**, leave build command and output directory empty.
  Vercel serves `index.html` at the root. `vercel.json` adds cache and security
  headers.
- **Via the CLI:**
  ```bash
  npm i -g vercel
  vercel          # preview deploy
  vercel --prod   # production deploy
  ```

## Deploy to IONOS

Two common paths:

- **Classic webspace (FTP/SFTP):** upload the entire repo contents (`index.html`,
  `assets/`, `.htaccess`) to your web root (often `/` or `htdocs`). The included
  `.htaccess` sets the default document, compression, caching, and security
  headers for Apache. Make sure hidden files (`.htaccess`) are uploaded too.
- **IONOS Deploy Now (Git-based):** connect this repository, choose a **static**
  project with **no build command** and the project root (`./`) as the output
  directory.

## Hosting anywhere else

Any static host works — Netlify, Cloudflare Pages, GitHub Pages, S3 + CloudFront,
nginx/Apache. Point the host at the repository root and serve `index.html`.

## Editing content

All copy and markup live in `index.html`. Design tokens (colors, fonts, radii)
live in `assets/tokens.css` — change a token there and it updates everywhere.
The roadmap, capabilities, and panel figures are honest placeholders; swap in
real values as the project evolves.
