# Parallax Newsletter Assets

Public CDN for image assets used by **The Brief** institutional newsletter (Chicago Global / Parallax).

Hosted via GitHub Pages at:

**`https://emmajoulin1009-hash.github.io/newsletter-assets/`**

## What lives here

| File | Purpose | Cadence |
|---|---|---|
| `parallax-logo-brand.png` | 70 × 39 brand-bar logo (header) | One-time, never changes |
| `parallax-logo-footer.png` | 60 × 33 footer logo | One-time, never changes |
| `marquee.gif` | Current week's animated ticker (always the latest) | Overwritten each issue |
| `marquee-YYYY-MM-DD.gif` | Dated archive of each issue's marquee | Append-only |
| `hero-YYYY-MM-DD.jpg` | Current week's hero photo (Institutional / Advisory / Prospect) | New file each issue |

## Weekly publish workflow

```bash
# 1. After regenerating marquee + picking hero, stage the new files
cd ~/Downloads/outputs/newsletter-assets
cp ../marquee.gif .
cp ../marquee-$(date -I).gif .
cp ../hero-$(date -I).jpg .   # picture for this week

# 2. Push to GitHub
git add . && git commit -m "Issue $(date -I)" && git push

# 3. Hosted URLs become live within ~60s. Run swap script:
cd ..
python3 host-images-swap.py
# Produces complete_institutional-production.html, etc.

# 4. Paste production HTML into mcp__getresponse__send_newsletter
```

## Why GitHub Pages

- **Free**, unlimited bandwidth for image hosting
- **Public read** (the URLs we paste into the newsletter need to be world-reachable for recipient email clients)
- **Versioned**: every issue's exact image is preserved in git history
- **Predictable URLs**: no random hash, just `…/newsletter-assets/marquee-2026-05-29.gif`

## Not a code repo

Don't add scripts, drafts, or HTML here — this is asset-only. The newsletter HTML generators live in `Downloads/outputs/` and reference these URLs at send time via `host-images-swap.py`.
hero-2026-06-08.jpg used for Issue 25 (8 June 2026)

## Hero rotation log
- hero-2026-05-29.jpg — Issue 22
- hero-2026-06-02.jpg — Issue 23
- hero-2026-06-03.jpg — Issue 24
- hero-2026-06-08.jpg — Issue 25 (generated: Parallax branded navy/chart)
