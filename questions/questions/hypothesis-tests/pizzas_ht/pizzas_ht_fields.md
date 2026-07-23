QUESTIONTEXT:
<p>Eagle Boys claims that its pizzas have a mean diameter of \(12\) inches. A quality-control officer measures a random sample of \(n={@n@}\) pizzas and finds a sample mean diameter of \(\bar{x}={@xbar@}\) inches, with sample standard deviation \(s={@s@}\) inches.</p>

<p>She wants to test, at the \(\alpha=0.05\) significance level, whether the mean diameter differs from the claimed \(12\) inches (in either direction).</p>

<h4>Part 1 — Standard error</h4>
<p>Calculate the standard error of the sample mean, \(SE=\dfrac{s}{\sqrt{n}}\). Give your answer to 4 decimal places.</p>
[[input:ans1]] [[validation:ans1]] [[feedback:prt_ans1]]

<h4>Part 2 — Hypotheses</h4>
<p>State the null and alternative hypotheses (using \(\mu\) for the true mean pizza diameter).</p>
<p>\(H_0:\) [[input:ans2a]] [[validation:ans2a]] [[feedback:prt_ans2a]]</p>
<p>\(H_1:\) [[input:ans2b]] [[validation:ans2b]] [[feedback:prt_ans2b]]</p>

<h4>Part 3 — Test statistic</h4>
<p>Using your own standard error from Part 1, calculate the t-score \(t=\dfrac{\bar{x}-12}{SE}\). Give your answer to 2 decimal places.</p>
[[input:ans3]] [[validation:ans3]] [[feedback:prt_ans3]]

<h4>Part 4 — Approximate P-value</h4>
<p>Using the 68-95-99.7 rule and your own t-score from Part 3, select the range that best approximates the two-tailed P-value.</p>
[[input:ans4]] [[validation:ans4]] [[feedback:prt_ans4]]

<h4>Part 5 — Decision</h4>
<p>Based on your bucket answer from Part 4, and testing at \(\alpha=0.05\), what is the decision about \(H_0\)?</p>
[[input:ans5]] [[validation:ans5]] [[feedback:prt_ans5]]

<h4>Part 6 — Validity check</h4>
<p>Is the sample size \(n={@n@}\) large enough to justify using the Central Limit Theorem here?</p>
[[input:ans6]] [[validation:ans6]] [[feedback:prt_ans6]]

QUESTIONVARIABLES:
n: rand([100,125,150,200]);
s: rand([0.20,0.21,0.22,0.23,0.24,0.25,0.26,0.27,0.28,0.29,0.30]);
SE_exact: s/sqrt(n);

bucket_pick: rand(100);
tA_list: makelist(3.1+0.1*i, i, 0, 13);
tB_list: makelist(2.1+0.1*i, i, 0, 7);
tC_list: makelist(1.1+0.1*i, i, 0, 7);
tD_list: makelist(0.1+0.1*i, i, 0, 7);

tmag: if bucket_pick<50 then rand(tA_list)
      elseif bucket_pick<70 then rand(tB_list)
      elseif bucket_pick<85 then rand(tC_list)
      else rand(tD_list);

t_target: -tmag;
xbar_raw: 12 + t_target*SE_exact;
xbar: float(round(1000*xbar_raw)/1000);
t_true: (xbar-12)/SE_exact;

bucket: if abs(t_true)>=3 then "A" elseif abs(t_true)>=2 then "B" elseif abs(t_true)>=1 then "C" else "D";
decision: if bucket="A" or bucket="B" then "reject" else "failtoreject";

ta1: SE_exact;
ta2a: mu=12;
ta2b: mu # 12;
ta3: t_true;

bucket_answer: if bucket="A" then "R1" elseif bucket="B" then "R2" elseif bucket="C" then "R3" else "R4";
decision_answer: if decision="reject" then "reject" else "failreject";
validity_answer: "yes";

