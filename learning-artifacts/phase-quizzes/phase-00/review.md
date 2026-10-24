# Phase 00 review queue

Historical notes are preserved verbatim; some early remediation requests were superseded by later passes. Latest completion status is in [phase progress](progress.md).

- Phase 00 / Lesson 13 (initial 1/3; retake 2/3, lesson minimum met): Generators are single-use iterators; consumption exhausts them regardless of epoch number. `iter()` does not reset an exhausted generator. Recreate the generator from a reusable source for each epoch. Nested-list repetition shares inner list references; use a comprehension to create independent rows. Retake also missed plain assignment aliasing: `backup = weights` shares the list; `weights.copy()` copies only the outer list. Retake attempt 2 completed 2/3; generator reuse and mutable defaults answered correctly, while assignment aliasing still needs review.

- Phase 00 / Lesson 12 (quiz-based assessment, 2/3): `cProfile` measures function execution time (including cumulative time); `tracemalloc` tracks Python memory allocations. Choose the profiler to match the observed problem.

- Phase 00 / Lesson 10 (initial 1/3; retake 2/3, lesson minimum met): `nohup` can preserve a process after hangup, but does not provide terminal reattachment; `fg` cannot recover another shell's job from a new SSH session. Use a persistent tmux session for detach/reattach. Also review left-to-right redirection: `2>&1 > train.log` leaves stderr on the terminal; `> train.log 2>&1` sends both streams to the file. Retake attempt 2 completed 2/3; append-both-streams question was still missed. Trace each redirection left to right: `>> train.log` first, then `2>&1`.

- Phase 00 / Lesson 09 (quiz-based assessment, 2/3): Calculate nested split fractions against the remaining subset: 20% of 1000 gives 200 test rows; 12.5% of remaining 800 gives 100 validation rows; 700 training rows remain. Trace final validation/test variable assignments.

- Phase 00 / Lesson 07 (quiz-based assessment, 2/3): Inside a container, `localhost` addresses that same container. Reach a Compose peer using its service name and container port (`qdrant:6333`); host-published port `7333` serves host access.

- Phase 00 / Lesson 04 (initial 2/3; fresh retake 3/3, resolved in retake; keep for spaced recall): Missing `os.environ["KEY"]` raises `KeyError` before any HTTP request; distinguish indexing from `.get()` defaults and local setup errors from server authentication errors.
