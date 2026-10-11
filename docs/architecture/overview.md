---
type: Concept
title: System overview
description: The services behind Fork & Flame and how an order flows through them.
tags: [backend, architecture]
status: stable
generated: 2026-10-11
verified: 2026-10-11
---

# System overview

Four services and one database run the restaurant. The [customer web app](../../forkflame-web/docs/index.md)
talks only to the API gateway; everything behind it is private.

```mermaid
flowchart LR
  Web[Web app] --> GW[API gateway]
  GW --> Menu[Menu service]
  GW --> Orders[Orders service]
  GW --> Pay[Payments]
  GW --> Auth[Auth]
  Orders --> DB[(Postgres)]
  Menu --> DB
  Orders --> Kitchen[Kitchen screen]
  Orders --> Courier[Delivery partners]
```

## Request path of an order

1. The gateway authenticates (or accepts a guest) and rate-limits per the
   [rate limits](../policies/rate-limits.md).
2. The orders service reserves the dishes, computes the total and creates the order
   in state `received`.
3. Payments captures the charge; only then does the order move to `firing` on the
   kitchen screen.
4. When the courier picks up, the orders service emits a webhook (see
   [outbound webhooks](../services/webhooks.md)).

Full service list with ports: [service map](./service-map.md).
