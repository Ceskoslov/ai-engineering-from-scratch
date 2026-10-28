# Phase 12 detailed quiz history

Archive: read only when an earlier question or attempt is relevant. [Phase progress](progress.md).

No questions presented yet.


### p12-l01-a1-q1 — 2026-10-28

What does the shared patch projection do in a Vision Transformer?

A) It averages all image patches into one image-level vector.
B) It assigns each patch a unique matrix based on its position.
C) It maps each flattened patch to a fixed-width token vector.
D) It converts each color channel into a separate text token.

Learner answer: B. Correct answer: C. Result: incorrect (0/1).

The same learned linear projection maps each flattened patch into the hidden dimension D; positional information is supplied separately.


### p12-l01-a1-q2 — 2026-10-28

A 224×224 image uses 16×16 patches. With one CLS token and four register tokens, how many tokens enter the vision transformer?

A) 196
B) 197
C) 200
D) 201

Learner answer: B. Correct answer: D. Result: incorrect (0/1).

The 14×14 grid gives 196 patch tokens; adding one CLS and four registers gives 201.


### p12-l01-a1-q3 — 2026-10-28

In the lesson code, grid_shape rejects image sizes not divisible by patch size. What happens when seq_length receives a config with image_size=384 and patch_size=14?

A) It raises ValueError before returning a sequence length.
B) It uses a 27×27 grid and discards the remaining pixels.
C) It pads the image and uses a 28×28 patch grid.
D) It returns 384×384 tokens plus any extra tokens.

Learner answer: A. Correct answer: A. Result: correct (1/1).

seq_length calls grid_shape, whose divisibility check raises ValueError because 384 % 14 is not zero.


### p12-l02-a1-q1 — 2026-10-28

In CLIP training, what does the symmetric contrastive objective encourage?

A) Each image to match every caption in its training batch equally.
B) Paired images and captions to outrank mismatches in both directions.
C) Each image encoder to reconstruct its original pixels from captions.
D) Image and text embeddings to occupy unrelated representation spaces.

Learner answer: B. Correct answer: B. Result: correct (1/1).

Image-to-text and text-to-image cross-entropies both use paired examples as positives and other batch entries as negatives.


### p12-l02-a1-q2 — 2026-10-28

You have a pretrained CLIP model and new class names, but no labeled training images. How do you perform zero-shot classification?

A) Train a new linear classifier using the class names as image labels.
B) Choose the class prompt with the smallest embedding vector norm.
C) Generate a caption and compare its character count with each class name.
D) Embed class prompts and select the highest cosine similarity to the image.

Learner answer: D. Correct answer: D. Result: correct (1/1).

Zero-shot classification compares the image embedding with text embeddings of candidate class prompts, without training a new classifier.


### p12-l02-a1-q3 — 2026-10-28

What class ranks first for zero_shot_classify([2, 0], {"cat": [1, 1], "dog": [1, 0]}) in the lesson code?

A) dog, because its normalized vector has cosine similarity 1.
B) cat, because its unnormalized vector has the larger coordinate sum.
C) cat, because the function preserves dictionary insertion order.
D) dog, because the function chooses the smallest cosine similarity.

Learner answer: D. Correct answer: A. Result: incorrect (0/1).

The function normalizes image and class vectors, computes dot products, and sorts descending. Dog scores 1; cat scores 1/sqrt(2).


### p12-l03-a1-q1 — 2026-10-28

How does a Q-Former reduce the visual token count passed to an LLM?

A) It turns each image patch into a separate natural-language sentence.
B) It expands each patch into several tokens using a wider projection.
C) It uses a fixed set of learned queries to summarize image features.
D) It removes the vision encoder and sends raw pixels to the text decoder.

Learner answer: C. Correct answer: C. Result: correct (1/1).

Learned queries cross-attend to image features, producing one summary token per query rather than one per image patch.


### p12-l03-a1-q2 — 2026-10-28

In BLIP-2 stage 2, which parameters are trained when connecting the vision features to the frozen LLM?

A) The vision encoder and LLM, while the Q-Former stays frozen.
B) The Q-Former and output projection, while both backbones stay frozen.
C) Only the LLM embedding table, while the full visual bridge stays frozen.
D) All model parameters, including both backbones and the visual bridge.

Learner answer: B. Correct answer: B. Result: correct (1/1).

Stage 2 trains the Q-Former and projection using the generative loss, leaving the vision encoder and LLM weights frozen.


### p12-l03-a1-q3 — 2026-10-28

The toy uses 8 queries, 64 patches, QUERY_DIM=16, and LLM_DIM=24. What are the attention-weight and projected-output shapes?

A) Attention: 64×8; projected output: 64×24.
B) Attention: 8×16; projected output: 64×24.
C) Attention: 64×64; projected output: 8×16.
D) Attention: 8×64; projected output: 8×24.

Learner answer: B. Correct answer: D. Result: incorrect (0/1).

Each query has weights over all 64 patches. Cross-attention preserves the 8-query count; projection changes each output width to 24.


### p12-l04-a1-q1 — 2026-10-28

Why initialize alpha to zero in the residual y = x + tanh(alpha) * cross_attention(x, visual)?

A) To make every visual token receive an equal attention weight.
B) To make the new visual branch contribute zero at initialization.
C) To prevent the visual branch from ever learning during training.
D) To replace the text representation with the visual representation.

Learner answer: B. Correct answer: B. Result: correct (1/1).

Because tanh(0)=0, the added visual contribution is zero and the residual output equals x at initialization.


