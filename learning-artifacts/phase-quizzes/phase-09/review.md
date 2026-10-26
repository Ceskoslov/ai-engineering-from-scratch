# Phase 09 review queue

Historical notes are preserved verbatim; some early remediation requests were superseded by later passes. Latest completion status is in [phase progress](progress.md).

No review items recorded.

- Lesson 01, p09-l01-a1-q2: chose averaging demand distributions rather than adding weekday to state. Review state sufficiency: averaging hides predictive context; include the relevant weekday information.

- Lesson 01, p09-l01-a1-q3: chose movement out of terminal. Trace the terminal early return: entering terminal costs -1, subsequent calls remain there with reward 0. Initial lesson score 1/3; fresh full-set retake required.

- Lesson 03, p09-l03-a1-q2: chose model-based Bellman expectation for a Monte Carlo control coverage problem. Review ε-greedy exploration when only sampled episodes are available.

- Lesson 03, p09-l03-a1-q3: reversed return order in backward sweep. Trace backward accumulation, then reverse to chronological order. Initial lesson score 1/3; fresh full-set retake required.

- Lesson 04, p09-l04-a1-q2: chose Q-learning based on an incorrect model requirement. Review SARSA on-policy next-action target versus Q-learning greedy target in cliff walking.

- Lesson 05, p09-l05-a1-q1: confused target network with exploration. Review frozen bootstrap targets versus ε-greedy action selection.

- Lesson 05, p09-l05-a1-q2: chose removing exploration for correlated sequential training data. Review replay-buffer random minibatches and temporal correlation.

- Lesson 05, p09-l05-a1-q3: included discounted next-state value after done=True. Review terminal target y=r; initial lesson score 0/3 requires fresh full-set retake.

- Lesson 07, p09-l07-a1-q2: confused A2C and A3C. A2C batches synchronized rollouts; A3C sends asynchronous worker gradients to shared parameters.

- Lesson 08, p09-l08-a1-q2: chose more PPO epochs despite high clip fraction and KL. Review reducing epochs or learning rate when policy drifts too far.

- Lesson 09, p09-l09-a1-q3: chose decreasing a token weight in the preferred response. Review the positive update sign: +lr(1−p)count.

- Lesson 11, p09-l11-a1-q3: missed strict inequality at slip threshold; equality leaves the action unchanged.

- Lesson 01 retake attempt 2, p09-l01-a2-q1: confused Qπ versus Vπ. Review fixed first action versus policy-averaged first action; both are defined at nonterminal states.

- Lesson 01 retake attempt 2, p09-l01-a2-q2: chose reward change for omitted velocity. Review state sufficiency: add velocity or observation history.

- Lesson 01 retake attempt 3, p09-l01-a3-q1: chose action-selection probability for Bellman state value; review one-step reward plus discounted successor value.

- Lesson 01 retake attempt 3, p09-l01-a3-q2: chose averaging recent rewards for infinite undiscounted sum. Review finite horizon or γ<1 for +1 continuing task.

- Lesson 01 retake attempt 4, p09-l01-a4-q1: kept horizon constant when γ rose; review 1/(1−γ).

- Lesson 03 retake attempt 2, p09-l03-a2-q1: confused Monte Carlo sampled-return averaging with dynamic programming model enumeration.

- Lesson 03 retake attempt 2, p09-l03-a2-q2: chose model-based Bellman expectations for nonterminating Monte Carlo rollouts; review max-step caps and reporting truncation.

- Lesson 03 retake attempt 2, p09-l03-a2-q3: did not increment count before averaging; new count 4 gives V=3. Attempt2 0/3.

- Lesson 03 retake attempt 3, p09-l03-a3-q1: confused visit counting with update timing. Both use completed returns; first-visit counts one occurrence, every-visit counts all.

- Lesson 03 retake attempt 3, p09-l03-a3-q3: chose last visit; first-visit code uses the first return 5 and skips later s. Attempt3 1/3.

- Lesson 03 retake attempt 4, p09-l03-a4-q2: chose dropping importance weights for high variance; review per-decision weighted IS or TD and behavior-target mismatch.

- Lesson 03 retake attempt 4, p09-l03-a4-q3: counted repeated state-action pair; first-visit MC control seen is keyed by (s,a), so only first occurrence of each pair updates Q.

- Lesson 03 retake attempt 5, p09-l03-a5-q1: attributed bootstrapped next-state value to MC; review full sampled return in MC versus one-step TD bootstrap.

- Lesson 03 retake attempt 5, p09-l03-a5-q2: treated eight MC samples as variance-free; review per-state coverage threshold and sampling variability.

- Lesson 05 retake attempt 2, p09-l05-a2-q2: proposed freezing online Q network; correct target-network lag freezes target temporarily while online trains.

- Lesson 05 retake attempt 2, p09-l05-a2-q3: omitted immediate reward from nonterminal target; r+γ max Qtarget = 4. Attempt2 1/3.

## Phase pass — 2026-10-26

Initial 24/36; cumulative 41/69 across initial and retake sets; effective latest complete sets 31/36 (86.11%). All lesson minima met. Residual review: Lesson 01 state/return formulation and discount horizon; Lesson 03 Monte Carlo versus TD, first-visit counting, and importance sampling; Lesson 04 exploration risk; Lesson 05 target-network timing and terminal bootstrap; Lessons 07, 08, 09, 11 individual missed items as detailed above. Credit is quiz-based; implementation labs were not performed in this assessment.
