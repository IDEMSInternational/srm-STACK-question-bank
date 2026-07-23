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

## Entry 5 — author · attempt 3/3 (2026-07-23T18:20:03)

**Reference files fetched:**
- (none)

**Already available (fetched earlier this session, not re-fetched):**
- stack-docs/Authoring/Inputs/Multiple_choice_input.md

```text
STACK API check: PASSED

All checks passed.
```

## Entry 6 — reviewer-self-fix · attempt 1/3 (2026-07-23T18:23:17)

**Reference files fetched:**
- (none)

**Already available (fetched earlier this session, not re-fetched):**
- stack-docs/Authoring/Inputs/Multiple_choice_input.md

```text
STACK API check: PASSED

All checks passed.
```

## Entry 7 — reviewer · round 1 (2026-07-23T18:23:19)

**Key facts to carry forward:**
- `r`'s sign was corrected (removed an extra negation) so it now correctly comes out negative for every variant, matching the plan's "sign negative" requirement.
- The decision PRT grades follow-through from the student's own `ans_p` (via `if is(ans_p<0.05) then reject else noreject`), not from the true `p_true` — this is deliberate per the plan's ANSWER TESTS section, and qtest cases 3/4 exercise this explicitly with variant-independent crafted values rather than relying on the actual random draw.
- With the current randomization (`t_target` minimum |t|=2, df=36), the true correct decision is always "reject H0" in every possible variant — "do not reject" as a *true* answer never actually occurs, only as a follow-through possibility from a student's own wrong p-value.

**Reference files fetched:**
- (none)

**Already available (fetched earlier this session, not re-fetched):**
- stack-docs/Authoring/Inputs/Multiple_choice_input.md

```text
VERDICT: NEEDS REVISION
SELF_FIXED:
- Fixed sign bug in `r` computation: the draft's `r: float(-t_true/sqrt(df+t_true^2));` includes a spurious extra negative sign. Since `t_true` is already negative (b1<0, se_b1>0), the standard relation `t = r*sqrt(df)/sqrt(1-r^2)` requires `r = t_true/sqrt(df+t_true^2)` (no extra negation) to correctly come out negative, matching the plan's explicit "sign negative" requirement. This is a one-line fix, contained entirely within QUESTIONVARIABLES — `{@r@}` is displayed as-is everywhere else, so nothing else needs to change.
- Replaced all six placeholder PRTs (`SANS: true / TANS: true`) with real grading logic, per my own PRT/QTEST authorship mandate: numeric parts (t, p, R², CI bounds) now use explicit tolerance checks compared via AlgEquiv rather than bare placeholders; the decision PRT now implements genuine follow-through — it compares the student's MCQ choice against `if is(ans_p<0.05) then reject else noreject`, i.e. consistency with the student's *own* submitted p-value, exactly as the (negotiable) ANSWER TESTS section specifies, rather than against the true p-value.
- Rewrote QTEST to 6 real cases: happy path, an isolated wrong-t case, a wrong-p-but-consistent-decision follow-through case, a correct-p-but-inconsistent-decision case, a wrong-R² case, and a swapped-CI-bounds case. Wrong values use variant-independent offsets (e.g. `t_true+1`, `ans_p:100`, swapped CI bounds) so they can't coincidentally collapse to the correct answer for any value the random variables can take.
ESCALATED_TO_AUTHOR:
- (none)
NOTED_FOR_PLANNER:
- The randomization for the "borderline" t-bin uses `t_target: 2+rand(2)` (i.e. |t| ∈ {2,3}), but for df=36 this always yields p < 0.05 (p≈0.027 at t=2, smaller at t=3) — so across every possible random variant, the true correct decision is always "reject H0"; "do not reject" never actually occurs as the correct answer in any real variant (though it's still exercised in qtest via a crafted student p-value). If a genuine "do not reject" variant is pedagogically wanted, the borderline bin would need to include |t| closer to ~1.5–1.9 (df=36, p≈0.05 near t≈1.69).
- There's a slight tension between the (negotiable) ANSWER TESTS section, which says p is graded absolutely against the true p-value, and the PRT/QTEST SUGGESTIONS section, which describes follow-through from a wrong t into p/decision. I implemented the ANSWER TESTS version (p graded absolutely, only decision has follow-through from the student's own p) since it's the more specific/explicit of the two; flagging in case the intent was actually full t→p→decision follow-through chaining.
- `FORBIDFLOAT: 0` is written explicitly on every numerical input; since floats are exactly what's expected here, this matches STACK's own default and could simply be omitted (cosmetic only, not a defect).
```

