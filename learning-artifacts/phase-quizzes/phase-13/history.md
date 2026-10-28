# Phase 13 detailed quiz history

Archive: read only when an earlier question or attempt is relevant. [Phase progress](progress.md).

No questions presented yet.

### p13-l01-a1-q1 — 2026-10-28

In the describe → decide → execute → observe loop, what happens after the model emits a structured tool call?

A) The model runs the executor and updates external state directly.
B) The host validates arguments, runs the executor, and returns its result to the model.
C) The host treats the call arguments as the completed tool result.
D) The model treats the tool description as evidence that the action succeeded.

Learner answer: B
Correct answer: B
Result: correct
Explanation: A tool call requests an action. The host validates and executes it, then supplies the result so the model can observe it.

### p13-l01-a1-q2 — 2026-10-28

Two independent tool calls finish in the reverse order from which they were requested. How should the host associate each result with its request?

A) Match each result to the earliest request without a result.
B) Match each result using only the tool name.
C) Match each result using its corresponding call ID.
D) Match each result using its position in the completion list.

Learner answer: c (C)
Correct answer: C
Result: correct
Explanation: Call IDs correlate results with specific requests even when execution finishes out of order or the same tool is called twice.

### p13-l01-a1-q3 — 2026-10-28

In run_loop, a selected tool has consequential=True. The code prints "GATE : tool is consequential, would confirm" and then calls tool.executor. What does this actually enforce?

A) It reports the classification but still executes without obtaining confirmation.
B) It pauses execution until the user explicitly approves the call.
C) It rejects consequential tools before their executors can run.
D) It runs the executor only against a read-only copy of external state.

Learner answer: a (A)
Correct answer: A
Result: correct
Explanation: Printing a gate message does not enforce approval. This implementation proceeds directly to tool.executor.

### p13-l02-a1-q1 — 2026-10-28

Why does this lesson use a canonical Tool and Call representation with provider-specific translators at the edges?

A) To make every provider accept exactly the same request JSON.
B) To let normalized tool calls bypass host-side argument validation.
C) To execute tools inside the provider instead of the host program.
D) To keep shared logic independent of provider envelopes and argument encodings.

Learner answer: D
Correct answer: D
Result: correct
Explanation: Adapters translate provider-specific fields, nesting, and argument encodings while shared application logic uses canonical representations.

### p13-l02-a1-q2 — 2026-10-28

In the lesson’s offline translator, you must force get_weather when several tools are available. Which Gemini configuration does tool_choice_gemini emit?

A) mode AUTO with allowed_function_names set to get_weather.
B) mode ANY with allowed_function_names set to get_weather.
C) mode ANY without restricting allowed_function_names.
D) mode NONE with allowed_function_names set to get_weather.

Learner answer: B
Correct answer: B
Result: correct
Explanation: The force branch combines mode ANY with allowed_function_names containing only the selected tool name.

### p13-l02-a1-q3 — 2026-10-28

In the supplied parse_openai function, function.arguments is changed from a JSON string to an already-parsed Python dict. What happens at json.loads(fn["arguments"])?

A) It raises TypeError because json.loads does not accept a dict.
B) It returns the same dict because decoding is idempotent.
C) It converts the dict to a JSON string for Call.args.
D) It skips the call because its arguments were already decoded.

Learner answer: A
Correct answer: A
Result: correct
Explanation: json.loads expects a string, bytes, or bytearray. This parser assumes the fixture’s string-encoded arguments and does not handle a dict.

### p13-l03-a1-q1 — 2026-10-28

Why should a host keep separate argument buffers for interleaved streamed tool calls and wait for each call’s completion signal before parsing?

A) To sort all calls alphabetically before any executor can run.
B) To combine all argument fragments into one shared JSON object.
C) To avoid mixing different calls or parsing incomplete JSON.
D) To ensure every call finishes execution in its request order.

Learner answer: C
Correct answer: C
Result: correct
Explanation: Separate buffers preserve call identity, and completion signals prevent attempts to decode incomplete argument JSON.

### p13-l03-a1-q2 — 2026-10-28

A create_record call returns the ID needed by update_record. How should the host schedule these two calls?

A) Run both concurrently and match their results by call ID.
B) Finish create_record, then supply its ID to update_record.
C) Start update_record first so it can wait for any new record.
D) Run both concurrently using the tool name as a shared key.

Learner answer: B
Correct answer: B
Result: correct
Explanation: The second call depends on the first call’s output. Correlation IDs do not remove this data dependency.

### p13-l03-a1-q3 — 2026-10-28

A CallBuffer contains args_buf='{"city":"Tokyo"}' but done=False. What does its try_parse() method return?

A) The dictionary {"city": "Tokyo"}, because the JSON is complete.
B) A JSONDecodeError, because no call_stop event has arrived.
C) The unchanged string, because parsing has not been enabled.
D) None, because the done check occurs before json.loads.

Learner answer: D
Correct answer: D
Result: correct
Explanation: try_parse returns None immediately while done is False, even if args_buf happens to contain valid JSON.

### p13-l04-a1-q1 — 2026-10-28

What distinguishes constrained decoding from validating an output after generation?

A) It checks the completed output and repairs any invalid fields.
B) It masks disallowed next tokens while the output is generated.
C) It adds instructions asking the model to avoid invalid JSON.
D) It retries generation until a completed output passes validation.

Learner answer: B
Correct answer: B
Result: correct
Explanation: Constrained decoding restricts token selection during generation. Post-generation validation checks output only after it has been produced.

### p13-l04-a1-q2 — 2026-10-28

An extraction output is valid JSON, but total_usd is -5 while its schema requires minimum: 0. How should the lesson’s handler classify it?

A) parse_error, because negative numbers are not valid JSON.
B) refusal, because the model supplied an unacceptable value.
C) violation, because parsed data fails a schema constraint.
D) ok, because successful JSON parsing establishes validity.

Learner answer: B
Correct answer: C
Result: incorrect
Explanation: The JSON parses successfully, but the negative value fails the minimum constraint, making it a schema violation.

### p13-l04-a1-q3 — 2026-10-28

In process_model_output, raw is "__REFUSAL__ Not an invoice." What kind, payload, and errors does it return?

A) kind="refusal", payload="Not an invoice.", errors=[].
B) kind="parse_error", payload=None, with a JSON parsing error.
C) kind="violation", payload="Not an invoice.", with missing-field errors.
D) kind="ok", payload="__REFUSAL__ Not an invoice.", errors=[].

Learner answer: A
Correct answer: A
Result: correct
Explanation: The refusal-prefix branch returns before json.loads or schema validation and strips the prefix and surrounding whitespace.

### p13-l05-a1-q1 — 2026-10-28

Why include both “Use when…” and “Do not use for…” in a tool description?

A) To make the description replace the argument schema.
B) To grant the tool permission to act without host checks.
C) To guarantee the model always selects that tool.
D) To distinguish intended use from similar but unsuitable cases.

Learner answer: D
Correct answer: D
Result: correct
Explanation: Positive usage guidance identifies suitable requests, while exclusions disambiguate nearby tools and use cases.

### p13-l05-a1-q2 — 2026-10-28

A units parameter accepts only celsius or fahrenheit. Which schema best expresses this closed set?

A) {"type":"string","enum":["celsius","fahrenheit"]}
B) {"type":"string","description":"Any temperature unit"}
C) {"type":"object","additionalProperties":true}
D) {"type":"string","minLength":1}

Learner answer: A
Correct answer: A
Result: correct
Explanation: A string enum explicitly restricts the parameter to the two accepted values.

### p13-l05-a1-q3 — 2026-10-28

lint_registry iterates over names and appends a duplicate-name finding whenever names.count(n)>1. If two otherwise valid tools share the same name, how many duplicate-name findings does it append?

A) Zero, because the later tool overwrites the earlier one.
B) One, because repeated names are deduplicated first.
C) Two, because each occurrence triggers the condition.
D) Four, because it compares every tool against every tool.

Learner answer: C
Correct answer: C
Result: correct
Explanation: The loop visits both occurrences, and names.count(n) is 2 each time, so it appends two findings.

### p13-l06-a1-q1 — 2026-10-28

In this lesson’s stateless request model, why must each request carry its own protocol version and client capabilities?

A) So the server can interpret the request without inheriting another request’s context.
B) So the client can use its capability declaration as proof of authorization.
C) So the server can create a persistent protocol session for each request ID.
D) So later requests can omit metadata after the first successful operation.

Learner answer: A
Correct answer: A
Result: correct
Explanation: Per-request metadata makes each request independently interpretable and prevents context from leaking between clients or requests.

### p13-l06-a1-q2 — 2026-10-28

In this lesson’s model, a clientInfo object claims name="trusted-admin". How should the server treat that name when authorizing a sensitive operation?

A) Grant admin access because clientInfo is carried in request metadata.
B) Reuse permissions from the last request with the same displayed name.
C) Treat it as display/debugging data and verify authorization separately.
D) Accept the name as a credential if its version field is also a string.

Learner answer: C
Correct answer: C
Result: correct
Explanation: Client identity metadata is self-reported display/debugging data. It is not a security credential.

### p13-l06-a1-q3 — 2026-10-28

In the supplied dispatcher, a valid tools/list request is followed by another supported-version request with clientCapabilities removed from params._meta. What does the second dispatch return?

A) A successful list using capabilities remembered from the first request.
B) A JSON-RPC error with code -32602 for the missing capability object.
C) A JSON-RPC error with code -32022 for an unsupported version.
D) No response, because missing capabilities makes it a notification.

Learner answer: B
Correct answer: B
Result: correct
Explanation: validate_request requires clientCapabilities to be a dict on each request and returns -32602 when it is absent. The dispatcher does not reuse previous metadata.

