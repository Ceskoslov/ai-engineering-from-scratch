# Phase 11 — llm-engineering Review Summary

[All phases](../progress.md)

- Status: **Done / Passed**; passed on 2026-10-28; coverage: **17 lessons**.
- Initial score: **42/51**; final effective score: **44/51 (86.27%)**.
- Cumulative responses: 54, with 45 correct; **9 initial/retake mistakes** retained. Cumulative responses include retakes and are not the mastery-score denominator.
- Pass criteria: effective phase score ≥85% and final score ≥2/3 in every lesson; all criteria met. Completion basis: quiz-based mastery; implementation labs were not performed in this assessment.

## Weak points and review priorities

- L01: valid JSON syntax does not establish object shape. L03: Python bool subclasses int and requires explicit handling in type validation. L16: an empty tool_calls list is falsey.
- L02: ReAct depends on actual tool observations. L04: a zero-vector cosine guard returning 0 does not establish relevance. L07: an evaluator may return 1.0 early because no sentences qualify for evaluation, without establishing evidence support.
- L13: bound retries with backoff and jitter. True streaming delivers incremental output to the caller; collecting a full response before returning is buffering. The retake reached 3/3, but retain these concepts for recall. L17: match framework complexity to actual state and collaboration requirements.

## Lessons with mistakes and retake outcomes

Lessons with mistakes or retakes are listed below, along with any additional rows retained from the original ledger. Unlisted lessons scored 3/3 initially and finally. A final 3/3 indicates correction in a later assessment where applicable; retain those topics for spaced recall. Lessons at 2/3 remain review priorities.

| Lesson | Initial score | Final effective score / retake |
|---|---|---|
| [Prompt Engineering: Techniques & Patterns](../../../phases/11-llm-engineering/01-prompt-engineering/docs/en.md) | 2/3 | 2/3 |
| [Few-Shot, Chain-of-Thought, Tree-of-Thought](../../../phases/11-llm-engineering/02-few-shot-cot/docs/en.md) | 2/3 | 2/3 |
| [Structured Outputs: JSON, Schema Validation, Constrained Decoding](../../../phases/11-llm-engineering/03-structured-outputs/docs/en.md) | 2/3 | 2/3 |
| [Embeddings & Vector Representations](../../../phases/11-llm-engineering/04-embeddings/docs/en.md) | 2/3 | 2/3 |
| [Advanced RAG (Chunking, Reranking, Hybrid Search)](../../../phases/11-llm-engineering/07-advanced-rag/docs/en.md) | 2/3 | 2/3 |
| [Building a Production LLM Application](../../../phases/11-llm-engineering/13-production-app/docs/en.md) | 1/3 | 3/3 |
| [Agent State Machines — Graphs, Nodes, Checkpoints](../../../phases/11-llm-engineering/16-langgraph-state-machines/docs/en.md) | 2/3 | 2/3 |
| [Agent Framework Tradeoffs — Graph, Role, and Actor Orchestration](../../../phases/11-llm-engineering/17-agent-framework-tradeoffs/docs/en.md) | 2/3 | 2/3 |

## Condensed mistake records

Question IDs, prompts, selected wrong answers, correct answers, and explanations are retained. Other distractors, correct-only questions, and per-response score logs are omitted. Prompts and explanations retain their original English wording. These are historical initial/retake mistakes, not pending retake requirements.

### p11-l01-a1-q3

The lesson’s scorer accepts JSON format whenever json.loads(response_text) succeeds. Its composite score averages the checks performed. Given response_text = '"hello"' and criteria = {"expected_format": "json"}, what does it report?

- Learner answer: B — format_valid=False and composite_score=0.0, because the value is a string.
- Correct answer: A — format_valid=True and composite_score=1.0, without checking object fields.
- Explanation: A JSON string is valid JSON. The scorer checks parsing, not an object schema; its sole boolean criterion passes.

### p11-l02-a1-q2

A question-answering task needs facts available only through an external search tool. Which approach directly incorporates retrieved observations into subsequent decisions?

- Learner answer: D — A longer single reasoning trace generated without external actions.
- Correct answer: B — ReAct with repeated action, observation, and decision steps.
- Explanation: ReAct incorporates tool observations into the next reasoning and action decisions.

### p11-l03-a1-q3

The toy validator checks a number with isinstance(data, (int, float)), then checks minimum=0. Its integer branch explicitly rejects bool. What happens for True under these two schemas?

- Learner answer: B — True fails both schemas because booleans are never numeric in Python.
- Correct answer: A — True passes the number schema but fails the integer schema.
- Explanation: In Python bool subclasses int, so the number branch accepts True and it meets minimum=0. The integer branch explicitly rejects bool; this is a toy validator limitation.

### p11-l04-a1-q3

SimpleEmbedder ignores words outside its fitted vocabulary and leaves zero vectors unnormalized. Its cosine function returns 0.0 if either norm is zero. What happens when every query word is outside the vocabulary?

- Learner answer: D — Cosine scoring raises ZeroDivisionError before any results are returned.
- Correct answer: B — The query vector stays zero and every cosine similarity score is 0.0.
- Explanation: No known words contribute to the query vector. The zero-norm guard yields 0.0 against every indexed document, so ties do not establish semantic relevance.

### p11-l07-a1-q3

The toy evaluate_faithfulness function keeps only sentences whose stripped length is greater than 10. If none remain, it returns (1.0, []). What does it return for answer="No." with no retrieved chunks?

- Learner answer: B — (0.0, []), because an empty context always scores zero.
- Correct answer: C — (1.0, []), because the short sentence is excluded before checking support.
- Explanation: "No" has length 2 after splitting on periods, so it is filtered out. The early return gives 1.0 without checking any claim; this does not establish actual faithfulness.

### p11-l13-a1-q2

A provider outage causes many clients to retry simultaneously. Which recovery design reduces synchronized retries while bounding work?

- Learner answer: D — Suppress failure logs and repeatedly resubmit the same request in a tight loop.
- Correct answer: C — Use bounded exponential backoff with jitter, then an appropriate fallback.
- Explanation: Exponential backoff spreads retries over time, jitter reduces synchronization, and retry limits plus fallback bound recovery work.

### p11-l13-a1-q3

handle_streaming_request first awaits handle_request, which returns the complete response. It then collects every item from stream_response into a list before returning a dictionary. What does its caller receive?

- Learner answer: C — A response before generation finishes, followed by automatic SSE updates.
- Correct answer: D — A final dictionary after generation and local word-by-word iteration finish.
- Explanation: This method buffers the full response and consumes the local stream internally. It does not yield tokens to its caller or provide live provider streaming.

### p11-l16-a1-q3

The lesson router returns "tools" if getattr(last, "tool_calls", None) is truthy, otherwise END. If the last message has tool_calls=[], where does it route?

- Learner answer: B — "tools", because the tool_calls attribute exists.
- Correct answer: A — END, because an empty list is falsey.
- Explanation: The condition tests truthiness, not attribute existence. An empty list is falsey, so the router returns END.

### p11-l17-a1-q2

A workflow uses two fixed model calls and one tool, with no roles, dialogue, durable state, fanout, or approval interruptions. Which starting point follows the lesson’s overhead guidance?

- Learner answer: C — A durable graph runtime with custom reducers for every intermediate value.
- Correct answer: D — A small explicit Python pipeline, adding orchestration machinery when requirements justify it.
- Explanation: For a small fixed workflow without orchestration requirements, plain Python avoids unnecessary framework overhead.