## Entry 8 — planner · review (2026-07-23T18:23:57)

**Reference files fetched:**
- (none)

```text
This is purely a randomization-range tweak inside the existing question variables — nothing about content (variables set, question text, feedback, input types) needs rewriting, just the numeric bounds on `t_target`'s third bin. That's squarely Reviewer's domain (constructing/validating the qtest and randomization logic), not new authoring. I'd suggest turning Author off for this round and letting Reviewer make the fix directly.

DECISION: REJECT
PLAN_CHANGED: NO
KEEP_DRAFT: YES
REVISED_PLAN: (not applicable)
FEEDBACK_TO_AUTHOR: Widen the "borderline" t-bin in the question variables so genuine "do not reject H0" variants actually occur. Currently `tcase=2` uses `t_target: 2+rand(2)` (|t| ∈ {2,3}), which at df=36 always yields p<0.05 — so "do not reject" never occurs as a true correct answer, only as a synthetic qtest case. Change this bin to target |t| roughly in the 1.5–1.9 range (e.g. something like `t_target: float((15+rand(5))/10)` giving |t| ∈ {1.5,...,1.9}) so that across real variants in this bin, p sometimes falls above and sometimes below 0.05, and the true decision genuinely varies. Recheck that `se_b1: float(abs(b1)/t_target)` and downstream `r`, `p_true` still behave sensibly (no division issues, r still comes out consistently negative) with these smaller |t| values. Keep everything else as-is: the corrected `r` sign, all six real PRTs, the follow-through logic on the decision step (graded against the student's own p, not p_true), and the qtest cases — add or adjust a qtest case if useful to demonstrate a genuine "do not reject" variant, but this is optional.
AGENT_SETTINGS_CHANGE: author=off
```

## Entry 9 — reviewer-self-fix · attempt 1/3 (2026-07-23T18:27:29)

**Reference files fetched:**
- (none)

**Already available (fetched earlier this session, not re-fetched):**
- stack-docs/Authoring/Inputs/Multiple_choice_input.md

```text
STACK API check: PASSED

All checks passed.
```

## Entry 10 — reviewer · round 1 (2026-07-23T18:27:32)

**Key facts to carry forward:**
- The borderline t-bin (tcase=2) now targets |t| ∈ {1.5,1.6,1.7,1.8,1.9} (df=36), straddling the true critical value ≈1.688, so real variants now sometimes have true decision "do not reject H0" — this was previously impossible with `2+rand(2)`.

**Reference files fetched:**
- (none)

**Already available (fetched earlier this session, not re-fetched):**
- stack-docs/Authoring/Inputs/Multiple_choice_input.md

```text
VERDICT: MINOR ISSUES
SELF_FIXED:
- Per Planner's explicit instruction this round, widened the "borderline" t-bin from `2+rand(2)` (|t| ∈ {2,3}, always p<0.05 at df=36) to `float((15+rand(5))/10)` (|t| ∈ {1.5,...,1.9}), which straddles the true df=36 critical value (t≈1.688 for one-tailed α=0.05) so genuine "do not reject" variants now actually occur. This is a one-line change contained entirely within QUESTIONVARIABLES — `se_b1`, `t_true`, `r`, `p_true`, `ci_lower/upper` are all still computed the same downstream formulas from `t_target`/`b1`, so nothing else needs to change; no division-by-zero risk since `t_target` stays comfortably away from 0.
ESCALATED_TO_AUTHOR:
- (none)
NOTED_FOR_PLANNER:
- The qtest suite still lacks a case drawn from the new borderline bin exercising a genuine "do not reject" true-answer variant; since qtest cases use fixed crafted values independent of the random draw, this is optional/cosmetic per Planner's own note ("add ... if useful ... but this is optional") and not required for correctness.
```

## Entry 11 — planner · review (2026-07-23T18:27:55)

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

