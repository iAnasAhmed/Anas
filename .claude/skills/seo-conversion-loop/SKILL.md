---
name: seo-conversion-loop
description: Run a conversion-first SEO + AEO (AI answers) loop - pick the ONE page worth this week's effort by joining search data with conversions, audit it in four passes (access/speed, competition, answer engines, conversion path), recommend one sourced change, and track it weekly behind a human approval gate. Use when the user asks for SEO, AEO, GEO, "rank in ChatGPT/AI Overviews/AI Mode", a Search Console review, a page audit, which page to optimize, a weekly SEO report, or setting up an SEO agent/autopilot - even if they never say "conversion". Also use for bootstrapping a new site from zero (offer, conversion event, landing + supporting page).
---

# SEO Conversion Loop

Core rule: **search visibility is only worth something when the page converts.** Rankings, impressions and AI citations are inputs; the named conversion event (signup, booked call, purchase, COD order that is actually delivered) is the output. Never recommend work on a page that cannot convert.

Funnel the whole skill follows:
L1 Visible (Google + AI answers) -> L2 Chosen (the one page) -> L3 Fixed (for Google and AI) -> L4 Converts (value starts here).

## 0. Preconditions - check before anything else

1. Does the target page have ONE clear next step (signup / call / checkout)? If not, stop: fixing that is the job, not SEO.
2. Is the conversion tracked as a **named event** (PostHog, GA4, server-side, Shopify order) and attributable per landing page? If not, fix tracking first - otherwise no SEO change can ever be judged.
3. Does the workspace have `brief.md`, `state.json`, `log.md`? If not, create them from `templates/`. Ask the user for offer, buyer, conversion definition - do not invent them.

If the user has **no site yet**, run section 6 (Zero to first page) instead.

## 1. Workspace (the agent's memory)

| File | Purpose | Rule |
|---|---|---|
| `brief.md` | Business, offer, buyer, what counts as a conversion, markets/language, brand no-go phrases | Read first every run. User edits it most. |
| `state.json` | Baseline metrics per page, daily GSC rows, current test | Pull GSC one day at a time and append; keeps quota safe and gives clean history |
| `log.md` | Append-only record of every run, change, date live, verdict | Never delete or rewrite old entries |
| `reports/YYYY-MM-DD-<slug>.md` | Audit output | Every claim has a source URL |

## 2. Pick the one page worth the week (decision tree)

Pull per page: GSC impressions, clicks, CTR, avg position (last 28 days, excluding the last 3 days - GSC lags 2-3 days). Pull conversions per landing page from the analytics tool. Join them page by page.

Run the four checks **in order**; a page must pass 1-3 to qualify:

1. **Already converts?** Has real conversions from the visitors it gets. No -> not this week's page.
2. **Visible in search?** Has impressions and sits within reach (typically avg position ~5-20 for its main query - "low enough that most searchers never see it"). No -> not this week's page.
3. **Matches intent?** Inspect the live SERP for the main query. If the top results are a different format (e.g. how-to guides vs your pricing page), drop it - no tuning fixes an intent mismatch.
4. **Rival wins on links?** If backlink data (Ahrefs etc.) shows competitors win on referring domains, that is a **different job (backlink gap)**, not a rewrite. Otherwise -> **killer page: rewrite it this week.**

Flag as a **trap**: high impressions + zero conversions. Never recommend it as the bet.

Each candidate gets exactly one call: **keep / keep-if (<one condition>) / drop**, with links to the evidence. Output of this step: one page, one main query, a short written reason.

