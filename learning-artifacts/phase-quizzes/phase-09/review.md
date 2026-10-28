# Phase 09 — reinforcement-learning Review Summary

[All phases](../progress.md)

- Status: **Done / Passed**; passed on 2026-10-26; coverage: **12 lessons**.
- Initial score: **24/36**; final effective score: **31/36 (86.11%)**.
- Cumulative responses: 69, with 41 correct; **28 initial/retake mistakes** retained. Cumulative responses include retakes and are not the mastery-score denominator.
- Pass criteria: effective phase score ≥85% and final score ≥2/3 in every lesson; all criteria met. Completion basis: quiz-based mastery; implementation labs were not performed in this assessment.

## Weak points and review priorities

- Highest priority: L01 state sufficiency, Vπ/Qπ, Bellman returns, and the effective discount horizon 1/(1−γ); L03 full sampled returns in MC versus TD bootstrapping, first/every visits, and (s,a) deduplication. Both lessons merit spaced recall after multiple retakes.
- L03: increment the count before an incremental-mean update and restore chronological order after computing returns backward. Limited coverage still has sampling variance. Off-policy estimation must address behavior/target-policy differences and importance weights.
- L04: SARSA's actual-next-action target reflects exploration risk. L05: freeze the target network temporarily while training the online network; replay reduces temporal correlation. Terminal targets are y=r; nonterminal targets include r+γ max Qtarget.
- L07: A2C is synchronous and A3C asynchronous. L08: reduce update intensity when PPO KL/clip fraction is high. L09: check the sign of preferred-response weight updates. L11: a strict threshold comparison excludes equality.

## Lessons with mistakes and retake outcomes

Lessons with mistakes or retakes are listed below, along with any additional rows retained from the original ledger. Unlisted lessons scored 3/3 initially and finally. A final 3/3 indicates correction in a later assessment where applicable; retain those topics for spaced recall. Lessons at 2/3 remain review priorities.

| Lesson | Initial score | Final effective score / retake |
|---|---|---|
| [MDPs, States, Actions & Rewards](../../../phases/09-reinforcement-learning/01-mdps-states-actions-rewards/docs/en.md) | 1/3 | 2/3 (attempt 4) |
| [Monte Carlo Methods — Learning from Complete Episodes](../../../phases/09-reinforcement-learning/03-monte-carlo-methods/docs/en.md) | 1/3 | 3/3 (attempt 6) |
| [Temporal Difference — Q-Learning & SARSA](../../../phases/09-reinforcement-learning/04-q-learning-sarsa/docs/en.md) | 2/3 | 3/3 (attempt 2) |
| [Deep Q-Networks (DQN)](../../../phases/09-reinforcement-learning/05-dqn/docs/en.md) | 0/3 | 3/3 (attempt 3) |
| [Actor-Critic — A2C and A3C](../../../phases/09-reinforcement-learning/07-actor-critic-a2c-a3c/docs/en.md) | 2/3 | 2/3 |
| [Proximal Policy Optimization (PPO)](../../../phases/09-reinforcement-learning/08-ppo/docs/en.md) | 2/3 | 2/3 |
| [Reward Modeling & RLHF](../../../phases/09-reinforcement-learning/09-reward-modeling-rlhf/docs/en.md) | 2/3 | 2/3 |
| [Sim-to-Real Transfer](../../../phases/09-reinforcement-learning/11-sim-to-real-transfer/docs/en.md) | 2/3 | 2/3 |

## Condensed mistake records

Question IDs, prompts, selected wrong answers, correct answers, and explanations are retained. Other distractors, correct-only questions, and per-response score logs are omitted. Prompts and explanations retain their original English wording. These are historical initial/retake mistakes, not pending retake requirements.

### p09-l01-a1-q2

An inventory agent sees only current stock. Two histories lead to the same stock level but different next-day demand distributions because demand depends on the day of the week. Which change addresses this missing state information?

- Learner answer: B — Average the demand distributions and keep current stock as the entire state.
- Correct answer: C — Add the day of the week to the state alongside current stock.
- Explanation: The day of the week carries information about future demand that stock alone omits. Including it addresses the stated source of dependence on history.

### p09-l01-a1-q3

In the lesson’s GridWorld, what do these two calls return?

