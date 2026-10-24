# Phase 00 detailed quiz history

Archive: read only when an earlier question or attempt is relevant. [Phase progress](progress.md).

### Phase 00 / Lesson 01 / Attempt 1 (complete)

- p00-l01-concept-v1: beginner-route required checks passed; optional later runtime missing. Options: A install all runtimes first; B start route and install later tools when needed; C reinstall Python; D skip third-party-library lessons.
- Learner answer: B. Correct answer: B. Result: correct (1 point).
- Explanation: Readiness is scoped to the selected route; missing optional later tools do not block it.
- Completed score: 3/3. Lesson remains todo pending the whole phase passing.

- p00-l01-application-v1: NumPy imports in system Python but not in the activated course virtual environment. Options: A copy system executable; B add global site-packages to every project; C install globally; D install NumPy into the course virtual environment.
- Learner answer: D. Correct answer: D. Result: correct (1 point).
- Explanation: The virtual environment has its own installed packages; install NumPy into that environment and retry using its interpreter.

- p00-l01-code-v1: trace CUDA=False and MPS=True, with the NVIDIA print guarded by if cuda_available. Options: A CUDA False/MPS True only; B also NVIDIA; C both False; D NVIDIA only.
- Learner answer: A. Correct answer: A. Result: correct (1 point).
- Explanation: Both unconditional print calls execute; the False CUDA condition skips the NVIDIA print. CUDA and MPS availability are separate checks.

### Phase 00 / Lesson 02 / Attempt 1 (complete)

- p00-l02-concept-v1: distinguish add, commit, and push. Options: A local history/staging/upload; B staging/upload/local history; C staging/local history/upload; D upload/local history/staging.
- Learner answer: C. Correct answer: C. Result: correct (1 point).
- Explanation: git add stages changes, git commit records the staged snapshot in local history, and git push sends local commits to the remote.
- Completed score: 3/3. Lesson remains todo pending the whole phase passing.

- p00-l02-application-v1: preserve main while testing an optimizer. Options: A commit on main then branch; B branch, commit/test, merge if accepted; C stage on main and push without committing; D branch then edit/commit on main.
- Learner answer: B. Correct answer: B. Result: correct (1 point).
- Explanation: Commits on the experiment branch advance that branch while main stays at its previous commit until integration.

- p00-l02-code-v1: create experiment branch from main, edit/commit optimizer rate 0.01, then checkout main without merging. Options: A both branches/new rate; B main only/new rate; C neither/old rate; D experiment only/old rate.
- Learner answer: D. Correct answer: D. Result: correct (1 point).
- Explanation: The commit advances only the experiment branch. Checking out main restores its tracked version of optimizer.py, containing rate = 0.1; no merge occurred.

### Phase 00 / Lesson 03 / Attempt 1 (complete)

- p00-l03-concept-v1: fp16 weight estimate slightly below total VRAM; explain possible out-of-memory failure. Options: A fp16 uses four bytes; B weights must stay in system RAM; C activations/runtime consume additional VRAM; D CPU clock determines VRAM.
- Learner answer: C. Correct answer: C. Result: correct (1 point).
- Explanation: The 2-bytes-per-parameter estimate covers fp16 weights only. Activations, CUDA context, and other runtime allocations require additional memory.
- Completed score: 3/3. Lesson remains todo pending the whole phase passing.

- p00-l03-application-v1: estimate fp16 weight memory for 3 billion parameters at 2 bytes each using decimal GB. Options: A 6 GB weights plus additional runtime memory; B 3 GB weights plus additional memory; C 12 GB weights plus additional memory; D 6 GB complete workload.
- Learner answer: A. Correct answer: A. Result: correct (1 point).
- Explanation: 3 × 10^9 parameters × 2 bytes = 6 × 10^9 bytes = 6 GB for weights alone. Runtime allocations need additional space.

- p00-l03-code-v1: remove post-matmul CUDA synchronization from a host-timed benchmark. Options: A CPU execution; B includes prior GPU work; C changes arithmetic precision; D may stop timer before GPU completion.
- Learner answer: D. Correct answer: D. Result: correct (1 point).
- Explanation: CUDA work can execute asynchronously relative to the host. Synchronizing after the multiplication ensures the measured interval includes completion rather than only dispatch.

### Phase 00 / Lesson 04 / Attempt 1 (complete)

