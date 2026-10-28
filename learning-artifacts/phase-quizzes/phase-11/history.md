# Phase 11 detailed quiz history

Archive: read only when an earlier question or attempt is relevant. [Phase progress](progress.md).

Initial coverage and Lesson13 remediation are complete; results are recorded below.


### p11-l01-a1-q1 — 2026-10-28

What distinguishes few-shot prompting from fine-tuning?

A) It updates model weights using a small labeled training set.

B) It adds input/output examples to the context without updating weights.

C) It retrieves training documents and permanently expands model knowledge.

D) It changes sampling settings to favor the supplied answer labels.

Learner answer: B

Correct answer: B

Result: Correct

Explanation: Few-shot prompting supplies examples in the input context; it does not update model weights.


### p11-l01-a1-q2 — 2026-10-28

A summarizer keeps returning long, general summaries. Which prompt revision most directly addresses both problems?

A) Ask for an expert persona and leave length and content unrestricted.

B) Increase temperature and ask for a more engaging summary of the article.

C) Repeat the original request and add examples of unrelated writing styles.

D) Request three one-sentence bullets, each under 20 words, focused on quantitative findings.

Learner answer: D

Correct answer: D

Result: Correct

Explanation: Explicit length, structure, and content constraints directly address verbosity and lack of focus.


### p11-l01-a1-q3 — 2026-10-28

The lesson’s scorer accepts JSON format whenever json.loads(response_text) succeeds. Its composite score averages the checks performed. Given response_text = '"hello"' and criteria = {"expected_format": "json"}, what does it report?

A) format_valid=True and composite_score=1.0, without checking object fields.

B) format_valid=False and composite_score=0.0, because the value is a string.

C) format_valid=True and composite_score=0.0, because no keywords are supplied.

D) It raises a TypeError because json.loads accepts only JSON objects.

Learner answer: B

Correct answer: A

Result: Incorrect

Explanation: A JSON string is valid JSON. The scorer checks parsing, not an object schema; its sole boolean criterion passes.


### p11-l02-a1-q1 — 2026-10-28

What distinguishes Tree-of-Thought from a single linear Chain-of-Thought?

A) It samples complete solutions and votes on their final answers.

B) It selects similar demonstrations before generating a single solution.

C) It evaluates partial reasoning branches and expands promising candidates.

D) It splits work into a fixed sequence without comparing alternatives.

Learner answer: C

Correct answer: C

Result: Correct

Explanation: Tree-of-Thought searches over candidate partial solutions, evaluates them, and expands promising branches.


### p11-l02-a1-q2 — 2026-10-28

A question-answering task needs facts available only through an external search tool. Which approach directly incorporates retrieved observations into subsequent decisions?

A) Few-shot prompting with a fixed set of labeled demonstrations.

B) ReAct with repeated action, observation, and decision steps.

C) Self-consistency with voting over answers generated without tools.

D) A longer single reasoning trace generated without external actions.

Learner answer: D

Correct answer: B

Result: Incorrect

Explanation: ReAct incorporates tool observations into the next reasoning and action decisions.


### p11-l02-a1-q3 — 2026-10-28

In the lesson voting code, five samples yield extracted answers ["24", None, "24", None, "27"]. None values are discarded before confidence is computed as winning votes / len(answers). What are the winning answer and confidence?

A) "24" and 2/5, because all requested samples form the denominator.

B) "27" and 1/3, because the last valid answer wins the vote.

C) None and 0, because any extraction failure invalidates the result.

D) "24" and 2/3, because only extracted answers form the denominator.

Learner answer: D

Correct answer: D

Result: Correct

Explanation: The code retains three parsed answers; two vote for "24". Its confidence ignores extraction failures and is not a calibrated probability of correctness.


### p11-l03-a1-q1 — 2026-10-28

What does constrained decoding do while generating a structured response?

A) It repairs invalid fields after the full response has been generated.

B) It masks tokens that would violate the supported output grammar or schema.

C) It verifies every extracted value against the original source document.

