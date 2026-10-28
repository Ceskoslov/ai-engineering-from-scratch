# Phase 02 — ml-fundamentals Review Summary

[All phases](../progress.md)

- Status: **Done / Passed**; passed on 2026-10-23; coverage: **21 lessons**.
- Initial score: **56/63**; final effective score: **56/63 (88.89%)**.
- Cumulative responses: 63, with 56 correct; **7 initial/retake mistakes** retained. Cumulative responses include retakes and are not the mastery-score denominator.
- Pass criteria: effective phase score ≥85% and final score ≥2/3 in every lesson; all criteria met. Completion basis: quiz-based mastery; implementation labs were not performed in this assessment.

## Weak points and review priorities

- L04: random forests reduce variance by aggregating less correlated trees. L06: increasing K in KNN usually lowers variance and increases bias. L10: distinguish prediction variance across training datasets from the bias of the average prediction relative to the truth.
- L07: DBSCAN supports density-connected curved clusters, unknown cluster counts, and noise. L11: distinguish AdaBoost reweighting, gradient boosting on negative gradients, and stacking with out-of-fold predictions.
- L09: fit each fold's scaler only on its training subset. L15: walk-forward validation trains before predicting the future evaluation interval to avoid temporal leakage.

## Lessons with mistakes and retake outcomes

Lessons with mistakes or retakes are listed below, along with any additional rows retained from the original ledger. Unlisted lessons scored 3/3 initially and finally. A final 3/3 indicates correction in a later assessment where applicable; retain those topics for spaced recall. Lessons at 2/3 remain review priorities.

| Lesson | Initial score | Final effective score / retake |
|---|---|---|
| [What Is Machine Learning](../../../phases/02-ml-fundamentals/01-what-is-machine-learning/docs/en.md) | attempt1: 3/3 | 3/3 |
| [Linear Regression](../../../phases/02-ml-fundamentals/02-linear-regression/docs/en.md) | attempt1: 3/3 | 3/3 |
| [Logistic Regression](../../../phases/02-ml-fundamentals/03-logistic-regression/docs/en.md) | attempt1: 3/3 | 3/3 |
| [Decision Trees and Random Forests](../../../phases/02-ml-fundamentals/04-decision-trees/docs/en.md) | attempt1: 2/3 | 2/3 |
| [Support Vector Machines](../../../phases/02-ml-fundamentals/05-support-vector-machines/docs/en.md) | attempt1: 3/3 | 3/3 |
| [K-Nearest Neighbors and Distances](../../../phases/02-ml-fundamentals/06-knn-and-distances/docs/en.md) | attempt1: 2/3 | 2/3 |
| [Unsupervised Learning](../../../phases/02-ml-fundamentals/07-unsupervised-learning/docs/en.md) | attempt1: 2/3 | 2/3 |
| [Feature Engineering & Selection](../../../phases/02-ml-fundamentals/08-feature-engineering/docs/en.md) | attempt1: 3/3 | 3/3 |
| [Model Evaluation](../../../phases/02-ml-fundamentals/09-model-evaluation/docs/en.md) | attempt1: 2/3 | 2/3 |
| [Bias-Variance Tradeoff](../../../phases/02-ml-fundamentals/10-bias-variance/docs/en.md) | attempt1: 2/3 | 2/3 |
| [Ensemble Methods](../../../phases/02-ml-fundamentals/11-ensemble-methods/docs/en.md) | attempt1: 2/3 | 2/3 |
| [Hyperparameter Tuning](../../../phases/02-ml-fundamentals/12-hyperparameter-tuning/docs/en.md) | attempt1: 3/3 | 3/3 |
| [ML Pipelines](../../../phases/02-ml-fundamentals/13-ml-pipelines/docs/en.md) | attempt1: 3/3 | 3/3 |
| [Naive Bayes](../../../phases/02-ml-fundamentals/14-naive-bayes/docs/en.md) | attempt1: 3/3 | 3/3 |
| [Time Series Fundamentals](../../../phases/02-ml-fundamentals/15-time-series/docs/en.md) | attempt1: 2/3 | 2/3 |
| [Anomaly Detection](../../../phases/02-ml-fundamentals/16-anomaly-detection/docs/en.md) | attempt1: 3/3 | 3/3 |
| [Handling Imbalanced Data](../../../phases/02-ml-fundamentals/17-imbalanced-data/docs/en.md) | attempt1: 3/3 | 3/3 |
| [Feature Selection](../../../phases/02-ml-fundamentals/18-feature-selection/docs/en.md) | attempt1: 3/3 | 3/3 |
| [ML System Design — From Problem to Deployed Model](../../../phases/02-ml-fundamentals/19-ml-system-design/docs/en.md) | attempt1: 3/3 | 3/3 |
| [Monitoring Models in Production — Data Drift and Concept Drift](../../../phases/02-ml-fundamentals/20-model-monitoring-and-drift/docs/en.md) | attempt1: 3/3 | 3/3 |
| [Feature Stores and Training-Serving Skew](../../../phases/02-ml-fundamentals/21-feature-stores-and-training-serving-skew/docs/en.md) | attempt1: 3/3 | 3/3 |

