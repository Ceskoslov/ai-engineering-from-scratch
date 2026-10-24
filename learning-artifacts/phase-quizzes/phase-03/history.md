# Phase 03 detailed quiz history

Archive: read only when an earlier question or attempt is relevant. [Phase progress](progress.md).

### Phase03 assessment started — 2026-10-24

Learner requested the next phase. English questions; three scored questions per lesson across13 lessons,39 total. Pass requires at least34/39 overall and at least2/3 per lesson. All lessons remain todo until the full phase passes. Phases00–02 remain done.

### Answer history: p03-l01-concept-v1

ID: p03-l01-concept-v1
Phase03 — Deep Learning Core; Lesson01 — The Perceptron.
Question1/39; lesson question1/3; conceptual.

Why can a single perceptron with inputs x1 and x2 not classify all four XOR examples correctly?

A) Its step activation cannot output both binary class labels.
B) Its bias must be zero, forcing the boundary through the origin.
C) Its decision boundary is a single line, and XOR is not linearly separable.
D) Its learning rule requires more examples than the four possible binary inputs.


Learner answer: C. Correct answer: C. Result: correct.
Explanation: A single perceptron thresholds an affine score and therefore defines a linear boundary. XOR's opposite-corner classes cannot be separated by one line in the original two-dimensional input space.
Phase03 running initial score: 1/1. Lesson01 attempt1: 1/1; incomplete.

### Answer history: p03-l01-application-v1

ID: p03-l01-application-v1
Phase03 — Deep Learning Core; Lesson01 — The Perceptron.
Question2/39; lesson question2/3; application.

You want a two-layer network to learn XOR using ordinary backpropagation through its hidden units. Why replace their hard step activations with sigmoid activations?

A) Sigmoid makes the network's overall decision boundary a single straight line.
B) Sigmoid provides useful derivatives for propagating gradients; a hard step has zero derivative away from its threshold and is undefined there.
C) Sigmoid guarantees convergence to the global optimum from every initialization.
D) Sigmoid removes the need to update the hidden-layer weights during training.


Learner answer: B. Correct answer: B. Result: correct.
Explanation: Sigmoid is differentiable, allowing the chain rule to propagate gradients through hidden units. A hard step is constant away from the threshold, with zero derivative, and is discontinuous at the threshold. Sigmoid does not guarantee global convergence or eliminate hidden-weight updates.
Phase03 running initial score: 2/2. Lesson01 attempt1: 2/2; incomplete.

### Answer history: p03-l01-code-v1

ID: p03-l01-code-v1
Phase03 — Deep Learning Core; Lesson01 — The Perceptron.
Question3/39; lesson question3/3; code tracing.

What are the weights and bias after this single perceptron update? The step function outputs1 when the score is exactly zero.

```python
weights = [0.0, 0.0]
bias = 0.0
inputs = [1.0, 0.0]
target = 0
lr = 0.1
score = sum(w * x for w, x in zip(weights, inputs)) + bias
prediction = 1 if score >= 0 else 0
error = target - prediction
weights = [w + lr * error * x for w, x in zip(weights, inputs)]
bias += lr * error
print(weights, bias)
```

A) [0.0, 0.0], 0.0
B) [0.1, 0.0], 0.1
C) [-0.1, -0.1], -0.1
D) [-0.1, 0.0], -0.1


Learner answer: D. Correct answer: D. Result: correct.
Explanation: The zero score predicts1, giving error=-1. The first weight changes by-0.1, the second by0 because its input is0, and the bias changes by-0.1.
Phase03 running initial score: 3/3. Lesson01 attempt1 complete: 3/3. Lessons remain todo until the full phase passes.

### Answer history: p03-l02-concept-v1

ID: p03-l02-concept-v1
Phase03 — Deep Learning Core; Lesson02 — Multi-Layer Networks and Forward Pass.
Question4/39; lesson question1/3; conceptual.

What happens if every activation in a multi-layer network is replaced with the identity function?

A) The network becomes equivalent to one affine transformation, regardless of its depth.
B) Each additional layer creates a new nonlinear decision boundary through matrix multiplication alone.
C) The network becomes unable to use bias terms in its output computation.
D) The network automatically computes gradients and updates its weights during the forward pass.


Learner answer: B. Correct answer: A. Result: incorrect.
Explanation: Composing affine maps yields another affine map: W2*(W1*x+b1)+b2=(W2*W1)*x+(W2*b1+b2). Identity activations introduce no nonlinearity; depth alone therefore cannot produce a nonlinear mapping.
Review: Lesson02 — nonlinear activations are needed to go beyond a single affine transformation.
Phase03 running initial score: 3/4. Lesson02 attempt1: 0/1; incomplete.

### Answer history: p03-l02-application-v1

ID: p03-l02-application-v1
Phase03 — Deep Learning Core; Lesson02 — Multi-Layer Networks and Forward Pass.
Question5/39; lesson question2/3; application.

For a single input column vector x with shape (4,), a network has5 hidden neurons and2 output neurons, using z=W@input+b at each layer. Which weight shapes are correct?

A) W1:(4,5), W2:(5,2)
B) W1:(5,4), W2:(5,2)
C) W1:(5,4), W2:(2,5)
D) W1:(4,5), W2:(2,5)


Learner initially answered A, then revised to C before answer feedback. Final scored answer: C. Correct answer: C. Result: correct; counted once.
Explanation: For W@input, each row corresponds to one output neuron and each column to an incoming feature. W1 therefore has shape(5,4), and W2 has shape(2,5).
Phase03 running initial score: 4/5. Lesson02 attempt1: 1/2; incomplete.

### Answer history: p03-l02-code-v1

ID: p03-l02-code-v1
Phase03 — Deep Learning Core; Lesson02 — Multi-Layer Networks and Forward Pass.
Question6/39; lesson question3/3; code tracing.

What does this two-layer forward pass print, rounded to three decimal places?

```python
import math

def sigmoid(z):
    return 1 / (1 + math.exp(-z))

x = [1.0, 2.0]
W1 = [[1.0, -0.5], [-1.0, 0.5]]
b1 = [0.0, 0.0]
h = [sigmoid(sum(w * v for w, v in zip(row, x)) + b)
     for row, b in zip(W1, b1)]
W2, b2 = [2.0, -2.0], 1.0
out = sigmoid(sum(w * v for w, v in zip(W2, h)) + b2)
print(round(out, 3))
```

A) 0.5
B) 1.0
C) 0.881
D) 0.731