### p13-l07-a1-q1 — 2026-10-28

Why should a newline-delimited JSON-RPC server send diagnostic logs to stderr rather than stdout?

A) Because stderr automatically turns log messages into JSON-RPC notifications.
B) Because stdout is reserved for requests and stderr for responses.
C) Because ordinary log lines on stdout can corrupt the protocol message stream.
D) Because stderr guarantees that log messages cannot contain sensitive data.

Learner answer: C
Correct answer: C
Result: correct
Explanation: The client reads stdout as protocol messages. Ordinary diagnostic text can break parsing; stderr keeps it outside that message stream.

### p13-l07-a1-q2 — 2026-10-28

A resource response contains one user’s private note body. Which cache policy fits the lesson’s guidance?

A) Mark it public so any authenticated client can reuse it.
B) Mark it private and prevent reuse across authorization contexts.
C) Mark it public if its URI and list ordering are deterministic.
D) Omit cacheScope because a short TTL establishes user isolation.

Learner answer: B
Correct answer: B
Result: correct
Explanation: User-specific data requires private caching scoped to the appropriate authorization context. A TTL does not establish access isolation.

### p13-l07-a1-q3 — 2026-10-28

With valid request metadata, tools/call invokes notes_search with arguments={"query":""}. Its executor raises ValueError. How does handle_tools_call return this failure?

A) A complete result with isError=True and the error message in content.
B) A JSON-RPC error with code -32603 because all executor exceptions escape.
C) A successful result with isError=False and an empty list of search hits.
D) No response because an empty query changes the request into a notification.

Learner answer: A
Correct answer: A
Result: correct
Explanation: handle_tools_call catches ValueError from the executor and wraps its message in content with isError=True using complete().

### p13-l08-a1-q1 — 2026-10-28

In this lesson’s dual-era client, why is a discovery timeout insufficient evidence to select legacy behavior?

A) Because timeouts prove the peer supports modern request metadata.
B) Because every legacy server must respond to discovery successfully.
C) Because a timeout means initialization has already completed.
D) Because overload or transport failure can produce the same signal.

Learner answer: D
Correct answer: D
Result: correct
Explanation: A timeout is ambiguous. Legacy selection requires explicit permission to probe plus a valid positive initialize result for a supported legacy revision.

### p13-l08-a1-q2 — 2026-10-28

An allowlisted peer returns the recognized modern error -32022 with a mutually supported version. What should the lesson’s client do next?

A) Send initialize because the legacy allowlist overrides the error.
B) Retry modern discovery using that version and a new request ID.
C) Resend the identical request with the same unsupported version.
D) Select legacy behavior immediately without a positive probe result.

Learner answer: B
Correct answer: B
Result: correct
Explanation: A recognized modern version error proves modern behavior. The client selects a mutual modern version and retries with a new ID; it does not downgrade.

### p13-l08-a1-q3 — 2026-10-28

Both files and notes advertise search, and merge() uses its default policy. With peers processed alphabetically, what does call("notes/search", {}) send?

A) A tools/call to files with name="notes/search".
B) A tools/call to notes with name="notes/search".
C) A tools/call to notes with name="search".
D) A tools/call to both peers with name="search".

Learner answer: A
Correct answer: C
Result: incorrect
Explanation: The merged registry stores notes/search as the canonical name with peer_name notes and local_name search. call routes to the owning peer using the local name.

### p13-l09-a1-q1 — 2026-10-28

Why does the lesson’s HTTP server compare mirrored method and name headers with the JSON-RPC body before executing a request?

A) To let routing headers override any conflicting body fields.
B) To ensure routing or policy checks and execution refer to the same operation.
C) To authenticate the client using its chosen tool name.
D) To recover missing arguments from an earlier connection.

Learner answer: B
Correct answer: B
Result: correct
Explanation: Header-body equality prevents a gateway from checking one operation while the server executes another.

### p13-l09-a1-q2 — 2026-10-28

A draft created on replica 1 must remain available when the next request reaches replica 2. Which design fits the lesson’s stateless transport model?

A) Keep the draft only in replica 1 and depend on sticky routing.
B) Use the next JSON-RPC request ID as the draft’s persistent identity.
C) Store the draft only in the current HTTP response stream.
D) Return an explicit draft handle backed by shared storage and authorize each use.

Learner answer: D
Correct answer: D
Result: correct
Explanation: Durable application state needs explicit identity and shared persistence so any replica can load it; each use must still be authorized.

### p13-l09-a1-q3 — 2026-10-28

In do_POST, the body’s version is unsupported and differs from MCP-Protocol-Version. Other structure and headers are valid. Which check fails first?

A) validate_http_headers raises -32020 before supported-version validation.
B) validate_supported_version raises -32022 before header comparison.
C) dispatch returns -32601 because the method is never inspected.
D) The server accepts the header version and overwrites the body version.

Learner answer: A
Correct answer: A
Result: correct
Explanation: do_POST validates structure, compares headers, then checks whether the matched version is supported. A version mismatch therefore raises -32020 first.

### p13-l10-a1-q1 — 2026-10-28

Which mapping best matches MCP primitives to consumer intent in this lesson?

A) Tool: read a URI; resource: start a template; prompt: mutate state.
B) Tool: start a template; resource: mutate state; prompt: read a URI.
C) Tool: perform an operation; resource: read URI-addressed content; prompt: start a user-selected message workflow.
D) Tool: store policy; resource: override host instructions; prompt: authorize operations.

Learner answer: C
Correct answer: C
Result: correct
Explanation: Tools expose operations, resources expose addressable content, and prompts package reusable message workflows chosen by users.

### p13-l10-a1-q2 — 2026-10-28

A client receives a resource-updated notification for notes://note-1. What should it do to obtain the current content?

A) Read the URI again through resources/read under current authorization.
B) Treat the notification as the complete replacement document.
C) Reuse the subscription ID as proof of permission to read the note.
D) Assume all cached note bodies now contain the updated text.

Learner answer: A
Correct answer: A
Result: correct
Explanation: An update notification identifies changed content; the client must read it again and remain subject to current authorization.

### p13-l10-a1-q3 — 2026-10-28

A SubscriptionStream has notifications={"resourcesListChanged": True} and no resourceSubscriptions entry. What does resource_updated("notes://note-1") return?

A) An update event because any resource-related subscription allows it.
B) A complete result that includes the note body.
C) A JSON-RPC error with code -32602 for the absent URI filter.
D) None because that URI is not in resourceSubscriptions.

Learner answer: C
Correct answer: D
Result: incorrect
Explanation: resource_updated checks membership in resourceSubscriptions, defaulting to an empty list. resourcesListChanged enables a separate notification category.

### p13-l11-a1-q1 — 2026-10-28

In this lesson’s MRTR workflow, how does a server obtain required client input without sending an independent request to the client?

A) It stores a callback in the HTTP connection and invokes it later.
B) It returns input_required with embedded input requests; the client fulfills them and retries the original operation.
C) It changes the original request ID into a persistent protocol session ID.
D) It treats the client’s capability declaration as the completed input response.

Learner answer: B
Correct answer: B
Result: correct
Explanation: MRTR expresses missing input as a result. The client obtains the requested input and makes a new independent request repeating the original operation with inputResponses and requestState.

### p13-l11-a1-q2 — 2026-10-28

The lesson seals requestState with HMAC. A valid token was issued for one principal and one set of arguments. Why must the server still check those bindings on retry?

A) Because HMAC automatically expires all tokens at the next request.
B) Because the client must be allowed to replace the token’s principal.
C) Because a valid signature alone does not prevent reuse in the wrong request context.
D) Because HMAC encrypts arguments but leaves principal names unsigned.

Learner answer: C
Correct answer: C
Result: correct
Explanation: Integrity proves the state was not altered, but principal, method, argument digest, and expiry checks restrict where and when an unchanged token may be accepted.

### p13-l11-a1-q3 — 2026-10-28

In run_mrtr(), the loop continues while resultType is input_required, increments request_id each round, and has no round counter. What happens if a modified server always returns a fulfillable input_required result?

A) It stops after three rounds because request_id enforces a budget.
B) It rejects the fourth response because all tokens expire after three requests.
C) It exits after the first input response because the request ID changes.
D) It keeps retrying because the loop has no explicit round limit.

Learner answer: B
Correct answer: D
Result: incorrect
Explanation: The demo’s normal state machine finishes, but run_mrtr itself has no enforced round budget. Incrementing IDs provides correlation, not a stopping condition.

### p13-l12-a1-q1 — 2026-10-28

A client supplies workspaceUri for a file operation. What does that argument establish by itself?

A) The caller is authorized to access every path under that URI.
B) The operating system prevents the server from leaving that workspace.
C) The server can skip path normalization because the scope is explicit.
D) The requested scope is visible, but authorization and containment still need enforcement.

Learner answer: D
Correct answer: D
Result: correct
Explanation: Explicit scope identifies what the caller wants to target. It is not permission or a sandbox; the server must authorize the workspace and enforce containment.

### p13-l12-a1-q2 — 2026-10-28

Two server instances may receive the same valid signed deletion confirmation before it expires. What prevents both from executing it?

A) Use a shared replay store to atomically consume a nonce with the mutation.
B) Issue a different JSON-RPC ID for each retry and trust the HMAC.
C) Encode the candidate list with Base64 instead of JSON.
D) Keep a separate consumed-nonce set in each server instance.

Learner answer: A
Correct answer: A
Result: correct
Explanation: A signature does not stop replay of an unchanged token. Shared atomic nonce consumption coupled to the mutation prevents both instances from accepting the same confirmation.

### p13-l12-a1-q3 — 2026-10-28

In NotesServer.tools_call, a valid confirmation state receives action="cancel". What happens to the note and the replay nonce?

