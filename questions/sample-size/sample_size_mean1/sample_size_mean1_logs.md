# Metadata — sample-size/sample_size_mean1/sample_size_mean1.xml

Running record of every agent (and user) action on this question that
isn't the XML itself: the reasoning, findings, improvement notes, and
reference lookups behind each change. Entries are appended in order,
newest at the bottom. The XML changes themselves are recorded by git —
this file holds the substance and meaning behind them, not the diffs.

## Entry 1 — concierge (2026-07-23T15:16:26)

**Issue:**
- #8

**Closes on merge:**
- yes

**Reference files fetched:**
- (none)

```text
Question reserved as part of issue #8.
```

## Entry 2 — planner (2026-07-23T18:25:00)

**Reference files fetched:**
- (none)

**Reference files recommended by Planner:**
- stack-docs/Authoring/Inputs/Multiple_choice_input.md

```text
Good catch — moving that into RANDOMIZATION as a hard construction constraint rather than leaving it to be caught after the fact.

GOAL (non-negotiable): Test whether a student can (a) compute the required sample size for a mean's confidence interval from z, s, and a margin of error, and (b) understand how required sample size scales with margin of error and with confidence level — not just recall fixed multipliers.

STRUCTURE (non-negotiable):
1. Compute n1 = ceil((z·s/E1)²) for a given s, E1, at 95% confidence. Numeric input.
2. Given a new margin E1/r2 (r2 an integer), compute the new required n. Correct answer is the student's own n1 (from part 1) × r2², graded via follow-through — so an arithmetic slip in part 1 doesn't cost them part 2, but a wrong scaling relationship does.
3. Same as part 2, with an independent integer ratio r3 (different from r2), also following through from the student's own part-1 n1 independently (not chained through part 2).
4. MCQ: "Would a smaller or larger sample be needed for the same margin E1, at [90%/99%] confidence instead of 95%?" — options larger/smaller/same/can't tell. Direction (90% vs 95%, or 99% vs 95%) randomized. No follow-through needed — doesn't depend on earlier parts' numeric answers.

RANDOMIZATION:
- s: decimal in a sensible range, e.g. [0.5, 2.0] kg.
- E1: drawn from a small set of round margins, e.g. {0.2, 0.3, 0.4, 0.5} kg.
- r2: integer from a small set, e.g. {2, 3, 4}.
- r3: integer from the same set **excluding whatever r2 came out as**, enforced at construction (e.g. sample r3 from `set - {r2}`) — not merely checked afterward — so parts 2 and 3 can never be redundant for any student.
- Part 4 direction: randomly 90%-vs-95% (→ smaller) or 99%-vs-95% (→ larger), so "larger" isn't a free answer.
- Confidence level for parts 1–3 fixed at 95% (book convention), z = 1.96.

ANSWER TESTS:
- Parts 1–3: numeric input, integer expected value, tested via AlgEquiv/numeric equivalence (exact integer match — ceiling means no tolerance needed).
- Part 2/3 follow-through: expected answer is a function of the student's own valid part-1 input, not a fixed teacher value.
- Part 4: MCQ (radio), single correct option.

FEEDBACK:
- Parts 1–3: show the formula n=(z·s/E)² substituted with the actual numbers, and the ceiling step explicitly, in general feedback.
- Parts 2/3: feedback should distinguish "wrong scaling relationship" (used a different power/multiplier than r²) from "correct scaling but propagated part-1 arithmetic error" (matches follow-through formula) — worth flagging to Reviewer as a diagnostic.
- Part 4: feedback should explain the precision/confidence tradeoff — higher confidence requires a larger critical value z, hence larger n for the same margin.

PRT/QTEST SUGGESTIONS:
- Test part 2/3 follow-through explicitly: submit an intentionally wrong part-1 answer (e.g. off by a small amount) and confirm part 2/3's expected value scales from that wrong value, not from the true n1.
- Test the boundary case where (z·s/E)² is already an exact integer (no actual rounding needed) — ceiling should be a no-op, not silently add 1.
- Test part 4 for both randomized directions (90%-vs-95% and 99%-vs-95%) to make sure the correct MCQ option flips correctly with the direction variable, not hardcoded to "larger."
```

## Entry 3 — author · attempt 1/3 (2026-07-23T18:25:33)

**Reference files fetched:**
- (none)

```text
STACK API check: PASSED

All checks passed.

Deviations reported: - STRUCTURE (non-negotiable), part 2/3 follow-through: I set each part's TANS to the fixed teacher value (n1*r2^2, n1*r3^2) rather than an expression depending on the student's own ans1, since my scope is limited to declaring TYPE/TANS/ANSWERTEST per input, not PRT logic — the actual follow-through comparison (using the student's submitted ans1 rather than the true n1) must be implemented by Reviewer in the PRT's feedback variables/answer tests, as the plan itself anticipates ("graded via follow-through"). Flagging this explicitly so Reviewer builds ans2/ans3's PRTs to use the student's own ans1 value, not the fixed n1.
- Also flagging per the plan's own note: Reviewer should build the "wrong scaling relationship" vs "correct scaling, propagated part-1 error" diagnostic distinction for parts 2/3, and test both randomized directions for part 4, per the PRT/QTEST SUGGESTIONS section.
```

