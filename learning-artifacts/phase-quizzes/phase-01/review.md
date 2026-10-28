# Phase 01 — math-foundations Review Summary

[All phases](../progress.md)

- Status: **Done / Passed**; passed on 2026-10-23; coverage: **22 lessons**.
- Initial score: **45/66**; final effective score: **57/66 (86.36%)**.
- Cumulative responses: 90, with 62 correct; **28 initial/retake mistakes** retained. Cumulative responses include retakes and are not the mastery-score denominator.
- Pass criteria: effective phase score ≥85% and final score ≥2/3 in every lesson; all criteria met. Completion basis: quiz-based mastery; implementation labs were not performed in this assessment.

Historical Phase 01 exception: complete retakes yielded 54/66; one correct targeted replacement each for L01 projection, L03 composition, and L07 conditional independence raised the result to 57/66. The denominator stayed 66; guided exercises were excluded. This exception is closed and does not apply to future study.

## Weak points and review priorities

- Prioritize L10 PCA maximum-variance directions and centering with the training mean; L11 truncated-SVD Frobenius error as the square root of the sum of squared discarded singular values; and L13 adding the maximum back in log-sum-exp.
- L16: top-p accumulates descending probabilities to the threshold, then renormalizes. L17: Cholesky requires SPD; general nonsingular matrices can use pivoted LU. L18: convexity does not guarantee a unique minimum, and positive semidefiniteness permits zero curvature.
- L19: complex rotation differs from conjugate reflection. L21: the number of zero graph-Laplacian eigenvalues gives the connected-component count. L22: update row distributions with distribution @ P.
- L01 projection, L03 transformation composition, and L07 conditional independence were corrected through targeted replacements. L04 gradients/Hessians, L06 densities/probabilities/variance, and L09 cross-entropy/MI/perplexity were corrected in retakes; retain them for spaced recall. Match perplexity to the loss logarithm: exp(H) for nats and 2**H for bits.

## Lessons with mistakes and retake outcomes

Lessons with mistakes or retakes are listed below, along with any additional rows retained from the original ledger. Unlisted lessons scored 3/3 initially and finally. A final 3/3 indicates correction in a later assessment where applicable; retain those topics for spaced recall. Lessons at 2/3 remain review priorities.

