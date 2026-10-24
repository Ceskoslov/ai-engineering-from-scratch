# Phase 04 review queue

Historical notes are preserved verbatim; some early remediation requests were superseded by later passes. Latest completion status is in [phase progress](progress.md).

- Phase04 Lesson20 retake Q3: recall@K under this lesson protocol divides queries with at least one correct top-K match by total queries. Three successful queries out of four give0.75;3/8 counts retrieved items instead. Chose A; correct B. Retake2/3 meets the lesson minimum; cosine/L2 equivalence and semi-hard negatives remediated.

- Phase04 Lesson12 retake: scored3/3 on temporal kernels, ordered dense sampling, and an order-sensitive convolution trace. Prior Q34–35 misses remediated by this complete set; retain for later spaced recall.

- Phase04 Lesson20: semi-hard negatives satisfy d_ap < d_an < d_ap + margin; negatives closer than the positive are hard. At distances0.4 and0.5 with margin0.2, loss=0.1 and the negative is semi-hard. Q60 chose D; correct B. Initial1/3 preserved; fresh retake2/3 complete; these topics remediated, with query hit-rate denominator remaining for review.

- Phase04 Lesson20: for L2-normalized embeddings, squared Euclidean distance = 2 - 2*cosine similarity. Highest cosine and smallest distance give the same retrieval ranking, not opposite rankings. Q58 chose B; correct C.

- Phase04 Lesson13: PointNet uses a shared per-point MLP and symmetric coordinate-wise max pooling for permutation invariance. Sequence-position embeddings and concatenation in input order introduce order dependence. Q37 chose C; correct B.

- Phase04 Lesson12: motion direction requires ordered frames; dense consecutive sampling with a temporal model preserves direction, whereas random frame shuffling destroys consistent temporal structure. Q35 chose C; correct A. Initial1/3 preserved; fresh retake3/3 complete; temporal-order topic remediated.

- Phase04 Lesson12: a 2D CNN extracts spatial frame features, but averaging independent frame embeddings discards temporal order; reversing the same frames preserves the pooled representation. Q34 chose D; correct C.

- Phase04 Lesson09: D(fake.detach()) permits gradients into D but blocks this loss’s path into G; detach does not freeze D or disable autograd globally. Q27 chose B; correct D.

- Phase04 Lesson08: replace both box and mask predictors for a custom vocabulary; four foreground classes require five output classes including background0. The mask predictor does not adapt automatically. Q23 chose A; correct B.