- p00-l04-concept-v1: SDK versus manually constructed HTTP for the same API. Options: A removes authentication; B handles request construction/response parsing; C runs model locally; D makes provider schemas identical.
- Learner answer: B. Correct answer: B. Result: correct (1 point).
- Explanation: The SDK wraps the underlying HTTP API and exposes convenient objects or methods. Authentication and provider-specific schemas still apply.
- Completed score: 2/3. Lesson meets the minimum lesson score; completion still awaits the whole phase passing. Review missing environment-variable access.

- p00-l04-application-v1: share an API example with teammates; real key never committed. Options: A Python constant removed before push; B tracked key config/private repo; C environment variable/ignored local .env/documentation; D Base64-encoded committed key.
- Learner answer: C. Correct answer: C. Result: correct (1 point).
- Explanation: Reading a key from the environment keeps it separate from shared source. A local .env containing secrets must be excluded from version control; teammates provide their own credentials.

- p00-l04-code-v1: ANTHROPIC_API_KEY absent; headers reads os.environ["ANTHROPIC_API_KEY"] before Request/urlopen. Options: A KeyError before request; B empty key then request; C automatic .env loading; D server supplies default key.
- Learner answer: B. Correct answer: A. Result: incorrect (0 points).
- Explanation: Indexing os.environ with a missing key raises KeyError immediately while constructing headers, before Request or urlopen executes. os.environ.get("ANTHROPIC_API_KEY", "") would return an empty string; the shown code does not use get.
- Review: phases/00-setup-and-tooling/04-apis-and-keys/docs/en.md, raw HTTP example; distinguish missing local configuration from a server-side authentication failure.

### Phase 00 / Lesson 05 / Attempt 1 (complete)

- p00-l05-concept-v1: threshold remains readable after deleting the cell that assigned it. Options: A restored from saved outputs; B permanent built-in; C persists in shared kernel until cleared/restarted; D separate processes reload deleted cell.
- Learner answer: C. Correct answer: C. Result: correct (1 point).
- Explanation: Deleting notebook source does not undo its prior execution. The running kernel retains the variable in memory until it is removed or the kernel restarts.
- Completed score: 3/3. Lesson remains todo pending the whole phase passing.

- p00-l05-application-v1: check a notebook that worked with custom execution order before sharing. Options: A save outputs; B restart kernel/run all top to bottom/check errors; C rerun custom order without restart; D clear outputs only.
- Learner answer: B. Correct answer: B. Result: correct (1 point).
- Explanation: Restarting removes hidden in-memory state. Running all cells in document order checks whether the saved source defines its dependencies in the required order.

- p00-l05-code-v1: fresh kernel, initialize losses once, append 0.5 twice, then print length/list. Options: A 1 [0.5]; B 0 []; C NameError; D 2 [0.5, 0.5].
- Learner answer: D. Correct answer: D. Result: correct (1 point).
- Explanation: Cell 2 mutates the same list on each execution. Cell 1 is not rerun, so the two appended entries both remain in the shared kernel.

### Phase 00 / Lesson 06 / Attempt 1 (complete)

- p00-l06-concept-v1: lockfile information beyond dependency version ranges. Options: A entire venv copy; B latest versions recalculated; C identical results on every machine guaranteed; D exact resolved direct/transitive dependency versions.
- Learner answer: D. Correct answer: D. Result: correct (1 point).
- Explanation: A lockfile records exact resolved dependency versions, including transitive dependencies. It supports repeatable package resolution without copying a machine-specific virtual environment or guaranteeing identical runtime outcomes.
- Completed score: 3/3. Lesson remains todo pending the whole phase passing.

- p00-l06-application-v1: projects require incompatible versions of the same Python package. Options: A separate venvs/lockfiles/matching interpreters; B reinstall globally on every switch; C commit venv to Git; D combine package paths with system Python.
- Learner answer: A. Correct answer: A. Result: correct (1 point).
- Explanation: Separate environments isolate incompatible dependencies; each project's lockfile records its resolved versions, and its matching interpreter uses those installed packages.

- p00-l06-code-v1: create .venv in Bash, then which python still outputs /usr/bin/python. Options: A creation activated environment; B activate with source and recheck; C environments cannot contain interpreters; D restart Bash required.
- Learner answer: B. Correct answer: B. Result: correct (1 point).
- Explanation: Creating an environment does not change the current shell's interpreter selection. Sourcing its activation script updates PATH so python resolves to the environment's interpreter.

### Phase 00 / Lesson 07 / Attempt 1 (complete)

