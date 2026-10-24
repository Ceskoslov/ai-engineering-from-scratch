# Phase 01 review queue

Historical notes are preserved verbatim; some early remediation requests were superseded by later passes. Latest completion status is in [phase progress](progress.md).

- Phase01 / Lesson09 guided-review follow-up: Still selected base2 exponentiation for cross-entropy measured in nats. Perplexity must invert the loss logarithm: `math.log` pairs with `math.exp`; `math.log2` pairs with `2 ** H`. Use uniform-V-token examples to recover V before starting attempt3.

- Phase 01 / Lesson 09 retake follow-up: Diagonal joint [.5,0;0,.5] describes identical fair binary variables and has MI1 bit (.5*log2(2) twice), not0. Contrast independent uniform joint [.25,.25;.25,.25], which has MI0. Work through this contrast and nats/bits before attempt3 after L10.

- Phase 01 / Lesson 22 (quiz-based assessment, 2/3): With row-vector state probabilities use `distribution @ P`; starting in state 0 yields row 0 of P, not column 0. For P=[[.8,.2],[.3,.7]], [1,0] advances to [.8,.2].

- Phase 01 / Lesson 21 (quiz-based assessment, 2/3): For an undirected unweighted graph, count zero Laplacian eigenvalues to get connected components; [0,0,0,2,2] means three components, not two.

- Phase 01 / Lesson 19 (quiz-based assessment, 2/3): Multiplication by `exp(i*theta)` rotates by theta and preserves magnitude. Complex conjugation reflects across the real axis; these are different operations.

- Phase 01 / Lesson 18 (quiz-based assessment, 2/3): Convexity guarantees local minima are global, not unique. For twice-differentiable convex functions the Hessian is positive semidefinite, allowing zero curvature; positive definiteness is stronger.

- Phase 01 / Lesson 17 (quiz-based assessment, 2/3): Nonsingular does not imply symmetric positive definite. Cholesky requires SPD; use reusable pivoted LU for general dense nonsingular square A with multiple right-hand sides.

- Phase 01 / Lesson 16 (quiz-based assessment, 2/3): Top-p retains the smallest descending-probability prefix reaching the threshold, then renormalizes. For [.50,.30,.15,.05] at p=.75, retain two tokens (mass .80), yielding [.625,.375].

- Phase 01 / Lesson 13 (quiz-based assessment, 2/3): Stable log-sum-exp adds the removed maximum back: `c + log(sum(exp(v-c)))`. For two values -1000, result is -1000 + ln(2), approximately -999.307.

- Phase 01 / Lesson 11 (quiz-based assessment, 2/3): Truncated-SVD Frobenius error is the square root of the sum of squared discarded singular values, not their sum. For discarded 4 and 3, error is 5; spectral norm error is 4.

- Phase 01 / Lesson 10 (initial1/3; retake2/3, lesson minimum met): The first PCA component maximizes projected variance over unit directions. Sort covariance eigenvalues descending; minimum-variance directions come last. Retake again selected the smallest eigenvalue: with9 versus1, keep the9 direction, capturing90% of total variance. To transform a new sample, subtract the stored training mean, then project: ([13,24]-[10,20]) dot [.6,.8] = 5. Retake attempt 2 completed 2/3; orthogonality and matrix-vector tracing improved, projection still needs recall.

- Phase 01 / Lesson 09 (initial1/3; attempt2=1/3; attempt3=3/3 after guided review, resolved; keep for spaced recall): Cross-entropy = source entropy + KL divergence: `H(P,Q)=H(P)+KL(P||Q)`. KL is nonnegative; for discrete distributions cross-entropy cannot be below source entropy. Retake missed perplexity units: bits -> 2^H, nats -> exp(H); ln4 nats gives perplexity4. MI=H(X)+H(Y)-H(X,Y); for a uniform independent 2x2 table this is 1+1-2=0, not joint entropy 2. Remediate and retake after the first pass.

- Phase 01 / Lesson 07 (quiz-based assessment, 2/3): Naive Bayes assumes features are conditionally independent of one another given the class; it does not assume features are independent of the class. Keep class-dependent feature likelihoods in scoring.

- Phase 01 / Lesson 06 (initial1/3; attempt2=0/3; attempt3=3/3 after guided review, resolved; keep for spaced recall): A discrete PMF sums to 1; a continuous PDF integrates to 1. Density at a point is not point probability and may exceed 1; e.g. Uniform(0,0.5) has density 2 and area 1. Compute variance as E[X²] - E[X]²; for X=0 (.75), X=2 (.25), the mean is .5, second moment 1, variance .75. Lesson retake required. Retake still confused a point with an interval: for Uniform[0,.25], P(X=.1)=0, while P(0<=X<=.1)=.4. Retake also confused mean squared with variance: for equally likely 1 and3, mean=2, E[X²]=5, mean²=4, variance=1. Deeper remediation needed before attempt3. Also review log-probability sign: log(.25) is -1.386, but negative log-likelihood is +1.386. Schedule worked examples and unscored checks after L09/L10 retakes.

- Phase 01 / Lesson 04 (initial 1/3; retake 3/3, resolved in retake; keep for spaced recall): Gradient = vector of first partial derivatives (slope); Hessian = matrix of second partial derivatives (curvature). Gradient descent subtracts lr times the gradient and recomputes it after every update; for x², x=5 and lr=0.1 yields 5 -> 4 -> 3.2. Remediate and retake after the first pass.

- Phase 01 / Lesson 03 (quiz-based assessment, 2/3): Transformation composition uses matrix multiplication, not element-wise multiplication. For column vectors, rotation R followed by fixed-axis scaling S is `S @ (R @ x) = (S @ R) @ x`; the rightmost transformation acts first.

- Phase 01 / Lesson 01 (initial 0/3; retake 2/3, lesson minimum met): For nonzero real vectors, zero dot product means perpendicular (orthogonal); opposite directions give a negative dot product. Orthogonal vectors need not have unit length; orthonormal adds the unit-length requirement. For projection onto a non-unit b, divide a dot b by b dot b before multiplying b; [3,4] onto [2,0] gives [3,0], residual [0,4]. Projection retake also missed: [4,2] onto [2,2] uses coefficient 12/8=1.5, projection [3,3], residual [1,-1]; check residual dot b=0. Matrix-vector multiplication takes each matrix row dotted with the input: [[0,-1],[1,0]] times [3,1] yields [-1,3]. Remediate and retake after the first pass.
