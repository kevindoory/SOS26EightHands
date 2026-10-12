# Reviewer run — Example Plumbing first-30-days draft

Run October 12, 2026, against the **final (v4)** Example Plumbing folder. Input: `03-agent/reviewer.md` (v2) + `examples/local-plumber/02-prospect-folder/` (all files) + `first-30-days-DRAFT.md`. Output below, unedited except formatting.

**How it was run:** by Claude, as two sequential passes in one working session — reviewer first, then fact-checker on the reviewer's output. Prompts: reviewer v2 and fact-checker v1 — earlier versions of the files in [`03-agent/`](../../../03-agent/). The current versions came out of this run and later reviews, so a rerun today will produce different sections. Not on a trigger or as separate automated agents; that's the [`setup.md`](../../../03-agent/setup.md) step, which wasn't tested for this example.

> **Test setup.** The draft was seeded with six mistakes before running it — the kind that get into real drafts: a wrong number, an unsupported ranking claim, a recommendation the client can't deliver, a recommendation that pre-empts an open question, a false comparison, and a target pulled from the air. The seed list is at the bottom. Read the reviewer output first and score it yourself.
>
> **A note on folder versions.** An earlier run used the first version of the folder. The folder then went through three cross-check passes. Re-running against the final folder changed two things: one seeded mistake dropped from blocker to should-fix because the folder itself got more careful; and the folder's own corrections exposed a *new* error in the draft that the first run had missed because the folder had the same error. That second thing is the point of the whole exercise.

---

## Agent 1 — Reviewer output

**Blockers**

1. **Section 4, "Add 'available 24/7 for emergencies' to your Google profile and homepage hero."**
Conflicts with `goals.md` §2: *"Either they offer after-hours and should say so everywhere, or they don't and the blog shouldn't promise it. We don't know which; we know the site currently says both."* And `preferences.md`: *"The FAQ says emergency calls are handled 'during business hours Monday through Friday, 8am to 5pm.'"* The draft tells them to promise after-hours without knowing whether they offer it. Cut, or reframe as the question the folder says to ask.

2. **"Where you are," "the fewest reviews of any established competitor."**
False against `competitors.md`, which lists Competitor I at 51 and Competitor J at 33 below Example Plumbing's 83: *"Eight businesses have more reviews; two have fewer."* Change to "ninth of eleven by review count."

3. **Section 4, "Every competitor in the results shows 24-hour availability."**
False against `competitors.md`: *"Nine of the ten other plumbers display 'Open 24 hours.' Competitor J displays 24-hour weekday hours and limited Saturday hours."* Change to "nine of ten" or "nearly every."

**Nitpicks**

4. **"5.0 across 82 reviews."** `brand.md`: *"5.0 rating, 83 Google reviews `[gbp]`. Site displays '82+'."* Use 83.

5. **"You have the best rating in the [City] plumber results."** `competitors.md`: *"Example Plumbing and Competitor I share the highest displayed rating, 5.0."* Say "tied for the best."

6. **"Your site currently ranks #3 for 'plumber [City] [State].'"** No file records an organic ranking. `competitors.md` header: *"Per-query positions aren't recoverable from this capture, so the table is sorted by review count, not rank."* Source it or cut it.

7. **Section 5, DIY how-to series.** `goals.md` §4 proposes to *"decide on purpose whether DIY content fits a call-driven business"* and `preferences.md` calls it *"worth asking whether that's intentional."* The draft decides for them. Not a contradiction — the folder leaves it open — but a recommendation that pre-empts a conversation the folder says to have. Reframe as a question.

8. **Section 6, "This is the cheapest new visibility available to you."** `goals.md` §3, explicitly: *"Not claimed: that this set is easier to rank in. Fewer businesses with fewer reviews is what we saw; demand and difficulty weren't measured."* The draft claims what the folder refused to claim. Soften to "a result set you're currently absent from."

