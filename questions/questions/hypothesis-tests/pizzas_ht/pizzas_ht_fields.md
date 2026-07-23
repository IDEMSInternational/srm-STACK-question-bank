QUESTIONTEXT:
<p>Eagle Boys advertises that its pizzas have a diameter of 12 inches. A quality-control inspector takes a random sample of \(n={@n@}\) pizzas and finds a sample mean diameter of \(\bar{x} = {@xbar@}\) inches, with sample standard deviation \(s = {@s@}\) inches.</p>

<p>The inspector wants to test, at the \(\alpha = 0.05\) significance level, whether the true mean pizza diameter differs from the advertised 12 inches.</p>

<h4>Part 1 — Standard error</h4>
<p>Compute the standard error of the sample mean, \(SE = \dfrac{s}{\sqrt{n}}\), correct to at least 4 decimal places.</p>
[[input:ans_se]] [[validation:ans_se]] [[feedback:prt_ans_se]]

<h4>Part 2 — Hypotheses</h4>
<p>State the null and alternative hypotheses for this test, in terms of the population mean \(\mu\).</p>
<p>\(H_0:\) [[input:ans_h0]] [[validation:ans_h0]] [[feedback:prt_ans_h0]]</p>
<p>\(H_1:\) [[input:ans_h1]] [[validation:ans_h1]] [[feedback:prt_ans_h1]]</p>

<h4>Part 3 — t-score</h4>
<p>Using your own standard error from Part 1, compute the test statistic \(t = \dfrac{\bar{x}-12}{SE}\), correct to 2 decimal places.</p>
[[input:ans_t]] [[validation:ans_t]] [[feedback:prt_ans_t]]

<h4>Part 4 — Approximate P-value</h4>
<p>Using the 68-95-99.7 rule and your own t-score from Part 3, select the range that best describes the (two-tailed) P-value.</p>
[[input:ans_bucket]] [[validation:ans_bucket]] [[feedback:prt_ans_bucket]]

<h4>Part 5 — Decision</h4>
<p>Based on your answer to Part 4, and using \(\alpha = 0.05\), what is the correct decision?</p>
[[input:ans_decision]] [[validation:ans_decision]] [[feedback:prt_ans_decision]]

<h4>Part 6 — Validity check</h4>
<p>Is the sample size \(n={@n@}\) large enough to justify using the Central Limit Theorem here?</p>
[[input:ans_validity]] [[validation:ans_validity]] [[feedback:prt_ans_validity]]

QUESTIONVARIABLES:
n: rand([100,125,150,200]);
s: (20+rand(11))/100;
se_exact: s/sqrt(n);
se: float(se_exact);

bucket_pick: rand(100);
bucket: if bucket_pick<50 then 4 elseif bucket_pick<70 then 3 elseif bucket_pick<85 then 2 else 1;

t_mag: if bucket=4 then 3.1+rand(14)/10
       elseif bucket=3 then 2.1+rand(8)/10
       elseif bucket=2 then 1.1+rand(8)/10
       else 0.1+rand(8)/10;

t_teacher: -t_mag;

xbar_exact: 12 + t_teacher*se_exact;
xbar: float(round(xbar_exact*1000)/1000);

t_actual: float((xbar-12)/se);
t_display: float(round(t_actual*100)/100);

bucket_label: if bucket=4 then "P < 0.003"
              elseif bucket=3 then "0.003 < P < 0.05"
              elseif bucket=2 then "0.05 < P < 0.32"
              else "P > 0.32";

decision_label: if bucket>=3 then "Reject H0" else "Fail to reject H0";

ta_se: se;
ta_h0: mu=12;
ta_h1: mu#12;
ta_t: t_display;
ta_bucket: bucket_label;
ta_decision: decision_label;
ta_validity: "Yes";

GENERALFEEDBACK:
<p><strong>Worked solution</strong></p>
<p>Standard error: \(SE = \dfrac{s}{\sqrt{n}} = \dfrac{{@s@}}{\sqrt{{@n@}}} = {@se@}\). A common mistake is dividing by \(n\) instead of \(\sqrt{n}\) — this gives a much smaller (wrong) SE.</p>
<p>Hypotheses: since the research question is whether the diameter differs from 12 (not specifically whether it is smaller), this is a two-tailed test: \(H_0:\mu=12\), \(H_1:\mu\neq 12\). Choosing a one-tailed \(H_1:\mu<12\) is a common error here, even though the sample mean happens to be below 12.</p>
<p>Test statistic: \(t = \dfrac{\bar{x}-12}{SE} = \dfrac{{@xbar@}-12}{{@se@}} = {@t_display@}\). Note it is \(\bar{x}-12\), not \(12-\bar{x}\) — a sign error here flips the direction of the t-score.</p>
<p>Using the 68-95-99.7 rule for the sampling distribution of \(t\): \(|t| = {@abs(t_display)@}\) falls in the range <strong>{@bucket_label@}</strong>.</p>
<p>Decision at \(\alpha=0.05\): since the approximate P-value is {@bucket_label@}, we <strong>{@decision_label@}</strong>.</p>
<p>Validity check: with \(n={@n@}\) (well over 25-30), the Central Limit Theorem applies, so using a t/normal-based procedure is justified.</p>

QUESTIONNOTE:
\(n={@n@}, s={@s@}, \bar{x}={@xbar@}, t={@t_display@}\), bucket {@bucket@} ({@decision_label@})

INPUT ans_se:
TYPE: numerical
TANS: ta_se
ANSWERTEST: NumRelative

INPUT ans_h0:
TYPE: algebraic
TANS: ta_h0
ANSWERTEST: AlgEquiv
BOXSIZE: 10

INPUT ans_h1:
TYPE: algebraic
TANS: ta_h1
ANSWERTEST: AlgEquiv
BOXSIZE: 10

INPUT ans_t:
TYPE: numerical
TANS: ta_t
ANSWERTEST: NumAbsolute

INPUT ans_bucket:
TYPE: dropdown
TANS: ta_bucket
ANSWERTEST: String
SHOWVALIDATION: 0

INPUT ans_decision:
TYPE: radio
TANS: ta_decision
ANSWERTEST: String
SHOWVALIDATION: 0

INPUT ans_validity:
TYPE: radio
TANS: ta_validity
ANSWERTEST: String
SHOWVALIDATION: 0

PRT prt_ans_se:
NODE 0:
SANS: true
TANS: true

PRT prt_ans_h0:
NODE 0:
SANS: true
TANS: true

PRT prt_ans_h1:
NODE 0:
SANS: true
TANS: true

PRT prt_ans_t:
NODE 0:
SANS: true
TANS: true

PRT prt_ans_bucket:
NODE 0:
SANS: true
TANS: true

PRT prt_ans_decision:
NODE 0:
SANS: true
TANS: true

PRT prt_ans_validity:
NODE 0:
SANS: true
TANS: true

QTEST 1:
INPUT ans_se: ta_se
INPUT ans_h0: ta_h0
INPUT ans_h1: ta_h1
INPUT ans_t: ta_t
INPUT ans_bucket: ta_bucket
INPUT ans_decision: ta_decision
INPUT ans_validity: ta_validity
EXPECT prt_ans_se: NODE0-T
EXPECT prt_ans_h0: NODE0-T
EXPECT prt_ans_h1: NODE0-T
EXPECT prt_ans_t: NODE0-T
EXPECT prt_ans_bucket: NODE0-T
EXPECT prt_ans_decision: NODE0-T
EXPECT prt_ans_validity: NODE0-T
