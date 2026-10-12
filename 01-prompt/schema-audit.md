# Rung 1 — The schema audit prompt

A saved prompt that does one job. You paste in a page's content and its JSON-LD; you get back a findings table and the corrected code. Same format every time, so you can skim it.

## The prompt

Copy everything between the lines.

---

You are a technical SEO reviewing structured data. I'll paste a page's visible content and its JSON-LD.

1. List every schema type present and whether it's valid against schema.org.
2. For each type, flag required or recommended properties that are missing.
3. Flag anything in the markup that contradicts the visible page — name, price, dates, address, hours, ratings — and anything on the page that contradicts itself.
4. Say which rich result each type is eligible for and what's blocking it.
5. Return a corrected JSON-LD draft. Put square brackets around any value you had to assume (a URL you can't see, an image that may not exist), then list every bracketed value under the code block.

Every finding says whose rule it is (schema.org, Google's structured data documentation, or the page itself) and gets a category and a status:

- Category: `validation` (invalid against schema.org or a missing required property), `eligibility` (valid markup that Google's policies won't reward), `content` (markup contradicts the page, or the page contradicts itself), or `optimization` (optional improvement).
- Status: `confirmed` (you can point to it in what I pasted), `unverifiable` (the markup says it, the page doesn't show it, could be true), or `input-gap` (you'd need something I didn't paste to judge it).

Format: a findings table with columns `type · issue · rule source · category · status · fix`, sorted validation, then content, then eligibility, then optimization. Then one code block with the draft JSON-LD, then the list of bracketed values. Don't explain what schema is. Don't pad. If there's no structured data on the page, say so and suggest the two types that would matter most for this page, with a draft of each.

---

*v3 — Oct 12, 2026. Codex and ChatGPT reviewed the repo. The corrected code is now called a draft, with its guesses listed; every finding names whose rule it breaks; the sort order is defined (v2 still said "blockers first" after blockers were gone).*

*v2 — Oct 12, 2026. v1 had three severity levels and no status column. A cross-check in ChatGPT showed it couldn't tell a confirmed error from something it just couldn't see in the input. The category/status split fixes that.*

## What you provide

1. **The page's visible text** — select-all on the rendered page, paste it all. Don't summarize.
2. **The page's JSON-LD** — every `<script type="application/ld+json">` block from view-source.

The prompt has no business baked in. It works on any page.

## How to use it

1. **Get the page text.** Open the page in Chrome or Edge. Click into the page, press Ctrl+A (Cmd+A on a Mac), then Ctrl+C.
2. **Get the JSON-LD.** Press Ctrl+U (Cmd+Option+U on a Mac) to open the page source. Press Ctrl+F and search for `ld+json`. Copy each block from `<script type="application/ld+json">` through its `</script>`. There may be more than one.
3. **Nothing found?** Some sites add structured data with JavaScript after the page loads, so it's not in the source. Paste the URL into Google's [Rich Results Test](https://search.google.com/test/rich-results) — it loads the page the way Google does and shows what it found. If that shows nothing either, the page has none; say so when you paste.
4. Paste the prompt, then the page text, then the JSON-LD.

## Before you trust it

Run it on three pages you've already audited by hand. Where it disagrees with you, decide who's right. If it's the prompt, fix the prompt. Do this once; then save it.

Before any corrected code goes live: replace or delete every bracketed value, then run it through the [Schema Markup Validator](https://validator.schema.org/) (is it valid schema.org?) and Google's [Rich Results Test](https://search.google.com/test/rich-results) (will Google use it?). Those are two different questions. You approve the code, not the prompt.

## Why it's written this way

- **The numbered list.** Each line is a hand. If the output skips one, you know which.
- **The format line.** You'll run this two hundred times. Make it skimmable the first time.
- **"Don't explain."** It's a tool, not a tutor. Cut the preamble.
- **The empty-page fallback.** Half the pages you check won't have schema at all. Make the prompt useful in that case too.
- **Category and status.** "Blocker" meant three different things in v1 — invalid markup, a Google policy, and a typo on the page. They're different fixes for different people. And "status" forces the tool to admit when it's guessing. That one line is the difference between a finding you act on and one you have to re-check yourself.
- **Brackets for assumptions.** The corrected markup will contain things the tool can't see. Make it mark them, so you don't ship a guess.

## Paste the whole page

The prompt is only as good as what you paste into it. The first time this prompt was cross-checked, the page text had been abbreviated — and it produced three confident, wrong findings about things that were fine on the real page. Paste everything. Don't summarize for the AI.

## Saving it

**Claude:** Create a Project called "SEO Tools." Paste the prompt into the project's instructions, or save it as a Skill if your plan offers them. Then every chat in that project already knows the job — you just paste the page.

**ChatGPT:** Create a Project called "SEO Tools." Paste the prompt into the project's instructions. (Don't build this as a Custom GPT — those are being retired.)

**Anything else:** Keep it in a text file. It's just text.

## Variations

Swap the job and keep the shape. The same structure works for:

- **GBP post generator** — paste this month's offers/events, get four weeks of posts in the client's voice, each under 1,500 characters, with a CTA.
- **SERP pattern read** — paste the top 10 titles and descriptions for a query, get the content format, angle, and gap.
- **Keyword clustering** — paste a raw export, get clusters by intent with a suggested page per cluster.

Rule for all of them: fixed input, fixed output, no explaining.
