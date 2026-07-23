QUESTIONTEXT:
<p>Eagle Boys advertises that its pizzas have a diameter of 12 inches. A quality-control officer takes a random sample of \(n={@n@}\) pizzas and finds a sample mean diameter of \(\bar{x}={@xbar@}\) inches with sample standard deviation \(s={@s@}\) inches. The officer wants to test, at the \(\alpha=0.05\) significance level, whether the true mean pizza diameter differs from the advertised 12 inches.</p>

<h4>Part 1: Standard error</h4>
<p>Calculate the standard error of the sample mean, \(SE=\dfrac{s}{\sqrt{n}}\). Give your answer to 4 decimal places.</p>
[[input:ans1]] [[validation:ans1]] [[feedback:prt_ans1]]

<h4>Part 2: Hypotheses</h4>
<p>State the null and alternative hypotheses for this test, in terms of the population mean \(\mu\).</p>
<p>\(H_0:\) [[input:ans2]] [[validation:ans2]] [[feedback:prt_ans2]]</p>
<p>\(H_1:\) [[input:ans3]] [[validation:ans3]] [[feedback:prt_ans3]]</p>

<h4>Part 3: t-score</h4>
<p>Using your own standard error from Part 1, calculate the test statistic \(t=\dfrac{\bar{x}-12}{SE}\). Give your answer to 2 decimal places.</p>
[[input:ans4]] [[validation:ans4]] [[feedback:prt_ans4]]

<h4>Part 4: Approximate P-value</h4>
<p>Using your own t-score from Part 3 and the 68-95-99.7 rule, which range best describes the (two-tailed) P-value?</p>
[[input:ans5]] [[validation:ans5]] [[feedback:prt_ans5]]

<h4>Part 5: Decision</h4>
<p>Based on your own answer to Part 4, and testing at \(\alpha=0.05\), what is the correct decision about \(H_0\)?</p>
[[input:ans6]] [[validation:ans6]] [[feedback:prt_ans6]]

<h4>Part 6: Validity check</h4>
<p>Is the sample size \(n={@n@}\) large enough for the Central Limit Theorem to justify this t-test?</p>
[[input:ans7]] [[validation:ans7]] [[feedback:prt_ans7]]

QUESTIONVARIABLES:
s: rand(11)*0.01 + 0.20;
n: rand([100,125,150,200]);
SE_ta: s/sqrt(n);

/* Choose a bucket with the specified weights, away from boundaries */
w: rand(100);
bucket_gen: if w<50 then 1 elseif w<70 then 2 elseif w<85 then 3 else 4;

tmag: if bucket_gen=1 then 3.2+rand(19)*0.1
      elseif bucket_gen=2 then 2.2+rand(8)*0.1
      elseif bucket_gen=3 then 1.2+rand(8)*0.1
      else 0.1+rand(9)*0.1;

/* Pizzas run small: t is negative */
t_exact: -tmag;

xbar_raw: 12 + t_exact*SE_ta;
xbar: float(round(xbar_raw*1000)/1000);

/* Recompute t and bucket from the rounded, displayed xbar */
t_ta: (xbar-12)/SE_ta;

bucket_num: if abs(t_ta)>=3 then 1
            elseif abs(t_ta)>=2 then 2
            elseif abs(t_ta)>=1 then 3
            else 4;

h0_ta: mu=12;
h1_ta: mu#12;

bucket_opts: [[1, is(bucket_num=1), "P < 0.003"],
              [2, is(bucket_num=2), "0.003 < P < 0.05"],
              [3, is(bucket_num=3), "0.05 < P < 0.32"],
              [4, is(bucket_num=4), "P > 0.32"]];

decision_opts: [[reject, is(bucket_num<=2), "Reject H0"],
                [fail, is(bucket_num>=3), "Fail to reject H0"]];

validity_opts: [[yes, true, "Yes, n is large enough for the CLT to apply"],
                [no, false, "No, n is too small for the CLT to apply"]];

