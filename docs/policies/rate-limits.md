---
type: Policy
title: Rate limits
description: Per-client request budgets and what a 429 means.
tags: [backend, api, policy]
status: stable
generated: 2026-10-11
stale_after: 2027-01-01
---

# Rate limits

The gateway budgets requests per client IP and per API key. Budgets are generous
for humans and strict for scrapers.

## Budgets

| Scope | Limit | Window |
| ----- | ----- | ------ |
| Menu and search reads | 600 | minute |
| Order creation | 20 | minute |
| Tracking polls | 120 | minute |
| Webhook deliveries (outbound) | 5 retries | ~1 hour |

## Rules

- A 429 carries `Retry-After` and the [error format](../decisions/error-format.md)
  with `code: "rate_limited"` and `retryable: true`.
- Allow-listed delivery-partner IPs get triple budgets; abuse revokes the listing.
- Hitting the order-creation limit returns the existing order for the same
  idempotency key instead of an error whenever one exists.
