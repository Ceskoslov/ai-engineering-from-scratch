# Phase 06 — speech-and-audio Review Summary

[All phases](../progress.md)

- Status: **Done / Passed**; passed on 2026-10-26; coverage: **17 lessons**.
- Initial score: **38/51**; final effective score: **44/51 (86.27%)**.
- Cumulative responses: 63, with 49 correct; **14 initial/retake mistakes** retained. Cumulative responses include retakes and are not the mastery-score denominator.
- Pass criteria: effective phase score ≥85% and final score ≥2/3 in every lesson; all criteria met. Completion basis: quiz-based mastery; implementation labs were not performed in this assessment.

## Weak points and review priorities

- Prioritize L12/L14 VAD counter reset conditions and consecutive versus accumulated silence. Trace the code rather than assuming the toy enforces consecutive speech. L16 selects the first position reaching the threshold.
- L04: CTC sums alignments that collapse to the target transcript. L05: avoid propagating hallucinated text as a prompt across windows. L08: distinguish voice conversion from text-driven voice cloning. L15: full-duplex interaction receives and produces audio simultaneously.
- L02 windowing/log compression, preprocessing consistency, and frame counting; L03 population variance and multilabel sigmoid+BCE; and L17 RTFx throughput/response latency and utterance/corpus WER all reached 3/3 in their final retakes. Retain them for spaced recall.

## Lessons with mistakes and retake outcomes

Lessons with mistakes or retakes are listed below, along with any additional rows retained from the original ledger. Unlisted lessons scored 3/3 initially and finally. A final 3/3 indicates correction in a later assessment where applicable; retain those topics for spaced recall. Lessons at 2/3 remain review priorities.

| Lesson | Initial score | Final effective score / retake |
|---|---|---|
| [Spectrograms, Mel Scale & Audio Features](../../../phases/06-speech-and-audio/02-spectrograms-mel-features/docs/en.md) | 0/3 | 3/3 (attempt2) |
| [Audio Classification — From k-NN on MFCCs to AST and BEATs](../../../phases/06-speech-and-audio/03-audio-classification/docs/en.md) | 2/3 | 3/3 (attempt3) |
| [Speech Recognition (ASR) — CTC, RNN-T, Attention](../../../phases/06-speech-and-audio/04-speech-recognition-asr/docs/en.md) | 2/3 | 2/3 |
| [Whisper — Architecture & Fine-Tuning](../../../phases/06-speech-and-audio/05-whisper-architecture-finetuning/docs/en.md) | 2/3 | 2/3 |
| [Voice Cloning & Voice Conversion](../../../phases/06-speech-and-audio/08-voice-cloning-conversion/docs/en.md) | 2/3 | 2/3 |
| [Build a Voice Assistant Pipeline — The Phase 6 Capstone](../../../phases/06-speech-and-audio/12-voice-assistant-pipeline/docs/en.md) | 2/3 | 2/3 |
| [Voice Activity Detection & Turn-Taking — Silero, Cobra, and the Flush Trick](../../../phases/06-speech-and-audio/14-voice-activity-detection-turn-taking/docs/en.md) | 2/3 | 2/3 |
| [Streaming Speech-to-Speech — Moshi, Hibiki, and Full-Duplex Dialogue](../../../phases/06-speech-and-audio/15-streaming-speech-to-speech-moshi-hibiki/docs/en.md) | 2/3 | 2/3 |
| [Voice Anti-Spoofing & Audio Watermarking — ASVspoof 5, AudioSeal, WaveVerify](../../../phases/06-speech-and-audio/16-anti-spoofing-audio-watermarking/docs/en.md) | 2/3 | 2/3 |
| [Audio Evaluation — WER, MOS, UTMOS, MMAU, FAD, and the Open Leaderboards](../../../phases/06-speech-and-audio/17-audio-evaluation-metrics/docs/en.md) | 1/3 | 3/3 (attempt2) |

## Condensed mistake records

Question IDs, prompts, selected wrong answers, correct answers, and explanations are retained. Other distractors, correct-only questions, and per-response score logs are omitted. Prompts and explanations retain their original English wording. These are historical initial/retake mistakes, not pending retake requirements.

### p06-l02-a1-q1

Why multiply each audio frame by a Hann window before computing its Fourier transform?

- Learner answer: B — To compress large differences in spectral magnitude logarithmically.
- Correct answer: C — To reduce spectral leakage by tapering the frame boundaries.
- Explanation: Tapering the frame boundaries reduces discontinuities at the edges, which reduces spectral leakage. Log compression handles spectral dynamic range, not frame-edge tapering.

### p06-l02-a1-q2

Training used 80 log-mel features with per-utterance normalization. Inference uses 128 features with global normalization. What should you do first?

- Learner answer: C — Increase the inference audio amplitude to compensate for the mismatch.
- Correct answer: A — Match the inference feature settings to the training pipeline.
- Explanation: Feature dimensions and normalization must match the trained frontend; different settings change the model input representation. Increasing amplitude does not fix feature-count or normalization mismatches.

### p06-l02-a1-q3

