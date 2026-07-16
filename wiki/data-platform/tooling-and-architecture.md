# Tooling & architecture

*Part of [Data platform](./README.md).*

Tooling decisions get outsized attention because they're visible and comparable — vendor A versus vendor B. They're rarely the reason a platform succeeds or fails. They're still worth getting right, because a bad fit compounds.

## Foundations

- **Architecture should follow workload, not fashion.** Warehouse-native, lakehouse, or hybrid approaches all solve real problems — the right one depends on data variety, team skillset, and query patterns, not on what's being talked about most this year.
- **Ingestion strategy (batch, streaming, CDC) is a business requirements question**, not a technical preference. It should be driven by how fresh the data actually needs to be for the decisions it supports.
- **Build vs. buy is a recurring decision, not a one-time one.** What's worth building in-house changes as the team and the platform mature.

## Common pitfalls

- **Buying the most well-known orchestration or platform tool by default**, then discovering months later that a stack of four or five other vendors had to be bought around it to make it actually work end to end.
- **Streaming everything because it's available**, when most consumers of the data only need daily or hourly freshness — paying for real-time infrastructure and operational complexity that nothing downstream actually uses.
- **Under-investing in the shared platform and forcing each team to build its own bespoke stack.** This is the most common way "distributed ownership" quietly becomes duplicated infrastructure cost, with every team solving the same ingestion and orchestration problems independently.
- **Coupling orchestration and transformation too tightly** — for example, running raw SQL scripts from a general-purpose orchestrator instead of letting a transformation tool own transformation logic and the orchestrator own scheduling and dependencies. It works until something needs debugging, at which point neither layer gives you the full picture.
- **No clear boundary between platform-provided infrastructure and team-built logic.** Without one, "who fixes this when it breaks" doesn't have an answer.

## How to succeed

1. Choose ingestion freshness (batch, micro-batch, streaming) based on what decisions actually depend on the data, not on what's technically possible.
2. Keep a clean separation of concerns: let an orchestrator own scheduling and dependencies, and a transformation tool own the transformation logic itself — that separation pays off the first time something needs debugging.
3. Invest in the shared platform layer deliberately, especially if you're distributing ownership to domain teams — the alternative is five teams independently solving the same ingestion problem, worse, five times.
4. Revisit build-vs-buy decisions periodically. A tool that was the right call at ten pipelines may not be the right call at two hundred.
5. Document the architecture's boundaries explicitly: what's shared infrastructure, what's team-owned logic, and who's responsible for each.

## See also

- [Data warehouse: architecture patterns](../data-warehouse/architecture-patterns.md) — how layering choices map onto storage and compute
- [Data engineering: orchestration](../data-engineering/orchestration.md) — the operational detail behind the architecture decisions here
