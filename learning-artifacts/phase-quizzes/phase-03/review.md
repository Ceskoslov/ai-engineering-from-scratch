# Phase 03 — deep-learning-core Review Summary

[All phases](../progress.md)

- Status: **Done / Passed**; passed on 2026-10-24; coverage: **13 lessons**.
- Initial score: **31/39**; final effective score: **34/39 (87.18%)**.
- Cumulative responses: 48, with 40 correct; **8 initial/retake mistakes** retained. Cumulative responses include retakes and are not the mastery-score denominator.
- Pass criteria: effective phase score ≥85% and final score ≥2/3 in every lesson; all criteria met. Completion basis: quiz-based mastery; implementation labs were not performed in this assessment.

## Weak points and review priorities

- L07: use eval mode for inference to disable dropout and reuse BatchNorm statistics. L08: initialization standard deviation is the square root of variance. L09: warmup increases the learning rate from a small value to its peak.
- L11: CrossEntropyLoss takes raw logits. L12: JAX explicitly receives and returns parameters and optimizer state; gradients do not automatically accumulate in .grad attributes.
- L02 nonlinear expressiveness, L03 summing shared-node gradients before parameter updates, and L05 label smoothing versus temperature scaling all reached 3/3 in retakes; retain them for spaced recall.

## Lessons with mistakes and retake outcomes

Lessons with mistakes or retakes are listed below, along with any additional rows retained from the original ledger. Unlisted lessons scored 3/3 initially and finally. A final 3/3 indicates correction in a later assessment where applicable; retain those topics for spaced recall. Lessons at 2/3 remain review priorities.

| Lesson | Initial score | Final effective score / retake |
|---|---|---|
| [The Perceptron](../../../phases/03-deep-learning-core/01-the-perceptron/docs/en.md) | attempt1: 3/3 | 3/3 |
| [Multi-Layer Networks and Forward Pass](../../../phases/03-deep-learning-core/02-multi-layer-networks/docs/en.md) | attempt1: 2/3 | attempt2: 3/3 |
| [Backpropagation from Scratch](../../../phases/03-deep-learning-core/03-backpropagation/docs/en.md) | attempt1: 2/3 | attempt2: 3/3 |
| [Activation Functions](../../../phases/03-deep-learning-core/04-activation-functions/docs/en.md) | attempt1: 3/3 | 3/3 |
| [Loss Functions](../../../phases/03-deep-learning-core/05-loss-functions/docs/en.md) | attempt1: 2/3 | attempt2: 3/3 |
| [Optimizers](../../../phases/03-deep-learning-core/06-optimizers/docs/en.md) | attempt1: 3/3 | 3/3 |
| [Regularization](../../../phases/03-deep-learning-core/07-regularization/docs/en.md) | attempt1: 2/3 | 2/3 |
| [Weight Initialization and Training Stability](../../../phases/03-deep-learning-core/08-weight-initialization/docs/en.md) | attempt1: 2/3 | 2/3 |
| [Learning Rate Schedules and Warmup](../../../phases/03-deep-learning-core/09-learning-rate-schedules/docs/en.md) | attempt1: 2/3 | 2/3 |
| [Build Your Own Mini Framework](../../../phases/03-deep-learning-core/10-mini-framework/docs/en.md) | attempt1: 3/3 | 3/3 |
| [Introduction to PyTorch](../../../phases/03-deep-learning-core/11-intro-to-pytorch/docs/en.md) | attempt1: 2/3 | 2/3 |
| [Introduction to JAX](../../../phases/03-deep-learning-core/12-intro-to-jax/docs/en.md) | attempt1: 2/3 | 2/3 |
| [Debugging Neural Networks](../../../phases/03-deep-learning-core/13-debugging-neural-networks/docs/en.md) | attempt1: 3/3 | 3/3 |

## Condensed mistake records

Question IDs, prompts, selected wrong answers, correct answers, and explanations are retained. Other distractors, correct-only questions, and per-response score logs are omitted. Prompts and explanations retain their original English wording. These are historical initial/retake mistakes, not pending retake requirements.

### p03-l02-concept-v1