A) The note is deleted and the nonce is consumed.
B) The note is preserved but the nonce is consumed as a terminal refusal.
C) The note is preserved and the nonce remains unconsumed until expiry.
D) The server raises -32602 because cancel is not a valid action.

Learner answer: C
Correct answer: C
Result: correct
Explanation: The cancel branch returns deleted=False before calling the replay store. Decline consumes the nonce without deletion; cancel does not.

### p13-l13-a1-q1 — 2026-10-28

In this lesson, tasks/get returns resultType="complete" with status="working". What does that mean?

A) The polling RPC finished, while the represented job is still running.
B) The job finished, but its final result has not been downloaded.
C) The response is invalid because complete requires status completed.
D) The task has become a persistent protocol session.

Learner answer: A
Correct answer: A
Result: correct
Explanation: The outer resultType describes completion of the tasks/get RPC; status describes the durable job’s separate lifecycle.

### p13-l13-a1-q2 — 2026-10-28

An already-created task pauses with status="input_required" and an approve_outline input request. How does the client submit the answer in this lesson’s task flow?

A) Retry the original tools/call without its taskId.
B) Send a server-initiated elicitation request back to the worker.
C) Call tasks/result with the approval embedded in headers.
D) Call tasks/update with the taskId and keyed inputResponses.

Learner answer: D
Correct answer: D
Result: correct
Explanation: Input after task creation is submitted through tasks/update for that durable task. Retrying the original tool call is the pre-task core MRTR pattern.

### p13-l13-a1-q3 — 2026-10-28

A task has status="completed". The supplied tasks_cancel method changes status only when it is outside TERMINAL_STATUSES={"completed","cancelled","failed"}. What happens when it is called for this task with valid ownership and capabilities?

A) It changes the status to cancelled and deletes the completed result.
B) It preserves completed and returns an empty complete acknowledgement.
C) It raises -32602 because completed tasks cannot be looked up.
D) It restarts the worker so cancellation can be applied.

Learner answer: B
Correct answer: B
Result: correct
Explanation: Completed is terminal, so the mutation block is skipped and tasks_cancel returns complete() without changing the result.

### p13-l14-a1-q1 — 2026-10-28

In this lesson, what does the Apps bridge’s ui/initialize exchange establish?

A) A core MCP protocol session shared by every later server request.
B) An authorization grant allowing the iframe to approve its own actions.
C) A local iframe-to-host bridge, separate from MCP core request handling.
D) A server-side cache that replaces per-request client capabilities.

Learner answer: C
Correct answer: C
Result: correct
Explanation: ui/initialize belongs to the iframe postMessage dialect. Core MCP requests remain independently described and authorized.

### p13-l14-a1-q2 — 2026-10-28

An App’s permission to perform a privileged action is revoked while its iframe remains open. What should the host do when the App requests that action?

A) Honor the request because permission existed during ui/initialize.
B) Recheck current authorization and reject the revoked action.
C) Let the iframe decide whether its earlier consent still applies.
D) Permit the action if the request uses the expected postMessage origin.

Learner answer: B
Correct answer: B
Result: correct
Explanation: Capabilities and authorization must be checked at action time. Bridge initialization and origin checks do not preserve revoked authority.

### p13-l14-a1-q3 — 2026-10-28

In McpAppServer.handle, a valid tools/list request has apps=False. What happens to the notes_timeline tool?

A) It remains listed, but the conditional _meta.ui binding is omitted.
B) It is removed from the tools list because an iframe is required.
C) The server returns -32021 before listing any tools.
D) The server lists it with the same UI binding despite missing capability.

Learner answer: D
Correct answer: A
Result: incorrect
Explanation: The handler always builds the tool descriptor and adds _meta.ui only when _apps_enabled(meta) is true, preserving the text-capable tool.

### p13-l15-a1-q1 — 2026-10-28

What does matching a tool descriptor to its previously approved hash establish?

A) The descriptor cannot contain malicious instructions.
B) The server’s display name is an authenticated publisher identity.
C) The descriptor has stayed unchanged, while its safety still depends on review.
D) The executor automatically enforces the permissions described in its annotations.

Learner answer: C
Correct answer: C
Result: correct
Explanation: Hash equality proves stability of the pinned bytes, not that the original descriptor was safe or that its claims are enforced.

### p13-l15-a1-q2 — 2026-10-28

An approved tool keeps its name and description but changes inputSchema. Which admission control detects this change?

A) Pin and compare a canonical digest of the complete descriptor.
B) Scan only the description for known injection phrases.
C) Trust the tool because its qualified name is unchanged.
D) Use clientInfo.version as permission to accept schema changes.

Learner answer: D
Correct answer: A
Result: incorrect
Explanation: Whole-descriptor pinning includes the schema. A description-only scan or hash misses changes to other fields.

### p13-l15-a1-q3 — 2026-10-28

In SecurityGateway.handle, _visible_tools scans descriptors for tools/list, but the tools/call branch routes directly by params.name. After notes.search is changed and hidden from the list, what does a direct valid tools/call to notes.search do?

A) It fails the approved-digest check before reaching the handler.
B) It returns the hard-coded search result because dispatch does not rescan the descriptor.
C) It automatically updates the approved hash before executing search.
D) It returns method-not-found because hidden tools are removed from the method table.

Learner answer: A
Correct answer: B
Result: incorrect
Explanation: The sample checks visibility during listing, but the direct call branch still matches notes.search and returns its fixed result. Discovery filtering alone does not enforce admission at dispatch.

### p13-l16-a1-q1 — 2026-10-28

Why does this lesson store access tokens under both issuer and resource rather than resource alone?

A) To let all resources share a token whenever the user is the same.
B) To replace server-side audience validation with a client cache key.
C) To allow an issuer’s refresh token to enroll clients at another issuer.
D) To keep tokens tied to the authorization server and intended protected service.

Learner answer: D
Correct answer: D
Result: correct
Explanation: Issuer and resource identify who issued the token and where it is intended to be used. Their binding prevents cross-issuer or cross-resource token confusion.

### p13-l16-a1-q2 — 2026-10-28

The client holds a token for the MCP notes service, which must call a downstream API. How should it authenticate to that downstream API?

A) Forward the notes-service token because the user already consented.
B) Obtain a separate token for the downstream audience or use explicit token exchange.
C) Put the notes-service token in the downstream URL for routing.
D) Change the token’s audience field locally before forwarding it.

Learner answer: B
Correct answer: B
Result: correct
Explanation: A token intended for the MCP resource must not be passed through to a different audience. Use an appropriately issued downstream credential.

### p13-l16-a1-q3 — 2026-10-28

In Client.authorize, the expected issuer is "https://auth.example.com", but response["iss"] is "https://auth.example.com/". What happens before auth.exchange is called?

A) The client strips the trailing slash and exchanges the code.
B) The client stores the token under both issuer spellings.
C) The exact comparison fails and raises ValueError.
D) The client ignores iss because the response contains a code.

Learner answer: C
Correct answer: C
Result: correct
Explanation: The code compares the issuer strings exactly and raises on mismatch before exchanging the authorization code.

### p13-l17-a1-q1 — 2026-10-28

Why must an admitted, descriptor-pinned backend still undergo policy checks for every live call?

A) Because a stable descriptor proves the user has current authorization.
B) Because admission evidence automatically expires after each request.
C) Because registry publication grants access only after discovery succeeds.
D) Because current roles, arguments, backend health, and approvals can change independently of admission.

Learner answer: D
Correct answer: D
Result: correct
Explanation: Admission establishes which backend may be used, not whether this principal may perform this operation now. Runtime policy evaluates current request conditions.

### p13-l17-a1-q2 — 2026-10-28

A gateway computes tools/list differently for different users. Which caching approach preserves that visibility boundary?

A) Use private cache scope and include the authorization context in the cache key.
B) Use public cache scope whenever tool names are deterministically sorted.
C) Cache one shared list because all backends passed admission.
D) Key the list only by the URL and rely on a short TTL.

Learner answer: A
Correct answer: A
Result: correct
Explanation: Principal-dependent visibility requires private caching scoped to authorization context. Stable sorting and short TTLs do not prevent cross-user reuse.

### p13-l17-a1-q3 — 2026-10-28

In Gateway.handle, RBAC allows a direct tool call and its rate bucket has capacity, but the live descriptor digest differs from its pin. What happens before _forward?

A) The gateway refreshes the pin automatically and forwards the call.
B) It forwards because RBAC approval overrides descriptor changes.
C) It records pin_mismatch and returns HTTP 409 with error -32010.
D) It removes only the list entry and forwards the direct call.

Learner answer: A
Correct answer: C
Result: incorrect
Explanation: The call path checks _is_pinned before _forward. A mismatch is audited and returns HTTP 409 with a Descriptor changed JSON-RPC error.

### p13-l18-a1-q1 — 2026-10-28

What distinguishes signing-key rotation from JWKS refresh in this lesson?

A) The resource server rotates private keys; the authorization server refreshes its token cache.
B) Both actions mint a new signing key whenever a token has an unknown kid.
C) Rotation changes issuer keys; refresh fetches the published key set into the resource server’s cache.
D) Refresh extends token expiry; rotation changes the token’s intended audience.

Learner answer: C
Correct answer: C
Result: correct
Explanation: The authorization server creates and retires signing keys. The resource server fetches their published set for verification; it does not create issuer keys.

### p13-l18-a1-q2 — 2026-10-28

An opaque-token introspection service is unavailable during a protected tool call. Which behavior matches the lesson’s declared failure policy?

A) Fail closed and report the dependency failure without executing the tool.
B) Treat the token as active if its string has the expected prefix.
C) Decode the opaque token locally and trust any recovered fields.
D) Skip authorization temporarily and record the outage afterward.

