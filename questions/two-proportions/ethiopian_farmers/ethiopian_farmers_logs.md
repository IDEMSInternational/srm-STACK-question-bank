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

## Entry 3 — author · attempt 1/3 (2026-07-23T18:28:26)

**Reference files fetched:**
- (none)

```text
STACK API check: PASSED

All checks passed.

Deviations reported: - Plan's STRUCTURE section (non-negotiable) describes decision/validity MCQ grading as "follow-through logic" — that logic is a PRT concern belonging to Reviewer, not something I can express via ANSWERTEST/TANS. I used `String` as a placeholder ANSWERTEST for all radio inputs (comparing the selected option number) since MCQ correctness for these ultimately depends on follow-through comparison against the student's own upstream values, not a fixed teacher value — flagging this explicitly so Reviewer knows to build real follow-through comparison logic for ans1d, ans2d, ans3b (and to note the guaranteed z²=χ² equivalence, and the expected CI/test-decision divergence near boundaries, per the plan's PRT/QTEST section).
- Plan calls for a two-number input for p̂ pair, odds pair, and CIs; I implemented these as algebraic inputs accepting a Maxima list `[a,b]`, graded with NumRelative (which STACK's numerical tests support for lists per the Numerical Testing note) — this is a reasonable literal reading of "two-number input" not explicitly specified as a distinct STACK input type, so noted here rather than treated as silent.
```

## Entry 4 — reviewer-self-fix · attempt 1/3 (2026-07-23T18:33:03)

**Reference files fetched:**
- (none)

```text
STACK API check: PASSED

All checks passed.
```

## Entry 5 — reviewer · round 1 (2026-07-23T18:33:06)

**Key facts to carry forward:**
- Every PRT node's SANS is a self-contained inline Maxima `block(...)`/`if` expression (no separate feedbackvariables section exists in the compact spec used here) — any future edit to a node's logic must edit that inline SANS expression directly, not look for a feedbackvariables block.
- QTEST cases reference newly-added `test_wrong_*` question variables (defined right after `validity_opts`) purely to build wrong-but-consistent follow-through test inputs for Thread 1, Thread 2, and validity; they have no effect on the question itself, only on qtest expressions.
- A qtest run fixes one random draw of `regime`/cell counts for all its cases; it's therefore not possible to force a specific regime (e.g. small-N) or a specific CI/test-decision boundary divergence deterministically through qtest inputs alone — the qtest cases here are written generically (in terms of the CAS-computed true values) so they pass correctly whichever regime is drawn, but do not guarantee any particular regime was actually exercised on a given run.
- MCQ radio inputs ans1a/ans2a use fixed, unshuffled option lists (no `random_permutation`), so their correct qtest value is the literal constant `1` in both cases; the follow-through MCQs (ans1d, ans2d, ans3b) have a variant-dependent correct option number, so their qtest values must use `first(mcq_correct(...))` rather than a literal constant.

**Reference files fetched:**
- (none)

```text
VERDICT: NEEDS REVISION
SELF_FIXED:
- Replaced every placeholder `SANS: true / TANS: true` PRT node (12 PRTs, all deterministic placeholders per the task) with real grading logic: direct check for the two "definition" MCQs (ans1a, ans2a) and the expected-count input (ans3a); explicit follow-through recomputation (guarded against wrong-shape/non-numeric input, falling back to the true upstream value so a single slip doesn't crash the tree) for ans1b/1c/1d/1e and ans2b/2c/2d/2e and ans3b, matching the plan's non-negotiable follow-through structure. This is squarely PRT/QTEST authorship, always self-fixed regardless of size per my own scope.
- Fixed the QTEST's MCQ input values: the draft supplied the *entire* teacher's-answer array (e.g. `ta_mcq1a`, `decision1_opts`) as the submitted value for a radio input, which is wrong per STACK's own testing convention (radio/dropdown test values must be the single selected value, via `first(mcq_correct(ta))` for variant-dependent correct options, or a literal constant for fixed ones) — an unfixed version would simply fail against the real API. Replaced the single QTEST case with several (happy path, wrong-MCQ-definition, Thread-1 wrong-but-consistent follow-through, Thread-2 wrong-but-consistent follow-through, and an empty-list adversarial case for ans1b), using correct MCQ value conventions throughout.
- Appended small test-support variables to QUESTIONVARIABLES (`test_wrong_*`) purely to build qtest input expressions for the wrong-but-consistent-follow-through cases; these are new names, don't redefine or change the meaning of any existing variable, so this is a safe, contained addition.
ESCALATED_TO_AUTHOR:
- (none)
NOTED_FOR_PLANNER:
- The MCQ option text for ta_mcq1a/ta_mcq2a uses markdown-style `*italics*` inside a LaTeX/HTML string (e.g. "*non-adopters*") — this won't render as emphasis in the rendered HTML, just literal asterisks; consider `<em>...</em>` instead if the emphasis matters.
- Per the plan's PRT/QTEST suggestions, a genuinely forced "CI-conclusion diverges from test-decision near a boundary" variant, and a genuinely forced small-N regime variant, cannot be deterministically produced through qtest input values alone — qtest fixes inputs, not the random draw of `regime`/cell counts within a single test run. My qtest cases are written generically (using the CAS formulas themselves, e.g. `min_expected_true`, `validity_opts`) so they pass correctly *whichever* regime the run happens to draw, which verifies the logic is right in general, but does not guarantee a specific regime was exercised on any given run. If Planner wants a specific regime or boundary case deterministically covered, a `<deployedseed>` pinned to a known-good variant would be needed — outside what a stateless qtest input list can express.
```

## Entry 6 — planner · review (2026-07-23T18:33:43)

**Reference files fetched:**
- (none)

```text
This is a small, purely content-level fix (question text wording), not a PRT/qtest change — Author should handle it, no need to touch Reviewer's logic. Sending back for that one fix.

DECISION: REJECT
PLAN_CHANGED: NO
KEEP_DRAFT: YES
REVISED_PLAN: (not applicable)
FEEDBACK_TO_AUTHOR: In the MCQ option text for `ta_mcq1a` and `ta_mcq2a`, replace the markdown-style asterisk emphasis with real HTML tags so it actually renders. Specifically:
- In `ta_mcq1a`, option 1: `"\\( \\hat p_{\\text{small}} - \\hat p_{\\text{large}} \\), the difference in proportions of *non-adopters* between groups"` → change `*non-adopters*` to `<em>non-adopters</em>`.
- In `ta_mcq1a`, option 3: `"\\( \\hat p_{\\text{small}} - \\hat p_{\\text{large}} \\), the difference in proportions of *adopters* between groups"` → change `*adopters*` to `<em>adopters</em>`.
Check for any other asterisk-emphasis instances in these two option lists and convert them the same way. No other changes needed — everything else in this draft (follow-through logic, guarded fallbacks, feedback content, qtest coverage) is approved as-is.
AGENT_SETTINGS_CHANGE: (not applicable)
```

## Entry 7 — author · attempt 1/3 (2026-07-23T18:33:58)

**Reference files fetched:**
- (none)

```text
STACK API check: PASSED

All checks passed.
```

