# Worked example — schema audit of example.com

Run on **October 12, 2026** against the homepage of [Example Plumbing](https://www.example.com/), a real local plumber with no connection to the author. Name, places, and contact details are replaced with placeholders. Inputs were the page's visible text and its two JSON-LD blocks, pulled from the live source. Output below is what **v1** of the prompt produced, lightly formatted — that's why it has a Severity column. The cross-check at the bottom is what turned it into the category/status columns of later versions. The current prompt is [`01-prompt/schema-audit.md`](../../01-prompt/schema-audit.md); run it on the same page and the format will differ.

> Why a real page: so you can run the same prompt on the same page in your own tool and compare. Where your output disagrees with this one, somebody's wrong — figure out who, and fix the prompt.

## What's on the page

Two JSON-LD blocks:

1. `LocalBusiness` + `Plumber` — name, address, geo, phone, email, hours (Mon–Fri 8–5), `priceRange`, `areaServed` (8 areas), `hasOfferCatalog` (4 services), `aggregateRating` (5.0 / 82), three full `Review` objects, `sameAs`.
2. `FAQPage` — 4 questions.

No microdata. Site generator: Astro.

## Findings

| # | Type | Issue | Severity | Fix |
|---|---|---|---|---|
| 1 | LocalBusiness | `aggregateRating` and three `Review` objects are Google reviews republished on the business's own site. Google's guidelines treat ratings/reviews about an entity, on that entity's own site, as **self-serving** — they're ineligible for review rich results (no stars). Policy as of Oct 2026 — confirm in Google's review snippet docs. | **Blocker** | Remove `aggregateRating` and `review` from the markup. Keep the reviews on the page as content. |
| 2 | Review | `datePublished` is `"April 2026"` / `"May 2026"` — not ISO 8601. | Should-fix (moot after #1) | `2026-04-15` format if reviews are ever kept. |
| 3 | LocalBusiness ↔ page | Schema `areaServed` lists 8 communities. Visible page says "Plumber Services Across **[Town 6]**" and "serving every corner of **[Town 6]**" — looks like a variable filled with the wrong area — an **inference**; the cause wasn't inspected. Same artifact appears in the blog intro ("…sewer health.[Town 6]."). | **Blocker** (content, not markup) | Find where that text comes from and fix it there. [Town 6] is one of eight areas, not the headline. |
| 4 | LocalBusiness ↔ page | Schema description: founder has "over 30 years of experience." Page hero: "[City]'s go-to plumbing **company** for 30+ years." Page body: "**Since 2007**." The person's experience and the company's age are being used interchangeably. | Should-fix | Pick one claim per sentence. Add `foundingDate: "2007"` (the year the site gives) to the markup so the company age is explicit. |
| 5 | LocalBusiness | No `logo`. Single `image`; Google recommends multiple aspect ratios (1:1, 4:3, 16:9) for LocalBusiness. | Should-fix | Add `logo`; make `image` an array of three crops. |
| 6 | OfferCatalog | Four `Service` items have no `url`. First one is named "Plumber" — a job title, not a service. | Should-fix | Add `url` for each service page. Rename "Plumber" to "Residential & Commercial Plumbing." |
| 7 | LocalBusiness | `openingHoursSpecification` covers Mon–Fri only. Page shows Sat/Sun Closed. Not wrong — just implicit. | Nice-to-have | Add a Sat/Sun entry with `opens`/`closes` of `00:00` to state closed explicitly. |
| 8 | FAQPage ↔ page | FAQ answer says emergency plumbing is handled "during business hours Monday through Friday, 8am to 5pm." **Interpretation:** most searchers read "emergency" as any-hour. | Should-fix (content) | Either offer after-hours and say so, or drop the word "emergency." |
| 9 | FAQPage | Valid, matches the visible FAQ. Google stopped showing FAQ rich results for all sites on May 7, 2026. *(Updated after the run — both tools cited the older 2023 restriction to government and health sites. Neither caught the change.)* | Nice-to-have | Harmless to keep; other tools may still read it. Don't expect a Google feature from it. |
| 10 | Missing | No `BreadcrumbList`. Blog posts not checked here but should carry `BlogPosting`. Service pages should carry their own `Service` markup. | Nice-to-have | Out of scope for the homepage; next audit. |
| 11 | Title / meta ↔ page | "#1 Plumbing Company in [City]" in the title and "#1 local plumber" in the meta description. Nothing on the page substantiates a ranking. | Nice-to-have | Replace with something verifiable ("family-run since 2007") or drop it. *(Caught by the ChatGPT cross-check, not by the Claude run.)* |

**Rich result eligibility, type by type**

- `LocalBusiness` / `Plumber` — valid markup Google can use for business details. Google doesn't guarantee how, or whether, it shows them.
- Review snippet — **not eligible** (self-serving). Remove.
- `FAQPage` — no FAQ rich results for any site since May 7, 2026. Keep or drop; no Google effect.

## Corrected JSON-LD

```json
{
  "@context": "https://schema.org",
  "@type": ["LocalBusiness", "Plumber"],
  "@id": "https://www.example.com/#business",
  "name": "Example Plumbing INC",
  "description": "Family-run plumbing company in [City], [State], founded in 2007 by [City] native [Owner]. Residential and commercial plumbing, water heaters, drain and sewer service, septic, excavation, and water treatment across [County].",
  "url": "https://www.example.com",
  "telephone": "+1-555-010-0189",
  "email": "office@example.com",
  "foundingDate": "2007",
  "founder": { "@type": "Person", "name": "[Owner]" },
  "logo": "[https://www.example.com/images/logo.png]",
  "image": [
    "[1:1 crop — does not exist yet]",
    "[4:3 crop — does not exist yet]",
    "https://www.example.com/images/og-home.webp"
  ],
  "priceRange": "$$",
  "address": {
    "@type": "PostalAddress",
    "streetAddress": "[street address]",
    "addressLocality": "[City]",
    "addressRegion": "[State]",
    "postalCode": "[ZIP]",
    "addressCountry": "US"
  },
  "geo": { "@type": "GeoCoordinates", "latitude": "[latitude]", "longitude": "[longitude]" },
  "openingHoursSpecification": [
    { "@type": "OpeningHoursSpecification", "dayOfWeek": ["Monday","Tuesday","Wednesday","Thursday","Friday"], "opens": "08:00", "closes": "17:00" },
    { "@type": "OpeningHoursSpecification", "dayOfWeek": ["Saturday","Sunday"], "opens": "00:00", "closes": "00:00" }
  ],
  "areaServed": [
    { "@type": "City", "name": "[City], [State]" },
    { "@type": "City", "name": "[Town 2], [State]" },
    { "@type": "City", "name": "[Town 3], [State]" },
    { "@type": "City", "name": "[Town 4], [State]" },
    { "@type": "City", "name": "[Town 5], [State]" },
    { "@type": "Place", "name": "[Town 6], [State]" },
    { "@type": "Place", "name": "[Town 7], [State]" },
    { "@type": "Place", "name": "[Town 8], [State]" }
  ],
  "hasOfferCatalog": {
    "@type": "OfferCatalog",
    "name": "Example Plumbing INC Services",
    "itemListElement": [
      { "@type": "Offer", "itemOffered": { "@type": "Service", "name": "Residential & Commercial Plumbing", "url": "https://www.example.com/[plumber-page]" } },
      { "@type": "Offer", "itemOffered": { "@type": "Service", "name": "Septic System Service", "url": "https://www.example.com/[septic-page]" } },
      { "@type": "Offer", "itemOffered": { "@type": "Service", "name": "Excavating Contractor", "url": "https://www.example.com/[excavating-page]" } },
      { "@type": "Offer", "itemOffered": { "@type": "Service", "name": "Water Treatment Service", "url": "https://www.example.com/[water-treatment-page]" } }
    ]
  },
  "sameAs": [
    "https://www.facebook.com/[business]",
    "https://www.instagram.com/[business]/"
  ]
}
```

Everything in square brackets is an assumption — the service page paths, the logo path, two image crops that don't exist yet. Fill or cut before deploying, then validate. This is a draft, not deployable code. [Town 6], [Town 7] and [Town 8] are unincorporated, so they're `Place`, not `City`. The `00:00`/`00:00` weekend entry is Google's documented way to mark a day closed in `LocalBusiness` hours — check their structured data docs for "closed all day" if you want to confirm.

The `FAQPage` block is fine as-is. Leave it.

## Cross-checked in ChatGPT (same day)

Same prompt, same page, run in ChatGPT. It agreed on the blockers and the content problems: the self-serving reviews, the date format, FAQ ineligibility, the [Town 6] text, the 30-years-vs-2007 muddle, the emergency wording, the weak "Plumber" service name. It added #11 above and correctly knocked `City` off three unincorporated communities. It skipped `foundingDate`, service URLs and image ratios, and it flagged several things as "unverifiable" (coordinates, social profiles, `priceRange`) that the Claude run took on faith.

Then it was asked to critique this file. Its best point: v1 of the prompt had one word — "blocker" — doing three jobs (invalid markup, a Google policy, a typo on the page), and no way to say "I can't tell from what you pasted." That's why v2 of the prompt has a category column and a status column. The cross-check improved the prompt more than it improved the audit.

It also raised three findings that turned out to be wrong — and the reason matters. The first cross-check input had the page text *abbreviated*: review bodies replaced with "[Google review text]", two FAQ answers trimmed, the footer summarized. ChatGPT flagged placeholder reviews, FAQ answers that didn't match the page, and an address it couldn't verify. All three are fine on the real page. The input was bad.

**The prompt is only as good as what you paste into it.** Paste the whole page. Don't summarize it for the AI.

## Check this work

Two of the findings rest on Google policy (#1 self-serving reviews, #9 FAQ eligibility). Both tools raised both. Policies change — #9 already did, between the 2023 rule both tools cited and May 2026. Confirm against Google's current structured data documentation before you build a slide on them.

## What this says about the prompt

It caught the content problems (#3, #4, #8) because step 3 tells it to compare markup to the visible page. It caught #1 because it knows the guideline. It would not have caught #10 — the prompt only looks at the page you give it. That's fine. It's a page auditor, not a site auditor. Build the site auditor as rung 3.

*File edited Oct 12, 2026, after the Codex and ChatGPT repo reviews: labeled as a v1 run, updated #9 for Google's May 2026 FAQ change, labeled inferences, removed the manual-action line.*
