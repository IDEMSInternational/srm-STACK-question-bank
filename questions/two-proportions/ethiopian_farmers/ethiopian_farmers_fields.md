QUESTIONTEXT:
<p>A study compares the adoption of a new technology between small firms and large firms. The observed data are:</p>

<table border="1" cellpadding="6" style="border-collapse:collapse; text-align:center;">
<tr><th></th><th>Adopters</th><th>Non-adopters</th><th>Total</th></tr>
<tr><th>Small firms</th><td>{@A@}</td><td>{@B@}</td><td>{@A+B@}</td></tr>
<tr><th>Large firms</th><td>{@C@}</td><td>{@D@}</td><td>{@C+D@}</td></tr>
</table>

<h4>Thread 1: Difference in proportions</h4>

<p>(a) Which of the following correctly defines the quantity we compare in a two-proportion test here?</p>
[[input:ans1a]] [[validation:ans1a]] [[feedback:prt_ans1a]]

<p>(b) Enter the sample proportion of non-adopters in each group, as a list \([\hat p_{\text{small}}, \hat p_{\text{large}}]\), to at least 3 decimal places.</p>
[[input:ans1b]] [[validation:ans1b]] [[feedback:prt_ans1b]]

<p>(c) Using your own values from part (b), compute the pooled two-proportion \(z\)-statistic for testing \(H_0: p_{\text{small}}=p_{\text{large}}\).</p>
[[input:ans1c]] [[validation:ans1c]] [[feedback:prt_ans1c]]

<p>(d) Based on your \(z\)-statistic from part (c), and a significance level where the critical value is \(\pm 1.96\), what is your conclusion?</p>
[[input:ans1d]] [[validation:ans1d]] [[feedback:prt_ans1d]]

<p>(e) Using your values from part (b), give a 95% confidence interval for \(p_{\text{small}}-p_{\text{large}}\) (unpooled standard error), as a list \([\text{lower},\text{upper}]\).</p>
[[input:ans1e]] [[validation:ans1e]] [[feedback:prt_ans1e]]

<h4>Thread 2: Odds ratio</h4>

<p>(a) Which of the following correctly defines the odds ratio being compared here?</p>
[[input:ans2a]] [[validation:ans2a]] [[feedback:prt_ans2a]]

<p>(b) Enter the odds of non-adoption (non-adopters ÷ adopters) in each group, as a list \([\text{odds}_{\text{small}}, \text{odds}_{\text{large}}]\), to at least 3 decimal places.</p>
[[input:ans2b]] [[validation:ans2b]] [[feedback:prt_ans2b]]

<p>(c) Using your own values from part (b), compute the chi-square test statistic for independence in this table.</p>
[[input:ans2c]] [[validation:ans2c]] [[feedback:prt_ans2c]]

<p>(d) Based on your \(\chi^2\)-statistic from part (c), and a critical value of \(3.84\), what is your conclusion?</p>
[[input:ans2d]] [[validation:ans2d]] [[feedback:prt_ans2d]]

<p>(e) Using your values from part (b), give a 95% confidence interval for the odds ratio, as a list \([\text{lower},\text{upper}]\).</p>
[[input:ans2e]] [[validation:ans2e]] [[feedback:prt_ans2e]]

<h4>Validity check</h4>

<p>(a) What is the smallest expected cell count in this table, to 2 decimal places?</p>
[[input:ans3a]] [[validation:ans3a]] [[feedback:prt_ans3a]]

<p>(b) Based on your answer to (a), is the chi-square approximation valid for this table?</p>
[[input:ans3b]] [[validation:ans3b]] [[feedback:prt_ans3b]]

QUESTIONVARIABLES:
regime: rand([0,1]);

if regime=0 then (
  n_small_total: rand(80)+80,
  n_large_total: rand(80)+80,
  p_small_true: (rand(30)+20)/100,
  p_large_true: (rand(30)+5)/100
) else (
  n_small_total: rand(15)+10,
  n_large_total: rand(15)+10,
  p_small_true: (rand(40)+10)/100,
  p_large_true: (rand(40)+10)/100
);

