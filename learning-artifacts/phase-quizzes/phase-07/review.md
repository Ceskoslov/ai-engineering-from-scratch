# Phase 07 review queue

Historical notes are preserved verbatim; some early remediation requests were superseded by later passes. Latest completion status is in [phase progress](progress.md).

- Lesson 01, initial attempt 0/3: review sequential hidden-state dependencies, quadratic dense attention storage, and tracing the decayed recurrence versus a mean. Requires a fresh scored three-question retake.

- Lesson 04, initial attempt 1/3: review permutation equivariance without positional signals and the negative distance penalty in ALiBi. RoPE common-offset invariance answered correctly. Requires a fresh scored three-question retake.

- Lesson 05, initial attempt 1/3: review GPT-style decoder-only blocks (causal self-attention plus FFN, no encoder cross-attention) and pre-norm versus post-norm placement. Cross-attention Q/K/V sources answered correctly. Requires a fresh scored three-question retake.

- Lesson 06, initial attempt 1/3: review bidirectional MLM context and selected-but-unchanged tokens retaining their original prediction labels. Correctly computed 15% × 80% mask rate. Requires a fresh scored three-question retake.

- Lesson 07, initial attempt 2/3: review teacher-forced parallel training versus sequential autoregressive generation. Shifted targets and causal-mask tracing answered correctly. Lesson minimum met.

- Lesson 08, initial attempt 2/3: review sentinel replacement in source order; removed spans must be reinserted in place, not appended after unchanged tokens. T5/BART targets and encoder-output reuse answered correctly. Lesson minimum met.

- Lesson 09, initial attempt 1/3: review patch-grid token counts including [CLS] and flattened patch width including RGB channels. Patch embedding concept answered correctly. Requires a fresh scored three-question retake.

- Lesson 10, initial attempt 2/3: review speaker diarization as a separate capability from transcription/timestamps. Core pipeline and prompt-token tracing answered correctly. Lesson minimum met.

- Lesson 12, initial attempt 1/3: review KV storage accounting for both keys and values, and list length counting cached vectors rather than scalar elements. FlashAttention tiling concept answered correctly. Requires a fresh scored three-question retake.

- Lesson 13, initial attempt 1/3: review the parameter/token trade-off at fixed compute and D=C/(6N), including doubling D when N halves. Inference-cost motivation for smaller, longer-trained models answered correctly. Requires a fresh scored three-question retake.

- Lesson 01 retake attempt2: 3/3; sequential dependencies, quadratic score counts, and recurrence tracing all correct. Earlier 0/3 retained; lesson minimum now met.

- Lesson 04 retake attempt2: 3/3; permutation equivariance, ALiBi distance penalties, and zero-angle rotation all correct. Earlier 1/3 retained; lesson minimum now met.

- Lesson 05 retake attempt2: 2/3; decoder-only sublayers and pre-norm rewrite correct. Residual must carry original x before normalization; retain as review topic. Earlier1/3 preserved; lesson minimum now met.

- Lesson 06 retake attempt2: 2/3; bidirectional context and random-replacement tracing correct. Review selected-but-unchanged input still retaining original target. Earlier1/3 preserved; lesson minimum now met.

- Lesson 09 retake attempt2: 2/3; [CLS] representation and RGB patch dimensions correct. Review adding [CLS] to patch count. Earlier1/3 preserved; lesson minimum now met.

- Lesson12 retake attempt2: 1/3; nested-list lengths correct. Revisit cached K/V versus changing output probabilities, and multiplication of all cache dimensions. Latest score1/3; another fresh full retake required.

- Lesson13 retake attempt2: 0/3. Review N=parameters, D=training tokens, fixed-compute inverse relation, and D/N versus D. Latest0/3 replaces1/3; another fresh full retake required.

- Lesson12 retake attempt3:1/3. List append tracing correct; causal cache validity and total scalar-bytes accounting missed. Latest1/3; another full retake required.

- Lesson13 retake attempt3:3/3; compute products, fixed-compute trade-off, and tokens-per-parameter calculation correct. Earlier attempts preserved; lesson minimum now met.

- Lesson12 attempt4:2/3, minimum met. Cache reuse and nested-list tracing correct; total byte accounting still missed.

## Phase pass — 2026-10-26

Initial30/48; latest complete sets41/48 (85.42%); cumulative49/78 across initial assessment and10 full retakes. All16 lessons credited by quiz-based mastery; implementation lab not performed in this assessment. Preserve residual review: KV byte accounting; pre-norm residual identity; selected-but-unchanged MLM targets; adding [CLS] to patch count; teacher forcing; sentinel reinsertion order; speaker diarization. Earlier failures and retakes remain historical evidence.
