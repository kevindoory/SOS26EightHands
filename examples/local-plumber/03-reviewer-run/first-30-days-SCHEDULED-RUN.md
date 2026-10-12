# Scheduled run — first-30-days draft, run on a trigger

- **Run time:** 2026-10-12, 16:59 UTC (clone) – ~17:03 UTC (both agents returned)
- **Repo commit:** `5f7bf9c`
- **Prompt versions:** Reviewer v4 · Fact-checker v3 (both Oct 12, 2026)

**How it was run.** A one-off Claude scheduled task, unattended, in a cloud session. Nobody was watching. It cloned the repo and ran two separate subagents one after the other, with no file access, working only from pasted text. Agent 1 (Reviewer) got the reviewer prompt, the six prospect-folder files (README excluded), and the draft with its warning banner removed. Agent 2 (Fact-checker) got the fact-checker prompt, the same six files, the same draft, and Agent 1's output verbatim. Neither agent saw `first-30-days-REVIEW.md` or any README. The scoring was added afterward. The report arrived by email and push notification. This is the same mechanism as [`03-agent/scheduled-review.md`](../../../03-agent/scheduled-review.md), pointed at this example instead of a private repo.

> Names, places, and contact details have since been replaced with placeholders, and a few folder lines were reworded after the run (for example, "a rating tie I'd missed" now reads "a missed rating tie"). Quotes below are what the agents saw at the time, with names replaced.

---

## Agent 1 — Reviewer (verbatim)

**Blockers**

1. **Review count is wrong.** Where: "Where you are", "5.0 across 82 reviews." Source: brand.md: "5.0 rating, 83 Google reviews `[gbp]`. Site displays "82+" `[site:home]`." The client can open their own profile and see 83.

2. **"Fewest reviews" is false.** Where: "Where you are", "the fewest reviews of any established competitor." Source: competitors.md: "Example Plumbing is ninth by review count. Eight businesses have more reviews; two have fewer." Competitor I (51) and Competitor J (33) both have fewer. "Established" is undefined and doesn't rescue the claim. log.md shows this exact error was already caught and fixed once: "'every competitor has more reviews' (false for two businesses)."

3. **The #3 ranking is unsupported, and the folder says rank can't be recovered.** Where: "Where you are", "Your site currently ranks #3 for 'plumber [City] [State].'" Source: competitors.md: "Per-query positions aren't recoverable from this capture, so the table is sorted by review count, not rank." The client can search it themselves. The claim also blurs local-pack (GBP) results with "your site."

4. **Rec 4 rests on a false premise.** Where: Rec 4, "Every competitor in the results shows 24-hour availability." Source: competitors.md: "Nine of the ten other plumbers display 'Open 24 hours.' Competitor J displays 24-hour weekday hours and limited Saturday hours." log.md shows this was caught once already: "'every competitor shows 24 hours' (false for one)."

5. **Rec 4 tells them to publish a 24/7 claim that their own stated hours contradict.** Where: Rec 4, "Add 'available 24/7 for emergencies' to your Google profile and homepage hero."
   - brand.md, Things to avoid repeating: "'24/7' or '24-hour' — the FAQ says emergency calls are handled 'during business hours Monday through Friday, 8am to 5pm' `[site:home]`; GBP hours are Mon–Fri 8–5 `[gbp]`"
   - preferences.md: "Published hours are Mon–Fri 8–5. Site and GBP agree."
   - goals.md #2 marks this as an open question: "Either they offer after-hours and should say so everywhere, or they don't and the blog shouldn't promise it. We don't know which."

   The draft decides the question in the direction the folder flags as the existing error. It also "never says" a phrase brand.md lists as banned.

**Should-fix**

1. **The rating tie is left out.** Where: "Where you are", "You have the best rating in the [City] plumber results." Source: competitors.md: "Example Plumbing and Competitor I share the highest displayed rating, 5.0." Without the tie, the sentence reads as sole top rating. log.md: "A second pass caught a rating tie I'd missed."

2. **A prediction about review velocity is stated as fact.** Where: "Where you are", "the gap in volume will widen without a process." Source: history.md, Inference: "a five-review sample says nothing reliable about velocity."

