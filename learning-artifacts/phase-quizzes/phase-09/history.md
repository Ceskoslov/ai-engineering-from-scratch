# Phase 09 detailed quiz history

Archive: read only when an earlier question or attempt is relevant. [Phase progress](progress.md).

No questions presented yet.


### p09-l01-a1-q1 — 2026-10-26

What does the Markov property require of an MDP state representation?

A) The next state must be uniquely determined by the current state and action.
B) The current state and action must contain all history relevant to the next-state distribution.
C) The policy must assign equal probability to every available action in the current state.
D) The immediate reward must depend only on the action, regardless of the current state.

Learner answer: B
Correct answer: B
Result: correct
Explanation: Given the current state and action, earlier history adds no information about the next-state distribution. Transitions may still be stochastic.


### p09-l01-a1-q2 — 2026-10-26

An inventory agent sees only current stock. Two histories lead to the same stock level but different next-day demand distributions because demand depends on the day of the week. Which change addresses this missing state information?

A) Lower the discount factor while keeping current stock as the entire state.
B) Average the demand distributions and keep current stock as the entire state.
C) Add the day of the week to the state alongside current stock.
D) Increase the reward for sales while keeping current stock as the entire state.

Learner answer: B
Correct answer: C
Result: incorrect
Explanation: The day of the week carries information about future demand that stock alone omits. Including it addresses the stated source of dependence on history.


### p09-l01-a1-q3 — 2026-10-26

In the lesson’s GridWorld, what do these two calls return?

first = step((3, 2), "right")
second = step(first[0], "up")

Presented context: step returns (state, 0.0, True) immediately when starting at (3, 3); otherwise it clips movement to the 4x4 grid, returns -1.0, and sets done when the next state equals (3, 3). right=(0,1); up=(-1,0).

A) first = ((3, 3), -1.0, True); second = ((2, 3), -1.0, False)
B) first = ((3, 3), 0.0, True); second = ((3, 3), 0.0, True)
C) first = ((3, 3), -1.0, False); second = ((2, 3), -1.0, False)
D) first = ((3, 3), -1.0, True); second = ((3, 3), 0.0, True)

Learner answer: A
Correct answer: D
Result: incorrect
Explanation: Entering the terminal cell still incurs the -1 step reward and sets done=True. A call starting at the terminal returns immediately with the same state, zero reward, and done=True.

Lesson 01 initial complete set: 1/3. Full three-question remediation required after initial phase coverage.


### p09-l02-a1-q1 — 2026-10-26

Which statement correctly distinguishes policy iteration from value iteration?

A) Policy iteration evaluates a policy then improves it; value iteration repeatedly applies a Bellman optimality backup.
B) Policy iteration requires a known model; value iteration learns only from sampled episodes without a model.
C) Policy iteration maximizes only immediate rewards; value iteration also considers discounted future rewards.
D) Policy iteration updates values once per policy; value iteration fully evaluates each policy before changing it.

Learner answer: A
Correct answer: A
Result: correct
Explanation: Policy iteration alternates policy evaluation and greedy improvement. Value iteration combines these through repeated max-over-actions Bellman backups without fully evaluating a policy each time.


### p09-l02-a1-q2 — 2026-10-26

In a discounted tabular MDP, two actions have equal expected return in one state. Policy iteration keeps switching between them despite unchanged values. Which change directly addresses this instability?

A) Increase the discount factor until one action becomes strictly better.
B) Stop evaluation when the average value change is small instead of the maximum.
C) Choose randomly between tied actions at every improvement step.
D) Use a fixed action ordering to break ties consistently at every improvement step.

Learner answer: D
Correct answer: D
Result: correct
Explanation: A stable tie-break prevents equally good actions from alternating across improvement steps, allowing the policy-stability check to succeed without changing the objective.


### p09-l02-a1-q3 — 2026-10-26

A value-iteration loop starts with V(s)=0. One nonterminal state has two actions: action left gives reward -1 then enters a terminal with V=0; action right gives reward -1 then returns to the same state. With γ=0.9, what is V(s) after one Bellman optimality backup?

A) 0, because both successor values start at zero.
B) -0.9, because the reward is discounted on the first step.
C) -1, because each action gives -1 and its successor currently has value zero.
D) -1.9, because the backup adds the rewards from both available actions.

Learner answer: C
Correct answer: C
Result: correct
Explanation: The backup computes max_a [r + γ V(next)]. Both actions yield -1 + 0.9×0 = -1 on the first sweep.

Lesson 02 initial complete set: 3/3.


### p09-l03-a1-q1 — 2026-10-26

What does first-visit Monte Carlo evaluation use to update the value of a state?

A) The one-step reward plus a bootstrapped estimate of the next state’s value.
B) The model’s expected reward and transition probabilities for every action.
C) The full observed return following the state’s first visit in each episode.
D) The full observed return following every visit to the state in each episode.

Learner answer: C
Correct answer: C
Result: correct
Explanation: First-visit MC averages complete observed returns following only the first occurrence of a state in each episode. It does not use a model or bootstrap from an estimated next-state value.


### p09-l03-a1-q2 — 2026-10-26

A deterministic policy never visits some state-action pairs, leaving their Monte Carlo Q estimates untouched. Which change best addresses this coverage problem during control?

A) Use ε-greedy action selection so non-greedy actions are sampled.
B) Use a smaller discount factor so unseen actions have lower value.
C) Average only the first return from each state in every episode.
D) Replace sampled returns with the Bellman expectation over a known model.

