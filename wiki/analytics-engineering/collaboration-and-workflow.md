# Collaboration & workflow

*Part of [Analytics engineering](./README.md).*

Analytics engineering exists in the gap between data engineering and the people asking business questions. That gap is exactly where the discipline adds value — and exactly where it gets squeezed if the surrounding roles aren't clearly defined.

## Foundations

- **Analytics engineers translate between two different worlds**: the data engineer's concern with reliable, well-structured raw data, and the analyst's or stakeholder's concern with a trustworthy, understandable answer to a business question.
- **A shared vocabulary has to exist across roles** — what a "metric," "dimension," "model," and "source" mean should be the same word for the same thing whether a data engineer, analytics engineer, or analyst is using it.
- **Requirements flow in both directions.** Reporting needs pull from analysts and stakeholders; structural constraints and source changes push from data engineering. Analytics engineering sits in the middle of both flows, not downstream of just one.

## Common pitfalls

- **Analytics engineers treated as "SQL analysts" or "junior data engineers."** Either framing strips out the translation role that makes the discipline valuable, and turns it into ticket-taking from whichever side has more organizational leverage.
- **Upstream changes made without looping in analytics engineering.** A data engineering team changes a source schema, or an analyst changes a reporting requirement, without involving the team maintaining the model layer in between — and the models drift out of sync with both ends simultaneously.
- **No agreed definition of terms across roles.** "Model" means one thing to a data engineer and something else to an analyst; without a shared glossary, every cross-team conversation starts by re-litigating vocabulary before it can get to substance.
- **Analytics engineering as a queue, not a partnership.** Requests come in, models come out, with no feedback loop about whether the requirement was actually well-formed or whether the underlying data supports it.
- **Stakeholder requirements taken at face value without checking against what the data can actually support.** Building exactly what was asked for, when what was asked for doesn't match what the source data can reliably provide, produces a model that's technically delivered and practically wrong.

## How to succeed

1. Give analytics engineering a real seat in decisions on both sides — source schema changes on one end, new reporting requirements on the other — not just the output of both.
2. Build and maintain a shared glossary of core terms (metric, dimension, entity, model) so cross-team conversations don't restart at vocabulary every time.
3. Establish a lightweight, two-way feedback loop: analytics engineers should be able to push back on a requirement that doesn't match what the data supports, not just execute it as specified.
4. Route structural changes (new sources, schema changes, new reporting needs) through analytics engineering rather than letting either side change things unilaterally and expecting the model layer to silently absorb it.
5. Protect the role's scope explicitly — analytics engineering is neither "just SQL" nor "just data engineering," and treating it as either erodes the exact value it's meant to add.

## See also

- [Transformation layer (dbt)](./transformation-layer-dbt.md) — the actual work this collaboration produces
- [Data platform: organization & ownership](../data-platform/organization-and-ownership.md) — the broader organizational patterns this role sits inside
