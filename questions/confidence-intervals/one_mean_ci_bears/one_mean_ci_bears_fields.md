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
TANS: mcq_valid
ANSWERTEST: CasEqual
SHOWVALIDATION: 0

INPUT ans6:
TYPE: radio
TANS: mcq_interp
ANSWERTEST: CasEqual
SHOWVALIDATION: 0

PRT prt_ans1:
FEEDBACKVARIABLES:
tol: 0.0005;
correct_p: is(abs(ans1-se_val)<tol);
mistake_p: is(abs(ans1-float(s/n))<tol);
NODE 0:
TEST: AlgEquiv
SANS: correct_p
TANS: true
FALSENEXT: 1
NODE 1:
TEST: AlgEquiv
SANS: mistake_p
TANS: true
TRUESCORE: 0
TRUEPENALTY: 0.1
TRUEFEEDBACK: <p>It looks like you divided by \(n\) instead of \(\sqrt{n}\) — remember \(SE=s/\sqrt{n}\), not \(s/n\).</p>
FALSEFEEDBACK: <p>Not correct — check your calculation of \(SE=s/\sqrt{n}\).</p>

PRT prt_ans2:
FEEDBACKVARIABLES:
tol2: 0.0005;
me_from_ans1: float(z*ans1);
correct_p: is(abs(ans2-me_from_ans1)<tol2);
mistake_p: is(abs(ans2-float(ans1))<tol2);
NODE 0:
TEST: AlgEquiv
SANS: correct_p
TANS: true
FALSENEXT: 1
NODE 1:
TEST: AlgEquiv
SANS: mistake_p
TANS: true
TRUESCORE: 0
TRUEPENALTY: 0.1
TRUEFEEDBACK: <p>It looks like you used your \(SE\) directly as the margin of error — remember to multiply by \(z^*=1.96\).</p>
FALSEFEEDBACK: <p>Not correct — check \(ME=z^*\times SE\), using your own \(SE\) from Part 1.</p>

PRT prt_ans3:
FEEDBACKVARIABLES:
tol3: 0.005;
lower_from_ans2: float(xbar-ans2);
correct_p: is(abs(ans3-lower_from_ans2)<tol3);
signerror_p: is(abs(ans3-float(xbar+ans2))<tol3);
NODE 0:
TEST: AlgEquiv
SANS: correct_p
TANS: true
FALSENEXT: 1
NODE 1:
TEST: AlgEquiv
SANS: signerror_p
TANS: true
TRUESCORE: 0
TRUEPENALTY: 0.1
TRUEFEEDBACK: <p>This matches the upper bound, not the lower bound — the lower bound is \(\bar{x}-ME\).</p>
FALSEFEEDBACK: <p>Not correct — check your arithmetic for \(\bar{x}-ME\), using your own \(ME\) from Part 2.</p>

PRT prt_ans4:
FEEDBACKVARIABLES:
tol4: 0.005;
upper_from_ans2: float(xbar+ans2);
correct_p: is(abs(ans4-upper_from_ans2)<tol4);
signerror_p: is(abs(ans4-float(xbar-ans2))<tol4);
NODE 0:
TEST: AlgEquiv
SANS: correct_p
TANS: true
FALSENEXT: 1
NODE 1:
TEST: AlgEquiv
SANS: signerror_p
TANS: true
TRUESCORE: 0
TRUEPENALTY: 0.1
TRUEFEEDBACK: <p>This matches the lower bound, not the upper bound — the upper bound is \(\bar{x}+ME\).</p>
FALSEFEEDBACK: <p>Not correct — check your arithmetic for \(\bar{x}+ME\), using your own \(ME\) from Part 2.</p>

PRT prt_ans5:
NODE 0:
TEST: CasEqual
SANS: ans5
TANS: valid_p

