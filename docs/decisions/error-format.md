---
type: Decision
title: Error response format
description: The one JSON shape every failure uses, and why codes are stable strings.
tags: [backend, api, errors]
status: stable
generated: 2026-10-11
---

# Error response format

**Decision:** every failure answers with the same shape, and `code` is a stable
machine-readable string, never a number:

```json
{
  "error": {
    "code": "dish_sold_out",
    "message": "The octopus just sold out — the menu has the rest.",
    "retryable": false
  }
}
```

## Context

The web app shows `message` to humans and branches on `code`. Numbers would collide
with HTTP statuses in every log line; strings grep cleanly.

## Consequences

- `message` is always safe to display; internals go to the logs, never to clients.
- `retryable` tells the web app whether to retry (rate limit: yes, sold out: no).
- New codes are added, never renamed; renaming one is a version bump per the
  [API versioning](./api-versioning.md) decision.
