# skeeterless.us

Marketing website for **SkeeterLess** — industrial-grade, CO2-powered mosquito trap installation and
maintenance, based in Knoxville, TN. Static HTML/CSS/JS, built to deploy on GitHub Pages under the
custom domain `skeeterless.us`.

## Structure

```
index.html                     Home page (all sections, SEO meta tags, JSON-LD)
thank-you.html                 Post-submit redirect target for the contact form (noindex)
404.html                       Custom not-found page
css/style.css                  All styling
js/script.js                   Mobile nav toggle + footer year
assets/favicon.svg             Site icon / logo mark
robots.txt                     Crawler rules + sitemap pointer
sitemap.xml                    Single-page sitemap
CNAME                          GitHub Pages custom domain config (skeeterless.us)
.github/workflows/deploy.yml   GitHub Actions workflow that deploys to Pages on every push to master
```

## Before going live

1. **Contact form (Formspree)** — In `index.html`, the contact `<form>` posts to
   `https://formspree.io/f/YOUR_FORM_ID`. Create a free form at [formspree.io](https://formspree.io),
   set it to send to `sales@skeeterless.us`, and replace `YOUR_FORM_ID` with your real form ID.
2. **OG image** — `og:image` / `twitter:image` point to `/assets/og-image.png`, which doesn't exist yet.
   Add a 1200×630 branded image at that path so link previews (iMessage, Slack, Facebook, etc.) render
   correctly.
3. **Verify contact info** — Phone `(740) 877-2320` and email `sales@skeeterless.us` are wired into the
   hero, contact section, `tel:`/`sms:`/`mailto:` links, and the JSON-LD structured data. Update in both
   places (`index.html` search for the number/email) if either ever changes.

## Deploying to GitHub Pages with a custom domain

Deployment is automated via [`.github/workflows/deploy.yml`](.github/workflows/deploy.yml) — every push
to `master` builds and publishes the site with no build step required (it just uploads the repo root as
the Pages artifact).

1. Push this repo to GitHub.
2. In the repo, go to **Settings → Pages** and under **Build and deployment → Source**, select
   **GitHub Actions** (not "Deploy from a branch").
3. Push to `master` (or run the workflow manually from the **Actions** tab) — this triggers the
   `Deploy to GitHub Pages` workflow, which publishes the site.
4. Still under **Settings → Pages**, enter `skeeterless.us` under **Custom domain** and save (this repo
   already has a `CNAME` file, so GitHub should pick it up automatically — but set it in the UI too so
   GitHub provisions HTTPS).
5. At your DNS provider, point the apex domain at GitHub Pages:
   - `A` records for `skeeterless.us` → `185.199.108.153`, `185.199.109.153`, `185.199.110.153`,
     `185.199.111.153`
   - Optionally a `CNAME` record for `www.skeeterless.us` → `<your-github-username>.github.io`
6. Wait for DNS to propagate, then enable **Enforce HTTPS** in the Pages settings once the certificate
   is issued.

## Local preview

No build step — just serve the folder statically, e.g.:

```
npx serve .
```