3. **Unverified photos are called "real."** Where: "Where you are", "real project photos." Sources:
   - brand.md: "Photos accompany them; not independently verified."
   - preferences.md: "Whether the images are of those jobs wasn't verified."

4. **"The copy is honest" isn't supported, and the folder points the other way.** Where: "Where you are." No source found for the claim. Against it:
   - brand.md: "'#1 Plumbing Company in [City], [State]'... No substantiation found."
   - brand.md: the hero's "30+ years" "doesn't match the founding date."
   - Two blog titles promise 24-hour service.

5. **"The structured data is mostly right" isn't supported.** Where: "Where you are." No source found. history.md records two separate problems: "a rich-result eligibility issue under Google's self-serving review rule" and "The date format is a validation issue."

6. **Rec 1 claims what goals.md says isn't claimed.** Where: Rec 1, "Doesn't touch the rating; just the count." Source: goals.md, Not claimed: "that the rating will hold as the count grows."

7. **Rec 1 target has no source.** Where: Rec 1, "Target: 10 new reviews in 30 days." No source found. The "text link, one tap" mechanism also has no source found.

8. **Rec 2 doesn't serve a stated goal.** Where: Rec 2 (structured data). goals.md proposes four goals (review volume, hours, differentiators, blog) and a win of "More calls." Structured data appears in none of them.

9. **Rec 2 assumes items are missing from the markup.** Where: Rec 2, "Add a founding date, a logo, and links from each service in the markup to its page." No source found that any of these is absent from the current markup.

10. **Rec 2 effort estimate has no source.** Where: Rec 2, "One afternoon of dev work." No source found.

11. **Rec 2 skips the date-format fix the folder records.** Where: Rec 2. Source: history.md: "the review `datePublished` values are in 'April 2026' format rather than ISO 8601... Different fixes." The rec addresses only the self-serving review issue.

12. **Rec 3 doesn't serve a stated goal.** Where: Rec 3 (service area copy). No goal in goals.md covers the service-area lists. history.md: "Whether they share a source is unknown. Impact unknown."

13. **An inference is stated as fact.** Where: Rec 3, "which is a template error." Source: brand.md: "**Inference:** possible templating or copy/paste error; cause unknown."

14. **"Ten communities" miscounts.** Where: Rec 3, "Your about page lists ten communities." Source: history.md: "The about page's list has ten entries, including a duplicate [City] entry." That is ten entries, not ten communities.

15. **Rec 5 decides an open question.** Where: Rec 5 (DIY how-to series). Sources:
    - goals.md #4: "decide on purpose whether DIY content fits a call-driven business."
    - preferences.md: "**Inference:** worth asking whether that's intentional. DIY content can serve a call-driven business; it depends on what they want."

16. **Rec 5 repeats what's already in place.** Where: Rec 5. Sources:
    - history.md, October 2026: "one is a DIY how-to `[site:blog]`"
    - history.md: "Ten blog posts in ten days."
    - goals.md #4: "One is a DIY how-to: 'How to Flush a Toilet With No Water.'"

    The draft proposes more of the same before goals.md's first step: "ask who produces the posts and whether they're reviewed before publishing."

17. **Rec 5 claims and cadence have no source.** Where: Rec 5, "build trust and rank for high-volume queries" and "Three per month." No source found. Search volume was never measured.

18. **Rec 6 decides what goals.md only proposes to evaluate.** Where: Rec 6, "Add the septic category to your Google profile." Source: goals.md #3: "evaluate whether GBP category and septic service-page improvements could improve visibility."

19. **Rec 6 claims what the folder says isn't claimed.** Where: Rec 6, "This is the cheapest new visibility available to you." Sources:
    - goals.md, Not claimed: "that this set is easier to rank in... demand and difficulty weren't measured."
    - competitors.md: "**Not claimed:** that it's easier to rank there."

20. **Rec 6 generalizes from one capture.** Where: Rec 6, "you're not in them yet." Source: goals.md: "Example Plumbing did not appear among them in this capture." That was one capture, not an established absence.

