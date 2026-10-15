---
name: wall-of-love-builder
description: Create a Bragly wall of love page from a team's best reviews and hand back the public link. Use when the user wants a wall of love, testimonial page, or a page showing off their reviews.
---

# Wall of love builder

Uses the `bragly` MCP tools.

## Steps

1. **Team.** If unclear and the user has several, call `list_accounts` and ask.
2. **Check what exists.** Call `list_walls`. If one already covers the user's goal, offer it instead of creating a duplicate.
3. **Check there's enough to show.** Call `list_reviews` with `rating: 5`, `status: public`. A new wall shows 4+ star reviews (up to 20) by default; if there are fewer than ~6, tell the user the wall will look thin and suggest collecting more first (`list_forms` + `get_form_link` gives them a link to share).
4. **Name and theme.** Ask for a name if the user gave none (suggest "<Company> Wall of Love"). Pick a `theme` to match the brand if the user expressed a style; otherwise use the default.
5. **Create.** Call `create_wall_of_love` with `name` (and `slug`/`theme` if chosen). On a slug clash, retry once with a suffixed slug.
6. **Optional curation.** If the user wants only certain reviews featured, hide off-message ones only with their explicit confirmation — hiding also removes them from every widget.

## Hand back

- `publicUrl` — the shareable page.
- `editUrl` — to fine-tune layout, filters and design in the dashboard.
- A preview of 3 reviews likely to appear (reviewer, rating, short excerpt).
