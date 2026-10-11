---
type: Reference
title: Database schema
description: The eight tables that hold the restaurant, and what references what.
tags: [backend, data, database]
status: stable
generated: 2026-10-11
verified: 2026-10-11
---

# Database schema

Postgres 17. Eight tables; every foreign key is indexed; money is integer cents.

| Table | Holds | Key references |
| ----- | ----- | -------------- |
| `dishes` | Name, price, course, diet marks | — |
| `ingredients` | Stock counts | — |
| `dish_ingredients` | Recipe links | `dishes`, `ingredients` |
| `customers` | Accounts, Ember balance | — |
| `orders` | State, totals, idempotency key (unique) | `customers` |
| `order_lines` | Dish + extras + quantity | `orders`, `dishes` |
| `order_events` | Append-only history | `orders` |
| `reservations` | Party, seating, booking code (unique) | `customers` |

Migrations are forward-only and applied at deploy time. The
[database failover runbook](../../forkflame-ops/docs/runbooks/database-failover.md)
covers the day this database misbehaves.
