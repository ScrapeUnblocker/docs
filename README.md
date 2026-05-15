# ScrapeUnblocker Documentation

Source for [developers.scrapeunblocker.com](https://developers.scrapeunblocker.com), hosted by [Mintlify](https://mintlify.com).

## Repo layout

```
.
├── docs.json                      # Mintlify config (theme, nav, branding)
├── introduction.mdx               # Landing page
├── quickstart.mdx                 # First request walkthrough
├── authentication.mdx             # API key handling
├── errors.mdx                     # Status code reference
├── rate-limits.mdx                # Concurrency + quota docs
├── changelog.mdx                  # Release notes
├── api-reference/
│   ├── introduction.mdx           # Endpoint overview
│   └── openapi.json               # Auto-generates 3 endpoint pages
├── guides/                        # Use-case walkthroughs
│   ├── page-source.mdx
│   ├── parsed-data.mdx
│   ├── serp-scraping.mdx
│   ├── image-fetching.mdx
│   ├── country-targeting.mdx
│   ├── cookies-and-sessions.mdx
│   └── handling-failures.mdx
├── sdks/                          # Code examples by language
│   ├── curl.mdx
│   ├── python.mdx
│   ├── nodejs.mdx
│   └── scrapy.mdx
├── logo/
│   ├── light.svg
│   └── dark.svg
└── favicon.svg
```

## How to deploy this (one-time setup)

### 1. Push this folder to a new GitHub repo

```bash
cd C:\Users\Uosis\Desktop\github\scrapeunblocker-docs
git init
git add .
git commit -m "initial docs"
git branch -M main
git remote add origin https://github.com/YOUR_GITHUB_USER/scrapeunblocker-docs.git
git push -u origin main
```

### 2. Sign up for Mintlify and connect the repo

1. Go to [mintlify.com](https://mintlify.com) and sign in with GitHub.
2. Click **Add deployment** → pick the `scrapeunblocker-docs` repo.
3. Mintlify auto-detects `docs.json` and deploys to a temporary URL like `scrapeunblocker.mintlify.app`. This takes ~2 minutes.

### 3. Configure the custom subdomain

In Mintlify dashboard → **Settings** → **Custom domain**:

1. Enter `developers.scrapeunblocker.com`.
2. Mintlify shows you a CNAME target (e.g. `cname.mintlify.app`).
3. Add a DNS record at your domain registrar:

   ```
   Type:  CNAME
   Name:  developers
   Value: cname.mintlify.app   (whatever Mintlify gives you)
   TTL:   3600
   ```

4. Wait 5-30 minutes for DNS propagation. Mintlify will show a green checkmark when it's live.

### 4. Done

`https://developers.scrapeunblocker.com` is live. HTTPS cert is auto-provisioned by Mintlify.

## How to make changes

### Edit docs locally

```bash
npm i -g mintlify
cd C:\Users\Uosis\Desktop\github\scrapeunblocker-docs
mintlify dev
```

Opens at `http://localhost:3000` with hot reload. Edit any `.mdx` file and the browser updates.

### Publish

Push to `main`. Mintlify auto-deploys on every push, usually within 60 seconds.

```bash
git add .
git commit -m "describe change"
git push
```

### When the API changes

If you add, remove, or modify endpoints in `scrapeunblocker-api`:

1. Regenerate `docs/openapi.json` in the API repo (FastAPI does this automatically at `/openapi.json` when the server runs).
2. Copy it into this repo: `cp ../scrapeunblocker-api/docs/openapi.json api-reference/openapi.json`.
3. Commit and push. Mintlify regenerates the API Reference pages automatically.

You can automate step 2 with a GitHub Action if you want changes to flow from the API repo to docs without manual copying - ask Claude later to set that up.

## Branding

Defined in `docs.json`. Current palette:

- Primary: `#00C896` (mint green)
- Background dark: `#0A0A0B`
- Default theme: dark mode

To change colors, edit `docs.json` → `colors` and `background`.

To change the logo, replace `logo/light.svg` and `logo/dark.svg`. SVGs work best - PNG also works but doesn't scale.

## Pricing

Mintlify's Hobby tier is free and includes:

- Custom domain
- Unlimited public pages
- GitHub auto-deploy
- 1 admin user

Paid tiers ($150/mo+) add team members, AI chat (the "Ask AI" button), analytics, and SSO. AI chat may also be available on the free tier - check during signup.

If AI chat is gated to a paid tier and you want it free, the alternative platform [Scalar](https://scalar.com) has equivalent quality with no AI feature paywall. The docs in this repo would need light adjustments to migrate (config file format differs).
