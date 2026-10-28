# Phase 13 — tools-and-protocols Review Summary

[All phases](../progress.md)

- Status: **Done / Passed**; passed on 2026-10-28; coverage: **45 lessons**.
- Initial score: **119/135**; final effective score: **121/135 (89.63%)**.
- Cumulative responses: 141, with 123 correct; **18 initial/retake mistakes** retained. Cumulative responses include retakes and are not the mastery-score denominator.
- Pass criteria: effective phase score ≥85% and final score ≥2/3 in every lesson; all criteria met. Completion basis: quiz-based mastery; implementation labs were not performed in this assessment.

## Weak points and review priorities

- Prioritize L15 canonical digests of complete descriptors and admission before execution: sort_keys=True removes dictionary insertion-order differences, and filtering tools/list cannot prevent direct tools/call dispatch. L17 pin mismatches should stop forwarding and require reapproval.
- L32: loaders use PT_LOAD program headers. L33: linear sweep can decode data as instructions; control-flow targets take precedence over questionable sweep boundaries. Enqueuing a worklist item does not traverse it immediately. Conflicting-target handling still needs review after the retake.
- L04: a schema violation is not a refusal. L08: separate canonical peer names from local tool names. L10: missing subscription lists default to empty. L11: request IDs correlate calls rather than limit loops. L14: preserve text fallback without Apps capability.
- L25: distinguish positive skill triggers from vocabulary-sharing near misses. L28: distinguish is None from an empty string. L35: missing observations are unknown; observed counterexamples yield fail. L37: VEX defers flag computation. L41: infer access patterns from field widths and strides, not base-register width alone.

## Lessons with mistakes and retake outcomes

Lessons with mistakes or retakes are listed below, along with any additional rows retained from the original ledger. Unlisted lessons scored 3/3 initially and finally. A final 3/3 indicates correction in a later assessment where applicable; retain those topics for spaced recall. Lessons at 2/3 remain review priorities.

| Lesson | Initial score | Final effective score / retake |
|---|---|---|
| [Structured Output — JSON Schema, Pydantic, Zod, Constrained Decoding](../../../phases/13-tools-and-protocols/04-structured-output/docs/en.md) | 2/3 | 2/3 |
| [Building an MCP Client: Discovery, Routing, and Dual-Era Fallback](../../../phases/13-tools-and-protocols/08-building-an-mcp-client/docs/en.md) | 2/3 | 2/3 |
| [MCP Resources and Prompts: Addressable Context for Stateless Servers](../../../phases/13-tools-and-protocols/10-mcp-resources-and-prompts/docs/en.md) | 2/3 | 2/3 |
| [MCP Model Input: Sampling Migration and Stateless MRTR](../../../phases/13-tools-and-protocols/11-mcp-sampling/docs/en.md) | 2/3 | 2/3 |
| [MCP Apps on the Stateless Protocol](../../../phases/13-tools-and-protocols/14-mcp-apps/docs/en.md) | 2/3 | 2/3 |
| [MCP Security: Poisoned Metadata, Routing, and MRTR State](../../../phases/13-tools-and-protocols/15-mcp-security-tool-poisoning/docs/en.md) | 1/3 | 2/3 |
| [Stateless MCP Gateways and Registry Admission](../../../phases/13-tools-and-protocols/17-mcp-gateways-and-registries/docs/en.md) | 2/3 | 2/3 |
| [Skill Invocation and Routing](../../../phases/13-tools-and-protocols/25-skill-invocation-and-routing/docs/en.md) | 2/3 | 2/3 |
| [MCP Tool Contracts and Content](../../../phases/13-tools-and-protocols/28-mcp-tool-contracts-and-content/docs/en.md) | 2/3 | 2/3 |
| [Program Anatomy: An ELF Reader From Scratch](../../../phases/13-tools-and-protocols/32-program-anatomy-elf-from-scratch/docs/en.md) | 2/3 | 2/3 |
| [Disassembly and Control Flow: From Bytes to a Graph You Can Check](../../../phases/13-tools-and-protocols/33-disassembly-and-control-flow/docs/en.md) | 1/3 | 2/3 |
| [Evidence, Confidence, and Unknowns in Binary Analysis](../../../phases/13-tools-and-protocols/35-evidence-confidence-and-unknowns/docs/en.md) | 2/3 | 2/3 |
| [The Reverse Engineering Landscape: History, Tool Families, and How a Decompiler Is Built](../../../phases/13-tools-and-protocols/37-the-reverse-engineering-landscape/docs/en.md) | 2/3 | 2/3 |
| [Recovering Data and Types: Structs, Arrays, C++ Objects, and DWARF](../../../phases/13-tools-and-protocols/41-recovering-data-and-types/docs/en.md) | 2/3 | 2/3 |

