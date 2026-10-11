---
type: Decision
title: API versioning
description: Why versions live in the URL path and old versions retire slowly.
tags: [backend, api, versioning]
status: stable
generated: 2026-10-11
---

# API versioning

**Decision:** versions live in the URL path (`/v1/menu`), and a version retires no
earlier than 6 months after its successor ships, announced in the change log.

## Context

The web app and the API deploy independently, and Friday-night traffic forgives no
flag day. Path versions let old and new clients coexist; the gateway routes by
prefix and reports per-version traffic on the dashboards.

## Consequences

- Breaking changes mean a new version, never a silent field change.
- Additive changes (new fields, new optional parameters) land in the current version.
- The gateway answers unknown versions with 404 and the list of live versions.