Learner answer: D
Correct answer: A
Result: incorrect
Explanation: ε-greedy exploration sometimes selects a random action, giving otherwise unvisited state-action pairs a chance to be sampled. Choice D assumes a known model and changes the method to dynamic programming.


### p09-l03-a1-q3 — 2026-10-26

The lesson’s returns_from loop sweeps rewards backward with G = r + γG. For an episode with rewards [1, 2, 3] and γ = 0.5, which return list does it produce in chronological order?

A) [1.0, 2.0, 3.0]
B) [3.0, 3.5, 2.75]
C) [2.75, 3.5, 3.0]
D) [4.5, 3.5, 3.0]

Learner answer: B
Correct answer: C
Result: incorrect
Explanation: Working backward: final return is 3; previous is 2 + 0.5×3 = 3.5; first is 1 + 0.5×3.5 = 2.75. The function reverses the collected backward-sweep results before returning.

Lesson 03 initial complete set: 1/3. Full three-question remediation required after initial phase coverage.


### p09-l04-a1-q1 — 2026-10-26

Why does Q-learning use max over next-state action values while SARSA uses the value of the action actually selected next?

A) Q-learning estimates the greedy target policy; SARSA evaluates the behavior policy that still explores.
B) Q-learning requires known transitions; SARSA estimates transitions from sampled episodes.
C) Q-learning removes discounting; SARSA discounts rewards according to the chosen action.
D) Q-learning averages all actions; SARSA selects the action with highest estimated value.

Learner answer: A
Correct answer: A
Result: correct
Explanation: Q-learning bootstraps toward the greedy next action even while behavior explores; SARSA bootstraps from the next action actually chosen by its current policy.


### p09-l04-a1-q2 — 2026-10-26

During training on cliff walking, exploration sometimes steps into the cliff. You want learned values to account for that continuing exploration risk. Which update should you choose?

A) Q-learning, because its max target includes the random action taken next.
B) SARSA, because its target uses the next action selected by the exploring policy.
C) Q-learning, because it replaces sampled rewards with known transition probabilities.
D) SARSA, because it ignores future action values when a cliff is nearby.

Learner answer: C
Correct answer: B
Result: incorrect
Explanation: SARSA bootstraps from the action actually selected under the exploring policy, so its values reflect occasional exploratory cliff falls. Q-learning also uses sampled transitions; it does not require known transition probabilities.


### p09-l04-a1-q3 — 2026-10-26

A nonterminal Q-learning update has Q(s,a)=2, reward r=1, γ=0.5, α=0.25, and next-state action values [4, 0]. What is the updated Q(s,a)?

A) 1.75
B) 2.00
C) 2.25
D) 3.00

Learner answer: C
Correct answer: C
Result: correct
Explanation: The target is 1 + 0.5×max(4,0) = 3. The update is 2 + 0.25×(3−2) = 2.25.

Lesson 04 initial complete set: 2/3.


### p09-l05-a1-q1 — 2026-10-26

What is the purpose of DQN’s target network?

A) It stores older transitions so each minibatch has independent samples.
B) It keeps bootstrap targets relatively stable while the online network trains.
C) It selects random exploratory actions while the online network remains greedy.
D) It clips rewards so different games produce similar gradient magnitudes.

Learner answer: C
Correct answer: B
Result: incorrect
Explanation: The target network uses frozen weights for the next-state Q estimate and is periodically synced from the online network, making regression targets less volatile. Exploration comes from ε-greedy action selection.


### p09-l05-a1-q2 — 2026-10-26

A DQN agent trains on consecutive, highly similar observations and its updates oscillate. Which change directly reduces correlation between training samples?

A) Copy online weights into the target network after every gradient step.
B) Remove exploratory actions so the agent follows its current Q estimates.
C) Store transitions and draw random minibatches from a replay buffer.
D) Raise the discount factor so later rewards affect each target more.

Learner answer: B
Correct answer: C
Result: incorrect
Explanation: Experience replay samples past transitions in random minibatches, reducing temporal correlation between successive training examples. Removing exploration does not decorrelate sequential observations.


### p09-l05-a1-q3 — 2026-10-26

In the lesson’s DQN train_step, a sampled transition has reward r=5 and done=True. The target network’s largest next-state Q estimate is 20, with γ=0.9. What training target y is used?

A) 5, because a terminal transition has no future-value term.
B) 18, because only the discounted next-state estimate is used.
C) 23, because reward and discounted next-state value are added.
D) 25, because reward and the full next-state value are added.

Learner answer: C
Correct answer: A
Result: incorrect
Explanation: For done=True, the code sets y=r and skips the target-network estimate, so y=5.

Lesson 05 initial complete set: 0/3. Full three-question remediation required after initial phase coverage.


### p09-l06-a1-q1 — 2026-10-26

In REINFORCE, why can a baseline that depends on the state but not the selected action be subtracted from the return?

A) It turns the policy update into an exact Bellman optimality backup.
B) It removes the need to sample complete trajectories for the update.
C) It changes the expected gradient so actions with low return are ignored.
D) It can reduce gradient variance without changing the expected gradient.

Learner answer: D
Correct answer: D
Result: correct
Explanation: An action-independent baseline has zero expected product with the score-function gradient, so subtracting it preserves the expected policy gradient while reducing variance.


### p09-l06-a1-q2 — 2026-10-26

A REINFORCE agent receives a positive reward early in an episode and a negative reward much later. You want each action update to depend only on rewards that follow that action. Which change should you make?

