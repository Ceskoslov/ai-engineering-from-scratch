# Phase 12 — multimodal-ai Review Summary

[All phases](../progress.md)

- Status: **Done / Passed**; passed on 2026-10-28; coverage: **25 lessons**.
- Initial score: **62/75**; final effective score: **65/75 (86.67%)**.
- Cumulative responses: 81, with 67 correct; **14 initial/retake mistakes** retained. Cumulative responses include retakes and are not the mastery-score denominator.
- Pass criteria: effective phase score ≥85% and final score ≥2/3 in every lesson; all criteria met. Completion basis: quiz-based mastery; implementation labs were not performed in this assessment.

## Weak points and review priorities

- Prioritize L16 disjoint modality ID ranges and exclusive end offsets: end=start+size, with last ID=end−1. This item was still missed in the retake.
- L02: choose the maximum cosine score for classification. L03: attention weights have query-count × patch-count shape; projection changes width, not token count. L04: scope attention to the most recent preceding image.
- L05: prompt metadata does not implement image-embedding insertion. L07: filtering only llm_b does not establish total budget compliance. L10: independent integer truncation can leave steps unallocated.
- L12: autoregressive image generation predicts discrete visual codes before decoding pixels. L17: temporal grounding localizes a time interval. L24: a fused retrieval score is not a calibrated confidence probability. L01 shared patch projection and CLS/register token counting reached 3/3 in the retake.

## Lessons with mistakes and retake outcomes

Lessons with mistakes or retakes are listed below, along with any additional rows retained from the original ledger. Unlisted lessons scored 3/3 initially and finally. A final 3/3 indicates correction in a later assessment where applicable; retain those topics for spaced recall. Lessons at 2/3 remain review priorities.

| Lesson | Initial score | Final effective score / retake |
|---|---|---|
| [Vision Transformers and the Patch-Token Primitive](../../../phases/12-multimodal-ai/01-vision-transformer-patch-tokens/docs/en.md) | 1/3 | 3/3 (attempt2) |
| [CLIP and Contrastive Vision-Language Pretraining](../../../phases/12-multimodal-ai/02-clip-contrastive-pretraining/docs/en.md) | 2/3 | 2/3 |
| [From CLIP to BLIP-2 — Q-Former as Modality Bridge](../../../phases/12-multimodal-ai/03-blip2-qformer-bridge/docs/en.md) | 2/3 | 2/3 |
| [Flamingo and Gated Cross-Attention for Few-Shot VLMs](../../../phases/12-multimodal-ai/04-flamingo-gated-cross-attention/docs/en.md) | 2/3 | 2/3 |
| [LLaVA and Visual Instruction Tuning](../../../phases/12-multimodal-ai/05-llava-visual-instruction-tuning/docs/en.md) | 2/3 | 2/3 |
| [Open-Weight VLM Recipes: What Actually Matters](../../../phases/12-multimodal-ai/07-open-weight-vlm-recipes/docs/en.md) | 2/3 | 2/3 |
| [InternVL3: Native Multimodal Pretraining](../../../phases/12-multimodal-ai/10-internvl3-native-multimodal/docs/en.md) | 2/3 | 2/3 |
| [Emu3: Next-Token Prediction for Image and Video Generation](../../../phases/12-multimodal-ai/12-emu3-next-token-for-generation/docs/en.md) | 2/3 | 2/3 |
| [MIO and Any-to-Any Streaming Multimodal Models](../../../phases/12-multimodal-ai/16-mio-any-to-any-streaming/docs/en.md) | 1/3 | 2/3 (attempt2) |
| [Video-Language Models: Temporal Tokens and Grounding](../../../phases/12-multimodal-ai/17-video-language-temporal-grounding/docs/en.md) | 2/3 | 2/3 |
| [Multimodal RAG and Cross-Modal Retrieval](../../../phases/12-multimodal-ai/24-multimodal-rag-cross-modal/docs/en.md) | 2/3 | 2/3 |

## Condensed mistake records

Question IDs, prompts, selected wrong answers, correct answers, and explanations are retained. Other distractors, correct-only questions, and per-response score logs are omitted. Prompts and explanations retain their original English wording. These are historical initial/retake mistakes, not pending retake requirements.

### p12-l01-a1-q1

What does the shared patch projection do in a Vision Transformer?

- Learner answer: B — It assigns each patch a unique matrix based on its position.
- Correct answer: C — It maps each flattened patch to a fixed-width token vector.
- Explanation: The same learned linear projection maps each flattened patch into the hidden dimension D; positional information is supplied separately.

### p12-l01-a1-q2

A 224×224 image uses 16×16 patches. With one CLS token and four register tokens, how many tokens enter the vision transformer?

- Learner answer: B — 197
- Correct answer: D — 201
- Explanation: The 14×14 grid gives 196 patch tokens; adding one CLS and four registers gives 201.

### p12-l02-a1-q3

What class ranks first for zero_shot_classify([2, 0], {"cat": [1, 1], "dog": [1, 0]}) in the lesson code?

