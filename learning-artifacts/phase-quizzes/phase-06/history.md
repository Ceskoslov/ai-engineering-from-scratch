# Phase 06 detailed quiz history

Archive: read only when an earlier question or attempt is relevant. [Phase progress](progress.md).

No questions presented yet.

### p06-l01-a1-q1 — 2026-10-26

Why should audio be low-pass filtered before downsampling?

A) To increase the number of amplitude levels available for each sample.
B) To prevent frequencies above the new Nyquist limit from aliasing.
C) To preserve every original frequency at the lower sampling rate.
D) To convert the waveform into frequency coefficients before storage.

Learner answer: B
Correct answer: B
Result: Correct
Explanation: Downsampling lowers the Nyquist limit. Filtering out frequencies above that limit prevents them from folding into lower frequencies.

### p06-l01-a1-q2 — 2026-10-26

A 7 kHz sine wave is sampled directly at 10 kHz without anti-alias filtering. At what frequency does its alias appear?

A) 2 kHz
B) 5 kHz
C) 7 kHz
D) 3 kHz

Learner answer: D
Correct answer: D
Result: Correct
Explanation: The 7 kHz tone exceeds the 5 kHz Nyquist limit and folds to 10 − 7 = 3 kHz.

### p06-l01-a1-q3 — 2026-10-26

For a DFT computed from N = 400 samples at sr = 16000, the dominant positive-frequency bin is k_star = 10. What does k_star * sr / N return?

A) 400 Hz
B) 40 Hz
C) 1600 Hz
D) 640 Hz

Learner answer: A
Correct answer: A
Result: Correct
Explanation: The bin spacing is 16000 / 400 = 40 Hz, so bin 10 corresponds to 400 Hz.

### p06-l02-a1-q1 — 2026-10-26

Why multiply each audio frame by a Hann window before computing its Fourier transform?

A) To map uniformly spaced frequency bins onto the mel scale.
B) To compress large differences in spectral magnitude logarithmically.
C) To reduce spectral leakage by tapering the frame boundaries.
D) To decorrelate mel features into a smaller set of coefficients.

Learner answer: B
Correct answer: C
Result: Incorrect
Explanation: Tapering the frame boundaries reduces discontinuities at the edges, which reduces spectral leakage. Log compression handles spectral dynamic range, not frame-edge tapering.

### p06-l02-a1-q2 — 2026-10-26

Training used 80 log-mel features with per-utterance normalization. Inference uses 128 features with global normalization. What should you do first?

A) Match the inference feature settings to the training pipeline.
B) Pad the trained model output with 48 extra feature values.
C) Increase the inference audio amplitude to compensate for the mismatch.
D) Apply a DCT at inference without changing the training features.

Learner answer: C
Correct answer: A
Result: Incorrect
Explanation: Feature dimensions and normalization must match the trained frontend; different settings change the model input representation. Increasing amplitude does not fix feature-count or normalization mismatches.

### p06-l02-a1-q3 — 2026-10-26

The framing code uses n = 1 + (len(signal) - frame_len) // hop and keeps only those full frames. For len(signal) = 1000, frame_len = 400, and hop = 160, how many frames does it return?

A) 3
B) 5
C) 6
D) 4

Learner answer: A
Correct answer: D
Result: Incorrect
Explanation: Integer division gives 600 // 160 = 3, so n = 4; starts are 0, 160, 320, and 480.

### p06-l02-a2-q1 — 2026-10-26

Which operation compresses the dynamic range of mel magnitudes while retaining their time-frequency organization?

A) Multiplying each waveform frame by a Hann window.
B) Taking a logarithm after applying a small positive floor.
C) Increasing the hop between successive waveform frames.
D) Applying an inverse Fourier transform to each spectrum.

Learner answer: B
Correct answer: B
Result: Correct
Explanation: A logarithm compresses the range of spectral values. A positive floor prevents taking the logarithm of zero.

### p06-l02-a2-q2 — 2026-10-26

A model was trained on 16 kHz audio using 80 log-mel bins. Your input is 48 kHz audio. Which preprocessing plan preserves the trained input representation?

A) Extract 80 bins at 48 kHz and keep all other settings.
B) Extract 240 bins at 48 kHz to match the rate ratio.
C) Relabel the audio as 16 kHz without resampling it.
D) Resample to 16 kHz, then use the training feature settings.

Learner answer: D
Correct answer: D
Result: Correct
Explanation: Proper resampling matches the expected sample rate, and matching the feature settings preserves the trained frontend representation.

### p06-l02-a2-q3 — 2026-10-26

With n = 1 + (len(signal) - frame_len) // hop, what is n when len(signal) = 720, frame_len = 400, and hop = 160?

