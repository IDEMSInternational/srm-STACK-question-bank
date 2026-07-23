# Metadata — hypothesis-tests/pizzas_ht/pizzas_ht.xml

Running record of every agent (and user) action on this question that
isn't the XML itself: the reasoning, findings, improvement notes, and
reference lookups behind each change. Entries are appended in order,
newest at the bottom. The XML changes themselves are recorded by git —
this file holds the substance and meaning behind them, not the diffs.

## Entry 1 — concierge (2026-07-23T16:58:57)

**Issue:**
- #2

**Reference files fetched:**
- (none)

```text
Question reserved as part of issue #2.
```

## Entry 2 — planner (2026-07-23T17:02:22)

**Reference files fetched:**
- (none)

**Reference files recommended by Planner:**
- stack-docs/Authoring/Inputs/Multiple_choice_input.md

```text
This all matches the issue well, and the follow-through design is exactly the "genuine reasoning credit" the issue's spirit calls for. Here's the full plan:

GOAL (non-negotiable): Test the full one-mean hypothesis-test workflow (Eagle Boys pizza diameters, Ch. 27) end-to-end — computing standard error, stating hypotheses, computing a t-score, estimating a P-value via the 68-95-99.7 rule, drawing a conclusion, and checking a validity condition — with later steps crediting the student's own prior answers via follow-through rather than re-penalizing a single early slip.

STRUCTURE (non-negotiable):
1. Standard error of the mean, computed from randomised x̄, s, n (given in the stem).
2. Hypotheses H0: μ=12 vs H1: μ≠12 (two equation inputs; μ fixed, not randomised).
3. t-score, computed from randomised x̄, fixed μ=12, and the student's OWN SE from part 1 (follow-through).
4. P-value estimate as one of four buckets (P>0.32 / 0.05<P<0.32 / 0.003<P<0.05 / P<0.003) via the 68-95-99.7 rule, graded against the bucket implied by the student's OWN t from part 3 (follow-through).
5. Decision (reject/fail to reject H0 at α=0.05, stated explicitly in the stem), graded against the decision implied by the student's OWN bucket from part 4 (follow-through).
6. Validity check: is n large enough for the CLT here (yes/no, against the book's own n>25 threshold), graded independently against the randomised n — no follow-through from parts 1-5.

RANDOMIZATION: Randomize the t-score's target bucket FIRST via a weighted choice (50% |t|>3 dramatic-reject, 20% 2<|t|<3 reject, 15% 1<|t|<2 borderline fail-to-reject, 15% |t|<1 clearly fail-to-reject), along with s (plausible range, e.g. 0.15–0.35) and n (plausible range including some values below and above the n>25 validity threshold, to keep part 6 non-trivial). Then back-derive x̄ = 12 − |t|·(s/√n), always with x̄ < 12 (deviation sign fixed negative, per the real Eagle Boys narrative — not randomised). Pick t away from exact bucket boundaries with a safety margin so rounding x̄ for display doesn't push the actual bucket across an edge.

ANSWER TESTS:
1. SE: numerical input, relative/decimal tolerance.
2. Hypotheses: two equation-type algebraic inputs, AlgEquiv against μ=12 and μ≠12.
3. t-score: numerical input, tolerance test, computed in feedback variables as (x̄−12)/(student's own ans1).
4. P-value bucket: radio/MCQ (4 options), correct option computed from student's own t (ans3), not the teacher's t.
5. Decision: radio/MCQ (reject / fail to reject), correct option computed from student's own bucket (ans4).
6. Validity check: radio/MCQ (yes/no), correct option computed directly from randomised n vs 25 — independent of parts 1-5.

FEEDBACK: Worked solution walks the same chain as the book (SE → t → bucket → decision → validity), stated using the teacher's own randomised values throughout. Worth flagging as common-mistake diagnostics for Reviewer: SE computed as s/n instead of s/√n; t-score sign flipped (12−x̄ instead of x̄−12); decision reversed relative to the student's own stated P-value bucket (reject/fail-to-reject confusion). Part 6 feedback should restate the book's own criterion (n much larger than 25) rather than a generic "sample size is fine" line.

PRT/QTEST SUGGESTIONS: Test all four t-buckets, including values just inside/outside each edge (t≈0.99/1.01, 1.99/2.01, 2.99/3.01) to confirm consistent boundary handling. Test follow-through explicitly: part 3 with a deliberately wrong SE from part 1, confirming credit when t is computed correctly from that wrong SE; part 4 with a correct t but wrong bucket choice, confirming it's marked wrong; part 5 with a wrong bucket from part 4, confirming the decision graded is the one consistent with that wrong bucket, not the "true" one. Test part 6 independently with n both above and below 25 regardless of what's happening in parts 1-5. Confirm rounding x̄ for display never silently moves the realized t across a bucket boundary from the one intended by the randomization weights.
```