B: round(n_small_total*p_small_true);
A: n_small_total - B;
D: round(n_large_total*p_large_true);
C: n_large_total - D;

s_assert(is(A>0 and B>0 and C>0 and D>0), true);

N: A+B+C+D;
n_s: A+B;
n_l: C+D;

p_hat_small: float(B/n_s);
p_hat_large: float(D/n_l);
diff_true: p_hat_small - p_hat_large;

p_pool: float((B+D)/N);
se_pooled: sqrt(p_pool*(1-p_pool)*(1/n_s+1/n_l));
z_true: float(diff_true/se_pooled);

se_unpooled: sqrt(p_hat_small*(1-p_hat_small)/n_s + p_hat_large*(1-p_hat_large)/n_l);
ci_diff_lower: float(diff_true - 1.96*se_unpooled);
ci_diff_upper: float(diff_true + 1.96*se_unpooled);

decision1_true: if abs(z_true)>1.96 then "reject" else "fail to reject";

odds_small_true: float(B/A);
odds_large_true: float(D/C);
OR_true: float(odds_small_true/odds_large_true);

chisq_true: float(N*(A*D-B*C)^2/((A+B)*(C+D)*(A+C)*(B+D)));
decision2_true: if chisq_true>3.84 then "reject" else "fail to reject";

se_logOR: sqrt(1/A+1/B+1/C+1/D);
ci_OR_lower: float(OR_true*exp(-1.96*se_logOR));
ci_OR_upper: float(OR_true*exp(1.96*se_logOR));

E_AA: float((A+B)*(A+C)/N);
E_AB: float((A+B)*(B+D)/N);
E_CA: float((C+D)*(A+C)/N);
E_CD: float((C+D)*(B+D)/N);
min_expected_true: min(E_AA,E_AB,E_CA,E_CD);

validity_true: if min_expected_true>=5 then "valid" else "invalid";

ta_mcq1a: [
  [1, true, "\\( \\hat p_{\\text{small}} - \\hat p_{\\text{large}} \\), the difference in proportions of <em>non-adopters</em> between groups"],
  [2, false, "\\( \\hat p_{\\text{large}} - \\hat p_{\\text{small}} \\), the difference in proportions of non-adopters between groups"],
  [3, false, "\\( \\hat p_{\\text{small}} - \\hat p_{\\text{large}} \\), the difference in proportions of <em>adopters</em> between groups"],
  [4, false, "The difference in raw counts of non-adopters between the two groups"]
];

ta_mcq2a: [
  [1, true, "\\( OR = \\dfrac{\\text{odds of non-adoption, small firms}}{\\text{odds of non-adoption, large firms}} \\)"],
  [2, false, "\\( OR = \\dfrac{\\text{odds of adoption, small firms}}{\\text{odds of adoption, large firms}} \\)"],
  [3, false, "\\( OR = \\dfrac{\\text{odds of non-adoption, large firms}}{\\text{odds of non-adoption, small firms}} \\)"],
  [4, false, "\\( OR = \\) the difference in proportions of non-adopters between the two groups"]
];

decision1_opts: [
  [1, is(decision1_true="reject"), "Reject \\(H_0\\): there is evidence of a difference in non-adoption proportions"],
  [2, is(decision1_true="fail to reject"), "Fail to reject \\(H_0\\): insufficient evidence of a difference in non-adoption proportions"]
];

decision2_opts: [
  [1, is(decision2_true="reject"), "Reject \\(H_0\\): there is evidence the odds ratio differs from 1"],
  [2, is(decision2_true="fail to reject"), "Fail to reject \\(H_0\\): insufficient evidence the odds ratio differs from 1"]
];

validity_opts: [
  [1, is(validity_true="valid"), "Valid — all expected cell counts are at least 5"],
  [2, is(validity_true="invalid"), "Invalid — at least one expected cell count is below 5"]
];

