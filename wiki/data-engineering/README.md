# Data engineering: foundations & how to succeed

Data engineering is the discipline of moving data reliably from where it's produced to where it's needed, at the freshness and quality the business actually requires — no more, no less. The craft is less about clever pipelines and more about pipelines that behave predictably when something inevitably goes wrong.

## Foundations

- **Idempotency is the single most important property of a reliable pipeline.** A pipeline that produces the same result whether it runs once or ten times for the same input is a pipeline that can safely be retried, backfilled, or re-run without fear.
- **Data quality has to be validated at every stage**, not just checked once at the end — poor quality cascades through everything downstream and gets more expensive to fix the later it's caught.
- **Pipelines are software** and deserve the same rigor as application code: version control, code review, CI/CD, and tests — not one-off scripts running on someone's schedule.
- **Observability isn't optional.** Logging, metrics, and lineage across every pipeline component are what make a pipeline a system you can reason about instead of a black box you restart and hope.

## Common pitfalls

- **Non-idempotent pipelines.** Re-running a job duplicates records or corrupts state, which means every failure requires manual cleanup instead of a simple retry — this alone accounts for a large share of "why is this pipeline scary to touch" situations.
- **Poor data quality treated as someone else's problem.** Poor quality data costs real money in downstream errors and flawed decisions, and it's cheaper to catch at ingestion than to catch in a dashboard three hops downstream.
- **Pipelines as scripts, not software.** No version control, no tests, no review — changes are made directly against production because that's the only environment that exists.
- **No monitoring until something breaks in front of a stakeholder.** Without proactive alerting, pipeline failures are discovered by the people consuming the output, not the people operating the input.
- **Secrets and credentials handled casually.** Hardcoded or loosely shared credentials are a security incident waiting for a trigger, not a hypothetical risk.

## How to succeed

1. Design for idempotency from the start — stable keys, deduplication logic, and job-state tracking so any run can be safely repeated.
2. Push data quality checks as early in the pipeline as possible, and treat a failed check as a stop-the-line event, not a warning to review later.
3. Apply real software practices to pipelines: version control, code review, automated tests, and CI/CD — see [Testing & CI/CD](./testing-and-cicd.md).
4. Build observability in from day one: logs, metrics, and lineage, not just "did the job succeed or fail."
5. Use centralized secret management from the first pipeline, not after the first exposed credential.

## Pages in this section

- [Ingestion & integration](./ingestion-and-integration.md) — batch, streaming, CDC, and choosing between them
- [Pipeline reliability & observability](./pipeline-reliability-and-observability.md) — idempotency, monitoring, and error handling
- [Orchestration](./orchestration.md) — Airflow, Dagster, Prefect, and the decisions that matter more than the tool
- [Testing & CI/CD](./testing-and-cicd.md) — treating pipelines as software

## See also

- [Data warehouse](../data-warehouse/README.md) — where the data engineering output ultimately lands
- [Analytics engineering](../analytics-engineering/README.md) — the discipline that picks up where ingestion ends and transformation begins
