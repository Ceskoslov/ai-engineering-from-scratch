# Phase 08 detailed quiz history

Archive: read only when an earlier question or attempt is relevant. [Phase progress](progress.md).

No questions presented yet.

### p08-l01-a1-q1

What distinguishes an implicit generative model from a model with a tractable explicit density?

A) It evaluates exact likelihoods but cannot generate new samples.
B) It generates samples without providing a tractable density evaluator.
C) It must generate each output component in sequential order.
D) It learns only a compressed representation without generating samples.

Learner response: A
Correct answer: B
Result: Incorrect (0/1)
Explanation: An implicit model provides a sampling mechanism without a tractable evaluator for the probability density of a given input.

### p08-l01-a1-q2

You need a generative model that supports exact log-likelihood evaluation and can accept an invertible architecture. Which approach fits?

A) A GAN trained with a discriminator.
B) A VAE evaluated using its ELBO.
C) A normalizing flow with a tractable Jacobian determinant.
D) A sampler that adds noise to random training examples.

Learner response: D
Correct answer: C
Result: Incorrect (0/1)
Explanation: A normalizing flow uses an invertible transformation and the change-of-variables formula to evaluate exact density with a tractable Jacobian determinant. A VAE ELBO is a bound, while the two implicit samplers do not provide exact density evaluation.

### p08-l01-a1-q3

What does this histogram density calculation return?

```python
def histogram_density(samples, x, bin_width=0.25):
    n = len(samples)
    lo, hi = x - bin_width / 2, x + bin_width / 2
    count = sum(1 for s in samples if lo <= s < hi)
    return count / (n * bin_width)

print(histogram_density([-0.5, 0.0, 0.5, 1.0], 0.0, bin_width=1.0))
```

A) 0.25
B) 0.50
C) 0.75
D) 2.00

Learner response: b (B)
Correct answer: B
Result: Correct (1/1)
Explanation: The bin is [-0.5, 0.5): it includes -0.5 and 0.0 but excludes 0.5. The density is 2 / (4 * 1.0) = 0.5.

Lesson 01 initial set: 1/3. Full three-question retake required; lesson remains todo pending phase pass.

### p08-l02-a1-q1

Why does a VAE use the reparameterization z = mu + sigma * epsilon, with epsilon drawn from a standard normal distribution?

A) To remove the need for a KL penalty during training.
B) To make every latent sample equal to the encoder mean.
C) To evaluate the exact marginal likelihood of each input.
D) To let reconstruction gradients flow through mu and sigma.

Learner response: D
Correct answer: D
Result: Correct (1/1)
Explanation: The random epsilon is independent of encoder parameters. With that noise fixed, z is differentiable in mu and sigma, so reconstruction gradients can train the encoder through the sampled latent.

### p08-l02-a1-q2

Early in VAE training, the encoder outputs nearly the same standard-normal distribution for every input, and the decoder ignores z. Which adjustment directly addresses this posterior collapse?

A) Start with a small KL weight and gradually increase it.
B) Start with a much larger KL weight and keep it fixed.
C) Remove reconstruction loss and optimize only the KL term.
D) Replace all sampled latent vectors with a fixed zero vector.

Learner response: B
Correct answer: A
Result: Incorrect (0/1)
Explanation: KL annealing starts with a small beta so reconstruction can encourage informative latents before stronger prior regularization is introduced. Increasing KL pressure immediately can worsen collapse.

### p08-l02-a1-q3

For this one-dimensional latent, what does the function return as (total loss, reconstruction loss, KL)?

```python
import math

def elbo(x, x_hat, mu, log_sigma2, beta=1.0):
    recon = sum((a - b) ** 2 for a, b in zip(x, x_hat))
    kl = 0.5 * sum(
        math.exp(lv) + m * m - lv - 1
        for m, lv in zip(mu, log_sigma2)
    )
    return recon + beta * kl, recon, kl

print(elbo([2.0], [1.0], [2.0], [0.0], beta=0.5))
```

A) (1.0, 1.0, 0.0)
B) (1.5, 1.0, 1.0)
C) (2.0, 1.0, 2.0)
D) (3.0, 1.0, 2.0)

Learner response: C
Correct answer: C
Result: Correct (1/1)
Explanation: Reconstruction is (2 - 1)^2 = 1. With log variance 0, variance is exp(0) = 1, so KL = 0.5 * (1 + 4 - 0 - 1) = 2. Total loss = 1 + 0.5 * 2 = 2.

Lesson 02 initial set: 2/3. Lesson minimum met; status remains todo pending phase pass.

### p08-l03-a1-q1

