# OnlyMacApp Site — LIVE

Marketing + paywall landing page for OnlyMacApp. Static HTML/CSS, no build step, no tracking.

**Live URL:** https://drclawrepo.github.io/onlymacapp/
**Repo:** DrClawRepo/onlymacapp (public — required for GitHub Pages on free plan)
**Deploy:** push to main; Pages serves automatically.

## How the paywall works (deployed 2026-10-22)

1. Buy button on `index.html` \u2192 Stripe Payment Link **https://buy.stripe.com/28EbJ3d9mggt6AKeoz2Ji00** (US$19.99 one-time, "OnlyMacApp \u2014 Lifetime License", live mode, Pathfindars Consulting Pte Ltd account).
2. After payment Stripe redirects to `thanks.html`.
3. `thanks.html` links the DMG at `/dl/<first-16-of-sha256>/OnlyMacApp.dmg` \u2014 an unguessable path, blocked from crawlers via `robots.txt`.
4. **Rotating the download URL on each release:** rebuild DMG \u2192 take first 16 hex chars of `shasum -a 256` \u2192 new `dl/<hash>/` folder \u2192 delete old folder \u2192 update the link in `thanks.html` \u2192 commit + push.

## Release procedure

```sh
cd /Users/wormfam/Projects/OnlyMacApp/app && bash scripts/build-app.sh
# build DMG per repo A README, then:
shasum -a 256 dist/OnlyMacApp.dmg   # first 16 chars = new /dl/ folder name
```

## Security notes

- The download link is obscurity-based: anyone who has it can share it. Acceptable for launch; upgrade path is Cloudflare Worker + R2 signed URLs (server-side Stripe session verification) or Stripe's built-in file delivery.
- App is ad-hoc signed, NOT notarized \u2014 buyers must right-click \u2192 Open on first launch. Apple Developer Program (US$99/yr) needed to fix.
- No Stripe secrets in this repo (verified). Key lives in the Hermes secrets file.
