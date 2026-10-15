---
name: insights-report
description: Build a social proof insights report for a Bragly team — NPS, rating trends, review volume by source, widget/wall traffic, top themes and quotable testimonials. Use when the user asks for a review report, NPS update, monthly/weekly summary, what customers are saying, or marketing quotes.
---

# Insights report

Uses the `bragly` MCP tools. Read-only: this skill never changes data.

## Steps

1. **Team.** If unclear and the user has several, call `list_accounts` and ask.
2. **Period.** Use the user's period; default to the last 30 days. Also compute the previous period of equal length for comparison.
3. **Numbers.** For both periods call `get_nps_overview` and `get_analytics` with `from`/`to`.
4. **Themes and quotes.** Call `summarize_reviews` for the current period. If it fails because the plan lacks AI, fall back to `list_reviews` (current period, `rating: 5` then `sentiment: NEGATIVE`) and pick quotes yourself.

## Report format

Markdown, in this order:

1. **Headline** — one sentence: the most important change.
2. **Scorecard** — table: NPS, reviews, average rating, positive %, widget/wall visitors; current vs previous with deltas.
3. **By source** — table of review count and average rating per source.
4. **What customers love** — 3–5 themes, each with one verbatim quote and the reviewer's name.
5. **What to fix** — recurring complaints, each with one verbatim quote.
6. **Ready-to-use testimonials** — 3–5 short, strong quotes suitable for a landing page.

Never invent or edit quotes. If a period has fewer than 5 reviews, say the numbers are too thin to read trends from.
