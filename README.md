# Agent Wiki

A wiki your AI agent reads, writes, and keeps current.

Every new chat, your agent has forgotten your business, and you explain the same
things again: what a number means, which table to use, what was agreed. Agent Wiki
gives that knowledge a home the agent finds on its own: a folder of plain Markdown
pages, linked like Wikipedia. The agent reads a short index first, then only the
pages it needs. It writes and maintains the pages for you. You say yes or no to
every change.

The idea is Andrej Karpathy's [LLM Wiki](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f)
(April 2026). This repo turns it into six short skill files any agent can follow.

## Install

Copy the `skills/` folder into the place your agent loads skills from.

| Agent | Where |
| --- | --- |
| Codex, GitHub Copilot and others that support [Agent Skills](https://agentskills.io) | `.agents/skills/` in your project, or `~/.agents/skills/` for all projects |
| Anything that can read files | put `skills/` in your project and say: "Read `skills/agent-wiki/SKILL.md` and follow it." |

Everything is plain Markdown. Nothing to install, no network calls, no scripts.

## Use

1. Pick one topic you keep explaining. Gather what you have on it: documents,
   notes, links, and what is only in your head.
2. Tell your agent: **"Start a wiki at `./wiki` for \<your topic\>."**
3. Then, for each source: **"Add this to the wiki."** Read what it proposes. Say yes or no.
4. From then on, ask it questions. It answers from the pages and tells you which ones it used.

You never pick a skill. The `agent-wiki` skill reads what you asked and hands the
work to the right one.

| You say | What happens |
| --- | --- |
| "Start a wiki at `./wiki` for refunds" | Creates the folder and the starter files, then stops. |
| "What's our refund window for annual plans?" | Reads the index, then the right pages, and answers with the pages it used. If no page covers it, it says so and notes the question in `gaps.md`. |
| "Add this document" or "That's wrong, it should be…" | Finds the page that owns the topic, says what it will change, waits for your yes, then writes it and keeps the indexes and logs in step. A copy of the document, or a note of what you said, goes in `raw/`. |
| "This page changed, here's the new version" | Compares it with the copy in `raw/`, shows the old line, the new line and the pages that state it, and waits for your yes. |
| "Check the wiki" | Reports broken links, missing index lines and missing headers, and offers to fix them. |
| "What should we write next?" | Reads the open questions and the logs and gives you a short to-do list. |

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
  raw/                  your documents, and notes of what you said, kept
                        exactly as they arrived
```

Each page is ordinary Markdown with a short header (type, title, one-line
description, tags) and a "Related" list at the bottom. The layout follows Google's
[Open Knowledge Format](https://github.com/GoogleCloudPlatform/open-knowledge-format),
so other tools that read that format can read your wiki too.

[`example/`](example/) is a small made-up wiki for a subscription business: a
finance page on monthly recurring revenue, linked to the billing table it is built from.

## The skills

```text
skills/
  agent-wiki/          start here: picks the right skill
    references/        the wiki standard and the profile template
  agent-wiki-init/     start a new wiki
  agent-wiki-read/     answer from the wiki, with sources
  agent-wiki-write/    add or correct knowledge, after your yes
  agent-wiki-lint/     check links, indexes and headers
  agent-wiki-health/   find what is missing or stale
```

Each one is a short Markdown file you can read in a minute. Change them to fit
how your team works.

## Privacy

The wiki is a folder you own. The skills read and write files in that folder and
nowhere else.

## License

MIT. See [LICENSE](LICENSE).
