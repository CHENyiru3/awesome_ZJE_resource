---
name: ads2-data-cleaning
description: Use this skill for ADS/ADS2 exam data import, checking, cleaning, reshaping, typo correction, missing values, duplicates, factor conversion, paired-data merging, or preparing data for R statistical tests. Trigger when the user says clean data, check NA, duplicates, typo, reshape long/wide, pivot, gather, merge before/after, or "import and organize the data".
---

# ADS2 Data Cleaning

In ADS2 exams, data cleaning is part of the answer. Show enough checks to demonstrate that the data were understood.

## Basic Audit

```r
dat <- read.csv("file.csv")
str(dat)
head(dat)
summary(dat)
colSums(is.na(dat))
sum(duplicated(dat))
```

For tab-delimited files:

```r
dat <- read.table("file.txt", header = TRUE, sep = "\t")
```

## Missing Values

First locate missing values:

```r
colSums(is.na(dat))
```

Drop rows only if defensible:

```r
dat_no_na <- na.omit(dat)
colSums(is.na(dat_no_na))
```

Report it:

```text
Rows with missing values were removed because [reason]. The remaining dataset contained [n] observations.
```

If many rows are missing, do not silently remove them. Mention possible bias.

## Duplicates

```r
dup <- duplicated(dat)
sum(dup)
dat[dup, ]
```

Remove only exact erroneous duplicates:

```r
dat <- dat[!duplicated(dat), ]
```

Repeated patient/time/sample IDs may be real repeated measurements, not duplicates.

## Typos and Factor Levels

```r
unique(dat$group)
table(dat$group)
```

Targeted correction:

```r
dat$group <- gsub("4x", "4", dat$group)
dat$group <- factor(dat$group)
```

Convert categorical predictors before ANOVA/plots:

```r
dat$dose <- factor(dat$dose)
dat$treatment <- factor(dat$treatment)
```

## Combine Units

Example: minutes and seconds.

```r
before_sec <- dat$before_minutes * 60 + dat$before_seconds
after_sec <- dat$after_minutes * 60 + dat$after_seconds
diff_sec <- after_sec - before_sec
```

For paired tests, check `diff_sec`.

## Long/Wide Reshaping

Modern default:

```r
library(tidyr)

long <- dat |>
  pivot_longer(cols = -c(Month, Day),
               names_to = "variable",
               values_to = "value")

wide <- long |>
  pivot_wider(names_from = variable,
              values_from = value)
```

Legacy course-compatible:

```r
long <- gather(dat, key = "variable", value = "value", -Month, -Day)
```

## Merge Paired Files

```r
before <- read.csv("SCI_before.csv")
after <- read.csv("SCI_after.csv")
dat <- merge(before, after, by = "patient_ID")
head(dat)
sum(duplicated(dat))
```

Merge by ID. Do not `cbind()` before/after files unless the row order is verified.

## Reporting Sentence

```text
I imported the dataset, checked its structure, missing values, and duplicated rows. [No/Some] missing values and [no/some] exact duplicates were found. I converted [variables] to factors because they are categorical predictors.
```
