---
name: agent-wiki-init
description: Use when starting a brand-new wiki from nothing, such as "start a wiki", "set up a wiki at <folder>", or "create a knowledge base for <topic>". Creates the folders and starter files, then stops. Not for a folder that already has content, and not for adding pages.
---

# Agent Wiki: Init

## Outcome

An empty wiki the user can start filling, created from one confirmed
sentence. Two decisions matter: where it lives and what its sections are.
Everything else is derived.

## Before you start

Read `../agent-wiki/references/wiki-standard.md` for the layout and
`../agent-wiki/references/wiki-profile-template.md` for the profile file.

## Steps

1. Work out the two decisions from what the user said. Where: the folder
   they named, or the current folder plus `wiki/` if they gave none.
   Sections: the topics they mentioned, kebab-cased, or one section named
   `general`. Derive the wiki name from the folder name. Ask only for what
   is missing, one question at a time.
2. Confirm once, in one sentence, before creating anything: "I'll create
   **Refunds Wiki** at `~/wikis/refunds` with sections `refunds` and
   `operations`. OK?" Never proceed on silence.
3. Refuse if the folder exists and is not empty. Never delete or reuse a
   folder to make it fit.
4. Create, using your own file tools:
   - `wiki-profile.md` from the template, placeholders filled.
   - `index.md` at the root listing each section as
     `* [<Section title>](<section>/index.md) - <one line>`, with
     `okf_version: "0.2"` as its only front matter.
   - `log.md` at the root with today's date and one line:
     `* **Creation**: Wiki created with sections <list>.`
   - `gaps.md` with the standard header (`type: Gap List`) and the line
     `No open questions yet.`
   - For each section: `index.md` holding only a heading and the line
     `No pages yet.`; `log.md` with a Creation entry; `source-register.md`
     with the standard header (`type: Source Register`) and an empty table.
   - An empty `raw/` folder. Some tools cannot create an empty folder; if
     so, write `raw/README.md` containing one line: "Original documents go
     here. They are never edited."
5. Close with one next step: "Your wiki is at `<path>`. Tell me something
   to add, or give me a document to put in."

## Rules

- Never run commands, install anything, initialise git, call the network,
  or ask a model to fill the wiki.
- Never add domain facts. The scaffold is empty on purpose.
- Every file you write follows the shapes in the standard, so `agent-wiki-lint`
  passes on a fresh wiki.

## When not to use

- The folder already has pages: use `agent-wiki-write` to add to it.
- The user wants to know what the wiki says: use `agent-wiki-read`.

## Hand off to

- `agent-wiki-write` as soon as the user has something to add.
