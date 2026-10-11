---
type: Concept
title: Auth and sessions
description: Optional accounts, short-lived sessions and what guests can do.
tags: [backend, auth, accounts]
status: stable
generated: 2026-10-11
---

# Auth and sessions

Accounts are optional — guests order freely — so auth is deliberately boring:
email-link login, no passwords to leak, sessions in Redis with a 30-day sliding
window.

## Capabilities

| Who | Can |
| --- | ---- |
| Guest | Order, track by order number, book nothing |
| Signed-in customer | Reorder, Ember points, receipts, reservations |
| Kitchen role | Availability toggles, firing queue, refunds |
| Manager role | Everything kitchen does, plus menu edits and user lookup |

Kitchen and manager sessions live 12 hours and are bound to the restaurant
network. Tokens are random 256-bit strings; the database stores hashes only.
