# Put the reviewer on a schedule (Claude)

The full setup, from a fresh copy of this repo to a review report showing up without you. About an hour the first time.

**What you end up with:** every weekday morning, Claude checks a private folder of drafts. Anything new or changed since yesterday gets reviewed by Agent 1, fact-checked by Agent 2, and the report lands in your email and phone. You read it and decide.

**How this was tested:** On Oct 12, 2026, a one-off Claude scheduled task ran the same steps on the worked example, with nobody watching: clone, two separate agents, report by email and push. It caught all six seeded mistakes plus about nineteen real ones, with one false flag that the fact-checker caught. The full output is in [`examples/local-plumber/03-reviewer-run/first-30-days-SCHEDULED-RUN.md`](../examples/local-plumber/03-reviewer-run/first-30-days-SCHEDULED-RUN.md). The private-repo version below is the same mechanism pointed at your own files. ChatGPT has its own scheduled tasks, but this recipe wasn't tested there.

## Before you start

- Run the two prompts by hand at least three times first ([`README.md`](README.md), "Start here"). If the manual version doesn't catch anything useful, a schedule won't help.
- You need a GitHub account (free) and a Claude plan with scheduled tasks.
- **Client files never go in a public repo.** Not this one, not a fork of it. Everything below goes in a separate **private** repo.

## 1. Make a private repo for your review desk

On GitHub: **New repository** → name it something like `review-desk` → set it to **Private** → create.

You can do everything below in the browser with **Add file → Upload files**. No git needed.

Make this layout:

```
review-desk/                      (private)
├── prompts/
│   ├── reviewer.md               copied from this repo's 03-agent/
│   └── fact-checker.md           copied from this repo's 03-agent/
├── clients/
│   └── <client-name>/            the six files from 02-memory/_template/, filled in
│       ├── brand.md
│       ├── goals.md
│       ├── history.md
│       ├── preferences.md
│       ├── competitors.md
│       └── log.md
└── drafts/
    └── <client-name>/            drafts go here as .md or .txt files
```

Why copy the prompts instead of pointing at this repo: so they don't change under you. When you improve a prompt, you change your copy, on purpose.

**Folder names matter.** The client folder in `clients/` and the one in `drafts/` must have the same name. That's how the agent knows which folder goes with which draft.

## 2. Let Claude read the private repo

A scheduled task runs in the cloud, so it can't see files on your computer. It can read a GitHub repo you've connected to Claude. Connect GitHub in Claude and give it access to `review-desk` only. Don't grant it every repo you have.

If you'd rather not connect GitHub at all, stop here and use the manual version. That's a fine answer.

## 3. Create the scheduled task

In a Claude chat, paste this, with your own repo name and schedule filled in. Claude will create the scheduled task for you:

> Create a scheduled task that runs every weekday at 7:10am my time, with email and push notifications on, using the prompt below.

Then paste the task prompt:

---

You're running an unattended review of client drafts. No one is watching; don't ask questions.

1. Clone `github.com/[your-username]/review-desk`.
2. Find drafts to review: every file under `drafts/` added or changed in the last 26 hours, by git history (`git log --since="26 hours ago" --name-only --pretty=format: -- drafts/`). If there are none, reply "No new drafts." and stop.
3. For each draft, the client is the folder name it sits in under `drafts/`. Read the six files in `clients/<that-name>/`. If that folder is missing or has fewer than six files, report it for that draft and skip it.
4. **Agent 1 — Reviewer.** Spawn a subagent. Give it only: the prompt section of `prompts/reviewer.md` (between the `---` lines), the six client files, and the draft, all pasted in. Tell it not to read any other files. Keep its output verbatim.
5. **Agent 2 — Fact-checker.** Spawn a second, separate subagent. Give it only: the prompt section of `prompts/fact-checker.md`, the six client files, the draft, and Agent 1's output. Tell it not to read any other files. Keep its output verbatim.
6. Reply with one report per draft: the draft's path, the reviewer's output, then the fact-checker's output, both verbatim. Put the reviewer's one-line verdict at the very top of each so it shows in the notification. Don't change any files and don't push anything.

---

Notes on the prompt:

- **Two subagents, not one chat.** The fact-checker only works if it didn't write the review. Separate subagents keep them apart.
- **"Last 26 hours."** A little overlap so a draft saved late the night before isn't missed. If you re-save a draft, it gets reviewed again. That's usually what you want.
- **Read-only.** The task never edits your repo. The report comes to you; you decide what to change.

## 4. Test it once before you trust it

Upload a draft you've already reviewed by hand. Run the task once (ask Claude to run it now, or wait for the morning). Then compare the report to what you caught yourself. If it misses something you'd consider a blocker, fix the prompt or the client folder before you rely on the schedule.

## 5. Daily use

- Drop the draft in `drafts/<client>/` when it's done.
- Read the report in the morning. Fix what's real.
- When the client tells you something new, update their folder. **The folder's quality is the reviewer's quality.**

## What can go wrong

- **"No new drafts" when you just added one.** Check that it went into `drafts/<client>/` in the private repo, not on your laptop.
- **The agent says a client folder is missing.** The folder names in `drafts/` and `clients/` don't match.
- **Every flag says "UNVERIFIED."** Usually the client folder is thin. Fill it in; the reviewer can only check against what's written down.
- **The schedule stops working after a platform update.** Feature names move. The shape doesn't: a prompt, a folder, a trigger. See [`setup.md`](setup.md).

*v1 — Oct 12, 2026. Written after a one-off scheduled test run of both agents on the worked example.*
