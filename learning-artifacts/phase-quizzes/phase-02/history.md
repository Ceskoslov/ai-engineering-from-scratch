# Phase 02 detailed quiz history

Archive: read only when an earlier question or attempt is relevant. [Phase progress](progress.md).

### Phase02 resumed

Learner requested continuation. Phase00 and Phase01 remain done. Phase02 covers 21 lessons with 63 initial scored questions; passing requires at least 54/63 and at least 2/3 per lesson.

### Answer history: p02-l01-concept-v1

ID: p02-l01-concept-v1
Phase02 — ML Fundamentals; Lesson01 — What Is Machine Learning.
Question1/63; lesson question1/3; conceptual.

A model is trained to predict words hidden from otherwise unlabeled text, using the original words as targets. Which learning setup best describes this?

A) Semi-supervised learning using a small human-labeled subset
B) Reinforcement learning using rewards from an environment
C) Self-supervised learning using targets derived from the data
D) Unsupervised clustering using similarity without prediction targets


Learner answer: C. Correct answer: C. Result: correct.
Explanation: The original text supplies prediction targets automatically, making this self-supervised learning. No human-labeled subset or environmental reward is required.
Phase02 running initial score: 1/1. Lesson01 attempt1: 1/1; incomplete.

### Answer history: p02-l01-application-v1

ID: p02-l01-application-v1
Phase02 — ML Fundamentals; Lesson01 — What Is Machine Learning.
Question2/63; lesson question2/3; application.

You train several spam classifiers and choose their hyperparameters. Which use of the data splits gives the most credible final estimate of generalization?

A) Fit on training data, select settings on validation data, then evaluate once on untouched test data.
B) Fit on training data, select settings on test data, then report the best test result.
C) Fit on all three splits, select settings on validation data, then report test performance.
D) Fit on training data, select settings by training accuracy, then report that same accuracy.


Learner answer: A. Correct answer: A. Result: correct.
Explanation: Training fits parameters, validation supports model and hyperparameter selection, and the untouched test split estimates performance after those choices are finalized.
Phase02 running initial score: 2/2. Lesson01 attempt1: 2/2; incomplete.

### Answer history: p02-l01-code-v1

ID: p02-l01-code-v1
Phase02 — ML Fundamentals; Lesson01 — What Is Machine Learning.
Question3/63; lesson question3/3; code tracing.

The following classifier uses Euclidean distance to each class centroid. What does it predict for the test point?

```python
X_train = np.array([[0., 0.], [2., 0.], [4., 2.], [4., 4.]])
y_train = np.array([10, 10, 20, 20])
model = NearestCentroid()
model.fit(X_train, y_train)
print(model.predict(np.array([[3., 2.]])))
```

A) [10], because the first class has the smaller centroid coordinates.
B) [1], because prediction returns the nearest centroid's array index.
C) [20], because the test point itself becomes the second class centroid.
D) [20], because its distance to centroid [4, 3] is smaller than to [1, 0].


Learner answer: D. Correct answer: D. Result: correct.
Explanation: Class10 centroid is [1, 0], and class20 centroid is [4, 3]. From [3, 2], their squared distances are 8 and 2 respectively; predict returns label20, not index1.
Phase02 running initial score: 3/3. Lesson01 attempt1 complete: 3/3. Lesson01 remains todo until the full phase passes.

### Answer history: p02-l02-concept-v1

ID: p02-l02-concept-v1
Phase02 — ML Fundamentals; Lesson02 — Linear Regression.
Question4/63; lesson question1/3; conceptual.

Why is the model y_hat = b + w1*x + w2*x**2 still considered linear regression?

A) Squared error makes every prediction a straight line in x.
B) It is linear in the learned coefficients, despite nonlinear features of x.
C) The squared feature is treated as constant while fitting the weights.
D) Gradient descent converts the quadratic term into a linear feature of x.


Learner answer: B. Correct answer: B. Result: correct.
Explanation: Linear regression is linear in its learned coefficients. Using x and x**2 as fixed input features permits a curved relationship with x without changing that property.
Phase02 running initial score: 4/4. Lesson02 attempt1: 1/1; incomplete.

### Answer history: p02-l02-application-v1

ID: p02-l02-application-v1
Phase02 — ML Fundamentals; Lesson02 — Linear Regression.
Question5/63; lesson question2/3; application.

A standardized multiple linear regression model has much lower training MSE than validation MSE. You add a Ridge penalty, lambda * sum(w_j**2); which approach best addresses this overfitting?

A) Increase lambda until training MSE reaches its minimum, then keep that setting.
B) Increase lambda to guarantee lower validation MSE and zero out unused weights.
C) Tune lambda on validation data; the penalty discourages large weights but excessive regularization can underfit.
D) Tune lambda on test data; the penalty removes the need for a separate validation set.


Learner answer: C. Correct answer: C. Result: correct.
Explanation: Ridge penalizes large coefficients and can reduce overfitting. Select lambda using validation performance; too much regularization can underfit. It neither guarantees improved validation error nor generally produces exact zero coefficients.
Phase02 running initial score: 5/5. Lesson02 attempt1: 2/2; incomplete.

### Answer history: p02-l02-code-v1

ID: p02-l02-code-v1
Phase02 — ML Fundamentals; Lesson02 — Linear Regression.
Question6/63; lesson question3/3; code tracing.

Using MSE = mean((prediction - target)**2), what are w and b after this single batch gradient descent update?

```python
X = [1.0, 2.0]
y = [2.0, 4.0]
w, b = 0.0, 0.0
lr = 0.1
errors = [w * x + b - target for x, target in zip(X, y)]
dw = (2 / len(y)) * sum(e * x for e, x in zip(errors, X))
db = (2 / len(y)) * sum(errors)
w -= lr * dw
b -= lr * db
```

A) w = 1.0, b = 0.6
B) w = 0.5, b = 0.3
C) w = -1.0, b = -0.6
D) w = 1.0, b = 0.3


Learner first entered W (invalid option; not scored), then answered A. Correct answer: A. Result: correct.
Explanation: The errors are [-2, -4], so dw = -10 and db = -6. Subtracting 0.1 times each gradient gives w = 1.0 and b = 0.6.
Phase02 running initial score: 6/6. Lesson02 attempt1 complete: 3/3. Lessons remain todo until the full phase passes.

### Answer history: p02-l03-concept-v1

ID: p02-l03-concept-v1
Phase02 — ML Fundamentals; Lesson03 — Logistic Regression.
Question7/63; lesson question1/3; conceptual.

For binary logistic regression with p = sigmoid(w dot x + b), why is binary cross-entropy a standard training objective?

A) It makes the predicted probability equal to the class label after every update.
B) It converts the linear score into a probability without requiring a sigmoid.
C) It optimizes classification accuracy directly while ignoring probability confidence.
D) It is the Bernoulli negative log-likelihood and penalizes confident wrong predictions strongly.


Learner answer: D. Correct answer: D. Result: correct.
Explanation: Binary cross-entropy is the negative log-likelihood for Bernoulli outcomes. Assigning a very low probability to the actual outcome incurs a large loss.
Phase02 running initial score: 7/7. Lesson03 attempt1: 1/1; incomplete.

### Answer history: p02-l03-application-v1

ID: p02-l03-application-v1
Phase02 — ML Fundamentals; Lesson03 — Logistic Regression.
Question8/63; lesson question2/3; application.

A spam filter predicts spam when p >= threshold. Blocking legitimate emails is especially costly; with predicted probabilities fixed, what happens if you raise the threshold from 0.5 to 0.8?

A) More emails are flagged; false positives cannot increase, and recall cannot decrease.
B) Fewer or equal emails are flagged; false positives cannot increase, but recall may decrease.
C) Fewer or equal emails are flagged; precision must increase, and recall stays unchanged.
D) The model learns new weights; both false positives and false negatives must decrease.


Learner answer: B. Correct answer: B. Result: correct.
Explanation: With fixed probabilities, raising the threshold selects a subset of the original positive predictions. False positives cannot increase, while true positives and recall can decrease. Precision need not improve on every finite dataset.
Phase02 running initial score: 8/8. Lesson03 attempt1: 2/2; incomplete.

