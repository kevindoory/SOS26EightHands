# Rung 2 — The client folder

A workflow with memory. One folder per client, a handful of plain text files, and a habit of pointing the AI at the folder before it does anything.

This is how one person holds ten clients in their head without holding ten clients in their head.

## The shape

```
clients/
└── <client-name>/
    ├── brand.md          voice, do-not-say list, how they talk about themselves
    ├── goals.md          what they're paying for, in their words
    ├── history.md        what we tried, what happened
    ├── preferences.md    what they rejected and why
    ├── competitors.md    who they lose to, and where
    └── log.md            one line per week
```

Six files. Plain markdown. No tool required to write them. Any AI you can attach files to can read them.

## What's in this folder

- `_template/` — the six files, blank, with prompts for what goes in each
- `examples/` — a filled-in *prospect* file for a real local business, built entirely from public sources. Every line is tagged with where it came from. See its README for how a prospect file differs from a client file.

## Setting it up

1. Download the repo (green **Code** button → **Download ZIP**) and unzip it. Copy the `_template` folder into `clients`, and rename the copy to your client's name. (`clients/` is yours; the worked example lives in `examples/`, so you never have to touch it.)
2. Open each file in any text editor and fill it in. Spend an hour writing down what's in your head. The `preferences.md` file — what they've rejected — is the one that pays off most. AI can help you gather and draft (the worked example was built that way), but you check every line, and the client's own words beat anything it finds.
3. Every week, add one line to `log.md`. That's the maintenance.

## Pointing the AI at it

The habit is one line in front of every task:

> Read the client files I've attached (brand, goals, history, preferences, competitors, log) before you do anything. Tell me if any are missing. Then: [the task].

If your tool can see the folder directly (the Claude desktop app with a connected folder, or a connected drive), name the folder instead of attaching the files.

**Claude:** Put the client folder in a Project and upload the six files to it, or — on the desktop app — point it at the folder on your machine directly. Memory keeps context across chats in the project.

**ChatGPT:** Put the six files in a Project with project-only memory on, or keep the folder in Drive/Box/Dropbox/SharePoint and connect it through Library.

**Obsidian / local files:** The folder lives on disk; the AI reads it through a desktop app. Same six files.

## Before and after

Same request, with and without the folder:

**Without:** "Draft three blog topics for [client]."
→ "1. 24/7 emergency plumbing in [city]. 2. How to unclog a drain yourself. 3. Signs you need a new water heater."
Generic. The first promises hours the client may not keep. The second is DIY content the client may not want. The third could be on any plumber's blog.

**With:** "Read the client files, then draft three blog topics."
→ "Skipping anything 24/7 — the folder says hours are Mon–Fri 8–5. Skipping DIY until we know whether they want it; `preferences.md` lists it as an open question. Given the services the folder flags as possible differentiators: 1. What a septic inspection in [county] actually checks, and what it costs. 2. Hydro excavation vs. digging: when it's worth it. 3. Live water tapping — what it is and when you need it…"
Closer to where someone who'd read the file would start. The second answer isn't smarter. It read the folder. (It still needs checking — the folder only knows what's in it.)

## Rule

Every rung above this one reads the folder too. The reviewer agent in `03-agent/` gets most of its value from knowing what "right" looks like for this client.

*v2 — Oct 12, 2026. After Codex and ChatGPT reviews: step-by-step setup from the ZIP, an attach-the-files version of the read-the-folder line, and the before/after no longer decides the DIY question the folder leaves open.*
