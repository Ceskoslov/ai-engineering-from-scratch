# Phase 06 review queue

Historical notes are preserved verbatim; some early remediation requests were superseded by later passes. Latest completion status is in [phase progress](progress.md).

No review items recorded.

- Lesson02, question4 (p06-l02-a1-q1): chose log compression instead of Hann windowing. Hann tapers frame boundaries to reduce spectral leakage; logarithms compress spectral dynamic range.

- Lesson02, question5 (p06-l02-a1-q2): chose amplitude adjustment for mismatched feature count and normalization. Match inference preprocessing to training; amplitude adjustment cannot repair either mismatch.

- Lesson02, question6 (p06-l02-a1-q3): omitted the initial frame in the full-frame count. Use 1 + (length - frame_len) // hop. Initial set 0/3; fresh scored retake started.

- Lesson02 remediation: fresh attempt2 scored3/3. Dynamic-range compression, training/inference preprocessing consistency, and full-frame counting answered correctly. Preserve initial misses for later recall.

- Lesson03, question9 (p06-l03-a1-q3): chose sample rather than population variances. summarize divides squared deviations by frame count n: means[2,5], population variances[1,4]. Lesson score2/3 meets minimum.

- Lesson04, question10 (p06-l04-a1-q1): chose equal-duration token assignment. CTC sums over all alignments collapsing to the transcript, allowing variable token durations and blanks.

- Lesson05, question14 (p06-l05-a1-q2): chose reusing a hallucinated phrase as prompt. Disable conditioning on previous decoded text to interrupt propagation across windows; reinserting the phrase may reinforce the error.

- Lesson08, question22 (p06-l08-a1-q1): confused voice conversion with text-based cloning. Conversion takes source speech and a target reference voice; text-based cloning takes written text and a reference voice.

- Lesson12, question36 (p06-l12-a1-q3): counted total silence instead of consecutive silence. Speech resets the counter; the final silence is40ms, below60ms. Lesson score2/3 meets minimum.

- Lesson14, question42 (p06-l14-a1-q3): assumed consecutive speech was enforced. Toy TurnDetector does not reset speech_ms during idle silence, so separated speech chunks accumulate to START. Lesson score2/3 meets minimum.

- Lesson15, question43 (p06-l15-a1-q1): chose waiting for full-conversation transcription. Full-duplex means receiving user audio and producing assistant audio simultaneously.

- Lesson16, question48 (p06-l16-a1-q3): chose index2 at cumulative8, below threshold8.5. Index3 reaches10 and is the first qualifying index. Lesson score2/3 meets minimum.

- Lesson17, question49 (p06-l17-a1-q1): confused RTFx with response latency. RTFx = audio seconds / processing wall-clock seconds; higher is faster throughput. End-of-speech to first-audio is response latency.

- Lesson17, question51 (p06-l17-a1-q3): confused corpus WER with mean utterance WER. Toy function averages0.5 and0.1 to0.3; corpus aggregation gives2/12. Initial set1/3; fresh scored retake started.

- Lesson17 remediation: fresh attempt2 scored3/3. RTFx, controlled FAD comparison, and mean utterance WER answered correctly. Phase effective43/51; Lesson03 full retake started to address the population-variance miss and overall threshold.

- Lesson03 retake attempt2 question2 (p06-l03-a2-q2): chose scalar regression on class index for simultaneous sound labels. Independent sigmoids plus binary cross-entropy support multiple positive classes; a single class index does not.

## Phase pass — 2026-10-26

Initial38/51; latest complete sets44/51 (86.27%); cumulative49/63. All17 lesson minima met. Lesson02 retake3/3, Lesson17 retake3/3, Lesson03 retakes2/3 then3/3. Preserve the earlier misses for spaced recall: windowing versus log compression; preprocessing consistency; population variance; CTC alignment marginalization; cross-window hallucination propagation; conversion versus cloning; consecutive versus cumulative VAD counters; full-duplex interaction; spectral threshold crossing; throughput versus latency; utterance versus corpus WER; multi-label outputs and losses. Remediation evidence remains above and in history.md. Quiz-based mastery only; implementation labs were not performed.
