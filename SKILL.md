---
name: site-factory
description: Build and launch a complete static website product from idea to deployed GitHub Pages site. Covers naming and collision checks, SEO-ready skeleton, legal red lines (data licensing, disclaimers, ad-network policy), a repeatable deploy pipeline, and post-launch verification. Use when the user wants to create a new website, micro-tool, or content site with no backend.
---

# Site Factory — idea → deployed static product site

A repeatable pipeline for launching small web products: **zero backend, free hosting, honest copy, legally clean**. Distilled from 8+ production launches of tools and content sites (job-tooling, market-data guides, voice utilities, game catalogs).

## When this applies

The user wants a new website, web tool, or content site — especially one intended to run at ~$0 cost (GitHub Pages / Netlify / Cloudflare Pages), store data client-side, and eventually monetize with ads or affiliate links.

## The 7-step pipeline

### 1. Name & collision check
- Shortlist 2–3 names: unique, self-explanatory, easy for AI search engines to cite.
- Check collisions: exact-phrase web search for each name; check domain availability via `https://rdap.org/domain/<name>.com` (404 = likely registrable).
- If a name collides with an existing product, pick another. Renaming later costs SEO.

### 2. Site skeleton
```
<folder>/
  index.html  style.css  [app.js]      # product surface
  about.html  privacy.html             # trust surface (required)
  [terms.html | disclaimer.html]       # required for finance/health/yMY-data topics
  robots.txt  sitemap.xml  .gitignore
  [scripts/update-*.js]  [data/*.json] # optional data pipeline
```
- **Legal pages from day one** (ad networks reject sites without them):
  - `about` — who runs this, how it works, editorial stance
  - `privacy` — no-account/no-tracking statement; if ads are planned, say so; localStorage usage disclosed
  - `disclaimer/terms` — for any finance, health, or legal-adjacent topic
- **SEO baseline**: unique title/description per page, keywords, canonical URL, Open Graph tags; add `FAQPage` or `WebApplication` JSON-LD for content/tool sites; static-render important content into the HTML (crawlers and AI search read HTML, not JS).
- **Privacy by default**: no accounts, no backend, no analytics until there's traffic; user data stays in `localStorage`.
- i18n by subdirectory (`/en/`) with `hreflang` if targeting multiple locales.

### 3. Content red lines (per site type)
- **Data-driven tools**: use official open data / public APIs only. Cite the source, state the update cadence, never imply endorsement. If the official API has no CORS, use the scheduled-cache pattern: a script fetches → writes `data/*.json` → the site loads it same-origin.
- **Reviews / recommendations**: label editorial opinion, disclose no-commercial-relationship (or disclose the relationship), use third-party assets only via official channels (RSS, API, press kits).
- **Finance / health topics**: describe facts, never advise ("education, not advice"); add an explicit non-advice disclaimer; don't time markets.
- **Every site**: no scraping non-official sources, no copying press articles, no unofficial logos/screenshots.

### 4. Deploy (GitHub Pages)
```bash
cd <folder>
git init -b main && git add -A && git commit -m "<name> v1.0"
git remote add origin https://github.com/<account>/<repo>.git
git push -u origin main
# Enable Pages: repo Settings → Pages → Deploy from branch → main / root
#   (or POST /repos/<account>/<repo>/pages with source {"branch":"main","path":"/"} using a token with Pages permission)
```
- Windows note: if `git push` hangs silently, a GUI credential helper is probably waiting. Fix: `git config --local credential.helper ""` then `git config --local --add credential.helper store` (or use a PAT over HTTPS non-interactively).

### 5. Verify
- Wait 50–90s for the Pages build, then `curl -w "%{http_code}"` every URL (home, assets, subpages) — expect 200.
- Non-ASCII display issues in terminals are usually terminal-side; verify actual bytes via `node -e "fetch(url).then(r=>r.text()).then(console.log)"`.
- Assert on rendered DOM snapshots rather than simulated clicks (click automation is flaky; DOM assertions are not).

### 6. Record & iterate
- Keep a registry (one line per site: URL, purpose, data source, monetization, next action).
- Version content with dates on the page ("knowledge as of YYYY-MM") — financial/factual content rots, and dated pages build trust.

### 7. Post-launch handoff
- Submit to Google Search Console (verify via meta tag), submit `sitemap.xml`.
- Share the URL where the target audience actually is.
- Decide on custom domain only after the site survives a week.

## Quality bar
- Professional typography; icon set with a permissive license (e.g., Lucide, ISC) — not emoji-as-icons.
- Honest copy: state limitations plainly ("end-of-day data, not real-time").
- Monetization pre-planned but user value first: free tier forever, ads clearly labeled, affiliate links disclosed.