A) Use reward-to-go from each action’s time step as its gradient weight.
B) Use the full episode return as the weight for every action in the episode.
C) Use only the immediate reward at each step and discard later rewards.
D) Use the largest action probability as the weight for every action.

Learner answer: A
Correct answer: A
Result: correct
Explanation: Reward-to-go weights each log-policy gradient by discounted rewards from that action onward, excluding earlier rewards that the action could not have caused.


### p09-l06-a1-q3 — 2026-10-26

In reinforce_step, a two-action policy assigns probabilities [0.25, 0.75] and selects action 0. What is grad_log_pi_a immediately after grad_log_pi_a = [-p for p in probs]; grad_log_pi_a[a] += 1.0?

A) [0.25, 0.75]
B) [-0.25, -0.75]
C) [0.75, -0.75]
D) [1.25, -0.75]

Learner answer: C
Correct answer: C
Result: correct
Explanation: Negating probabilities gives [-0.25,-0.75]; adding 1 to the chosen action 0 yields [0.75,-0.75].

Lesson 06 initial complete set: 3/3.


### p09-l07-a1-q1 — 2026-10-26

In actor-critic learning, what does the critic estimate for the actor?

A) The probability of each action under the current policy.
B) The expected return from a state, used to form an advantage.
C) The transition probabilities for all possible next states.
D) The entropy of each action distribution, used as the reward.

Learner answer: B
Correct answer: B
Result: correct
Explanation: The critic estimates V(s), which is subtracted from a return or TD target to estimate how much better or worse an action was than expected.


### p09-l07-a1-q2 — 2026-10-26

You have several parallel environments and a GPU that works best on batches. Which actor-critic setup matches that hardware and why?

A) A3C, because asynchronous workers each send gradients to one shared model.
B) A3C, because it reuses a replay buffer across many update epochs.
C) A2C, because it batches synchronized environment rollouts for one update.
D) A2C, because each worker independently updates shared weights without waiting.

Learner answer: D
Correct answer: C
Result: incorrect
Explanation: A2C gathers synchronous rollouts from parallel environments and makes a batched update, which suits GPU throughput. Independent asynchronous shared-weight updates describe A3C.


### p09-l07-a1-q3 — 2026-10-26

In compute_advantages with rewards=[1], values=[2], gamma=0.5, lam=0.9, and last_value=4, what are the returned advantages and returns?

A) advantages=[-1.0], returns=[1.0]
B) advantages=[1.0], returns=[3.0]
C) advantages=[2.0], returns=[4.0]
D) advantages=[3.0], returns=[5.0]

Learner answer: B
Correct answer: B
Result: correct
Explanation: The single TD residual is 1 + 0.5×4 − 2 = 1. With no later residual, GAE is 1 and the critic target return is 1 + V(s)=3.

Lesson 07 initial complete set: 2/3.


### p09-l08-a1-q1 — 2026-10-26

What problem does PPO’s clipped likelihood-ratio objective address when it reuses a rollout for several update epochs?

A) It removes the need to estimate advantages from the rollout.
B) It makes transition probabilities available to the policy optimizer.
C) It limits incentive to move action probabilities too far from the collecting policy.
D) It lets the same rollout train indefinitely without any policy drift.

Learner answer: C
Correct answer: C
Result: correct
Explanation: The clipped surrogate caps the beneficial incentive once the new-to-old action likelihood ratio passes the clip range, helping limit policy drift during data reuse.


### p09-l08-a1-q2 — 2026-10-26

During PPO training, the clip fraction stays near 0.6 and measured KL rises above the target. Which adjustment best follows the lesson’s diagnostics?

A) Increase the number of epochs so each rollout gets more updates.
B) Reduce the learning rate or the number of epochs per rollout.
C) Increase the clip coefficient so more ratios remain unclipped.
D) Stop computing advantages and optimize reward directly.

Learner answer: A
Correct answer: B
Result: incorrect
Explanation: A high clip fraction and excessive KL indicate policy drift on the reused rollout. Lowering learning rate or update epochs reduces that drift. Increasing epochs would typically increase drift.


### p09-l08-a1-q3 — 2026-10-26

For one PPO sample, advantage A=2, old action probability=0.2, new probability=0.3, and ε=0.2. What is min(rA, clip(r, 0.8, 1.2)A)?

A) 1.6
B) 2.0
C) 2.4
D) 3.0

Learner answer: C
Correct answer: C
Result: correct
Explanation: The ratio is 0.3/0.2=1.5. The unclipped term is 3.0, the clipped term is 1.2×2=2.4, and PPO takes the minimum.

Lesson 08 initial complete set: 2/3.


### p09-l09-a1-q1 — 2026-10-26

What does the Bradley–Terry reward-model loss encourage for a human-preferred response pair?

A) Equal scores for both responses to prevent preference overfitting.
B) A higher scalar score for the preferred response than for the rejected one.
C) A larger KL divergence between the policy and its SFT reference.
D) A higher probability for every token in both responses under the policy.

Learner answer: B
Correct answer: B
Result: correct
Explanation: The pairwise logistic loss uses the difference R(preferred)−R(rejected), so minimizing it pushes the preferred response’s score above the rejected response’s score.


### p09-l09-a1-q2 — 2026-10-26

An RLHF policy’s reward-model score keeps rising, but blind human evaluation says its responses are getting worse and KL from the SFT reference is growing. Which response best addresses the lesson’s diagnosis?

A) Increase PPO epochs so the policy exploits the reward model more strongly.
B) Discard the reference policy and optimize only the reward-model score.
C) Keep training until reward and human evaluation eventually converge.
D) Stop or slow optimization, strengthen the KL penalty, and inspect reward-model failures.

