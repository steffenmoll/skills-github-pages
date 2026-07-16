# Scaling the platform

*Part of [Data platform](./README.md).*

Scaling a data platform isn't mainly about data volume — most warehouses handle a lot more data than they handle organizational complexity gracefully. The thing that actually breaks first is the number of people who need to understand and trust what's there.

## Foundations

- **What "works" changes with headcount, not with terabytes.** A setup that's functional for one team is often unworkable, unchanged, across ten — not because the technology stopped scaling, but because the implicit knowledge that held it together (who owns what, what already exists) stopped scaling.
- **Discoverability degrades before quality does.** At small scale, everyone knows what datasets exist. At larger scale, teams that can't find an existing dataset rebuild it — same numbers, slightly different logic, different name — not out of carelessness, but because finding the original was harder than writing a new query.
- **Governance and self-service pull in opposite directions**, and scaling means managing that tension deliberately rather than defaulting to one extreme.

## Common pitfalls

- **Assuming the platform that worked at N people will work at 10N.** The org outgrows the implicit coordination that used to substitute for explicit process, and nobody planned the transition.
- **Duplicate datasets as a symptom, treated as a cause.** Teams rebuilding "active customers" for the third time isn't a training problem — it's a discoverability and ownership problem, and training doesn't fix either.
- **Self-service without guardrails.** Opening up broad access and tooling to move fast is exactly the decision that, six months later, produces the clutter nobody set out to create.
- **Scaling technology before scaling process.** Bigger compute and more storage don't address the actual bottleneck once the constraint has shifted from "can we process this data" to "can anyone find and trust this data."
- **No visible catalog or map of what exists.** Without one, tribal knowledge is the discovery mechanism, and tribal knowledge doesn't scale past the size of a team that eats lunch together.

## How to succeed

1. Invest in discoverability before it becomes the bottleneck: a catalog, clear naming conventions, and documented ownership, so finding an existing dataset is easier than rebuilding it.
2. Revisit "what does functional mean" explicitly at each growth stage, rather than assuming last year's definition still holds.
3. Pair any expansion of self-service with a corresponding expansion of governance — the two need to scale together, not one after the other.
4. Treat duplicate datasets as a signal to fix discovery and ownership, not as a one-off cleanup task.
5. Plan the transition from implicit to explicit coordination deliberately, ideally before a specific headcount or reorg forces it on you reactively.

## See also

- [Organization & ownership](./organization-and-ownership.md) — the ownership model that has to hold as the org grows
- [Data warehouse: performance & cost](../data-warehouse/performance-and-cost.md) — the cost side of scaling, which needs the same deliberate guardrails