first = step((3, 2), "right")
second = step(first[0], "up")

Presented context: step returns (state, 0.0, True) immediately when starting at (3, 3); otherwise it clips movement to the 4x4 grid, returns -1.0, and sets done when the next state equals (3, 3). right=(0,1); up=(-1,0).

- Learner answer: A — first = ((3, 3), -1.0, True); second = ((2, 3), -1.0, False)
- Correct answer: D — first = ((3, 3), -1.0, True); second = ((3, 3), 0.0, True)
- Explanation: Entering the terminal cell still incurs the -1 step reward and sets done=True. A call starting at the terminal returns immediately with the same state, zero reward, and done=True.

### p09-l03-a1-q2

A deterministic policy never visits some state-action pairs, leaving their Monte Carlo Q estimates untouched. Which change best addresses this coverage problem during control?

- Learner answer: D — Replace sampled returns with the Bellman expectation over a known model.
- Correct answer: A — Use ε-greedy action selection so non-greedy actions are sampled.
- Explanation: ε-greedy exploration sometimes selects a random action, giving otherwise unvisited state-action pairs a chance to be sampled. Choice D assumes a known model and changes the method to dynamic programming.

### p09-l03-a1-q3

The lesson’s returns_from loop sweeps rewards backward with G = r + γG. For an episode with rewards [1, 2, 3] and γ = 0.5, which return list does it produce in chronological order?

- Learner answer: B — [3.0, 3.5, 2.75]
- Correct answer: C — [2.75, 3.5, 3.0]
- Explanation: Working backward: final return is 3; previous is 2 + 0.5×3 = 3.5; first is 1 + 0.5×3.5 = 2.75. The function reverses the collected backward-sweep results before returning.

### p09-l04-a1-q2

During training on cliff walking, exploration sometimes steps into the cliff. You want learned values to account for that continuing exploration risk. Which update should you choose?

- Learner answer: C — Q-learning, because it replaces sampled rewards with known transition probabilities.
- Correct answer: B — SARSA, because its target uses the next action selected by the exploring policy.
- Explanation: SARSA bootstraps from the action actually selected under the exploring policy, so its values reflect occasional exploratory cliff falls. Q-learning also uses sampled transitions; it does not require known transition probabilities.

### p09-l05-a1-q1

What is the purpose of DQN’s target network?

- Learner answer: C — It selects random exploratory actions while the online network remains greedy.
- Correct answer: B — It keeps bootstrap targets relatively stable while the online network trains.
- Explanation: The target network uses frozen weights for the next-state Q estimate and is periodically synced from the online network, making regression targets less volatile. Exploration comes from ε-greedy action selection.

### p09-l05-a1-q2

A DQN agent trains on consecutive, highly similar observations and its updates oscillate. Which change directly reduces correlation between training samples?

- Learner answer: B — Remove exploratory actions so the agent follows its current Q estimates.
- Correct answer: C — Store transitions and draw random minibatches from a replay buffer.
- Explanation: Experience replay samples past transitions in random minibatches, reducing temporal correlation between successive training examples. Removing exploration does not decorrelate sequential observations.

### p09-l05-a1-q3

In the lesson’s DQN train_step, a sampled transition has reward r=5 and done=True. The target network’s largest next-state Q estimate is 20, with γ=0.9. What training target y is used?

- Learner answer: C — 23, because reward and discounted next-state value are added.
- Correct answer: A — 5, because a terminal transition has no future-value term.
- Explanation: For done=True, the code sets y=r and skips the target-network estimate, so y=5.

### p09-l07-a1-q2

You have several parallel environments and a GPU that works best on batches. Which actor-critic setup matches that hardware and why?

- Learner answer: D — A2C, because each worker independently updates shared weights without waiting.
- Correct answer: C — A2C, because it batches synchronized environment rollouts for one update.
- Explanation: A2C gathers synchronous rollouts from parallel environments and makes a batched update, which suits GPU throughput. Independent asynchronous shared-weight updates describe A3C.

### p09-l08-a1-q2

During PPO training, the clip fraction stays near 0.6 and measured KL rises above the target. Which adjustment best follows the lesson’s diagnostics?