- p00-l07-concept-v1: image/container relationship. Options: A read-only template/instance with writable layer; B running process/Dockerfile; C source-only image/host dependency installs; D guest OS/independent kernel.
- Learner answer: A. Correct answer: A. Result: correct (1 point).
- Explanation: An image provides the read-only template. A container adds runtime state and a writable layer; changes there do not modify the image.
- Completed score: 2/3. Lesson meets the minimum lesson score; completion still awaits the whole phase passing. Review container-local localhost and Compose service addressing.

- p00-l07-application-v1: preserve model downloads across image rebuilds/container removal. Options: A unmounted /tmp with --rm; B publish serving port; C persistent host directory bind-mounted at /models; D --gpus all.
- Learner answer: C. Correct answer: C. Result: correct (1 point).
- Explanation: Weights saved through the bind mount live in the host directory, independently of the container's writable layer or image rebuilds. Port publishing and GPU access do not provide file persistence.

- p00-l07-code-v1: ai-dev reaches qdrant on default Compose network; published host/container mapping 7333:6333. Options: A localhost:7333; B qdrant:7333; C localhost:6333; D qdrant:6333.
- Learner answer: C. Correct answer: D. Result: incorrect (0 points).
- Explanation: Inside ai-dev, localhost refers to ai-dev itself. Reach the other service by its Compose service name qdrant and its container listening port 6333. Published port 7333 is used from the host.
- Review: phases/00-setup-and-tooling/07-docker-for-ai/docs/en.md, Step 6: Compose service names and port mappings.

### Phase 00 / Lesson 08 / Attempt 1 (complete)

- p00-l08-concept-v1: static type checking versus format-on-save. Options: A type checker rewrites whitespace/formatter checks types; B type checker flags incompatible annotated types/formatter standardizes layout; C checker executes tests/formatter checks assertions; D checker guarantees results/formatter installs dependencies.
- Learner answer: B. Correct answer: B. Result: correct (1 point).
- Explanation: Static type checking reports potential type incompatibilities without proving full runtime correctness. Formatting standardizes code layout rather than checking program behavior.
- Completed score: 3/3. Lesson remains todo pending the whole phase passing.

- p00-l08-application-v1: edit remote GPU project via laptop VS Code UI and run commands on server. Options: A local run automatically forwards GPU; B formatter syncs files/runs remote training; C IP as local folder makes local Python use remote packages; D Remote SSH/remote project/environment/terminal.
- Learner answer: D. Correct answer: D. Result: correct (1 point).
- Explanation: Remote SSH keeps the editor interface local while working with files and executing project commands in the remote environment.

- p00-l08-code-v1: working formatter selected; effective formatOnSave=false. Options: A enable formatOnSave; B disable type checking; C disable output scrolling; D enable auto-save only.
- Learner answer: A. Correct answer: A. Result: correct (1 point).
- Explanation: editor.formatOnSave enables the selected formatter on saving. Auto-save controls when files are saved, not whether formatting is enabled.

### Phase 00 / Lesson 09 / Attempt 1 (complete)

- p00-l09-concept-v1: benefit of streaming data too large for a full local download. Options: A save examples in Git; B guaranteed arbitrary row access; C incremental processing without full local dataset first; D load entire dataset into GPU memory.
- Learner answer: C. Correct answer: C. Result: correct (1 point).
- Explanation: Streaming lets iteration fetch and process examples incrementally rather than requiring a complete local download before processing.
- Completed score: 2/3. Lesson meets the minimum lesson score; completion still awaits the whole phase passing. Review fractions of the remaining subset and validation/test assignments.

- p00-l09-application-v1: compact tabular storage with analytics reading a few columns. Options: A CSV for inherent column-only reads; B nested JSON smaller than compressed columns; C Python list literals columnar; D compressed columnar Parquet.
- Learner answer: D. Correct answer: D. Result: correct (1 point).
- Explanation: Parquet uses a columnar storage layout and compression, fitting analytical workloads that read selected columns.

- p00-l09-code-v1: 1000 rows; split off 20% as test, then 12.5% of remaining 800 as validation. Options (train/validation/test): A 800/100/100; B 700/100/200; C 675/125/200; D 700/200/100.
- Learner answer: initially C, revised to D before feedback. Final graded answer: D. Correct answer: B. Result: incorrect (0 points).
- Explanation: The first split reserves 200 test rows and leaves 800. The second takes 0.125 × 800 = 100 validation rows, leaving 700 training rows. Validation comes from train_val["test"], while final test is split["test"].
- Review: phases/00-setup-and-tooling/09-data-management/docs/en.md, Step 5: calculate the second fraction on the remaining subset and trace the final variable assignments.

