---
name: agent-wiki-catch-up
description: Use when something may have moved on and the wiki should catch up, such as "catch up", "what changed", "is the refunds section out of date", "what are we missing", "what should we write next". Reads the sources in the register against their copies in raw/, then gaps, logs, and pages, and returns a short to-do list. Not for broken links or file shape; that is agent-wiki-lint.
---

# Agent Wiki: Catch-up

## Outcome

A to-do list of at most ten items, most valuable first, telling the user
what has changed, what to write or refresh, and why. Catch-up reads only; it
never edits. Each item the user picks is done by `agent-wiki-write`.

## Before you start

Read `../agent-wiki/references/wiki-standard.md`. Read `wiki-profile.md` for the
sections, the freshness window (default 90 days), and any outside source of
truth. If the user named one section, limit everything below to it.

## Checks

1. **Changed sources.** If the user names a source that changed (a new
   version of a document, a code change, a Confluence page), or points at a
   newer file, compare it with the earlier copy in `raw/` (for code, with
   the commit or date the source register records). List what differs and
   the pages that state each changed fact. Do not change anything here; that
   is the first item on the to-do list.
2. **Open questions.** Read `gaps.md`. Group the questions by the section
   they belong to. A section with two or more open questions is the top of
   the list.
3. **Quiet sections.** Read each section's `log.md`. Flag sections with no
   entry inside the freshness window, and sections whose index says
   "No pages yet."
4. **Dated claims.** Read each section's `index.md`, then the pages. Flag
   pages whose "As of" date is older than the freshness window, and pages
   whose description is empty or generic ("notes on X").
5. **Questions inside pages.** Collect anything under an `## Open questions`
   heading across pages.
6. **Outside truth.** If the profile names an outside source of truth, say
   in one line that pages depending on it should be checked against it,
   naming the pages. Do not fetch or diff the source; that is out of scope.

## Report

One list. Each line: section, the page to write or refresh, and the reason
in a few words. Order: changed sources, then open questions asked more than once, then sections
with no pages, then stale dated claims, then quiet sections, then vague
descriptions. Stop at ten.

Close with one line offering to start on the first item with `agent-wiki-write`.

If there is nothing to report, say the wiki is up to date and name the
newest log date so the user knows what "up to date" was measured against.

## Rules

- Never edit a page, index, log, or `gaps.md`.
- Never fill a gap from general knowledge. Catch-up finds work; it does not do
  it.
- Broken links, missing headers, and index mismatches are `agent-wiki-lint`
  findings. If you notice one, mention it in one line and move on.

## When not to use

- "Are the links broken": `agent-wiki-lint`.
- A content question: `agent-wiki-read`.
- The user already knows what to add: `agent-wiki-write`.

## Hand off to

- `agent-wiki-write` for each item the user picks.
- `agent-wiki-lint` if you noticed structural problems on the way.
