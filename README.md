# Agent Wiki

A wiki your AI agent reads, writes, and keeps current.

Your agent forgets your business every time you open a new chat. You end up
explaining the same things again: what a number really means, which table to
use, what was agreed. Agent Wiki gives that knowledge a home your agent can
find on its own: a folder of plain Markdown pages, linked like Wikipedia. The
agent reads a small index first, then only the pages it needs. It writes and
maintains the pages for you, and you approve every change.

The idea comes from Andrej Karpathy's
[LLM Wiki](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f)
(April 2026). Agent Wiki turns it into a few short skill files any agent can
follow.

## Start in three steps

1. **Get the skills** (pick one way below).
2. **Pick one topic** you keep explaining, and gather what you have on it:
   documents, notes, links, and what is only in your head.
3. **Tell your agent:** "Start a wiki at `./wiki` for <your topic>", then
   "Add this to the wiki" for each source. Read what it proposes and say yes
   or no.

## Get the skills

**Copy the folder.** Copy the six folders in `skills/` into the folder your
agent loads skills from. Codex, GitHub Copilot and other agents that support
[Agent Skills](https://agentskills.io) read `.agents/skills/` in your project,
or `~/.agents/skills/` for every project.

**No skills support?** Put the `skills/` folder anywhere in your project and
tell your agent: "Read `skills/agent-wiki/SKILL.md` and follow it." Everything
is plain Markdown, so any agent that can read files can use it.

**Install as a plugin.** GitHub Copilot CLI:

```bash
copilot plugin marketplace add mukulmalik2/agent-wiki
copilot plugin install agent-wiki@agent-wiki
```

## What you can say

You never pick a skill. The `agent-wiki` skill reads what you asked and hands
the work to the right one.

| You say | Skill | What happens |
| --- | --- | --- |
| "Start a wiki at `./wiki` for refunds" | Init | Creates the folder and starter files, then stops. |
| "What's our refund window for annual plans?" | Read | Reads the index, then the right pages, and answers with the pages it used. If no page covers it, it says so and notes the question in `gaps.md`. |
| "Add this document" or "that's wrong, it should be…" | Write | Finds the page that owns the topic, tells you what it will change, waits for your yes, then writes it and keeps the indexes and logs in step. |
| "Check the wiki" | Lint | Reports broken links, missing index lines, and missing headers, and offers to fix them. |
| "What should we write next?" | Health | Reads the open questions and logs and gives you a short to-do list. |

The skills hand work to each other: a question the wiki cannot answer becomes
a gap, a gap becomes something to write, and a large write is followed by a
check.

## What it looks like on disk

```text
wiki/
  wiki-profile.md       what this wiki covers, its sections, what to trust
  index.md              front page: the sections, one line each
  log.md                what changed, and when
  gaps.md               questions the wiki could not answer yet
  finance/
    index.md            the pages in this section, one line each
    revenue.md          one page per topic
    log.md
    source-register.md  where the knowledge came from
  data-model/
    index.md
    billing-table.md
    log.md
    source-register.md
  raw/                  original documents, kept exactly as they arrived
```

See [`example/acme-wiki`](example/acme-wiki) for a small, made-up wiki: a
finance page on monthly recurring revenue that links to the billing table it
is built from.

Each page is ordinary Markdown with a short header (type, title, a one-line
description, tags) and a "Related" list at the bottom. The layout follows
Google's [Open Knowledge Format](https://github.com/GoogleCloudPlatform/open-knowledge-format),
so other tools that understand that format can read the same wiki. Put it
wherever your agent works: next to your code, in a shared folder, anywhere.

## Privacy

The wiki is a folder you own. The skills read and write files in that folder
and nowhere else. They make no network calls, run no scripts, and keep no
record outside the wiki.

## What's inside

```text
plugin.json            Agent Plugins 1.0 manifest
skills/
  agent-wiki/          start here: picks the right skill
    references/        the wiki standard and the profile template
  agent-wiki-init/     start a new wiki
  agent-wiki-read/     answer from the wiki, with sources
  agent-wiki-write/    add or correct knowledge, after your yes
  agent-wiki-lint/     check links, indexes, and headers
  agent-wiki-health/   find what is missing or stale
example/acme-wiki/     a small example wiki
```

Each skill is a short Markdown file you can read in a minute. Change them to
fit how your team works.

## License

MIT. See [LICENSE](LICENSE).
