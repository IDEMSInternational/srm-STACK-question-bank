GOAL: Test whether a student can execute the one-mean, large-sample z-confidence-interval pipeline (SE → margin of error → CI bounds → validity check → interpretation) on randomized data modeled on a black bear weight study, with genuine follow-through credit through the arithmetic chain and a validity check that isn't a rubber stamp.

DESCRIPTION: The student is given a randomized sample (n, x̄, s) of male black bear weights and a fixed z*=1.96 for 95% confidence. An ungraded framing paragraph asks them to mentally consider what μ represents and picture the sampling distribution. They then work through five graded parts: (1) type in the standard error SE=s/√n as a decimal (numerical input); (2) type in the margin of error ME=z*·SE (numerical input); (3) type in the lower and upper CI bounds x̄±ME as two separate numerical inputs; (4) a two-option radio button asking whether the large-sample z-procedure is valid here (i.e. n≥25); (5) a four-option radio button asking them to pick the correctly worded interpretation of the confidence interval among distractors that misstate the population, the parameter, or the meaning of confidence.

STRUCTURE:
- Non-graded stem: narrative context, no input.
1. SE = s/√n — numerical input, graded independently against the teacher's value (3 dp).
2. ME = z*·SE — numerical input, graded via follow-through against z*·(student's Part 1 answer).
3. Lower and upper CI bounds — two separate numerical inputs (ans3, ans4), each graded via follow-through against x̄∓(student's Part 2 answer), independently of each other.
4. Validity check (n≥25) — two-option radio input, graded strictly against the actual randomized n, with no follow-through from Parts 1–3.
5. Interpretation — four-option radio input, single correct option, independent of the numerical parts.

RANDOMIZATION: n drawn from the fixed list {10,15,18,22,30,45,80,150,250} (spans clearly below/above 25, avoiding the 20–30 boundary zone); x̄ = rand(51)+60 (60–110 kg); s = rand(31)+30 (30–60 kg). All three vary independently per variant.

ANSWER TESTS:
- Part 1: numerical, tolerance 0.0005 against SE; a specific-mistake branch (s/n instead of s/√n) scores 0 with a 0.1 penalty and dedicated feedback, distinct from the generic wrong-answer branch.
- Part 2: numerical, tolerance 0.0005, follow-through off the student's own ans1; a specific mistake branch (using SE directly as ME, i.e. forgetting the ×z*) scores 0/0.1-penalty with dedicated feedback.
- Part 3/4 (bounds): numerical, tolerance 0.005 each, follow-through off the student's own ans2; each has a sign-flip detection branch (matches the *other* bound) scoring 0/0.1-penalty with feedback naming the mix-up, distinct from generic-wrong.
- Part 4 (validity): CasEqual against the actual `valid_p` (n≥25), independent of all earlier parts.
- Part 5 (interpretation): CasEqual against option 2 (correct), with three further branches each individually detecting one specific wrong distractor (1, 3, 4) to give a targeted rather than generic "incorrect" response.

FEEDBACK: Part 1 flags s/n vs s/√n. Part 2 flags omitting the z* multiplier. Parts 3/4 flag a bounds sign-swap separately from other arithmetic slips. Part 4's shared general feedback explains the CLT/n≥25 rationale for both valid and invalid cases (conditional block). Part 5's general feedback restates the correct interpretation and, per-distractor in the PRT, explains what's specifically wrong with each of the three wrong options (probability-about-a-fixed-interval; statement about individual bears; statement about repeated sample means rather than μ).

IMPLEMENTATION NOTES:
- Numerical inputs (parts 1–4) require the student to type a manually-rounded decimal with no syntax hint; Reviewer flagged this as a source of possible ambiguity but left it as a non-blocking suggestion, not a fix.
- Part 5's distractor set does not include the "sample mean will be within 1.96 SE of μ 95% of the time" variant Reviewer suggested for extra discrimination — current set has 3 distractors (population-individuals, fixed-interval-probability, repeated-sample-means) plus the correct option.
- Reviewer confirmed via qtest cases that follow-through works correctly through a consistently-wrong SE (forgot sqrt) into Parts 2–3, that a sign-flipped bound is marked wrong independent of correct SE/ME, and that Part 4 is graded strictly off the actual n regardless of earlier arithmetic errors — matching the plan's PRT/QTEST suggestions exactly.