Learner answer: D. Correct answer: D. Result: correct.
Explanation: Both hidden preactivations are zero, so h=[0.5,0.5]. The output preactivation is2*0.5-2*0.5+1=1, and sigmoid(1) rounds to0.731.
Phase03 running initial score: 5/6. Lesson02 attempt1 complete: 2/3, meeting the lesson minimum. Lessons remain todo until the full phase passes. Affine composition remains in the review queue.

### Answer history: p03-l03-concept-v1

ID: p03-l03-concept-v1
Phase03 — Deep Learning Core; Lesson03 — Backpropagation from Scratch.
Question7/39; lesson question1/3; conceptual.

Why must an autograd engine accumulate gradient contributions with += when a value is used along multiple paths to the loss?

A) The total derivative is the sum of the contributions from all paths through that value.
B) Each path requires updating the parameter before processing the next path.
C) Accumulation makes gradients independent of the operations in the forward graph.
D) The total derivative is the largest contribution among the paths through that value.


Learner answer: B. Correct answer: A. Result: incorrect.
Explanation: The multivariable chain rule sums contributions from every path to a shared value. Backpropagation computes gradients at the forward pass's parameter values; the optimizer updates parameters afterward, not between paths.
Review: Lesson03 — sum gradient contributions at shared nodes; keep gradient computation separate from optimizer updates.
Phase03 running initial score: 5/7. Lesson03 attempt1: 0/1; incomplete.

### Answer history: p03-l03-application-v1

ID: p03-l03-application-v1
Phase03 — Deep Learning Core; Lesson03 — Backpropagation from Scratch.
Question8/39; lesson question2/3; application.

In a manual two-layer backward pass, you update the output-layer weights before computing the hidden-layer gradients. How should you fix this so all gradients correspond to the original forward pass?

A) Use the updated output weights, because each gradient should reflect the newest parameters.
B) Skip the hidden-layer gradients whenever output weights have already changed.
C) Compute all gradients before updating parameters, or preserve the original output weights for the hidden-gradient calculation.
D) Reuse the previous batch's hidden gradients, because hidden parameters change slowly.


Learner answer: C. Correct answer: C. Result: correct.
Explanation: Hidden gradients depend on the output weights used in the forward pass. Compute gradients before optimizer updates, or preserve the original weights where needed, to avoid mixing parameter versions.
Phase03 running initial score: 6/8. Lesson03 attempt1: 1/2; incomplete.

### Answer history: p03-l03-code-v1

ID: p03-l03-code-v1
Phase03 — Deep Learning Core; Lesson03 — Backpropagation from Scratch.
Question9/39; lesson question3/3; code tracing.

Using the lesson's Value engine with correct gradient accumulation, what is x.grad after backward? All gradients start at zero.

```python
x = Value(3.0)
a = x * x
loss = a + x
loss.backward()
print(x.grad)
```

A) 3.0
B) 6.0
C) 1.0
D) 7.0


Learner answer: D. Correct answer: D. Result: correct.
Explanation: loss=x*x+x, so its derivative is2*x+1=7 at x=3. Both uses in multiplication contribute3 each, and the direct addition contributes1.
Phase03 running initial score: 7/9. Lesson03 attempt1 complete: 2/3, meeting the lesson minimum. Lessons remain todo until the full phase passes. Gradient accumulation remains in the review queue.

### Answer history: p03-l04-concept-v1

ID: p03-l04-concept-v1
Phase03 — Deep Learning Core; Lesson04 — Activation Functions.
Question10/39; lesson question1/3; conceptual.

A ReLU unit has strictly negative preactivations for every training example. Why can this block learning through that unit, and how does Leaky ReLU address the problem?

A) ReLU's derivative is zero there; Leaky ReLU supplies a small nonzero negative-side slope.
B) ReLU's derivative is infinite there; Leaky ReLU clips it to zero.
C) ReLU's output is always one there; Leaky ReLU rescales it into a probability.
D) ReLU's derivative is negative there; Leaky ReLU reverses the optimizer's update direction.


Learner answer: A. Correct answer: A. Result: correct.
Explanation: ReLU has zero derivative for negative preactivations, blocking the gradient through that activation. Leaky ReLU retains a small nonzero slope on the negative side, allowing gradient flow.
Phase03 running initial score: 8/10. Lesson04 attempt1: 1/1; incomplete.

### Answer history: p03-l04-application-v1

ID: p03-l04-application-v1
Phase03 — Deep Learning Core; Lesson04 — Activation Functions.
Question11/39; lesson question2/3; application.

A model must return probabilities for exactly one of four mutually exclusive classes. Which output transformation directly enforces that the four probabilities sum to one?

A) Apply ReLU independently to the four logits.
B) Apply sigmoid independently to the four logits.
C) Apply softmax jointly across the four logits.
D) Apply tanh independently to the four logits.


Learner answer: C. Correct answer: C. Result: correct.
Explanation: Softmax normalizes exponentiated logits jointly across classes, yielding a probability distribution that sums to one. Independent sigmoid outputs do not impose that sum constraint.
Phase03 running initial score: 9/11. Lesson04 attempt1: 2/2; incomplete.

### Answer history: p03-l04-code-v1

ID: p03-l04-code-v1
Phase03 — Deep Learning Core; Lesson04 — Activation Functions.
Question12/39; lesson question3/3; code tracing.

What does this numerically stable softmax print?

```python
import math
logits = [1000.0, 1000.0 + math.log(3.0)]
m = max(logits)
exps = [math.exp(z - m) for z in logits]
probs = [e / sum(exps) for e in exps]
print([round(p, 2) for p in probs])
```

A) [0.5, 0.5]
B) [0.25, 0.75]
C) [0.33, 1.0]
D) [0.0, 1.0]


Learner answer: b (normalized B). Correct answer: B. Result: correct.
Explanation: Subtracting the maximum yields logits [-ln(3),0], whose exponentials are [1/3,1]. Normalizing gives [1/4,3/4]. A common shift preserves softmax probabilities while avoiding overflow here.
Phase03 running initial score: 10/12. Lesson04 attempt1 complete: 3/3. Lessons remain todo until the full phase passes.

### Answer history: p03-l05-concept-v1

ID: p03-l05-concept-v1
Phase03 — Deep Learning Core; Lesson05 — Loss Functions.
Question13/39; lesson question1/3; conceptual.

What does label smoothing do to a one-hot target distribution when training with categorical cross-entropy?

