# Parallax Newsletter Playbook

A single self-contained brief for drafting the weekly **Parallax by Chicago Global** investor newsletter. Drop this whole file into any AI chat with the instruction *"build the newsletter following this playbook exactly"* and you should get the same output you'd get here. No prior context required.

---

## 0. What this newsletter is

A weekly HTML email. The automated run sends **Monday 10:00 (local)** via the `weekly-newsletter-send` scheduled task. The current scope is **four segments** (institutional, advisory, platform, prospects) — see CLAUDE.md and the vault `Newsletter Instructions.md` for the full 4-segment spec — all from the **same underlying data**. (The two-segment table below is the original core; the institutional + prospects rows still apply.)

| Segment | File name | Subject line | Audience | Width | Font |
|---|---|---|---|---|---|
| Institutional | `newsletter_institutional.html` | **The Brief** | Self-directed investors, $100K–$5M books, sophisticated, MSCI ACWI benchmarkers | 680 px | Helvetica Neue / Arial (no webfont) |
| Prospects | `newsletter_prospects.html` | **Parallax News** | BD funnel, partner outreach, less-technical readers | 600 px | Inter via Google Fonts |

Producer: **Chicago Global** (Singapore), regulated by **MAS CMS101590**. Engine behind the newsletter: **Parallax**, a Large Investment Model covering 62,400+ securities across 48 markets.

---

## 1. Voice

**Thriller cadence, telemetry-grounded, observational only.**

- Short sentences. Concrete numbers from Parallax telemetry. Second person occasionally ("your book", "your ETFs").
- Each "Portfolio impact" callout: 3–5 sentences, leads with a punchy framing line, cites 2–3 specific telemetry numbers (basket name + daily/MTD/YTD %, breadth %, divergence flag), ends with a practical implication.
- **Observations, not advice.** Never "buy / sell / rotate into". Always "telemetry shows / the tape closed / breadth at X".
- Bold key numbers via `<strong>`. Italicise basket names via `<em>`. Minus signs via `&minus;` (not `-`).
- No emojis, no gradients, no drop shadows, no stock photography.
- Educational where possible: explain *why* a signal matters in one phrase.
- Reference common DIY instruments (VOO, SPY, VT, EEM, VWO) where natural.

**Punctuation signature**: em-dashes (—) and middle dots (·). See em-dash budget below.

---

## 2. Brand colour palette

Locked. Never substitute.

| Use | Hex | Notes |
|---|---|---|
| Navy (primary) | `#0F2A4A` | Headlines, primary buttons, brand text |
| Dark navy (ticker) | `#0A1F3A` | Ticker bar only |
| Body grey | `#3A3F47` | Body copy |
| Muted grey | `#6B7280` | Eyebrows, fineprint, captions |
| Panel light grey | `#F2F4F6` | Card backgrounds, holding panels |
| Divider grey | `#D9DDE2` | Horizontal rules |
| Page background | `#ECEEF1` | The grey behind the white card |
| Success green | `#3F8E5C` | Positive returns, brand stacked-bars logo |
| Alert red | `#C24A4A` | Negative returns |
| Amber accent | `#E5B23C` | Regime tag (MIXED / SELECTIVE ROTATION), divergence flag count, REGIME label in ticker |
| Alert blue (panel bg) | `#E3F0FF` | Rotation Trigger panel background only |
| Alert blue (accent) | `#4A90D9` | Rotation Trigger left border + arrow |
| Alert blue (text) | `#1E5C9F` | Rotation Trigger header text |

**Light blue (`#6FAFEE`) rule**: there used to be a dark-mode swap for outlined buttons to light blue. **It is removed.** Outlined buttons stay navy on white in every mode. Do not reintroduce the swap — it caused readable navy-on-white to break to light-blue-on-white in light mode on dark-mode devices.

---

## 3. Typography

**Institutional (`The Brief`)**: `'Helvetica Neue', Helvetica, Arial, sans-serif`. No webfont link. Outlook safe.

**Prospects (`Parallax News`)**: `'Inter', Helvetica, Arial, sans-serif` via Google Fonts `<link>`. Falls back to Helvetica on Outlook.

**One webfont exception (institutional only)**: the words *"The Brief"* in the hero use Instrument Serif italic at 30 px, loaded from Google Fonts, with Georgia / Times fallback. This is the only italic serif in the whole document.

| Element | Size | Weight | Family |
|---|---|---|---|
| Hero "The Brief" label (institutional) | 30 px italic | 400 | Instrument Serif |
| H1 hero catchy title | 34 px (mobile 26 px) | 700 | sans |
| H2 section title | 24 px (mobile 20 px) | 700 | sans |
| H3 news headline | 16 px | 700 | sans |
| Body paragraph | 14 px | 400 | sans |
| Portfolio impact callout | 13.5 px | 400 | sans |
| Eyebrow / section label | 11 px | 600 | sans, 2px letter-spacing, uppercase |
| Stat value | 22 px | 700 | sans |
| Stat label | 10 px | 600 | sans, 1.5px letter-spacing, uppercase |
| Footer fineprint | 11.5 px italic | 400 | sans |
| Compliance line | 10.5 px | 600 | sans, 3px letter-spacing, uppercase |

---

## 4. Layout — institutional (4 cards)

Container 680 px, white background, sits on `#ECEEF1` page bg with 24 px padding all sides. Top-down structure:

1. **Ticker bar** (dark navy `#0A1F3A`). A single `<img>` tag referencing the animated GIF at `https://assets.chicago.global/parallax/ticker.gif` — 680 × 36 px, ~160 KB, 60 frames at 60 ms, regenerated every Thursday by `scripts/generate_ticker_gif.py` from `scripts/metrics.json`. The `alt` attribute carries the full metrics line as a text fallback for clients that block images. The GIF is the only motion in the email — CSS animation is blocked by Gmail / Outlook / Apple Mail, so this is the only way to get a moving ticker in inbox.

2. **Brand bar** (white). Left: `DD MMM YYYY · Platform Issue`. Center: green stacked-bars mark + word "Parallax". Right: `Vol. YYYY / WK`. Left and right cells get `class="hide-mob"` so on phones only the centered logo shows.

3. **Hero** (white). Centered. *The Brief* in 30 px Instrument Serif italic above a 34 px H1 catchy question + a small subtitle paragraph.

4. **Editorial split** (no gap between left and right panels). Left 55% = **Telemetry Snapshot** on a navy `#0F2A4A` panel with a 6-cell metrics grid (Regime / US breadth / Top YTD basket / Bottom YTD / HK breadth / Divergence flags). Right 45% = **In this memo** TOC on a light-grey `#F2F4F6` panel listing the four cards with each title wrapped in an anchor link (`#this-week`, `#portfolio`, `#checks`, `#platform`).

