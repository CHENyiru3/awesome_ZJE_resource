---
name: ads2-correlation-regression
description: Use this skill for ADS/ADS2 correlation, simple linear regression, multiple regression, regression assumptions, residual diagnostics, slope interpretation, R-squared, nested model comparison, interaction terms, VIF/multicollinearity, time-window/local regressions, and ICA trend modeling. Trigger on correlation, cor.test, regression, lm, slope, residuals, R-squared, model comparison, VIF, trend, predictor, or association.
---

# ADS2 Correlation And Regression

Correlation and regression describe association. Do not claim causation unless the study design supports it.

## Correlation

Use when both variables are numeric and the question asks about association.

```r
plot(dat$x, dat$y, xlab = "x", ylab = "y")
cor(dat$x, dat$y, use = "complete.obs")
cor.test(dat$x, dat$y)
```

Interpret:

```text
The correlation was r = [r], indicating a [weak/moderate/strong] [positive/negative] association between [x] and [y]. This does not show causation.
```

## Simple Linear Regression

```r
fit <- lm(y ~ x, data = dat)
summary(fit)
plot(dat$x, dat$y)
abline(fit, col = "red")
plot(fit)
confint(fit)
```

Slope:

```text
For each one-unit increase in [x], the model predicts [y] changes by [slope] units on average.
```

## Multiple Regression

```r
fit <- lm(y ~ x1 + x2 + group, data = dat)
summary(fit)
plot(fit)
```

Interaction:

```r
fit_int <- lm(y ~ x1 * group + x2, data = dat)
summary(fit_int)
```

If interaction is significant, the slope/effect of one predictor depends on the other.

## Assumptions

Check:

- independence of observations/errors from design;
- linear relationship;
- homoscedastic residuals;
- approximately normal residuals;
- no severe multicollinearity in multiple regression.

R checks:

```r
plot(fit, which = 1)  # residuals vs fitted
plot(fit, which = 2)  # QQ plot
hist(resid(fit))
shapiro.test(resid(fit))
```

Optional VIF if `car` is installed:

```r
library(car)
vif(fit)
```

Rule of thumb from course notes: VIF > 5 suggests potentially severe multicollinearity.

## Nested Model Comparison

```r
fit_simple <- lm(y ~ x1 + x2, data = dat)
fit_complex <- lm(y ~ x1 * x2 + x3, data = dat)
anova(fit_simple, fit_complex)
```

Interpret:

```text
The nested model comparison tests whether the additional terms improve fit enough to justify the more complex model. If p < 0.05, the complex model fits significantly better; otherwise prefer the simpler model.
```

## Local/Time-Window Regression

Useful for COVID/ICA trend tasks:

```r
library(dplyr)

models <- dat |>
  group_by(age) |>
  do(model = lm(value ~ year, data = .))

slopes <- sapply(models$model, function(m) coef(summary(m))[2, 1])
```

Compare slopes between periods:

```r
wilcox.test(slopes_late, slopes_early, paired = TRUE, alternative = "greater")
```

State that this is a trend analysis in observational data.
