# Phase 07 detailed quiz history

Archive: read only when an earlier question or attempt is relevant. [Phase progress](progress.md).

No questions presented yet.

## p07-l01-a1-q1 — 2026-10-26

Why can a standard RNN not compute all hidden states across a sequence simultaneously during training?

A) Each hidden state must have a different vector dimension.
B) Each hidden state depends on the preceding hidden state.
C) Each input token must use a separately trained weight matrix.
D) Each input token must attend to all future input tokens.

Learner answer: D
Correct answer: B
Result: Incorrect
Explanation: The recurrence h_t = f(h_(t-1), x_t) creates a dependency chain along the sequence.

## p07-l01-a1-q2 — 2026-10-26

An implementation explicitly stores a dense attention score matrix for a sequence of N tokens. If the sequence length doubles while other dimensions stay fixed, how does the number of score entries change?

A) It stays approximately the same.
B) It grows by a factor of two.
C) It grows by a factor of four.
D) It grows by a factor of eight.

Learner answer: D
Correct answer: C
Result: Incorrect
Explanation: A dense score matrix has N squared entries; (2N) squared is four times N squared.

## p07-l01-a1-q3 — 2026-10-26

For xs = [2.0, 4.0], what do the two lesson functions return?

```python
def rnn_style(xs):
    h = 0.0
    for x in xs:
        h = 0.9 * h + x
    return h

def attention_style(xs):
    return sum(xs) / len(xs)
```

A) rnn_style: 5.8; attention_style: 3.0
B) rnn_style: 6.0; attention_style: 3.0
C) rnn_style: 5.8; attention_style: 6.0
D) rnn_style: 3.0; attention_style: 5.8

Learner answer: B
Correct answer: A
Result: Incorrect
Explanation: The recurrence gives h=2.0 then h=0.9*2+4=5.8; the mean is (2+4)/2=3.0. These toy functions compute different quantities.

## p07-l02-a1-q1 — 2026-10-26

Why does scaled dot-product attention divide query–key scores by the square root of the key dimension?

A) To make every token receive the same attention weight.
B) To prevent the value vectors from changing dimension.
C) To remove the need for learned query and key projections.
D) To limit score growth that can cause softmax saturation.

Learner answer: D
Correct answer: D
Result: Correct
Explanation: As key dimension increases, unscaled dot products tend to grow in magnitude. Scaling helps avoid overly peaked softmax distributions and very small gradients.

## p07-l02-a1-q2 — 2026-10-26

You are adding causal masking so each token can attend only to itself and earlier tokens. What should happen to scores for future positions?

A) Set them to zero after the softmax, without renormalizing.
B) Set them to negative infinity before applying softmax.
C) Set them to positive infinity before applying softmax.
D) Set their corresponding value vectors to all ones.

Learner answer: B
Correct answer: B
Result: Correct
Explanation: Negative infinity before softmax gives future positions zero probability while normalizing over allowed positions.

## p07-l02-a1-q3 — 2026-10-26

Given these attention weights and value vectors, what is weights @ V?

```python
weights = np.array([[0.25, 0.75]])
V = np.array([[4.0, 0.0], [0.0, 8.0]])
output = weights @ V
```

A) [[1.0, 6.0]]
B) [[3.0, 2.0]]
C) [[4.0, 8.0]]
D) [[0.25, 0.75]]

Learner answer: A
Correct answer: A
Result: Correct
Explanation: The output is 0.25*[4,0] + 0.75*[0,8] = [1,6].

## p07-l03-a1-q1 — 2026-10-26

What is the main representational benefit of multi-head attention over a single attention head?

A) It guarantees that every head learns a distinct grammatical rule.
B) It lets heads attend through different learned projection subspaces.
C) It removes the need to compute similarities between token positions.
D) It forces every head to share the same attention weight matrix.

Learner answer: B
Correct answer: B
Result: Correct
Explanation: Different learned projections allow heads to form different attention patterns and combine complementary information; distinct specialization is not guaranteed.

## p07-l03-a1-q2 — 2026-10-26

You replace 16 KV heads with 4 KV heads using grouped-query attention, keeping head dimension, sequence length, layers, batch size, and cache precision fixed. What happens to the stored KV-cache size?

A) It becomes one quarter of the original size.
B) It becomes one half of the original size.
C) It stays the same as the original size.
D) It becomes four times the original size.

Learner answer: A
Correct answer: A
Result: Correct
Explanation: The stored cache scales with KV head count, so 4/16 gives one quarter of the original size.

## p07-l03-a1-q3 — 2026-10-26

For X.shape == (5, 12) and n_heads == 3, what shape does split_heads return?

```python
def split_heads(X, n_heads):
    n, d = X.shape
    d_head = d // n_heads
    return X.reshape(n, n_heads, d_head).transpose(1, 0, 2)
```

A) (5, 3, 4)
B) (3, 4, 5)
C) (5, 4, 3)
D) (3, 5, 4)

Learner answer: D
Correct answer: D
Result: Correct
Explanation: The reshape produces (5,3,4), then transpose(1,0,2) swaps the first two axes to (3,5,4).

## p07-l04-a1-q1 — 2026-10-26

Without positional signals or masks, what happens when the input token rows of a self-attention layer are permuted?

A) The output rows stay in their original order regardless of the input.
B) The layer reconstructs the original order from query–key similarities.
C) The output rows follow the same permutation as the input rows.
D) The layer assigns each token a new absolute position automatically.

Learner answer: B
Correct answer: C
Result: Incorrect
Explanation: Unmasked self-attention without positional information is permutation equivariant: permuting inputs permutes outputs in the same way. It does not encode sequence order by itself.