/* Test-support variables, used only to build qtest input expressions below. */
test_wrong_p_small: p_hat_small+0.1;
test_wrong_p_pool: (test_wrong_p_small*n_s+p_hat_large*n_l)/(n_s+n_l);
test_wrong_se_pooled: sqrt(test_wrong_p_pool*(1-test_wrong_p_pool)*(1/n_s+1/n_l));
test_wrong_z: (test_wrong_p_small-p_hat_large)/test_wrong_se_pooled;
test_wrong_decision_opt: if abs(test_wrong_z)>1.96 then 1 else 2;
test_wrong_se_unpooled: sqrt(test_wrong_p_small*(1-test_wrong_p_small)/n_s+p_hat_large*(1-p_hat_large)/n_l);
test_wrong_ci_lower: (test_wrong_p_small-p_hat_large)-1.96*test_wrong_se_unpooled;
test_wrong_ci_upper: (test_wrong_p_small-p_hat_large)+1.96*test_wrong_se_unpooled;

test_wrong_odds_small: odds_small_true+0.1;
test_wrong_A: n_s/(1+test_wrong_odds_small);
test_wrong_B: n_s-test_wrong_A;
test_wrong_C: n_l/(1+odds_large_true);
test_wrong_D: n_l-test_wrong_C;
test_wrong_chisq: (n_s+n_l)*(test_wrong_A*test_wrong_D-test_wrong_B*test_wrong_C)^2/((test_wrong_A+test_wrong_B)*(test_wrong_C+test_wrong_D)*(test_wrong_A+test_wrong_C)*(test_wrong_B+test_wrong_D));
test_wrong_decision2_opt: if test_wrong_chisq>3.84 then 1 else 2;
test_wrong_OR: test_wrong_odds_small/odds_large_true;
test_wrong_se_logOR: sqrt(1/test_wrong_A+1/test_wrong_B+1/test_wrong_C+1/test_wrong_D);
test_wrong_ci_OR_lower: test_wrong_OR*exp(-1.96*test_wrong_se_logOR);
test_wrong_ci_OR_upper: test_wrong_OR*exp(1.96*test_wrong_se_logOR);

GENERALFEEDBACK:
<p>The observed table was:</p>
<table border="1" cellpadding="6" style="border-collapse:collapse; text-align:center;">
<tr><th></th><th>Adopters</th><th>Non-adopters</th><th>Total</th></tr>
<tr><th>Small firms</th><td>{@A@}</td><td>{@B@}</td><td>{@A+B@}</td></tr>
<tr><th>Large firms</th><td>{@C@}</td><td>{@D@}</td><td>{@C+D@}</td></tr>
</table>

<h4>Thread 1: proportion difference</h4>
<p>\(\hat p_{\text{small}} = {@p_hat_small@}\), \(\hat p_{\text{large}} = {@p_hat_large@}\), so the difference is \({@diff_true@}\).</p>
<p>The pooled standard error (used for the hypothesis test) uses the pooled proportion \(\hat p = {@p_pool@}\), giving \(z = {@z_true@}\).</p>
<p>The (unpooled) standard error, used for the confidence interval, uses each group's own \(\hat p\) separately, giving a 95% CI of \([{@ci_diff_lower@}, {@ci_diff_upper@}]\).</p>
<p>Since \(|z| {@if abs(z_true)>1.96 then ">" else "\\le"@} 1.96\), we {@decision1_true@} \(H_0\).</p>

<h4>Thread 2: odds ratio</h4>
<p>\(\text{odds}_{\text{small}} = {@odds_small_true@}\), \(\text{odds}_{\text{large}} = {@odds_large_true@}\), so \(OR = {@OR_true@}\).</p>
<p>The chi-square statistic for this table is \(\chi^2 = {@chisq_true@}\), and the 95% CI for the odds ratio is \([{@ci_OR_lower@}, {@ci_OR_upper@}]\).</p>
<p>Since \(\chi^2 {@if chisq_true>3.84 then ">" else "\\le"@} 3.84\), we {@decision2_true@} \(H_0\).</p>

