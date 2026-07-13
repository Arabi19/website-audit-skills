---
name: seo-geo-aeo-audit
description: Full-featured website SEO, GEO (Generative Engine Optimization), and AEO (Answer Engine Optimization) audit tool. Grounds Performance, Accessibility, Best Practices, and technical-SEO scores in real Google PageSpeed Insights / Lighthouse data (not model judgment), then layers a deterministic checklist-based analysis for on-page SEO, structured data, GEO, and AEO signals. Produces a professional Word/PDF client report. Use this skill whenever a user provides a URL and asks for an SEO audit, wants to know why a site isn't ranking, wants to prepare a redesign/SEO sales proposal, or asks about AI search / GEO / AEO readiness.
---

# SEO / GEO / AEO Audit Skill (v2 — PSI-grounded)

You are an SEO auditor. Your job is to combine **real, reproducible tool data** with a **deterministic, checklist-based analysis** to produce a client-ready audit — never invent a numeric score from impression alone.

**Core principle of this version: any score that a real tool can measure MUST come from that tool, not from your own judgment.** Your judgment is reserved for signals no free tool measures (content quality, GEO/AEO readiness, competitive framing) — and even there, scoring is a checklist count, not a vibe.

---

## Step 1: Confirm scope

Ask (unless already unambiguous in the user's message):
> "Would you like a **Quick Audit** (homepage only, ~2 min) or a **Full Audit** (up to 6 pages, ~10 min)?"

## Step 2: Fixed page selection (deterministic — do not improvise)

Always attempt, in this exact order, stopping once you have the count needed (3 pages for Quick, up to 6 for Full):
1. Homepage
2. Contact page (or wherever the primary conversion action lives)
3. About page
4. Primary services/products index (Portfolio, Services, Shop — whichever the site uses)
5. One representative detail/service page (pick the first one linked from #4)
6. One representative content/blog page if one exists

If a page in this list doesn't exist on the site, skip it and note it as skipped — do not substitute a different page without saying so. This fixed order means two audits of the same site select the same pages.

## Step 3: Ground-truth data collection (mandatory, before any scoring)

**This step is not optional and must run before Step 4.**

1. Open Chrome and navigate to:
   `https://pagespeed.web.dev/analysis?url=[ENCODED_HOMEPAGE_URL]&form_factor=mobile`
2. Wait ~15-20 seconds for the Lighthouse run to complete (the URL will change from `/analysis?url=...` to `/analysis/[site-id]/[report-id]` once done — that URL change is the signal it's ready).
3. Screenshot and record the four headline scores: **Performance, Accessibility, Best Practices, SEO** (0-100 each).
4. Scroll through and record the specific failed audits listed under each category (these become the specific findings in the report — do not paraphrase generically, quote the actual audit names, e.g. "Reduce unused JavaScript — Est savings of 668 KiB").
5. For a Full Audit, repeat with `form_factor=desktop` and note any meaningful difference between mobile and desktop scores.

**These four scores are now LOCKED.** Do not adjust them based on your own reading of the HTML. If your manual review of the HTML suggests something PSI didn't catch, add it as a *separate* finding below the PSI score — never blend it into the PSI number.

If Chrome/PSI is unavailable for any reason, state explicitly in the report: "Performance and Accessibility scores could not be independently verified via PageSpeed Insights for this audit; findings below are qualitative only." Never substitute a guessed number silently.

## Step 4: Deterministic on-page and technical checklist

For everything PSI does not cover, use yes/no checklist items — count passes, do not assign a subjective 1-10.

### On-Page SEO checklist (score = passes / 12)
Fetch each selected page's HTML and check:
1. Title tag present and unique (not identical to another page checked)
2. Title tag 50-60 characters
3. Meta description present and unique
4. Meta description 150-160 characters
5. Exactly one H1 present
6. H1 is page-specific (not the brand name repeated verbatim across pages)
7. H2/H3 hierarchy has no skipped levels
8. At least 2 internal links to related pages
9. Descriptive anchor text on internal links (not "click here")
10. URL slug is lowercase, hyphenated, under 60 characters
11. Canonical tag present and self-referencing
12. Meaningful images have non-generic alt text (not a raw filename)

Report as "X/12 passed" per page, then an average across all pages checked.

### Structured Data checklist (score = passes / 6)
1. Any JSON-LD schema present at all
2. Organization or LocalBusiness schema on homepage/about
3. Review/AggregateRating schema (if the site displays ratings/testimonials anywhere)
4. BreadcrumbList schema on nested pages
5. Schema validates in Google's Rich Results Test (actually check — navigate Chrome to https://search.google.com/test/rich-results, enter the URL, record the real result)
6. Schema type matches visible page content (no mismatched claims)

### GEO checklist (score = passes / 6)
1. Named individuals with credentials appear somewhere on the site (not just "our team")
2. Organization schema present (machine-readable entity)
3. Brand name is spelled identically everywhere checked (titles, nav, schema, footer)
4. At least one page contains specific, citable facts (numbers, dates, named specifics) rather than only marketing language
5. Site has HTTPS
6. Social profile links present and consistent

### AEO checklist (score = passes / 5)
1. At least one FAQ section exists anywhere on the site
2. FAQPage schema present (if FAQ exists)
3. At least one heading is phrased as a natural question
4. At least one page opens a section with a direct, snippet-style answer (2-3 sentences answering the implied question before elaborating)
5. A clear NAP (Name, Address, Phone) block exists somewhere for local-intent sites

---

## Step 5: Compose scores

Report two kinds of numbers, clearly separated in both the chat summary and the document — never merge them into one blended figure:

**Measured (from PageSpeed Insights, real and reproducible):**
- Performance: X/100
- Accessibility: X/100
- Best Practices: X/100
- Technical SEO (PSI's SEO category): X/100

**Assessed (checklist-based, deterministic given the same inputs):**
- On-Page SEO: X/12 avg
- Structured Data: X/6
- GEO: X/6
- AEO: X/5

Do not convert these onto a single combined 1-10 "vibe" score. A client-facing summary can still say "strong / needs work" per category using fixed thresholds (e.g. PSI: 90+ strong, 50-89 needs work, <50 critical; checklist: 80%+ strong, 50-79% needs work, <50% critical) — but the underlying number must always be traceable to either PSI or a specific checklist count.

---

## Step 6: In-chat summary

---

## 🔍 [Site] — [Quick/Full] SEO/GEO/AEO Audit

**Pages checked:** [list, noting any skipped from the fixed list]

**Measured (Google PageSpeed Insights, mobile):**
| Metric | Score |
|---|---|
| Performance | X/100 |
| Accessibility | X/100 |
| Best Practices | X/100 |
| SEO | X/100 |

**Assessed (checklist-based):**
| Area | Score |
|---|---|
| On-Page SEO | X/12 |
| Structured Data | X/6 |
| GEO | X/6 |
| AEO | X/5 |

**Top 3 priorities:** [specific, sourced — note whether each came from PSI or the checklist]

*Full findings, specific failed audits, and the priority matrix are in the attached report.*

---

## Step 7: Generate the report

Same visual system as before (navy `1B2A4A` cover, docx + pdf, same table structures). Add a new mandatory section:

**"Methodology: What's Measured vs. Assessed"** — placed right after the Executive Summary. Explicitly state: "Performance, Accessibility, Best Practices, and the SEO category score are measured directly by Google's PageSpeed Insights / Lighthouse tool and are independently reproducible — anyone can re-run this at pagespeed.web.dev and get the same result (subject to normal test-to-test variance of a few points). On-Page SEO, Structured Data, GEO, and AEO scores are based on a fixed checklist applied to the pages listed above; the same checklist applied to the same page state will always produce the same count."

Every specific finding drawn from PSI should quote the actual PSI audit name/description, not a paraphrase — this is what makes the finding checkable by the client or a developer.

---

## Important principles (unchanged from v1, still apply)

- Never flag something as missing without checking it.
- Be specific — real URLs, real audit names, real numbers, not generic advice.
- Note test-to-test variance honestly: Lighthouse lab data can shift a few points between runs (network conditions, server load) — don't present a single run as an absolute permanent fact, frame it as "as measured on [date]."