ta4: [[1, is(bucket="A"), "\\(P<0.003\\)"], [2, is(bucket="B"), "\\(0.003<P<0.05\\)"], [3, is(bucket="C"), "\\(0.05<P<0.32\\)"], [4, is(bucket="D"), "\\(P>0.32\\)"]];
ta5: [[1, is(decision="reject"), "Reject \\(H_0\\)"], [2, is(decision="failtoreject"), "Fail to reject \\(H_0\\)"]];
ta6: [[1, true, "Yes, the CLT applies"], [2, false, "No, the sample is too small"]];

GENERALFEEDBACK:
<p><strong>Worked solution</strong></p>
<p>Standard error: \(SE=\dfrac{s}{\sqrt{n}}=\dfrac{ {@s@} }{\sqrt{ {@n@} }} = {@float(SE_exact)@}\).</p>
<p>Since the research question asks whether the mean differs from \(12\) in either direction, the hypotheses are two-tailed: \(H_0:\mu=12\) vs \(H_1:\mu\neq12\). (A common mistake is to write a one-tailed \(H_1:\mu<12\) just because the sample mean happens to be below \(12\) — the claim being tested is "different from", not "less than".)</p>
<p>Test statistic: \(t=\dfrac{\bar{x}-12}{SE}=\dfrac{ {@xbar@}-12}{ {@float(SE_exact)@} } = {@float(t_true)@}\). (A common slip here is computing \(s/n\) instead of \(s/\sqrt{n}\) for the SE, or reversing the numerator to \(12-\bar{x}\).)</p>
<p>Using the 68-95-99.7 rule for a two-tailed test: \(|t|\ge3\) gives \(P<0.003\); \(2\le|t|<3\) gives \(0.003<P<0.05\); \(1\le|t|<2\) gives \(0.05<P<0.32\); \(|t|<1\) gives \(P>0.32\). Here \(|t|={@float(abs(t_true))@}\), which falls in bucket {@bucket@}.</p>
<p>At \(\alpha=0.05\): if \(P<0.05\) we reject \(H_0\); otherwise we fail to reject \(H_0\). Since \(n={@n@}>25\), the CLT applies and the sampling distribution of \(\bar{x}\) is approximately normal, so this reasoning is valid.</p>

QUESTIONNOTE:
\(n={@n@}, s={@s@}, \bar{x}={@xbar@}, SE={@float(SE_exact)@}, t={@float(t_true)@}\), bucket={@bucket@}, decision={@decision@}

INPUT ans1:
TYPE: numerical
TANS: ta1
ANSWERTEST: NumDecPlaces
SHOWVALIDATION: 1

INPUT ans2a:
TYPE: algebraic
TANS: ta2a
ANSWERTEST: AlgEquiv

INPUT ans2b:
TYPE: algebraic
TANS: ta2b
ANSWERTEST: AlgEquiv

INPUT ans3:
TYPE: numerical
TANS: ta3
ANSWERTEST: NumDecPlaces
SHOWVALIDATION: 1

INPUT ans4:
TYPE: dropdown
TANS: ta4
ANSWERTEST: String
SHOWVALIDATION: 0

INPUT ans5:
TYPE: radio
TANS: ta5
ANSWERTEST: String
SHOWVALIDATION: 0

INPUT ans6:
TYPE: radio
TANS: ta6
ANSWERTEST: String
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
INPUT ans1: ta1
INPUT ans2a: ta2a
INPUT ans2b: ta2b
INPUT ans3: ta3
INPUT ans4: bucket_answer
INPUT ans5: decision_answer
INPUT ans6: validity_answer
EXPECT prt_ans1: NODE0-T
EXPECT prt_ans2a: NODE0-T
EXPECT prt_ans2b: NODE0-T
EXPECT prt_ans3: NODE0-T
EXPECT prt_ans4: NODE0-T
EXPECT prt_ans5: NODE0-T
EXPECT prt_ans6: NODE0-T
