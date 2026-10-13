---
name: agent-wiki-health
description: Use when the user asks how the wiki is doing, what to write next, where it is thin, or whether an area is out of date, such as "how healthy is the wiki", "what are we missing", "is the refunds section stale". Reads gaps, logs, and pages and returns a short to-do list. Not for broken links or file shape; that is agent-wiki-lint.
---

# Agent Wiki: Health

## Outcome

A to-do list of at most ten items, most valuable first, telling the user
what to write or refresh and why. Health reads only; it never edits.

## Before you start

Read `../agent-wiki/references/wiki-standard.md`. Read `wiki-profile.md` for the
sections, the freshness window (default 90 days), and any outside source of
truth. If the user named one section, limit everything below to it.

## Checks

1. **Open questions.** Read `gaps.md`. Group the questions by the section
   they belong to. A section with two or more open questions is the top of
   the list.
2. **Quiet sections.** Read each section's `log.md`. Flag sections with no
   entry inside the freshness window, and sections whose index says
   "No pages yet."
3. **Dated claims.** Read each section's `index.md`, then the pages. Flag
   pages whose "As of" date is older than the freshness window, and pages
   whose description is empty or generic ("notes on X").
4. **Questions inside pages.** Collect anything under an `## Open questions`
   heading across pages.
5. **Outside truth.** If the profile names an outside source of truth, say
   in one line that pages depending on it should be checked against it,
   naming the pages. Do not fetch or diff the source; that is out of scope.

## Report

One list. Each line: section, the page to write or refresh, and the reason
in a few words. Order: open questions asked more than once, then sections
with no pages, then stale dated claims, then quiet sections, then vague
descriptions. Stop at ten.

Close with one line offering to start on the first item with `agent-wiki-write`.

If there is nothing to report, say the wiki looks healthy and name the
newest log date so the user knows what "healthy" was measured against.

## Rules

- Never edit a page, index, log, or `gaps.md`.
- Never fill a gap from general knowledge. Health finds work; it does not do
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