### p12-l04-a1-q2 — 2026-10-28

An image produces 196 patches and another produces 900. A Perceiver resampler uses K=64 latents per image. How many output tokens does each image produce?

A) 196 for the first image and 900 for the second.
B) 64 for the first image and 900 for the second.
C) 196 for the first image and 64 for the second.
D) 64 for each image, independent of its patch count.

Learner answer: D. Correct answer: D. Result: correct (1/1).

The learned latent count K sets the output token count per image regardless of how many patches attend as keys and values.


### p12-l04-a1-q3 — 2026-10-28

What does interleaved_mask(["intro", "IMG0", "a", "IMG1", "b"]) return, with columns ordered IMG0, IMG1?

A) [[False, False], [True, False], [False, True]]
B) [[True, False], [True, False], [True, True]]
C) [[False, False], [True, False], [True, True]]
D) [[False, False], [False, True], [False, True]]

Learner answer: D. Correct answer: A. Result: incorrect (0/1).

Intro has no preceding image; a sees IMG0; b sees only its most recent preceding image, IMG1.


### p12-l05-a1-q1 — 2026-10-28

Compared with a Q-Former bottleneck, what is the main token-budget tradeoff of projecting every image patch through an MLP?

A) It produces a single pooled token but requires training both encoders.
B) It removes visual tokens from the context but requires gated LLM layers.
C) It preserves one token per patch but uses more LLM context positions.
D) It fixes the output at 32 tokens but requires extra contrastive losses.

Learner answer: C. Correct answer: C. Result: correct (1/1).

A per-patch MLP changes embedding width without reducing patch count. This avoids a fixed-query bottleneck but consumes more context positions.


### p12-l05-a1-q2 — 2026-10-28

During LLaVA stage-1 projector alignment, which components are trained using caption language-modeling loss?

A) Only the projector, while the vision encoder and LLM stay frozen.
B) Only the vision encoder, while the projector and LLM stay frozen.
C) Only the LLM, while the vision encoder and projector stay frozen.
D) The vision encoder and LLM, while the projector stays frozen.

Learner answer: A. Correct answer: A. Result: correct (1/1).

Stage 1 learns the projector mapping using a frozen vision encoder and frozen LLM, with caption LM loss.


### p12-l05-a1-q3 — 2026-10-28

In the toy code, what does build_llava_prompt(system, user, image_tokens=576) actually do with the image placeholder?

A) It replaces the placeholder with 576 numeric embedding vectors.
B) It keeps the placeholder in raw_prompt and records the count as metadata.
C) It runs the vision encoder and inserts 576 generated text tokens.
D) It removes the placeholder and verifies the LLM context length.

Learner answer: A. Correct answer: B. Result: incorrect (0/1).

The helper builds a string containing <image> and returns the supplied image_tokens count separately. It does not implement embedding insertion or model execution.


### p12-l06-a1-q1 — 2026-10-28

Why use a block-diagonal attention mask when packing patch sequences from different images into one sequence?

A) To let every patch attend to every image in the batch.
B) To reduce every image to the same number of patch tokens.
C) To replace all patch-position information with image labels.
D) To restrict each patch to attending within its own image.

Learner answer: D. Correct answer: D. Result: correct (1/1).

Concatenation places images in one sequence; the mask prevents cross-image attention while allowing attention within each image.


### p12-l06-a1-q2 — 2026-10-28

Your frozen vision encoder accepts only 336×336 inputs, but you need fine detail from a large document image. Which strategy fits this constraint?

A) Resize the full document to 336×336 and discard all local detail.
B) Use AnyRes tiles plus a global thumbnail, encoding each at 336×336.
C) Send the full native-resolution image to the fixed-size encoder unchanged.
D) Use a packing mask to make every patch contain more pixels.

Learner answer: B. Correct answer: B. Result: correct (1/1).

AnyRes applies the fixed-size encoder to separate tiles and a global thumbnail, retaining more local detail at a higher visual token cost.


### p12-l06-a1-q3 — 2026-10-28

pack_batch receives image token lengths [2, 3]. It accumulates offsets from [0] and sums n*n for mask_nonzero. What are cu_seqlens and mask_nonzero?

A) cu_seqlens=[0, 2, 5]; mask_nonzero=13.
B) cu_seqlens=[0, 2, 3]; mask_nonzero=13.
C) cu_seqlens=[0, 2, 5]; mask_nonzero=25.
D) cu_seqlens=[0, 3, 5]; mask_nonzero=5.

Learner answer: A. Correct answer: A. Result: correct (1/1).

Cumulative offsets are 0, 2, 2+3=5. The two within-image blocks contain 2²+3²=13 allowed cells, compared with 25 dense cells.


### p12-l07-a1-q1 — 2026-10-28

What makes a comparison a controlled ablation of connector architecture in a VLM?

A) Changing the connector and training data while retaining the model name.
B) Comparing two published checkpoints using their best reported scores.
C) Changing the connector while holding the other experimental settings fixed.
D) Changing the encoder and resolution while retaining the connector.

Learner answer: C. Correct answer: C. Result: correct (1/1).

A controlled ablation varies the axis being tested and holds other settings fixed, including data, backbone, token budget, and evaluation.


### p12-l07-a1-q2 — 2026-10-28

You want to test whether denser captions improve your VLM. Which experiment best isolates caption quality?

A) Keep images, backbone, connector, resolution, and training budget fixed; vary captions.
B) Replace both captions and the vision encoder, then compare final scores.
C) Compare a small short-caption model with a much larger dense-caption model.
D) Increase image resolution only for the dense-caption training run.

