# Where each rung lives

Checked the week of October 12, 2026. If a cell is out of date by the time you read this, that's the point of the ground rule: learn the shape, not the button.

| Rung | Claude | ChatGPT |
|---|---|---|
| **1 · Prompt** | A saved prompt in a Project's instructions, or packaged as a Skill | A saved prompt in a Project's instructions. Custom GPTs are being retired (announced Sept 2026, migrating to "plugins") — don't build on them |
| **2 · Memory** | Projects with memory (shared across chat and Cowork); the desktop app reads a local folder directly | Projects with project-only memory; Library pulls from Drive, Box, Dropbox, SharePoint |
| **3 · Agent** | Scheduled tasks that run in the cloud with your machine off (so they can't see files on that machine — point them at a Project or a connected drive); Claude Code subagents for reviewer chains | Scheduled tasks + webhooks; "Dots" always-on agents (launched Sept 29, 2026) |

**Tested for this repo:** rungs 1 and 2, and the rung 3 prompts run by hand, in both. The rung 3 automation features are listed from each platform's release notes, not tested end to end here. Plans and permissions vary — check yours.

## Elsewhere

- **Gemini:** Gems for rung 1 and 2; scheduled actions for rung 3. Not tested as thoroughly.
- **Local models:** The prompts are plain text. Ollama plus a folder of markdown handles rung 1 and most of rung 2. Rung 3 needs something to run the schedule — a cron job is fine.

## Sources

- [ChatGPT release notes](https://help.openai.com/en/articles/6825453-chatgpt-release-notes)
- [Claude release notes](https://support.claude.com/en/articles/12138966-release-notes)

*v2 — Oct 12, 2026. Added what was and wasn't tested, and the cloud-vs-local-files caveat on Claude scheduled tasks.*
