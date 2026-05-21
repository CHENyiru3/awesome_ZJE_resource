---
name: ads2-exam-workflow
description: Use this skill whenever the user is answering an ADS/ADS2 coding challenge, online problem-solving exam, or ICA-style RMarkdown report and needs the overall answer structure. Trigger on ADS exam, ADS2 exam, coding challenge, RMarkdown exam answer, ICA report, "how should I write the answer", or when multiple statistical tasks must be presented coherently.
---

# ADS2 Exam Workflow

Use this as the top-level workflow skill. ADS2 marking rewards a readable report, not only correct code.

## Default Answer Shape

For each question, produce:

1. **Data import and inspection**: show data loaded, structure, missing values, duplicates.
2. **Cleaning or reshaping**: only what is needed; explain it.
3. **Useful plot or summary**: boxplot, scatterplot, barplot, histogram, trend plot, paired plot.
4. **Method choice**: name the method and justify using variable types/design.
5. **Hypotheses**: state H0 and H1 in context.
6. **Assumptions**: check or explain why a non-parametric/simulation alternative is used.
7. **R code and output**: include code and key result.
8. **Conclusion**: contextual interpretation, limitations, and next step.

## Fast Report Template

```markdown
### Data checking
I imported the data and checked its structure, missing values, and duplicate rows. [State findings.]

### Plot and summary
[Describe the plot and what it suggests.]

### Method
The response variable is [response]. The explanatory variable(s) are [predictors]. Because [design/variable types], I used [method].

H0: [null in context].
H1: [alternative in context].

### Assumptions
[State checks and results.]

### Result
[Report test statistic/model coefficient/p-value/CI/effect size.]

### Conclusion
At alpha = 0.05, I [reject/fail to reject] H0. This suggests [contextual conclusion]. A useful next step is [specific recommendation].
```

## Time Priority

If time is short, do these first:

1. correct data import and plot;
2. correct method and hypotheses;
3. p-value/result and contextual conclusion;
4. one sentence on assumptions or limitations.

## Next-Step Recommendations

Good ADS2 recommendations are specific:

- Use power analysis before recommending a larger sample size.
- Add a control group if the design lacks one.
- Collect key covariates such as age, sex, baseline severity, batch, site, or genotype.
- Use a paired design if biologically appropriate.
- Run Tukey HSD or another post-hoc comparison after a significant ANOVA.
- Use Fisher exact test or collect more data if chi-square expected counts are too small.

Avoid generic "more research is needed" without saying what and why.

## Required Language

- Use "fail to reject H0", not "accept H0".
- Use "evidence suggests", not "prove".
- Say "association" unless the design supports causation.
- Mention units where possible.