## p07-l04-a1-q2 — 2026-10-26

You hold query and key vectors fixed, apply standard RoPE at positions 3 and 8, then repeat at positions 13 and 18. How do the resulting query–key dot products compare?

A) They match within floating-point error because the relative gap is unchanged.
B) The second is twice as large because both positions increased by ten.
C) The second becomes zero because the two rotation angles are different.
D) They must differ because RoPE uses absolute positions for its rotations.

Learner answer: A
Correct answer: A
Result: Correct
Explanation: For fixed vectors and frequencies, a common position shift cancels in the relative rotation, preserving the dot product.

## p07-l04-a1-q3 — 2026-10-26

What does this ALiBi-style bias row contain?

```python
m = 0.5
i = 2
row = [-m * abs(i - j) for j in range(4)]
```

A) [0.0, -0.5, -1.0, -1.5]
B) [1.0, 0.5, 0.0, 0.5]
C) [-1.0, -0.5, 0.0, 0.5]
D) [-1.0, -0.5, 0.0, -0.5]

Learner answer: C
Correct answer: D
Result: Incorrect
Explanation: Distances from i=2 are [2,1,0,1]; multiplying each by -0.5 gives [-1,-0.5,0,-0.5].

## p07-l05-a1-q1 — 2026-10-26

In an encoder–decoder transformer, where do the queries, keys, and values for decoder cross-attention come from?

A) Queries and keys come from the encoder; values come from the decoder.
B) Queries, keys, and values all come from the decoder hidden states.
C) Queries come from the decoder; keys and values come from encoder outputs.
D) Queries come from the encoder; keys and values come from decoder states.

Learner answer: C
Correct answer: C
Result: Correct
Explanation: Decoder cross-attention uses decoder states to query the encoded source, which provides the keys and values.

## p07-l05-a1-q2 — 2026-10-26

You adapt an encoder–decoder block into a standard GPT-style decoder-only block. Which change preserves the intended architecture?

A) Remove cross-attention; retain causal self-attention and the feed-forward sublayer.
B) Remove causal self-attention; retain cross-attention and the feed-forward sublayer.
C) Remove the feed-forward sublayer; retain cross-attention and unmasked self-attention.
D) Remove the causal mask; retain cross-attention to an empty encoder output.

Learner answer: C
Correct answer: A
Result: Incorrect
Explanation: A standard decoder-only block omits encoder cross-attention while retaining causal self-attention, an FFN, normalization, and residual connections.

## p07-l05-a1-q3 — 2026-10-26

Which expression implements a pre-norm residual sublayer?

A) LN(x + sublayer(x))
B) sublayer(x + LN(x))
C) LN(x) + sublayer(x)
D) x + sublayer(LN(x))

Learner answer: A
Correct answer: D
Result: Incorrect
Explanation: Pre-norm normalizes the input to the sublayer and adds its output back to the unchanged residual input x.

## p07-l06-a1-q1 — 2026-10-26

What distinguishes BERT’s masked language modeling objective from standard causal next-token prediction?

A) It predicts selected original tokens using context from both sides.
B) It predicts every next token using only the preceding token context.
C) It reconstructs sentence order without predicting any token identities.
D) It predicts selected original tokens using only the following tokens.

Learner answer: D
Correct answer: A
Result: Incorrect
Explanation: BERT predicts original tokens at selected positions with bidirectional context, whereas causal next-token prediction conditions on preceding tokens.

## p07-l06-a1-q2 — 2026-10-26

Under original BERT’s 15% selection rate and 80/10/10 corruption rule, approximately how many of 1,000 eligible tokens are replaced with [MASK]?

A) 15
B) 80
C) 150
D) 120

Learner answer: D
Correct answer: D
Result: Correct
Explanation: About 150 tokens are selected, and 80% of those (120) are replaced with [MASK].

## p07-l06-a1-q3 — 2026-10-26

A token with original ID 7 is selected for MLM prediction. The corruption draw r is 0.95. What are input_ids[i] and labels[i] after this code?

```python
labels[i] = t
r = 0.95
if r < 0.8:
    input_ids[i] = MASK_ID
elif r < 0.9:
    input_ids[i] = rng.randrange(vocab_size)
# input_ids initially contains the original tokens
```

A) input_ids[i] = MASK_ID; labels[i] = 7
B) input_ids[i] = 7; labels[i] = -100
C) input_ids[i] = 7; labels[i] = 7
D) input_ids[i] = a random token; labels[i] = 7

Learner answer: D
Correct answer: C
Result: Incorrect
Explanation: The selected token retains its original label. Neither replacement branch runs at r=0.95, so the input remains 7 and still contributes to the prediction loss.

## p07-l07-a1-q1 — 2026-10-26

Why can causal language-model training compute predictions at all sequence positions in parallel, while ordinary autoregressive generation proceeds token by token?

A) Training removes the causal mask, while generation restores it.
B) Training knows the true prefix tokens; generation must produce new prefix tokens.
C) Training predicts all tokens independently, while generation uses no attention.
D) Training uses encoder cross-attention, while generation uses self-attention.

Learner answer: C
Correct answer: B
Result: Incorrect
Explanation: Teacher-forced training provides all ground-truth input tokens, and a causal mask prevents future leakage. During ordinary generation, each new token is needed to form the prefix for the next prediction.

## p07-l07-a1-q2 — 2026-10-26

For the token sequence [11, 22, 33, 44], which input–target pair correctly trains next-token prediction with a one-token shift?

