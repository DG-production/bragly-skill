---
name: review-triage
description: Triage a Bragly team's recent reviews — classify sentiment, tag themes and complaints, and flag negative reviews for follow-up or hiding. Use when the user asks to triage, sort, clean up, go through or review their new/recent reviews.
---

# Review triage

Uses the `bragly` MCP tools. Goal: every recent review has sentiment, useful tags, and negative ones are surfaced to the user.

## Steps

1. **Pick the team.** If the user hasn't named one and has several, call `list_accounts` and ask. Pass the slug as `account` on every later call.
2. **Pick the window.** Default to the last 30 days (`from` = today − 30). Say which window you used.
3. **Classify.** Call `classify_unclassified_reviews`; keep passing `nextCursor` back until `remaining` is 0.
4. **Survey.** Call `list_reviews` with `from`, paging with `offset` until done (cap at ~200 reviews; say so if truncated). Note counts by sentiment, rating and source.
5. **Tag themes.** From the review text, pick 3–6 recurring themes (e.g. "Onboarding", "Pricing", "Support"). Check `list_tags` first and reuse existing tags with the same meaning. For each theme call `tag_reviews` with `tagName`, the same `from`, and a `topic` describing the theme. If `topic` screening is unavailable, pass explicit `reviewIds` you chose instead.
6. **Flag negatives.** Tag `sentiment: NEGATIVE` (and rating ≤ 2) reviews with `Needs Follow-up` via `tag_reviews`.
7. **Hiding is the user's call.** Never call `update_review_status` with `hidden` on your own. List candidates (spam, abusive, off-topic) with reviewer, rating and a one-line excerpt, and hide only the ones the user confirms.

## Report back

- Window, total reviews, sentiment split, average rating.
- Tags applied: name → count.
- Negative reviews needing follow-up: reviewer, source, rating, one-line excerpt.
- Any hide candidates awaiting the user's decision.

Keep it short; quote reviewers verbatim, never paraphrase a quote.
