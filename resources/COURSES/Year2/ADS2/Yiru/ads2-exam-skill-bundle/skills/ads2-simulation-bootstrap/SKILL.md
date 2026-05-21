---
name: ads2-simulation-bootstrap
description: Use this skill for ADS/ADS2 bootstrapping, simulation-based tests, bootstrap confidence intervals, randomization/permutation tests, sample-with-replacement, simulation-based p-values, simulation power, and resampling medians or proportions. Trigger on bootstrap, simulation, sample with replacement, randomization, permutation, confidence interval by simulation, or "data do not fit assumptions".
---

# ADS2 Simulation And Bootstrap

Use bootstrap when the distribution is unknown and you want uncertainty for a statistic. Use randomization when H0 says labels do not matter.

## Bootstrap CI

```r
set.seed(123)
B <- 5000

boot_median <- replicate(B, {
  x_boot <- sample(x, size = length(x), replace = TRUE)
  median(x_boot)
})

quantile(boot_median, c(0.025, 0.975))
```

Two-group median difference:

```r
boot_diff <- replicate(B, {
  x_boot <- sample(x, length(x), replace = TRUE)
  y_boot <- sample(y, length(y), replace = TRUE)
  median(x_boot) - median(y_boot)
})
quantile(boot_diff, c(0.025, 0.975))
```

## Bootstrap Proportion

```r
outcome <- c(rep(1, satisfied), rep(0, unsatisfied))
B <- 5000
prop_boot <- replicate(B, {
  mean(sample(outcome, length(outcome), replace = TRUE))
})
quantile(prop_boot, c(0.025, 0.975))
```

## Null Randomization Test

Use when H0 says group labels are exchangeable.

```r
set.seed(123)
B <- 5000
obs <- median(x) - median(y)
pool <- c(x, y)
n_x <- length(x)

null_stats <- replicate(B, {
  shuffled <- sample(pool, length(pool), replace = FALSE)
  x_null <- shuffled[1:n_x]
  y_null <- shuffled[(n_x + 1):length(pool)]
  median(x_null) - median(y_null)
})

mean(abs(null_stats) >= abs(obs))
```

## Power Simulation

```r
set.seed(123)
B <- 10000
pvals <- replicate(B, {
  x <- rnorm(10, mean = 178, sd = 10)
  t.test(x, mu = 175, alternative = "greater")$p.value
})
mean(pvals < 0.05)
```

## Report Template

```text
I used [B] simulations. In each simulation, I [sampling procedure]. The estimated [p-value/power/95% interval] was [result]. This simulation depends on the assumptions used to generate/resample the data.
```

## Common Mistakes

- Bootstrap CI is not the same as a null hypothesis test.
- Use replacement for bootstrap.
- Use no replacement when shuffling labels for a permutation/randomization test.
- Set a seed for reproducibility.
- Do not simulate from assumptions you cannot explain.