9. **Section 3, "ten communities including [Town 9] and [Town 10]."** `history.md`: *"ten entries, including a duplicate [City] entry."* Nine distinct communities. Say "ten entries."

10. **"The structured data is mostly right."** `history.md` records a rich-result eligibility issue and a validation issue, *"different fixes,"* plus the audit's list. Undersells Section 2. Say "has one fix that matters and a few small ones."

**Claims I can't trace to a source file**

- "ranks #3 for 'plumber [City] [State]'" (see 6)
- "Target: 10 new reviews in 30 days" — no file gives a number
- "One afternoon of dev work" (Section 2) — effort estimate, no basis
- "Three per month" (Section 5) — moot if reframed

**Verdict**

Not ready. Two factual claims are false against the folder (2, 3), one recommendation contradicts the folder's explicit open question (1), and one claims what the folder explicitly declined to claim (8). Fix those four and source or cut the three numbers, and it's ready.

---

## Agent 2 — Fact-checker output

Input: the folder, the draft, and the reviewer output above.

**Reviewer's blockers**

1. 24/7 recommendation — **VERIFIED.** Quoted lines present in `goals.md` §2 and `preferences.md` as cited.
2. "Fewest reviews" — **VERIFIED.** `competitors.md` table: Competitor I 51, Competitor J 33; summary line 2 as quoted.
3. "Every competitor shows 24-hour" — **VERIFIED.** `competitors.md` summary line 1 as quoted.

**Reviewer's nitpicks**

4. 82 vs 83 — **VERIFIED.** `brand.md` proof points, as quoted.
5. "Best rating" vs tie — **VERIFIED.** `competitors.md` summary line 2.
6. "#3 ranking" unsourced — **VERIFIED.** No file records organic rank; header line as quoted.
7. DIY pre-empts open question — **VERIFIED.** Both quotes present. The reviewer's classification (nitpick, not blocker) matches the folder's own framing.
8. "Cheapest new visibility" — **VERIFIED.** `goals.md` §3 "Not claimed" line as quoted.
9. "Ten communities" — **VERIFIED.** `history.md` service-area entry as quoted.
10. "Mostly right" — **VERIFIED.** `history.md` structured-data entry: "The review markup is a rich-result eligibility issue… The date format is a validation issue. Different fixes."

**Reviewer's untraceable list** — all four confirmed absent from the folder.

**MISSED by the reviewer**

- "Competitor A, Competitor B and Competitor C each have over 1,000" — traceable (`competitors.md`: 1,183 / 1,114 / 1,070). Not an error.
- Section 6, "you're not in them yet" — traceable (`competitors.md` septic set: "did not appear in this capture's septic results").
- Section 2, "Google treats reviews you host about yourself as self-serving" — traceable (`history.md` → `[audit]`).
- Section 3, "serving every corner of [Town 6]… a template error" — the draft states the cause as fact; `brand.md` and `history.md` label it **Inference:** "possible templating or copy/paste error; cause unknown." The reviewer didn't flag that the draft upgrades an inference to a fact. **MISSED.**

*(Note added later: the first three items above are the fact-checker listing things it checked and found supported — not real misses. Only the fourth is a miss. That's the noise fact-checker v2's strictness rule is for.)*

**Tally:** 10 of 10 reviewer flags held up. One miss: the draft asserts a cause the folder marks as unknown.

---

## Scoring against the seed list

| Seeded mistake | Caught? | By |
|---|---|---|
| "82 reviews" (profile says 83) | Yes | Reviewer, nitpick 4 |
| "ranks #3" — unsupported | Yes | Reviewer, nitpick 6 |
| 24/7 recommendation — can't deliver, folder says ask | Yes | Reviewer, blocker 1 |
| DIY series — pre-empts an open question | Yes | Reviewer, nitpick 7 (was a blocker against folder v1; the folder got more careful, so this got less severe) |
| "fewest reviews of any established competitor" — false | Yes | Reviewer, blocker 2 |
| "10 new reviews in 30 days" — pulled from the air | Yes | Reviewer, untraceable list |

