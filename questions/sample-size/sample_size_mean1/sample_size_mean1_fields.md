QUESTIONTEXT:
<p>A sample is to be drawn from a population with standard deviation \(s = {@s@}\) kg, in order to estimate the population mean with a margin of error \(E\), using a 95% confidence interval (\(z = 1.96\)).</p>

<p><b>Part 1.</b> What is the minimum sample size \(n\) required to achieve a margin of error of \(E_1 = {@E1@}\) kg? (Give a whole number.)</p>
[[input:ans1]] [[validation:ans1]] [[feedback:prt_ans1]]

<p><b>Part 2.</b> Suppose instead the margin of error required is \(E_1/{@r2@} = {@E1/r2@}\) kg. Using your answer to Part 1, what is the new minimum sample size?</p>
[[input:ans2]] [[validation:ans2]] [[feedback:prt_ans2]]

<p><b>Part 3.</b> Suppose instead the margin of error required is \(E_1/{@r3@} = {@E1/r3@}\) kg. Using your answer to Part 1, what is the new minimum sample size?</p>
[[input:ans3]] [[validation:ans3]] [[feedback:prt_ans3]]

<p><b>Part 4.</b> For the same margin of error \(E_1 = {@E1@}\) kg, would a <b>smaller</b> or <b>larger</b> sample be needed if a {@conf_alt@}% confidence interval were used instead of a 95% confidence interval?</p>
[[input:ans4]] [[validation:ans4]] [[feedback:prt_ans4]]

QUESTIONVARIABLES:
s: (5+rand(16))/10;
E1: rand([0.2,0.3,0.4,0.5]);
r2: rand([2,3,4]);
r3set: setdifference({2,3,4},{r2});
r3: rand(listify(r3set));
z95: 1.96;
n1: ceiling((z95*s/E1)^2);
n2: n1*r2^2;
n3: n1*r3^2;
dir: rand([1,2]);
conf_alt: if dir=1 then 90 else 99;
z_alt: if dir=1 then 1.645 else 2.576;
option_larger: larger;
option_smaller: smaller;
option_same: same_size;
option_cant: cant_tell;
mcq_ans: if dir=1 then [[option_larger,false,"Larger"],[option_smaller,true,"Smaller"],[option_same,false,"Same"],[option_cant,false,"Can't tell"]] else [[option_larger,true,"Larger"],[option_smaller,false,"Smaller"],[option_same,false,"Same"],[option_cant,false,"Can't tell"]];
mcq_ans: random_permutation(mcq_ans);
mcq_correct_ans: first(mcq_correct(mcq_ans));

GENERALFEEDBACK:
<p><b>Part 1.</b> The required sample size is
\[ n = \left(\frac{z \cdot s}{E_1}\right)^2 = \left(\frac{1.96 \times {@s@}}{{@E1@}}\right)^2 = {@float((z95*s/E1)^2)@}, \]
which rounds up (since sample size must be a whole number) to \(n_1 = {@n1@}\).</p>

<p><b>Part 2.</b> Halving/scaling the margin of error to \(E_1/{@r2@}\) scales \(n\) by a factor of \({@r2@}^2 = {@r2^2@}\), since \(n\) is inversely proportional to \(E^2\). So the new required sample size is \(n_1 \times {@r2@}^2 = {@n1@} \times {@r2^2@} = {@n2@}\).</p>

<p><b>Part 3.</b> Similarly, scaling the margin of error to \(E_1/{@r3@}\) gives a new required sample size of \(n_1 \times {@r3@}^2 = {@n1@} \times {@r3^2@} = {@n3@}\).</p>

<p><b>Part 4.</b> A higher confidence level requires a larger critical value \(z\) (e.g. \(z = {@z_alt@}\) for {@conf_alt@}% confidence, compared to \(z=1.96\) for 95%). Since \(n\) is proportional to \(z^2\), a larger \(z\) requires a larger sample for the same margin of error, and a smaller \(z\) requires a smaller sample.</p>

QUESTIONNOTE:
\(s={@s@}, E_1={@E1@}, r_2={@r2@}, r_3={@r3@}, n_1={@n1@}, \text{dir}={@dir@}\)

INPUT ans1:
TYPE: numerical
TANS: n1
ANSWERTEST: AlgEquiv
FORBIDFLOAT: 1

INPUT ans2:
TYPE: numerical
TANS: n2
ANSWERTEST: AlgEquiv
FORBIDFLOAT: 1

INPUT ans3:
TYPE: numerical
TANS: n3
ANSWERTEST: AlgEquiv
FORBIDFLOAT: 1

INPUT ans4:
TYPE: radio
TANS: mcq_ans
ANSWERTEST: AlgEquiv
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

QTEST 1:
INPUT ans1: n1
INPUT ans2: n2
INPUT ans3: n3
INPUT ans4: mcq_ans
EXPECT prt_ans1: NODE0-T
EXPECT prt_ans2: NODE0-T
EXPECT prt_ans3: NODE0-T
EXPECT prt_ans4: NODE0-T
