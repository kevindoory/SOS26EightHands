# Eight Hands

Prompts, a client-folder template, and two reviewer agents for small SEO teams. Companion repo to the talk "Using AI Associates to Expand Capabilities of Smaller SEO Teams," given at State of Search 2026 (Dallas, October 2026).

This is a jumping-off point, not a product. It's what worked for one SEO as of October 2026, with the runs and cross-checks included so you can see how it was tested. The tools will change. The approach is meant to outlast them. Take it and make it yours — fork the repo, or just download the ZIP from the green Code button.

## The idea

Don't start with the AI. Start with a deliverable you make every month. List every hand it takes, start to send. Decide which hands need you. Everything else is a candidate — not automatically a fit — for an AI hand.

**A hand** is one discrete task with a clear input and a clear output. "Pull last month's GSC numbers into the report template" is a hand. "Do the monthly report" is a deliverable made of eight of them.

**A hand needs you** when it's a business decision, a recommendation the client will act on, a client conversation, or something that'd cost you the account if it went wrong. Be strict about this list; most people pad it.

An AI hand comes in three shapes, and each one here uses the one below it:

| Rung | Shape | What it is | Build time* |
|---|---|---|---|
| 1 | A prompt | Fixed instructions for one task, with a fixed output format. The output still gets checked. | An afternoon |
| 2 | A workflow with memory | A prompt that reads a folder of client files you wrote before it starts. "Memory" here means those files — not a platform's memory feature. You have to give the AI the folder. | A weekend |
| 3 | An agent | A prompt plus a folder plus a trigger — something that starts it without you, like a nightly schedule or a file landing in a folder. It runs, then hands you the result. | A week of evenings |

*Illustrative. Assumes you already use an AI tool daily and can make a folder of text files. Not a promise.

## What's here

```
eight-hands/
├── 01-prompt/           Rung 1 — the schema audit prompt (generic; you paste your page)
├── 02-memory/           Rung 2 — the client folder template (generic; you fill it in)
├── 03-agent/            Rung 3 — reviewer + fact-checker instructions (generic; you supply the folder and draft)
├── monday-morning/      Five prompts to map your own deliverable
├── platforms.md         Where each rung lives in Claude and ChatGPT, dated
├── REVIEW.md            A prompt for checking any file here with a second AI
├── examples/           All three rungs run on one real business, with cross-checks. Worked example, not template.
└── LICENSE              MIT
```

Two layers. The top-level folders are generic — every prompt says what you paste in. `examples/` is one real business run through all three, so you can see what comes out. Use the first; read the second.

The agents in `03-agent/` are instructions — prompts you paste, or save as a scheduled task. They aren't code you run. `setup.md` in that folder lists the options for putting them on a trigger; `scheduled-review.md` walks through one end to end.

**What was tested:** the prompts were run manually in Claude and ChatGPT on the worked example. A separate one-off, unattended Claude scheduled-task run on the worked example is documented in [`03-agent/scheduled-review.md`](03-agent/scheduled-review.md). That single run does not validate the full private-repo walkthrough, recurring operation, or ChatGPT automation. Other tools and accounts will need their own tests.

## Start here

Open [`monday-morning/five-prompts.md`](monday-morning/five-prompts.md). Paste prompt 1 into Claude or ChatGPT and describe a deliverable you produce every month — what it is, what goes in, the steps, where you make decisions, what comes out. Work through the five. You'll end with a draft of a rung 1 prompt.

Then test it: run it on two of those deliverables you already did by hand, and compare. Don't use it on client work until it agrees with you — or you've figured out why it doesn't.

## About the example

`examples/` runs all three rungs on one real local business, using only public sources: its site, its Google Business Profile, and local search results, all captured October 12, 2026. It's independent research for teaching — the business didn't commission it and isn't a client. Sourced observations carry a tag; inferences are labeled; the proposals are in one file and say so. Raw captures (full page text, search results) aren't included.

To make your own: copy `02-memory/_template/` to `02-memory/clients/<your-client>/` and fill it in. Nothing in `examples/` needs editing.

## Checking this repo

Everything here was drafted by one AI and checked in another, and the prompts changed because of it (version notes are in each prompt). [`REVIEW.md`](REVIEW.md) has the prompt to do the same to any file here. Use it.

## Words used here

- **JSON-LD** — the block of structured data (schema) in a page's source, inside `<script type="application/ld+json">`.
- **Markdown (`.md`)** — plain text files with light formatting. Open them in any text editor (Notepad, TextEdit) or in Obsidian.
- **Fork** — GitHub's copy-this-repo-to-my-account button. Downloading the ZIP does the same job without an account.
- **Trigger** — whatever starts an agent without you: a schedule, or a file landing in a folder.
- **Webhook / cron** — two kinds of trigger. A webhook fires when something happens somewhere else; cron is a schedule on a computer.
- **Subagent** — in Claude Code, a separate agent with its own instructions that another agent hands work to.
- **GBP** — Google Business Profile. **SERP** — the search results page. **CTA** — call to action ("Get a free estimate").

## License

MIT. See [LICENSE](LICENSE) — short version: use it, change it, ship it, keep the notice.

*v3 — Oct 12, 2026. After Codex and ChatGPT reviewed the repo: says exactly what was tested (the prompts, by hand) and what wasn't (the automated setups), adds a glossary, calls the example a worked example instead of proof.*