6 of 6. **Plus four that weren't seeded:** "every competitor shows 24-hour" (blocker 3 — written in good faith, and the folder's cross-check proved it false), "best rating" vs. the tie, "cheapest new visibility" against the folder's explicit "not claimed," and "ten communities." And the fact-checker caught one the reviewer didn't: the draft stating "template error" as a cause the folder marks unknown.

## What this says about the prompts

The reviewer's value came almost entirely from the lines in `goals.md` and `preferences.md` that say what's *not* claimed and what's *still open*. A draft that over-promises gets caught by a folder that's careful about what it knows. **The folder's quality is the reviewer's quality.** Build the folder first, and check the folder before you check the draft.

The fact-checker earned its keep on the one thing a reviewer tends to miss: a draft repeating the folder's own inference as a fact. Worth a line in `reviewer.md` v3: *"Flag any place the draft states as fact something the folder marks as Inference."*

## Check this work

Run the same three inputs — `reviewer.md`, the final folder, the draft — in another tool. Then its output through `fact-checker.md`. Score against the seed list. The four un-seeded catches are the interesting comparison: a second tool with the same folder should find the same four. If it finds a fifth, check it against the folder before you count it.

---

## Cross-checked in ChatGPT (same day, same inputs)

Same reviewer prompt, same final folder, same draft, then its own output through the fact-checker prompt. Summarized below; ChatGPT's full output isn't included.

**Seeded mistakes:** 6 of 6. **The Claude run's four un-seeded catches:** all four. **The fact-checker's catch** (template error stated as fact): ChatGPT's reviewer got it directly.

**ChatGPT caught nine things the Claude run didn't**, all real:
- "the gap in volume will widen" — a prediction with no velocity data
- Recommendations 2 and 3 don't tie to any goal in `goals.md` (the prompt asks for exactly this; the Claude run skipped it)
- The DIY series ignores that they've already published DIY
- "Pick one list" presumes we know which service-area list is right
- "Add the septic category" skips the evaluation the folder proposes
- "Doesn't touch the rating" contradicts the folder's "Not claimed"
- Agency vocabulary vs. `brand.md`'s plain voice
- "Calls. Not rankings." vs. the folder's "rankings would be a secondary check"
- Six commitments presented to a prospect the folder says we haven't talked to

**Where the runs disagreed — and why it was the prompt's fault:** ChatGPT filed 16 blockers; Claude filed 3 blockers and 7 nitpicks. Same findings, different severity. v2 of the prompt defined "blocker" as "anything that would embarrass us," and one tool read every untraceable number as embarrassing. Fair reading. **v3 of the reviewer prompt has four sections** — blockers are only what the client could check and find wrong; unsupported claims and pre-empted questions go in should-fix.

**ChatGPT's fact-checker** verified 19 of 21 reviewer flags, marked two unverified with sound reasons, and listed four misses. Two were over-strict ("founding date" when the folder gives 2007; "real phone number" when the folder confirms it). Two were fair (the service-link assumption; whether a septic GBP category exists). **v2 of the fact-checker prompt** adds a strictness rule for MISSED and a one-line section check.

**Verdicts:** Claude's "not ready"; ChatGPT's "needs a rewrite." Same call.

## Score, final

| | Claude run | ChatGPT run |
|---|---|---|
| Seeded (6) | 6 | 6 |
| Un-seeded, real | 4 (+1 fact-checker) | 13 |
| False flags | 0 | 2 (fact-checker, over-strict) |
| Verdict | Not ready | Needs a rewrite |

Two tools, one prompt, one folder, one draft. They agreed on every seeded error and every substantive un-seeded one. The thorough one found more. The prompt got two versions better. That's what the exercise is for.