A) Inputs [11, 22, 33]; targets [11, 22, 33].
B) Inputs [22, 33, 44]; targets [11, 22, 33].
C) Inputs [11, 33, 44]; targets [22, 33, 44].
D) Inputs [11, 22, 33]; targets [22, 33, 44].

Learner answer: D
Correct answer: D
Result: Correct
Explanation: Each input position predicts the next token, so the targets are shifted one position ahead.

## p07-l07-a1-q3 — 2026-10-26

What is causal_mask(3)[1] (using zero-based indexing)?

```python
def causal_mask(n):
    return [[0.0 if j <= i else float("-inf")
             for j in range(n)] for i in range(n)]
```

A) [0.0, 0.0, -inf]
B) [0.0, -inf, -inf]
C) [-inf, 0.0, 0.0]
D) [0.0, 0.0, 0.0]

Learner answer: A
Correct answer: A
Result: Correct
Explanation: Row i=1 permits columns j=0 and j=1, and masks future column j=2.

## p07-l08-a1-q1 — 2026-10-26

How do the reconstruction targets differ between T5-style span corruption and BART-style denoising?

A) T5 predicts the full clean input; BART predicts only deleted tokens.
B) Both predict only the unchanged tokens from the corrupted input.
C) T5 predicts corrupted spans with sentinels; BART predicts the full clean sequence.
D) Both classify the noise type instead of reconstructing original tokens.

Learner answer: C
Correct answer: C
Result: Correct
Explanation: T5 span corruption targets contain removed spans tagged by sentinel tokens. BART denoising targets reconstruct the entire original sequence.

## p07-l08-a1-q2 — 2026-10-26

During encoder–decoder generation for a fixed source document, which computation can be reused across output-token steps?

A) The encoder output representing the unchanged source document.
B) The final next-token logits, which remain constant throughout generation.
C) The complete decoder hidden states for all future output tokens.
D) The sampled output token, which must be repeated at every step.

Learner answer: A
Correct answer: A
Result: Correct
Explanation: The source stays fixed, so its encoder output can be computed once and reused by decoder cross-attention.

## p07-l08-a1-q3 — 2026-10-26

A span-corruption routine produces the following data. What sequence does this reconstruction code return?

```python
source = ["A", "<sent0>", "D", "<sent1>"]
spans = {"<sent0>": ["B", "C"], "<sent1>": ["E"]}
out = []
for token in source:
    out.extend(spans.get(token, [token]))
```

A) ["A", "D", "B", "C", "E"]
B) ["B", "C", "E"]
C) ["A", "<sent0>", "D", "<sent1>"]
D) ["A", "B", "C", "D", "E"]

Learner answer: A
Correct answer: D
Result: Incorrect
Explanation: Each sentinel is replaced in place by its corresponding span; ordinary tokens are retained in source order.

## p07-l09-a1-q1 — 2026-10-26

How does a standard Vision Transformer convert an image into inputs for its transformer encoder?

A) It treats each color channel as a single token and discards spatial position.
B) It flattens image patches, projects them into embeddings, and adds positional signals.
C) It converts pixels into word IDs using a pretrained language tokenizer.
D) It replaces each attention head with a convolution over the original image.

Learner answer: B
Correct answer: B
Result: Correct
Explanation: ViT turns non-overlapping flattened patches into learned embedding vectors and supplies positional information before processing the sequence.

## p07-l09-a1-q2 — 2026-10-26

A 224 × 224 image uses non-overlapping 16 × 16 patches and one prepended [CLS] token. How many tokens enter the encoder?

A) 14
B) 196
C) 197
D) 225

Learner answer: D
Correct answer: C
Result: Incorrect
Explanation: There are (224/16) squared = 196 patches, plus one [CLS] token, giving 197 tokens.

## p07-l09-a1-q3 — 2026-10-26

For a 24 × 24 RGB image, what are len(patches) and len(patches[0]) after patchify(image, 6)?

```python
def patchify(image, P):
    H, W = len(image), len(image[0])
    patches = []
    for i in range(0, H, P):
        for j in range(0, W, P):
            patch = []
            for di in range(P):
                for dj in range(P):
                    patch.extend(image[i + di][j + dj])
            patches.append(patch)
    return patches
```

A) 16 patches, each with 108 values
B) 16 patches, each with 36 values
C) 36 patches, each with 48 values
D) 4 patches, each with 108 values

Learner answer: B
Correct answer: A
Result: Incorrect
Explanation: The grid has (24/6)*(24/6)=16 patches; each contains 6*6*3=108 channel values.

## p07-l10-a1-q1 — 2026-10-26

Which description matches Whisper’s core encoder–decoder pipeline?

A) The encoder reads text tokens; the decoder generates waveform samples.
B) The encoder reads raw waveform samples; a CTC head labels each sample.
C) The encoder reads log-mel features; the decoder generates text tokens autoregressively.
D) The encoder reads speaker identities; the decoder generates image patches.

Learner answer: C
Correct answer: C
Result: Correct
Explanation: Whisper encodes log-mel spectrogram features through a convolutional stem and transformer encoder, then generates text with an autoregressive decoder.

## p07-l10-a1-q2 — 2026-10-26

A transcription application also needs to identify which speaker spoke each segment. What additional capability is needed beyond Whisper’s transcription and timestamps?

A) A speaker-diarization component that assigns speaker labels.
B) A larger text vocabulary that includes more punctuation tokens.
C) A causal mask that blocks all previous audio frames.
D) An output head that converts the transcript into a mel spectrogram.

Learner answer: D
Correct answer: A
Result: Incorrect
Explanation: Whisper does not natively provide speaker diarization; assigning speaker labels requires an additional component.