### Answer history: p02-l03-code-v1

ID: p02-l03-code-v1
Phase02 — ML Fundamentals; Lesson03 — Logistic Regression.
Question9/63; lesson question3/3; code tracing.

What does this code print for precision, recall, and F1, rounded to three decimal places?

```python
y_true = [1, 0, 1, 0, 1]
probs = [0.9, 0.8, 0.7, 0.2, 0.4]
y_pred = [int(p >= 0.5) for p in probs]
tp = sum(t == 1 and p == 1 for t, p in zip(y_true, y_pred))
fp = sum(t == 0 and p == 1 for t, p in zip(y_true, y_pred))
fn = sum(t == 1 and p == 0 for t, p in zip(y_true, y_pred))
precision = tp / (tp + fp)
recall = tp / (tp + fn)
f1 = 2 * precision * recall / (precision + recall)
print(round(precision, 3), round(recall, 3), round(f1, 3))
```

A) 0.667 0.667 0.667
B) 0.667 1.0 0.8
C) 1.0 0.667 0.8
D) 0.6 0.6 0.6


Learner answer: A. Correct answer: A. Result: correct.
Explanation: Predictions are [1, 1, 1, 0, 0]. TP=2, FP=1, FN=1, so precision, recall, and F1 all equal 2/3, rounded to 0.667.
Phase02 running initial score: 9/9. Lesson03 attempt1 complete: 3/3. Lessons remain todo until the full phase passes.

### Answer history: p02-l04-concept-v1

ID: p02-l04-concept-v1
Phase02 — ML Fundamentals; Lesson04 — Decision Trees and Random Forests.
Question10/63; lesson question1/3; conceptual.

Why do random forests combine bootstrap samples with random feature subsets at each split?

A) To make all trees choose the same splits, reducing differences between predictions.
B) To remove each sampled row from the training data before building the next tree.
C) To create diverse, less correlated trees whose aggregated predictions reduce variance.
D) To force each individual tree to have a linear decision boundary with low variance.


Learner answer: A. Correct answer: C. Result: incorrect.
Explanation: Bootstrap samples and random feature subsets encourage different trees, reducing correlation among their errors. Aggregating diverse trees reduces variance; identical trees provide no averaging benefit.
Review: Lesson04 — random forest diversity, error correlation, and variance reduction.
Phase02 running initial score: 9/10. Lesson04 attempt1: 0/1; incomplete.

### Answer history: p02-l04-application-v1

ID: p02-l04-application-v1
Phase02 — ML Fundamentals; Lesson04 — Decision Trees and Random Forests.
Question11/63; lesson question2/3; application.

A random forest assigns high impurity-based importance (MDI) to a random ID column with many unique values. What is the best next step to assess whether the model benefits from this feature on unseen data?

A) Treat the high MDI score as proof that the ID generalizes well.
B) Shuffle the ID column in held-out validation data and measure the performance change.
C) Replace the ID with a new unique random ID and check training accuracy only.
D) Count how often the ID is used in training splits and ignore validation performance.


Learner answer: B. Correct answer: B. Result: correct.
Explanation: MDI can favor high-cardinality features because they offer many possible splits. Permutation importance on held-out validation data measures the performance change when the fitted model can no longer use the feature's original associations.
Phase02 running initial score: 10/11. Lesson04 attempt1: 1/2; incomplete.

### Answer history: p02-l04-code-v1

ID: p02-l04-code-v1
Phase02 — ML Fundamentals; Lesson04 — Decision Trees and Random Forests.
Question12/63; lesson question3/3; code tracing.

Using the lesson's Gini criterion, what does this code print?

```python
parent = [0, 0, 0, 0, 1, 1, 1, 1]
left = [0, 0]
right = [0, 0, 1, 1, 1, 1]

def gini(labels):
    return 1 - sum((labels.count(c) / len(labels))**2
                   for c in set(labels))

gain = gini(parent) - (
    len(left) / len(parent) * gini(left)
    + len(right) / len(parent) * gini(right)
)
print(round(gain, 3))
```

A) 0.278
B) 0.444
C) 0.333
D) 0.167


Learner answer: D. Correct answer: D. Result: correct.
Explanation: Parent Gini is 1/2, left Gini is 0, and right Gini is 4/9. Weighted child impurity is (2/8)*0 + (6/8)*(4/9) = 1/3. Gain is 1/2 - 1/3 = 1/6, rounded to 0.167.
Phase02 running initial score: 11/12. Lesson04 attempt1 complete: 2/3, meeting the lesson minimum. Lessons remain todo until the full phase passes. Random forest diversity remains in the review queue.

### Answer history: p02-l05-concept-v1

ID: p02-l05-concept-v1
Phase02 — ML Fundamentals; Lesson05 — Support Vector Machines.
Question13/63; lesson question1/3; conceptual.

What does the kernel trick allow an SVM to do?

A) Compute inner products in a transformed feature space without explicitly constructing the transformed vectors.
B) Find a nonlinear boundary by fitting a separate linear classifier to every training point.
C) Replace margin optimization with nearest-neighbor voting over the original input features.
D) Guarantee perfect classification by mapping all inputs to the same feature vector.


Learner answer: A. Correct answer: A. Result: correct.
Explanation: A kernel evaluates inner products between implicit feature mappings, allowing nonlinear decision boundaries in input space without explicitly constructing those feature vectors.
Phase02 running initial score: 12/13. Lesson05 attempt1: 1/1; incomplete.

### Answer history: p02-l05-application-v1

ID: p02-l05-application-v1
Phase02 — ML Fundamentals; Lesson05 — Support Vector Machines.
Question14/63; lesson question2/3; application.

A soft-margin SVM minimizes 0.5 * ||w||**2 + C * sum(hinge_losses). On noisy data it fits training points closely but generalizes poorly; which change is reasonable to try, with other settings fixed?

A) Increase C to reduce the penalty for margin violations.
B) Decrease C to require every training point to lie outside the margin.
C) Decrease C to reduce the penalty for margin violations relative to the weight penalty.
D) Increase C to strengthen regularization on w relative to the hinge losses.


Learner answer: C. Correct answer: C. Result: correct.
Explanation: Decreasing C reduces the relative cost of hinge-loss violations, increasing the relative influence of the weight penalty. This can reduce sensitivity to noisy training points; choose C using validation performance.
Phase02 running initial score: 13/14. Lesson05 attempt1: 2/2; incomplete.

### Answer history: p02-l05-code-v1

ID: p02-l05-code-v1
Phase02 — ML Fundamentals; Lesson05 — Support Vector Machines.
Question15/63; lesson question3/3; code tracing.

For this single-example SVM update, what are w and b afterward?

```python
w, b = 0.5, 0.0
x, y = 1.0, 1
lr, lam = 0.1, 0.2
margin = y * (w * x + b)
if margin >= 1:
    w -= lr * lam * w
else:
    w -= lr * (lam * w - y * x)
    b -= lr * (-y)
print(round(w, 2), round(b, 2))
```

A) 0.49 0.0
B) 0.59 0.1
C) 0.41 -0.1
D) 0.6 0.1


Learner answer: B. Correct answer: B. Result: correct.
Explanation: The margin is 0.5, so the hinge-loss branch is active. The weight gradient is 0.2*0.5 - 1*1 = -0.9, yielding w=0.59; the bias gradient is -1, yielding b=0.1.
Phase02 running initial score: 14/15. Lesson05 attempt1 complete: 3/3. Lessons remain todo until the full phase passes.

### Answer history: p02-l06-concept-v1

ID: p02-l06-concept-v1
Phase02 — ML Fundamentals; Lesson06 — K-Nearest Neighbors and Distances.
Question16/63; lesson question1/3; conceptual.

In unweighted KNN classification, what generally happens as K increases from 1 toward the full training-set size N?

A) Predictions become more sensitive to individual points, typically increasing variance.
B) Predictions become smoother, typically lowering variance while risking higher bias.
C) The model learns more coefficients, typically reducing both bias and variance.
D) The neighbor search becomes approximate, typically making predictions random.