A) 3
B) 2
C) 4
D) 5

Learner answer: A
Correct answer: A
Result: Correct
Explanation: 1 + (720 - 400) // 160 = 1 + 2 = 3; the frames start at 0, 160, and 320.

Lesson02 attempt2 complete: 3/3, replacing initial0/3 for effective scoring. Initial phase score3/6; effective6/6 covered (51 planned); cumulative6/9.

### p06-l03-a1-q1 — 2026-10-26

An audio classifier has high overall accuracy but often misses rare sound classes. Which metrics best reveal this weakness?

A) Top-1 accuracy and the total number of test clips.
B) Average training loss and total parameter count.
C) Per-class recall and macro-averaged F1.
D) Inference speed and mean clip duration.

Learner answer: C
Correct answer: C
Result: Correct
Explanation: Per-class recall exposes missed rare classes; macro F1 gives each class equal weight instead of letting common classes dominate.

### p06-l03-a1-q2 — 2026-10-26

You use balanced sampling to train on an imbalanced sound dataset. How should you evaluate expected performance on the original deployment distribution?

A) Use a held-out set preserving the deployment class distribution.
B) Balance the test set and report only overall accuracy.
C) Evaluate on balanced batches drawn from the training clips.
D) Remove rare classes from evaluation to stabilize the score.

Learner answer: A
Correct answer: A
Result: Correct
Explanation: Keep evaluation representative of deployment, separate from training, and include per-class metrics for imbalance.

### p06-l03-a1-q3 — 2026-10-26

The summarize function concatenates per-coefficient means with population variances across frames. What does summarize([[1, 3], [3, 7]]) return?

A) [2, 5]
B) [2, 5, 2, 8]
C) [1, 4, 2, 5]
D) [2, 5, 1, 4]

Learner answer: B
Correct answer: D
Result: Incorrect
Explanation: Means are 2 and 5; average squared deviations are 1 and 4. The function returns mean + var. Option B uses sample variances with denominator n-1 rather than population variances with denominator n.

Lesson03 initial set complete: 2/3; lesson minimum met. Initial phase5/9; effective8/9 covered (51 planned); cumulative8/12.

### p06-l04-a1-q1 — 2026-10-26

What does CTC training do when the transcript is known but the frame-to-token alignment is not?

A) Assign each transcript token to an equally sized audio segment.
B) Sum the probabilities of alignments that collapse to the transcript.
C) Train only on the single alignment chosen by framewise argmax.
D) Require manually annotated token boundaries before computing loss.

Learner answer: a (normalized: A)
Correct answer: B
Result: Incorrect
Explanation: CTC marginalizes over valid frame-level alignments, including blanks and repeats, whose collapse yields the target transcript. Tokens need not occupy equally sized audio segments.

### p06-l04-a1-q2 — 2026-10-26

An ASR system makes 2 substitutions, 1 deletion, and 3 insertions against a 20-word reference. What is its word error rate?

A) 15%
B) 20%
C) 25%
D) 30%

Learner answer: D
Correct answer: D
Result: Correct
Explanation: WER = (2 + 1 + 3) / 20 = 0.30, or 30%.

### p06-l04-a1-q3 — 2026-10-26

The greedy CTC decoder appends p when p != prev and p != blank, then always sets prev = p. With blank represented by _, what does a a _ a b b _ collapse to?

A) aab
B) ab
C) aaabb
D) a_b_

Learner answer: A
Correct answer: A
Result: Correct
Explanation: Adjacent repeated a values merge, but a blank resets prev and separates the second a; adjacent b values merge and blanks are omitted.

Lesson04 initial set complete: 2/3; lesson minimum met. Initial phase7/12; effective10/12 covered (51 planned); cumulative10/15.

### p06-l05-a1-q1 — 2026-10-26

In Whisper’s encoder-decoder architecture, what does decoder cross-attention let each generated token use?

A) Only the previously generated text, without audio information.
B) The reference transcript supplied at inference time.
C) Audio representations produced by the encoder.
D) The output probabilities of an independent CTC decoder.

Learner answer: C
Correct answer: C
Result: Correct
Explanation: The decoder uses cross-attention to condition text generation on the encoder’s audio representations.

### p06-l05-a1-q2 — 2026-10-26

A hallucinated phrase in one audio window keeps appearing in later windows because earlier decoded text is reused as context. Which change directly interrupts that feedback path?

A) Disable conditioning on previous decoded text.
B) Increase the number of mel features at inference.
C) Reuse the hallucinated phrase as the language prompt.
D) Replace overlapping chunks with a larger vocabulary.