### Phase 00 / Lesson 10 / Attempt 1 (complete)

- p00-l10-concept-v1: command1 | command2 with no other redirects. Options: A first stderr to second stdin; B second stdout to first stdin; C first stdout to second stdin; D both outputs to file.
- Learner answer: C. Correct answer: C. Result: correct (1 point).
- Explanation: A standard pipe connects the left command's stdout to the right command's stdin; stderr is separate unless explicitly redirected.
- Completed score: 1/3. Below lesson minimum 2/3; remediate and administer a fresh three-question set after the remaining first-pass lessons. Preserve this attempt.

- p00-l10-application-v1: persist remote training after SSH disconnect AND reattach to the same interactive terminal. Options: A foreground SSH process; B nohup plus fg from new session; C background plus inherited jobs in new shell; D named tmux session/detach/reattach.
- Learner answer: B. Correct answer: D. Result: incorrect (0 points).
- Explanation: nohup can keep the process running after a hangup, but does not provide a reattachable terminal. fg operates on jobs belonging to the current shell, not an earlier SSH shell. tmux supplies a persistent terminal session that can be detached and reattached.
- Review: phases/00-setup-and-tooling/10-terminal-and-shell/docs/en.md, Steps 3–4: process survival versus terminal reattachment.

- p00-l10-code-v1: stdout/stderr initially terminal, run python train.py 2>&1 > train.log. Options: A stdout file/stderr terminal; B both file; C stdout terminal/stderr file; D both terminal.
- Learner answer: B. Correct answer: A. Result: incorrect (0 points).
- Explanation: Bash applies redirects left to right. 2>&1 first duplicates stdout's current terminal destination onto stderr. > train.log then redirects only stdout to the file. To send both to the file, use > train.log 2>&1.
- Review: phases/00-setup-and-tooling/10-terminal-and-shell/docs/en.md, Step 2: stream redirection and order.

### Phase 00 / Lesson 11 / Attempt 1 (complete)

- p00-l11-concept-v1: chmod versus chown. Options: A ownership/permissions; B install packages/list processes; C permissions/ownership; D file contents/working directory.
- Learner answer: C. Correct answer: C. Result: correct (1 point).
- Explanation: chmod changes permission bits, while chown changes file ownership (owner and/or group).
- Completed score: 3/3. Lesson remains todo pending the whole phase passing.

- p00-l11-application-v1: owned valid shell script mode -rw-r--r--; direct execution denied; directory and mount allow execution. Options: A chmod 777; B chown root; C apt update; D chmod u+x.
- Learner answer: D. Correct answer: D. Result: correct (1 point).
- Explanation: chmod u+x adds execute permission for the owner while preserving other existing permission bits. It avoids unnecessary permissions or ownership changes.

- p00-l11-code-v1: initial config.yaml; mkdir experiment/backup; copy config into backup; move original into experiment. Options: A experiment/config.yaml and backup/config.yaml; B root config and backup; C root config and experiment/config; D experiment/config only.
- Learner answer: A. Correct answer: A. Result: correct (1 point).
- Explanation: cp creates a separate backup file. mv relocates the original to experiment/config.yaml, leaving no config.yaml at the starting directory root.

### Phase 00 / Lesson 12 / Attempt 1 (complete)

- p00-l12-concept-v1: identify functions accounting for cumulative execution time. Options: A tracemalloc; B cProfile; C chmod; D git log.
- Learner answer: A. Correct answer: B. Result: incorrect (0 points).
- Explanation: cProfile records function-call timing statistics, including cumulative time. tracemalloc tracks Python memory allocations rather than function execution time.
- Completed score: 2/3. Lesson meets the minimum lesson score; completion still awaits the whole phase passing. Review execution-time profiling versus memory tracking.
- Review: phases/00-setup-and-tooling/12-debugging-and-profiling/docs/en.md, Parts 5–6: execution-time profiling versus memory-allocation tracking.

- p00-l12-application-v1: profile reports 70% data loading/preprocessing, 20% GPU computation. Options: A buy faster GPU first; B disable validation automatically speeds loading; C enlarge model; D investigate data pipeline/try suitable parallelism/remeasure.
- Learner answer: D. Correct answer: D. Result: correct (1 point).
- Explanation: The measured dominant cost is the data pipeline. Investigate and benchmark changes there before assuming faster GPU computation will address the bottleneck.

