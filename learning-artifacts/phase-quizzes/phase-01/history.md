# Phase 01 detailed quiz history

Archive: read only when an earlier question or attempt is relevant. [Phase progress](progress.md).

### Phase 01 / Lesson 01 / Attempt 1 (complete)

- p01-l01-concept-v1: zero dot product between nonzero real vectors. Options: A same direction; B perpendicular, lengths need not match; C opposite direction/equal lengths; D orthonormal/unit length.
- Learner answer: C. Correct answer: B. Result: incorrect (0 points).
- Explanation: a dot b = ||a|| ||b|| cos(theta). With nonzero vectors, zero dot product means cos(theta)=0 and a right angle. Opposite directions give a negative dot product; orthogonality does not require unit length.
- Completed score: 0/3. Remediate orthogonality, projection normalization, and row-by-column multiplication; administer a fresh three-question retake after the first pass. Lesson and phase remain todo.
- Review: phases/01-math-foundations/01-linear-algebra-intuition/docs/en.md, Dot product; distinguish orthogonal from opposite and orthonormal.

- p01-l01-application-v1: project a=[3,4] onto b=[2,0]; return projection and residual. Options: A [6,0]/[-3,4]; B [0,4]/[3,0]; C [1.5,0]/[1.5,4]; D [3,0]/[0,4].
- Learner answer: A. Correct answer: D. Result: incorrect (0 points).
- Explanation: a dot b=6 and b dot b=4, so projection=(6/4)[2,0]=[3,0]. The residual is [3,4]-[3,0]=[0,4], perpendicular to b. A non-unit direction requires division by its squared magnitude.
- Review: phases/01-math-foundations/01-linear-algebra-intuition/docs/en.md, Projection.

- p01-l01-code-v1: matrix [[0,-1],[1,0]] times point [3,1] by row dot products. Options: A [1,-3]; B [3,-1]; C [-1,3]; D [-3,1].
- Learner answer: B. Correct answer: C. Result: incorrect (0 points).
- Explanation: First output is 0*3 + (-1)*1 = -1; second is 1*3 + 0*1 = 3. Matrix-vector multiplication takes a dot product of each row with the input vector.
- Review: phases/01-math-foundations/01-linear-algebra-intuition/docs/en.md, Matrices from scratch.

### Phase 01 / Lesson 02 / Attempt 1 (complete)

