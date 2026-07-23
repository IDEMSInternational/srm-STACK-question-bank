# Metadata — hypothesis-tests/pizzas_ht/pizzas_ht.xml

Running record of every agent (and user) action on this question that
isn't the XML itself: the reasoning, findings, improvement notes, and
reference lookups behind each change. Entries are appended in order,
newest at the bottom. The XML changes themselves are recorded by git —
this file holds the substance and meaning behind them, not the diffs.

## Entry 1 — concierge (2026-07-23T15:14:27)

**Issue:**
- #2

**Reference files fetched:**
- (none)

```text
Question reserved as part of issue #2.
```

## Entry 2 — author · attempt 1/3 (2026-07-23T16:31:50)

**Reference files fetched:**
- stack-docs/Authoring/Inputs/Multiple_choice_input.md

```text
STACK API check: PASSED

All checks passed.

Deviations reported: - STRUCTURE (non-negotiable) plan item 2 asks for H0/H1 as "equation/expression input(s)" without specifying one vs two inputs; I split into two separate algebraic inputs (ans2 for H0, ans3 for H1) rather than one combined input, because a single input can't cleanly hold two separate equations for independent AlgEquiv grading and clear per-part feedback placement. This is a minimal implementation choice within a negotiable detail of a non-negotiable structural item.
- Flagging for Reviewer (per the NOTE on equations vs expressions): Part 2's inputs expect equations (`mu=12`, `mu#12`); a student typing a bare expression instead should get diagnostic feedback rather than generic "incorrect" — this is a PRT-branch decision left to Reviewer, not something I implemented myself.
- Flagging for Reviewer: Parts 3–5 need genuine follow-through PRT logic (recomputing the expected t-score from the student's own Part-1 SE, the expected bucket from the student's own Part-3 t, and the expected decision from the student's own Part-4 bucket) as specified in the plan's ANSWER TESTS section — this is real PRT authorship outside my scope, so I've only supplied ANSWERTEST choices and teacher answers based on the randomised teacher path.
```

