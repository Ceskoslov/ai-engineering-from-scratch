# Phase 10 — llms-from-scratch Review Summary

[All phases](../progress.md)

- Status: **Done / Passed**; passed on 2026-10-27; coverage: **24 lessons**.
- Initial score: **59/72**; final effective score: **63/72 (87.50%)**.
- Cumulative responses: 78, with 65 correct; **13 initial/retake mistakes** retained. Cumulative responses include retakes and are not the mastery-score denominator.
- Pass criteria: effective phase score ≥85% and final score ≥2/3 in every lesson; all criteria met. Completion basis: quiz-based mastery; implementation labs were not performed in this assessment.

## Weak points and review priorities

- L02: BPE merges independently within pre-tokenized chunks. L08: KTO supports unpaired good/bad feedback, while DPO uses preferred/rejected pairs. L09: verifiable rewards need external test evidence; style preferences do not establish correctness.
- L10: benchmark contamination can inflate scores through memorization. L11: retain per-channel scales for dequantization. L13: missing dict.get values return None. L14: explicit head_dim overrides its fallback.
- L18: MTP shares the main embedding/output head but still adds depth-specific parameters. L22: deduplicate categories within each step rather than counting repeated writes as progress.
- L03 LSH candidate verification and padding masks versus document isolation, and L12 KV reuse and continuous batching all reached 3/3 in retakes. Each decode step still computes the next-token distribution.

## Lessons with mistakes and retake outcomes

Lessons with mistakes or retakes are listed below, along with any additional rows retained from the original ledger. Unlisted lessons scored 3/3 initially and finally. A final 3/3 indicates correction in a later assessment where applicable; retain those topics for spaced recall. Lessons at 2/3 remain review priorities.

| Lesson | Initial score | Final effective score / retake |
|---|---|---|
| [Building a Tokenizer from Scratch](../../../phases/10-llms-from-scratch/02-building-a-tokenizer/docs/en.md) | 2/3 | 2/3 |
| [Data Pipelines for Pre-Training](../../../phases/10-llms-from-scratch/03-data-pipelines/docs/en.md) | 1/3 | 3/3 (attempt2) |
| [DPO: Direct Preference Optimization](../../../phases/10-llms-from-scratch/08-dpo/docs/en.md) | 2/3 | 2/3 |
| [Constitutional AI and Self-Improvement](../../../phases/10-llms-from-scratch/09-constitutional-ai-self-improvement/docs/en.md) | 2/3 | 2/3 |
| [Evaluation: Benchmarks, Evals, LM Harness](../../../phases/10-llms-from-scratch/10-evaluation/docs/en.md) | 2/3 | 2/3 |
| [Quantization: Making Models Fit](../../../phases/10-llms-from-scratch/11-quantization/docs/en.md) | 2/3 | 2/3 |
| [Inference Optimization](../../../phases/10-llms-from-scratch/12-inference-optimization/docs/en.md) | 1/3 | 3/3 (attempt2) |
| [Building a Complete LLM Pipeline](../../../phases/10-llms-from-scratch/13-building-complete-llm-pipeline/docs/en.md) | 2/3 | 2/3 |
| [Open Models: Architecture Walkthroughs](../../../phases/10-llms-from-scratch/14-open-models-architecture-walkthroughs/docs/en.md) | 2/3 | 2/3 |
| [Multi-Token Prediction (MTP)](../../../phases/10-llms-from-scratch/18-multi-token-prediction/docs/en.md) | 2/3 | 2/3 |
| [Async and Hogwild! Inference](../../../phases/10-llms-from-scratch/22-async-hogwild-inference/docs/en.md) | 2/3 | 2/3 |

## Condensed mistake records

Question IDs, prompts, selected wrong answers, correct answers, and explanations are retained. Other distractors, correct-only questions, and per-response score logs are omitted. Prompts and explanations retain their original English wording. These are historical initial/retake mistakes, not pending retake requirements.

### p10-l02-a1-q2

Your trained BPE starts merging across spaces, creating tokens that span separate words. Which pipeline change directly prevents those merges?

- Learner answer: C — Decode each merged token before counting pairs.
- Correct answer: B — Run BPE separately on pre-tokenized chunks.
- Explanation: The lesson's pre-tokenizer splits text into chunks, and BPE trains and encodes each chunk independently, so adjacent pairs cannot cross a chunk boundary.

### p10-l03-a1-q1

What is the role of LSH in the lesson's MinHash deduplication pipeline?

- Learner answer: C — It computes exact Jaccard similarity for every document pair.
- Correct answer: D — It selects candidate pairs for an exact similarity check.
- Explanation: LSH groups similar MinHash signatures into buckets to find candidate pairs. The implementation then verifies candidates using exact Jaccard similarity before removing a document.

