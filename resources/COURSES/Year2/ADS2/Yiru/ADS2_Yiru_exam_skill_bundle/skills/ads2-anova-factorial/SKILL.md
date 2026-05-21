---
name: ads2-anova-factorial
description: Use this skill for ADS/ADS2 one-way ANOVA, two-way/factorial ANOVA, interaction effects, Tukey HSD post-hoc tests, ANOVA assumption checks, numeric response by categorical factors, tooth-growth vitamin C designs, and ANOVA power. Trigger on ANOVA, aov, Tukey, interaction, factorial, two-way, dose and treatment, supplement, or numeric outcome across groups.
---

# ADS2 ANOVA And Factorial Designs

Use ANOVA when the response is numeric and predictors are categorical factors. ADS2 mock material includes a two-factor design, so do not assume ANOVA is only one-way.

## One-Way ANOVA

```r
dat$group <- factor(dat$group)
model <- aov(y ~ group, data = dat)
summary(model)
```

Hypotheses:

```text
H0: all group means are equal.
H1: at least one group mean differs.
```

## Two-Way / Factorial ANOVA

Example tooth-growth structure:

```r
dat$supp <- factor(dat$supp)
dat$dose <- factor(dat$dose)
model <- aov(len ~ supp * dose, data = dat)
summary(model)
```

`supp * dose` includes:

- main effect of `supp`;
- main effect of `dose`;
- interaction `supp:dose`.

If interaction is significant, interpret the interaction before main effects:

```text
The effect of supplement depends on dose, so the supplement effect should be compared within dose levels rather than only as an overall main effect.
```

## Assumption Checks

Independence is from study design. Check residuals:

```r
hist(resid(model))
shapiro.test(resid(model))
plot(model, 1)  # residuals vs fitted
plot(model, 2)  # normal Q-Q
```

Report:

```text
The residual normality check did not show strong evidence against normality (Shapiro p = [p]). The residuals-vs-fitted plot did not show an obvious pattern, so the equal-variance assumption appears reasonable.
```

If assumptions fail badly, consider Kruskal-Wallis for one-factor designs or simulation/bootstrap; for complex two-factor designs, state the limitation clearly.

## Post-Hoc Tests

After significant ANOVA:

```r
TukeyHSD(model)
```

Report:

```text
Tukey's HSD suggests the main pairwise difference is between [A] and [B] with adjusted p = [p].
```

## Plot

```r
boxplot(len ~ supp * dose, data = dat, xlab = "Group", ylab = "Length")
interaction.plot(dat$dose, dat$supp, dat$len)
```

## ANOVA Power

```r
a <- anova(model)
ss_factor <- a$"Sum Sq"[1]
ss_resid <- a$"Sum Sq"[nrow(a)]
eta_sq <- ss_factor / (ss_factor + ss_resid)
f <- sqrt(eta_sq / (1 - eta_sq))

library(pwr)
k <- length(unique(dat$group))
n_per_group <- min(table(dat$group))
pwr.anova.test(k = k, n = n_per_group, f = f, sig.level = 0.05)
```

Remember: `n` is per group.
