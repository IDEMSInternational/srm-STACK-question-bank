QUESTIONTEXT:
<p>In 2011, Eagle Boys Pizza ran a campaign claiming their pizzas were "Real size 12-inch large pizzas." A sample of \(n={@n@}\) large pizzas was measured, giving sample mean diameter \(\bar{x}={@xbar@}\) inches and sample standard deviation \(s={@s@}\) inches. We wish to test, at significance level \(\alpha=0.05\), whether the mean diameter of Eagle Boys pizzas is actually 12 inches, or not.</p>

<p><b>Part 1.</b> Calculate the standard error of the sample mean, \(SE=\dfrac{s}{\sqrt{n}}\). Give your answer to 4 decimal places.</p>
[[input:ans1]] [[validation:ans1]] [[feedback:prt_ans1]]

<p><b>Part 2.</b> Write down the null and alternative hypotheses for \(\mu\), the population mean pizza diameter.</p>
<p>\(H_0:\) \(\mu=\) [[input:ans2a]] [[validation:ans2a]]</p>
<p>\(H_1:\) \(\mu\) [[input:ans2b]] [[validation:ans2b]] [[feedback:prt_ans2b]]</p>

<p><b>Part 3.</b> Using your own standard error from Part 1, calculate the t-score \(t=\dfrac{\bar{x}-12}{SE}\). Give your answer to 2 decimal places.</p>
[[input:ans3]] [[validation:ans3]] [[feedback:prt_ans3]]

<p><b>Part 4.</b> Using the 68-95-99.7 rule and your own t-score from Part 3, choose the approximate P-value range.</p>
[[input:ans4]] [[validation:ans4]] [[feedback:prt_ans4]]

<p><b>Part 5.</b> Based on your answer to Part 4, and using \(\alpha=0.05\), what is the appropriate decision about \(H_0\)?</p>
[[input:ans5]] [[validation:ans5]] [[feedback:prt_ans5]]

<p><b>Part 6.</b> Is the sample size \(n={@n@}\) large enough for the statistical validity conditions (Central Limit Theorem) to hold here?</p>
[[input:ans6]] [[validation:ans6]] [[feedback:prt_ans6]]

QUESTIONVARIABLES:
n: rand([100,125,150,200]);
s: float(0.20 + 0.10*rand(11)/10);
mu0: 12;
/* Choose a bucket with weights 50/20/15/15, then a t value comfortably inside it */
bucket_pick: rand(100);
bucket: if bucket_pick<50 then 1 else if bucket_pick<70 then 2 else if bucket_pick<85 then 3 else 4;
/* bucket 1: |t|>=3, well clear, up to 4.5
   bucket 2: 2<=|t|<3, clear of both boundaries
   bucket 3: 1<=|t|<2, clear of both boundaries
   bucket 4: |t|<1, clear of boundary */
tmag: if bucket=1 then 3.2+0.1*rand(11) else
      if bucket=2 then 2.2+0.1*rand(6) else
      if bucket=3 then 1.2+0.1*rand(6) else
      0.1+0.1*rand(7);
t_val: -tmag;
SE_exact: s/sqrt(n);
xbar_exact: mu0 + t_val*SE_exact;
xbar: 0.001*round(xbar_exact*1000);
SE: 0.0001*round(SE_exact*10000);
t_display: 0.01*round(t_val*100);
bucket_label: if bucket=1 then "P<0.003" else
              if bucket=2 then "0.003<P<0.05" else
              if bucket=3 then "0.05<P<0.32" else
              "P>0.32";
decision_label: if bucket=1 or bucket=2 then "Reject H0" else "Fail to reject H0";

/* MCQ option lists in the required [value, correct, display] format */
ans2b_ta: [[1, false, "&lt; 12"], [2, true, "&ne; 12"], [3, false, "&gt; 12"]];
ans4_ta: [[1, is(bucket=1), "P&lt;0.003"], [2, is(bucket=2), "0.003&lt;P&lt;0.05"], [3, is(bucket=3), "0.05&lt;P&lt;0.32"], [4, is(bucket=4), "P&gt;0.32"]];
ans5_ta: [[1, is(bucket=1 or bucket=2), "Reject H0"], [2, is(bucket=3 or bucket=4), "Fail to reject H0"]];
ans6_ta: [[1, true, "Yes"], [2, false, "No"]];

GENERALFEEDBACK:
<p>The standard error is \(SE=\dfrac{s}{\sqrt{n}}=\dfrac{{@s@}}{\sqrt{{@n@}}}={@SE@}\). A common mistake is computing \(s/n\) instead of \(s/\sqrt{n}\).</p>

<p>The hypotheses are \(H_0:\mu=12\) versus \(H_1:\mu\neq 12\). This is two-tailed, since the research question asks whether the mean diameter is 12 inches "or not" — not specifically whether it is smaller.</p>

<p>The t-score is \(t=\dfrac{\bar{x}-12}{SE}=\dfrac{{@xbar@}-12}{{@SE@}}={@t_display@}\). A common mistake is a sign error, computing \(\dfrac{12-\bar{x}}{SE}\) instead.</p>

<p>Using the 68-95-99.7 rule with \(|t|={@abs(t_display)@}\), the approximate P-value range is \({@bucket_label@}\).</p>

<p>Since \(\alpha=0.05\), the decision is: {@decision_label@}.</p>

<p>Since \(n={@n@}\) is much larger than 25, the statistical validity conditions (Central Limit Theorem) are satisfied.</p>

QUESTIONNOTE:
\(n={@n@}, s={@s@}, \bar{x}={@xbar@}, t={@t_display@}\), bucket {@bucket@} ({@bucket_label@}), {@decision_label@}

INPUT ans1:
TYPE: numerical
TANS: SE
ANSWERTEST: NumDecPlaces
BOXSIZE: 10

INPUT ans2a:
TYPE: algebraic
TANS: 12
ANSWERTEST: AlgEquiv
BOXSIZE: 5
SHOWVALIDATION: 0

INPUT ans2b:
TYPE: dropdown
TANS: ans2b_ta
ANSWERTEST: String
SHOWVALIDATION: 0

INPUT ans3:
TYPE: numerical
TANS: t_display
ANSWERTEST: NumDecPlaces
BOXSIZE: 10

INPUT ans4:
TYPE: dropdown
TANS: ans4_ta
ANSWERTEST: String
SHOWVALIDATION: 0

INPUT ans5:
TYPE: dropdown
TANS: ans5_ta
ANSWERTEST: String
SHOWVALIDATION: 0

INPUT ans6:
TYPE: dropdown
TANS: ans6_ta
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
INPUT ans1: SE
INPUT ans2a: 12
INPUT ans2b: "\\neq 12"
INPUT ans3: t_display
INPUT ans4: bucket_label
INPUT ans5: decision_label
INPUT ans6: "Yes"
EXPECT prt_ans1: NODE0-T
EXPECT prt_ans2a: NODE0-T
EXPECT prt_ans2b: NODE0-T
EXPECT prt_ans3: NODE0-T
EXPECT prt_ans4: NODE0-T
EXPECT prt_ans5: NODE0-T
EXPECT prt_ans6: NODE0-T
