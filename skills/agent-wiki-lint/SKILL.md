---
name: agent-wiki-lint
description: Use for a mechanical check of the wiki's files, such as "check the wiki", "are the links ok", "anything broken", or after a large write. Finds broken links, orphan pages, missing headers, and indexes out of step with pages. Not for judging whether content is stale or missing; that is agent-wiki-catch-up.
---

# Agent Wiki: Lint

## Outcome

A short list of what is structurally wrong, with file paths, and an offer to
fix it. Lint reports first and edits only when told to.

## Before you start

Read `../agent-wiki/references/wiki-standard.md` for the exact shapes. Read
`wiki-profile.md` for folders to leave alone. Skip `raw/` and any folder the
profile lists, always.

## Checks

Use your own file tools. List every `.md` file in the wiki, then check:

1. **Header.** Every page except `index.md` files opens with a front
   matter block containing a non-empty `type`, plus `title` and
   `description`. Section indexes carry no front matter. The root index
   carries at most `okf_version`.
2. **Links.** Every Markdown link to a `.md` file resolves to a file that
   exists inside the wiki. Links into `raw/` from a page are allowed only
   from a source register.
3. **Indexes.** Every content page in a section has a line in that
   section's `index.md`. Every index line points at an existing file and
   follows `* [Title](file.md) - description`. Every section folder has a
   line in the root index. Bookkeeping files (`log.md`,
   `source-register.md`, `gaps.md`, `wiki-profile.md`) and index files are
   never listed and are not checked here.
4. **Orphans.** Every content page is linked from at least one index or one
   other page. Bookkeeping files and indexes are exempt.
5. **Bookkeeping files.** Every section has `index.md`, `log.md`, and
   `source-register.md`. The root has `wiki-profile.md`, `index.md`,
   `log.md`, and `gaps.md`.
## Report

Group findings by check, one line each: `check - path - what is wrong`. If
nothing is wrong, say "Nothing broken." Then offer, in one line, to fix
what can be fixed mechanically: missing index lines, wrong index shapes,
missing bookkeeping files, dead links whose target moved.

On yes, apply fixes with `agent-wiki-write` bookkeeping rules and add one log
entry per section touched. Never rewrite page content to fix a link; report
that and let the user decide.

## Rules

- Never edit without a yes.
- Never touch `raw/`.
- Lint does not read for meaning. Thin, stale, or vague content is a
  `agent-wiki-catch-up` finding, not a lint finding.

## When not to use

- "What should we write next" or "is X out of date": `agent-wiki-catch-up`.
- A question about content: `agent-wiki-read`.

## Hand off to

- `agent-wiki-catch-up` when structure is fine but the user's real worry is
  content.