## p07-l10-a1-q3 — 2026-10-26

What does whisper_prompt("fr", "translate", timestamps=False) return?

```python
def whisper_prompt(lang="en", task="transcribe", timestamps=True):
    tokens = ["<|startoftranscript|>", f"<|{lang}|>", f"<|{task}|>"]
    if not timestamps:
        tokens.append("<|notimestamps|>")
    return tokens
```

A) ["<|startoftranscript|>", "<|en|>", "<|translate|>", "<|notimestamps|>"]
B) ["<|startoftranscript|>", "<|fr|>", "<|transcribe|>", "<|notimestamps|>"]
C) ["<|startoftranscript|>", "<|fr|>", "<|translate|>"]
D) ["<|startoftranscript|>", "<|fr|>", "<|translate|>", "<|notimestamps|>"]

Learner answer: D
Correct answer: D
Result: Correct
Explanation: The supplied language and task become prefix tokens, and timestamps=False appends the no-timestamps token.

## p07-l11-a1-q1 — 2026-10-26

How does a sparsely routed Mixture-of-Experts layer increase model capacity without running every expert for every token?

A) It removes unused experts permanently after processing the first token.
B) It stores only one expert’s weights and recreates all others from the input.
C) It replaces all attention and feed-forward computation with a lookup table.
D) It stores multiple experts but routes each token through a selected subset.

Learner answer: D
Correct answer: D
Result: Correct
Explanation: MoE stores many experts while activating only a subset for each token, separating total expert capacity from per-token expert computation.

## p07-l11-a1-q2 — 2026-10-26

A toy MoE has 8 equal-sized routed experts and selects 2 per token, with no shared experts. Ignoring the router and all other layers, what fraction of expert parameters is active per token?

A) One eighth
B) One quarter
C) One half
D) All of them

Learner answer: B
Correct answer: B
Result: Correct
Explanation: Two of eight equal-sized experts are active, giving 2/8 = 1/4 of the expert parameters.

## p07-l11-a1-q3 — 2026-10-26

Which experts are selected, and what scores are used to compute their gate weights?

```python
scores = [3.0, 2.0, 1.0]
bias = [-3.0, 0.0, 2.0]
biased = [s + b for s, b in zip(scores, bias)]
top_idx = sorted(range(3), key=lambda i: -biased[i])[:2]
chosen = [scores[i] for i in top_idx]
# gates = softmax(chosen)
```

A) top_idx = [2, 1]; chosen = [1.0, 2.0]
B) top_idx = [2, 1]; chosen = [3.0, 2.0]
C) top_idx = [0, 1]; chosen = [3.0, 2.0]
D) top_idx = [1, 2]; chosen = [2.0, 3.0]

Learner answer: A
Correct answer: A
Result: Correct
Explanation: Biased scores [0,2,3] select experts 2 then 1. Gating uses their original scores [1,2], not their biased selection scores.

## p07-l12-a1-q1 — 2026-10-26

How does FlashAttention reduce the memory overhead of standard dense attention?

A) It discards all but the nearest key for each query.
B) It tiles computation and uses online softmax to avoid storing the full attention matrix in GPU main memory.
C) It removes softmax and replaces attention with an unweighted mean.
D) It caches generated text instead of computing query–key dot products.

Learner answer: B
Correct answer: B
Result: Correct
Explanation: FlashAttention uses tiling and online softmax to compute dense attention without materializing the full N-by-N score/probability matrices in GPU main memory. It preserves the attention computation up to numerical differences.

## p07-l12-a1-q2 — 2026-10-26

A KV cache has batch size 1, 2 layers, 4 KV heads, head dimension 8, and 10 cached tokens. At 2 bytes per element, how many bytes store the keys and values, excluding allocation overhead?

A) 640 bytes
B) 1,280 bytes
C) 2,560 bytes
D) 5,120 bytes

Learner answer: B
Correct answer: C
Result: Incorrect
Explanation: K and V require 2 * layers * KV heads * head dimension * tokens * bytes = 2*2*4*8*10*2 = 2560 bytes.

## p07-l12-a1-q3 — 2026-10-26

After this code runs, what is len(cache.K[0][1])?

```python
class KVCache:
    def __init__(self, n_layers, n_heads):
        self.K = [[[] for _ in range(n_heads)] for _ in range(n_layers)]
        self.V = [[[] for _ in range(n_heads)] for _ in range(n_layers)]
    def append(self, layer, head, k, v):
        self.K[layer][head].append(k)
        self.V[layer][head].append(v)

cache = KVCache(1, 2)
cache.append(0, 1, [1, 2], [3, 4])
cache.append(0, 1, [5, 6], [7, 8])
```

A) 2
B) 4
C) 1
D) 8

Learner answer: B
Correct answer: A
Result: Incorrect
Explanation: Each append adds one key vector to that head’s token list. Two appended vectors give a list length of two, regardless of vector width.

## p07-l13-a1-q1 — 2026-10-26

At a fixed pretraining compute budget, what trade-off do compute-optimal scaling laws help choose?

A) The split between attention heads and output vocabulary, regardless of data.
B) The split between training loss and test labels, regardless of model size.
C) The balance between parameter count and number of training tokens.
D) The balance between prompt length and output temperature during sampling.

Learner answer: D
Correct answer: C
Result: Incorrect
Explanation: Training compute is approximately 6ND, so allocating a fixed budget requires balancing model parameters N and training tokens D.

## p07-l13-a1-q2 — 2026-10-26

Why might a model intended to serve a very large volume of inference tokens be trained smaller and for more tokens than a pretraining-compute-only optimum suggests?