D) It repeats the prompt until several generated responses agree.

Learner answer: B

Correct answer: B

Result: Correct

Explanation: Constrained decoding restricts allowed next tokens during generation. It does not establish factual accuracy.


### p11-l03-a1-q2 — 2026-10-28

An extracted product price is a non-negative number and passes schema validation, but differs from the price in the source text. What additional check addresses this failure?

A) Check that the response parses as JSON before accepting the price.

B) Require the price field and forbid additional output properties.

C) Check the extracted price against the evidence in the source text.

D) Retry only when the extracted price has the wrong numeric type.

Learner answer: C

Correct answer: C

Result: Correct

Explanation: Schema compliance checks shape, types, and declared constraints; source-grounded checking is needed to detect an invented but correctly typed price.


### p11-l03-a1-q3 — 2026-10-28

The toy validator checks a number with isinstance(data, (int, float)), then checks minimum=0. Its integer branch explicitly rejects bool. What happens for True under these two schemas?

A) True passes the number schema but fails the integer schema.

B) True fails both schemas because booleans are never numeric in Python.

C) True passes both schemas because bool subclasses int in Python.

D) True fails the number schema but passes the integer schema.

Learner answer: B

Correct answer: A

Result: Incorrect

Explanation: In Python bool subclasses int, so the number branch accepts True and it meets minimum=0. The integer branch explicitly rejects bool; this is a toy validator limitation.


### p11-l04-a1-q1 — 2026-10-28

Why can a learned semantic embedding retrieve "transaction was declined" for the query "my payment did not go through" even when exact words differ?

A) It replaces every query word with all dictionary synonyms before matching.

B) It assigns the same vector to all documents about customer support.

C) It ranks documents solely by their length and shared punctuation.

D) It can place expressions with similar meanings close together in vector space.

Learner answer: D

Correct answer: D

Result: Correct

Explanation: Learned semantic representations can encode similarity beyond exact token overlap. The lesson’s TF-IDF toy does not itself learn synonym equivalence.


### p11-l04-a1-q2 — 2026-10-28

You need to search a large corpus quickly, then improve relevance among the retrieved candidates. Which pipeline matches the lesson?

A) Retrieve candidates with a bi-encoder, then rerank query-document pairs with a cross-encoder.

B) Run a cross-encoder over every document, then store one query-independent score per document.

C) Average all corpus vectors into one vector, then return documents in insertion order.

D) Retrieve candidates by document length, then discard the query before reranking.

Learner answer: A

Correct answer: A

Result: Correct

Explanation: Bi-encoders support precomputed document vectors for fast retrieval; cross-encoders jointly process query-document pairs for candidate reranking.


### p11-l04-a1-q3 — 2026-10-28

SimpleEmbedder ignores words outside its fitted vocabulary and leaves zero vectors unnormalized. Its cosine function returns 0.0 if either norm is zero. What happens when every query word is outside the vocabulary?

A) The embedder expands its vocabulary and relearns all document vectors.

B) The query vector stays zero and every cosine similarity score is 0.0.

C) The query receives a unit vector and matches the shortest document.

D) Cosine scoring raises ZeroDivisionError before any results are returned.

Learner answer: D

Correct answer: B

Result: Incorrect

Explanation: No known words contribute to the query vector. The zero-norm guard yields 0.0 against every indexed document, so ties do not establish semantic relevance.


### p11-l05-a1-q1 — 2026-10-28

Why does a context budget reserve space for generation before allocating input components?

A) To ensure the response has room within the model’s total token limit.

B) To guarantee that every retrieved document is factually accurate.

C) To prevent conversation history from influencing the response.

D) To convert unused input tokens into permanent model knowledge.

Learner answer: A

Correct answer: A

Result: Correct

Explanation: Input components and generated output consume the available context capacity; reserving output space avoids filling it entirely with input.


### p11-l05-a1-q2 — 2026-10-28

A coding assistant includes 50 tool definitions, mostly unrelated retrieved documents, and a long conversation history in every request. Which change best follows dynamic context assembly?

