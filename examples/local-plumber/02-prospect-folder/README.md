# Example Plumbing — prospect folder

**Example Plumbing INC** is a real plumbing company in [City], [State]. The author has no connection to them. Name, places, and contact details are replaced with placeholders. This folder is what an agency builds *before* a first call — a prospect file — so the factual observations are drawn from public sources: their website, their Google Business Profile, and the Google local results for their core queries. Inferences and proposals are identified separately.

Built October 12, 2026. Revised the same day after a cross-check in ChatGPT (see "What the cross-check changed"). It's a snapshot. Their site will change.

**How to read it.** Factual claims carry a source tag. Inferences are labeled. `goals.md` holds the proposals.
- A tagged line (`[site:home]`, `[gbp]`…) is an observation you can go check.
- A line starting **Inference:** is reasoning from the observations. It could be wrong.
- `goals.md` is **what we'd propose** — a proposal, labeled as one. It is not what Example Plumbing has said.

**What's different from a real client folder:** no owner quotes, no internal history, no "what they rejected." `preferences.md` is what we can observe they've chosen. When they become a client, their words replace the inferences.

## Sources

| Tag | Source | Captured |
|---|---|---|
| `[site:home]` | https://www.example.com/ | 2026-10-12 |
| `[site:about]` | https://www.example.com/about | 2026-10-12 |
| `[site:blog]` | https://www.example.com/blog (index page only) | 2026-10-12 |
| `[site:schema]` | JSON-LD in the homepage source | 2026-10-12 |
| `[gbp]` | Google Business Profile fields (name, address, phone, hours, rating, count, five most recent reviews) via Google Places | 2026-10-12 |
| `[local-results]` | Google local results for "plumber [City] [State]", "commercial plumber [City] [State]", "septic service [City] [State]", returned as one merged list — **per-query positions are not recoverable from this capture** | 2026-10-12 |
| `[competitor-reviews]` | Up to five review excerpts per business, returned with the local results above | 2026-10-12 |
| `[competitor-site]` | A competitor's own homepage: Competitor D's site, Competitor H's site | 2026-10-12 |
| `[audit]` | `examples/local-plumber/01-schema-audit.md` — derived from `[site:schema]` and `[site:home]`, not an independent source | 2026-10-12 |

Pages **not** captured: contact, projects, individual service pages, individual blog posts, area pages. Where the folder counts service or area pages, that's from the homepage's link list, not from visiting them.

## What the cross-check changed

A second AI reviewed the first version of this folder and found two claims that contradicted the folder's own competitor table ("every competitor has more reviews" — false for two; "every competitor shows 24 hours" — false for one), several inferences written as facts (blog "programmatic," copy problems as "template bugs," a site "rebuild" with no date), and three predictions about what the owners would think or do. A second pass caught a rating tie, an area-pages scope contradiction, and a dozen precision issues; a third pass returned wording only. The identified issues were addressed in the revised files. The cross-check outputs themselves aren't in the repo; `log.md` summarizes each pass.
