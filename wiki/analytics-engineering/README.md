# Analytics engineering: foundations & how to succeed

Analytics engineering is the discipline of turning raw, ingested data into models and metrics people can actually trust — the layer between "data exists in the warehouse" and "a stakeholder can make a decision with it." It emerged as its own discipline precisely because that gap used to fall into a crack between data engineering and analytics, owned properly by neither.

## Foundations

- **Modularity and reuse over one-off SQL.** Staging → intermediate → marts isn't a naming convention, it's a discipline for avoiding the same business logic being redefined five times in five different dashboards.
- **Testing and documentation are part of the model, not an afterthought appended to it.** A model without tests or documentation is a model nobody downstream can trust without independently re-verifying it.
- **A semantic layer** — a single, reusable definition of metrics, dimensions, and entities — is what keeps "active customers" meaning the same thing in every dashboard, every AI copilot, and every analyst's ad hoc query.
- **Analytics engineers sit between data engineers and analysts/stakeholders**, and the discipline only works if that connective role is respected, not treated as "SQL analyst" or "junior data engineer" by another name.

## Common pitfalls

- **One-off SQL duplicated across dashboards.** Without a shared modeling layer, "revenue" gets computed slightly differently in five places, and nobody notices until two of them disagree in the same meeting.
- **Skipping tests because "it's just a transformation."** Transformation logic is exactly where subtle bugs hide — a join that fans out rows, a filter that silently excludes an edge case — and it's cheaper to catch with a test than in a stakeholder's inbox.
- **A semantic layer treated as a one-time setup instead of critical infrastructure.** Poorly maintained semantic models degrade in performance and trust exactly like any other production system, because that's what they are.
- **Analytics engineers doing the work but not owning the decisions.** If data engineers or analysts unilaterally change upstream sources or downstream requirements without looping in the team building the model layer, the models drift out of sync with both ends.
- **No agreed vocabulary between roles.** Data engineers, analytics engineers, and analysts using different words for the same concepts is a small friction that compounds into real miscommunication at scale.

## How to succeed

1. Build a real modeling layer — staging, intermediate, marts — and route all business logic through it rather than letting it accumulate in individual dashboards.
2. Treat tests and documentation as required parts of shipping a model, not optional polish added if time allows.
3. Invest in a semantic layer once more than a couple of dashboards need the same metrics, and maintain it with the same rigor as any other production system.
4. Give analytics engineers real ownership of the transformation layer, with a seat in decisions that affect it from either side (source changes, new reporting requirements).
5. Establish and write down shared vocabulary — what a "metric," a "dimension," and an "entity" mean in your stack — so the same word means the same thing to everyone using it.

## Pages in this section

- [Transformation layer (dbt)](./transformation-layer-dbt.md) — modularity, staging/intermediate/marts, and DRY modeling
- [Testing & documentation](./testing-and-documentation.md) — making trust verifiable, not just assumed
- [Semantic layer & metrics](./semantic-layer-and-metrics.md) — one definition of a metric, everywhere it's used
- [Collaboration & workflow](./collaboration-and-workflow.md) — how analytics engineers work with data engineers and analysts

## See also

- [Data warehouse: data modeling](../data-warehouse/data-modeling.md) — the modeling foundations this layer builds on top of
- [Data platform: governance & trust](../data-platform/governance-and-trust.md) — where model-level trust meets organizational governance