A) Mixes it with a uniform distribution, assigning some target probability to other classes.
B) Replaces the target with the model's current prediction and removes the original label.
C) Divides the logits by a temperature while leaving the target distribution unchanged.
D) Sets every incorrect-class target to zero and increases the correct-class target above one.


Learner answer: c (normalized C). Correct answer: A. Result: incorrect.
Explanation: Label smoothing changes the target to (1-alpha)*one_hot + alpha/K for K classes. Dividing logits by a temperature changes the predicted distribution instead and does not change the targets.
Review: Lesson05 — distinguish label smoothing of targets from temperature scaling of logits.
Phase03 running initial score: 10/13. Lesson05 attempt1: 0/1; incomplete.

### Answer history: p03-l05-application-v1

ID: p03-l05-application-v1
Phase03 — Deep Learning Core; Lesson05 — Loss Functions.
Question14/39; lesson question2/3; application.

An object detector's training loss is dominated by numerous easy background examples. Which change specifically down-weights easy examples so harder ones receive more relative emphasis?

A) Replace cross-entropy with MSE so all easy examples have identical loss.
B) Use focal loss, multiplying cross-entropy by (1-p_t)**gamma with gamma>0.
C) Increase every background example's loss weight by the same large constant.
D) Remove all negative examples so the detector never trains on background.


Learner answer: b (normalized B). Correct answer: B. Result: correct.
Explanation: For easy examples p_t is near1, so (1-p_t)**gamma is small. Focal loss therefore reduces their contribution relative to harder examples with lower true-class probability.
Phase03 running initial score: 11/14. Lesson05 attempt1: 1/2; incomplete.

### Answer history: p03-l05-code-v1

ID: p03-l05-code-v1
Phase03 — Deep Learning Core; Lesson05 — Loss Functions.
Question15/39; lesson question3/3; code tracing.

For one example, softmax probabilities are [0.2,0.5,0.3] and the true class index is2 (zero-indexed). What gradient with respect to the logits does the lesson's categorical cross-entropy code produce?

```python
probs = [0.2, 0.5, 0.3]
target_index = 2
grads = probs[:]
grads[target_index] -= 1.0
print(grads)
```

A) [-0.8, 0.5, 0.3]
B) [0.2, -0.5, 0.3]
C) [-0.2, -0.5, 0.7]
D) [0.2, 0.5, -0.7]


Learner answer: d (normalized D). Correct answer: D. Result: correct.
Explanation: For softmax plus categorical cross-entropy, the logit gradient is predicted probabilities minus the target distribution. Subtract1 at index2 to obtain [0.2,0.5,-0.7].
Phase03 running initial score: 12/15. Lesson05 attempt1 complete: 2/3, meeting the lesson minimum. Lessons remain todo until the full phase passes. Label smoothing versus temperature remains in the review queue.

### Answer history: p03-l06-concept-v1

ID: p03-l06-concept-v1
Phase03 — Deep Learning Core; Lesson06 — Optimizers.
Question16/39; lesson question1/3; conceptual.

Why does Adam divide its moving moment estimates by 1-beta**t during bias correction?

A) To force every parameter to receive the same raw gradient on every step.
B) To compensate for moment estimates being biased toward zero by their zero initialization.
C) To remove the need for a learning rate after the first optimizer step.
D) To turn the second raw moment into the exact centered variance of the gradients.


Learner answer: B. Correct answer: B. Result: correct.
Explanation: Adam initializes its first and second moment estimates at zero, biasing early exponential averages toward zero. Dividing by1-beta**t corrects this initialization effect; the second estimate remains a raw second moment, not centered variance.
Phase03 running initial score: 13/16. Lesson06 attempt1: 1/1; incomplete.

### Answer history: p03-l06-application-v1

ID: p03-l06-application-v1
Phase03 — Deep Learning Core; Lesson06 — Optimizers.
Question17/39; lesson question2/3; application.

You want weight decay that shrinks parameters proportionally without passing the decay term through Adam's adaptive moment scaling. Which implementation matches that goal?

A) Add lambda*w to the loss gradient before updating Adam's moment estimates.
B) Divide the decay coefficient by each parameter's second-moment estimate.
C) Apply a separate -lr*lambda*w decay term outside the adaptive gradient update, as in AdamW.
D) Replace Adam's gradient with lambda*w and discard the task-loss gradient.


Learner answer: C. Correct answer: C. Result: correct.
Explanation: AdamW decouples weight decay from the loss-gradient moment estimates and adaptive scaling. Adding a weight-proportional term to the gradient instead couples regularization to Adam's moment statistics.
Phase03 running initial score: 14/17. Lesson06 attempt1: 2/2; incomplete.

### Answer history: p03-l06-code-v1

ID: p03-l06-code-v1
Phase03 — Deep Learning Core; Lesson06 — Optimizers.
Question18/39; lesson question3/3; code tracing.

What parameter value does this first Adam step produce? Epsilon is omitted here because the denominator is nonzero.

```python
import math
w, g = 1.0, 2.0
lr = 0.1
beta1, beta2 = 0.9, 0.999
m, v, t = 0.0, 0.0, 1
m = beta1 * m + (1 - beta1) * g
v = beta2 * v + (1 - beta2) * g**2
m_hat = m / (1 - beta1**t)
v_hat = v / (1 - beta2**t)
w -= lr * m_hat / math.sqrt(v_hat)
print(round(w, 3))
```

A) 0.8
B) 0.99
C) 1.1
D) 0.9


Learner answer: D. Correct answer: D. Result: correct.
Explanation: Bias correction gives m_hat=2 and v_hat=4. The normalized update is0.1*2/sqrt(4)=0.1, so w becomes0.9.
Phase03 running initial score: 15/18. Lesson06 attempt1 complete: 3/3. Lessons remain todo until the full phase passes.

### Answer history: p03-l07-concept-v1

ID: p03-l07-concept-v1
Phase03 — Deep Learning Core; Lesson07 — Regularization.
Question19/39; lesson question1/3; conceptual.

For an activation matrix shaped (batch, features), which statement correctly distinguishes LayerNorm from BatchNorm in the lesson's basic setup?

A) LayerNorm normalizes each feature across examples; BatchNorm normalizes features within each example.
B) Both require current-batch statistics during inference, so predictions always depend on batch composition.
C) LayerNorm normalizes features within each example; BatchNorm uses per-feature batch statistics in training and stored running statistics in evaluation.
D) LayerNorm computes only a root mean square without centering; BatchNorm never learns scale or shift parameters.