## Condensed mistake records

Question IDs, prompts, selected wrong answers, correct answers, and explanations are retained. Other distractors, correct-only questions, and per-response score logs are omitted. Prompts and explanations retain their original English wording. These are historical initial/retake mistakes, not pending retake requirements.

### p13-l04-a1-q2

An extraction output is valid JSON, but total_usd is -5 while its schema requires minimum: 0. How should the lesson’s handler classify it?

- Learner answer: B — refusal, because the model supplied an unacceptable value.
- Correct answer: C — violation, because parsed data fails a schema constraint.
- Explanation: The JSON parses successfully, but the negative value fails the minimum constraint, making it a schema violation.

### p13-l08-a1-q3

Both files and notes advertise search, and merge() uses its default policy. With peers processed alphabetically, what does call("notes/search", {}) send?

- Learner answer: A — A tools/call to files with name="notes/search".
- Correct answer: C — A tools/call to notes with name="search".
- Explanation: The merged registry stores notes/search as the canonical name with peer_name notes and local_name search. call routes to the owning peer using the local name.

### p13-l10-a1-q3

A SubscriptionStream has notifications={"resourcesListChanged": True} and no resourceSubscriptions entry. What does resource_updated("notes://note-1") return?

- Learner answer: C — A JSON-RPC error with code -32602 for the absent URI filter.
- Correct answer: D — None because that URI is not in resourceSubscriptions.
- Explanation: resource_updated checks membership in resourceSubscriptions, defaulting to an empty list. resourcesListChanged enables a separate notification category.

### p13-l11-a1-q3

In run_mrtr(), the loop continues while resultType is input_required, increments request_id each round, and has no round counter. What happens if a modified server always returns a fulfillable input_required result?

- Learner answer: B — It rejects the fourth response because all tokens expire after three requests.
- Correct answer: D — It keeps retrying because the loop has no explicit round limit.
- Explanation: The demo’s normal state machine finishes, but run_mrtr itself has no enforced round budget. Incrementing IDs provides correlation, not a stopping condition.

### p13-l14-a1-q3

In McpAppServer.handle, a valid tools/list request has apps=False. What happens to the notes_timeline tool?

- Learner answer: D — The server lists it with the same UI binding despite missing capability.
- Correct answer: A — It remains listed, but the conditional _meta.ui binding is omitted.
- Explanation: The handler always builds the tool descriptor and adds _meta.ui only when _apps_enabled(meta) is true, preserving the text-capable tool.

### p13-l15-a1-q2

An approved tool keeps its name and description but changes inputSchema. Which admission control detects this change?

- Learner answer: D — Use clientInfo.version as permission to accept schema changes.
- Correct answer: A — Pin and compare a canonical digest of the complete descriptor.
- Explanation: Whole-descriptor pinning includes the schema. A description-only scan or hash misses changes to other fields.

### p13-l15-a1-q3

In SecurityGateway.handle, _visible_tools scans descriptors for tools/list, but the tools/call branch routes directly by params.name. After notes.search is changed and hidden from the list, what does a direct valid tools/call to notes.search do?

- Learner answer: A — It fails the approved-digest check before reaching the handler.
- Correct answer: B — It returns the hard-coded search result because dispatch does not rescan the descriptor.
- Explanation: The sample checks visibility during listing, but the direct call branch still matches notes.search and returns its fixed result. Discovery filtering alone does not enforce admission at dispatch.

### p13-l17-a1-q3

In Gateway.handle, RBAC allows a direct tool call and its rate bucket has capacity, but the live descriptor digest differs from its pin. What happens before _forward?

- Learner answer: A — The gateway refreshes the pin automatically and forwards the call.
- Correct answer: C — It records pin_mismatch and returns HTTP 409 with error -32010.
- Explanation: The call path checks _is_pinned before _forward. A mismatch is audited and returns HTTP 409 with a Descriptor changed JSON-RPC error.

