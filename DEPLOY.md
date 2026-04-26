# Deploy

Two scripts: pick one. Run from the unzipped `cypherpunks-gtm` folder.

## A — Vercel CLI (fastest, no GitHub needed)

```bash
# one-time
npm i -g vercel

# every time
cd cypherpunks-gtm
vercel login                    # opens browser
vercel                          # preview deploy → outputs a *.vercel.app URL
vercel --prod                   # promote to production
```

First `vercel` run asks four questions:

```
? Set up and deploy "~/cypherpunks-gtm"?         Y
? Which scope do you want to deploy to?          (your account)
? Link to existing project?                      N
? What's your project's name?                    cypherpunks-gtm
? In which directory is your code located?       ./
? Want to modify these settings?                 N
```

That's it. Future deploys are just `vercel --prod`.

## B — GitHub + Vercel (auto-deploy on push)

```bash
cd cypherpunks-gtm
git init
git add .
git commit -m "init: gtm console v2"
git branch -M main

# create a new repo at github.com/new (private if you want), then:
git remote add origin git@github.com:YOUR_USER/cypherpunks-gtm.git
git push -u origin main
```

Then at [vercel.com/new](https://vercel.com/new):

1. Import the `cypherpunks-gtm` repo
2. Framework Preset: **Other**
3. Root Directory: **./**
4. Build Command: **leave empty**
5. Output Directory: **leave empty** (or `.`)
6. Click Deploy

Future pushes to `main` auto-deploy to production. Branches get preview URLs.

## Custom domain

After first deploy:

```bash
vercel domains add gtm.yourdomain.art
```

Vercel prints the DNS records — add them at your registrar. Propagation usually <60s on Cloudflare, up to 30min elsewhere.

## Update workflow

Edit `index.html` locally → test by opening it in a browser → push.

```bash
# A: CLI
vercel --prod

# B: GitHub
git add . && git commit -m "update: copy" && git push
```

## Auth — keep it private

If you don't want this public, two options:

1. **Vercel password protection** (paid plan): project → Settings → Deployment Protection → enable for production
2. **Self-host basic auth**: keep it on GitHub private + share the .vercel.app URL only with your team

For a 30-day campaign, option 1 is cleanest.

## Safety

The dashboard saves everything to your browser's `localStorage`. It does NOT sync between devices. Two implications:

- If you start on phone, end on laptop: you'll have two separate sets of CRM data. Pick one as primary.
- Hit **EXPORT CSV** every ~3 days. Save the file somewhere safe. If your browser ever clears storage, that CSV is your only backup.
