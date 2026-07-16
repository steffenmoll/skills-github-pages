# Transformation layer (dbt): staging, intermediate, marts

*Part of [Analytics engineering](./README.md).*

dbt (and tools like it) didn't invent the idea of a layered transformation model — it made it cheap enough to actually do consistently. The discipline still has to be supplied by the team; the tool just removes the excuse not to.

## Foundations

- **Staging models** do the minimum: rename, cast types, light cleaning — a thin, consistent layer directly on top of raw sources, with no business logic yet.
- **Intermediate models** combine and reshape staging models into reusable building blocks — joins, deduplication, business rules that multiple downstream marts will need.
- **Marts** are the consumption layer: dimensional models, wide tables, or metrics built specifically for how a given audience actually queries the data.
- **DRY (don't repeat yourself) is the organizing principle.** Any business logic used more than once belongs in a shared model, not copy-pasted across the marts that need it.

## Common pitfalls

- **Business logic creeping into staging models.** Once staging starts encoding business rules, every downstream consumer inherits assumptions they can't see or override, and the "thin, consistent layer" promise breaks.
- **Marts built directly on raw sources**, skipping staging and intermediate layers because it's faster for one specific report — it is, until the underlying source changes and there's no insulation layer to absorb it.
- **Copy-pasted CTEs across multiple marts.** The same join or the same filter, slightly modified, in five different models is the single clearest sign the intermediate layer is underused.
- **No clear ownership of the boundary between layers.** Without a shared convention for what belongs in staging versus intermediate versus marts, every contributor draws the line differently, and the project's structure stops being predictable.
- **Treating the transformation layer as a one-time build instead of a maintained codebase.** Models rot the same way any other code rots — through untracked assumptions and unreviewed changes — if nobody treats it as ongoing engineering work.

## How to succeed

1. Keep staging genuinely thin: renaming, casting, light cleaning — nothing that encodes a business decision.
2. Push shared logic (joins, business rules, deduplication) into intermediate models specifically so it's written once and reused, not rediscovered per mart.
3. Build marts for the actual audience and access pattern — a BI tool that struggles with joins may need a wider, more denormalized mart even if the intermediate layer stays properly normalized underneath.
4. Document, in the project itself, what belongs in each layer — make the convention explicit rather than assuming everyone will converge on the same mental model.
5. Review the transformation layer's health periodically, the same way you'd review any codebase — duplicated logic and layer violations accumulate quietly if nobody looks.

## See also

- [Data warehouse: data modeling](../data-warehouse/data-modeling.md) — the modeling theory this layer implements in practice
- [Testing & documentation](./testing-and-documentation.md) — verifying the transformation layer actually does what it claims