Learner answer: A
Correct answer: A
Result: correct
Explanation: Introspection failure cannot establish active status or authorization. Protected calls must fail closed rather than turn network failure into access.

### p13-l18-a1-q3 — 2026-10-28

ResourceServer.validate decodes a well-formed token whose iss is not in allowed_issuers. According to the supplied code, what happens before any JWKS lookup?

A) It refreshes JWKS for the token-supplied issuer and then checks trust.
B) It accepts the issuer if the audience matches this resource.
C) It selects a trusted issuer with the same key ID and verifies there.
D) It returns valid=False with HTTP401 and "iss not allowed" without refreshing JWKS.

Learner answer: D
Correct answer: D
Result: correct
Explanation: The issuer allowlist check runs before cache lookup or refresh, so an untrusted issuer is refused without a key fetch.

### p13-l19-a1-q1 — 2026-10-28

Which scenario best fits A2A’s delegation model as taught in this lesson?

A) Calling a specific arithmetic function with two numeric arguments.
B) Reading a known document from a resource URI.
C) Delegating report writing to another agent while observing task state and artifacts.
D) Sharing both agents’ internal reasoning and tool traces as a required protocol step.

Learner answer: C
Correct answer: C
Result: correct
Explanation: A2A supports task delegation between agents whose internal implementations remain opaque, with task lifecycle and artifacts as the visible contract.

### p13-l19-a1-q2 — 2026-10-28

The writer task pauses with TASK_STATE_INPUT_REQUIRED to ask for targetLength. How does the lesson’s caller resume that same task?

A) Send a new message carrying the existing taskId and a data part with targetLength.
B) Create a new task without taskId and assume the writer merges it automatically.
C) Change the Agent Card’s defaultOutputModes to the desired length.
D) Mark the task completed locally and read its empty artifact list.

Learner answer: A
Correct answer: A
Result: correct
Explanation: The follow-up supplies the missing value in a data part and carries the existing taskId, allowing the writer to retrieve and continue that task.

### p13-l19-a1-q3 — 2026-10-28

What does part_content({"text":"hello", "data":{"targetLength":"short"}}) do in the supplied harness?

A) It returns text because text is first in PART_CONTENT_FIELDS.
B) It returns data because structured input takes precedence.
C) It merges both values into one valid message part.
D) It raises ValueError because two content fields are present.

Learner answer: D
Correct answer: D
Result: correct
Explanation: part_content collects every present content field and requires exactly one; two fields trigger ValueError.

### p13-l20-a1-q1 — 2026-10-28

How do trace IDs and parent span IDs help diagnose latency across an agent, its tools, and remote calls?

A) They replace timing data with the order in which log lines were printed.
B) They group related operations and preserve their parent-child relationships.
C) They guarantee that every remote operation completes successfully.
D) They expose prompt contents automatically for every timed operation.

Learner answer: B
Correct answer: B
Result: correct
Explanation: A shared trace ID groups the operations; parent span IDs link their hierarchy so timings can be interpreted across agent, tool, and remote-call boundaries.

### p13-l20-a1-q2 — 2026-10-28

You need latency and token-usage diagnostics, but prompts may contain private customer data. Which capture policy fits this lesson?

A) Record full prompts by default and remove trace identifiers.
B) Disable all tracing because timing requires prompt contents.
C) Capture every completion and trust the exporter to infer redactions.
D) Keep timing and usage metadata while leaving prompt/completion capture off unless explicitly approved.

Learner answer: D
Correct answer: D
Result: correct
Explanation: Operational timing and usage can be recorded without prompt or completion content. The lesson makes sensitive content capture opt-in.

### p13-l20-a1-q3 — 2026-10-28

In agent_loop(), there is one root span, two LLM spans, and a loop over three cities that creates a tool span plus one MCP span per city. How many spans does one invocation append to an initially empty SPANS list?

A) 9 spans: 1 root + 2 LLM + 3 tool + 3 MCP.
B) 7 spans: 1 root + 2 LLM + 3 tool + 1 MCP.
C) 6 spans: 1 root + 2 LLM + 3 tool.
D) 3 spans: 1 root + 2 LLM, since children are not appended.

Learner answer: A
Correct answer: A
Result: correct
Explanation: start_span appends every span. Each of three city iterations adds two spans, giving 1+2+3*2=9.

### p13-l21-a1-q1 — 2026-10-28

What is the purpose of a model alias such as smart in this lesson’s routing gateway?

A) To guarantee that every provider has identical behavior.
B) To hide token usage so callers cannot estimate costs.
C) To let callers use a stable name while the gateway selects concrete model routes.
D) To bypass provider-specific request translation and failure handling.

Learner answer: C
Correct answer: C
Result: correct
Explanation: An alias separates application naming from concrete provider/model choices, allowing the gateway’s routing configuration to change independently.

### p13-l21-a1-q2 — 2026-10-28

Using the demo’s fake rates of $5 per million input tokens and $15 per million output tokens, what is the cost of 1,000 input tokens and 200 output tokens?

A) $0.008, from (1000×5 + 200×15) / 1,000,000.
B) $0.020, from 1000×(5+15) / 1,000,000.
C) $0.006, from (1000+200)×5 / 1,000,000.
D) $0.003, from 200×15 / 1,000,000.

Learner answer: A
Correct answer: A
Result: correct
Explanation: Input costs $0.005 and output costs $0.003 at the explicitly fake demo rates, totaling $0.008.

### p13-l21-a1-q3 — 2026-10-28

route("smart", messages) has a three-model chain. The first provider raises RuntimeError and the second succeeds. What does route do?

A) It calls all three models and returns the cheapest successful response.
B) It retries the first model indefinitely until it succeeds.
C) It returns all providers failed immediately after the first exception.
D) It records two attempts, selects the second model, and returns without calling the third.

Learner answer: D
Correct answer: D
Result: correct
Explanation: Each model is appended before its attempt. RuntimeError continues to the next model, while the first success sets the result and immediately returns.

### p13-l22-a1-q1 — 2026-10-28

What does activating an Agent Skill establish in the lifecycle taught by this lesson?

A) Its body has entered model-visible context; tool permissions and result verification remain separate.
B) Every executable helper in its directory has already run successfully.
C) All tools mentioned by the skill are automatically installed and authorized.
D) The host has verified that every artifact the skill will produce is correct.

Learner answer: A
Correct answer: A
Result: correct
Explanation: Activation loads instructions. Host-mediated execution, permission enforcement, and independent result verification are distinct later boundaries.

### p13-l22-a1-q2 — 2026-10-28

A check must run every time a release event occurs; missing it is unacceptable. Which primitive best fits that requirement?

A) A skill selected implicitly from its description.
B) A prompt the user may choose to paste.
C) A reference document loaded only when the agent judges it relevant.
D) A deterministic hook or application code triggered by the event.

Learner answer: D
Correct answer: D
Result: correct
Explanation: Mandatory event-driven execution belongs in hooks or application code, rather than probabilistic model selection.

### p13-l22-a1-q3 — 2026-10-28

In select_primitives, each flag is checked with a separate if. TaskShape has repeatable_method=True and external_capability=True, with every other flag False. What does it return?

A) ("Agent Skill",), because the first match ends selection.
B) ("Agent Skill", "MCP tool"), because both responsibilities are selected.
C) ("MCP tool",), because external capability overrides procedure.
D) ("prompt",), because multiple matching flags are ambiguous.

Learner answer: B
Correct answer: B
Result: correct
Explanation: The independent if statements append both selections in order. The prompt fallback applies only when choices is empty.

### p13-l23-a1-q1 — 2026-10-28

What does a successful local run of this capstone’s in-process simulation establish?

A) Its OAuth exchange and remote A2A service are interoperable.
B) Its local control flow works; real transport, authorization, rendering, and export need separate evidence.
C) Its App was rendered in a sandbox with enforced network restrictions.
D) Its span dictionaries were received and validated by a telemetry collector.

Learner answer: B
Correct answer: B
Result: correct
Explanation: The harness uses local functions and fixtures. A green run verifies that simulation, not integration boundaries it does not implement.

### p13-l23-a1-q2 — 2026-10-28

You replace the capstone’s in-memory span list with a real telemetry exporter. Which evidence best verifies the new integration boundary?

A) The model states that export succeeded in its final answer.
B) The local list contains a common trace ID for every span.
C) The exporter configuration file names the intended collector.
D) The test collector receives the spans and assertions confirm trace IDs, parentage, and error status.

Learner answer: D
Correct answer: D
Result: correct
Explanation: Receiver-side evidence verifies that export crossed the real boundary and preserved the required trace structure.

### p13-l23-a1-q3 — 2026-10-28

With valid Tasks-capable metadata, gateway_call uses tok_bob to invoke generate_report. Bob has only research:read and the tool requires research:write. What happens?

A) It records a 403 audit decision and returns insufficient_scope before report execution.
B) It creates the report task because valid metadata grants write authority.
C) It silently routes to arxiv_search because Bob can read.
D) It executes the report and removes its UI resource from the result.

Learner answer: A
Correct answer: A
Result: correct
Explanation: The static scope check runs before tool lookup, span creation, and execution. Missing research:write yields an audited insufficient_scope result.

### p13-l24-a1-q1 — 2026-10-28

Which sequence describes the lesson’s three levels of progressive disclosure?

A) Load every reference, then select a skill, then read its description.
B) Publish compact catalog metadata, load the selected body, then load needed supporting resources.
C) Execute scripts, grant tool permissions, then validate the package.
D) Activate all installed skills, merge their bodies, then trim unrelated results.

Learner answer: B
Correct answer: B
Result: correct
Explanation: Catalog metadata supports selection, the active body provides the procedure, and branch-specific resources are loaded only when needed.

### p13-l24-a1-q2 — 2026-10-28