## Condensed mistake records

Question IDs, prompts, selected wrong answers, correct answers, and explanations are retained. Other distractors, correct-only questions, and per-response score logs are omitted. Prompts and explanations retain their original English wording. These are historical initial/retake mistakes, not pending retake requirements.

### p02-l04-concept-v1

Why do random forests combine bootstrap samples with random feature subsets at each split?

- Learner answer: A — To make all trees choose the same splits, reducing differences between predictions.
- Correct answer: C — To create diverse, less correlated trees whose aggregated predictions reduce variance.
- Explanation: Bootstrap samples and random feature subsets encourage different trees, reducing correlation among their errors. Aggregating diverse trees reduces variance; identical trees provide no averaging benefit.

### p02-l06-concept-v1

In unweighted KNN classification, what generally happens as K increases from 1 toward the full training-set size N?

- Learner answer: D — The neighbor search becomes approximate, typically making predictions random.
- Correct answer: B — Predictions become smoother, typically lowering variance while risking higher bias.
- Explanation: Increasing K aggregates more neighbors, smoothing predictions and typically reducing variance while potentially increasing bias. At K=N, unweighted classification predicts the training majority class everywhere (with fixed tie handling). K does not determine whether neighbor search is exact or approximate.

### p02-l07-application-v1

Your scaled 2D data contains two curved, dense bands of similar density, separated by a sparse gap, plus isolated outliers. You want clusters without specifying their number and want outliers left unassigned; which approach best fits?

- Learner answer: B — K-Means with K=2, assigning every point to its nearest centroid.
- Correct answer: A — DBSCAN with neighborhood radius and minimum sample count chosen for the density scale.
- Explanation: DBSCAN groups density-connected regions, supports curved clusters without a preset cluster count, and labels isolated noise points as unassigned. K-Means requires K, assigns every point, and partitions by nearest centroids, making it poorly suited to the requested curved bands and noise handling.

### p02-l09-application-v1

You compare KNN hyperparameters using cross-validation, and features require standardization. Which workflow avoids preprocessing leakage into validation folds?

- Learner answer: C — Within each fold, fit separate scalers on training and validation rows, using each split's own statistics.
- Correct answer: B — Within each fold, fit the scaler on that fold's training rows and apply it unchanged to its validation rows.
- Explanation: Fit the scaler using only each fold's training data, then reuse those exact statistics to transform validation data. Fitting a separate validation scaler adapts preprocessing to the held-out distribution and creates a different coordinate system from the one used to train KNN.

### p02-l10-concept-v1

At a fixed input x, you train the same algorithm on many independently sampled training datasets. What does the variance term in the squared-error decomposition measure?

- Learner answer: A — The squared difference between the average prediction and the true conditional mean.
- Correct answer: B — The spread of the model's predictions around their average across training datasets.
- Explanation: Variance measures how predictions at the same input change across sampled training datasets, relative to their average prediction. Option A describes squared bias, the gap between the average prediction and the true conditional mean; option C describes irreducible noise.

### p02-l11-concept-v1

Which statement correctly distinguishes AdaBoost from gradient boosting?

- Learner answer: C — AdaBoost learns a meta-model from out-of-fold predictions; gradient boosting votes on fixed class labels.
- Correct answer: D — AdaBoost reweights training examples; gradient boosting fits new learners to negative loss gradients.
- Explanation: AdaBoost reweights training examples to emphasize errors; gradient boosting fits each new learner to negative gradients of the current ensemble loss. A meta-learner trained on out-of-fold base predictions describes stacking, not AdaBoost.

### p02-l15-application-v1

You forecast tomorrow's sales using observations available by today's close. Recent behavior is more relevant than old regimes; which evaluation design best matches this deployment?

- Learner answer: D — Use an expanding window that includes each validation period before generating its predictions.
- Correct answer: B — Use a fixed-length historical training window, evaluate on the following period, and move both windows forward.
- Explanation: Sliding-window walk-forward validation trains on a fixed-length past window and evaluates on subsequent observations. It respects forecast-time availability while limiting old-regime influence. An expanding window can also be valid if strictly historical, but D explicitly includes the validation period before predicting it, causing leakage.
