# Origin Oolong LLC: trade website

Static site for a Hong Kong based buyer and exporter of single-origin Zhangping shuixian oolong. No framework, no build step, one stylesheet.

Live: https://logansolaman.github.io/origin-oolong/

## Pages

| File | Purpose |
|---|---|
| `index.html` | Trade landing page, price ladder, FAQ, request form |
| `wholesale.html` | Leaf programme: volume tiers, landed cost, terms |
| `private-label.html` | Private label from 500 units, label compliance |
| `oolong.html` | The range, six axis grading sheet, defect vocabulary |
| `quality.html` | Document register, what we do and do not claim |
| `about.html` | Farm, region, master, entity |
| `contact.html` | Request form and direct channels |
| `privacy.html` | Privacy notice |

## Local preview

```bash
python3 -m http.server 8899
# open http://localhost:8899
```

## Editing

This repository is the published copy. The source of truth is `origin-oolong/site/` in the private `logansolaman/hermes` repo, with the design and content rationale in `origin-oolong/website-design-and-content.md`.

Sync after editing the source:

```bash
rsync -a --exclude '_*' ~/Documents/GitHub/hermes/origin-oolong/site/ ~/Documents/GitHub/origin-oolong-site/
cd ~/Documents/GitHub/origin-oolong-site && git add -A && git commit -m "update site" && git push
```

Pushing to `main` triggers the Pages workflow in `.github/workflows/pages.yml`.

## Before this goes live on the real domain

1. **Prices, lot code and availability figures are placeholders.** Confirm against the farm and update the price validity date each quarter.
2. **Canonical tags, `sitemap.xml` and `robots.txt` all point at `https://originoolong.com`.** While the site is served from `github.io`, that canonical tells search engines the real home is the domain, so this copy will not accumulate ranking of its own. That is intentional.
3. **The contact form has no backend.** It composes a pre-filled email in the buyer's mail client. Wire a form endpoint before launch.
4. **`trade@originoolong.com` must exist** before launch. Every call to action points at it.

## Moving to originoolong.com

When you own the domain:

```bash
# 1. add the custom domain in the repo settings, or drop a CNAME file at the repo root
echo "originoolong.com" > CNAME

# 2. at your DNS provider, point the apex at GitHub Pages
#    A    @    185.199.108.153
#    A    @    185.199.109.153
#    A    @    185.199.110.153
#    A    @    185.199.111.153
#    CNAME www  logansolaman.github.io

# 3. enable HTTPS once the certificate is issued (Settings, Pages, Enforce HTTPS)
```

No path changes are needed: the site uses relative links throughout, so it works at a subpath now and at a domain root later.

## Design

Aligned to the Origin Oolong | Grand Cru identity sheet.

- *Stark Parchment* `#F3F0E8` page, *Oxidation Black* `#0B0B0B` ink and hero ground, *Alluvial Gray* `#C8CAC9` hairlines, *Clay Terracotta* `#B86B4A` for marks, rules and display accents.
- Small terracotta text uses `#7A4025` (`--accent-text`) because `#B86B4A` is only 3.5:1 on parchment; the brand tone survives, the contrast budget does not. Every text token measures 7:1 or better.
- Type: Bodoni Moda (display serif, standing in for Rugiet, which is a commercial licence) + IBM Plex Mono (labels, lot codes, figures) + the system Helvetica Neue stack for body copy. Two webfonts, `font-display: swap`, Latin subset.
- Structure per the sheet: circular OO medallion lockup, square corners only (`--r: 0`), hairline rules instead of shadows, dark hero band with a contour-line field and a copper seal, then the parchment certificate system.
- Copy is the existing site copy. The Grand Cru sheet's placeholder numbers (FIT-098, 1850 m, Puru China) are not used anywhere; every batch figure on the site is one of the site's own lot codes.