Learner answer: A. Correct answer: A. Result: correct (1/1).

Holding the other axes and training budget fixed makes caption quality the experimental variable instead of confounding it with model or compute changes.


### p12-l07-a1-q3 — 2026-10-28

The picker filters candidates with r.llm_b <= budget_b. A recipe has llm_b=7, but its vision encoder and connector bring the total above 8B. With budget_b=8, what happens?

A) It is rejected because the filter sums all component parameter counts.
B) It remains eligible because the filter checks only the LLM parameter count.
C) Its encoder and connector are removed to fit the total parameter budget.
D) It raises ValueError because the total parameter count exceeds the budget.

Learner answer: A. Correct answer: B. Result: incorrect (0/1).

The filter reads only llm_b. It does not calculate total model size, memory requirements, or latency.


### p12-l08-a1-q1 — 2026-10-28

Why allocate a shared visual-token budget differently across single-image, multi-image, and video inputs?

A) To make every scenario use identical image resolution and frame counts.
B) To eliminate the need for image encoders when processing video inputs.
C) To guarantee that temporal reasoning improves whenever tokens are removed.
D) To balance spatial detail against image or frame coverage within bounded context.

Learner answer: D. Correct answer: D. Result: correct (1/1).

Single images can spend tokens on detail; multi-image and video inputs distribute the budget over more views or frames, often using spatial pooling.


### p12-l08-a1-q2 — 2026-10-28

A video has 32 sampled frames, each with a 24×24 patch grid. Pooling each grid to 8×8 gives how many visual tokens in total?

A) 768 tokens.
B) 2048 tokens.
C) 6144 tokens.
D) 18432 tokens.

Learner answer: B. Correct answer: B. Result: correct (1/1).

Each pooled frame has 8×8=64 tokens; 32 frames produce 32×64=2048 tokens.


### p12-l08-a1-q3 — 2026-10-28

After every candidate exceeds the budget, plan_video returns {"n_frames": 8, "per_frame": 64, "total": 512}. What happens for budget=100?

A) It raises an exception because no candidate fits the budget.
B) It reduces the frame count until total tokens are at most 100.
C) It returns the fallback even though its 512 tokens exceed the budget.
D) It returns an empty plan with zero frames and zero tokens.

Learner answer: C. Correct answer: C. Result: correct (1/1).

The fallback is returned unconditionally after the loops. There is no final budget check, so the planner does not enforce its advertised limit for very small budgets.


### p12-l09-a1-q1 — 2026-10-28

Why preserve actual frame timestamps when a video may be sampled at different frame rates?

A) Frame indices alone always specify elapsed seconds regardless of FPS.
B) Timestamps remove the need to encode spatial positions within frames.
C) Timestamps preserve elapsed-time information that frame indices alone omit.
D) Timestamps guarantee that every brief event appears in the sampled frames.

Learner answer: C. Correct answer: C. Result: correct (1/1).

The same frame-index gap can represent different elapsed times at different sampling rates. Actual timestamps retain that temporal information but cannot recover events omitted by sampling.


### p12-l09-a1-q2 — 2026-10-28

Ignoring timestamp and text overhead, a 60-second video has a budget of 9720 visual tokens and costs 81 tokens per frame. What is the highest affordable FPS?

A) 1 FPS.
B) 2 FPS.
C) 4 FPS.
D) 8 FPS.

Learner answer: B. Correct answer: B. Result: correct (1/1).

fps_max = 9720 / (60 × 81) = 2 FPS, giving 120 frames and 9720 visual tokens.


### p12-l09-a1-q3 — 2026-10-28

parse_tool_call first returns json.loads(raw) if parsing succeeds, without schema validation. What happens for raw=' {"tool": "mouse_click", "coords": "somewhere"} '?

A) It returns the dictionary even though coords is a string.
B) It returns PARSE_ERROR because coords must be a numeric pair.
C) It converts the string into validated screen coordinates.
D) It executes a mouse click using the supplied coordinate value.

Learner answer: A. Correct answer: A. Result: correct (1/1).

The JSON is syntactically valid, so json.loads returns a dictionary. This helper neither validates the tool schema or coordinates nor executes actions.


### p12-l10-a1-q1 — 2026-10-28

What does catastrophic forgetting mean when adapting a text LLM into a VLM?

A) The model consumes more context positions when image tokens are added.
B) The model loses previously learned text skills during multimodal adaptation.
C) The vision encoder produces different patch counts for different resolutions.
D) The training corpus includes both image-caption and interleaved documents.

Learner answer: B. Correct answer: B. Result: correct (1/1).

Catastrophic forgetting is degradation of previously learned capabilities while learning new ones, such as text-only reasoning regressing during multimodal adaptation.


### p12-l10-a1-q2 — 2026-10-28

A resolution router lowers average visual-token usage. What else must you measure before claiming it preserves answer quality?

A) Only whether each request returns a syntactically valid answer.
B) Only whether the average input resolution is lower than before.
C) Only whether the routing tier fractions sum to one.
D) Task accuracy, including detail-sensitive cases routed to low resolution.

Learner answer: D. Correct answer: D. Result: correct (1/1).

Token savings alone do not establish quality preservation. Misrouting OCR or fine-detail queries can remove evidence the model needs, so task accuracy and routing failures must be evaluated.


### p12-l10-a1-q3 — 2026-10-28

CorpusMix.steps computes int(total * fraction) independently for each modality. With normalized fractions 0.4, 0.35, 0.2, 0.05 and total=3, what counts result?

