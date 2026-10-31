---
name: statistical-analysis
description: Use when the user needs hypothesis testing, A/B testing, experimental design, statistical inference, confidence intervals, Bayesian analysis, causal inference, or any question that requires rigorous statistical reasoning rather than ML prediction.
---

# Statistical Analysis & Experimentation

Apply rigorous statistical reasoning. Do not confuse prediction with inference or correlation with causation.

## 1. Clarify the question

Determine whether the task is estimation, comparison, association, prediction, or causal inference. Identify the population, sampling mechanism, unit of observation, response variable, and potential confounders. Ask for the business context and decision that depends on the result.

## 2. Choose the right framework

- **Frequentist inference**: use when the question maps naturally to null-hypothesis significance testing, confidence intervals, or controlled experiments with clear rejection criteria.
- **Bayesian inference**: use when prior information is meaningful, sample sizes are small, or the stakeholder needs probability statements about parameters rather than p-values.
- **Causal inference**: use when the question is about the effect of an intervention. Identify potential outcomes, confounders, and the assignment mechanism. Apply difference-in-differences, instrumental variables, regression discontinuity, propensity score matching, or randomised experiments as appropriate.

State which framework is chosen and why.

## 3. Hypothesis testing checklist

- Define H₀ and H₁ before looking at the data.
- Select the test based on data type, distribution assumptions, sample size, and independence structure:
  * Continuous, normal, two groups: t-test (independent or paired).
  * Continuous, non-normal or ordinal: Mann-Whitney U / Wilcoxon signed-rank.
  * Proportions: z-test for proportions, chi-squared, or Fisher's exact test.
  * Multiple groups: ANOVA / Kruskal-Wallis with post-hoc corrections.
  * Correlation: Pearson (linear, normal) or Spearman (monotonic, ordinal).
  * Repeated measures / mixed designs: repeated-measures ANOVA or mixed-effects models.
- Check assumptions: normality (Shapiro-Wilk, Q-Q plot), equal variances (Levene's), independence.
- Report test statistic, p-value, effect size (Cohen's d, η², odds ratio, risk ratio), and confidence interval.
- Interpret p-values correctly: a p-value is not the probability that H₀ is true.
- Apply multiple-comparison corrections (Bonferroni, Holm, Benjamini-Hochberg) when testing multiple hypotheses.

## 4. A/B testing and experimentation

- **Power analysis**: calculate required sample size before running the experiment using `statsmodels.stats.power` or equivalent. Specify minimum detectable effect, significance level (α), power (1 − β), and baseline metric.
- **Randomisation**: verify that assignment is truly random and balanced. Check for sample ratio mismatch (SRM).
- **Guardrail metrics**: define metrics that must not degrade.
- **Sequential testing**: if monitoring results during the experiment, use sequential methods (e.g., alpha spending, always-valid p-values) to control false positive rate. Do not repeatedly check a fixed-horizon test.
- **Duration**: run the experiment long enough to capture weekly cycles and novelty/primacy effects.
- **Analysis**: compare treatment vs control using the pre-registered primary metric. Report confidence interval, practical significance, and segment-level effects when relevant.

## 5. Common pitfalls to flag

- p-hacking: testing many hypotheses and reporting only significant ones.
- Confusing statistical significance with practical significance.
- Survivorship bias, selection bias, Simpson's paradox.
- Using correlation to imply causation without a causal design.
- Ignoring multiple comparisons.
- Underpowered studies that cannot detect meaningful effects.

## 6. Deliverable

Provide: the statistical question in plain language, chosen test with justification, assumption checks, test results with effect sizes and confidence intervals, plain-language interpretation, limitations, and a reproducible Python/R code block using scipy, statsmodels, pingouin, or pymc as appropriate.