Why is the non-saturating generator loss -log D(G(z)) commonly used instead of the original minimax generator loss?

A) It supplies a stronger learning signal when the discriminator confidently rejects generated samples.
B) It allows the generator to evaluate the exact likelihood of every generated sample.
C) It guarantees that the generator covers every mode in the training distribution.
D) It eliminates the need to train a discriminator after the first update.

Learner response: A
Correct answer: A
Result: Correct (1/1)
Explanation: For a sigmoid discriminator confidently rejecting fakes, the original minimax generator objective gives weak gradients through the discriminator logit. The non-saturating objective provides a stronger signal; it does not guarantee coverage or give explicit likelihoods.

### p08-l03-a1-q2

Your training data has two well-separated modes, but generated samples cluster around only one mode despite varied noise inputs. What is the most direct diagnosis?

A) Posterior collapse: the encoder distribution has matched its prior.
B) Likelihood overfitting: exact density evaluation has become too costly.
C) Mode collapse: the generator has lost coverage of the data distribution.
D) Reconstruction failure: the decoder cannot recover its paired inputs.

Learner response: C
Correct answer: C
Result: Correct (1/1)
Explanation: Mode collapse means diverse noise inputs yield samples covering only a small part of the real distribution, such as one of its two modes. A standard GAN does not have a VAE posterior or paired reconstruction objective.

### p08-l03-a1-q3

Using this lesson's mode-collapse diagnostic, what does the code print?

```python
samples = [-1.0] * 50 + [1.0] * 450
mode_a = sum(1 for s in samples if s < 0)
mode_b = 500 - mode_a

if min(mode_a, mode_b) < 50:
    print("warning")
else:
    print("no warning")
```

A) warning, because 90% of samples belong to one mode.
B) no warning, because the smaller count equals the threshold.
C) warning, because the smaller count is at most the threshold.
D) no warning, because the diagnostic requires equal mode counts.

Learner response: B
Correct answer: B
Result: Correct (1/1)
Explanation: The counts are 50 and 450. The condition is strictly less than 50, so 50 < 50 is false and the code prints no warning. This threshold result does not establish that the generated distribution matches the data.

Lesson 03 initial set: 3/3. Lesson minimum met; status remains todo pending phase pass.

### p08-l04-a1-q1

Why does the Pix2Pix discriminator receive both the input image x and the candidate output y?

A) To reconstruct x from y using the discriminator as a decoder.
B) To compute an exact conditional likelihood for each image pair.
C) To replace the generator's need for paired training examples.
D) To judge whether y looks realistic and is consistent with x.

Learner response: A
Correct answer: D
Result: Incorrect (0/1)
Explanation: Conditioning the discriminator on the pair lets it assess compatibility with the input as well as output realism. Seeing only y would not let it directly judge that relationship.

### p08-l04-a1-q2

You have separate collections of summer and winter scenes with no matched image pairs. Which training setup is designed to learn translation between these domains without pairs?

A) Pix2Pix with an L1 loss against randomly selected winter targets.
B) CycleGAN with two generators and round-trip consistency losses.
C) An unconditional GAN with neither domain labels nor input images.
D) Pix2Pix with only a larger weight on paired reconstruction loss.

Learner response: A
Correct answer: B
Result: Incorrect (0/1)
Explanation: CycleGAN learns mappings in both directions using unpaired domain samples and cycle consistency: F(G(x)) approximates x and G(F(y)) approximates y. Standard Pix2Pix requires aligned pairs; random targets do not provide that correspondence.

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

A) [True, True]
B) [True, False]
C) [False, True]
D) [False, False]

Learner response: A
Correct answer: D
Result: Incorrect (0/1)
Explanation: Class 0 generates mean +2 instead of -2, and class 1 generates mean -2 instead of +2. Both absolute errors are 4, so both checks fail. The pooled mean is nevertheless correct, showing why conditional checks matter.

Lesson 04 initial set: 0/3. Fresh full three-question retake required; status remains todo pending phase pass.

### p08-l05-a1-q1

In the original StyleGAN, what is the main role of the mapping network from z to w?

A) To classify generated images as real or fake before synthesis.
B) To learn an intermediate latent used to modulate synthesis at multiple resolutions.
C) To reconstruct a specific real image using an exact inverse of the generator.
D) To force every generated image to use identical scale and bias values.

Learner response: B
Correct answer: B
Result: Correct (1/1)
Explanation: The mapping network transforms the input latent z into an intermediate w. Affine projections of w control the synthesis layers, separating the input prior geometry from learned style controls. It is neither a discriminator nor an exact image inverse.

### p08-l05-a1-q2

