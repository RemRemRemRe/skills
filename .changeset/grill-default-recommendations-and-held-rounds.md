---
"mattpocock-skills": patch
---

grilling, batch-grill-with-docs: an unanswered question now takes its recommendation, and a round is held until every lookup that could change one of its questions has reported.

- An unanswered question settles at its recommendation, so a round waits only on its **blocking** questions: a decision that changes an interface or observable behaviour, is hard to reverse, or overturns something already settled. The round says which questions those are. The default settles individual questions, never the plan: implementation still waits for an explicit go.
- A round is held until every lookup that could change a question has reported, because a question asked before its facts arrive may be the wrong question and rounds scattered by late lookups are harder to read and answer. A lookup that can no longer change any question may stay in flight.
