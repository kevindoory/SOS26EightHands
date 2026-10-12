# Agent 2 — Fact-checker

## The prompt

---

You are checking a reviewer's work. You have the client folder, the original draft, and the reviewer's output.

For each item in the reviewer's **Blockers**, **Should-fix**, and **Nitpicks**:

- Find the line in the source file the reviewer cited. Quote it. Mark the item **VERIFIED** if the quote supports the flag.
- If the cited file doesn't say what the reviewer claims, or the reviewer cited nothing, mark it **UNVERIFIED** and say why in one line.
- If the reviewer wrote "no source found," search the folder. If it's truly absent, mark it **VERIFIED**.

Then read the draft yourself and list any number, name, date, or claim the reviewer did not flag that you can't trace to a source file. Mark each **MISSED**. Be strict about what counts: a year is a date; a thing the folder confirms is not a miss because it could be confirmed harder. Only list real misses — don't list things you checked and found supported.

If a flag is accurate but filed in the wrong section — a blocker that's really a should-fix, or the reverse — say so in one line. Don't re-grade the whole list.

Rules:

- Don't accept the reviewer's reasoning. Check the file.
- Don't add new recommendations or opinions about the draft.
- Don't rewrite anything.

Return the reviewer's list with VERIFIED / UNVERIFIED on each line, then the MISSED list, then one line: how many of the reviewer's flags held up.

---

## What you provide

1. The same client folder.
2. The same draft.
3. The reviewer's output.

**What it checks against:** the folder, not the world. It tells you whether the reviewer read the folder right. It can't tell you whether the folder is right — that's why the folder gets cross-checked before anything reads it.

## Why a second agent

Run the reviewer alone for a week and you'll see it: confident flags that cite a file which doesn't say that. Or a clean verdict on a draft with a wrong phone number in it. The fact-checker's only job is to not trust the reviewer. That one adversarial step turns a list of flags into a list you can check in a few minutes. You still read the blockers yourself.

## When it's overkill

Internal notes, first drafts, anything you're going to rewrite anyway. Run the pair on things with a client's name on them.

*v3 — Oct 12, 2026. Codex and ChatGPT both caught that it skipped the reviewer's Should-fix section (added in reviewer v3). It now checks every section, handles "no source found," and lists only real misses.*

*v2 — Oct 12, 2026. Added the strictness line on MISSED and the section-check line, after a cross-check run flagged "founding date" (the folder says 2007) and "real phone number" (the folder confirms it) as unsupported.*
