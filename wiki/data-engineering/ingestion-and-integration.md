# Ingestion & integration

*Part of [Data engineering](./README.md).*

The most expensive ingestion mistake isn't picking the wrong tool — it's picking a freshness requirement (streaming, when batch would do) that nobody downstream actually needed, and paying for that complexity indefinitely.

## Foundations

- **Batch, micro-batch, and streaming are freshness choices, not maturity levels.** Streaming isn't a more "advanced" version of batch — it's the right answer only when a decision genuinely depends on sub-minute freshness.
- **Change Data Capture (CDC)** captures row-level changes from a source system as they happen, and is the standard way to replicate operational databases into a warehouse without full reloads.
- **EL vs. ELT vs. ETL is a question of where transformation happens**, not just a naming preference — modern cloud warehouses generally favor ELT (load raw, transform in-warehouse) because warehouse compute is cheap and flexible relative to a separate transformation tier.

## Common pitfalls

- **Streaming everything because the tooling makes it easy**, when most consumers only need hourly or daily data — the cost isn't just infrastructure spend, it's the ongoing operational complexity of running and debugging streaming systems for no realized benefit.
- **Full reloads instead of incremental or CDC-based ingestion.** Reprocessing an entire source table on every run is a common, fixable source of both cost and fragility, and it's often left in place simply because incremental logic was never built.
- **No deduplication strategy at the integration boundary.** Source systems retry, webhooks fire twice, and without stable keys and dedup logic, duplicate records quietly inflate every downstream count.
- **Treating source systems as static.** Upstream schemas change without warning; ingestion that doesn't expect this breaks in ways that are hard to diagnose because the failure surfaces downstream, not at the source.
- **No contract with the source system owner.** Without an agreed schema and change-notification process, every upstream change is a surprise instead of a planned event.

## How to succeed

1. Choose ingestion freshness based on a specific, named decision that depends on it — not on what the tooling makes easiest.
2. Prefer incremental or CDC-based ingestion over full reloads once a source is large or changes are frequent enough to make full reloads expensive or slow.
3. Build deduplication and idempotency into the ingestion layer itself, using stable identifiers, so retries and replays are safe by default.
4. Expect upstream schema changes and design ingestion to fail loudly and specifically when they happen, rather than silently propagating bad data.
5. Where possible, formalize the relationship with source system owners — even an informal data contract beats discovering a breaking change in production.

## See also

- [Pipeline reliability & observability](./pipeline-reliability-and-observability.md) — what happens after ingestion when something inevitably goes wrong
- [Data warehouse: architecture patterns](../data-warehouse/architecture-patterns.md) — what lands in the raw layer, and what promises it needs to keep
