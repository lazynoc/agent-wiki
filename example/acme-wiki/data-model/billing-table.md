---
type: Reference
title: Billing table
description: One row per invoice line; MRR uses paid, recurring rows only.
tags: [billing, invoices, table, columns]
---

# Billing table

## What it holds

One row per invoice line. As of October 2026 it is the only table finance
uses for revenue.

## Columns

| Column | Meaning |
| --- | --- |
| `invoice_id` | The invoice this line belongs to. |
| `account_id` | The customer account. |
| `charge_type` | `recurring` for subscriptions, `one_off` for set-up fees and extras. |
| `amount_net` | Amount after discounts, before tax. |
| `billed_at` | When the line was billed. Revenue months use this date. |
| `status` | `paid`, `unpaid`, or `void`. |

## Related

* [Monthly recurring revenue](../finance/revenue.md) - how finance counts revenue from these rows.