Learner answer: C. Correct answer: C. Result: correct.
Explanation: LayerNorm computes statistics across a sample's feature dimension independently of other examples. In this setup BatchNorm computes each feature's statistics across the training batch and reuses stored running statistics for evaluation.
Phase03 running initial score: 16/19. Lesson07 attempt1: 1/1; incomplete.

### Answer history: p03-l07-application-v1

ID: p03-l07-application-v1
Phase03 — Deep Learning Core; Lesson07 — Regularization.
Question20/39; lesson question2/3; application.

A trained model uses inverted dropout and BatchNorm with stored running statistics. During ordinary inference, predictions vary because dropout is still active and BatchNorm is using the incoming batch. What is the appropriate fix?

A) Switch to evaluation mode: disable dropout and use BatchNorm's stored running statistics.
B) Keep training mode but set the learning rate to zero, which disables dropout automatically.
C) Refit BatchNorm separately on every request and increase dropout to stabilize outputs.
D) Remove all learned normalization parameters and scale every output by the dropout keep probability.


Learner answer: C. Correct answer: A. Result: incorrect.
Explanation: Ordinary inference should disable dropout and use BatchNorm's stored running statistics. Refitting statistics per request makes outputs depend on the incoming batch, and increasing dropout adds randomness rather than removing it. Learning rate and autograd settings do not themselves switch these layer behaviors.
Review: Lesson07 — evaluation mode disables dropout and uses BatchNorm running statistics; zero learning rate is not evaluation mode.
Phase03 running initial score: 16/20. Lesson07 attempt1: 1/2; incomplete.

### Answer history: p03-l07-code-v1

ID: p03-l07-code-v1
Phase03 — Deep Learning Core; Lesson07 — Regularization.
Question21/39; lesson question3/3; code tracing.

For inverted dropout with drop probability p=0.25, what are the training outputs and input gradients for this fixed mask? A mask value of1 means kept.

```python
x = [3.0, 6.0, 9.0]
mask = [1, 0, 1]
p = 0.25
grad_out = [1.5, 1.5, 1.5]
out = [v * m / (1-p) for v, m in zip(x, mask)]
grad_in = [g * m / (1-p) for g, m in zip(grad_out, mask)]
print(out, grad_in)
```

A) [3.0, 0.0, 9.0], [1.5, 0.0, 1.5]
B) [12.0, 0.0, 36.0], [6.0, 0.0, 6.0]
C) [4.0, 0.0, 12.0], [2.0, 0.0, 2.0]
D) [4.0, 0.0, 12.0], [1.5, 1.5, 1.5]


Learner answer: C. Correct answer: C. Result: correct.
Explanation: Kept outputs and gradients are divided by keep probability0.75. This yields outputs[4,0,12] and gradients[2,0,2]; dropped entries have zero gradient.
Phase03 running initial score: 17/21. Lesson07 attempt1 complete: 2/3, meeting the lesson minimum. Lessons remain todo until the full phase passes. Evaluation-mode behavior remains in the review queue.

### Answer history: p03-l08-concept-v1

ID: p03-l08-concept-v1
Phase03 — Deep Learning Core; Lesson08 — Weight Initialization and Training Stability.
Question22/39; lesson question1/3; conceptual.

Hidden neurons start with identical incoming weights and biases, and their outgoing connections are also symmetric. Under deterministic gradient-based training, what problem can this cause?

A) Every hidden neuron immediately receives an infinite gradient.
B) The neurons can remain identical and update together, failing to learn distinct features.
C) The optimizer automatically assigns a different random learning rate to each neuron.
D) Zero biases alone prevent learning even when the neurons' weights differ randomly.


Learner answer: B. Correct answer: B. Result: correct.
Explanation: Symmetric neurons compute identical outputs and can receive identical gradients, preserving their symmetry through updates. Random weight initialization breaks this symmetry; biases can still start at zero.
Phase03 running initial score: 18/22. Lesson08 attempt1: 1/1; incomplete.

### Answer history: p03-l08-application-v1

ID: p03-l08-application-v1
Phase03 — Deep Learning Core; Lesson08 — Weight Initialization and Training Stability.
Question23/39; lesson question2/3; application.

For a wide feed-forward ReLU layer, you want the standard fan-in He initialization under its usual independent, zero-mean weight assumptions. Which weight variance and rationale match it?

A) Var(w)=1, so every input contributes an unscaled unit of variance.
B) Var(w)=1/fan_in**2, so the sum of inputs is always close to zero.
C) Var(w)=2/fan_in, compensating for ReLU discarding the negative half of a symmetric preactivation distribution.
D) Var(w)=fan_in/2, so wider layers receive proportionally larger signals.


Learner answer: C. Correct answer: C. Result: correct.
Explanation: Fan-in He initialization uses weight variance2/fan_in. Under its symmetry and independence assumptions, the factor2 compensates for the halving of the preactivation second moment by ReLU.
Phase03 running initial score: 19/23. Lesson08 attempt1: 2/2; incomplete.

### Answer history: p03-l08-code-v1

ID: p03-l08-code-v1
Phase03 — Deep Learning Core; Lesson08 — Weight Initialization and Training Stability.
Question24/39; lesson question3/3; code tracing.

What standard deviations does this code compute for Xavier-normal and He-normal initialization?

```python
import math
fan_in, fan_out = 8, 24
xavier_std = math.sqrt(2.0 / (fan_in + fan_out))
he_std = math.sqrt(2.0 / fan_in)
print(xavier_std, he_std)
```

A) 0.0625 0.25
B) 0.25 0.5
C) 0.5 0.25
D) 0.125 0.5


Learner answer: A. Correct answer: B. Result: incorrect.
Explanation: The variances are2/32=0.0625 and2/8=0.25. The code takes square roots to obtain standard deviations0.25 and0.5; option A listed the variances instead.
Review: Lesson08 — distinguish initialization variance from the standard deviation passed to a normal sampler.
Phase03 running initial score: 19/24. Lesson08 attempt1 complete: 2/3, meeting the lesson minimum. Lessons remain todo until the full phase passes.

### Answer history: p03-l09-concept-v1

ID: p03-l09-concept-v1
Phase03 — Deep Learning Core; Lesson09 — Learning Rate Schedules and Warmup.
Question25/39; lesson question1/3; conceptual.

What does linear learning-rate warmup do at the start of training?

A) Keeps the learning rate fixed at its maximum until the validation loss stops improving.
B) Starts at the peak learning rate and halves it after every optimizer step.
C) Starts with a small learning rate and gradually increases it toward the target peak.
D) Freezes all model parameters while only updating the validation-set statistics.


