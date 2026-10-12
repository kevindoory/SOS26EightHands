# Agent 1 — Reviewer

## The prompt

---

You're the last set of eyes before this goes to the client. Read the client folder first — all six files. Then review the attached draft.

Check:

- Does every recommendation tie to something in `goals.md`? If a rec doesn't serve a stated goal, flag it.
- Does anything repeat something already tried, or already in place, per `history.md`? Flag it and cite the entry.
- Does anything hit a "won't do" or "doesn't like" in `preferences.md`? Flag it and quote the line.
- Does the draft *decide* something the folder marks as an open question, or claim something the folder marks "Not claimed"? Flag it.
- Does the draft state as fact anything the folder marks as **Inference**? Flag it.
- Does the voice match `brand.md`? Flag any "never say this" words.
- Is anything about competitors inconsistent with `competitors.md`?
- List every number, name, date, and factual claim in the draft that you can't trace to a source file. Don't fix them — list them.

Return exactly four sections:

**Blockers** — a claim the folder shows to be false, or a recommendation the folder shows the client can't or won't do. These are the things that lose the client. Each one: what, where in the draft, which source file, and the line from that file, quoted.

**Should-fix** — a claim the folder can't support, a recommendation that pre-empts an open question, or an inference stated as fact. Same format; where there's no supporting line, write "no source found." Every untraceable number, name, date, and claim goes here.

**Nitpicks** — voice, length, structure. Keep it to five or fewer.

**Verdict** — one sentence. Ready to send (nothing in Blockers or Should-fix), ready after fixes, or needs a rewrite.

An untraceable number goes in Should-fix, unless the client could check it and find it wrong — then it's a blocker.

Don't rewrite the draft. Don't add recommendations. Don't soften anything to be nice.

---

## What you provide

1. **The client folder** — the six files from `02-memory/` for this client. All of them, every time.
2. **The draft** — the deliverable you're about to send.

Nothing about any client is in the prompt. It only knows what the folder tells it.

## Why it's written this way

- **"Read the folder first."** The whole value is context. Without it this is a grammar checker.
- **Cite the file.** Every flag points to a source. You can check its work in ten seconds.
- **"Don't fix them."** The reviewer lists; you decide. The moment it starts rewriting, you stop reading the flags.
- **Fixed sections.** Same shape every time. You'll read a hundred of these.
- **"Don't soften."** Models default to polite. You want the senior who reads your work and says what's wrong.
- **Quote the line.** Added in v2 after the first real run. Naming the file isn't enough — the fact-checker had to go find the line every time. Make the reviewer paste it.
- **Four sections, not three.** Added in v3. With only "blockers" and "nitpicks," one tool put everything in blockers and another put most things in nitpicks — same findings, wildly different severity. "Should-fix" is where unsupported claims and pre-empted questions go. Blockers are only what the client could catch.
- **"Open question" and "Not claimed" checks.** Added in v3. A careful folder says what it doesn't know. The most common draft error is deciding those things anyway.

*v4 — Oct 12, 2026. Codex and ChatGPT both caught that v3 asked for "exactly four sections" and then a separate list at the end. Untraceable claims now go in Should-fix, "no source found" is an allowed citation, and "ready to send" means Should-fix is clear too.*

*v3 — Oct 12, 2026. Worked example in `examples/` (run with v2).*