A) Always fill the entire context window with additional historical messages.

B) Remove the current query whenever the context exceeds its budget.

C) Select tools and documents for the current task and compress older history.

D) Include all tools unchanged and reduce only the response budget.

Learner answer: C

Correct answer: C

Result: Correct

Explanation: Dynamic assembly prioritizes task-relevant tools, evidence, and history while preserving output room.


### p11-l05-a1-q3 — 2026-10-28

The history compressor totals only self.turns, moves old pairs into self.summaries, and stops when len(self.turns) <= 4. get_context() includes both lists. What limitation follows?

A) It deletes all summaries before returning the final context.

B) It guarantees the assembled history always fits max_history_tokens.

C) It measures summary tokens but never measures recent turn tokens.

D) Returned context can exceed the limit because summaries are uncounted and four turns may remain oversized.

Learner answer: D

Correct answer: D

Result: Correct

Explanation: The loop’s budget excludes summaries, and its four-turn floor can retain oversized recent content. The full returned context is not guaranteed to fit the configured history limit.


### p11-l06-a1-q1 — 2026-10-28

How does RAG provide a model with application-specific knowledge at query time?

A) It updates the model weights separately for each incoming question.

B) It stores all source documents permanently inside the system prompt.

C) It retrieves relevant passages and includes them in the generation context.

D) It replaces generation with a vote over document embedding coordinates.

Learner answer: C

Correct answer: C

Result: Correct

Explanation: RAG retrieves relevant evidence and augments the model input with it; this does not require changing model weights.


### p11-l06-a1-q2 — 2026-10-28

A company refund policy changes frequently. What keeps a RAG assistant’s evidence current without retraining its language model?

A) Increase output temperature whenever an old policy is retrieved.

B) Update and re-index changed policy documents, replacing stale chunks.

C) Retain old indexed chunks and ask for longer answers about refunds.

D) Add more few-shot examples while leaving the document index untouched.

Learner answer: B

Correct answer: B

Result: Correct

Explanation: Updating the retrieval corpus and its indexed chunks makes current evidence available at query time without retraining the generator.


### p11-l06-a1-q3 — 2026-10-28

In chunk_text, start begins at 0 and advances by chunk_size - overlap on each loop iteration. For nonempty text, chunk_size=200, and overlap=200, what happens?

A) It produces one 200-word chunk and exits normally.

B) It moves backward through the text until start becomes negative.

C) It skips the first chunk and immediately returns an empty list.

D) It keeps appending the same first chunk because start never advances.

Learner answer: D

Correct answer: D

Result: Correct

Explanation: The step is zero, so start remains 0 and the loop condition stays true for nonempty text. The implementation needs validation that 0 <= overlap < chunk_size.


### p11-l07-a1-q1 — 2026-10-28

Why does Reciprocal Rank Fusion use ranking positions rather than adding raw BM25 and vector similarity scores?

A) To guarantee that every relevant document appears in the fused results.

B) To combine results without requiring the two score scales to be comparable.

C) To discard documents that appear in only one retrieval method.

D) To remove the need to rank documents within either retrieval method.

Learner answer: B

Correct answer: B

Result: Correct

Explanation: RRF sums reciprocal-rank contributions, allowing fusion across retrieval methods whose raw scores have different scales.


### p11-l07-a1-q2 — 2026-10-28

A short passage matches a query precisely but lacks surrounding conditions needed to answer it. Which strategy directly addresses this retrieval-versus-context tradeoff?

A) Search child chunks, then include their larger parent chunks in the prompt.

B) Search child chunks, then remove all surrounding text before generation.

C) Increase sampling temperature while keeping the same incomplete passage.

D) Use a hypothetical answer as verified evidence without retrieving documents.

Learner answer: A

Correct answer: A

Result: Correct

Explanation: Parent-child retrieval matches smaller passages while supplying their larger parent sections as generation context.


### p11-l07-a1-q3 — 2026-10-28