Learner answer: D
Correct answer: D
Result: correct
Explanation: Rising RM reward alongside falling human quality is reward hacking. Stopping or slowing optimization, increasing the KL penalty, and examining reward-model errors address the drift.


### p09-l09-a1-q3 — 2026-10-26

In rm_train_step, r_pos=2 and r_neg=2, so p=sigmoid(r_pos−r_neg)=0.5. For a token appearing once in y_pos and not in y_neg, with lr=0.1, how does its weight change?

A) It decreases by 0.05.
B) It increases by 0.05.
C) It decreases by 0.10.
D) It increases by 0.10.

Learner answer: A
Correct answer: B
Result: incorrect
Explanation: The positive-response loop adds lr×(1−p)×count = 0.1×0.5×1 = 0.05 to that token’s weight.

Lesson 09 initial complete set: 2/3.


### p09-l10-a1-q1 — 2026-10-26

What defines centralized training with decentralized execution (CTDE) in multi-agent RL?

A) A joint critic can use global state and actions during training, while each deployed policy uses its local observation.
B) Every agent shares one action at execution, while each critic trains only on its agent’s local observation.
C) Agents train and deploy with full global state, while their rewards remain private during execution.
D) One central policy selects all agents’ actions at execution, while each agent trains its own local critic.

Learner answer: A
Correct answer: A
Result: correct
Explanation: CTDE gives the training critic joint information to handle coordination, but each agent’s deployed policy acts from its own local observation.


### p09-l10-a1-q2 — 2026-10-26

In a competitive game, a single agent repeatedly trains against its latest copy and cycles among strategies that beat one another. Which training change best addresses this?

A) Use only the most recent opponent policy so updates remain on-policy.
B) Remove opponent history and increase the discount factor instead.
C) Train against a league containing past and varied opponent policies.
D) Give every opponent the same action so the game becomes stationary.

Learner answer: C
Correct answer: C
Result: correct
Explanation: League play samples from a population of past and varied opponents, which helps expose and reduce cyclic weaknesses that single-opponent self-play can miss.


### p09-l10-a1-q3 — 2026-10-26

In CoopGridWorld.step, done is true only when both new positions equal (5,5); reward is 10 if done, otherwise -1. If the two new positions are ((5,5),(5,4)), what does step report for reward and done?

A) reward=10, done=True
B) reward=10, done=False
C) reward=-1, done=True
D) reward=-1, done=False

Learner answer: D
Correct answer: D
Result: correct
Explanation: Only one agent has reached the shared goal, so the conjunction is false; the environment returns the per-step penalty -1 and done=False.

Lesson 10 initial complete set: 3/3.


### p09-l11-a1-q1 — 2026-10-26

What is the purpose of domain randomization for sim-to-real transfer?

A) Measure one exact real-world parameter set and train only on that setting.
B) Replace real sensor observations with simulator-only privileged state at deployment.
C) Vary plausible simulator parameters during training so the policy tolerates real-world variation.
D) Increase the number of policy updates on one unchanged simulator until it memorizes the dynamics.

Learner answer: C
Correct answer: C
Result: correct
Explanation: Domain randomization exposes the policy to a range of plausible physics and sensing parameters during simulation training, aiming for robustness when the real system lies within that range.


### p09-l11-a1-q2 — 2026-10-26

A robot fails after sim training because its real motors respond with a delay that the simulator omits. Which first change best targets the identified reality gap?

A) Randomize camera hue more widely while leaving motor dynamics unchanged.
B) Measure motor delay, represent it in the simulator, and train across a plausible delay range.
C) Remove the safety controller so the policy can adapt faster on hardware.
D) Train longer with the same zero-delay simulator and the same observations.

Learner answer: B
Correct answer: B
Result: correct
Explanation: The observed mismatch is motor delay. Measuring and modeling it, then randomizing over a plausible range, directly targets the gap rather than unrelated visual changes.


### p09-l11-a1-q3 — 2026-10-26

In the lesson’s step function, slip happens when rng.random() < slip. If slip=0.4 and the sampled number is exactly 0.4, what happens to the requested action?

A) It slips, because equality satisfies the threshold check.
B) It slips with a separate 0.4 probability after the sampled check.
C) It stays requested, because 0.4 < 0.4 is false.
D) It becomes a random action, because the sample is in training support.

Learner answer: B
Correct answer: C
Result: incorrect
Explanation: The comparison is strict: 0.4 < 0.4 is false, so the branch that substitutes a perpendicular action does not run.

Lesson 11 initial complete set: 2/3.


### p09-l12-a1-q1 — 2026-10-26

What distinguishes MuZero from AlphaZero in the lesson’s comparison?

A) MuZero trains a value network but never searches; AlphaZero searches with MCTS.
B) MuZero learns latent dynamics for search; AlphaZero searches using known game rules.
C) MuZero uses group-relative rewards; AlphaZero uses a learned reward model.
D) MuZero requires human move labels; AlphaZero trains only from game outcomes.

Learner answer: B
Correct answer: B
Result: correct
Explanation: AlphaZero searches using known game rules, while MuZero learns a latent dynamics and reward model and runs search in that learned space.


### p09-l12-a1-q2 — 2026-10-26

You want to train a reasoning policy with GRPO on coding tasks. What must supply a dependable reward for sampled solutions?

A) A diverse set of past opponent policies for league play.
B) A learned simulator of latent code execution dynamics.
C) A trusted verifier that tests whether each solution is correct.
D) A value critic that predicts every token’s expected return.