A) text=1, interleaved=1, caption=0, video=0; sum=2.
B) text=1, interleaved=1, caption=1, video=0; sum=3.
C) text=2, interleaved=1, caption=0, video=0; sum=3.
D) text=0, interleaved=0, caption=0, video=0; sum=0.

Learner answer: B. Correct answer: A. Result: incorrect (0/1).

Independent integer truncation gives int(1.2)=1, int(1.05)=1, int(0.6)=0, int(0.15)=0. No remainder allocation is implemented.


### p12-l11-a1-q1 — 2026-10-28

What enables a Chameleon-style autoregressive decoder to predict both text and image content?

A) A shared token-ID vocabulary containing text tokens, discrete image codes, and separators.
B) A text-only output vocabulary with image patches used only as continuous input features.
C) A frozen vision encoder that converts every output word into an image caption.
D) A separate diffusion model that replaces next-token prediction for every modality.

Learner answer: A. Correct answer: A. Result: correct (1/1).

Discrete image codes and text IDs occupy one vocabulary, allowing a single autoregressive output distribution to predict either modality. An image decoder renders the generated image codes.


### p12-l11-a1-q2 — 2026-10-28

Your image tokenizer loses fine text detail even when decoding the correct image codes. What follows for generation through that tokenizer?

A) A larger text vocabulary automatically restores the missing pixel detail.
B) Longer captions guarantee exact reconstruction of the original image.
C) Better next-token prediction alone cannot remove that reconstruction bottleneck.
D) Removing image separators makes the quantizer lossless.

Learner answer: C. Correct answer: C. Result: correct (1/1).

A lossy tokenizer constrains the information available to its decoder. Improving code prediction alone cannot recover detail that the representation discards.


### p12-l11-a1-q3 — 2026-10-28

quantize_patch returns best + IMG_OFFSET, where IMG_OFFSET=32. If nearest-codebook lookup selects index 5, which shared-vocabulary ID is returned?

A) 5
B) 32
C) 48
D) 37

Learner answer: D. Correct answer: D. Result: correct (1/1).

Image code indices are offset past the 32 text IDs: 5+32=37.


### p12-l12-a1-q1 — 2026-10-28

How can next-token prediction support image generation in an Emu3-style model?

A) It predicts continuous pixels directly from a text-only output vocabulary.
B) It removes the visual tokenizer and uses a diffusion loss for image tokens.
C) It predicts discrete visual codes that an image decoder can render.
D) It treats all image tokens as fixed placeholders excluded from the loss.

Learner answer: A. Correct answer: C. Result: incorrect (0/1).

A visual tokenizer represents image content as discrete codes; autoregressive next-token prediction can model their sequence, and a visual decoder converts generated codes to pixels.


### p12-l12-a1-q2 — 2026-10-28

Assume an image tokenizer reduces each spatial dimension by 8. How many tokens represent a 1024×1024 image, excluding separators?

A) 4096
B) 8192
C) 65536
D) 16384

Learner answer: D. Correct answer: D. Result: correct (1/1).

The latent grid is (1024/8)×(1024/8)=128×128=16384 tokens.


### p12-l12-a1-q3 — 2026-10-28

cfg_mix uses u + gamma * (c - u) per logit. For cond=[4, 1], uncond=[2, 3], and gamma=2, what does it return?

A) [6, -1]
B) [4, 1]
C) [8, 2]
D) [2, 3]

Learner answer: A. Correct answer: A. Result: correct (1/1).

The first logit is 2+2×(4−2)=6; the second is 3+2×(1−3)=−1.


### p12-l13-a1-q1 — 2026-10-28

Which pairing describes the core Transfusion-style training design?

A) Text uses diffusion loss; discrete image codes use text classification loss.
B) Text uses next-token loss; continuous image representations use denoising loss.
C) Text and images both use next-token loss over discrete image codebook IDs.
D) Text and images both use pixel reconstruction loss without a vocabulary.

Learner answer: B. Correct answer: B. Result: correct (1/1).

A shared transformer combines autoregressive cross-entropy for discrete text with a diffusion or denoising objective for continuous image representations.


### p12-l13-a1-q2 — 2026-10-28

Which attention pattern supports causal text generation while allowing patches in one noisy image to coordinate denoising?

A) Fully bidirectional attention over all text and all images.
B) Fully causal attention everywhere, with no within-image exceptions.
C) Each image patch attends only to itself, while text sees future tokens.
D) Causal text attention with bidirectional attention within each image block.

Learner answer: D. Correct answer: D. Result: correct (1/1).

Text must not access future text targets, while patches in the same noisy image block can attend bidirectionally to coordinate image denoising.


### p12-l13-a1-q3 — 2026-10-28

The toy train loop computes losses, then executes text_scale += 1 and img_scale += 1 without gradients. What does this demonstrate?

A) Loss accounting with scripted scale changes, rather than learned gradient updates.
B) Backpropagation through the shared transformer using an implicit optimizer.
C) Independent gradient descent on two complete pretrained model backbones.
D) Automatic optimization of loss weights using validation-set accuracy.

Learner answer: A. Correct answer: A. Result: correct (1/1).

The scales increment unconditionally. No differentiation or optimizer applies gradients from the computed loss, so this is a simulation of loss plumbing.


### p12-l14-a1-q1 — 2026-10-28

How does masked discrete image generation differ from strictly autoregressive image-token generation?

A) It predicts continuous pixel noise instead of using discrete image tokens.
B) It fills multiple masked image-token positions in parallel over successive rounds.
C) It predicts each image token once in a fixed left-to-right order.
D) It generates text captions and never predicts image-token IDs.

