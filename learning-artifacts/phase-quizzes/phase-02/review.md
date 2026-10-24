# Phase 02 review queue

Historical notes are preserved verbatim; some early remediation requests were superseded by later passes. Latest completion status is in [phase progress](progress.md).

- Phase02 Lesson15: walk-forward validation trains strictly before each evaluation period; including that period before predicting leaks future information. Fixed-length sliding windows limit outdated regimes. Q44 chose D; correct B.

- Phase02 Lesson11: AdaBoost reweights examples; gradient boosting fits negative loss gradients; stacking trains a meta-learner on out-of-fold base predictions. Q31 chose C; correct D.

- Phase02 Lesson10: variance is the spread of predictions across training datasets at fixed x; squared bias is the squared gap between their average and the true conditional mean. Q28 chose A; correct B.

- Phase02 Lesson09: fit a scaler only on each fold’s training rows, then reuse those statistics on validation. Separately fitting validation scaling changes coordinates and adapts to held-out data. Q26 chose C; correct B.

- Phase02 Lesson07: choose DBSCAN for density-connected curved clusters, unknown cluster count, and unassigned noise; K-Means requires K and assigns every point to a centroid. Q20 chose B; correct A.

- Phase02 Lesson06: increasing K smooths unweighted KNN predictions, usually lowering variance and risking higher bias; it does not make the search approximate. Q16 chose D; correct B.

- Phase02 Lesson04: random forests reduce variance by aggregating diverse, less correlated trees; bootstrap sampling and random feature subsets encourage diversity. Q10 chose A; correct C.