Learner answer: C
Correct answer: A
Result: Incorrect
Explanation: Disabling conditioning on previous text prevents an erroneous previous-window transcript from being reused as decoder context. Reusing the hallucinated phrase as a prompt could reinforce it.

### p06-l05-a1-q3 — 2026-10-26

A chunk scheduler sets step = chunk_s - stride_s, starts at 0, and stops once a chunk reaches the clip end. With total_seconds = 60, chunk_s = 30, and stride_s = 5, which intervals does it return?

A) [(0,30), (30,60)]
B) [(0,30), (5,35), (10,40), (15,45), (20,50), (25,55), (30,60)]
C) [(0,25), (25,50), (50,60)]
D) [(0,30), (25,55), (50,60)]

Learner answer: D
Correct answer: D
Result: Correct
Explanation: The step is 25 seconds; chunks start at 0, 25, and 50. The last end is capped at 60, then the loop stops.

Lesson05 initial set complete: 2/3; lesson minimum met. Initial phase9/15; effective12/15 covered (51 planned); cumulative12/18.

### p06-l06-a1-q1 — 2026-10-26

A caller claims to be Alice, and the system compares the caller’s voice embedding with Alice’s enrolled reference. Which task is this?

A) Speaker identification across the entire enrollment bank.
B) Speaker verification against a claimed identity.
C) Speaker diarization across the conversation timeline.
D) Speech recognition of the caller’s spoken words.

Learner answer: B
Correct answer: B
Result: Correct
Explanation: Verification checks a claimed identity using a 1:1 comparison; identification searches a bank, diarization finds who spoke when, and ASR finds the words.

### p06-l06-a1-q2 — 2026-10-26

A speaker verifier will serve telephone calls, but its published threshold was evaluated on web-video audio. How should you choose its operating threshold?

A) Keep the published threshold because cosine scores are domain-independent.
B) Tune it on the final test calls, then report performance on those same calls.
C) Use the average similarity among enrollment recordings as the threshold.
D) Tune it on held-out target-domain development trials with genuine and impostor pairs.

Learner answer: D
Correct answer: D
Result: Correct
Explanation: Channel mismatch changes score distributions. Choose the operating threshold using representative held-out development trials, and keep the final test set separate.

### p06-l06-a1-q3 — 2026-10-26

The verifier returns cosine(enroll, test) >= threshold, and cosine returns 0.0 if either vector has zero norm. What does verify([0, 0], [1, 0], threshold=0.0) return?

A) True, because 0.0 >= 0.0.
B) False, because zero vectors are explicitly rejected.
C) It raises a division-by-zero error.
D) None, because the embedding has no direction.

Learner answer: A
Correct answer: A
Result: Correct
Explanation: The cosine helper returns 0.0 for a zero-norm vector; the inclusive threshold comparison then returns True. The toy verifier has no separate invalid-embedding rejection.

Lesson06 initial set complete: 3/3. Initial phase12/18; effective15/18 covered (51 planned); cumulative15/21.

### p06-l07-a1-q1 — 2026-10-26

In a TTS pipeline with separate acoustic and vocoder stages, what is the vocoder’s role?

A) Normalize written dates and numbers into spoken text.
B) Predict phoneme durations from the input text.
C) Convert an acoustic representation such as a mel spectrogram into a waveform.
D) Compare synthesized speech with a claimed speaker’s enrollment embedding.

Learner answer: C
Correct answer: C
Result: Correct
Explanation: The vocoder maps the acoustic representation to audio samples; text normalization and duration prediction belong to earlier stages.

### p06-l07-a1-q2 — 2026-10-26

Synthesized speech sounds smooth, but abbreviations and dates are spoken with the wrong meaning. Which pipeline stage should you inspect first?

A) Text normalization before phonemization.
B) Waveform clipping after vocoding.
C) Speaker-embedding similarity scoring.
D) Audio sample-rate conversion after synthesis.

Learner answer: A
Correct answer: A
Result: Correct
Explanation: Text normalization determines how dates, numbers, and abbreviations should be expanded before pronunciation and synthesis.

### p06-l07-a1-q3 — 2026-10-26

The lesson’s toy pipeline maps a mel sequence with T frames to a waveform with T * 256 samples. For T = 100, how many samples does wav contain?

A) 256
B) 24000
C) 256000
D) 25600

Learner answer: D
Correct answer: D
Result: Correct
Explanation: 100 frames multiplied by 256 samples per frame gives 25,600 waveform samples.

Lesson07 initial set complete: 3/3. Initial phase15/21; effective18/21 covered (51 planned); cumulative18/24.

### p06-l08-a1-q1 — 2026-10-26

