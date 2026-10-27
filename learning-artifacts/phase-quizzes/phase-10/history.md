# Phase 10 detailed quiz history

Archive: read only when an earlier question or attempt is relevant. [Phase progress](progress.md).

## 2026-10-27 — Lesson 01, attempt 1

### p10-l01-a1-q1 — concept

How does WordPiece choose a merge differently from the BPE approach described in this lesson?

- A) It merges the pair with the fewest characters.
- B) It merges the pair with the highest raw count.
- C) It favors pairs with high co-occurrence relative to individual counts.
- D) It prunes the token with the smallest vocabulary ID.

Learner: C. Correct: C. Result: correct.

Explanation: The lesson contrasts BPE's raw adjacent-pair frequency with WordPiece's count(AB)/(count(A) × count(B)) score.

### p10-l01-a1-q2 — application

A tokenizer handles your target language using many more tokens per sentence than English. Which change would you test first to reduce that gap?

- A) Train on more target-language text and compare tokens per sentence.
- B) Remove target-language text and compare tokens per sentence.
- C) Shrink the vocabulary to bytes and compare tokens per sentence.
- D) Increase the model context and compare tokens per sentence.

Learner: A. Correct: A. Result: correct.

Explanation: The training corpus determines which subword merges exist; more representative target-language text can improve compression for that language.

### p10-l01-a1-q3 — code

In the lesson's byte-level BPETokenizer, training on 'aaaa' for one merge learns (97, 97) → 256. What does encode('aaaa') return?

- A) [97, 97, 97, 97]
- B) [97, 256, 97]
- C) [256, 97, 97]
- D) [256, 256]

Learner: D. Correct: D. Result: correct.

Explanation: _merge_pair scans left to right and consumes both bytes for each non-overlapping match, so the four a bytes form two merged tokens.

Lesson 01 attempt 1: 3/3. Effective lesson score: 3/3. Phase initial: 3/72 answered; phase completion pending.

## 2026-10-27 — Lesson 02, attempt 1

### p10-l02-a1-q1 — concept

Why does the lesson's tokenizer match special tokens before pre-tokenization and BPE?

- A) So their fixed IDs survive without being split or merged.
- B) So their byte lengths determine the merge order.
- C) So normalization can assign them temporary IDs.
- D) So the regex can learn them from corpus counts.

Learner: A. Correct: A. Result: correct.

Explanation: Special tokens are structural markers with reserved IDs. The tokenizer matches them exactly and sends only surrounding ordinary text through pre-tokenization and BPE.

### p10-l02-a1-q2 — application

Your trained BPE starts merging across spaces, creating tokens that span separate words. Which pipeline change directly prevents those merges?

- A) Increase the number of merges on the same byte stream.
- B) Run BPE separately on pre-tokenized chunks.
- C) Decode each merged token before counting pairs.
- D) Reserve additional IDs for special tokens.

Learner: C. Correct: B. Result: incorrect.

Explanation: The lesson's pre-tokenizer splits text into chunks, and BPE trains and encodes each chunk independently, so adjacent pairs cannot cross a chunk boundary.

### p10-l02-a1-q3 — code

With no BPE merges, the lesson's ProductionTokenizer adds '[END]' as its first special token. What does encode('A[END]B') return?

- A) [65, 91, 69, 78, 68, 93, 66]
- B) [256, 65, 66]
- C) [65, 256, 66]
- D) [65, 66, 256]

Learner: C. Correct: C. Result: correct.

Explanation: The first special token receives ID 256, while the surrounding ASCII characters use their byte IDs 65 and 66.

Lesson 02 attempt 1: 2/3. Effective lesson score: 2/3. Phase initial: 5 correct out of 6 answered; phase completion pending.

## 2026-10-27 — Lesson 03, attempt 1

### p10-l03-a1-q1 — concept

What is the role of LSH in the lesson's MinHash deduplication pipeline?

- A) It replaces each document with its most frequent shingle.
- B) It removes every pair whose document hashes differ.
- C) It computes exact Jaccard similarity for every document pair.
- D) It selects candidate pairs for an exact similarity check.

Learner: C. Correct: D. Result: incorrect.

Explanation: LSH groups similar MinHash signatures into buckets to find candidate pairs. The implementation then verifies candidates using exact Jaccard similarity before removing a document.

### p10-l03-a1-q2 — application

Two scraped articles contain nearly identical text but different advertisements. Exact document hashes miss them. Which approach best addresses this?

- A) Pad both documents to the same token length.
- B) Compare shingle sets using MinHash/LSH and Jaccard verification.
- C) Shuffle the documents before calculating exact hashes.
- D) Increase the batch size before tokenizing the documents.

Learner: B. Correct: B. Result: correct.

Explanation: Near-duplicate detection compares overlapping content rather than byte-for-byte equality. Shingles capture shared passages, and Jaccard verification checks candidate similarity.

### p10-l03-a1-q3 — code

The lesson's pack_sequences([10, 99, 20, 99], seq_length=4) returns mask [[1, 1, 1, 1]]. If 99 marks document endings, what does this mask establish?

- A) All positions contain real tokens; document isolation is not encoded.
- B) Each document can attend only to its own token positions.
- C) Only the two document-ending positions are visible to attention.
- D) Document-ending tokens are excluded from all training losses.

Learner: B. Correct: A. Result: incorrect.

Explanation: pack_sequences emits a one-dimensional real-token versus padding mask for each sequence. It does not construct a pairwise block-diagonal attention mask or loss mask.

Lesson 03 attempt 1: 1/3. Effective lesson score: 1/3. Requires a fresh three-question remediation set. Phase initial: 6 correct out of 9 answered; phase completion pending.

## 2026-10-27 — Lesson 04, attempt 1

### p10-l04-a1-q1 — concept

Why does GPT apply a causal mask during next-token training?

- A) To force every position to predict the same next token.
- B) To prevent a position from attending to future input tokens.
- C) To prevent a position from attending to earlier input tokens.
- D) To remove positional information from token embeddings.

Learner: B. Correct: B. Result: correct.

Explanation: A causal mask blocks attention to future positions so a next-token prediction cannot use the future token it is supposed to predict.

