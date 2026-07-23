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

## Entry 2 — planner (2026-07-23T16:25:57)

**Reference files fetched:**
- (none)

**Reference files recommended by Planner:**
- stack-docs/Authoring/Inputs/Multiple_choice_input.md

```text
This locks in nicely. Here's the full plan:

GOAL (non-negotiable): Test the full one-mean two-tailed hypothesis-test workflow (SE → hypotheses → t-score → approximate P-value via the 68-95-99.7 rule → decision) using the Eagle Boys pizza-diameter scenario, with randomised sample statistics and follow-through marking so a student who propagates an early slip consistently is credited for correct reasoning rather than penalised twice.

STRUCTURE (non-negotiable):
1. **Standard error**: compute SE = s/√n from randomised x̄, s, n (stated in the stem).
2. **Hypotheses**: state H0: μ = 12 vs H1: μ ≠ 12 (μ fixed, not randomised).
3. **t-score**: compute t = (x̄ − 12)/SE, using the student's own SE from Part 1 (follow-through).
4. **Approximate P-value bucket**: choose the correct 68-95-99.7-rule range, matched against the student's own t-score from Part 3 (follow-through), not the teacher's t.
5. **Decision**: reject/fail-to-reject H0 at α = 0.05 (stated explicitly in the stem), following from the student's own bucket answer from Part 4 (follow-through).
6. **Validity check** (independent, not part of the follow-through chain): is n large enough for the CLT here? Graded against the actual randomised n (always "yes" since n stays >25).

RANDOMIZATION:
- n ∈ {100, 125, 150, 200}.
- s ∈ [0.20, 0.30] (modest spread).
- Bucket weights: 50% |t|≥3 ("P<0.003", reject), 20% 2≤|t|<3 ("0.003<P<0.05", reject), 15% 1≤|t|<2 ("0.05<P<0.32", fail to reject), 15% |t|<1 ("P>0.32", fail to reject).
- Within the chosen bucket, pick t comfortably away from its boundary (avoid within 0.1 of 1, 2, 3) so rounding x̄ never crosses buckets.
- x̄ = 12 + t·SE (t negative — "pizzas run small"), rounded to 3 dp for display.

ANSWER TESTS:
- Part 1: numeric, relative/absolute tolerance on SE.
- Part 2: equation/expression input(s) for H0 and H1, AlgEquiv.
- Part 3: numeric tolerance, computed from the *student's* Part-1 SE (follow-through), not the teacher's SE.
- Part 4: MCQ/dropdown of the four P-value ranges, correctness judged against the student's own Part-3 t-score.
- Part 5: MCQ (reject/fail to reject), correctness judged against the student's own Part-4 bucket answer.
- Part 6: MCQ/true-false, graded against actual n.

FEEDBACK: Worked solution shows the book's method (SE formula, two-tailed rationale, 68-95-99.7 lookup, decision rule at α=0.05) using the actual randomised numbers. Worth flagging as common mistakes: SE computed as s/n instead of s/√n; sign error or using μ−x̄ instead of x̄−μ in t; one-tailed reasoning error (picking H1: μ<12 given "smaller than claimed" framing, when the RQ is genuinely two-tailed "or not").

PRT/QTEST SUGGESTIONS: Explicit correct-path qtest cases for all four buckets (not just the dominant one) and both decisions, since real coverage of the fail-to-reject path was the whole point of widening the range. Test follow-through with a deliberately wrong Part-1 SE propagated consistently through Part-3/4/5 (should still score those as correct). Test a bucket boundary case is never actually generated (confirm the "away from boundary" guard holds). Test inconsistent follow-through (e.g. right SE, wrong t, then a bucket/decision that doesn't match either) to confirm it's marked wrong rather than accidentally credited.
```