21. **The measurement section contradicts goals.md.** Where: "What we'd measure", "Calls. Not rankings." Source: goals.md: "Rankings would be a secondary check." It also doesn't address goals.md: "What they measure: Unknown. Ask on the first call whether they track calls by source." Calls can't be the measure until tracking is confirmed.

22. **Untraceable items, all in one place:**
    - 82 reviews
    - ranks #3
    - "fewest reviews of any established competitor"
    - "gap will widen"
    - "real project photos"
    - "copy is honest"
    - "structured data mostly right"
    - 10 reviews / 30 days
    - "one tap" text link
    - "doesn't touch the rating"
    - founding date, logo and service links missing from the markup
    - "one afternoon"
    - "template error"
    - "ten communities"
    - "high-volume queries"
    - "three per month"
    - "build trust"
    - "cheapest new visibility"

**Nitpicks**

1. The header says "Draft for internal review," but this is going to the client.
2. Rec 1 is titled "Review velocity," while goals.md frames the goal as review volume. history.md says velocity can't be judged from the data.
3. "Where you are" uses #3 rankings as its headline evidence, then "What we'd measure" says "Not rankings." The draft contradicts itself.
4. "Real phone number, real address, real reviews, real..." repeats "real" four times. That reads as filler, against the plain, direct voice in brand.md.
5. Rec 3 quotes "serving every corner of [Town 6]" but doesn't mention the same stray "[Town 6]" at the end of the blog index intro (goals.md #4).

**Verdict**

Needs a rewrite: three of the four claims in the opening section are wrong or untraceable, and Rec 4 asks the client to publish a 24/7 claim that their own hours contradict.

---

## Agent 2 — Fact-checker (verbatim)

**Blockers**

1. **82 reviews.** VERIFIED. brand.md: "5.0 rating, 83 Google reviews `[gbp]`. Site displays "82+" `[site:home]`."
2. **"Fewest reviews" is false.** VERIFIED. competitors.md: "Example Plumbing is ninth by review count. Eight businesses have more reviews; two have fewer." The table shows Competitor I at 51 and Competitor J at 33. log.md: "'every competitor has more reviews' (false for two businesses)."
3. **"#3 for 'plumber [City] [State]'" is unsupported.** VERIFIED. competitors.md: "Per-query positions aren't recoverable from this capture, so the table is sorted by review count, not rank."
4. **"Every competitor... shows 24-hour availability."** VERIFIED. competitors.md: "Nine of the ten other plumbers display 'Open 24 hours.' Competitor J displays 24-hour weekday hours and limited Saturday hours." log.md: "'every competitor shows 24 hours' (false for one)."
5. **The 24/7 recommendation conflicts with stated hours.** VERIFIED. All three quotes match their files:
   - brand.md, "Things to avoid repeating": "'24/7' or '24-hour' — the FAQ says emergency calls are handled 'during business hours Monday through Friday, 8am to 5pm'… GBP hours are Mon–Fri 8–5"
   - preferences.md: "Published hours are Mon–Fri 8–5. Site and GBP agree."
   - goals.md #2: "We don't know which."

   One wording problem: "never says" is not a phrase in brand.md. The section heading is "Things to avoid repeating."

**Should-fix**

