---
name: ads2-ica-open-analysis
description: Use this skill for ADS2 ICA or open-ended analysis reports, especially substance_use.csv, Global Burden of Disease data, filtering by measure/location/sex/age/cause/year, trend plots, age/sex comparisons, asking an original question, reproducible RMarkdown, and interpreting observational data. Trigger on ICA, group exercise, substance_use, open question, prevalence, deaths, opioid, alcohol, trend over time, or "ask your own question".
---

# ADS2 ICA Open Analysis

ICA marking emphasizes clarity, complete code, interpretation, reproducibility, and sensible scope. A simple question thoroughly answered can score better than an ambitious weak model.

## ICA Workflow

1. State the question.
2. Import and check data.
3. Filter relevant rows.
4. Summarize values with grouping.
5. Plot before modeling.
6. Choose a course-covered method.
7. Interpret in context.
8. State limitations and a next step.

## Substance Use Dataset Columns

Common columns:

- `measure`: `Deaths` or `Prevalence`
- `location`: world region
- `sex`: `Male` or `Female`
- `age`: 5-year age group
- `cause`: `Alcohol use disorders` or `Opioid use disorders`
- `metric`: usually `Percent`
- `year`
- `val`: best estimate
- `upper`, `lower`: uncertainty interval

## Import And Check

```r
library(tidyverse)
health_df <- read.csv("substance_use.csv")
str(health_df)
head(health_df)
colSums(is.na(health_df))
sum(duplicated(health_df))
```

Do not use personal absolute paths in final submission.

## Direct Question Example

"In 2019, what region has the highest alcohol-related death rate among men aged 40-44?"

```r
q1 <- health_df |>
  filter(measure == "Deaths",
         cause == "Alcohol use disorders",
         sex == "Male",
         age == "40 to 44",
         year == 2019)

q1[which.max(q1$val), c("location", "val", "lower", "upper")]
```

## Trend Plot

```r
trend <- health_df |>
  filter(measure == "Prevalence",
         cause == "Opioid use disorders",
         location == "North America") |>
  group_by(year, age) |>
  summarise(mean_val = mean(val), .groups = "drop")

ggplot(trend, aes(x = year, y = mean_val, color = age)) +
  geom_line() +
  labs(x = "Year", y = "Prevalence (%)")
```

## Regression-By-Group Trend

```r
models <- trend |>
  group_by(age) |>
  do(model = lm(mean_val ~ year, data = .))

slopes <- sapply(models$model, function(m) coef(summary(m))[2, 1])
data.frame(age = models$age, slope = slopes)
```

## Comparing Periods

```r
early <- trend |> filter(year >= 1992, year <= 1997)
late <- trend |> filter(year >= 1998, year <= 2003)

get_slopes <- function(dat) {
  models <- dat |>
    group_by(age) |>
    do(model = lm(mean_val ~ year, data = .))
  sapply(models$model, function(m) coef(summary(m))[2, 1])
}

slopes_early <- get_slopes(early)
slopes_late <- get_slopes(late)
wilcox.test(slopes_late, slopes_early, paired = TRUE, alternative = "greater")
```

## Good Open Question Criteria

Choose a question that:

- uses only available columns or clearly cited additional data;
- can be answered by plots, summaries, hypothesis tests, regression, or simulation learned in the course;
- has enough data after filtering;
- has a clear response variable and comparison/trend;
- avoids causal claims from observational data.

## ICA Interpretation Template

```text
The plot shows [trend/pattern] in [group/location]. The model/test provides [evidence/insufficient evidence] that [specific claim]. Because these are observational prevalence/death estimates, this should be interpreted as an association/trend rather than proof of causation. A useful next step would be [specific follow-up].
```
