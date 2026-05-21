# ADS2 Exam Skill Bundle

Portable multi-skill bundle for ADS/ADS2 online problem-solving exams and ICA-style analysis.

This folder is not installed. To install later, copy the individual folders under `skills/` into a Codex/Claude skills directory.

## Skills

- `ads2-exam-workflow`: report structure, time management, and final-answer shape.
- `ads2-data-cleaning`: import, audit, missing values, duplicates, typos, factor conversion, reshaping, merge by ID.
- `ads2-probability-bayes-markov`: conditional probability, Bayes theorem, Bayes factor, logic-card tasks, Markov simulation.
- `ads2-power-sample-size`: power, Type I/II error, sample-size recommendations, `power.t.test`, `pwr` formulas, simulation fallback.
- `ads2-t-wilcoxon-tests`: one-sample, two-sample, paired t-tests, Wilcoxon rank-sum, Wilcoxon signed-rank, Kruskal-Wallis.
- `ads2-anova-factorial`: one-way and two-way/factorial ANOVA, interaction, assumptions, Tukey HSD, ANOVA power.
- `ads2-categorical-tests`: chi-square goodness-of-fit, independence/homogeneity, Fisher exact test, ordinal categorical choices.
- `ads2-correlation-regression`: correlation, simple/multiple regression, local trend regression, model comparison, diagnostics.
- `ads2-simulation-bootstrap`: bootstrap CIs, permutation/null randomization, simulation-based p-values and power.
- `ads2-clustering-feature-extraction`: k-means, cluster validation against labels, simple image feature extraction.
- `ads2-ica-open-analysis`: open-ended ICA workflow, substance-use dataset patterns, reproducibility and interpretation.
- `ads2-result-interpretation`: p-value, CI, slope, ANOVA, chi-square, Bayes, power, and limitation wording.
- `ads2-common-traps-checklist`: final pre-submit checklist for common ADS2 errors.

## Source

The bundle was distilled from the user's local ADS/ADS2 folders and user-provided exam notes. See `source-index.md`.

## Design Note

Each section is a separate skill with its own `SKILL.md`, because the exam tasks are modular. Agents can load only the relevant section instead of a large monolithic skill.
