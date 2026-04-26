# cypherpunks-gtm

Single-file launch console for CypherPunks. CRM, calendar, growth model, send-time heatmaps, bespoke per-target outreach copy, mint day playbook. Everything saves to `localStorage` — no backend, no analytics, no tracking.

## Stack

- One static HTML file (`index.html`)
- No build step, no dependencies
- Deploys as static on Vercel

## Local

Just open `index.html` in a browser, or:

```bash
npx serve .
# → http://localhost:3000
```

## Deploy to Vercel

Two paths. Use the second.

### Path 1 — push to GitHub, import in Vercel UI

```bash
# from the repo root
git init
git add .
git commit -m "init"
git branch -M main
git remote add origin git@github.com:YOUR_USER/cypherpunks-gtm.git
git push -u origin main
```

Then go to [vercel.com/new](https://vercel.com/new), pick the repo, accept defaults, deploy. Done.

### Path 2 — Vercel CLI from the terminal (faster)

```bash
npm i -g vercel
vercel login
vercel              # preview deploy → returns a URL
vercel --prod       # promote to production
```

First run asks: scope, link to existing project? (no), project name (`cypherpunks-gtm`), in which directory is your code? (`./`), modify settings? (no). Done in ~20 seconds.

## Backups

Hit `EXPORT CSV` on the Brief page every few days. Browser localStorage can be cleared by browser cleanup, profile resets, or accidental "reset all" clicks. The CSV is your safety net.

## Editing

All copy and target lists live as JS arrays inside `index.html`:

- `ARTISTS` — line ~970
- `COLLECTORS` — line ~1250
- `PRESS` — line ~1485
- `TWEETS` — line ~1650
- `TASKS` — line ~1755
- `HEATMAPS` — line ~1770

Edit, save, push. Vercel auto-deploys on push.

## Custom domain

After first deploy:

```bash
vercel domains add gtm.cypherpunks.art
# follow the DNS instructions Vercel prints
```

Or add via Vercel dashboard → project → Settings → Domains.