A system takes source speech from speaker A and a reference voice from speaker B, then produces B’s voice saying the source words. Which task is this?

A) Speaker verification.
B) Voice conversion.
C) Text-based voice cloning.
D) Speaker diarization.

Learner answer: C
Correct answer: B
Result: Incorrect
Explanation: Voice conversion preserves the source speech content while changing speaker identity; text-based cloning instead starts with text plus a reference voice.

### p06-l08-a1-q2 — 2026-10-26

A generated clip has high speaker-embedding similarity to its target voice. What additional check addresses whether it actually says the intended words?

A) Measure similarity between two target reference recordings.
B) Check only the duration of the generated clip.
C) Check whether the watermark payload is recoverable.
D) Transcribe the generated clip and compute CER or WER against the intended text.

Learner answer: D
Correct answer: D
Result: Correct
Explanation: Speaker similarity measures voice identity, while ASR-based CER or WER checks intelligibility and content accuracy.

### p06-l08-a1-q3 — 2026-10-26

The toy gate first asserts verify_signature(record), then asserts record["speaker_id"] == hash_speaker(ref_audio), then calls tts.infer and watermark. With Python assertions enabled, a valid signature, and a mismatched speaker_id, what happens?

A) AssertionError is raised before synthesis or watermarking.
B) Synthesis runs, but watermarking is skipped.
C) Watermarked audio is returned because the signature is valid.
D) The speaker_id is automatically replaced before synthesis.

Learner answer: A
Correct answer: A
Result: Correct
Explanation: The second assertion fails and raises AssertionError, so neither the synthesis nor watermark call is reached.

Lesson08 initial set complete: 2/3. Initial phase17/24; effective20/24 covered (51 planned); cumulative20/27.

### p06-l09-a1-q1 — 2026-10-26

In a music generator that autoregressively predicts neural-codec tokens, what converts the generated token sequence into an audible waveform?

A) The text tokenizer.
B) The neural audio codec decoder.
C) The CLAP similarity scorer.
D) The FAD evaluation routine.

Learner answer: B
Correct answer: B
Result: Correct
Explanation: The language model predicts discrete audio-codec tokens, and the codec decoder reconstructs waveform samples from those tokens.

### p06-l09-a1-q2 — 2026-10-26

Generated music has a low FAD relative to a reference set but often ignores the text prompt. Which additional evaluation directly targets prompt adherence?

A) Count the model’s parameters.
B) Compare generated and reference file sizes.
C) Measure only average clip duration.
D) Measure text-audio alignment with CLAP.

Learner answer: D
Correct answer: D
Result: Correct
Explanation: FAD compares audio embedding distributions; CLAP compares the text prompt with the generated audio to assess alignment.

### p06-l09-a1-q3 — 2026-10-26

The toy tempo parser starts with bpm = 120. For each whitespace-separated token ending in "bpm", it tries int(token[:-3]) and ignores ValueError. What bpm results from the prompt "pop at 140 bpm"?

A) 120
B) 140
C) 0
D) A ValueError escapes the parser.

Learner answer: A
Correct answer: A
Result: Correct
Explanation: The token "140" does not end in "bpm"; the token "bpm" yields int("") and a caught ValueError. The initial 120 remains.

Lesson09 initial set complete: 3/3. Initial phase20/27; effective23/27 covered (51 planned); cumulative23/30.

### p06-l10-a1-q1 — 2026-10-26

In an audio encoder → projector → language model architecture, what is the projector’s main role?

A) Convert the language model’s text output into waveform samples.
B) Assign speaker identities to every segment before encoding.
C) Map audio-encoder features into the language model’s embedding space.
D) Compute word error rate between the model output and a reference.

Learner answer: C
Correct answer: C
Result: Correct
Explanation: The projector bridges the audio encoder’s feature representation and the language model’s input embedding space.

### p06-l10-a1-q2 — 2026-10-26

An audio-language model has strong aggregate QA accuracy. Your task requires comparing two clips. What evaluation best establishes whether it fits your task?

A) Evaluate a representative multi-audio comparison subset separately.
B) Use aggregate accuracy as proof of equal performance across categories.
C) Evaluate only single-clip speech transcription questions.
D) Choose the largest model without evaluating clip comparisons.

Learner answer: A
Correct answer: A
Result: Correct
Explanation: Aggregate results can hide category-specific weaknesses. Direct multi-audio comparison evaluation tests the capability the deployment actually needs.

### p06-l10-a1-q3 — 2026-10-26

AudioProjector applies Linear(1280, 4096), GELU, then Linear(4096, 4096) to the last dimension. For input shape (2, 50, 1280), what is the output shape?

