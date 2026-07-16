# Pipeline reliability & observability

*Part of [Data engineering](./README.md).*

A pipeline that's never failed hasn't been proven reliable — it's just been lucky, or not yet observed closely enough. Reliability is a property you design in, not one you discover by waiting.

## Foundations

- **Idempotency**: running a pipeline once or ten times on the same input produces the same result. This is what makes retries, backfills, and replays safe rather than terrifying.
- **Observability** means logs, metrics, and lineage across every pipeline component — not just a success/failure flag. Metadata about execution status, dependencies, and performance is what turns "the pipeline broke" into "the pipeline broke here, for this reason."
- **Error handling that assumes partial failure.** Pipelines should be able to run multiple times without duplicating or corrupting data, using stable identifiers to deduplicate and job-state or audit tables to track what actually completed.

## Common pitfalls

- **No idempotency, so every failure requires manual cleanup.** A job that partially completes and then gets re-run duplicates records or leaves the target in an inconsistent state — and the fix becomes a one-off investigation instead of "just run it again."
- **Monitoring that only reports success or failure, with no detail.** When something breaks, the on-call engineer's first hour is spent figuring out *what* broke before they can even start fixing it.
- **Silent partial failures.** A pipeline that "succeeds" but only processed half its input is often worse than one that fails loudly — the bad data quietly ships to a dashboard, and someone downstream discovers it days later.
- **Alerting that trains people to ignore it.** Alerts with no clear severity or no clear owner get muted, and the one alert that mattered gets muted along with the noise.
- **No write-audit-publish pattern for critical outputs.** Without staging a run's output separately before promoting it, a partial or bad run can pollute a "gold" or production table before anyone notices.

## How to succeed

1. Build idempotency in from the start: stable keys for deduplication, and job-state or audit tables that track exactly what a given run touched.
2. Instrument pipelines with logging, metrics (latency, success/failure rate, row counts), and lineage — treat this as part of the pipeline, not an add-on.
3. Fail loudly and specifically. A pipeline that stops and clearly reports "source X returned zero rows" is far more useful than one that silently ships an empty result.
4. Route alerts to a specific owner with a clear severity, and periodically prune alerts that don't warrant action — an ignored alert channel is a reliability risk in itself.
5. Use write-audit-publish (stage, validate, then promote) for anything feeding a production-facing table, so a bad run never directly overwrites what people already trust.

## See also

- [Orchestration](./orchestration.md) — retries, circuit breakers, and where reliability logic actually lives
- [Ingestion & integration](./ingestion-and-integration.md) — reliability concerns specific to getting data in the door
- [Testing & CI/CD](./testing-and-cicd.md) — catching problems before they reach production at all
