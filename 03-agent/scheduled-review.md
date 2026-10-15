# Put the reviewer on a schedule (Claude)

An example setup, from a fresh copy of this repo to a review report. Allow time to configure access and test it; this private-repository recipe has not been validated end to end.

**Intended result (not a verified recurring deployment):** on weekday mornings, a scheduled task checks a private repository for changed drafts, runs the reviewer and fact-checker, and returns a report for human approval. Notifications and access depend on the account and configuration. A one-off run was observed; recurring operation has not been established.

**How this was tested:** On Oct 12, 2026, a one-off Claude scheduled task ran the same steps on the worked example, with nobody watching: clone, two separate agents, report by email and push. It caught all six seeded mistakes plus about nineteen real ones, with one false flag that the fact-checker caught. The full output is in [`../examples/local-plumber/03-reviewer-run/first-30-days-SCHEDULED-RUN.md`](../examples/local-plumber/03-reviewer-run/first-30-days-SCHEDULED-RUN.md). The private-repo version below is an adaptation of that mechanism and has not been tested end to end. ChatGPT has its own scheduled tasks, but this recipe wasn't tested there.

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

A cloud task cannot assume access to files on your computer. This recipe requires the scheduled-task environment to have working, authorized access to your private GitHub repository **and** permission to clone it. A GitHub connection in the chat interface does not by itself prove that shell-based cloning will work in a scheduled task. Verify access with a harmless test before uploading any client data. Connect GitHub in Claude and give it access to `review-desk` only. Don't grant it every repo you have.

If you'd rather not connect GitHub at all, stop here and use the manual version. That's a fine answer.

## 3. Create the scheduled task

In a Claude chat, paste this, with your own repo name and schedule filled in. Claude will create the scheduled task for you:

> Create a scheduled task that runs every weekday at 7:10am my time, with email and push notifications on, using the prompt below.

Then paste the task prompt:

---

You're running an unattended review of client drafts. No one is watching; don't ask questions.

1. Clone `https://github.com/[your-username]/review-desk.git` using the task environment's authorized GitHub connection. If the clone fails, report the error and stop.
2. Find candidate drafts added or changed in the last **96 hours** (to cover weekends) using `git log --since="96 hours ago" --name-only --pretty=format: -- drafts/`. Deduplicate the paths, exclude deleted files, and review only files that still exist. This is a rolling window, **not** a true since-last-successful-run checkpoint: it can re-review the same file on multiple weekdays and can miss work after a longer outage. If there are none, reply "No new drafts." and stop.
3. For each draft, the client is the folder name it sits in under `drafts/`. Read the six files in `clients/<that-name>/`. If that folder is missing or has fewer than six files, report it for that draft and skip it.
4. **Agent 1 — Reviewer.** Spawn a subagent. Give it only: the prompt section of `prompts/reviewer.md` (between the `---` lines), the six client files, and the draft, all pasted in. Tell it not to read any other files. Keep its output verbatim.
5. **Agent 2 — Fact-checker.** Spawn a second, separate subagent. Give it only: the prompt section of `prompts/fact-checker.md`, the six client files, the draft, and Agent 1's output. Tell it not to read any other files. Keep its output verbatim.
6. Reply with one report per draft: the draft's path, the reviewer's output, then the fact-checker's output, both verbatim. Put the reviewer's one-line verdict at the very top of each so it shows in the notification. Don't change any files and don't push anything.

---

Notes on the prompt:

- **Two subagents, not one chat.** The fact-checker only works if it didn't write the review. Separate subagents keep them apart.
- **"Last 96 hours."** Covers a normal Friday-to-Monday gap, but causes repeated reviews and is not a durable change tracker. For production use, store the last successful reviewed commit and process the diff since that commit; this guide does not implement that state management.
- **Read-only.** The task never edits your repo. The report comes to you; you decide what to change.

## 4. Test it once before you trust it

Use a **synthetic, non-client** draft first. Confirm the task can access the private repo, clone it, find the draft, and run both independent reviews without leaking file contents into an unintended destination. Then run the task once (ask Claude to run it now, or wait for the morning). Then compare the report to what you caught yourself. If it misses something you'd consider a blocker, fix the prompt or the client folder before you rely on the schedule.

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