A) (2, 4096, 50)
B) (2, 1280, 4096)
C) (2, 50, 1280)
D) (2, 50, 4096)

Learner answer: D
Correct answer: D
Result: Correct
Explanation: The linear layers transform only the last feature dimension; the batch size 2 and sequence length 50 remain unchanged.

Lesson10 initial set complete: 3/3. Initial phase23/30; effective26/30 covered (51 planned); cumulative26/33.

### p06-l11-a1-q1 — 2026-10-26

What tradeoff does a network jitter buffer introduce in a real-time audio pipeline?

A) Higher sample precision at the cost of a lower Nyquist frequency.
B) More tolerance for late or reordered packets at the cost of added latency.
C) Better speaker recognition at the cost of fewer enrolled speakers.
D) Faster model inference at the cost of lower text-token accuracy.

Learner answer: B
Correct answer: B
Result: Correct
Explanation: Buffering allows packets to be reordered and late arrivals to be absorbed, but waiting before playback adds delay.

### p06-l11-a1-q2 — 2026-10-26

A voice assistant’s own synthesized speech re-enters its microphone and triggers recognition as if the user were speaking. Which component directly addresses this feedback path?

A) A larger network jitter buffer.
B) A higher mel-filterbank bin count.
C) A longer text generation context.
D) Acoustic echo cancellation.

Learner answer: D
Correct answer: D
Result: Correct
Explanation: Acoustic echo cancellation suppresses the speaker-to-microphone echo path so the assistant’s output is not treated as user input.

### p06-l11-a1-q3 — 2026-10-26

RingBuffer uses deque(maxlen=4); write extends it and read removes the oldest available items. After write([1,2,3]), write([4,5]), then read(2), what is returned and what remains?

A) Returns [2,3]; leaves [4,5].
B) Returns [1,2]; leaves [3,4].
C) Returns [4,5]; leaves [2,3].
D) Returns [1,2]; leaves [3,4,5].

Learner answer: A
Correct answer: A
Result: Correct
Explanation: Extending beyond capacity drops the oldest sample 1, leaving [2,3,4,5]; reading two removes 2 and 3, leaving [4,5].

Lesson11 initial set complete: 3/3. Initial phase26/33; effective29/33 covered (51 planned); cumulative29/36.

### p06-l12-a1-q1 — 2026-10-26

Why keep a short pre-roll audio buffer before voice activity detection triggers a new turn?

A) To include the assistant’s previous answer in the user transcript.
B) To wait for the entire utterance before starting audio capture.
C) To recover speech onset that occurred before the detector triggered.
D) To replace the speech recognizer with a fixed-length recording.

Learner answer: C
Correct answer: C
Result: Correct
Explanation: Pre-roll retains recent audio from before the trigger so detection delay does not clip the first sounds or words.

### p06-l12-a1-q2 — 2026-10-26

On user interruption, playback stops, but the old LLM continues generating and fills the next response queue. What should the interruption handler also do?

A) Cancel the old LLM generation and discard its queued output.
B) Increase the silence threshold before recognizing the interruption.
C) Append the old generated text to the new user transcript.
D) Restart playback when the old model finishes generating.

Learner answer: A
Correct answer: A
Result: Correct
Explanation: Barge-in must cancel stale generation and prevent its buffered output from leaking into the new turn.

### p06-l12-a1-q3 — 2026-10-26

In capture_turn, each silent chunk after speech increments silent by 20; a speech chunk resets silent to 0. With silence_ms = 60, after speech then two silent chunks, one speech chunk, and two silent chunks, has it returned?

A) Yes, because four silent chunks exceed 60 ms in total.
B) Yes, because any silent chunk immediately ends the turn.
C) No, because the silence counter increases only during speech.
D) No, because the latest speech reset the consecutive silence counter.

Learner answer: A
Correct answer: D
Result: Incorrect
Explanation: The intervening speech resets silent to zero. The final two silent chunks accumulate only 40 ms, below the 60 ms threshold.

Lesson12 initial set complete: 2/3. Initial phase28/36; effective31/36 covered (51 planned); cumulative31/39.

### p06-l13-a1-q1 — 2026-10-26

In residual vector quantization, what does each codebook after the first quantize?

A) The original waveform independently of the earlier codebooks.
B) The remaining error after the earlier quantized approximations.
C) The text transcript corresponding to the audio frame.
D) The decoder’s final waveform after resampling.

Learner answer: B
Correct answer: B
Result: Correct
Explanation: Each successive codebook approximates the residual left by earlier stages; the selected code vectors are summed to reconstruct the encoder representation.