Learner answer: B. Correct answer: C. Result: incorrect.
Explanation: Linear warmup gradually increases the learning rate from a small starting value toward the target peak. Starting at the peak and repeatedly halving is decay, not warmup.
Review: Lesson09 — distinguish warmup's initial increase from learning-rate decay.
Phase03 running initial score: 19/25. Lesson09 attempt1: 0/1; incomplete.

### Answer history: p03-l09-application-v1

ID: p03-l09-application-v1
Phase03 — Deep Learning Core; Lesson09 — Learning Rate Schedules and Warmup.
Question26/39; lesson question2/3; application.

Your schedule is defined in optimizer-update steps, with100 warmup updates. You accumulate gradients over4 microbatches before each optimizer update; how should the schedule counter advance?

A) Advance once per microbatch, so warmup ends after25 optimizer updates.
B) Advance once per optimizer update, so warmup spans400 microbatches.
C) Advance only when validation loss improves, regardless of optimizer updates.
D) Advance once per epoch, regardless of the number of optimizer updates.


Learner answer: B. Correct answer: B. Result: correct.
Explanation: The schedule's unit is optimizer updates, so its counter advances only when an update occurs. With4 microbatches per update,100 warmup updates span400 microbatches.
Phase03 running initial score: 20/26. Lesson09 attempt1: 1/2; incomplete.

### Answer history: p03-l09-code-v1

ID: p03-l09-code-v1
Phase03 — Deep Learning Core; Lesson09 — Learning Rate Schedules and Warmup.
Question27/39; lesson question3/3; code tracing.

What learning rates does this warmup-plus-cosine schedule print at steps10 and60?

```python
import math

def lr(step):
    peak, floor = 0.1, 0.01
    warmup, total = 20, 100
    if step < warmup:
        return peak * step / warmup
    progress = (step - warmup) / (total - warmup)
    return floor + 0.5 * (peak - floor) * (1 + math.cos(math.pi * progress))

print(round(lr(10), 3), round(lr(60), 3))
```

A) 0.05 0.055
B) 0.05 0.05
C) 0.1 0.055
D) 0.05 0.01


Learner answer: A. Correct answer: A. Result: correct.
Explanation: Step10 is halfway through warmup, giving0.1*10/20=0.05. At step60, cosine progress=(60-20)/(100-20)=0.5, so lr=0.01+0.5*(0.1-0.01)=0.055.
Phase03 running initial score: 21/27. Lesson09 attempt1 complete: 2/3, meeting the lesson minimum. Lessons remain todo until the full phase passes. Warmup versus decay remains in the review queue.

### Answer history: p03-l10-concept-v1

ID: p03-l10-concept-v1
Phase03 — Deep Learning Core; Lesson10 — Build Your Own Mini Framework.
Question28/39; lesson question1/3; conceptual.

A Sequential container runs modules A, then B, then C during its forward pass. In what order should its explicit backward pass call the modules, and why?

A) A, B, C; gradients follow the same direction as input values.
B) C, B, A; each module transforms the upstream gradient into a gradient for the preceding module.
C) B, A, C; trainable modules must always run before activations.
D) Any order; cached forward values make all module gradients independent.


Learner answer: B. Correct answer: B. Result: correct.
Explanation: The backward pass reverses the forward composition. Each module uses the gradient from its successor to compute gradients for its own parameters and inputs, passing the input gradient to the preceding module.
Phase03 running initial score: 22/28. Lesson10 attempt1: 1/1; incomplete.

### Answer history: p03-l10-application-v1

ID: p03-l10-application-v1
Phase03 — Deep Learning Core; Lesson10 — Build Your Own Mini Framework.
Question29/39; lesson question2/3; application.

Your mini framework accumulates parameter gradients with +=. To optimize the mean loss of a batch by processing one sample at a time, which procedure is correct?

A) Zero gradients before every sample, backpropagate all samples, and step once after the batch.
B) Keep all previous batches' gradients, sum the current gradients, and step after every sample.
C) Zero gradients once per batch, accumulate each sample's gradients, divide by batch size, and step once.
D) Update weights after every sample, then average the final weights to recover the exact batch gradient update.


Learner answer: C. Correct answer: C. Result: correct.
Explanation: Clear gradients once for the batch, accumulate all sample contributions at unchanged parameter values, average by the actual batch size, then update once. Clearing per sample discards prior contributions; stepping per sample changes the parameter point.
Phase03 running initial score: 23/29. Lesson10 attempt1: 2/2; incomplete.

### Answer history: p03-l10-code-v1

ID: p03-l10-code-v1
Phase03 — Deep Learning Core; Lesson10 — Build Your Own Mini Framework.
Question30/39; lesson question3/3; code tracing.

A Linear layer has one output, weights [2,-1], and cached input [3,4]. With upstream gradient0.5 and all parameter gradients initially zero, what are the weight gradients, bias gradient, and input gradients after backward?

```python
weights = [2.0, -1.0]
x = [3.0, 4.0]
g = 0.5
weight_grads = [g * v for v in x]
bias_grad = g
input_grads = [g * w for w in weights]
print(weight_grads, bias_grad, input_grads)
```

A) [1.0,-0.5], 0.5, [1.5,2.0]
B) [1.5,2.0], 1.0, [1.0,-0.5]
C) [3.0,4.0], 0.5, [2.0,-1.0]
D) [1.5,2.0], 0.5, [1.0,-0.5]


Learner answer: D. Correct answer: D. Result: correct.
Explanation: For y=w dot x+b and upstream gradient0.5, dL/dw=0.5*x=[1.5,2], dL/db=0.5, and dL/dx=0.5*w=[1,-0.5].
Phase03 running initial score: 24/30. Lesson10 attempt1 complete: 3/3. Lessons remain todo until the full phase passes.

### Answer history: p03-l11-concept-v1

ID: p03-l11-concept-v1
Phase03 — Deep Learning Core; Lesson11 — Introduction to PyTorch.
Question31/39; lesson question1/3; conceptual.

What is the distinction between model.eval() and torch.no_grad() in the lesson's inference pattern?

A) Both disable dropout, freeze BatchNorm statistics, and disable gradient recording identically.
B) model.eval() clears parameter gradients; torch.no_grad() updates BatchNorm running statistics.
C) model.eval() changes mode-dependent layer behavior; torch.no_grad() disables gradient recording in its context.
D) model.eval() moves tensors to the GPU; torch.no_grad() moves them back to the CPU.


