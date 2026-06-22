# orient

The rent is a direction. We point at it.

Single-page marketing site for [withorient.com](https://withorient.com).

Brand history: Canary (initial) → Kestrel (briefly) → orient (current, from 22 June 2026). The compass-needle mark is the brand metaphor: the system takes an address and points at the right rent.

## What this is

A static, three-file site that explains what orient does for an institutional leasing team - the asset manager who reviews and signs, and the on-site leasing executives who quote at the front desk. No screenshots, no real operator names, no real assets, no named personas - pure typography and a compass-needle mark.

## Stack

- Plain HTML, CSS, and a small inline script for the dark-mode toggle.
- No build step. No framework. No JavaScript dependencies.
- Fonts loaded from Google Fonts CDN (Inter + Instrument Serif).
- Designed for static hosting on GitHub Pages, Cloudflare Pages, Netlify, or any S3 bucket.

## Files

| File | Purpose |
|---|---|
| `index.html` | Single page. Semantic HTML. Inline dark-mode toggle script. |
| `styles.css` | Design tokens, layout, responsive breakpoints. |
| `favicon.svg` | Compass needle in teal. |
| `DEPLOY.md` | Step-by-step deployment instructions (GitHub Pages path). |

## Brand

- Teal `#01696F` (light) / `#4F98A3` (dark).
- Warm beige background `#f8f7f3` (light) / near-black `#131310` (dark).
- Inter for body, Instrument Serif for display.
- Wordmark is lowercase: `orient`.
- No em-dashes. No en-dashes. Hyphens with spaces only.
