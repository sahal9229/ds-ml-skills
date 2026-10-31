---
name: model-evaluation-deployment
description: Use when evaluating, comparing, validating, packaging, serving, or deploying data-science and machine-learning models, including production-readiness reviews.
---

# Model Evaluation and Deployment

## Model evaluation

Choose metrics according to the task and error costs:

- Classification: confusion matrix, precision, recall, F1, ROC-AUC, PR-AUC, log loss, and threshold-specific performance as appropriate. For imbalanced targets, do not rely on accuracy alone. Explain positive-class definition and threshold.
- Regression: MAE, RMSE, and R-squared as appropriate. Negative R-squared is valid and indicates performance worse than predicting the test-set mean baseline; never clamp it to zero.
- Forecasting: evaluate against chronological holdouts and simple seasonal/naive baselines. Use metrics aligned to the scale and business cost; beware percentage metrics near zero.
- Clustering: combine suitable internal metrics with stability and domain usefulness. Do not pretend that a metric proves clusters are meaningful.

Always compare against a baseline. Report the validation method, sample size, confidence/variability where feasible, and limitations. Check train-versus-validation gaps, leakage, subgroup performance, calibration where relevant, and threshold effects. Do not tune on the final test set.

## Production readiness

Before recommending deployment, define the inference contract: input schema, output schema, validation, preprocessing, model version, and failure behavior. Package the complete fitted preprocessing-plus-model pipeline, not just an estimator when transformations are required.

For an API (for example FastAPI), include input validation, clear response schema, health endpoint, structured logging, useful error responses, and model loading strategy. For Docker, pin dependencies sensibly, use a small base image, avoid copying secrets, define a non-root user where practical, and add health checks. For CI, include tests, lint/type checks where appropriate, and reproducible builds.

For cloud services (AWS/GCP), explain the architecture and least-privilege IAM/service-account requirements. Never invent resource IDs, credentials, bucket names, regions, or console states. Verify current provider and library instructions when version-specific or time-sensitive details matter. Separate local proof-of-concept steps from production operations.

## Delivery checklist

- Reproducible training and inference environment.
- Versioned model and preprocessing artifacts.
- Input schema and data validation.
- Tests for preprocessing and prediction behavior.
- Monitoring plan for data quality, drift, latency, errors, and model performance where labels arrive.
- Rollback/version strategy and logging without leaking sensitive data.
- Clear README: setup, train, evaluate, serve, test, and deploy.

State what is production-ready, what remains a prototype, and which operational assumptions need confirmation. Never claim a deployment succeeded unless a deployment tool or user-provided evidence confirms it.
