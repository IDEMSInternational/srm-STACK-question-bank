QUESTIONTEXT:
<p>A study of used Toyota Corollas relates the car's age (in years) to its advertised price (in $1000s), based on a sample of \(n=38\) cars. A least-squares regression of price on age gives the following software output:</p>
<p>
Intercept: \(b_0 = {@b0@}\)<br/>
Slope: \(b_1 = {@b1@}\)<br/>
SE(\(b_1\)) \(= {@se_b1@}\)<br/>
\(r = {@r@}\)
</p>
<p>We want to test \(H_0: \beta_1 = 0\) versus \(H_1: \beta_1 < 0\) (older cars are cheaper), using \(\alpha = 0.05\).</p>

<p><b>Part 1.</b> Compute the value of the test statistic \(t\) for this hypothesis test.</p>
[[input:ans_t]] [[validation:ans_t]] [[feedback:prt_ans_t]]

<p><b>Part 2.</b> Using \(df = 36\), compute the exact one-tailed p-value corresponding to your value of \(t\), and hence state the decision at \(\alpha = 0.05\).</p>
<p>p-value: [[input:ans_p]] [[validation:ans_p]] [[feedback:prt_ans_p]]</p>
<p>Decision: [[input:ans_decision]] [[validation:ans_decision]] [[feedback:prt_ans_decision]]</p>

<p><b>Part 3.</b> Compute \(R^2\), the percentage of variation in price explained by age, from the given value of \(r\). Give your answer as a percentage, to 1 decimal place.</p>
[[input:ans_r2]] [[validation:ans_r2]] [[feedback:prt_ans_r2]]

<p><b>Part 4.</b> Using the rule-of-thumb multiplier of 2, compute a 95% confidence interval for the population slope \(\beta_1\), using \(b_1 \pm 2\times SE(b_1)\).</p>
<p>Lower bound: [[input:ans_ci_lower]] [[validation:ans_ci_lower]] [[feedback:prt_ans_ci_lower]]</p>
<p>Upper bound: [[input:ans_ci_upper]] [[validation:ans_ci_upper]] [[feedback:prt_ans_ci_upper]]</p>

QUESTIONVARIABLES:
n: 38;
df: 36;
b1: float(-(rand(10)+5)/10);
tcase: rand(3);
t_target: if tcase=0 then 10+rand(5) elseif tcase=1 then 4+rand(4) else 2+rand(2);
se_b1: float(abs(b1)/t_target);
b0: float(rand(11)+12);
t_true: float(b1/se_b1);
r: float(t_true/sqrt(df+t_true^2));
r2pct: float(100*r^2);
p_true: float(cdf_student_t(t_true, df));
ci_lower: float(b1 - 2*se_b1);
ci_upper: float(b1 + 2*se_b1);
ta_decision: [[reject, is(p_true<0.05), "Reject H0"],[noreject, is(p_true>=0.05), "Do not reject H0"]];

GENERALFEEDBACK:
<p>The test statistic is
\[ t = \frac{b_1}{SE(b_1)} = \frac{ {@b1@} }{ {@se_b1@} } = {@t_true@}. \]</p>
<p>Since \(H_1: \beta_1 < 0\), the p-value is the one-tailed (lower-tail) probability
\[ p = P(T_{36} \le t) = {@p_true@}. \]
This is the ONE-tailed p-value, not the two-tailed value — a common mistake is to double it or use the wrong tail.</p>
[[if test="p_true<0.05"]]
<p>Since \(p < 0.05\), we reject \(H_0\): there is significant evidence that price decreases with age.</p>
[[else]]
<p>Since \(p \geq 0.05\), we do not reject \(H_0\): there is insufficient evidence that price decreases with age.</p>
[[/if]]
<p>\(R^2 = r^2 = {@r@}^2 = {@r2pct@}\%\) of the variation in price is explained by age. (Remember to report \(R^2\) as a percentage, not a proportion.)</p>
<p>The 95% confidence interval for \(\beta_1\) using the rule-of-thumb multiplier of 2 is
\[ b_1 \pm 2\times SE(b_1) = {@b1@} \pm 2({@se_b1@}) = ({@ci_lower@}, {@ci_upper@}). \]
Be careful to apply this margin to \(b_1\) only, not to \(b_0\) or \(r\).</p>

QUESTIONNOTE:
\(b_0={@b0@}, b_1={@b1@}, SE(b_1)={@se_b1@}, r={@r@}, t={@t_true@}, p={@p_true@}\)

INPUT ans_t:
TYPE: numerical
TANS: t_true
ANSWERTEST: NumRelative
FORBIDFLOAT: 0

INPUT ans_p:
TYPE: numerical
TANS: p_true
ANSWERTEST: NumAbsolute
FORBIDFLOAT: 0

INPUT ans_decision:
TYPE: dropdown
TANS: ta_decision
ANSWERTEST: String
SHOWVALIDATION: 0

INPUT ans_r2:
TYPE: numerical
TANS: r2pct
ANSWERTEST: NumRelative
FORBIDFLOAT: 0

INPUT ans_ci_lower:
TYPE: numerical
TANS: ci_lower
ANSWERTEST: NumRelative
FORBIDFLOAT: 0

INPUT ans_ci_upper:
TYPE: numerical
TANS: ci_upper
ANSWERTEST: NumRelative
FORBIDFLOAT: 0

PRT prt_ans_t:
NODE 0:
TEST: AlgEquiv
SANS: is(abs(ans_t-t_true)<=0.05*abs(t_true)+0.005)
TANS: true
FALSEFEEDBACK: <p>Recall \(t=b_1/SE(b_1)\).</p>