You lower StyleGAN's truncation parameter psi from 1.0 to 0.5, using w_truncated = w_mean + psi * (w - w_mean). What tradeoff should you expect?

A) Latents move farther from the mean, increasing output diversity.
B) The synthesis network uses fewer layers, reducing inference cost.
C) Latents move toward the mean, reducing diversity and often improving visual quality.
D) The generator gains exact likelihood evaluation for truncated samples.

Learner response: C
Correct answer: C
Result: Correct (1/1)
Explanation: Reducing psi contracts each latent toward the mean w. Truncation trades reduced variation and mode coverage for often cleaner-looking samples; it does not remove synthesis layers or expose exact likelihoods.

### p08-l05-a1-q3

This simplified AdaIN calculation uses population standard deviation and omits epsilon. What does it print?

```python
import math

x = [1.0, 3.0]
scale, bias = 2.0, 5.0
mu = sum(x) / len(x)
sd = math.sqrt(sum((v - mu) ** 2 for v in x) / len(x))
out = [scale * ((v - mu) / sd) + bias for v in x]
print(out)
```

A) [3.0, 7.0]
B) [-2.0, 2.0]
C) [7.0, 11.0]
D) [4.0, 6.0]

Learner response: A
Correct answer: A
Result: Correct (1/1)
Explanation: The mean is 2 and the population standard deviation is 1. Normalization yields [-1, 1]; multiplying by 2 and adding 5 yields [3, 7].

Lesson 05 initial set: 3/3. Lesson minimum met; status remains todo pending phase pass.

### p08-l06-a1-q1

In standard epsilon-prediction DDPM training, what target does the network learn from the noisy sample x_t and timestep t?

A) The discriminator probability that x_t is a real sample.
B) The cumulative noise variance schedule for the entire dataset.
C) The Gaussian noise epsilon used to construct x_t from x_0.
D) The exact marginal log-likelihood of the original sample x_0.

Learner response: d (D)
Correct answer: C
Result: Incorrect (0/1)
Explanation: Training constructs x_t = sqrt(alpha_bar_t) * x_0 + sqrt(1 - alpha_bar_t) * epsilon, then minimizes squared error between the network prediction and the known sampled epsilon.

### p08-l06-a1-q2

You have a trained epsilon-prediction diffusion model and want to reduce sampling steps without retraining its weights. Which approach fits?

A) Train a new student model using progressive distillation.
B) Replace the sampling loop with a compatible DDIM sampler.
C) Increase the number of reverse steps in the DDPM sampler.
D) Remove timestep conditioning from the trained denoiser.

Learner response: B
Correct answer: B
Result: Correct (1/1)
Explanation: A compatible DDIM sampler can reuse the trained noise predictor while sampling with fewer steps. Distillation requires training a student; more reverse steps increase work, and removing time conditioning does not implement a valid faster sampler.

### p08-l06-a1-q3

This code constructs a noisy training sample using the DDPM closed form. What does it print?

```python
import math

x0 = 2.0
alpha_bar = 0.36
epsilon = -1.0
x_t = (math.sqrt(alpha_bar) * x0
       + math.sqrt(1 - alpha_bar) * epsilon)
print(round(x_t, 2))
```

A) -0.32
B) 1.20
C) 2.00
D) 0.40

Learner response: D
Correct answer: D
Result: Correct (1/1)
Explanation: sqrt(0.36) = 0.6 and sqrt(0.64) = 0.8. Thus x_t = 0.6 * 2 + 0.8 * (-1) = 0.4, printed as 0.4.

Lesson 06 initial set: 2/3. Lesson minimum met; status remains todo pending phase pass.

### p08-l07-a1-q1

What is the main computational advantage of latent diffusion over pixel-space diffusion?

A) It performs repeated denoising on a compressed representation, then decodes the result.
B) It replaces every reverse denoising step with a single VAE encoder pass.
C) It removes the need to train a model on noisy data at different timesteps.
D) It guarantees exact pixel reconstruction regardless of the compression strength.

Learner response: A
Correct answer: A
Result: Correct (1/1)
Explanation: The diffusion network operates repeatedly on compressed latents rather than full-resolution pixels, reducing denoising work. A decoder maps the final latent back to an image; compression can lose information and does not remove diffusion training or iterative sampling.

### p08-l07-a1-q2

You are training a latent diffusion denoiser with a frozen VAE. The checkpoint requires a latent scaling factor after encoding, but your data pipeline omits it. What is the appropriate fix?

A) Increase classifier-free guidance to compensate for latent variance.
B) Decode every noisy latent into pixels before each training step.
C) Apply the checkpoint's prescribed scaling consistently in the latent pipeline.
D) Replace the VAE with any other encoder having the same output shape.