Learner answer: D. Correct answer: B. Result: incorrect.
Explanation: Increasing K aggregates more neighbors, smoothing predictions and typically reducing variance while potentially increasing bias. At K=N, unweighted classification predicts the training majority class everywhere (with fixed tie handling). K does not determine whether neighbor search is exact or approximate.
Review: Lesson06 — K controls prediction smoothing and the bias–variance tradeoff, not search approximation.
Phase02 running initial score: 14/16. Lesson06 attempt1: 0/1; incomplete.

### Answer history: p02-l06-application-v1

ID: p02-l06-application-v1
Phase02 — ML Fundamentals; Lesson06 — K-Nearest Neighbors and Distances.
Question17/63; lesson question2/3; application.

You retrieve text embeddings where vector direction captures similarity, while vector magnitude should be ignored. Which distance best matches that requirement for nonzero vectors?

A) Euclidean distance on the original, unnormalized vectors.
B) Manhattan distance on the original, unnormalized vectors.
C) Cosine distance, computed as 1 - dot(a,b)/(norm(a)*norm(b)).
D) Absolute difference between the two vector norms.


Learner answer: C. Correct answer: C. Result: correct.
Explanation: Cosine distance compares vector directions by dividing the dot product by both norms. Positive rescaling of either nonzero vector leaves the distance unchanged.
Phase02 running initial score: 15/17. Lesson06 attempt1: 1/2; incomplete.

### Answer history: p02-l06-code-v1

ID: p02-l06-code-v1
Phase02 — ML Fundamentals; Lesson06 — K-Nearest Neighbors and Distances.
Question18/63; lesson question3/3; code tracing.

These are the three nearest neighbors of a regression query. What does this inverse-distance-weighted prediction print? All distances are positive, so no epsilon is needed here.

```python
distances = [1.0, 2.0, 4.0]
targets = [10.0, 20.0, 40.0]
weights = [1 / d for d in distances]
pred = sum(w * y for w, y in zip(weights, targets)) / sum(weights)
print(round(pred, 2))
```

A) 23.33
B) 30.0
C) 10.0
D) 17.14


Learner answer: D. Correct answer: D. Result: correct.
Explanation: The weights are [1, 0.5, 0.25]. The weighted target sum is 30 and the weight sum is 1.75, giving 30/1.75 = 17.142857..., rounded to 17.14.
Phase02 running initial score: 16/18. Lesson06 attempt1 complete: 2/3, meeting the lesson minimum. Lessons remain todo until the full phase passes. KNN bias–variance tradeoff remains in the review queue.

### Answer history: p02-l07-concept-v1

ID: p02-l07-concept-v1
Phase02 — ML Fundamentals; Lesson07 — Unsupervised Learning.
Question19/63; lesson question1/3; conceptual.

In a Gaussian Mixture Model trained with Expectation-Maximization, which description correctly matches the two steps?

A) E-step assigns every point permanently to one component; M-step chooses the number of components.
B) E-step updates component means; M-step computes the distances used to initialize the model.
C) E-step computes component-membership probabilities; M-step updates parameters using those responsibilities.
D) E-step removes low-density points; M-step joins the remaining points into density-connected clusters.


Learner answer: C. Correct answer: C. Result: correct.
Explanation: The E-step computes posterior component-membership probabilities (responsibilities). The M-step uses them to update component means, covariances, and mixing weights.
Phase02 running initial score: 17/19. Lesson07 attempt1: 1/1; incomplete.

### Answer history: p02-l07-application-v1

ID: p02-l07-application-v1
Phase02 — ML Fundamentals; Lesson07 — Unsupervised Learning.
Question20/63; lesson question2/3; application.

Your scaled 2D data contains two curved, dense bands of similar density, separated by a sparse gap, plus isolated outliers. You want clusters without specifying their number and want outliers left unassigned; which approach best fits?

A) DBSCAN with neighborhood radius and minimum sample count chosen for the density scale.
B) K-Means with K=2, assigning every point to its nearest centroid.
C) A two-component GMM, assigning every point to its most probable component.
D) Agglomerative clustering cut into two groups, assigning every point to a group.


Learner answer: B. Correct answer: A. Result: incorrect.
Explanation: DBSCAN groups density-connected regions, supports curved clusters without a preset cluster count, and labels isolated noise points as unassigned. K-Means requires K, assigns every point, and partitions by nearest centroids, making it poorly suited to the requested curved bands and noise handling.
Review: Lesson07 — DBSCAN versus K-Means: density connectivity, arbitrary shapes, unknown cluster count, and noise labels.
Phase02 running initial score: 17/20. Lesson07 attempt1: 1/2; incomplete.

### Answer history: p02-l07-code-v1

ID: p02-l07-code-v1
Phase02 — ML Fundamentals; Lesson07 — Unsupervised Learning.
Question21/63; lesson question3/3; code tracing.

For these one-dimensional points, what centroids and inertia result after one K-Means assignment/update cycle? No point is tied between centroids.

```python
points = [0.0, 2.0, 8.0, 10.0]
centroids = [0.0, 8.0]
labels = [min(range(2), key=lambda j: (x - centroids[j])**2)
          for x in points]
new_centroids = [sum(x for x, c in zip(points, labels) if c == j)
                 / labels.count(j) for j in range(2)]
inertia = sum((x - new_centroids[c])**2
              for x, c in zip(points, labels))
print(new_centroids, inertia)
```

A) [0.0, 8.0], 8.0
B) [1.0, 9.0], 2.0
C) [1.0, 9.0], 4.0
D) [5.0, 5.0], 68.0


Learner answer: C. Correct answer: C. Result: correct.
Explanation: Assignments are [0, 0, 1, 1], so the updated centroids are [1, 9]. Each of the four points has squared distance1 from its centroid, giving inertia4.
Phase02 running initial score: 18/21. Lesson07 attempt1 complete: 2/3, meeting the lesson minimum. Lessons remain todo until the full phase passes. DBSCAN method selection remains in the review queue.

### Answer history: p02-l08-concept-v1

ID: p02-l08-concept-v1
Phase02 — ML Fundamentals; Lesson08 — Feature Engineering & Selection.
Question22/63; lesson question1/3; conceptual.

You encode a nominal color feature as red=0, blue=1, green=2 before using a linear model. What is the main concern compared with one-hot encoding?

A) Integer encoding prevents the model from learning any coefficient for color.
B) It imposes an artificial numeric ordering and spacing between unrelated categories.
C) One-hot encoding requires the categories to have a meaningful numerical order.
D) Integer encoding always creates more feature columns than one-hot encoding.


Learner answer: B. Correct answer: B. Result: correct.
Explanation: A single numeric code imposes an arbitrary ordering and spacing. A linear model treats those codes as a numeric feature; one-hot encoding allows separate category effects without that imposed relationship.
Phase02 running initial score: 19/22. Lesson08 attempt1: 1/1; incomplete.

### Answer history: p02-l08-application-v1

ID: p02-l08-application-v1
Phase02 — ML Fundamentals; Lesson08 — Feature Engineering & Selection.
Question23/63; lesson question2/3; application.

You evaluate a classifier that target-encodes a high-cardinality category using its mean label. Which workflow best avoids leaking labels into features?

A) Compute category means from all labels, then split the encoded data into training and validation.
B) Split first, but encode each validation category using its own validation labels.
C) Compute means from all labels, then add smoothing so validation labels cannot leak.
D) Split first; use out-of-fold training encodings, then encode validation with training-only category statistics.


Learner answer: D. Correct answer: D. Result: correct.
Explanation: Out-of-fold encoding computes each training row's category statistic without using labels from its own fold. Validation encodings use training-only statistics, keeping validation labels out of preprocessing. Smoothing alone does not prevent leakage.
Phase02 running initial score: 20/23. Lesson08 attempt1: 2/2; incomplete.

### Answer history: p02-l08-code-v1

ID: p02-l08-code-v1
Phase02 — ML Fundamentals; Lesson08 — Feature Engineering & Selection.
Question24/63; lesson question3/3; code tracing.

Using the lesson's unsmoothed TF-IDF formula, what does this code print for the first document?

