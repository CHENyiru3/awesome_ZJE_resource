---
name: ads2-power-sample-size
description: Use this skill for ADS/ADS2 statistical power, sample size, Type I and Type II error, power.t.test, pwr.t.test, pwr.anova.test, pwr.chisq.test, simulation-based power, or justifying whether to increase sample size. Trigger on power, sample size, beta, Type II error, underpowered, 0.8 power, pwr, or "what should we do next" when sample size is involved.
---

# ADS2 Power And Sample Size

Power is the probability that a test rejects a false null hypothesis:

```text
power = 1 - beta
```

Low power means high Type II error risk. Non-significance does not prove no effect.

## Report Template

Sufficient power:

```text
At alpha = 0.05, the estimated current power is [power]. This meets the common 0.8 target, so the current sample size is sufficient to detect an effect of approximately the observed size.
```

Insufficient power:

```text
At alpha = 0.05, the estimated current power is [power], below the common 0.8 target. This indicates high Type II error risk. To reach power 0.8 for an effect of this size, the estimated required sample size is [n]. I recommend increasing the sample size to at least this value, with balanced groups if possible.
```

## One-Sample t-Test

```r
power.t.test(n = 10, delta = 3, sd = 10,
             sig.level = 0.05,
             type = "one.sample",
             alternative = "one.sided")

power.t.test(delta = 3, sd = 10,
             sig.level = 0.05,
             power = 0.8,
             type = "one.sample",
             alternative = "one.sided")
```

## Two-Sample t-Test

Important: `n` is per group, not total sample size.

```r
library(pwr)

x <- c(...)  # group 1
y <- c(...)  # group 2
n1 <- length(x)
n2 <- length(y)

sd_pool <- sqrt(((n1 - 1) * var(x) + (n2 - 1) * var(y)) / (n1 + n2 - 2))
d <- abs(mean(x) - mean(y)) / sd_pool

current <- pwr.t.test(n = min(n1, n2), d = d,
                      sig.level = 0.05,
                      type = "two.sample")
needed <- pwr.t.test(d = d,
                     sig.level = 0.05,
                     power = 0.8,
                     type = "two.sample")
current
needed
```

If groups are unequal or variances differ, say this is an approximation.

## Paired t-Test

```r
diff <- after - before
d <- abs(mean(diff)) / sd(diff)

library(pwr)
pwr.t.test(n = length(diff), d = d,
           sig.level = 0.05,
           type = "paired")
```

## ANOVA

```r
model <- aov(y ~ group, data = dat)
a <- anova(model)
ss_group <- a$"Sum Sq"[1]
ss_resid <- a$"Sum Sq"[2]
eta_sq <- ss_group / (ss_group + ss_resid)
f <- sqrt(eta_sq / (1 - eta_sq))

library(pwr)
k <- length(unique(dat$group))
n_per_group <- min(table(dat$group))

current <- pwr.anova.test(k = k, n = n_per_group, f = f,
                          sig.level = 0.05)
needed <- pwr.anova.test(k = k, f = f,
                         sig.level = 0.05, power = 0.8)
```

Important: `n` is per group. Do not use the sum of response values.

## Chi-Square

```r
tab <- table(dat$x, dat$y)
fit <- chisq.test(tab)
X2 <- unname(fit$statistic)
N <- sum(tab)
r <- nrow(tab)
c <- ncol(tab)
w <- sqrt(X2 / (N * min(r - 1, c - 1)))

library(pwr)
current <- pwr.chisq.test(w = w, N = N,
                          df = (r - 1) * (c - 1),
                          sig.level = 0.05)
needed <- pwr.chisq.test(w = w,
                         df = (r - 1) * (c - 1),
                         sig.level = 0.05,
                         power = 0.8)
```

For goodness-of-fit, `w = sqrt(X2 / N)` is a common observed-effect estimate.

## Simulation Fallback

```r
set.seed(123)
B <- 10000
pvals <- replicate(B, {
  x <- rnorm(10, mean = 178, sd = 10)
  t.test(x, mu = 175, alternative = "greater")$p.value
})
mean(pvals < 0.05)
```

State the assumed effect size.
