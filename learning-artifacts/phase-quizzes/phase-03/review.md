# Phase 03 review queue

Historical notes are preserved verbatim; some early remediation requests were superseded by later passes. Latest completion status is in [phase progress](progress.md).

- Phase03 Lesson12: JAX training passes parameters and optimizer state explicitly and returns updated values; grad/value_and_grad return gradients rather than accumulating array .grad attributes. Q34 chose C; correct B.

- Phase03 Lesson11: CrossEntropyLoss expects raw logits and internally computes log-softmax plus negative log-likelihood. Applying softmax twice does not add stability and gives the wrong objective. Q32 chose C; correct A.

- Phase03 Lesson09: linear warmup increases the learning rate from small to peak; halving from a peak is decay. Q25 chose B; correct C.

- Phase03 Lesson08: initialization standard deviation is the square root of variance. For fan_in8/fan_out24, Xavier variance0.0625 gives std0.25; He variance0.25 gives std0.5. Q24 chose A; correct B.

- Phase03 Lesson07: ordinary inference uses evaluation mode to disable dropout and reuse BatchNorm running statistics; refitting per request and increasing dropout do not stabilize predictions. Q20 chose C; correct A.

- Phase03 Lesson05 (resolved in retake, keep for spaced recall): label smoothing mixes one-hot targets with a uniform distribution; temperature scaling changes logits and predictions, not targets. Q13 chose C; correct A. Fresh retake attempt2 completed3/3.

- Phase03 Lesson03 (resolved in retake, keep for spaced recall): gradients at a shared value sum contributions from all paths; compute them at the forward-pass parameter values, then update parameters. Q7 chose B; correct A. Fresh retake attempt2 completed3/3.

- Phase03 Lesson02 (resolved in retake, keep for spaced recall): composing affine layers with identity activations gives one affine map; nonlinear activations provide nonlinear expressive power. Q4 chose B; correct A. Fresh retake attempt2 completed3/3.