```python
import math

docs = ["cat cat dog", "dog bird"]
words = docs[0].split()

def weight(term):
    tf = words.count(term) / len(words)
    df = sum(term in doc.split() for doc in docs)
    return tf * math.log(len(docs) / df)

print(round(weight("cat"), 3), round(weight("dog"), 3))
```

A) 0.462 0.0
B) 0.693 0.0
C) 0.462 0.231
D) 0.667 0.333


Learner answer: A. Correct answer: A. Result: correct.
Explanation: Cat has TF=2/3 and IDF=ln(2/1), giving approximately0.462. Dog appears in both documents, so its IDF=ln(2/2)=0 and its weight is0.
Phase02 running initial score: 21/24. Lesson08 attempt1 complete: 3/3. Lessons remain todo until the full phase passes.

### Answer history: p02-l09-concept-v1

ID: p02-l09-concept-v1
Phase02 — ML Fundamentals; Lesson09 — Model Evaluation.
Question25/63; lesson question1/3; conceptual.

For independent classification examples with a rare positive class and enough positives for all folds, why prefer stratified K-fold over ordinary shuffled K-fold?

A) It ensures every fold has equal numbers of positive and negative examples.
B) It prevents overfitting by keeping every positive example out of training.
C) It approximately preserves class proportions in each fold, reducing unstable minority-class evaluation.
D) It selects the best classification threshold without using validation labels.


Learner answer: C. Correct answer: C. Result: correct.
Explanation: Stratification approximately preserves the original class proportions, helping avoid folds with too few minority examples. It does not balance the classes to 50/50 or exclude positives from training.
Phase02 running initial score: 22/25. Lesson09 attempt1: 1/1; incomplete.

### Answer history: p02-l09-application-v1

ID: p02-l09-application-v1
Phase02 — ML Fundamentals; Lesson09 — Model Evaluation.
Question26/63; lesson question2/3; application.

You compare KNN hyperparameters using cross-validation, and features require standardization. Which workflow avoids preprocessing leakage into validation folds?

A) Fit the scaler on all available rows once, then cross-validate KNN on the scaled rows.
B) Within each fold, fit the scaler on that fold's training rows and apply it unchanged to its validation rows.
C) Within each fold, fit separate scalers on training and validation rows, using each split's own statistics.
D) Fit the scaler on the final test rows once, then use those statistics throughout cross-validation.


Learner answer: C. Correct answer: B. Result: incorrect.
Explanation: Fit the scaler using only each fold's training data, then reuse those exact statistics to transform validation data. Fitting a separate validation scaler adapts preprocessing to the held-out distribution and creates a different coordinate system from the one used to train KNN.
Review: Lesson09 — fit preprocessing on fold-training rows only; transform held-out rows using the same fitted transform.
Phase02 running initial score: 22/26. Lesson09 attempt1: 1/2; incomplete.

### Answer history: p02-l09-code-v1

ID: p02-l09-code-v1
Phase02 — ML Fundamentals; Lesson09 — Model Evaluation.
Question27/63; lesson question3/3; code tracing.

What does this code print for MSE, MAE, and R-squared?

```python
y_true = [1.0, 3.0]
y_pred = [0.0, 0.0]
n = len(y_true)
mse = sum((t - p)**2 for t, p in zip(y_true, y_pred)) / n
mae = sum(abs(t - p) for t, p in zip(y_true, y_pred)) / n
mean_y = sum(y_true) / n
ss_tot = sum((t - mean_y)**2 for t in y_true)
r2 = 1 - n * mse / ss_tot
print(mse, mae, r2)
```

A) 5.0 2.0 0.0
B) 2.0 5.0 -4.0
C) 5.0 2.0 0.2
D) 5.0 2.0 -4.0


Learner answer: D. Correct answer: D. Result: correct.
Explanation: Squared residuals sum to10, so MSE=5; absolute residuals sum to4, so MAE=2. The target mean is2 and SS_tot=2, so R-squared=1-10/2=-4. Negative R-squared means worse squared error than the evaluation-target mean baseline.
Phase02 running initial score: 23/27. Lesson09 attempt1 complete: 2/3, meeting the lesson minimum. Lessons remain todo until the full phase passes. Fold-specific preprocessing remains in the review queue.

### Answer history: p02-l10-concept-v1

ID: p02-l10-concept-v1
Phase02 — ML Fundamentals; Lesson10 — Bias-Variance Tradeoff.
Question28/63; lesson question1/3; conceptual.

At a fixed input x, you train the same algorithm on many independently sampled training datasets. What does the variance term in the squared-error decomposition measure?

A) The squared difference between the average prediction and the true conditional mean.
B) The spread of the model's predictions around their average across training datasets.
C) The randomness in new target observations even when the true conditional mean is known.
D) The average squared difference between training features and their feature means.


Learner answer: A. Correct answer: B. Result: incorrect.
Explanation: Variance measures how predictions at the same input change across sampled training datasets, relative to their average prediction. Option A describes squared bias, the gap between the average prediction and the true conditional mean; option C describes irreducible noise.
Review: Lesson10 — distinguish prediction variance across datasets from squared bias of their average and irreducible target noise.
Phase02 running initial score: 23/28. Lesson10 attempt1: 0/1; incomplete.

### Answer history: p02-l10-application-v1

ID: p02-l10-application-v1
Phase02 — ML Fundamentals; Lesson10 — Bias-Variance Tradeoff.
Question29/63; lesson question2/3; application.

A well-optimized linear model has high training and validation error, with a small gap; both errors plateau as more data is added. Which next experiment best addresses the likely problem?

A) Increase regularization strongly to make the model less flexible.
B) Keep the model and features fixed and only collect more similar data.
C) Stop training much earlier to prevent fitting the training examples.
D) Add useful nonlinear features or try a more flexible model, selecting with validation.


Learner answer: D. Correct answer: D. Result: correct.
Explanation: High, plateaued training and validation errors with a small gap suggest underfitting (high bias). Useful nonlinear features or increased model flexibility can address the limitation; use validation to choose among candidates.
Phase02 running initial score: 24/29. Lesson10 attempt1: 1/2; incomplete.

### Answer history: p02-l10-code-v1

ID: p02-l10-code-v1
Phase02 — ML Fundamentals; Lesson10 — Bias-Variance Tradeoff.
Question30/63; lesson question3/3; code tracing.

Treat these predictions at a fixed input as equally likely across training datasets. What does this code print for squared bias, variance, and expected squared error against a fresh target with independent zero-mean noise of variance1?

```python
predictions = [2.0, 4.0, 6.0]
f_true = 3.0
noise_variance = 1.0
mean_pred = sum(predictions) / len(predictions)
bias_sq = (mean_pred - f_true)**2
variance = sum((p - mean_pred)**2 for p in predictions) / len(predictions)
expected_error = bias_sq + variance + noise_variance
print(round(bias_sq, 3), round(variance, 3), round(expected_error, 3))
```

A) 1.0 2.667 4.667
B) 1.0 4.0 6.0
C) 1.0 2.667 3.667
D) 0.0 2.667 3.667


Learner answer: A. Correct answer: A. Result: correct.
Explanation: Mean prediction=4, squared bias=(4-3)**2=1, and variance=(4+0+4)/3=8/3. Including independent target noise of variance1 gives expected squared error=14/3, approximately4.667.
Phase02 running initial score: 25/30. Lesson10 attempt1 complete: 2/3, meeting the lesson minimum. Lessons remain todo until the full phase passes. Bias versus variance definitions remain in the review queue.

### Answer history: p02-l11-concept-v1

ID: p02-l11-concept-v1
Phase02 — ML Fundamentals; Lesson11 — Ensemble Methods.
Question31/63; lesson question1/3; conceptual.

Which statement correctly distinguishes AdaBoost from gradient boosting?

A) AdaBoost trains independent models on bootstrap samples; gradient boosting averages independently trained models.
B) AdaBoost fits residuals for every loss; gradient boosting only increases weights on misclassified examples.
C) AdaBoost learns a meta-model from out-of-fold predictions; gradient boosting votes on fixed class labels.
D) AdaBoost reweights training examples; gradient boosting fits new learners to negative loss gradients.


