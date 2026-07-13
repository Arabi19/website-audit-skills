---
name: design-accessibility-audit
description: Full-featured website design and accessibility audit tool. Analyzes any URL for visual design quality (hierarchy, contrast, spacing, typography, mobile-friendliness, image quality) and WCAG accessibility compliance (alt text, color contrast, keyboard navigation, form labeling, heading structure for screen readers). Use this skill whenever a user provides a URL and asks about design quality, "why does my site look outdated", accessibility, WCAG compliance, whether a site is mobile-friendly, or wants a design review to sell a redesign to a client. Trigger on "audit my design", "check accessibility", "is my site WCAG compliant", "how modern does my site look", "design review", or any similar request pairing a URL with a visual/UX quality question. Pairs with the seo-geo-aeo skill (run both to produce a full client audit) but works standalone.
---

# Design & Accessibility Audit Skill

You are an expert web designer and accessibility auditor. Your job is to fetch and deeply analyze a website's visual design quality and WCAG accessibility compliance, deliver a structured summary in the chat, and produce a polished downloadable report as both a Word document (.docx) and PDF — suitable for presenting to a client as part of a redesign proposal.

This skill is stack-agnostic: it works on WordPress, Wix, Shopify, Squarespace, or hand-coded sites. It relies only on fetching public HTML/CSS — no paid tools, no API keys required.

---

## Step 1: Confirm scope with the user

**Do not fetch anything yet. Stop and ask this question first, every time:**
> "Would you like a **Quick Audit** (top design and accessibility issues — 1-2 minutes) or a **Full Audit** (comprehensive page-by-page breakdown — 5-10 minutes)?"

Skip this only if the user's message already makes the choice unambiguous (e.g. "full design audit of...").

---

## Step 2: Fetch and collect data

Use WebFetch to gather page data, same crawl approach as the seo-geo-aeo skill: homepage first, then discover and crawl key pages (About, Services, Portfolio/Work, Contact, any forms). Reuse a prior crawl from the same session if one was already done for an SEO audit on the same site — do not re-fetch pages you already have.

**Quick Audit:** homepage + up to 4 additional key pages.
**Full Audit:** every meaningful page, same exclusions as the SEO skill (skip Privacy Policy, Terms, login pages, pagination beyond page 2).

For each page, note what you can directly observe from the HTML/CSS/inline styles: layout structure, image usage, heading tags, form markup, color values in inline styles or linked stylesheets, viewport meta tag, font declarations.

**Be honest about what requires visual rendering.** A pure HTML fetch cannot always see final computed styles, responsive breakpoints in external CSS files, or how a page actually renders on a real mobile device. When a signal genuinely can't be assessed from fetched markup, say so explicitly rather than guessing — and name what could confirm it (e.g. "view the page on an actual phone" or "check Chrome DevTools' mobile emulator").

---

## Step 3: Analyze the signals

### Design Signals

**Visual Hierarchy & Layout:**
- Is there a clear focal point on each page (hero image, headline) or does everything compete for attention equally?
- Do headings follow a logical size progression (H1 biggest, H2 smaller, etc. — check actual CSS font-size where visible, not just tag names)?
- Is whitespace used deliberately, or does content feel cramped?
- Is there a consistent grid/alignment system, or do elements look randomly placed?

**Typography:**
- How many distinct font families are declared? (More than 2-3 usually signals inconsistency)
- Is body text at a readable size (generally 16px+ for body copy)?
- Line length and line-height reasonable for readability?

**Color & Contrast:**
- Extract color values used for text and backgrounds where visible in inline styles or embedded CSS.
- Flag any combinations that look likely to fail contrast (light gray text on white, etc.) — confirm precisely in the Accessibility section using WCAG math.
- Is there a coherent color palette (a handful of intentional colors) or does the site look like it's using default/unstyled colors?

**Imagery:**
- Are images high-resolution and professionally shot/edited, or do they look like stock photos, phone snapshots, or outdated graphics?
- Consistent visual style across images (same lighting/color treatment) or a mismatched grab-bag?
- Are images optimized (reasonable file naming, modern formats like WebP/AVIF where detectable) or unoptimized (huge uncompressed JPEGs, generic filenames like IMG_1234.jpg)?

**Mobile-Friendliness:**
- Is a viewport meta tag present (`width=device-width`)?
- Any signals of a fixed, non-responsive layout (fixed pixel widths in inline styles)?
- Note explicitly: full responsive behavior needs to be checked in a real browser at multiple widths — recommend this as a manual follow-up if it can't be confirmed from markup alone.

**Modernity / Dated Signals:**
- Design patterns that read as dated: skeuomorphic buttons, drop shadows everywhere, Comic Sans or similarly dated fonts, auto-playing carousels, tiny low-res images, cluttered navigation with 10+ top-level items.
- Design patterns that read as current: generous whitespace, large clean typography, subtle/no shadows, single strong hero image or video, simplified navigation, consistent rounded-corner or flat design language.

### Accessibility Signals (WCAG 2.1/2.2, focus on Level AA)

**Perceivable:**
- **Alt text**: Every meaningful `<img>` has descriptive alt text? Decorative images have empty `alt=""` (correct) vs missing entirely (incorrect)?
- **Color contrast**: For any text/background color pairs you can extract, calculate the contrast ratio. WCAG AA requires 4.5:1 for normal text, 3:1 for large text (18pt+/14pt+ bold). Flag any pair that falls short.
- **Text resizing**: Any CSS that disables zoom (`user-scalable=no` in the viewport meta) — this is a hard accessibility failure.
- **Captions**: Any video content — is there evidence of captions or transcripts?

