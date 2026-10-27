# Phase 10 review queue

Historical notes are preserved verbatim; some early remediation requests were superseded by later passes. Latest completion status is in [phase progress](progress.md).

No review items recorded.

- Lesson 02, p10-l02-a1-q2: chose decoding merged tokens before pair counting; review how independently processing pre-tokenized chunks prevents cross-boundary merges. Correct answer: B; learner answer: C.

- Lesson 03, p10-l03-a1-q1: chose exact Jaccard comparison of every document pair as LSH's role. Review LSH candidate selection followed by exact Jaccard verification. Correct answer: D; learner answer: C.

- Lesson 03, p10-l03-a1-q3: chose document isolation for a one-dimensional padding mask. Review padding masks versus pairwise attention masks; pack_sequences does not enforce document boundaries. Correct answer: A; learner answer: B. Lesson latest score 1/3; fresh three-question remediation required.

- Lesson 08, p10-l08-a1-q2: chose standard DPO for unpaired good/bad response labels. Review KTO for unpaired binary feedback versus DPO for prompt-level preferred/rejected pairs. Correct answer: B; learner answer: A.

- Lesson 09, p10-l09-a1-q2: chose constitutional style preferences as a correctness guarantee for generated code. Review externally verifiable outcome rewards such as trusted test results; style and confidence do not verify task correctness. Correct answer: A; learner answer: D.

- Lesson 10, p10-l10-a1-q1: chose scorer comparison failure as the effect of contamination. Review how exposure to benchmark questions or answers can inflate performance through memorization rather than unseen-case generalization. Correct answer: D; learner answer: B.

- Lesson 11, p10-l11-a1-q2: chose discarding scale factors to fix loss of small-channel values. Review per-channel scaling for different channel ranges and retaining scales for dequantization. Correct answer: C; learner answer: D.

- Lesson 12, p10-l12-a1-q1: chose avoiding the next-token probability distribution as the purpose of KV caching. Review reuse of earlier key/value projections; each decode step still computes attention for the new query and the next-token distribution. Correct answer: A; learner answer: C.

- Lesson 12, p10-l12-a1-q2: chose disabling KV caching to fix idle static-batch slots. Review continuous batching: admit waiting requests each decode iteration as completed requests release slots. Correct answer: D; learner answer: B.

- Lesson 12 latest score 1/3; fresh three-question remediation required for KV-cache purpose and continuous batching.

- Lesson 13, p10-l13-a1-q3: predicted KeyError for a missing required metric accessed with dict.get. Review .get returning None and gate recording HOLD, setting all_pass=False, and assigning shippable=False. Correct answer: A; learner answer: C.

- Lesson 14, p10-l14-a1-q3: used hidden_size // num_attention_heads despite explicit head_dim. Review config.get returning an existing field rather than its fallback; explicit head_dim=256 overrides computed 224. Correct answer: B; learner answer: A.

- Lesson 18, p10-l18-a1-q2: chose duplicating embedding/output matrices to reduce MTP overhead. Review sharing the main embedding and output head across depths; depth-specific module parameters remain additional. Correct answer: B; learner answer: A.

- Lesson 22, p10-l22-a1-q3: counted two same-category writes as two units of progress. Review per-step set deduplication: only the first A or B of each category counts within a step. Correct answer: D; learner answer: B.

- Lesson03 remediation attempt2 completed 3/3 on 2026-10-27: candidate verification, document-level causal isolation, and padding-mask tracing answered correctly. Earlier misses retained as review evidence.

## Phase pass — 2026-10-27

Lesson12 remediation attempt2: 3/3 (remaining decode computation, continuous slot reuse, logical versus allocated cache memory). Lesson03 and12 latest scores are both 3/3. Phase effective 63/72 (87.50%), initial 59/72, cumulative 65/78. Earlier review notes are historical evidence and remain for spaced review; all lesson minima are now met. Residual review includes pre-tokenization boundaries; KTO versus paired DPO; verifiable rewards; benchmark contamination; per-channel scales; dict.get and explicit config overrides; shared MTP parameters; and per-step set deduplication. Implementation labs were not performed in this assessment.
