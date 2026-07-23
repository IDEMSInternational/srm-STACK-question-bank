# Metadata — regression/corolla_price/corolla_price.xml

Running record of every agent (and user) action on this question that
isn't the XML itself: the reasoning, findings, improvement notes, and
reference lookups behind each change. Entries are appended in order,
newest at the bottom. The XML changes themselves are recorded by git —
this file holds the substance and meaning behind them, not the diffs.

## Entry 1 — concierge (2026-07-23T15:16:50)

**Issue:**
- #10

**Closes on merge:**
- yes

**Reference files fetched:**
- (none)

```text
Question reserved as part of issue #10.
```

## Entry 2 — planner (2026-07-23T18:17:05)

**Reference files fetched:**
- (none)

**Reference files recommended by Planner:**
- stack-docs/Authoring/Answer_Tests/Numerical.md

```text
Both settled, no changes needed elsewhere. Locking this in.

GOAL (non-negotiable): Test whether a student can carry out a full hypothesis test and confidence interval for a regression slope from given software output (intercept, slope, SE of slope, r, n), including computing R², and drawing a correct conclusion — without re-doing any visual/subjective judgment steps (scatterplot description, hand-fitting, axis-swap reasoning).

STRUCTURE (non-negotiable):
Single question, stem gives the fixed Corolla scenario (n=38, age vs. price in $1000s) and presents "software output": intercept b0, slope b1, SE(b1), r — framed as ungraded narrative context, exactly like part 9 of the original.
1. Compute the t-statistic for H0: β1=0 vs H1: β1<0, from b1 and SE(b1).
2. Compute the exact one-tailed p-value (df=36), and state the decision at α=0.05 — follow-through from the student's own Part 1 answer, not the true t.
3. Compute R² from the given r, reported as a percentage.
4. Compute the 95% CI for the population slope using b1 ± 2×SE(b1) (book's rule-of-thumb multiplier), reported as two separate numeric inputs (lower bound, upper bound) — independent of parts 1–2 since it only uses the given b1/SE directly.

RANDOMIZATION:
- n fixed at 38 (df=36).
- b1 (slope, $1000s/year): random negative value, e.g. −1.4 to −0.5.
- SE(b1): randomized so |t| = |b1|/SE spans genuinely different evidence-strength bins — very strong (|t|>10), moderate (|t|≈4–7), borderline (|t|≈2–3, p near 0.01–0.05) — the key "no pattern-matching the conclusion" lever.
- b0 (intercept, $1000s): random positive, e.g. 12–22.
- r: derived from the resulting t and df (not independently randomized) so all reported "software output" numbers stay mutually consistent, sign negative.

ANSWER TESTS:
- t-statistic: numeric, tolerance test against b1/SE.
- p-value: numeric, tolerance test against the true one-tailed p-value (exact t-distribution, df=36); decision step's grading uses the student's own p-value (follow-through).
- Decision: MCQ/dropdown (reject H0 / do not reject H0), graded for consistency with the student's own p-value vs. 0.05.
- R²: numeric, tolerance test, r² from the given r, as a percentage.
- CI bounds: two numeric inputs, tolerance test, against b1 ± 2×SE.

FEEDBACK: Worked solution walks through t = b1/SE, exact p-value via the t-distribution, decision rule at α=0.05, R²=r² (as %), and CI = b1±2SE — mirroring the book's own layout. Common mistakes worth flagging: sign/direction errors in the one-tailed test (using the two-tailed p-value, or testing the wrong tail), forgetting R² is a percentage, and misapplying the ±2×SE margin to the wrong quantity.

PRT/QTEST SUGGESTIONS: Test a borderline variant where |t|≈2 so p is close to 0.05 on both sides of the threshold — verify the decision branch flips correctly. Test follow-through explicitly: a student who gets t wrong (e.g. sign flip) but then computes a p-value and decision consistent with their own wrong t should still score those steps as correct. Also test a very-strong-evidence variant (|t|≈13, matching the book) to confirm the exact p-value calculation doesn't choke or underflow at extreme t. Confirm the one-tailed p-value direction is computed correctly given H1: β1<0 (i.e., not silently reporting the two-tailed value).
```

## Entry 3 — author · attempt 1/3 (2026-07-23T18:18:06)

**Reference files fetched:**
- stack-docs/Authoring/Inputs/Multiple_choice_input.md

```text
STACK API check: FAILED

Render failed: Error(s) in question-variables: Forbidden function: <span class="stacksyntaxexample">load</span>.
```

## Entry 4 — author · attempt 2/3 (2026-07-23T18:18:13)

**Reference files fetched:**
- (none)

**Already available (fetched earlier this session, not re-fetched):**
- stack-docs/Authoring/Inputs/Multiple_choice_input.md

```text
STACK API check: FAILED

Render failed: Error rendering input: The teacher did not indicate at least one correct answer.
```