<p><strong>Key point:</strong> the pooled two-proportion \(z\)-test and the chi-square test of independence on a 2×2 table are mathematically equivalent — \(\chi^2 = z^2\) exactly, and \(1.96^2 = 3.8416 \approx 3.84\). So the two hypothesis-test decisions above will always agree. (Note the difference between the pooled standard error used for the test statistics and the unpooled standard error used for the confidence intervals — this is why a CI-based conclusion can occasionally look slightly different from the test-statistic conclusion near a boundary, even though the two hypothesis tests themselves always agree with each other.)</p>

<h4>Validity</h4>
<p>The smallest expected cell count is \({@min_expected_true@}\), so the chi-square approximation is {@validity_true@} here.</p>

QUESTIONNOTE:
\(A={@A@}, B={@B@}, C={@C@}, D={@D@}\), regime={@regime@}

INPUT ans1a:
TYPE: radio
TANS: ta_mcq1a
ANSWERTEST: String
SHOWVALIDATION: 0

INPUT ans1b:
TYPE: algebraic
TANS: [p_hat_small, p_hat_large]
ANSWERTEST: NumRelative

INPUT ans1c:
TYPE: algebraic
TANS: z_true
ANSWERTEST: NumRelative

INPUT ans1d:
TYPE: radio
TANS: decision1_opts
ANSWERTEST: String
SHOWVALIDATION: 0

INPUT ans1e:
TYPE: algebraic
TANS: [ci_diff_lower, ci_diff_upper]
ANSWERTEST: NumRelative

INPUT ans2a:
TYPE: radio
TANS: ta_mcq2a
ANSWERTEST: String
SHOWVALIDATION: 0

INPUT ans2b:
TYPE: algebraic
TANS: [odds_small_true, odds_large_true]
ANSWERTEST: NumRelative

INPUT ans2c:
TYPE: algebraic
TANS: chisq_true
ANSWERTEST: NumRelative

INPUT ans2d:
TYPE: radio
TANS: decision2_opts
ANSWERTEST: String
SHOWVALIDATION: 0

INPUT ans2e:
TYPE: algebraic
TANS: [ci_OR_lower, ci_OR_upper]
ANSWERTEST: NumRelative

INPUT ans3a:
TYPE: algebraic
TANS: min_expected_true
ANSWERTEST: NumDecPlaces

INPUT ans3b:
TYPE: radio
TANS: validity_opts
ANSWERTEST: String
SHOWVALIDATION: 0

PRT prt_ans1a:
NODE 0:
SANS: ans1a
TANS: 1

PRT prt_ans1b:
NODE 0:
SANS: if not(listp(ans1b) and length(ans1b)=2) then false else is(abs(float(ans1b[1])-p_hat_small)<0.001 and abs(float(ans1b[2])-p_hat_large)<0.001)
TANS: true
TRUEFEEDBACK: <p>Correct — this matches the sample proportions of non-adopters computed from the table.</p>
FALSEFEEDBACK: <p>Not correct. Recompute \(\hat p_{\text{small}}\) and \(\hat p_{\text{large}}\) as (non-adopters)/(row total) in each group.</p>

