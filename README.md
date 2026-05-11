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
- **Swap Cal link:** replace the href on both "Book a Call" buttons + footer CTA

## Links to set up

1. **Stripe Payment Link:** Create at dashboard.stripe.com/payment-links
   - Product: "AI Build Day - Open Session"
   - Price: $750
   - Allow quantity adjustment
2. **Cal.com booking:** Create a 30-min "Build Day Discovery Call" event type

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