1. **Rating tie left out.** VERIFIED. competitors.md: "Example Plumbing and Competitor I share the highest displayed rating, 5.0." log.md: "A second pass caught a rating tie I'd missed."
2. **"Gap will widen" stated as fact.** VERIFIED. history.md: "**Inference:** a five-review sample says nothing reliable about velocity."
3. **"Real project photos."** VERIFIED. brand.md: "Photos accompany them; not independently verified." preferences.md: "Whether the images are of those jobs wasn't verified."
4. **"Copy is honest."** VERIFIED. No assessment of the copy's honesty exists in the folder. brand.md only lists "honest" as a word the site itself uses. The quotes against the claim are accurate: "No substantiation found on the captured pages" and "the hero one doesn't match the founding date."
5. **"Structured data mostly right."** VERIFIED. history.md: "The review markup is a rich-result eligibility issue under Google's self-serving review rule. The date format is a validation issue." (brand.md does say schema and GBP agree on name, address, phone and hours, but nothing calls the markup "mostly right.")
6. **"Doesn't touch the rating."** VERIFIED. goals.md, Not claimed: "that the rating will hold as the count grows."
7. **10 reviews in 30 days, and "one tap."** VERIFIED. Neither appears anywhere in the folder.
8. **Rec 2 serves no stated goal.** VERIFIED. goals.md has four goals (Review volume, The hours story, The differentiators, The blog) and "More calls." Structured data is in none of them.
9. **Founding date, logo and service links assumed missing.** VERIFIED. No file says what the current markup includes or lacks.
10. **"One afternoon."** VERIFIED. Not in the folder.
11. **Date-format fix skipped.** VERIFIED. history.md: "the review `datePublished` values are in 'April 2026' format rather than ISO 8601." Also: "Different fixes."
12. **Rec 3 serves no stated goal.** VERIFIED. No service-area goal in goals.md. history.md: "Whether they share a source is unknown. Impact unknown."
13. **"Template error" stated as fact.** VERIFIED. brand.md: "**Inference:** possible templating or copy/paste error; cause unknown."
14. **"Ten communities."** VERIFIED. history.md: "The about page's list has ten entries, including a duplicate [City] entry."
15. **Rec 5 decides an open question.** VERIFIED. goals.md #4: "decide on purpose whether DIY content fits a call-driven business." preferences.md: "worth asking whether that's intentional."
16. **Rec 5 repeats what's already in place.** VERIFIED. history.md: "one is a DIY how-to `[site:blog]`." goals.md #4: "How to Flush a Toilet With No Water" and "ask who produces the posts and whether they're reviewed before publishing."
17. **"Build trust," "high-volume queries," "three per month."** VERIFIED. None are in the folder. The reviewer's "search volume was never measured" is an inference, not a quote: goals.md only says demand wasn't measured for the septic set. The flag still holds because the folder has nothing on search volume.
18. **Rec 6 decides what goals.md only proposes to evaluate.** VERIFIED. goals.md #3: "evaluate whether GBP category and septic service-page improvements could improve visibility."
19. **"Cheapest new visibility."** VERIFIED. goals.md: "Not claimed: that this set is easier to rank in… demand and difficulty weren't measured." competitors.md: "Not claimed: that it's easier to rank there."
20. **"Not in them yet."** VERIFIED. goals.md: "Example Plumbing did not appear among them in this capture."
21. **Measurement section contradicts goals.md.** VERIFIED. goals.md: "Rankings would be a secondary check." Also: "Unknown. Ask on the first call whether they track calls by source."
22. **Untraceable roll-up.** VERIFIED as a summary, with one correction. "82" does trace to a source, the site's "82+" `[site:home]`; the problem is that it conflicts with GBP's 83, not that it's untraceable. "Fewest reviews" and "doesn't touch the rating" are contradicted by the folder rather than missing from it.

**Nitpicks**

1. **"Internal review" header, but the draft goes to the client.** UNVERIFIED. The reviewer cites nothing, and no file says where the draft is going.
2. **"Velocity" vs "volume."** VERIFIED. goals.md: "### 1. Review volume." history.md: "says nothing reliable about velocity."
3. **Rankings used as evidence, then "Not rankings."** VERIFIED. Both lines are in the draft: "Your site currently ranks #3…" and "Calls. Not rankings."
4. **"Real" four times.** VERIFIED. The draft has "real phone number, real address, real reviews, real project photos." brand.md: "Plain and direct." That this conflicts with the voice is the reviewer's judgment.
5. **Stray "[Town 6]" on the blog index not mentioned.** VERIFIED. goals.md #4: "The blog index intro ends with a stray '[Town 6].'"

**Misfiled**

- Should-fix 14 ("ten communities") and Should-fix 20 ("yet") are accurate but are precision issues, closer to nitpicks.
- Should-fix 22 isn't a separate flag. It repeats items already listed.

**MISSED**

- **MISSED:** "Your site already does the important things." This is an evaluative claim, and no file says which things are important or that the site does them.
- **MISSED:** "every button on your site is a phone number or a free-estimate form." goals.md lists a third call to action, "schedule a free inspection." The folder also only covers the CTAs on captured pages ("No booking tool, no pricing, no chat seen on the captured pages"), not "your site" as a whole.