PRT prt_ans1c:
NODE 0:
SANS: block([spv, sps, spl, ppool, sepool, zsa], spv: listp(ans1b) and length(ans1b)=2, sps: if spv then float(ans1b[1]) else p_hat_small, spl: if spv then float(ans1b[2]) else p_hat_large, ppool: (sps*n_s+spl*n_l)/(n_s+n_l), sepool: sqrt(ppool*(1-ppool)*(1/n_s+1/n_l)), zsa: if sepool=0 then 0 else (sps-spl)/sepool, is(numberp(ans1c) and abs(ans1c-zsa)<0.01))
TANS: true
TRUEFEEDBACK: <p>Correct, using the pooled standard error and your own \(\hat p\) pair from part (b) (not necessarily the table's true values).</p>
FALSEFEEDBACK: <p>Not correct. Recompute \(z\) using the pooled standard error and your own \(\hat p\) pair from part (b).</p>

PRT prt_ans1d:
NODE 0:
SANS: block([dsa, optsa], dsa: if not numberp(ans1c) then "undetermined" elseif abs(ans1c)>1.96 then "reject" else "fail to reject", optsa: if dsa="reject" then 1 elseif dsa="fail to reject" then 2 else -1, is(ans1d=optsa))
TANS: true
TRUEFEEDBACK: <p>Correct — this is the right conclusion given your own \(z\)-statistic from part (c).</p>
FALSEFEEDBACK: <p>Not correct given your own \(z\)-statistic from part (c): compare \(|z|\) to 1.96.</p>

PRT prt_ans1e:
NODE 0:
SANS: block([spv, sps, spl, seunp, diffsa, cilo, ciup], spv: listp(ans1b) and length(ans1b)=2, sps: if spv then float(ans1b[1]) else p_hat_small, spl: if spv then float(ans1b[2]) else p_hat_large, seunp: sqrt(sps*(1-sps)/n_s+spl*(1-spl)/n_l), diffsa: sps-spl, cilo: diffsa-1.96*seunp, ciup: diffsa+1.96*seunp, if not(listp(ans1e) and length(ans1e)=2) then false else is(abs(float(ans1e[1])-cilo)<0.01 and abs(float(ans1e[2])-ciup)<0.01))
TANS: true
TRUEFEEDBACK: <p>Correct, using the unpooled standard error and your own \(\hat p\) pair from part (b).</p>
FALSEFEEDBACK: <p>Not correct. Recompute the CI using the unpooled standard error and your own \(\hat p\) pair from part (b).</p>

PRT prt_ans2a:
NODE 0:
SANS: ans2a
TANS: 1

PRT prt_ans2b:
NODE 0:
SANS: if not(listp(ans2b) and length(ans2b)=2) then false else is(abs(float(ans2b[1])-odds_small_true)<0.01 and abs(float(ans2b[2])-odds_large_true)<0.01)
TANS: true
TRUEFEEDBACK: <p>Correct — these are the odds of non-adoption in each group.</p>
FALSEFEEDBACK: <p>Not correct. Odds of non-adoption = non-adopters \(\div\) adopters, in each group.</p>

PRT prt_ans2c:
NODE 0:
SANS: block([osv, osa, ola, Asa, Bsa, Csa, Dsa, chisa], osv: listp(ans2b) and length(ans2b)=2, osa: if osv then float(ans2b[1]) else odds_small_true, ola: if osv then float(ans2b[2]) else odds_large_true, Asa: n_s/(1+osa), Bsa: n_s-Asa, Csa: n_l/(1+ola), Dsa: n_l-Csa, chisa: if (Asa+Bsa)*(Csa+Dsa)*(Asa+Csa)*(Bsa+Dsa)=0 then 0 else (n_s+n_l)*(Asa*Dsa-Bsa*Csa)^2/((Asa+Bsa)*(Csa+Dsa)*(Asa+Csa)*(Bsa+Dsa)), is(numberp(ans2c) and abs(ans2c-chisa)<0.05))
TANS: true
TRUEFEEDBACK: <p>Correct, recomputed from your own odds pair from part (b).</p>
FALSEFEEDBACK: <p>Not correct given your own odds pair from part (b): rebuild the implied 2x2 table from those odds and each group's row total, then recompute \(\chi^2\).</p>

PRT prt_ans2d:
NODE 0:
SANS: block([dsa, optsa], dsa: if not numberp(ans2c) then "undetermined" elseif ans2c>3.84 then "reject" else "fail to reject", optsa: if dsa="reject" then 1 elseif dsa="fail to reject" then 2 else -1, is(ans2d=optsa))
TANS: true
TRUEFEEDBACK: <p>Correct — this is the right conclusion given your own \(\chi^2\)-statistic from part (c).</p>
FALSEFEEDBACK: <p>Not correct given your own \(\chi^2\)-statistic from part (c): compare it to 3.84.</p>

PRT prt_ans2e:
NODE 0:
SANS: block([osv, osa, ola, Asa, Bsa, Csa, Dsa, ORsa, selog, cilo, ciup], osv: listp(ans2b) and length(ans2b)=2, osa: if osv then float(ans2b[1]) else odds_small_true, ola: if osv then float(ans2b[2]) else odds_large_true, Asa: n_s/(1+osa), Bsa: n_s-Asa, Csa: n_l/(1+ola), Dsa: n_l-Csa, ORsa: if ola=0 then 0 else osa/ola, selog: if Asa<=0 or Bsa<=0 or Csa<=0 or Dsa<=0 then 0 else sqrt(1/Asa+1/Bsa+1/Csa+1/Dsa), cilo: ORsa*exp(-1.96*selog), ciup: ORsa*exp(1.96*selog), if not(listp(ans2e) and length(ans2e)=2) then false else is(abs(float(ans2e[1])-cilo)<0.05 and abs(float(ans2e[2])-ciup)<0.05))
TANS: true
TRUEFEEDBACK: <p>Correct, using your own odds pair from part (b).</p>
FALSEFEEDBACK: <p>Not correct. Recompute the CI for the odds ratio using your own odds pair from part (b).</p>

PRT prt_ans3a:
NODE 0:
SANS: is(numberp(ans3a) and abs(ans3a-min_expected_true)<0.01)
TANS: true
TRUEFEEDBACK: <p>Correct — this is the smallest expected cell count in the table.</p>
FALSEFEEDBACK: <p>Not correct. Expected count for a cell = (row total \(\times\) column total)/grand total; find the smallest across all four cells.</p>

PRT prt_ans3b:
NODE 0:
SANS: block([vsa, optsa], vsa: if not numberp(ans3a) then "undetermined" elseif ans3a>=5 then "valid" else "invalid", optsa: if vsa="valid" then 1 elseif vsa="invalid" then 2 else -1, is(ans3b=optsa))
TANS: true
TRUEFEEDBACK: <p>Correct given your own answer to part (a): compare it to the threshold of 5.</p>
FALSEFEEDBACK: <p>Not correct given your own answer to part (a): compare it to the threshold of 5.</p>

QTEST 1:
DESCRIPTION: Fully correct answers (both regimes)
INPUT ans1a: 1
INPUT ans1b: [p_hat_small, p_hat_large]
INPUT ans1c: z_true
INPUT ans1d: first(mcq_correct(decision1_opts))
INPUT ans1e: [ci_diff_lower, ci_diff_upper]
INPUT ans2a: 1
INPUT ans2b: [odds_small_true, odds_large_true]
INPUT ans2c: chisq_true
INPUT ans2d: first(mcq_correct(decision2_opts))
INPUT ans2e: [ci_OR_lower, ci_OR_upper]
INPUT ans3a: min_expected_true
INPUT ans3b: first(mcq_correct(validity_opts))
EXPECT prt_ans1a: NODE0-T
EXPECT prt_ans1b: NODE0-T
EXPECT prt_ans1c: NODE0-T
EXPECT prt_ans1d: NODE0-T
EXPECT prt_ans1e: NODE0-T
EXPECT prt_ans2a: NODE0-T
EXPECT prt_ans2b: NODE0-T
EXPECT prt_ans2c: NODE0-T
EXPECT prt_ans2d: NODE0-T
EXPECT prt_ans2e: NODE0-T
EXPECT prt_ans3a: NODE0-T
EXPECT prt_ans3b: NODE0-T

QTEST 2:
DESCRIPTION: Wrong MCQ definitions (ans1a, ans2a), everything else correct
INPUT ans1a: 2
INPUT ans1b: [p_hat_small, p_hat_large]
INPUT ans1c: z_true
INPUT ans1d: first(mcq_correct(decision1_opts))
INPUT ans1e: [ci_diff_lower, ci_diff_upper]
INPUT ans2a: 3
INPUT ans2b: [odds_small_true, odds_large_true]
INPUT ans2c: chisq_true
INPUT ans2d: first(mcq_correct(decision2_opts))
INPUT ans2e: [ci_OR_lower, ci_OR_upper]
INPUT ans3a: min_expected_true
INPUT ans3b: first(mcq_correct(validity_opts))
EXPECT prt_ans1a: NODE0-F
EXPECT prt_ans2a: NODE0-F
EXPECT prt_ans1b: NODE0-T
EXPECT prt_ans1c: NODE0-T
EXPECT prt_ans1d: NODE0-T
EXPECT prt_ans1e: NODE0-T
EXPECT prt_ans2b: NODE0-T
EXPECT prt_ans2c: NODE0-T
EXPECT prt_ans2d: NODE0-T
EXPECT prt_ans2e: NODE0-T
EXPECT prt_ans3a: NODE0-T
EXPECT prt_ans3b: NODE0-T

QTEST 3:
DESCRIPTION: Thread 1 wrong-but-consistent follow-through (wrong p-hat pair, correctly propagated)
INPUT ans1a: 1
INPUT ans1b: [test_wrong_p_small, p_hat_large]
INPUT ans1c: test_wrong_z
INPUT ans1d: test_wrong_decision_opt
INPUT ans1e: [test_wrong_ci_lower, test_wrong_ci_upper]
INPUT ans2a: 1
INPUT ans2b: [odds_small_true, odds_large_true]
INPUT ans2c: chisq_true
INPUT ans2d: first(mcq_correct(decision2_opts))
INPUT ans2e: [ci_OR_lower, ci_OR_upper]
INPUT ans3a: min_expected_true
INPUT ans3b: first(mcq_correct(validity_opts))
EXPECT prt_ans1b: NODE0-F
EXPECT prt_ans1c: NODE0-T
EXPECT prt_ans1d: NODE0-T
EXPECT prt_ans1e: NODE0-T

QTEST 4:
DESCRIPTION: Thread 2 wrong-but-consistent follow-through (wrong odds pair, correctly propagated)
INPUT ans1a: 1
INPUT ans1b: [p_hat_small, p_hat_large]
INPUT ans1c: z_true
INPUT ans1d: first(mcq_correct(decision1_opts))
INPUT ans1e: [ci_diff_lower, ci_diff_upper]
INPUT ans2a: 1
INPUT ans2b: [test_wrong_odds_small, odds_large_true]
INPUT ans2c: test_wrong_chisq
INPUT ans2d: test_wrong_decision2_opt
INPUT ans2e: [test_wrong_ci_OR_lower, test_wrong_ci_OR_upper]
INPUT ans3a: min_expected_true
INPUT ans3b: first(mcq_correct(validity_opts))
EXPECT prt_ans2b: NODE0-F
EXPECT prt_ans2c: NODE0-T
EXPECT prt_ans2d: NODE0-T
EXPECT prt_ans2e: NODE0-T

QTEST 5:
DESCRIPTION: Adversarial edge case - ans1b submitted as an empty list; guard should fall back to true values downstream
INPUT ans1a: 1
INPUT ans1b: []
INPUT ans1c: z_true
INPUT ans1d: first(mcq_correct(decision1_opts))
INPUT ans1e: [ci_diff_lower, ci_diff_upper]
INPUT ans2a: 1
INPUT ans2b: [odds_small_true, odds_large_true]
INPUT ans2c: chisq_true
INPUT ans2d: first(mcq_correct(decision2_opts))
INPUT ans2e: [ci_OR_lower, ci_OR_upper]
INPUT ans3a: min_expected_true
INPUT ans3b: first(mcq_correct(validity_opts))
EXPECT prt_ans1b: NODE0-F
EXPECT prt_ans1c: NODE0-T
EXPECT prt_ans1e: NODE0-T

QTEST 6:
DESCRIPTION: Validity wrong-but-consistent follow-through (wrong expected-count value, correctly compared to threshold)
INPUT ans1a: 1
INPUT ans1b: [p_hat_small, p_hat_large]
INPUT ans1c: z_true
INPUT ans1d: first(mcq_correct(decision1_opts))
INPUT ans1e: [ci_diff_lower, ci_diff_upper]
INPUT ans2a: 1
INPUT ans2b: [odds_small_true, odds_large_true]
INPUT ans2c: chisq_true
INPUT ans2d: first(mcq_correct(decision2_opts))
INPUT ans2e: [ci_OR_lower, ci_OR_upper]
INPUT ans3a: min_expected_true+7
INPUT ans3b: if min_expected_true+7>=5 then 1 else 2
EXPECT prt_ans3a: NODE0-F
EXPECT prt_ans3b: NODE0-T