- Learner answer: A — Increase the number of epochs so each rollout gets more updates.
- Correct answer: B — Reduce the learning rate or the number of epochs per rollout.
- Explanation: A high clip fraction and excessive KL indicate policy drift on the reused rollout. Lowering learning rate or update epochs reduces that drift. Increasing epochs would typically increase drift.

### p09-l09-a1-q3

In rm_train_step, r_pos=2 and r_neg=2, so p=sigmoid(r_pos−r_neg)=0.5. For a token appearing once in y_pos and not in y_neg, with lr=0.1, how does its weight change?

- Learner answer: A — It decreases by 0.05.
- Correct answer: B — It increases by 0.05.
- Explanation: The positive-response loop adds lr×(1−p)×count = 0.1×0.5×1 = 0.05 to that token’s weight.

### p09-l11-a1-q3

In the lesson’s step function, slip happens when rng.random() < slip. If slip=0.4 and the sampled number is exactly 0.4, what happens to the requested action?

- Learner answer: B — It slips with a separate 0.4 probability after the sampled check.
- Correct answer: C — It stays requested, because 0.4 < 0.4 is false.
- Explanation: The comparison is strict: 0.4 < 0.4 is false, so the branch that substitutes a perpendicular action does not run.

### p09-l01-a2-q1

Under a fixed policy π, how does Qπ(s,a) differ from Vπ(s)?

- Learner answer: D — Qπ(s,a) is defined only for terminal states; Vπ(s) is defined elsewhere.
- Correct answer: A — Qπ(s,a) fixes the first action at a; Vπ(s) averages over actions chosen by π.
- Explanation: Qπ conditions on taking action a first, then following π; Vπ starts in state s and averages over the policy’s action choice. Both include future discounted return.

### p09-l01-a2-q2

A navigation agent’s current camera frame shows the same hallway on two visits, but its velocity differs and changes which turn is safe. What state change best restores the Markov property?

- Learner answer: A — Increase the reward for arriving safely, keeping the camera frame as the state.
- Correct answer: B — Add velocity information or a short frame history to the state representation.
- Explanation: The camera frame alone omits velocity that predicts future dynamics. Adding velocity or sufficient observation history makes the state more nearly sufficient. Reward changes do not add predictive information to state.

### p09-l01-a3-q1

What does the Bellman equation express about a state’s value under a policy?

- Learner answer: B — It equals the probability that the policy chooses its best action.
- Correct answer: C — It is expected immediate reward plus discounted successor-state value.
- Explanation: The Bellman relation decomposes expected return into the current reward and the discounted expected value of the next state under the policy.

### p09-l01-a3-q2

A continuing task pays reward +1 every step without a terminal state. If γ=1, which formulation change avoids an unbounded discounted return?

- Learner answer: C — Average the rewards over the last two steps without changing the horizon.
- Correct answer: B — Add a finite horizon or use a discount factor below 1.
- Explanation: With reward +1 forever and γ=1, the return sum diverges. A finite horizon or γ<1 makes this discounted-return formulation finite.

### p09-l01-a4-q1

If γ changes from 0.9 to 0.99 in the same continuing MDP, what happens to the approximate effective reward horizon?

- Learner answer: B — It stays near 10 steps because the policy is unchanged.
- Correct answer: D — It grows from about 10 steps to about 100 steps.
- Explanation: The effective horizon is roughly 1/(1−γ): γ=0.9 gives about 10 steps and γ=0.99 gives about 100.

### p09-l03-a2-q1

Why can Monte Carlo policy evaluation work without knowing the environment’s transition probabilities?

- Learner answer: A — It solves the Bellman equation by enumerating every possible next state.
- Correct answer: B — It averages returns observed after visits to states in sampled episodes.
- Explanation: Monte Carlo estimates expected return by sampling whole episodes and averaging observed returns; it need not enumerate or know transition probabilities.

### p09-l03-a2-q2

A Monte Carlo evaluator runs a policy in an environment where some episodes can loop indefinitely. What practical change lets it collect bounded rollouts while making the truncation explicit?

- Learner answer: C — Replace observed returns with exact Bellman expectations from a model.
- Correct answer: B — Stop after a maximum step count and report capped episodes separately.
- Explanation: Monte Carlo needs bounded episodes for usable returns. A max-step cap prevents endless rollouts, and tracking capped episodes makes the resulting truncation visible. Choice C requires a model and switches to dynamic programming.

