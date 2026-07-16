# Governance & access

*Part of [Data warehouse](./README.md).*

Governance is the part of a warehouse project that's cheapest before there's data in it and most expensive after. It's also the part most often deferred, because it doesn't block the first demo — only every demo after that.

## Foundations

- **Data classification** (what's sensitive, what's regulated, what's public-safe) has to exist before access rules can mean anything. You can't set correct permissions on data you haven't categorized.
- **Access control** should follow role and need, not follow whoever asked first or shouted loudest. Warehouse-native role-based access control (RBAC) is table stakes; row- and column-level security matter as soon as sensitive data (PII, financials) shares a warehouse with everything else.
- **Ownership** — a named person or team accountable for a dataset's correctness and access decisions — is what makes the rest of governance enforceable. Without an owner, "who approves access to this" has no answer.

## Common pitfalls

- **Governance as an afterthought, bolted on after an incident.** Waiting for a data leak, a compliance audit, or an executive asking "who can see this" before defining classification and access rules — reactive governance is always more expensive than proactive governance.
- **No classification, so everything defaults to either "wide open" or "locked down for everyone."** Both extremes come from the same root cause: nobody did the work of categorizing the data.
- **Access requests routed to whoever happens to have admin rights**, rather than to a documented owner — this is how a warehouse ends up with permissions nobody can explain or safely revoke.
- **Treating governance as purely a technical control.** RBAC without documented policy just moves the ambiguity into the permissions table instead of removing it.

## How to succeed

1. Classify data as it lands, not after the fact — bake classification into the ingestion or modeling step so it's never a separate backlog item.
2. Define access tiers before you need to enforce them: who gets what by default, and what the exception process looks like.
3. Assign an explicit owner to every dataset or domain, and make that ownership discoverable — a governance rule nobody can find might as well not exist.
4. Treat access review as a recurring process, not a one-time setup: teams change, projects end, access should expire with them.

## See also

- [Data platform: governance & trust](../data-platform/governance-and-trust.md) — governance at the organizational and cross-domain level
- [Data platform: organization & ownership](../data-platform/organization-and-ownership.md) — how domain ownership actually gets assigned and survives reorgs