The toy evaluate_faithfulness function keeps only sentences whose stripped length is greater than 10. If none remain, it returns (1.0, []). What does it return for answer="No." with no retrieved chunks?

A) (0.0, ["No"]), because the answer has no supporting source.

B) (0.0, []), because an empty context always scores zero.

C) (1.0, []), because the short sentence is excluded before checking support.

D) It raises ValueError because the retrieved context is empty.

Learner answer: B

Correct answer: C

Result: Incorrect

Explanation: "No" has length 2 after splitting on periods, so it is filtered out. The early return gives 1.0 without checking any claim; this does not establish actual faithfulness.


### p11-l08-a1-q1 — 2026-10-28

Which description captures the core difference between LoRA and full fine-tuning?

A) LoRA freezes the base weights and trains low-rank adapter matrices.

B) LoRA changes only the prompt while leaving all parameters untrained.

C) LoRA trains every base weight but discards optimizer states after each step.

D) LoRA replaces the base model with a database of training examples.

Learner answer: A

Correct answer: A

Result: Correct

Explanation: LoRA learns a low-rank update through smaller trainable matrices while keeping the original weights frozen.


### p11-l08-a1-q2 — 2026-10-28

A square 1024-by-1024 projection receives a rank-8 LoRA adapter. Ignoring biases, how many trainable adapter parameters does this add?

A) 8,192, because only one 1024-by-8 matrix is trained.

B) 1,048,576, because the entire projection must be updated.

C) 16,384, from two matrices with 1024 times 8 parameters each.

D) 1,064,960, because both base and adapter weights are trained.

Learner answer: C

Correct answer: C

Result: Correct

Explanation: The two adapter matrices have 1024×8 and 8×1024 entries, totaling 16,384 trainable parameters; the base remains frozen.


### p11-l08-a1-q3 — 2026-10-28

LoRALayer computes (x @ A @ B) * (alpha / rank). A is random and B is all zeros at initialization. What does LinearWithLoRA return before training?

A) A random perturbation of the base output because A is random.

B) The base linear output, because the adapter contribution is zero.

C) An all-zero output, because B also zeros the frozen base path.

D) The base output multiplied by alpha / rank on both paths.

Learner answer: B

Correct answer: B

Result: Correct

Explanation: The adapter product is zero because B is zero, so adding it preserves the frozen linear layer’s original output.


### p11-l09-a1-q1 — 2026-10-28

In a function-calling interaction, who executes the requested function?

A) The model executes it internally while generating the tool-call JSON.

B) The JSON Schema executes it after checking parameter descriptions.

C) The application dispatches the model’s request to a tool implementation.

D) The tool result executes it when appended to the conversation.

Learner answer: C

Correct answer: C

Result: Correct

Explanation: The model emits a structured request; application code validates and dispatches it, then returns the tool result.


### p11-l09-a1-q2 — 2026-10-28

A weather tool reports CITY_NOT_FOUND for a misspelled city. Which handling best supports a bounded correction loop?

A) Return a structured error to the model and permit correction within a retry limit.

B) Replace the error with invented weather so the conversation can continue.

C) Return an empty response and allow unlimited retries until a call succeeds.

D) Hide the error and repeat the identical call without updating the conversation.

Learner answer: A

Correct answer: A

Result: Correct

Explanation: A structured error gives the next decision useful feedback, while a retry limit bounds execution.


### p11-l09-a1-q3 — 2026-10-28

The toy loop executes requested tools, appends their results, then reaches an unconditional break. With max_iterations=5 and a request requiring a second tool decision based on the first result, what happens?

A) It automatically completes all five decision rounds before returning.

B) It raises an error because max_iterations must equal one.

C) It recursively invokes the decision function from each tool result.

D) It exits after the first tool batch without making the dependent second decision.

Learner answer: D

Correct answer: D

Result: Correct

Explanation: The unconditional break stops the loop after one batch. A larger iteration limit does not override that control flow.


### p11-l10-a1-q1 — 2026-10-28

Why should an LLM evaluation rubric anchor each score to observable behavior?

