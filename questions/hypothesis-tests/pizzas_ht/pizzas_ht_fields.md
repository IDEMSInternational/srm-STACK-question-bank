QUESTIONTEXT:
<p>A quality-control officer at Eagle Boys measured the diameter (in inches) of a random sample of \(n={@n@}\) pizzas advertised as having diameter \(12\) inches. The sample mean was \(\bar{x}={@xbar@}\) inches, with sample standard deviation \(s={@s@}\) inches.</p>

<p>We wish to test, at the \(\alpha=0.05\) significance level, whether the true mean diameter differs from \(12\) inches.</p>

<h4>1. Standard error</h4>
<p>Compute the standard error of the sample mean (give your answer correct to at least 3 significant figures).</p>
[[input:ans1]] [[validation:ans1]] [[feedback:prt_ans1]]

<h4>2. Hypotheses</h4>
<p>State the null and alternative hypotheses, in terms of the population mean \(\mu\).</p>
<p>\(H_0:\) [[input:ans2a]] [[validation:ans2a]] [[feedback:prt_ans2a]]</p>
<p>\(H_1:\) [[input:ans2b]] [[validation:ans2b]] [[feedback:prt_ans2b]]</p>

<h4>3. Test statistic</h4>
<p>Using your own answer to Part 1 as the standard error, compute the \(t\)-score for this sample (give your answer to 2 decimal places).</p>
[[input:ans3]] [[validation:ans3]] [[feedback:prt_ans3]]

<h4>4. P-value estimate</h4>
<p>Using the 68-95-99.7 rule and your own \(t\)-score from Part 3, which of the following best describes the two-sided P-value?</p>
[[input:ans4]] [[validation:ans4]] [[feedback:prt_ans4]]

<h4>5. Conclusion</h4>
<p>Based on your own P-value estimate from Part 4, and using \(\alpha=0.05\), what conclusion should be drawn about \(H_0\)?</p>
[[input:ans5]] [[validation:ans5]] [[feedback:prt_ans5]]

<h4>6. Validity check</h4>
<p>Regardless of your previous answers: is the sample size \(n={@n@}\) large enough for the Central Limit Theorem to justify this t-test, using the textbook's rule of thumb that \(n\) should be much larger than 25?</p>
[[input:ans6]] [[validation:ans6]] [[feedback:prt_ans6]]

QUESTIONVARIABLES:
w: rand(100);
bucket_target: if w<50 then 1 elseif w<70 then 2 elseif w<85 then 3 else 4;

t_abs: if bucket_target=1 then 3.2+rand(9)/10
       elseif bucket_target=2 then 2.2+rand(7)/10
       elseif bucket_target=3 then 1.2+rand(7)/10
       else 0.3+rand(6)/10;

s: 0.15+rand(21)/100;
n: rand(35)+15;

xbar_exact: 12 - t_abs*s/sqrt(n);
xbar: float(round(1000*xbar_exact)/1000);

se_true: s/sqrt(n);
t_true: (xbar-12)/se_true;

bucket_true: if abs(t_true)>3 then 1 elseif abs(t_true)>2 then 2 elseif abs(t_true)>1 then 3 else 4;

decision_true: if bucket_true=1 or bucket_true=2 then 1 else 2;

validity_true: if n>25 then 1 else 2;

h0_ta: mu=12;
h1_ta: mu#12;

ta4: [[1, is(bucket_true=1), "\\( P \\lt 0.003 \\)"],
      [2, is(bucket_true=2), "\\( 0.003 \\lt P \\lt 0.05 \\)"],
      [3, is(bucket_true=3), "\\( 0.05 \\lt P \\lt 0.32 \\)"],
      [4, is(bucket_true=4), "\\( P \\gt 0.32 \\)"]];
ta4: random_permutation(ta4);

ta5: [[1, is(decision_true=1), "Reject \\(H_0\\)"],
      [2, is(decision_true=2), "Fail to reject \\(H_0\\)"]];

ta6: [[1, is(validity_true=1), "Yes"],
      [2, is(validity_true=2), "No"]];

GENERALFEEDBACK:
<p>The standard error of the mean is</p>
\[ SE = \frac{s}{\sqrt{n}} = \frac{ {@s@} }{\sqrt{ {@n@} }} = {@se_true@}. \]

<p>The hypotheses are \(H_0:\mu=12\) versus \(H_1:\mu\neq12\).</p>

<p>The test statistic is</p>
\[ t = \frac{\bar{x}-\mu_0}{SE} = \frac{ {@xbar@} - 12}{ {@se_true@} } = {@t_true@}. \]

