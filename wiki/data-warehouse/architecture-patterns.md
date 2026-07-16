# Architecture patterns: layered warehouses and the medallion model

*Part of [Data warehouse](./README.md).*

Almost every modern warehouse ends up layered — raw, cleaned, curated, however it's named. The pattern isn't the risk. Treating it as a pipeline you build once and forget, instead of a set of contracts you enforce continuously, is the risk.

## Foundations

- The common shape is **raw → staging/cleaned → marts/curated** (or bronze → silver → gold in the medallion naming). Each layer has a job: raw preserves source fidelity, staging standardizes and cleans, marts model for consumption.
- Layers should be **contracts, not folders**. Each layer promises something specific about the data it holds (schema stability, deduplication, business logic applied), and downstream consumers rely on that promise.
- Not every dataset needs every layer. A small dataset feeding one dashboard doesn't need a three-hop pipeline — that's paying storage, latency, and maintenance cost for no return.

## Common pitfalls

- **Blurred layer boundaries.** Raw events written straight into the gold layer, or curated tables built on unrefined bronze data. The moment a source schema changes, it cascades through the whole stack because nothing was actually insulating downstream consumers.
- **Semantic sprawl in the middle layer.** Teams start building business KPIs and heavy aggregations in "silver" because it's convenient, and now there are several different definitions of the same metric depending on which pipeline you ask.
- **Applying three layers reflexively to everything.** Not every pipeline needs the full medallion treatment. Doing it anyway is one of the most common anti-patterns — pure overhead with no corresponding benefit.
- **Inconsistent layer definitions across teams.** Without a shared, written definition of what "silver" means, every team invents its own, and the layers stop meaning anything as an organizational contract.
- **Treating it as a linear pipeline you configure once.** Layers need ongoing governance — who owns transformations at each layer, who can promote data from one layer to the next — and that ownership question doesn't answer itself.

## How to succeed

1. Write down, once, what each layer promises — not just what it usually contains. Make it a contract the whole org can point to.
2. Keep business logic and KPI definitions in the layer designed for consumption (marts/gold), not scattered wherever it was convenient to add.
3. Scale the pattern to the dataset. A three-layer pipeline for a five-row lookup table is cost with no benefit.
4. Assign explicit ownership per layer, especially the promotion step from one layer to the next — that's where responsibility most often falls through the cracks.
5. Revisit the pattern as the org grows. What worked as an implicit convention for one team needs to become an explicit, enforced rule once ten teams are building on top of it.

## See also

- [Data modeling](./data-modeling.md) — the modeling choices that live inside the curated layer
- [Data platform: tooling & architecture](../data-platform/tooling-and-architecture.md) — how these layers map onto storage, compute, and orchestration choices
- [Ingestion & integration](../data-engineering/ingestion-and-integration.md) — what actually lands in the raw layer, and how
