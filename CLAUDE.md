# Zinkann Performance website — notes for Claude

This repo is the live website for **zinkannperformance.com**, a cycling coaching business (GitHub owner: mpzinkann). The owner is not a developer, so explain things in plain language and keep steps simple.

## Before you change anything

1. **Get the latest version first:** `git fetch origin && git reset --hard origin/main` (or `git pull`). More than one Claude chat may edit this site. Working from an old copy has already overwritten another chat's changes once.
2. Make changes on **main** and push to **main**. There are no other branches.
3. Only one chat should be editing at a time.

## How hosting works

- Hosted on **Cloudflare Workers** (static assets), project name **zinkannperformance**.
- Cloudflare is connected to this repo. Every push to `main` builds and goes live within a minute or two.
- Test address: https://zinkannperformance.mpzinkann.workers.dev/
- Custom domains: `zinkannperformance.com` and `www.zinkannperformance.com`. The domain is registered with Cloudflare.
- Cloudflare's build links say "previews/main", but pushes to main do reach the live site.
- Claude's web tools can't load zinkannperformance.com because Cloudflare blocks AI crawlers there. Check the `workers.dev` address instead; it serves the same site.
- GitHub Pages may still be switched on for this repo. It isn't used and can be turned off.

## Files

- `wrangler.jsonc`: Cloudflare settings. `name` must stay `zinkannperformance`. Publishes the `public/` folder. The empty `previews` block is required, or preview builds fail.
- `public/index.html`: the main page. Sections switched by URL hash: `#about` (Home), `#blog`, `#contact`. Old `#plans` and `#faq` links redirect to the pages below.
- `public/plans.html` and `public/faq.html`: separate pages (better for Google). They are copies of the index shell (header, footer, styles, menu script) with only their own section. **A change to the header, footer, nav or shared CSS must be made in index.html, plans.html, faq.html, terms.html and every blog post.**
- `public/sitemap.xml` and `robots.txt`: for Google. Add new pages to the sitemap.
- `public/blog/*.html`: individual blog posts (cornering, first FTP test, durability, No Coasting, Zone 2).
- `public/terms.html`: Terms and Privacy page, linked from the footer and the contact form.
- `public/images/`: photos. They're stored as separate files, not embedded in the HTML, so pages load fast.

## Contact form

- Sends through **Web3Forms** (`api.web3forms.com`). The access key is in the script near the bottom of `index.html`.
- Has a hidden honeypot checkbox (`f-bot`) to stop spam bots. No captcha at the moment. Cloudflare Turnstile is the option if spam becomes a problem.
- Messages go to the owner's email. `coach@zinkannperformance.com` is shown on the site and works.
- The owner has tested the form and email, and both work.

## Look and feel

- Fonts: **Russo One** (italic, uppercase) for headings and buttons, **Barlow** for body text.
- Colors: black, white, light grey bands, and an orange accent, **#F25C1E**.
- Style: slanted section edges, skewed buttons, bold black borders. Black hero banners with photos fading in from the right.
- Mobile: hamburger menu, plus a fixed orange "Let's get faster" button along the bottom of the screen.

## Ideas not done yet

- Page description and a sharing preview image (Open Graph tags), so links look good when shared.
- Google Search Console setup.
- Cloudflare Web Analytics.
- The footer used to read "© 2026 Zinkann Performance". A later update removed the year, and it's worth re-adding if the owner wants it.
