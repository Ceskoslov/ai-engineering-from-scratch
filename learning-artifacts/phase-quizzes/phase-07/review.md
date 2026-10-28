# Phase 07 — transformers-deep-dive Review Summary

[All phases](../progress.md)

- Status: **Done / Passed**; passed on 2026-10-26; coverage: **16 lessons**.
- Initial score: **30/48**; final effective score: **41/48 (85.42%)**.
- Cumulative responses: 78, with 49 correct; **29 initial/retake mistakes** retained. Cumulative responses include retakes and are not the mastery-score denominator.
- Pass criteria: effective phase score ≥85% and final score ≥2/3 in every lesson; all criteria met. Completion basis: quiz-based mastery; implementation labs were not performed in this assessment.

## Weak points and review priorities

- Highest priority: L12 KV-cache byte accounting. Include both K and V, then multiply layers, batch size, cache length, KV heads, head_dim, and bytes per element. List length is not the total scalar count. The final score remained 2/3 after four attempts.
- L05: pre-norm residuals retain the original x before normalization. L06: selected-but-unchanged MLM tokens still predict their original labels. L09: add CLS to the patch count and include channels in flattened patch width.
- L07: teacher forcing permits parallel training, while autoregressive generation proceeds sequentially. L08: reinsert sentinel spans at their original positions in order. L10: transcription/timestamps do not imply speaker diarization.
- L01 sequential dependencies and quadratic attention storage, L04 positional equivariance/ALiBi, and L13 the parameter/token inverse relation under fixed compute C≈6ND and the D/N ratio all reached 3/3 in final retakes. Retain them for spaced recall.

## Lessons with mistakes and retake outcomes

Lessons with mistakes or retakes are listed below, along with any additional rows retained from the original ledger. Unlisted lessons scored 3/3 initially and finally. A final 3/3 indicates correction in a later assessment where applicable; retain those topics for spaced recall. Lessons at 2/3 remain review priorities.

| Lesson | Initial score | Final effective score / retake |
|---|---|---|
| [Why Transformers — The Problems with RNNs](../../../phases/07-transformers-deep-dive/01-why-transformers/docs/en.md) | 0/3 | 3/3 |
| [Positional Encoding — Sinusoidal, RoPE, ALiBi](../../../phases/07-transformers-deep-dive/04-positional-encoding/docs/en.md) | 1/3 | 3/3 |
| [The Full Transformer — Encoder + Decoder](../../../phases/07-transformers-deep-dive/05-full-transformer/docs/en.md) | 1/3 | 2/3 |
| [BERT — Masked Language Modeling](../../../phases/07-transformers-deep-dive/06-bert-masked-language-modeling/docs/en.md) | 1/3 | 2/3 |
| [GPT — Causal Language Modeling](../../../phases/07-transformers-deep-dive/07-gpt-causal-language-modeling/docs/en.md) | 2/3 | 2/3 |
| [T5, BART — Encoder-Decoder Models](../../../phases/07-transformers-deep-dive/08-t5-bart-encoder-decoder/docs/en.md) | 2/3 | 2/3 |
| [Vision Transformers (ViT)](../../../phases/07-transformers-deep-dive/09-vision-transformers/docs/en.md) | 1/3 | 2/3 |
| [Audio Transformers — Whisper Architecture](../../../phases/07-transformers-deep-dive/10-audio-transformers-whisper/docs/en.md) | 2/3 | 2/3 |
| [KV Cache, Flash Attention & Inference Optimization](../../../phases/07-transformers-deep-dive/12-kv-cache-flash-attention/docs/en.md) | 1/3 | 2/3 |
| [Scaling Laws](../../../phases/07-transformers-deep-dive/13-scaling-laws/docs/en.md) | 1/3 | 3/3 |

## Condensed mistake records

Question IDs, prompts, selected wrong answers, correct answers, and explanations are retained. Other distractors, correct-only questions, and per-response score logs are omitted. Prompts and explanations retain their original English wording. These are historical initial/retake mistakes, not pending retake requirements.

### p07-l01-a1-q1

Why can a standard RNN not compute all hidden states across a sequence simultaneously during training?

- Learner answer: D — Each input token must attend to all future input tokens.
- Correct answer: B — Each hidden state depends on the preceding hidden state.
- Explanation: The recurrence h_t = f(h_(t-1), x_t) creates a dependency chain along the sequence.

### p07-l01-a1-q2

An implementation explicitly stores a dense attention score matrix for a sequence of N tokens. If the sequence length doubles while other dimensions stay fixed, how does the number of score entries change?

- Learner answer: D — It grows by a factor of eight.
- Correct answer: C — It grows by a factor of four.
- Explanation: A dense score matrix has N squared entries; (2N) squared is four times N squared.

### p07-l01-a1-q3

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