| Lesson | Initial score | Final effective score / retake |
|---|---|---|
| [Linear Algebra Intuition](../../../phases/01-math-foundations/01-linear-algebra-intuition/docs/en.md) | 0/3 | 3/3 (attempt2 + targeted correction) |
| [Matrix Transformations](../../../phases/01-math-foundations/03-matrix-transformations/docs/en.md) | 2/3 | 3/3 (attempt1 + targeted correction) |
| [Calculus for Machine Learning](../../../phases/01-math-foundations/04-calculus-for-ml/docs/en.md) | 1/3 | 3/3 (attempt 2) |
| [Probability and Distributions](../../../phases/01-math-foundations/06-probability-and-distributions/docs/en.md) | 1/3 | 3/3 (attempt 3) |
| [Bayes' Theorem](../../../phases/01-math-foundations/07-bayes-theorem/docs/en.md) | 2/3 | 3/3 (attempt1 + targeted correction) |
| [Information Theory](../../../phases/01-math-foundations/09-information-theory/docs/en.md) | 1/3 | 3/3 (attempt 3) |
| [Dimensionality Reduction](../../../phases/01-math-foundations/10-dimensionality-reduction/docs/en.md) | 1/3 | 2/3 (attempt 2) |
| [Singular Value Decomposition](../../../phases/01-math-foundations/11-singular-value-decomposition/docs/en.md) | 2/3 | 2/3 |
| [Numerical Stability](../../../phases/01-math-foundations/13-numerical-stability/docs/en.md) | 2/3 | 2/3 |
| [Sampling Methods](../../../phases/01-math-foundations/16-sampling-methods/docs/en.md) | 2/3 | 2/3 |
| [Linear Systems](../../../phases/01-math-foundations/17-linear-systems/docs/en.md) | 2/3 | 2/3 |
| [Convex Optimization](../../../phases/01-math-foundations/18-convex-optimization/docs/en.md) | 2/3 | 2/3 |
| [Complex Numbers for AI](../../../phases/01-math-foundations/19-complex-numbers/docs/en.md) | 2/3 | 2/3 |
| [Graph Theory for Machine Learning](../../../phases/01-math-foundations/21-graph-theory/docs/en.md) | 2/3 | 2/3 |
| [Stochastic Processes](../../../phases/01-math-foundations/22-stochastic-processes/docs/en.md) | 2/3 | 2/3 |

## Condensed mistake records

Question IDs, prompts, selected wrong answers, correct answers, and explanations are retained. Other distractors, correct-only questions, and per-response score logs are omitted. Prompts and explanations retain their original English wording. These are historical initial/retake mistakes, not pending retake requirements.

### p01-l01-concept-v1

zero dot product between nonzero real vectors.

- Learner answer: C — opposite direction/equal lengths
- Correct answer: B — perpendicular, lengths need not match
- Explanation: a dot b = ||a|| ||b|| cos(theta). With nonzero vectors, zero dot product means cos(theta)=0 and a right angle. Opposite directions give a negative dot product; orthogonality does not require unit length.

### p01-l01-application-v1

project a=[3,4] onto b=[2,0]; return projection and residual.

- Learner answer: A — [6,0]/[-3,4]
- Correct answer: D — [3,0]/[0,4].
- Explanation: a dot b=6 and b dot b=4, so projection=(6/4)[2,0]=[3,0]. The residual is [3,4]-[3,0]=[0,4], perpendicular to b. A non-unit direction requires division by its squared magnitude.

### p01-l01-code-v1

matrix [[0,-1],[1,0]] times point [3,1] by row dot products.

- Learner answer: B — [3,-1]
- Correct answer: C — [-1,3]
- Explanation: First output is 0*3 + (-1)*1 = -1; second is 1*3 + 0*1 = 3. Matrix-vector multiplication takes a dot product of each row with the input vector.

### p01-l03-application-v1

apply rotation R first, fixed-axis scaling S second to column vector x.

- Learner answer: D — (S*R)@x with element-wise *.
- Correct answer: C — (S@R)@x
- Explanation: Applying R then S means S@(R@x), which equals (S@R)@x by associativity. Element-wise multiplication does not compose linear transformations.

### p01-l04-concept-v1

gradient versus Hessian of a smooth scalar loss.

- Learner answer: B — second partials/first partials-slope
- Correct answer: A — first partials/second partials-curvature
- Explanation: The gradient is the vector of first partial derivatives. The Hessian is the matrix of second partial derivatives, describing local curvature and changes in the gradient.

### p01-l04-code-v1

x=5.0, lr=0.1, two iterations recomputing grad=2*x and subtracting lr*grad.

- Learner answer: C — 7.2
- Correct answer: D — 3.2.
- Explanation: First step grad=10, x=5-1=4. Second step grad=8, x=4-0.8=3.2. Gradient descent subtracts the gradient; adding it would instead give 5 -> 6 -> 7.2.

### p01-l06-concept-v1

continuous probability density.

- Learner answer: C — sum over reals without integration
- Correct answer: A — density may exceed 1/probability via interval integral
- Explanation: A PDF integrates to 1 over its support; density values themselves are not discrete probability masses. For Uniform(0,0.5), the density is 2 and the total probability is 2*0.5=1.

### p01-l06-application-v1

X=0 with probability .75 and X=2 with probability .25; mean and variance.

- Learner answer: B — .5/.25
- Correct answer: D — .5/.75.
- Explanation: E[X]=0*.75+2*.25=.5. E[X^2]=0*.75+4*.25=1, so Var(X)=1-.5^2=.75. The squared mean .25 is subtracted from the second moment; it is not itself the variance.

### p01-l07-concept-v1

Naive Bayes feature-likelihood factorization assumption.

- Learner answer: B — features independent of class/omit likelihoods
- Correct answer: D — conditional feature independence given class.
- Explanation: Naive Bayes assumes features are independent of each other conditional on the class, not independent of the class itself. Class-dependent feature likelihoods remain essential to its scores.

### p01-l09-concept-v1

relationship between entropy, cross-entropy, and KL with same log base.

- Learner answer: A — CE=H(P)-KL(P||Q)
- Correct answer: B — CE=H(P)+KL(P||Q)
- Explanation: KL(P||Q)=H(P,Q)-H(P), so H(P,Q)=H(P)+KL(P||Q). For discrete distributions KL is nonnegative, so cross-entropy cannot be less than the source entropy.

### p01-l09-code-v1

uniform 2x2 joint table, marginals each [.5,.5]; sum pxy*log2(pxy/(px*py)).

- Learner answer: B — 2/always joint entropy
- Correct answer: D — 0/independent.
- Explanation: Each ratio is .25/(.5*.5)=1, so every log2 term is zero and MI=0. Joint entropy is 2 bits here, but H(X)+H(Y)-H(X,Y)=1+1-2=0.

### p01-l10-concept-v1

first PCA component criterion for centered data.

- Learner answer: D — unit direction of min variance.
- Correct answer: A — unit direction of max projected variance
- Explanation: PCA orders covariance eigenvectors by decreasing eigenvalues, keeping directions of greatest variance first. The minimum-variance direction is the last component, not the first.

### p01-l10-code-v1

sample [13,24] minus training mean [10,20], dotted with unit component [.6,.8].

- Learner answer: B — 0.0
- Correct answer: C — 5.0
- Explanation: Centered sample=[3,4]; coordinate=3*.6+4*.8=1.8+3.2=5.0. Subtract the stored training mean, not the new sample itself.

### p01-l11-application-v1

singular values [5,4,3], Frobenius error after keeping only first.

- Learner answer: C — 7
- Correct answer: D — 5.
- Explanation: Frobenius error is sqrt(sum of squares of discarded singular values)=sqrt(4^2+3^2)=5. Adding magnitudes gives 7; spectral norm error is instead 4.

### p01-l13-code-v1

stable logsumexp for [-1000,-1000].

- Learner answer: B — -1000.693
- Correct answer: C — -999.307
- Explanation: c=-1000, both shifted values=0, exponentials sum to 2. Result=-1000+ln(2), approximately -999.307; the log term is added, not subtracted.

### p01-l16-application-v1

sorted probabilities [.50,.30,.15,.05], top-p=.75 with smallest qualifying prefix and renormalization.

- Learner answer: A — top token only
- Correct answer: D — top two .625/.375.
- Explanation: First probability .50 is below .75; the first two sum to .80, so retain both and divide by .80: .50/.80=.625, .30/.80=.375.

### p01-l17-application-v1

1000 right-hand sides for fixed dense nonsingular square A; no SPD guarantee.

- Learner answer: C — unconditional Cholesky
- Correct answer: A — factor pivoted LU once/reuse triangular solves
- Explanation: Reuse a pivoted LU factorization for a general nonsingular square matrix; each new right-hand side needs triangular solves and permutation handling. Cholesky requires symmetric positive definiteness, which nonsingularity alone does not imply.

### p01-l18-concept-v1

guarantee for convex functions on convex domains.

- Learner answer: C — positive definite Hessian including flats
- Correct answer: D — all local minima global/minimizers may be nonunique.
- Explanation: Convexity guarantees every local minimum is global, not uniqueness. For a twice-differentiable convex function the Hessian is positive semidefinite; zero-curvature directions are allowed, so positive definiteness is not required.

### p01-l19-concept-v1

multiply nonzero complex z by exp(i*theta), real theta.

- Learner answer: B — always real-axis reflection
- Correct answer: C — rotation preserving magnitude
- Explanation: exp(i*theta)=cos(theta)+i*sin(theta) has unit magnitude, so multiplication adds theta to phase without changing magnitude. Conjugation, not general multiplication by a fixed unit complex number, reflects across the real axis.

### p01-l21-concept-v1

unweighted undirected graph Laplacian spectrum [0,0,0,2,2].

- Learner answer: A — two components
- Correct answer: B — three components
- Explanation: The multiplicity of eigenvalue zero equals the number of connected components. There are three zeros, hence three components; count zeros, not positive eigenvalues.

### p01-l22-code-v1

distribution [1,0] multiplied as row vector by P=[[.8,.2],[.3,.7]].

- Learner answer: A — [.8,.3]
- Correct answer: D — [.8,.2].
- Explanation: Starting entirely in state0 gives P's first row: [.8,.2]. Output j sums distribution[i]*P[i][j] over source states i, not entries down the first column.

### p01-l01-application-v2

projection a=[4,2] onto b=[2,2].

- Learner answer: A — [6,6]/[-2,-4]
- Correct answer: C — [3,3]/[1,-1]
- Explanation: a dot b=12; b dot b=8. The coefficient is 12/8=1.5, so projection=1.5*[2,2]=[3,3] and residual=[1,-1]. The residual is perpendicular to b: 1*2+(-1)*2=0.

### p01-l06-concept-v2

Uniform[0,.25], density4; P(X=.1).

- Learner answer: B — .4
- Correct answer: D — 0/point zero width.
- Explanation: A single point has probability zero under this continuous distribution. The value .4 is instead P(0<=X<=.1)=4*.1, which refers to an interval rather than equality at one point.

### p01-l06-application-v2

X=1 or3 each probability .5; mean and variance.

- Learner answer: A — 2/4
- Correct answer: B — 2/1
- Explanation: Mean=.5*1+.5*3=2. Squared deviations from mean are both1, so variance=.5*1+.5*1=1. Equivalently E[X^2]=5, mean squared=4, variance=5-4=1. Mean squared alone is not variance.

### p01-l06-code-v2

normalize [1,3] into [.25,.75]; target0; negative natural log loss.

- Learner answer: C — -1.386
- Correct answer: D — 1.386.
- Explanation: log(.25)=-1.386..., so the leading minus sign gives positive loss1.386. Negative log probability is nonnegative for probabilities in (0,1].

### p01-l09-application-v2

cross-entropy ln4 nats; perplexity.

- Learner answer: A — 2^1.386 approximately2.61
- Correct answer: B — exp(ln4)=4
- Explanation: Nats use natural logarithms, so invert with exp: perplexity=exp(ln4)=4. Use base2 exponentiation only when cross-entropy is measured in bits.

### p01-l09-code-v2

diagonal joint table [.5,0;0,.5], marginals [.5,.5], mutual information sum p*log2(p/.25) over positive entries.

- Learner answer: A — 0
- Correct answer: D — 1.
- Explanation: Each nonzero term=.5*log2(.5/.25)=.5*1=.5; two terms sum1 bit. X and Y are identical fair binary variables, so observing one completely determines the other. Contrast independent joint [.25,.25;.25,.25], whose MI is0.

### p01-l10-concept-v2

eigenvalues9 and1 with eigenvectors v1,v2; one-component PCA.

- Learner answer: A — v2/smallest strongest
- Correct answer: B — v1/largest projected variance
- Explanation: For unit covariance eigenvectors, projected variance equals the eigenvalue. v1 captures9 units of variance versus1 along v2, so standard PCA keeps v1, capturing90% of total variance.