### p10-l04-a1-q2 — application

A training sample contains token IDs [12, 7, 9, 4]. Which input/target pair correctly implements the lesson's next-token objective?

- A) Input [12, 7, 9]; target [12, 7, 9].
- B) Input [7, 9, 4]; target [12, 7, 9].
- C) Input [12, 9, 4]; target [7, 9, 4].
- D) Input [12, 7, 9]; target [7, 9, 4].

Learner: D. Correct: D. Result: correct.

Explanation: Targets are shifted one position ahead of inputs: each input position is trained to predict the following token.

### p10-l04-a1-q3 — code

The lesson's generate function always divides logits by temperature, then samples with np.random.choice. Which change correctly supports temperature=0 as greedy decoding?

- A) Divide by zero, then normalize the resulting probabilities.
- B) Replace zero with one, then keep random sampling.
- C) Handle zero separately by choosing argmax of the logits.
- D) Set all logits to zero, then keep random sampling.

Learner: C. Correct: C. Result: correct.

Explanation: The supplied function has no zero-temperature branch. Division by zero can produce invalid sampling probabilities; greedy decoding should explicitly choose the maximum-logit token.

Lesson 04 attempt 1: 3/3. Effective lesson score: 3/3. Phase initial: 9 correct out of 12 answered; phase completion pending.

## 2026-10-27 — Lesson 05, attempt 1

### p10-l05-a1-q1 — concept

How does FSDP reduce persistent model-state memory per GPU compared with ordinary data parallelism?

- A) It stores a full model copy but removes all activations.
- B) It stores only different layer groups on each GPU.
- C) It shards parameters, gradients, and optimizer states across GPUs.
- D) It shares input batches while keeping full model states on each GPU.

Learner: C. Correct: C. Result: correct.

Explanation: Ordinary data parallelism replicates model states on each GPU. FSDP shards those states and temporarily gathers parameters needed for computation.

### p10-l05-a1-q2 — application

One large linear layer must be split across several GPUs, each computing a different subset of its output columns. Which strategy is this?

- A) Tensor parallelism.
- B) Pipeline parallelism.
- C) Ordinary data parallelism.
- D) Gradient accumulation.

Learner: A. Correct: A. Result: correct.

Explanation: Tensor parallelism partitions an individual layer. The lesson splits a weight matrix along its output dimension and concatenates the partial outputs.

### p10-l05-a1-q3 — code

The data-parallel simulator uses np.mean(gpu_gradients, axis=0). Two unequal shards contain 2 and 1 samples, with mean gradients 2 and 8. What does it return, and what is the sample-weighted mean?

- A) Returns 4; sample-weighted mean is 5.
- B) Returns 5; sample-weighted mean is 4.
- C) Returns 5; sample-weighted mean is 5.
- D) Returns 10; sample-weighted mean is 4.

Learner: B. Correct: B. Result: correct.

Explanation: The simulator averages shard means equally: (2+8)/2=5. Weighting by sample counts gives (2×2+1×8)/3=4; unequal shard sizes require weighted aggregation for the global sample mean.

Lesson 05 attempt 1: 3/3. Effective lesson score: 3/3. Phase initial: 12 correct out of 15 answered; phase completion pending.

## 2026-10-27 — Lesson 06, attempt 1

### p10-l06-a1-q1 — concept

In the lesson's response-only SFT objective, how are instruction tokens used?

- A) They are removed before the model computes its forward pass.
- B) They receive the same direct prediction loss as response tokens.
- C) They are replaced with padding before the assistant response.
- D) They provide context, while direct prediction loss covers response tokens.

Learner: D. Correct: D. Result: correct.

Explanation: The full instruction-response sequence supplies context. The loss mask excludes instruction targets and includes response targets; gradients from response predictions can still pass through computations involving the context.

### p10-l06-a1-q2 — application

After extended SFT, held-out instruction performance stops improving and held-out general-text loss rises. Which adjustment best addresses this?

- A) Raise the learning rate and add more epochs on the same examples.
- B) Reduce training duration or learning rate and check both evaluations.
- C) Remove the instruction context and keep training on responses alone.
- D) Evaluate only training responses and ignore the general-text loss.

Learner: B. Correct: B. Result: correct.

Explanation: The pattern suggests overfitting or forgetting. Smaller updates and earlier stopping can preserve general capabilities; both held-out instruction and general-text evaluations are needed to assess the tradeoff.

### p10-l06-a1-q3 — code

The supplied sft_train computes dlogits, but updates W1 using W1 -= lr * np.random.randn(*W1.shape) * 0.01. What is the key defect?

- A) The update uses random noise rather than a gradient derived from the loss.
- B) The update correctly implements masked-loss backpropagation through W1.
- C) The update freezes W1 because random values always average to zero.
- D) The update automatically applies Adam using dlogits as its state.

Learner: A. Correct: A. Result: correct.

Explanation: Computing dlogits is insufficient: it must be backpropagated through the model to obtain parameter gradients. The supplied updates instead perturb feedforward parameters with random noise.

Lesson 06 attempt 1: 3/3. Effective lesson score: 3/3. Phase initial: 15 correct out of 18 answered; phase completion pending.

## 2026-10-27 — Lesson 07, attempt 1

### p10-l07-a1-q1 — concept

What role does the frozen reference model play in the lesson's RLHF objective?

- A) It replaces human comparisons with randomly generated labels.
- B) It anchors a KL penalty that discourages excessive policy drift.
- C) It changes its weights after every policy update to match the policy.
- D) It directly assigns the scalar preference reward to each response.

Learner: B. Correct: B. Result: correct.

Explanation: The reference is a fixed checkpoint used to measure policy divergence. Penalizing that divergence limits drift, although it does not guarantee freedom from reward hacking.

### p10-l07-a1-q2 — application

During RLHF, reward-model scores rise while human reviewers find responses increasingly repetitive and unhelpful. What is the best interpretation?

- A) The rising scores prove that human reviewers are mistaken.
- B) The policy has necessarily failed to learn any reward signal.
- C) The reference model must have updated its weights incorrectly.
- D) The policy may be exploiting weaknesses in the reward model.