Learner answer: C. Correct answer: C. Result: correct.
Explanation: eval changes mode-dependent behavior such as dropout and BatchNorm. no_grad disables gradient recording in its scope; it does not itself set evaluation mode, clear stored gradients, or move tensors.
Phase03 running initial score: 25/31. Lesson11 attempt1: 1/1; incomplete.

### Answer history: p03-l11-application-v1

ID: p03-l11-application-v1
Phase03 — Deep Learning Core; Lesson11 — Introduction to PyTorch.
Question32/39; lesson question2/3; application.

Your ten-class classifier ends with nn.Linear(hidden_dim,10), and you train using nn.CrossEntropyLoss() with integer class-index targets. What should you pass as the loss's prediction input?

A) The raw logits from the linear layer, without applying softmax first.
B) The class indices returned by argmax over the logits.
C) The probabilities after applying softmax twice for numerical stability.
D) The target labels converted to floating-point values, instead of model outputs.


Learner answer: C. Correct answer: A. Result: incorrect.
Explanation: CrossEntropyLoss expects raw logits and internally combines log-softmax with negative log-likelihood. Applying softmax beforehand changes the input and gradients; applying it twice does not improve numerical stability.
Review: Lesson11 — pass raw logits to CrossEntropyLoss, not softmax probabilities or argmax labels.
Phase03 running initial score: 25/32. Lesson11 attempt1: 1/2; incomplete.

### Answer history: p03-l11-code-v1

ID: p03-l11-code-v1
Phase03 — Deep Learning Core; Lesson11 — Introduction to PyTorch.
Question33/39; lesson question3/3; code tracing.

What does this code print? Each loss is computed from a fresh graph, and x.grad is not cleared between the two backward calls.

```python
import torch
x = torch.tensor(2.0, requires_grad=True)
(x * x).backward()
(3 * x).backward()
print(x.grad.item())
```

A) 3.0
B) 4.0
C) 6.0
D) 7.0


Learner answer: D. Correct answer: D. Result: correct.
Explanation: The first backward contributes2*x=4; the second contributes3. Because the leaf gradient is not cleared, x.grad accumulates to7. The losses use fresh graphs, so no retained graph is needed here.
Phase03 running initial score: 26/33. Lesson11 attempt1 complete: 2/3, meeting the lesson minimum. Lessons remain todo until the full phase passes. CrossEntropyLoss input remains in the review queue.

### Answer history: p03-l12-concept-v1

ID: p03-l12-concept-v1
Phase03 — Deep Learning Core; Lesson12 — Introduction to JAX.
Question34/39; lesson question1/3; conceptual.

In the lesson's functional JAX training pattern, how are model parameters and optimizer state managed across updates?

A) They are hidden global variables that JIT automatically mutates after each call.
B) They are passed into the training function, which returns updated parameters and state.
C) Gradients are always stored in each parameter array's .grad attribute until zero_grad is called.
D) The optimizer reconstructs all parameter values from scratch after every forward pass.


Learner answer: C. Correct answer: B. Result: incorrect.
Explanation: The functional training step receives parameters and optimizer state explicitly and returns their updated versions. JAX gradients are returned by function transformations such as grad or value_and_grad, not accumulated in parameter-array .grad attributes.
Review: Lesson12 — distinguish JAX explicit input/output state and returned gradients from PyTorch leaf .grad accumulation.
Phase03 running initial score: 26/34. Lesson12 attempt1: 0/1; incomplete.

### Answer history: p03-l12-application-v1

ID: p03-l12-application-v1
Phase03 — Deep Learning Core; Lesson12 — Introduction to JAX.
Question35/39; lesson question2/3; application.

You add dropout to a functional JAX training loop and want a fresh reproducible mask on each step. How should you manage the PRNG key?

A) Reuse the same key for every random call, relying on an implicit global counter to advance it.
B) Recreate the same seed on each step so the key produces a different mask automatically.
C) Split the carried key into a new carried key and a subkey; use the subkey for that step's dropout.
D) Store randomness in a Python global variable that the compiled function mutates on each execution.


Learner answer: c (normalized C). Correct answer: C. Result: correct.
Explanation: Explicit key splitting provides a subkey for the current step and a new key to carry forward. Reusing the same key for the same random operation reproduces the same result rather than implicitly advancing global state.
Phase03 running initial score: 27/35. Lesson12 attempt1: 1/2; incomplete.

### Answer history: p03-l12-code-v1

ID: p03-l12-code-v1
Phase03 — Deep Learning Core; Lesson12 — Introduction to JAX.
Question36/39; lesson question3/3; code tracing.

What per-example gradients does this compute? jax.grad differentiates loss with respect to its first argument w, and in_axes=None shares w across examples.

```python
import jax
import jax.numpy as jnp

def loss(w, x, y):
    return (w * x - y)**2

per_example_grad = jax.vmap(jax.grad(loss), in_axes=(None, 0, 0))
grads = per_example_grad(2.0, jnp.array([1.0, 3.0]),
                        jnp.array([0.0, 1.0]))
print(grads.tolist())
```

A) [4.0, 30.0]
B) [2.0, 5.0]
C) [17.0, 17.0]
D) [4.0, 10.0]


Learner answer: A. Correct answer: A. Result: correct.
Explanation: Each gradient is2*(w*x-y)*x. With w=2, the two examples give2*(2-0)*1=4 and2*(6-1)*3=30. vmap returns per-example gradients rather than their mean.
Phase03 running initial score: 28/36. Lesson12 attempt1 complete: 2/3, meeting the lesson minimum. Lessons remain todo until the full phase passes. JAX explicit state remains in the review queue.

### Answer history: p03-l13-concept-v1

ID: p03-l13-concept-v1
Phase03 — Deep Learning Core; Lesson13 — Debugging Neural Networks.
Question37/39; lesson question1/3; conceptual.

What does successfully overfitting one small, fixed batch primarily establish during debugging?

A) The model generalizes to unseen examples from any distribution.
B) The training and test datasets contain no duplicates or label leakage.
C) The model and training path can fit those examples, providing a useful basic sanity check.
D) The architecture and learning rate are optimal for full-dataset training.


Learner answer: C. Correct answer: C. Result: correct.
Explanation: Fitting a small fixed batch verifies that the tested model and training path can learn those examples. It does not establish generalization, rule out all data issues, or prove optimal hyperparameters.
Phase03 running initial score: 29/37. Lesson13 attempt1: 1/1; incomplete.

### Answer history: p03-l13-application-v1

ID: p03-l13-application-v1
Phase03 — Deep Learning Core; Lesson13 — Debugging Neural Networks.
Question38/39; lesson question2/3; application.

