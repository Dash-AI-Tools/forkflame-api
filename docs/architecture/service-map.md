---
type: Reference
title: Services, repos and ports
description: Every backend service, its repository, port and health endpoint.
tags: [backend, architecture, reference]
status: stable
generated: 2026-10-11
verified: 2026-10-11
---

# Services, repos and ports

| Service | Repo | Port | Health |
| ------- | ---- | ---- | ------ |
| API gateway | `forkflame-api` | 8080 | `GET /health` |
| Menu service | `forkflame-api` | 8081 | `GET /health` |
| Orders service | `forkflame-api` | 8082 | `GET /health` |
| Payments worker | `forkflame-api` | — (queue) | queue depth metric |
| Auth | `forkflame-api` | 8084 | `GET /health` |
| Postgres | managed | 5432 | `pg_isready` |
| Redis (cache, sessions) | managed | 6379 | `PING` |

All services expose Prometheus metrics on `/metrics` and log one JSON object per
line. Nothing listens on any other port in production.