A) It guarantees that the judge cannot make factual mistakes.

B) It removes the need for representative evaluation examples.

C) It ensures every prompt revision receives a higher score.

D) It reduces ambiguity about what each score means for the judge.

Learner answer: D

Correct answer: D

Result: Correct

Explanation: Behavioral anchors give the judge concrete criteria and reduce scoring ambiguity; calibration and representative data remain necessary.


### p11-l10-a1-q2 — 2026-10-28

A prompt change reduces hallucinations but also causes many useful answers to become refusals. Which evaluation design best exposes this tradeoff?

A) Compare only hallucination rates on five handpicked examples.

B) Score correctness and helpfulness on the same representative cases for both versions.

C) Evaluate the new prompt only on examples included in its demonstrations.

D) Replace the baseline whenever the new prompt produces one impressive response.

Learner answer: B

Correct answer: B

Result: Correct

Explanation: Before/after evaluation on shared representative cases with multiple criteria can reveal improved correctness alongside degraded helpfulness.


### p11-l10-a1-q3 — 2026-10-28

compare_eval_runs marks a criterion REGRESSION only when diff < -0.3, otherwise STABLE unless diff > 0.3. ship_decision is SHIP if there are no regressions. For diff=-0.2 on every criterion, what does it report?

A) All criteria STABLE and SHIP, without using confidence intervals in that decision.

B) All criteria REGRESSION and BLOCK, because any negative difference blocks.

C) All criteria STABLE and BLOCK, because confidence intervals are always required.

D) All criteria IMPROVED and SHIP, because a negative difference favors the new version.

Learner answer: A

Correct answer: A

Result: Correct

Explanation: The fixed threshold controls the status and deployment label. Confidence intervals are computed for reporting but do not determine the decision; SHIP does not establish statistical equivalence.


### p11-l11-a1-q1 — 2026-10-28

What distinguishes application-level semantic response caching from exact response caching?

A) Semantic caching retrains model weights, whereas exact caching changes the prompt.

B) Semantic caching matches every query to the most recent response regardless of meaning.

C) Semantic caching reuses responses for sufficiently similar queries, while exact caching matches a request key.

D) Semantic caching only stores prompt prefixes, while exact caching only stores embeddings.

Learner answer: C

Correct answer: C

Result: Correct

Explanation: Semantic response caching uses a similarity threshold to match queries, while exact caching looks up an identical request key.


### p11-l11-a1-q2 — 2026-10-28

An application logs a stop alert when spending reaches its limit but continues making paid model calls. What change makes the spending limit enforceable?

A) Add a longer alert message after each additional paid call.

B) Record the same spending under a different model name.

C) Lower response temperature while leaving all requests admitted.

D) Check budget state before paid calls and reject or serve cached responses when stopped.

Learner answer: D

Correct answer: D

Result: Correct

Explanation: A spending control must affect request admission before the paid call; merely recording an alert does not stop spending.


### p11-l11-a1-q3 — 2026-10-28

ExactCache hashes model, messages, and temperature together. A response is stored with model="gpt-4o-mini", but lookup uses model="gpt-4o" with identical messages and temperature=0.0. Both models are uncached beforehand. What happens?

A) A cache miss, because changing the model changes the request key.

B) A cache hit, because the model is ignored when messages match.

C) A cache hit, because temperature=0.0 makes all models equivalent.

D) A TypeError, because two model names cannot share one cache.

Learner answer: A

Correct answer: A

Result: Correct

Explanation: The model is part of the hashed key. The different lookup model produces a different key even with matching messages and temperature.


### p11-l12-a1-q1 — 2026-10-28

Which scenario is an indirect prompt injection?

A) A user asks an ordinary question outside the assistant’s supported topic.

B) An attacker places instructions in a retrieved document to redirect the assistant.

C) The model returns malformed JSON despite a formatting instruction.

D) A rate limiter rejects a user who exceeds the request quota.

Learner answer: B

Correct answer: B

Result: Correct