Learner answer: B. Correct answer: B. Result: correct (1/1).

Masked discrete generation predicts multiple missing image codes per round, then progressively commits predictions instead of decoding every image code sequentially.


### p12-l14-a1-q2 — 2026-10-28

How would you apply a masked-token image generator to inpainting while preserving the visible region?

A) Mask the entire image and remove all visible-region conditioning.
B) Convert visible image codes into text and use only text next-token prediction.
C) Freeze all masked positions and generate only the already visible positions.
D) Keep known-region codes as context and predict codes for the masked region.

Learner answer: D. Correct answer: D. Result: correct (1/1).

Inpainting conditions on the known image-token region while filling the unknown masked region, using the masked-prediction mechanism.


### p12-l14-a1-q3 — 2026-10-28

step_unmask computes n_to_keep=max(1, int(len(masked_indices)*keep_ratio)). With 5 masked positions and keep_ratio=0.15, how many are filled this step?

A) 0
B) 5
C) 1
D) 2

Learner answer: C. Correct answer: C. Result: correct (1/1).

int(5×0.15)=int(0.75)=0, but max(1,0)=1 ensures at least one masked position is filled.


### p12-l15-a1-q1 — 2026-10-28

Why decouple visual encoding for understanding and generation in a Janus-style model?

A) To prevent the two tasks from sharing any transformer parameters.
B) To make semantic image embeddings directly reversible into exact pixels.
C) To avoid using a visual decoder when producing generated images.
D) To use semantic features for understanding and reconstruction-oriented codes for generation.

Learner answer: D. Correct answer: D. Result: correct (1/1).

Understanding and generation benefit from different visual representations. Separate encoding paths serve those goals while retaining a shared transformer body.


### p12-l15-a1-q2 — 2026-10-28

In a Janus-Pro-style generation path, the transformer has predicted image VQ code IDs. What produces the image pixels?

A) A text tokenizer converts the IDs into a natural-language caption.
B) The VQ decoder reconstructs an image from the generated codes.
C) The semantic encoder treats each ID as a class label and returns pixels.
D) The router averages all code IDs into one RGB color.

Learner answer: B. Correct answer: B. Result: correct (1/1).

The VQ generation path predicts codebook IDs, and its visual decoder renders those codes into an image.


### p12-l15-a1-q3 — 2026-10-28

The toy router counts matching understanding and generation keywords and returns ambiguous on a tie. What does route("Sketch a cat and then describe its breed") return?

A) generate, because sketch appears first.
B) understand, because describe appears last.
C) ambiguous, because each keyword group matches once.
D) generate, because generation takes precedence on ties.

Learner answer: C. Correct answer: C. Result: correct (1/1).

Sketch contributes one generation match and describe one understanding match. The scores tie, so the function returns ambiguous.


### p12-l16-a1-q1 — 2026-10-28

Why assign disjoint token-ID ranges to text, image, speech, and music codebooks in a shared vocabulary?

A) To let the same integer identify unrelated codes without modality information.
B) To ensure every modality produces exactly the same number of tokens.
C) To prevent collisions between modality codes in the shared ID space.
D) To make every modality tokenizer lossless without changing its codebook.

Learner answer: A. Correct answer: C. Result: incorrect (0/1).

Disjoint ranges give distinct IDs to codes from different modalities so the shared embedding and output layers can distinguish them.


### p12-l16-a1-q2 — 2026-10-28

A speech system streams text tokens quickly but waits for the entire response before decoding any audio. What change directly reduces time to first audio?

A) Decode playable audio chunks as sufficient speech tokens arrive.
B) Increase the final output audio duration before starting playback.
C) Wait for every residual codebook token of the full response.
D) Measure only text-token latency and omit the audio decoder.

Learner answer: A. Correct answer: A. Result: correct (1/1).

Incremental audio decoding and playback allow the user to hear the first chunk before the complete response finishes.


### p12-l16-a1-q3 — 2026-10-28

VocabSlot.end returns start + size, and build_vocab sets the next start to that end. For start=32000 and size=4096, what is the allocated ID range?

A) 32000 through 36096 inclusive; next start=36097.
B) 32001 through 36096 inclusive; next start=36096.
C) 0 through 4095 inclusive; next start=4096.
D) 32000 through 36095 inclusive; next start=36096.

Learner answer: A. Correct answer: D. Result: incorrect (0/1).

The end is exclusive: [32000,36096) contains 4096 IDs, so the last valid ID is 36095 and the next slot starts at 36096.


### p12-l17-a1-q1 — 2026-10-28

What distinguishes temporal grounding from simply recognizing that an event occurs in a video?

A) It identifies the event without needing any time information.
B) It localizes when the event occurs using timestamps or an interval.
C) It replaces video frames with one image-level semantic vector.
D) It predicts only the overall topic of the video.

Learner answer: A. Correct answer: B. Result: incorrect (0/1).

Temporal grounding associates an event with its time location, such as start and end timestamps, rather than only detecting its presence.


### p12-l17-a1-q2 — 2026-10-28

To fit a video token budget, you can reduce sampled frames or pool each frame more. Which tradeoff is correct?

A) Fewer frames lose spatial detail; stronger spatial pooling loses temporal coverage.
B) Both changes preserve all event timing and all fine spatial detail.
C) Fewer frames increase temporal coverage; stronger pooling increases spatial detail.
D) Fewer frames risk missing brief events; stronger pooling risks losing fine spatial detail.