Learner answer: c (normalized C). Correct answer: D. Result: incorrect.
Explanation: AdaBoost reweights training examples to emphasize errors; gradient boosting fits each new learner to negative gradients of the current ensemble loss. A meta-learner trained on out-of-fold base predictions describes stacking, not AdaBoost.
Review: Lesson11 — distinguish AdaBoost sample reweighting, gradient boosting negative-gradient fitting, and stacking meta-learning.
Phase02 running initial score: 25/31. Lesson11 attempt1: 0/1; incomplete.

### Answer history: p02-l11-application-v1

ID: p02-l11-application-v1
Phase02 — ML Fundamentals; Lesson11 — Ensemble Methods.
Question32/63; lesson question2/3; application.

You build a stacking ensemble with a meta-learner trained on base-model predictions. How should you generate those predictions for the meta-learner's training rows?

A) Fit each base model on all training rows and predict those same rows.
B) Use out-of-fold predictions, so each row is predicted by base models trained without its fold.
C) Fit each base model on test labels and predict the training rows.
D) Replace each base model's prediction with the row's true target label.


Learner answer: B. Correct answer: B. Result: correct.
Explanation: Out-of-fold predictions ensure each meta-training row is scored by base models that were not fitted on that row's fold, avoiding in-sample predictions that can make base performance appear misleadingly strong.
Phase02 running initial score: 26/32. Lesson11 attempt1: 1/2; incomplete.

### Answer history: p02-l11-code-v1

ID: p02-l11-code-v1
Phase02 — ML Fundamentals; Lesson11 — Ensemble Methods.
Question33/63; lesson question3/3; code tracing.

In this squared-error gradient-boosting round, assume the new tree predicts the residuals exactly. What does the code print?

```python
y = [2.0, 6.0]
current = [4.0, 4.0]
residuals = [target - pred for target, pred in zip(y, current)]
tree_output = residuals[:]
lr = 0.25
updated = [pred + lr * delta for pred, delta in zip(current, tree_output)]
print(updated)
```

A) [2.0, 6.0]
B) [4.5, 3.5]
C) [3.5, 4.5]
D) [-0.5, 0.5]


Learner answer: C. Correct answer: C. Result: correct.
Explanation: Residuals are [-2, 2]. Adding one quarter of the tree outputs to [4, 4] gives [3.5, 4.5]. Shrinkage limits the contribution of the new learner.
Phase02 running initial score: 27/33. Lesson11 attempt1 complete: 2/3, meeting the lesson minimum. Lessons remain todo until the full phase passes. Boosting versus stacking remains in the review queue.

### Answer history: p02-l12-concept-v1

ID: p02-l12-concept-v1
Phase02 — ML Fundamentals; Lesson12 — Hyperparameter Tuning.
Question34/63; lesson question1/3; conceptual.

In Bayesian hyperparameter optimization, what is the role of the acquisition function?

A) Compute the training gradients used to update the candidate model's weights.
B) Replace validation scores with test scores when the search budget is small.
C) Rank candidate settings using surrogate predictions and uncertainty to choose the next evaluation.
D) Enumerate every combination in a fixed grid before fitting the surrogate model.


Learner answer: C. Correct answer: C. Result: correct.
Explanation: The acquisition function uses the surrogate's predicted objective and uncertainty to choose the next expensive evaluation, balancing exploration and exploitation.
Phase02 running initial score: 28/34. Lesson12 attempt1: 1/1; incomplete.

### Answer history: p02-l12-application-v1

ID: p02-l12-application-v1
Phase02 — ML Fundamentals; Lesson12 — Hyperparameter Tuning.
Question35/63; lesson question2/3; application.

After searching hundreds of hyperparameter settings, you want to estimate the generalization of the entire tuning procedure using nested cross-validation. Which design is correct?

A) Tune settings using all rows, then run outer cross-validation with those fixed settings.
B) Tune settings within each outer training fold using inner CV, then evaluate on that untouched outer test fold.
C) Choose settings using each outer test fold, then report their scores on those same folds.
D) Report the best inner CV score from every search, without evaluating outer test folds.


Learner answer: B. Correct answer: B. Result: correct.
Explanation: Each outer training fold runs its own inner hyperparameter search. The chosen model is evaluated on the outer fold excluded from that search, so outer scores assess the tuning procedure on held-out data.
Phase02 running initial score: 29/35. Lesson12 attempt1: 2/2; incomplete.

### Answer history: p02-l12-code-v1

ID: p02-l12-code-v1
Phase02 — ML Fundamentals; Lesson12 — Hyperparameter Tuning.
Question36/63; lesson question3/3; code tracing.

This grid search maximizes negative validation MSE. Which learning rate is selected, and how many candidate configurations are evaluated?

```python
from itertools import product

best_score = -float("inf")
best_lr = None
n_evals = 0
for lr, depth in product([0.01, 0.1], [2, 4, 6]):
    mse = (lr - 0.1)**2 + (depth - 4)**2
    score = -mse
    n_evals += 1
    if score > best_score:
        best_score = score
        best_lr = lr
print(best_lr, n_evals)
```

A) 0.01 6
B) 0.1 5
C) 0.01 2
D) 0.1 6


Learner answer: D. Correct answer: D. Result: correct.
Explanation: The Cartesian product evaluates2*3=6 configurations. MSE is minimized at lr=0.1 and depth=4, where negative MSE reaches its maximum0.
Phase02 running initial score: 30/36. Lesson12 attempt1 complete: 3/3. Lessons remain todo until the full phase passes.

### Answer history: p02-l13-concept-v1

ID: p02-l13-concept-v1
Phase02 — ML Fundamentals; Lesson13 — ML Pipelines.
Question37/63; lesson question1/3; conceptual.

A fitted pipeline contains an imputer, a scaler, and a classifier. What should happen when it predicts on a new batch?

A) Refit the imputer and scaler on the new batch, then use the existing classifier.
B) Refit only the scaler so the new batch has zero mean and unit variance.
C) Transform using the stored imputation and scaling statistics, then call the fitted classifier.
D) Skip preprocessing because the classifier already saw transformed data during training.


Learner answer: C. Correct answer: C. Result: correct.
Explanation: Prediction reuses the preprocessing statistics learned during training and passes transformed data to the fitted classifier. Refitting on a new batch changes the representation and makes predictions depend on batch composition.
Phase02 running initial score: 31/37. Lesson13 attempt1: 1/1; incomplete.

### Answer history: p02-l13-application-v1

ID: p02-l13-application-v1
Phase02 — ML Fundamentals; Lesson13 — ML Pipelines.
Question38/63; lesson question2/3; application.

Your model works in a notebook, but serving code recreates preprocessing separately and predictions differ. Which deployment approach most directly reduces this training/serving skew?

A) Serialize the full fitted preprocessing-and-model pipeline; load it in serving and verify prediction parity on fixed examples.
B) Serialize only classifier weights; recompute preprocessing statistics from each incoming batch.
C) Copy preprocessing into a second implementation; update its category order whenever new values arrive.
D) Remove preprocessing in serving; rely on the classifier to compensate for raw feature scales.


Learner answer: A. Correct answer: A. Result: correct.
Explanation: Shipping the full fitted pipeline preserves transformation order, learned statistics, category mappings, and classifier parameters together. Fixed-example parity checks verify that loading and serving reproduce the expected predictions.
Phase02 running initial score: 32/38. Lesson13 attempt1: 2/2; incomplete.

### Answer history: p02-l13-code-v1

ID: p02-l13-code-v1
Phase02 — ML Fundamentals; Lesson13 — ML Pipelines.
Question39/63; lesson question3/3; code tracing.

This scaler is fitted only on training values. What does it output for the new batch?

```python
train = [2.0, 4.0, 6.0]
mean = sum(train) / len(train)
std = (sum((x - mean)**2 for x in train) / len(train))**0.5
new_batch = [4.0, 8.0]
scaled = [(x - mean) / std for x in new_batch]
print([round(x, 3) for x in scaled])
```

A) [-1.0, 1.0]
B) [0.0, 2.449]
C) [0.0, 2.0]
D) [4.0, 8.0]


