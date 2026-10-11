---
type: Concept
title: Orders service
description: The state machine every order travels, from received to delivered.
tags: [backend, orders]
status: stable
generated: 2026-10-11
---

# Orders service

The orders service is the heart of the backend. Each order carries an idempotency
key from the web app, so a double-tapped pay button creates exactly one order.

## States

`received` → `firing` → `ready` → `picked_up` → `delivered`. Two side states:
`cancelled` (before `firing` only) and `failed` (payment never captured).

## Rules

- Stock is reserved at `received` and released on `cancelled` — overselling the
  last burrata is a bug, not bad luck.
- The transition to `firing` requires a captured payment or a cash flag.
- Every transition appends to the order history; the current state is never
  overwritten in place, so the [tracking page](../../forkflame-web/docs/ordering/tracking.md)
  can always explain "why is my pizza still firing".