Learner answer: D. Correct answer: D. Result: correct (1/1).

Temporal subsampling can miss events between sampled frames. Spatial pooling compresses each frame and can obscure small objects or text.


### p12-l17-a1-q3 — 2026-10-28

For a matching event name, predicted interval [2, 6] and ground-truth interval [4, 8] have what IoU, and do they pass tol_iou=0.3?

A) IoU=1/3; hit.
B) IoU=1/2; hit.
C) IoU=1/4; miss.
D) IoU=0; miss.

Learner answer: A. Correct answer: A. Result: correct (1/1).

Intersection length is 6−4=2; union spans 8−2=6. IoU=2/6=1/3, which is at least 0.3.


### p12-l18-a1-q1 — 2026-10-28

What is the main failure risk when answering long-video questions by retrieving only selected clips?

A) Every retrieved clip must contain the entire original video.
B) Retrieval guarantees all relevant events reach the answer model.
C) The retriever may miss relevant evidence before the answer model sees it.
D) The model must generate every video frame before reading the question.

Learner answer: C. Correct answer: C. Result: correct (1/1).

Retrieval reduces context cost by selecting clips, but omitted evidence cannot inform the downstream answer. Retrieval recall becomes a key bottleneck.


### p12-l18-a1-q2 — 2026-10-28

A 30-minute video is sampled at 1 FPS with 81 visual tokens per frame. Ignoring text overhead, how many visual tokens does it require?

A) 145800
B) 2430
C) 291600
D) 1800

Learner answer: A. Correct answer: A. Result: correct (1/1).

30×60=1800 seconds; at one frame per second, 1800×81=145800 visual tokens.


### p12-l18-a1-q3 — 2026-10-28

nih_trial samples a marker position and returns recall_prob from a supplied lookup curve, without calling a model. What does its output establish?

A) A measured model accuracy on a real long-video recall benchmark.
B) An observed success or failure on recognizing the inserted visual marker.
C) A guarantee that the downstream retriever finds the marker clip.
D) A simulated probability selected from the supplied curve, not measured recall.

Learner answer: D. Correct answer: D. Result: correct (1/1).

The helper chooses a probability using input assumptions. It neither invokes a video model nor tests marker recognition, so its probability is simulated.


### p12-l19-a1-q1 — 2026-10-28

Why can a plain speech transcript be insufficient for reasoning about an audio recording?

A) It preserves every acoustic feature, leaving no information to analyze.
B) It always contains more temporal detail than the original waveform.
C) It prevents a language model from reasoning about spoken words.
D) It can omit nonverbal sounds, vocal delivery, and other acoustic evidence.

Learner answer: D. Correct answer: D. Result: correct (1/1).

A plain transcript mainly preserves words. Music, environmental sounds, vocal delivery, and other acoustic cues may be missing from that representation.


### p12-l19-a1-q2 — 2026-10-28

You need to identify instruments in a recording. Which input path preserves the evidence needed for that task?

A) Only the spoken-word transcript, with the waveform discarded.
B) Audio encoder features that retain musical and acoustic information.
C) Only the recording filename, converted into text tokens.
D) A text summary of speech with all non-speech sounds removed.

Learner answer: B. Correct answer: B. Result: correct (1/1).

Instrument identification depends on the sound itself, so the model needs acoustic features rather than only transcribed words.


### p12-l19-a1-q3 — 2026-10-28

window_frames uses win=400, hop=160, starts at i=0, and appends while i+win<=16000, then increments i by hop. Without padding, how many frames does it append?

A) 100
B) 99
C) 98
D) 97

Learner answer: C. Correct answer: C. Result: correct (1/1).

Valid starts are 0 through 15520 in steps of160. The count is floor((16000−400)/160)+1=97+1=98; the next start15680 would overrun.


### p12-l20-a1-q1 — 2026-10-28

Why stream partial Thinker output into a Talker instead of waiting for the complete text response?

A) So speech synthesis can start while the Thinker continues composing the response.
B) So the Talker can avoid producing any speech tokens until the turn ends.
C) So all input audio can be discarded before the Thinker processes it.
D) So the waveform decoder can be removed from the speech pipeline.

Learner answer: A. Correct answer: A. Result: correct (1/1).

Incremental handoff overlaps response composition and speech synthesis, reducing the wait for first audio compared with completing all text first.


### p12-l20-a1-q2 — 2026-10-28

An audio codec requires 50 base speech tokens for each second of playback. What sustained production rate must the Talker meet to avoid falling behind?

A) At most 25 base tokens per second.
B) Any positive rate, provided the first token arrives quickly.
C) At least 50 base tokens per second.
D) Exactly one base token for the entire response.

Learner answer: C. Correct answer: C. Result: correct (1/1).

Real-time playback consumes 50 base tokens each second, so sustained generation must meet or exceed that rate; low first-token latency alone does not prevent later underruns.


### p12-l20-a1-q3 — 2026-10-28

The VAD simulator sets user stop=3800 ms and first audio=3800+silence_threshold_ms+400. With a 200 ms silence threshold, what is the lag from user stop to first audio?

A) 200 ms
B) 400 ms
C) 4400 ms
D) 600 ms

Learner answer: D. Correct answer: D. Result: correct (1/1).

First audio is at 4400 ms; subtract the 3800 ms stop time to get 600 ms. The silence threshold adds to the later 400 ms delay.


### p12-l21-a1-q1 — 2026-10-28

What distinguishes a vision-language-action model from a model that only answers visual questions?

