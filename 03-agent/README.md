# Rung 3 — The reviewer agents

An agent is a prompt plus a folder plus a trigger. This one is the hand solo SEOs never had: a second set of eyes on the deliverable before it goes to the client.

It's two agents, not one — because the first thing an AI reviewer does is confidently approve its own mistakes. The second one doesn't take its word for it.

## How it works

```
your draft  →  Agent 1: Reviewer  →  Agent 2: Fact-checker  →  blockers / should-fix / nitpicks / verdict  →  you decide
                (reads the client       (traces every flagged
                 folder, then the        claim to a source file
                 draft)                  or marks it UNVERIFIED)
```

Both agents read the client folder from `02-memory/`. That's how they know what "right" looks like for this client. Without the folder, a reviewer can mostly only check the writing.

The fact-checker checks against the folder, not the world. If the folder's wrong, it'll verify the wrong thing. That's why the folder gets checked first.

## Start here: run it by hand

Before you automate anything, run both prompts by hand on your next deliverable:

1. New chat: the reviewer prompt + the six client files + your draft.
2. New chat: the fact-checker prompt + the six client files + your draft + the reviewer's output.

Do that three times. If it catches something you'd have missed, it's earned a trigger.

## What's in this folder

- `reviewer.md` — Agent 1's instructions
- `fact-checker.md` — Agent 2's instructions
- `setup.md` — the options for running them on a trigger in Claude and ChatGPT
- `scheduled-review.md` — the full setup for one of those options: a private repo of client files and drafts, and a Claude scheduled task that reviews anything new every morning
- The worked example — a run on a first-30-days plan for a real local business with six seeded mistakes, the reviewer's output, the fact-checker's output, the score, a comparison against the same run in ChatGPT, and a later run of the current prompts on a schedule — is in [`../examples/local-plumber/03-reviewer-run/`](../examples/local-plumber/03-reviewer-run/). Read it after your first manual run.

## Notice the ladder

Rung 3 is rung 1 (a fixed prompt with a fixed output) plus rung 2 (it reads the folder) plus a trigger. You don't need to be a developer. You need a prompt, a folder, and a schedule.

*v2 — Oct 12, 2026. After Codex and ChatGPT reviews: manual steps first, with all three fact-checker inputs; four output sections, matching reviewer.md; the fact-checker's limit stated.*