PRT prt_ans6:
NODE 0:
TEST: CasEqual
SANS: ans6
TANS: 2
FALSENEXT: 1
NODE 1:
TEST: CasEqual
SANS: ans6
TANS: 1
TRUESCORE: 0
TRUEPENALTY: 0.1
TRUEFEEDBACK: <p>This describes a probability statement about a fixed interval containing a fixed parameter — that's not what "95% confidence" means. The confidence level describes the long-run success rate of the method.</p>
FALSENEXT: 2
NODE 2:
TEST: CasEqual
SANS: ans6
TANS: 3
TRUESCORE: 0
TRUEPENALTY: 0.1
TRUEFEEDBACK: <p>This describes individual bears, but the interval is about the population mean weight \(\mu\), not individual weights.</p>
FALSENEXT: 3
NODE 3:
TEST: CasEqual
SANS: ans6
TANS: 4
TRUESCORE: 0
TRUEPENALTY: 0.1
TRUEFEEDBACK: <p>This describes the sampling distribution of \(\bar{x}\) across repeated samples, not what a single confidence interval tells us about \(\mu\).</p>
FALSEFEEDBACK: <p>Not correct — review what "95% confidence" actually means for this interval.</p>

QTEST 1:
DESCRIPTION: Fully correct answers throughout
INPUT ans1: se_val
INPUT ans2: me_val
INPUT ans3: lower_val
INPUT ans4: upper_val
INPUT ans5: valid_p
INPUT ans6: 2
EXPECT prt_ans1: NODE0-T
EXPECT prt_ans2: NODE0-T
EXPECT prt_ans3: NODE0-T
EXPECT prt_ans4: NODE0-T
EXPECT prt_ans5: NODE0-T
EXPECT prt_ans6: NODE0-T

QTEST 2:
DESCRIPTION: Classic SE mistake (s/n instead of s/sqrt(n))
INPUT ans1: float(s/n)
EXPECT prt_ans1: NODE1-T SCORE=0 PENALTY=0.1

QTEST 3:
DESCRIPTION: Follow-through — consistently wrong SE (forgot sqrt) should still earn ME/bounds credit
INPUT ans1: float(s/n)
INPUT ans2: float(z*(s/n))
INPUT ans3: float(xbar-z*(s/n))
INPUT ans4: float(xbar+z*(s/n))
EXPECT prt_ans1: NODE1-T SCORE=0 PENALTY=0.1
EXPECT prt_ans2: NODE0-T
EXPECT prt_ans3: NODE0-T
EXPECT prt_ans4: NODE0-T

QTEST 4:
DESCRIPTION: Correct SE/ME but sign-flipped bounds — must be marked wrong independent of Parts 1-2
INPUT ans1: se_val
INPUT ans2: me_val
INPUT ans3: float(xbar+me)
INPUT ans4: float(xbar-me)
EXPECT prt_ans1: NODE0-T
EXPECT prt_ans2: NODE0-T
EXPECT prt_ans3: NODE1-T SCORE=0 PENALTY=0.1
EXPECT prt_ans4: NODE1-T SCORE=0 PENALTY=0.1

QTEST 5:
DESCRIPTION: Validity check graded strictly off actual n, regardless of an unrelated wrong SE
INPUT ans1: float(s/n)
INPUT ans5: valid_p
EXPECT prt_ans1: NODE1-T SCORE=0 PENALTY=0.1
EXPECT prt_ans5: NODE0-T

QTEST 6:
DESCRIPTION: Validity check answered incorrectly (opposite of actual n)
INPUT ans5: not valid_p
EXPECT prt_ans5: NODE0-F

QTEST 7:
DESCRIPTION: Interpretation — probability misinterpretation distractor
INPUT ans6: 1
EXPECT prt_ans6: NODE1-T SCORE=0 PENALTY=0.1

QTEST 8:
DESCRIPTION: Interpretation — individual-bears misinterpretation distractor
INPUT ans6: 3
EXPECT prt_ans6: NODE2-T SCORE=0 PENALTY=0.1

QTEST 9:
DESCRIPTION: Interpretation — repeated-sample-means misinterpretation distractor
INPUT ans6: 4
EXPECT prt_ans6: NODE3-T SCORE=0 PENALTY=0.1