### p06-l13-a1-q2 — 2026-10-26

Two codecs reconstruct held-out audio equally well, but you need tokens for text-conditioned speech generation. Which additional property should you evaluate?

A) Whether the codec output filenames contain the transcript.
B) Whether its decoder can run without any input tokens.
C) Whether all codebooks have identical token sequences.
D) Whether the tokens expose content structure that a language model can learn.

Learner answer: D
Correct answer: D
Result: Correct
Explanation: Reconstruction fidelity alone does not establish suitability for generation. Useful linguistic structure, including semantic-acoustic organization, can help the language model predict speech.

### p06-l13-a1-q3 — 2026-10-26

Given codes.shape == (1, 8, 125), the code sets semantic = codes[:, 0] and acoustic = codes[:, 1:]. What are their shapes?

A) semantic: (1, 125); acoustic: (1, 7, 125).
B) semantic: (1, 1, 125); acoustic: (1, 8, 125).
C) semantic: (8, 125); acoustic: (7, 125).
D) semantic: (1, 8); acoustic: (1, 8, 124).

Learner answer: A
Correct answer: A
Result: Correct
Explanation: Integer indexing selects and removes the codebook axis for semantic; slicing retains that axis with the remaining seven codebooks for acoustic.

Lesson13 initial set complete: 3/3. Initial phase31/39; effective34/39 covered (51 planned); cumulative34/42.

### p06-l14-a1-q1 — 2026-10-26

Why add semantic endpointing to a voice activity detector when deciding whether a user has finished their turn?

A) To reconstruct a waveform from the transcript.
B) To identify the user from a voice embedding.
C) To eliminate the need to capture audio frames.
D) To distinguish a pause within a thought from a completed turn.

Learner answer: D
Correct answer: D
Result: Correct
Explanation: VAD detects speech activity; semantic endpointing adds context to judge whether a silent pause means the user is finished.

### p06-l14-a1-q2 — 2026-10-26

Your streaming recognizer buffers look-ahead audio and explicitly supports flushing. Once turn end is detected, how can you request the remaining transcript promptly?

A) Discard buffered audio and transcribe only the next turn.
B) Send the remaining audio, issue a flush, and receive the final transcript.
C) Increase the silence hangover by the recognizer’s full look-ahead delay.
D) Replace the recognizer’s sample rate metadata without resampling.

Learner answer: B
Correct answer: B
Result: Correct
Explanation: A supported flush asks the recognizer to process buffered audio and emit the remaining transcript rather than wait for more audio.

### p06-l14-a1-q3 — 2026-10-26

In the shown TurnDetector, speech adds 20 to speech_ms; idle silence does not reset speech_ms. Starting idle with min_speech_ms=60, what happens on speech, silence, speech, silence, speech?

A) END is emitted on the final chunk.
B) No event occurs because speech was never consecutive.
C) START is emitted on the final chunk.
D) START is emitted on the first chunk.

Learner answer: B
Correct answer: C
Result: Incorrect
Explanation: The toy code accumulates speech_ms across idle gaps: 20, then 40, then 60. It emits START on the final speech chunk, despite the gaps.

Lesson14 initial set complete: 2/3. Initial phase33/42; effective36/42 covered (51 planned); cumulative36/45.

### p06-l15-a1-q1 — 2026-10-26

What distinguishes full-duplex speech interaction from a system that strictly alternates listening and speaking?

A) It can receive user audio while producing its own audio.
B) It must finish transcribing the entire conversation before replying.
C) It uses one audio stream that switches direction after each turn.
D) It converts all audio into text and never produces speech.

Learner answer: B
Correct answer: A
Result: Incorrect
Explanation: Full-duplex interaction keeps both incoming and outgoing audio streams active simultaneously, enabling interruptions and back-channeling.

### p06-l15-a1-q2 — 2026-10-26

A low-latency dialogue model handles natural conversation but lacks reliable tool calling. Your assistant must execute validated calendar actions. Which design addresses that gap?

A) Treat generated speech as proof that the calendar action succeeded.
B) Reduce codec frame duration until tool execution emerges.
C) Integrate a separate tool-capable orchestration path with validated dispatch.
D) Replace tool schemas with speaker embeddings.

Learner answer: C
Correct answer: C
Result: Correct
Explanation: Low-latency dialogue capability does not establish tool orchestration. A separate path can validate and dispatch actions and return actual results.

### p06-l15-a1-q3 — 2026-10-26

The client creates mic_task and spk_task with asyncio.create_task, then awaits asyncio.gather(mic_task, spk_task). Both coroutines regularly await I/O. How do they run?