A) A smaller model always reaches zero loss if it sees enough tokens.
B) Extra training can improve a smaller model while reducing recurring inference cost.
C) More training tokens eliminate the need to store model weights at inference.
D) A smaller model makes training compute independent of the number of tokens.

Learner answer: B
Correct answer: B
Result: Correct
Explanation: Accounting for repeated serving costs can favor more training of a smaller model, trading additional training expense for lower inference cost.

## p07-l13-a1-q3 — 2026-10-26

With the same compute budget C, how does D change if N is halved in this estimate?

```python
def training_tokens(C, N):
    return C / (6 * N)
```

A) D is halved.
B) D stays unchanged.
C) D becomes four times larger.
D) D doubles.

Learner answer: B
Correct answer: D
Result: Incorrect
Explanation: D=C/(6N), so halving N doubles D at fixed C.

## p07-l14-a1-q1 — 2026-10-26

What does tying the token embedding and language-model output-head weights accomplish in the capstone?

A) It forces every token to have the same embedding vector.
B) It shares parameters between token lookup and vocabulary-logit projection.
C) It removes the need for a vocabulary-sized output distribution.
D) It makes the causal attention mask unnecessary during training.

Learner answer: B
Correct answer: B
Result: Correct
Explanation: Weight tying reuses token embedding parameters for the output vocabulary projection rather than learning an independent output matrix.

## p07-l14-a1-q2 — 2026-10-26

Training loss keeps decreasing while held-out validation loss starts increasing. What does this pattern most directly suggest?

A) The validation data must have become part of the training batches.
B) The causal mask has necessarily been removed from every layer.
C) The model is generalizing better because training loss is lower.
D) The model may be overfitting the training data.

Learner answer: D
Correct answer: D
Result: Correct
Explanation: Improving training loss alongside worsening held-out loss is evidence of overfitting and should guide stopping or regularization decisions.

## p07-l14-a1-q3 — 2026-10-26

Why does this training loop call opt.zero_grad() after opt.step()?

```python
loss.backward()
torch.nn.utils.clip_grad_norm_(model.parameters(), 1.0)
opt.step()
opt.zero_grad()
```

A) To clear accumulated gradients before the next batch’s backward pass.
B) To reset all learned model weights to zero after each update.
C) To undo gradient clipping before applying the optimizer update.
D) To remove the loss computation from the previous forward pass.

Learner answer: A
Correct answer: A
Result: Correct
Explanation: Backward accumulates gradients into parameter gradient buffers. Clearing them prevents unintended accumulation across batches.

## p07-l15-a1-q1 — 2026-10-26

What distinguishes sliding-window attention from FlashAttention applied to full dense attention?

A) Both remove all long-range query–key pairs from the model.
B) Sliding-window attention changes allowed token pairs; FlashAttention changes how dense attention is computed.
C) FlashAttention changes allowed token pairs; sliding-window attention only changes memory layout.
D) Both replace attention weights with a uniform distribution over the prefix.

Learner answer: B
Correct answer: B
Result: Correct
Explanation: Sliding-window attention restricts the attention pattern. FlashAttention tiles and reorganizes dense attention computation without removing allowed pairs.

## p07-l15-a1-q2 — 2026-10-26

A model using only narrow sliding windows struggles to retrieve distant information. Which architectural change directly restores some global attention paths?

A) Remove positional signals from every attention layer.
B) Use the same narrow window in every layer and remove residuals.
C) Interleave sliding-window layers with full-attention layers.
D) Replace every attention output with the current token embedding.

Learner answer: C
Correct answer: C
Result: Correct
Explanation: Interleaving global layers lets positions access distant tokens directly while retaining local attention in other layers.

## p07-l15-a1-q3 — 2026-10-26

For swa_mask(6, 3), which column indices in row i=4 have value 0.0?

```python
def swa_mask(n, window):
    M = [[float("-inf")] * n for _ in range(n)]
    for i in range(n):
        lo = max(0, i - window + 1)
        for j in range(lo, i + 1):
            M[i][j] = 0.0
    return M
```

A) [1, 2, 3, 4]
B) [3, 4, 5]
C) [0, 1, 2, 3, 4]
D) [2, 3, 4]

Learner answer: D
Correct answer: D
Result: Correct
Explanation: At i=4 with window=3, lo=max(0,4-3+1)=2 and range(2,5) permits indices 2,3,4.

## p07-l16-a1-q1 — 2026-10-26

What does exact speculative sampling preserve when its acceptance and residual-sampling steps are implemented correctly?

A) The exact token sequence from every direct-sampling run with the same random seed.
B) The draft model’s output distribution, regardless of the verifier.
C) The verifier’s output distribution, while potentially reducing decoding latency.
D) A fixed number of accepted draft tokens at every verification step.

Learner answer: C
Correct answer: C
Result: Correct
Explanation: Exact speculative sampling preserves the target verifier distribution. It does not require identical samples for a particular random seed, and the number of accepted drafts varies.

## p07-l16-a1-q2 — 2026-10-26

A verifier cache contains a 10-token prefix plus 5 proposed draft tokens. The first 2 drafts are accepted and the third is rejected. Before processing the replacement token, which cache entries should remain committed?

A) The 10-token prefix and the first 2 accepted drafts.
B) The 10-token prefix and all 5 proposed drafts.
C) Only the original 10-token prefix, discarding accepted drafts too.
D) The prefix and first 3 drafts, including the rejected token.

Learner answer: A
Correct answer: A
Result: Correct
Explanation: The cache must match the accepted prefix: 10 original tokens plus 2 accepted drafts. Rejected and later speculative entries must be discarded.

