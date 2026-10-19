---
type: Profile
title: Acme Wiki
description: What Acme Wiki covers, its sections, and what to trust.
tags: [profile]
---

# Acme Wiki

A made-up example for a small subscription business: what its finance
numbers mean, and which tables they come from. Used by the finance and data
teams and by their AI assistants.

## Sections

* [Finance](finance/index.md) - What the finance numbers mean and the rules behind them.
* [Data model](data-model/index.md) - The tables behind the numbers, column by column.

## What to trust

The wiki records what you told it, and you are the final word. If something
outside the wiki should win over a page, list it here, strongest first.

* The billing code in the `billing` repository, for what the system actually does.

## Leave alone

Folders the assistant never edits or checks:

* `raw/` - original documents as they arrived

## Freshness

A section with no log entry in 90 days is flagged by `agent-wiki-health`.
Change the number here if this wiki moves faster or slower.

## Extra fields

Front matter fields allowed on pages beyond the standard four. Leave empty
unless you need them.

* (none)
