# Phase 13 — tools-and-protocols

Status: **done**. Lessons: 45. Scored responses: 141.

Score: initial 119/135 (88.15%); effective 121/135 (89.63%); cumulative 123/141. Passed: all45 lessons meet the2/3 minimum. Lessons15 and33 each retook once and scored2/3. Quiz-based mastery; implementation labs not performed in this assessment.

[All phases](../progress.md) · [Detailed attempts](history.md) · [Review notes](review.md)

## Lesson checklist

| Lesson | Title | Status | Initial score | Latest score | Completion basis |
|---|---|---|---|---|---|
| 13-tools-and-protocols/01-the-tool-interface | The Tool Interface — Why Agents Need Structured I/O | done | 3/3 | 3/3 | quiz-based mastery |
| 13-tools-and-protocols/02-function-calling-deep-dive | Function Calling Deep Dive — OpenAI, Anthropic, Gemini | done | 3/3 | 3/3 | quiz-based mastery |
| 13-tools-and-protocols/03-parallel-and-streaming-tool-calls | Parallel Tool Calls and Streaming with Tools | done | 3/3 | 3/3 | quiz-based mastery |
| 13-tools-and-protocols/04-structured-output | Structured Output — JSON Schema, Pydantic, Zod, Constrained Decoding | done | 2/3 | 2/3 | quiz-based mastery |
| 13-tools-and-protocols/05-tool-schema-design | Tool Schema Design — Naming, Descriptions, Parameter Constraints | done | 3/3 | 3/3 | quiz-based mastery |
| 13-tools-and-protocols/06-mcp-fundamentals | MCP Fundamentals: Stateless Requests and JSON-RPC | done | 3/3 | 3/3 | quiz-based mastery |
| 13-tools-and-protocols/07-building-an-mcp-server | Building an MCP Server: Stateless Python and TypeScript | done | 3/3 | 3/3 | quiz-based mastery |
| 13-tools-and-protocols/08-building-an-mcp-client | Building an MCP Client: Discovery, Routing, and Dual-Era Fallback | done | 2/3 | 2/3 | quiz-based mastery |
| 13-tools-and-protocols/09-mcp-transports | MCP Transports: stdio and Stateless Streamable HTTP | done | 3/3 | 3/3 | quiz-based mastery |
| 13-tools-and-protocols/10-mcp-resources-and-prompts | MCP Resources and Prompts: Addressable Context for Stateless Servers | done | 2/3 | 2/3 | quiz-based mastery |
| 13-tools-and-protocols/11-mcp-sampling | MCP Model Input: Sampling Migration and Stateless MRTR | done | 2/3 | 2/3 | quiz-based mastery |
| 13-tools-and-protocols/12-mcp-roots-and-elicitation | Explicit Scope and Stateless Elicitation | done | 3/3 | 3/3 | quiz-based mastery |
| 13-tools-and-protocols/13-mcp-async-tasks | MCP Tasks Extension: Durable Work on a Stateless Core | done | 3/3 | 3/3 | quiz-based mastery |
| 13-tools-and-protocols/14-mcp-apps | MCP Apps on the Stateless Protocol | done | 2/3 | 2/3 | quiz-based mastery |
| 13-tools-and-protocols/15-mcp-security-tool-poisoning | MCP Security: Poisoned Metadata, Routing, and MRTR State | done | 1/3 | 2/3 | quiz-based mastery |
| 13-tools-and-protocols/16-mcp-security-oauth-2-1 | MCP Authorization: CIMD, Issuer Binding, PKCE, and Step-Up | done | 3/3 | 3/3 | quiz-based mastery |
| 13-tools-and-protocols/17-mcp-gateways-and-registries | Stateless MCP Gateways and Registry Admission | done | 2/3 | 2/3 | quiz-based mastery |
| 13-tools-and-protocols/18-mcp-auth-production | MCP Auth in Production: Issuer-Bound Enrollment and Tokens | done | 3/3 | 3/3 | quiz-based mastery |
| 13-tools-and-protocols/19-a2a-protocol | A2A — Agent-to-Agent Protocol | done | 3/3 | 3/3 | quiz-based mastery |
| 13-tools-and-protocols/20-opentelemetry-genai | OpenTelemetry GenAI — Tracing Tool Calls End-to-End | done | 3/3 | 3/3 | quiz-based mastery |
| 13-tools-and-protocols/21-llm-routing-layer | LLM Routing Layer — LiteLLM, OpenRouter, Portkey | done | 3/3 | 3/3 | quiz-based mastery |
| 13-tools-and-protocols/22-skills-and-agent-sdks | Agent Skills: Portable Contract and Runtime Boundary | done | 3/3 | 3/3 | quiz-based mastery |
| 13-tools-and-protocols/23-capstone-tool-ecosystem | Capstone: Stateless Tool Ecosystem | done | 3/3 | 3/3 | quiz-based mastery |
| 13-tools-and-protocols/24-skill-discovery-and-progressive-disclosure | Skill Discovery and Progressive Disclosure | done | 3/3 | 3/3 | quiz-based mastery |
| 13-tools-and-protocols/25-skill-invocation-and-routing | Skill Invocation and Routing | done | 2/3 | 2/3 | quiz-based mastery |
| 13-tools-and-protocols/26-skill-permissions-sandboxes-and-trust | Skill Permissions, Sandboxes, and Trust | done | 3/3 | 3/3 | quiz-based mastery |
| 13-tools-and-protocols/27-skill-evals-packaging-and-portability | Skill Evals, Packaging, and Portability | done | 3/3 | 3/3 | quiz-based mastery |
| 13-tools-and-protocols/28-mcp-tool-contracts-and-content | MCP Tool Contracts and Content | done | 2/3 | 2/3 | quiz-based mastery |
| 13-tools-and-protocols/29-mcp-reliability-cancellation-and-flow-control | MCP Reliability, Cancellation, and Flow Control | done | 3/3 | 3/3 | quiz-based mastery |
| 13-tools-and-protocols/30-mcp-registry-supply-chain-and-drift | MCP Registry Supply Chain: Admission, Drift, and Rollback | done | 3/3 | 3/3 | quiz-based mastery |
| 13-tools-and-protocols/31-mcp-conformance-versioning-and-operations | MCP Conformance Engineering: Versioning, Evidence, and Operations | done | 3/3 | 3/3 | quiz-based mastery |
| 13-tools-and-protocols/32-program-anatomy-elf-from-scratch | Program Anatomy: An ELF Reader From Scratch | done | 2/3 | 2/3 | quiz-based mastery |
| 13-tools-and-protocols/33-disassembly-and-control-flow | Disassembly and Control Flow: From Bytes to a Graph You Can Check | done | 1/3 | 2/3 | quiz-based mastery |
| 13-tools-and-protocols/34-lifting-to-pseudocode | Lifting to Pseudocode: IR, SSA, and Structuring From Scratch | done | 3/3 | 3/3 | quiz-based mastery |
| 13-tools-and-protocols/35-evidence-confidence-and-unknowns | Evidence, Confidence, and Unknowns in Binary Analysis | done | 2/3 | 2/3 | quiz-based mastery |
| 13-tools-and-protocols/36-rebuild-and-prove-equal | Rebuild and Prove Equal: Differential Tests, Byte Comparison, and the Evidence Loop | done | 3/3 | 3/3 | quiz-based mastery |
| 13-tools-and-protocols/37-the-reverse-engineering-landscape | The Reverse Engineering Landscape: History, Tool Families, and How a Decompiler Is Built | done | 2/3 | 2/3 | quiz-based mastery |
| 13-tools-and-protocols/38-calling-conventions-and-stack-frames | Calling Conventions and Stack Frames: System V, Windows x64, and AArch64 | done | 3/3 | 3/3 | quiz-based mastery |
| 13-tools-and-protocols/39-compiler-idioms-and-optimization | Compiler Idioms: What Optimization Does to Your Code and How to Read It Back | done | 3/3 | 3/3 | quiz-based mastery |
| 13-tools-and-protocols/40-linking-loading-and-stripped-binaries | Linking, Loading, and Stripped Binaries: PLT, GOT, Imports, Fixups, and Function Identification | done | 3/3 | 3/3 | quiz-based mastery |
| 13-tools-and-protocols/41-recovering-data-and-types | Recovering Data and Types: Structs, Arrays, C++ Objects, and DWARF | done | 2/3 | 2/3 | quiz-based mastery |
| 13-tools-and-protocols/42-dynamic-analysis-of-your-own-program | Dynamic Analysis of Your Own Program: Debuggers, Traces, and Confirming Static Claims | done | 3/3 | 3/3 | quiz-based mastery |
| 13-tools-and-protocols/43-bytecode-and-managed-formats | Beyond Native Code: Python, JVM, .NET, and WebAssembly Bytecode | done | 3/3 | 3/3 | quiz-based mastery |
| 13-tools-and-protocols/44-binary-diffing-and-symbolic-execution | Binary Diffing and Symbolic Execution: Matching Functions and Solving for Inputs | done | 3/3 | 3/3 | quiz-based mastery |
| 13-tools-and-protocols/45-ai-assisted-reverse-engineering | AI-Assisted Reverse Engineering: LLM Decompilers, Analysis Agents, and Ground Truth | done | 3/3 | 3/3 | quiz-based mastery |

