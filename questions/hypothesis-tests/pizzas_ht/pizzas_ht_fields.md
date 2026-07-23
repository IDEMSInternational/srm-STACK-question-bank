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

ta4: [[1, is(bucket_true=1), "\\( P < 0.003 \\)"],
      [2, is(bucket_true=2), "\\( 0.003 < P < 0.05 \\)"],
      [3, is(bucket_true=3), "\\( 0.05 < P < 0.32 \\)"],
      [4, is(bucket_true=4), "\\( P > 0.32 \\)"]];
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
FORBIDFLOAT: 0

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
SANS: true
TANS: true

PRT prt_ans2a:
NODE 0:
SANS: true
TANS: true

PRT prt_ans2b:
NODE 0:
SANS: true
TANS: true

PRT prt_ans3:
NODE 0:
SANS: true
TANS: true

PRT prt_ans4:
NODE 0:
SANS: true
TANS: true

PRT prt_ans5:
NODE 0:
SANS: true
TANS: true

PRT prt_ans6:
NODE 0:
SANS: true
TANS: true

QTEST 1:
INPUT ans1: se_true
INPUT ans2a: h0_ta
INPUT ans2b: h1_ta
INPUT ans3: t_true
INPUT ans4: ta4
INPUT ans5: ta5
INPUT ans6: ta6
EXPECT prt_ans1: NODE0-T
EXPECT prt_ans2a: NODE0-T
EXPECT prt_ans2b: NODE0-T
EXPECT prt_ans3: NODE0-T
EXPECT prt_ans4: NODE0-T
EXPECT prt_ans5: NODE0-T
EXPECT prt_ans6: NODE0-T