Learner answer: B. Correct answer: B. Result: correct.
Explanation: Training mean=4 and population standard deviation=sqrt(8/3). Applying those stored statistics gives [0, 4/sqrt(8/3)], rounded to [0.0, 2.449].
Phase02 running initial score: 33/39. Lesson13 attempt1 complete: 3/3. Lessons remain todo until the full phase passes.

### Answer history: p02-l14-concept-v1

ID: p02-l14-concept-v1
Phase02 — ML Fundamentals; Lesson14 — Naive Bayes.
Question40/63; lesson question1/3; conceptual.

What is the conditional independence assumption made by Naive Bayes for features X1 and X2 and class C?

A) P(X1, X2) = P(X1) * P(X2), regardless of the class.
B) P(C | X1, X2) = P(C), regardless of the feature values.
C) P(X1 | C) = P(X2 | C), so features have identical distributions.
D) P(X1, X2 | C) = P(X1 | C) * P(X2 | C).


Learner answer: D. Correct answer: D. Result: correct.
Explanation: Naive Bayes factorizes the feature likelihood conditional on the class. This neither requires unconditional independence nor identical feature distributions.
Phase02 running initial score: 34/40. Lesson14 attempt1: 1/1; incomplete.

### Answer history: p02-l14-application-v1

ID: p02-l14-application-v1
Phase02 — ML Fundamentals; Lesson14 — Naive Bayes.
Question41/63; lesson question2/3; application.

You represent each short message with binary word-presence features and want both word presence and word absence to contribute evidence. Which Naive Bayes variant directly matches this representation?

A) Multinomial NB, because it explicitly includes likelihood terms for absent vocabulary words.
B) Bernoulli NB, because each binary feature contributes a presence or absence likelihood.
C) Gaussian NB, because each word-presence flag must follow a continuous normal distribution.
D) All three variants, because they use identical feature likelihoods for binary inputs.


Learner answer: B. Correct answer: B. Result: correct.
Explanation: Bernoulli NB models each feature as present or absent, including likelihood factors for both outcomes. In Multinomial NB, a zero word count contributes zero to the log-score sum.
Phase02 running initial score: 35/41. Lesson14 attempt1: 2/2; incomplete.

### Answer history: p02-l14-code-v1

ID: p02-l14-code-v1
Phase02 — ML Fundamentals; Lesson14 — Naive Bayes.
Question42/63; lesson question3/3; code tracing.

These are the total training word counts for one class over a fixed three-word vocabulary. What probabilities result from Laplace smoothing with alpha=1?

```python
counts = [3, 1, 0]
alpha = 1
smoothed = [c + alpha for c in counts]
probs = [c / sum(smoothed) for c in smoothed]
print([round(p, 3) for p in probs])
```

A) [0.75, 0.25, 0.0]
B) [0.8, 0.4, 0.2]
C) [0.571, 0.286, 0.143]
D) [0.333, 0.333, 0.333]


Learner answer: C. Correct answer: C. Result: correct.
Explanation: Adding1 gives counts [4, 2, 1] with denominator7. The probabilities are [4/7, 2/7, 1/7], so the unseen-in-class vocabulary term receives a nonzero probability.
Phase02 running initial score: 36/42. Lesson14 attempt1 complete: 3/3. Lessons remain todo until the full phase passes.

### Answer history: p02-l15-concept-v1

ID: p02-l15-concept-v1
Phase02 — ML Fundamentals; Lesson15 — Time Series Fundamentals.
Question43/63; lesson question1/3; conceptual.

In ARIMA(p, d, q), what does the parameter d represent?

A) The number of lagged observations used by the autoregressive component.
B) The number of past forecast errors used by the moving-average component.
C) The number of future time steps predicted in a single forecast.
D) The number of times the series is differenced before modeling.


Learner answer: D. Correct answer: D. Result: correct.
Explanation: d is the differencing order. p counts autoregressive lags, and q counts lagged forecast-error terms in the moving-average component.
Phase02 running initial score: 37/43. Lesson15 attempt1: 1/1; incomplete.

### Answer history: p02-l15-application-v1

ID: p02-l15-application-v1
Phase02 — ML Fundamentals; Lesson15 — Time Series Fundamentals.
Question44/63; lesson question2/3; application.

You forecast tomorrow's sales using observations available by today's close. Recent behavior is more relevant than old regimes; which evaluation design best matches this deployment?

A) Randomly shuffle dates, then use stratified K-fold to balance high- and low-sales days.
B) Use a fixed-length historical training window, evaluate on the following period, and move both windows forward.
C) Train on dates both before and after each validation date to maximize available history.
D) Use an expanding window that includes each validation period before generating its predictions.


Learner answer: D. Correct answer: B. Result: incorrect.
Explanation: Sliding-window walk-forward validation trains on a fixed-length past window and evaluates on subsequent observations. It respects forecast-time availability while limiting old-regime influence. An expanding window can also be valid if strictly historical, but D explicitly includes the validation period before predicting it, causing leakage.
Review: Lesson15 — temporal validation must train before the evaluation period; distinguish valid expanding history from leaking the evaluation period itself. Sliding windows limit stale history.
Phase02 running initial score: 37/44. Lesson15 attempt1: 1/2; incomplete.

### Answer history: p02-l15-code-v1

ID: p02-l15-code-v1
Phase02 — ML Fundamentals; Lesson15 — Time Series Fundamentals.
Question45/63; lesson question3/3; code tracing.

What is the final feature-target pair produced by this lag-feature code? Each feature list is ordered [lag_1, lag_2].

```python
series = [10, 12, 14, 13, 15]
rows = []
for t in range(2, len(series)):
    features = [series[t - 1], series[t - 2]]
    target = series[t]
    rows.append((features, target))
print(rows[-1])
```

A) ([13, 14], 15)
B) ([14, 13], 15)
C) ([15, 13], 15)
D) ([12, 10], 14)


Learner answer: A. Correct answer: A. Result: correct.
Explanation: The final index is t=4: lag1=series[3]=13, lag2=series[2]=14, and target=series[4]=15. Both features precede the target.
Phase02 running initial score: 38/45. Lesson15 attempt1 complete: 2/3, meeting the lesson minimum. Lessons remain todo until the full phase passes. Temporal validation remains in the review queue.

### Answer history: p02-l16-concept-v1

ID: p02-l16-concept-v1
Phase02 — ML Fundamentals; Lesson16 — Anomaly Detection.
Question46/63; lesson question1/3; conceptual.

In Isolation Forest, why can a shorter average isolation path indicate a more anomalous point?

A) The trees optimize class-label purity, so short paths identify the minority label.
B) Dense-region points always reach leaves before points in sparse regions.
C) Unusual, isolated points often need fewer random splits to separate them from other observations.
D) The method assigns shorter paths to every point with a larger feature-vector norm.


Learner answer: C. Correct answer: C. Result: correct.
Explanation: Random partitions often isolate unusual points in fewer splits, while separating points among many nearby observations generally requires longer paths. Isolation Forest does not optimize labeled class purity.
Phase02 running initial score: 39/46. Lesson16 attempt1: 1/1; incomplete.

### Answer history: p02-l16-application-v1

ID: p02-l16-application-v1
Phase02 — ML Fundamentals; Lesson16 — Anomaly Detection.
Question47/63; lesson question2/3; application.

Only 0.1% of events are true anomalies, and analysts can investigate the 100 highest-scoring events per day. Which metric most directly measures how useful those daily reviews are, assuming reliable labels for reviewed events?

A) Overall accuracy across all daily events.
B) The fraction of daily events predicted normal.
C) Mean anomaly score across all daily events.
D) Precision@100: the fraction of the top 100 flagged events that are true anomalies.


Learner answer: D. Correct answer: D. Result: correct.
Explanation: Precision@100 measures the fraction of the daily review budget spent on true anomalies. Overall accuracy is dominated by normal events under this imbalance.
Phase02 running initial score: 40/47. Lesson16 attempt1: 2/2; incomplete.

### Answer history: p02-l16-code-v1

ID: p02-l16-code-v1
Phase02 — ML Fundamentals; Lesson16 — Anomaly Detection.
Question48/63; lesson question3/3; code tracing.

Given these quartiles from the baseline data, which new values does the IQR detector flag?

