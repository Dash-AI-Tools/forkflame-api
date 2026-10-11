---
type: Concept
title: Caching strategy
description: What is cached, for how long, and what invalidates it.
tags: [backend, data, caching]
status: stable
generated: 2026-10-11
---

# Caching strategy

Redis holds three things: the rendered menu (60 seconds), sessions (sliding
30 days), and the oven-queue hint (60 seconds). Everything else hits Postgres,
which is fast enough and always right.

## Invalidation

- Menu cache: invalidated on any availability, price or dish change — the kitchen
  never waits a minute to 86 the octopus.
- Sessions: deleted on logout and on password-less re-login from a new device.
- Queue hint: expires naturally; a stale hint only misleads for one minute.

Cache misses are logged but never fatal: every read path works with Redis down,
just slower. That property is tested weekly by turning Redis off in staging.