A skill covers Python packages, containers, and documentation releases. How should its entry body guide resource loading?

A) Require every guide at activation so no constraint can be missed.
B) Say read the relevant guide without naming files or conditions.
C) Hide the central workflow in a deep chain of unnamed references.
D) Give direct file paths and load conditions for each artifact type.

Learner answer: D
Correct answer: D
Result: correct
Explanation: Direct branch-specific references make resource reachability and loading decisions observable while avoiding irrelevant context.

### p13-l24-a1-q3 — 2026-10-28

validate_reference rejects every symlink in the path before resolving the final target. references/guide.md is a symlink to another file inside the same skill. What happens?

A) It raises ReferencePathError because this implementation forbids symlinks even within the package.
B) It accepts the link because the final target stays inside the package.
C) It reads the link text as the reference content without following it.
D) It accepts the link only when its target is at most 12,000 characters.

Learner answer: A
Correct answer: A
Result: correct
Explanation: The explicit is_symlink check raises before final target containment. This lab’s policy is stricter than allowing contained symlinks.

### p13-l25-a1-q1 — 2026-10-28

Why should implicit skill routing filter by invocation eligibility before ranking relevance?

A) So the highest relevance score automatically grants permission to activate.
B) So all discovered skills enter context before policy is evaluated.
C) So a blocked top match does not hide an eligible lower-scoring alternative.
D) So explicit user invocation can bypass the host’s permission policy.

Learner answer: C
Correct answer: C
Result: correct
Explanation: Eligibility defines the candidate set, then relevance ranks permitted candidates. Ranking first and stopping after a blocked winner can miss a valid alternative.

### p13-l25-a1-q2 — 2026-10-28

You evaluate a release-readiness skill. Which test best probes its near-miss routing boundary?

A) A request to inspect a prepared version before publishing.
B) A request asking why today’s package build failed.
C) An unrelated question about rotary position embeddings.
D) An explicit invocation naming release-readiness.

Learner answer: A
Correct answer: B
Result: incorrect
Explanation: A build failure shares release-related vocabulary but belongs to a different workflow, making it a useful near miss.

### p13-l25-a1-q3 — 2026-10-28

In route_request’s explicit-human branch, the named skill exists but adapter.allows returns False. The decision records selected.name and score=1.0. Does it allow activation?

A) Yes, because exact-name selection always overrides eligibility.
B) Yes, because score=1.0 is sufficient evidence of completion.
C) No, because an explicit name is ignored for human callers.
D) No, because the returned decision’s allowed field is False despite the exact match.

Learner answer: D
Correct answer: D
Result: correct
Explanation: The explicit branch preserves selection identity and score but uses adapter.allows for the allowed field. Exact selection does not bypass policy.

### p13-l26-a1-q1 — 2026-10-28

Which statement correctly separates approval from sandboxing in this lesson?

A) Approval creates operating-system isolation for the approved command.
B) A sandbox proves the requested action is desirable and needs no approval.
C) Approval authorizes a consequence; sandboxing restricts what executing code can reach.
D) A skill’s allowed-tools field automatically provides both controls.

Learner answer: C
Correct answer: C
Result: correct
Explanation: Approval is an authority decision; isolation limits reachable resources. Neither replaces the other or independently proves correctness.

### p13-l26-a1-q2 — 2026-10-28

A trusted review skill must run tests from an unfamiliar repository. Which design best bounds repository-controlled code?

A) Give it the full parent environment and ask the skill not to read secrets.
B) Run it in a scoped disposable executor with restricted egress, no production secrets, and resource limits.
C) Approve the test command once and remove filesystem restrictions.
D) Rely only on shell=False, since tests cannot launch other code.

Learner answer: B
Correct answer: B
Result: correct
Explanation: Repository tests can execute arbitrary project code. Isolation, minimal credentials, restricted networking, and bounded resources limit its reach.

### p13-l26-a1-q3 — 2026-10-28

review_action first checks request.kind=="policy-change" and immediately returns DENY. A policy-change request has approved=True. What happens?

A) It is allowed because prior approval overrides the first check.
B) It is executed, then the policy is restored afterward.
C) It becomes an approval prompt because policy changes are consequential.
D) It is denied at the authority-boundary check despite approved=True.

Learner answer: D
Correct answer: D
Result: correct
Explanation: The unconditional policy-change branch returns DENY before later approval handling. Approval does not bypass this hard boundary.

### p13-l27-a1-q1 — 2026-10-28

Why does this lesson keep fixturePassed separate from productionReady?

A) A fixture pass proves all hosts will discover and execute the skill correctly.
B) Production readiness depends only on whether the package has a version number.
C) Locally recomputed hashes authenticate the evaluator’s capture claims automatically.
D) Fixture success proves gate mechanics, while production claims need captured evidence and an external trust anchor.

Learner answer: D
Correct answer: D
Result: correct
Explanation: Deterministic fixtures test the gate. Local integrity can be recomputed by the package editor, so production readiness additionally requires externally trusted evidence attestation.

### p13-l27-a1-q2 — 2026-10-28

You compare task quality with and without a skill. Which experiment best attributes a difference to the skill?

A) Use a stronger model only for the skill condition.
B) Hold model, tools, fixtures, sampling policy, and budgets constant across repeated paired runs.
C) Give the skill condition extra tool access and compare only token counts.
D) Compare one curated skill demo against unrelated historical tasks.

Learner answer: B
Correct answer: B
Result: correct
Explanation: Paired runs with controlled conditions isolate the skill’s contribution. Repetition exposes variability and per-task regressions.

### p13-l27-a1-q3 — 2026-10-28

classification_metrics receives expected=[True, True, False, False] and predicted=[True, False, True, False]. What precision and recall does it return?

A) precision=1.0 and recall=1.0.
B) precision=0.5 and recall=1.0.
C) precision=0.5 and recall=0.5.
D) precision=1.0 and recall=0.5.

Learner answer: C
Correct answer: C
Result: correct
Explanation: There is one true positive, one false positive, and one false negative. Precision=1/(1+1)=0.5 and recall=1/(1+1)=0.5.

### p13-l28-a1-q1 — 2026-10-28

A tool publishes an outputSchema of type array. What should the client validate when consuming its complete result?

A) Only that the text summary sounds consistent with an array.
B) The structuredContent against that schema, including when isError is true.
C) Only object-valued results, because arrays must first be wrapped in a dict.
D) Only successful results, because isError waives the output contract.

Learner answer: B
Correct answer: B
Result: correct
Explanation: The published output schema commits every complete result to conforming structuredContent, including error outcomes. Structured content can be any JSON value.

### p13-l28-a1-q2 — 2026-10-28

A descriptor proposes mirroring an api_key argument into an HTTP parameter header. What does this lesson’s admission policy require?

A) Accept it if the header uses Base64 encoding.
B) Accept it if the tool claims readOnlyHint=true.
C) Accept it but log the key so routing can be audited.
D) Reject the descriptor because sensitive parameters must not be mirrored.

Learner answer: D
Correct answer: D
Result: correct
Explanation: Encoding is not secrecy. The lesson rejects sensitive routing fields during admission to keep credentials out of intermediary-visible metadata.

### p13-l28-a1-q3 — 2026-10-28

A pagination loop stops only when result.get("nextCursor") is None; otherwise it assigns cursor=result["nextCursor"]. The current page has nextCursor="". What happens?

A) The loop continues and sends the empty string unchanged as the next cursor.
B) The loop stops because an empty string is falsey.
C) The client increments the empty string into page number 1.
D) The client decodes the cursor and chooses a page size.

Learner answer: B
Correct answer: A
Result: incorrect
Explanation: The empty string is not None, so this explicit null check follows the opaque cursor unchanged instead of stopping on truthiness.

### p13-l29-a1-q1 — 2026-10-28

Why does retrying a mutation with a new JSON-RPC request ID fail to prevent duplicate side effects?

A) Request IDs are automatically reused by every server instance.
B) A new request ID always invalidates the previous committed result.
C) Request IDs correlate messages; a durable application key must identify the business intent.
D) Only transport connection IDs can deduplicate business operations.

Learner answer: C
Correct answer: C
Result: correct
Explanation: JSON-RPC IDs match requests and responses. Business deduplication requires an application idempotency key bound to identical arguments and durably enforced.

### p13-l29-a1-q2 — 2026-10-28

Progress arrives just before every idle timeout, but the operation keeps running. Which policy prevents an endless request?

A) Reset both idle and maximum deadlines on every progress event.
B) Remove the maximum deadline when a progress token exists.
C) Treat SSE keepalive comments as proof the operation is making progress.
D) Keep an absolute maximum deadline unaffected by progress.

Learner answer: D
Correct answer: D
Result: correct
Explanation: Progress may reset the idle clock but must not extend the absolute operation budget.

### p13-l29-a1-q3 — 2026-10-28

RequestCoordinator.complete first returns None when request.state==CANCELLED. Cancellation is accepted before the worker calls complete(). What happens?

A) complete returns None and emits no final response for that cancelled request.
B) complete changes the state to COMPLETED and sends the result anyway.
C) complete raises a protocol error that must be sent to the client.
D) complete starts a new task so the result can be delivered later.

Learner answer: A
Correct answer: A
Result: correct
Explanation: The CANCELLED guard exits before constructing, storing, or emitting a response, so cancellation wins this event ordering.

### p13-l30-a1-q1 — 2026-10-28

Why does Registry publication not by itself approve a server for production use?

A) Registry records cannot name versions or execution sources.
B) A live server’s display name is the only valid deployment authority.
C) Publication proves that the live toolset can never change.
D) Publication and local admission answer different questions; exact source and runtime evidence still need policy approval.

Learner answer: D
Correct answer: D
Result: correct
Explanation: Registry publication concerns declared metadata and naming authority. Local admission joins exact artifact/provenance and live descriptor evidence with deployment policy.