```python
q1, q3 = 10.0, 14.0
factor = 1.5
iqr = q3 - q1
lower = q1 - factor * iqr
upper = q3 + factor * iqr
values = [3.0, 4.0, 12.0, 20.0, 21.0]
flagged = [x for x in values if x < lower or x > upper]
print(flagged)
```

A) [3.0, 4.0, 20.0, 21.0]
B) [3.0, 21.0]
C) [12.0]
D) [21.0]


Learner answer: B. Correct answer: B. Result: correct.
Explanation: IQR=4, giving lower=4 and upper=20. The strict comparisons flag only3 and21; values exactly on the bounds are not flagged.
Phase02 running initial score: 41/48. Lesson16 attempt1 complete: 3/3. Lessons remain todo until the full phase passes.

### Answer history: p02-l17-concept-v1

ID: p02-l17-concept-v1
Phase02 — ML Fundamentals; Lesson17 — Handling Imbalanced Data.
Question49/63; lesson question1/3; conceptual.

How does standard SMOTE generate a synthetic minority-class example?

A) Duplicate a minority example and assign it a new random label.
B) Interpolate between a minority example and one of its nearest minority-class neighbors.
C) Interpolate between a minority example and its nearest majority-class neighbor.
D) Delete a majority example and replace its label with the minority label.


Learner answer: B. Correct answer: B. Result: correct.
Explanation: Standard SMOTE interpolates between a minority example and a selected nearest minority neighbor, using x_new=x+t*(neighbor-x) with t in [0,1]. It does not relabel majority data or interpolate toward majority neighbors.
Phase02 running initial score: 42/49. Lesson17 attempt1: 1/1; incomplete.

### Answer history: p02-l17-application-v1

ID: p02-l17-application-v1
Phase02 — ML Fundamentals; Lesson17 — Handling Imbalanced Data.
Question50/63; lesson question2/3; application.

You compare SMOTE-based classifiers using cross-validation on data whose deployment positive rate is 1%. Which workflow gives a credible evaluation at that prevalence?

A) Apply SMOTE to the full dataset, then split the synthetic and original rows into folds.
B) Balance both training and validation folds with SMOTE before scoring each model.
C) Apply SMOTE only within each training fold; score on untouched validation folds with their original prevalence.
D) Apply SMOTE only to validation folds, leaving training folds unchanged.


Learner answer: C. Correct answer: C. Result: correct.
Explanation: Resampling belongs only inside the training fold. Untouched validation folds retain the target evaluation prevalence, and their rows cannot influence synthetic training examples.
Phase02 running initial score: 43/50. Lesson17 attempt1: 2/2; incomplete.

### Answer history: p02-l17-code-v1

ID: p02-l17-code-v1
Phase02 — ML Fundamentals; Lesson17 — Handling Imbalanced Data.
Question51/63; lesson question3/3; code tracing.

Using balanced class weights, how many times greater is a positive example's loss weight than a negative example's?

```python
n_negative, n_positive = 900, 100
n = n_negative + n_positive
w_negative = n / (2 * n_negative)
w_positive = n / (2 * n_positive)
print(round(w_positive / w_negative, 1))
```

A) 9.0
B) 5.0
C) 10.0
D) 0.1


Learner answer: A. Correct answer: A. Result: correct.
Explanation: The negative weight is1000/1800=5/9 and the positive weight is1000/200=5. Their ratio is9, the inverse class-count ratio.
Phase02 running initial score: 44/51. Lesson17 attempt1 complete: 3/3. Lessons remain todo until the full phase passes.

### Answer history: p02-l18-concept-v1

ID: p02-l18-concept-v1
Phase02 — ML Fundamentals; Lesson18 — Feature Selection.
Question52/63; lesson question1/3; conceptual.

A feature X has a symmetric distribution around zero and the target is Y=X**2. Why might mutual information identify its relevance when Pearson correlation is zero?

A) Mutual information measures only the sign of the linear regression coefficient.
B) Zero correlation proves independence, so any positive mutual information must be estimation error.
C) Mutual information can detect nonlinear dependence, whereas Pearson correlation measures linear association.
D) Mutual information ignores the target and ranks features only by their variance.


Learner answer: C. Correct answer: C. Result: correct.
Explanation: Pearson correlation measures linear association. Mutual information can detect nonlinear statistical dependence, so a quadratic relationship can be informative despite zero correlation.
Phase02 running initial score: 45/52. Lesson18 attempt1: 1/1; incomplete.

### Answer history: p02-l18-application-v1

ID: p02-l18-application-v1
Phase02 — ML Fundamentals; Lesson18 — Feature Selection.
Question53/63; lesson question2/3; application.

You want a sparse linear model but cannot afford hundreds of model fits for recursive feature elimination. Which approach directly performs embedded feature selection during model fitting?

A) Use a variance filter, which removes features based on their fitted target coefficients.
B) Use Ridge regularization, which is designed to set irrelevant coefficients exactly to zero.
C) Use forward selection, which evaluates all candidate subsets in a single model fit.
D) Use L1 regularization, which can drive coefficients exactly to zero as part of fitting.


Learner answer: D. Correct answer: D. Result: correct.
Explanation: L1 regularization can produce exact zero coefficients during fitting, making it an embedded selection method. RFE and forward selection require repeated fits; Ridge generally shrinks coefficients without creating sparsity.
Phase02 running initial score: 46/53. Lesson18 attempt1: 2/2; incomplete.

### Answer history: p02-l18-code-v1

ID: p02-l18-code-v1
Phase02 — ML Fundamentals; Lesson18 — Feature Selection.
Question54/63; lesson question3/3; code tracing.

These coefficients have already completed a gradient step. What remains after the L1 soft-thresholding step below?

```python
weights = [-0.3, 0.05, 0.8]
threshold = 0.1

def soft_threshold(w):
    magnitude = max(abs(w) - threshold, 0.0)
    return -magnitude if w < 0 else magnitude

print([round(soft_threshold(w), 2) for w in weights])
```

A) [-0.2, 0.0, 0.7]
B) [-0.4, 0.0, 0.9]
C) [-0.3, 0.0, 0.8]
D) [0.2, 0.0, 0.7]


Learner answer: A. Correct answer: A. Result: correct.
Explanation: Soft-thresholding subtracts0.1 from each absolute magnitude, clips at zero, and preserves signs, producing [-0.2, 0.0, 0.7].
Phase02 running initial score: 47/54. Lesson18 attempt1 complete: 3/3. Lessons remain todo until the full phase passes.

### Answer history: p02-l19-concept-v1

ID: p02-l19-concept-v1
Phase02 — ML Fundamentals; Lesson19 — ML System Design.
Question55/63; lesson question1/3; conceptual.

Which statement correctly distinguishes shadow deployment from a canary release?

A) Shadow deployment makes decisions for all users; canary runs only on historical data.
B) Shadow deployment tunes on live outcome labels; canary skips all production monitoring.
C) Shadow deployment scores live traffic without affecting decisions; canary makes real decisions for a small traffic share.
D) Shadow deployment measures business impact by random assignment; canary never affects users.


Learner answer: C. Correct answer: C. Result: correct.
Explanation: Shadow deployment logs predictions on live inputs without using them for user-facing decisions. A canary uses the new model for real decisions on a limited traffic share with monitoring and rollback.
Phase02 running initial score: 48/55. Lesson19 attempt1: 1/1; incomplete.

### Answer history: p02-l19-application-v1

ID: p02-l19-application-v1
Phase02 — ML Fundamentals; Lesson19 — ML System Design.
Question56/63; lesson question2/3; application.

A churn model sends retention offers to high-risk users, and some stay because of the offers. How should you address the resulting feedback loop when evaluating impact and preparing future training data?

A) Treat all retained users as proof that their original churn-risk scores were wrong.
B) Log scores and interventions, and maintain a randomized no-offer holdout to estimate outcomes without the intervention.
C) Remove intervention logs so the next model learns only from the observed churn labels.
D) Evaluate only offer recipients, since users without offers cannot inform the model's business impact.


Learner answer: B. Correct answer: B. Result: correct.
Explanation: Retention offers change observed outcomes. Logging scores and interventions distinguishes treated data, while a randomized no-offer group supports estimation of untreated outcomes and intervention impact.
Phase02 running initial score: 49/56. Lesson19 attempt1: 2/2; incomplete.

