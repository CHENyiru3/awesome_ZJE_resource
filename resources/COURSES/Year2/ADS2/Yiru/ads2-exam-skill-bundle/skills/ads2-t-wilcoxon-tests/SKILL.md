---
name: ads2-t-wilcoxon-tests
description: Use this skill for ADS/ADS2 one-sample t-tests, independent t-tests, paired t-tests, Shapiro normality checks, Wilcoxon rank-sum/Mann-Whitney tests, Wilcoxon signed-rank tests, Kruskal-Wallis tests, and choosing between parametric and non-parametric group comparisons. Trigger on t-test, paired test, before after, normality, Shapiro, Wilcoxon, Mann-Whitney, rank-sum, signed-rank, Kruskal, or non-parametric.
---

# ADS2 t-Tests And Wilcoxon Tests

Start with the design: one sample, two independent groups, or paired observations.

## Decision Rules

- One numeric sample vs known mean: one-sample t-test.
- Two independent numeric groups: Welch two-sample t-test by default.
- Same subjects before/after: paired t-test.
- If non-normal or ordinal:
  - independent two groups: Wilcoxon rank-sum / Mann-Whitney U;
  - paired two groups: Wilcoxon signed-rank;
  - three or more groups: Kruskal-Wallis.

For paired t-tests, check normality of differences, not raw groups.

## One-Sample t-Test

```r
hist(dat$x)
shapiro.test(dat$x)
t.test(dat$x, mu = 20)
```

Report:

```text
H0: the true mean [x] is 20.
H1: the true mean [x] is not 20.
```

## Paired t-Test

```r
diff <- dat$after - dat$before
hist(diff)
shapiro.test(diff)
t.test(dat$after, dat$before, paired = TRUE, alternative = "less")
```

Check the direction:

- `alternative = "less"` tests whether mean of first argument is less than second.
- Swap arguments or alternative carefully.

Report:

```text
Because each subject was measured before and after treatment, the observations are paired. The Shapiro-Wilk test on paired differences did not show strong evidence against normality, so I used a paired t-test.
```

## Independent t-Test

```r
boxplot(y ~ group, data = dat)
t.test(y ~ group, data = dat)  # Welch default
```

Report:

```text
I used Welch's two-sample t-test because the response is numeric and the two groups are independent; Welch's test does not assume equal variances.
```

## Wilcoxon Rank-Sum / Mann-Whitney U

```r
wilcox.test(y ~ group, data = dat, paired = FALSE, exact = FALSE)
```

Use for independent groups when data are ordinal or clearly non-normal.

## Wilcoxon Signed-Rank

```r
wilcox.test(dat$after, dat$before, paired = TRUE, exact = FALSE)
```

Use for paired non-normal/ordinal data, such as before/after ordinal clinical severity.

## Kruskal-Wallis

```r
kruskal.test(y ~ group, data = dat)
```

Use for three or more independent groups when ANOVA assumptions are not plausible. If significant, follow up with pairwise comparisons if time permits:

```r
pairwise.wilcox.test(dat$y, dat$group, p.adjust.method = "BH")
```

## Interpretation Template

```text
At alpha = 0.05, p = [p]. Therefore, I [reject/fail to reject] H0. This provides [evidence/insufficient evidence] that [contextual group difference].
```
