# Blog backlog

## Series: Data platforms

A four-part series on why data platforms don't solve the problems people buy them for, and what actually helps.

Storytelling approach: promise and overdeliver, like Mark Rober — open with the claim, then earn it.

### Post 1: One platform doesn't solve your data problem — status: drafted

Angle: buying/building a data platform doesn't remove your underlying data problems, it trades them for a new set.

Key points:
- A platform promises to solve everything, but introduces its own new problems
- The flexibility that makes a platform useful is the same thing that creates mess
- "Data mesh" often becomes "data mess" in practice

Avoid: don't get into governance or ownership here (that's post 3), don't get into specific tooling (that's post 4).

### Post 2: Making a functional data platform is not a technical problem

Angle: the hard part of a data platform isn't the tech stack, it's the organization around it.

Key points:
- Problems scale with org size, not with data volume. Small organization, people know the available datasets. With bigger organizations, people tend to stick to their familiar branch, and datasets easily become duplicated with different colors.
- What "functional" means changes as the org grows — a platform that works for one team breaks down across ten
- Where the data-mesh idea already assumes an organizational maturity most orgs don't have
- the vision should be to build datasets hence data domains - often (unfortunatley) managed by one team - which lasts and lives healty also after an org change. Domains could be a database, schema, dbt project, etc.

Avoid: don't repeat post 1's "platform doesn't solve everything" framing, take it as given and move on.

### Post 3: Flexibility vs governance — where to draw the line

Angle: every platform sits somewhere on a flexibility/governance spectrum, and most orgs default to the wrong end without deciding on purpose.

Key points:
- Who should own a data product — the data engineer who builds it, or the business stakeholder who needs it?
- Is a data product one dataset or a bundle of related ones? This decision is a governance choice, not a technical one
- Need for a quality "stamp" on a data product before others can trust and reuse it
- What you gain and lose at each end of the spectrum — be concrete, not both-sides-y

Avoid: don't resolve this into a single "best practice," the point is that it's a real trade-off.

### Post 4: Practical thoughts on scaling

Angle: grounded, example-driven follow-up — what does dealing with the scaling problem actually look like.

Key points:
- Is bronze/silver/gold (e.g. Matillion's medallion pattern) practically sufficient, or does it fall short in practice?
- NBIM as a reference case: raw → int → mrt, with dbt

Avoid: keep this concrete and example-led, it's the payoff post after three posts of framing.

## Standalone posts (not part of a series)

### AI doesn't fix your data problems, it amplifies them — status: drafted

Angle: layering AI (copilots, agents, natural-language analytics) on top of a data platform doesn't fix the underlying data problems, it removes the human buffer that used to quietly absorb them, so the same rot now surfaces faster, more confidently, and to a wider audience.

Key points:
- An analyst who hits a shady table usually hesitates, caveats, or asks around. An AI agent doesn't — it picks a plausible-looking table and answers with full confidence, at the speed of a chat message
- This turns old, slow-burning failure modes ("I don't know where this number came from") into fast, wide-blast-radius ones ("the AI told the exec team a confidently wrong number in a meeting")
- AI tools that bypass a semantic layer and query raw/intermediate models directly reintroduce the exact inconsistency a semantic layer exists to prevent — just faster and to more people
- The preconditions that make a platform trustworthy (durable ownership, a quality stamp, real governance) stop being "nice to have eventually" and become urgent the moment AI starts querying broadly
- Framing: AI is a magnifying glass on the data platform, not a fix for it — it makes existing quality visible at a scale and speed nothing before it did

Avoid: don't make this a generic "AI and data quality" listicle — keep it specifically about how AI changes the *shape* and *speed* of data platform failure modes. Don't frame it as part of the data platforms series.

## Idea bank (unsorted, not yet assigned to a post)

- How do you actually choose the right dataset in the first place? (practical checklist: owner, description, modeled vs. raw, lineage/usage, tests, freshness — but the checklist itself is a symptom, not a fix; ties to post 2's ownership and post 3's quality stamp)