### p13-l25-a1-q2

You evaluate a release-readiness skill. Which test best probes its near-miss routing boundary?

- Learner answer: A — A request to inspect a prepared version before publishing.
- Correct answer: B — A request asking why today’s package build failed.
- Explanation: A build failure shares release-related vocabulary but belongs to a different workflow, making it a useful near miss.

### p13-l28-a1-q3

A pagination loop stops only when result.get("nextCursor") is None; otherwise it assigns cursor=result["nextCursor"]. The current page has nextCursor="". What happens?

- Learner answer: B — The loop stops because an empty string is falsey.
- Correct answer: A — The loop continues and sends the empty string unchanged as the next cursor.
- Explanation: The empty string is not None, so this explicit null check follows the opaque cursor unchanged instead of stopping on truthiness.

### p13-l32-a1-q1

Why can an ELF executable still run after its section header table has been removed?

- Learner answer: C — The symbol table provides all memory mappings needed to load it.
- Correct answer: A — The loader uses program headers to map segments into memory.
- Explanation: Program headers describe the loader’s segment mappings. Section headers support the linking and analysis view and can be absent from an executable.

### p13-l33-a1-q1

Why can a linear-sweep listing agree with llvm-objdump yet still misrepresent the instructions that execute?

- Learner answer: C — Both methods reject data bytes before attempting instruction decoding.
- Correct answer: D — Both methods can decode embedded data as plausible instructions.
- Explanation: Agreement checks the decoder against the same sweep strategy. Embedded data can decode successfully and shift instruction boundaries, so execution reachability needs separate analysis.

### p13-l33-a1-q3

In recursive_descent, a branch appends instruction.target to worklist and sets address = instruction.end before continuing. Which path is decoded immediately?

- Learner answer: A — The taken branch target, while fallthrough is discarded.
- Correct answer: C — The fallthrough path, while the target remains queued.
- Explanation: The current inner loop continues from instruction.end. The target stays on the worklist for a later traversal, subject to visited-address checks.

### p13-l35-a1-q2

A claim covers grade(score) for all eleven scores from 90 through 100. Agreeing observed runs exist only for 95 and 100. How should the lesson’s ledger classify the claim?

- Learner answer: C — fail, because every untested input counts as a disagreement.
- Correct answer: B — unknown, because nine claimed inputs have no observed run.
- Explanation: Partial coverage with no disagreement is unknown: 2 of 11 inputs are covered. No observations would be unsupported; any disagreement would be fail.

### p13-l37-a1-q1

A VEX lift stores cc_op and its operands but does not immediately write individual flags. What does this mean?

- Learner answer: C — The lifter requires source-level variable types to recover flags.
- Correct answer: D — The lifter stores a thunk so flags can be computed when needed.
- Explanation: VEX records the operation and dependencies rather than eagerly computing each flag. A later consumer computes flags from that saved state.

### p13-l41-a1-q2

An optimized loop loads eight 4-byte values at offsets 4, 36, 68, 100, 132, 164, 196, and 228, then advances the base by 256. Which interpretation should the recovery pass check?

- Learner answer: C — Eight pointers, because all offsets came from a 64-bit base register.
- Correct answer: D — One field at offset 4 across eight elements with a 32-byte stride.
- Explanation: The offsets differ by 32 and the loop advances 8*32 bytes. Folding the unrolled accesses recovers one repeated field rather than eight separate fields.

### p13-l15-a2-q3

descriptor_digest uses json.dumps(tool, sort_keys=True, separators=(",", ":")) before hashing. Two descriptors differ only in dictionary key insertion order. What does the function produce?

- Learner answer: A — Different digests, because dictionary insertion order is always hashed.
- Correct answer: D — The same digest, because sorted keys produce the same serialized content.
- Explanation: Sorting object keys canonicalizes insertion-order differences, including nested dictionaries. Actual descriptor value changes still change the serialized content.

### p13-l33-a2-q2

An unconditional jump skips four table bytes, but linear sweep decodes those bytes and starts an instruction one byte before the jump target. What should you do?

- Learner answer: B — Remove the jump target because it conflicts with the sweep listing.
- Correct answer: C — Follow the jump from the known entry and decode at its actual target.
- Explanation: A sweep can absorb data bytes into plausible instructions. Recursive descent follows the control-flow target and avoids the skipped data on this path.
