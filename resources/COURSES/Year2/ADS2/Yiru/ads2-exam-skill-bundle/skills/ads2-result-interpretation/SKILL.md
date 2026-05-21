---
name: ads2-result-interpretation
description: Use this skill for ADS/ADS2 result wording, p-value interpretation, confidence interval interpretation, slope and coefficient interpretation, ANOVA and chi-square conclusions, Bayes posterior wording, power-analysis reporting, limitations, and "what should we conclude" exam prose. Trigger on interpret, conclusion, p-value, confidence interval, slope, R-squared, report wording, limitation, next step, or "how to write this result".
---

# ADS2 Result Interpretation

Use context-specific language. A result without interpretation loses marks.

## p-Value Decision

```text
At alpha = 0.05, the p-value is [p]. Since [p < 0.05 / p >= 0.05], I [reject / fail to reject] H0. This provides [evidence / insufficient evidence] that [contextual claim].
```

Do not write "accept H0". Do not write "prove".

## t-Test

```text
I used a [paired / Welch two-sample / one-sample] t-test because [reason]. The test gave t = [t], df = [df], p = [p]. Therefore, [contextual conclusion]. The direction of the effect is [describe mean difference].
```

## Wilcoxon

```text
Because the data were [ordinal / not approximately normal], I used a Wilcoxon [rank-sum / signed-rank] test. The p-value was [p], so there is [evidence / insufficient evidence] for a difference in [median/location] between [groups].
```

## ANOVA

```text
I used ANOVA because the response [y] is numeric and the explanatory variable(s) [x] are categorical. The model was [formula]. The ANOVA result showed [factor] had p = [p]. Therefore, there is [evidence / insufficient evidence] that [factor] affects [response].
```

Interaction:

```text
The interaction between [A] and [B] was significant, so the effect of [A] depends on the level of [B]. Main effects should be interpreted cautiously.
```

Tukey:

```text
Tukey's HSD suggests the main differences are between [group1] and [group2], with adjusted p = [p].
```

## Chi-Square

Goodness-of-fit:

```text
I used a chi-square goodness-of-fit test because the question compares observed counts with an expected distribution. The test gave X2 = [stat], df = [df], p = [p]. Thus, the observed counts [do / do not] differ from the expected distribution.
```

Independence/homogeneity:

```text
I used a chi-square test on the contingency table because both variables are categorical. The test gave X2 = [stat], df = [df], p = [p]. This provides [evidence / insufficient evidence] that [variables] are associated.
```

Small expected counts:

```text
Some expected counts were small, so the chi-square approximation may be unreliable. I therefore used Fisher's exact test, which gave p = [p].
```

## Correlation and Regression

Correlation:

```text
The correlation between [x] and [y] was r = [r], indicating a [weak/moderate/strong] [positive/negative] association. This does not by itself show causation.
```

Slope:

```text
The slope for [x] was [beta]. This means that for a one-unit increase in [x], the model predicts [y] changes by [beta] units on average, assuming the model is appropriate.
```

R-squared:

```text
The model R-squared was [R2], meaning that about [percent]% of the variation in [y] is explained by the model. This is model fit, not proof of causation.
```

## Bayes

```text
Assuming [prior assumptions], the posterior probability of [hypothesis] after observing [data] is [probability]. This result would change if the prior probabilities changed.
```

## Power

```text
The estimated current power is [power] at alpha = 0.05. Since this is [below/above] 0.8, the study is [underpowered / adequately powered] for an effect of this size. To reach 0.8 power, the estimated required sample size is [n].
```

## Limitations and Next Step

```text
This conclusion is limited by [sample size / missing covariates / observational design / small expected counts / non-normal residuals / lack of control group]. A useful next step would be [specific recommendation].
```
