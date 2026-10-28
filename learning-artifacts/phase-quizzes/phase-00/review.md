# Phase 00 — setup-and-tooling Review Summary

[All phases](../progress.md)

- Status: **Done / Passed**; passed on 2026-10-23; coverage: **13 lessons**.
- Initial score: **31/39**; final effective score: **34/39 (87.18%)**.
- Cumulative responses: 48, with 38 correct; **10 initial/retake mistakes** retained. Cumulative responses include retakes and are not the mastery-score denominator.
- Pass criteria: effective phase score ≥85% and final score ≥2/3 in every lesson; all criteria met. Completion basis: quiz-based mastery; implementation labs were not performed in this assessment.

## Weak points and review priorities

- Prioritize L10 shell redirections evaluated from left to right, and L13 assignment aliasing, shallow copies, and independent nested lists. Both lessons remained at 2/3 after retakes.
- L07: localhost inside a container refers to that container; reach a Compose peer through its service name and container port. L09: apply a second split fraction to the remaining subset. L12: distinguish execution-time profiling from allocation tracking.
- L04: indexing a missing environment variable raises KeyError before any HTTP request; the retake reached 3/3, so retain this for spaced recall. Recreate exhausted generators from a reusable source.

## Lessons with mistakes and retake outcomes

Lessons with mistakes or retakes are listed below, along with any additional rows retained from the original ledger. Unlisted lessons scored 3/3 initially and finally. A final 3/3 indicates correction in a later assessment where applicable; retain those topics for spaced recall. Lessons at 2/3 remain review priorities.

| Lesson | Initial score | Final effective score / retake |
|---|---|---|
| [APIs & Keys](../../../phases/00-setup-and-tooling/04-apis-and-keys/docs/en.md) | 2/3 | 3/3 (attempt 2) |
| [Docker for AI](../../../phases/00-setup-and-tooling/07-docker-for-ai/docs/en.md) | 2/3 | 2/3 |
| [Data Management](../../../phases/00-setup-and-tooling/09-data-management/docs/en.md) | 2/3 | 2/3 |
| [Terminal & Shell](../../../phases/00-setup-and-tooling/10-terminal-and-shell/docs/en.md) | 1/3 | 2/3 (attempt 2) |
| [Debugging and Profiling](../../../phases/00-setup-and-tooling/12-debugging-and-profiling/docs/en.md) | 2/3 | 2/3 |
| [Python for AI Engineering](../../../phases/00-setup-and-tooling/13-python-for-ai-engineering/docs/en.md) | 1/3 | 2/3 (attempt 2) |

## Condensed mistake records

Question IDs, prompts, selected wrong answers, correct answers, and explanations are retained. Other distractors, correct-only questions, and per-response score logs are omitted. Prompts and explanations retain their original English wording. These are historical initial/retake mistakes, not pending retake requirements.

### p00-l04-code-v1

ANTHROPIC_API_KEY absent; headers reads os.environ["ANTHROPIC_API_KEY"] before Request/urlopen.

- Learner answer: B — empty key then request
- Correct answer: A — KeyError before request
- Explanation: Indexing os.environ with a missing key raises KeyError immediately while constructing headers, before Request or urlopen executes. os.environ.get("ANTHROPIC_API_KEY", "") would return an empty string; the shown code does not use get.

### p00-l07-code-v1

ai-dev reaches qdrant on default Compose network; published host/container mapping 7333:6333.

- Learner answer: C — localhost:6333
- Correct answer: D — qdrant:6333.
- Explanation: Inside ai-dev, localhost refers to ai-dev itself. Reach the other service by its Compose service name qdrant and its container listening port 6333. Published port 7333 is used from the host.

### p00-l09-code-v1

1000 rows; split off 20% as test, then 12.5% of remaining 800 as validation.

- Learner answer: D — 700/200/100.
- Correct answer: B — 700/100/200
- Explanation: The first split reserves 200 test rows and leaves 800. The second takes 0.125 × 800 = 100 validation rows, leaving 700 training rows. Validation comes from train_val["test"], while final test is split["test"].

### p00-l10-application-v1

persist remote training after SSH disconnect AND reattach to the same interactive terminal.

- Learner answer: B — nohup plus fg from new session
- Correct answer: D — named tmux session/detach/reattach.
- Explanation: nohup can keep the process running after a hangup, but does not provide a reattachable terminal. fg operates on jobs belonging to the current shell, not an earlier SSH shell. tmux supplies a persistent terminal session that can be detached and reattached.

### p00-l10-code-v1

stdout/stderr initially terminal, run python train.py 2>&1 > train.log.

- Learner answer: B — both file
- Correct answer: A — stdout file/stderr terminal
- Explanation: Bash applies redirects left to right. 2>&1 first duplicates stdout's current terminal destination onto stderr. > train.log then redirects only stdout to the file. To send both to the file, use > train.log 2>&1.

### p00-l12-concept-v1

identify functions accounting for cumulative execution time.

- Learner answer: A — tracemalloc
- Correct answer: B — cProfile
- Explanation: cProfile records function-call timing statistics, including cumulative time. tracemalloc tracks Python memory allocations rather than function execution time.

### p00-l13-concept-v1

reuse a fully consumed generator for another training epoch.

- Learner answer: B — epoch number automatically discards batches
- Correct answer: A — exhausted single-use generator must be recreated
- Explanation: The generator is exhausted after its items are consumed; it has no knowledge of training epochs and iter() does not reset it. Create a new generator from the underlying reusable source for each epoch.

### p00-l13-code-v1

grid=[[0,0]]*2; mutate grid[0][1]=7.

- Learner answer: A — first row only
- Correct answer: C — both rows [0,7]
- Explanation: List repetition copies references to the same inner list. Both row references therefore expose the mutation. Use [[0, 0] for _ in range(2)] for independent rows.

### p00-l10-application-v2

append both stdout and stderr to existing train.log.

- Learner answer: C — 2>&1 >> train.log
- Correct answer: A — >> train.log 2>&1
- Explanation: >> first points stdout at the log in append mode; 2>&1 then duplicates that destination onto stderr. With the chosen reverse order, stderr retains stdout's earlier destination and is not appended to train.log.

### p00-l13-concept-v2

backup = weights for a list.

- Learner answer: A — independent copy
- Correct answer: B — same list/mutations visible through both names
- Explanation: Assignment binds a second name to the same object. Use weights.copy() or list(weights) for an independent outer list; nested mutable contents still need separate copying when independence is required.
