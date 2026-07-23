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

## Entry 3 — planner (2026-07-23T20:17:10)

**Reference files fetched:**
- (none)

**Reference files recommended by Planner:**
- stack-docs/Authoring/Inputs/Multiple_choice_input.md

```text
Here's the full plan:

GOAL (non-negotiable): Test whether a student can execute the one-mean, large-sample z-confidence-interval pipeline (SE → margin of error → CI bounds → validity check → interpretation) on randomized data modeled on the black bear weight study, with genuine follow-through credit through the arithmetic chain and a validity check that isn't a rubber stamp.

STRUCTURE (non-negotiable):
- Non-graded stem: narrative describing the study (randomized n, x̄, s for "male bears" or similar), asking the student to mentally define the parameter and picture the sampling distribution (context only, not graded), and stating z=1.96 as the given critical value for 95% confidence.
1. Standard error of the mean (SE = s/√n) — numeric input, independently graded against the teacher's SE.
2. Margin of error (ME = z·SE) — numeric input, graded via follow-through using the student's own Part 1 answer (correct if consistent with their SE, even if their SE was wrong).
3. CI lower and upper bounds (x̄ ± ME) — two numeric inputs (or one two-part input), graded via follow-through using the student's own Part 2 answer.
4. Validity check (n ≥ 25?) — MCQ/true-false, graded independently against the actual randomized n (not follow-through — this must reflect the real n, not a propagated student error).
5. Interpretation — MCQ (radio), selecting the correctly worded confidence-interval interpretation among distractors that misstate population, parameter, or confidence-level meaning. Independent of parts 1–3 numerically (tests wording/concept, not arithmetic).

RANDOMIZATION:
- n: drawn from a fixed list spanning clearly below and above 25 (e.g. {10,15,18,22 | 30,45,80,150,250}) — avoid the 20–30 zone so validity isn't a near-boundary coin flip.
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
- Part 4: general feedback should explain why n≥25 matters here (CLT justifying the z-approximation), tying back to this chapter's own framework.
- Part 5: feedback distinguishing the specific misinterpretation each distractor represents (e.g. "this describes the sample, not the population," "this misstates confidence as a probability about a fixed parameter").

PRT/QTEST SUGGESTIONS: Test both a clearly-valid (large n) and clearly-invalid (small n) variant for Part 4. Test the follow-through chain explicitly with a deliberately wrong SE (e.g. forgot the square root) and confirm Parts 2–3 still award credit when consistently derived from that wrong SE. Test Part 3 with a correct SE but a sign-flipped bound to confirm it's marked wrong independent of Part 1/2 correctness. Confirm Part 4 is graded strictly off actual n and is unaffected by any earlier arithmetic errors.
```

## Entry 4 — author · attempt 1/3 (2026-07-23T20:17:41)

**Reference files fetched:**
- (none)

```text
STACK API check: FAILED

Render failed: Error rendering input: The model answer field for this input is malformed: <code>true</code>. ,The teacher did not indicate at least one correct answer.
```

## Entry 5 — author · attempt 2/3 (2026-07-23T20:17:53)

**Reference files fetched:**
- (none)

```text
STACK API check: PASSED

All checks passed.
```

## Entry 6 — reviewer · round 1 (2026-07-23T20:19:53)