- p01-l02-concept-v1: NumPy 2x2 arrays, A*B versus A@B. Options: A both element-wise/@ transposes; B * dot products/@ matching elements; C both dot products/* adds bias; D * matching elements/@ row-column dot products.
- Learner answer: D. Correct answer: D. Result: correct (1 point).
- Explanation: For NumPy arrays, * is element-wise multiplication and @ is matrix multiplication, with each output entry computed as a row-column dot product.
- Completed score: 3/3. Lesson remains todo pending the whole phase passing.

- p01-l02-application-v1: dense layer relu(W@x+b), x=(3,1), output=(2,1), no bias broadcasting. Options (W,b): A (3,2)/(2,1); B (2,3)/(2,1); C (2,3)/(3,1); D (3,3)/(2,1).
- Learner answer: B. Correct answer: B. Result: correct (1 point).
- Explanation: (2,3) @ (3,1) gives (2,1); the bias has the same (2,1) shape, and element-wise ReLU preserves it.

- p01-l02-code-v1: determinant of [[1,2],[2,4]], zero check raises before inverse expression. Options: A prints unscaled adjugate; B identity; C ZeroDivisionError during inverse; D ValueError before inverse.
- Learner answer: D. Correct answer: D. Result: correct (1 point).
- Explanation: det=1*4-2*2=0; the explicit ValueError stops execution before divisions or printing.

### Phase 01 / Lesson 03 / Attempt 1 (complete)

- p01-l03-concept-v1: nonzero real v with A@v=-2*v. Options: A double length/reverse direction; B double length/same direction; C rotate 90/same length; D halve length/reverse direction.
- Learner answer: A. Correct answer: A. Result: correct (1 point).
- Explanation: The absolute eigenvalue 2 scales the length by two, while its negative sign reverses direction along the same line.
- Completed score: 2/3. Lesson meets minimum score; completion awaits phase pass. Review transformation composition versus element-wise multiplication.

- p01-l03-application-v1: apply rotation R first, fixed-axis scaling S second to column vector x. Options: A (R@S)@x; B (R+S)@x; C (S@R)@x; D (S*R)@x with element-wise *.
- Learner answer: D. Correct answer: C. Result: incorrect (0 points).
- Explanation: Applying R then S means S@(R@x), which equals (S@R)@x by associativity. Element-wise multiplication does not compose linear transformations.
- Review: phases/01-math-foundations/03-matrix-transformations/docs/en.md, Composition.

- p01-l03-code-v1: eigenvalues from trace/determinant for [[2,1],[1,2]]. Options: A 4.0 3.0; B 3.0 1.0; C 2.0 2.0; D 1.0 -1.0.
- Learner answer: B. Correct answer: B. Result: correct (1 point).
- Explanation: trace=4, det=3, root=sqrt(16-12)=2; outputs are (4+2)/2=3.0 and (4-2)/2=1.0.

### Phase 01 / Lesson 04 / Attempt 1 (complete)

- p01-l04-concept-v1: gradient versus Hessian of a smooth scalar loss. Options: A first partials/second partials-curvature; B second partials/first partials-slope; C parameters/predictions; D global minimum direction/guaranteed step size.
- Learner answer: B. Correct answer: A. Result: incorrect (0 points).
- Explanation: The gradient is the vector of first partial derivatives. The Hessian is the matrix of second partial derivatives, describing local curvature and changes in the gradient.
- Completed score: 1/3. Remediate gradient/Hessian distinction and gradient-descent direction; administer a fresh three-question retake after the first pass. Lesson and phase remain todo.
- Review: phases/01-math-foundations/04-calculus-for-ml/docs/en.md, Gradient and Hessian Matrix.

- p01-l04-application-v1: gradient of x^2+3xy+y^2 at (1,2). Options: A [2,4]; B [7,8]; C [8,7]; D [4,2].
- Learner answer: C. Correct answer: C. Result: correct (1 point).
- Explanation: df/dx=2x+3y=8; df/dy=3x+2y=7, so the gradient in the requested order is [8,7].

- p01-l04-code-v1: x=5.0, lr=0.1, two iterations recomputing grad=2*x and subtracting lr*grad. Options: A 3.0; B 4.0; C 7.2; D 3.2.
- Learner answer: C. Correct answer: D. Result: incorrect (0 points).
- Explanation: First step grad=10, x=5-1=4. Second step grad=8, x=4-0.8=3.2. Gradient descent subtracts the gradient; adding it would instead give 5 -> 6 -> 7.2.
- Review: phases/01-math-foundations/04-calculus-for-ml/docs/en.md, Gradient descent.

### Phase 01 / Lesson 05 / Attempt 1 (complete)

- p01-l05-concept-v1: reverse-mode advantage for millions of parameters and a scalar loss. Options: A perturb each parameter twice; B separate forward derivatives for each parameter; C backward traversal from loss computes all parameter gradients; D avoids chain rule.
- Learner answer: C. Correct answer: C. Result: correct (1 point).
- Explanation: Reverse mode starts with the scalar loss gradient and propagates through the recorded graph, computing derivatives with respect to all contributing parameters in one backward traversal.
- Completed score: 3/3. Lesson remains todo pending the whole phase passing.

- p01-l05-application-v1: test a new backward rule on a smooth scalar expression. Options: A finite forward output proves correctness; B compare central finite differences at several points/tolerance; C gradient/output signs must match; D prediction changes after update.
- Learner answer: B. Correct answer: B. Result: correct (1 point).
- Explanation: Central finite differences provide an independently computed numerical derivative to compare with autodiff, allowing for approximation and floating-point error.

- p01-l05-code-v1: Value x=2, y=x*x+3*x, correct accumulation with += and zero initial gradients. Options: A 4.0; B 3.0; C 7.0; D 10.0.
- Learner answer: C. Correct answer: C. Result: correct (1 point).
- Explanation: dy/dx=2*x+3=7. Both paths through x*x contribute, and the 3*x path contributes another 3.

### Phase 01 / Lesson 06 / Attempt 1 (complete)

- p01-l06-concept-v1: continuous probability density. Options: A density may exceed 1/probability via interval integral; B point density equals point probability; C sum over reals without integration; D density over 1 implies interval probability over 1.
- Learner answer: C. Correct answer: A. Result: incorrect (0 points).
- Explanation: A PDF integrates to 1 over its support; density values themselves are not discrete probability masses. For Uniform(0,0.5), the density is 2 and the total probability is 2*0.5=1.
- Completed score: 1/3. Remediate PDF versus PMF and variance; administer a fresh three-question retake after the first pass. Lesson and phase remain todo.
- Review: phases/01-math-foundations/06-probability-and-distributions/docs/en.md, PMF versus PDF.

- p01-l06-application-v1: X=0 with probability .75 and X=2 with probability .25; mean and variance. Options: A 1/1; B .5/.25; C 1/.75; D .5/.75.
- Learner answer: B. Correct answer: D. Result: incorrect (0 points).
- Explanation: E[X]=0*.75+2*.25=.5. E[X^2]=0*.75+4*.25=1, so Var(X)=1-.5^2=.75. The squared mean .25 is subtracted from the second moment; it is not itself the variance.
- Review: phases/01-math-foundations/06-probability-and-distributions/docs/en.md, Expected Value and Variance.

- p01-l06-code-v1: softmax of [1000,1000] after max shift. Options: A [.5,.5]/preserves probabilities and avoids exp overflow; B zeros; C ones; D overflow.
- Learner answer: A. Correct answer: A. Result: correct (1 point).
- Explanation: Subtracting 1000 gives [0,0], so exps=[1,1] and normalization yields [.5,.5]. A common shift cancels from the softmax numerator and denominator.

### Phase 01 / Lesson 07 / Attempt 1 (complete)

- p01-l07-concept-v1: Naive Bayes feature-likelihood factorization assumption. Options: A equal class priors; B features independent of class/omit likelihoods; C mutually exclusive features; D conditional feature independence given class.
- Learner answer: B. Correct answer: D. Result: incorrect (0 points).
- Explanation: Naive Bayes assumes features are independent of each other conditional on the class, not independent of the class itself. Class-dependent feature likelihoods remain essential to its scores.
- Completed score: 2/3. Lesson meets minimum score; completion awaits phase pass. Review conditional independence given the class.
- Review: phases/01-math-foundations/07-bayes-theorem/docs/en.md, Naive Bayes independence assumption.

- p01-l07-application-v1: spam prior .2; keyword likelihood .6 for spam, .1 for non-spam. Options: A 20%; B 60%; C 75%; D 90%.
- Learner answer: B. Correct answer: B. Result: correct (1 point).
- Explanation: P(keyword)=.6*.2+.1*.8=.20; P(spam|keyword)=.12/.20=.60. The posterior happens to equal the likelihood numerically in this scenario; they are distinct conditional probabilities.

- p01-l07-code-v1: Beta prior (2,3) updated with batches (successes,failures)=(3,1),(1,2); print parameters and posterior mean. Options: A 6 6 .5; B 3 5 .38; C 5 4 .56; D 4 3 .57.
- Learner answer: A. Correct answer: A. Result: correct (1 point).
- Explanation: a=2+3+1=6 and b=3+1+2=6; posterior mean=6/(6+6)=0.5. Both batches update the same posterior parameters sequentially.

### Phase 01 / Lesson 08 / Attempt 1 (complete)

- p01-l08-concept-v1: Adam running statistics per parameter. Options: A parameter/prediction averages; B gradient extrema; C exponential moving averages of gradients/squared gradients; D exact Hessian/inverse.
- Learner answer: C. Correct answer: C. Result: correct (1 point).
- Explanation: Adam tracks first- and second-moment estimates using exponential moving averages of gradients and their squares, then applies bias correction and adaptive scaling.
- Completed score: 3/3. Lesson remains todo pending the whole phase passing.

- p01-l08-application-v1: schedule ramps from small learning rate to peak, then gradually reduces. Options: A fixed; B only step decay from peak; C exponential growth; D linear warmup then cosine decay.
- Learner answer: D. Correct answer: D. Result: correct (1 point).
- Explanation: Warmup increases the learning rate during the initial steps; cosine decay then reduces it over the remaining schedule.

- p01-l08-code-v1: w=5, velocity=0, lr=.1, beta=.9; gradients [2,0]. Options: A 4.62 1.8; B 4.8 0; C 5.38 1.8; D 4.6 2.
- Learner answer: A. Correct answer: A. Result: correct (1 point).
- Explanation: First velocity=2 and w=4.8. Next velocity=.9*2+0=1.8 and w=4.8-.18=4.62. Momentum keeps an update even when the current gradient is zero.

### Phase 01 / Lesson 09 / Attempt 1 (complete)

- p01-l09-concept-v1: relationship between entropy, cross-entropy, and KL with same log base. Options: A CE=H(P)-KL(P||Q); B CE=H(P)+KL(P||Q); C CE=H(Q)+KL(P||Q); D CE=KL(Q||P)-H(P).
- Learner answer: A. Correct answer: B. Result: incorrect (0 points).
- Explanation: KL(P||Q)=H(P,Q)-H(P), so H(P,Q)=H(P)+KL(P||Q). For discrete distributions KL is nonnegative, so cross-entropy cannot be less than the source entropy.
- Completed score: 1/3. Remediate cross-entropy/KL identity and mutual information; administer a fresh three-question retake after the first pass. Lesson and phase remain todo.
- Review: phases/01-math-foundations/09-information-theory/docs/en.md, KL Divergence.

- p01-l09-application-v1: mean cross-entropy 3 bits/token; perplexity. Options: A 3; B approximately 20.1; C 8; D 9.
- Learner answer: C. Correct answer: C. Result: correct (1 point).
- Explanation: With base-2 logs, perplexity=2^H=2^3=8. Using exp(3) would instead apply to a cross-entropy of 3 nats.

- p01-l09-code-v1: uniform 2x2 joint table, marginals each [.5,.5]; sum pxy*log2(pxy/(px*py)). Options: A 1/deterministic; B 2/always joint entropy; C -1/increased uncertainty; D 0/independent.
- Learner answer: B. Correct answer: D. Result: incorrect (0 points).
- Explanation: Each ratio is .25/(.5*.5)=1, so every log2 term is zero and MI=0. Joint entropy is 2 bits here, but H(X)+H(Y)-H(X,Y)=1+1-2=0.
- Review: phases/01-math-foundations/09-information-theory/docs/en.md, Mutual Information.

### Phase 01 / Lesson 10 / Attempt 1 (complete)

- p01-l10-concept-v1: first PCA component criterion for centered data. Options: A unit direction of max projected variance; B label accuracy; C equal pairwise distances; D unit direction of min variance.
- Learner answer: D. Correct answer: A. Result: incorrect (0 points).
- Explanation: PCA orders covariance eigenvectors by decreasing eigenvalues, keeping directions of greatest variance first. The minimum-variance direction is the last component, not the first.
- Completed score: 1/3. Remediate maximum-variance directions and centering/projection; administer a fresh three-question retake after the first pass. Lesson and phase remain todo.
- Review: phases/01-math-foundations/10-dimensionality-reduction/docs/en.md, PCA.

- p01-l10-application-v1: covariance eigenvalues [6,3,1], minimum components for at least 90% variance. Options: A one/60%; B two/90%; C three required; D two/80%.
- Learner answer: B. Correct answer: B. Result: correct (1 point).
- Explanation: Total variance=10; top two sum to 9, giving 90%, while the first alone retains 60%.

- p01-l10-code-v1: sample [13,24] minus training mean [10,20], dotted with unit component [.6,.8]. Options: A 27.0; B 0.0; C 5.0; D 7.0.
- Learner answer: B. Correct answer: C. Result: incorrect (0 points).
- Explanation: Centered sample=[3,4]; coordinate=3*.6+4*.8=1.8+3.2=5.0. Subtract the stored training mean, not the new sample itself.
- Review: phases/01-math-foundations/10-dimensionality-reduction/docs/en.md, PCA transform.

### Phase 01 / Lesson 11 / Attempt 1 (complete)

- p01-l11-concept-v1: real SVD factor meanings. Options: A U eigenvalues/Sigma inputs/V.T inverse; B Sigma nonnegative values/U output directions/V input directions; C negative values/triangular factors; D square invertible only.
- Learner answer: B. Correct answer: B. Result: correct (1 point).
- Explanation: Singular values are nonnegative scaling factors; left/right singular vectors provide orthonormal directions in output/input spaces. SVD also exists for rectangular and singular matrices.
- Completed score: 2/3. Lesson meets minimum score; completion awaits phase pass. Review Frobenius reconstruction error.

- p01-l11-application-v1: singular values [5,4,3], Frobenius error after keeping only first. Options: A 3; B 4; C 7; D 5.
- Learner answer: C. Correct answer: D. Result: incorrect (0 points).
- Explanation: Frobenius error is sqrt(sum of squares of discarded singular values)=sqrt(4^2+3^2)=5. Adding magnitudes gives 7; spectral norm error is instead 4.
- Review: phases/01-math-foundations/11-singular-value-decomposition/docs/en.md, Truncated SVD.

- p01-l11-code-v1: reciprocal singular values [4,2,0], conditional inversion above tolerance 1e-10. Options: A [4,2,0]; B [.25,.5,0]; C [.25,.5,1]; D zero division.
- Learner answer: B. Correct answer: B. Result: correct (1 point).
- Explanation: Values above tolerance are inverted; zero follows the else branch and remains zero without evaluating 1/0.

### Phase 01 / Lesson 12 / Attempt 1 (complete)

- p01-l12-concept-v1: broadcasting compatibility. Options: A align left/equal only; B same element count; C align right/equal or 1/missing leading axes 1; D any smaller size expands.
- Learner answer: C. Correct answer: C. Result: correct (1 point).
- Explanation: Broadcasting aligns trailing dimensions. Each aligned pair must be equal or contain a singleton dimension; missing leading axes behave as singleton axes.
- Completed score: 3/3. Lesson remains todo pending the whole phase passing.

- p01-l12-application-v1: Q,K=(2,4,8,16), einsum bhtd,bhsd->bhts. Options: A (2,4,8,16); B (2,8,4,4); C (2,4,16,16); D (2,4,8,8).
- Learner answer: D. Correct answer: D. Result: correct (1 point).
- Explanation: d is contracted out; b,h,t,s remain. Both sequence axes have length 8, so scores have shape (2,4,8,8).

- p01-l12-code-v1: shape (2,3), element strides (3,1), index (1,2), flat data [10,20,30,40,50,60]. Options: A 5 60; B 3 40; C 4 50; D 2 30.
- Learner answer: A. Correct answer: A. Result: correct (1 point).
- Explanation: offset=1*3+2*1=5; zero-based flat index 5 contains 60.

### Phase 01 / Lesson 13 / Attempt 1 (complete)

- p01-l13-concept-v1: nearly equal floating-point approximations and subtraction relative error. Options: A integer conversion; B exponent overflow; C common leading digits cancel/rounding errors dominate small difference; D random replacement.
- Learner answer: C. Correct answer: C. Result: correct (1 point).
- Explanation: Cancellation removes shared significant digits, exposing rounding error already present in the approximations and making it large relative to the small true difference.
- Completed score: 2/3. Lesson meets minimum score; completion awaits phase pass. Review log-sum-exp shift restoration.

- p01-l13-application-v1: preserve small float16 gradients via loss scaling without changing intended update, assuming no overflow. Options: A scale loss/unscale gradients in higher precision before step; B divide loss then rescale after step; C use scaled gradients directly; D replace zero gradients with fixed positive values.
- Learner answer: A. Correct answer: A. Result: correct (1 point).
- Explanation: Scaling before backprop increases intermediate gradient magnitudes, reducing underflow risk. Unscaling before the optimizer step recovers the intended gradient scale.

- p01-l13-code-v1: stable logsumexp for [-1000,-1000]. Options: A .693; B -1000.693; C -999.307; D ValueError/zero sum.
- Learner answer: B. Correct answer: C. Result: incorrect (0 points).
- Explanation: c=-1000, both shifted values=0, exponentials sum to 2. Result=-1000+ln(2), approximately -999.307; the log term is added, not subtracted.
- Review: phases/01-math-foundations/13-numerical-stability/docs/en.md, Log-Sum-Exp Trick.

### Phase 01 / Lesson 14 / Attempt 1 (complete)

- p01-l14-concept-v1: L1 versus squared-L2 regularization. Options: A reverse penalties/sparsity; B L1 often exact zeros/L2 shrinkage; C same fitted results guaranteed; D learning rate/batch size only.
- Learner answer: B. Correct answer: B. Result: correct (1 point).
- Explanation: L1 penalizes absolute weights and promotes sparse solutions; squared-L2 penalizes squared magnitudes and generally shrinks weights without promoting exact zeros.
- Completed score: 3/3. Lesson remains todo pending the whole phase passing.

- p01-l14-application-v1: direction-based similarity invariant to positive rescaling of either nonzero vector without preprocessing. Options: A raw dot; B Euclidean; C cosine; D Manhattan.
- Learner answer: C. Correct answer: C. Result: correct (1 point).
- Explanation: Cosine divides the dot product by both vector norms; positive rescaling cancels, preserving the directional similarity.

- p01-l14-code-v1: Jaccard of {cat,dog,fish} and {cat,fish,bird,snake}. Options: A .6; B .5; C .67; D .4.
- Learner answer: D. Correct answer: D. Result: correct (1 point).
- Explanation: Intersection size=2, union size=5, so similarity=2/5=.4.

### Phase 01 / Lesson 15 / Attempt 1 (complete)

- p01-l15-concept-v1: p=.03 assuming valid null model/test assumptions. Options: A at-least-as-extreme statistic probability .03; B null true probability .03; C alternative true probability .97; D practical importance probability .97.
- Learner answer: A. Correct answer: A. Result: correct (1 point).
- Explanation: A p-value is a tail probability under the null model, not a posterior probability for either hypothesis or a measure of practical value.
- Completed score: 3/3. Lesson remains todo pending the whole phase passing.

- p01-l15-application-v1: tiny accuracy gain with p=.001 on large evaluation set but doubled latency/cost. Options: A p proves deployment value; B assess practical effect/uncertainty/tradeoffs; C tiny gain invalidates test; D cost proves noise.
- Learner answer: B. Correct answer: B. Result: correct (1 point).
- Explanation: Statistical significance does not quantify operational usefulness. Deployment needs assessment of improvement magnitude, uncertainty, latency, cost, and task requirements.

- p01-l15-code-v1: bootstrap means using random.sample(data,k=len(data)). Options: A wrong number of resamples; B means unsupported; C without replacement/every original value/use replacement; D requires set storage.
- Learner answer: C. Correct answer: C. Result: correct (1 point).
- Explanation: random.sample samples without replacement; drawing the full length only permutes the observed values, leaving the mathematical mean unchanged. Bootstrap draws with replacement, e.g. random.choices(data,k=len(data)).

### Phase 01 / Lesson 16 / Attempt 1 (complete)

- p01-l16-concept-v1: Gaussian reparameterization z=mu+sigma*epsilon with parameter-free standard-normal noise. Options: A removes randomness; B differentiable transform/fixed-noise partials 1 and epsilon; C epsilon depends on mu/zero derivative; D categorical replacement.
- Learner answer: B. Correct answer: B. Result: correct (1 point).
- Explanation: Reparameterization places randomness in a parameter-free noise variable and expresses the sample as a differentiable function of mu and sigma for a fixed noise draw.
- Completed score: 2/3. Lesson meets minimum score; completion awaits phase pass. Review top-p selection and renormalization.

- p01-l16-application-v1: sorted probabilities [.50,.30,.15,.05], top-p=.75 with smallest qualifying prefix and renormalization. Options: A top token only; B top two unnormalized; C top three renormalized; D top two .625/.375.
- Learner answer: A. Correct answer: D. Result: incorrect (0 points).
- Explanation: First probability .50 is below .75; the first two sum to .80, so retain both and divide by .80: .50/.80=.625, .30/.80=.375.
- Review: phases/01-math-foundations/16-sampling-methods/docs/en.md, Top-p Sampling.

- p01-l16-code-v1: symmetric Metropolis proposal target .4->.1 and u=.2. Options: A new; B old; C .25; D normalization error.
- Learner answer: A. Correct answer: A. Result: correct (1 point).
- Explanation: Acceptance=min(1,.1/.4)=.25; u=.2 is below .25, so the lower-density proposal is accepted. A shared unknown target normalizer cancels in the ratio.

### Phase 01 / Lesson 17 / Attempt 1 (complete)

- p01-l17-concept-v1: reason for partial pivoting in Gaussian elimination. Options: A probability row sums; B positive eigenvalues; C large available pivot/avoid small divisors/reduce amplification; D change RHS only.
- Learner answer: C. Correct answer: C. Result: correct (1 point).
- Explanation: Partial pivoting swaps in the largest absolute available entry in the pivot column, avoiding an avoidable zero pivot and controlling elimination multipliers.
- Completed score: 2/3. Lesson meets minimum score; completion awaits phase pass. Review solver requirements and LU reuse.

- p01-l17-application-v1: 1000 right-hand sides for fixed dense nonsingular square A; no SPD guarantee. Options: A factor pivoted LU once/reuse triangular solves; B repeated elimination; C unconditional Cholesky; D reuse first solution unchanged.
- Learner answer: C. Correct answer: A. Result: incorrect (0 points).
- Explanation: Reuse a pivoted LU factorization for a general nonsingular square matrix; each new right-hand side needs triangular solves and permutation handling. Cholesky requires symmetric positive definiteness, which nonsingularity alone does not imply.
- Review: phases/01-math-foundations/17-linear-systems/docs/en.md, LU and Cholesky.

- p01-l17-code-v1: back substitution U=[[2,1],[0,3]], b=[5,3]. Options: A [2.5,1]; B [1,2]; C [2,1]; D [5,3].
- Learner answer: C. Correct answer: C. Result: correct (1 point).
- Explanation: Solve last row first: x[1]=3/3=1; then x[0]=(5-1)/2=2.

### Phase 01 / Lesson 18 / Attempt 1 (complete)

- p01-l18-concept-v1: guarantee for convex functions on convex domains. Options: A unique minimizer despite flats; B GD converges for any positive lr; C positive definite Hessian including flats; D all local minima global/minimizers may be nonunique.
- Learner answer: C. Correct answer: D. Result: incorrect (0 points).
- Explanation: Convexity guarantees every local minimum is global, not uniqueness. For a twice-differentiable convex function the Hessian is positive semidefinite; zero-curvature directions are allowed, so positive definiteness is not required.
- Completed score: 2/3. Lesson meets minimum score; completion awaits phase pass. Review positive semidefiniteness versus definiteness and local/global minima.
- Review: phases/01-math-foundations/18-convex-optimization/docs/en.md, Convexity and Hessian test.

- p01-l18-application-v1: minimize x^2+y^2 subject to x+y=2. Options: A (0,0); B (1,1); C (2,0); D (0,2).
- Learner answer: B. Correct answer: B. Result: correct (1 point).
- Explanation: Substitute y=2-x: f=2(x-1)^2+2, minimized at x=1,y=1. The origin is infeasible; the endpoints listed have larger objective values.

- p01-l18-code-v1: Newton step for 5x^2+y^2 from [3,4], gradient [30,8], Hessian diagonal [10,2]. Options: A [-27,-4]; B [2.7,2]; C [0,0]; D [3,4].
- Learner answer: C. Correct answer: C. Result: correct (1 point).
- Explanation: Subtract gradient divided by diagonal curvature: [3-30/10,4-8/2]=[0,0]. The full Newton step reaches this quadratic's minimum exactly.

### Phase 01 / Lesson 19 / Attempt 1 (complete)

- p01-l19-concept-v1: multiply nonzero complex z by exp(i*theta), real theta. Options: A magnitude addition; B always real-axis reflection; C rotation preserving magnitude; D scale theta/remove imaginary part.
- Learner answer: B. Correct answer: C. Result: incorrect (0 points).
- Explanation: exp(i*theta)=cos(theta)+i*sin(theta) has unit magnitude, so multiplication adds theta to phase without changing magnitude. Conjugation, not general multiplication by a fixed unit complex number, reflects across the real axis.
- Completed score: 2/3. Lesson meets minimum score; completion awaits phase pass. Review complex rotation versus conjugation.
- Review: phases/01-math-foundations/19-complex-numbers/docs/en.md, Euler formula and rotations.

- p01-l19-application-v1: unnormalized DFT zero-frequency coefficient for [1,2,3,4]. Options: A 10+0i; B 2.5+0i; C 0+10i; D -2+2i.
- Learner answer: A. Correct answer: A. Result: correct (1 point).
- Explanation: At k=0 every complex exponential is exp(0)=1, so the coefficient is the sum of all samples: 10. No 1/N normalization is applied in the specified forward DFT.

- p01-l19-code-v1: z=3+4j; multiply by conjugate; print real and imaginary parts. Options: A 5 0; B -7 24; C 0 25; D 25 0.
- Learner answer: D. Correct answer: D. Result: correct (1 point).
- Explanation: (3+4i)(3-4i)=3^2+4^2=25, with zero imaginary part. This is squared magnitude, not magnitude 5.

### Phase 01 / Lesson 20 / Attempt 1 (complete)

- p01-l20-concept-v1: FFT versus direct DFT evaluation. Options: A same coefficients/faster algorithm/rounding; B magnitudes only; C different approximate transform; D changes sampling rate.
- Learner answer: A. Correct answer: A. Result: correct (1 point).
- Explanation: FFT is an efficient algorithm for computing the DFT, not a different transform. Direct evaluation is quadratic; standard FFT algorithms achieve O(N log N) for supported lengths.
- Completed score: 3/3. Lesson remains todo pending the whole phase passing.

- p01-l20-application-v1: linear convolution of lengths 5 and 4 via FFT with no wraparound. Options: A pad5/multiply spectra/IFFT; B pad8/add spectra/IFFT; C pad8/multiply spectra/IFFT; D pad8/multiply time samples/FFT.
- Learner answer: C. Correct answer: C. Result: correct (1 point).
- Explanation: Full output length is 5+4-1=8. Padding both to at least 8 avoids circular aliasing; pointwise spectral multiplication and IFFT produce linear convolution.

- p01-l20-code-v1: frequency for bin15 at sample rate800 and transform length200. Options: A15; B60; C4; D400.
- Learner answer: B. Correct answer: B. Result: correct (1 point).
- Explanation: Bin spacing=800/200=4 Hz; bin15 corresponds to 15*4=60 Hz.

### Phase 01 / Lesson 21 / Attempt 1 (complete)

- p01-l21-concept-v1: unweighted undirected graph Laplacian spectrum [0,0,0,2,2]. Options: A two components; B three components; C three edges; D connected/nonnegative spectrum.
- Learner answer: A. Correct answer: B. Result: incorrect (0 points).
- Explanation: The multiplicity of eigenvalue zero equals the number of connected components. There are three zeros, hence three components; count zeros, not positive eigenvalues.
- Completed score: 2/3. Lesson meets minimum score; completion awaits phase pass. Review zero Laplacian eigenvalues and connected components.
- Review: phases/01-math-foundations/21-graph-theory/docs/en.md, Graph Laplacian.

- p01-l21-application-v1: minimum hop counts from a source in an unweighted graph. Options: A DFS first-path shortest; B degree sorting; C BFS FIFO layers; D any traversal/all paths same length.
- Learner answer: C. Correct answer: C. Result: correct (1 point).
- Explanation: BFS discovers reachable nodes in nondecreasing edge distance, so first-discovery levels give shortest hop counts.

- p01-l21-code-v1: synchronous neighbor mean on path0-1-2, no self-loops, features[2,4,8]. Options: A[2,4,8]; B[4,5,4]; C[4,10,4]; D[3,4.67,6].
- Learner answer: B. Correct answer: B. Result: correct (1 point).
- Explanation: End nodes each receive node1's value 4; node1 receives the mean of original endpoint values (2+8)/2=5. All outputs use the old feature vector.

### Phase 01 / Lesson 22 / Attempt 1 (complete)

- p01-l22-concept-v1: stationary row distribution for row-stochastic P. Options: A pi@P=pi/nonnegative sum1; B zero vector; C support states absorbing; D all rows must equal pi.
- Learner answer: A. Correct answer: A. Result: correct (1 point).
- Explanation: A stationary distribution is invariant under one transition: piP=pi. It is still a valid probability distribution; stationarity alone does not require absorbing states or identical transition rows.
- Completed score: 2/3. Lesson meets minimum score; completion awaits phase pass. Review row-vector transition updates.

- p01-l22-application-v1: fair independent +/-1 walk, 400 steps, initial0; mean and standard deviation. Options: A0/400; B20/20; C0/20; D400/0.
- Learner answer: initially A, revised to C before feedback. Final graded answer: C. Correct answer: C. Result: correct (1 point).
- Explanation: Each step has mean0 and variance1. Independent sums have mean0 and variance400, so standard deviation=sqrt(400)=20.

- p01-l22-code-v1: distribution [1,0] multiplied as row vector by P=[[.8,.2],[.3,.7]]. Options: A [.8,.3]; B [.3,.7]; C [1,0]; D [.8,.2].
- Learner answer: A. Correct answer: D. Result: incorrect (0 points).
- Explanation: Starting entirely in state0 gives P's first row: [.8,.2]. Output j sums distribution[i]*P[i][j] over source states i, not entries down the first column.
- Review: phases/01-math-foundations/22-stochastic-processes/docs/en.md, Markov transition matrices.

### Phase 01 first-pass summary

- Completed all 66 questions spanning 22 lessons. Initial score: 45/66 (68.18%); not passed.
- Per-lesson initial scores (01–22, each out of 3): 0,3,2,1,3,1,2,3,1,1,2,3,2,3,3,2,2,2,2,3,2,2.
- Passing requires at least 57/66 and every latest complete lesson set at least 2/3.
- Required retakes in order: Lessons 01, 04, 06, 09, 10. Preserve initial results and completed attempts. Replace effective lesson scores only after each full fresh three-question set is finished.
- Even perfect retakes on those five yield 56/66, so at least one additional missed-topic lesson set will need improvement. Reassess after the required retakes and select the next missed-topic lesson as needed.
- No Phase 01 lesson completion credit yet; all remain todo pending phase pass.

### Phase 01 / Lesson 01 / Attempt 2 (complete)

Remediation delivered: For nonzero real vectors, zero dot product means perpendicular, while orthonormal also requires unit lengths. Projection onto b uses ((a dot b)/(b dot b))*b; divide by squared length if b is not unit. Matrix-vector products compute one row dot product for each output coordinate. 

- p01-l01-concept-v2: u=[2,0], v=[0,5]. Options: A orthonormal because dot0; B orthogonal but not orthonormal/nonunit; C opposite directions; D dependent/different lengths.
- Learner answer: B. Correct answer: B. Result: correct (1 point).
- Explanation: Their dot product is zero, hence they are orthogonal. Their lengths are 2 and 5, so neither is a unit vector and the pair is not orthonormal.
- Completed retake score: 2/3. Effective lesson score is now 2/3 (initial 0/3 preserved). Latest complete phase sets: 47/66.

- p01-l01-application-v2: projection a=[4,2] onto b=[2,2]. Options: A [6,6]/[-2,-4]; B [1.5,1.5]/[2.5,.5]; C [3,3]/[1,-1]; D [4,2]/[0,0].
- Learner answer: A. Correct answer: C. Result: incorrect (0 points).
- Explanation: a dot b=12; b dot b=8. The coefficient is 12/8=1.5, so projection=1.5*[2,2]=[3,3] and residual=[1,-1]. The residual is perpendicular to b: 1*2+(-1)*2=0.
- Recurring review: compute the denominator b dot b before scaling b; verify the residual dot b is zero.

- p01-l01-code-v2: [[2,1],[-1,3]] times [4,2] by row dot products. Options: A [6,10]; B [10,2]; C [8,6]; D [2,10].
- Learner answer: B. Correct answer: B. Result: correct (1 point).
- Explanation: First output=2*4+1*2=10; second=(-1)*4+3*2=2.

### Phase 01 / Lesson 04 / Attempt 2 (complete)

Remediation delivered: gradient contains first derivatives (slope); Hessian contains second derivatives (curvature). Gradient descent uses w_new=w-lr*dL/dw with positive lr, so a negative derivative increases w. Recompute the derivative at the updated parameter on each step. 

- p01-l04-concept-v2: gradient-descent update with negative dL/dw and positive lr. Options: A always decreases parameter; B no update; C uses second derivative; D increases w by subtracting negative derivative.
- Learner answer: D. Correct answer: D. Result: correct (1 point).
- Explanation: Delta w=-lr*dL/dw is positive when the derivative is negative and lr is positive. Descent refers to the objective, not to decreasing every parameter numerically.
- Completed retake score: 3/3. Effective lesson score is now 3/3 (initial 1/3 preserved). Latest complete phase sets: 49/66.

- p01-l04-application-v2: stationary point with Hessian diag(2,-2). Options: A strict min/zero gradient; B strict max/one negative direction; C saddle/mixed eigenvalues; D flat/zero off-diagonals.
- Learner answer: C. Correct answer: C. Result: correct (1 point).
- Explanation: Positive curvature in one direction and negative curvature in another at a stationary point establish a saddle point. Zero gradient alone does not identify a minimum.

- p01-l04-code-v2: w=-4, lr=.25, two updates recomputing grad=2*w. Options: A -1; B -2; C -9; D 0.
- Learner answer: A. Correct answer: A. Result: correct (1 point).
- Explanation: First gradient=-8, w=-4-.25*(-8)=-2. Second gradient=-4, w=-2-.25*(-4)=-1.

### Phase 01 / Lesson 06 / Attempt 2 (complete)

Remediation delivered: a discrete PMF assigns probability masses that sum to one. A continuous PDF assigns density; interval probabilities are areas under it, total area is one, and individual point probability is zero. Variance is E[X²]-E[X]², not the squared mean alone. 

- p01-l06-concept-v2: Uniform[0,.25], density4; P(X=.1). Options: A4; B.4; C1; D0/point zero width.
- Learner answer: B. Correct answer: D. Result: incorrect (0 points).
- Explanation: A single point has probability zero under this continuous distribution. The value .4 is instead P(0<=X<=.1)=4*.1, which refers to an interval rather than equality at one point.
- Completed retake score: 0/3. Effective lesson score is now 0/3 under the latest-complete-set rule (initial 1/3 preserved). Effective phase total is 48/66. Deeper remediation and attempt3 required after L09/L10.
- Recurring review: distinguish P(X=x) from P(a<=X<=b); density times interval width is not point probability.

- p01-l06-application-v2: X=1 or3 each probability .5; mean and variance. Options: A2/4; B2/1; C2/5; D1/2.
- Learner answer: A. Correct answer: B. Result: incorrect (0 points).
- Explanation: Mean=.5*1+.5*3=2. Squared deviations from mean are both1, so variance=.5*1+.5*1=1. Equivalently E[X^2]=5, mean squared=4, variance=5-4=1. Mean squared alone is not variance.
- Recurring review: separate E[X^2], E[X]^2, and Var(X); need deeper remediation before a third attempt.

- p01-l06-code-v2: normalize [1,3] into [.25,.75]; target0; negative natural log loss. Options: A .25; B .288; C -1.386; D 1.386.
- Learner answer: C. Correct answer: D. Result: incorrect (0 points).
- Explanation: log(.25)=-1.386..., so the leading minus sign gives positive loss1.386. Negative log probability is nonnegative for probabilities in (0,1].
- Review for attempt3: point probability versus interval area, variance versus squared mean, log probability versus negative log loss. Use worked examples and unscored learner calculations before a new scored set.

### Phase 01 / Lesson 09 / Attempt 2 (complete)

Remediation delivered: H(P,Q)=H(P)+KL(P||Q). For fixed P, H(P) is constant, so minimizing CE over Q also minimizes KL. Perplexity uses the matching log base: 2^H in bits, exp(H) in nats. MI=H(X)+H(Y)-H(X,Y), and independent variables have MI0. 

- p01-l09-concept-v2: fixed P, equivalence of minimizing cross-entropy over Q and forward KL. Options: A always equal; B KL symmetric; C CE=H(P)+KL and H(P) constant; D H(P) changes with Q.
- Learner answer: C. Correct answer: C. Result: correct (1 point).
- Explanation: Cross-entropy differs from forward KL by the constant entropy of the fixed true distribution. The two objectives therefore have the same minimizers in Q.
- Completed retake score: 1/3. Effective lesson score remains 1/3 (initial attempt preserved). Phase total remains48/66. Deeper remediation and fresh attempt3 required after L10.

- p01-l09-application-v2: cross-entropy ln4 nats; perplexity. Options: A2^1.386 approximately2.61; Bexp(ln4)=4; C1.386; D16.
- Learner answer: A. Correct answer: B. Result: incorrect (0 points).
- Explanation: Nats use natural logarithms, so invert with exp: perplexity=exp(ln4)=4. Use base2 exponentiation only when cross-entropy is measured in bits.
- Review: match log/exponential bases; bits -> 2^H, nats -> exp(H).

- p01-l09-code-v2: diagonal joint table [.5,0;0,.5], marginals [.5,.5], mutual information sum p*log2(p/.25) over positive entries. Options: A0; B2; C-1; D1.
- Learner answer: A. Correct answer: D. Result: incorrect (0 points).
- Explanation: Each nonzero term=.5*log2(.5/.25)=.5*1=.5; two terms sum1 bit. X and Y are identical fair binary variables, so observing one completely determines the other. Contrast independent joint [.25,.25;.25,.25], whose MI is0.
- Review for attempt3: independence versus deterministic dependence, joint entropy versus MI, nats versus bits. Use worked examples and unscored learner calculations before another scored set.

### Phase 01 / Lesson 10 / Attempt 2 (complete)

Remediation delivered: standard PCA orders covariance eigenvectors from largest to smallest eigenvalue, keeping maximum-variance directions first. It is unsupervised; variance is not a guarantee of task relevance. To transform a new sample, subtract the fitted training mean and project onto the stored components. 

- p01-l10-concept-v2: eigenvalues9 and1 with eigenvectors v1,v2; one-component PCA. Options: A v2/smallest strongest; B v1/largest projected variance; C label accuracy; D average equally.
- Learner answer: A. Correct answer: B. Result: incorrect (0 points).
- Explanation: For unit covariance eigenvectors, projected variance equals the eigenvalue. v1 captures9 units of variance versus1 along v2, so standard PCA keeps v1, capturing90% of total variance.
- Completed retake score:2/3. Effective lesson score now2/3 (initial1/3 preserved); latest phase sets49/66.
- Recurring review: PCA keeps maximum variance first; the smallest-eigenvalue direction comes last.

- p01-l10-application-v2: validation mean differs; apply same train-fitted PCA. Options: A sample minus itself; B refit on validation; C validation mean with training components; D stored training mean/components.
- Learner answer: D. Correct answer: D. Result: correct (1 point).
- Explanation: A fitted PCA transformation includes both the training mean and components. Reuse both on validation data to preserve the fitted coordinate system and avoid learning preprocessing from held-out data.

- p01-l10-code-v2: sample[7,9] minus mean[3,6], projected onto [.8,.6]. Options:A11;B0;C5;D7.
- Learner answer:C. Correct answer:C. Result:correct (1 point).
- Explanation: Centered sample=[4,3], coordinate=4*.8+3*.6=5.

### Lesson06 deeper remediation (unscored; before attempt3)

- Interval versus point: Uniform[0,1] has density1; probability over [.2,.5] is width .3 times density1 = .3, while probability of exactly .2 is0.
- Variance is mean squared deviation, not square of mean. For equally likely2 and6, mean4 and variance ((2-4)^2+(6-4)^2)/2=4; E[X²]=20 and E[X]²=16.
- Negative log loss: ln(.5) is approximately -.693, so -ln(.5) is +.693. Probabilities at most1 have nonpositive logarithms.
- Ask unscored checks one at a time, give targeted feedback, and only then start a fresh three-question scored attempt. Preserve all previous attempts and mark unscored review separately.

- p01-l06-review-interval-1 (unscored): Uniform[0,2], density .5, interval [.5,1]. Learner answer:B. Correct answer:B. Correct; area=.5*(1-.5)=.25. No mastery score changes.

- p01-l06-review-variance-2 (unscored): equally likely2 and6, mean4; variance calculation. Learner answer:C. Correct answer:C. Correct; mean squared deviations=.5*4+.5*4=4. Distinguish mean4, squared mean16, second moment20, variance4. No mastery score changes.

- p01-l06-review-logloss-3 (unscored): p=.2, ln(p)=-1.609; negative log-loss. Learner answer:D. Correct answer:D. Correct; minus negative gives+1.609. All three guided checks correct; no mastery score changes.

### Phase01 / Lesson06 / Attempt3 (complete)

Start after three correct unscored review checks. Use a fresh three-question scored set. Preserve initial1/3 and attempt2=0/3; update effective score only after attempt3 is complete.

- p01-l06-concept-v3: Uniform[0,4], probability interval[1,3] and point2. Options:A .25/.25;B .5/0;C2/1;D0/0.
- Learner answer:B. Correct answer:B. Result:correct (1 point).
- Explanation: Density1/4 times interval width2 gives .5; a single point has zero probability in this continuous distribution.
- Completed attempt3 score:3/3. Effective lesson score now3/3, replacing attempt2=0/3. Initial1/3 and attempt2 retained. Effective phase52/66.

- p01-l06-application-v3: X0 with probability.25, X4 with probability.75;mean/variance. Options:A3/9;B2/4;C3/12;D3/3.
- Learner answer:D. Correct answer:D. Result:correct (1 point).
- Explanation:E[X]=3; E[X²]=.75*16=12; Var(X)=12-3²=3. Equivalently .25*(0-3)²+.75*(4-3)²=3.

- p01-l06-code-v3: weights[4,1], normalize, target0, negative natural log. Options:A .8/+.223;B .8/-.223;C .2/1.609;D4/-1.386.
- Learner answer:A. Correct answer:A. Result:correct (1 point).
- Explanation: Target probability4/5=.8; -ln(.8)=+.223143..., giving .8 and .223 after rounding.

### Lesson09 deeper remediation (unscored; before attempt3)

- MI is uncertainty removed: I(X;Y)=H(Y)-H(Y|X). A fair bit Y has H(Y)=1 bit. Independent X leaves H(Y|X)=1 -> MI0. If X=Y, H(Y|X)=0 -> MI1.
- MI is not joint entropy. Independent fair bits have joint entropy2 but MI0; identical fair bits have joint entropy1 and MI1.
- Perplexity reverses the logarithm used by mean cross-entropy: bits ->2^H; nats ->exp(H). H=ln(4) nats ->perplexity4.
- Cross-entropy=H(P)+KL(P||Q), so the KL term is extra surprise above fixed source entropy.
- Ask unscored checks one at a time, then a fresh scored attempt3; exclude these checks from all mastery totals.

- p01-l09-review-mi-1 (unscored): fair Y entropy1; independent X conditional entropy1; identical X conditional entropy0. Learner answer:C. Correct answer:C. Correct; MI=1-1=0 and1-0=1. No mastery score changes.

- p01-l09-review-perplexity-2 (unscored): H=ln8 nats; perplexity expression. Learner answer:A (2^ln8). Correct answer:B (exp(ln8)=8). Incorrect; no mastery score changes.
- Additional explanation: perplexity undoes the log used in cross-entropy. log2 and powers of2 are inverses; natural log and exp are inverses. For uniform V choices, natural-log CE=lnV, so perplexity must recover V via exp, not base2. Show code distinction math.log versus math.log2; math.exp(H) versus2**H.

- p01-l09-review-perplexity-2b (unscored): H=math.log(5); recover perplexity5. Learner answer:A (2**H). Correct answer:D (math.exp(H)). Incorrect; no mastery score changes.
- Numeric walkthrough delivered: H=ln5 approximately1.609; 2^1.609 approximately3.05, which fails to recover5. exp(1.609) approximately5. Therefore nats require exp. Adapt unscored review from letters to a direct numeric trace to diagnose the inverse operation, without changing scored-quiz format.

- p01-l09-review-perplexity-2c (unscored): round(exp(log(10))). Learner answer:10. Correct answer:10. Correct; natural log and exponential are inverse operations. No mastery score changes.

- p01-l09-review-perplexity-2d (unscored): mean CE2.0 nats/token, perplexity expression/value. Learner answer:e**2 approximately7.389. Correct; exp(2)=7.389056..., demonstrating base-matching on a directly supplied nat loss. No mastery score changes.

- p01-l09-review-cekl-3 (unscored): H(P)=1.2 bits, CE=1.7 bits; infer KL. Learner answer:.5. Correct answer:.5 bits. Correct; KL=CE-H(P)=1.7-1.2=.5. No mastery score changes.

### Phase01 / Lesson09 / Attempt3 (complete)

Start a fresh scored set after guided review. Preserve initial1/3 and attempt2=1/3; replace effective score only after the full set is complete.

- p01-l09-concept-v3: H(Y)=2 bits, H(Y|X)=.5 bits; MI. Options:A2.5/add;B.5/remaining;C1.5/removed;D2/always all.
- Learner answer:C. Correct answer:C. Result:correct (1 point).
- Explanation: I(X;Y)=H(Y)-H(Y|X)=2-.5=1.5 bits.
- Completed attempt3 score:3/3. Effective L09 score now3/3 (initial and attempt2 retained). Effective phase54/66.

- p01-l09-application-v3: mean cross-entropy2.5 bits; perplexity calculation. Options:Aexp2.5≈12.182;B2^2.5≈5.657;C6.25;Dln2.5≈.916.
- Learner answer:B. Correct answer:B. Result:correct (1 point).
- Explanation: Bit units use logarithm base2, so perplexity=2^2.5≈5.656854.

- p01-l09-code-v3: p=[.5,.5], q=[.25,.75], KL=CE-H(p) in bits. Options:A1.208;B-.208;C.208;D2.208.
- Learner answer:C. Correct answer:C. Result:correct (1 point).
- Explanation: H(p)=1 bit; CE≈1.20751875 bits; KL≈.20751875 rounds to.208.

### Phase01 latest-set checkpoint after required retakes

- Initial45/66 preserved. Latest complete sets54/66 (81.82%); all22 lessons≥2/3, but overall requires57/66.
- Latest lesson scores01–22:2,3,2,3,3,3,2,3,3,2,2,3,2,3,3,2,2,2,2,3,2,2.
- Need at least3 additional effective points; retake missed-topic lessons with fresh full sets, beginning L01 (projection remains weak), then reassess and choose subsequent missed-topic lessons in order as needed.
- No Phase01 completion credit yet. Original and all retake scores preserved; guided checks excluded.

### Lesson01 focused projection remediation (unscored; before attempt3)

- Separate scalar coefficient c=(a dot b)/(b dot b) from projected vector c*b. The denominator accounts for a non-unit direction vector's squared length.
- Work in stages: compute dot products, divide, multiply the vector, subtract from a, check residual dot b=0.
- Ask learner to calculate stages before starting a new scored set. No scores change during this review.

### Phase01 assessment mode change — learner instruction

- Learner: "go with missed questions, no more unscored review for this phase".
- Scope of change: Phase01 only. Stop guided unscored checks and whole-lesson sets; continue scored counterparts of remaining missed items. The pending unscored projection-coefficient question was withdrawn unanswered, with no score effect.
- Baseline: latest complete lesson sets54/66; each lesson≥2/3. For each targeted question, replace only the matching missed item's effective result. A correct replacement adds one effective point once; an incorrect replacement keeps the item missed. Do not add extra denominator items or duplicate credit. Keep all original answers and scored corrections.
- Phase pass remains≥57/66 and every lesson≥2/3. On pass, mark all22 lessons and Phase01 done and append22 normal progress entries with quiz-based credit.
- Target queue, in lesson order: L01 projection (p01-l01-application-v2); L03 composition (p01-l03-application-v1); L07 conditional independence (p01-l07-concept-v1); L10 maximum variance (p01-l10-concept-v2); L11 Frobenius error (p01-l11-application-v1); L13 log-sum-exp (p01-l13-code-v1); L16 top-p (p01-l16-application-v1); L17 LU/Cholesky (p01-l17-application-v1); L18 convexity (p01-l18-concept-v1); L19 rotations (p01-l19-concept-v1); L21 Laplacian zeros (p01-l21-concept-v1); L22 transition update (p01-l22-code-v1).
- Targeted corrections:L01 projection,L03 composition,and L07 conditional independence correct; effective57/66. Phase passed; other misses remain review topics.

- p01-l01-projection-correction-v3 (scored targeted replacement for p01-l01-application-v2): a=[2,4], b=[1,1], projection. Options:A[6,6];B[3,3];C[1.5,1.5];D[2,4].
- Learner answer:B. Correct answer:B. Result:correct. Matching effective missed item replaced once, +1 point; L01 effective3/3, phase55/66. Earlier wrong answers retained.
- Explanation:a dot b=6; b dot b=2; projection=(6/2)*[1,1]=[3,3].

- p01-l03-composition-correction-v2 (scored targeted replacement for p01-l03-application-v1): scale S then rotate R on column x. Options:A(S@R)@x;B(R+S)@x;C(R@S)@x;D(R*S)@x.
- Learner answer:C. Correct answer:C. Result:correct. Matching effective missed item replaced once,+1 point; L03 effective3/3, phase56/66. Earlier answers retained.
- Explanation:Apply S to x first, then R: R@(S@x)=(R@S)@x.

- p01-l07-independence-correction-v2 (scored targeted replacement for p01-l07-concept-v1): conditional independence factorization. Options:A joint conditional equals product of conditional feature likelihoods;B unconditional features regardless of class;C no class information;D identical feature distributions.
- Learner answer:A. Correct answer:A. Result:correct. Matching effective missed item replaced once,+1 point; L07 effective3/3, phase57/66. Earlier answers retained.
- Explanation:Naive Bayes factors P(X1,X2|C) as P(X1|C)*P(X2|C), expressing feature independence conditional on the class.

### Phase01 mastery completion and stopping checkpoint

- Learner requested:mark this phase done and stop; resume later.
- Passed:57/66 (86.36%) using latest complete sets plus the three authorized targeted missed-item replacements. Every one of22 lessons meets the minimum2/3.
- Initial45/66 preserved. Retakes and targeted corrections preserved. Cumulative scored responses90, correct62; guided review checks excluded from these totals and the mastery score.
- Latest lesson scores01–22:3,3,3,3,3,3,3,3,3,2,2,3,2,3,3,2,2,2,2,3,2,2.
- Phase01 and all22 lessons marked done by quiz-based mastery. Normal per-lesson Progress log entries added to LEARNING.md; no implementation-lab completion claimed.
- Residual review retained for spaced recall:maximum PCA variance,Frobenius error,log-sum-exp,top-p,LU/Cholesky,convexity/semidefiniteness,complex rotations,Laplacian zeros,and row-vector Markov updates.
- Stopped at learner request. No unanswered question is active. Resume Phase02, Lesson01 (What Is Machine Learning), question1/3 of63 phase questions when the learner returns. Do not start now.


