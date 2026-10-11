---
type: Concept
title: Menu service
description: How dishes, availability and prices are served to the storefront.
tags: [backend, menu]
status: stable
generated: 2026-10-11
---

# Menu service

The menu service owns dishes, prices and availability. It is read-heavy: the
storefront asks it on every page view, but dishes change a few times a day. See the
[caching strategy](../data/caching.md) for how it stays fast.

## Availability

A dish is orderable when `available = true` and every ingredient is in stock. The
kitchen toggles availability from the kitchen screen; the change reaches the
storefront within 5 seconds through cache invalidation, not polling.

## Prices

Prices live in integer cents. Happy-hour and loyalty prices are computed at read
time from the base price, so there is exactly one number to change when flour gets
expensive.