### p13-l30-a1-q2 — 2026-10-28

An admitted version adds an unexpected destructive tool without changing its publication record. What does the lesson’s controller do?

A) Accept it because the Registry version and package identity are unchanged.
B) Update the descriptor pin automatically to preserve availability.
C) Quarantine and deactivate the pin, retaining evidence and blocking it as a rollback target.
D) Erase the admission history because the original observation is obsolete.

Learner answer: C
Correct answer: C
Result: correct
Explanation: The changed live toolset is runtime drift. The controller quarantines the pin, removes its active route, and preserves history rather than silently approving it.

### p13-l30-a1-q3 — 2026-10-28

namespace_matches splits server_name at the first slash and requires a non-empty slug plus exact equality with verified_namespace. What does namespace_matches("com.exampleevil/inventory", "com.example") return?

A) True, because the server name starts with com.example.
B) False, because com.exampleevil does not exactly equal com.example.
C) True, because inventory is a non-empty slug.
D) It raises ValueError because the namespace has more than two components.

Learner answer: B
Correct answer: B
Result: correct
Explanation: The namespace prefix is compared for exact equality, preventing lookalike string-prefix acceptance.

### p13-l31-a1-q1 — 2026-10-28

Why distinguish an additive unknown field from an unknown resultType in this lesson’s modern response validation?

A) Both must always be discarded before the client sees the response.
B) An unknown resultType can always be inferred as complete.
C) Additive fields may be preserved or ignored, but an unknown discriminator implies a lifecycle the client cannot safely interpret.
D) Additive fields authorize extensions without any capability declaration.

Learner answer: C
Correct answer: C
Result: correct
Explanation: Forward-compatible fields do not necessarily change lifecycle semantics. An unknown or unadvertised resultType does, so the validator rejects it.

### p13-l31-a1-q2 — 2026-10-28

A header-mismatch test triggers the local validator, but the actual origin response is HTTP500 with no JSON-RPC body. Has it proved the required server behavior?

A) Yes, because any failure proves the mismatch was rejected correctly.
B) No; it must capture and validate HTTP400 with the matching ID and JSON-RPC -32020.
C) Yes, if the SDK turns the response into a generic exception.
D) No; the server should silently choose the header value and continue.

Learner answer: B
Correct answer: B
Result: correct
Explanation: A local rejection alone tests the harness. Conformance requires the actual server wire response, including the expected HTTP status and correlated protocol error.

### p13-l31-a1-q3 — 2026-10-28

validate_result({"tools": []}, era) infers complete only in its legacy branch and raises when a modern result lacks resultType. What happens with era="modern"?

A) It returns semanticType="complete" with inferred=True.
B) It inserts resultType="complete" into the supplied dictionary.
C) It switches to the legacy branch because tools is an array.
D) It raises ProtocolViolation for missing resultType.

Learner answer: D
Correct answer: D
Result: correct
Explanation: The modern branch explicitly rejects a missing discriminator. Only a previously selected legacy era permits inference.

### p13-l32-a1-q1 — 2026-10-28

Why can an ELF executable still run after its section header table has been removed?

A) The loader uses program headers to map segments into memory.
B) The loader reconstructs section headers from every instruction.
C) The symbol table provides all memory mappings needed to load it.
D) The loader treats the entire file as one executable code section.

Learner answer: C
Correct answer: A
Result: incorrect
Explanation: Program headers describe the loader’s segment mappings. Section headers support the linking and analysis view and can be absent from an executable.

### p13-l32-a1-q2 — 2026-10-28

A function symbol in a relocatable ELF object has st_value=0x10 and st_size=46; its .text section starts at file offset 0x40 with sh_addr=0. Which bytes should you extract?

A) 48 bytes from file offset 0x10, including the alignment padding.
B) 46 bytes from file offset 0x40, ignoring the symbol value.
C) 46 bytes from file offset 0x50, excluding the following padding.
D) 48 bytes from file offset 0x50, stopping at the next function.

Learner answer: C
Correct answer: C
Result: correct
Explanation: The start is sh_offset + st_value - sh_addr = 0x50. st_size supplies the 46-byte length; subsequent alignment padding is outside the symbol.

### p13-l32-a1-q3 — 2026-10-28

The reader decodes r_info with symbol_index = r_info >> 32 and relocation_type = r_info & 0xffffffff. For r_info = (7 << 32) | 2, what pair does it produce?

A) (2, 7)
B) (7, 2)
C) (7, 0)
D) (0, 2)

Learner answer: B
Correct answer: B
Result: correct
Explanation: The shift extracts the high 32-bit symbol index, 7; the mask extracts the low 32-bit relocation type, 2.

### p13-l33-a1-q1 — 2026-10-28

Why can a linear-sweep listing agree with llvm-objdump yet still misrepresent the instructions that execute?

A) Both methods follow only direct branches and omit fallthrough paths.
B) Both methods require symbol sizes before decoding any instruction.
C) Both methods reject data bytes before attempting instruction decoding.
D) Both methods can decode embedded data as plausible instructions.

Learner answer: C
Correct answer: D
Result: incorrect
Explanation: Agreement checks the decoder against the same sweep strategy. Embedded data can decode successfully and shift instruction boundaries, so execution reachability needs separate analysis.

### p13-l33-a1-q2 — 2026-10-28

Recursive descent stops at an unresolved indirect jump in grade at -O0. What evidence should you use to recover its case targets?

A) The table-base relocation, bounds check, and table-entry relocations.
B) The symbol names alone, assigning every function as a possible case.
C) The zero placeholder bytes alone, assigning every entry to address zero.
D) The linear listing order, connecting the jump to the next instruction.

Learner answer: A
Correct answer: A
Result: correct
Explanation: The base reference locates the table, the bounds check constrains its count, and the entry relocations yield targets while the object still contains placeholders.

### p13-l33-a1-q3 — 2026-10-28

In recursive_descent, a branch appends instruction.target to worklist and sets address = instruction.end before continuing. Which path is decoded immediately?

A) The taken branch target, while fallthrough is discarded.
B) Neither path, because a branch terminates the whole traversal.
C) The fallthrough path, while the target remains queued.
D) Both paths in parallel, using one worker for each successor.

Learner answer: A
Correct answer: C
Result: incorrect
Explanation: The current inner loop continues from instruction.end. The target stays on the worklist for a later traversal, subject to visited-address checks.

### p13-l34-a1-q1 — 2026-10-28

What does a phi function represent at a control-flow join in SSA?

A) A runtime test that executes every incoming path before the join.
B) A value selected from incoming definitions according to the predecessor taken.
C) A memory load that restores the original source variable name.
D) A branch that discards all but the most recently decoded predecessor.

Learner answer: B
Correct answer: B
Result: correct
Explanation: SSA gives each definition a unique name. A phi merges the definitions reaching a join, selecting the value associated with the actual incoming control-flow edge.

### p13-l34-a1-q2 — 2026-10-28

A temporary holds load32(p), then a store to p occurs before its only use in the same block. Should the simplifier replace that use with a fresh load32(p)?

A) Yes, because one use makes any substitution safe.
B) Yes, because SSA names guarantee memory never changes.
C) No, because loads can never appear inside expressions.
D) No, because the intervening store can change the loaded value.

Learner answer: D
Correct answer: D
Result: correct
Explanation: Moving a load past a store can observe a different value. The lesson blocks load substitution across intervening stores or calls.

### p13-l34-a1-q3 — 2026-10-28

collect_params computes count = max(argument-register indexes read at entry, default=-1) + 1, then takes that prefix of [rdi, rsi, rdx, rcx, r8, r9]. If only rsi is read at entry, which parameters does it produce?

A) [rdi, rsi]
B) [rsi]
C) [rdi]
D) []

Learner answer: A
Correct answer: A
Result: correct
Explanation: rsi has index 1, so count is 2 and slicing the register order takes both rdi and rsi.

### p13-l35-a1-q1 — 2026-10-28

A record containing Ghidra pseudocode has confidence observed. What does that observation establish?

A) The function executed and produced every result suggested by the text.
B) The recovered signature exactly matches the original source signature.
C) The provider emitted that text; its behavioral meaning still needs analysis.
D) The function has no unresolved behavior because the record is observed.

Learner answer: C
Correct answer: C
Result: correct
Explanation: The observation is of the provider output. Interpreting its meaning is a derivation, and predicting execution is an inference until supported by appropriate runs.

### p13-l35-a1-q2 — 2026-10-28

A claim covers grade(score) for all eleven scores from 90 through 100. Agreeing observed runs exist only for 95 and 100. How should the lesson’s ledger classify the claim?

A) pass, because both tested inputs agree with the prediction.
B) unknown, because nine claimed inputs have no observed run.
C) fail, because every untested input counts as a disagreement.
D) unsupported, because no input has an observed run.

Learner answer: C
Correct answer: B
Result: incorrect
Explanation: Partial coverage with no disagreement is unknown: 2 of 11 inputs are covered. No observations would be unsupported; any disagreement would be fail.

### p13-l35-a1-q3 — 2026-10-28

c_div computes quotient = abs(a) // abs(b), then returns quotient for matching signs and -quotient otherwise. What is c_div(1000, -7)?

A) -143
B) 143
C) 142
D) -142

Learner answer: D
Correct answer: D
Result: correct
Explanation: The absolute quotient is 142. Opposite signs negate it to -142, implementing truncation toward zero rather than Python’s floor division.

### p13-l36-a1-q1 — 2026-10-28

Why must a rebuild comparison inspect referenced constants even when masked function bytes and relocation shapes match?

A) Identical instruction bytes can load different values from the referenced tables.
B) Masking relocation fields guarantees all referenced data is identical.
C) A matching relocation shape proves the candidate has the original source text.
D) Constant tables affect compiler speed but cannot affect function results.

