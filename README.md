# Website Audit Skills for Claude

Two [Claude Agent Skills](https://www.anthropic.com/news/agent-skills) that turn a single URL into a client-ready audit report — no paid tools, no API keys, no manual copy-pasting.

Built for agencies and freelancers who need to analyze a prospect's or client's website, identify real issues, and hand over a professional Word/PDF report as part of a sales or delivery process.

## What's in here

### `seo-geo-aeo-audit/`
A full SEO audit that also covers **GEO** (Generative Engine Optimization — is this site understandable and citable by AI search tools like ChatGPT/Perplexity) and **AEO** (Answer Engine Optimization — is this site structured to win featured snippets and voice search).

**Design principle: measured, not guessed.** Performance, Accessibility, Best Practices, and the SEO category score come directly from Google PageSpeed Insights (Lighthouse) — a real, reproducible tool result, not a model's impression of the HTML. Structured data presence is verified against Google's own Rich Results Test. Everything else (on-page checks, GEO signals, AEO signals) is scored against a fixed yes/no checklist, so the same site audited twice produces the same numbers.

### `design-accessibility-audit/`
A companion audit covering visual design quality and WCAG accessibility — heading hierarchy, contrast, imagery, mobile-friendliness, form labeling, keyboard operability. Shares the same visual report design as the SEO skill so the two can be delivered together as a matched pair.

Both skills are explicit about the difference between what they can **confirm** from a live tool or fetched markup and what genuinely needs a **manual check** (live keyboard navigation, real rendered contrast, screen-reader testing) — they flag these separately rather than guessing.

## Why this approach

Most audit prompts ask an LLM to read HTML and assign a 1–10 score from impression. That's fast, but it's not reproducible, and it doesn't hold up if a client re-checks the numbers themselves.

These skills instead:
1. Pull real scores from free Google tools (PageSpeed Insights, Rich Results Test) wherever a real tool exists for the signal
2. Reduce everything else to a fixed, countable checklist instead of a subjective score
3. Clearly separate "measured" from "assessed" in the final report, so a client can verify the numbers independently

## Output

Both skills produce a two-part deliverable:
- A short chat summary (scores + top 3 priorities)
- A downloadable Word (.docx) and PDF report with an executive summary, full findings tables, a priority matrix (effort vs. impact), and a methodology section

## Requirements

- Claude.ai with Code execution and file creation enabled (Pro/Max/Team/Enterprise)
- For the ground-truth PSI/Rich Results steps: browser access (e.g. Claude in Chrome)
- No API keys or paid SEO tool subscriptions required

## Install

Download the `SKILL.md` from either folder, zip the folder, and upload it via **Settings → Capabilities → Skills** in claude.ai. See [Anthropic's Skills documentation](https://support.claude.com/en/articles/12512180-use-skills-in-claude) for the current install flow.

## License

MIT — fork it, adapt it, use it commercially.
