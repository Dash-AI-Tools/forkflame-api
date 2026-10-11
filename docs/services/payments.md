---
type: Concept
title: Payments integration
description: Cards, wallets and cash: how money moves without ever touching card numbers.
tags: [backend, payments]
status: stable
generated: 2026-10-11
---

# Payments integration

Card numbers never reach our servers. The web app tokenizes with the payment
provider; the backend only ever sees tokens and capture IDs.

## Flow

1. The web app sends a payment token with the order key.
2. The backend authorizes the exact total (dishes + fee − Ember discount).
3. On kitchen acceptance the authorization is captured; on rejection it is voided.
4. Cash orders skip all three steps and are flagged for the courier.

## Refunds

Full refunds are automatic on cancellation before `firing`. After firing, refunds
need a manager's tap on the kitchen screen and land within 5 business days. The
[ payment outage runbook](../../forkflame-ops/docs/runbooks/payment-outage.md)
covers what happens when the provider itself is down.