- Learner answer: B — rnn_style: 6.0; attention_style: 3.0
- Correct answer: A — rnn_style: 5.8; attention_style: 3.0
- Explanation: The recurrence gives h=2.0 then h=0.9*2+4=5.8; the mean is (2+4)/2=3.0. These toy functions compute different quantities.

### p07-l04-a1-q1

Without positional signals or masks, what happens when the input token rows of a self-attention layer are permuted?

- Learner answer: B — The layer reconstructs the original order from query–key similarities.
- Correct answer: C — The output rows follow the same permutation as the input rows.
- Explanation: Unmasked self-attention without positional information is permutation equivariant: permuting inputs permutes outputs in the same way. It does not encode sequence order by itself.

### p07-l04-a1-q3

What does this ALiBi-style bias row contain?

```python
m = 0.5
i = 2
row = [-m * abs(i - j) for j in range(4)]
```

- Learner answer: C — [-1.0, -0.5, 0.0, 0.5]
- Correct answer: D — [-1.0, -0.5, 0.0, -0.5]
- Explanation: Distances from i=2 are [2,1,0,1]; multiplying each by -0.5 gives [-1,-0.5,0,-0.5].

### p07-l05-a1-q2

You adapt an encoder–decoder block into a standard GPT-style decoder-only block. Which change preserves the intended architecture?

- Learner answer: C — Remove the feed-forward sublayer; retain cross-attention and unmasked self-attention.
- Correct answer: A — Remove cross-attention; retain causal self-attention and the feed-forward sublayer.
- Explanation: A standard decoder-only block omits encoder cross-attention while retaining causal self-attention, an FFN, normalization, and residual connections.

### p07-l05-a1-q3

Which expression implements a pre-norm residual sublayer?

- Learner answer: A — LN(x + sublayer(x))
- Correct answer: D — x + sublayer(LN(x))
- Explanation: Pre-norm normalizes the input to the sublayer and adds its output back to the unchanged residual input x.

### p07-l06-a1-q1

What distinguishes BERT’s masked language modeling objective from standard causal next-token prediction?

- Learner answer: D — It predicts selected original tokens using only the following tokens.
- Correct answer: A — It predicts selected original tokens using context from both sides.
- Explanation: BERT predicts original tokens at selected positions with bidirectional context, whereas causal next-token prediction conditions on preceding tokens.

### p07-l06-a1-q3

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

- Learner answer: D — input_ids[i] = a random token; labels[i] = 7
- Correct answer: C — input_ids[i] = 7; labels[i] = 7
- Explanation: The selected token retains its original label. Neither replacement branch runs at r=0.95, so the input remains 7 and still contributes to the prediction loss.

### p07-l07-a1-q1

Why can causal language-model training compute predictions at all sequence positions in parallel, while ordinary autoregressive generation proceeds token by token?

- Learner answer: C — Training predicts all tokens independently, while generation uses no attention.
- Correct answer: B — Training knows the true prefix tokens; generation must produce new prefix tokens.
- Explanation: Teacher-forced training provides all ground-truth input tokens, and a causal mask prevents future leakage. During ordinary generation, each new token is needed to form the prefix for the next prediction.

### p07-l08-a1-q3

A span-corruption routine produces the following data. What sequence does this reconstruction code return?

```python
source = ["A", "<sent0>", "D", "<sent1>"]
spans = {"<sent0>": ["B", "C"], "<sent1>": ["E"]}
out = []
for token in source:
    out.extend(spans.get(token, [token]))
```

- Learner answer: A — ["A", "D", "B", "C", "E"]
- Correct answer: D — ["A", "B", "C", "D", "E"]
- Explanation: Each sentinel is replaced in place by its corresponding span; ordinary tokens are retained in source order.

### p07-l09-a1-q2

A 224 × 224 image uses non-overlapping 16 × 16 patches and one prepended [CLS] token. How many tokens enter the encoder?

- Learner answer: D — 225
- Correct answer: C — 197
- Explanation: There are (224/16) squared = 196 patches, plus one [CLS] token, giving 197 tokens.

### p07-l09-a1-q3

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

- Learner answer: B — 16 patches, each with 36 values
- Correct answer: A — 16 patches, each with 108 values
- Explanation: The grid has (24/6)*(24/6)=16 patches; each contains 6*6*3=108 channel values.

### p07-l10-a1-q2

A transcription application also needs to identify which speaker spoke each segment. What additional capability is needed beyond Whisper’s transcription and timestamps?

- Learner answer: D — An output head that converts the transcript into a mel spectrogram.
- Correct answer: A — A speaker-diarization component that assigns speaker labels.
- Explanation: Whisper does not natively provide speaker diarization; assigning speaker labels requires an additional component.

### p07-l12-a1-q2

A KV cache has batch size 1, 2 layers, 4 KV heads, head dimension 8, and 10 cached tokens. At 2 bytes per element, how many bytes store the keys and values, excluding allocation overhead?

- Learner answer: B — 1,280 bytes
- Correct answer: C — 2,560 bytes
- Explanation: K and V require 2 * layers * KV heads * head dimension * tokens * bytes = 2*2*4*8*10*2 = 2560 bytes.

