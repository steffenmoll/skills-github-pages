# Orchestration

*Part of [Data engineering](./README.md).*

Orchestrator choice gets debated far more than it deserves. The bigger risk is almost always what gets built *around* the orchestrator, not which one you picked.

## Foundations

- **Task-centric vs. asset-centric orchestration** are the two dominant paradigms. Task-centric tools (e.g. Airflow) model workflows as DAGs of tasks and dependencies. Asset-centric tools (e.g. Dagster) center on the data assets themselves — their inputs, outputs, and relationships — which tends to give better native lineage.
- **Separation of concerns matters more than the tool.** Transformation logic belongs in a transformation tool; the orchestrator's job is scheduling, dependencies, and coordination — not embedding SQL or business logic directly in orchestration code.
- **Infrastructure as code applies to orchestration too**: workflows in version control, changes via pull request, deployment via CI/CD — the same discipline expected of any other production system.

## Common pitfalls

- **Buying the most well-known tool by default and building a stack of other vendors around it within months** to cover gaps it didn't fill — the tool choice wasn't wrong so much as made without a clear picture of everything it needed to integrate with.
- **Running transformation logic directly from the orchestrator** (e.g. raw SQL scripts via a generic operator) instead of delegating to a dedicated transformation tool — it works until something needs debugging, and then neither the orchestrator nor the transformation layer gives a complete picture.
- **No retry or backoff strategy**, so a transient failure (a flaky API, a momentary network blip) becomes a full pipeline failure requiring manual intervention instead of a routine, automatic retry.
- **Treating the orchestrator as a black box**, with no lineage or dependency visibility — when something breaks, nobody can quickly answer "what does this feed, and what feeds it."
- **Orchestration configuration that lives outside version control**, changed directly in a UI — no review trail, no rollback, and no way to know who changed what and why.

## How to succeed

1. Choose an orchestration paradigm (task-centric or asset-centric) based on whether asset lineage and dependency visibility matter most to your stack, or whether broad ecosystem support and an existing platform team matter most.
2. Keep transformation logic in a transformation tool and let the orchestrator own scheduling and dependency coordination — resist the shortcut of embedding SQL directly in orchestration code.
3. Build automatic retries with backoff for transient failures, and reserve human alerting for failures that actually need a human.
4. Treat orchestration definitions as code: version-controlled, reviewed via pull request, deployed through CI/CD, same as any other production system.
5. Invest in lineage and dependency visibility early — it's the difference between a five-minute diagnosis and a half-day one when something breaks.

## See also

- [Pipeline reliability & observability](./pipeline-reliability-and-observability.md) — the reliability properties orchestration needs to support
- [Data platform: tooling & architecture](../data-platform/tooling-and-architecture.md) — the platform-level decisions orchestration choices sit inside
