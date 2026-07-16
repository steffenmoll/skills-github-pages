# Domain wiki

Internal reference material for the blog. Not published, not linked from the site — a working knowledge base to draw on when writing posts.

Each section covers one domain from two angles: **foundations** (what has to be true for this to work at all) and **how to succeed** (the challenges, pitfalls, and solutions that separate teams that get value from the thing from teams that just have the thing).

## Sections

- [Data warehouse](./data-warehouse/README.md) — the storage and modeling layer: how data is structured, organized, and made queryable.
- [Data platform](./data-platform/README.md) — the organizational and architectural system around the warehouse: ownership, tooling, governance, scale.
- [Data engineering](./data-engineering/README.md) — the discipline of moving data reliably: ingestion, pipelines, orchestration, testing.
- [Analytics engineering](./analytics-engineering/README.md) — the discipline of transforming raw data into trusted, reusable models and metrics.

## How these relate

These aren't four independent topics — they're four layers of the same stack, and the boundaries are where most of the interesting failure modes live:

- A **data warehouse** is a thing you have (storage + schema).
- A **data platform** is the system of people, tooling, and rules that keeps the warehouse (and everything around it) usable as the org grows.
- **Data engineering** gets data into the warehouse reliably.
- **Analytics engineering** turns what's in the warehouse into something a human or a dashboard can trust.

A good platform can't fix bad pipelines. Good pipelines can't fix a warehouse with no modeling discipline. Good models can't fix an org with no ownership. Each layer's "how to succeed" section assumes the layers below it are basically sound — pitfalls are noted where a lower layer's failure is commonly misdiagnosed as a problem in the layer above it.

## Format

Each subject page follows the same shape:

- **Foundations** — the non-negotiable basics
- **Common pitfalls** — how this goes wrong in practice, and why the failure is tempting
- **How to succeed** — what to actually do about it
- **See also** — related pages, inside and outside this wiki
