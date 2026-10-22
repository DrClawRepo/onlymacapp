# OnlyMacApp Site

Marketing + paywall landing page for OnlyMacApp. Static HTML/CSS, no build step, no tracking.

## Structure

- `index.html` — hero, tool categories, experience, privacy, pricing, FAQ, footer
- `styles.css` — full styling
- `assets/img/` — app icon at 1024/512/128

## Paywall wiring (when launching)

1. Create a Stripe Payment Link (or Lemon Squeezy / Gumroad product) for $19.99.
2. Host `OnlyMacApp.dmg` privately (S3/R2 signed URLs, or Stripe's built-in file delivery).
3. Replace the `[data-checkout]` handler in `index.html` with your checkout URL.
4. Host anywhere static: GitHub Pages, Netlify, Cloudflare Pages, Vercel.

Prototype note: the buy button currently shows a placeholder alert instead of real checkout.

## Local preview

```sh
cd OnlyMacApp-site && python3 -m http.server 8080
# open http://localhost:8080
```