## p07-l16-a1-q3 — 2026-10-26

For q_prob=0.2 and p_prob=0.5, which result does each draw produce?

```python
def accept_or_reject(q_prob, p_prob, u):
    return u < min(1.0, q_prob / p_prob)

a = accept_or_reject(0.2, 0.5, 0.3)
b = accept_or_reject(0.2, 0.5, 0.6)
```

A) a=False; b=True
B) a=True; b=True
C) a=False; b=False
D) a=True; b=False

Learner answer: D
Correct answer: D
Result: Correct
Explanation: The acceptance threshold is 0.2/0.5=0.4. The draw 0.3 is below the threshold, while 0.6 is above it.

Initial phase assessment complete: 30/48 (62.5%). Phase not passed; fresh full retakes required for lessons 01, 04, 05, 06, 09, 12, 13.

## p07-l01-a2-q1 — 2026-10-26

For an RNN with h_t = f(h_(t-1), x_t), why do additional GPU cores alone not eliminate the sequential dependency across tokens?

A) The next hidden state requires the preceding hidden state to be computed.
B) Every token requires its own separately trained copy of the model.
C) The hidden-state vector must grow in width after every token.
D) The recurrence must first construct a dense attention matrix.

Learner answer: A
Correct answer: A
Result: Correct
Explanation: The hidden-state recurrence imposes an ordered dependency chain even if individual operations within each step can run in parallel.

## p07-l01-a2-q2 — 2026-10-26

A dense attention score matrix contains one entry per ordered token pair. If context length triples, how many times as many score entries are required?

A) Three times
B) Six times
C) Nine times
D) Twenty-seven times

Learner answer: C
Correct answer: C
Result: Correct
Explanation: The matrix has N squared entries. Tripling length gives (3N) squared = 9N squared.

## p07-l01-a2-q3 — 2026-10-26

What does this recurrence return?

```python
h = 0.0
for x in [10.0, 0.0, 0.0]:
    h = 0.9 * h + x
print(h)
```

A) 10.0
B) 8.1
C) 9.0
D) 3.3333333333333335

Learner answer: B
Correct answer: B
Result: Correct
Explanation: The successive hidden states are 10.0, 9.0, and 8.1.

Lesson01 attempt2 complete: 3/3 replaces 0/3; effective phase score 33/48.

## p07-l04-a2-q1 — 2026-10-26

Why does an unmasked self-attention layer need positional information to represent sequence order?

A) Its projection matrices otherwise assign identical vectors to all tokens.
B) Its softmax otherwise gives uniform weights to every token.
C) Its output rows follow any input-row permutation without identifying original positions.
D) Its value vectors otherwise contain only absolute position indices.

Learner answer: C
Correct answer: C
Result: Correct
Explanation: Without positional information, unmasked self-attention is permutation equivariant: rearranging inputs rearranges outputs in the same way, without supplying sequence-position identity.

## p07-l04-a2-q2 — 2026-10-26

Two allowed keys have identical content-based scores but are 2 and 6 positions from the query. With ALiBi slope m=0.25, which receives the higher biased score?

A) The nearer key, because its penalty is -0.5 rather than -1.5.
B) The farther key, because its penalty is +1.5 rather than +0.5.
C) They remain tied, because ALiBi affects only the value vectors.
D) They remain tied, because equal content scores cancel the bias.

Learner answer: A
Correct answer: A
Result: Correct
Explanation: ALiBi adds a negative distance penalty. The nearer key loses 0.5 while the farther loses 1.5, so the nearer key has the higher biased score.

## p07-l04-a2-q3 — 2026-10-26

What pair is returned when pos=0?

```python
import math
a, b = 3.0, 4.0
pos = 0
c, s = math.cos(pos), math.sin(pos)
out = (a*c - b*s, a*s + b*c)
```

A) (-4.0, 3.0)
B) (4.0, 3.0)
C) (0.0, 0.0)
D) (3.0, 4.0)

Learner answer: D
Correct answer: D
Result: Correct
Explanation: At zero angle, cosine is 1 and sine is 0, so the rotation leaves the pair unchanged.

Lesson04 attempt2 complete: 3/3 replaces 1/3; effective phase score 35/48.

## p07-l05-a2-q1 — 2026-10-26

Which pair of sublayers forms the core of a standard GPT-style decoder-only transformer block?

A) Unmasked self-attention and encoder cross-attention.
B) Causal self-attention and a position-wise feed-forward network.
C) Encoder cross-attention and a position-wise feed-forward network.
D) Token embedding lookup and a speaker-diarization classifier.

Learner answer: B
Correct answer: B
Result: Correct
Explanation: A standard GPT-style block combines causal self-attention and an FFN with normalization and residual connections, and has no encoder cross-attention.

## p07-l05-a2-q2 — 2026-10-26

A pre-norm attention sublayer has normalized its input and computed attention output y. Which value should the residual connection add to y?

A) The encoder output, regardless of which block is running.
B) The attention weights summed across all token positions.
C) The normalized input with the original input discarded.
D) The original input x from before normalization.

Learner answer: C
Correct answer: D
Result: Incorrect
Explanation: Pre-norm uses x + Attention(Norm(x)); the residual branch carries the original x unchanged.

## p07-l05-a2-q3 — 2026-10-26

Which rewrite changes this post-norm sublayer to pre-norm?

```python
out = norm(x + ffn(x))
```

A) out = x + ffn(norm(x))
B) out = ffn(norm(x + x))
C) out = norm(x) + ffn(x)
D) out = norm(ffn(x))