- p00-l12-code-v1: intersection of train IDs {1,2,3,4} and test IDs {4,5,6}; print length and bool. Options: A 1 True/shared ID; B 1 False/no shared IDs; C 7 True/all shared; D 0 False/all leakage absent.
- Learner answer: A. Correct answer: A. Result: correct (1 point).
- Explanation: The intersection is {4}; its length is 1 and the nonempty set is truthy. The check detects this ID overlap; it is not a complete test for every type of leakage.

### Phase 00 / Lesson 13 / Attempt 1 (complete)

- p00-l13-concept-v1: reuse a fully consumed generator for another training epoch. Options: A exhausted single-use generator must be recreated; B epoch number automatically discards batches; C requires global copies; D iter resets exhausted object.
- Learner answer: B. Correct answer: A. Result: incorrect (0 points).
- Explanation: The generator is exhausted after its items are consumed; it has no knowledge of training epochs and iter() does not reset it. Create a new generator from the underlying reusable source for each epoch.
- Completed score: 1/3. Below lesson minimum 2/3; remediate and administer a fresh three-question set after Lesson 10 retake. Preserve this attempt.
- Review: phases/00-setup-and-tooling/13-python-for-ai-engineering/docs/en.md, Iterators and generators; distinguish a reusable iterable from an exhausted iterator.

- p00-l13-application-v1: avoid learning standardization statistics from test data. Options: A fit all rows before split; B fit training split only/apply same stats to both; C fit separately on train and test; D fit test/apply to train.
- Learner answer: B. Correct answer: B. Result: correct (1 point).
- Explanation: Split first and fit preprocessing only on training rows. Applying that fitted transformation to held-out rows keeps test data out of the learned statistics.

- p00-l13-code-v1: grid=[[0,0]]*2; mutate grid[0][1]=7. Options: A first row only; B second row only; C both rows [0,7]; D all values 7.
- Learner answer: A. Correct answer: C. Result: incorrect (0 points).
- Explanation: List repetition copies references to the same inner list. Both row references therefore expose the mutation. Use [[0, 0] for _ in range(2)] for independent rows.
- Review: phases/00-setup-and-tooling/13-python-for-ai-engineering/docs/en.md, Names refer to objects; Values, collections, and unpacking.

### Phase 00 first-pass summary

- Initial score: 31/39 (79.49%); below required 85% (at least 34/39).
- Completed lesson scores in order 01–13: 3, 3, 3, 2, 3, 3, 2, 3, 2, 1, 3, 2, 1 (each out of 3).
- Retake required: Lessons 10 and 13, each below minimum 2/3.
- Preserve original scores. Replace a lesson's effective score only when its full fresh three-question retake is complete; maintain separate cumulative response statistics.
- After both retakes, evaluate latest complete lesson sets against both phase pass requirements. If overall remains below 34/39, remediate additional missed-topic lessons with fresh sets.
- Phase and every lesson remain todo until the phase passes.
- Remediation delivered: nohup preserves a process after hangup but does not provide a reattachable terminal; tmux supports detach/reattach. Bash redirects left to right: use > log 2>&1 for both streams. Python list repetition shares inner references; use a comprehension for independent rows. Generators are exhausted after consumption and must be recreated for another pass.

### Phase 00 / Lesson 10 / Attempt 2 (complete)

- p00-l10-concept-v2: remote job must survive hangup, no interactive reattachment needed. Options: A background only; B foreground redirected; C nohup/background/log; D foreground then fg in new shell.
- Learner answer: C. Correct answer: C. Result: correct (1 point).
- Explanation: nohup makes the command ignore hangup; output redirection saves logs and & backgrounds the command. No terminal reattachment is required in this scenario.
- Completed retake score: 2/3. Effective lesson score is now 2/3, replacing initial 1/3. Latest complete phase score is 32/39; original attempt is preserved.

- p00-l10-application-v2: append both stdout and stderr to existing train.log. Options: A >> train.log 2>&1; B > train.log 2>&1; C 2>&1 >> train.log; D stdout append log/stderr errors.log.
- Learner answer: C. Correct answer: A. Result: incorrect (0 points).
- Explanation: >> first points stdout at the log in append mode; 2>&1 then duplicates that destination onto stderr. With the chosen reverse order, stderr retains stdout's earlier destination and is not appended to train.log.
- Review: redirection order remains a recurring difficulty; practice stream destinations step by step.

