# Testing & CI/CD for data pipelines

*Part of [Data engineering](./README.md).*

Application engineering settled the "should we test and automate deployment" debate years ago. Data teams are still catching up, mostly because a bad pipeline deploy fails quietly in a dashboard instead of loudly in a stack trace.

## Foundations

- **Pipelines should go through the same lifecycle as application code**: version control, code review, automated tests, and CI/CD — manual, ad hoc deployment to production is a reliability risk regardless of how experienced the person doing it is.
- **Data tests fall into a few core categories**: schema tests (types, nullability, uniqueness), referential integrity (foreign keys resolve), and business-logic tests (the numbers make sense given known constraints).
- **State-aware CI** (comparing a proposed change against production's current state) makes it possible to test only what actually changed and its downstream dependents, instead of rebuilding an entire project on every change.

## Common pitfalls

- **No tests at all, because "the data is different every time."** Data does vary, but schema shape, referential integrity, and known business constraints (a percentage between 0 and 100, a total that shouldn't go negative) are stable and absolutely testable.
- **Full rebuild-and-test on every pull request**, which on a large project can take 30+ minutes and burn significant warehouse compute for a change that touched two models — this cost alone causes teams to skip CI rather than fix it.
- **State comparisons that go stale.** Deferring to a "production" state for CI works cleanly with one deploy job and infrequent merges; with high merge volume or multiple busy environments overwriting the same state artifact, CI can silently compare against outdated state and produce confusing results.
- **Manual production deploys "just this once."** Every pipeline incident retrospective that includes the phrase "someone pushed directly to prod" is describing a process gap, not a one-off mistake.
- **Documentation as a separate, deprioritized task**, disconnected from the code review that would have caught it going stale.

## How to succeed

1. Apply the same CI/CD discipline data teams would expect from an application team: pull requests, review, automated tests, and a defined deployment process — no direct-to-production changes.
2. Write tests for what's actually stable: schema, referential integrity, and known business constraints — don't skip testing just because raw values vary.
3. Adopt state-aware, "test only what changed" CI once project size makes full rebuilds slow or expensive, and keep the state artifact fresh enough that comparisons stay meaningful under your team's actual merge frequency.
4. Treat documentation as part of the change, reviewed in the same pull request as the code — not a follow-up task that quietly never happens.
5. Make production deploys boring: automated, consistent, and logged, so "who changed this and when" is always answerable.

## See also

- [Pipeline reliability & observability](./pipeline-reliability-and-observability.md) — what testing is trying to prevent in the first place
- [Analytics engineering: testing & documentation](../analytics-engineering/testing-and-documentation.md) — the same discipline applied specifically to transformation models