What happens if every activation in a multi-layer network is replaced with the identity function?

- Learner answer: B — Each additional layer creates a new nonlinear decision boundary through matrix multiplication alone.
- Correct answer: A — The network becomes equivalent to one affine transformation, regardless of its depth.
- Explanation: Composing affine maps yields another affine map: W2*(W1*x+b1)+b2=(W2*W1)*x+(W2*b1+b2). Identity activations introduce no nonlinearity; depth alone therefore cannot produce a nonlinear mapping.

### p03-l03-concept-v1

Why must an autograd engine accumulate gradient contributions with += when a value is used along multiple paths to the loss?

- Learner answer: B — Each path requires updating the parameter before processing the next path.
- Correct answer: A — The total derivative is the sum of the contributions from all paths through that value.
- Explanation: The multivariable chain rule sums contributions from every path to a shared value. Backpropagation computes gradients at the forward pass's parameter values; the optimizer updates parameters afterward, not between paths.

### p03-l05-concept-v1

What does label smoothing do to a one-hot target distribution when training with categorical cross-entropy?

- Learner answer: C — Divides the logits by a temperature while leaving the target distribution unchanged.
- Correct answer: A — Mixes it with a uniform distribution, assigning some target probability to other classes.
- Explanation: Label smoothing changes the target to (1-alpha)*one_hot + alpha/K for K classes. Dividing logits by a temperature changes the predicted distribution instead and does not change the targets.

### p03-l07-application-v1

A trained model uses inverted dropout and BatchNorm with stored running statistics. During ordinary inference, predictions vary because dropout is still active and BatchNorm is using the incoming batch. What is the appropriate fix?

- Learner answer: C — Refit BatchNorm separately on every request and increase dropout to stabilize outputs.
- Correct answer: A — Switch to evaluation mode: disable dropout and use BatchNorm's stored running statistics.
- Explanation: Ordinary inference should disable dropout and use BatchNorm's stored running statistics. Refitting statistics per request makes outputs depend on the incoming batch, and increasing dropout adds randomness rather than removing it. Learning rate and autograd settings do not themselves switch these layer behaviors.

### p03-l08-code-v1

What standard deviations does this code compute for Xavier-normal and He-normal initialization?

```python
import math
fan_in, fan_out = 8, 24
xavier_std = math.sqrt(2.0 / (fan_in + fan_out))
he_std = math.sqrt(2.0 / fan_in)
print(xavier_std, he_std)
```

- Learner answer: A — 0.0625 0.25
- Correct answer: B — 0.25 0.5
- Explanation: The variances are2/32=0.0625 and2/8=0.25. The code takes square roots to obtain standard deviations0.25 and0.5; option A listed the variances instead.

### p03-l09-concept-v1

What does linear learning-rate warmup do at the start of training?

- Learner answer: B — Starts at the peak learning rate and halves it after every optimizer step.
- Correct answer: C — Starts with a small learning rate and gradually increases it toward the target peak.
- Explanation: Linear warmup gradually increases the learning rate from a small starting value toward the target peak. Starting at the peak and repeatedly halving is decay, not warmup.

### p03-l11-application-v1

Your ten-class classifier ends with nn.Linear(hidden_dim,10), and you train using nn.CrossEntropyLoss() with integer class-index targets. What should you pass as the loss's prediction input?

- Learner answer: C — The probabilities after applying softmax twice for numerical stability.
- Correct answer: A — The raw logits from the linear layer, without applying softmax first.
- Explanation: CrossEntropyLoss expects raw logits and internally combines log-softmax with negative log-likelihood. Applying softmax beforehand changes the input and gradients; applying it twice does not improve numerical stability.

### p03-l12-concept-v1

In the lesson's functional JAX training pattern, how are model parameters and optimizer state managed across updates?

- Learner answer: C — Gradients are always stored in each parameter array's .grad attribute until zero_grad is called.
- Correct answer: B — They are passed into the training function, which returns updated parameters and state.
- Explanation: The functional training step receives parameters and optimizer state explicitly and returns their updated versions. JAX gradients are returned by function transformations such as grad or value_and_grad, not accumulated in parameter-array .grad attributes.