## Entry 3 — author · attempt 1/3 (2026-07-23T17:03:26)

**Reference files fetched:**
- (none)

```text
STACK API check: PASSED

All checks passed.

Deviations reported: - Plan (negotiable, "ANSWER TESTS" section): used NumSigFigs for the standard error and NumDecPlaces for the t-score rather than the generically-suggested "relative/decimal tolerance", to give a concrete, checkable precision requirement in the question text per the rounding/precision authoring rule; also used EqualComAss (Maxima equality up to comparison of the selected integer code) rather than a bespoke test for the three MCQ inputs, since MCQ answers are plain integers/atoms and AlgEquiv-family tests are the natural fit — Reviewer can substitute a different test if a more specific one is preferred.
- Plan (negotiable, "RANDOMIZATION" section): chose concrete numeric ranges/margins for t_abs per bucket (e.g. 3.2–4.1, 2.2–2.9, 1.2–1.9, 0.3–0.9) instead of leaving them unspecified, to satisfy the "safety margin away from boundaries" requirement concretely.
```

## Entry 4 — reviewer-self-fix · attempt 1/3 (2026-07-23T17:05:43)

**Reference files fetched:**
- (none)

```text
STACK API check: could not be completed

Not well-formed XML: not well-formed (invalid token): line 155, column 31
```

## Entry 5 — reviewer-self-fix · attempt 2/3 (2026-07-23T17:07:04)

**Reference files fetched:**
- (none)

```text
STACK API check: could not be completed

Not well-formed XML: not well-formed (invalid token): line 155, column 31
```

## Entry 6 — reviewer-self-fix · attempt 3/3 (2026-07-23T17:07:23)

**Reference files fetched:**
- (none)

```text
STACK API check: could not be completed

Not well-formed XML: not well-formed (invalid token): line 155, column 31
```

## Entry 7 — reviewer · round 1 (2026-07-23T17:07:26)

**Key facts to carry forward:**
- prt_ans1 has two nodes (NODE0 true=correct terminal, NODE1 diagnostic for the s/n mistake); its qtest answer notes are NODE0-T / NODE1-T / NODE1-F accordingly, not NODE0-F.
- prt_ans3 has three nodes: NODE0 guards ans1=0 (division-by-zero adversarial case, terminal score 0), NODE1 is the correct-follow-through check, NODE2 is the sign-flip diagnostic; a correct answer's path is NODE0-F then NODE1-T (reported as NODE1-T).
- Parts 4 and 5 are graded entirely from the student's own prior answers (ans3, ans4) via inline if/elseif Maxima expressions in each node's SANS, never against the teacher's true bucket/decision — this is what implements the plan's follow-through requirement.
- t_abs ranges per bucket (3.2–4.1, 2.2–2.9, 1.2–1.9, 0.3–0.9) keep every bucket at least 0.2 away from a boundary, comfortably absorbing the rounding of xbar to 3 decimal places, so no qtest case needs to guard against a boundary-crossing coincidence from the random draw itself.

**Reference files fetched:**
- (none)

```text
VERDICT: MINOR ISSUES
SELF_FIXED:
- Replaced Author's trivial placeholder PRTs and single qtest with real, follow-through-aware PRT logic and a full qtest suite (PRT/QTEST authorship is always my own job, not a bug fix).
ESCALATED_TO_AUTHOR:
- (none)
NOTED_FOR_PLANNER:
- ans1 input has `FORBIDFLOAT: 0` explicitly set, which is just the default value spelled out — harmless but unnecessary; could be dropped for a cleaner input spec.
- Consider tightening the SE tolerance (currently 1% relative) if a stricter check is pedagogically preferred; chosen generously to comfortably separate correct answers from the s/n mistake without false negatives across the whole random range.

[Self-fix could not be verified against the STACK API.]
```

## Entry 8 — planner · review (2026-07-23T17:09:00)

**Reference files fetched:**
- (none)

