---
name: batch-grill-with-docs
description: "Batch-grill a plan or design by its current decision frontier: all resolvable questions per round with recommended answers and close-call scores, glossary capture, selective ADRs, pre-mortem on irreversible calls."
---

# Batch Grill with Docs

Interview the user relentlessly until you reach a shared understanding, and capture the results as docs as you go. Model the plan as a decision graph: decisions are nodes, and their prerequisites are dependencies.

Explore the repository, source, and available tools before asking anything. Resolve queryable facts yourself; surface missing evidence instead of asking the user to supply facts. For a frontier question that needs real investigation, dispatch a sub-agent to find it — never ask the user for anything you could look up yourself. Don't block on it: a running exploration is an unsettled prerequisite, so only the questions downstream of it wait for the report; ask the rest of the frontier now. Rendezvous every dispatched lookup before you synthesize or act.

Before each round, recompute the **frontier**: every unresolved decision whose prerequisites are resolved. Ask all mutually independent frontier questions in one numbered batch, with your recommended answer and its reason for each, then wait for the user's reply. Format each question as in `grilling`, putting your recommended option first; on genuinely close or high-stakes calls, score each option 0.0–10.0 and aim for a 9.0+ recommendation — skip the scores on clear-cut questions. Keep coupled questions in dependency order; a question whose answer depends on one still open in this round belongs to a later round.

Resolve clear answers, retain omitted questions, turn ambiguity or contradiction into a decision, and add any newly revealed dependencies. Recompute the frontier after every reply. Accept all recommendations only when the user says so explicitly.

Run the `domain-modeling` discipline throughout. When a term is confirmed, write it immediately to the correct-scope `CONTEXT.md` as glossary language, without implementation details. Create an ADR only when the decision is hard to reverse, reflects a real trade-off, and needs its reason preserved for future maintainers. When a settled decision is high-stakes or hard to reverse, offer a `pre-mortem` on it before moving on.

When no unresolved decision or evidence blocker remains, summarize the proposed consensus and ask for explicit confirmation — the last batch answer is not confirmation by itself. Offer a full `pre-mortem` on the settled plan before handing back. Do not implement the plan before confirmation; afterward, implement only if the user's request authorized it.

Stop only when consensus is explicit, confirmed terms and qualifying ADRs are written, every dispatched lookup has rendezvoused, and no unauthorized implementation has begun.