A) It discards visual input and operates only on transcribed instructions.
B) It maps visual observations and language instructions to action outputs.
C) It generates image captions without any action representation.
D) It guarantees every predicted action is physically valid without control checks.

Learner answer: B. Correct answer: B. Result: correct (1/1).

A VLA consumes observations and instructions and produces actions or action representations, rather than only descriptive text.


### p12-l21-a1-q2 — 2026-10-28

A 10-dimensional action uses one discrete token per dimension at each 30 Hz control step. How many action tokens per second must be produced?

A) 30
B) 256
C) 300
D) 3000

Learner answer: C. Correct answer: C. Result: correct (1/1).

10 tokens per step ×30 steps per second =300 action tokens per second, before any other overhead.


### p12-l21-a1-q3 — 2026-10-28

discretize uses idx=int((a+1)/2*(bins-1)), then clips idx to [0,bins-1]. What does discretize([-1, 0, 1], bins=5) return?

A) [0, 2, 4]
B) [0, 3, 5]
C) [-1, 0, 1]
D) [1, 2, 5]

Learner answer: A. Correct answer: A. Result: correct (1/1).

The normalized values map to 0,2,4 using bins−1=4, all within the clipping range.


### p12-l22-a1-q1 — 2026-10-28

Why include word bounding boxes alongside recognized text in document understanding?

A) They prove that every recognized word is spelled correctly.
B) They replace the need to identify text content in the document.
C) They preserve spatial relationships such as columns and label-value positions.
D) They guarantee that every table can be converted into exact JSON.

Learner answer: C. Correct answer: C. Result: correct (1/1).

Bounding boxes retain where text occurs, helping distinguish layout-dependent relationships that plain text extraction can lose.


### p12-l22-a1-q2 — 2026-10-28

Two document extractors disagree about a field. Which evidence best supports resolving the disagreement?

A) Choose whichever extractor emits more verbose JSON.
B) Inspect the source page region and retained extraction provenance.
C) Accept whichever answer appears first in the combined output.
D) Average the two values without checking the document.

Learner answer: B. Correct answer: B. Result: correct (1/1).

The original page region and extraction provenance allow the disputed value and its context to be checked against source evidence.


### p12-l22-a1-q3 — 2026-10-28

The toy layoutlm_input uses text_ids=[hash(t.text)%10000 for t in tokens]. What limitation matters if these IDs are saved for later Python processes?

A) They are guaranteed stable vocabulary IDs across all Python processes.
B) Every distinct string is guaranteed to produce a distinct ID.
C) The IDs encode the pixel content of each image patch.
D) String hashes may vary across processes, and modulo reduction allows collisions.

Learner answer: D. Correct answer: D. Result: correct (1/1).

Python string hashes are randomized by default across processes; modulo10000 also allows distinct strings to share IDs. This is a toy stand-in for a tokenizer.


### p12-l23-a1-q1 — 2026-10-28

How does ColPali-style late interaction score a query against a page?

A) It averages every query-to-patch similarity into a single mean.
B) It selects one page patch and ignores all remaining query tokens.
C) It sums each query token’s highest similarity to any page patch.
D) It counts the number of characters shared by query and document IDs.

Learner answer: C. Correct answer: C. Result: correct (1/1).

MaxSim takes the maximum similarity over page patches separately for each query token, then sums those maxima.


### p12-l23-a1-q2 — 2026-10-28

You replace one embedding per page with 729 patch embeddings per page, keeping dimension and numeric precision fixed. What happens to raw vector storage?

A) It remains unchanged because the page count is the same.
B) It increases by a factor of729, before compression and metadata.
C) It decreases because each query uses only the best-matching patch.
D) It becomes independent of page count because vectors are cached.

Learner answer: B. Correct answer: B. Result: correct (1/1).

Raw vector bytes scale with pages×vectors per page×dimensions×bytes per value. Replacing one vector with729 multiplies the vector storage by729.


### p12-l23-a1-q3 — 2026-10-28

MaxSim receives a precomputed similarity matrix with query-token rows [[0.9, 0.2], [0.8, 0.1]]. What score does summing the row maxima produce?

A) 1.0
B) 0.5
C) 0.9
D) 1.7

Learner answer: D. Correct answer: D. Result: correct (1/1).

The maxima are0.9 and0.8, giving1.7. The same page patch may be selected by more than one query token; no one-to-one assignment is enforced.


### p12-l24-a1-q1 — 2026-10-28

What makes retrieval cross-modal?

A) A query in one modality retrieves relevant evidence in another modality.
B) A text query retrieves only text passages using two identical indexes.
C) A generator produces longer answers without retrieving evidence.
D) A system ranks documents only by their file size.

Learner answer: A. Correct answer: A. Result: correct (1/1).

Cross-modal retrieval connects query and evidence across modalities, such as text-to-image or image-to-text, using compatible representations or mappings.


### p12-l24-a1-q2 — 2026-10-28

Text and image retrievers return scores on very different numeric scales. What should you address before interpreting their weighted sum as balanced evidence?

A) Make all retrieved items have identical filenames.
B) Discard all source identities so the generator sees only scores.
C) Normalize or calibrate scores and evaluate the fusion weights on the task.
D) Assume the retriever with larger raw numbers is more reliable.

Learner answer: C. Correct answer: C. Result: correct (1/1).

Uncalibrated score scales can dominate fusion regardless of evidence quality. Normalization or calibration and task evaluation make the weighting meaningful.


### p12-l24-a1-q3 — 2026-10-28

The toy sets confidence=top[0][1], where the value is a weighted retrieval score, then compares it with confidence_floor. What does this confidence actually represent?