A) The microphone coroutine finishes before the speaker coroutine starts.
B) They run concurrently, yielding to each other while waiting for I/O.
C) They necessarily execute in two separate operating-system processes.
D) gather cancels the microphone task when speaker playback starts.

Learner answer: B
Correct answer: B
Result: Correct
Explanation: Both tasks are scheduled on the event loop and can make progress while the other awaits I/O; this is concurrency, not an automatic separate-process guarantee.

Lesson15 initial set complete: 2/3. Initial phase35/45; effective38/45 covered (51 planned); cumulative38/48.

### p06-l16-a1-q1 — 2026-10-26

Which statement correctly distinguishes audio watermarking from anti-spoofing detection?

A) Watermarking proves the spoken words are factually accurate.
B) Anti-spoofing detection requires every generator to embed a payload.
C) Both methods require the original reference waveform at detection time.
D) Watermarking embeds a detectable signal; anti-spoofing estimates whether audio is synthetic.

Learner answer: D
Correct answer: D
Result: Correct
Explanation: Watermarking adds a signal during generation. Anti-spoofing classifies audio and can be applied to outputs from generators that do not cooperate.

### p06-l16-a1-q2 — 2026-10-26

Your watermark detector finds no watermark in an uploaded recording. What conclusion is justified?

A) The recording is certainly authentic human speech.
B) No watermark was detected; this alone does not establish authenticity.
C) The recording must be synthetic because metadata was removed.
D) The speaker’s identity has been cryptographically verified.

Learner answer: B
Correct answer: B
Result: Correct
Explanation: Synthetic audio may never have been watermarked, or the watermark may be damaged or missed. Absence of detection is not proof of authenticity.

### p06-l16-a1-q3 — 2026-10-26

spectral_rolloff sets threshold = 0.85 * sum(spec), accumulates from index 0, and returns the first index where cum >= threshold. For spec = [1, 1, 6, 2], which index is returned?

A) 0
B) 1
C) 3
D) 2

Learner answer: D
Correct answer: C
Result: Incorrect
Explanation: The threshold is 8.5. Cumulative sums are 1, 2, 8, 10; index 3 is the first to reach it.

Lesson16 initial set complete: 2/3. Initial phase37/48; effective40/48 covered (51 planned); cumulative40/51.

### p06-l17-a1-q1 — 2026-10-26

What does inverse real-time factor (RTFx) measure for an audio system?

A) The delay between the last user word and the first audible response.
B) The fraction of generated words matching the reference transcript.
C) The mean listener rating of the generated audio’s naturalness.
D) The number of audio seconds processed per wall-clock second.

Learner answer: A
Correct answer: D
Result: Incorrect
Explanation: RTFx is throughput: audio duration divided by processing time. It differs from first-token or first-audio latency.

### p06-l17-a1-q2 — 2026-10-26

A new ASR model improves overall WER, but users with certain accents report worse recognition. What should the evaluation report add?

A) Only the new model’s total parameter count.
B) WER by relevant accent slices on a representative held-out set.
C) Only the fastest processing time observed.
D) A smaller test set containing only the majority accent.

Learner answer: B
Correct answer: B
Result: Correct
Explanation: Aggregate WER can hide subgroup regressions. Slice-level evaluation reveals which users experience worse recognition.

### p06-l17-a1-q3 — 2026-10-26

The toy ttr_wer function returns sum(per_utterance_WERs) / number_of_utterances. Two utterances have 1 error in 2 reference words and 1 error in 10 reference words. What does it return?

A) 2/12, about 0.167.
B) 0.6, the sum of the two rates.
C) 0.3, the mean of 0.5 and 0.1.
D) 0.2, the mean error count divided by 5.

Learner answer: A
Correct answer: C
Result: Incorrect
Explanation: The function averages utterance rates: (1/2 + 1/10)/2 = 0.3. It does not aggregate total errors over total reference words, which would give 2/12.

Lesson17 initial set complete: 1/3. Initial phase38/51; effective41/51 (80.39%); cumulative41/54. Phase not passed: overall below85%, Lesson17 below2/3. Starting full Lesson17 retake.

### p06-l17-a2-q1 — 2026-10-26

A recognizer processes a 60-second recording in 3 seconds. What is its RTFx?

A) 0.05×
B) 3×
C) 20×
D) 60×

Learner answer: C
Correct answer: C
Result: Correct
Explanation: RTFx = audio duration / processing time = 60 / 3 = 20×.

### p06-l17-a2-q2 — 2026-10-26

Two music generators are compared using FAD, but each is scored against a different reference genre distribution. How should you make the comparison interpretable?