Learner: D. Correct: D. Result: correct.

Explanation: An imperfect reward model can reward patterns that do not improve actual quality. Higher proxy reward alongside worse human judgments is evidence to investigate reward hacking.

### p10-l07-a1-q3 — code

The function computes -log(sigmoid(r_preferred - r_rejected) + 1e-8). If both reward scores increase by 10, what happens to this pair's loss?

- A) It increases by 10 because both scores are larger.
- B) It decreases by 10 because both scores are larger.
- C) It stays unchanged because the score difference is unchanged.
- D) It becomes zero because both scores are positive.

Learner: C. Correct: C. Result: correct.

Explanation: Bradley-Terry loss depends on the difference between preferred and rejected scores. Adding a common constant cancels in the subtraction.

Lesson 07 attempt 1: 3/3. Effective lesson score: 3/3. Phase initial: 18 correct out of 21 answered; phase completion pending.

## 2026-10-27 — Lesson 08, attempt 1

### p10-l08-a1-q1 — concept

What does standard DPO remove from the reward-model-plus-PPO preference-training pipeline?

- A) The separately trained reward model and PPO optimization loop.
- B) The preference labels and all response likelihood calculations.
- C) The trainable policy and its next-token probability distribution.
- D) The reference probabilities and all use of a frozen checkpoint.

Learner: A. Correct: A. Result: correct.

Explanation: Standard DPO trains the policy directly on preference pairs using policy/reference log-probability ratios, without separately fitting a reward model or running PPO.

### p10-l08-a1-q2 — application

Your feedback dataset labels individual responses as good or bad, with no paired comparisons. Which method described in this lesson is designed for that format?

- A) Standard DPO on chosen/rejected pairs.
- B) KTO using unpaired binary feedback.
- C) PPO without any reward signal.
- D) MinHash using document shingles.

Learner: A. Correct: B. Result: incorrect.

Explanation: KTO accepts unpaired desirable/undesirable response labels, whereas standard DPO requires a preferred and rejected response for each prompt.

### p10-l08-a1-q3 — code

In dpo_loss, policy log-probabilities are preferred=-4 and rejected=-5; reference values are preferred=-6 and rejected=-4. With beta=0.1, what is logit = beta * (preferred_ratio - rejected_ratio)?

- A) -0.3
- B) -0.1
- C) 0.1
- D) 0.3

Learner: D. Correct: D. Result: correct.

Explanation: The preferred log ratio is -4-(-6)=2; the rejected log ratio is -5-(-4)=-1. Thus the logit is 0.1×(2-(-1))=0.3.

Lesson 08 attempt 1: 2/3. Effective lesson score: 2/3. Phase initial: 20 correct out of 24 answered; phase completion pending.

## 2026-10-27 — Lesson 09, attempt 1

### p10-l09-a1-q1 — concept

In Constitutional AI, what guides the model's critique and revision of a response?

- A) A rule that always selects the longest candidate response.
- B) A requirement to copy the initial response without changes.
- C) Written principles describing the desired response behavior.
- D) Random preference labels unrelated to the prompt or response.

Learner: C. Correct: C. Result: correct.

Explanation: The constitution supplies written principles against which responses are critiqued and revised. The quality of the resulting feedback still depends on the judge and the principles.

### p10-l09-a1-q2 — application

You can cheaply run trusted tests that verify whether generated code solves a task. Which feedback source best fits the lesson's rule-based outcome-reward approach?

- A) Use the test results to score each generated solution.
- B) Use response length as proof that the code is correct.
- C) Use the model's confident tone instead of executing tests.
- D) Use constitutional style preferences as a correctness guarantee.

Learner: D. Correct: A. Result: incorrect.

Explanation: A verifiable outcome such as trusted test results supplies an external correctness signal. It measures what the tests cover; style and confidence do not establish correctness.

### p10-l09-a1-q3 — code

The lesson's group_relative_advantage returns zeros when reward standard deviation is below 1e-8. What does it return for rewards [1.0, 1.0, 1.0, 1.0]?

- A) [1.0, 1.0, 1.0, 1.0]
- B) [0.25, 0.25, 0.25, 0.25]
- C) [-1.0, 0.0, 0.0, 1.0]
- D) [0.0, 0.0, 0.0, 0.0]

Learner: D. Correct: D. Result: correct.

Explanation: All rewards are equal, so standard deviation is zero and the explicit guard returns zeros. There is no within-group relative advantage; equal rewards alone do not establish mode collapse.

Lesson 09 attempt 1: 2/3. Effective lesson score: 2/3. Phase initial: 22 correct out of 27 answered; phase completion pending.

## 2026-10-27 — Lesson 10, attempt 1

### p10-l10-a1-q1 — concept

Why can training-data contamination make a benchmark score misleading?

- A) It guarantees that the model will fail every unseen task.
- B) It prevents the benchmark scorer from comparing predictions.
- C) It makes each test question require a different tokenizer.
- D) It lets memorized test material inflate measured performance.

Learner: B. Correct: D. Result: incorrect.

Explanation: If training includes test questions or answers, performance can reflect exposure to that material rather than generalization to unseen cases.

### p10-l10-a1-q2 — application

An LLM judge often picks whichever response appears first in a pair. Which evaluation change directly checks and reduces this position bias?

- A) Always put the model you expect to win first.
- B) Randomize response order and compare swapped-order judgments.
- C) Replace all reference answers with longer responses.
- D) Remove the rubric and ask for a faster judgment.

Learner: B. Correct: B. Result: correct.

Explanation: Randomized ordering reduces systematic advantage from presentation position. Swapping the same pair tests whether the judgment changes merely because the order changes.

### p10-l10-a1-q3 — code

The lesson's token_f1 converts lowercase whitespace-separated tokens into sets before computing overlap. What does token_f1("cat cat", "cat") return?

- A) 1.0, because repeated tokens collapse into one set member.
- B) 0.5, because the prediction contains twice as many tokens.
- C) 0.0, because the complete strings are not identical.
- D) 2.0, because the matching token appears twice.

Learner: A. Correct: A. Result: correct.