Learner response: C
Correct answer: C
Result: Correct (1/1)
Explanation: Latent scaling is part of the checkpoint convention and determines the distribution seen by the denoiser. Apply the required encoding scale and its inverse at decoding consistently; guidance or matching tensor shapes does not repair a latent-distribution mismatch.

### p08-l07-a1-q3

Using the lesson's classifier-free guidance convention, what does this code print?

```python
eps_cond = 2.0
eps_uncond = 1.0
w = 3.0
eps_cfg = (1 + w) * eps_cond - w * eps_uncond
print(eps_cfg)
```

A) 2.0
B) 5.0
C) 3.0
D) 8.0

Learner response: B
Correct answer: B
Result: Correct (1/1)
Explanation: The guided prediction is (1 + 3) * 2 - 3 * 1 = 8 - 3 = 5. Equivalently it is eps_cond + w * (eps_cond - eps_uncond).

Lesson 07 initial set: 3/3. Lesson minimum met; status remains todo pending phase pass.

### p08-l08-a1-q1

Why are ControlNet's connections into the frozen diffusion backbone initialized with zero weights?

A) To prevent the conditioning branch from ever affecting generated images.
B) To make the frozen backbone produce a zero-valued image initially.
C) To force the conditioning branch to learn an exact inverse of the backbone.
D) To start with zero added residual so the pretrained backbone is initially unperturbed.

Learner response: D
Correct answer: D
Result: Correct (1/1)
Explanation: Zero-initialized connections initially add zero to the backbone features. Training can then learn conditioning residuals without an arbitrary initial perturbation to the pretrained network.

### p08-l08-a1-q2

You want generated images to follow a supplied pose skeleton and use a learned brand style, while keeping the base diffusion weights frozen. Which combination fits these two controls?

A) A pose ControlNet for spatial structure and a style LoRA for adaptation.
B) A style LoRA for spatial structure and a pose-free discriminator for adaptation.
C) An unconditional generator for spatial structure and a VAE scaling factor for style.
D) A text tokenizer for spatial structure and a noise schedule for brand identity.

Learner response: A
Correct answer: A
Result: Correct (1/1)
Explanation: A pose-conditioned ControlNet supplies spatial guidance, while a trained style LoRA adds a low-rank adaptation to the frozen base. These address different controls and can be combined with compatible checkpoints.

### p08-l08-a1-q3

This rank-1 LoRA computes W*x + alpha*B*(A*x). What does it print?

```python
x = [2.0, 3.0]
A = [1.0, -1.0]  # one row
B = [2.0, 4.0]   # one column
alpha = 0.5
base = x[:]       # W is the identity matrix
ax = sum(a * v for a, v in zip(A, x))
out = [v + alpha * b * ax for v, b in zip(base, B)]
print(out)
```

A) [0.0, -1.0]
B) [3.0, 5.0]
C) [1.0, 1.0]
D) [2.0, 3.0]

Learner response: C
Correct answer: C
Result: Correct (1/1)
Explanation: A*x = 2 - 3 = -1. The scaled correction is 0.5 * [2, 4] * (-1) = [-1, -2]. Adding it to the base output [2, 3] gives [1, 1].

Lesson 08 initial set: 3/3. Lesson minimum met; status remains todo pending phase pass.

### p08-l09-a1-q1

In SDEdit, what generally happens when you add more noise to the source image before starting reverse denoising?

A) The source is preserved more exactly because the reverse chain is longer.
B) The model gains more freedom to change the image, reducing source fidelity.
C) Only masked pixels change, regardless of whether a mask is supplied.
D) The model no longer needs a learned denoiser to produce an edited image.

Learner response: B
Correct answer: B
Result: Correct (1/1)
Explanation: A higher starting noise level destroys more source information. Reverse denoising then has greater creative freedom but typically preserves less of the original image; this does not inherently enforce a mask.

### p08-l09-a1-q2

You need to remove a small sign from a product photo while keeping all pixels outside the edit region identical. Which workflow directly fits?

A) Generate a new image from a detailed text description of the photo.
B) Run whole-image SDEdit from a near-pure-noise starting point.
C) Extend the canvas and regenerate only the newly added border.
D) Inpaint a mask covering the sign, then composite the edited region onto the original.

Learner response: D
Correct answer: D
Result: Correct (1/1)
Explanation: Masked inpainting targets the sign, and final compositing with the original explicitly preserves outside-mask pixels. Whole-image generation or high-noise SDEdit can change the product and background; outpainting targets added canvas.

