# Wiki Profile Template

`agent-wiki-init` writes this file as `<wiki-root>/wiki-profile.md`, replacing every
`<placeholder>`. Every skill reads it first. Keep it short; it is read on
every question.

```markdown
---
type: Profile
title: <Wiki Name>
description: What <Wiki Name> covers, its sections, and what to trust.
tags: [profile]
---

# <Wiki Name>

<One or two sentences: what this wiki is for and who uses it.>

## Sections

* [<Section title>](<section>/index.md) - <what it covers, one line>
* [<Section title>](<section>/index.md) - <what it covers, one line>

## What to trust

The wiki records what you told it, and you are the final word. If something
outside the wiki should win over a page, list it here, strongest first.

* (none)

## Leave alone

Folders the assistant never edits or checks:

* `raw/` - original documents as they arrived

## Freshness

A section with no log entry in 90 days is flagged by `agent-wiki-catch-up`.
Change the number here if this wiki moves faster or slower.

## Extra fields

Front matter fields allowed on pages beyond the standard four. Leave empty
unless you need them.

* (none)
```