Learner answer: A
Correct answer: A
Result: Correct
Explanation: Pre-norm applies normalization to the sublayer input, then adds the sublayer output to the original residual input x.

Lesson05 attempt2 complete: 2/3 replaces 1/3; effective phase score 36/48.

## p07-l06-a2-q1 — 2026-10-26

In the input “the [MASK] chased the mouse,” which visible words can a standard bidirectional BERT encoder use to predict the masked token?

A) Only “the” before the mask.
B) Only “chased the mouse” after the mask.
C) No visible words; only the mask token itself.
D) Visible words both before and after the mask.

Learner answer: D
Correct answer: D
Result: Correct
Explanation: Bidirectional attention allows the masked position to use visible context on both sides.

## p07-l06-a2-q2 — 2026-10-26

An MLM-selected token is left unchanged under BERT’s 80/10/10 rule. Should its original token ID still be used as a prediction target?

A) Yes; selection determines the target even when the input is unchanged.
B) No; every unchanged input token must use the ignore-index label.
C) No; its label must be replaced with the [MASK] token ID.
D) Yes; but only after replacing its input with a random token.

Learner answer: D
Correct answer: A
Result: Incorrect
Explanation: Selected positions contribute original-token targets regardless of whether they are masked, randomized, or left unchanged.

## p07-l06-a2-q3 — 2026-10-26

What are input_ids and labels after this code?

```python
tokens = [5, 8]
input_ids = list(tokens)
labels = [-100] * len(tokens)
i = 1
labels[i] = tokens[i]
r = 0.85
if r < 0.8:
    input_ids[i] = 99
elif r < 0.9:
    input_ids[i] = 3  # supplied random replacement
```

A) input_ids=[5, 99]; labels=[-100, 8]
B) input_ids=[5, 3]; labels=[-100, 3]
C) input_ids=[5, 3]; labels=[-100, 8]
D) input_ids=[5, 8]; labels=[-100, -100]

Learner answer: C
Correct answer: C
Result: Correct
Explanation: r=0.85 enters the random-replacement branch, changing input ID8 to3; the target remains the original8 and the unselected position remains ignored.

Lesson06 attempt2 complete: 2/3 replaces 1/3; effective phase score 37/48.

## p07-l09-a2-q1 — 2026-10-26

In a standard ViT classifier with a prepended [CLS] token, what is passed to the final classification head?

A) The raw pixel values of the first image patch.
B) The list of integer patch-position indices.
C) The final hidden state of the [CLS] token.
D) The unnormalized attention scores from the first layer.

Learner answer: C
Correct answer: C
Result: Correct
Explanation: The final [CLS] representation aggregates information through the encoder and is used as input to the image classification head.

## p07-l09-a2-q2 — 2026-10-26

A 32 × 32 RGB image is split into non-overlapping 8 × 8 patches, then one [CLS] token is added. How many tokens enter the encoder?

A) 17
B) 16
C) 65
D) 193

Learner answer: B
Correct answer: A
Result: Incorrect
Explanation: There are (32/8)*(32/8)=16 patches, plus one [CLS] token, giving17 tokens.

## p07-l09-a2-q3 — 2026-10-26

What are n_patches and flat_width?

```python
H, W, C, P = 12, 8, 3, 4
n_patches = (H // P) * (W // P)
flat_width = P * P * C
```

A) n_patches=6; flat_width=16
B) n_patches=24; flat_width=48
C) n_patches=6; flat_width=12
D) n_patches=6; flat_width=48

Learner answer: D
Correct answer: D
Result: Correct
Explanation: The patch grid is3 by2, giving6 patches; each patch has4*4*3=48 channel values.

Lesson09 attempt2 complete: 2/3 replaces 1/3; effective phase score 38/48.

## p07-l12-a2-q1 — 2026-10-26

During causal autoregressive decoding with fixed model weights, what does the KV cache let the model reuse?

A) The final next-token probabilities, unchanged for all subsequent tokens.
B) Previously computed key and value vectors for the prefix at each layer.
C) The new token’s query vector before the new token is known.
D) Future token embeddings before those tokens have been generated.

Learner answer: A
Correct answer: B
Result: Incorrect
Explanation: Prefix keys and values remain valid under causal attention and can be reused instead of recomputing them for each new token.

## p07-l12-a2-q2 — 2026-10-26

At batch size1, a cache stores2 layers,2 KV heads,4 dimensions per head, and5 tokens. Each scalar uses2 bytes. Including both K and V, how much storage is needed, excluding overhead?

A) 80 bytes
B) 160 bytes
C) 640 bytes
D) 320 bytes

Learner answer: C
Correct answer: D
Result: Incorrect
Explanation: Storage is2(K,V)*2(layers)*2(heads)*4(dimensions)*5(tokens)*2(bytes)=320 bytes.

## p07-l12-a2-q3 — 2026-10-26

After these appends, what are len(K) and len(K[0])?

```python
K = []
K.append([1, 2, 3])
K.append([4, 5, 6])
K.append([7, 8, 9])
```

A) len(K)=3; len(K[0])=3
B) len(K)=9; len(K[0])=1
C) len(K)=1; len(K[0])=9
D) len(K)=3; len(K[0])=9

Learner answer: A
Correct answer: A
Result: Correct
Explanation: K contains three vectors, each containing three scalar elements. Appending a vector adds one outer-list entry.

Lesson12 attempt2 complete: 1/3 replaces 1/3; effective phase score remains38/48.

## p07-l13-a2-q1 — 2026-10-26

In the estimate C ≈ 6ND, what do N and D represent?

A) Attention head count and hidden dimension.
B) Prompt token count and generated token count.
C) GPU count and training duration.
D) Model parameter count and training token count.