## Progress log

| Date | Lesson | Quiz | Note |
|---|---|---|---|

| 2026-10-28 | 13-tools-and-protocols/01-the-tool-interface | 3/3 | Quiz-based mastery credit; implementation lab not performed in this assessment. |
| 2026-10-28 | 13-tools-and-protocols/02-function-calling-deep-dive | 3/3 | Quiz-based mastery credit; implementation lab not performed in this assessment. |
| 2026-10-28 | 13-tools-and-protocols/03-parallel-and-streaming-tool-calls | 3/3 | Quiz-based mastery credit; implementation lab not performed in this assessment. |
| 2026-10-28 | 13-tools-and-protocols/04-structured-output | 2/3 | Quiz-based mastery credit; implementation lab not performed in this assessment. |
| 2026-10-28 | 13-tools-and-protocols/05-tool-schema-design | 3/3 | Quiz-based mastery credit; implementation lab not performed in this assessment. |
| 2026-10-28 | 13-tools-and-protocols/06-mcp-fundamentals | 3/3 | Quiz-based mastery credit; implementation lab not performed in this assessment. |
| 2026-10-28 | 13-tools-and-protocols/07-building-an-mcp-server | 3/3 | Quiz-based mastery credit; implementation lab not performed in this assessment. |
| 2026-10-28 | 13-tools-and-protocols/08-building-an-mcp-client | 2/3 | Quiz-based mastery credit; implementation lab not performed in this assessment. |
| 2026-10-28 | 13-tools-and-protocols/09-mcp-transports | 3/3 | Quiz-based mastery credit; implementation lab not performed in this assessment. |
| 2026-10-28 | 13-tools-and-protocols/10-mcp-resources-and-prompts | 2/3 | Quiz-based mastery credit; implementation lab not performed in this assessment. |
| 2026-10-28 | 13-tools-and-protocols/11-mcp-sampling | 2/3 | Quiz-based mastery credit; implementation lab not performed in this assessment. |
| 2026-10-28 | 13-tools-and-protocols/12-mcp-roots-and-elicitation | 3/3 | Quiz-based mastery credit; implementation lab not performed in this assessment. |
| 2026-10-28 | 13-tools-and-protocols/13-mcp-async-tasks | 3/3 | Quiz-based mastery credit; implementation lab not performed in this assessment. |
| 2026-10-28 | 13-tools-and-protocols/14-mcp-apps | 2/3 | Quiz-based mastery credit; implementation lab not performed in this assessment. |
| 2026-10-28 | 13-tools-and-protocols/15-mcp-security-tool-poisoning | 2/3 | Quiz-based mastery credit; implementation lab not performed in this assessment. Initial1/3; fresh retake2/3. |
| 2026-10-28 | 13-tools-and-protocols/16-mcp-security-oauth-2-1 | 3/3 | Quiz-based mastery credit; implementation lab not performed in this assessment. |
| 2026-10-28 | 13-tools-and-protocols/17-mcp-gateways-and-registries | 2/3 | Quiz-based mastery credit; implementation lab not performed in this assessment. |
| 2026-10-28 | 13-tools-and-protocols/18-mcp-auth-production | 3/3 | Quiz-based mastery credit; implementation lab not performed in this assessment. |
| 2026-10-28 | 13-tools-and-protocols/19-a2a-protocol | 3/3 | Quiz-based mastery credit; implementation lab not performed in this assessment. |
| 2026-10-28 | 13-tools-and-protocols/20-opentelemetry-genai | 3/3 | Quiz-based mastery credit; implementation lab not performed in this assessment. |
| 2026-10-28 | 13-tools-and-protocols/21-llm-routing-layer | 3/3 | Quiz-based mastery credit; implementation lab not performed in this assessment. |
| 2026-10-28 | 13-tools-and-protocols/22-skills-and-agent-sdks | 3/3 | Quiz-based mastery credit; implementation lab not performed in this assessment. |
| 2026-10-28 | 13-tools-and-protocols/23-capstone-tool-ecosystem | 3/3 | Quiz-based mastery credit; implementation lab not performed in this assessment. |
| 2026-10-28 | 13-tools-and-protocols/24-skill-discovery-and-progressive-disclosure | 3/3 | Quiz-based mastery credit; implementation lab not performed in this assessment. |
| 2026-10-28 | 13-tools-and-protocols/25-skill-invocation-and-routing | 2/3 | Quiz-based mastery credit; implementation lab not performed in this assessment. |
| 2026-10-28 | 13-tools-and-protocols/26-skill-permissions-sandboxes-and-trust | 3/3 | Quiz-based mastery credit; implementation lab not performed in this assessment. |
| 2026-10-28 | 13-tools-and-protocols/27-skill-evals-packaging-and-portability | 3/3 | Quiz-based mastery credit; implementation lab not performed in this assessment. |
| 2026-10-28 | 13-tools-and-protocols/28-mcp-tool-contracts-and-content | 2/3 | Quiz-based mastery credit; implementation lab not performed in this assessment. |
| 2026-10-28 | 13-tools-and-protocols/29-mcp-reliability-cancellation-and-flow-control | 3/3 | Quiz-based mastery credit; implementation lab not performed in this assessment. |
| 2026-10-28 | 13-tools-and-protocols/30-mcp-registry-supply-chain-and-drift | 3/3 | Quiz-based mastery credit; implementation lab not performed in this assessment. |
| 2026-10-28 | 13-tools-and-protocols/31-mcp-conformance-versioning-and-operations | 3/3 | Quiz-based mastery credit; implementation lab not performed in this assessment. |
| 2026-10-28 | 13-tools-and-protocols/32-program-anatomy-elf-from-scratch | 2/3 | Quiz-based mastery credit; implementation lab not performed in this assessment. |
| 2026-10-28 | 13-tools-and-protocols/33-disassembly-and-control-flow | 2/3 | Quiz-based mastery credit; implementation lab not performed in this assessment. Initial1/3; fresh retake2/3. |
| 2026-10-28 | 13-tools-and-protocols/34-lifting-to-pseudocode | 3/3 | Quiz-based mastery credit; implementation lab not performed in this assessment. |
| 2026-10-28 | 13-tools-and-protocols/35-evidence-confidence-and-unknowns | 2/3 | Quiz-based mastery credit; implementation lab not performed in this assessment. |
| 2026-10-28 | 13-tools-and-protocols/36-rebuild-and-prove-equal | 3/3 | Quiz-based mastery credit; implementation lab not performed in this assessment. |
| 2026-10-28 | 13-tools-and-protocols/37-the-reverse-engineering-landscape | 2/3 | Quiz-based mastery credit; implementation lab not performed in this assessment. |
| 2026-10-28 | 13-tools-and-protocols/38-calling-conventions-and-stack-frames | 3/3 | Quiz-based mastery credit; implementation lab not performed in this assessment. |
| 2026-10-28 | 13-tools-and-protocols/39-compiler-idioms-and-optimization | 3/3 | Quiz-based mastery credit; implementation lab not performed in this assessment. |
| 2026-10-28 | 13-tools-and-protocols/40-linking-loading-and-stripped-binaries | 3/3 | Quiz-based mastery credit; implementation lab not performed in this assessment. |
| 2026-10-28 | 13-tools-and-protocols/41-recovering-data-and-types | 2/3 | Quiz-based mastery credit; implementation lab not performed in this assessment. |
| 2026-10-28 | 13-tools-and-protocols/42-dynamic-analysis-of-your-own-program | 3/3 | Quiz-based mastery credit; implementation lab not performed in this assessment. |
| 2026-10-28 | 13-tools-and-protocols/43-bytecode-and-managed-formats | 3/3 | Quiz-based mastery credit; implementation lab not performed in this assessment. |
| 2026-10-28 | 13-tools-and-protocols/44-binary-diffing-and-symbolic-execution | 3/3 | Quiz-based mastery credit; implementation lab not performed in this assessment. |
| 2026-10-28 | 13-tools-and-protocols/45-ai-assisted-reverse-engineering | 3/3 | Quiz-based mastery credit; implementation lab not performed in this assessment. |
