GOAL: Test the full one-mean hypothesis-test workflow (Eagle Boys pizza diameters, Ch. 27) end-to-end — computing standard error, stating hypotheses, computing a t-score, estimating a P-value via the 68-95-99.7 rule, drawing a conclusion, and checking a validity condition — with later steps crediting the student's own prior answers via follow-through rather than re-penalizing a single early slip.

DESCRIPTION: A single scenario (a sample of n pizzas with mean diameter x̄ and sample SD s, testing whether the true mean differs from 12 inches at α=0.05) broken into six parts, all on one page: (1) a numerical input for the standard error; (2) two algebraic/equation inputs for H0 and H1 in terms of μ; (3) a numerical input for the t-score; (4) a 4-option radio button choosing the P-value bucket implied by the 68-95-99.7 rule; (5) a 2-option radio button (reject/fail to reject H0); (6) a 2-option radio button (yes/no) on whether n is large enough for the CLT, using the book's n>25 rule of thumb.

STRUCTURE:
1. Standard error, computed from randomised x̄, s, n.
2. Hypotheses H0: μ=12 vs H1: μ≠12 (two separate algebraic inputs; μ fixed).
3. t-score, computed from randomised x̄, fixed μ=12, and the student's own SE from Part 1 (follow-through) — guarded against division by zero if the student entered SE=0.
4. P-value bucket (4 radio options, order shuffled via random_permutation), graded against the bucket implied by the student's own t from Part 3 (follow-through).
5. Decision (reject/fail to reject, radio), graded against the decision implied by the student's own bucket from Part 4 (follow-through).
6. Validity check (yes/no, radio) against n>25, graded independently of Parts 1–5.

RANDOMIZATION: Bucket target chosen first via a weighted draw (w=rand(100): <50 → bucket 1 |t|>3, <70 → bucket 2, <85 → bucket 3, else bucket 4), each with an internal random offset comfortably clear of boundaries. s is drawn in [0.15, 0.36], n in [15, 49]. x̄ is back-derived as 12 − |t|·s/√n and rounded to 3 decimals for display; the underlying t_true/bucket_true used for grading are recomputed from this rounded x̄, so rounding is guaranteed self-consistent with the realized bucket. x̄ is always below 12 (deviation sign fixed negative), matching the original narrative.

ANSWER TESTS:
1. SE: numerical input, teacher answer se_true, graded true if within 1% relative tolerance (built as an explicit `is(abs(...)<=...)` node rather than a numerical answer-test option); a dedicated wrong branch specifically detects s/n (SE mistake of dividing by n instead of √n) and gives targeted feedback, scored 0.
2. Hypotheses: two algebraic inputs, AlgEquiv against μ=12 and μ≠12 respectively, independent PRTs.
3. t-score: numerical input; feedback variables compute (x̄−12)/ans1 using the student's own Part-1 answer. A guard node scores 0 with an explicit message if ans1=0 (undefined t). Correct branch accepts within ±0.02 absolute; a dedicated wrong branch detects the sign-flipped (12−x̄)/ans1 and gives targeted feedback, scored 0.
4. P-value bucket: radio (4 shuffled options); correct option is whichever bucket abs(ans3) (the student's own t) falls into, not the teacher's t.
5. Decision: radio (2 options); correct option is derived from the student's own ans4 (reject if bucket 1 or 2, else fail to reject).
6. Validity check: radio (2 options); correct option is validity_true, computed directly from randomised n vs 25, independent of all other parts.

FEEDBACK: General feedback walks the same chain as the book (SE → t → bucket → decision → validity) using the teacher's own randomised values, with `[[if]]` blocks selecting the applicable bucket/decision/validity wording for that variant. Dedicated PRT branches give targeted messages for: SE = s/n instead of s/√n; sign-flipped t-score ((μ−x̄)/SE instead of (x̄−μ)/SE); Part 4/5 mismatches just restate "re-apply the rule to your own answer from the previous part." Part 6 feedback explicitly restates the n≫25 rule of thumb rather than a generic sample-size-is-fine line.

IMPLEMENTATION NOTES:
- All PRTs use `AlgEquiv` on hand-built boolean/`is(...)` expressions rather than a numerical-tolerance answer-test type, per house style of avoiding specialized-test edge cases — tolerances (1% relative for SE, ±0.02 absolute for t) are hard-coded directly into the feedback-variable comparisons.
- Reviewer flagged, non-blocking: SE's 1% relative tolerance and t's ±0.02 tolerance are intentionally generous but were checked to comfortably separate correct answers from the s/n and sign-flip mistake-branches across the full randomised range; tighten only if a stricter check is later found pedagogically preferable.
- Part 4's MCQ option order is shuffled per-variant via `random_permutation(ta4)` — the "correct" index is carried alongside each option's text/boolean flag, not fixed positionally.
- Rounding x̄ to 3dp for display, then recomputing t_true/bucket_true from that same rounded x̄ (rather than from the unrounded exact value), is what actually guarantees the displayed numbers and the graded bucket never disagree — this was the specific risk flagged in the original plan's randomization notes.
- Qtest suite explicitly covers all four bucket boundaries (0.99/1.01, 1.99/2.01, 2.99/3.01 pattern), the zero-SE guard, the sign-flip branch, the s/n mistake branch, and independent follow-through chains (wrong SE→correct-relative-t; wrong bucket→correct-relative-decision), matching every case raised in the plan's PRT/QTEST SUGGESTIONS.