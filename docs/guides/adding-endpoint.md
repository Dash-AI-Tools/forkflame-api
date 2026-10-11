---
type: Guide
title: Adding a new endpoint
description: From route to test to changelog entry when the API grows.
tags: [backend, development, api]
status: stable
generated: 2026-10-11
---

# Adding a new endpoint

1. Pick the version: new behavior goes under the current [API version](../decisions/api-versioning.md),
   never by moving an old route.
2. Define the handler next to its service (`src/orders/routes/`), with request
   validation before any database call.
3. Errors use the [error response format](../decisions/error-format.md) — a failing
   test for a new error shape comes first.
4. Add a test that hits the route through the gateway, including the 429 case from
   the [rate limits](../policies/rate-limits.md).
5. Document the route in the service doc and note it in `docs/log.md`.

Routes without a test and a doc entry do not merge.