A) Score both against the same appropriate reference set using the same embedding pipeline.
B) Choose whichever has the lower score without changing the reference sets.
C) Replace the reference audio with each generator’s own outputs.
D) Multiply each score by the model’s parameter count.

Learner answer: A
Correct answer: A
Result: Correct
Explanation: FAD depends on the reference distribution and embedding pipeline. A controlled comparison holds these fixed.

### p06-l17-a2-q3 — 2026-10-26

The toy evaluator returns sum(errors) / len(errors), where errors contains per-utterance WERs. For errors = [0.0, 0.25, 0.5], what is returned?

A) 0.75
B) 0.5
C) 0.125
D) 0.25

Learner answer: D
Correct answer: D
Result: Correct
Explanation: The function computes the arithmetic mean: (0 + 0.25 + 0.5) / 3 = 0.25.

Lesson17 attempt2 complete: 3/3, replacing initial1/3. Initial38/51; effective43/51 (84.31%); cumulative44/57. All lesson minima met; overall below85%. Starting full Lesson03 retake (latest2/3).

### p06-l03-a2-q1 — 2026-10-26

Why summarize MFCC frames using per-coefficient means and variances before k-NN classification?

A) To retain the exact temporal order of every phoneme.
B) To obtain a fixed-size vector from clips with different frame counts.
C) To turn each clip into a manually aligned text transcript.
D) To guarantee perfect classification without labeled examples.

Learner answer: B
Correct answer: B
Result: Correct
Explanation: Pooling across time yields a fixed-size embedding (twice the coefficient count), regardless of the number of frames, while discarding temporal order.

### p06-l03-a2-q2 — 2026-10-26

A sound clip may contain both a siren and barking. Which output-and-loss pairing supports these simultaneous labels?

A) One softmax output with exactly one class selected.
B) A scalar regression output trained on the alphabetic class index.
C) Independent sigmoid outputs with binary cross-entropy.
D) A forced blank label whenever two events overlap.

Learner answer: B
Correct answer: C
Result: Incorrect
Explanation: Multi-label classification needs independent per-class probabilities; binary cross-entropy supports more than one positive label per clip.

### p06-l03-a2-q3 — 2026-10-26

summarize returns per-coefficient means followed by population variances, dividing squared deviations by the number of frames. For frames [[2], [6]], what does it return?

A) [4, 4]
B) [4, 8]
C) [4, 2]
D) [2, 6]

Learner answer: A
Correct answer: A
Result: Correct
Explanation: The mean is4. Squared deviations are4 and4, and their population average is4, so the result is[4,4].

Lesson03 attempt2 complete: 2/3, replacing initial2/3. Initial38/51; effective43/51 (84.31%); cumulative46/60. All lesson minima met; overall below85%. Starting full Lesson03 attempt3.

### p06-l03-a3-q1 — 2026-10-26

What makes a sound-classification task multi-label rather than mutually exclusive multiclass?

A) Every recording must contain exactly one positive class.
B) Every class must have the same number of training examples.
C) Each recording must be converted into a text transcript first.
D) One recording can have several positive sound labels at once.

Learner answer: D
Correct answer: D
Result: Correct
Explanation: Multi-label classification allows simultaneous positive labels, such as both speech and music in one clip.

### p06-l03-a3-q2 — 2026-10-26

A sound-tagging model must detect overlapping events. Which evaluation directly assesses ranking quality across its multiple labels?

A) Mean average precision across sound classes.
B) Only top-1 accuracy after forcing one label per clip.
C) Only the number of audio frames per recording.
D) Word error rate on an unrelated speech transcript.

Learner answer: A
Correct answer: A
Result: Correct
Explanation: mAP evaluates class-wise label rankings and is appropriate for multi-label audio tagging; forcing one label would discard overlapping events.

### p06-l03-a3-q3 — 2026-10-26

The k-NN code selects the three highest cosine similarities, then returns the majority label. Neighbors in descending similarity are [(0.95, "dog"), (0.90, "siren"), (0.85, "siren"), (0.20, "dog")]. What does k=3 return?

A) "dog", because the closest neighbor always decides.
B) "siren", because it has two of the three selected votes.
C) Both labels, because k-NN always returns all labels.
D) An error, because similarities must sum to one.

Learner answer: B
Correct answer: B
Result: Correct
Explanation: The top three labels are dog, siren, siren. The supplied classifier uses majority voting, so siren wins.

Lesson03 attempt3 complete: 3/3, replacing attempt2 score2/3. Phase06 passed: initial38/51 (74.51%); effective44/51 (86.27%); cumulative49/63 including12 retake responses. All17 lessons meet2/3 minimum. Quiz-based mastery credit only; implementation lab not performed in this assessment.