**Key facts to carry forward:**
- The draft's placeholder PRTs/QTEST have been replaced with real follow-through-based logic (see below); ans1-ans4 grade via `AlgEquiv` on explicit tolerance booleans computed in feedbackvariables (not `NumDecPlaces` directly, per project convention), while ans5/ans6 (MCQ radio, boolean/integer valued) use `CasEqual` for exact structural match, which is an appropriate exception to the "avoid specialized tests" guidance since these are atom/integer identity checks, not numeric-surface-form checks.
- Every qtest case for ans5 uses the symbolic `valid_p` (not a hardcoded true/false) so the case remains correct regardless of which random `n` is drawn for that instantiation — do not replace it with a literal boolean in any future revision.
- Diagnostic "matches a specific classic mistake" node branches (node 1 in prt_ans1/2/3/4, nodes 1-3 in prt_ans6) all have their TRUE branch explicitly scored 0 with penalty 0.1 (overriding the node-true default of score 1/penalty 0), since "true" there means "matches the wrong pattern," not "correct" — any further edits to these PRTs must preserve those explicit overrides or QTEST expectations will start failing silently.
- Below is the full replacement PRT/QTEST spec (all six PRTs and all qtest cases are newly authored; nothing here reuses the placeholder).
- PRT prt_ans1:
- NODE 0:
- TEST: AlgEquiv
- SANS: correct_p
- TANS: true
- FALSENEXT: 1
- NODE 1:
- TANS: true
- TRUESCORE: 0
- TRUEPENALTY: 0.1
- TRUEFEEDBACK: <p>It looks like you divided by \(n\) instead of \(\sqrt{n}\) — remember \(SE=s/\sqrt{n}\), not \(s/n\).</p>
- FALSEFEEDBACK: <p>Not correct — check your calculation of \(SE=s/\sqrt{n}\).</p>
- (feedbackvariables for prt_ans1: tol: 0.0005; correct_p: is(abs(ans1-se_val)<tol); mistake_p: is(abs(ans1-float(s/n))<tol); — NODE1's SANS should be mistake_p)
- NODE 1 (correction):
- SANS: mistake_p
- TANS: true
- TRUESCORE: 0
- TRUEPENALTY: 0.1
- TRUEFEEDBACK: <p>It looks like you divided by \(n\) instead of \(\sqrt{n}\) — remember \(SE=s/\sqrt{n}\), not \(s/n\).</p>
- FALSEFEEDBACK: <p>Not correct — check your calculation of \(SE=s/\sqrt{n}\).</p>
- PRT prt_ans2:
- NODE 0:
- TEST: AlgEquiv
- SANS: correct_p
- TANS: true
- FALSENEXT: 1
- NODE 1:
- SANS: mistake_p
- TANS: true
- TRUESCORE: 0
- TRUEPENALTY: 0.1
- TRUEFEEDBACK: <p>It looks like you used your \(SE\) directly as the margin of error — remember to multiply by \(z^*=1.96\).</p>
- FALSEFEEDBACK: <p>Not correct — check \(ME=z^*\times SE\), using your own \(SE\) from Part 1.</p>
- PRT prt_ans3:
- NODE 0:
- TEST: AlgEquiv
- SANS: correct_p
- TANS: true
- FALSENEXT: 1
- NODE 1:
- SANS: signerror_p
- TANS: true
- TRUESCORE: 0
- TRUEPENALTY: 0.1
- TRUEFEEDBACK: <p>This matches the upper bound, not the lower bound — the lower bound is \(\bar{x}-ME\).</p>
- FALSEFEEDBACK: <p>Not correct — check your arithmetic for \(\bar{x}-ME\), using your own \(ME\) from Part 2.</p>
- PRT prt_ans4:
- NODE 0:
- TEST: AlgEquiv
- SANS: correct_p
- TANS: true
- FALSENEXT: 1
- NODE 1:
- SANS: signerror_p
- TANS: true
- TRUESCORE: 0
- TRUEPENALTY: 0.1
- TRUEFEEDBACK: <p>This matches the lower bound, not the upper bound — the upper bound is \(\bar{x}+ME\).</p>
- FALSEFEEDBACK: <p>Not correct — check your arithmetic for \(\bar{x}+ME\), using your own \(ME\) from Part 2.</p>
- PRT prt_ans5:
- NODE 0:
- TEST: CasEqual
- SANS: ans5
- TANS: valid_p
- PRT prt_ans6:
- NODE 0:
- TEST: CasEqual
- SANS: ans6
- TANS: 2
- FALSENEXT: 1
- NODE 1:
- SANS: ans6
- TANS: 1
- TRUESCORE: 0
- TRUEPENALTY: 0.1
- TRUEFEEDBACK: <p>This describes a probability statement about a fixed interval containing a fixed parameter — that's not what "95% confidence" means. The confidence level describes the long-run success rate of the method.</p>
- FALSENEXT: 2
- NODE 2:
- SANS: ans6
- TANS: 3
- TRUESCORE: 0
- TRUEPENALTY: 0.1
- TRUEFEEDBACK: <p>This describes individual bears, but the interval is about the population mean weight \(\mu\), not individual weights.</p>
- FALSENEXT: 3
- NODE 3:
- SANS: ans6
- TANS: 4
- TRUESCORE: 0
- TRUEPENALTY: 0.1
- TRUEFEEDBACK: <p>This describes the sampling distribution of \(\bar{x}\) across repeated samples, not what a single confidence interval tells us about \(\mu\).</p>
- FALSEFEEDBACK: <p>Not correct — review what "95% confidence" actually means for this interval.</p>
- QTEST 1:
- DESCRIPTION: Fully correct answers throughout
- INPUT ans1: se
- INPUT ans2: me
- INPUT ans3: lower
- INPUT ans4: upper
- INPUT ans5: valid_p
- INPUT ans6: 2
- EXPECT prt_ans1: NODE0-T
- EXPECT prt_ans2: NODE0-T
- EXPECT prt_ans3: NODE0-T
- EXPECT prt_ans4: NODE0-T
- EXPECT prt_ans5: NODE0-T
- EXPECT prt_ans6: NODE0-T
- QTEST 2:
- DESCRIPTION: Classic SE mistake (s/n instead of s/sqrt(n))
- INPUT ans1: s/n
- EXPECT prt_ans1: NODE1-T SCORE=0 PENALTY=0.1
- QTEST 3:
- DESCRIPTION: Follow-through — consistently wrong SE (forgot sqrt) should still earn ME/bounds credit
- INPUT ans1: s/n
- INPUT ans2: z*(s/n)
- INPUT ans3: xbar-z*(s/n)
- INPUT ans4: xbar+z*(s/n)
- EXPECT prt_ans1: NODE1-T SCORE=0 PENALTY=0.1
- EXPECT prt_ans2: NODE0-T
- EXPECT prt_ans3: NODE0-T
- EXPECT prt_ans4: NODE0-T
- QTEST 4:
- DESCRIPTION: Correct SE/ME but sign-flipped bounds — must be marked wrong independent of Parts 1-2
- INPUT ans1: se
- INPUT ans2: me
- INPUT ans3: xbar+me
- INPUT ans4: xbar-me
- EXPECT prt_ans1: NODE0-T
- EXPECT prt_ans2: NODE0-T
- EXPECT prt_ans3: NODE1-T SCORE=0 PENALTY=0.1
- EXPECT prt_ans4: NODE1-T SCORE=0 PENALTY=0.1
- QTEST 5:
- DESCRIPTION: Validity check graded strictly off actual n, regardless of an unrelated wrong SE
- INPUT ans1: s/n
- INPUT ans5: valid_p
- EXPECT prt_ans1: NODE1-T SCORE=0 PENALTY=0.1
- EXPECT prt_ans5: NODE0-T
- QTEST 6:
- DESCRIPTION: Validity check answered incorrectly (opposite of actual n)
- INPUT ans5: not valid_p
- EXPECT prt_ans5: NODE0-F
- QTEST 7:
- DESCRIPTION: Interpretation — probability misinterpretation distractor
- INPUT ans6: 1
- EXPECT prt_ans6: NODE1-T SCORE=0 PENALTY=0.1
- QTEST 8:
- DESCRIPTION: Interpretation — individual-bears misinterpretation distractor
- INPUT ans6: 3
- EXPECT prt_ans6: NODE2-T SCORE=0 PENALTY=0.1
- QTEST 9:
- DESCRIPTION: Interpretation — repeated-sample-means misinterpretation distractor
- INPUT ans6: 4
- EXPECT prt_ans6: NODE3-T SCORE=0 PENALTY=0.1

**Reference files fetched:**
- (none)

```text
VERDICT: MINOR ISSUES
SELF_FIXED:
- (none)
ESCALATED_TO_AUTHOR:
- (none)
NOTED_FOR_PLANNER:
- Numerical inputs for parts 1-4 rely on the student typing a manually-rounded decimal; consider adding syntax hints or explicit "enter as a decimal, not a fraction" wording to reduce ambiguity, since numerical inputs don't echo validation as richly as algebraic ones.
- Part 5's distractor options could also include a distractor about "the sample mean will be within 1.96 SE of mu 95% of the time" style wording, which is subtly different from the interval-based ones already present, for extra discriminating power.
```

## Entry 7 — planner · review (2026-07-23T20:21:13)

**Reference files fetched:**
- (none)

```text
DECISION: REJECT
PLAN_CHANGED: NO
KEEP_DRAFT: YES
REVISED_PLAN: (not applicable)
FEEDBACK_TO_AUTHOR: The current draft XML still has trivial placeholder PRTs for all six inputs (every node is `<sans>true</sans>`/`<tans>true</tans>`, always scoring correct regardless of the student's actual answer) and a qtest block that never really exercises the grading logic. This must be replaced with the real follow-through PRT/QTEST spec already settled for this question (see KEY FACTS ESTABLISHED, full node-by-node spec and all 9 qtest cases): ans1–ans4 graded via `AlgEquiv` on explicit `correct_p`/`mistake_p`/`signerror_p` booleans computed in feedback variables (SE→ME→bounds follow-through chain, with classic-mistake diagnostic branches scored 0/penalty 0.1), ans5 graded via `CasEqual` against the symbolic `valid_p` (never a hardcoded boolean), and ans6 graded via `CasEqual` against the correct interpretation option with three diagnostic distractor branches. Implement exactly that spec, including all 9 qtest cases with their described expected notes/scores/penalties.
AGENT_SETTINGS_CHANGE: author=off
```

## Entry 8 — reviewer-self-fix · attempt 1/3 (2026-07-23T23:25:05)

**Reference files fetched:**
- (none)

```text
STACK API check: PASSED

All checks passed.
```

## Entry 9 — reviewer · round 1 (2026-07-23T23:25:09)

**Key facts to carry forward:**
- The final, authoritative PRT/QTEST spec is now written directly into the fields (not just recorded in prior session notes); any future round should read it from the fields rather than reconstructing it from earlier entries.
- prt_ans2/3/4's "correct_p" is computed via genuine follow-through from the student's own prior-part answer (`ans1`/`ans2`), not the teacher's `se`/`me` — this is essential to the follow-through credit requirement and must not be changed to reference `se_val`/`me_val` directly.
- QTEST 1 and QTEST 4/5 use `se_val`/`me_val` (already-floated teacher values) as literal correct inputs for ans1/ans2, consistent with the numerical input's decimal-answer expectation.

**Reference files fetched:**
- (none)

```text
VERDICT: NEEDS REVISION
SELF_FIXED:
- Replaced the entire trivial placeholder PRT/QTEST block (all `SANS: true`/`TANS: true` nodes, which score every answer correct regardless of content) with the real follow-through grading logic previously settled for this question: `AlgEquiv` on explicit `correct_p`/`mistake_p`/`signerror_p` booleans (computed in each PRT's own feedback variables) for ans1–ans4, and `CasEqual` diagnostic-branch trees for ans5/ans6. This is PRT/QTEST authorship, which is always a self-fix regardless of size per my own scope.
ESCALATED_TO_AUTHOR:
- (none)
NOTED_FOR_PLANNER:
- Numerical inputs for parts 1-4 rely on the student typing a manually-rounded decimal; a syntax hint or explicit "enter as a decimal" wording could reduce ambiguity.
- Part 5's distractor set could add a subtly different "the sample mean will be within 1.96 SE of mu 95% of the time" style option for extra discriminating power.
```

## Entry 10 — planner · review (2026-07-23T23:25:47)

**Reference files fetched:**
- (none)

```text
DECISION: APPROVE
PLAN_CHANGED: NO
KEEP_DRAFT: YES
REVISED_PLAN: (not applicable)
FEEDBACK_TO_AUTHOR: (not applicable)
AGENT_SETTINGS_CHANGE: (not applicable)
```

## Entry 11 — planner (2026-07-23T23:26:08)

**Reference files fetched:**
- (none)

```text
Wrote the current-state plan description for the approved, merged question.
```