### p09-l03-a2-q3

A state starts with V=2 and has count=3. The next first-visit return is G=6. After counts[s] += 1 and V[s] += (G−V[s])/counts[s], what is the new V?

- Learner answer: C — 4.0
- Correct answer: B — 3.0
- Explanation: The new count is 4, so the incremental update is 2 + (6−2)/4 = 3.

### p09-l03-a3-q1

When an episode visits the same state twice, how do first-visit and every-visit Monte Carlo evaluation differ?

- Learner answer: D — First-visit updates after each step; every-visit waits until the episode ends.
- Correct answer: A — First-visit uses only the first visit’s return; every-visit uses returns from both visits.
- Explanation: First-visit counts a state once per episode at its first occurrence; every-visit counts every occurrence and its following return.

### p09-l03-a3-q3

A first-visit evaluator sees trajectory states [s, t, s] with returns [5, 3, 1]. Its seen set starts empty and it skips a state already seen in this episode. Which return updates V(s)?

- Learner answer: A — Only 1, because the last visit is closest to episode end.
- Correct answer: D — Only 5, because the later visit is skipped after s is marked seen.
- Explanation: The first s is processed with return 5 and added to seen. When s appears again, the code continues without updating it.

### p09-l03-a4-q2

Off-policy Monte Carlo importance weights become extremely variable on long episodes because action-probability ratios multiply across steps. Which response does the lesson recommend?

- Learner answer: C — Drop importance weights while still evaluating the target policy from behavior-policy data.
- Correct answer: A — Use a per-decision weighted importance-sampling variant or switch to TD.
- Explanation: The lesson flags exploding trajectory-weight variance and recommends per-decision weighted importance sampling or a TD method. Dropping weights leaves the behavior-target policy mismatch uncorrected.

### p09-l03-a4-q3

In mc_control, seen stores (state, action) pairs. An episode visits (s,left), then (s,right), then (s,left), with following returns 5, 4, and 3. Which returns update Q in this episode?

- Learner answer: D — 5, 4, and 3, because all visits are counted.
- Correct answer: B — 5 and 4, because the repeated (s,left) pair is skipped.
- Explanation: The first (s,left) and first (s,right) are distinct pairs and both update Q. The second (s,left) is already in seen, so its return 3 is skipped.

### p09-l03-a5-q1

Why can Monte Carlo value estimates have high variance on long episodes compared with one-step TD estimates?

- Learner answer: D — Monte Carlo updates from a bootstrapped next-state value each step.
- Correct answer: B — Monte Carlo uses the full sampled future return, including distant random outcomes.
- Explanation: Monte Carlo waits for the entire observed return, so distant random outcomes affect the estimate; one-step TD bootstraps from a next-state estimate instead.

### p09-l03-a5-q2

A policy is evaluated from complete episodes, but one state was visited in only 8 of them. The lesson’s shipped evaluator requires at least 100 episodes per state before reporting a tabular estimate. What should the evaluator do?

- Learner answer: A — Report the estimate as reliable because 8 complete returns have no sampling variance.
- Correct answer: B — Increase sampling until that state has enough visits, or withhold its estimate.
- Explanation: With only 8 episode visits, the stated reporting threshold is unmet. Collect more coverage or do not report that state estimate as ready.

### p09-l05-a2-q2

A DQN learner keeps copying online weights into its target network after every gradient step, and its targets oscillate. Which adjustment directly restores the target network’s intended role?

- Learner answer: B — Freeze the online network and update only the target network.
- Correct answer: C — Copy online weights to the target only at spaced intervals.
- Explanation: The target network should hold weights fixed across many gradient steps, then periodically sync from the online network; copying every step removes that stabilizing lag. Freezing the online network would prevent Q learning.

### p09-l05-a2-q3

DQN train_step sees a nonterminal sample with r=1, γ=0.5, and target.forward(s_next)=[2, 6]. What bootstrap target y does the code compute?

- Learner answer: B — 3, from discounting the largest target Q value only.
- Correct answer: C — 4, from reward plus discounted largest target Q value.
- Explanation: The nonterminal target is r + γ×max(Q_target(next)) = 1 + 0.5×6 = 4.