5. **Card 01 — Markets This Week**. Anchor: `id="this-week"`. Eyebrow with circled "01" badge. H2: *"The headlines that moved the tape."* Then three news items, each:
   - H3 headline (16 px)
   - 1–2 sentence lede paragraph (14 px)
   - "Portfolio impact" callout in a 3-px left navy bar (`<table>` with a 3 px navy `<td>` then 14 px padded body)
   
   No source line under the H3 (sources stay in the LLM's audit trail, not the email body). One bulletproof navy button below the three items: **Run Impact Assessment** → `https://parallax.chicago.global/assessment`.

6. **Card 02 — Portfolio of the Week**. Anchor: `id="portfolio"`. Top-to-bottom inside this card:
   - Eyebrow with circled "02" badge: *"Portfolio of the Week · Parallax Builder"*
   - H2 (rotation narrative title, e.g. *"Entered AI compute Monday, rotated to defensives Wednesday."*)
   - Period italic stamp: *"Generated by Parallax · benchmark: MSCI ACWI · period: 12 May to 18 May 2026 · one rebalance on 14 May"*
   - **Stat strip**, 4 equal-width cells on a light-grey panel: **Return** (green if positive, red if negative) · **Benchmark** (the ACWI return, same color rule — NOT the alpha) · **Sharpe** (navy) · **Info Ratio** (navy)
   - **Rotation narrative**, two plain prose paragraphs (no panel background) — see template in section 6.
   - **Phase 1 panel** (grey `#F2F4F6`, 18px padding, 2 px navy bottom-border under "Phase 1 · Entry · DD MMM" header) with two holdings rows (each row: name list, weight %, theme label) summing to 100%.
   - **Rotation Trigger panel** (light blue `#E3F0FF`, 4 px `#4A90D9` left border, 14 px padding) with a large amber-blue ↓ arrow, header `Rotation Trigger · DD MMM YYYY` in `#1E5C9F`, body in navy describing the flagged divergence.
   - **Phase 2 panel** (same grey, 2 px navy bottom-border on header — same color as Phase 1 for visual consistency) with two holdings rows.
   - **Three buttons** in one row: **Portfolio of the Week ↓** (filled navy, primary, links to the .xlsx URL with a `download` attribute) · **Open in Analyzer** (outlined, links to `/analyzer/create-portfolio`) · **Stress-Test Your Book** (outlined, links to `/assessment`).
   - Helper line below buttons in muted grey: *"Download the .xlsx and upload it under Analyzer → New analysis to replicate the exact basket."*
   - Single line *"Powered by Parallax Builder"* in muted grey, uppercase, letter-spaced.
   - Disclaimer line in muted grey italic: *"Beta to ACWI: X · Tracking error: X% · Max DD: −X% · Sharpe X · Info Ratio X. Generated from the Parallax six-factor framework, rebalanced once on DD MMM after the fatigue divergence flagged. Not investment advice. Past performance not indicative of future results."*

7. **Card 03 — Three Checks for Your Book**. Anchor: `id="checks"`. Eyebrow circled "03". H2: *"Three diagnostics worth running this week."* Three numbered diagnostic rows (01/02/03) each with a bold title + 13.5 px body + a muted-grey Console reference. Buttons row: **Run These Checks on Parallax** (filled, → `/analyzer/manage-portfolios`) · **Read the Methodology** (outlined, → `https://docs.chicago.global/`).

8. **Card 04 — Parallax Updates**. Anchor: `id="platform"`. Eyebrow circled "04". H2: *"New on the platform."* Three light-grey 32%-wide stack panels (height 220 px), each with a label, a short pitch paragraph, and a button anchored bottom-left: **Try it on Parallax** (filled navy, → `/login`), **API Setup Guide** (outlined, → `docs.chicago.global/api-reference/introduction`), **Talk to the Team** (outlined, → calendly URL). Closing line: *"Console · AI Portfolio Builder · REST · MCP: same engine, four surfaces."*

9. **Footer** (white card bottom). Centered green stacked-bars mark + "Parallax" + "BY CHICAGO GLOBAL" + contact line + `Parallax · Chicago Global · MAS CMS101590` + the italic compliance fineprint *"Shared for discussion with prospective partners. This material is not investment advice and does not claim regulatory approval. It is not a substitute for institutional suitability, supervision, or compliance review."*

---

## 5. Layout — prospects (3 cards)

Container 600 px. Simpler structure aimed at BD outreach.

1. **Card 1 — Markets This Week** (no separate ticker / brand bar / hero / snapshot — those are institutional-only). Eyebrow: `MARKETS THIS WEEK · DD MMM YYYY`. H1: *"The Headlines That Moved the Tape"*. Three news items, same format as institutional's Card 01 but slightly shorter copy (1–2 sentence lede, 4–5 sentence Portfolio impact). One navy button at the bottom: **Run Impact Assessment**.

2. **Card 2 — Portfolio of the Week**. Eyebrow: `PORTFOLIO OF THE WEEK · PARALLAX BY CHICAGO GLOBAL`. H1: a 1-line portfolio name (e.g. *"Capital Markets, REITs & Defense"*). Italic period stamp. **3-cell stat strip** on a `#F2F4F6` background: **RETURN** (green) · **BENCHMARK** (the benchmark's OWN return, e.g. ACWI +0.80%, NOT excess — corrected 2026-06-03, see §16c) · **HOLDINGS** (`14`, navy). 4-row holdings table — name list, weight, sector label. One button **Open in Analyzer**. *"POWERED BY PARALLAX BUILDER"* uppercase line. Disclaimer line.

3. **Card 3 — The Parallax Engine** (platform pitch). Eyebrow. H1: *"The Parallax Engine"*. Two paragraphs pitching the LIM + portfolio-first design + three delivery modes (Console / REST / MCP). One button **Schedule a Demo** → calendly URL.

4. **Footer**. Same green stacked-bars mark + "Parallax" + "BY CHICAGO GLOBAL" + contact line (info@chicago.global, docs.chicago.global only — no telemetry.chicago.global in this simpler version) + MAS line + shorter compliance line.

**Stat strip — all segments (corrected 2026-06-03):** the strip is `Return / Benchmark / Holdings`, where the **Benchmark** cell shows the benchmark's OWN window return (e.g. ACWI +0.80%), never "vs benchmark"/excess/alpha. Institutional/platform may additionally carry Sharpe / Info Ratio cells, but the Benchmark cell is always the benchmark's own return. Excess belongs in prose only. (This supersedes the older "prospects show alpha" framing.)

---

## 5b. Layout — country-tailored prospects (Jakarta / Saigon / etc.)

Country variants follow the **prospects 3-card layout exactly** with three differences:

1. **Subject and eyebrow rebrand.** Each country gets its own series name:

| Country | Subject + Eyebrow | Title H1 stamp |
|---|---|---|
| Indonesia | `Jakarta Signal · DD MMM YYYY` | same |
| Vietnam | `Saigon Signal · DD MMM YYYY` | same |
| Thailand | `Bangkok Signal · DD MMM YYYY` | same |
| Malaysia | `KL Signal · DD MMM YYYY` | same |
| Singapore | `Marina Signal · DD MMM YYYY` | same |
| United Kingdom | `London Signal · DD MMM YYYY` | same |

   The eyebrow on Card 1 and Card 2 uses the city-signal stamp instead of `MARKETS THIS WEEK` / `PORTFOLIO OF THE WEEK`. Footer line and brand mark stay identical. UK / London variants carry **no ticker** (country-variant rule).

   **London Signal (UK)** was first built 2026-06-02 as `parallax_newsletter_london.html`: London Signal branding, three UK stories (FTSE/gilts, Bank of England, oil with UK read-through), and the Parallax Engine pitch. The UK sits **inside** Parallax coverage (GB baskets), so its Portfolio of the Week should be a UK-domiciled basket once telemetry is pulled; the first build reused the real global flagship book (+6.11% vs ACWI) as an engine demo because the data key was down at build time.

2. **Stat-box convention changes from the standard `Return / Benchmark / Holdings` (benchmark's own return) to a country-scoped 3-cell version.** The labels change based on whether the country is **inside Parallax's equity universe** (covered: ID, MY, TH, SG, PH, HK, CN, KR, TW, IN, JP, AU, IL, ZA, EU markets, US) or **outside** (most notably **Vietnam** — VN is not in `get_telemetry.markets` today).

   - **Covered country, normal week** (basket beats ACWI):
     `BASKET WTD` (green) · `ACWI WTD` (red if ACWI fell) · `MARKET WTD` (e.g. `JCI WTD`, colour by sign)
   - **Covered country, dispersion week** (country sells off but Parallax flagged a positive sub-basket): see Section 7b.
   - **Uncovered country (Vietnam, smaller frontier markets)**:
     `ASEAN FACTOR WTD` (green, cite the *nearest covered-market basket*, e.g. ID Small-Cap Domestic Cyclicals) · `ACWI WTD` · `HOLDINGS`. Footer disclaimer must say explicitly: *"Indicative HOSE-listed proxy for the ASEAN domestic small-cap factor. Vietnam equities sit outside Parallax's direct equity coverage today; the +X.XX% WTD figure shown is the Parallax `<basket name>` basket, used here as the nearest ASEAN proxy."*

3. **Holdings table swaps to country-domiciled names** with locally relevant sector labels (`IDX Banks`, `VN Banks`, `Domestic Property`, `FDI Beneficiaries`, etc.). The 3-column header table (`TOP HOLDINGS / WEIGHT / SECTOR`) stays the same.

**News selection for country variants**: at least 2 of 3 news items must be country- or region-specific. The third may be a global macro print (Fed, oil, US PPI) but its "Portfolio impact" callout must tie back to local FX / rates / equities. Brent → Petrolimex (VN) or Adaro (ID), Fed cuts → SBV or BI policy stance, etc.

---

## 5c. Layout — advisory (The Advisory Brief, WSJ-style)

A long-form editorial newsletter for **independent RIAs and wealth managers** (US- and Singapore-based, fee-only or fee-based, fiduciary). Voice is **peer-to-peer practitioner with Wall Street Journal cadence**: serif editorial headlines, named bylines, source attributions, deep prose. Container **680 px** (matches institutional).

**Subject and eyebrow**: `The Advisory Brief · DD MMM YYYY · Parallax by Chicago Global`.

**Typography exception**: Instrument Serif (italic + regular) is used across all section H2s and the "The Advisory Brief" hero label. This is the segment's signature — extends the existing institutional serif exception. Inter sans for everything else.

**Top-to-bottom structure** (no ticker bar — it sits institutional-only):

### Brand bar
Single row, white background, navy `#0F2A4A` 1 px bottom border. Three cells:
- Left (33%): date `2026-05-19`, 11 px Inter 600 muted grey, 2 px letter-spacing.
- Center (34%): `THE ADVISORY BRIEF` 11 px Inter 600 muted grey, 2.5 px letter-spacing, uppercase.
- Right (33%): stacked-bars green mark + `PARALLAX` 14 px Inter 700 navy.

### Hero
Centered card, 48 px padding. Three lines:
1. `The Advisory Brief` — 34 px Instrument Serif italic navy.
2. **H1 catchy headline** — 34 px Inter 700 navy, e.g. *"Energy reclaims the lead. Mega-cap tech finally cracks."*
3. Lede subtitle — 15 px sans, body grey, max-width 540 px.

### Editorial split — photo + TOC (heights matched at 380 px)
Two-column table inside the white card. Both cells **height 380 px**, `vertical-align: top`.

- **Left cell**: B&W editorial photo, 305 × 380 px, `style="filter:grayscale(100%); object-fit:cover;"`. Replace the `i.ibb.co/REPLACE-ME/...` placeholder URL each week with the hosted image.
- **Right cell**: light-grey `#F2F4F6` background, 28 px padding, contains the numbered TOC (eyebrow `IN THIS MEMO`, then 5 rows of `## title + subtitle`).

The two cell heights must match — set `height="380"` on both `<td>` tags. On mobile (≤480 px) the split collapses to single column and photo height becomes auto.

### Slim CTA strip
Light grey `#F2F4F6` background, 18 px padding. Left: *"Run your book against this week's factor regime"*. Right: navy uppercase button **RUN ASSESSMENT →** linking to `https://parallax.chicago.global/assessment`.

### Five numbered sections
Each section has the same skeleton:
- Eyebrow: `0X` (Inter 600 muted grey 2.5 px letter-spacing) + section title in UPPERCASE.
- H2: 36 px Instrument Serif regular weight navy, single sentence ending with a period.
- Byline: 12.5 px sans muted grey: *"Ben Charoenwong · Cofounder · DD MMM YYYY"* (or *"Chicago Global Team · DD MMM YYYY"* for §05). The byline title is always **Cofounder**, never "Chief Investment Officer".
- Body: 14.5 px Inter sans, line-height 1.65.

Section thin-divider: 1 px `#D9DDE2` top border between sections.

**§01 — This Week** (3 news items, deep development):
Each item:
- H3 (18 px Inter 700 navy) — punchy claim, not a question.
- Source line (italic 11.5 px muted grey) — *"Reuters energy desk · Bloomberg commodities · Parallax telemetry"*. Always cite at least one external source plus Parallax.
- **One tight body paragraph** — merge the "what happened" (hard numbers: basket %, breadth, WTD) and the "client read-through" into a single dense paragraph. Do not use two separate paragraphs. Aim for ~80–100 words per item max. *(Feedback 2026-06-15: advisory was too long, trim aggressively.)*

**§02 — Client Questions** (3 questions clients will ask):
Each item:
- Italic-serif question (20 px Instrument Serif italic navy): *"Should I be worried about US tech concentration?"*
- Plain-prose answer (2–3 sentences max): the honest framing and the portfolio implication. Keep it punchy — the evidence line carries the supporting data.
- Source line: *"Evidence to cite: <Parallax data point or external source>"*.

**§03 — Portfolio of the Week** (real Parallax-built book that beats the benchmark):
This is a **simple single-basket portfolio (like prospects), NOT the rotation**: no Phase 1 / Phase 2 panels and no Rotation Trigger. The rotation block is reserved for institutional and platform only. Advisor-shippable:
- H2 names the theme (e.g. *"Energy, Defensive Sectors & Real Yield."*).
- Period stamp: italic muted-grey *"Parallax Builder · benchmark MSCI ACWI · window DD to DD Mon YYYY · 14 US-listed holdings"* (no "one rebalance" line, since there is no rotation). Add a credibility line: *"Built to be advisor-shippable: every name is US-listed, daily-liquid, and clearable in standard custodian platforms."*
- **3-cell stat strip** (like prospects) on `#F2F4F6` panel: `RETURN` (green) · `BENCHMARK` (the benchmark's OWN return over the window, e.g. ACWI +0.80%, NOT excess — corrected 2026-06-03) · `HOLDINGS` (navy). Excess may appear in the disclosure prose only.
- **Holdings table** — 6 rows, grouped by theme (e.g. *Energy*, *Staples & Utilities*, *Real Estate*, *Capital Markets*, *Defensive Blue-Chips*, *Real Yield*). Three columns: name list · weight · theme label.
- Button: **Open in Analyzer**. Bottom italic disclosure cites real performance metrics (beta, alpha annualized, tracking error, max drawdown, downside capture) and ends with "Not investment advice. Past performance not indicative of future results."

**Universe constraints for the §03 portfolio**: every name must resolve cleanly in Parallax. Prefer US-listed ETFs (XLE, XLP, XLU, VNQ, VTIP, SHY) and large-cap single names (AMT, CME, ICE, KO, WMT, KMB, CL, PG). **Avoid tickers prone to mis-resolution** — `IAU` resolves to *I-80 Gold Corp* (Canadian microcap), `GLD` resolves to *Gold Finder Resources*. Use `IAU.P` explicit suffix or skip gold ETFs entirely. Iterate up to 3 times via `analyze_portfolio` until the book beats ACWI.

**§04 — What Other Advisors Aren't Saying Yet** (3 contrarian conversation hooks):
The "pitch ideas" section, renamed for stronger contrarian framing. **Section H2 must use a fiduciary, client-conversation tone, NOT cold-prospecting language** — e.g. *"Three Contrarian Reads Worth Raising With Clients."*, never *"…for Cold Outreach"* (the advisory audience is fee-only/fiduciary RIAs talking to existing clients, not running cold sales). Each item:
- H3 (17 px Inter 700 navy) — provocative client-facing line in quotes: *"Your portfolio is one stock away from your retirement plan failing."*
- One body paragraph (2–3 sentences) — the underlying argument grounded in Parallax data, and why most advisors won't say it. Keep it punchy.

**§05 — Parallax Updates** (platform notes):
Three bulleted-prose paragraphs (no actual bullet markers — leading `·` middle dot + `<strong>` bold lead-in):
- Advisor-tier launch, coverage update, methodology refresh.
Closing button: **Schedule a 30-min walkthrough** → calendly URL.

### Footer
2 px navy `#0F2A4A` top border, 32 px top padding, centered. Same green stacked-bars + Parallax logo + `BY CHICAGO GLOBAL · THE ADVISORY BRIEF` line + contact line + MAS CMS101590 line + italic compliance: *"Not investment advice. For RIA / wealth-manager educational use; review against your firm's policies before client communications. Past performance not indicative of future results."*

### What's gone vs the v1 spec
- The animated factor ticker at the top is removed (advisory does not carry a marquee).
- Container width moved from 640 → 680 px.
- Card 2's "Client Talking Points" became §02 *"Client Questions"* (preserved) AND §03 became a real portfolio (new).
- §04 renamed from "Pitch Ideas" → "What Other Advisors Aren't Saying Yet".

---

## 6. Content templates

### Rotation narrative (institutional Card 02)

Two plain prose paragraphs, navy `#0F2A4A` headings inline:

> On `<D Mon>` the portfolio entered **AI compute and mega-cap tech**, the trade that worked year-to-date. Two days later, Parallax flagged a fatigue divergence in `<flagged basket name>` after the cluster rolled over. The book rebalanced into **Specialized REITs** (which rebounded +4.7% daily), **Capital Markets** (+10.5% MTD), **Defense**, and **Discount Retail** (+4.5% daily).

> Held statically through `<end date>`, the entry basket would have returned just **+X.XX%**. Rotated, the portfolio returned **+X.XX%** versus ACWI **±X.XX%**, a **+X.XXpp** excess. (return = green; benchmark = red; alpha = green; all bold via `<strong style="color:...;">`.)

### Rotation Trigger panel body

> `Rotation Trigger · <Wednesday DD MMM YYYY>` (header in `#1E5C9F`, uppercase, letter-spaced)
> `Parallax flagged a fatigue divergence in <em>[flagged basket]</em>. The book rebalanced out of [Phase 1 short theme] and into [Phase 2 short theme].` (body in navy, 13.5 px)

### Portfolio impact paragraphs

Three news items, three "Portfolio impact" callouts. Each:
- Leads with a punchy framing line (*"Higher-for-longer just got harder to argue against."* / *"The trade that compounded is now rotating."* / *"Oil at $111 is the linkage between PPI and the rate path."*).
- Cites at least 2 specific Parallax telemetry numbers: basket name + daily / MTD / YTD %, breadth %, divergence flag.
- Ends with a practical implication: *"Stress your book against a no-cuts-in-2026 path before the June FOMC."*

---

## 7. Portfolio of the Week — rotation logic

**Which segments carry the rotation:** the two-phase rotation block (Phase 1 → Rotation Trigger → Phase 2) appears ONLY in **institutional** (Section 02, where it replaces the old Factor Snapshot) and **platform** (Card 02). **Advisory** and **prospects** show a SIMPLE single-basket portfolio instead: one holdings table with a Return / vs Benchmark / Holdings stat strip, no phases and no trigger (see §5 and §5c). The rotation analysis below is computed once and feeds all four; advisory/prospects just present the final basket without the phase framing.

The portfolio must beat **two bars** every week:
1. Outperform MSCI ACWI over the analysis window.
2. Outperform a *no-rotation hold* of Phase 1 — the rotation has to actually add value, otherwise the story is empty.

### Construction

- **Window**: previous Monday → yesterday (YYYY-MM-DD). One 7-calendar-day rolling window.
- **Rebalance day**: Wednesday of the analysis week (Monday + 2 days). Canonical "Parallax flagged it Wednesday" beat.
- **Benchmark**: `ACWI.OQ` (MSCI ACWI).
- **Per-phase weight**: equal-weight `1/14` so each phase sums to exactly 100%.

### Phase 1 — entry basket (Monday)

14 names representing the trade that worked year-to-date (default theme: AI compute + semis + mega-cap tech, but rotate the theme each week to match telemetry context). Mix concentrated momentum (7 names) with broader carryover (7 names).

### Phase 2 — rebalance basket (Wednesday)

14 names from the **rebound divergence cluster** flagged by Parallax telemetry. Standard mappings:
- Specialized REITs (AMT, EQIX, DLR, CCI) when REITs flagged as rebound
- Capital Markets (CME, ICE, MSCI, NDAQ) when Capital Markets has positive MTD
- Defense (LMT, NOC, RTX) on geopolitical/oil signal
- Discount Retail + Staples (COST, WMT, KO) when Discount Retail rebounded

### Verification protocol

1. Call `analyze_portfolio` with **both** date blocks → captures rotation return.
2. Call `analyze_portfolio` again with **only the Phase 1 date block** → captures static-hold counterfactual.
3. If rotation_return ≤ benchmark_return OR rotation_return ≤ static_return, narrow the rebound basket and retry up to **3 times**. Keep the best run regardless, flag underperformance loudly in the report.

---

## 7b. Dispersion-week fallback (Option B — institutional truth-telling)

**When to invoke**: a country basket loses money after **3 honest iterations** through `analyze_portfolio`, because the underlying market genuinely sold off that week (e.g. ID aggregate −2.13% WTD, only 2 of 31 baskets positive — verified case from 19 May 2026 Indonesia issue). Do **not** curve-fit a fake-winner by cherry-picking the few stocks that held up — that's marketing, not methodology.

**Decision rule**: if no honest 14-name proxy outperforms ACWI over the window, pivot the framing from *"our basket beat the market"* to *"here is the dispersion the market hid from the index"*.

**Narrative pivot** (Card 1 H1 changes shape):
- ❌ Old: *"Three Moves That Set Indonesia's Week"*
- ✅ New: *"Indonesia Retraces −X.X%. Parallax Flags Where Capital Rotated."*

**Three news items become three lenses on the dispersion**:
1. **The aggregate sold off** — cite the market-aggregate WTD and the n-of-N positive-basket count (e.g. "only 2 of 31 baskets positive").
2. **The losers** — name the bottom basket (e.g. Indonesian Commodity Miners −4.92% WTD) and explain the macro driver.
3. **The single bid** — name the divergence flag from `get_telemetry.divergences` (fatigue / rebound type, basket name, MTD %) and the only positive basket of the week with its WTD %.

**Stat box becomes 3-cell country-scoped**:
`BASKET WTD` (green, the **real** Parallax sub-basket WTD return from `get_telemetry.markets.<XX>.top_wtd.value`) · `ACWI WTD` (red, the real `analyze_portfolio` benchmark return over the same window) · `MARKET WTD` (red, the country aggregate from `get_telemetry.markets.<XX>.aggregate_wtd`).

**Holdings table**: 14 representative IDX/local-exchange constituents of the **winning Parallax basket theme**, sourced from `build_stock_universe(query=<theme description>)`. Footer disclaimer must explicitly say *"Names shown are representative constituents of the basket theme; weights illustrative."* — you cite the Parallax basket's WTD return, not the literal holdings' return, because you don't know the exact constituents.

**Spread to ACWI**: cite as `basket_wtd − acwi_wtd` rounded to the nearest 0.01pp. Use language *"Parallax's basket led ACWI by +X.XXpp on the week"* — not *"our portfolio returned X%"*. The basket is the unit of attribution, not a hypothetical 14-name backtest.

This pivot is **stronger** than fake-winning: it shows the methodology working (telemetry caught the dispersion the index couldn't), is regulatorily honest, and reuses the same Parallax narrative that powers institutional Card 02 rotation logic. Use it any time a country basket honestly underperforms.

---

## 8. The Portfolio of the Week .xlsx upload file

Readers click *Portfolio of the Week ↓* in the email and get the basket as a **.csv** (served from raw.githubusercontent — the only host that returns 200 on a click; see §20), then upload it to Parallax Analyzer at `/analyzer/create-portfolio`. (The Analyzer accepts CSV and xlsx; we serve CSV because every GitHub host 503/403s .xlsx.)

**Strict file-format contract** (do not break):

- **One sheet only.** No Reference / metadata / total sheets. The Analyzer reads sheet 1; extra sheets or a row labeled "Total" cause `Symbol not found in our database` errors.
- **Three columns**: `Date`, `Symbol`, `Weight`.
- 28 rows total (header + 14 Phase 1 + 14 Phase 2). No total row.
- **Date**: YYYY-MM-DD. One date per phase (Monday for Phase 1, Wednesday for Phase 2).
- **Symbol**: plain US tickers or Refinitiv RICs (`AAPL.O`, `MSFT.O`, `NVDA.O`). Parallax resolves both.
- **Weight**: decimal 0–1. Use `1/14 = 0.07142857...` so each phase sums to exactly 1.0. Avoid rounded `0.0714` (those sum to 99.96% and trip the normalization warning).

The generator (`build_pow_xlsx.py` or the weekly rebuild) produces the .xlsx (ROTATION = 28 rows / two phase-dates; SIMPLE = 14 rows / one date), then `xlsx_to_csv.py` writes the matching **.csv**. Filename patterns: `Parallax_Portfolio_of_the_Week_<YYYY-MM-DD>.{xlsx,csv}` (rotation, institutional + platform) and `Parallax_Portfolio_Simple_<YYYY-MM-DD>.{xlsx,csv}` (simple, advisory + prospects). Both are pushed (via `weekly-publish.py`) before send. **The download button links the CSV on raw.githubusercontent** (`https://raw.githubusercontent.com/emmajoulin1009-hash/newsletter-assets/main/…csv`), NOT the github.io Pages URL (Pages 503s .csv) and NOT jsDelivr (503 on a click). The old `assets.chicago.global/parallax/portfolio-of-the-week.xlsx` URL is DEAD. See §20 for the full host matrix + the navigation-vs-fetch lesson.

---

## 9. Email-safe HTML rules

- **DOCTYPE**: XHTML 1.0 Transitional. (Yes, it's archaic. It's what survives Outlook.)
- **Layout**: nested `<table role="presentation" cellpadding="0" cellspacing="0" border="0">`. No CSS grid or flexbox. No `position:absolute`.
- **Colors**: every coloured element gets both a `bgcolor=""` attribute AND an inline `style="background-color:#..."`. Outlook reads the attribute; everyone else reads the inline.
- **MSO reset**: `<style>` block contains `table, td { mso-table-lspace:0pt; mso-table-rspace:0pt; border-collapse:collapse; }` and `body, table, td, p, a, h1, h2, h3 { -webkit-text-size-adjust:100%; -ms-text-size-adjust:100%; }`.
- **Viewport**: `<meta name="viewport" content="width=device-width, initial-scale=1.0">`.
- **No Apple Mail text-resize**: `<meta name="x-apple-disable-message-reformatting">`.
- **Force light scheme on email body**: `<meta name="color-scheme" content="light only">` and `<meta name="supported-color-schemes" content="light only">`.
- **Bulletproof buttons**: wrap each `<a>` in a `<td bgcolor="#0F2A4A">` so Gmail doesn't strip the background. For outlined buttons, the wrapping `<td>` carries the border, and the inner `<a>` carries the matching `color:` inline.
- **No JavaScript. No CSS animation. No `<form>`s.**

---

## 10. Mobile responsive rules

A single `@media screen and (max-width: 600px)` block in the `<style>`:

- `.container { width:100% !important; max-width:100% !important; }`
- `.stack { display:block !important; width:100% !important; }` — used on side-by-side cells that should stack on phone
- `.stack-gap { display:block !important; height:12px !important; ...; background-color:#FFFFFF !important; }` — 12 px spacer between stacked rows
- `.hide-mob { display:none !important; max-height:0 !important; overflow:hidden !important; mso-hide:all !important; }` — used on brand-bar left ("19 May 2026 · Institutional Issue") and right ("Vol. 2026 / 20") cells so only the centered logo shows on phone
- `.px-lg { padding-left:20px !important; padding-right:20px !important; }` — replaces 48–64px desktop padding
- `.h1-mob { font-size:26px !important; }` — hero H1 shrinks from 34 to 26
- `.h2-mob { font-size:20px !important; }` — section H2 shrinks from 24 to 20
- Stat box, ticker, holdings row classes all shrink proportionally

---

## 11. Dark mode rules

**Lock everything light.** No color swaps to light blue or anything else. The principle: keep the email rendering identical in light mode and dark mode by preserving the background colors so the foreground text stays readable.

In the `<style>` block:

```css
[data-ogsc] .navy-bg, [data-ogsb] .navy-bg { background-color:#0F2A4A !important; }
[data-ogsc] .ticker-bg, [data-ogsb] .ticker-bg { background-color:#0A1F3A !important; }
[data-ogsc] .panel-bg, [data-ogsb] .panel-bg { background-color:#F2F4F6 !important; }
[data-ogsc] .white-bg, [data-ogsb] .white-bg { background-color:#FFFFFF !important; }
[data-ogsc] .navy-text, [data-ogsb] .navy-text { color:#0F2A4A !important; }
[data-ogsc] .white-text, [data-ogsb] .white-text { color:#FFFFFF !important; }
[data-ogsc] .alert-bg, [data-ogsb] .alert-bg { background-color:#E3F0FF !important; }
@media (prefers-color-scheme: dark) {
  .ticker-bg { background-color:#0A1F3A !important; }
  .navy-bg { background-color:#0F2A4A !important; }
  .panel-bg { background-color:#F2F4F6 !important; }
  .white-bg { background-color:#FFFFFF !important; }
  .alert-bg { background-color:#E3F0FF !important; }
}
u + .body .ticker-bg, .gmail-dark .ticker-bg, .darkmode .ticker-bg { background-color:#0A1F3A !important; }
u + .body .navy-bg, .gmail-dark .navy-bg, .darkmode .navy-bg { background-color:#0F2A4A !important; }
u + .body .panel-bg, .gmail-dark .panel-bg, .darkmode .panel-bg { background-color:#F2F4F6 !important; }
u + .body .white-bg, .gmail-dark .white-bg, .darkmode .white-bg { background-color:#FFFFFF !important; }
u + .body .alert-bg, .gmail-dark .alert-bg, .darkmode .alert-bg { background-color:#E3F0FF !important; }
```

The `<body>` carries `class="body"` so the Gmail-mobile `u + .body` selectors can attach.

**Known limitation**: Gmail iOS sometimes overrides these locks and applies its own hue-shift. There is no further CSS fix — that's documented across email-dev resources. Accept that Gmail iOS may render the dark navy ticker bg as slightly mauve.

**Do NOT add a dark-mode color swap for the outlined buttons.** A previous version swapped navy → light blue `#6FAFEE` in dark mode. It triggered in light mode on dark-mode devices and produced light blue text on white bg = unreadable. Removed. Buttons stay navy on white in every mode.

---

## 12. Em-dash budget — HARD LIMIT

**Maximum 2 em-dashes (`—` or `&mdash;`) in EVERY newsletter — institutional, advisory, platform, AND prospects.** This applies to every segment, with no exception for the WSJ-style advisory voice. Use commas, semicolons, or colons in prose; use the brand middle dot "·" for section dividers (e.g. "02 · Portfolio of the Week", not "02 — Portfolio of the Week"). Reserve en-dashes for numeric ranges only (e.g. 16–17). Use `&minus;` for minus signs.

Aim for **zero** em-dashes; two is the hard ceiling, not a target. If you introduce a new one, drop another. After every refresh, audit ALL four files:

```bash
for f in complete_institutional parallax_newsletter_advisory parallax_newsletter_platform parallax_prospects_newsletter; do
  echo "$f: $(grep -o -e '—' -e '&mdash;' $f.html | wc -l)"   # each must be ≤ 2
done
```

---

## 13. News sources — strict allowlist

Pull from these only. If a story isn't covered by at least one, don't use it.

- Bloomberg (bloomberg.com)
- Reuters (reuters.com)
- Wall Street Journal (wsj.com)
- Financial Times (ft.com)
- The Economist (economist.com)
- Barron's (barrons.com)
- CNBC (cnbc.com)
- MarketWatch (marketwatch.com)
- Morningstar (morningstar.com)

Pick three stories that are (a) macro-relevant to a sophisticated DIY investor with a global equity portfolio, (b) covered by ≥ 2 of these sources, (c) different angles (one US tape, one single-name/sector, one geopolitical or macro). Sources do **not** appear in the email body — they live in the audit trail only.

**Forbidden sources**: anonymous blogs, social-media-only, Seeking Alpha, partisan outlets, crypto-press, anything where authorship is unclear.

---

## 14. Compliance & disclosures (non-negotiable)

Every send carries:

1. **MAS line** in eyebrow caps in the footer: `Parallax · Chicago Global · MAS CMS101590`. Appears in the Telemetry Snapshot footer (institutional) AND the bottom footer (both versions).
2. **Italic fineprint** at the bottom: *"Shared for discussion with prospective partners. This material is not investment advice and does not claim regulatory approval. It is not a substitute for institutional suitability, supervision, or compliance review."*
3. **Card 02 disclaimer** italic muted-grey: *"... Not investment advice. Past performance not indicative of future results."*
4. **Voice rule**: observations only, never outcome promises. Frame metrics as "telemetry shows", "the tape closed", "breadth at X". Never "buy", "sell", "rotate into", or any prediction of future return.

What MAS CMS101590 means:
- **MAS** = Monetary Authority of Singapore (central bank & financial regulator)
- **CMS** = Capital Markets Services license (Singapore licensing regime for fund management, dealing in capital markets products, financial advisory)
- **101590** = Chicago Global's specific license number on the MAS register

---

## 15. CTA URLs (do not change without explicit approval)

| Button | URL |
|---|---|
| Run Impact Assessment | `https://parallax.chicago.global/assessment` |
| Open in Analyzer | `https://parallax.chicago.global/analyzer/create-portfolio` |
| Stress-Test Your Book | `https://parallax.chicago.global/assessment` |
| Run These Checks on Parallax | `https://parallax.chicago.global/analyzer/manage-portfolios` |
| Read the Methodology | `https://docs.chicago.global/methodology/overview` |
| Try it on Parallax | `https://parallax.chicago.global/login` |
| API Setup Guide | `https://docs.chicago.global/api-reference/introduction` |
| Talk to the Team | `https://calendly.com/arnav-chicago/30min?month=YYYY-MM` |
| Schedule a Demo (prospects) | same calendly URL |
| Portfolio of the Week ↓ | **raw.githubusercontent CSV** (the ONLY host that returns 200 on a click; Pages 503s .csv, jsDelivr 503s .csv on navigation): `https://raw.githubusercontent.com/emmajoulin1009-hash/newsletter-assets/main/Parallax_Portfolio_of_the_Week_<YYYY-MM-DD>.csv` (rotation) · `…/Parallax_Portfolio_Simple_<YYYY-MM-DD>.csv` (simple). Set anchor `download="…<date>.csv"`. Analyzer accepts CSV. github.io Pages, jsDelivr, and `assets.chicago.global` are DEAD/unreliable for downloads. See §20. |
| Footer mailto | `mailto:info@chicago.global` |
| Footer docs link | `https://docs.chicago.global` |
| Footer telemetry link (institutional only) | `https://telemetry.chicago.global` |

---

## 16. GetResponse send specs

| Key | Value |
|---|---|
| **Live campaign ID ("weekly newsletter" list)** | **`LtYQV`** — the weekly distribution list; this is where the automated Monday send goes. Manage members in the GetResponse UI. |
| Test campaign ID ("emma" list) | `LtYf4` (review-only test list) |
| From-field ID (verified sender) | `BIlWF` → `info@chicago.global` (Chicago Global). NOTE: `emma@chicago.global` / the old `Q8mex` is NOT a registered sender; use `BIlWF`. Old test list `uKibb` is deprecated. |
| MCP tool for **live** send | `send_newsletter(subject, html_content, plain_content, from_field_id="BIlWF", campaign_id="LtYQV", confirm=true)` — the connector works for real sends. A too-large "exceeds maximum tokens" tool response means the send SUCCEEDED; never retry. Delegate each send to its own sub-agent so the ~50 KB HTML stays out of context. |
| MCP tool for test send | `send_test_newsletter(subject, html_content, plain_content, from_field_id, test_campaign_id="LtYf4")` |
| NOT exposed by the connector | Adding contacts; deleting/canceling a scheduled newsletter. Do these in the GetResponse UI / browser (Newsletters → row ⋮ → **Stop sending** → confirm → delete from Drafts). |
| Subject prefix on test sends | `[TEST]` (auto-prepended by GetResponse) |

**Subject convention by segment** (exact strings — no truncation, no `[TEST]` prefix in your call; GetResponse adds it):

| Segment | Subject |
|---|---|
| Institutional | `The Brief · DD MMM YYYY · Parallax by Chicago Global` |
| Platform | `Parallax · DD MMM YYYY · Parallax by Chicago Global` |
| Prospects (global) | `Parallax News · DD MMM YYYY · Parallax by Chicago Global` |
| Advisory (RIAs) | `The Advisory Brief · DD MMM YYYY · Parallax by Chicago Global` |
| Indonesia | `Jakarta Signal · DD MMM YYYY · Parallax by Chicago Global` |
| Vietnam | `Saigon Signal · DD MMM YYYY · Parallax by Chicago Global` |
| Country variants | `<City> Signal · DD MMM YYYY · Parallax by Chicago Global` |

Plain-text fallback is required for deliverability — generate a stripped-tags version from the HTML and include it in the `plain_content` arg.

**Sharing for review (test-send workflow)**: the GetResponse MCP test endpoint sends to **whoever is currently subscribed to the "emma" test list `LtYf4`**, not to an ad-hoc address. To loop a reviewer in:
1. `get_recent_contacts(campaign_id="LtYf4")` → confirm reviewer is on the list.
2. If absent, add via the GetResponse web UI (Contacts → Add → assign to campaign `LtYf4`); the API does not currently expose contact-add through the MCP.
3. Run two `send_test_newsletter` calls (one per country file). Both names on the list receive both emails within ~2 minutes.
4. The reviewer can reply directly with feedback; no further sharing infra needed.

Confirmed test-list members at last refresh: `emmajoulin1009@gmail.com`, `stevean@chicago.global`. Emma's `u.nus.edu` address is **not** on the test list — add it explicitly if Cowork-default emails matter.

---

## 16b. Ticker GIF smoothness physics

The marquee ticker is rendered as an animated GIF because CSS animation is blocked in Gmail and Outlook. The scrolling-text illusion only works when **per-frame pixel displacement is small relative to the framerate**. The eye fuses motion above ~16 FPS but perceives discrete stepping when each frame jumps too far.

**Canonical spec** (`scripts/generate_ticker_gif.py` defaults):

| Parameter | Value | Why |
|---|---|---|
| `--frames` | 600 (renders ~620 with auto-loop padding) | More frames = smaller per-frame jump |
| `--frame-ms` | 50 | 20 FPS — broadly honored by email clients |
| `--width` | 680 | Matches email container |
| Strip width | ~3,500 px (auto from metrics) | 13 metrics × ~270 px each + padding |
| Per-frame jump | strip_w / frames ≈ **5.6 px** | Below the ~10 px perceptual stepping threshold |
| Loop duration | ~31 sec | Leisurely reading pace |
| Output size | ~1.5 MB | Acceptable for hosted GIF |
| Palette | BG `#0F2A4A` brand navy, value-colour map (white / green / red / amber) | Matches Card 01 telemetry snapshot |
| Item spacing | `BETWEEN_ITEMS=50 px`, leading/trailing pad 40 px | Mat, breathy, Bloomberg-crawl feel |

**Failure modes & fixes**:
- *"Looks like it's moving one little step at a time"* → frames too few (under ~300) or frame-ms too high (over 80). Push to defaults above.
- *"Background looks washed out / not navy enough"* → palette quantization with too few colours. Keep MEDIANCUT with 32 colours.
- *GIF refuses to update in email* → image host (ImgBB free tier) doesn't overwrite; the URL is content-addressed by upload. Re-upload to get a fresh URL, then patch the `<img src>` in `newsletter_institutional.html`.

**Country newsletters do not carry the ticker** (no marquee row in the 3-card prospects/country layout). The ticker GIF lives only in the institutional 4-card layout.

### 16c. Email-rendering + asset rules (added 2026-06-02)

- **Marquee must render INSIDE the 680px container, never as a separate full-width table above it.** Gmail desktop ignores `max-width` on a `<table>`, so a marquee placed outside the container stretches to the full Gmail pane and overflows the email body (Outlook renders it fine, which masks the bug). Keep the marquee `<img>` as the first row inside `.container` (platform/prospects already do this; institutional was fixed 2026-06-02).
- **Hero rotates every week.** Pick a NEW image each issue from `pictures claude/`; never reuse the previous week's hero, even on a repeat topic. Track recent hero filenames to guarantee a different pick.
- **Regenerate + push assets before every send.** Rebuild `marquee.gif` from the JSON and copy the new hero into `newsletter-assets/`, then run `weekly-publish.py` to push them to the GitHub-Pages CDN BEFORE sending. All four files reference hosted URLs (`https://emmajoulin1009-hash.github.io/newsletter-assets/`); an unpushed asset shows last week's ticker/hero in the inbox.
- **Stat strip = Return · Benchmark · Holdings** (3 cells). Show the benchmark's OWN return (ACWI +0.44%), never "vs benchmark"/excess as a cell, in any segment. Excess may stay in the rotation narrative prose, not in the strip.
- **Portfolio numbers are REAL only** (Parallax `analyze_portfolio` + telemetry). Rotation issues (institutional + platform) and simple issues (advisory + prospects) each carry their own real return; never reuse the rotation figure for the simple basket. Every Portfolio of the Week must beat ACWI over the window.
- **Methodology links/buttons → `https://docs.chicago.global/methodology/overview`** everywhere.
- **Working .xlsx per portfolio, Analyzer-pastable** (one sheet: `Date · Symbol · Weight`, weights 1/14). ROTATION shape = two phases/two dates/28 rows (institutional + platform); SIMPLE shape = one basket/one date/14 rows (advisory + prospects). Build with `build_pow_xlsx.py`, host on the CDN, push before send, and point the download button at the hosted file.
- **Platform Card 03 is a dark `#1A2C6B` contrasted band** (light text), mirroring advisory §04.
- **Gmail does not support in-email anchor (`#section`) jumps.** Memo/TOC links work in Apple Mail / Outlook / browser only; Gmail strips the anchors. Keep `id`+`href` correct, but treat Gmail jump-links as a known unfixable limitation.
- **All image refs use the hosted CDN URL** (`https://emmajoulin1009-hash.github.io/newsletter-assets/...`), never relative filenames — relative paths show as broken images for external recipients and in preview panes. Every `<img>` carries `max-width:100%;height:auto;`.
- **Phone-render QA before every send.** Each issue must pass a fresh ~375px mobile check: no horizontal overflow, container collapses to 100%, multi-button rows stack full-width (~44px tap target, uniform style), data tables wrap/shrink to fit, body text ≥13px. Running a fresh no-chat-history reviewer agent per file is the reliable way to catch these.
- **Standing practice:** whenever a rendering bug is fixed, update CLAUDE.md, this Playbook, and the vault `Newsletter Instructions.md` together.

### 16d. Styling + send updates (added 2026-06-03)

- **Stat strip shows the benchmark's OWN return in ALL four segments** (`Return · Benchmark · Holdings`), never "vs benchmark"/excess/alpha as a cell. Excess belongs in prose only. (Reconciles the older §5 / §5b / §5c "alpha/excess" wording.)
- **Institutional §01 "This Week" is a dark section with white story cards:** deep navy `#0B1B3F` background, NO top divider line, each of the 5 stories a white card (white bg, `#6FC3E8` 4px cyan left accent, navy `#0B1B3F` headline, `#3A3F47` body), mirroring the advisory dark-section treatment. The closing CTA box stays `#0B1B3F`.
- **Institutional §03 "Factor Performance" = color-coded factor boxes in Inter:** keep it transposed (factors are the columns), but render five light-grey cards (`#f5f6f8`) with a colored top accent (green `#2e7d32` / red `#c62828`), a big colored Return-WTD value, and Contribution below. Font Inter only (never Trebuchet/Gill Sans/Futura). Context stays as prose below the boxes.
- **Platform Card 03 "Three Checks"** keeps the dark `#1A2C6B` band but uses white inner cards (same pattern as advisory §04) — not thin-divider numbered rows.
- **Live send goes to the "weekly newsletter" list `LtYQV`** (test list `LtYf4` is review-only), from `BIlWF`, via `send_newsletter(confirm=true)`. The connector works for real sends/drafts; it does NOT do contact-add or scheduled-newsletter delete (UI/browser for those).
- **Automation:** the `weekly-newsletter-send` scheduled task runs the full pipeline every **Monday 10:00 (local)** and sends to `LtYQV`. Runs only while the desktop app is open.

---

## 17. Weekly refresh cadence

**Trigger**: automated every **Monday 10:00 (local)** via the `weekly-newsletter-send` scheduled task (was Thursday 09:00 SGT before 2026-06-03). Can also be run manually via `/full-refresh` or cron + `scripts/refresh.py`.

End-to-end sequence:

1. `/refresh-ticker` — pull telemetry, regen the animated GIF (620 frames × 50 ms = ~31 s loop at 

## 18. Hero image — correct approach (never embed base64 in send files)

**Rule**: The 4 newsletter HTML files (`complete_institutional.html`, `parallax_newsletter_advisory.html`, etc.) must always reference the hero via **CDN `src`**:
```
src="https://emmajoulin1009-hash.github.io/newsletter-assets/hero-YYYY-MM-DD.jpg"
```
Email clients (Gmail, Outlook, Apple Mail) fetch images from the URL at open time. Embedding base64 bloats the file, breaks some clients, and is unnecessary.

**For browser preview only**: build `newsletter_preview_2026-MM-DD.html` separately. That file reads the 4 HTML files, replaces the CDN URL with a base64 data URI sourced from `newsletter-assets/hero-YYYY-MM-DD.jpg` (local copy), and wraps all 4 in a tabbed iframe viewer. The send files are never modified.

**Hero source**: `C:\Users\emmaj\Downloads\outputs\newsletter-assets\hero-YYYY-MM-DD.jpg` (published there by `weekly-publish.py`). Use this file for base64 preview embedding — do not try to fetch CDN from the sandbox (blocked 403).

**Hero layout — FULL-WIDTH STACKED (updated 2026-06-15, replaces all prior split-table approaches):**

Hero is always a **full-width single image** in its own row, followed by the TOC/memo in a second full-width row directly below. **NEVER use a 50/50 split-column table** — it renders as a half-width image with a grey gap beside it on mobile and looks broken.

Correct two-row structure (institutional, prospects, advisory — all newsletters with a hero):
```html
<!-- HERO IMAGE · full width -->
<tr>
  <td bgcolor="#0B1B3F" style="background-color:#0B1B3F;padding:0;font-size:0;line-height:0;">
    <img src="https://emmajoulin1009-hash.github.io/newsletter-assets/hero-YYYY-MM-DD.jpg"
         width="680" height="453" alt="" border="0"
         style="display:block;width:100%;max-width:680px;height:auto;border:0;outline:none;text-decoration:none;" />
  </td>
</tr>
<!-- TOC / MEMO · full width below hero -->
<tr>
  <td bgcolor="#F2F4F6" style="background-color:#F2F4F6;padding:24px 32px;">
    <!-- TOC table here -->
  </td>
</tr>
```

**Hero image crop spec**: landscape ~3:2 ratio (680×453 display). Save at 2× retina = **1360×906px**. Starting from a portrait source (e.g. 526×800): compute `crop_h = int(width / (680/453))`, center-crop vertically, then scale to 1360×906. JPEG quality 88, optimize=True.

Key rules:
- `width="680" height="453"` on the `<img>` tag
- `style="display:block;width:100%;max-width:680px;height:auto"` — scales down on mobile, never distorts
- No `object-fit`, no `overflow:hidden`, no split columns, no VML, no CSS background-image
- The `font-size:0;line-height:0` on the `<td>` eliminates the phantom gap below the image in some clients


---

## 18d. Hero + "In This Memo" side-by-side on laptop, stacked on mobile (LOCKED 29 Jun 2026)

**Approved layout, apply to every issue with a hero (institutional, advisory, prospects).** The hero image and the numbered "In This Memo" TOC sit **side-by-side as a 58/42 two-column row on laptop**, and **stack (hero on top, memo below) on phones**. Verified working across all three (hero/memo cell heights match to 0px; marquee full letter-width).

**Structure (one `<tr>` holding a 2-col inner table):**
```html
<tr><td bgcolor="#0E1A30" style="background-color:#0E1A30;padding:0;">
  <table role="presentation" cellpadding="0" cellspacing="0" border="0" width="100%"><tr>
    <td class="stack-mob hero-cell" width="58%" valign="top" align="center"
        background="<HERO_URL>" bgcolor="#0E1A30"
        style="background-color:#0E1A30;background-image:url('<HERO_URL>');background-position:center;background-size:cover;background-repeat:no-repeat;padding:0;font-size:0;line-height:0;">
      <!--[if !mso]><!--><img src="<HERO_URL>" width="100%" alt="…" border="0" class="hero-img-mob"
           style="display:none;width:100%;max-width:100%;height:auto;border:0;outline:none;text-decoration:none;" /><!--<![endif]-->
    </td>
    <td class="stack-mob memo-cell" width="42%" valign="top" bgcolor="#1E3052" style="background-color:#1E3052;padding:22px 24px;">
      <p …>In this memo</p>
      <!-- numbered TOC rows -->
    </td>
  </tr></table>
</td></tr>
```

**Why the hero is a CSS `background-image` (cover), not an `<img>`, on desktop:** sibling table cells share the row height, so the memo's text height drives the row; `background-size:cover` makes the hero fill that exact height with **no empty gap below it**. A plain `<img>` only renders at its own aspect ratio and leaves a navy gap when the memo is taller. The `<img class="hero-img-mob">` is the mobile/Outlook fallback (shown only when stacked).

**Required CSS — the stack rule MUST live in the `@media (max-width:480px)` block, NOT 768px:**
```css
@media screen and (max-width: 480px) {
  .stack-mob   { display:block !important; width:100% !important; box-sizing:border-box !important; }
  .hero-cell   { background-image:none !important; min-height:0 !important; }  /* drop bg, show the <img> */
  .hero-img-mob{ display:block !important; }                                   /* full image, stacked */
}
```
**CRITICAL breakpoint lesson (29 Jun):** the email container is only **680px** wide, so a `max-width:768px` stack rule fires at *every* width and the columns NEVER go side-by-side — the memo always renders below the hero. The side-by-side must be the **default** (no media query) and stacking triggers only at ≤480px (true phones). First attempt failed exactly this way; fixed by moving `.stack-mob{display:block}` from the 768px block to the 480px block.

**Marquee full letter-width (LOCKED same day):** the marquee `<img>` must use **`width="100%"`** (HTML attribute), not `width="680"`. A fixed `width="680"` attribute is honored over CSS by some mobile clients and overflows / mis-sizes on phones. Keep `style="display:block;width:100%;max-width:680px;height:auto;…"`. Applies to institutional + platform + prospects marquees.

**Verification caveat:** the sandbox browser reports a 0px viewport (forces the ≤480 mobile state) and the marquee GIF freezes iframes, so desktop side-by-side can't be screenshotted in-tool — verify by (a) on-disk CSS/structure grep, (b) a forced-`display:table-cell` DOM measurement, and (c) a real send to the solo-review list opened on a laptop.

---

## 18b. CRITICAL — every referenced asset must be PUSHED to the CDN (fixes "images won't load")

**Root cause of the 15 Jun "images won't load" report:** the publish pipeline did not push every asset the HTML references. Two concrete gaps, both now mandatory to close on every run:

1. **`parallax-logo-footer-white.png` was never in the publish allowlist.** Institutional, advisory, and prospects all reference it in the footer, but `weekly-publish.py` `TRACKED_FILES` and `DYNAMIC_PATTERNS` did not include it, and the `--files` line in the scheduled task omitted it. Result: the white footer logo 404s for every recipient. **Fix:** `parallax-logo-footer-white.png` is now a permanently tracked asset. Always push it. (Also push `parallax-logo-footer.png` and `parallax-logo-brand.png` — the full logo set.)

2. **Dated hero + dated xlsx files are not git-tracked in the local mount index** (the real push goes via the `/tmp` mirror). They must be passed explicitly every week or auto-discovered. Never assume "it pushed last week" — each issue has new dated filenames.

**Mandatory pre-send asset audit (do this BEFORE the send, every run).** Extract every `src=` and `href=` CDN URL from all four HTML files, then confirm each one is live on the CDN. If any asset is not confirmed live, push it and re-check before sending:

```bash
cd <outputs>
# 1. list every CDN asset referenced by the four send files
for f in complete_institutional parallax_newsletter_advisory parallax_newsletter_platform parallax_prospects_newsletter; do
  python3 - "$f.html" <<'PYINNER'
import sys,re
h=open(sys.argv[1],"rb").read().split(b"\x00")[0].decode("utf-8","replace")
for m in re.finditer(r'(?:src|href)="(https://emmajoulin1009-hash\.github\.io/newsletter-assets/[^"]+)"',h):
    print(m.group(1).split("/")[-1])
PYINNER
done | sort -u > /tmp/referenced_assets.txt
# 2. confirm each referenced file exists on disk in newsletter-assets/ before publish
while read a; do [ -f "newsletter-assets/$a" ] && echo "OK   $a" || echo "MISSING $a"; done < /tmp/referenced_assets.txt
# 3. publish EVERYTHING referenced (logos + dated hero + dated marquee + both xlsx)
python3 weekly-publish.py --files $(tr '\n' ' ' < /tmp/referenced_assets.txt)
```

Every line in step 2 must read `OK`. Any `MISSING` is a hard stop — generate/copy the asset into `newsletter-assets/` first. GitHub Pages redeploys ~30 s after push; wait, then a referenced URL opened in a browser must return the image (not a 404 page) before you send.

**The marquee filename rule:** the HTML references the *undated* `marquee.gif`. The weekly build overwrites `marquee.gif` in place AND saves a dated `marquee-YYYY-MM-DD.gif` archive copy. Push both. Do not point the HTML at the dated marquee — keep it on `marquee.gif` so the reference is stable.

---

## 18c. Image-blocking graceful degradation (recipient-side default)

Gmail, Outlook desktop, and most corporate clients **block remote images by default** until the recipient clicks "display images" or trusts the sender. A first-time recipient (e.g. a reviewer seeing the email cold) will see placeholders, not images — this is expected client behaviour, not a bug. We cannot force images on, but we MUST make blocked images degrade gracefully:

- **Every `<img>` carries descriptive `alt` text.** No empty `alt=""`. The hero alt describes the issue (e.g. `alt="Parallax — the defensive-quality rotation, week ending 15 Jun 2026"`). The marquee alt already carries the full metrics line; keep it. Logos use `alt="Parallax"`.
- **Every `<img>` carries explicit `width` and `height`** so a blocked image reserves correct layout space and shows a properly-sized labelled placeholder instead of a tiny broken icon.
- When sharing a preview for review, tell the reviewer the email uses hosted images and they may need to click "display images" — this prevents false "images are broken" reports.

---

## 19. Design feedback fixes — Kevin Ku review, 17 Jun 2026 (apply to ALL segments)

These are durable layout rules from a full design review. They override any earlier conflicting guidance. Apply every one on every weekly run.

**19.1 Factor description text on one row each (institutional §03 Factor Performance).**
The five factor descriptions below the color-coded boxes (Momentum / Tactical / Defensive / Quality / Value) must each sit on **its own single row** — one factor label + its one-line description per row, stacked vertically — not run together in a dense wrapped paragraph. Format each as: `<strong>Factor:</strong> one concise sentence.` on its own line/row with comfortable line spacing (line-height ≥ 1.6). Easier to scan; one idea per line.

**19.2 Button labels in Title Case.**
Every button label uses **Title Case** (capitalise principal words): `Book a Demo`, `Open in Analyzer`, `Run Impact Assessment`, `Stress-Test Your Book`, `Read the Methodology`, `Try It on Parallax`, `API Setup Guide`, `Talk to the Team`, `Schedule a Demo`, `Explore Live Telemetry`, `Run Assessment`, `Open Parallax`. Fix sentence-case stragglers — `Book a demo` → `Book a Demo`. Keep any trailing `→`/`↓` arrow. Do not change the destination URLs (§15).

**19.3 Footer "email" word → cleaner mark (NO new icon asset).**
In the footer social row (`in · x · email`) that appears in institutional and advisory, the literal word **"email"** reads awkwardly next to the `in` / `x` marks. Do NOT create a new mail-icon asset (`icon-mail.png` is cancelled). Reuse what already ships: either (a) drop the standalone "email" link entirely and rely on the existing footer contact line `mailto:info@chicago.global` (already present in every footer), or (b) keep a single linked mark in the social row using the existing **Parallax logo / brand mark** instead of the word "email". The `in` and `x` marks stay as they are. The mailto target is `mailto:info@chicago.global` (§15).

**19.4 Adopt the numbered "In This Memo" summary layout for ALL segments.**
The institutional **"In This Memo"** block — a numbered list (`01 / 02 / 03 / 04`) where each row is a small-caps navy title plus a one-line grey summary, on the light-grey `#F2F4F6` panel — is the canonical key-points/summary format. Use this exact pattern for the opening summary/TOC in **every** segment (institutional, advisory, platform, prospects), adapting the row count to each segment's sections. Replace any other intro-summary styling with this numbered-row format.

**19.5 Separate the final dark content cell from the footer.**
When the last content card has a dark background (e.g. platform Card 03 `#1A2C6B`, institutional dark CTA `#0B1B3F`) it blends into the dark footer and the email's end is unclear. **Insert a visual separator between the last dark content cell and the footer:** either a full-width white/`#ECEEF1` spacer row (≥ 24 px) OR a 1 px `#D9DDE2` divider line on a white band, so the reader can see where the newsletter content ends and the footer begins. Never let a dark content cell butt directly against a dark footer.

**19.6 De-clutter the left summary/snapshot panel (reduce visual noise).**
The dark navy Telemetry Snapshot panel (institutional left column / the "IN THIS ISSUE" style block) reads as crowded and noisy. Reduce the noise by **either** dialing back the use of bright colour on the metric values (use white/light-grey for labels and reserve green/red only for the single most important figure), **or** reducing the metric-value font size a step, **or** increasing spacing between the metric cells. Goal: fewer competing bright elements, clearer hierarchy. Keep the data, lower the visual volume.

**19.7 Make links look like links.**
Any inline hyperlink in body/footer prose (e.g. `docs.chicago.global/methodology/overview`, "View in browser", "Unsubscribe", "Update preferences", documentation URLs) must be **visually distinct as a link**: use the brand alert-blue `#1E5C9F` (or `#4A90D9`) **and/or** underline. Do not leave links rendered in the same grey/navy as surrounding body text with no affordance. Buttons are exempt (they already read as actions); this applies to text links.

**Apply-everywhere note:** after wiring these, re-run the full QA (§5/§9/§10 + §18b asset audit + em-dash audit) and a fresh ~375 px mobile check on all four files before sending.

## 19b. Design feedback — Emma review, 18 Jun 2026 (apply to ALL segments every run)

These override any earlier conflicting guidance and apply on top of §19.

**19.8 Email SUBJECT = the week's catchy headline, NOT the segment name.** Do not send with subjects like "The Brief / The Advisory Brief / Parallax / Parallax News". Lead each subject with the catchy title, varied slightly per segment so the four are distinguishable in one inbox. Worked example (15 Jun 2026): institutional `Chips and Gold Lead a Narrow Tape. The Fed Decides Today.`, advisory `Chips Whipsaw, Gold Leads: What to Tell Clients Before the Fed Prints.`, platform `A Narrow Tape: See Your Factor Tilt Before the Dot Plot.`, prospects `Chips Round-Trip, Gold Leads, Oil Slides Into the Fed.` (This supersedes the §16 segment-name subject convention for the visible subject line.)

**19.9 Benchmark stat-strip cell: index name in the LABEL, number-only as the value.** The small grey label reads `BENCHMARK · ACWI`; the big colored value is only the number, e.g. `+2.21%`. Never render `ACWI +2.21%` together as the big green value. (Benchmark's own return, green when positive; never excess/alpha — rule 17.)

**19.10 §03 factor boxes must align — and NEVER overlap the value.** When a factor/basket label wraps it pushes its value down and, if the reserved height is too small, the label text collides with the big number (Emma flagged "RATE-SENS. PROPERTY" overlapping `−3.5%`, 18 Jun 2026). Give each label `<p>` a fixed height tall enough for the WORST-CASE wrap: at `font-size:9px` + `letter-spacing:1.5px` + `text-transform:uppercase` in a ~75px-wide 20% box, "RATE-SENS. PROPERTY" wraps to **3 lines**, so use **`height:40px;line-height:13px`** (3 × 13 = 39px) on ALL five labels — never `height:26px` (that only fits 2 lines and caused the overlap). All five labels share the same height so the values sit on one baseline. Institutional only (only file with the 5-box section).

**19.11 CTA buttons must POP — no hollow/outline boxes.** Kill the `outline-btn` pattern (white or `#F2F4F6` fill + thin navy border) on light panels; it reads as an inert box, not a button. Fill rules: on DARK navy bg, primary = solid cyan `#6FC3E8` + navy text; on WHITE/light panels, solid navy `#0B1B3F` (darkest-navy primary + `#1A2C6B` filled secondaries when 2-3 sit in a row); on the dark `#1A2C6B` band, primary = solid white + navy text, secondary = `#1A2C6B` fill + 1.5px white border + white text. Every button must look clickable.

**19.12 Footer divider = full-width thin cyan line, flush, NO spacer band.** Between the last content cell and the footer put exactly one row: `<tr><td height="2" bgcolor="#6FC3E8" style="height:2px;background-color:#6FC3E8;font-size:0;line-height:0;">&nbsp;</td></tr>`. No `#ECEEF1` gap band, no short centered tick. Applies to all four (institutional/advisory/prospects line → dark `#0B1B3F` footer; platform line → white footer). This supersedes §19.5's "spacer or divider" wording.

**19.13 Advisory §01 news = SHORT.** Each of the three §01 news cards is ~2 sentences / ~40-55 words: key fact + client implication. Drop "for clients, the message is…" / "the read-through:" filler. (Reinforces the §5c trim.)

## 19c. Design feedback — Emma review, 18 Jun 2026 (second batch — apply to ALL segments every run)

These override any earlier conflicting guidance and apply on top of §19 / §19b.

**19.14 Buttons must HUG their label — never full-width banners.** Every CTA button (filled navy `#0B1B3F`, filled cyan `#6FC3E8`, or the dark-band white/`#1A2C6B` variants) must size to its text, NOT stretch the full width of its column/card. A full-width filled bar reads as a banner, not a button (Emma flagged platform Card 03 and the Portfolio-of-the-Week / Open-in-Analyzer buttons, 18 Jun 2026). Implementation rules, on every send file:

- The button `<a>` uses **`display:inline-block; width:auto`** with horizontal padding (`padding:13px 22-26px`), never `display:block` / `width:100%`. A bare inline-block anchor already hugs its text.
- For table-wrapped bulletproof buttons (platform), the wrapper `<table align="left|center">` must carry **`class="btn-auto"`** and the `<style>` must include `.btn-auto, table.btn-auto { width:auto !important; max-width:100% !important; }` — this beats the email's global mobile `table { width:100% !important; }` rule by selector specificity (otherwise that rule stretches the wrapper on phones).
- In the `@media (max-width:600px)` block, button classes (`.btn`, `.btn-stack`, `.btn-stack-last`, `.btn-mob-block`, and the institutional `a[style*="display:inline-block"]` selector) must use **`display:inline-block !important; width:auto !important`**, NOT `display:block; width:100%`. Keep comfortable padding for the tap target (≈13px × 22px); do NOT force a 100%-width 44px bar. This **supersedes** the older §10 / §18b "multi-button rows stack full-width (~44px tap target)" wording — Emma prefers compact buttons that hug their label on mobile too.
- Center or left-align via the wrapping `<td align="center|left">`; the inline-block button then sits compact within it.
- After wiring, grep every file for `display:block` anchors that carry a button background + padding — there must be **zero** banner buttons in any of the four send files.

**Apply-everywhere note:** §19.14 + the corrected §19.10 height are durable. Re-run the full QA (§5/§9/§10 + §18b asset audit + em-dash audit + the banner-button sweep) and a fresh ~375 px mobile check on all four files before sending.

## 19e. Design feedback — Kevin Ku review, 22 Jun 2026 (apply to ALL segments every run)

A second full design review from Kevin Ku (delivered in Slack DM, 22 Jun 2026). These are durable and override earlier conflicting guidance. Kevin reviewed an in-flight version; some items he raised had already been superseded by Emma's same-day rework, but the rules below are the standing policy going forward.

**19.19 Differentiate the "Portfolio impact" callout from body copy (prospects §01 + anywhere the callout appears).** A thin navy left-bar with the text inline reads as ordinary body copy. Give the callout its own **filled light-grey panel**: left accent `<td width="4" bgcolor="#6FC3E8">`, body `<td bgcolor="#F2F4F6" style="background-color:#F2F4F6;padding:12px 16px;">`, and lead with a small uppercase label on its own line: `<strong style="color:#0B1B3F;letter-spacing:0.5px;text-transform:uppercase;font-size:11px;">Portfolio impact</strong><br>` then the sentence. Cyan accent + grey fill makes it a distinct "so what" box.

**19.20 Byline appears ONCE per newsletter, never under every section heading.** Repeating "Ben Charoenwong · Cofounder · date" under each advisory section reads as filler and hurts authenticity. Rule: **do not put a person's name on every section heading.** Advisory §01–§05 carry at most a plain date stamp (e.g. `22 Jun 2026 · window 15–18 Jun 2026`) with NO name. If a single signature is wanted, it lives once (institutional keeps one `Ben Charoenwong, Cofounder · DD Month YYYY` line near the foot of §05; that single instance is fine). Grep each file: a person's name should appear ≤ 1 time.

**19.21 Source citations are clickable links.** The advisory §02 "Evidence to cite: … (Parallax / CNBC)" attributions — and any inline source mention — wrap each source token in an alert-blue underlined `<a>`: `Parallax` → `https://docs.chicago.global`, `CNBC` → `https://www.cnbc.com`, etc. Style `color:#1E5C9F;text-decoration:underline;` (§19.7 link affordance). If a source has no obvious public URL, leave it plain rather than inventing one.

**19.22 CTA button labels are short — drop time qualifiers.** "Schedule a 30-min Walkthrough" → **"Schedule a Walkthrough"**. Remove "30-min"/"30-minute"/duration words from button labels generally; keep them tight and Title Case (§19.2). Destination URLs unchanged (§15).

**19.23 A dark final CTA box must not butt against the dark footer — use a LIGHTER NAVY box and REMOVE the cyan line (supersedes §19.12/§19.5 for the dark-CTA-before-dark-footer case).** When the last content cell is the dark `#0B1B3F` "How Parallax Helps" CTA and the footer is also dark `#0B1B3F`, a thin cyan line between two identical darks is not enough separation (Kevin, 22 Jun; Emma's call: change the box colour, drop the line). **Fix:** set that final CTA cell to the lighter navy **`#1A2C6B`** (muted sub-text → `#C7CEE2`, eyebrow → `#AEB8D4`; keep the cyan or white button), and **delete the full-width `height:2px #6FC3E8` divider row** between it and the footer. The tonal step (lighter-navy box → darker-navy footer) is the separator. Applies to **institutional + advisory** (both have the dark CTA-before-footer). **Platform + prospects keep their cyan line** — their final content cell is white, so white → cyan line → footer already reads as separated; do NOT change those. (So §19.12's flush-cyan-line rule still holds wherever the cell above the line is light; §19.23 overrides it only for a dark-CTA-above-dark-footer.)

**19.24 Multi-button rows need breathing room and balanced widths.** When two or three buttons sit on one row (e.g. institutional Card 02 "Portfolio of the Week ↓" + "Open in Analyzer"), they must not touch. Use ≥ 10 px gutter each side (≥ 20 px between buttons) and equal horizontal padding (`13px 22px`) so the buttons are visually balanced, not one long + one short. Buttons in a card grid (e.g. platform/§04 update cards) are **centered** within their box (`<td align="center">`), not left-aligned.

**19.25 Avoid ambiguous trailing words in data panels.** Kevin flagged "… 18 JUN 2026 CLOSE" in the telemetry-snapshot source line as unclear (reads like a market-close time). Prefer "AS OF 18 JUN 2026" or just the date. (The institutional snapshot panel that carried this was already replaced by the hero + memo layout, so this is a standing copy rule, not a live element.)

**Apply-everywhere note:** §19.19–§19.25 are durable. After wiring, re-run the full QA (em-dash ≤ 2, §18b asset audit, banner-button sweep, name-appears-once grep, 390 px mobile check) on all four files before sending.

---

## 20. Known infrastructure issue — .xlsx download returns HTTP 503 (open, 22 Jun 2026)

The Portfolio-of-the-Week download buttons point at `https://emmajoulin1009-hash.github.io/newsletter-assets/Parallax_Portfolio_*_<date>.xlsx`. As of 22 Jun 2026 **GitHub Pages returns HTTP 503 for every `.xlsx` URL on this site** (and for `.zip`/`.bin`/`.xls` test files), while images (`.jpg`/`.gif`/`.png`), `.md`, and `.html` all serve 200. It is NOT this week's build: last week's `…2026-06-15.xlsx` is 503 too, and the files are correctly committed/pushed (verified via the mirror). Diagnosis: a GitHub Pages serving-layer limitation for binary download content-types on this Pages site — `.nojekyll` is already present, so Jekyll is not the cause; a query-string cache-buster does NOT fix it.

Implication: the email renders fine (all inline images are live), but the click-to-download spreadsheet 503s.

### RESOLVED (22 Jun 2026) — serve the portfolio as **.csv via raw.githubusercontent.com**

Tested every GitHub-fronting host. **`.xlsx` is refused everywhere** (GitHub Pages `503`, raw.githubusercontent `503`, jsDelivr `403`). For **`.csv`**, only **raw.githubusercontent** serves it reliably to a real click:

| Host | `.csv` on NAVIGATION (a click) | `.csv` on `fetch()` |
|---|---|---|
| GitHub Pages (github.io) | **503** | 503 |
| jsDelivr (@main) | **503** (fails) | 200 (misleading) |
| **raw.githubusercontent.com** | **200** (use this) | n/a |

**LESSON (do not repeat):** jsDelivr returns 200 to `fetch()` but **503 to a top-level navigation** — and an email link click IS a navigation, so a `fetch()`-based check gives a false pass. **Always liveness-check the download by NAVIGATION** (Claude_in_Chrome navigate + read_network_requests statusCode), never by fetch. The Parallax **Analyzer accepts CSV** (docs.chicago.global/console/analyzer; schema `Date, Symbol, Weight`).

The fix:
1. **Build a `.csv` next to each portfolio `.xlsx`** every run. Helper: `xlsx_to_csv.py` (converts every `newsletter-assets/Parallax_Portfolio_*.xlsx` -> sibling `.csv`). The `.xlsx` is still pushed as an archive/alt-upload; the **download button links the CSV**.
2. **Link the button at the raw.githubusercontent CSV URL** (200 on navigation):
   `https://raw.githubusercontent.com/emmajoulin1009-hash/newsletter-assets/main/Parallax_Portfolio_of_the_Week_<YYYY-MM-DD>.csv` (rotation) and `.../Parallax_Portfolio_Simple_<YYYY-MM-DD>.csv` (simple). Set anchor `download="...<date>.csv"`. **Do NOT use github.io Pages (503 on .csv) or jsDelivr (503 on navigation) for the download.**
3. **Fully automated:** the weekly `git push` of `newsletter-assets` (via `weekly-publish.py`, whose `DYNAMIC_PATTERNS` now include `Parallax_Portfolio_*.csv` and `*.xlsx`) puts the dated CSV on raw immediately — no API, no manual upload, no GitHub Release, no new account.

**Caveat (acceptable):** raw serves `Content-Type: text/plain`, so the CSV opens **inline** in the recipient's browser tab rather than force-downloading (the cross-origin `download` attribute can't force a save on a different domain). The recipient saves it (Ctrl+S) then uploads to Analyzer. The file is reliably reachable and Analyzer-ingestible. IMAGES (hero/marquee/logos) stay on the github.io Pages CDN — Pages serves images at 200.

**Liveness check every run:** open each CSV download URL by NAVIGATION -> must be `200` (a 404 OR 503 is a hard stop). `assets.chicago.global` is a dead domain — do not use.

Old dead host (do not use): `assets.chicago.global/parallax/portfolio-of-the-week.xlsx` (domain no longer resolves).

## 19d. Approved baseline — Emma review, 22 Jun 2026 (THIS is the reference draft; apply to ALL segments every run)

The **22 Jun 2026 (Vol. 2026 / 28) pack is the approved gold-standard draft.** Every rule below is locked in and overrides any earlier conflicting guidance. Reproduce this exact layout/quality each week.

**19.15 Hero = full-width single image, white cell, `width="100%"` attribute (fixes the Apple Mail "blue square beside the image").** The §18 hero (single full-width `<img>` row + memo/TOC stacked below) is correct, but Apple Mail iOS pins the HTML `width="680"` attribute and paints the cell's dark `#0B1B3F` background in the leftover space → a navy rectangle beside a half-width photo. **Fix, on every hero file (institutional, advisory, prospects):**
- Hero `<td>`: `align="center" bgcolor="#FFFFFF" style="background-color:#FFFFFF;padding:0;font-size:0;line-height:0;">` — WHITE, never `#0B1B3F`. Any client quirk then leaves invisible white, not blue.
- Hero `<img>`: HTML attributes `width="100%" height="auto"` (NOT `width="680" height="453"`), keep `style="display:block;width:100%;max-width:680px;height:auto;margin:0 auto"`.
- Verify in a true 390 px render that image width == cell width (no gap). Platform has no hero (telemetry-snapshot split instead) — leave it.

**19.16 §03 factor boxes use `min-height`, never fixed `height` (final fix, supersedes §19.10's `hei