Learner answer: C
Correct answer: C
Result: correct
Explanation: The lesson’s GRPO setup scores sampled completions with a verifier, such as tests for code or an exact answer checker, then forms group-relative advantages.


### p09-l12-a1-q3 — 2026-10-26

In the lesson’s grpo_step, one group has rewards [1, 1, 1, 1]. The code computes each advantage as (r − mean_r)/(std_r + 1e−8). What is every advantage?

A) 1, because every sampled answer passed the verifier.
B) 0, because each reward equals the group mean.
C) 0.25, because each reward is one quarter of the total.
D) Undefined, because the code divides by an exact zero.

Learner answer: B
Correct answer: B
Result: correct
Explanation: The group mean is 1, so each numerator r−mean is 0. The small denominator offset prevents division by zero; every advantage is 0.

Lesson 12 initial complete set: 3/3. Initial phase score: 24/36 (66.67%). Lessons 01 (1/3), 03 (1/3), and 05 (0/3) require full three-question retakes; effective score remains 24/36 until complete retakes.


### p09-l01-a2-q1 — 2026-10-26

Under a fixed policy π, how does Qπ(s,a) differ from Vπ(s)?

A) Qπ(s,a) fixes the first action at a; Vπ(s) averages over actions chosen by π.
B) Qπ(s,a) uses only immediate reward; Vπ(s) includes discounted future rewards.
C) Qπ(s,a) averages all states; Vπ(s) fixes the next state after action a.
D) Qπ(s,a) is defined only for terminal states; Vπ(s) is defined elsewhere.

Learner answer: D
Correct answer: A
Result: incorrect
Explanation: Qπ conditions on taking action a first, then following π; Vπ starts in state s and averages over the policy’s action choice. Both include future discounted return.


### p09-l01-a2-q2 — 2026-10-26

A navigation agent’s current camera frame shows the same hallway on two visits, but its velocity differs and changes which turn is safe. What state change best restores the Markov property?

A) Increase the reward for arriving safely, keeping the camera frame as the state.
B) Add velocity information or a short frame history to the state representation.
C) Set γ to zero so the agent only values the next immediate reward.
D) Average the two safe-turn probabilities for that camera frame.

Learner answer: A
Correct answer: B
Result: incorrect
Explanation: The camera frame alone omits velocity that predicts future dynamics. Adding velocity or sufficient observation history makes the state more nearly sufficient. Reward changes do not add predictive information to state.


### p09-l01-a2-q3 — 2026-10-26

In the lesson’s step function on a 4×4 grid, action "up" from (0,0) is clipped at the boundary. What does step((0,0), "up") return?

A) ((0,0), 0.0, False)
B) ((0,0), -1.0, False)
C) ((-1,0), -1.0, False)
D) ((0,0), -1.0, True)

Learner answer: B
Correct answer: B
Result: correct
Explanation: The row is clipped to 0, so position stays (0,0). It is nonterminal, so the attempted step still costs -1 and done remains False.

Lesson 01 attempt 2 complete: 1/3. Latest complete set remains 1/3. Cumulative phase: 25/39; effective 24/36.


### p09-l01-a3-q1 — 2026-10-26

What does the Bellman equation express about a state’s value under a policy?

A) It equals only the reward received on entering that state.
B) It equals the probability that the policy chooses its best action.
C) It is expected immediate reward plus discounted successor-state value.
D) It is the largest return observed in any rollout from that state.

Learner answer: B
Correct answer: C
Result: incorrect
Explanation: The Bellman relation decomposes expected return into the current reward and the discounted expected value of the next state under the policy.


### p09-l01-a3-q2 — 2026-10-26

A continuing task pays reward +1 every step without a terminal state. If γ=1, which formulation change avoids an unbounded discounted return?

A) Make the reward +2 so the policy sees a stronger learning signal.
B) Add a finite horizon or use a discount factor below 1.
C) Average the rewards over the last two steps without changing the horizon.
D) Use a deterministic policy so every state has one possible action.

Learner answer: C
Correct answer: B
Result: incorrect
Explanation: With reward +1 forever and γ=1, the return sum diverges. A finite horizon or γ<1 makes this discounted-return formulation finite.


### p09-l01-a3-q3 — 2026-10-26

In policy_evaluation, the terminal state is skipped, and V starts at 0 everywhere. If a nonterminal state has one action with probability 1 that gives reward -1 and moves directly to terminal, what value is assigned to that state on its first update?

A) 0, because terminal V starts at zero.
B) -γ, because the immediate reward is discounted.
C) -1, because the immediate reward is -1 and terminal V is zero.
D) -1/(1−γ), because the reward repeats forever.

Learner answer: C
Correct answer: C
Result: correct
Explanation: The update is -1 + γ×V(terminal) = -1 + γ×0 = -1. The immediate reward is not discounted.

Lesson 01 attempt 3 complete: 1/3. Latest complete set remains 1/3. Cumulative phase: 26/42; effective 24/36.


### p09-l01-a4-q1 — 2026-10-26

If γ changes from 0.9 to 0.99 in the same continuing MDP, what happens to the approximate effective reward horizon?

A) It shrinks from about 100 steps to about 10 steps.
B) It stays near 10 steps because the policy is unchanged.
C) It becomes infinite because γ is close to 1.
D) It grows from about 10 steps to about 100 steps.

Learner answer: B
Correct answer: D
Result: incorrect
Explanation: The effective horizon is roughly 1/(1−γ): γ=0.9 gives about 10 steps and γ=0.99 gives about 100.


