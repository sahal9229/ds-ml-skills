---
name: ml-workflow-engineering
description: Use when designing or implementing an end-to-end machine-learning workflow, including target definition, preprocessing, feature engineering, data splitting, model selection, training, and reproducible pipelines.
---

# ML Workflow Engineering

Design a reliable workflow matched to the data and objective.

## 1. Frame the problem

Confirm the prediction target, prediction time, unit of analysis, available-at-prediction features, deployment constraints, and cost of different errors. Classify the task as classification, regression, clustering, ranking, forecasting, NLP, computer vision, or another justified formulation. Do not infer the task from a dataset name alone.

## 2. Choose a validation strategy

- IID classification/regression: holdout split, often with stratification for classification when class counts permit.
- Repeated entities: group-aware split to prevent the same entity leaking across partitions.
- Temporal prediction: chronological or rolling-origin split; never randomly shuffle future and past observations.
- Small datasets: consider cross-validation, while keeping a genuinely untouched final test set when feasible.
- Image/text data: check near-duplicates, source-level grouping, and augmentation leakage.

Explain why the selected split reflects the intended real-world use.

## 3. Build preprocessing correctly

For tabular data, inspect numerical/categorical columns and create a ColumnTransformer with appropriate imputers, scaling where the estimator needs it, and OneHotEncoder(handle_unknown='ignore') or another justified encoding. Put all learned preprocessing inside a Pipeline and fit only on training folds. Never fit a scaler or imputer on the full dataset before splitting.

For text, establish a simple baseline such as TF-IDF with Naive Bayes or Logistic Regression where appropriate. Keep vectorization inside the evaluation pipeline. Fit vocabulary and IDF only on training data.

For images, verify labels, split by source/identity when necessary, use consistent resizing and normalization, and apply augmentation only to training data. Explain the trade-offs between a small CNN baseline and transfer learning. Do not use augmentation on validation/test images.

For sequence/time-series tasks, preserve ordering, define the forecast horizon and lookback window, and ensure every feature is available at prediction time. Scale using training data only and invert target scaling only when interpreting predictions in original units.

## 4. Establish and compare models

Start with a simple baseline, then compare a small number of justified candidates. Examples: DummyClassifier/Regressor, LogisticRegression, Naive Bayes, tree ensembles, gradient boosting, linear models, or neural networks when data scale and problem structure justify them. State why an algorithm is suitable and its limitations.

Avoid unnecessary deep learning for small structured datasets. Do not tune many models before verifying the data and baseline.

## 5. Reproducibility and implementation

Provide runnable code with imports, dependency assumptions, deterministic seeds where meaningful, explicit target/features, Pipeline, evaluation, and saved artifacts when requested. Use a clear project structure only when the task warrants it. Keep train/validation/test roles explicit. Include checks for shape, missing values, label encoding, class counts, and prediction output.

## 6. Required validation

Check that preprocessing is fitted only on training data, the split matches the intended deployment scenario, the baseline is recorded, metrics suit the objective, and no information from the future or target leaks into features. State limitations and practical next steps.