### p10-l03-a1-q3

The lesson's pack_sequences([10, 99, 20, 99], seq_length=4) returns mask [[1, 1, 1, 1]]. If 99 marks document endings, what does this mask establish?

- Learner answer: B — Each document can attend only to its own token positions.
- Correct answer: A — All positions contain real tokens; document isolation is not encoded.
- Explanation: pack_sequences emits a one-dimensional real-token versus padding mask for each sequence. It does not construct a pairwise block-diagonal attention mask or loss mask.

### p10-l08-a1-q2

Your feedback dataset labels individual responses as good or bad, with no paired comparisons. Which method described in this lesson is designed for that format?

- Learner answer: A — Standard DPO on chosen/rejected pairs.
- Correct answer: B — KTO using unpaired binary feedback.
- Explanation: KTO accepts unpaired desirable/undesirable response labels, whereas standard DPO requires a preferred and rejected response for each prompt.

### p10-l09-a1-q2

You can cheaply run trusted tests that verify whether generated code solves a task. Which feedback source best fits the lesson's rule-based outcome-reward approach?

- Learner answer: D — Use constitutional style preferences as a correctness guarantee.
- Correct answer: A — Use the test results to score each generated solution.
- Explanation: A verifiable outcome such as trusted test results supplies an external correctness signal. It measures what the tests cover; style and confidence do not establish correctness.

### p10-l10-a1-q1

Why can training-data contamination make a benchmark score misleading?

- Learner answer: B — It prevents the benchmark scorer from comparing predictions.
- Correct answer: D — It lets memorized test material inflate measured performance.
- Explanation: If training includes test questions or answers, performance can reflect exposure to that material rather than generalization to unseen cases.

### p10-l11-a1-q2

A weight matrix has channels with very different magnitudes. One shared scale rounds many small-channel weights to zero. Which change most directly addresses this?

- Learner answer: D — Discard the scale factors after rounding the weights.
- Correct answer: C — Give each channel its own quantization scale.
- Explanation: Per-channel scales adapt the quantization step size to each channel's range, preserving small values that a global outlier-dominated scale can erase.

### p10-l12-a1-q1

What repeated computation does a KV cache avoid during autoregressive decoding?

- Learner answer: C — Computing the next-token probability distribution for the new position.
- Correct answer: A — Recomputing key and value projections for earlier tokens.
- Explanation: The cache retains prior key/value projections. Each new query still attends to cached keys and values, and the model still predicts the next-token distribution.

### p10-l12-a1-q2

Requests have very different output lengths, and queued requests wait while finished slots sit idle in a static batch. Which change directly improves slot reuse?

- Learner answer: B — Disable KV caching for all requests in the batch.
- Correct answer: D — Admit waiting requests at decode iterations as slots become free.
- Explanation: Continuous batching revisits the active batch each iteration so completed requests can be replaced by waiting ones without waiting for the longest output.

### p10-l13-a1-q3

The gate function checks each configured metric with eval_metrics.get(metric). If one required metric is absent and all other metrics pass, what does gate return and set?

- Learner answer: C — Raises KeyError before updating the shippable field.
- Correct answer: A — Returns False with a missing-metric HOLD reason; shippable=False.
- Explanation: The None branch records HOLD: missing metric, sets all_pass=False, and continues checking the rest. At the end it assigns manifest.shippable=all_pass and returns it with the reasons.

### p10-l14-a1-q3

The calculator uses config.get("head_dim", hidden_size // num_attention_heads). With hidden_size=3584, num_attention_heads=16, and head_dim=256 explicitly set, which head dimension does it return?

- Learner answer: A — 224
- Correct answer: B — 256
- Explanation: The explicit head_dim field takes precedence over the fallback division, so the function returns 256 rather than 3584/16=224.

### p10-l18-a1-q2

You want to limit the parameter overhead of adding several MTP modules. Which sharing strategy described in the lesson directly helps?

- Learner answer: A — Duplicate the full embedding and output matrices at every depth.
- Correct answer: B — Reuse the main model's embedding and output head across depths.
- Explanation: Sharing the embedding and output head avoids adding another vocabulary-sized pair of matrices per depth. Depth-specific projection and transformer parameters are still added.

### p10-l22-a1-q3

The toy resets seen_work_categories each step and increments progress only for the first A or B occurrence in that step. If two workers both emit A during one step, how much does progress increase?

- Learner answer: B — 2
- Correct answer: D — 1
- Explanation: The first A is counted and added to the set; the second A in the same step is tagged redundant. The set resets for the next step.