A) A calibrated probability that every answer claim is correct.
B) The top fused retrieval score used as a heuristic threshold.
C) A verified measure of agreement between independent human graders.
D) The fraction of generated claims proven by their cited sources.

Learner answer: A. Correct answer: B. Result: incorrect (0/1).

The code reuses the fused ranking score as confidence. It does not calibrate a probability or verify answer claims.


### p12-l25-a1-q1 — 2026-10-28

Why observe the browser again after executing a GUI action?

A) To assume the requested state change succeeded without checking it.
B) To replace every future action with the original fixed plan.
C) To avoid passing action outcomes back into the planning loop.
D) To check the resulting state and adjust the next action if needed.

Learner answer: D. Correct answer: D. Result: correct (1/1).

An observation closes the feedback loop: actions can fail or produce unexpected state, so the next decision should use the updated evidence.


### p12-l25-a1-q2 — 2026-10-28

A button moved after a page update, so an old click coordinate is stale. What is the best next step?

A) Repeat the same coordinate until the step budget expires.
B) Use the current screenshot or accessibility tree to locate the target again.
C) Mark the task complete because the earlier plan named the right button.
D) Drop all observations and continue the remaining actions unchanged.

Learner answer: B. Correct answer: B. Result: correct (1/1).

Grounding must use the current UI state. A semantic target description plus fresh screenshot or accessibility evidence allows the target to be located again.


### p12-l25-a1-q3 — 2026-10-28

run_task applies every planned action and then checks state.page==expected_page. apply_action treats done as a no-op. If page is confirmation, expected_page is reset_sent, and done says success=True, what is the reported success?

A) False, because the final page does not match expected_page.
B) True, because the done action explicitly claims success.
C) True, because any terminal action changes the page to expected_page.
D) An exception, because a done action must overwrite the page.

Learner answer: A. Correct answer: A. Result: correct (1/1).

Success comes from the final state comparison, not the supplied done.success flag. A done action leaves page unchanged, so confirmation != reset_sent yieldsFalse.

Initial phase complete: 62/75 (82.67%). Lessons01 and16 scored1/3; full fresh three-question remediation required.


### p12-l01-a2-q1 — 2026-10-28

After a shared projection embeds each image patch, what does adding positional information provide?

A) A different projection matrix trained separately for every input image.
B) A signal indicating where each patch lies in the image grid.
C) A guarantee that all patches produce the same hidden vector.
D) A replacement for the pixel values inside every patch.

Learner answer: B. Correct answer: B. Result: correct (1/1).

The shared projection maps patch content to a vector. Position information adds where the patch lies, distinguishing content representation from spatial location.


### p12-l01-a2-q2 — 2026-10-28

A 128×128 image is divided into 16×16 patches. One CLS token and two register tokens are added. What is the full transformer sequence length?

A) 64
B) 65
C) 66
D) 67

Learner answer: D. Correct answer: D. Result: correct (1/1).

There are8×8=64 patch tokens; adding1 CLS and2 registers gives67 total tokens.


### p12-l01-a2-q3 — 2026-10-28

patch_embed_params computes 3*p*p*hidden + hidden, including a bias. For p=4 and hidden=8, how many parameters does it return?

A) 392
B) 384
C) 128
D) 136

Learner answer: A. Correct answer: A. Result: correct (1/1).

Each RGB patch has3×4×4=48 values. Projection to8 dimensions uses48×8=384 weights plus8 bias parameters, totaling392.

Lesson01 attempt2 complete:3/3 replaces1/3; effective phase64/75 (85.33%). Lesson16 minimum still unmet.


### p12-l16-a2-q1 — 2026-10-28

An image tokenizer and a speech tokenizer both emit local code7. How should those codes be represented in a shared vocabulary that uses disjoint modality ranges?

A) Use global ID7 for both and discard modality information.
B) Map both codes to the same text token because their local IDs match.
C) Apply different modality offsets so they receive distinct global IDs.
D) Delete both codes because local code numbers must never repeat.

Learner answer: C. Correct answer: C. Result: correct (1/1).

Local code indices may repeat across codebooks; modality-specific offsets map them to distinct global IDs and prevent vocabulary collisions.


### p12-l16-a2-q2 — 2026-10-28

An image codebook has100 entries and starts at global ID200. Using a contiguous range with an exclusive end, where should the next modality range begin?

A) 299
B) 300
C) 301
D) 100

Learner answer: C. Correct answer: B. Result: incorrect (0/1).

The image codes occupy IDs200 through299. The exclusive end and next available ID are200+100=300.


### p12-l16-a2-q3 — 2026-10-28

route_inputs maps kind in ("speech", "voice") to "SpeechTokenizer residual-VQ" and uses "UNKNOWN" for unrecognized kinds. What paths result for kinds ["voice", "video"]?

A) ["UNKNOWN", "SEED-Tokenizer"]
B) ["BPE", "SpeechTokenizer residual-VQ"]
C) ["Encodec", "SEED-Tokenizer"]
D) ["SpeechTokenizer residual-VQ", "UNKNOWN"]

Learner answer: D. Correct answer: D. Result: correct (1/1).

Voice is an explicit alias for speech. Video has no matching branch in this toy router, so it receives UNKNOWN; the helper only labels paths.

Phase12 passed: initial62/75; effective65/75 (86.67%); cumulative67/81. Lesson01 retake3/3 and Lesson16 retake2/3 replace initial1/3 each. All25 lessons meet2/3 minimum. Quiz-based mastery; implementation labs not performed.