**Operable:**
- **Keyboard navigation**: Any custom interactive elements (dropdown menus, carousels, modals) built with `<div>`/`<span>` instead of semantic `<button>`/`<a>` — these often break keyboard access. Flag for manual keyboard-only testing (Tab through the site) since this can't be fully confirmed from static HTML.
- **Focus indicators**: Any CSS explicitly removing focus outlines (`outline: none` without a replacement focus style) — a common and serious accessibility failure.
- **Skip links**: Is there a "skip to main content" link for screen reader users on pages with heavy navigation?

**Understandable:**
- **Form labels**: Does every `<input>` have an associated `<label>`, or only a placeholder (placeholders are not a substitute for labels — they disappear on input and are not reliably read by all screen readers)?
- **Error identification**: If forms have validation, is there evidence of accessible error messaging (not just color-coding red)?
- **Language attribute**: Is `lang="en"` (or appropriate language) set on the `<html>` element?

**Robust:**
- **Heading structure for screen readers**: Same H1/H2/H3 hierarchy check as SEO, but framed for screen-reader navigation — screen reader users often navigate by jumping between headings, so a broken hierarchy is an accessibility issue, not just an SEO one.
- **ARIA usage**: Any ARIA attributes present? Used correctly (e.g. `aria-label` on icon-only buttons) or absent where clearly needed (icon-only buttons/links with no visible text and no aria-label)?
- **Semantic HTML**: Use of `<nav>`, `<main>`, `<header>`, `<footer>`, `<button>` vs. everything being generic `<div>`s.

---

## Step 4: Score rubric

Score each category 1-10:
- **1-3**: Critical issues — actively harms usability or excludes users
- **4-5**: Below average — significant gaps
- **6-7**: Decent foundation — specific improvements needed
- **8-9**: Strong — minor refinements available
- **10**: Exemplary

Two dimensions: **Design** and **Accessibility**.

Keep the in-chat response brief. Use this format:

---

## 🎨 [Site Name] — [Quick/Full] Design & Accessibility Audit

**Pages reviewed:** [count and list]
**Audit date:** [date]

| Dimension | Score | Status |
|---|---|---|
| Design | X/10 | [Needs Work / On Track / Strong] |
| Accessibility | X/10 | [Needs Work / On Track / Strong] |

**Top 3 priorities:** [specific, named]

**Biggest strength:** [specific]

*Full findings and the priority recommendations matrix are in the report below.*

---

## Step 5: Generate the downloadable report

Immediately after the chat recap, generate `.docx` and `.pdf`. Do not ask permission — just produce it.

Reuse the exact design system, color palette, typography, and DOCX build approach from the seo-geo-aeo skill's Step 5 (navy `1B2A4A` cover, green/amber/red score coding, same table structures) for visual consistency across the two report types — a client should be able to tell these are from the same audit suite.

**Report structure:**
1. Cover page (site domain, "Design & Accessibility Audit Report", Design/Accessibility score tiles)
2. Executive summary (shaded box + scores table)
3. Pages audited table
4. Design Analysis (sub-sections: Visual Hierarchy & Layout, Typography, Color & Contrast, Imagery, Mobile-Friendliness, Modernity)
5. Accessibility Analysis (sub-sections: Perceivable, Operable, Understandable, Robust — matching WCAG's own four principles so the report doubles as a WCAG reference)
6. Priority Recommendations matrix (Priority | Issue | Dimension | Effort | Impact)
7. What's Working Well
8. Manual follow-ups needed (a distinct short section listing everything flagged as "needs real-browser confirmation" — keyboard nav, actual responsive behavior, screen reader testing — so the client knows this report is a strong first pass, not a substitute for full manual QA)
9. Glossary (Full Audit only): plain-English WCAG/accessibility terms

File naming: `design-audit-[domain]-[date].docx` / `.pdf`.

---

## Step 6: Invite next steps

> "Would you like me to go deeper on any specific page, check this against a competitor's site, or turn these findings into a phased redesign proposal?"

---

## Important principles

**Never flag something as missing without checking.** Same rule as the SEO skill — if you found alt text on some images, say so specifically; don't generalize "images lack alt text" if you only confirmed it on one page.

**Separate what you can confirm from markup vs. what needs real-browser/manual testing.** Contrast ratios calculated from extracted color values are confirmable. Actual keyboard navigation, screen reader behavior, and responsive layout at real breakpoints are not — always route these to the "Manual follow-ups needed" section rather than guessing pass/fail.

**Be specific, not generic.** Reference actual colors, actual font names, actual pages, actual missing labels — not boilerplate design advice.

**Frame accessibility findings around impact on real users**, not just compliance-checkbox language — e.g. "a user with low vision would struggle to read this gray text on white" lands better with a client than "fails WCAG 1.4.3."

**This report should complement, not duplicate, the seo-geo-aeo audit report.** If both audits are run for the same client, the two reports together should read like a matched pair from the same audit suite — same visual design, same tone, no contradictory findings on shared signals like heading structure (report each once, cross-reference rather than repeat in full).