The framing code uses n = 1 + (len(signal) - frame_len) // hop and keeps only those full frames. For len(signal) = 1000, frame_len = 400, and hop = 160, how many frames does it return?

- Learner answer: A — 3
- Correct answer: D — 4
- Explanation: Integer division gives 600 // 160 = 3, so n = 4; starts are 0, 160, 320, and 480.

### p06-l03-a1-q3

The summarize function concatenates per-coefficient means with population variances across frames. What does summarize([[1, 3], [3, 7]]) return?

- Learner answer: B — [2, 5, 2, 8]
- Correct answer: D — [2, 5, 1, 4]
- Explanation: Means are 2 and 5; average squared deviations are 1 and 4. The function returns mean + var. Option B uses sample variances with denominator n-1 rather than population variances with denominator n.

### p06-l04-a1-q1

What does CTC training do when the transcript is known but the frame-to-token alignment is not?

- Learner answer: A — Assign each transcript token to an equally sized audio segment.
- Correct answer: B — Sum the probabilities of alignments that collapse to the transcript.
- Explanation: CTC marginalizes over valid frame-level alignments, including blanks and repeats, whose collapse yields the target transcript. Tokens need not occupy equally sized audio segments.

### p06-l05-a1-q2

A hallucinated phrase in one audio window keeps appearing in later windows because earlier decoded text is reused as context. Which change directly interrupts that feedback path?

- Learner answer: C — Reuse the hallucinated phrase as the language prompt.
- Correct answer: A — Disable conditioning on previous decoded text.
- Explanation: Disabling conditioning on previous text prevents an erroneous previous-window transcript from being reused as decoder context. Reusing the hallucinated phrase as a prompt could reinforce it.

### p06-l08-a1-q1

A system takes source speech from speaker A and a reference voice from speaker B, then produces B’s voice saying the source words. Which task is this?

- Learner answer: C — Text-based voice cloning.
- Correct answer: B — Voice conversion.
- Explanation: Voice conversion preserves the source speech content while changing speaker identity; text-based cloning instead starts with text plus a reference voice.

### p06-l12-a1-q3

In capture_turn, each silent chunk after speech increments silent by 20; a speech chunk resets silent to 0. With silence_ms = 60, after speech then two silent chunks, one speech chunk, and two silent chunks, has it returned?

- Learner answer: A — Yes, because four silent chunks exceed 60 ms in total.
- Correct answer: D — No, because the latest speech reset the consecutive silence counter.
- Explanation: The intervening speech resets silent to zero. The final two silent chunks accumulate only 40 ms, below the 60 ms threshold.

### p06-l14-a1-q3

In the shown TurnDetector, speech adds 20 to speech_ms; idle silence does not reset speech_ms. Starting idle with min_speech_ms=60, what happens on speech, silence, speech, silence, speech?

- Learner answer: B — No event occurs because speech was never consecutive.
- Correct answer: C — START is emitted on the final chunk.
- Explanation: The toy code accumulates speech_ms across idle gaps: 20, then 40, then 60. It emits START on the final speech chunk, despite the gaps.

### p06-l15-a1-q1

What distinguishes full-duplex speech interaction from a system that strictly alternates listening and speaking?

- Learner answer: B — It must finish transcribing the entire conversation before replying.
- Correct answer: A — It can receive user audio while producing its own audio.
- Explanation: Full-duplex interaction keeps both incoming and outgoing audio streams active simultaneously, enabling interruptions and back-channeling.

### p06-l16-a1-q3

spectral_rolloff sets threshold = 0.85 * sum(spec), accumulates from index 0, and returns the first index where cum >= threshold. For spec = [1, 1, 6, 2], which index is returned?

- Learner answer: D — 2
- Correct answer: C — 3
- Explanation: The threshold is 8.5. Cumulative sums are 1, 2, 8, 10; index 3 is the first to reach it.

### p06-l17-a1-q1

What does inverse real-time factor (RTFx) measure for an audio system?

- Learner answer: A — The delay between the last user word and the first audible response.
- Correct answer: D — The number of audio seconds processed per wall-clock second.
- Explanation: RTFx is throughput: audio duration divided by processing time. It differs from first-token or first-audio latency.

### p06-l17-a1-q3

The toy ttr_wer function returns sum(per_utterance_WERs) / number_of_utterances. Two utterances have 1 error in 2 reference words and 1 error in 10 reference words. What does it return?

- Learner answer: A — 2/12, about 0.167.
- Correct answer: C — 0.3, the mean of 0.5 and 0.1.
- Explanation: The function averages utterance rates: (1/2 + 1/10)/2 = 0.3. It does not aggregate total errors over total reference words, which would give 2/12.

### p06-l03-a2-q2

A sound clip may contain both a siren and barking. Which output-and-loss pairing supports these simultaneous labels?

- Learner answer: B — A scalar regression output trained on the alphabetic class index.
- Correct answer: C — Independent sigmoid outputs with binary cross-entropy.
- Explanation: Multi-label classification needs independent per-class probabilities; binary cross-entropy supports more than one positive label per clip.
