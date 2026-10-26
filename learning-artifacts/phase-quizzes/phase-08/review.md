# Phase 08 review queue

Historical notes are preserved verbatim; some early remediation requests were superseded by later passes. Latest completion status is in [phase progress](progress.md).

- Lesson 01, initial 1/3: distinguish an implicit sampler from a tractable explicit density evaluator (Q1: A; correct B). For exact log-likelihood with invertible architecture, use a normalizing flow (Q2: D; correct C). Histogram boundary trace correct. Requires a fresh full three-question retake.

- Lesson 02, initial 2/3: posterior collapse and KL annealing (Q2: B; correct A). Begin with low KL weight and increase gradually; strong early pressure can suppress input information. Reparameterization and ELBO code trace correct. Lesson minimum met.

- Lesson 04, initial 0/3: conditional discriminator judges realism and compatibility, not reconstruction (Q1: A; correct D). CycleGAN uses two generators and cycle consistency for unpaired data; random Pix2Pix pairings are not aligned targets (Q2: A; correct B). Per-condition means swapped: both errors are 4, so both checks fail despite a matching pooled mean (Q3: A; correct D). Fresh full three-question retake required.

- Lesson 06, initial 2/3: epsilon-prediction DDPM learns sampled Gaussian noise using squared error, not exact marginal log-likelihood (Q1: D; correct C). Compatible DDIM sampler and closed-form forward sample trace correct. Lesson minimum met.

- Lesson01 attempt2: 2/3; lesson minimum now met. Remaining review: joint probability multiplies conditional probabilities; log-probabilities add (retake Q1: A; correct B). Explicit-density requirement and histogram-density trace correct. Original attempt preserved.

- Phase08 passed on 2026-10-26: effective42/45 (93.33%), initial38/45, cumulative43/51. Lesson04 attempt2 scored3/3; all lesson minima now met. Preserve review of chain-rule products versus log sums (Lesson01), KL annealing (Lesson02), paired versus unpaired translation and per-condition checks (Lesson04), and noise prediction versus likelihood evaluation (Lesson06). Implementation labs were not performed in this assessment.
