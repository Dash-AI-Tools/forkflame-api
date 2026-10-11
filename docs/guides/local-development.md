---
type: Guide
title: Running the stack locally
description: Start Postgres, Redis and all services on a fresh machine.
tags: [backend, development]
status: stable
generated: 2026-10-11
verified: 2026-10-11
---

# Running the stack locally

You need Docker and one `.env` file. No cloud account, no VPN.

## Checklist

- [ ] Copy `.env.example` to `.env` (database passwords are throwaway locally).
- [ ] Start Postgres 17 and Redis: `docker compose up -d db cache`.
- [ ] Apply migrations: `./scripts/db-migrate.sh`.
- [ ] Start the services: `./scripts/dev.sh` (gateway on `http://localhost:8080`).
- [ ] Seed tonight's menu: `./scripts/seed-menu.sh`.

## Smoke test

```bash
curl http://localhost:8080/health
curl http://localhost:8080/v1/menu | head -c 300
```

Both answer 200. If the menu is empty, the seed script did not run — it is
idempotent, so run it again.
