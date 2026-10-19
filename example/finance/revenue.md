---
type: Concept
title: Monthly recurring revenue
description: MRR counts paid, active subscriptions only, net of discounts, in the month they are billed.
tags: [mrr, revenue, monthly recurring revenue, subscriptions]
---

# Monthly recurring revenue

## What it means

Monthly recurring revenue (MRR) is the money we expect every month from
subscriptions that are active and paid. As of October 2026:

- Count a subscription in the month it is **billed**, not the month it is
  paid.
- Use the amount **after discounts**, before tax.
- Leave out one-off charges such as set-up fees.
- Leave out invoices that were voided.

## Where the numbers come from

Each billed subscription is one row in the [Billing table](../data-model/billing-table.md).
MRR is the sum of `amount_net` for rows with `status = paid` and
`charge_type = recurring`, grouped by the month of `billed_at`.

## Open questions

- Do refunds after month end reduce last month's revenue? Unknown; see
  `gaps.md`.

## Related

* [Billing table](../data-model/billing-table.md) - the columns MRR is built from.