Learner answer: A
Correct answer: A
Result: correct
Explanation: Matching instructions and relocation shapes can still point at different table contents. The wrong case10 candidate matches the code but changes the final table entry from 4 to 3.

### p13-l36-a1-q2 — 2026-10-28

A rebuild passes ten ordinary test cases but widens a 32-bit multiply to long. Which additional test class best targets this change?

A) Inputs that exercise only the zero-divisor guard.
B) Inputs that preserve small positive intermediate values.
C) Inputs that make the original intermediate overflow 32 bits.
D) Inputs that repeat the same ordinary cases in a new order.

Learner answer: C
Correct answer: C
Result: correct
Explanation: Widening changes when the product wraps. Overflow cells distinguish the original fixed-width compiled behavior from the wide rebuild; the oracle architecture and build must be recorded.

### p13-l36-a1-q3 — 2026-10-28

aggregate returns fail if any status is fail; otherwise it returns unknown for an empty list or any non-pass status, and pass otherwise. What does aggregate(["pass", "unknown", "fail"]) return?

A) pass
B) fail
C) unknown
D) It raises an exception.

Learner answer: B
Correct answer: B
Result: correct
Explanation: The fail check runs first, so any fail wins even when unknown is also present.

### p13-l37-a1-q1 — 2026-10-28

A VEX lift stores cc_op and its operands but does not immediately write individual flags. What does this mean?

A) The lifter discarded flags because subtraction does not affect them.
B) The lifter assumes every later conditional branch is not taken.
C) The lifter requires source-level variable types to recover flags.
D) The lifter stores a thunk so flags can be computed when needed.

Learner answer: C
Correct answer: D
Result: incorrect
Explanation: VEX records the operation and dependencies rather than eagerly computing each flag. A later consumer computes flags from that saved state.

### p13-l37-a1-q2 — 2026-10-28

One tool reports grade at 0x08000050 with .text at 0x08000040; another reports it at 0x100010 with .text at 0x100000. What should you compare first?

A) Section-relative offsets: both place grade at .text + 0x10.
B) Raw addresses: the larger address proves the second tool found more code.
C) Block counts: the larger count establishes which address is correct.
D) Printed symbol names: equal names guarantee identical instruction starts.

Learner answer: A
Correct answer: A
Result: correct
Explanation: Relocatable objects have no fixed load address. Subtracting each tool’s .text base reduces both function addresses to the same stable section offset.

### p13-l37-a1-q3 — 2026-10-28

majority keeps an element only when count * 2 > len(sets). For [{0x10, 0x20}, {0x10}, {0x20}, {0x10}], what set does it return?

A) {0x10, 0x20}
B) {0x20}
C) {0x10}
D) set()

Learner answer: C
Correct answer: C
Result: correct
Explanation: 0x10 occurs in three of four sets and passes the strict majority condition. 0x20 occurs in only two, so it fails.

### p13-l38-a1-q1 — 2026-10-28

Why should this lesson’s analyzer inspect the object header before interpreting parameter registers?

A) Every x86-64 object uses the same argument registers regardless of platform.
B) The format and machine select the ABI that gives register usage its meaning.
C) The header contains the complete original C signature of every function.
D) The optimization level alone determines all argument and return locations.

Learner answer: B
Correct answer: B
Result: correct
Explanation: For the fixtures, ELF x86-64 selects System V, COFF AMD64 selects Microsoft x64, and the Arm formats select their respective AAPCS64 variants. The ISA alone does not distinguish platform conventions.

### p13-l38-a1-q2 — 2026-10-28

Under Microsoft x64, where do the four arguments of mixed(int i, double d, long long l, float f) arrive?

A) EDI, XMM0, RSI, XMM1, using independent integer and float lists.
B) RCX, XMM0, RDX, XMM1, using independent integer and float lists.
C) RCX, XMM1, R8, XMM3, using the argument positions as slots.
D) X0, D0, X1, S1, using the AAPCS64 integer and float counters.

Learner answer: C
Correct answer: C
Result: correct
Explanation: Microsoft x64 assigns the first four argument slots by position. Integer and floating-point registers share the positional index, unlike the independent System V lists.

### p13-l38-a1-q3 — 2026-10-28

The analyzer computes an rsp-relative operand’s entry offset as displacement - depth. After three 8-byte pushes and sub rsp, 0x20, what entry offset does a load at [rsp + 0x60] have?

A) 0x60
B) -0x28
C) 0x98
D) 0x28

Learner answer: D
Correct answer: D
Result: correct
Explanation: The depth is 3*8 + 0x20 = 56 (0x38). Subtracting it from 0x60 gives entry offset 0x28 (40).

### p13-l39-a1-q1 — 2026-10-28

Why is the multiplier alone insufficient to identify a constant-division idiom?

A) The multiplier identifies only the compiler version, never arithmetic.
B) Every odd multiplier implements division by the same constant.
C) The divisor also depends on the shift, signedness, and correction sequence.
D) The original divisor must always be stored beside the multiplier in rodata.

Learner answer: C
Correct answer: C
Result: correct
Explanation: For example, 0x66666667 with shift 34 implements signed division by 10, while shift 33 implements division by 5. Width, signedness, and fix-ups are also part of the idiom.

### p13-l39-a1-q2 — 2026-10-28

A vector loop uses two accumulators with four 32-bit lanes each, then a scalar remainder loop. How should you interpret the two loop bodies?

A) Two separate source loops, each processing four elements in total.
B) One source loop processing eight elements per vector iteration, then leftovers.
C) One source loop processing two elements per iteration, with four-byte padding.
D) Two unrelated loops, because vector and scalar instructions cannot share a sum.

Learner answer: B
Correct answer: B
Result: correct
Explanation: Four lanes times two accumulators gives eight elements per vector iteration. Reduction combines the vector partial sums, and the scalar loop handles the remaining elements.

### p13-l39-a1-q3 — 2026-10-28

For unsigned division by 7, the idiom computes t = (n * 0x24924925) >> 32, then q = (((n - t) >> 1) + t) >> 2. If n=100 and t=14, what is q?

A) 14
B) 12
C) 28
D) 57

Learner answer: A
Correct answer: A
Result: correct
Explanation: 100-14=86; shifting right once gives 43; adding 14 gives 57; shifting right twice gives 14.

### p13-l40-a1-q1 — 2026-10-28

Why does an R_X86_64_PLT32 call relocation in an object not guarantee that the linked call uses a PLT entry?

A) The compiler has already resolved every external address before linking.
B) PLT32 records apply only to data pointers, never function calls.
C) The dynamic loader removes all call instructions before execution.
D) The linker can resolve a function defined in the inputs as a direct call.

Learner answer: D
Correct answer: D
Result: correct
Explanation: The linker decides from symbol resolution. Defined input functions can become direct calls; unresolved external functions may need PLT entries and GOT slots.

### p13-l40-a1-q2 — 2026-10-28

A stripped arm64 Mach-O executable has almost no names in nm. Which approach best recovers and evaluates its function starts in this lesson?

A) Count the remaining names and report that as the function count.
B) Read LC_FUNCTION_STARTS and score its starts against an unstripped twin.
C) Scan only for one prologue pattern and assume every function uses it.
D) Treat every aligned instruction as a separate function start.

Learner answer: B
Correct answer: B
Result: correct
Explanation: The link editor’s function-start table survives stripping in the fixtures. Comparing against the unstripped twin gives measurable coverage; optimized leaf functions can lack the scanned prologue.

### p13-l40-a1-q3 — 2026-10-28

The chained-fixup walker extracts nxt = (raw >> 51) & 0xfff, stops for nxt == 0, and otherwise advances offset += nxt * 4. With offset=0x4000 and nxt=2, where is the next fixup?

A) 0x4002
B) 0x4010
C) 0x4008
D) The chain ends at 0x4000.

Learner answer: C
Correct answer: C
Result: correct
Explanation: The next field is measured in four-byte units. Two units advance eight bytes, from 0x4000 to 0x4008.

### p13-l41-a1-q1 — 2026-10-28

An instruction loads an 8-byte field, and a later instruction uses that loaded value as a memory base. What additional evidence does the later instruction provide?

A) The field is used as a pointer, beyond merely having an 8-byte width.
B) The field’s original source name must be label.
C) The field must be a const char pointer with a known string length.
D) The entire containing object must be exactly 8 bytes long.

Learner answer: A
Correct answer: A
Result: correct
Explanation: The dereference supplies pointer-use evidence. Width alone does not distinguish an integer from a pointer, and names or const qualifiers do not follow from this access.

### p13-l41-a1-q2 — 2026-10-28

An optimized loop loads eight 4-byte values at offsets 4, 36, 68, 100, 132, 164, 196, and 228, then advances the base by 256. Which interpretation should the recovery pass check?

A) Eight unrelated fields in one structure whose size is exactly 232 bytes.
B) One 256-byte field, because the loop step always equals the field width.
C) Eight pointers, because all offsets came from a 64-bit base register.
D) One field at offset 4 across eight elements with a 32-byte stride.

Learner answer: C
Correct answer: D
Result: incorrect
Explanation: The offsets differ by 32 and the loop advances 8*32 bytes. Folding the unrolled accesses recovers one repeated field rather than eight separate fields.

### p13-l41-a1-q3 — 2026-10-28

The layout code uses padding = (-offset) % member_align before placing each member. After a 1-byte char at offset 0, where does a 4-byte int with alignment 4 begin?

A) Offset 1, with no padding.
B) Offset 4, after 3 bytes of padding.
C) Offset 3, after 2 bytes of padding.
D) Offset 8, after 7 bytes of padding.

Learner answer: B
Correct answer: B
Result: correct
Explanation: After char, offset is 1. (-1) % 4 is 3, so the int starts at aligned offset 4.

