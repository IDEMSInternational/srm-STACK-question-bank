# Five STACK-conversion candidates: full text, worked solutions, and book context

These are the 5 hand-picked Tier-A candidates from `shortlist_top.md` (see that file for why
these five were chosen over the other 87 Tier-A exercises). All five have a worked solution
in the textbook, so all five are included here in full: original exercise text, worked
solution, and where each sits in the book.

---

## 1. PizzasHT — Ch. 27 "Hypothesis tests: one mean" (§Exercises, `27-Testing-OneMean.Rmd`)

**Book context:** Comes right after the chapter's own worked example (§"Example: student IQs")
and the statistical-validity-conditions section. The same *Eagle Boys Pizza* dataset
(`PizzaSize`) is used earlier in Ch. 23 for a **confidence interval** on the same claim ("also
seen in Exercise CIPizzas") — so the book deliberately reuses this dataset to contrast CI vs.
hypothesis-test workflows on identical data.

**Original text:**
> *Dataset: `PizzaSize`.* In 2011, Eagle Boys Pizza ran a campaign that claimed Eagle Boys
> pizzas were "Real size 12-inch large pizzas." Eagle Boys made the data from the campaign
> publicly available. Using the summary of the diameters of a sample of 125 of their large
> pizzas (software output figure), test the company's claim:
> *For Eagle Boys' pizzas, is mean diameter actually 12 inches, or not?*
>
> 1. What is the parameter of interest?
> 2. Write down the values of x̄ and s.
> 3. Determine the value of the standard error of the mean.
> 4. Write the hypotheses to test if the mean pizza diameter is 12 inches.
> 5. Is the alternative hypothesis one- or two-tailed? Why?
> 6. Draw the normal distribution that shows how the sample mean pizza diameter would vary by
>    chance, even if the population mean diameter was 12 inches.
> 7. Compute the t-score for testing the hypotheses.
> 8. What is the approximate P-value using the 68–95–99.7 rule?
> 9. Write a conclusion: do pizzas have a mean diameter of 12 inches, as claimed?
> 10. Is it reasonable to assume the statistical validity conditions are satisfied?

**Worked solution:**
1. μ: population mean pizza diameter.
2. x̄ = 11.486; s = 0.247.
3. SE = 0.02205479.
4. H₀: μ = 12; H₁: μ ≠ 12.
5. Two-tailed; RQ asks if diameter is 12 inches, or not.
6. Normal distribution, mean 12, std dev = s.e.(x̄) = 0.02205.
7. t = −23.3.
8. P really small.
9. Very strong evidence mean diameter is not 12 inches.
10. n much larger than 25; statistically valid.

---

## 2. EthiopianFarmers — Ch. 31 "Comparing two odds or proportions: CIs and tests" (§Exercises, `31-CIsTesting-OddsRatios.Rmd`)

**Book context:** Follows two worked examples in the chapter ("Example: turtle nests" and
"Example: health of female burros"), which build up the same proportion-difference →
odds-ratio → CI/test pipeline this exercise applies to new data.

**Original text:**
> Meresa et al. (2023) investigated Ethiopian farmers' adoption of improved soil and water
> conservation structures on their farms. Software output is shown in an accompanying figure.
>
> Raw 2×2 table (adoption of conservation practices by farm size):
>
> | | Non-adopter | Adopter |
> |---|---|---|
> | < 0.5 ha (small) | 86 | 61 |
> | ≥ 0.5 ha (large) | 43 | 71 |
>
> 1. Based on the output, how is the difference between the two proportions defined?
> 2. Write the hypothesis for comparing the proportions, using this definition of the
>    difference.
> 3. Use the software output to conduct the test.
> 4. Use the software output to write down the corresponding CI for the difference in
>    proportions.
> 5. Based on the output, how is the OR defined?
> 6. Write the hypothesis for comparing the odds, for farmers with small and large farms.
> 7. Use the software output to conduct the test.
> 8. Use the software output to write down the corresponding CI for the OR.
> 9. Are the CIs and tests statistically valid?

**Worked solution:**
1. Proportion non-adopters in small (Row 1), minus proportion non-adopters in large (Row 2).
2. H₀: p_S − p_L = 0; H₁: p_S − p_L ≠ 0.
3. z = 3.33; P < 0.001; evidence of a difference.
4. 0.0881 to 0.327, larger proportion non-adopters in small farms.
5. Odds of non-adopter, comparing small to large.
6. One option: H₀: OR = 1; H₁: OR ≠ 1.
7. χ² = 11.10; P < 0.001; no evidence of difference (odds version).
8. OR between 1.41 and 3.84.
9. Smallest expected count: 56.3; yes, valid.

---

## 3. OneMeanCIBears — Ch. 23 "Confidence intervals: one mean" (§Exercises, `23-CIs-OneMean.Rmd`)

**Book context:** This is the first exercise in Ch. 23's exercise set, immediately after the
chapter's own worked example ("Example: cadmium in peanuts") — it's meant to be the cleanest,
most stripped-down instance of the one-mean-CI pipeline in the book.

**Original text:**
> Bartareau et al. (2017) studied American black bears, and found the mean weight of the
> n = 185 male bears was x̄ = 84.9 kg, with a standard deviation of s = 51.1 kg.
>
> 1. Define the parameter of interest.
> 2. Compute the standard error of the mean.
> 3. Draw a picture of the approximate sampling distribution for x̄.
> 4. Compute the approximate 95% CI.
> 5. Write a conclusion.
> 6. Is the CI statistically valid?

**Worked solution:**
1. Parameter: population mean weight of American black bear, μ.
2. s.e.(x̄) = 3.756947.
3. Normal; mean μ; std dev: 3.757.
4. 77.4 to 92.4 kg.
5. Approx. 95% confident population mean weight of male American black bears is between 77.4
   and 92.4 kg.
6. Statistically valid: n ≥ 25.

---

## 4. SampleSizeMean1 — Ch. 32 "Finding sample sizes for CIs" (§Exercises, `32-Sample-Size-Estimation.Rmd`)

**Book context:** Follows the chapter's worked example ("Example: emergency residential aged
care") which derives the n = (z·s/E)² formula this exercise applies directly.

**Original text:**
> Suppose we need to estimate a population mean (with 95% confidence), using s = 1 kg.
>
> 1. What size sample is needed to estimate the population mean within 0.4 kg?
> 2. What size sample is needed to estimate the population mean within 0.2 kg (that is, the CI
>    will be half as wide as in the first calculation)?
> 3. What size sample is needed to estimate the population mean within 0.1 kg (that is, the CI
>    will be a quarter as wide as in the first calculation)?
> 4. To get a CI half as wide, how many times more units of analysis are needed?
> 5. To get a CI a quarter as wide, how many times more units of analysis are needed?
> 6. Would a smaller or larger sample be needed to estimate the population mean within 0.4 kg,
>    with 99% confidence? Explain.

**Worked solution:**
1. At least 25.
2. At least 100 (4 times as many).
3. At least 400 (16 times as many).
4. Halve width: 4 times as many.
5. Quarter width: 16 times as many.
6. More needed for greater precision (99% vs 95%).

---

## 5. CorollaPrice — Ch. 33 "Correlation and regression: CIs and tests" (§Exercises, `33-CorrelationRegression.Rmd`)

**Book context:** Sits after the chapter's worked example ("Example: removal efficiency");
it's the richest single regression exercise in the book, chaining scatterplot description,
hand-fitting, software-output interpretation, prediction, hypothesis test, and CI all in one
exercise. It's also the exercise underlying the bank's existing regression match (#104, see
`strongest_matches.md`), but #104 only covers the "fit and predict" portion — parts 12–13
(test and CI for slope) have no existing bank equivalent.

**Original text:**
> *Dataset: `Corollas`.* On 25 June 2014, I searched Gum Tree (an Australian online
> marketplace) for "Toyota Corolla" in the "Cars, Vans & Utes" category. I recorded the age
> and the price of each (second-hand) car from the first two pages of results returned. I
> restricted the data to cars less than 14 years old at the time, removed one 13-year-old
> Corolla advertised for sale for $390,000, then produced a scatterplot of price vs. age
> (n = 38).
>
> 1. Describe the relationship displayed in the graph, in words.
> 2. What else could influence the price of a second-hand Corolla besides the age?
> 3. Consider a seven-year-old Corolla selling for $15,000. Would this be cheap or expensive?
>    Explain.
> 4. As stated, I removed one observation: a 13-year-old Corolla for sale at $390,000. What do
>    you think the price was meant to be listed as, by looking at the scatterplot? Explain.
> 5. From the scatterplot, draw (or estimate by eye) an approximation of the regression line.
>    Then estimate the value of b₀ (the intercept) from the line you drew. What does this
>    mean? Do you think this value is meaningful?
> 6. Estimate the value of b₁ (the slope) from the line you drew. What does this mean? Do you
>    think this value is meaningful?
> 7. From the line you drew above, write down an estimate of the regression equation.
> 8. What are the units of the intercept and the slope?
> 9. Use the software output (relating price in thousands of dollars to age) to write down the
>    regression equation.
> 10. Using the software output, write down the value of r. Using this value of r, compute the
>     value of R². What does this mean?
> 11. Use the regression equation from the software output to estimate the sale price of a
>     Corolla that is 20 years old, and explain your answer.
> 12. Using the software output, perform a suitable hypothesis test to determine if there is
>     evidence that lower prices are associated with older Corollas.
> 13. Compute an approximate 95% CI for the population slope (use the software output).
> 14. I could have drawn a scatterplot with Price on the vertical axis and Year of manufacture
>     on the horizontal axis instead. For this graph: (a) What is the value of the correlation
>     coefficient? (b) How would R² change (if at all)? (c) How would the slope change (if at
>     all)? (d) How would the intercept change (if at all)?

**Worked solution:**
1. Approximately linear, negative, reasonably strong.
2. Condition; extras (air con, etc.); sedan/hatch; etc.
3. Expensive: above the regression line.
4. Probably $3,900.
5. b₀ ≈ 20; mean price of a 2014 second-hand Corolla about $20,000.
6. b₁ = (2 − 20)/(14 − 0) ≈ −1.3; price reduces about $1,300 each year older.
7. ŷ = 20 − 1.3x (very rough).
8. Intercept: dollars; slope: dollars per year.
9. ŷ = 16.41 − 0.96x; y = price in thousands of dollars, x = age in years.
10. r = −0.922, R² = 85%.
11. ŷ = 16.41 − (0.96 × 20) = −2.79: extrapolating (nonsensical negative price — the point).
12. Hardly need a test: H₀: β₁ = 0 vs H₁: β₁ < 0; t = −13.71, P = 0.0001/2 = 0.00005. Very
    strong evidence older cars fetch lower second-hand prices, on average.
13. −0.958 ± (2 × 0.070), i.e. −0.958 ± 0.140, or −1.098 to −0.818.
14. Same relationship, reflected left-to-right. (a) Size of r same but positive: r = 0.93.
    (b) Same R². (c) Same slope magnitude, but positive. (d) Intercept changes — becomes the
    predicted price at year 0, which is meaningless.
