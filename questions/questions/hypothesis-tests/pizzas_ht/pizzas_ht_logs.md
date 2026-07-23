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

## Entry 2 — author · attempt 1/3 (2026-07-23T16:27:01)

**Reference files fetched:**
- (none)

```text
STACK API check: FAILED

Render failed: Error rendering input: The model answer field for this input is malformed: <code>"P < 0.003"</code>. ,The teacher did not indicate at least one correct answer.
```

## Entry 3 — author · attempt 2/3 (2026-07-23T16:27:50)

**Reference files fetched:**
- stack-docs/Authoring/Inputs/Multiple_choice_input.md
- stack-docs/Authoring/Inputs/index.md

```text
STACK API check: PASSED

All checks passed.

Deviations reported: - Plan section "ANSWER TESTS" (negotiable): changed Parts 4/5/6 from `String` to `CasEqual`, and rebuilt their model answers as proper MCQ `[[value, correct, display], ...]` lists (per STACK's MCQ input requirements) instead of plain strings — the plain-string model answer was the actual cause of the confirmed render failure ("model answer field is malformed... did not indicate at least one correct answer"), since dropdown/radio inputs require this specific list structure, not a bare CAS string. Also added `tac_bucket`/`tac_decision`/`tac_validity` question variables (the correct atom values) for Reviewer's follow-through PRT logic, since the MCQ value type changed from strings to atoms/integers.
```