GSC caveats to state in reports: data lags 2-3 days; page+query breakdown drops anonymized rows (totals won't match); AI Overview appearances can flatter average position.

## 3. Take the page apart - four passes

**Pass 1 - Access and speed.** Crawlable (robots, status 200, indexable text), URL Inspection / Page Indexing status, rendered vs raw HTML if JS-heavy, PageSpeed Insights mobile first - report only failures big enough to hurt real visitors. Eligibility for AI features requires crawlable + indexed + snippet-eligible.

**Pass 2 - Competition.** Fetch the top 10 for the main query, read each page in full (scrape, don't guess), compare to ours. Return: topics/questions winners cover that we skip, and what we say better than all of them. Every claim cites its URL; missing data is stated as missing, never filled.

**Pass 3 - Answer engines (AEO).** Stay grounded: Google states no special optimization is needed for AI Overviews/AI Mode beyond SEO basics and does not use llms.txt. Treat schema as a rich-result tool, not an AI-citation shortcut. Changes that make sense:
- answer the question in the first line under each heading
- headings phrased the way people ask
- each section readable on its own
- consistent business details (NAP, pricing, claims) everywhere online
Also search third-party mentions (Reddit, YouTube, forums, publications): list wrong details and threads where the brand is missing. Check current AI citations where tooling allows (AI Mode SERP data, Bing Webmaster Tools AI performance).

**Pass 4 - Conversion path** (the pass everything hangs on). Read as a buyer: one obvious next step? above the fold / early enough? are pre-purchase doubts answered (price, delivery, returns, trust)? Is the conversion a named event? Which of our own pages already get traffic and should link to this money page (suggest exact anchor + placement)?

End with one report: ranked fixes, and **ONE change to make first**, with evidence links. Use `templates/report.md`.

## 4. Weekly loop

1. Pull fresh search + conversion numbers into `state.json`.
2. Compare to the baseline from before the last change (know how long ago it went live - check `log.md`).
3. Check nothing on the page broke (status, indexing, CTA, tracking event still firing).
4. Recommend **one** change with evidence and links.
5. **Wait for explicit human approval** before drafting or publishing anything.
6. Append what happened and what changed to `log.md`.

Judgment rules:
- One change at a time per page, or attribution is impossible.
- Ignore moves shorter than ~2 weeks; rankings wiggle and self-correct.
- Don't touch a page that is doing well without a strong reason.
- Verdict uses search AND business together: climbed but zero extra conversions = **miss**; flat rankings but better conversion = **win**.
- AI-citation trends can move from model updates - never attribute them to one change with confidence.
- Freeze these instructions and the brief during a test; changing the prompt mid-test makes weeks incomparable.

## 5. Guardrails (non-negotiable)

- Read-only by default. Anything that publishes, edits a live page, changes titles/meta/schema, or submits URLs requires explicit user "yes" in this session. Drafts only (e.g. Webflow/WordPress draft), user does the final read and publishes.
- Unattended scheduled/cloud runs: read + report only, never publish credentials.
- Never invent metrics, API fields, endpoints or competitor claims. Verify tool/API versions before calling. Use sandbox modes (e.g. DataForSEO sandbox) before spending budget; respect rate limits and pagination.
- Brand voice: agent finds problems; the human owns what the brand would never say.
- Keep secrets out of `brief.md`, `state.json`, `log.md` and any committed file.

## 6. Zero to first page (no site)

1. **Offer** - what you sell, to whom (user decides).
2. **Conversion** - the one action, decided with the offer; write both into `brief.md`.
3. Pick one problem + one **ready-to-act** search topic (buyer intent, not curiosity).
4. Simplest site (Webflow / WordPress / framework the user already runs - ask).
5. **Landing page** - offer + one clear conversion near the top.
6. **Supporting page** - answers a close pre-purchase question, links to the landing page ("where to go next").
7. Plug in GSC + analytics, then start the weekly loop. Reader path: question -> supporting page -> landing page -> conversion.

## 7. First four weeks

- **Week 1 - Connect + baseline:** GSC, keyword/SERP data, crawler, web search, conversion tracking (+ backlinks if already paid). Set spend limits and approval rules first. Write brief, confirm named event, backfill history into `state.json`.
- **Week 2 - Pick + audit:** decision tree -> four-pass report. User challenges any unsourced claim; agree ONE change.
- **Week 3 - Ship:** draft, user reviews and publishes, log date + exact change.
- **Week 4 - Loop:** schedule weekly run; give the change several weeks before calling win/miss. Then next change on same page or next money page.

## Tooling map (use whatever is connected; ask, don't assume)

| Need | Typical sources |
|---|---|
| Search performance | Google Search Console (OAuth), Bing Webmaster Tools |
| Keywords, live SERP, AI Mode results | DataForSEO (sandbox first) |
| Backlinks | Ahrefs (optional, only if already paid) |
| Web / brand-mention search | Parallel or any web search tool |
| Page reading / crawling | Firecrawl or equivalent (handles JS + sitemaps) |
| Speed | PageSpeed Insights API |
| Conversions | PostHog, GA4, server-side events, Shopify orders |
| Drafting changes | Webflow MCP, WordPress, repo PR |

For COD / e-commerce: the conversion to judge is the **delivered** order (net of RTO/returns) where data allows, not the placed order. For Arabic/RTL sites, research queries in the language and dialect buyers actually type and compare against local SERPs.
