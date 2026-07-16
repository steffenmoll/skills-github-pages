# Governance & trust

*Part of [Data platform](./README.md).*

Trust in data isn't a feeling — it's the accumulated result of governance decisions someone actually made and enforced. Skip the decisions, and the trust doesn't show up either, no matter how good the platform looks.

## Foundations

- **Data contracts** — explicit, ideally machine-readable agreements between producers and consumers covering schema, quality expectations, SLAs, and ownership — are what make "distributed ownership" survivable instead of chaotic. Without them, every schema change downstream is a surprise.
- **Governance maturity has to precede decentralization.** Organizations that couldn't govern a single centralized system don't gain governance by splitting it into ten decentralized ones — most orgs adopting mesh-style patterns are not yet at the governance maturity that model assumes.
- **Consistent quality across domains** is a genuinely hard, recurring problem the moment more than one team owns data — schema drift and inconsistent definitions are the default outcome, not the exception, unless something actively counteracts them.

## Common pitfalls

- **Weak governance masquerading as autonomy.** "Each team owns their data" without shared standards produces inconsistent semantics and incompatible schemas — autonomy without accountability, which reads as flexibility right up until two teams' numbers disagree in front of an executive.
- **Treating data mesh (or any decentralization) as an organizational change you can skip by buying a tool.** The tool doesn't do the governance work; it just gives you a nicer interface to the same ungoverned data.
- **No consequence for schema changes that break downstream consumers.** Without a contract and an enforcement mechanism, "we changed the schema and didn't tell anyone" keeps happening, because nothing makes it costly to the team that did it.
- **Trying to mesh (or govern) everything at once**, instead of proving the model on a few domains first. Big-bang governance rollouts fail in the same way big-bang platform rollouts do — no early feedback before the mistakes are expensive.
- **Governance owned by no one in particular.** A policy without an enforcing party is a suggestion.

## How to succeed

1. Put data contracts in place at team boundaries before scaling ownership further — schema, quality expectations, and SLAs, agreed by both sides, not imposed by one.
2. Assess governance maturity honestly before decentralizing. Centralized governance done well is a better foundation for a future mesh than a mesh with no governance at all.
3. Make schema-breaking changes costly to skip communicating — automated contract checks in CI, not just a Slack norm that erodes under deadline pressure.
4. Pilot governance and ownership changes on a small number of domains, learn from what breaks, then expand — resist the big-bang rollout.
5. Name an actual owner for governance itself — someone (or some group) whose job includes enforcing the standards, not just writing them down.

## See also

- [Organization & ownership](./organization-and-ownership.md) — the ownership model governance has to support
- [Data warehouse: governance & access](../data-warehouse/governance-and-access.md) — governance mechanics at the warehouse level
- [Analytics engineering: semantic layer & metrics](../analytics-engineering/semantic-layer-and-metrics.md) — where inconsistent definitions become visible to end users