## Entry 4 — reviewer-self-fix · attempt 1/3 (2026-07-23T18:26:47)

**Reference files fetched:**
- (none)

```text
STACK API check: PASSED

All checks passed.
```

## Entry 5 — reviewer · round 1 (2026-07-23T18:26:50)

**Key facts to carry forward:**
- Part 2/3 PRTs grade follow-through against the student's own submitted `ans1` (e.g. `ans1*r2^2`), not the fixed teacher `n1`, per the plan's non-negotiable structure — Author's draft had wrongly used fixed `n2`/`n3` teacher values, corrected here.
- The linear-scaling mistake distractor (`ans1*r2` instead of `ans1*r2^2`) is safe from degeneracy for all r2/r3 in {2,3,4} since `r^2 ≠ r` for every value in that range, so it never coincides with the correct follow-through answer.
- Part 4's two randomized directions (90-vs-95, 99-vs-95) can't both be exercised by qtest cases within one variant, since `dir` is fixed once per variant — only one direction is ever testable per deployed seed.

**Reference files fetched:**
- (none)

```text
VERDICT: NEEDS REVISION
SELF_FIXED:
- Built the real PRT logic and qtest cases for all four inputs (Author only left placeholder trivial PRTs, as expected — this is squarely my job per scope). This included implementing the plan's mandatory Part 2/3 follow-through logic (grading against the student's own submitted `ans1`, not the fixed teacher `n1`), and a diagnostic node distinguishing a "wrong scaling power" mistake (student multiplied by `r2`/`r3` instead of `r2^2`/`r3^2`) from other wrong answers.
ESCALATED_TO_AUTHOR:
- (none)
NOTED_FOR_PLANNER:
- Only one of the two Part-4 randomized directions (90-vs-95 or 99-vs-95) can ever be exercised by a qtest for a given variant, since `dir` is a question variable fixed once per variant — genuinely testing both directions would require two separately-seeded variants/deployments, which is outside qtest's scope. Noted as a limitation of the "test both directions" suggestion, not a bug.
```

## Entry 6 — planner · review (2026-07-23T18:28:33)

**Reference files fetched:**
- (none)

```text
Good catch — that's a real display bug in the question variables, not something Reviewer's PRT/qtest work can fix, since it's about how `s` itself is defined. This needs to go back to Author.

DECISION: REJECT
PLAN_CHANGED: NO
KEEP_DRAFT: YES
REVISED_PLAN: (not applicable)
FEEDBACK_TO_AUTHOR: In the question variables, `s: (5+rand(16))/10;` stays an exact Maxima rational (e.g. 6/5, 4/5) rather than a clean decimal, since 5, rand(16), and 10 are all integers — so `{@s@}` in the question text/questionnote can display as "6/5 kg" instead of "1.2 kg", which doesn't match how a standard deviation would normally be stated. Fix by forcing float arithmetic in the definition itself, e.g. `s: (5+rand(16))/10.0;` (or wrap in `float(...)`), so `s` always renders as a one-decimal number regardless of which integer `rand(16)` draws. Everything downstream (n1, n2, n3 computations) remains mathematically consistent either way — this is purely a display/authoring fix to the variable definition, not a PRT change.
AGENT_SETTINGS_CHANGE: (not applicable)
```

## Entry 7 — author · attempt 1/3 (2026-07-23T18:28:42)

**Reference files fetched:**
- (none)

```text
STACK API check: PASSED

All checks passed.
```

## Entry 8 — reviewer · round 1 (2026-07-23T18:29:46)

**Key facts to carry forward:**
- Verified all 5 qtest cases against the actual PRT node logic (NODE0/NODE1 routing, TRUESCORE overrides, default false-branch scoring) and all expected scores/penalties/notes are consistent with STACK's terminal-node-only penalty rule.
- Confirmed no degenerate coincidences in the qtest wrong-answer cases: n1*r2 ≠ n1*r2^2 for all r2∈{2,3,4} given n1≥1 (verified n1's true range is [4,385] across the s/E1 randomization), and n1*r2^2+7 ≠ n1*r2 always since the RHS-minus-7 term is strictly negative.

**Reference files fetched:**
- (none)

```text
VERDICT: LOOKS GOOD
SELF_FIXED:
- (none)
ESCALATED_TO_AUTHOR:
- (none)
NOTED_FOR_PLANNER:
- The plan's suggested "boundary case where (z·s/E)² is already an exact integer" qtest is not actually constructible: n1 is derived from randomized s/E1 via question variables, and qtest can only supply input values, not override s/E1 to force an exact square — so this suggestion can't be exercised deterministically without a dedicated non-random variant, similar to the already-noted part-4 direction limitation.
- Minor style nit (not a bug): question variables introduce indirection symbols `option_larger`/`option_smaller`/`option_same`/`option_cant` purely to hold atoms `larger`/`smaller`/`same_size`/`cant_tell` — functionally fine, but could be simplified by using the atoms directly in `mcq_ans` without the extra aliasing variables.
```