You compare backpropagation gradients with central finite differences, but dropout draws a new mask for every loss evaluation. What should you do before interpreting the discrepancy as a backward-pass bug?

A) Disable dropout or hold its mask fixed across analytical and numerical evaluations so both differentiate the same deterministic function.
B) Increase the learning rate until the numerical gradient agrees with backpropagation.
C) Update the weights between loss(w+eps) and loss(w-eps) to include optimizer behavior.
D) Keep changing masks and choose whichever numerical gradient is closest to backpropagation.


Learner answer: A. Correct answer: A. Result: correct.
Explanation: Gradient checking must compare derivatives of the same function. Disable stochastic dropout or reuse an identical mask and keep inputs and other state fixed; otherwise random mask changes contaminate the finite difference.
Phase03 running initial score: 30/38. Lesson13 attempt1: 2/2; incomplete.

### Answer history: p03-l13-code-v1

ID: p03-l13-code-v1
Phase03 — Deep Learning Core; Lesson13 — Debugging Neural Networks.
Question39/39; lesson question3/3; code tracing.

What numerical gradient and relative difference does this central-difference check print, rounded to three decimals?

```python
def loss(w):
    return (2*w - 1)**2

w, eps = 1.0, 1e-4
numerical = (loss(w + eps) - loss(w - eps)) / (2*eps)
analytical = 2 * (2*w - 1)  # candidate backward implementation
relative = abs(analytical - numerical) / max(
    abs(analytical), abs(numerical), 1e-8
)
print(round(numerical, 3), round(relative, 3))
```

A) 2.0 0.0
B) 4.0 0.5
C) 4.0 0.0
D) 2.0 1.0


Learner answer: B. Correct answer: B. Result: correct.
Explanation: The true derivative is4*(2*w-1)=4 at w=1. The candidate backward expression omits the inner derivative2 and yields2, giving relative difference abs(2-4)/4=0.5.
Phase03 initial score: 31/39 (79.49%). Lesson13 attempt1 complete: 3/3.

### Phase03 initial assessment results and remediation

- Initial lesson scores01–13:3,2,2,3,2,3,2,2,2,3,2,2,3. Sum31/39; all lesson minima met, but below required34/39. Phase and all13 lessons remain todo.
- Misses: L02 affine composition Q4; L03 shared gradient accumulation Q7; L05 label smoothing Q13; L07 evaluation mode Q20; L08 variance versus standard deviation Q24; L09 warmup Q25; L11 logits for cross-entropy Q32; L12 explicit JAX state Q34.
- Default remediation: fresh three-question sets, preserving initial evidence and using the latest complete set per lesson. Start Lesson02 attempt2; incomplete retakes do not change effective score.

### Answer history: p03-l02-concept-v2

ID: p03-l02-concept-v2
Phase03 — Deep Learning Core; Lesson02 — Multi-Layer Networks and Forward Pass.
Retake attempt2, question1/3; conceptual.

A network uses h=W1@x+b1 followed by y=W2@h+b2, with no activation between them. Which replacement produces exactly the same outputs for every x?

A) y=(W2+W1)@x+(b1+b2), whenever the additions have matching shapes.
B) y=(W1@W2)@x+b2, because matrix multiplication order does not matter.
C) y=(W2@W1)@x+(W2@b1+b2), a single affine layer.
D) No single affine layer can reproduce two affine layers, even with compatible shapes.


Learner answer: C. Correct answer: C. Result: correct.
Explanation: Substitute h into y and distribute W2: the effective weight is W2@W1 and bias is W2@b1+b2. No intervening nonlinearity means the composition remains affine.
Lesson02 retake attempt2 running score:1/1. Phase03 latest complete sets remain31/39 until the full retake set is complete. Cumulative scored responses40, correct32.

### Answer history: p03-l02-application-v2

ID: p03-l02-application-v2
Phase03 — Deep Learning Core; Lesson02 — Multi-Layer Networks and Forward Pass.
Retake attempt2, question2/3; application.

A fully connected 3-4-2 network has a bias for each hidden and output neuron. How many trainable scalar parameters does it contain?

A) 20: count the weights, since biases are not trainable.
B) 26: 3*4+4 weights and biases in the hidden layer, plus4*2+2 in the output layer.
C) 24: count both weight matrices and only the hidden biases.
D) 9: one trainable scalar for each input, hidden, and output node.


Learner answer: B. Correct answer: B. Result: correct.
Explanation: Hidden layer has3*4 weights and4 biases; output layer has4*2 weights and2 biases. Total16+10=26 trainable scalar parameters.
Lesson02 retake attempt2 running score:2/2. Phase03 latest complete sets remain31/39 until the full retake set is complete. Cumulative scored responses41, correct33.

### Answer history: p03-l02-code-v2

ID: p03-l02-code-v2
Phase03 — Deep Learning Core; Lesson02 — Multi-Layer Networks and Forward Pass.
Retake attempt2, question3/3; code tracing.

What does this two-layer forward pass print? The hidden activation is ReLU, and the output layer is affine.

```python
x = [2.0, -1.0]
W1 = [[1.0, 1.0], [-1.0, 2.0]]
b1 = [0.0, 1.0]
h = [max(0.0, sum(w*v for w, v in zip(row, x)) + b)
     for row, b in zip(W1, b1)]
y = 3.0*h[0] - 2.0*h[1] + 0.5
print(h, y)
```

A) [1.0,-3.0], 9.5
B) [0.0,1.0], -1.5
C) [1.0,0.0], 3.5
D) [1.0,0.0], 3.0


Learner answer: C. Correct answer: C. Result: correct.
Explanation: Hidden preactivations are1 and-3; ReLU gives[1,0]. Output=3*1-2*0+0.5=3.5.
Lesson02 retake attempt2 complete:3/3, replacing the initial2/3 for the effective phase score. Phase03 latest complete sets32/39 (82.05%); needs34/39. Initial results preserved. Cumulative scored responses42, correct34.
Affine composition answered correctly in retake; retain for spaced recall. All lessons remain todo until the whole phase passes.

### Answer history: p03-l03-concept-v2

ID: p03-l03-concept-v2
Phase03 — Deep Learning Core; Lesson03 — Backpropagation from Scratch.
Retake attempt2, question1/3; conceptual.

Why does the lesson's autograd engine traverse a reverse topological ordering during backward?

A) To update each parameter immediately after processing its first outgoing path.
B) To ensure a node has received all downstream gradient contributions before propagating its gradient to its inputs.
C) To recompute each node's random initialization before differentiating it.
D) To avoid summing gradient contributions when a value is reused.