### p09-l01-a4-q2 — 2026-10-26

A warehouse agent is rewarded only when every order is fulfilled at the end of a long shift. It rarely sees a successful episode. Which change directly addresses this sparse-reward problem?

A) Remove state information so the agent explores more broadly.
B) Add useful intermediate rewards tied to progress toward fulfilled orders.
C) Set γ=0 so the final outcome no longer affects early actions.
D) Increase the size of the terminal reward without changing when feedback arrives.

Learner answer: B
Correct answer: B
Result: correct
Explanation: Intermediate reward shaping tied to the target outcome provides more frequent learning signals when terminal success is rare.


### p09-l01-a4-q3 — 2026-10-26

The GridWorld starts at (0,0). A deterministic policy moves right, right, right, down, down, down into terminal (3,3), receiving -1 on each move. With γ=1 for this finite episode, what is the rollout’s total return?

A) -3, because only the horizontal moves count.
B) -5, because entering the terminal gives no reward.
C) -6, because all six moves each give reward -1.
D) 0, because γ=1 cancels the step penalties.

Learner answer: C
Correct answer: C
Result: correct
Explanation: There are six transitions from (0,0) to (3,3), and entering the terminal still incurs -1; with γ=1, the total is -6.

Lesson 01 attempt 4 complete: 2/3. Latest complete set replaces prior 1/3; cumulative phase 28/45, effective 25/36.


### p09-l03-a2-q1 — 2026-10-26

Why can Monte Carlo policy evaluation work without knowing the environment’s transition probabilities?

A) It solves the Bellman equation by enumerating every possible next state.
B) It averages returns observed after visits to states in sampled episodes.
C) It replaces environment transitions with a learned dynamics model.
D) It chooses only greedy actions, so all transitions become predictable.

Learner answer: A
Correct answer: B
Result: incorrect
Explanation: Monte Carlo estimates expected return by sampling whole episodes and averaging observed returns; it need not enumerate or know transition probabilities.


### p09-l03-a2-q2 — 2026-10-26

A Monte Carlo evaluator runs a policy in an environment where some episodes can loop indefinitely. What practical change lets it collect bounded rollouts while making the truncation explicit?

A) Use an unlimited rollout and wait for every trajectory to finish naturally.
B) Stop after a maximum step count and report capped episodes separately.
C) Replace observed returns with exact Bellman expectations from a model.
D) Treat every incomplete trajectory as a successful terminal episode.

Learner answer: C
Correct answer: B
Result: incorrect
Explanation: Monte Carlo needs bounded episodes for usable returns. A max-step cap prevents endless rollouts, and tracking capped episodes makes the resulting truncation visible. Choice C requires a model and switches to dynamic programming.


### p09-l03-a2-q3 — 2026-10-26

A state starts with V=2 and has count=3. The next first-visit return is G=6. After counts[s] += 1 and V[s] += (G−V[s])/counts[s], what is the new V?

A) 2.5
B) 3.0
C) 4.0
D) 6.0

Learner answer: C
Correct answer: B
Result: incorrect
Explanation: The new count is 4, so the incremental update is 2 + (6−2)/4 = 3.

Lesson 03 attempt 2 complete: 0/3. Latest complete set replaces prior 1/3; cumulative phase 28/48, effective 24/36.


### p09-l03-a3-q1 — 2026-10-26

When an episode visits the same state twice, how do first-visit and every-visit Monte Carlo evaluation differ?

A) First-visit uses only the first visit’s return; every-visit uses returns from both visits.
B) First-visit uses only immediate rewards; every-visit uses discounted returns.
C) First-visit uses the model’s transitions; every-visit uses sampled episodes.
D) First-visit updates after each step; every-visit waits until the episode ends.

Learner answer: D
Correct answer: A
Result: incorrect
Explanation: First-visit counts a state once per episode at its first occurrence; every-visit counts every occurrence and its following return.


### p09-l03-a3-q2 — 2026-10-26

A policy changes during Monte Carlo control, but its state-value estimate is an average over every return since training began. Which update choice helps the estimate track the newer policy more quickly?

A) Use a constant step size α so recent returns retain substantial weight.
B) Keep the 1/n step size so older returns dominate as n grows.
C) Stop sampling new episodes after each policy improvement.
D) Replace every observed return with a fixed terminal reward.

Learner answer: A
Correct answer: A
Result: correct
Explanation: A constant step size keeps reacting to new returns, whereas the sample-average step size 1/n becomes very small as the count grows.


### p09-l03-a3-q3 — 2026-10-26

A first-visit evaluator sees trajectory states [s, t, s] with returns [5, 3, 1]. Its seen set starts empty and it skips a state already seen in this episode. Which return updates V(s)?

A) Only 1, because the last visit is closest to episode end.
B) Both 5 and 1, because both visits appear in the trajectory.
C) The average 3, because the two visits are merged before update.
D) Only 5, because the later visit is skipped after s is marked seen.

Learner answer: A
Correct answer: D
Result: incorrect
Explanation: The first s is processed with return 5 and added to seen. When s appears again, the code continues without updating it.

Lesson 03 attempt 3 complete: 1/3. Latest complete set replaces prior 0/3; cumulative phase 29/51, effective 25/36.


### p09-l03-a4-q1 — 2026-10-26

In off-policy Monte Carlo evaluation, why are importance-sampling weights needed?

A) They convert a full episode return into an immediate reward.
B) They correct for trajectories sampled under a behavior policy different from the target policy.
C) They replace exploration with exact model-based expectations.
D) They make the next-state value estimate stationary during training.

