## What it does

`batch-grill-with-docs` interrogates a plan or design until nothing in it is left assumed, and writes the result down as it goes. It models the plan as a **decision graph**: decisions are nodes and their prerequisites are dependencies, so each **round** can ask the current **frontier**, every unresolved decision whose prerequisites are already resolved. The graph carries the observable surface too: every log line, file format, public signature, error string or console output the change alters is a node, so it belongs in a round's frontier while planning, never in a mid-flight round once implementation has started.

Its defining move is that implementation does not end the interview. Writing code is the cheapest way to discover facts, so the frontier grows back as the work proceeds: a question that turns out to be yours to decide opens a new round in the same batch format, instead of being settled by assumption or dropped in as a one-off. Alongside the interview it runs the [domain-modeling](https://aihero.dev/skills-domain-modeling) discipline, so a confirmed term lands in `GLOSSARY.md` at once and a hard-to-reverse decision becomes an ADR.

## When to reach for it

Type `/batch-grill-with-docs`, or the [agent](https://www.aihero.dev/ai-coding-dictionary/agent) reaches for it when a plan is big enough that decisions will still surface after the agreement. Reach for it inside a working directory, when the decisions need to survive the session. For the interview alone, use [grilling](https://aihero.dev/skills-grilling); for a one-shot planning grill in a codebase that leaves the same docs, use [grill-with-docs](https://aihero.dev/skills-grill-with-docs).

## Prerequisites

A working directory it can write into. Confirmed terms go to the correct-scope `GLOSSARY.md` and qualifying decisions to ADRs, so there has to be a project to keep them.

## The round, and the loop that outlives it

Each round asks all mutually independent frontier questions at once, numbered, each with the agent's recommended answer and its reason. A question whose answer depends on one still open in the round belongs to a later round, never this one. On a genuinely close or high-stakes call the options carry a 0.0 to 10.0 score.

An unanswered question takes its recommendation. Two categories are exempt and come back marked **blocking**: a decision that changes an interface or observable behaviour, is hard to reverse, or overturns something already settled. The default settles questions, not the plan, so the plan still ends at an explicit confirmation.

Facts are the agent's job, never yours. A frontier question that needs real investigation goes to a [sub-agent](https://www.aihero.dev/ai-coding-dictionary/subagent) rather than to you, and the round is held until every lookup that could change a question has reported: asking early risks asking the wrong question. A lookup that can no longer change any question may stay in flight.

Mid-implementation rounds are the normal case. Only a decision that changes an interface or observable behaviour, is hard to reverse, or overturns something already settled re-opens the interview; a local, cheaply reversible implementation choice is the agent's to make, and to report as a deviation.

## Common questions

**What if I don't answer a question?**
It stands at its recommendation. Anything blocking was labelled as blocking, and that label is the only thing that holds the round open. Silence never approves the plan.

**How is this different from `grill-with-docs`?**
`grill-with-docs` is the one-shot front door: a planning interview that leaves `GLOSSARY.md` and ADRs behind. `batch-grill-with-docs` is the same interview in batch rounds, and it stays in the loop afterwards, so decisions the code surfaces mid-build still get a round rather than an assumption.

**It kept asking questions long after we agreed the plan.**
That is the skill working, up to a point. Writing code is how the graph grows, so a question the work raised and only you can settle belongs in a round of its own. If it never stops, the scope was too big: break the work up and batch-grill the pieces.

## It's working if

- A round arrives as a numbered batch, each question with its recommended answer, and you answer only what matters to you; the rest stand as recommended.
- Anything blocking is flagged as blocking, and nothing changes an interface, proves hard to reverse, or reopens a settled decision without one.
- A round waits for its lookups instead of arriving in pieces as each report lands.
- Confirmed terms appear in `GLOSSARY.md` and hard-to-reverse calls as ADRs without you asking.
- It stops at the agreed plan and asks for confirmation before writing code.

## Where it fits

`batch-grill-with-docs` is a **reach-for-it-anytime loop**, not a single chain step: it spans the planning interview and the implementation that follows, because implementation is where the graph grows back. It sits on the same [grilling](https://aihero.dev/skills-grilling) primitive as [grill-me](https://aihero.dev/skills-grill-me) and [grill-with-docs](https://aihero.dev/skills-grill-with-docs), runs [domain-modeling](https://aihero.dev/skills-domain-modeling) as it goes, and reaches for `pre-mortem` on decisions that are hard to reverse. When you are unsure which entry point fits, [ask-matt](https://aihero.dev/skills-ask-matt) routes you.
