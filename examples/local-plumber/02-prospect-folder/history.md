# History — Example Plumbing INC

> Prospect file. This is what we can *see* on the site as of October 12, 2026, with the dates the site gives. Where the site gives no date, the entry says "observed." Not an internal history. Newest first.

## October 2026 — Ten blog posts in ten days
- **Observed:** posts dated Oct 2, 3, 4, 5, 7, 7, 8, 9, 11, 11. Every title follows "[topic] in [city], [State]." Every one tagged Buyer's Guide. Read times 7–13 minutes. Cities rotate: [Town 3], [Town 7], [Town 6], [Town 5], [Town 2], [City], [Town 4], [Town 8]. `[site:blog]`
- **Observed:** two titles promise 24-hour service `[site:blog]`, which the FAQ and GBP hours don't support `[site:home]` `[gbp]`; one is a DIY how-to `[site:blog]`; the index intro ends "sewer health. [Town 6]." `[site:blog]`
- **Inference:** the cadence and the identical title pattern suggest a templated process. How the posts are produced is unknown. Worth asking.

## Observed October 2026 — Current site build
- **Observed:** generator meta tag reads Astro v6.2.1. `[site:home]` Links from the homepage: 4 service categories with 20 sub-pages, 8 area pages, projects, blog, about, contact, review. `[site:home]` (extracted from the homepage's links; those pages weren't visited)
- **Observed:** about page reads "Plumber backed by Since 2007 years of local experience" and shows a stats block "467+ / 2 SERVICE AREAS / 5+ SERVICES OFFERED." `[site:about]` Homepage reads "serving every corner of [Town 6]" under a [City] heading. `[site:home]` `[audit]`
- **Inference:** these look like unresolved template variables. The cause wasn't inspected. When the site was built or rebuilt is not observable from the capture.

## Observed October 2026 — Structured data
- **Observed:** `LocalBusiness`/`Plumber` and `FAQPage` JSON-LD on the homepage. `[site:schema]` The business block includes three Google reviews and an `aggregateRating` republished as markup. `[site:schema]` Separately, the review `datePublished` values are in "April 2026" format rather than ISO 8601. `[site:schema]`
- Finding detail and corrected markup: `[audit]`. The review markup is a rich-result eligibility issue under Google's self-serving review rule. The date format is a validation issue. Different fixes.
- When the markup was added is not observable.

## Google reviews
- **Observed:** 83 reviews, 5.0. The five reviews returned in the capture are dated April–May 2026. `[gbp]` (Whether newer ones exist isn't established by a five-review capture.) Recurring themes: on time, explains the work, fair price, handled permits. `[gbp]`
- **Inference:** a five-review sample says nothing reliable about velocity. A review-ask process is a reasonable thing to propose; whether it's the cheapest win depends on things not measured here.

## Service area lists
- **Observed:** homepage schema and the homepage's area-page links name 8 communities. `[site:schema]` `[site:home]` The about page's list has ten entries, including a duplicate [City] entry and references to [Town 9] and [Town 10]. `[site:about]`
- The lists differ. Whether they share a source is unknown. Impact unknown.

## Before 2026
- Company founded 2007. [Owner] has 30+ years in the trade. `[site:about]`
- Nothing else about the site's history is observable from the current capture. A Wayback Machine pass would fill this in.