Learner answer: B
Correct answer: B
Result: correct
Explanation: Off-policy data comes from behavior policy μ, while the target is π. Importance weights use their action-probability ratios to account for that difference.


### p09-l03-a4-q2 — 2026-10-26

Off-policy Monte Carlo importance weights become extremely variable on long episodes because action-probability ratios multiply across steps. Which response does the lesson recommend?

A) Use a per-decision weighted importance-sampling variant or switch to TD.
B) Increase the episode horizon so the ratio product averages out.
C) Drop importance weights while still evaluating the target policy from behavior-policy data.
D) Set every action probability under the target policy to one.

Learner answer: C
Correct answer: A
Result: incorrect
Explanation: The lesson flags exploding trajectory-weight variance and recommends per-decision weighted importance sampling or a TD method. Dropping weights leaves the behavior-target policy mismatch uncorrected.


### p09-l03-a4-q3 — 2026-10-26

In mc_control, seen stores (state, action) pairs. An episode visits (s,left), then (s,right), then (s,left), with following returns 5, 4, and 3. Which returns update Q in this episode?

A) Only 5, because s is counted once regardless of action.
B) 5 and 4, because the repeated (s,left) pair is skipped.
C) 5 and 3, because the first and last actions match.
D) 5, 4, and 3, because all visits are counted.

Learner answer: D
Correct answer: B
Result: incorrect
Explanation: The first (s,left) and first (s,right) are distinct pairs and both update Q. The second (s,left) is already in seen, so its return 3 is skipped.

Lesson 03 attempt 4 complete: 1/3. Latest complete set remains 1/3; cumulative phase 30/54, effective 25/36.


### p09-l03-a5-q1 — 2026-10-26

Why can Monte Carlo value estimates have high variance on long episodes compared with one-step TD estimates?

A) Monte Carlo uses exact transition probabilities for every future state.
B) Monte Carlo uses the full sampled future return, including distant random outcomes.
C) Monte Carlo averages only immediate rewards and ignores later outcomes.
D) Monte Carlo updates from a bootstrapped next-state value each step.

Learner answer: D
Correct answer: B
Result: incorrect
Explanation: Monte Carlo waits for the entire observed return, so distant random outcomes affect the estimate; one-step TD bootstraps from a next-state estimate instead.


### p09-l03-a5-q2 — 2026-10-26

A policy is evaluated from complete episodes, but one state was visited in only 8 of them. The lesson’s shipped evaluator requires at least 100 episodes per state before reporting a tabular estimate. What should the evaluator do?

A) Report the estimate as reliable because 8 complete returns have no sampling variance.
B) Increase sampling until that state has enough visits, or withhold its estimate.
C) Fill in the missing visits with zero returns and report a 100-sample mean.
D) Replace the state estimate with the maximum return seen elsewhere.

Learner answer: A
Correct answer: B
Result: incorrect
Explanation: With only 8 episode visits, the stated reporting threshold is unmet. Collect more coverage or do not report that state estimate as ready.


### p09-l03-a5-q3 — 2026-10-26

A rollout records (s,a,r) before checking done. If env.step returns done=True on the second move, how many transition tuples are in the returned trajectory?

A) One, because the terminal move is excluded.
B) Two, because the terminal move is appended before breaking.
C) Three, because the loop adds an extra terminal transition.
D) Zero, because the trajectory is cleared when done is true.

Learner answer: B
Correct answer: B
Result: correct
Explanation: The code appends the current transition before the done check. It records both moves, then breaks after the second one.

Lesson 03 attempt 5 complete: 1/3. Latest complete set remains 1/3; cumulative phase 31/57, effective 25/36.


### p09-l05-a2-q1 — 2026-10-26

What three elements form the “deadly triad” that can destabilize naive deep Q-learning?

A) Function approximation, bootstrapping, and off-policy learning.
B) Reward clipping, exploration, and a target network.
C) A replay buffer, a target network, and stochastic gradients.
D) Discrete actions, terminal rewards, and discounted returns.

Learner answer: A
Correct answer: A
Result: correct
Explanation: The deadly triad is the combination of function approximation, bootstrapped targets, and off-policy updates; DQN’s replay and target network mitigate instability.


### p09-l05-a2-q2 — 2026-10-26

A DQN learner keeps copying online weights into its target network after every gradient step, and its targets oscillate. Which adjustment directly restores the target network’s intended role?

A) Remove the target network and reuse the online network for both sides.
B) Freeze the online network and update only the target network.
C) Copy online weights to the target only at spaced intervals.
D) Clip all rewards to zero so targets cannot change.

Learner answer: B
Correct answer: C
Result: incorrect
Explanation: The target network should hold weights fixed across many gradient steps, then periodically sync from the online network; copying every step removes that stabilizing lag. Freezing the online network would prevent Q learning.


### p09-l05-a2-q3 — 2026-10-26

DQN train_step sees a nonterminal sample with r=1, γ=0.5, and target.forward(s_next)=[2, 6]. What bootstrap target y does the code compute?

A) 2, from reward plus the smaller target Q value.
B) 3, from discounting the largest target Q value only.
C) 4, from reward plus discounted largest target Q value.
D) 7, from reward plus the undiscounted largest target Q value.

Learner answer: B
Correct answer: C
Result: incorrect
Explanation: The nonterminal target is r + γ×max(Q_target(next)) = 1 + 0.5×6 = 4.

Lesson 05 attempt 2 complete: 1/3. Latest complete set replaces prior 0/3; cumulative phase 32/60, effective 26/36.


