# highwaterdesigns.com

The public website of High Water Designs LLC, served by GitHub Pages from `main`.
Until the custom domain is connected it lives at https://high-water-designs-llc.github.io/.

Plain static HTML: no build step, no Jekyll (`.nojekyll`), no trackers, no third-party requests.
Fonts are self-hosted, so the site sets no cookies and sends nothing to Google.

## Map

| Path | Page | Source of truth |
|---|---|---|
| `/` | Studio home | this repo |
| `/restockrush/` | Restock Rush game page | this repo |
| `/restockrush/privacy/` | Privacy policy | **RestockRush repo** `Docs/Store/privacy/index.html`, copied here by `Docs/Store/build_site.py`. Until the policy is final (postal address pending) this repo holds a "coming soon" stub. |
| `/app-ads.txt` | Ad sellers file (must stay at the root) | **RestockRush repo** `Docs/Store/app-ads.txt`, copied by `build_site.py` once ad accounts exist |
| `/support/` | Player support and FAQ, data deletion (`#delete-data`) | this repo |
| `/press/` | Press kit | this repo |
| `/404.html` | Not-found page | this repo |
| `/assets/` | `css/site.css`, `fonts/` (Fredoka, Baloo 2, OFL licences beside them), `img/mark.svg` | this repo |

Every page carries the same header and footer; change them on every page.

## Look

Colours, fonts and tone follow the Restock Rush art bible (RestockRush `Docs/Art_Bible.md`, sections 0 and 4):
ink `#3B2F2A` on paper `#FFF8EC`, Corner Shop sage, oak and tomato, UI green for buttons, no pure black or white,
no gradients. Headings Fredoka, body Baloo 2. The studio mark is a tide-gauge staff ("high water").

The illustrations are simple hand-placed vector shapes using the game's colourblind glyphs (star, heart, ring,
diamond). They are stand-ins until real captures exist. Nothing on the site is AI-generated imagery, and real
art must stay that way (art bible handcrafted checklist).

## Slots to fill later

Search the HTML for these comments:

- `STORE BADGE` (`/restockrush/`): swap in the official "Get it on Google Play" badge once the listing is live.
- `TRAILER SLOT` (`/restockrush/`): the WP-20a capture video, in `/restockrush/media/`.
- `SCREENSHOT SLOTS` (`/restockrush/`): 8 portrait shots, same order and captions as the Play listing.
- `MEDIA SLOTS` (`/press/`): trailer, screenshots, key art, logos, icon, in `/press/media/`.
- Postal address: none on the site yet. Add it to the footer when Billy supplies the business address.

## Connecting highwaterdesigns.com

Do **not** add a `CNAME` file by hand before DNS points here: GitHub then redirects the `github.io` address to a
domain that still shows the old site. The steps below do it in the right order.

1. **Verify the domain for the org** (stops anyone else claiming it on GitHub). GitHub org
   `High-Water-Designs-LLC` > Settings > Pages > Add a domain > `highwaterdesigns.com`. GitHub shows a TXT record:
   `_github-pages-challenge-high-water-designs-llc` with a one-time value. Add it at the DNS host and press Verify.
   This changes nothing for the current website or email.
2. **When the old site may go dark**, at the DNS host change only the website records:

   | Type | Host / name | Value | Replaces |
   |---|---|---|---|
   | A | `@` | `185.199.108.153` | the current apex A record(s) |
   | A | `@` | `185.199.109.153` | |
   | A | `@` | `185.199.110.153` | |
   | A | `@` | `185.199.111.153` | |
   | AAAA | `@` | `2606:50c0:8000::153` | any current apex AAAA |
   | AAAA | `@` | `2606:50c0:8001::153` | |
   | AAAA | `@` | `2606:50c0:8002::153` | |
   | AAAA | `@` | `2606:50c0:8003::153` | |
   | CNAME | `www` | `high-water-designs-llc.github.io` | the current `www` record |

   **Leave every MX record, every TXT record (SPF `v=spf1`, DKIM, `_dmarc`, verification codes) and any mail host
   such as `mail`, `autodiscover` or `webmail` exactly as they are.** Email keeps working because it uses only those.
3. Repo Settings > Pages > Custom domain: `highwaterdesigns.com` > Save (GitHub commits the `CNAME` file).
   When the DNS check passes, tick **Enforce HTTPS** (the certificate can take up to an hour).

If the domain's nameservers belong to the old website builder (Squarespace, Wix, GoDaddy Website Builder and similar),
check before step 2 whether email is set up through that builder. Moving the domain's DNS away from it, or deleting
the builder site, can take the mail records with it; copy every MX and TXT record somewhere first.