Explanation: Indirect injection delivers attacker instructions through external content processed as data, such as retrieved documents or emails.


### p11-l12-a1-q2 — 2026-10-28

An input filter passes a normal account question, but the generated response includes an email address the user is not allowed to receive. Which design directly addresses both access and delivery?

A) Trust the output because the input filter already passed the question.

B) Add a system instruction and remove all output validation checks.

C) Increase the input length limit so the model has more room to explain.

D) Enforce authorization when retrieving data and check/redact sensitive output before delivery.

Learner answer: D

Correct answer: D

Result: Correct

Explanation: Authorization limits what data can be accessed, while output checks provide another layer before delivery; input filtering alone cannot enforce either.


### p11-l12-a1-q3 — 2026-10-28

detect_injection assigns encoding_evasion confidence=0.70 and returns passed=max_confidence < 0.75. If encoding_evasion is the only detection, what result follows?

A) passed=True with confidence=0.70, because the detection remains below the blocking threshold.

B) passed=False with confidence=0.70, because any detection automatically blocks.

C) passed=True with confidence=0.0, because passing clears the detection score.

D) passed=False with confidence=1.0, because encoding detections are always certain.

Learner answer: A

Correct answer: A

Result: Correct

Explanation: The comparison 0.70 < 0.75 is True. The detection remains in the report but does not block at this threshold.


### p11-l13-a1-q1 — 2026-10-28

What is the primary user-experience benefit of streaming an LLM response as it is generated?

A) It guarantees that the complete answer requires fewer generated tokens.

B) It lets the user see initial content before the complete response is ready.

C) It removes the need to handle provider failures or output validation.

D) It guarantees that every model call finishes in less than one second.

Learner answer: B

Correct answer: B

Result: Correct

Explanation: True incremental streaming reduces time until the user sees content, even when total generation time is unchanged.


### p11-l13-a1-q2 — 2026-10-28

A provider outage causes many clients to retry simultaneously. Which recovery design reduces synchronized retries while bounding work?

A) Retry immediately forever and disable timeouts until the provider recovers.

B) Send all retries at fixed identical intervals with no attempt limit.

C) Use bounded exponential backoff with jitter, then an appropriate fallback.

D) Suppress failure logs and repeatedly resubmit the same request in a tight loop.

Learner answer: D

Correct answer: C

Result: Incorrect

Explanation: Exponential backoff spreads retries over time, jitter reduces synchronization, and retry limits plus fallback bound recovery work.


### p11-l13-a1-q3 — 2026-10-28

handle_streaming_request first awaits handle_request, which returns the complete response. It then collects every item from stream_response into a list before returning a dictionary. What does its caller receive?

A) Individual generated tokens immediately as the provider produces them.

B) An async generator that the caller can consume during the model call.

C) A response before generation finishes, followed by automatic SSE updates.

D) A final dictionary after generation and local word-by-word iteration finish.

Learner answer: C

Correct answer: D

Result: Incorrect

Explanation: This method buffers the full response and consumes the local stream internally. It does not yield tokens to its caller or provide live provider streaming.


### p11-l14-a1-q1 — 2026-10-28

Which mapping correctly distinguishes MCP server primitives?

A) Tools are callable actions; resources are URI-addressed content; prompts are reusable templates.

B) Tools are transport connections; resources are model weights; prompts are authorization tokens.

C) Tools are conversation logs; resources execute every action; prompts define network sockets.

D) Tools are user interfaces; resources are client identities; prompts store database credentials.

Learner answer: A

Correct answer: A

Result: Correct

Explanation: MCP exposes callable tools, readable URI-addressed resources, and reusable prompt templates; the host owns the AI application.


### p11-l14-a1-q2 — 2026-10-28

An MCP tool returns text containing instructions to disclose unrelated private data. How should the host handle that text?

A) Treat the instructions as authoritative because they came through MCP.

B) Grant the tool additional permissions before reading the returned text.

C) Treat it as untrusted data and enforce the host’s authorization and instruction boundaries.

D) Disable authorization checks once the server reports its name and version.

