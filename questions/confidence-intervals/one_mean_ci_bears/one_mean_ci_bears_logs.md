# Metadata — confidence-intervals/one_mean_ci_bears/one_mean_ci_bears.xml

Running record of every agent (and user) action on this question that
isn't the XML itself: the reasoning, findings, improvement notes, and
reference lookups behind each change. Entries are appended in order,
newest at the bottom. The XML changes themselves are recorded by git —
this file holds the substance and meaning behind them, not the diffs.

## Entry 1 — concierge (2026-07-23T15:16:00)

**Issue:**
- #6

**Closes on merge:**
- yes

**Reference files fetched:**
- (none)

```text
Question reserved as part of issue #6.
```

## Entry 2 — planner (2026-07-23T18:11:36)

**Reference files fetched:**
- (none)

**Reference files recommended by Planner:**
- stack-docs/Authoring/Inputs/Multiple_choice_input.md

```text
Good, that settles the last open point. Here's the full plan:

GOAL (non-negotiable): Test whether a student can execute the one-mean, large-sample z-confidence-interval pipeline (SE → margin of error → CI bounds → validity check → interpretation) on randomized data modeled on the black bear weight study, with genuine follow-through credit through the arithmetic chain and a validity check that isn't a rubber stamp.

STRUCTURE (non-negotiable):
- Non-graded stem: narrative describing the study (randomized n, x̄, s for "male bears" or similar), asking the student to mentally define the parameter and picture the sampling distribution (context only, not graded), and stating z=1.96 as the given critical value for 95% confidence.
1. Standard error of the mean (SE = s/√n) — numeric input, independently graded against the teacher's SE.
2. Margin of error (ME = z·SE) — numeric input, graded via follow-through using the student's own Part 1 answer (correct if consistent with their SE, even if their SE was wrong).
3. CI lower and upper bounds (x̄ ± ME) — two numeric inputs (or one two-part input), graded via follow-through using the student's own Part 2 answer.
4. Validity check (n ≥ 25?) — MCQ/true-false, graded independently against the actual randomized n (not follow-through — this must reflect the real n, not a propagated student error).
5. Interpretation — MCQ (radio), selecting the correctly worded confidence-interval interpretation among distractors that misstate population, parameter, or confidence-level meaning. Independent of parts 1–3 numerically (tests wording/concept, not arithmetic).

RANDOMIZATION: 
- n: wide range, e.g. drawn from a fixed list spanning clearly below and above 25 (e.g. {10,15,18,22 | 30,45,80,150,250}) — avoid values in the 20–30 zone so validity isn't a near-boundary coin flip.
- x̄: realistic adult black bear mean weight, e.g. 60–110 kg.
- s: realistic standard deviation, e.g. 30–60 kg.
All three vary independently each variant.

ANSWER TESTS:
- Part 1 (SE): numeric, relative/absolute tolerance (a few decimal places).
- Part 2 (ME): numeric, tolerance test, computed via follow-through from student's Part 1 SE.
- Part 3 (bounds): numeric, tolerance test, computed via follow-through from student's Part 2 ME (and given x̄).
- Part 4 (validity): true/false or two-option MCQ, graded against actual n≥25, independent of parts 1–3.
- Part 5 (interpretation): MCQ radio, single correct option among conceptual distractors.

FEEDBACK: 
- Part 1: flag the classic s/n vs s/√n mistake if detected.
- Part 2: flag missing/incorrect z multiplier (e.g. using 1 instead of 1.96, or using SE directly as ME).
- Part 3: flag sign errors (e.g. x̄−ME as both bounds) separately from arithmetic slips.
- Part 4: general feedback should explain *why* n≥25 matters here (CLT justifying the z-approximation), tying back to this chapter's own framework.
- Part 5: feedback distinguishing the specific misinterpretation each distractor represents (e.g. "this describes the sample, not the population," "this misstates confidence as a probability about a fixed parameter").

PRT/QTEST SUGGESTIONS: Test both a clearly-valid (large n) and clearly-invalid (small n) variant for Part 4. Test the follow-through chain explicitly with a deliberately wrong SE (e.g. forgot the square root) and confirm Parts 2–3 still award credit when consistently derived from that wrong SE. Test Part 3 with a correct SE but a sign-flipped bound to confirm it's marked wrong independent of Part 1/2 correctness. Confirm Part 4 is graded strictly off actual n and is unaffected by any earlier arithmetic errors.
```

