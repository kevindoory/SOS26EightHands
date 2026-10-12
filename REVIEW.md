# Checking this repo with another AI

Everything here was drafted by one AI and cross-checked in another. You should do the same before you trust any of it. Paste this prompt plus the file you're checking into ChatGPT, Codex, Gemini, whatever you don't normally use. (The cross-checks behind the examples used prompts written for each piece; this is the general version.)

---

You're reviewing a file from a public repo meant to help solo and small-team SEOs build their own AI tools. Read it and tell me:

1. Every factual claim that isn't sourced or can't be checked from what's in the file.
2. Every instruction that's ambiguous — where two reasonable people would do different things.
3. Every place a solo SEO with no dev background would get stuck.
4. Anything that reads as a product or service pitch.
5. Anything that would be wrong or stale if a named tool changed its features next month.

Format: a table — line or section · issue · which of the five · suggested fix. Then one sentence: should this ship as-is, with fixes, or not at all. Don't summarize the file back to me.

---

## What came out of doing this

- The schema audit prompt went from v1 to v2 because a cross-check showed it couldn't tell a confirmed error from something it couldn't see in the input. (`01-prompt/schema-audit.md`)
- The reviewer prompt went to v2 because the fact-checker kept having to find the lines the reviewer only named, to v3 because two tools filed the same findings at wildly different severity, and to v4 because a repo review caught it asking for "exactly four sections" plus a fifth list. (`03-agent/reviewer.md`)
- The fact-checker went to v2 after it flagged things the folder plainly confirmed, and to v3 when a repo review noticed it wasn't checking the reviewer's Should-fix section at all. (`03-agent/fact-checker.md`)
- The first cross-check produced three false findings — because the input had been abbreviated. The lesson went into the prompt. (`examples/`)

The point isn't that the second AI is smarter. It's that it didn't write the first draft, so it has nothing to defend. It can still be wrong — sometimes the same way. Check what it flags before you act on it.

*v2 — Oct 12, 2026. Updated the version history after the Codex and ChatGPT repo reviews; added the line about checking what the second AI flags.*
