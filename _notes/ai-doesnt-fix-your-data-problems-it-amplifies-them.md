---
title: "AI doesn't fix your data problems, it amplifies them"
date: 2026-07-16
---

Before AI, a bad table had a natural predator: the analyst who queried it. They'd notice the row count looked off, ask around, remember that "oh yeah, that one's stale, use the other one." Slow, informal, entirely dependent on someone's memory — but it worked as a filter. Bad data mostly stayed contained to whoever was unlucky enough to hit it.

Point an AI agent at the same warehouse and that filter is gone. It doesn't hesitate, doesn't ask around, doesn't remember which table someone mentioned was stale in a hallway conversation two years ago. It picks whatever looks plausible, and answers with exactly the same confidence whether it's right or not.

> A wrong answer from a person comes with a shrug. A wrong answer from an AI comes with a citation.

That's the actual shift, and it's not really about AI being unreliable. It's that AI removes the one thing standing between a data quality problem and an executive's inbox: a human who might pause. The usual suspects — the undocumented table, the two versions of "active customers," the dataset nobody's owned since the last reorg — used to surface slowly, in a dashboard someone occasionally double-checked. Now they surface at the speed of a chat message, delivered with total confidence, to whoever asked the question.

The semantic layer angle makes this concrete. A well-built semantic layer exists to guarantee that "revenue" means the same thing everywhere it's asked. The moment an AI tool skips it — querying raw or half-modeled tables directly because that's what it had access to — you don't just lose that guarantee, you lose it at scale. Not one dashboard with a quietly wrong number. Every question anyone asks the AI, potentially wrong in a slightly different way each time, none of it visibly flagged as uncertain.

None of this means don't use AI on your data. It means the excuses that let "eventually" governance survive for years just ran out. A quality stamp on a dataset, a durable owner, a semantic layer that's actually enforced instead of optional — these were always the right answer, and until now, most orgs could get away with skipping them because the blast radius of skipping them was small and slow. AI doesn't create that need. It just removes the last thing that was quietly protecting you from it.

Think of AI as a magnifying glass held over the data platform you already have, not a fix for it. It doesn't care whether what it's magnifying is the well-modeled, well-owned mart your platform team is proud of, or the abandoned table nobody's touched since the last reorg. It just makes whatever's actually there visible, faster and to more people, than anything that came before it.
