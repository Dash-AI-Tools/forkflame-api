---
type: Concept
title: Dish search
description: How menu search ranks dishes with Postgres full-text search.
tags: [backend, data, search]
status: stable
generated: 2026-10-11
---

# Dish search

Menu search is Postgres full-text search over a weighted vector: dish names
outrank ingredient lists, which outrank descriptions. "Funghi" finds the mushroom
pizza before the pizza whose description mentions a mushroom forest.

## Behavior

- Queries use `websearch_to_tsquery` — never hand-built tsquery — so quotes and
  minus signs behave like customers expect.
- Results only include orderable dishes; sold-out dishes never rank.
- Typos within two edits still match ("margerita" finds the margherita); beyond
  that the page suggests the closest course instead of an empty list.
- Search terms are logged without session identifiers to learn which dishes to add.
