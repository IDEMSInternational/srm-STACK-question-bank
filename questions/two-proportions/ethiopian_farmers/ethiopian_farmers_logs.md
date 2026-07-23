# Metadata — two-proportions/ethiopian_farmers/ethiopian_farmers.xml

Running record of every agent (and user) action on this question that
isn't the XML itself: the reasoning, findings, improvement notes, and
reference lookups behind each change. Entries are appended in order,
newest at the bottom. The XML changes themselves are recorded by git —
this file holds the substance and meaning behind them, not the diffs.

## Entry 1 — concierge (2026-07-23T15:15:28)

**Issue:**
- #4

**Closes on merge:**
- yes

**Reference files fetched:**
- (none)

```text
Question reserved as part of issue #4.
```

## Entry 2 — planner (2026-07-23T18:26:40)

**Reference files fetched:**
- (none)

**Reference files recommended by Planner:**
- stack-docs/Authoring/Inputs/Multiple_choice_input.md
- stack-docs/CAS/Equations.md

```text
Good catch, and thanks for flagging that — locking in the plan with that correction.

GOAL (non-negotiable): Test a student's ability to carry the same 2×2 table through two parallel inferential frameworks — a two-proportion z-test/CI and a chi-square-based odds-ratio test/CI — including recognizing which quantities each framework compares, computing each, drawing a conclusion, and checking the validity conditions.

STRUCTURE (non-negotiable):
1. **Thread 1 — proportion difference** (5 answers): (a) MCQ identifying how the difference is defined (p̂ non-adopter, small − large); (b) two-number input for (p̂_small, p̂_large); (c) z-statistic — follow-through, recomputed from the student's own p̂ pair (pooled SE); (d) reject/fail-to-reject decision — follow-through from the student's own z vs ±1.96; (e) CI for the difference — follow-through, recomputed from the student's own p̂ pair (unpooled SE).
2. **Thread 2 — odds ratio** (5 answers), structurally mirroring Thread 1: MCQ for OR definition; two-number input for (odds_small, odds_large); χ² statistic (follow-through from student's own odds pair); decision (follow-through from student's own χ² vs 3.84); CI for OR (follow-through from student's own odds pair).
3. **Validity** (2 answers): smallest expected cell count (base, graded directly); valid/invalid MCQ — follow-through from the student's own expected-count value vs the ≥5 threshold.

Each thread and the validity check is its own self-contained follow-through chain; no cross-thread dependency.

RANDOMIZATION: Vary the four raw 2×2 cell counts. Two regimes: (a) "normal" — moderate/large row totals (broadly like the source data) spanning reject/fail-to-reject outcomes and narrow/wide/border-crossing CIs across variants; (b) "small-N" — deliberately produces an expected count under 5, so the validity check isn't trivially always "yes." Regime chosen randomly per variant.

ANSWER TESTS:
- MCQs (definition, decision, validity): multiple choice, correct option graded directly (decision/validity options graded via follow-through logic as described in STRUCTURE).
- Two-number inputs (p̂ pair, odds pair): numerical, tolerance-based, graded against true values.
- z/χ² statistics, CIs: numerical tolerance, each recomputed from the student's own upstream inputs per STRUCTURE (not the teacher's raw values).
- Expected count: numerical tolerance, graded directly.

FEEDBACK: Each numeric/decision node's feedback should state which upstream value it's using (the student's own, not the "true" one) so a student can see exactly where a discrepancy entered. General feedback (worked solution) should present both threads side-by-side using the true table, explicitly naming the pooled-vs-unpooled SE distinction, and should make it an explicit teaching point that both frameworks' hypothesis-test decisions always agree, because the pooled two-proportion z-test and the chi-square test of independence are mathematically equivalent on a 2×2 table (χ² = z² exactly, matching 1.96² = 3.8416 ≈ 3.84) — this is also why the source material's own step 7 conclusion was inconsistent with step 3 on the same table. For the decision/validity MCQs, feedback should explain the reasoning (e.g. "your z of X falls outside ±1.96, so ...") rather than just right/wrong.

PRT/QTEST SUGGESTIONS:
- Verify all "true" worked-solution values independently from the actual randomized table, rather than trusting the issue's own worked-solution text at face value — its χ²=11.10 "no evidence of difference" line is a source-text typo, now understood precisely: it's mathematically impossible for the proportion-test and odds-ratio-test decisions to disagree on the same 2×2 table (χ² = z² exactly), so do NOT test for or expect a variant where these two decisions disagree — flag this equivalence explicitly to Reviewer so consistent matching across every variant is recognized as guaranteed-correct behavior, not treated as a suspicious PRT bug.
- Separately, DO test a variant where the CI-based conclusion (does the proportion CI cross 0, does the OR CI cross 1) diverges slightly from the hypothesis-test decision near a boundary — this is a real, expected subtlety (CIs use unpooled SE, test statistics use pooled SE) and should be verified as handled correctly, not conflated with the guaranteed test-decision agreement above.
- Test the small-N regime producing expected count < 5, confirming the validity MCQ follow-through correctly flags "invalid."
- Test follow-through explicitly: a student who enters a wrong p̂ pair (or odds pair) but then correctly propagates it through z/decision/CI should score full follow-through credit on those downstream nodes despite the initial slip.
```

