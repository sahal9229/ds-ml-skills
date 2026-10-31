---
name: root-cause-debugging
description: Use when the user shares Python code, tracebacks, notebook failures, ML training errors, shape/type errors, dependency problems, or unexpected outputs and needs a verified root-cause diagnosis.
---

# Root-Cause Debugging

Debug systematically. Do not guess, randomly reinstall packages, or rewrite the whole project before identifying the failure.

## 1. Read the evidence

Inspect the complete traceback from the final exception line upward to the relevant user-code frame. Review the smallest code path that produces the failure, inputs, shapes, dtypes, versions, and expected versus actual behavior. If essential evidence is absent, ask for the traceback and the smallest reproducible snippet. Do not ask for information already supplied.

## 2. Form a root-cause diagnosis

Classify the problem where possible: syntax/name/import, wrong API/signature, shape mismatch, dtype mismatch, missing data, incorrect indexing, data leakage, device/memory, version incompatibility, filesystem/permissions, credentials/IAM, network, orchestration/task configuration, or logic error.

State:
- **Root cause:** the specific mismatch or faulty assumption.
- **Why it fails:** what the runtime expects versus what it receives.
- **Minimal fix:** the smallest correct code/configuration change.
- **Verification:** a check that demonstrates the fix and guards against regression.

If there are multiple plausible causes, rank them and state what evidence would distinguish them. Never present a hypothesis as confirmed fact.

## 3. Common ML/Python checks

- Print/check `shape`, `ndim`, `dtype`, index alignment, class counts, and nulls before changing code.
- Confirm scikit-learn estimator input dimensions and whether a 1D or 2D array is required.
- For scalers, fit on training data, preserve feature order, and pass the same number and order of features to `transform` and `inverse_transform`.
- For Keras/TensorFlow, verify batch, sequence, channel, and target shapes; check output layer/activation against task and loss; verify labels and data ranges.
- For NLP, inspect tokenization, vocabulary fit boundaries, sparse matrix dimensions, and label alignment.
- For Airflow, check DAG parse errors, task IDs, operator signatures, connections, hooks, permissions, and task logs before changing scheduler configuration.
- For AWS/GCP errors, inspect the exact denied action/resource and principal; propose least-privilege access, not broad administrator permissions.

## 4. Fix quality

Preserve the user's intended behavior. Do not hide errors by clamping metrics, swallowing exceptions, dropping rows without justification, or changing a function's contract silently. Explain any behavioral change. Prefer a focused patch and a small test. If dependencies may be involved, inspect the current environment first and offer a compatible installation command only when necessary.

## 5. Response format

Lead with the root cause in plain language. Then show the corrected line or complete corrected block, explain the important change, and provide a verification step. Keep the answer focused on the actual failure.