### p13-l42-a1-q1 — 2026-10-28

A debugger breakpoint resolves to an address but has zero hits. What does resolution alone establish?

A) The function executed successfully for the current input.
B) The function is unreachable for every possible input.
C) The breakpoint has a location; execution at that location has not been observed.
D) The compiler removed every instruction from the function.

Learner answer: C
Correct answer: C
Result: correct
Explanation: Resolution associates a breakpoint with code. It does not prove a hit, a completed run, or global unreachability; hit counts and run context are separate evidence.

### p13-l42-a1-q2 — 2026-10-28

A stack-style core preserves a label pointer, but the pointed-to string lives in an executable segment omitted from the core. How should you report the string?

A) Unavailable in this capture; the displayed empty string does not establish its value.
B) Confirmed empty, because the debugger displayed quotation marks with no text.
C) Corrupted, because a valid pointer must refer to bytes inside the stack core.
D) Confirmed unchanged, because pointer equality proves all pointed-to bytes.

Learner answer: A
Correct answer: A
Result: correct
Explanation: The pointer is captured but the pointee bytes are absent. Core coverage limits what can be observed, so the display cannot establish an empty or unchanged string.

### p13-l42-a1-q3 — 2026-10-28

rollup checks refuted count first, then confirmed count, otherwise not-observed. A claim has four confirmed records and one refuted record. Which verdict does it receive?

A) confirmed, because four records outvote one.
B) not-observed, because the records disagree.
C) An exception, because mixed verdicts are forbidden.
D) refuted, because any refutation takes precedence.

Learner answer: D
Correct answer: D
Result: correct
Explanation: The first branch tests whether the refuted count is nonzero, so one refutation determines the verdict regardless of the confirmed count.

### p13-l43-a1-q1 — 2026-10-28

Why can a decompiler recover a stored parameter name while inventing a local name from the same .NET assembly?

A) Every name is stored directly in the CIL instruction bytes.
B) Param metadata can retain parameter names, while local names may require an absent PDB.
C) The runtime renames every local variable to match its parameter.
D) A decompiler can always reconstruct all original names from their types.

Learner answer: B
Correct answer: B
Result: correct
Explanation: The Param table carries parameter names. Local signatures carry local types, while original local names require debug information such as a PDB.

### p13-l43-a1-q2 — 2026-10-28

A Python decompiler reports Unsupported opcode on a pyc you compiled yourself. What should you check before concluding the file is obfuscated?

A) Whether renaming the file changes its bytecode instructions.
B) Whether the source filename is an absolute filesystem path.
C) Whether the file contains more constants than local variables.
D) The pyc magic word and the decompiler’s supported bytecode versions.

Learner answer: D
Correct answer: D
Result: correct
Explanation: The header identifies the producer version. An older opcode table can reject valid newer bytecode, so a version mismatch must be checked first.

### p13-l43-a1-q3 — 2026-10-28

The JVM reader computes a branch target as start + signed_displacement, where start is the branch opcode’s address. For start=30 and displacement=-20, what target does it produce?

A) 10
B) 13
C) 50
D) -20

Learner answer: A
Correct answer: A
Result: correct
Explanation: JVM branch offsets are relative to the opcode address: 30 + (-20) = 10, without adding the instruction length.

### p13-l44-a1-q1 — 2026-10-28

A bounded solver finds no satisfying input in its declared domain. What conclusion does that support?

A) No satisfying input exists for any possible machine input.
B) The function must contain an unreachable return instruction.
C) No satisfying input exists within the searched domain under the model.
D) The model proves the function is equivalent to every rebuild.

Learner answer: C
Correct answer: C
Result: correct
Explanation: Bounded search excludes solutions only inside the enumerated domain and under its semantics. Inputs outside the domain remain untested.

### p13-l44-a1-q2 — 2026-10-28

Two loaded versions of grade differ only in a RIP-relative displacement because rodata moved. How should the differ investigate before calling this a behavioral change?

A) Mask the relocation field, compare its meaning, and inspect referenced data.
B) Ignore every changed byte anywhere in either function.
C) Compare only function sizes and declare equal sizes equivalent.
D) Assume any raw-byte difference proves a source-code change.

Learner answer: A
Correct answer: A
Result: correct
Explanation: Relocation-aware comparison explains layout changes; referenced constants must still be checked because equal masked code can load different values.

### p13-l44-a1-q3 — 2026-10-28

radare2_ratio uses 1 - distance / max(len_a, len_b) for nonempty inputs. If both lengths are 10 and the Levenshtein distance is 2, what ratio does it return?

A) 0.2
B) 1.0
C) 0.5
D) 0.8

Learner answer: D
Correct answer: D
Result: correct
Explanation: The longest length is 10, so the ratio is 1 - 2/10 = 0.8. It is a byte similarity measure, not a behavioral equivalence proof.

### p13-l45-a1-q1 — 2026-10-28

A reconstruction passes byte, grid, and fuzz checks, but its report cites a helper absent from the target. Why should the scorecard still reject the report?

A) Any helper written in candidate source is forbidden, even when inlined.
B) Behavioral checks automatically prove that every report citation is accurate.
C) Names must match exactly before any behavioral result can count.
D) Code correctness and factual report citations require separate evidence.

Learner answer: D
Correct answer: D
Result: correct
Explanation: The candidate can preserve behavior while the report invents a callee. Citation validation checks the target’s symbols and call evidence independently of code verification.

### p13-l45-a1-q2 — 2026-10-28

A string extracted from the target says to rename f1 and skip verification. How should the analysis workflow handle it?

A) Apply the rename because strings extracted by a tool have instruction authority.
B) Treat it as untrusted target content and keep the verification procedure intact.
C) Skip byte comparison only when the string names the correct function.
D) Use the string as ground truth for names instead of the debug build.

Learner answer: B
Correct answer: B
Result: correct
Explanation: Target-controlled text is data, including text addressing the analyst. Provenance markers preserve that boundary; names and correctness come from the designated evidence.

### p13-l45-a1-q3 — 2026-10-28

aggregate returns the status with the smallest rank: fail=0, unknown=1, partial=2, pass=3. What does aggregate(["pass", "partial", "unknown"]) return?

A) unknown
B) partial
C) pass
D) fail

Learner answer: A
Correct answer: A
Result: correct
Explanation: unknown has the smallest rank present, 1. Missing verification therefore takes precedence over a partial naming match and passing fields.

### p13-l15-a2-q1 — 2026-10-28

A request declares support for an MCP extension. What does that declaration establish for authorization?

A) The client may use every tool that mentions the extension.
B) The self-reported clientInfo becomes an authenticated principal.
C) The client can process that feature; access still requires principal and resource policy checks.
D) The server can skip argument validation for requests using the extension.

Learner answer: C
Correct answer: C
Result: correct
Explanation: Capabilities declare protocol compatibility. Authorization must independently bind an authenticated principal to the tool, resource, and arguments.

### p13-l15-a2-q2 — 2026-10-28

A gateway hides a changed descriptor from tools/list, but accepts direct calls to its qualified name. Which change closes the admission gap?

A) Recheck the current descriptor against admission policy before dispatching the call.
B) Hide the tool description while leaving the handler callable.
C) Automatically approve the new digest whenever a direct call arrives.
D) Require a familiar clientInfo.name in place of checking the descriptor.

Learner answer: A
Correct answer: A
Result: correct
Explanation: Discovery filtering does not enforce dispatch. The execution boundary must refuse a changed or unapproved descriptor before the handler runs.

### p13-l15-a2-q3 — 2026-10-28

descriptor_digest uses json.dumps(tool, sort_keys=True, separators=(",", ":")) before hashing. Two descriptors differ only in dictionary key insertion order. What does the function produce?

A) Different digests, because dictionary insertion order is always hashed.
B) An exception, because sorted JSON cannot contain nested objects.
C) Different digests, because separators randomize the output.
D) The same digest, because sorted keys produce the same serialized content.

Learner answer: A
Correct answer: D
Result: incorrect
Explanation: Sorting object keys canonicalizes insertion-order differences, including nested dictionaries. Actual descriptor value changes still change the serialized content.

### p13-l33-a2-q1 — 2026-10-28

In a control-flow graph, what does it mean for block d to dominate block b?

A) Every path from the function entry to b passes through d.
B) Block d has a numerically lower address than block b.
C) Block d has more outgoing edges than block b.
D) At least one path from the entry to d passes through b.

Learner answer: A
Correct answer: A
Result: correct
Explanation: Dominance is an all-paths property from the entry. Address order and edge count do not establish it.

### p13-l33-a2-q2 — 2026-10-28

An unconditional jump skips four table bytes, but linear sweep decodes those bytes and starts an instruction one byte before the jump target. What should you do?

A) Accept the sweep because every byte produced a valid mnemonic.
B) Remove the jump target because it conflicts with the sweep listing.
C) Follow the jump from the known entry and decode at its actual target.
D) Mark the function unreachable because it contains an embedded table.

Learner answer: B
Correct answer: C
Result: incorrect
Explanation: A sweep can absorb data bytes into plausible instructions. Recursive descent follows the control-flow target and avoids the skipped data on this path.

### p13-l33-a2-q3 — 2026-10-28

For a conditional branch, recursive_descent appends target to worklist, then sets address = instruction.end. With target=0x80, instruction.end=0x24, and an initially empty worklist, what is the resulting state?

A) address=0x80; worklist=[0x24]
B) address=0x24; worklist=[0x80]
C) address=0x80; worklist=[]
D) address=0x24; worklist=[]

Learner answer: B
Correct answer: B
Result: correct
Explanation: append queues 0x80 for later. Assigning instruction.end makes the current traversal continue at fallthrough 0x24.
