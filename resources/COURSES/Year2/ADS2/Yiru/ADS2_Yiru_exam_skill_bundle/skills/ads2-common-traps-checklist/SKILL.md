---
name: ads2-common-traps-checklist
description: Use this skill as a final ADS/ADS2 exam answer review checklist. It catches common mistakes in data cleaning, test choice, paired designs, ANOVA interactions, chi-square expected counts, pwr sample-size formulas, regression wording, clustering interpretation, and report language. Trigger on review my ADS answer, check mistakes, before submission, common traps, is this correct, or final checklist.
---

# ADS2 Common Traps Checklist

Run this before final submission or when reviewing an answer.

## Language

- Use "fail to reject H0", not "accept H0".
- Use "evidence suggests" or "is associated with", not "prove".
- Do not report only a p-value; write a contextual conclusion.
- Do not call a non-significant result "no effect"; mention insufficient evidence and power if relevant.

## Data Handling

- Avoid personal absolute file paths in final RMarkdown.
- Do not remove missing values or duplicates silently.
- Do not treat repeated measures as independent observations.
- Convert categorical numeric codes to factors when needed.
- Merge paired files by ID, not row order unless order is verified.

## Test Choice

- Paired before/after data needs paired tests.
- Independent groups need independent tests.
- For paired t-tests, check normality of differences.
- Ordinal data should not be treated as interval numeric without justification.
- More than two groups: use ANOVA/Kruskal-Wallis first, not many t-tests.
- Two-factor designs need factorial ANOVA and interaction consideration.

## Chi-Square

- Check expected counts, not observed counts.
- Goodness-of-fit uses expected probabilities explicitly.
- Independence/homogeneity uses a count table or matrix.
- Use Fisher exact test if expected counts are too small.
- Do not run `chisq.test()` on a `CrossTable` display object; use the count matrix.

## Power

- `pwr.t.test(n = ...)` uses per-group n for two-sample tests.
- `pwr.anova.test(n = ...)` uses per-group n.
- Cohen's f for ANOVA is `sqrt(eta_sq / (1 - eta_sq))`.
- A sample-size recommendation needs an effect size and target power.

## Regression

- Correlation is not causation.
- Slope interpretation needs units.
- Intercept interpretation may be meaningless if x = 0 is outside the data range.
- Check residual plots before trusting linear model inference.
- Correlated predictors can make coefficient p-values unstable.

## Clustering

- Set a seed for k-means.
- Scale numeric features if ranges differ.
- Cluster labels are arbitrary.
- Compare clusters to known labels with a table, not by color alone.