### Answer history: p02-l19-code-v1

ID: p02-l19-code-v1
Phase02 — ML Fundamentals; Lesson19 — ML System Design.
Question57/63; lesson question3/3; code tracing.

Using this simplified online-serving cost model, how many replicas are provisioned and what is their daily cost?

```python
import math

peak_qps = 450
replica_qps = 200
min_replicas = 2
dollars_per_replica_hour = 0.50
replicas = max(min_replicas, math.ceil(peak_qps / replica_qps))
daily_cost = replicas * dollars_per_replica_hour * 24
print(replicas, daily_cost)
```

A) 2 24.0
B) 3 1.5
C) 4 48.0
D) 3 36.0


Learner answer: D. Correct answer: D. Result: correct.
Explanation: ceil(450/200)=3 exceeds the minimum2 replicas. Daily cost=3*0.50*24=36 dollars under the supplied exercise cost model.
Phase02 running initial score: 50/57. Lesson19 attempt1 complete: 3/3. Lessons remain todo until the full phase passes.

### Answer history: p02-l20-concept-v1

ID: p02-l20-concept-v1
Phase02 — ML Fundamentals; Lesson20 — Monitoring Models in Production.
Question58/63; lesson question1/3; conceptual.

The input distribution P(x) stays unchanged, but the probability of a positive outcome for the same input changes. Which drift is this, and why might input-only monitoring miss it?

A) Covariate drift; input monitors cannot compare numerical feature distributions.
B) Prior drift; its definition requires the class-conditional input distributions to change.
C) Concept drift; P(y | x) changes even though the monitored input distribution does not.
D) No drift; unchanged inputs guarantee unchanged prediction accuracy.


Learner answer: C. Correct answer: C. Result: correct.
Explanation: Concept drift changes P(y|x). Input-only monitors compare P(x), so they can remain quiet when the same inputs acquire different outcome probabilities. Outcome monitoring with new labels is needed to assess correctness.
Phase02 running initial score: 51/58. Lesson20 attempt1: 1/1; incomplete.

### Answer history: p02-l20-application-v1

ID: p02-l20-application-v1
Phase02 — ML Fundamentals; Lesson20 — Monitoring Models in Production.
Question59/63; lesson question2/3; application.

A drift test on a million events gives a tiny p-value, but its effect size is below your meaningful-change threshold and labeled performance is stable. Which response best follows the lesson's alert-policy principles?

A) Retrain immediately because statistical significance proves harmful concept drift.
B) Record the signal and keep monitoring; require meaningful effect size and persistence before escalating.
C) Disable outcome monitoring because the input test already measures model correctness.
D) Replace the reference window immediately so the current difference disappears.


Learner answer: B. Correct answer: B. Result: correct.
Explanation: Large samples can make tiny distribution changes statistically significant. Meaningful effect sizes and persistence help limit false alarms; stable outcome performance does not justify automatic retraining or deleting the reference.
Phase02 running initial score: 52/59. Lesson20 attempt1: 2/2; incomplete.

### Answer history: p02-l20-code-v1

ID: p02-l20-code-v1
Phase02 — ML Fundamentals; Lesson20 — Monitoring Models in Production.
Question60/63; lesson question3/3; code tracing.

Which windows trigger an alert in this simplified policy? Each tuple contains (p_value, effect_size); alerts occur when the drift streak first reaches two.

```python
alpha = 0.01 / 2
windows = [(0.001, 0.03), (0.001, 0.20),
           (0.02, 0.25), (0.001, 0.20), (0.001, 0.25)]
streak = 0
alerts = []
for i, (p, effect) in enumerate(windows, start=1):
    drift = p < alpha and effect >= 0.1
    streak = streak + 1 if drift else 0
    if streak == 2:
        alerts.append(i)
print(alerts)
```

A) [2, 5]
B) [3, 5]
C) [2, 4, 5]
D) [5]


Learner answer: D. Correct answer: D. Result: correct.
Explanation: The corrected alpha is0.005. Window1 fails the effect threshold, window2 starts a streak, and window3 resets it because p=0.02. Windows4 and5 meet both criteria consecutively, producing the only alert at5.
Phase02 running initial score: 53/60. Lesson20 attempt1 complete: 3/3. Lessons remain todo until the full phase passes.

### Answer history: p02-l21-concept-v1

ID: p02-l21-concept-v1
Phase02 — ML Fundamentals; Lesson21 — Feature Stores and Training-Serving Skew.
Question61/63; lesson question1/3; conceptual.

What is the main purpose of a point-in-time feature join when constructing historical training rows?

A) Attach the newest feature snapshot to every label, regardless of the label timestamp.
B) Select features that would have been available at each prediction time, avoiding future information.
C) Replace all historical feature timestamps with the date the training job runs.
D) Ensure every entity uses the same feature values across all historical prediction times.


Learner answer: B. Correct answer: B. Result: correct.
Explanation: Point-in-time joins reconstruct the features available at each historical prediction time rather than attaching future snapshots. Strict availability also requires accounting for late arrivals and later corrections.
Phase02 running initial score: 54/61. Lesson21 attempt1: 1/1; incomplete. Final phase completion still requires completing the remaining questions and satisfying the per-lesson minimum.

### Answer history: p02-l21-application-v1

ID: p02-l21-application-v1
Phase02 — ML Fundamentals; Lesson21 — Feature Stores and Training-Serving Skew.
Question62/63; lesson question2/3; application.

A backfill run on day30 creates a feature row with event time day10, using a correction that first became available on day25. For a training example whose prediction occurred on day20, is checking event time <= day20 sufficient to reproduce what serving knew?

A) Yes; an old event timestamp guarantees that the corrected value was available then.
B) Yes; backfilled features are exempt from point-in-time availability checks.
C) No; select the latest feature row regardless of time so training benefits from corrections.
D) No; also track availability or creation time and exclude information first available after day20.


Learner answer: D. Correct answer: D. Result: correct.
Explanation: An event timestamp alone does not establish historical availability. The correction arrived after day20, so including it would leak later knowledge; availability or creation timestamps must also be checked.
Phase02 running initial score: 55/62. Lesson21 attempt1: 2/2; incomplete.

### Answer history: p02-l21-code-v1

ID: p02-l21-code-v1
Phase02 — ML Fundamentals; Lesson21 — Feature Stores and Training-Serving Skew.
Question63/63; lesson question3/3; code tracing.

All rows below were available by their event day and belong to the same entity. What does this point-in-time lookup return with a TTL of5 days?

```python
rows = [(7, 4), (14, 3), (21, 1)]  # (event_day, feature_value)

def lookup(day):
    eligible = [row for row in rows if row[0] <= day]
    match = max(eligible, default=None)
    if match is None or day - match[0] > 5:
        return None
    return match[1]

print(lookup(19), lookup(20))
```

A) 3 None
B) 1 1
C) None None
D) 3 3


Learner answer: A. Correct answer: A. Result: correct.
Explanation: The latest eligible row for both queries is day14. At day19 its age is5, within the TTL; at day20 its age is6, so it expires. The future day21 row is ineligible.
Phase02 final initial score: 56/63 (88.89%). Lesson21 attempt1 complete: 3/3.

### Phase02 mastery completion

- Passed on the initial assessment:56/63 (88.89%), meeting the required54/63. All21 lessons meet the minimum2/3; no retakes required.
- Lesson scores01–21:3,3,3,2,3,2,2,3,2,2,2,3,3,3,2,3,3,3,3,3,3.
- All21 lessons done by quiz-based mastery; implementation labs not performed in this assessment. Normal per-lesson progress entries saved in LEARNING.md.
- Seven misses preserved for spaced recall: random forest diversity (Q10), KNN bias–variance tradeoff (Q16), DBSCAN selection (Q20), validation scaling (Q26), bias versus variance definitions (Q28), AdaBoost/gradient boosting/stacking (Q31), and temporal validation (Q44).
- Next assessment:Phase03 — Deep Learning Core, Lesson01, question1/39, not yet presented. No pending answer at this phase boundary.


