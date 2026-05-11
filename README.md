# AI Build Day - Landing Page

## To deploy

Option A (fastest): Drag the folder to [Netlify Drop](https://app.netlify.com/drop)
Option B: `npx vercel build-day-site/`
Option C: GitHub Pages

## To update

- **Change pricing:** search for "$" in index.html
- **Change date:** search for "Next date coming soon" in index.html
- **Add testimonial:** copy a proof-card div and edit text
- **Swap Stripe link:** search for `STRIPE_LINK_TBD` and replace with the real Payment Link URL (occurs once per variant, on the "Reserve Your Spot" CTA)
- **Swap Cal link:** find the two `data-cta="book"` anchors per variant (Private Build Day card + footer CTA) and update the `href`. Currently `https://cal.com/alexsky/build-day-discovery`.

## To switch the primary variant

`index.html` is what's served at `/`. The other variants stay reachable at `/v2-speed.html`, `/v3-pain.html`, `/v4-cohort.html`. To promote a different variant to primary:

1. Copy the variant file you want over `index.html` (e.g. `cp v3-pain.html index.html`).
2. The `data-variant` attribute on `<body>` keeps the file's original tag (v1/v2/v3/v4), so analytics still distinguish "which variant ran as primary" in events.
3. Commit + push. GitHub Pages redeploys automatically.

To rename or add a new variant, mirror the same three CTA `data-cta` attributes (`reserve`, `book`, `book`) and the `data-variant` on `<body>`. The analytics block at the bottom of each file is identical and does the rest.

## Analytics

Click events fire on the two CTAs (`Reserve Your Spot`, `Book a Call`) across all variants. The wiring is **provider-agnostic** — works with Plausible or GA4, no-ops if neither is loaded.

**Event:** `CTA Click` with props `{ variant: 'v1'|'v2'|'v3'|'v4', cta: 'reserve'|'book' }`

### Option A — Plausible (recommended for static site)

1. Sign up at https://plausible.io (or self-host) and add the live domain.
2. In each `*.html` file, replace `data-domain="REPLACE_WITH_DOMAIN"` on the Plausible `<script>` tag with the live domain.
3. Events flow to the Plausible dashboard under "Goals → Custom Events → CTA Click".

### Option B — GA4

1. Create a GA4 property and copy the gtag.js snippet.
2. In each `*.html` file, delete the Plausible `<script>` tag and paste the GA4 snippet above the inline tracker.
3. Events flow as GA4 event name `CTA_Click` with `variant` and `cta` as parameters (register them as custom dimensions in GA4 Admin → Custom definitions).

### Verifying analytics locally

```bash
python -m http.server 8123
# Open http://127.0.0.1:8123/index.html, click Reserve / Book.
# Plausible script will 404 on REPLACE_WITH_DOMAIN until configured — that is expected.
# The inline tracker still no-ops cleanly; the click navigation is unaffected.
```

## Links to set up

1. **Stripe Payment Link:** Create at dashboard.stripe.com/payment-links
   - Product: "AI Build Day - Open Session"
   - Price: $750
   - Allow quantity adjustment
2. **Cal.com booking:** ✅ Live at `https://cal.com/alexsky/build-day-discovery` — "AI Build Day — Discovery Call", 30 min, Cal Video, 2h min notice, auto-confirm (event type id `5656599`)

## Live URL

- Primary (index/default variant): https://alexsalinsky.github.io/build-day-site/
- Variant 2 (speed framing): https://alexsalinsky.github.io/build-day-site/v2-speed.html
- Variant 3 (pain framing): https://alexsalinsky.github.io/build-day-site/v3-pain.html
- Variant 4 (cohort framing): https://alexsalinsky.github.io/build-day-site/v4-cohort.html

Hosted on GitHub Pages from `main` branch root. Repo: https://github.com/alexsalinsky/build-day-site

### Proposed custom domain (NOT purchased — needs CEO approval)

- First choice: `aibuildday.com` (clear, brandable, matches event name)
- Backup: `buildwith.ai` if `.com` is unavailable or too expensive
- Cheap-fallback: `aibuildday.co` or `aibuildday.dev`

Once a domain is approved and registered, configure DNS:
- `A` records for the apex pointing to GitHub Pages IPs: 185.199.108.153, 185.199.109.153, 185.199.110.153, 185.199.111.153
- `CNAME` for `www` -> `alexsalinsky.github.io`

Then add a `CNAME` file to this repo containing the domain, and enable HTTPS in repo Settings -> Pages.
