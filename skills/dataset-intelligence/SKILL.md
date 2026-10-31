---
name: dataset-intelligence
description: Use when the user uploads or describes a CSV, Excel, Parquet, SQL extract, or other dataset and needs profiling, data-quality checks, exploratory analysis, or preparation recommendations.
---

# Dataset Intelligence

Perform evidence-based dataset reconnaissance before recommending transformations or models.

## 1. Establish the dataset

- Identify file type, shape, columns, data types, target candidate (only when evident), date/time fields, likely identifiers, and units where available.
- If the file is accessible, inspect it using the available data-analysis runtime. For large datasets, inspect schema and representative samples first; disclose sampling and avoid loading everything unnecessarily.
- If the file is not accessible, ask the user to attach it or provide `df.head()`, `df.info()`, `df.describe(include='all')`, and relevant target-column details. Do not pretend to have inspected it.

## 2. Profile quality

Check and report:

- Missing values: count and percentage per column; distinguish structural missingness from accidental missingness where evidence permits.
- Duplicate rows and likely duplicate entities; do not delete automatically.
- Data types that do not match the column meaning, malformed dates, mixed units, whitespace/casing inconsistencies, and invalid categories.
- Unique counts, high-cardinality columns, constant or near-constant columns, and likely ID columns.
- Numeric distributions, skew, ranges, quantiles, and potential outliers. Treat outliers as flags for investigation, not automatic deletion instructions.
- Categorical frequency and rare levels; target distribution and class imbalance when a target exists.
- Potential leakage, label contamination, time ordering, repeated customers/patients/devices, and train/test overlap risks.

## 3. EDA decisions

Choose analyses based on the question. Avoid generating every possible chart. Useful options include histograms and boxplots for numerical distributions, bar charts for categorical counts, time trends for temporal columns, and carefully chosen target-vs-feature comparisons. Explain what each plot can and cannot establish.

For supervised tasks, examine the target and its relationship to candidate predictors without using the final test set to guide feature selection. For time series, inspect frequency, missing timestamps, trend, seasonality, and chronological coverage.

## 4. Deliverable

Provide:

1. Dataset snapshot (shape, columns, types, target if known).
2. Data-quality findings, prioritised by impact.
3. Statistical or distribution findings supported by actual values.
4. Potential leakage, sampling, fairness, privacy, or representativeness risks when relevant.
5. Recommended cleaning actions, with rationale and what should not be changed automatically.
6. Next analysis or modeling step.

When asked for code, write a reusable Pandas profiling/cleaning script that uses the actual column names. Separate diagnosis from mutation: preserve a raw copy, make transformations explicit, and validate the result. Never assume a missing-value strategy, outlier rule, or target column without evidence.