- Learner answer: D — dog, because the function chooses the smallest cosine similarity.
- Correct answer: A — dog, because its normalized vector has cosine similarity 1.
- Explanation: The function normalizes image and class vectors, computes dot products, and sorts descending. Dog scores 1; cat scores 1/sqrt(2).

### p12-l03-a1-q3

The toy uses 8 queries, 64 patches, QUERY_DIM=16, and LLM_DIM=24. What are the attention-weight and projected-output shapes?

- Learner answer: B — Attention: 8×16; projected output: 64×24.
- Correct answer: D — Attention: 8×64; projected output: 8×24.
- Explanation: Each query has weights over all 64 patches. Cross-attention preserves the 8-query count; projection changes each output width to 24.

### p12-l04-a1-q3

What does interleaved_mask(["intro", "IMG0", "a", "IMG1", "b"]) return, with columns ordered IMG0, IMG1?

- Learner answer: D — [[False, False], [False, True], [False, True]]
- Correct answer: A — [[False, False], [True, False], [False, True]]
- Explanation: Intro has no preceding image; a sees IMG0; b sees only its most recent preceding image, IMG1.

### p12-l05-a1-q3

In the toy code, what does build_llava_prompt(system, user, image_tokens=576) actually do with the image placeholder?

- Learner answer: A — It replaces the placeholder with 576 numeric embedding vectors.
- Correct answer: B — It keeps the placeholder in raw_prompt and records the count as metadata.
- Explanation: The helper builds a string containing <image> and returns the supplied image_tokens count separately. It does not implement embedding insertion or model execution.

### p12-l07-a1-q3

The picker filters candidates with r.llm_b <= budget_b. A recipe has llm_b=7, but its vision encoder and connector bring the total above 8B. With budget_b=8, what happens?

- Learner answer: A — It is rejected because the filter sums all component parameter counts.
- Correct answer: B — It remains eligible because the filter checks only the LLM parameter count.
- Explanation: The filter reads only llm_b. It does not calculate total model size, memory requirements, or latency.

### p12-l10-a1-q3

CorpusMix.steps computes int(total * fraction) independently for each modality. With normalized fractions 0.4, 0.35, 0.2, 0.05 and total=3, what counts result?

- Learner answer: B — text=1, interleaved=1, caption=1, video=0; sum=3.
- Correct answer: A — text=1, interleaved=1, caption=0, video=0; sum=2.
- Explanation: Independent integer truncation gives int(1.2)=1, int(1.05)=1, int(0.6)=0, int(0.15)=0. No remainder allocation is implemented.

### p12-l12-a1-q1

How can next-token prediction support image generation in an Emu3-style model?

- Learner answer: A — It predicts continuous pixels directly from a text-only output vocabulary.
- Correct answer: C — It predicts discrete visual codes that an image decoder can render.
- Explanation: A visual tokenizer represents image content as discrete codes; autoregressive next-token prediction can model their sequence, and a visual decoder converts generated codes to pixels.

### p12-l16-a1-q1

Why assign disjoint token-ID ranges to text, image, speech, and music codebooks in a shared vocabulary?

- Learner answer: A — To let the same integer identify unrelated codes without modality information.
- Correct answer: C — To prevent collisions between modality codes in the shared ID space.
- Explanation: Disjoint ranges give distinct IDs to codes from different modalities so the shared embedding and output layers can distinguish them.

### p12-l16-a1-q3

VocabSlot.end returns start + size, and build_vocab sets the next start to that end. For start=32000 and size=4096, what is the allocated ID range?

- Learner answer: A — 32000 through 36096 inclusive; next start=36097.
- Correct answer: D — 32000 through 36095 inclusive; next start=36096.
- Explanation: The end is exclusive: [32000,36096) contains 4096 IDs, so the last valid ID is 36095 and the next slot starts at 36096.

### p12-l17-a1-q1

What distinguishes temporal grounding from simply recognizing that an event occurs in a video?

- Learner answer: A — It identifies the event without needing any time information.
- Correct answer: B — It localizes when the event occurs using timestamps or an interval.
- Explanation: Temporal grounding associates an event with its time location, such as start and end timestamps, rather than only detecting its presence.

### p12-l24-a1-q3

The toy sets confidence=top[0][1], where the value is a weighted retrieval score, then compares it with confidence_floor. What does this confidence actually represent?

- Learner answer: A — A calibrated probability that every answer claim is correct.
- Correct answer: B — The top fused retrieval score used as a heuristic threshold.
- Explanation: The code reuses the fused ranking score as confidence. It does not calibrate a probability or verify answer claims.

### p12-l16-a2-q2

An image codebook has100 entries and starts at global ID200. Using a contiguous range with an exclusive end, where should the next modality range begin?

- Learner answer: C — 301
- Correct answer: B — 300
- Explanation: The image codes occupy IDs200 through299. The exclusive end and next available ID are200+100=300.