Explanation: Both token sets are {cat}, so precision and recall are both 1 and F1 is 1. This implementation ignores token multiplicity.

Lesson 10 attempt 1: 2/3. Effective lesson score: 2/3. Phase initial: 24 correct out of 30 answered; phase completion pending.

## 2026-10-27 — Lesson 11, attempt 1

### p10-l11-a1-q1 — concept

What distinguishes quantization-aware training (QAT) from post-training quantization (PTQ)?

- A) QAT removes all rounding, while PTQ uses only exact floating-point values.
- B) QAT exposes training to simulated quantization, while PTQ quantizes a trained model.
- C) QAT changes only the tokenizer, while PTQ changes only the context window.
- D) QAT always uses more bits per weight than PTQ, regardless of configuration.

Learner: B. Correct: B. Result: correct.

Explanation: QAT incorporates quantization effects into training so weights can adapt. PTQ converts an already trained model, often using calibration data without retraining its weights.

### p10-l11-a1-q2 — application

A weight matrix has channels with very different magnitudes. One shared scale rounds many small-channel weights to zero. Which change most directly addresses this?

- A) Use the largest channel's scale for every channel.
- B) Lower every channel's bit width without changing scales.
- C) Give each channel its own quantization scale.
- D) Discard the scale factors after rounding the weights.

Learner: D. Correct: C. Result: incorrect.

Explanation: Per-channel scales adapt the quantization step size to each channel's range, preserving small values that a global outlier-dominated scale can erase.

### p10-l11-a1-q3 — code

The toy quantize_symmetric uses num_bits=4 but stores its result with astype(np.int32). How much storage does each array element actually occupy, excluding scales?

- A) 4 bits, because num_bits overrides the NumPy dtype.
- B) 8 bits, because the result fits inside a byte.
- C) 16 bits, because the input model used FP16 weights.
- D) 32 bits, because the codes are stored as int32 values.

Learner: D. Correct: D. Result: correct.

Explanation: The bit-width argument limits the integer code range, but the NumPy dtype determines actual storage. Packed four-bit storage requires a separate packing representation.

Lesson 11 attempt 1: 2/3. Effective lesson score: 2/3. Phase initial: 26 correct out of 33 answered; phase completion pending.

## 2026-10-27 — Lesson 12, attempt 1

### p10-l12-a1-q1 — concept

What repeated computation does a KV cache avoid during autoregressive decoding?

- A) Recomputing key and value projections for earlier tokens.
- B) Computing attention scores between the new query and earlier keys.
- C) Computing the next-token probability distribution for the new position.
- D) Reading any earlier token information during the new decode step.

Learner: C. Correct: A. Result: incorrect.

Explanation: The cache retains prior key/value projections. Each new query still attends to cached keys and values, and the model still predicts the next-token distribution.

### p10-l12-a1-q2 — application

Requests have very different output lengths, and queued requests wait while finished slots sit idle in a static batch. Which change directly improves slot reuse?

- A) Wait for every request in the batch to finish before admitting more.
- B) Disable KV caching for all requests in the batch.
- C) Reserve a larger contiguous KV block for every request.
- D) Admit waiting requests at decode iterations as slots become free.

Learner: B. Correct: D. Result: incorrect.

Explanation: Continuous batching revisits the active batch each iteration so completed requests can be replaced by waiting ones without waiting for the longest output.

### p10-l12-a1-q3 — code

KVCache.update writes at self.seq_len but does not advance it. Starting at seq_len=0, you call update twice for the same layer with one token each and never call advance. What happens?

- A) Both tokens append, and seq_len automatically becomes 2.
- B) Both tokens append, but seq_len remains 0.
- C) The second write replaces position 0, and seq_len remains 0.
- D) The second write raises an error because position 0 is occupied.

Learner: C. Correct: C. Result: correct.

Explanation: Both calls use the unchanged cursor 0, so each writes the slice 0:1. The second token overwrites the first; callers must advance the cursor at the appropriate point.

Lesson 12 attempt 1: 1/3. Effective lesson score: 1/3. Requires a fresh three-question remediation set. Phase initial: 27 correct out of 36 answered; phase completion pending.

## 2026-10-27 — Lesson 13, attempt 1

### p10-l13-a1-q1 — concept

Why does the pipeline address artifacts by a hash of their contents?

- A) To guarantee that every training replay produces identical weights.
- B) To identify exact artifact contents and detect unintended changes.
- C) To prove that a checkpoint meets every evaluation threshold.
- D) To eliminate the need to record data and configuration versions.

Learner: B. Correct: B. Result: correct.

Explanation: A content hash identifies a particular byte sequence and helps detect corruption or unintended changes. It does not by itself establish quality or deterministic replay.

### p10-l13-a1-q2 — application

Quantized weights from stage 11 are found to be corrupt, while their upstream policy checkpoint is verified intact. What is the appropriate recovery scope in the lesson's DAG?

- A) Retrain the tokenizer and base model before checking anything else.
- B) Reuse the corrupt weights because the earlier policy eval passed.
- C) Rerun only the reward model and leave the server unchanged.
- D) Rebuild stage 11 and its server descendant, then reassess shipping.

Learner: D. Correct: D. Result: correct.

Explanation: Recovery invalidates the failed artifact and stages depending on it. Intact upstream checkpoints can be reused; the rebuilt serving artifact still needs an appropriate shipping decision.

### p10-l13-a1-q3 — code

The gate function checks each configured metric with eval_metrics.get(metric). If one required metric is absent and all other metrics pass, what does gate return and set?

- A) Returns False with a missing-metric HOLD reason; shippable=False.
- B) Returns True because missing metrics are skipped; shippable=True.
- C) Raises KeyError before updating the shippable field.
- D) Returns True after replacing the missing metric with its threshold.

Learner: C. Correct: A. Result: incorrect.

Explanation: The None branch records HOLD: missing metric, sets all_pass=False, and continues checking the rest. At the end it assigns manifest.shippable=all_pass and returns it with the reasons.

Lesson 13 attempt 1: 2/3. Effective lesson score: 2/3. Phase initial: 29 correct out of 39 answered; phase completion pending.

