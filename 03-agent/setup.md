# Running the agents on a trigger

Checked October 2026. Feature names change — if a button here has moved, the shape hasn't. You need three things: the prompts, the client folder, and something that kicks the job off.

**What was tested:** the manual version, in Claude and ChatGPT. The scheduled and always-on versions below are the shape of the setup, from each platform's release notes — not a tested recipe. Plans and permissions vary. If you automate, do one trial run and check it before you trust the schedule.

## The manual version (start here)

1. New chat. Paste `reviewer.md`'s prompt. Attach or point at the client folder. Attach the draft. Run.
2. New chat. Paste `fact-checker.md`'s prompt. Attach the folder, the draft, and the reviewer's output. Run.

Two chats, about five minutes once the folder exists and the draft is done. Do this three times before automating anything.

## Claude

**One-off, with memory:** Put the client folder in a Project. Save the reviewer prompt as the project's instructions (or as a Skill). Every new chat in that project is a reviewer; you just paste the draft. Do the same in a second project for the fact-checker, or keep both prompts as Skills in one project.

**On a schedule:** Full walkthrough, with a ready-to-paste task prompt: [`scheduled-review.md`](scheduled-review.md). In short: scheduled tasks run in the cloud, even when your machine is off — which also means they can't see files on a computer that's off. Point the task at files it can reach (a Project's files, or a connected drive), not a folder on your laptop. Example instruction: "Review anything new in [your drafts folder] using the reviewer instructions, then fact-check it, and send me the result." `[your drafts folder]` is a placeholder for wherever your drafts live.

**Chained (advanced):** If you're comfortable at a terminal, Claude Code subagents fit this well — one agent for the reviewer, one for the fact-checker. Give the second one the folder, the original draft, and the reviewer's output, same as the manual version. Needs some terminal setup; Claude Code's docs cover subagents.

## ChatGPT

**One-off, with memory:** Put the client folder in a Project with project-only memory on. Save the reviewer prompt as the project's instructions. Paste the draft. Same pattern for the fact-checker in a second project.

**On a schedule:** Scheduled tasks. Set one for nightly review. The release notes describe webhooks that can fire it when a file lands in a connected Drive/Box/Dropbox/SharePoint folder — check that your plan and storage connection support it before relying on it.

**Always-on:** "Dots" are ChatGPT's always-on agents. Give one the reviewer instructions and the folder and it watches for drafts. New as of late September 2026 — expect it to change.

**Don't** build these as Custom GPTs. They're being retired.

## Anything else

The prompts are plain text and the folder is plain markdown. Any tool that can read files and run a prompt on a schedule can run this. Gemini has rough equivalents (Gems, scheduled actions). Local models through something like Ollama work for the reviewer if the folder's small.

*v2 — Oct 12, 2026. After Codex and ChatGPT reviews: says what was tested, fixes the scheduled-task-vs-local-files contradiction, gives the chained fact-checker all three inputs, marks the drafts path as a placeholder.*
