# Data warehouse: foundations & how to succeed

A data warehouse is a storage and modeling layer built to answer questions across the business, not just to run one application. That's the entire point, and it's also where most of the trouble starts: a warehouse has no single owner in the way an application does, so the discipline that keeps it usable has to be imposed deliberately. It doesn't emerge on its own.

## Foundations

- **Clear purpose before architecture.** "We want a data warehouse" is not a goal. The most common failure point in warehouse projects is starting design before anyone has agreed what decisions the warehouse needs to support. Architecture, schema, and tooling choices should all trace back to specific questions the business needs answered.
- **A modeling discipline, chosen on purpose.** Star schema, data vault, one-big-table — pick based on how many sources you have, how fast they change, and who's querying, not on what's trendy. See [Data modeling](./data-modeling.md).
- **A layered architecture with real contracts between layers**, not just three folders called bronze/silver/gold. See [Architecture patterns](./architecture-patterns.md).
- **Governance from day one.** Access control, data classification, and ownership are cheapest to set up before there's data in the warehouse, and increasingly expensive after.
- **A cost model you understand before you scale it.** Cloud warehouses make it trivial to spend a lot of money accidentally. See [Performance & cost](./performance-and-cost.md).

## Common pitfalls

- **Loading everything, modeling nothing.** Ingestion is easy to celebrate and modeling is easy to defer. Six months in, the warehouse is a raw-data landfill with a BI tool pointed at it, and every dashboard re-derives its own version of the same business logic.
- **Confusing "we have a warehouse" with "we have trustworthy data."** A perfectly designed architecture is worthless if the data in it is wrong, and modeling doesn't fix upstream data quality — it just gives the bad data a nicer home.
- **No maintenance plan.** Warehouses degrade: schemas drift, models rot, costs creep. Treating launch as the finish line instead of the start of ongoing operation is the single most common way a warehouse becomes unreliable a year later.
- **Undocumented transformation logic.** The tenth analyst to touch a model can't tell what it's for or why a filter is there. Documentation debt compounds exactly like the technical kind.

## How to succeed

1. Start from the questions the business actually needs answered, and build backward from there — not from a reference architecture diagram.
2. Choose a modeling approach deliberately and write down why, so the next person doesn't have to reverse-engineer the reasoning.
3. Put governance (access, classification, ownership) in place before the data lands, not after the first incident.
4. Budget for ongoing maintenance the same way you'd budget for ongoing application support — it's not optional, it's deferred cost.
5. Treat documentation as part of the deliverable for any model, not as a nice-to-have that happens if there's time left.

## Pages in this section

- [Data modeling](./data-modeling.md) — star schema, data vault, one big table, and how to choose
- [Architecture patterns](./architecture-patterns.md) — layered warehouses, medallion architecture, and where it breaks
- [Performance & cost](./performance-and-cost.md) — compute, storage, and the ways cloud warehouses get expensive
- [Governance & access](./governance-and-access.md) — classification, access control, and trust

## See also

- [Data platform](../data-platform/README.md) — the organizational layer that determines whether the warehouse stays usable
- [Analytics engineering](../analytics-engineering/README.md) — the discipline that actually builds and maintains the models living in the warehouse
