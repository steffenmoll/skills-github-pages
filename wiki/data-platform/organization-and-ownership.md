# Organization & ownership

*Part of [Data platform](./README.md).*

The org chart is the real architecture; the tech stack just draws it. Most platform failures that look technical are actually ownership failures wearing a technical costume.

## Foundations

- **"Functional" is relative to org size.** In a small team, functional means "ask the person who built it." Across ten teams, that answer stops working the moment that person changes roles, and nothing replaces it automatically.
- **Ownership needs to be durable across reorgs**, not just assigned once at launch. Boundaries move overnight in a reorg; the data doesn't move with them unless someone makes it.
- **Data mesh is an organizational maturity bet, not a tooling choice.** Its core idea — distribute ownership to the teams closest to the data — only works if those teams can actually hold onto that ownership through growth and change. Most organizations adopting the label don't yet have that maturity.

## Common pitfalls

- **Datasets outliving their owning team.** A reorg splits or merges a team, and the dataset just sits there, kept alive by whoever still has write access, while attention moves to the new org chart's priorities. Nobody decided to abandon it; it just stopped being anyone's explicit problem.
- **Domains defined by a snapshot of the org chart instead of a business function.** When a domain is defined purely as "whatever this team currently owns," it stops making sense the moment the team's shape changes.
- **Distributing ownership without distributing standards.** This is the data-mesh failure mode in miniature: teams get autonomy, quality and consistency don't travel with it, and the result is more datasets of less certain quality, not more trustworthy ones.
- **The first quiet exception.** A team with more political capital wants to skip an ownership rule because something's urgent, or because working around someone else's boundary is faster than working within it. The rule survives on paper and dies in practice the first time it's not enforced.
- **Owning code (or data) you didn't build.** Inheriting a domain nobody can fully explain isn't a promotion — without support, it becomes debt with your team's name on the pager.

## How to succeed

1. Define domains around durable business functions, not around whichever team happens to hold them today — a domain should be handed over intact, not reverse-engineered by whoever inherits it.
2. Make ownership handoff an explicit checklist item in any reorg process, with a real deadline, not an assumption that it'll sort itself out.
3. Pair any distribution of ownership with a distribution of standards: shared definitions of data quality, documentation expectations, and what "trustworthy" means before you hand teams the keys.
4. Enforce boundary rules consistently, especially the first time someone with leverage wants an exception — that's the moment that decides whether the rule is real.
5. Be honest about organizational maturity before adopting mesh-style ownership. A platform with strong central governance beats a decentralized one with none, even though decentralized sounds more advanced.

## See also

- [Scaling the platform](./scaling-the-platform.md) — how ownership models need to evolve as headcount grows
- [Governance & trust](./governance-and-trust.md) — the standards that have to travel with distributed ownership
- [Data warehouse: governance & access](../data-warehouse/governance-and-access.md) — where ownership meets access control in practice
