GOAL: Test whether a student can carry out a full hypothesis test and confidence interval for a regression slope from given software output (intercept, slope, SE of slope, r, n), including computing R², and drawing a correct conclusion — without re-doing any visual/subjective judgment steps (scatterplot description, hand-fitting, axis-swap reasoning).

DESCRIPTION: A single question presents a fixed scenario (Toyota Corolla age vs. price, n=38) with "software output" — an intercept, slope, SE(slope), and r — as narrative context. The student answers four parts: (1) a numeric box for the t-statistic; (2) a numeric box for the one-tailed p-value, plus a dropdown for the reject/do-not-reject decision; (3) a numeric box for R² as a percentage; (4) two numeric boxes for the lower and upper bounds of the 95% CI for the slope.

STRUCTURE:
1. Compute the t-statistic for H0: β1=0 vs H1: β1<0, from b1 and SE(b1).
2. Compute the exact one-tailed p-value (df=36), and a dropdown decision (reject H0 / do not reject H0) at α=0.05 — the decision is graded for consistency with the student's own p-value, not the true p-value, so a wrong p-value followed by a decision consistent with it still scores correctly.
3. Compute R² from the given r, reported as a percentage.
4. Compute the 95% CI for the population slope using b1 ± 2×SE(b1), as two independent numeric inputs (lower bound, upper bound); graded independently of parts 1–2.

RANDOMIZATION:
- n fixed at 38 (df=36).
- b1: random negative value in [-1.5, -0.5] (one decimal place).
- Evidence-strength bin (tcase, uniform over 3 bins) drives the target |t|: very strong (10–14), moderate (4–7), or borderline (1.5–1.9); se_b1 is then derived as |b1|/t_target so t_true, and hence r and p_true, are all consistent with the same draw.
- b0: random positive value in [12, 22].
- r is derived from t_true and df (r = t/√(df+t²)), not independently randomized, so all reported figures stay mutually consistent; sign is always negative.

ANSWER TESTS:
- t-statistic: numeric input, tolerance test (relative 5% + small absolute buffer) against b1/se_b1.
- p-value: numeric input, tolerance test (absolute 0.005) against the exact one-tailed p-value from the t-distribution (df=36).
- Decision: dropdown, correct answer computed from the student's own submitted p-value (reject if ans_p<0.05, else do not reject) — genuine follow-through.
- R²: numeric input, tolerance test (absolute 0.5 percentage points) against 100×r².
- CI bounds: two numeric inputs, each with its own tolerance test (relative 5% + small absolute buffer) against b1∓2×se_b1 respectively.

FEEDBACK: General feedback walks through t = b1/SE(b1), the one-tailed p-value via the t-distribution (explicitly flagging that doubling or using the wrong tail is a common mistake), the decision rule at α=0.05 (shown via a conditional branch on the true p-value), R²=r² as a percentage, and the CI as b1±2×SE(b1) (flagging misapplying the margin to b0 or r as a common mistake). Each part's PRT also carries brief targeted false-branch feedback pointing back at the relevant formula.

IMPLEMENTATION NOTES:
- The t-statistic bin (tcase) is drawn via `rand(3)` and used to set a target |t| range per bin, then se_b1 is derived from b1/t_target — this is the "randomize the answer, not the surface parameter" pattern applied to the evidence-strength lever, keeping r and p mutually consistent by construction rather than independently randomized.
- Decision-part grading intentionally compares against a value computed from the student's own `ans_p` (not `p_true`), implementing the planned follow-through; qtest case 3 explicitly exercises this (wrong p, decision consistent with it still scores full marks) and case 4 exercises the inconsistent case (correct p, wrong decision → scored wrong).
- Reviewer flagged as optional/cosmetic (not fixed): the qtest suite has no crafted case whose *true* answer lands in the borderline "do not reject" bin — existing cases use fixed hand-picked values regardless of the random draw, so this is a coverage gap only, not a correctness issue, per the plan's own "optional" framing of this suggestion.

PRT/QTEST SUGGESTIONS: (none beyond what qtest already covers — borderline flip, follow-through both directions, and CI-swap are all tested; the one open item is the optional borderline "do not reject" crafted case noted above)

REFERENCE POINTERS (optional):
- (none)

ADDITIONAL LANGUAGES (optional): (none)