Learner answer: A
Correct answer: D
Result: Incorrect
Explanation: The approximate dense-transformer training compute estimate multiplies parameter count N by training token count D and a factor of about6.

## p07-l13-a2-q2 — 2026-10-26

You double a dense model’s parameter count while keeping its training compute budget fixed under C ≈ 6ND. What happens to the affordable training-token count?

A) It doubles.
B) It halves.
C) It stays unchanged.
D) It quadruples.

Learner answer: A
Correct answer: B
Result: Incorrect
Explanation: At fixed C, D=C/(6N); doubling N halves D.

## p07-l13-a2-q3 — 2026-10-26

What is ratio?

```python
C = 6000
N = 10
D = C / (6 * N)
ratio = D / N
```

A) 10.0
B) 20.0
C) 100.0
D) 1000.0

Learner answer: C
Correct answer: A
Result: Incorrect
Explanation: D=6000/(6*10)=100; D/N=100/10=10.

Lesson13 attempt2 complete: 0/3 replaces1/3; effective phase score37/48.

## p07-l12-a3-q1 — 2026-10-26

Why can a causal decoder reuse an earlier token’s cached keys and values after a new token is appended, with fixed weights and deterministic inference?

A) Every token in the growing sequence has identical keys and values.
B) Its causal hidden states cannot depend on tokens appended later.
C) Appending a token freezes the next-token probability distribution.
D) The cache replaces every earlier token with the newest token.

Learner answer: A
Correct answer: B
Result: Incorrect
Explanation: Causal attention prevents an earlier position from depending on later positions, so appending a token does not invalidate earlier per-layer keys and values.

## p07-l12-a3-q2 — 2026-10-26

A cache stores100 scalar elements for K and100 for V. Each scalar uses2 bytes. What is their combined storage, excluding overhead?

A) 100 bytes
B) 200 bytes
C) 400 bytes
D) 800 bytes

Learner answer: D
Correct answer: C
Result: Incorrect
Explanation: There are200 total scalar elements across K and V;200*2=400 bytes.

## p07-l12-a3-q3 — 2026-10-26

What is len(K) after this code?

```python
K = [[1, 2], [3, 4]]
K.append([5, 6])
```

A) 2
B) 5
C) 6
D) 3

Learner answer: D
Correct answer: D
Result: Correct
Explanation: The outer list starts with two vectors; append adds one vector, yielding three outer-list entries.

Lesson12 attempt3 complete:1/3 replaces1/3; effective phase score remains37/48.

## p07-l13-a3-q1 — 2026-10-26

Under the approximate dense-training compute relation C=6ND, what happens to C if both parameter count N and training-token count D double?

A) C is unchanged.
B) C doubles.
C) C quadruples.
D) C increases eightfold.

Learner answer: C
Correct answer: C
Result: Correct
Explanation: Multiplying both N and D by2 multiplies their product, and hence C, by4.

## p07-l13-a3-q2 — 2026-10-26

Two training plans have parameter/token counts (N,D) and (N/4,4D). Under C≈6ND, how do their training-compute estimates compare?

A) The second needs one quarter as much compute.
B) The second needs four times as much compute.
C) The second needs sixteen times as much compute.
D) They have the same estimated training compute.

Learner answer: D
Correct answer: D
Result: Correct
Explanation: (N/4)*(4D)=ND, so the compute estimate is unchanged.

## p07-l13-a3-q3 — 2026-10-26

What is tokens_per_parameter?

```python
parameters = 5
training_tokens = 100
tokens_per_parameter = training_tokens / parameters
```

A) 20.0
B) 5.0
C) 100.0
D) 500.0

Learner answer: A
Correct answer: A
Result: Correct
Explanation: Tokens per parameter is100/5=20.

Lesson13 attempt3 complete:3/3 replaces0/3; effective phase score40/48.

## p07-l12-a4-q1 — 2026-10-26

Which statement correctly distinguishes KV caching from caching one fixed next-token distribution?

A) KV caching forces every generation step to reuse identical output probabilities.
B) KV caching stores only the most probable vocabulary token at each position.
C) KV caching reuses prefix representations while each new query computes updated attention and output probabilities.
D) KV caching removes the need to process any newly generated token.

Learner answer: C
Correct answer: C
Result: Correct
Explanation: Cached prefix keys and values are reused, but the newly processed token supplies new queries and produces updated attention outputs and next-token probabilities.

## p07-l12-a4-q2 — 2026-10-26

A cache contains40 K scalars and40 V scalars. Each scalar uses4 bytes. What is the total storage, excluding overhead?

A) 320 bytes
B) 160 bytes
C) 80 bytes
D) 640 bytes

Learner answer: D
Correct answer: A
Result: Incorrect
Explanation: There are40+40=80 total scalars;80*4=320 bytes.

## p07-l12-a4-q3 — 2026-10-26

What are len(K) and len(K[0]) after the append?

```python
K = [[1, 2, 3, 4]]
K.append([5, 6, 7, 8])
```

A) len(K)=8; len(K[0])=1
B) len(K)=4; len(K[0])=2
C) len(K)=2; len(K[0])=8
D) len(K)=2; len(K[0])=4

Learner answer: D
Correct answer: D
Result: Correct
Explanation: The outer list has two vectors, and each vector has four scalar elements.

Lesson12 attempt4 complete:2/3 replaces1/3; effective phase score41/48 (85.42%). Phase passed: every lesson at least2/3. Initial30/48; cumulative49/78;10 full retake sets. Quiz-based mastery; implementation lab not performed in this assessment.
