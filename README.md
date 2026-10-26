# webstrides.com

The company site for WebStrides LLC. One static page: no framework, no build step.
Edit `index.html` and push; GitHub Pages serves the repo root.

## Files

- `index.html` — the page, styles inline. Black and white on purpose: the company has its own look,
  separate from FluentStrides. Inter Tight from Google Fonts; the WEBSTRIDES wordmark is hand-drawn
  SVG strokes in the page (each letter a `<path>` on a 100-unit-tall grid, stroke 20).
  [Motion](https://motion.dev) 12.43.0, loaded from jsDelivr, draws the wordmark in on load and
  pulls its letters apart on scroll. Reduced motion, or Motion failing to load within 3 s,
  shows the wordmark as it is.
- `favicon.svg` — the "W" from the wordmark, real vector paths.
- `CNAME` — tells GitHub Pages the custom domain.
- `.nojekyll` — serve files as they are.

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
- Add each new product as another card under Products.