## 2026-10-27 — Lesson 14, attempt 1

### p10-l14-a1-q1 — concept

How does grouped-query attention (GQA) reduce KV-cache storage relative to full multi-head attention?

- A) It removes all query heads and stores only token embeddings.
- B) It gives every query head an additional independent key/value pair.
- C) It lets multiple query heads share fewer key/value heads.
- D) It replaces attention with a separate expert MLP for each token.

Learner: C. Correct: C. Result: correct.

Explanation: GQA retains multiple query heads while sharing key/value heads across groups. Fewer KV heads reduce the stored K/V values per token.

### p10-l14-a1-q2 — application

An MoE model activates only a small fraction of its experts for each token. What must you still account for when planning weight storage?

- A) Only the active experts exist as trained model weights.
- B) Inactive expert weights can always be reconstructed from the router.
- C) The router eliminates any need to load or store expert weights.
- D) All expert weights must be stored somewhere, even when inactive.

Learner: D. Correct: D. Result: correct.

Explanation: Sparse routing reduces per-token expert computation, but inactive experts remain part of the model. Their weights still require memory, offload storage, or distribution across devices.

### p10-l14-a1-q3 — code

The calculator uses config.get("head_dim", hidden_size // num_attention_heads). With hidden_size=3584, num_attention_heads=16, and head_dim=256 explicitly set, which head dimension does it return?

- A) 224
- B) 256
- C) 16
- D) 3584

Learner: A. Correct: B. Result: incorrect.

Explanation: The explicit head_dim field takes precedence over the fallback division, so the function returns 256 rather than 3584/16=224.

Lesson 14 attempt 1: 2/3. Effective lesson score: 2/3. Phase initial: 31 correct out of 42 answered; phase completion pending.

## 2026-10-27 — Lesson 15, attempt 1

### p10-l15-a1-q1 — concept

After rejecting a drafted token, which correction rule is required by the lesson's exact speculative-sampling algorithm?

- A) Keep the rejected token and lower the sampling temperature.
- B) Choose the draft distribution's highest-probability token.
- C) Sample from normalized max(0, verifier_probability - draft_probability).
- D) Sample uniformly from tokens that have not appeared in the prefix.

Learner: C. Correct: C. Result: correct.

Explanation: Acceptance uses min(1,q(d)/p(d)), and rejection requires the normalized positive residual (q-p). Together these yield the verifier distribution.

### p10-l15-a1-q2 — application

Increasing draft length emits more expected tokens per verifier call but also costs more draft computation. How should you choose the draft length?

- A) Minimize total expected time per emitted token, including draft cost.
- B) Always use the longest draft the context window can hold.
- C) Maximize proposed tokens while ignoring how many are accepted.
- D) Choose solely from verifier parameter count, ignoring draft quality.

Learner: A. Correct: A. Result: correct.

Explanation: The lesson compares (1+N*c) with the expected emitted-token count. More speculative tokens can help until added drafting cost outweighs the gain.

### p10-l15-a1-q3 — code

The residual function clamps q-p at zero, then normalizes. What does residual(q=[0.7, 0.3], p=[0.4, 0.6]) return?

- A) [0.7, 0.3]
- B) [0.4, 0.6]
- C) [0.5, 0.5]
- D) [1.0, 0.0]

Learner: D. Correct: D. Result: correct.

Explanation: The positive differences are [0.3,0]. Dividing by their sum 0.3 gives [1,0].

Lesson 15 attempt 1: 3/3. Effective lesson score: 3/3. Phase initial: 34 correct out of 45 answered; phase completion pending.

## 2026-10-27 — Lesson 16, attempt 1

### p10-l16-a1-q1 — concept

In differential attention, why can the combined weights A1 - lambda*A2 be negative?

- A) Each softmax branch already assigns negative probabilities.
- B) Subtracting two nonnegative attention maps can produce signed weights.
- C) The value vectors must be negative before attention is computed.
- D) The softmax normalization is omitted from both branches.

Learner: B. Correct: B. Result: correct.

Explanation: Each softmax map is nonnegative, but their scaled difference can be negative. The combined weights are signed coefficients rather than a probability distribution.

### p10-l16-a1-q2 — application

Both attention branches assign exactly the same map to signal and noise, and lambda=1. What should you expect from their subtraction?

- A) Only the noise cancels, while all signal is guaranteed to remain.
- B) The shared signal doubles, while the noise remains unchanged.
- C) The subtraction automatically renormalizes the map to uniform weights.
- D) Both shared signal and shared noise cancel, producing zero output.

Learner: D. Correct: D. Result: correct.

Explanation: When A1=A2 and lambda=1, their difference is zero everywhere. Useful cancellation requires the branches to differ in how they represent the desired signal.

### p10-l16-a1-q3 — code

For A1=[0.8,0.2], A2=[0.3,0.7], lambda=1, and scalar values V=[10,2], what is sum((A1[i]-lambda*A2[i])*V[i])?

- A) 4.0
- B) 6.0
- C) 8.4
- D) 0.0

Learner: A. Correct: A. Result: correct.

Explanation: The differential weights are [0.5,-0.5]. Their weighted sum is 0.5×10-0.5×2=4.

Lesson 16 attempt 1: 3/3. Effective lesson score: 3/3. Phase initial: 37 correct out of 48 answered; phase completion pending.

## 2026-10-27 — Lesson 17, attempt 1

### p10-l17-a1-q1 — concept

Which three views of context does the lesson's Native Sparse Attention combine?

- A) Compressed block summaries, selected fine-grained blocks, and a local window.
- B) Three full-context attention maps with identical keys and values.
- C) Token embeddings, optimizer moments, and parameter gradients.
- D) A draft model, a reward model, and a frozen reference policy.

Learner: A. Correct: A. Result: correct.

Explanation: The compressed branch supplies a coarse global view, the selected branch reads detailed relevant blocks, and the sliding window preserves local context.

### p10-l17-a1-q2 — application

A query needs exact details from an old block outside the local window, and the compressed branch ranks that block highly. Which branch reads its original tokens?

