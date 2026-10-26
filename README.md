# webstrides.com

The company site for WebStrides LLC. One static page: no framework, no build step.
Edit `index.html` and push; GitHub Pages serves the repo root.

## Files

- `index.html` — the page, styles inline. Black and white on purpose: the company has its own look,
  separate from FluentStrides. The WEBSTRIDES wordmark is hand-drawn SVG strokes in the page (each
  letter a `<path>` on a 100-unit-tall grid, stroke 20). Motion draws it in on load, pulls its
  letters apart on scroll, traces the circle and grows the crosshairs. Reduced motion, or Motion
  failing to load within 3 s, shows everything as it is.
- `404.html` — served by GitHub Pages for any unknown path. Uses absolute paths (`/fonts/…`) because
  it can be served at any depth.
- `fonts/InterTight-latin.woff2` — Inter Tight, one variable file covering weights 300–500, Latin
  subset, from Google Fonts. Licence: `fonts/OFL.txt`.
- `vendor/motion.js` — [Motion](https://motion.dev) 12.43.0's standalone build (`dist/motion.js` from
  the npm package), exposing `window.Motion`. Licence: `vendor/MOTION-LICENSE.md`. To upgrade:
  `npm pack motion@<version>`, copy `package/dist/motion.js` over it.
- `favicon.svg`, `favicon-32.png`, `apple-touch-icon.png` — the "W" from the wordmark. iOS needs the
  PNG; the touch icon is full-bleed because iOS rounds the corners itself.
- `assets/og.png` — 1200×630 link-preview image (iMessage, Slack, LinkedIn, email).
- `CNAME` — tells GitHub Pages the custom domain.
- `.nojekyll` — serve files as they are.

The font and Motion are served from this site, so a visit makes no requests to anyone else. Keep
it that way; it's why the site needs no privacy notice.

## Adding a product

Copy the `<a class="product">` row under Products in `index.html`, change the number (`002`), name,
description and link. The PNGs were rendered from HTML in headless Edge at their exact sizes; if
the wordmark or tagline changes, re-render `assets/og.png` the same way.

## Deploy (GitHub Pages)

1. Create the repo `web-strides/webstrides` on GitHub.
2. Push `main`:
   ```sh
   git remote add origin git@github-fluentstrides:web-strides/webstrides.git
   git push -u origin main
   ```
   `github-fluentstrides` is the SSH alias that uses the web-strides key.
3. Repo **Settings → Pages**: Source "Deploy from a branch", branch `main`, folder `/ (root)`.
   Custom domain: `webstrides.com`.
4. At the domain registrar, add DNS records:

   | Type | Name | Value |
   |---|---|---|
   | A | @ | 185.199.108.153 |
   | A | @ | 185.199.109.153 |
   | A | @ | 185.199.110.153 |
   | A | @ | 185.199.111.153 |
   | CNAME | www | web-strides.github.io |

   Keep the MX, SPF, DKIM and DMARC records Proton gives you for email; they don't conflict.
5. Once the certificate is issued (minutes to a day), tick **Enforce HTTPS**.

## Later

- Link Privacy and Terms in the footer once FluentStrides has them.
