GOAL: Test whether a student can compute required sample size for a mean's CI given z, s, and margin of error, and understand how sample size scales with margin of error and confidence level.

DESCRIPTION: A four-part question. Part 1 asks the student to compute the minimum whole-number sample size for a stated margin of error at 95% confidence (numeric input). Parts 2 and 3 each ask for the new sample size if the margin of error is divided by a different factor (r2, then r3), explicitly instructed to build on the student's own Part 1 answer (numeric inputs). Part 4 is a radio-button multiple choice asking whether the sample would be smaller, larger, the same, or impossible to tell, if a different (90% or 99%) confidence level were used instead of 95%, for the same margin of error.

STRUCTURE: Four parts.
1. Compute n1 = ceiling((z·s/E1)²) with z=1.96, numeric input, graded against the teacher's n1.
2. Given margin of error E1/r2, compute the new n. Graded via follow-through against the student's own Part 1 answer (ans1·r2²) rather than the teacher's n1 — so a student who got Part 1 wrong but scales correctly from their own value still gets full credit. A second PRT node specifically detects the common linear-scaling mistake (ans1·r2, forgetting the square) and gives targeted feedback with score 0; anything else wrong falls through to generic incorrect feedback.
3. Same structure as Part 2, using an independent ratio r3 (guaranteed different from r2), also following through independently from the student's own ans1.
4. Radio MCQ (smaller/larger/same/can't tell), options shuffled per variant, correct answer depends on whether the alternate confidence level is below (90%) or above (99%) 95%.

RANDOMIZATION: s ∈ {1.0, 1.1, ..., 2.5} (step 0.1); E1 ∈ {0.2, 0.3, 0.4, 0.5}; r2 ∈ {2,3,4}; r3 drawn from the remaining two values after r2 is picked (so r2≠r3 always); dir ∈ {1,2} picks between a 90%-vs-95% or 99%-vs-95% comparison for Part 4, with z_alt set accordingly (1.645 or 2.576); MCQ option order shuffled via `random_permutation`.

ANSWER TESTS: Parts 1–3 use numerical input with `forbidfloat`, graded by `AlgEquiv` (Part 1 against n1; Parts 2/3 against the student's own ans1-based follow-through expression, with a second node for the linear-scaling distractor). Part 4 is a radio input graded by `AlgEquiv` against the correct shuffled MCQ option.

FEEDBACK: General feedback shows the full formula substitution and ceiling step for Part 1, the E²-inverse-proportionality scaling argument for Parts 2/3, and the z²-proportionality explanation for Part 4's confidence-level tradeoff. Parts 2/3 PRTs distinguish three outcomes: correct follow-through from the student's own Part 1 (full credit, explicit note this is checked against their own value), the linear-scaling mistake r2/r3 instead of r2²/r3² (score 0, feedback explaining n depends on E² not E), and any other wrong answer (score 0, generic re-check feedback referencing their own n1).

IMPLEMENTATION NOTES:
- Only one of the two Part 4 directions (90-vs-95 or 99-vs-95) is exercisable per deployed seed/qtest — this is an inherent limitation of per-variant testing, not a bug; both directions are still correctly implemented in the question variables/MCQ logic.
- The exact-integer-square boundary case for Part 1 (where (z·s/E1)² lands exactly on an integer) cannot be deliberately forced via qtest, since n1 is derived from randomized s and E1 rather than being a direct, controllable input — also inherent, not a bug.
- Both qtest rounds passed with all 5 cases (all-correct, wrong-Part-1-with-consistent-follow-through, linear-scaling mistake, unrelated wrong answer, wrong MCQ choice) verified consistent with the PRT logic and free of degenerate coincidences (e.g. r2≠r3 enforced by construction).
- No deviations from the original plan; both review rounds concluded LOOKS GOOD with no changes requested.