- A) The sliding-window branch, which always includes every old block.
- B) The selected branch, which loads uncompressed tokens from top-ranked blocks.
- C) The compressed branch, which permanently deletes all block summaries.
- D) The gate alone, which reconstructs original tokens from three scalar weights.

Learner: B. Correct: B. Result: correct.

Explanation: Compressed attention helps choose relevant blocks. The selected branch then loads their original uncompressed keys and values for fine-grained attention.

### p10-l17-a1-q3 — code

The toy gate applies sigmoid separately to three query projections. If all three logits are zero, what gate weights does it produce?

- A) [0.0, 0.0, 0.0], with sum 0.0.
- B) [1/3, 1/3, 1/3], with sum 1.0.
- C) [1.0, 1.0, 1.0], with sum 3.0.
- D) [0.5, 0.5, 0.5], with sum 1.5.

Learner: D. Correct: D. Result: correct.

Explanation: Sigmoid(0)=0.5 for each branch. Independent sigmoid gates are not softmax-normalized and need not sum to one.

Lesson 17 attempt 1: 3/3. Effective lesson score: 3/3. Phase initial: 40 correct out of 51 answered; phase completion pending.

## 2026-10-27 — Lesson 18, attempt 1

### p10-l18-a1-q1 — concept

What distinguishes the lesson's sequential MTP design from independent parallel future-token heads?

- A) Each depth ignores every token after the original prefix.
- B) Each depth uses an unrelated vocabulary with no shared embeddings.
- C) Later depths combine the previous-depth state with an intermediate token embedding.
- D) Later depths predict only the current token rather than future tokens.

Learner: C. Correct: C. Result: correct.

Explanation: Sequential MTP passes information through depth-specific modules conditioned on intermediate tokens. Independent parallel heads instead predict future offsets directly from the same backbone state.

### p10-l18-a1-q2 — application

You want to limit the parameter overhead of adding several MTP modules. Which sharing strategy described in the lesson directly helps?

- A) Duplicate the full embedding and output matrices at every depth.
- B) Reuse the main model's embedding and output head across depths.
- C) Remove the backbone and keep only the vocabulary IDs.
- D) Use a separate tokenizer and vocabulary for every prediction depth.

Learner: A. Correct: B. Result: incorrect.

Explanation: Sharing the embedding and output head avoids adding another vocabulary-sized pair of matrices per depth. Depth-specific projection and transformer parameters are still added.

### p10-l18-a1-q3 — code

The code aggregates total = (lam / D) * sum(per_depth). With lam=0.3, D=2, and per_depth=[2.0,4.0], what is the auxiliary MTP loss?

- A) 0.9
- B) 1.8
- C) 3.0
- D) 6.3

Learner: A. Correct: A. Result: correct.

Explanation: The auxiliary loss is 0.3/2×(2+4)=0.9. This is the auxiliary term, not the full main-plus-MTP training loss.

Lesson 18 attempt 1: 2/3. Effective lesson score: 2/3. Phase initial: 42 correct out of 54 answered; phase completion pending.

## 2026-10-27 — Lesson 19, attempt 1

### p10-l19-a1-q1 — concept

What is the main scheduling goal of overlapping MoE all-to-all communication with computation?

- A) To remove the need to route tokens to experts.
- B) To keep GPUs doing useful computation while communication proceeds.
- C) To guarantee that every GPU stores every expert.
- D) To replace all backward passes with forward passes.

Learner: B. Correct: B. Result: correct.

Explanation: Overlap hides some communication time behind independent computation, reducing time spent waiting. It does not eliminate the communication itself.

### p10-l19-a1-q2 — application

In the lesson's schedule comparison, parameter replication is a memory concern and expert communication overlap is less important. Which tradeoff motivates DualPipeV?

- A) Keep two parameter copies and disable every backward pass.
- B) Add more parameter copies to eliminate all activation storage.
- C) Remove all pipeline stages and run only expert routing.
- D) Use one parameter copy while accepting a somewhat larger bubble.

Learner: D. Correct: D. Result: correct.

Explanation: The lesson presents DualPipeV as reducing parameter-copy memory at the expense of a modest bubble/overlap tradeoff compared with DualPipe.

### p10-l19-a1-q3 — code

The simulator computes bubble_1f1b(P,M) = 2*(P-1) / (2*M + 2*(P-1)). What does it return for P=4 and M=3?

- A) 0.0
- B) 0.25
- C) 0.5
- D) 1.0

Learner: C. Correct: C. Result: correct.

Explanation: The numerator is 2×3=6 and the denominator is 2×3+2×3=12, so the fraction is 0.5.

Lesson 19 attempt 1: 3/3. Effective lesson score: 3/3. Phase initial: 45 correct out of 57 answered; phase completion pending.

## 2026-10-27 — Lesson 20, attempt 1

### p10-l20-a1-q1 — concept

What is the central KV-storage idea behind Multi-Head Latent Attention (MLA)?

- A) Represent key/value information with a shared low-rank latent.
- B) Store a full independent model checkpoint for every query head.
- C) Replace every attention block with an always-on expert MLP.
- D) Cache only the next-token ID and discard all attention state.

Learner: A. Correct: A. Result: correct.

Explanation: MLA compresses key/value information into a shared latent representation, reducing cached state relative to storing full per-head keys and values. A faithful cache budget also accounts for required positional components.

### p10-l20-a1-q2 — application

In the lesson's bias-adjusted load-balancing scheme, one routed expert is overloaded. Which adjustment discourages routing more tokens to it?

- A) Increase its selection bias while leaving all others fixed.
- B) Delete the shared expert and route every token to the overloaded one.
- C) Decrease the overloaded expert's selection bias.
- D) Increase the number of stored tokenizer vocabulary entries.

Learner: C. Correct: C. Result: correct.

Explanation: Reducing an overloaded expert's selection bias makes it less likely to be selected; underloaded experts can receive increased bias. This is an adjustment to routing selection.

### p10-l20-a1-q3 — code

The simplified calculator uses kv_cache = num_layers * kv_lora_rank * context_length * 2. If only kv_lora_rank changes from 512 to 256, what happens to its estimate?

- A) It doubles.
- B) It halves.
- C) It stays unchanged.
- D) It becomes zero.