[[ if test="bucket_true=1" ]]
<p>Since \(|t| > 3\), by the 68-95-99.7 rule the two-sided P-value satisfies \(P<0.003\).</p>
[[ elif test="bucket_true=2" ]]
<p>Since \(2<|t|<3\), by the 68-95-99.7 rule the two-sided P-value satisfies \(0.003<P<0.05\).</p>
[[ elif test="bucket_true=3" ]]
<p>Since \(1<|t|<2\), by the 68-95-99.7 rule the two-sided P-value satisfies \(0.05<P<0.32\).</p>
[[ else ]]
<p>Since \(|t|<1\), by the 68-95-99.7 rule the two-sided P-value satisfies \(P>0.32\).</p>
[[/ if ]]

[[ if test="decision_true=1" ]]
<p>Since \(P<0.05\), we reject \(H_0\): there is evidence the mean diameter differs from 12 inches.</p>
[[ else ]]
<p>Since \(P>0.05\), we fail to reject \(H_0\): there is not enough evidence that the mean diameter differs from 12 inches.</p>
[[/ if ]]

[[ if test="validity_true=1" ]]
<p>Since \(n={@n@}\) is much larger than 25, the sample size is large enough for the Central Limit Theorem to justify this t-test.</p>
[[ else ]]
<p>Since \(n={@n@}\) is not much larger than 25, the sample size is not large enough to safely justify this t-test using the Central Limit Theorem.</p>
[[/ if ]]

QUESTIONNOTE:
\(\bar{x}={@xbar@}\), \(s={@s@}\), \(n={@n@}\), \(t={@t_true@}\), bucket={@bucket_true@}, decision={@decision_true@}, validity={@validity_true@}

INPUT ans1:
TYPE: numerical
TANS: se_true
ANSWERTEST: NumSigFigs

INPUT ans2a:
TYPE: algebraic
TANS: h0_ta
ANSWERTEST: AlgEquiv

INPUT ans2b:
TYPE: algebraic
TANS: h1_ta
ANSWERTEST: AlgEquiv

INPUT ans3:
TYPE: numerical
TANS: t_true
ANSWERTEST: NumDecPlaces

INPUT ans4:
TYPE: radio
TANS: ta4
ANSWERTEST: EqualComAss
SHOWVALIDATION: 0

INPUT ans5:
TYPE: radio
TANS: ta5
ANSWERTEST: EqualComAss
SHOWVALIDATION: 0

INPUT ans6:
TYPE: radio
TANS: ta6
ANSWERTEST: EqualComAss
SHOWVALIDATION: 0

PRT prt_ans1:
NODE 0:
SANS: is(abs(ans1-se_true)&lt;=0.01*se_true)
TANS: true
FALSENEXT: 1
NODE 1:
SANS: is(abs(ans1-(s/n))&lt;=0.01*(s/n))
TANS: true
TRUESCORE: 0
TRUEFEEDBACK: <p>It looks like you divided \(s\) by \(n\) instead of \(\sqrt{n}\). Recall \(SE=s/\sqrt{n}\).</p>
FALSEFEEDBACK: <p>Not correct — check the formula \(SE=s/\sqrt{n}\).</p>

PRT prt_ans2a:
NODE 0:
TEST: AlgEquiv
SANS: ans2a
TANS: h0_ta

PRT prt_ans2b:
NODE 0:
TEST: AlgEquiv
SANS: ans2b
TANS: h1_ta

PRT prt_ans3:
NODE 0:
SANS: is(ans1=0)
TANS: true
TRUESCORE: 0
TRUEFEEDBACK: <p>Your standard error is zero, so a \(t\)-score cannot be computed from it.</p>
FALSENEXT: 1
NODE 1:
SANS: is(abs(ans3-(xbar-12)/ans1)&lt;=0.02)
TANS: true
FALSENEXT: 2
TRUEFEEDBACK: <p>Correct — well done.</p>
NODE 2:
SANS: is(abs(ans3-(12-xbar)/ans1)&lt;=0.02)
TANS: true
TRUESCORE: 0
TRUEFEEDBACK: <p>It looks like you flipped the sign — use \(t=(\bar{x}-\mu_0)/SE\), not \((\mu_0-\bar{x})/SE\).</p>
FALSEFEEDBACK: <p>Not correct — recompute \(t=(\bar{x}-\mu_0)/SE\) using your own answer to Part 1 as \(SE\).</p>

