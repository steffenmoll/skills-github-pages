---
title: "How do you actually choose the right dataset in the first place?"
date: 2026-07-16
---

*This is the fifth post in a series on data platforms. If you haven't, <a class="internal-link" href="/one-platform-does-not-solve-your-data-problem">read part 1</a> first.*

You open the catalog, search for "customers," and get seven results. `customers`, `dim_customers`, `customers_v2`, `active_customers`, one in a schema called `legacy_do_not_use` that half the company still queries anyway, and two with no description at all. You have a dashboard due this afternoon. Which one do you pick?

Most people pick by vibes. Whichever name sounds most official, whichever one a colleague mentioned once, whichever one shows up first in autocomplete. Then they build on it, and three months later someone asks why their number doesn't match finance's number, and the answer turns out to be "we queried different tables that were both plausibly called customers."

> The table doesn't tell you it's wrong. It just answers.

That's the actual danger. A missing table throws an error. A wrong table returns a perfectly reasonable-looking number, and nothing about the query result tells you it came from the stale, half-abandoned version. You only find out later, usually in a meeting, usually at the worst possible moment.

So here's the practical version, the checklist I actually use: Is there a named owner, and are they still at the company? Does it have a description that explains what a row *is*, not just what columns exist? Is it downstream of a modeled layer (marts, not raw staging) — because raw tables reflect a source system's opinion of the world, not the business's? Does anything reputable already query it — check lineage, not vibes? Are there tests on it, and are they passing? Is there a fresher, more-queried table right next to it that makes this one look suspiciously abandoned?

None of that is exotic. It's also not what most people actually do under deadline pressure, which is the point: a checklist that only works when you have time to run it isn't solving the problem, it's just documenting how good intentions fail.

Which is why this isn't really an individual-diligence problem, and treating it as one is a category error. It's the same problem from every earlier post in this series, just arriving at the exact moment someone tries to use the platform instead of build it. Post 2's argument was that datasets need durable owners. Post 3's argument was that a data product needs a quality stamp before anyone can trust it on sight. Both of those, done properly, are what make the checklist above unnecessary — because the answer to "which one do I use" should be visible without investigation: one canonical table, clearly labeled, with a stamp that means something, and the six near-duplicates either deleted or clearly marked as deprecated.

If your organization can't tell an analyst which of seven "customers" tables is the real one without them reverse-engineering it from lineage and vibes, that's not a discovery problem to solve with a better search bar. It's a governance problem the platform was supposed to solve back at post 1, showing up again with a different face. The clutter didn't go away. It just waited for someone to go looking for a table.
