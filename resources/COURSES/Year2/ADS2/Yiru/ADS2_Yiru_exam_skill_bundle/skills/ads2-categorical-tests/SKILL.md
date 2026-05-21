---
name: ads2-categorical-tests
description: Use this skill for ADS/ADS2 categorical data, chi-square goodness-of-fit, chi-square independence or homogeneity, Fisher exact test, Mendelian ratios, genotype/survival counts, satisfaction tables, expected counts, CrossTable usage, ordinal categorical choices, and categorical plots. Trigger on chi-square, chisq.test, Fisher, categorical, counts, contingency table, Mendelian, genotype, survival, satisfaction, homogeneity, independence, or goodness-of-fit.
---

# ADS2 Categorical Tests

Categorical tests use counts, not raw continuous measurements.

## Decide Which Test

- One categorical variable vs expected proportions: chi-square goodness-of-fit.
- Two categorical variables in a contingency table: chi-square independence/homogeneity.
- Small expected counts: Fisher exact test or simulation.
- Ordinal categorical response: consider Wilcoxon/Kruskal instead of pretending equal intervals.

## Goodness-of-Fit

Example Mendelian genotype ratio:

```r
obs <- c(WT = 17, het = 56, mut = 7)
fit <- chisq.test(obs, p = c(1/4, 1/2, 1/4))
fit
fit$expected
```

Hypotheses:

```text
H0: observed counts follow the expected distribution.
H1: observed counts do not follow the expected distribution.
```

## Independence / Homogeneity

```r
tab <- table(dat$treatment, dat$outcome)
fit <- chisq.test(tab)
fit
fit$expected
```

Known counts:

```r
tab <- matrix(c(980, 473, 864, 714), nrow = 2, byrow = TRUE)
rownames(tab) <- c("late", "early")
colnames(tab) <- c("satisfied", "unsatisfied")
chisq.test(tab)
prop.table(tab, margin = 1)
```

Hypotheses:

```text
H0: [variable 1] and [variable 2] are independent / distributions are the same across groups.
H1: [variable 1] and [variable 2] are associated / distributions differ across groups.
```

## Expected Count Rule

Check expected counts:

```r
fit$expected
any(fit$expected < 1)
mean(fit$expected < 5)
```

Course rule:

- no expected count below 1;
- no more than 20% of expected counts below 5.

If violated:

```r
fisher.test(tab)
```

## CrossTable

`gmodels::CrossTable()` is useful for display, but run the test on the count matrix/table.

```r
library(gmodels)
ct <- CrossTable(dat$x, dat$y, chisq = FALSE)
chisq.test(ct$t)
```

Do not run `chisq.test(ct)` on the display object.

## Interpretation

```text
I used a chi-square [goodness-of-fit / independence] test because the data are categorical counts. The test gave X2 = [stat], df = [df], p = [p]. Since [decision], there is [evidence/insufficient evidence] that [contextual conclusion].
```

For Fisher:

```text
Some expected counts were too small for the chi-square approximation, so I used Fisher's exact test. The p-value was [p], giving [conclusion].
```