Learner answer: C

Correct answer: C

Result: Correct

Explanation: Standardized communication does not make returned content trusted or grant authority. The host and server still enforce access and action boundaries.


### p11-l14-a1-q3 — 2026-10-28

The lesson request helper begins with body_params = dict(params or {}), then sets body_params["_meta"] to a new metadata dictionary. If params is a nonempty dictionary containing an existing _meta, what happens?

A) The original params dictionary is modified in place and its metadata is deleted.

B) The returned request uses the new metadata, while the original params dictionary remains unchanged.

C) The two metadata dictionaries are automatically merged key by key.

D) The existing metadata prevents assignment and raises KeyError.

Learner answer: B

Correct answer: B

Result: Correct

Explanation: dict creates a shallow copy. Assigning a new value at the copy’s _meta key replaces that value only in the copy; it does not merge metadata or modify the original dictionary.


### p11-l15-a1-q1 — 2026-10-28

What computation does provider-side prompt caching primarily reuse?

A) The complete final answer, so every later request receives identical text.

B) The model’s training gradients from an earlier fine-tuning run.

C) A permanent update to model weights containing the conversation.

D) Previously computed prefix state, while the model still generates a response.

Learner answer: D

Correct answer: D

Result: Correct

Explanation: Prompt caching reuses computation for a matching input prefix; it is distinct from application response caching and does not store knowledge in model weights.


### p11-l15-a1-q2 — 2026-10-28

A changing timestamp precedes a long stable rubric in a prefix-cached prompt. Which layout change best preserves reuse of the rubric?

A) Place the stable rubric first and the changing timestamp after the cacheable prefix.

B) Randomize the rubric’s wording on every request to improve diversity.

C) Place a unique request ID before the rubric along with the timestamp.

D) Move the user’s changing question before every stable instruction.

Learner answer: A

Correct answer: A

Result: Correct

Explanation: Stable content should precede changing fields so an early difference does not invalidate reuse of the long shared prefix.


### p11-l15-a1-q3 — 2026-10-28

In the lesson simulator, an entry expires when now - written_at >= ttl. Reads do not update written_at. Three requests with one prefix arrive at t=0, 200, and 400 seconds with ttl=300. What are the counts?

A) One write and two reads, because every read refreshes written_at.

B) Three writes and zero reads, because timestamps always change.

C) Two writes and one read, because the last request is 400 seconds after the initial write.

D) Zero writes and three reads, because a repeated prefix never expires.

Learner answer: C

Correct answer: C

Result: Correct

Explanation: The first request writes, the second reads at age 200, and the third rewrites at age 400. The simulator does not refresh written_at on reads; this describes its code, not a universal provider TTL policy.


### p11-l16-a1-q1 — 2026-10-28

What role does a reducer play in an explicit agent state graph?

A) It decides the model’s next generated token from vocabulary logits.

B) It automatically grants approval for every side-effecting tool call.

C) It specifies how an incoming field update combines with that field’s existing state.

D) It deletes all checkpoints after every successful node execution.

Learner answer: C

Correct answer: C

Result: Correct

Explanation: A reducer defines how updates merge into existing state, such as appending a list or replacing a value.


### p11-l16-a1-q2 — 2026-10-28

A graph proposes a refund that requires human authorization. Where should an approval interrupt occur?

A) After the refund tool executes, so the reviewer can inspect the payment receipt.

B) Before the side-effecting refund tool runs, with the proposal preserved for review.

C) Only after the final answer is sent, so the user sees no delay.

D) At an unrelated logging node, while refund execution continues independently.

Learner answer: B

Correct answer: B

Result: Correct

Explanation: Approval must gate the side effect before execution; persisting the proposal allows review and a controlled resume.


### p11-l16-a1-q3 — 2026-10-28

The lesson router returns "tools" if getattr(last, "tool_calls", None) is truthy, otherwise END. If the last message has tool_calls=[], where does it route?

A) END, because an empty list is falsey.

B) "tools", because the tool_calls attribute exists.