**Tally**

31 of the reviewer's 32 flags held up. The one that didn't is Nitpick 1, which cites no source.

---

## Score (added after the report was written, against the seed list in `first-30-days-REVIEW.md`)

**Seeded mistakes: 6 of 6 caught by the reviewer, all six confirmed VERIFIED by the fact-checker.**

| Seeded mistake | Caught? | Where |
|---|---|---|
| "82 reviews" (profile says 83) | Yes | Reviewer Blocker 1 |
| "ranks #3" (unsupported) | Yes | Reviewer Blocker 3 |
| 24/7 rec: can't deliver, and the folder says to ask | Yes | Reviewer Blocker 5 (Blocker 4 catches the false premise behind it) |
| DIY series pre-empts an open question | Yes | Reviewer Should-fix 15 (also Should-fix 16: DIY content already exists) |
| "fewest reviews of any established competitor" (false) | Yes | Reviewer Blocker 2 |
| "10 new reviews in 30 days" (made-up target) | Yes | Reviewer Should-fix 7 |

**Severity shift compared with the v2 run:** "82" and "#3" moved from nitpicks to blockers. That fits v4's rule that an untraceable number the client could check and find wrong is a blocker. The DIY seed is now in Should-fix, the section v3 created for this kind of flag.

**Real issues found beyond the seeds:**
- **All four un-seeded catches from the earlier Claude run:** "every competitor shows 24-hour" (B4), the rating tie (SF1), "cheapest new visibility" (SF19), "ten communities" (SF14).
- **The earlier run's fact-checker-only catch,** "template error" stated as fact, was caught directly by the reviewer this time (SF13).
- **7 of the 9 extra issues ChatGPT found:** "gap will widen" (SF2), Recs 2 and 3 don't tie to a goal (SF8, SF12), DIY content already published (SF16), septic category skips the evaluation step (SF18), "doesn't touch the rating" (SF6), "Calls. Not rankings." vs "rankings would be a secondary check" (SF21).
- **New in this run:** "real project photos" when the folder says they're unverified (SF3), "copy is honest" (SF4), "structured data mostly right" (SF5), founding date, logo and service links assumed missing from the markup (SF9), "one afternoon" (SF10), "high-volume queries" and "three per month" (SF17).
- **The fact-checker's two MISSED items are both fair.**
- **Not caught this run (ChatGPT caught them):** "Pick one list" assumes we know which service-area list is right; agency vocabulary vs brand.md's plain voice; six commitments made to a prospect the folder says we haven't talked to.

**Weak or questionable flags:**
- **Nitpick 1 ("internal review" header) is a false flag.** The fact-checker correctly marked it UNVERIFIED.
- **Should-fix 11 (skips the date-format fix) is a gap, not an error,** and moves toward adding a recommendation, which the prompt forbids.
- **Should-fix 20 ("not in them yet" from one capture) is a stretch,** and the fact-checker suggested it was misfiled.
- **Should-fix 22 duplicates earlier items,** and "82" is traceable (the site shows "82+"); the fact-checker caught this.
- **Wording slip in Blocker 5:** "never says" isn't a phrase in brand.md (fact-checker noted it).

None of these is a real false accusation against the draft.

**Tally:**

| | This run (reviewer v4 / fact-checker v3, scheduled) | Earlier Claude run (v2 / v1, by hand) | ChatGPT run (by hand) |
|---|---|---|---|
| Seeded (6) | 6 | 6 | 6 |
| Un-seeded, real | ~19 (+2 fact-checker MISSED) | 4 (+1 fact-checker) | 13 |
| False or weak flags | 1 false (N1), 2–3 weak | 0 | 2 (fact-checker, over-strict) |
| Fact-checker held-up rate | 31/32 | 10/10 | 19/21 |
| Verdict | Needs a rewrite | Not ready | Needs a rewrite |

The fact-checker v3 strictness rule worked: it listed only 2 MISSED, both real, with none of the "checked and found supported" noise the v1 run had.
