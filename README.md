# Invictus-Hair-Studio
This is a website demo for Invictus Hair Studio in UC Davis, California


# Invictus Hair Studio — Unofficial Website Concept

A premium, single-page barber website built as a **demonstration concept** for Invictus
Hair Studio in Davis, California.

> **This is not the business's official website.** It is an independent design concept, not
> affiliated with, endorsed by, or approved by Invictus Hair Studio. The design-side disclaimer
> has been removed at the client's request; the page is still marked `noindex, nofollow`, and the
> browser title/meta description still identify it as a concept.

---

## Run it

**Requirements:** Node.js 20.19+ in the workspace PATH (the Freebuff Sites publish pipeline
requires it; Bun alone is not enough). This workspace uses Node 22.23.4 linked at
`~/.local/bin/node`.

```bash
npm install      # or: bun install
npm run dev      # dev server on http://127.0.0.1:5178
npm run build    # type-check + static build into dist/
npm run preview  # preview the production build
```

Built with Vite + React + TypeScript, plus [Leaflet](https://leafletjs.com/) for the interactive
map. No UI framework — the design system is plain CSS tokens in `src/styles/global.css`.

---

## Updating the site

### 1. Business details, services and prices

Everything factual lives in **one file**: [`src/content/site.ts`](src/content/site.ts).

| What you want to change | Field in `src/content/site.ts` |
| --- | --- |
| Business name / wordmark | `business.name`, `business.subName`, `business.fullName` |
| Address | `business.addressLine1`, `business.addressLine2`, `business.geo` |
| Phone | `business.phone`, `business.phoneHref` (digits only, with country code) |
| Booking link | `business.bookingUrl` |
| Instagram | `business.instagram`, `business.instagramHandle` |
| Opening hours | `hours` (edit `open` / `close`; `days` controls the "Today" highlight) |
| Services & prices | `services` — add, remove or reorder entries freely |
| Section headings and intro copy | `copy` |
| Gallery captions / credits | `gallery` |
| Map tiles / zoom / attribution | `map` (Leaflet tile URL and attribution) |

Adding a third service is just a new object in the `services` array — the grid, the
marquee strip and the mobile price bar all read from it.

### 2. Photos

Placeholder photos are in [`public/images`](public/images). To swap in approved photography:

1. Drop the new file into `public/images/` (JPEG or WebP, roughly 1200–2200px wide).
2. Point the matching `src` in the `gallery` array (or the hero / about / booking images)
   at the new file, e.g. `"/images/gallery-01-razor.jpg"`.
3. Update `alt` text and the `credit` entry. **Remove the placeholder notice** in
   `galleryNotice` once real, approved photos are in place.

Images referenced in code:

- Hero background: `public/images/hero-shop.jpg` (in `src/components/Hero.tsx`)
- About image: `public/images/about-chair.jpg` (in `src/components/About.tsx`)
- Booking band: `public/images/booking-bg.jpg` (in `src/components/Booking.tsx`)
- Gallery: six files listed in `site.gallery`

### 3. Map

The Visit section uses a Leaflet map centered on `business.geo`:

- A brass pin marks the studio with a popup and a directions link.
- **Use my location** asks the browser for the visitor's position, drops a blue "you are here"
dot, zooms to show both points, and reports the straight-line distance.
- **Get directions** opens Google Maps — with the visitor's coordinates as the origin once location
is on — and **Apple Maps** is offered as a second option (both open the phone's map app on mobile).
- On touch devices the map starts locked behind a "Tap to explore the map" overlay so the page
still scrolls normally; tapping it enables pan and pinch-zoom.

Tiles come from OpenStreetMap's public tile server, which is fine for a low-traffic concept but
**not** intended for production traffic. Before launch, switch `map.tileUrl` to a provider with an
SLA and API key (MapTiler, Stadia, Mapbox) and update `map.attribution`.

### 4. Booking

The site deliberately has **no booking engine**. Every "Book" button opens the studio's
existing Booksy page in a new tab (`business.bookingUrl`). If the owner prefers a different
booking provider or a second listing, change that one URL.

---

## Fact sheet

### Verified from public sources (October 2026)

| Fact | Value | Source |
| --- | --- | --- |
| Address | 903 3rd Street, Davis, CA 95616 | Booksy listing (as "903 3rd street, Davis, 95616") |
| Phone | (530) 650-2351 | Yelp business listing (mirrored on Yahoo Local) |
| Service — Haircut | $40, 45 min | Booksy listing |
| Service — Cut + Beard | $50, 45 min | Booksy listing |
| Booking page | `booksy.com/en-us/1440419_invictus-barber-studio_barber-shop_134667_davis` | Linked from the Booksy listing |
| Instagram | @invictus_hairstudio, bio "Davis, Ca / Link in the bio to book appointment" | Public Instagram profile |
| Listed business name | "Invictus Barber Studio" (Booksy), "Invictus" (Yelp/MapQuest) | Public listings |
| Instagram account name | "UC Davis barbershop" | Public Instagram profile |
| Rating shown on listing | 4.8 from 17 reviews | Booksy listing — **deliberately not displayed on the site** |
| Storefront coordinates | ≈ 38.5453, −121.7379 | Geocoded from the street address via OpenStreetMap |

Hours in the site (Mon–Fri 10:00 AM–8:00 PM, Sat 9:00 AM–5:00 PM, Sun 1:00 PM–5:00 PM)
come from the Yelp-derived public listing.

### Needs confirmation before this is shown as anything but a concept

1. **Business name.** The Booksy listing says *Invictus Barber Studio*; the Instagram handle
   and the client brief say *Invictus Hair Studio*. The site uses "Invictus Hair Studio" with
   the alternate name noted in the footer.
2. **Duplicate Booksy listings.** Two listings exist for the same address:
   `1440419` (4.8, 17 reviews, services listed) and `1429677` (4.8, 33 reviews, no services
   shown). The site links to `1440419`; confirm which one the owner uses.
3. **Opening hours.** Booksy shows 10:00 AM – 9:00 PM for the current day, while the
   Yelp-derived listing shows Mon–Fri 10:00 AM – 8:00 PM. Booksy also shows several
   consecutive days as "Closed", which most likely reflects fully booked days rather than
   closures. All hours need confirming.
4. **Services and prices.** Only two services are publicly listed. Any beard-only, line-up,
   kids, or package pricing is unknown and was intentionally not invented.
5. **Phone number.** Sourced from Yelp, not from a first-party page — confirm it is current.
6. **Staff.** Reviews and the Instagram bio reference barbers (e.g. owner @julycutz_,
   and reviews mentioning "Marco"/"Julio"), but no names, roles, or biographies are published
   here. A team section needs first-party confirmation and photos.
7. **Walk-ins, parking, accessibility, payment methods, policies.** All unknown — nothing
   is claimed on the site.
8. **Logo / brand assets.** No logo file was available; the wordmark is typeset from the
   business name. The brass colour palette is a design proposal, not the studio's brand.
9. **Reviews.** The listing's rating and review text are real but were left off the concept so
   the demo doesn't imply a testimonial relationship. Add only with permission.
10. **Photography permission.** Every photo is licensed stock imagery, clearly labelled as a
    placeholder. The studio's own photos need written approval before use, and the placeholder
    notice should then be removed.

### Not functional (by design)

- **Booking** — no booking system is built; the button links out to Booksy.
- **Contact form / email** — intentionally omitted; phone and Instagram are the listed routes.
- **Live availability or "open now" state** — hours are static text.
- **CMS** — updates are made in `src/content/site.ts` (a CMS can be added later).
- **Analytics, cookie banner, booking confirmation emails** — not included.
- **Turn-by-turn navigation** — the map shows the shop, your approximate position and the
distance; routing itself happens in Google Maps or Apple Maps.
- **Server-side geocoding** — the marker sits at the geocoded street address, not at a
studio-verified pin. Confirm the exact storefront location with the business.

---

## Photo credits

All images are used under the [Pexels license](https://www.pexels.com/license/) (free for
commercial use, no attribution required). They are placeholders and are **not** the studio's
work. Per-file mapping is in [`public/images/CREDITS.md`](public/images/CREDITS.md).

Background photos of a shop interior are generic; none of them depict Invictus Hair Studio.

---

## Deployment

Published on **Freebuff Sites (production)** on 27 Oct 2026.

- **Production URL:** https://site-3f9f15137096462ca4c14031e584f63b.freebuff.page
- **Site ID:** `17518f42-3e5f-4383-bc41-245dd3d9b7cf` (name: “Invictus Hair Studio — Website Concept”)
- **Worker:** [`worker/index.js`](worker/index.js) — serves the static build through `env.ASSETS`
- **Deploy manifest:** [`sites.manifest.json`](sites.manifest.json) — `dist/` as assets, `spa: true`
- **Bindings:** none (no D1, R2, auth or secrets for this static site)

Build and ship a change:

```bash
npm run build
# local Workers-runtime check (same asset + SPA behaviour as production)
npx wrangler dev --config wrangler.test.jsonc --port 8788
# then deploy the existing build with the Sites deployer using sites.manifest.json
```

## Public URL and consent

This concept is currently published at the production URL above, so it can be reviewed on any
device. It has **not** been approved by, and is not affiliated with, Invictus Hair Studio, and it
is not linked from the business's own channels. Get the owner's sign-off before presenting it as
their site — and take it offline with the Sites unpublish control if they decline.
