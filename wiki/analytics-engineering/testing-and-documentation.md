# Testing & documentation as a practice

*Part of [Analytics engineering](./README.md).*

A model without tests or documentation isn't necessarily wrong — it's just unverifiable, which downstream is functionally the same thing. Nobody can tell the difference between "correct and untested" and "wrong and untested" until it's too late.

## Foundations

- **Tests belong at the model level**, checking exactly the things that should always be true: uniqueness of a key, non-null on a required field, referential integrity to a related model, accepted values within a known set.
- **Documentation is part of the deliverable**, not a follow-up task — a model's purpose, its grain, and any non-obvious logic should be written down by whoever built it, while the reasoning is still fresh.
- **CI should run tests automatically** on every change, using state-aware selection (test what changed and its downstream dependents) once project size makes a full run slow.

## Common pitfalls

- **Testing only the easy things.** Uniqueness and not-null tests are simple to add and genuinely useful, but stopping there misses the business-logic bugs that actually cause incidents — a join that silently fans out, a filter that quietly drops a segment.
- **Documentation written after the fact, by someone who didn't build the model.** By the time documentation happens as a separate cleanup task, the person doing it is often guessing at intent rather than recording it.
- **Tests that get silently skipped or excluded when they start failing**, instead of being fixed or the underlying issue addressed — a disabled test is worse than no test, because it advertises coverage that isn't real.
- **No test for the specific bug that already happened once.** Incidents are free test cases — if a wrong number shipped once because of a bad join, the fix isn't complete until there's a test that would have caught it.
- **Treating documentation as prose no one reads**, instead of structured, discoverable metadata (column descriptions, model descriptions) that surfaces directly in the tools people already use to explore data.

## How to succeed

1. Write tests that check business assumptions, not just schema mechanics — the constraints that, if violated, mean something is actually wrong.
2. Require documentation as part of the same pull request that adds or changes a model, written by the person who has the context, not assigned later to someone who doesn't.
3. Run tests automatically in CI on every change, and treat a newly failing test as a signal to investigate, never as friction to route around.
4. Turn every real incident into a permanent test — the fix isn't done until the failure mode can't silently recur.
5. Keep documentation structured and close to the model (descriptions, not separate wiki pages) so it surfaces where people are actually looking: in the catalog, in the BI tool, in the model itself.

## See also

- [Transformation layer (dbt)](./transformation-layer-dbt.md) — the models this testing and documentation practice applies to
- [Data engineering: testing & CI/CD](../data-engineering/testing-and-cicd.md) — the same discipline applied earlier in the pipeline
