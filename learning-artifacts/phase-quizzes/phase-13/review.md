# Phase 13 review queue

Historical notes are preserved verbatim; some early remediation requests were superseded by later passes. Latest completion status is in [phase progress](progress.md).

No review items recorded.

- Lesson04, p13-l04-a1-q2: Chose refusal for valid JSON with total_usd=-5 under minimum: 0. This is a schema violation; refusal means the model declined. Review: phases/13-tools-and-protocols/04-structured-output/docs/en.md.

- Lesson08, p13-l08-a1-q3: Chose routing notes/search to files. Canonical notes/search maps to the notes peer; outgoing tools/call uses local name search. Review: phases/13-tools-and-protocols/08-building-an-mcp-client/docs/en.md.

- Lesson10, p13-l10-a1-q3: Chose -32602 for absent resourceSubscriptions. The method defaults to [] and returns None when URI membership fails. resourcesListChanged is a separate category. Review: phases/13-tools-and-protocols/10-mcp-resources-and-prompts/docs/en.md.

- Lesson11, p13-l11-a1-q3: Chose automatic expiry after three requests. run_mrtr has no explicit round limit; request IDs only correlate calls. A persistently input_required server keeps the loop running. Review: phases/13-tools-and-protocols/11-mcp-sampling/docs/en.md.

- Lesson14, p13-l14-a1-q3: Chose retaining UI binding without Apps capability. tools/list preserves notes_timeline but conditionally omits _meta.ui; text fallback remains available. Review: phases/13-tools-and-protocols/14-mcp-apps/docs/en.md.

- Lesson15, p13-l15-a1-q2: Chose clientInfo.version as approval for schema changes. Pin and compare the full canonical descriptor, including inputSchema. Self-reported clientInfo is not authorization or admission approval. Review: phases/13-tools-and-protocols/15-mcp-security-tool-poisoning/docs/en.md.

- Lesson15, p13-l15-a1-q3: Chose an enforced digest check on direct dispatch. The toy only scans for listing; tools/call still directly returns notes.search. Admission must also be enforced before dispatch. Initial lesson score 1/3; fresh three-question remediation required. Review: phases/13-tools-and-protocols/15-mcp-security-tool-poisoning/docs/en.md.

- Lesson17, p13-l17-a1-q3: Chose automatic pin refresh and forwarding. The code records pin_mismatch and returns HTTP409/-32010 before forwarding; changes require re-approval. Review: phases/13-tools-and-protocols/17-mcp-gateways-and-registries/docs/en.md.

- Lesson25, p13-l25-a1-q2: Chose prepared-release inspection as a near miss. That is a positive trigger; a package build failure is a near miss because it shares vocabulary but belongs to build diagnostics. Review: phases/13-tools-and-protocols/25-skill-invocation-and-routing/docs/en.md.

- Lesson28, p13-l28-a1-q3: Chose stopping on empty cursor. The actual test is is None, not truthiness: empty string continues unchanged. Review: phases/13-tools-and-protocols/28-mcp-tool-contracts-and-content/docs/en.md.

- Lesson32, question94 (p13-l32-a1-q1): Chose the symbol table as the source of loader mappings. Review program headers versus section headers: PT_LOAD entries describe memory mappings; symbol tables name symbols and are not required to load an executable.

- Lesson33, question97 (p13-l33-a1-q1): Chose automatic data rejection by linear sweep. Linear sweep can decode embedded data as plausible instructions and shift instruction boundaries; agreement with llvm-objdump does not independently prove reachability or distinguish code from data. Review the sweep-trap example and recursive descent.

- Lesson33, question99 (p13-l33-a1-q3): Chose immediate traversal of the taken branch. worklist.append queues the target; address = instruction.end continues immediately along fallthrough. Lesson33 initial 1/3; requires a fresh scored three-question retake.

- Lesson35, question104 (p13-l35-a1-q2): Chose fail for partial observed coverage. Missing runs are unknown, not disagreement: two agreeing runs out of eleven claimed inputs yield unknown (2/11). A disagreeing run yields fail; no runs yields unsupported.

- Lesson37, question109 (p13-l37-a1-q1): Chose source-level types as necessary for flag recovery. VEX stores cc_op and operand dependencies as a thunk; flag consumers compute flags later from this state. Source variable types are not required. Review eager P-code flags versus deferred VEX flags.

- Lesson41, question122 (p13-l41-a1-q2): Chose eight pointers from a 64-bit base register. The base width does not determine loaded field kind. Eight 4-byte loads spaced 32 bytes apart with a 256-byte loop step support an unrolled access to one field at offset 4 across eight 32-byte elements. Review fold_unrolled and stride evidence.

- Lesson15 retake2, question3 (p13-l15-a2-q3): Chose different hashes for dictionary insertion order. sort_keys=True serializes dictionary keys in sorted order, so otherwise identical descriptors hash identically. Retake2 scored2/3, replacing initial1/3 for effective scoring; retain schema/dispatch and serialization review notes.

- Lesson33 retake2, question2 (p13-l33-a2-q2): Chose removing a jump target when it conflicts with linear sweep. Preserve the control-flow target and decode there from the known entry; a sweep may have consumed skipped table data as instruction prefixes. Plausible sweep mnemonics do not override control-flow evidence.

## Phase pass — 2026-10-28

Initial119/135; effective121/135 (89.63%); cumulative123/141. Lesson15 and Lesson33 retakes scored2/3 each. Preserve all earlier missed-topic notes, especially sorted descriptor serialization and distinguishing sweep-decoded data from reachable instructions. All45 lessons received quiz-based mastery credit; implementation lab not performed in this assessment.
