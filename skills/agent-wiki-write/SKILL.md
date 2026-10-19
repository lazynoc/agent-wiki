---
name: agent-wiki-write
description: Use when confirmed knowledge should go into the wiki or a page should be corrected, such as "add this to the wiki", "ingest this document", "update the page on X", "this source changed", or "that's wrong, it should be". Reads first, proposes, then writes. Not for answering questions from existing pages or for checking wiki health.
---

# Agent Wiki: Write

## Outcome

Confirmed knowledge turned into a page a future asker can find, with the
indexes, logs, and source register kept in step. One strong page beats a thin
summary plus an unread document.

## Before you start

Read `../agent-wiki/references/wiki-standard.md` for page, index, log, and register
shapes. Then read first, using the navigation steps of `agent-wiki-read` (profile, root
index, section index, pages) without its gaps step: find every existing page
that may already own the concept. If the user gave a document, read all of it.

## Steps

1. **Propose before editing.** In one short message say which page you will
   update or create, in which section, and what will change. If a page
   already owns the concept, propose updating it, not a new page. Wait for
   yes, even when the user's message was itself an instruction; the
   proposal is what lets them catch a wrong page or section before it is
   written. If the source is a newer version of one in the source register,
   first compare it with the earlier copy in `raw/` (for code, with the
   commit or date the register records) and propose only what changed: the
   old line, the new line, and each page that states it. If you cannot tell
   what changed or which version is newer, ask.
2. **Write the page.** Start with the standard header: `type`, `title`, a
   description written in the words a future asker would use, and tags
   covering aliases and acronyms. Use simple, specific English. Use headings
   that fit the knowledge, for example `Decision`, `Current status`,
   `Rationale`, `Dependencies`, `Open questions`, only when those things
   exist. Mark unknowns as unknown. Qualify time-sensitive claims with
   "As of <date or version>". End with `## Related`, listing only real
   relationships to existing pages with a few words on why each helps. If
   none exist yet, write "None yet." under the heading.
3. **Check the page against the source.** Every material point in the source
   is either on the page, linked to another page that holds it, or noted as
   a gap. If something useful lives only in the source, the write is not
   finished.
4. **Bookkeeping, always, in this order:**
   - Section `index.md`: add, rename, or remove the page's line in the
     `* [Title](file.md) - description` shape.
   - Section `log.md`: one entry under today's date naming the page, what
     changed, and the source and version it came from.
   - Section `source-register.md`: one row if a source was used.
   - Root `index.md` and the `## Sections` list in `wiki-profile.md`: one
     line each if you created a new section (and create that section's
     index, log, and register as `agent-wiki-init` would).
   - `gaps.md`: remove any line the page now answers.
5. **Keep the original.** `raw/` holds what the wiki was built from,
   exactly as it arrived:
   - A document (an exported page, a PDF, meeting notes): copy it unchanged
     into `raw/`. A newer version goes in beside the old one, with its date
     or version in the file name.
   - Something the user told you that no file holds: save their words
     unchanged as a dated note, for example
     `raw/2026-10-15-note-store-eligibility.md`.
   - Code, or anything else that keeps its own history: read it where it
     is, and record its location and the commit or date you read.

   Record each in the register's Location and Version columns. Never edit
   anything in `raw/`.
6. **Report** what changed, which pages hold it, and any gap left.

## Rules

- One page per concept. Update over duplicate. Create a new page only for a
  genuinely distinct concept.
- Show a conflict between the source and an existing page before replacing
  either claim. Follow the profile's "What to trust" order. If it does not
  decide, ask.
- Never put PII, credentials, tokens, or customer data in a page.
- Never invent a Related link to make a page look connected.
- Edit pages, not indexes, to change what an index says about a page; the
  index line mirrors the page's title and description.
- Keep raw documents immutable.

## When not to use

- The user only wants to know what the wiki says: `agent-wiki-read`.
- The user wants a structural check: `agent-wiki-lint`.
- The wiki does not exist yet: `agent-wiki-init`.

## Hand off to

- `agent-wiki-lint` after a large write or a new section.
- `agent-wiki-health` when the write revealed several thin areas.