- p00-l10-code-v2: Python writes loss line to stdout and warning to stderr; stderr redirected to errors.log; stdout piped through grep loss into selected.log. Options: A both selected; B both errors; C swapped lines; D loss selected/warning errors.
- Learner answer: D. Correct answer: D. Result: correct (1 point).
- Explanation: The separate stderr redirect captures the warning. The pipe carries stdout to grep, which selects the loss line and writes it to selected.log.

### Phase 00 / Lesson 13 / Attempt 2 (complete)

Remediation: names refer to objects; assignment does not copy a list. Use a new generator object for each pass over a reusable source. Mutable default arguments persist across calls unless a new object is created inside the function.

- p00-l13-concept-v2: backup = weights for a list. Options: A independent copy; B same list/mutations visible through both names; C makes immutable; D copy-on-write.
- Learner answer: A. Correct answer: B. Result: incorrect (0 points).
- Explanation: Assignment binds a second name to the same object. Use weights.copy() or list(weights) for an independent outer list; nested mutable contents still need separate copying when independence is required.
- Completed retake score: 2/3. Effective lesson score is now 2/3, replacing initial 1/3. Latest complete phase score is 33/39; original attempt is preserved.
- Recurring difficulty: assignment versus copying and shared nested-list references.

- p00-l13-application-v2: reusable rows list; make_batches returns a fresh single-use generator. Options: A reuse one generator; B call iter on same generator; C call make_batches inside each epoch; D call list on same generator each epoch.
- Learner answer: C. Correct answer: C. Result: correct (1 point).
- Explanation: Calling the generator factory within each epoch creates a fresh iterator over the reusable source. Reusing, wrapping with iter, or converting an already exhausted generator does not reset it.

- p00-l13-code-v2: record with default history=[] called with start, then finish and printed. Options: A finish only; B start and finish; C start only; D empty.
- Learner answer: B. Correct answer: B. Result: correct (1 point).
- Explanation: The default list is created once at function definition and reused by both calls, so it accumulates both values.

### Phase 00 / Lesson 04 / Attempt 2 (complete)

Reason: all lesson minima are met, but the phase total is 33/39, below 34/39. Select the earliest 2/3 lesson with a missed topic. Remediation: os.environ["KEY"] raises KeyError locally when missing, before HTTP is sent; a received authentication error is a server response to an actual request. Preserve initial 2/3 until the full fresh set is complete.

- p00-l04-concept-v2: program sent request and received HTTP 401 reporting invalid key. Options: A local KeyError before sending; B no response/network disconnected; C server rejected authentication; D 401 model output/success.
- Learner answer: C. Correct answer: C. Result: correct (1 point).
- Explanation: A received authentication-error response establishes that a request reached the server, which rejected the credentials. It differs from a local configuration exception before transmission.
- Completed retake score: 3/3. Effective lesson score is now 3/3, replacing initial 2/3. Latest complete phase score is 34/39; original attempt is preserved.

- p00-l04-application-v2: stop clearly for absent API key before network call. Options: A get empty string and always send; B retrieve/check nonempty/stop clearly if missing; C hardcoded real key; D retry indefinitely.
- Learner answer: B. Correct answer: B. Result: correct (1 point).
- Explanation: Explicit configuration validation can stop locally with a useful message rather than sending a request with missing credentials.

- p00-l04-code-v2: absent dictionary key accessed with indexing in try/except, then get with empty-string default and repr. Options: A indexed/None; B missing/None; C indexed/empty string; D missing/empty string.
- Learner answer: D. Correct answer: D. Result: correct (1 point).
- Explanation: Indexing raises KeyError and enters the handler; get returns the supplied empty-string default, whose repr is two quotes.

### Phase 00 mastery completion — 2026-10-23

- Passed: latest complete sets 34/39 (87.18%), exceeding 85%; minimum per lesson 2/3 met for all 13 lessons.
- Initial first pass: 31/39. Completed retakes: Lesson 10 2/3, Lesson 13 2/3, Lesson 04 3/3. Latest complete lesson scores (01–13): 3,3,3,3,3,3,2,3,2,2,3,2,2.
- All attempts preserved; 38 correct across 48 cumulative scored responses, separate from the effective mastery score.
- Phase 00 and all 13 lessons marked done; one normal Progress log entry per lesson added to LEARNING.md. Completion basis is quiz-based mastery, not implementation-lab completion.
- Residual review retained: container addressing, nested split fractions, shell redirection order, timing versus allocation profilers, list aliasing.
- Next phase: 01 Math Foundations, 22 lessons, 66 initial questions.