Learner: B. Correct: B. Result: correct.

Explanation: The toy formula is linear in kv_lora_rank, so halving that rank halves its estimate when other inputs stay fixed. This is the supplied simplified formula, not a full production cache budget.

Lesson 20 attempt 1: 3/3. Effective lesson score: 3/3. Phase initial: 48 correct out of 60 answered; phase completion pending.

## 2026-10-27 — Lesson 21, attempt 1

### p10-l21-a1-q1 — concept

Why can a recurrent SSM layer keep its inference state size constant as a sequence grows?

- A) It stores every earlier key and value in a larger cache.
- B) It ignores the current input after the first token.
- C) It updates a fixed-size state using the prior state and current input.
- D) It reruns the entire input history to avoid storing any state.

Learner: C. Correct: C. Result: correct.

Explanation: The recurrence carries a fixed-size summary forward. Unlike a full attention KV cache, that state need not grow with sequence length for a fixed model configuration.

### p10-l21-a1-q2 — application

A hybrid calculator reports that KV cache plus SSM state fits within GPU memory. What must you check before concluding the full deployment fits?

- A) Add weight storage and runtime memory needs to the budget.
- B) Assume inactive MoE expert weights require no storage.
- C) Ignore model weights because SSM states already contain them.
- D) Treat the cache estimate as the full GPU allocation.

Learner: A. Correct: A. Result: correct.

Explanation: The calculator covers attention cache and SSM state. Model weights, workspaces, activations, batching, and other runtime overheads also consume memory.

### p10-l21-a1-q3 — code

The toy KV-cache formula is linear in attn_layers. Holding KV heads, head dimension, context, and dtype fixed, how does a 4-attention-layer hybrid compare with a 32-attention-layer baseline?

- A) It needs the same KV-cache memory.
- B) It needs four times the KV-cache memory.
- C) It needs half the KV-cache memory.
- D) It needs one-eighth the KV-cache memory.

Learner: D. Correct: D. Result: correct.

Explanation: The ratio is 4/32=1/8 for the KV-cache term. The hybrid also has a separate fixed-size SSM state term.

Lesson 21 attempt 1: 3/3. Effective lesson score: 3/3. Phase initial: 51 correct out of 63 answered; phase completion pending.

## 2026-10-27 — Lesson 22, attempt 1

### p10-l22-a1-q1 — concept

In the lesson's Hogwild-style setup, how can workers observe and react to each other's generated work?

- A) They remain isolated until a final majority vote.
- B) They discard all earlier outputs after every generation step.
- C) They read a shared context/cache containing other workers' writes.
- D) They receive a new separately fine-tuned model after each write.

Learner: C. Correct: C. Result: correct.

Explanation: The defining shared-context setup lets workers inspect work already written and adjust their next contribution. The toy implements this with a shared token list.

### p10-l22-a1-q2 — application

A task is short, mostly sequential, and requires substantial coordination between workers. What should you expect when adding more workers?

- A) Guaranteed linear speedup regardless of communication costs.
- B) Coordination overhead can outweigh the limited parallelism and slow it down.
- C) The sequential part vanishes automatically once two workers start.
- D) The task becomes parallelizable because the cache is shared.

Learner: B. Correct: B. Result: correct.

Explanation: Only the parallelizable fraction benefits from extra workers, while coordination adds cost. Short, mostly sequential tasks can therefore become slower.

### p10-l22-a1-q3 — code

The toy resets seen_work_categories each step and increments progress only for the first A or B occurrence in that step. If two workers both emit A during one step, how much does progress increase?

- A) 0
- B) 2
- C) 4
- D) 1

Learner: B. Correct: D. Result: incorrect.

Explanation: The first A is counted and added to the set; the second A in the same step is tagged redundant. The set resets for the next step.

Lesson 22 attempt 1: 2/3. Effective lesson score: 2/3. Phase initial: 53 correct out of 66 answered; phase completion pending.

## 2026-10-27 — Lesson 25, attempt 1

### p10-l25-a1-q1 — concept

What must a tree attention mask prevent when verifying alternative speculative branches?

- A) A candidate attending to the shared prompt or its ancestors.
- B) A candidate attending to tokens on competing sibling branches.
- C) The verifier computing logits for more than one candidate.
- D) A candidate attending to its own position in the tree.

Learner: B. Correct: B. Result: correct.

Explanation: Each candidate should be conditioned on its own prefix path, not on mutually exclusive sibling alternatives. The toy mask includes self and ancestors.

### p10-l25-a1-q2 — application

A heavily batched server already uses most available compute, and speculative verification adds substantial work. What is the best way to decide whether speculation helps?

- A) Assume every emitted draft token guarantees a wall-time speedup.
- B) Compare only the number of target calls and ignore their cost.
- C) Measure end-to-end latency and throughput with draft/verify overhead included.
- D) Increase draft length until all free KV-cache memory is consumed.

Learner: C. Correct: C. Result: correct.

Explanation: Tokens per verification do not alone determine wall time. At high utilization, extra draft and verification work can offset savings, so measure the actual workload.

### p10-l25-a1-q3 — code

The acceptance test is u < min(1, target_prob/draft_prob). For a proposed token with target_prob=0.2, draft_prob=0.5, and u=0.3, what happens?

- A) Accept, because 0.3 < 0.4.
- B) Reject, because 0.2 < 0.5.
- C) Accept, because 0.3 < 1.0 regardless of the ratio.
- D) Reject, because the target probability must exceed 0.5.

Learner: A. Correct: A. Result: correct.

Explanation: The acceptance probability is min(1,0.2/0.5)=0.4. Since the sampled uniform value 0.3 is below it, this proposal is accepted.

Lesson 25 attempt 1: 3/3. Effective lesson score: 3/3. Phase initial: 56 correct out of 69 answered; phase completion pending.

## 2026-10-27 — Lesson 34, attempt 1

### p10-l34-a1-q1 — concept

What resource tradeoff does activation checkpointing make during training?

- A) It reduces parameter storage by deleting optimizer updates.
- B) It saves activation memory by recomputing intermediates during backward.
- C) It removes backward computation by keeping every activation.
- D) It shortens the training dataset to avoid storing any model state.