C) Both branches, because an empty list means parallel dispatch.

D) It raises AttributeError because getattr cannot return lists.

Learner answer: B

Correct answer: A

Result: Incorrect

Explanation: The condition tests truthiness, not attribute existence. An empty list is falsey, so the router returns END.


### p11-l17-a1-q1 — 2026-10-28

What should primarily guide the choice of an agent orchestration abstraction?

A) The number of stars on the framework’s repository alone.

B) Whether its state, branching, and persistence model match the workflow’s requirements.

C) Whether it adds the most autonomous agents to every task.

D) Whether its demo uses the same model provider as your application.

Learner answer: B

Correct answer: B

Result: Correct

Explanation: The lesson emphasizes matching the workflow shape and its state, branching, durability, and cost needs to the abstraction.


### p11-l17-a1-q2 — 2026-10-28

A workflow uses two fixed model calls and one tool, with no roles, dialogue, durable state, fanout, or approval interruptions. Which starting point follows the lesson’s overhead guidance?

A) A manager agent that repeatedly assigns work to several specialist crews.

B) A multi-agent group chat with model-selected speakers at every step.

C) A durable graph runtime with custom reducers for every intermediate value.

D) A small explicit Python pipeline, adding orchestration machinery when requirements justify it.

Learner answer: C

Correct answer: D

Result: Incorrect

Explanation: For a small fixed workflow without orchestration requirements, plain Python avoids unnecessary framework overhead.


### p11-l17-a1-q3 — 2026-10-28

The recommender first returns plain python for <=2 calls if roles, dialogue, resume, fanout, and human interrupts are all false. That first check omits has_typed_state; a later branch checks it. With total_llm_calls=2, has_typed_state=True, and all other flags false, what is returned?

A) plain python, because the first matching branch returns before the typed-state branch.

B) langgraph, because the later typed-state branch overrides earlier returns.

C) crewai, because any typed state implies specialist roles.

D) agno, because two model calls automatically imply session memory.

Learner answer: A

Correct answer: A

Result: Correct

Explanation: The first condition does not inspect has_typed_state, so it succeeds and returns plain python. Later branches never execute; this reveals a limitation in the toy rule ordering.


### p11-l13-a2-q1 — 2026-10-28

What does random jitter add to an exponential-backoff retry schedule?

A) It guarantees that the provider will accept the next request.

B) It removes the need to limit the number of retries.

C) It varies retry timing across clients to reduce synchronized retry bursts.

D) It makes every client retry at exactly the same increasing intervals.

Learner answer: C

Correct answer: C

Result: Correct

Explanation: Jitter adds variation to delay timing so clients that failed together are less likely to retry together.


### p11-l13-a2-q2 — 2026-10-28

A chat endpoint waits for the full provider response, then sends its words as SSE events. Users still wait several seconds for the first word. Which change addresses that initial wait?

A) Collect the SSE events into a larger list before returning them.

B) Consume the provider’s incremental stream and forward permitted chunks as they arrive.

C) Add random delays between words after the full answer has been buffered.

D) Rename the final response dictionary to streaming_result without changing its control flow.

Learner answer: B

Correct answer: B

Result: Correct

Explanation: Reducing initial wait requires receiving and forwarding incremental provider output, with an appropriate output-checking policy. Replaying an already completed answer does not shorten generation wait.


### p11-l13-a2-q3 — 2026-10-28

The retry function loops over range(max_retries + 1). Each attempt raises ConnectionError; it retries while attempt < max_retries and otherwise re-raises. With max_retries=3, how many attempts occur before the error escapes?

A) Three attempts, because range excludes its upper bound of three.

B) Two attempts, because the first failure consumes two retry slots.

C) An unlimited number, because every exception restarts the loop.

D) Four attempts, with attempt values 0, 1, 2, and 3.

Learner answer: D

Correct answer: D

Result: Correct

Explanation: range(3 + 1) yields four attempt values. There is one initial attempt followed by up to three retries; the final failure is re-raised.
