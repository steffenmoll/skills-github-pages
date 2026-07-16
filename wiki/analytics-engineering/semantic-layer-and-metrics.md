# Semantic layer & metrics

*Part of [Analytics engineering](./README.md).*

A semantic layer exists to answer one question the same way everywhere it's asked: what does "active customer" (or "revenue," or "churn") actually mean? Skip it, and every dashboard, analyst, and AI copilot ends up answering that question slightly differently, with no way to tell which one is right.

## Foundations

- **A semantic layer defines reusable metrics, dimensions, and entities** in a way downstream tools (BI dashboards, notebooks, AI copilots) can actually consume consistently, instead of each tool re-implementing the definition.
- **Architectural approaches differ**: warehouse-native (semantic metadata as objects in the warehouse itself), transformation-layer (semantic models as code alongside dbt, e.g. MetricFlow), and OLAP-acceleration (a caching/pre-aggregation layer, e.g. Cube). The right choice depends on where your team already has the most modeling maturity and tooling investment.
- **Metrics should be computed, not frozen.** Preferring to compute values in measures and metrics — rather than materializing pre-aggregated rollups — keeps the semantic layer flexible as questions change, at some cost to raw query speed.

## Common pitfalls

- **Skipping the semantic layer because dashboards work fine individually.** They work fine right up until two dashboards report different numbers for the same metric in the same meeting, and nobody can quickly say which one (if either) is correct.
- **Treating the semantic layer as a one-time setup rather than critical infrastructure.** Like any production system, it needs planning, testing, and ongoing operational rigor — poor optimization here causes real performance degradation as data volume and user base grow.
- **Denormalizing too early in the underlying models**, then trying to build a flexible semantic layer on top of data that's already collapsed into one fixed shape — flexibility upstream (normalized staging/intermediate models) makes a much more capable semantic layer than flexibility bolted on after the fact.
- **AI tools and copilots bypassing the semantic layer entirely**, querying raw or lightly modeled tables directly and inventing their own definitions of business terms — this reintroduces exactly the inconsistency the semantic layer was built to prevent, just faster.
- **No governance over who can add or change a metric definition.** Without an owner, metric definitions drift the same way any other unowned artifact does.

## How to succeed

1. Invest in a semantic layer once more than a couple of dashboards or tools need the same metrics — the cost of inconsistency grows faster than the cost of building it.
2. Build semantic models on top of well-normalized staging/intermediate models, and let the semantic layer handle denormalization for consumers dynamically, rather than baking denormalization in upstream.
3. Prefer computing metrics dynamically over freezing pre-aggregated rollups, reserving materialized rollups for the specific cases where performance genuinely requires them.
4. Route AI and BI tools through the semantic layer rather than letting them query raw or intermediate models directly — consistency has to be enforced structurally, not requested politely.
5. Assign clear ownership over metric definitions, with a real review process for adding or changing one — treat it as a governance surface, not just a technical config file.

## See also

- [Testing & documentation](./testing-and-documentation.md) — verifying semantic definitions stay correct as models change
- [Data platform: governance & trust](../data-platform/governance-and-trust.md) — the organizational trust problem a semantic layer is built to solve
