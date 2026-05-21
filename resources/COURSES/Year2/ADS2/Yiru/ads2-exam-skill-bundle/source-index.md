# Source Index

This bundle distills reusable ADS/ADS2 exam workflows, not full course documents.

## Source Folders

- `/Users/eric_yiru/Library/CloudStorage/OneDrive-InternationalCampus,ZhejiangUniversity/过去的/大二下/incourse/ADS2`
- `/Users/eric_yiru/Library/CloudStorage/OneDrive-InternationalCampus,ZhejiangUniversity/过去的/大二下/incourse/大二下`

## High-Relevance Sources

| Source | Type | Distilled topics |
|---|---|---|
| `ADS2_CC1_2023-24_Review.pdf` | PDF | paired t-test, Wilcoxon, ordinal SCI before/after, report marking expectations |
| `ADS2_mock_CC2_2023-24.pdf` | PDF | two-factor tooth-growth ANOVA, Mendelian genotype chi-square, coffee-shop contingency table |
| `mock.Rmd`, `mock.pdf` | Rmd/PDF | worked mock code, common solution pitfalls |
| `19级ADS2 S2.pdf`, `19ADS.Rmd` | PDF/Rmd | bioarchaeology normal-probability reasoning, categorical dementia example |
| `20级ADS2 S2.pdf`, `20ADS.Rmd` | PDF/Rmd | turtles Bayes example, k-means neuron classification, T-cell factor design |
| `Group_exercise-2023-24.pdf` | PDF | ICA requirements, reproducible open analysis, grading criteria |
| `Q1result.Rmd`, `Q1result.pdf`, `ICA2.md` | Rmd/PDF/MD | substance-use filtering, trend summaries, regression-by-age analysis |
| `Categorical_data(2).pdf` | PDF | chi-square, Fisher exact, ordinal categorical tests, expected-count rules |
| `ADS2Week2.4_Practical.pdf`, `week2.4_lecture_slides.pptx` | PDF/PPTX | power, sample size, Type I/II error, simulation |
| `Lecture2.14_slides.pptx` | PPTX | bootstrapping, sampling with replacement |
| `ADS2_CorLR_Practical 2023-24(1).Rmd`, `Correlation and regression.R` | Rmd/R | correlation and regression with COVID data |
| `regression.Rmd` | Rmd | multiple regression, interaction, VIF, nested model comparison |
| `week4 pra.Rmd` | Rmd | power simulation and `power.t.test` |
| `week7.Rmd` | Rmd | Bayes, lie detector, Markov chain simulation |
| `week14.Rmd` | Rmd | bootstrap medians and proportions |
| `feature_extract.Rmd` | Rmd | image reshaping and simple feature extraction |

## Key Datasets

| Dataset | Use |
|---|---|
| `ADS_files/teeth.csv` | two-factor ANOVA (`len ~ supp * dose`) |
| `ADS_files/genotype.csv` | Mendelian/categorical tests |
| `ADS_files/vmndata.csv` | k-means clustering |
| `ICA/substance_use.csv` | open ICA trend analysis |
| `owid-covid-data.txt`, `WBpopulation.csv` | correlation/regression practical |
| `mnist_train.csv`, `really_tiny_dataset.csv` | feature extraction practice |

## Extraction Notes

- Main PDFs were extracted with `pdftotext`.
- Main R/Rmd/MD files were read directly.
- PPTX text was extracted with `officecli view ... text`.
- `week2.13_lecture_slides(1).pptx` is 0 bytes and unusable.

## Excluded

IFBS, GP2, and DST2 files in the same parent folder were excluded unless referenced by ADS/ADS2 material.