### p07-l12-a1-q3

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

- Learner answer: B — 4
- Correct answer: A — 2
- Explanation: Each append adds one key vector to that head’s token list. Two appended vectors give a list length of two, regardless of vector width.

### p07-l13-a1-q1

At a fixed pretraining compute budget, what trade-off do compute-optimal scaling laws help choose?

- Learner answer: D — The balance between prompt length and output temperature during sampling.
- Correct answer: C — The balance between parameter count and number of training tokens.
- Explanation: Training compute is approximately 6ND, so allocating a fixed budget requires balancing model parameters N and training tokens D.

### p07-l13-a1-q3

With the same compute budget C, how does D change if N is halved in this estimate?

```python
def training_tokens(C, N):
    return C / (6 * N)
```

- Learner answer: B — D stays unchanged.
- Correct answer: D — D doubles.
- Explanation: D=C/(6N), so halving N doubles D at fixed C.

### p07-l05-a2-q2

A pre-norm attention sublayer has normalized its input and computed attention output y. Which value should the residual connection add to y?

- Learner answer: C — The normalized input with the original input discarded.
- Correct answer: D — The original input x from before normalization.
- Explanation: Pre-norm uses x + Attention(Norm(x)); the residual branch carries the original x unchanged.

### p07-l06-a2-q2

An MLM-selected token is left unchanged under BERT’s 80/10/10 rule. Should its original token ID still be used as a prediction target?

- Learner answer: D — Yes; but only after replacing its input with a random token.
- Correct answer: A — Yes; selection determines the target even when the input is unchanged.
- Explanation: Selected positions contribute original-token targets regardless of whether they are masked, randomized, or left unchanged.

### p07-l09-a2-q2

A 32 × 32 RGB image is split into non-overlapping 8 × 8 patches, then one [CLS] token is added. How many tokens enter the encoder?

- Learner answer: B — 16
- Correct answer: A — 17
- Explanation: There are (32/8)*(32/8)=16 patches, plus one [CLS] token, giving17 tokens.

### p07-l12-a2-q1

During causal autoregressive decoding with fixed model weights, what does the KV cache let the model reuse?

- Learner answer: A — The final next-token probabilities, unchanged for all subsequent tokens.
- Correct answer: B — Previously computed key and value vectors for the prefix at each layer.
- Explanation: Prefix keys and values remain valid under causal attention and can be reused instead of recomputing them for each new token.

### p07-l12-a2-q2

At batch size1, a cache stores2 layers,2 KV heads,4 dimensions per head, and5 tokens. Each scalar uses2 bytes. Including both K and V, how much storage is needed, excluding overhead?

- Learner answer: C — 640 bytes
- Correct answer: D — 320 bytes
- Explanation: Storage is2(K,V)*2(layers)*2(heads)*4(dimensions)*5(tokens)*2(bytes)=320 bytes.

### p07-l13-a2-q1

In the estimate C ≈ 6ND, what do N and D represent?

- Learner answer: A — Attention head count and hidden dimension.
- Correct answer: D — Model parameter count and training token count.
- Explanation: The approximate dense-transformer training compute estimate multiplies parameter count N by training token count D and a factor of about6.

### p07-l13-a2-q2

You double a dense model’s parameter count while keeping its training compute budget fixed under C ≈ 6ND. What happens to the affordable training-token count?

- Learner answer: A — It doubles.
- Correct answer: B — It halves.
- Explanation: At fixed C, D=C/(6N); doubling N halves D.

### p07-l13-a2-q3

What is ratio?

```python
C = 6000
N = 10
D = C / (6 * N)
ratio = D / N
```

- Learner answer: C — 100.0
- Correct answer: A — 10.0
- Explanation: D=6000/(6*10)=100; D/N=100/10=10.

### p07-l12-a3-q1

Why can a causal decoder reuse an earlier token’s cached keys and values after a new token is appended, with fixed weights and deterministic inference?

- Learner answer: A — Every token in the growing sequence has identical keys and values.
- Correct answer: B — Its causal hidden states cannot depend on tokens appended later.
- Explanation: Causal attention prevents an earlier position from depending on later positions, so appending a token does not invalidate earlier per-layer keys and values.

### p07-l12-a3-q2

A cache stores100 scalar elements for K and100 for V. Each scalar uses2 bytes. What is their combined storage, excluding overhead?

- Learner answer: D — 800 bytes
- Correct answer: C — 400 bytes
- Explanation: There are200 total scalar elements across K and V;200*2=400 bytes.

### p07-l12-a4-q2

A cache contains40 K scalars and40 V scalars. Each scalar uses4 bytes. What is the total storage, excluding overhead?

- Learner answer: D — 640 bytes
- Correct answer: A — 320 bytes
- Explanation: There are40+40=80 total scalars;80*4=320 bytes.