PRT prt_ans_p:
NODE 0:
TEST: AlgEquiv
SANS: is(abs(ans_p-p_true)<=0.005)
TANS: true
FALSEFEEDBACK: <p>Recompute the one-tailed p-value from the t-distribution with df=36, using the correct (lower) tail for \(H_1:\beta_1<0\).</p>

PRT prt_ans_decision:
NODE 0:
TEST: AlgEquiv
SANS: ans_decision
TANS: if is(ans_p<0.05) then reject else noreject
FALSEFEEDBACK: <p>Your decision should be consistent with your own p-value: reject \(H_0\) if \(p<0.05\), otherwise do not reject.</p>

PRT prt_ans_r2:
NODE 0:
TEST: AlgEquiv
SANS: is(abs(ans_r2-r2pct)<=0.5)
TANS: true
FALSEFEEDBACK: <p>Remember \(R^2=r^2\), reported as a percentage.</p>

PRT prt_ans_ci_lower:
NODE 0:
TEST: AlgEquiv
SANS: is(abs(ans_ci_lower-ci_lower)<=0.05*abs(ci_lower)+0.005)
TANS: true

PRT prt_ans_ci_upper:
NODE 0:
TEST: AlgEquiv
SANS: is(abs(ans_ci_upper-ci_upper)<=0.05*abs(ci_upper)+0.005)
TANS: true

QTEST 1:
DESCRIPTION: All correct (happy path)
INPUT ans_t: t_true
INPUT ans_p: p_true
INPUT ans_decision: first(mcq_correct(ta_decision))
INPUT ans_r2: r2pct
INPUT ans_ci_lower: ci_lower
INPUT ans_ci_upper: ci_upper
EXPECT prt_ans_t: NODE0-T
EXPECT prt_ans_p: NODE0-T
EXPECT prt_ans_decision: NODE0-T
EXPECT prt_ans_r2: NODE0-T
EXPECT prt_ans_ci_lower: NODE0-T
EXPECT prt_ans_ci_upper: NODE0-T

QTEST 2:
DESCRIPTION: Wrong t-statistic, everything else correct
INPUT ans_t: t_true+1
INPUT ans_p: p_true
INPUT ans_decision: first(mcq_correct(ta_decision))
INPUT ans_r2: r2pct
INPUT ans_ci_lower: ci_lower
INPUT ans_ci_upper: ci_upper
EXPECT prt_ans_t: NODE0-F
EXPECT prt_ans_p: NODE0-T
EXPECT prt_ans_decision: NODE0-T
EXPECT prt_ans_r2: NODE0-T
EXPECT prt_ans_ci_lower: NODE0-T
EXPECT prt_ans_ci_upper: NODE0-T

QTEST 3:
DESCRIPTION: Wrong p-value but decision correctly follows through from the student's own (wrong) p
INPUT ans_t: t_true
INPUT ans_p: 100
INPUT ans_decision: noreject
INPUT ans_r2: r2pct
INPUT ans_ci_lower: ci_lower
INPUT ans_ci_upper: ci_upper
EXPECT prt_ans_t: NODE0-T
EXPECT prt_ans_p: NODE0-F
EXPECT prt_ans_decision: NODE0-T
EXPECT prt_ans_r2: NODE0-T
EXPECT prt_ans_ci_lower: NODE0-T
EXPECT prt_ans_ci_upper: NODE0-T

QTEST 4:
DESCRIPTION: Correct p-value but decision inconsistent with it
INPUT ans_t: t_true
INPUT ans_p: p_true
INPUT ans_decision: if is(p_true<0.05) then noreject else reject
INPUT ans_r2: r2pct
INPUT ans_ci_lower: ci_lower
INPUT ans_ci_upper: ci_upper
EXPECT prt_ans_t: NODE0-T
EXPECT prt_ans_p: NODE0-T
EXPECT prt_ans_decision: NODE0-F
EXPECT prt_ans_r2: NODE0-T
EXPECT prt_ans_ci_lower: NODE0-T
EXPECT prt_ans_ci_upper: NODE0-T

QTEST 5:
DESCRIPTION: Wrong R^2 (off by 1 percentage point)
INPUT ans_t: t_true
INPUT ans_p: p_true
INPUT ans_decision: first(mcq_correct(ta_decision))
INPUT ans_r2: r2pct+1
INPUT ans_ci_lower: ci_lower
INPUT ans_ci_upper: ci_upper
EXPECT prt_ans_t: NODE0-T
EXPECT prt_ans_p: NODE0-T
EXPECT prt_ans_decision: NODE0-T
EXPECT prt_ans_r2: NODE0-F
EXPECT prt_ans_ci_lower: NODE0-T
EXPECT prt_ans_ci_upper: NODE0-T

QTEST 6:
DESCRIPTION: CI bounds swapped (both wrong)
INPUT ans_t: t_true
INPUT ans_p: p_true
INPUT ans_decision: first(mcq_correct(ta_decision))
INPUT ans_r2: r2pct
INPUT ans_ci_lower: ci_upper
INPUT ans_ci_upper: ci_lower
EXPECT prt_ans_t: NODE0-T
EXPECT prt_ans_p: NODE0-T
EXPECT prt_ans_decision: NODE0-T
EXPECT prt_ans_r2: NODE0-T
EXPECT prt_ans_ci_lower: NODE0-F
EXPECT prt_ans_ci_upper: NODE0-F