Learner: B. Correct: B. Result: correct.

Explanation: Checkpointing keeps selected boundary inputs and reconstructs intermediates when backward needs them, trading extra computation for lower saved-activation memory.

### p10-l34-a1-q2 — application

You add checkpointing to a deterministic toy network. Which comparison most directly verifies that recomputation preserves training calculations?

- A) Check only that the checkpointed run prints fewer arrays.
- B) Compare the number of model parameters before and after.
- C) Compare forward outputs and parameter gradients using identical inputs and weights.
- D) Confirm that the checkpointed run has a longer wall-clock time.

Learner: C. Correct: C. Result: correct.

Explanation: Matching outputs and parameter gradients checks the functional forward and backward results. For stochastic or stateful layers, recomputation must also reproduce the relevant random/state behavior.

### p10-l34-a1-q3 — code

For an FFN, should_recompute returns recompute_flops_ratio < 0.1 when activation_bytes_mb > 500; otherwise False. What does it return for 600 MB and a ratio of exactly 0.1?

- A) True, because the activation exceeds 500 MB.
- B) True, because 0.1 is included in the ratio threshold.
- C) It raises an error because the ratio equals the threshold.
- D) False, because the ratio test is strictly less than 0.1.

Learner: D. Correct: D. Result: correct.

Explanation: 600>500 selects the FFN ratio branch, but 0.1<0.1 is false. The code uses a strict comparison.

Lesson 34 attempt 1: 3/3. Effective lesson score: 3/3.

## Initial phase review complete — 2026-10-27

Initial: 59/72 (81.94%). Effective: 59/72. Cumulative: 59/72. All 24 lesson sets answered. Phase not passed: overall below 85%; Lessons03 and12 each scored 1/3. Begin fresh scored three-question sets for those lessons; retain initial evidence.

## 2026-10-27 — Lesson 03, attempt 2 (remediation)

### p10-l03-a2-q1 — concept

Two documents land in the same LSH bucket. Why does the lesson's pipeline still compare their shingle sets before removing a copy?

- A) A bucket match proves that their raw bytes are identical.
- B) A bucket match only identifies candidates; actual similarity still needs verification.
- C) Jaccard similarity determines the tokenizer's vocabulary IDs.
- D) The comparison is needed only to choose a padding length.

Learner: B. Correct: B. Result: correct.

Explanation: LSH narrows the candidate search and can group dissimilar items. Exact shingle-set Jaccard similarity verifies whether the pair meets the removal threshold.

### p10-l03-a2-q2 — application

Two independent documents are packed together for causal language-model training. You require that neither document use the other as context. What mask enforces that requirement?

- A) A vector of ones for all non-padding positions.
- B) An EOS token alone with unrestricted cross-document attention.
- C) One ordinary causal mask across the entire packed sequence.
- D) A causal mask within each document block that blocks cross-document pairs.

Learner: D. Correct: D. Result: correct.

Explanation: A block-diagonal causal mask allows each token to attend only to its own document's earlier positions and itself. Padding masks and EOS markers alone do not enforce this isolation.

### p10-l03-a2-q3 — code

pack_sequences slices token IDs into chunks and pads the final chunk, marking real tokens 1 and padding 0. For tokens=[5,6,7], seq_length=2, pad_id=0, what are the final sequence and mask?

- A) Sequence [7,0]; mask [1,0].
- B) Sequence [7,0]; mask [1,1].
- C) Sequence [0,7]; mask [0,1].
- D) Sequence [7]; mask [1].

Learner: A. Correct: A. Result: correct.

Explanation: The first chunk is [5,6]. The final chunk [7] receives one padding token, giving [7,0] with mask [1,0].

Lesson 03 attempt 2: 3/3 replaces initial 1/3 in effective score. Initial remains 59/72; effective 61/72 (84.72%); cumulative 62/75. Lesson12 remediation remains; phase not passed.

## 2026-10-27 — Lesson 12, attempt 2 (remediation)

### p10-l12-a2-q1 — concept

With earlier key/value projections cached, what must still happen for the newly processed token during decode?

- A) Every earlier token must have its key/value projections recomputed.
- B) The model can skip predicting a next-token distribution entirely.
- C) Its query attends to cached keys/values before predicting the next token.
- D) All model weights are replaced by the cached key/value vectors.

Learner: C. Correct: C. Result: correct.

Explanation: KV caching reuses old projections. Computation for the new token, attention over available context, and next-token prediction still occur.

### p10-l12-a2-q2 — application

Two batch slots are occupied. One request finishes after step 2; the other needs eight more steps. Under continuous batching, what should happen to a waiting request if capacity permits?

- A) It must wait until the longer request finishes.
- B) It replaces the longer request and discards that request's output.
- C) It starts only after both existing KV caches are erased.
- D) It can enter the freed slot at the next scheduling iteration.

Learner: D. Correct: D. Result: correct.

Explanation: Continuous batching reuses a completed request's slot without waiting for other active requests to finish, subject to resource and scheduling constraints.

### p10-l12-a2-q3 — code

KVCache preallocates arrays to max_seq_len. memory_bytes returns their nbytes; used_bytes is proportional to seq_len. Below capacity, what changes after advance(1)?

- A) Used bytes increase; allocated memory_bytes stays unchanged.
- B) Allocated memory_bytes increases; used bytes stay unchanged.
- C) Both allocated and used bytes become zero.
- D) Neither changes because advance never changes seq_len.

Learner: A. Correct: A. Result: correct.

Explanation: advance increments seq_len, increasing logical usage. It does not resize the already allocated arrays, so their nbytes remains constant.

Lesson 12 attempt 2: 3/3 replaces initial 1/3 in effective score.

## Phase10 passed — 2026-10-27

Initial: 59/72 (81.94%). Effective latest complete sets: 63/72 (87.50%). Cumulative: 65/78. Both remediation sets scored 3/3; all 24 lessons meet the 2/3 minimum. Mastery credit is quiz-based; implementation labs were not performed in this assessment. Original misses and corrections remain in this archive and review.md.
