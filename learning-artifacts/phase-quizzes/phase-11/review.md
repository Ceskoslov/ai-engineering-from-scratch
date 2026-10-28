# Phase 11 review queue

Historical notes are preserved verbatim; some early remediation requests were superseded by later passes. Latest completion status is in [phase progress](progress.md).

Review topics from initial responses follow; all lessons now meet the mastery threshold.


- Lesson01, question3: JSON parsing accepts scalar strings; syntax validation does not enforce object shape or required fields. Answer B; correct A. Lesson score 2/3.

- Lesson02, question2: ReAct incorporates external tool observations into subsequent decisions; longer reasoning without tools cannot retrieve unavailable facts. Answer D; correct B.

- Lesson03, question3: bool subclasses int in Python. The toy number branch accepts True; the integer branch explicitly rejects bool. Answer B; correct A. Lesson score 2/3.

- Lesson04, question3: Unknown query words yield a zero vector. The cosine zero-norm guard returns 0.0 instead of dividing by zero; tied scores do not demonstrate relevance. Answer D; correct B. Lesson score 2/3.

- Lesson07, question3: The toy faithfulness evaluator excludes short sentences and returns 1.0 when none remain, even with no evidence. Follow the early return; a perfect proxy score does not prove support. Answer B; correct C. Lesson score 2/3.

- Lesson13, question2: Bound retries, space them with exponential backoff, add jitter to reduce synchronized load, then use an appropriate fallback. A tight loop worsens outage load. Answer D; correct C.

- Lesson13, question3: Awaiting a full response and collecting a local stream before returning a dictionary does not deliver live tokens to the caller. Answer C; correct D. Lesson13 initial 1/3; fresh scored three-question remediation required.

- Lesson16, question3: Attribute existence is different from truthiness. tool_calls=[] is falsey, so the router returns END. Answer B; correct A. Lesson score 2/3.

- Lesson17, question2: A small fixed pipeline without state, dialogue, roles, fanout, or approval requirements can start in plain Python; add framework machinery when requirements justify its overhead. Answer C; correct D.


## Phase pass — 2026-10-28

Lesson13 attempt2 scored 3/3; its initial 1/3 remains historical evidence. Effective total 44/51 (86.27%), initial 42/51, cumulative 45/54. All lesson minima met. Residual recall topics: JSON syntax versus schema, ReAct tool observations, Python bool/int inheritance, zero-vector guards, evaluator early returns, true streaming versus buffering, bounded retries with jitter, empty-list truthiness, and matching framework overhead to requirements. No implementation labs performed in this assessment.
