# My AI Engineering Path
<!-- Managed by the ai-engineering-from-scratch learning skills.
     Repo: https://github.com/rohitg00/ai-engineering-from-scratch -->

## Mission
For career growth and personal work to follow the new knowledge

Build goal: As many as possible, everything

## Placement
- Date: 2026-09-17
- Score: 10/10 (Math & Statistics: 2/2; Classical ML: 2/2; Deep Learning: 2/2; NLP & Transformers: 2/2; Applied AI: 2/2)
- Entry point: Phase 14: Agent Engineering
- Pace: As fast as possible

## Path
| Phase | Name | Status | Est. hours |
|-------|------|--------|------------|
| 0 | Setup & Tooling | Skip | -- |
| 1 | Math Foundations | Skip | -- |
| 2 | ML Fundamentals | Skip | -- |
| 3 | Deep Learning Core | Skip | -- |
| 4 | Computer Vision | Skip | -- |
| 5 | NLP — Foundations to Advanced | Skip | -- |
| 6 | Speech & Audio | Skip | -- |
| 7 | Transformers Deep Dive | Skip | -- |
| 8 | Generative AI | Skip | -- |
| 9 | Reinforcement Learning | Skip | -- |
| 10 | LLMs from Scratch | Skip | -- |
| 11 | LLM Engineering | Skip | -- |
| 12 | Multimodal AI | Skip | -- |
| 13 | Tools & Protocols | Skip | -- |
| 14 | Agent Engineering | Do | 55 |
| 15 | Autonomous Systems | Do | 20 |
| 16 | Multi-Agent & Swarms | Do | 28 |
| 17 | Infrastructure & Production | Do | 32 |
| 18 | Ethics, Safety & Alignment | Do | 31 |
| 19 | Capstone Projects | Do | 620 |

Total estimated hours (Review + Do): 786 across 6 phases.

## Progress log
| Date | Lesson | Quiz | Note |
|------|--------|------|------|
| 2026-09-17 | 14-agent-engineering/01-the-agent-loop | 2/2 | Explained observation feedback and hard execution limits; correctly predicted the five-turn budget cutoff. Practiced exception formatting with help on isinstance, str, and returning dictionaries; revisit these and framework budget configuration during recall. |
| 2026-09-19 | 14-agent-engineering/02-rewoo-plan-and-execute | 2/2 | Wrote a four-step plan and identified parallel branches; explained reference substitution, early return, dependency ordering, and blocked vs failed steps. Revisit full argument dictionaries vs substituted values and replanner inputs beyond status flags. Demo ran; lesson has no tests directory. |
| 2026-09-21 | 14-agent-engineering/03-reflexion-verbal-rl | 2/2 | Identified test-based scalar feedback and memory eviction; practiced actionable reflections and preserving task constraints. Revisit scripted actor counting entries vs model interpreting text, fresh empty memory with use_memory=False, and application-owned test execution. Demo ran successfully; no tests directory. |
| 2026-09-21 | 14-agent-engineering/04-tree-of-thoughts-lats | 2/2 | Solved (6-1)*4+4; explained exploration, noisy evaluators, application-owned correctness, and a three-attempt stopping rule. Revisit retaining highest-scoring beam candidates vs discarding branches and adding rollout rewards. Demo exited 0 but neither default search found a valid solution; no tests directory. Quiz cost multiplier was presented as the lesson estimate, not a universal rule. |
| 2026-09-22 | 14-agent-engineering/05-self-refine-and-critic | 2/2 | Chose deterministic tests for code verification, traced the three-attempt CRITIC repair, and explained framework vs application responsibilities. Revisit making critiques structurally compatible with refiners: human-readable feedback without the expected keyword left the scripted Self-Refine loop stuck. Demo ran successfully; no tests directory. |

| 2026-09-23 | 14-agent-engineering/06-tool-use-and-function-calling | 2/2 | Explained validation errors, correlation IDs, sequential dependencies, and account authorization before reads; wrote a read-only invoice-tool description. Revisit int("4.5") rejection versus int("4") conversion and string tool results. Demo exited 0; dispatch is sequential despite its label, timeout is unenforced, and no sandbox or tests directory is provided. Toolformer and a concrete production-library example remain follow-up topics. |

| 2026-09-28 | 14-agent-engineering/07-memory-virtual-context-memgpt | 2/2 | Distinguished core preferences from archival logs and proposed JSONL persistence; traced eviction, overlap scoring, and core replacement. Revisit top_k limits, quoted tool roles, and saving versus including retrieved evidence in the next model input; ultimately identified application ownership correctly. Demo exited 0 but only prints retrievals and has no model call. Compared documented Letta semantic-search API without running the service; final architecture question qualified as an analogy. |

| 2026-09-28 | 14-agent-engineering/08-memory-blocks-sleep-time-compute | 2/2 | Preserved general Python and project TypeScript preferences; traced append/version history, lossy summarization, and supplied contradiction matching. Revisit stale-write version checks versus merely recording versions, and verifying scope/meaning beyond block identifiers. Demo exited 0; sequential sleep pass invalidated one archival record but summarized no blocks, with no enforced limits or tests directory. Compared current Letta memory/dreaming docs without running the service; official V1 announcement dated October 2025 corrects lesson date. |

| 2026-09-28 | 14-agent-engineering/09-hybrid-memory-mem0 | 2/2 | Traced distinct KV keys, graph replacement errors for multi-valued relations, and application-owned user/session/agent filtering. Initially confused semantic search with graph traversal and recency with validity; ultimately explained that old unsuperseded facts remain current and superseded facts serve historical queries. Demo exited 0; combined search ignores graph validity, ranks an unrelated project first for a city query, and has incomplete scope enforcement; no tests directory. Compared current Mem0 SDK documentation without running it; toy fusion is not verified production internals. Qualified the stored quiz's re-embedding claim: unchanged text with the same model does not inherently improve retrieval. |

## Review queue