PRT prt_ans4:
NODE 0:
SANS: is(ans4=(if abs(ans3)>3 then 1 elseif abs(ans3)>2 then 2 elseif abs(ans3)>1 then 3 else 4))
TANS: true
TRUEFEEDBACK: <p>Correct bucket, consistent with your own \(t\)-score.</p>
FALSEFEEDBACK: <p>Not correct — re-apply the 68-95-99.7 rule to your own \(t\)-score from Part 3.</p>

PRT prt_ans5:
NODE 0:
SANS: is(ans5=(if ans4=1 or ans4=2 then 1 else 2))
TANS: true
TRUEFEEDBACK: <p>Correct conclusion, consistent with your own P-value bucket.</p>
FALSEFEEDBACK: <p>Not correct — your conclusion should match the P-value bucket you chose in Part 4: reject if \(P<0.05\), otherwise fail to reject.</p>

PRT prt_ans6:
NODE 0:
SANS: is(ans6=validity_true)
TANS: true
TRUEFEEDBACK: <p>Correct.</p>
FALSEFEEDBACK: <p>Not correct — compare \(n\) to the textbook's rule of thumb of \(n\) much larger than 25.</p>

QTEST 1:
DESCRIPTION: All correct (teacher's answer)
INPUT ans1: se_true
INPUT ans2a: h0_ta
INPUT ans2b: h1_ta
INPUT ans3: t_true
INPUT ans4: bucket_true
INPUT ans5: decision_true
INPUT ans6: validity_true
EXPECT prt_ans1: NODE0-T
EXPECT prt_ans2a: NODE0-T
EXPECT prt_ans2b: NODE0-T
EXPECT prt_ans3: NODE1-T
EXPECT prt_ans4: NODE0-T
EXPECT prt_ans5: NODE0-T
EXPECT prt_ans6: NODE0-T

QTEST 2:
DESCRIPTION: SE computed as s/n (common mistake), but t-score correctly follows through from that wrong SE
INPUT ans1: s/n
INPUT ans2a: h0_ta
INPUT ans2b: h1_ta
INPUT ans3: (xbar-12)/(s/n)
INPUT ans4: bucket_true
INPUT ans5: decision_true
INPUT ans6: validity_true
EXPECT prt_ans1: NODE1-T SCORE=0 PENALTY=0.1
EXPECT prt_ans3: NODE1-T

QTEST 3:
DESCRIPTION: Correct t-score but wrong bucket chosen in Part 4
INPUT ans1: se_true
INPUT ans3: t_true
INPUT ans4: ev(mod(bucket_true,4)+1,simp)
EXPECT prt_ans3: NODE1-T
EXPECT prt_ans4: NODE0-F

QTEST 4:
DESCRIPTION: Wrong bucket in Part 4, but Part 5 decision follows through from that wrong bucket (not the true one)
INPUT ans1: se_true
INPUT ans3: t_true
INPUT ans4: ev(mod(bucket_true,4)+1,simp)
INPUT ans5: ev(if (mod(bucket_true,4)+1)=1 or (mod(bucket_true,4)+1)=2 then 1 else 2,simp)
EXPECT prt_ans4: NODE0-F
EXPECT prt_ans5: NODE0-T

QTEST 5:
DESCRIPTION: Validity check wrong, independent of other parts
INPUT ans6: if validity_true=1 then 2 else 1
EXPECT prt_ans6: NODE0-F

QTEST 6:
DESCRIPTION: t-score boundary just above 3 -> bucket 1
INPUT ans3: 3.01
INPUT ans4: 1
EXPECT prt_ans4: NODE0-T

QTEST 7:
DESCRIPTION: t-score boundary just below 3 -> bucket 2
INPUT ans3: 2.99
INPUT ans4: 2
EXPECT prt_ans4: NODE0-T

QTEST 8:
DESCRIPTION: t-score boundary just below 2 -> bucket 3
INPUT ans3: 1.99
INPUT ans4: 3
EXPECT prt_ans4: NODE0-T

QTEST 9:
DESCRIPTION: t-score boundary just below 1 -> bucket 4
INPUT ans3: 0.99
INPUT ans4: 4
EXPECT prt_ans4: NODE0-T

QTEST 10:
DESCRIPTION: Blank/zero SE guard on Part 3 — division-by-zero adversarial case
INPUT ans1: 0
INPUT ans3: 0
EXPECT prt_ans1: NODE1-F
EXPECT prt_ans3: NODE0-T SCORE=0 PENALTY=0.1

QTEST 11:
DESCRIPTION: Sign-flip mistake on t-score, using correct own SE
INPUT ans1: se_true
INPUT ans3: (12-xbar)/se_true
EXPECT prt_ans1: NODE0-T
EXPECT prt_ans3: NODE2-T SCORE=0 PENALTY=0.1