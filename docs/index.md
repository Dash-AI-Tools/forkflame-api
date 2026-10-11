---
okf_version: "0.2"
title: Fork & Flame backend documentation
description: Architecture, services, data, decisions and API policies of the restaurant backend.
generated: 2026-10-11
---

# Fork & Flame backend documentation

How the Fork & Flame backend serves the [customer web app](../../forkflame-web/docs/index.md):
services for menu, orders, payments and auth, the data layer, and the rules every
endpoint follows. Start with the [system overview](./architecture/overview.md).

## Contents

| Folder | What it holds |
| ------ | ------------- |
| [Architecture](./architecture/index.md) | System overview, service map. |
| [Guides](./guides/index.md) | Local development, adding an endpoint. |
| [Services](./services/index.md) | Menu, orders, payments, auth, webhooks. |
| [Data](./data/index.md) | Schema, caching, search. |
| [Decisions](./decisions/index.md) | API versioning, error format. |
| [Policies](./policies/index.md) | Rate limits. |

Recent changes are listed in the [change log](./log.md).

## Concept types used in this bundle

| `type` | Used for |
| ------ | -------- |
| `Concept` | How a service or data flow works. |
| `Guide` | Steps to build or run the backend. |
| `Reference` | Exact facts to look up: ports, schema, webhooks. |
| `Decision` | An API design decision with context and consequences. |
| `Policy` | A rule every endpoint or client must follow. |

`index.md` and `log.md` are reserved files in OKF. They are not concepts and carry no `type`.
