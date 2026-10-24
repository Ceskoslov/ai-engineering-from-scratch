# Phase 05 review queue

Historical notes are preserved verbatim; some early remediation requests were superseded by later passes. Latest completion status is in [phase progress](progress.md).

- Phase05 Lesson22: MaxSim with query-token rows takes each row maximum then sums across query tokens. Row maxima0.9 and0.8 give1.7. Q66 chose B(1.5); correct D(1.7).

- Phase05 Lesson12: TextRank selects top sentence indices by score, then ranked.sort() restores source order for output. Indices[2,1] become[1,2], yielding Evidence then Conclusion. Q36 chose A; correct C.

- Phase05 Lesson08: backward states of a bidirectional LSTM require future tokens. Strict prefix-only streaming requires a forward-only recurrent model carrying state; full bidirectional context is unavailable. Q23 chose A; correct D.

- Phase05 Lesson03: skip-gram predicts surrounding context words from the center word; CBOW predicts the center word from surrounding context. Q7 chose C, reversing the directions; correct A.