GENERALFEEDBACK:
<p>The standard error is \(SE=\dfrac{s}{\sqrt{n}}=\dfrac{{@s@}}{\sqrt{{@n@}}}={@float(SE_ta)@}\) (note: a common mistake is dividing \(s\) by \(n\) instead of \(\sqrt{n}\)).</p>

<p>Since we are asking whether the mean differs from 12 (not specifically whether it is smaller or larger), this is a two-tailed test:</p>
<p>\(H_0:\mu=12\), \(H_1:\mu\neq12\). (A common error here is writing \(H_1:\mu<12\) because the wording suggests pizzas "run small" — but the research question is genuinely two-tailed.)</p>

<p>The test statistic is \(t=\dfrac{\bar{x}-12}{SE}=\dfrac{{@xbar@}-12}{{@float(SE_ta)@}}={@float(t_ta)@}\). (Take care to compute \(\bar{x}-12\), not \(12-\bar{x}\).)</p>

<p>By the 68-95-99.7 rule applied to \(|t|={@float(abs(t_ta))@}\):</p>
[[ if test="bucket_num=1" ]]
<p>\(|t|\geq 3\), so \(P<0.003\).</p>
[[ elif test="bucket_num=2" ]]
<p>\(2\leq|t|<3\), so \(0.003<P<0.05\).</p>
[[ elif test="bucket_num=3" ]]
<p>\(1\leq|t|<2\), so \(0.05<P<0.32\).</p>
[[ else ]]
<p>\(|t|<1\), so \(P>0.32\).</p>
[[/ if ]]

[[ if test="bucket_num<=2" ]]
<p>Since the P-value range lies below \(\alpha=0.05\), we reject \(H_0\): there is evidence the mean diameter differs from 12 inches.</p>
[[ else ]]
<p>Since the P-value range lies above \(\alpha=0.05\), we fail to reject \(H_0\): there is not enough evidence that the mean diameter differs from 12 inches.</p>
[[/ if ]]

<p>Finally, since \(n={@n@}>25\), the Central Limit Theorem justifies using this approximate normal-based procedure.</p>

QUESTIONNOTE:
\(n={@n@}, s={@s@}, \bar{x}={@xbar@}, t={@float(t_ta)@}, \text{bucket}={@bucket_num@}\)

INPUT ans1:
TYPE: numerical
TANS: SE_ta
ANSWERTEST: NumDecPlaces
BOXSIZE: 10

INPUT ans2:
TYPE: algebraic
TANS: h0_ta
ANSWERTEST: AlgEquiv
BOXSIZE: 10

INPUT ans3:
TYPE: algebraic
TANS: h1_ta
ANSWERTEST: AlgEquiv
BOXSIZE: 10

INPUT ans4:
TYPE: numerical
TANS: t_ta
ANSWERTEST: NumDecPlaces
BOXSIZE: 10

INPUT ans5:
TYPE: dropdown
TANS: bucket_opts
ANSWERTEST: String
SHOWVALIDATION: 0

INPUT ans6:
TYPE: radio
TANS: decision_opts
ANSWERTEST: String
SHOWVALIDATION: 0

INPUT ans7:
TYPE: radio
TANS: validity_opts
ANSWERTEST: String
SHOWVALIDATION: 0

PRT prt_ans1:
NODE 0:
SANS: true
TANS: true

PRT prt_ans2:
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

PRT prt_ans7:
NODE 0:
SANS: true
TANS: true

QTEST 1:
INPUT ans1: SE_ta
INPUT ans2: h0_ta
INPUT ans3: h1_ta
INPUT ans4: t_ta
INPUT ans5: bucket_opts
INPUT ans6: decision_opts
INPUT ans7: validity_opts
EXPECT prt_ans1: NODE0-T
EXPECT prt_ans2: NODE0-T
EXPECT prt_ans3: NODE0-T
EXPECT prt_ans4: NODE0-T
EXPECT prt_ans5: NODE0-T
EXPECT prt_ans6: NODE0-T
EXPECT prt_ans7: NODE0-T