### p08-l09-a1-q3

Here True marks a region to regenerate. What does this final compositing step print?

```python
original = [10, 20, 30, 40]
generated = [11, 22, 33, 44]
mask = [False, True, False, True]

result = [g if m else o
          for o, g, m in zip(original, generated, mask)]
print(result)
```

A) [10, 22, 30, 44]
B) [11, 20, 33, 40]
C) [11, 22, 33, 44]
D) [10, 20, 30, 40]

Learner response: A
Correct answer: A
Result: Correct (1/1)
Explanation: The expression selects generated values where the mask is True (positions 1 and 3) and original values where it is False (positions 0 and 2), yielding [10, 22, 30, 44].

Lesson 09 initial set: 3/3. Lesson minimum met; status remains todo pending phase pass.

### p08-l10-a1-q1

Why does a video diffusion model couple information across frames instead of generating each frame independently with an image model?

A) To eliminate the need for spatial compression of high-resolution frames.
B) To guarantee physically correct motion for arbitrarily long clips.
C) To model temporal relationships and reduce inconsistent appearance across frames.
D) To replace denoising with exact likelihood evaluation of each frame.

Learner response: C
Correct answer: C
Result: Correct (1/1)
Explanation: Cross-frame coupling lets the model learn motion and preserve related content across time. Independent image generation lacks those dependencies and can flicker. Coupling does not guarantee physics or eliminate compression and denoising.

### p08-l10-a1-q2

Full attention over all spatiotemporal patches exceeds your video model's memory budget. Which change reduces attention cost while retaining spatial and temporal interactions?

A) Replace all temporal position embeddings with the same constant.
B) Generate each frame independently and discard cross-frame interactions.
C) Increase the number of patches by reducing every patch dimension.
D) Factorize attention into within-frame spatial and across-frame temporal passes.

Learner response: D
Correct answer: D
Result: Correct (1/1)
Explanation: Factorized attention separates within-frame spatial attention from temporal attention across frames, reducing the cost relative to full attention over every spatiotemporal token pair while retaining both kinds of interaction.

### p08-l10-a1-q3

This diagnostic measures mean absolute frame-to-frame change. What does it print?

```python
def mean_delta(frames):
    return sum(abs(b - a)
               for a, b in zip(frames, frames[1:])) / (len(frames) - 1)

smooth = [0.0, 1.0, 2.0, 3.0]
flickery = [0.0, 3.0, 0.0, 3.0]
print(mean_delta(smooth), mean_delta(flickery))
```

A) 1.0 3.0
B) 1.0 1.0
C) 3.0 9.0
D) 0.75 2.25

Learner response: A
Correct answer: A
Result: Correct (1/1)
Explanation: The smooth sequence has three absolute deltas of 1, averaging 1. The flickery sequence has three absolute deltas of 3, averaging 3. This diagnostic measures changes, not semantic correctness or motion quality by itself.

Lesson 10 initial set: 3/3. Lesson minimum met; status remains todo pending phase pass.

### p08-l11-a1-q1

In a neural audio codec using residual vector quantization (RVQ), what does each quantizer after the first represent?

A) An independent copy of the original waveform, ignoring earlier quantizers.
B) A text embedding that replaces the need to encode audio features.
C) The probability that the preceding audio token came from real data.
D) The residual representation error remaining after earlier quantizers.

Learner response: D
Correct answer: D
Result: Correct (1/1)
Explanation: RVQ successively quantizes the error left by previous codebook approximations. Adding their selected vectors refines the representation of the encoder output.

### p08-l11-a1-q2

A live voice application must begin playback before the full utterance is generated. Which design most directly supports incremental audio generation?

A) A full-clip diffusion model that releases audio only after all denoising steps.
B) A causal codec-token generator paired with a decoder that supports streaming.
C) A waveform generator that waits for the entire recording before decoding.
D) An offline codec that compresses completed recordings without generating tokens.

Learner response: B
Correct answer: B
Result: Correct (1/1)
Explanation: A causal token generator can emit successive codec tokens, and a streaming-capable decoder turns available tokens into audio chunks. Playback still requires adequate generation throughput and buffering; full-clip generation does not directly provide incremental output.

### p08-l11-a1-q3

What token sequence does this lesson's synthetic style generator return?

```python
def make_tokens(style, length, vocab_size):
    if style == 0:
        return [i % vocab_size for i in range(length)]
    return [(i * 3) % vocab_size for i in range(length)]

print(make_tokens(style=1, length=6, vocab_size=5))
```