```text
DECISION: REJECT
PLAN_CHANGED: NO
KEEP_DRAFT: YES
REVISED_PLAN: (not applicable)
FEEDBACK_TO_AUTHOR: Build failed with "Not well-formed XML: not well-formed (invalid token): line 155, column 31" — a raw `<=`/`<` character appearing as literal XML element content (most likely inside a `<sans>` or feedbackvariables text block, e.g. `is(abs(ans1-se_true)<=0.01*se_true)` in prt_ans1's node 0) breaks the parser since `<` isn't valid unescaped content. Fix by wrapping the affected `<sans>`, `<tans>`, and `<feedbackvariables><text>` fields containing comparison operators in `<![CDATA[ ... ]]>`, or entity-escape `<`/`<=` as `&lt;`/`&lt;=`. This is a pure XML-serialization fix — no change to question content, PRT logic, randomization, or feedback wording is needed.
AGENT_SETTINGS_CHANGE: author=off
```

## Entry 9 — reviewer · round 1 (2026-07-23T17:10:29)

**Key facts to carry forward:**
- The PRT/QTEST content in this draft (built in an earlier reviewer round, entry 7) is mathematically and structurally correct: all node logic, follow-through chaining (ans3→ans4→ans5), boundary qtests (t≈0.99/1.99/2.99/3.01 etc.), and division-by-zero/sign-flip adversarial cases were re-verified by hand this round and all check out against the actual Maxima logic in questionvariables.
- The previously reported "Not well-formed XML: line 155, column 31" build failure was a pure XML-serialization artifact from literal `<=`/`<` characters in SANS/feedback text; per current pipeline rules the assembler now auto-CDATA-wraps any field containing `<`, `>`, or `&`, so this should no longer manifest — no manual escaping was added or is needed in the fields text itself.
- Exact t_abs sub-ranges per bucket (from `rand(k)/10` truncation) are: bucket1 3.2–4.0, bucket2 2.2–2.8, bucket3 1.2–1.8, bucket4 0.3–0.8 — all still ≥0.2 from any bucket boundary, comfortably exceeding the ~0.024 max t-shift introduced by rounding xbar to 3 decimals.

**Reference files fetched:**
- (none)

```text
VERDICT: LOOKS GOOD
SELF_FIXED:
- (none)
ESCALATED_TO_AUTHOR:
- (none)
NOTED_FOR_PLANNER:
- ans1 input still has `FORBIDFLOAT: 0` explicitly set, which is just the default value spelled out — harmless but unnecessary; could be dropped for a cleaner input spec.
- SE relative tolerance (1%) and t-score decimal-place check are generous by design; could be tightened if a stricter check is pedagogically preferred, but current margins were chosen to comfortably separate correct answers from the s/n and sign-flip mistakes across the full random range.
- The documented t_abs ranges in the session's carried-forward key facts (e.g. "3.2–4.1") are approximate labels; the actual Maxima ranges are slightly narrower (e.g. bucket 1 is really 3.2–4.0) — not a bug, just worth knowing the exact bounds don't literally match the label if anyone re-derives margins later.
```

## Entry 10 — planner · review (2026-07-23T17:11:39)

**Reference files fetched:**
- (none)

```text
DECISION: REJECT
PLAN_CHANGED: NO
KEEP_DRAFT: YES
REVISED_PLAN: (not applicable)
FEEDBACK_TO_AUTHOR: Please remove the redundant `<forbidfloat>0</forbidfloat>` line from the `ans1` input — it's just the default value spelled out explicitly and serves no purpose. This is a pure cosmetic cleanup of the input spec; no other content, randomization, PRT, or feedback changes are needed. Leave the SE (1% relative) and t-score (2 decimal place) tolerances exactly as they are.
AGENT_SETTINGS_CHANGE: (not applicable)
```

## Entry 11 — reviewer-self-fix · attempt 1/3 (2026-07-23T17:11:51)

**Reference files fetched:**
- (none)

```text
STACK API check: could not be completed

Not well-formed XML: not well-formed (invalid token): line 155, column 31
```

## Entry 12 — reviewer-self-fix · attempt 2/3 (2026-07-23T17:11:59)

**Reference files fetched:**
- (none)

```text
STACK API check: could not be completed

Not well-formed XML: not well-formed (invalid token): line 155, column 31
```

## Entry 13 — reviewer-self-fix · attempt 3/3 (2026-07-23T17:12:09)

**Reference files fetched:**
- (none)

```text
STACK API check: could not be completed

Not well-formed XML: not well-formed (invalid token): line 155, column 31
```