Learner answer: B. Correct answer: B. Result: correct.
Explanation: Reverse topological traversal processes consumers before their inputs, so all downstream contributions reach a shared node before its backward rule propagates the accumulated gradient further.
Lesson03 retake attempt2 running score:1/1. Phase03 latest complete sets remain32/39 until the full retake set is complete. Cumulative scored responses43, correct35.

### Answer history: p03-l03-application-v2

ID: p03-l03-application-v2
Phase03 — Deep Learning Core; Lesson03 — Backpropagation from Scratch.
Retake attempt2, question2/3; application.

A shared intermediate h feeds two branches of the loss. One branch contributes dL/dh=2 and the other contributes dL/dh=-0.5. If dh/dw=3, what contribution should be propagated to w through h?

A) 6.0, using only the branch with the largest magnitude.
B) -1.5, using only the last branch processed.
C) 4.5, summing the branch contributions before multiplying by dh/dw.
D) 1.5, summing the branches but ignoring the local derivative.


Learner answer: C. Correct answer: C. Result: correct.
Explanation: The accumulated gradient at h is2-0.5=1.5. Applying the local derivative gives dL/dw=1.5*3=4.5 through this intermediate.
Lesson03 retake attempt2 running score:2/2. Phase03 latest complete sets remain32/39 until the full retake set is complete. Cumulative scored responses44, correct36.

### Answer history: p03-l03-code-v2

ID: p03-l03-code-v2
Phase03 — Deep Learning Core; Lesson03 — Backpropagation from Scratch.
Retake attempt2, question3/3; code tracing.

Using the lesson's Value engine with gradients initially zero, what are w.grad and b.grad after backward?

```python
w = Value(2.0)
b = Value(-1.0)
x = Value(3.0)
z = w * x + b
loss = z * z
loss.backward()
print(w.grad, b.grad)
```

A) 10.0 10.0
B) 30.0 6.0
C) 15.0 5.0
D) 30.0 10.0


Learner answer: D. Correct answer: D. Result: correct.
Explanation: z=2*3-1=5 and dL/dz=2*z=10. Hence dL/dw=10*x=30 and dL/db=10.
Lesson03 retake attempt2 complete:3/3, replacing the initial2/3 for the effective phase score. Phase03 latest complete sets33/39 (84.62%); needs34/39. Initial results preserved. Cumulative scored responses45, correct37.
Shared-gradient accumulation answered correctly in retake; retain for spaced recall. All lessons remain todo until the whole phase passes.

### Answer history: p03-l05-concept-v2

ID: p03-l05-concept-v2
Phase03 — Deep Learning Core; Lesson05 — Loss Functions.
Retake attempt2, question1/3; conceptual.

For four classes, label smoothing uses q=(1-alpha)*one_hot+alpha/4. With alpha=0.2 and true class index1 (zero-indexed), what is the target distribution q?

A) [0.05,0.85,0.05,0.05]
B) [0.0,0.8,0.0,0.0]
C) [0.2,0.4,0.2,0.2]
D) [0.25,0.25,0.25,0.25]


Learner answer: A. Correct answer: A. Result: correct.
Explanation: Each class receives alpha/4=0.05, and the true class additionally receives1-alpha=0.8, yielding [0.05,0.85,0.05,0.05]. The target distribution sums to1.
Lesson05 retake attempt2 running score:1/1. Phase03 latest complete sets remain33/39 until the full retake set is complete. Cumulative scored responses46, correct38.

### Answer history: p03-l05-application-v2

ID: p03-l05-application-v2
Phase03 — Deep Learning Core; Lesson05 — Loss Functions.
Retake attempt2, question2/3; application.

You train embeddings from anchor-positive pairs with several negative candidates per anchor. Which InfoNCE setup correctly rewards identifying the positive among all candidates?

A) Put only the positive's exponential similarity in both numerator and denominator.
B) Minimize the positive similarity while maximizing similarities to the negative candidates.
C) Use -log(exp(sim_pos/tau)/(exp(sim_pos/tau)+sum(exp(sim_neg/tau)))).
D) Replace every candidate similarity with the same constant to remove the influence of negatives.


Learner answer: C. Correct answer: C. Result: correct.
Explanation: InfoNCE maximizes the positive candidate's softmax probability relative to the positive and all negative candidates. The denominator includes the positive term as well as the negatives.
Lesson05 retake attempt2 running score:2/2. Phase03 latest complete sets remain33/39 until the full retake set is complete. Cumulative scored responses47, correct39.

### Answer history: p03-l05-code-v2

ID: p03-l05-code-v2
Phase03 — Deep Learning Core; Lesson05 — Loss Functions.
Retake attempt2, question3/3; code tracing.

For a single example, sigmoid produces p=0.1 and the target is1. What gradient with respect to the logit z does this binary cross-entropy chain-rule calculation produce?

```python
p, y = 0.1, 1.0
dloss_dp = -y/p + (1-y)/(1-p)
dp_dz = p*(1-p)
dloss_dz = dloss_dp * dp_dz
print(round(dloss_dz, 2))
```

A) -10.0
B) -0.9
C) -0.09
D) 0.9


Learner answer: B. Correct answer: B. Result: correct.
Explanation: dL/dp=-10 and dp/dz=0.09, giving dL/dz=-0.9. Equivalently, sigmoid plus binary cross-entropy gives p-y.
Lesson05 retake attempt2 complete:3/3, replacing initial2/3 for effective scoring. Phase03 latest complete sets34/39 (87.18%). Initial31/39 preserved. Cumulative scored responses48, correct40.

### Phase03 mastery completion — 2026-10-24

- Passed: latest complete lesson sets34/39 (87.18%), meeting required34/39. Every lesson meets minimum2/3.
- Initial31/39 (79.49%) preserved. Lessons02,03,05 fresh retakes each3/3. All questions, answers, and explanations preserved.
- Latest lesson scores01–13:3,3,3,3,3,3,2,2,2,3,2,2,3.
- All13 lessons marked done by quiz-based mastery; implementation labs not performed in this assessment. One normal progress entry per lesson added to LEARNING.md.
- Residual review: evaluation mode (L07), initialization variance versus standard deviation (L08), warmup versus decay (L09), raw logits for cross-entropy (L11), and JAX explicit state (L12). Resolved retake topics remain for spaced recall.
- Next: Phase04 — Computer Vision, Lesson01, question1/84, not yet presented. No pending answer at phase boundary.


