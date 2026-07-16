# Data modeling: star schema, data vault, one big table

*Part of [Data warehouse](./README.md).*

The modeling question is really a question about where you want to pay the cost: up front in structure, or later in maintenance. There is no model that avoids the cost entirely.

## Foundations

- **Star schema (Kimball / dimensional modeling)** organizes data into fact tables (events, measurements) and dimension tables (the who/what/where/when around them). Few joins, intuitive for BI tools, easy for analysts to reason about.
- **Data vault** splits data into hubs (business keys), links (relationships), and satellites (attributes and history). It's built to absorb new and changing sources without redesigning the model, at the cost of being much harder to query directly.
- **One big table (OBT)** denormalizes everything into a single wide table per use case. Fast to query, trivial to understand, but expensive to maintain the moment an upstream dimension changes and every downstream row needs rewriting.

## Common pitfalls

- **Picking a model based on what's trendy rather than what fits.** Data vault solves a scaling and source-volatility problem most small teams don't have yet, and importing its complexity anyway.
- **Star schema that takes a full sprint to onboard a new source.** This is the classic failure mode at the other end: a schema too rigid for a business that's still figuring out what data it has.
- **OBT as the *only* layer.** It's excellent as a serving layer for a specific dashboard or join-averse BI tool. It's a maintenance trap as the general-purpose foundation, because reprocessing 50 million rows because a dimension changed is a recurring cost, not a one-time one.
- **Mixing modeling philosophies without a boundary.** Some tables dimensional, some ad hoc wide tables, some raw dumps, with no documented rule for which is which — the worst of all three, because nobody can predict where a given piece of logic lives.

## How to succeed

- Default to a **dimensional core** (star schema) for the shared, canonical layer — it's the best balance of query simplicity, maintainability, and tooling support for most organizations.
- Reach for **data vault** specifically when you have many volatile sources and need historization and source-onboarding speed more than query simplicity — and be honest that it needs a BI/serving layer on top, not instead of.
- Use **OBT as a serving layer**, built *from* the dimensional core for a specific high-traffic dashboard or tool, not as a replacement for it.
- Whatever you choose, write the decision down. The cost of the wrong model is mostly paid by people who didn't make the choice and don't know why it was made.

## See also

- [Architecture patterns](./architecture-patterns.md) — where modeling choices meet layered pipeline design
- [Transformation layer (dbt)](../analytics-engineering/transformation-layer-dbt.md) — how these models actually get built and maintained day to day
