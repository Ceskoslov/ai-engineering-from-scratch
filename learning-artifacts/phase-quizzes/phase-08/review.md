# Phase 08 — generative-ai Review Summary

[All phases](../progress.md)

- Status: **Done / Passed**; passed on 2026-10-26; coverage: **15 lessons**.
- Initial score: **38/45**; final effective score: **42/45 (93.33%)**.
- Cumulative responses: 51, with 43 correct; **8 initial/retake mistakes** retained. Cumulative responses include retakes and are not the mastery-score denominator.
- Pass criteria: effective phase score ≥85% and final score ≥2/3 in every lesson; all criteria met. Completion basis: quiz-based mastery; implementation labs were not performed in this assessment.

## Weak points and review priorities

- L01: continue reviewing joint probabilities as products of conditionals, with sums applying to log-probabilities. Distinguish implicit samplers from explicit density evaluators; invertible flows support exact likelihood evaluation.
- L02: KL annealing gradually raises a low initial weight to avoid suppressing input information too early. L06: epsilon-prediction DDPM minimizes squared error against sampled noise rather than directly evaluating exact marginal likelihood.
- L04: a conditional discriminator judges realism and condition compatibility. Do not substitute random pairings for paired Pix2Pix data; CycleGAN handles unpaired translation. A matching pooled mean cannot replace per-condition checks. The retake reached 3/3.

## Lessons with mistakes and retake outcomes

Lessons with mistakes or retakes are listed below, along with any additional rows retained from the original ledger. Unlisted lessons scored 3/3 initially and finally. A final 3/3 indicates correction in a later assessment where applicable; retain those topics for spaced recall. Lessons at 2/3 remain review priorities.

| Lesson | Initial score | Final effective score / retake |
|---|---|---|
| [Generative Models — Taxonomy & History](../../../phases/08-generative-ai/01-generative-models-taxonomy-history/docs/en.md) | 1/3 | 2/3 |
| [Autoencoders & Variational Autoencoders (VAE)](../../../phases/08-generative-ai/02-autoencoders-vae/docs/en.md) | 2/3 | 2/3 |
| [Conditional GANs & Pix2Pix](../../../phases/08-generative-ai/04-conditional-gans-pix2pix/docs/en.md) | 0/3 | 3/3 |
| [Diffusion Models — DDPM from Scratch](../../../phases/08-generative-ai/06-diffusion-ddpm-from-scratch/docs/en.md) | 2/3 | 2/3 |

## Condensed mistake records

Question IDs, prompts, selected wrong answers, correct answers, and explanations are retained. Other distractors, correct-only questions, and per-response score logs are omitted. Prompts and explanations retain their original English wording. These are historical initial/retake mistakes, not pending retake requirements.

### p08-l01-a1-q1

What distinguishes an implicit generative model from a model with a tractable explicit density?

- Learner answer: A — It evaluates exact likelihoods but cannot generate new samples.
- Correct answer: B — It generates samples without providing a tractable density evaluator.
- Explanation: An implicit model provides a sampling mechanism without a tractable evaluator for the probability density of a given input.

### p08-l01-a1-q2

You need a generative model that supports exact log-likelihood evaluation and can accept an invertible architecture. Which approach fits?

- Learner answer: D — A sampler that adds noise to random training examples.
- Correct answer: C — A normalizing flow with a tractable Jacobian determinant.
- Explanation: A normalizing flow uses an invertible transformation and the change-of-variables formula to evaluate exact density with a tractable Jacobian determinant. A VAE ELBO is a bound, while the two implicit samplers do not provide exact density evaluation.

### p08-l02-a1-q2

Early in VAE training, the encoder outputs nearly the same standard-normal distribution for every input, and the decoder ignores z. Which adjustment directly addresses this posterior collapse?

- Learner answer: B — Start with a much larger KL weight and keep it fixed.
- Correct answer: A — Start with a small KL weight and gradually increase it.
- Explanation: KL annealing starts with a small beta so reconstruction can encourage informative latents before stronger prior regularization is introduced. Increasing KL pressure immediately can worsen collapse.

### p08-l04-a1-q1

Why does the Pix2Pix discriminator receive both the input image x and the candidate output y?

- Learner answer: A — To reconstruct x from y using the discriminator as a decoder.
- Correct answer: D — To judge whether y looks realistic and is consistent with x.
- Explanation: Conditioning the discriminator on the pair lets it assess compatibility with the input as well as output realism. Seeing only y would not let it directly judge that relationship.

### p08-l04-a1-q2

You have separate collections of summer and winter scenes with no matched image pairs. Which training setup is designed to learn translation between these domains without pairs?

- Learner answer: A — Pix2Pix with an L1 loss against randomly selected winter targets.
- Correct answer: B — CycleGAN with two generators and round-trip consistency losses.
- Explanation: CycleGAN learns mappings in both directions using unpaired domain samples and cycle consistency: F(G(x)) approximates x and G(F(y)) approximates y. Standard Pix2Pix requires aligned pairs; random targets do not provide that correspondence.

### p08-l04-a1-q3

This check compares generated and real means for each condition. What does it print?

```python
real_means = {0: -2.0, 1: 2.0}
generated = {0: [2.0, 2.0], 1: [-2.0, -2.0]}

passed = []
for c in [0, 1]:
    mean_c = sum(generated[c]) / len(generated[c])
    passed.append(abs(mean_c - real_means[c]) < 0.1)

print(passed)
```

- Learner answer: A — [True, True]
- Correct answer: D — [False, False]
- Explanation: Class 0 generates mean +2 instead of -2, and class 1 generates mean -2 instead of +2. Both absolute errors are 4, so both checks fail. The pooled mean is nevertheless correct, showing why conditional checks matter.

### p08-l06-a1-q1

In standard epsilon-prediction DDPM training, what target does the network learn from the noisy sample x_t and timestep t?

- Learner answer: D — The exact marginal log-likelihood of the original sample x_0.
- Correct answer: C — The Gaussian noise epsilon used to construct x_t from x_0.
- Explanation: Training constructs x_t = sqrt(alpha_bar_t) * x_0 + sqrt(1 - alpha_bar_t) * epsilon, then minimizes squared error between the network prediction and the known sampled epsilon.

### p08-l01-a2-q1

An autoregressive model provides normalized conditional probabilities p(x_i | x_<i). How does it obtain the joint probability of a complete sequence?

- Learner answer: A — Average the conditional probabilities across sequence positions.
- Correct answer: B — Multiply the conditional probabilities across sequence positions.
- Explanation: The probability chain rule gives p(x) = product_i p(x_i | x_<i). Equivalently, log p(x) is the sum of the conditional log-probabilities.
