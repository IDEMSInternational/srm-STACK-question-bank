QUESTIONTEXT:
<p>A biologist is studying the weight of adult male black bears. A random sample of \(n={@n@}\) male bears has sample mean weight \(\bar{x}={@xbar@}\) kg and sample standard deviation \(s={@s@}\) kg. The biologist wants to construct a 95% confidence interval for the population mean weight \(\mu\) of all adult male black bears, using the critical value \(z^*=1.96\).</p>

<p>Before doing any calculations, think about what population parameter \(\mu\) represents here, and picture the sampling distribution of \(\bar{x}\) that the confidence interval is based on. (This part is not graded.)</p>

<p><b>Part 1.</b> Calculate the standard error of the mean, \(SE=\dfrac{s}{\sqrt{n}}\). Give your answer to 3 decimal places.</p>
[[input:ans1]] [[validation:ans1]] [[feedback:prt_ans1]]

<p><b>Part 2.</b> Calculate the margin of error, \(ME=z^*\times SE\), using your own value of \(SE\) from Part 1. Give your answer to 3 decimal places.</p>
[[input:ans2]] [[validation:ans2]] [[feedback:prt_ans2]]

<p><b>Part 3.</b> Using your own value of \(ME\) from Part 2, calculate the lower and upper bounds of the confidence interval, \(\bar{x}-ME\) and \(\bar{x}+ME\). Give each answer to 2 decimal places.</p>
<p>Lower bound: [[input:ans3]] [[validation:ans3]] [[feedback:prt_ans3]]</p>
<p>Upper bound: [[input:ans4]] [[validation:ans4]] [[feedback:prt_ans4]]</p>

<p><b>Part 4.</b> Is it valid to use the large-sample \(z\)-confidence interval procedure here (i.e. is \(n\ge 25\))?</p>
[[input:ans5]] [[validation:ans5]] [[feedback:prt_ans5]]

<p><b>Part 5.</b> Which of the following is the correct interpretation of this confidence interval?</p>
[[input:ans6]] [[validation:ans6]] [[feedback:prt_ans6]]

QUESTIONVARIABLES:
n: rand([10,15,18,22,30,45,80,150,250]);
xbar: rand(51)+60;
s: rand(31)+30;
z: 1.96;
se: s/sqrt(n);
me: z*se;
lower: xbar-me;
upper: xbar+me;
se_val: float(se);
me_val: float(me);
lower_val: float(lower);
upper_val: float(upper);
valid_p: is(n>=25);
mcq_valid: [[true, valid_p, "Yes, the procedure is valid"], [false, not valid_p, "No, the procedure is not valid"]];
mcq_interp: [
  [1, false, "There is a 95% probability that the true population mean \\(\\mu\\) lies between the lower and upper bound computed from this particular sample."],
  [2, true, "We are 95% confident that the interval from the lower to the upper bound contains the true population mean weight \\(\\mu\\) of all adult male black bears."],
  [3, false, "95% of all adult male black bears have weights between the lower and upper bound."],
  [4, false, "95% of all possible sample means \\(\\bar{x}\\) from repeated samples will fall between the lower and upper bound computed from this particular sample."]
];

GENERALFEEDBACK:
<p>With \(n={@n@}\), \(\bar{x}={@xbar@}\), \(s={@s@}\):</p>
<p>\(SE=\dfrac{s}{\sqrt{n}}={@s@}/\sqrt{@n@}={@se_val@}\)</p>
<p>\(ME=z^*\times SE=1.96\times {@se_val@}={@me_val@}\)</p>
<p>Confidence interval: \(\bar{x}\pm ME = ({@lower_val@},\,{@upper_val@})\)</p>
[[if test="valid_p"]]
<p>Since \(n={@n@}\ge 25\), the sample size is large enough for the Central Limit Theorem to justify treating the sampling distribution of \(\bar{x}\) as approximately normal, so the \(z\)-interval procedure is valid here.</p>
[[else]]
<p>Since \(n={@n@}<25\), the sample size is too small to rely on the Central Limit Theorem to justify the normal approximation used in this \(z\)-interval procedure, so strictly this method should not be used here.</p>
[[/if]]
<p>The correct interpretation is: we are 95% confident that the interval contains the true population mean \(\mu\) — the confidence level describes the long-run success rate of the method, not a probability statement about this one fixed interval, and it says nothing directly about individual bears or individual sample means.</p>

QUESTIONNOTE:
\(n={@n@}, \bar{x}={@xbar@}, s={@s@}\), valid={@valid_p@}

INPUT ans1:
TYPE: numerical
TANS: se
ANSWERTEST: NumDecPlaces
BOXSIZE: 10

INPUT ans2:
TYPE: numerical
TANS: me
ANSWERTEST: NumDecPlaces
BOXSIZE: 10

INPUT ans3:
TYPE: numerical
TANS: lower
ANSWERTEST: NumDecPlaces
BOXSIZE: 10

INPUT ans4:
TYPE: numerical
TANS: upper
ANSWERTEST: NumDecPlaces
BOXSIZE: 10

INPUT ans5:
TYPE: radio
TANS: true
ANSWERTEST: CasEqual
SHOWVALIDATION: 0

INPUT ans6:
TYPE: radio
TANS: 2
ANSWERTEST: CasEqual
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

QTEST 1:
INPUT ans1: se
INPUT ans2: me
INPUT ans3: lower
INPUT ans4: upper
INPUT ans5: true
INPUT ans6: 2
EXPECT prt_ans1: NODE0-T
EXPECT prt_ans2: NODE0-T
EXPECT prt_ans3: NODE0-T
EXPECT prt_ans4: NODE0-T
EXPECT prt_ans5: NODE0-T
EXPECT prt_ans6: NODE0-T