A) [0, 1, 2, 3, 4, 0]
B) [0, 3, 6, 9, 12, 15]
C) [0, 3, 1, 4, 2, 0]
D) [1, 4, 2, 0, 3, 1]

Learner response: C
Correct answer: C
Result: Correct (1/1)
Explanation: Style 1 uses (i * 3) % 5 for i = 0 through 5: 0, 3, 1, 4, 2, 0. The modulo wraps each value into the vocabulary range.

Lesson 11 initial set: 3/3. Lesson minimum met; status remains todo pending phase pass.

### p08-l12-a1-q1

How does the lesson's simple 2D splat renderer differ from real 3D Gaussian Splatting rendering?

A) The toy simply sums Gaussian contributions; real 3DGS projects splats and alpha-composites them in depth order.
B) The toy uses Gaussian contributions; real 3DGS represents every scene as a dense voxel grid.
C) The toy renders an image; real 3DGS only evaluates an exact scene probability density.
D) The toy has splat colors; real 3DGS cannot represent view-dependent appearance.

Learner response: A
Correct answer: A
Result: Correct (1/1)
Explanation: The toy render adds color-weighted 2D Gaussian values. Real 3D Gaussian Splatting projects 3D Gaussians to the image plane and uses depth-ordered alpha compositing, accounting for opacity and occlusion.

### p08-l12-a1-q2

Four independently generated views disagree about an object's shape, causing a poor 3D reconstruction. Which change most directly addresses the conflicting supervision?

A) Add more splats while keeping all contradictory views unchanged.
B) Fit each view separately and assume their geometry will align.
C) Use jointly conditioned multi-view generation to encourage consistent geometry.
D) Increase image sharpness without checking agreement between viewpoints.

Learner response: C
Correct answer: C
Result: Correct (1/1)
Explanation: Joint multi-view generation couples viewpoints to encourage agreement about one object. More reconstruction capacity or sharper individual images does not resolve inconsistent geometric evidence.

### p08-l12-a1-q3

At the shared center of two splats, what does this toy additive renderer print?

```python
import math

def gaussian_at(x, y, g):
    px, py = g["pos"]
    d2 = (x - px) ** 2 + (y - py) ** 2
    return math.exp(-d2 / (2 * g["sigma"] ** 2))

splats = [
    {"pos": (0, 0), "sigma": 1.0, "color": 0.7},
    {"pos": (0, 0), "sigma": 2.0, "color": 0.6},
]
pixel = sum(g["color"] * gaussian_at(0, 0, g) for g in splats)
print(round(pixel, 1))
```

A) 0.7
B) 1.3
C) 0.42
D) 1.0

Learner response: B
Correct answer: B
Result: Correct (1/1)
Explanation: At each Gaussian center d2 = 0, so exp(0) = 1 regardless of sigma. The toy sums 0.7 + 0.6 = 1.3 and does not clamp or alpha-composite the value.

Lesson 12 initial set: 3/3. Lesson minimum met; status remains todo pending phase pass.

### p08-l13-a1-q1

For the straight-line interpolant x_t = (1 - t)*x_0 + t*x_1, where x_0 is data and x_1 is noise, what velocity target is used in the lesson's flow-matching loss?

A) x_0 - x_1
B) x_t - x_0
C) x_0 + x_1
D) x_1 - x_0

Learner response: D
Correct answer: D
Result: Correct (1/1)
Explanation: Differentiating the interpolant with respect to t gives dx_t/dt = -x_0 + x_1. Sampling travels backward from noise at t=1 to data at t=0, using negative time increments.

### p08-l13-a1-q2

Your flow model needs many integration steps because its learned trajectories curve. Which procedure matches rectified-flow reflow?

A) Replace the velocity target with discriminator scores and freeze the flow model.
B) Integrate the trained model to pair noise with its generated endpoints, then train a new flow on those pairs.
C) Pair each noise sample with a new random data point at every sampling step.
D) Remove time conditioning and assume that every learned trajectory is already straight.

Learner response: B
Correct answer: B
Result: Correct (1/1)
Explanation: Reflow uses the existing flow to obtain coupled noise/data endpoint pairs, then trains a new flow with straight interpolants on those pairs. This aims to straighten learned trajectories and improve few-step sampling; it does not guarantee exact one-step generation.

### p08-l13-a1-q3

This sampler integrates backward from t=1 to t=0. What does it print?

```python
def velocity(x, t):
    return 2.0

x = 3.0
num_steps = 4
for i in range(num_steps):
    t = 1.0 - i / num_steps
    dt = 1.0 / num_steps
    x -= dt * velocity(x, t)
print(x)
```

A) 5.0
B) 2.5
C) 1.0
D) -5.0