### p09-l05-a3-q1 — 2026-10-26

In Double DQN, which network selects the next action and which evaluates its value in the bootstrap target?

A) The target network selects; the online network evaluates.
B) The online network selects; the target network evaluates.
C) The online network both selects and evaluates.
D) The target network both selects and evaluates.

Learner answer: B
Correct answer: B
Result: correct
Explanation: Double DQN uses online Q values for argmax action selection and target-network Q values to evaluate that chosen action, reducing maximization bias.


### p09-l05-a3-q2 — 2026-10-26

A DQN run begins gradient updates when its replay buffer holds only 20 nearly identical transitions. What change best addresses the lesson’s cold-start warning?

A) Wait until the buffer has many varied transitions before training.
B) Increase the target sync frequency to every transition.
C) Clip every reward to zero until the buffer is full.
D) Turn off replay and train directly on each new transition.

Learner answer: A
Correct answer: A
Result: correct
Explanation: DQN should collect a replay warmup before training so early updates are not fitted to a tiny, correlated sample.


### p09-l05-a3-q3 — 2026-10-26

In QNet.forward, suppose one hidden unit has weights [2, -1], input [1, 3], and bias 0. What hidden activation does ReLU produce?

A) -1, because the weighted sum is -1.
B) 0, because ReLU clips a negative weighted sum.
C) 1, because the input values are both positive.
D) 5, because ReLU adds the input magnitudes.

Learner answer: B
Correct answer: B
Result: correct
Explanation: The weighted sum is 2×1 + (−1)×3 = −1. ReLU computes max(0,−1)=0.

Lesson 05 attempt 3 complete: 3/3. Latest complete set replaces prior 1/3; cumulative phase 35/63, effective 28/36.


### p09-l03-a6-q1 — 2026-10-26

What must happen before a standard Monte Carlo method can compute the full return for a state visit?

A) The transition model must be enumerated for every action.
B) The value function must first converge under Bellman updates.
C) The episode must finish or reach an explicit finite cutoff.
D) The behavior policy must become fully deterministic.

Learner answer: C
Correct answer: C
Result: correct
Explanation: Monte Carlo uses the observed return from a complete or explicitly capped trajectory, so it must wait for an endpoint before computing that full return.


### p09-l03-a6-q2 — 2026-10-26

Logged behavior-policy episodes never take action right in state s, but the target policy always takes right there. Can importance-sampled Monte Carlo estimate that target choice from these logs alone?

A) Yes; assign infinite weight to missing right-action trajectories.
B) Yes; multiply each observed left-action return by the target probability of right.
C) No; collect behavior-policy data that gives the target action nonzero support.
D) No; replace each missing trajectory with a zero return and keep the logs.

Learner answer: C
Correct answer: C
Result: correct
Explanation: Importance sampling cannot reweight a target action that the behavior policy never sampled. Data collection must give target actions nonzero probability.


### p09-l03-a6-q3 — 2026-10-26

The lesson’s ε-greedy policy uses a random action only if random() < ε; otherwise it returns max(Q[s], key=Q[s].get). With ε=0.1, random()=0.2, and Q[s]={"up":0, "down":3, "left":1, "right":2}, which action is returned?

A) up, because it is the first action in the Q dictionary.
B) down, because the greedy branch picks the largest Q value.
C) left, because random() exceeded ε by 0.1.
D) right, because it has the second-largest Q value.

Learner answer: B
Correct answer: B
Result: correct
Explanation: Since 0.2 < 0.1 is false, the random branch is skipped; max over Q[s] selects down with value 3.

Lesson 03 attempt 6 complete: 3/3. Latest complete set replaces prior 1/3; cumulative phase 38/66, effective 30/36 (83.33%). All lesson minima met; phase threshold 31/36 not yet met.


### p09-l04-a2-q1 — 2026-10-26

What makes a one-step temporal-difference update different from Monte Carlo evaluation?

A) TD waits for a full episode; MC updates after each transition.
B) TD uses a model of all transitions; MC uses only a reward function.
C) TD bootstraps from an estimated next-state value after one step.
D) TD never discounts future rewards; MC always discounts them.

Learner answer: C
Correct answer: C
Result: correct
Explanation: TD updates after a transition using r+γV(s′), while Monte Carlo waits for the complete sampled return.


### p09-l04-a2-q2 — 2026-10-26

In a noisy tabular task, Q-learning repeatedly overestimates the best next action because it takes a maximum over noisy Q values. Which change addresses this specific bias?

A) Use Double Q-learning with separate value estimates for action selection and evaluation.
B) Increase ε until every action is chosen with equal probability forever.
C) Use γ=1 so future rewards receive no discount.
D) Replace the maximum with the minimum Q value in the same table.

Learner answer: A
Correct answer: A
Result: correct
Explanation: Double Q-learning reduces maximization bias by decoupling selection from evaluation using two value estimates.


### p09-l04-a2-q3 — 2026-10-26

SARSA has Q(s,a)=2, reward r=1, γ=0.5, α=0.5, and Q(s_next,a_next)=4 for the action actually chosen next. What is the updated Q(s,a)?

A) 2.0
B) 2.5
C) 3.0
D) 4.0

Learner answer: B
Correct answer: B
Result: correct
Explanation: The SARSA target is 1 + 0.5×4 = 3; the update is 2 + 0.5×(3−2)=2.5.

Lesson 04 attempt 2 complete: 3/3. Latest complete set replaces prior 2/3; cumulative phase 41/69, effective 31/36 (86.11%). Every lesson latest complete set >=2/3. Phase 09 passed.
