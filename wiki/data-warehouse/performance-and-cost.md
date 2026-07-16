# Performance & cost

*Part of [Data warehouse](./README.md).*

Cloud warehouses removed the friction of provisioning hardware and replaced it with the friction of an invoice nobody understands. The mechanics differ by platform, but the failure mode is the same: nobody was watching the meter.

## Foundations

- Cloud warehouse cost generally breaks into **compute** (queries and transformations), **storage** (raw + historical data), and **services overhead** (metadata, orchestration features). Compute is almost always the lever with the most leverage.
- Pricing models differ by platform in ways that change what "wasteful" even means: **on-demand, scan-based pricing** (e.g. BigQuery) punishes unfiltered full-table scans; **warehouse/credit-based pricing** (e.g. Snowflake) punishes idle, oversized, or always-on compute.
- Query patterns and access patterns should drive platform and configuration choices — a platform optimized for predictable BI concurrency behaves very differently under bursty, ad hoc analyst workloads.

## Common pitfalls

- **Overprovisioned, always-on compute.** Warehouses sized for peak load and left running, or auto-suspend left disabled or set too generously, so idle time is billed like active time.
- **The scan-based pricing trap.** On scan-priced platforms, an unfiltered `SELECT *` over a multi-terabyte table from someone who didn't know better can produce a bill that dwarfs a week of normal usage — in seconds, with no warning until the invoice arrives.
- **No resource monitors or budget guardrails.** Without automated circuit breakers, a runaway query or a mis-scheduled job runs to completion (and to full cost) before anyone notices.
- **Full refreshes where incremental would do.** Reprocessing an entire table on every run because incremental logic was never built is one of the most common and most fixable sources of both cost and fragility.
- **Access controls that let anyone spin up large compute.** Without guardrails, a well-meaning analyst testing a query on the biggest available warehouse size is a predictable, recurring cost event, not a one-off mistake.

## How to succeed

1. Set aggressive auto-suspend on compute (seconds, not minutes) and right-size warehouses by testing at a smaller size before defaulting to a larger one.
2. Put resource monitors or spend alerts in place before you need them, not after the first surprise invoice.
3. Match ingestion and transformation strategy to the pricing model: incremental loads almost always beat full refreshes on scan-priced platforms, and matter enormously for warehouse-credit platforms too.
4. Gate who can query at scale — training and tooling (query cost estimates, warehouse size limits) beat after-the-fact policing.
5. Review cost the same way you review performance: on a schedule, not only when something breaks.

## See also

- [Architecture patterns](./architecture-patterns.md) — layering choices that directly affect how much gets reprocessed and how often
- [Data platform: scaling](../data-platform/scaling-the-platform.md) — cost governance as an organizational, not just technical, problem