Learner response: C
Correct answer: C
Result: Correct (1/1)
Explanation: Each of four steps subtracts 0.25 * 2 = 0.5. Starting from 3, the result is 3 - 4 * 0.5 = 1. The subtraction implements integration toward decreasing time.

Lesson 13 initial set: 3/3. Lesson minimum met; status remains todo pending phase pass.

### p08-l14-a1-q1

What does FID directly compare when evaluating generated images?

A) The exact pixel correspondence between each generated image and its prompt.
B) Gaussian fits to real and generated image features from an Inception network.
C) The proportion of human judges who prefer generated images to real ones.
D) The cosine similarity between image embeddings and text embeddings.

Learner response: B
Correct answer: B
Result: Correct (1/1)
Explanation: FID compares means and covariances of real and generated Inception feature distributions using their Gaussian fits. It does not directly evaluate prompt adherence or collect human judgments.

### p08-l14-a1-q2

A model scores highly on CLIP similarity but often swaps object colors in prompts such as "a red cube on a blue sphere." Which evaluation best investigates this weakness?

A) Measure only FID on unrelated unconditional images.
B) Shorten every prompt until its CLIP similarity increases.
C) Add targeted attribute-binding checks and blinded human review of those prompts.
D) Treat the high CLIP score as proof that every requested relationship is correct.

Learner response: C
Correct answer: C
Result: Correct (1/1)
Explanation: CLIP similarity can miss compositional and attribute-binding errors. Targeted checks and blinded review assess whether the requested colors and relationships actually hold; FID alone or improving a proxy score does not establish that.

### p08-l14-a1-q3

Both models start with equal Elo ratings. What ratings does this update return after model A wins?

```python
def elo_update(r_a, r_b, winner, k=32):
    expected_a = 1 / (1 + 10 ** ((r_b - r_a) / 400))
    actual_a = 1.0 if winner == "a" else 0.0
    change = k * (actual_a - expected_a)
    return r_a + change, r_b - change

print(elo_update(1000, 1000, "a"))
```

A) (1032.0, 968.0)
B) (1000.0, 1000.0)
C) (984.0, 1016.0)
D) (1016.0, 984.0)

Learner response: D
Correct answer: D
Result: Correct (1/1)
Explanation: Equal ratings give expected_a = 0.5. With A winning, change = 32 * (1 - 0.5) = 16. A gains 16 and B loses 16, yielding (1016, 984).

Lesson 14 initial set: 3/3. Lesson minimum met; status remains todo pending phase pass.

### p08-l19-a1-q1

What makes VAR next-scale generation different from raster-order next-token image generation?

A) It generates all scales simultaneously without any conditioning between scales.
B) It replaces the discrete tokenizer with a pixel-space diffusion noise schedule.
C) It predicts each finer token grid conditioned on earlier scales, generating positions within that scale in parallel.
D) It predicts each pixel sequentially while discarding previously generated coarse structure.

Learner response: C
Correct answer: C
Result: Correct (1/1)
Explanation: VAR generates a pyramid of discrete token grids from coarse to fine. Each scale conditions on earlier scales and predicts its positions in parallel, rather than sampling individual positions sequentially in raster order.

### p08-l19-a1-q2

A VAR tokenizer reconstructs coarse layout well, but fine details remain inaccurate. What should the higher-resolution residual token grids learn to represent?

A) The remaining latent error after adding the upsampled contributions of coarser scales.
B) Independent complete images that discard all previously generated scales.
C) Only the scale indices, with no information about the image content.
D) The same coarse token grid repeated unchanged at every resolution.

Learner response: A
Correct answer: A
Result: Correct (1/1)
Explanation: Multi-scale residual VQ uses each finer scale to encode what the coarser-scale reconstruction missed. Decoding sums embedded, upsampled scale contributions to reconstruct the image latent.

### p08-l19-a1-q3

Assume predict_scale generates all tokens for one scale in a single transformer pass. What does this code print as (passes, total tokens)?

```python
scales = [1, 2, 4, 8]
passes = 0
total_tokens = 0
for side in scales:
    passes += 1
    total_tokens += side * side
print(passes, total_tokens)
```

A) 85 85
B) 4 64
C) 15 85
D) 4 85

Learner response: D
Correct answer: D
Result: Correct (1/1)
Explanation: There is one pass for each of four scales. Their token counts are 1, 4, 16, and 64, totaling 85. Parallel generation within each scale separates pass count from token count.

Lesson 19 initial set: 3/3. Initial phase round complete: 38/45 (84.44%). Lessons 01 (1/3) and 04 (0/3) below minimum. Phase not passed.

