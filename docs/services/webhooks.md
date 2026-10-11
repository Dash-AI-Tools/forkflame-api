---
type: Reference
title: Outbound webhooks
description: Events we send to delivery partners and analytics, with retry rules.
tags: [backend, webhooks, integrations]
status: draft
generated: 2026-10-11
---

# Outbound webhooks

Delivery partners and the analytics pipeline subscribe to order events. Deliveries
are at-least-once with exponential-backoff retries (5 attempts over ~1 hour);
receivers must de-duplicate by event ID.

## Event catalog

| Event | When | Payload key |
| ----- | ---- | ----------- |
| `order.ready` | Dish leaves the oven | `order_id`, `ready_at` |
| `order.picked_up` | Courier takes the bag | `order_id`, `courier_id` |
| `order.delivered` | Customer confirms | `order_id`, `delivered_at` |
| `order.cancelled` | Cancelled before firing | `order_id`, `reason` |

Signatures use HMAC-SHA256 over the raw body. Retry behavior is still being
load-tested, which is why this document is a draft.
