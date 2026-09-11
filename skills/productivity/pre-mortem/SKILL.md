---
name: pre-mortem
description: Stress-test a plan by assuming it already failed and working backwards to surface risky assumptions and irreversible bets. Use when the user wants to pre-mortem a plan or decision; offer it proactively on hard-to-reverse decisions or plans drawing only positive feedback.
---

# Pre-Mortem

Stress-test this plan before reality does. Not to kill it, but to make it survive contact with reality.

When you surface this proactively (rather than because the user asked): only do so when a decision is genuinely hard to reverse (a public API, schema migration, framework or architecture choice, a hire) or a plan is drawing only positive feedback, and raise it after you finish the user's current request, as a one-line offer. Produce the full Challenge Report only once they confirm. When the user invokes it directly, skip the offer and run it.

The technique: imagine it is 12 months from now and this plan failed. Work backwards, find why, then harden the plan against it.

Run the five-step framework in [references/pre-mortem-framework.md](references/pre-mortem-framework.md): extract the assumptions the plan needs to be true, rate each on confidence and impact-if-wrong, map the vulnerabilities (low confidence + high impact), trace the dependency chain, and test reversibility. Close with kill switches and hardening actions. The template is the definition of done: self-check the report against it — an empty KILL SWITCHES or HARDENING ACTIONS section means the analysis isn't finished, not that there is nothing to say. Never stop at the vulnerability map.

Find facts yourself rather than asking: explore the codebase and tools for what you can look up; for anything that needs real investigation, dispatch a sub-agent to research it. The risk tolerance is the user's; the facts are yours to find.

Do not treat the output as a verdict; it is a vulnerability map. Surface the risky bets so they can be validated, hedged, or accepted knowingly. Unknown risks are dangerous; known risks are manageable.