### p08-l01-a2-q1

An autoregressive model provides normalized conditional probabilities p(x_i | x_<i). How does it obtain the joint probability of a complete sequence?

A) Average the conditional probabilities across sequence positions.
B) Multiply the conditional probabilities across sequence positions.
C) Use only the conditional probability of the final sequence element.
D) Subtract the probability of generated sequences from one.

Learner response: A
Correct answer: B
Result: Incorrect (0/1)
Explanation: The probability chain rule gives p(x) = product_i p(x_i | x_<i). Equivalently, log p(x) is the sum of the conditional log-probabilities.

### p08-l01-a2-q2

A proposed generator can draw realistic samples in one forward pass but exposes no tractable probability-density evaluator. You need exact log-likelihoods for arbitrary inputs. What should you conclude?

A) Fast sampling alone is sufficient to recover exact input likelihoods.
B) A discriminator score is automatically a normalized input density.
C) Drawing more samples makes each input's exact likelihood directly available.
D) The sampling interface does not meet the requirement; use a tractable explicit-density model.

Learner response: D
Correct answer: D
Result: Correct (1/1)
Explanation: A sampler without a tractable density evaluator does not provide exact log-likelihoods. A model with tractable explicit density, such as a suitable autoregressive model or normalizing flow, addresses that requirement. Discriminator scores are not normalized data densities.

### p08-l01-a2-q3

This histogram estimator divides the fraction of samples in a bin by its width. What does it print?

```python
def histogram_density(samples, x, bin_width):
    lo, hi = x - bin_width / 2, x + bin_width / 2
    count = sum(1 for s in samples if lo <= s < hi)
    return count / (len(samples) * bin_width)

print(histogram_density([0.0, 0.1, 0.2, 0.8], 0.1, 0.4))
```

A) 0.75
B) 1.875
C) 0.3
D) 2.5

Learner response: B
Correct answer: B
Result: Correct (1/1)
Explanation: The bin is approximately [-0.1, 0.3), containing 0.0, 0.1, and 0.2. The density is 3 / (4 * 0.4) = 1.875. A density may exceed 1; the probability mass for this bin is density times width = 0.75.

Lesson 01 attempt 2 complete: 2/3 replaces initial 1/3. Effective phase score 39/45 (86.67%); cumulative 40/48. Lesson04 remains below minimum; phase not passed.

### p08-l04-a2-q1

What does a PatchGAN discriminator primarily assess in Pix2Pix?

A) Whether translating an image to another domain and back reproduces the input.
B) Whether the generator assigns an exact normalized probability to the whole image.
C) Whether local image patches look realistic, using a grid of discriminator scores.
D) Whether every generated pixel exactly equals its paired target pixel.

Learner response: C
Correct answer: C
Result: Correct (1/1)
Explanation: PatchGAN produces scores for local receptive fields rather than only one whole-image score. In Pix2Pix it sees the condition/output pair; cycle consistency and exact pixel reconstruction are separate objectives, not its patch-realism test.

### p08-l04-a2-q2

A paired sketch-to-photo model produces realistic photos that often ignore the input sketch. You discover its discriminator sees only the output photo. Which change directly lets the discriminator assess input-output consistency?

A) Feed the discriminator the sketch and candidate photo together.
B) Remove the sketch from the generator input as well.
C) Replace each paired target with a randomly chosen real photo.
D) Evaluate only the realism of pooled generated photos.

Learner response: A
Correct answer: A
Result: Correct (1/1)
Explanation: A conditional discriminator D(x, y) sees both the input sketch and output photo, so it can assess their correspondence as well as realism. A discriminator seeing only y cannot directly inspect consistency with x.

### p08-l04-a2-q3

This toy CycleGAN check computes round-trip error. What does it print?

```python
def G(x):
    return x + 3

def F(y):
    return y - 2

x = 4
y = G(x)
x_reconstructed = F(y)
cycle_error = abs(x_reconstructed - x)
print(y, x_reconstructed, cycle_error)
```

A) 7 4 0
B) 7 5 1
C) 6 4 0
D) 7 5 5

Learner response: B
Correct answer: B
Result: Correct (1/1)
Explanation: G(4) = 7, then F(7) = 5. The round-trip error is abs(5 - 4) = 1. Cycle consistency penalizes failure to reconstruct the source after translating in both directions.

Lesson04 attempt2 complete: 3/3 replaces initial0/3. Phase08 passed: initial38/45, effective42/45 (93.33%), cumulative43/51. Two full retake sets; every lesson >=2/3. Quiz-based mastery; implementation lab not performed in this assessment.
