AIMLCZG512

Deep Reinforcement Learning

Comprehensive Practice Question Bank

BITS Pilani | Prof. Vimal SP | CSIS Department

Covers All Syllabus Topics | Exam-Style Questions with Full Solutions

Document Details

Total Questions

Topics Covered

Format

Topics Covered

Info

18 Questions (10 Marks Each)

9 Major Topics

Scenario-based, Numerical, Conceptual

•  Topic 1: K-Armed Bandit Problem (UCB, epsilon-greedy, non-stationary, gradient bandit)
•  Topic 2: Markov Decision Processes (Bellman equations, value functions, policies)

•  Topic 3: Dynamic Programming (Policy Iteration, Value Iteration)
•  Topic 4: Monte Carlo Methods (First-visit MC, Importance Sampling, On/Off-policy)
•  Topic 5: Temporal Difference Learning (TD(0), SARSA, Q-learning, Expected SARSA)

•  Topic 6: Function Approximation and Deep Q-Networks (DQN, Double DQN)
•  Topic 7: Policy Gradient Methods (REINFORCE, Baseline, Actor-Critic / A2C)

•  Topic 8: Model-Based RL and Monte Carlo Tree Search (MCTS, AlphaGo, AlphaZero)
•  Topic 9: Imitation Learning (Behavioral Cloning, DAGGER)

TOPIC 1: K-Armed Bandit Problem

QUESTION 1 [10 Marks] — K-Armed Bandit | UCB | Non-Stationary

Scenario: A smart city traffic management system uses a K-armed bandit model to select
one of 4 signal timing strategies (S1, S2, S3, S4) at each decision cycle. The system
observes the following data over 6 time steps:  Time 1: S1, Reward=+2 | Time 2: S2,
Reward=+4 | Time 3: S1, Reward=+3 | Time 4: S3, Reward=-1 | Time 5: S2, Reward=+2 |
Time 6: S4, Reward=r (unknown)  a) Using sample average estimates and UCB with c = 1.5,
compute the UCB score for each strategy at time step 7. Which strategy will be selected?
Assume S4 reward r = +3. [4 Marks] b) Recompute Q(S1) at t=7 using the non-stationary
(exponential recency-weighted average) update rule with alpha = 0.4 and Q1(S1) = 0. [3
Marks] c) Compare sample-average vs. exponential recency-weighted average methods in
the context of this traffic signal scenario and explain when each is appropriate. [3 Marks]

MODEL ANSWER

a) UCB Score Computation at t=7 (c=1.5):

Total steps so far = 6. UCB formula: UCB(a) = Q(a) + c * sqrt(ln(t) / N(a))

Action visits and sample averages:

S1: visited t=1(+2), t=3(+3) => N(S1)=2, Q(S1) = (2+3)/2 = 2.5

S2: visited t=2(+4), t=5(+2) => N(S2)=2, Q(S2) = (4+2)/2 = 3.0

S3: visited t=4(-1) => N(S3)=1, Q(S3) = -1.0

S4: visited t=6(+3) => N(S4)=1, Q(S4) = +3.0

ln(7) = 1.9459

UCB(S1) = 2.5 + 1.5 * sqrt(1.9459/2) = 2.5 + 1.5 * 0.9858 = 2.5 + 1.479 = 3.979

UCB(S2) = 3.0 + 1.5 * sqrt(1.9459/2) = 3.0 + 1.479 = 4.479

UCB(S3) = -1.0 + 1.5 * sqrt(1.9459/1) = -1.0 + 1.5 * 1.3949 = -1.0 + 2.092 = 1.092

UCB(S4) = 3.0 + 1.5 * sqrt(1.9459/1) = 3.0 + 2.092 = 5.092

Selected action: S4 (highest UCB = 5.092), because it was tried least and has high
reward potential.

b) Non-stationary Q update for S1 (alpha=0.4):

Update rule: Q_new = Q_old + alpha * (R - Q_old) = (1-alpha)*Q_old + alpha*R

Q1(S1) = 0 (initial)

t=1: S1 selected, R=+2: Q2(S1) = 0 + 0.4*(2-0) = 0.8

t=3: S1 selected, R=+3: Q3(S1) = 0.8 + 0.4*(3-0.8) = 0.8 + 0.88 = 1.68

At t=7, Q(S1) = 1.68

Expanded form: Q = sum of alpha*(1-alpha)^k * R_{t-k}, giving exponentially decaying
weights to past rewards — recent reward R=3 has weight 0.4, older R=2 has weight
0.4*0.6=0.24.

c) Comparative Analysis:

Sample Average Method: Equal weight to all past rewards. Formula: Q_n = (1/n) * sum(R_i).
Step size 1/n decreases over time. Suitable for stationary environments where true action
values do not change. Converges to true mean in limit.

Exponential Recency-Weighted Average: Constant alpha gives recent rewards higher weight
via exponential decay. Suitable for non-stationary traffic environments where optimal signal
timing can change with time-of-day, weather, events. Ensures the agent adapts quickly to
changing conditions. Does not fully converge but stays responsive.

In the traffic signal context: Non-stationary (constant alpha) is preferred since traffic patterns
change by hour/day. Sample average would be slow to adapt to a road closure or new
congestion pattern.

Source: Study Material: Lectures 1-3, Pages 19-46 (K-Armed Bandit, Non-Stationary, UCB)

QUESTION 2 [10 Marks] — K-Armed Bandit | Epsilon-Greedy | Gradient Bandit

Scenario: A recommendation system chooses between 3 content categories: News (N),
Sports (Sp), Entertainment (E). Rewards represent user engagement (clicks: +1 or -1). After
5 interactions, the Q-value estimates are: Q(N)=0.5, Q(Sp)=0.8, Q(E)=-0.2, and each action
was taken N(N)=2, N(Sp)=2, N(E)=1 times.  a) With epsilon=0.3 and 2 actions available,
calculate the probability that the greedy action (Sports) is selected at the next step. [2 Marks]
b) Explain why epsilon=0.01 would outperform epsilon=0.5 in the long run on a stationary
problem using the 10-armed testbed intuition. Under what reward variance condition would
epsilon=0.5 be better? [3 Marks] c) The system switches to a gradient bandit algorithm.
Given action preferences H(N)=1.0, H(Sp)=2.0, H(E)=0.5, compute the softmax probability
pi(Sp) of selecting Sports. Then, if Sports is selected at this step with reward R=1 and
current baseline B=0.6, write the updated preference H_new(Sp) and H_new(N) using
alpha=0.1. [5 Marks]

MODEL ANSWER

a) Probability of selecting greedy action (Sports) with epsilon=0.3, k=3 actions:

P(greedy) = P(greedy | greedy selection) * P(greedy selection) + P(greedy | random
selection) * P(random selection)

= 1 * (1 - epsilon) + (1/k) * epsilon

= 1 * 0.7 + (1/3) * 0.3 = 0.7 + 0.1 = 0.80

Probability of selecting Sports (greedy action) = 0.80

b) Epsilon comparison (stationary environment):

epsilon=0.01: Exploits nearly all the time (99%). After sufficient exploration, the agent locks
onto the best action and achieves near-optimal reward. Eventually outperforms because it
exploits the best arm most frequently.

epsilon=0.5: Explores 50% of the time permanently. Wastes too many trials on suboptimal
arms in the long run, resulting in lower average reward. Useful early in learning but harmful
later.

epsilon=0.01 outperforms in the long run because it spends 99% of time on the identified
best action, whereas epsilon=0.5 spends only 50%, even after the estimates have
converged.

epsilon=0.5 would be preferable: When reward variance is very high (e.g., variance=10
instead of 1). High variance means more samples are needed to distinguish between
actions, making frequent exploration more necessary to avoid locking onto a false best arm.

c) Gradient Bandit Algorithm:

Softmax probability formula: pi(a) = exp(H(a)) / sum_b(exp(H(b)))

exp(H(N)) = exp(1.0) = 2.718

exp(H(Sp)) = exp(2.0) = 7.389

exp(H(E)) = exp(0.5) = 1.649

Sum = 2.718 + 7.389 + 1.649 = 11.756

pi(Sp) = 7.389 / 11.756 = 0.628 (62.8%)

Preference update rules for selected action A=Sp:

For selected action: H_new(Sp) = H(Sp) + alpha * (R - B) * (1 - pi(Sp))

= 2.0 + 0.1 * (1 - 0.6) * (1 - 0.628) = 2.0 + 0.1 * 0.4 * 0.372 = 2.0 + 0.0149 = 2.015

For non-selected action (News): H_new(N) = H(N) - alpha * (R - B) * pi(N)

pi(N) = 2.718 / 11.756 = 0.231

H_new(N) = 1.0 - 0.1 * (1 - 0.6) * 0.231 = 1.0 - 0.00924 = 0.991

Updated: H_new(Sp) = 2.015, H_new(N) = 0.991. Since R=1 > B=0.6, the agent
reinforces Sports.

Source: Study Material: Lectures 1-3, Pages 29-57 (Epsilon-greedy, Gradient Bandit, Softmax)

TOPIC 2: Markov Decision Processes (MDP)

QUESTION 3 [10 Marks] — MDP | Bellman Equations | Optimal Policy

Scenario: An autonomous irrigation system manages a smart farm with three soil moisture
states: Dry (D), Optimal (O), and Wet (W). At each time step the agent can take one of two
actions: Irrigate (I) or Skip (S). The discount factor gamma = 0.9.  State Transition Table: D +
I -> O (prob=0.8, reward=+3), D + I -> D (prob=0.2, reward=+0) D + S -> D (prob=1.0,
reward=-2) O + I -> W (prob=0.5, reward=+1), O + I -> O (prob=0.5, reward=+1) O + S -> O
(prob=0.7, reward=+5), O + S -> D (prob=0.3, reward=0) W + I -> W (prob=1.0, reward=-3)
W + S -> O (prob=1.0, reward=+2)  Current value estimates: V(D)=2, V(O)=6, V(W)=1.  a)
Write and compute the Bellman expectation equation for V_pi(O) under the policy
pi(Skip|O)=1.0. [3 Marks] b) Compute Q_pi(O, Irrigate) and Q_pi(O, Skip) using the given
value estimates and determine whether the policy should improve at state O. [4 Marks] c)
Write the Bellman optimality equation for V*(O) and explain its difference from the Bellman
expectation equation. [3 Marks]

MODEL ANSWER

a) Bellman Expectation Equation for V_pi(O) with pi(Skip|O)=1.0:

V_pi(s) = sum_a pi(a|s) * sum_s' P(s'|s,a) * [R(s,a,s') + gamma * V_pi(s')]

Since pi(Skip|O)=1.0, only action Skip applies:

V_pi(O) = P(O|O,S)*[R(O,S,O) + gamma*V(O)] + P(D|O,S)*[R(O,S,D) + gamma*V(D)]

= 0.7 * [5 + 0.9 * 6] + 0.3 * [0 + 0.9 * 2]

= 0.7 * [5 + 5.4] + 0.3 * [1.8]

= 0.7 * 10.4 + 0.3 * 1.8

= 7.28 + 0.54 = 7.82

b) Computing Q values and policy improvement at O:

Q_pi(O, Irrigate) = sum_s' P(s'|O,I) * [R(O,I,s') + gamma * V(s')]

= P(W|O,I)*[R+gamma*V(W)] + P(O|O,I)*[R+gamma*V(O)]

= 0.5*[1 + 0.9*1] + 0.5*[1 + 0.9*6]

= 0.5*[1 + 0.9] + 0.5*[1 + 5.4]

= 0.5*1.9 + 0.5*6.4 = 0.95 + 3.2 = 4.15

Q_pi(O, Skip) = 0.7*[5 + 0.9*6] + 0.3*[0 + 0.9*2] = 7.28 + 0.54 = 7.82

Since Q_pi(O, Skip) = 7.82 > Q_pi(O, Irrigate) = 4.15, the Skip action is already optimal at
state O.

Policy does NOT need to change. The improved policy pi_1(Skip|O) = 1.0 remains the
same.

c) Bellman Optimality Equation for V*(O):

V*(O) = max_a { sum_s' P(s'|O,a) * [R(s,a,s') + gamma * V*(s')] }

= max { Q*(O, Irrigate), Q*(O, Skip) } = max { 4.15, 7.82 } = 7.82

Difference from Bellman Expectation Equation:

Bellman Expectation: Averages over all actions according to a fixed policy pi. It evaluates the
expected return for a GIVEN policy — used in policy evaluation.

Bellman Optimality: Takes the maximum over all possible actions. It identifies the best
possible action — used in finding the OPTIMAL policy. It is nonlinear due to the max
operator, making it harder to solve analytically but yielding optimal behavior.

Source: Study Material: Lectures 3-5, Pages 21-32 (Value Functions, Bellman Equations, Optimal Policies)

TOPIC 3: Dynamic Programming

QUESTION 4 [10 Marks] — Dynamic Programming | Policy Iteration | Value
Iteration

Scenario: An energy management system for a smart building has 3 temperature states:
Cold (C), Comfortable (Co), Hot (H). Actions: Heat (He) or Cool (Cl). Discount gamma=0.9.
Transitions: C + He -> Co (p=0.9, r=+3), C + He -> C (p=0.1, r=0) C + Cl -> C (p=1.0, r=-2)
Co + He -> H (p=0.4, r=+1), Co + He -> Co (p=0.6, r=+2) Co + Cl -> C (p=0.3, r=-1), Co + Cl
-> Co (p=0.7, r=+4) H + He -> H (p=1.0, r=-4) H + Cl -> Co (p=1.0, r=+1)  Initial Policy pi0:
pi0(He|C)=1, pi0(He|Co)=1, pi0(Cl|H)=1 Initial Values: V0(C)=0, V0(Co)=0, V0(H)=0  a)
Perform ONE step of policy evaluation. Compute V1(C), V1(Co), V1(H) under pi0. [4 Marks]
b) Perform policy improvement after the evaluation in part (a). Compute Q_pi0(Co, He) and
Q_pi0(Co, Cl). Should the policy change at Co? [4 Marks] c) Briefly distinguish between
Policy Iteration and Value Iteration and state when Value Iteration is preferred. [2 Marks]

MODEL ANSWER

a) Policy Evaluation - Compute V1 under pi0:

V1(s) = sum_s' P(s'|s, pi0(s)) * [R(s,a,s') + gamma * V0(s')]

Since V0(all) = 0, the gamma*V0 terms vanish in first iteration:

V1(C) [pi0=He]: = P(Co|C,He)*[3 + 0.9*0] + P(C|C,He)*[0 + 0.9*0]

= 0.9 * 3 + 0.1 * 0 = 2.7

V1(Co) [pi0=He]: = P(H|Co,He)*[1 + 0] + P(Co|Co,He)*[2 + 0]

= 0.4 * 1 + 0.6 * 2 = 0.4 + 1.2 = 1.6

V1(H) [pi0=Cl]: = P(Co|H,Cl)*[1 + 0] = 1.0 * 1 = 1.0

Result: V1(C)=2.7, V1(Co)=1.6, V1(H)=1.0

b) Policy Improvement at state Co:

Using V1 values from part (a):

Q_pi0(Co, He) = P(H|Co,He)*[1 + 0.9*V1(H)] + P(Co|Co,He)*[2 + 0.9*V1(Co)]

= 0.4*[1 + 0.9*1.0] + 0.6*[2 + 0.9*1.6]

= 0.4*[1 + 0.9] + 0.6*[2 + 1.44]

= 0.4*1.9 + 0.6*3.44 = 0.76 + 2.064 = 2.824

Q_pi0(Co, Cl) = P(C|Co,Cl)*[-1 + 0.9*V1(C)] + P(Co|Co,Cl)*[4 + 0.9*V1(Co)]

= 0.3*[-1 + 0.9*2.7] + 0.7*[4 + 0.9*1.6]

= 0.3*[-1 + 2.43] + 0.7*[4 + 1.44]

= 0.3*1.43 + 0.7*5.44 = 0.429 + 3.808 = 4.237

Q_pi0(Co, Cl) = 4.237 > Q_pi0(Co, He) = 2.824

Policy should CHANGE at Co: pi1(Cl|Co) = 1.0 (switch from Heat to Cool at
Comfortable state)

c) Policy Iteration vs. Value Iteration:

Policy Iteration: Alternates between full policy evaluation (running Bellman equations to
convergence) and policy improvement. Produces an explicit interpretable policy at each step.
Preferred for smaller state spaces.

Value Iteration: Combines evaluation and improvement in a single Bellman update:
V_{k+1}(s) = max_a { sum P(s'|s,a)[R + gamma*V_k(s')] }. No explicit intermediate policy.
Converges faster for large state spaces. Preferred when fast convergence to optimal value
function is needed.

Source: Study Material: Lectures 3-5, Pages 42-50 (Value Iteration), Lecture Notes Pages 7-13 (DP, Policy Iteration)

TOPIC 4: Monte Carlo Methods

QUESTION 5 [10 Marks] — Monte Carlo | First-Visit MC | Importance Sampling

Scenario: A retail store uses an RL agent to determine restocking policies. States represent
inventory levels: Full (F), Moderate (M), Low (L). Actions: Order (O) or Wait (W). The agent
generates episodes to learn state values. Discount gamma = 0.9.  Episode 1: (M, O, +2, F) -
> (F, W, +5, M) -> (M, W, -1, L) -> (L, O, +4, Terminal) Episode 2: (M, W, -2, L) -> (L, O, +4,
F) -> (F, W, +5, Terminal)  a) Using First-Visit Monte Carlo, compute the estimated V(M)
from Episodes 1 and 2. Show all return calculations with discounting. [5 Marks] b) The store
now uses an off-policy approach. The behavior policy b selects: b(O|M)=0.6, b(W|M)=0.4.
The target policy pi is deterministic: pi(O|M)=1.0. For the trajectory in Episode 1 starting at
the first M: compute the importance sampling ratio rho, the return G(M), and explain how
Weighted Importance Sampling would update V(M). [5 Marks]

MODEL ANSWER

a) First-Visit Monte Carlo for V(M):

Episode 1: (M,O,+2,F) -> (F,W,+5,M) -> (M,W,-1,L) -> (L,O,+4,Terminal)

First visit to M at t=0:

G(M,t=0) = 2 + 0.9*5 + 0.9^2*(-1) + 0.9^3*4

= 2 + 4.5 - 0.81 + 2.916 = 8.606

Second visit to M at t=2: NOT counted in First-Visit MC.

Episode 2: (M,W,-2,L) -> (L,O,+4,F) -> (F,W,+5,Terminal)

First visit to M at t=0:

G(M,t=0) = -2 + 0.9*4 + 0.9^2*5 = -2 + 3.6 + 4.05 = 5.65

V(M) = Average of returns from first visits = (8.606 + 5.65) / 2 = 7.128

b) Off-Policy Importance Sampling:

Episode 1 trajectory from state M: actions taken are (O, W, O)

At t=0, state M: action O taken. pi(O|M)=1.0, b(O|M)=0.6

At t=1, state F: action W taken. Both pi and b assign probability 1 to W (deterministic); ratio =
1

At t=2, state M: action W taken. pi(W|M)=0 (deterministic pi selects only O)

Since pi(W|M)=0, rho = 0. This episode would be discarded or contribute 0.

For the purpose of illustration, if we consider only the segment where M takes action O:

rho(t=0) = pi(O|M) / b(O|M) = 1.0 / 0.6 = 1.667

Return G from M: G = 2 + 0.9*5 + 0.9^2*(-1) + 0.9^3*4 = 8.606

Weighted Importance Sampling (WIS) update:

WIS avoids the high variance of ordinary IS by normalizing weights:

V_WIS(M) = [sum_k rho_k * G_k] / [sum_k rho_k]

For a single episode with rho=1.667, G=8.606:

V_WIS(M) = (1.667 * 8.606) / 1.667 = 8.606

WIS is biased (unlike ordinary IS) but has much lower variance. As more episodes are
collected, WIS estimates converge more reliably than ordinary IS. This is critical for off-policy
RL where behavioral and target policies differ significantly.

Source: Study Material: Lectures 6-8, Pages 7-40 (MC Methods, First-Visit, Importance Sampling)

QUESTION 6 [10 Marks] — Monte Carlo | On-Policy vs Off-Policy | MC Control

Scenario: A drone delivery system explores routes using Monte Carlo Control. States: {Base
(B), Zone1 (Z1), Zone2 (Z2), Destination (D)}. Actions: {Fly (F), Wait (W)}. Gamma=0.9,
epsilon=0.1.  a) Explain First-Visit MC vs. Every-Visit MC. Which is statistically unbiased?
Under what condition do they produce the same estimate? [3 Marks] b) On-policy MC control
uses an epsilon-soft policy. Explain how the epsilon-soft policy maintains exploration while
still converging to the optimal policy. What is the key limitation compared to off-policy MC? [3
Marks] c) An episode is: (Z1,F,+3,Z2) -> (Z2,W,-1,Z2) -> (Z2,F,+10,D,Terminal).
Gamma=0.9. Using Every-Visit MC, compute Q(Z2,F) and Q(Z2,W) from this single episode.
[4 Marks]

MODEL ANSWER

a) First-Visit vs. Every-Visit MC:

First-Visit MC: Only the FIRST occurrence of a state-action pair in an episode contributes to
the average. Return G is computed from that first visit forward.

Every-Visit MC: EVERY occurrence of a state-action pair in an episode contributes. Multiple
returns from the same episode are averaged.

Statistical Unbiasedness: Both converge to the true value function. First-Visit MC is unbiased
per episode. Every-Visit MC is also consistent but uses correlated samples from the same
episode.

Same estimate condition: When each state/action pair appears at most ONCE per episode,
both methods produce identical estimates.

b) Epsilon-Soft Policy and On-Policy MC Control:

Epsilon-soft policy: pi(a|s) >= epsilon/|A(s)| for all actions. Greedy action gets 1-epsilon +
epsilon/|A| probability; others get epsilon/|A|.

This ensures every action has a non-zero probability, guaranteeing all state-action pairs are
visited infinitely often, allowing convergence.

As learning proceeds, epsilon is gradually reduced, so the policy approaches greedy
(optimal) behavior while still exploring.

Key Limitation vs Off-Policy: On-policy MC can only learn the optimal epsilon-soft policy (not
the truly greedy optimal), because the behavior and target policies must be the same. Off-
policy MC (using importance sampling) can learn the optimal deterministic policy while
exploring with a different behavior policy.

c) Every-Visit MC - Q(Z2,F) and Q(Z2,W):

Episode: (Z1,F,+3,Z2) -> (Z2,W,-1,Z2) -> (Z2,F,+10,D)

t=0: (Z1, F, r=3) | t=1: (Z2, W, r=-1) | t=2: (Z2, F, r=10)

Return from t=2 (Z2, F): G2 = 10 [terminal after this]

Return from t=1 (Z2, W): G1 = -1 + 0.9 * 10 = -1 + 9 = 8

Every-Visit MC for Q(Z2, F): Only t=2 contributes -> Q(Z2,F) = 10

Every-Visit MC for Q(Z2, W): Only t=1 contributes -> Q(Z2,W) = 8

Note: Z2,F at t=2 and Z2,W at t=1 each appear once, so first-visit and every-visit yield the
same result here.

Source: Study Material: Lectures 6-8, Pages 7-30 (MC Policy Evaluation, On/Off Policy, MC Control)

TOPIC 5: Temporal Difference Learning (SARSA, Q-Learning)

QUESTION 7 [10 Marks] — TD Learning | SARSA vs Q-Learning | TD Error

Scenario: A self-driving vehicle learns lane-keeping behavior using TD methods. States:
{Left-Lane (L), Center-Lane (C), Right-Lane (R)}. Actions: {Steer-Left (SL), Steer-Right (SR),
Go-Straight (GS)}. Gamma=0.9, alpha=0.5, epsilon=0.1.  Initial Q-values: All Q(s,a) = 0.
Episode sequence: (C, GS, +2, C) -> (C, SR, -1, R) -> (R, SL, +3, C) -> (C, GS, +5,
Terminal)  a) Compute the SARSA update for Q(C, GS) using the first two transitions. State
the SARSA quintuple for each step. [4 Marks] b) Redo the updates using Q-learning for the
same transitions. Highlight the key algorithmic difference compared to SARSA. [3 Marks] c)
Define the TD error (delta_t). Explain how it drives learning differently in TD(0) compared to
Monte Carlo. Why is TD learning more suitable for continuing tasks? [3 Marks]

MODEL ANSWER

a) SARSA Updates:

SARSA quintuples: (St, At, Rt+1, St+1, At+1). Action At+1 is chosen by epsilon-greedy from
current Q.

Update rule: Q(St, At) <- Q(St, At) + alpha * [Rt+1 + gamma*Q(St+1, At+1) - Q(St, At)]

Step 1: SARSA quintuple = (C, GS, +2, C, SR)

[At t=1, next state is C; epsilon-greedy selects SR as next action (as per episode)]

Q(C, GS) <- 0 + 0.5 * [2 + 0.9 * Q(C, SR) - 0]

= 0 + 0.5 * [2 + 0.9 * 0] = 0 + 0.5 * 2 = 1.0

Step 2: SARSA quintuple = (C, SR, -1, R, SL)

Q(C, SR) <- 0 + 0.5 * [-1 + 0.9 * Q(R, SL) - 0]

= 0 + 0.5 * [-1 + 0.9 * 0] = 0 + 0.5 * (-1) = -0.5

Updated values: Q(C,GS) = 1.0, Q(C,SR) = -0.5

b) Q-Learning Updates:

Q-Learning rule: Q(St, At) <- Q(St, At) + alpha * [Rt+1 + gamma * max_a Q(St+1, a) - Q(St,
At)]

Key Difference: Q-learning uses max_a Q(St+1, a) (greedy over next state) regardless of
actual action taken. SARSA uses Q(St+1, At+1) where At+1 is the actual next action chosen
by policy.

Step 1: (C, GS, +2, C)

max_a Q(C, a) = max{Q(C,GS), Q(C,SR), Q(C,SL)} = max{0,0,0} = 0

Q(C, GS) <- 0 + 0.5 * [2 + 0.9*0 - 0] = 1.0

Step 2: (C, SR, -1, R)

max_a Q(R, a) = max{0,0,0} = 0

Q(C, SR) <- 0 + 0.5 * [-1 + 0.9*0 - 0] = -0.5

Results are identical here because all Q-values are 0, but will diverge as values propagate.

c) TD Error and Comparison with MC:

TD Error: delta_t = R_{t+1} + gamma * V(S_{t+1}) - V(S_t)

This error measures how 'surprised' the agent is: the difference between the predicted value
and the TD target (bootstrapped estimate).

TD(0) vs MC: TD uses a ONE-STEP lookahead (bootstrap from next state estimate) — it can
update after every single transition without waiting for episode end. MC requires a
COMPLETE episode to compute actual return Gt.

TD is better for continuing tasks because: (1) Episodes may never terminate; (2) Online
updates allow faster adaptation; (3) Lower variance (though biased), leading to more stable
learning in long episodes or non-terminating environments.

Source: Study Material: Lecture 9, Pages 3-20 (TD Learning, SARSA, Q-Learning)

QUESTION 8 [10 Marks] — TD Learning | Expected SARSA | Double Q-Learning
| Maximization Bias

Scenario: A financial trading agent uses TD methods to learn buy/sell policies. States: {Bull
(B), Neutral (N), Bear (Br)} representing market conditions. Actions: {Buy (By), Sell (Se),
Hold (H)}. gamma=0.9, alpha=0.5, epsilon=0.1.  Current Q-table (after some learning):
Q(B,By)=2.0, Q(B,Se)=0.5, Q(B,H)=1.0 Q(N,By)=1.0, Q(N,Se)=1.5, Q(N,H)=0.8 Q(Br,By)=-
1.0, Q(Br,Se)=2.5, Q(Br,H)=0.3  Transition observed: (B, Buy, +3, N)  a) Compute the
Expected SARSA update for Q(B, Buy) given epsilon=0.1 and 3 actions. [4 Marks] b) Explain
Maximization Bias in Q-Learning with a concrete example from this trading scenario. How
does Double Q-Learning address this? [4 Marks] c) Compare SARSA, Expected SARSA and
Q-Learning in terms of on-policy vs off-policy, variance, and bias. [2 Marks]

MODEL ANSWER

a) Expected SARSA Update for Q(B, Buy):

Expected SARSA uses the expected value of Q(S', a) under current epsilon-greedy policy:

E_pi[Q(S', a)] = sum_a pi(a|S') * Q(S', a)

At state N, epsilon=0.1, 3 actions:

Greedy action at N: Sell (Q(N,Se)=1.5 is highest)

P(greedy action = Sell) = 1 - epsilon + epsilon/|A| = 1 - 0.1 + 0.1/3 = 0.9333

P(other actions, By and H) = epsilon/|A| = 0.1/3 = 0.0333 each

E_pi[Q(N,a)] = 0.9333*Q(N,Se) + 0.0333*Q(N,By) + 0.0333*Q(N,H)

= 0.9333*1.5 + 0.0333*1.0 + 0.0333*0.8

= 1.4 + 0.0333 + 0.0267 = 1.46

Expected SARSA update:

Q(B,Buy) <- Q(B,Buy) + alpha * [R + gamma * E_pi[Q(N,a)] - Q(B,Buy)]

= 2.0 + 0.5 * [3 + 0.9*1.46 - 2.0]

= 2.0 + 0.5 * [3 + 1.314 - 2.0]

= 2.0 + 0.5 * 2.314 = 2.0 + 1.157 = 3.157

b) Maximization Bias and Double Q-Learning:

Maximization Bias: Q-learning uses max_a Q(S', a) as the target. If Q-values are noisy
estimates, max over them is systematically higher than the true maximum (overestimation).

Trading Example: Suppose the true Q(Br, Se) = 2.5 but due to noise the estimates could be
Q(Br,Se)=2.5 and Q(Br,By)=-1.0. If the agent consistently uses max (2.5) but the true
expectation is lower, it overestimates the Bear market returns for Sell action, potentially
causing overconfident trading decisions.

Double Q-Learning Solution: Uses TWO independent Q-networks (theta and theta').

1. Use theta to SELECT the best action: a* = argmax_a Q(S', a, theta)

2. Use theta' to EVALUATE that action: Q(S', a*, theta')

This decoupling prevents the same noise from inflating both selection and evaluation,
reducing overestimation bias.

c) Comparison Table (SARSA vs Expected SARSA vs Q-Learning):

SARSA: On-policy. Uses actual next action. Medium variance (depends on exploration).
Converges to optimal epsilon-soft policy.

Expected SARSA: Can be on or off-policy. Uses expected value over next actions. Lower
variance than SARSA (averages out randomness). More computationally expensive.

Q-Learning: Off-policy. Uses greedy max over next state. Subject to maximization bias.
Converges to optimal policy regardless of behavior policy. Higher variance at early stages.

Source: Study Material: Lecture 9 and Notes (SARSA, Expected SARSA, Q-Learning, Double Q-Learning)

TOPIC 6: Function Approximation and Deep Q-Networks (DQN)

QUESTION 9 [10 Marks] — Function Approximation | Linear FA | Semi-Gradient
TD

Scenario: A robotic arm uses linear function approximation to estimate Q-values for joint
control. States are described by feature vectors using coarse coding. State S1 has feature
vector phi(S1) = [1, 0, 1]^T and State S2 has phi(S2) = [1, 1, 0]^T. Actions: {Extend (E),
Retract (R)}. Initial parameter vector theta_E = [0.5, 0.3, 0.2]^T (for Extend action). Discount
gamma = 0.8, learning rate alpha = 0.5.  a) Compute Q(S1, E) and Q(S2, E) using linear
function approximation: Q(s,a) = theta^T * phi(s). [2 Marks] b) A transition is observed: (S1,
E, reward=+4, S2). Using semi-gradient SARSA, compute the TD error and update theta_E.
Assume the agent next selects action E at S2. [5 Marks] c) Explain coarse coding as used in
part (a). What are its advantages over tabular methods in large/continuous state spaces? [3
Marks]

MODEL ANSWER

a) Linear Function Approximation:

Q(s, a) = theta_a^T * phi(s)

Q(S1, E) = [0.5, 0.3, 0.2] . [1, 0, 1] = 0.5*1 + 0.3*0 + 0.2*1 = 0.7

Q(S2, E) = [0.5, 0.3, 0.2] . [1, 1, 0] = 0.5*1 + 0.3*1 + 0.2*0 = 0.8

b) Semi-Gradient SARSA Update:

TD Target: R + gamma * Q(S2, A') = 4 + 0.8 * Q(S2, E) = 4 + 0.8 * 0.8 = 4.64

TD Error: delta = Target - Q(S1, E) = 4.64 - 0.7 = 3.94

Semi-gradient update rule:

theta <- theta + alpha * delta * gradient_theta Q(S1, E, theta)

For linear Q: gradient = phi(S1) = [1, 0, 1]^T

theta_E_new = [0.5, 0.3, 0.2]^T + 0.5 * 3.94 * [1, 0, 1]^T

= [0.5, 0.3, 0.2]^T + [1.97, 0, 1.97]^T

= [2.47, 0.3, 2.17]^T

Note: theta2 (0.3) did not change because phi(S1)[2] = 0 — feature F2 is inactive in S1.

c) Coarse Coding:

Coarse coding represents a state by which features (circles/receptive fields) are active. Each
feature Fi has a specific activation rule (e.g., F1=1 if mastery is Partial or Strong). A state's
representation phi(s) is a binary vector of active features.

Advantages over tabular methods:

1. Generalization: States sharing active features share weight updates. Learning in one
region of the state space transfers to similar regions.

2. Scalability: Works for large or continuous state spaces where a table would need
exponentially many entries.

3. Compact: A small feature vector can represent a huge state space efficiently.

4. Function approximation enables learning even in unseen states, as long as they have
similar feature activations.

Source: Study Material: Notes Pages 18-49 (Function Approximation, Coarse Coding, Semi-Gradient TD)

QUESTION 10 [10 Marks] — Deep Q-Network | Experience Replay | Target
Network | DDQN

Scenario: A game-playing AI agent (like the T-Rex Chrome Dino game) uses DQN. State
features phi(S1)=[1,0,0], phi(S2)=[1,1,0]. Actions: 0 (Jump), 1 (Duck). theta=[1.0, 0.5, 1.0]
(online network), theta'=[0.1, 0.3, 1.0] (target network). Gamma=0.2, alpha=0.9.  Transition:
(S1, a=0, reward=+2, S2)  a) Compute the DQN update for theta using the transition above.
Show Q(S1,0) estimate and the TD target using the target network. [4 Marks] b) Double
DQN is used to fix the maximization bias. Using the same transition, compute the Double
DQN target and the resulting theta update. [3 Marks] c) State and explain TWO key
techniques DQN uses to stabilize training. Why does each address the instability problem?
[3 Marks]

MODEL ANSWER

a) Standard DQN Update:

Q(S1, a=0, theta) = theta^T * phi(S1) = [1.0, 0.5, 1.0] . [1,0,0] = 1.0

DQN Target: y = R + gamma * max_a Q(S2, a, theta')

Q(S2, 0, theta') = [0.1, 0.3, 1.0] . [1,1,0] = 0.1 + 0.3 = 0.4

Q(S2, 1, theta') = [0.1, 0.3, 1.0] . [1,1,0] = 0.4 (assuming action 1 same features)

[Note: for action 1 using features [1,1,1]: Q(S2,1,theta') = 0.1+0.3+1.0 = 1.4]

y = 2 + 0.2 * max{Q(S2,0,theta'), Q(S2,1,theta')} = 2 + 0.2 * 1.4 = 2.28

TD Error: delta = y - Q(S1,0,theta) = 2.28 - 1.0 = 1.28

theta_new = theta + alpha * delta * phi(S1) = [1.0,0.5,1.0] + 0.9*1.28*[1,0,0]

= [1.0+1.152, 0.5, 1.0] = [2.152, 0.5, 1.0]

b) Double DQN Update:

Step 1 - Action Selection using ONLINE network theta:

a* = argmax_a Q(S2, a, theta)

Q(S2,0,theta)=[1.0,0.5,1.0].[1,1,0]=1.5; Q(S2,1,theta)=[1.0,0.5,1.0].[1,1,1]=2.5

a* = argmax = action 1 (value 2.5)

Step 2 - Action Evaluation using TARGET network theta':

Q(S2, a*=1, theta') = [0.1,0.3,1.0].[1,1,1] = 1.4

Double DQN Target: y = 2 + 0.2 * 1.4 = 2.28

This matches here, but the key benefit: when the online network overestimates one action,
the target network corrects it, reducing maximization bias.

c) Two Key DQN Stabilization Techniques:

1. Experience Replay: The agent stores past transitions (s, a, r, s') in a replay buffer. During
training, mini-batches are randomly sampled from this buffer. This breaks the temporal
correlation between consecutive transitions (which causes instability in gradient updates)
and allows the agent to reuse past data multiple times, improving sample efficiency.

2. Target Network: A separate copy of the Q-network (theta') is kept fixed for multiple training
steps and updated periodically. The TD target y = R + gamma * max Q(s', a, theta') remains
stable across updates. Without this, the target changes every step as theta changes,
creating a moving target problem that causes oscillations and divergence.

Source: Study Material: Lectures 12-13, Pages 46-49 (DQN, DDQN, Experience Replay, Target Network)

TOPIC 7: Policy Gradient Methods

QUESTION 11 [10 Marks] — Policy Gradient | REINFORCE | Baseline | Policy
Update

Scenario: A smart traffic signal controller learns action selection using policy gradient. States
represent congestion levels: Low (L), Medium (M), High (H). Actions: Extend-Green (EG),
Extend-Red (ER). The policy is parameterized as pi(a|s) = softmax(theta^T * phi(s)).  For
state M: phi(M) = [1, 1, 0]^T. theta_EG = [0.3, 0.2, 0.1]^T, theta_ER = [0.0, 0.0, 0.0]^T.  a)
Compute pi(EG|M) and pi(ER|M) using softmax. [2 Marks] b) The agent observes trajectory
(M, EG, +3, Terminal). Baseline b=1.5. Using REINFORCE with baseline and alpha=0.1,
compute the updated theta_EG. Show the gradient computation. [5 Marks] c) What is the
role of the baseline in REINFORCE? Does it introduce bias into the policy gradient? Explain
mathematically or intuitively. [3 Marks]

MODEL ANSWER

a) Softmax Policy Computation:

h(EG|M) = theta_EG^T * phi(M) = [0.3,0.2,0.1].[1,1,0] = 0.3+0.2 = 0.5

h(ER|M) = theta_ER^T * phi(M) = [0,0,0].[1,1,0] = 0.0

pi(EG|M) = exp(0.5) / (exp(0.5) + exp(0.0)) = 1.6487 / (1.6487 + 1.0) = 1.6487 / 2.6487 =
0.6226

pi(ER|M) = 1.0 / 2.6487 = 0.3774

b) REINFORCE with Baseline Update:

REINFORCE update rule (with baseline):

theta_EG <- theta_EG + alpha * (G - b) * gradient_theta ln pi(EG|M)

G = 3 (observed return), b = 1.5 (baseline)

(G - b) = 3 - 1.5 = 1.5

Gradient of log policy for softmax:

gradient_theta_EG ln pi(EG|M) = phi(M) - pi(EG|M) * phi(M) = (1 - pi(EG|M)) * phi(M)

= (1 - 0.6226) * [1, 1, 0]^T = 0.3774 * [1, 1, 0]^T = [0.3774, 0.3774, 0]^T

Update:

theta_EG_new = [0.3, 0.2, 0.1]^T + 0.1 * 1.5 * [0.3774, 0.3774, 0]^T

= [0.3, 0.2, 0.1]^T + [0.0566, 0.0566, 0]^T

= [0.3566, 0.2566, 0.1]^T

Since G > b, the gradient is positive and the parameters are reinforced — EG becomes more
likely at M.

c) Role of Baseline:

The baseline b (which can be a constant or the value function V(s)) is subtracted from the
return G to form the advantage estimate (G - b).

Bias: The baseline does NOT introduce bias into the policy gradient. The policy gradient
theorem states: gradient J(theta) = E[gradient ln pi(a|s) * G_t]. The expectation of gradient ln
pi(a|s) is 0 (it sums to zero over all actions), so adding any state-dependent baseline leaves
the expected gradient unchanged.

Variance reduction: The baseline reduces the variance of gradient estimates. Without
baseline, G values can be very large or noisy, causing high-variance gradient steps. With
b=V(s), the term (G-b) is the advantage function A(s,a), which is centered around 0 and has
lower variance.

Intuition: With baseline, the agent reinforces actions that performed BETTER than expected
(advantage > 0) and discourages those that performed worse (advantage < 0), enabling
more stable learning.

Source: Study Material: Lecture Notes on Policy Gradient (Pages on REINFORCE, Baseline, Actor-Critic)

QUESTION 12 [10 Marks] — Actor-Critic | A2C | Lane Keeping Scenario

Scenario: An autonomous lane-keeping assistant uses the Actor-Critic (A2C) algorithm.
States: {Left (L), Center (C), Right (R)}. Actions: {Steer-Left (-0.3), Straight (-0), Steer-Right
(+0.3)}. The policy network (actor) has parameter theta_old = [-0.5, 0, 0.5]^T. Value
estimates (critic): V(L)=0.3, V(C)=0.9, V(R)=0.2. Learning rate alpha_theta = 0.01. Gamma =
1.0.  Trajectory 1: (S0=Left, a=-0.3, r=+1, S1=Center)  a) Compute the TD error (advantage)
for this transition. [2 Marks] b) Using the Actor-Critic update rule, compute the gradient of the
log policy and update theta. The softmax policy at state Left gives pi(-0.3|Left) = 0.3. [4
Marks] c) Compare the Monte Carlo policy gradient (REINFORCE) with Actor-Critic in terms
of: update frequency, variance, and suitability for continuing vs. episodic tasks. [4 Marks]

MODEL ANSWER

a) TD Error (Advantage):

TD Error delta = r + gamma * V(S1) - V(S0)

= 1 + 1.0 * V(Center) - V(Left)

= 1 + 0.9 - 0.3 = 1.6

This positive TD error means the agent performed better than expected, and the actor
should reinforce the action taken.

b) Actor-Critic Update:

Actor update rule: theta_new = theta_old + alpha_theta * delta * gradient_theta ln pi(a|s)

For softmax policy, the gradient of log policy:

gradient ln pi(a=-0.3|Left) = phi(Left) * (1 - pi(-0.3|Left))

We use feature vector phi(Left) = [1, 0, 0]^T (Left state indicator)

gradient = (1 - 0.3) * [1, 0, 0]^T = 0.7 * [1, 0, 0]^T = [0.7, 0, 0]^T

Update:

theta_new = [-0.5, 0, 0.5]^T + 0.01 * 1.6 * [0.7, 0, 0]^T

= [-0.5, 0, 0.5]^T + [0.0112, 0, 0]^T

= [-0.4888, 0, 0.5]^T

The first parameter increases (less negative), making the Left action slightly more likely at
Left state.

c) REINFORCE vs. Actor-Critic Comparison:

Update Frequency:

REINFORCE (MC): Updates occur ONCE per complete episode. Must wait until episode
terminates to compute G.

Actor-Critic (TD-based): Updates occur EVERY TIME STEP using TD error. Can update
online without waiting for episode end.

Variance:

REINFORCE: HIGH variance because the return G can vary significantly across episodes.
The full trajectory contributes to each update.

Actor-Critic: LOWER variance due to TD bootstrapping. The critic provides a stable baseline
(V(s)) that reduces gradient variance.

Bias:

REINFORCE: Unbiased (uses actual returns).

Actor-Critic: Biased (bootstrap estimate from critic which may be inaccurate early in training).

Suitability:

REINFORCE: Suited for EPISODIC tasks where full trajectories are available and
reasonable in length.

Actor-Critic: Suited for CONTINUING tasks and long/infinite-horizon problems. Its online
updates and lower variance make it preferable for real-time systems like the lane-keeping
assistant.

Source: Study Material: Lecture Notes on Actor-Critic, A2C (Pages on Lane Keeping, Policy Gradient with TD)

TOPIC 8: Monte Carlo Tree Search (MCTS) and
AlphaGo/AlphaZero

QUESTION 13 [10 Marks] — MCTS | UCB for Trees | AlphaGo vs AlphaZero

Scenario: A game AI company builds a strategy game agent using Monte Carlo Tree Search
(MCTS). A node in the search tree at state s has three available actions: a1, a2, a3. The
stored statistics are:  a1: N(s,a1)=8, Q(s,a1)=0.72 | a2: N(s,a2)=25, Q(s,a2)=0.68 | a3:
N(s,a3)=2, Q(s,a3)=0.80  Total visits to parent node N(s) = 35.  a) Compute the UCB score
for all three actions using the PUCT formula: UCB(s,a) = Q(s,a) + c * sqrt(ln(N(s)) / N(s,a))
with c=1.5. Which action is selected next? [4 Marks] b) Describe the four phases of MCTS
(Selection, Expansion, Simulation, Backpropagation) in the context of this game agent. [4
Marks] c) State ONE key difference between AlphaGo and AlphaZero in terms of training
data. Why does this design choice make AlphaZero more generalizable? [2 Marks]

MODEL ANSWER

a) UCB Score Computation (c=1.5, N(s)=35):

UCB(s,a) = Q(s,a) + 1.5 * sqrt(ln(35) / N(s,a))

ln(35) = 3.5553

UCB(s, a1) = 0.72 + 1.5 * sqrt(3.5553 / 8) = 0.72 + 1.5 * sqrt(0.4444)

= 0.72 + 1.5 * 0.6667 = 0.72 + 1.000 = 1.720

UCB(s, a2) = 0.68 + 1.5 * sqrt(3.5553 / 25) = 0.68 + 1.5 * sqrt(0.1422)

= 0.68 + 1.5 * 0.3771 = 0.68 + 0.566 = 1.246

UCB(s, a3) = 0.80 + 1.5 * sqrt(3.5553 / 2) = 0.80 + 1.5 * sqrt(1.7777)

= 0.80 + 1.5 * 1.3333 = 0.80 + 2.000 = 2.800

Selected action: a3 (UCB = 2.800)

Justification: a3 has high UCB due to very few visits (N=2), making the uncertainty term
large. Despite having the highest Q-value (0.80), it was underexplored.

b) Four Phases of MCTS:

1. SELECTION: Starting from the root node (current game state), the algorithm traverses the
tree by selecting child nodes that maximize UCB scores. This balances exploitation (high Q)
with exploration (low N) until a leaf node or unexplored node is reached.

2. EXPANSION: At the selected leaf node, one or more new child nodes are created by
expanding untried actions. In the game agent, this means adding a new game state reached
by taking an unexplored action.

3. SIMULATION (Rollout): From the newly expanded node, a random (or policy-guided in
AlphaZero) simulation is run until a terminal game state is reached. The outcome
(win/loss/draw) provides a reward signal.

4. BACKPROPAGATION: The simulation result is propagated back up the tree, updating the
visit count N(s,a) and mean value Q(s,a) at each node along the path. This allows the tree to
learn which actions lead to better outcomes over many iterations.

c) AlphaGo vs AlphaZero:

AlphaGo: Trained using human expert game data (supervised learning on human moves)
combined with self-play reinforcement learning. Its policy and value networks were initialized
from human knowledge.

AlphaZero: Trained entirely through SELF-PLAY from random initialization, with NO human
game data. It started from scratch and discovered strategies independently.

Why AlphaZero is more generalizable: Since it does not rely on domain-specific human data,
the same algorithm can be applied to other games (Chess, Shogi) without any modification
or expert data collection. It is a truly general algorithm, not limited by the availability or quality
of human expert demonstrations.

Source: Study Material: Lectures 14-15, Pages 3-30 (MCTS, UCB, AlphaGo, AlphaZero)

QUESTION 14 [10 Marks] — Model-Based RL | MCTS Deep Dive | MuZero

Scenario: A robotics company builds a planning system using model-based RL for a maze
navigation task. The robot has a known model of the maze dynamics.  a) Explain the
advantages and challenges of model-based RL compared to model-free RL (TD/MC) in the
context of maze navigation. [3 Marks] b) In MCTS applied to maze navigation, explain what
role the UCB term (exploration bonus) plays in the search, and what would happen if c=0
(pure exploitation). [3 Marks] c) MuZero extends AlphaZero to unknown environments.
Briefly explain how MuZero handles the unknown dynamics compared to AlphaZero, and
give one application where this capability is critical. [4 Marks]

MODEL ANSWER

a) Model-Based vs Model-Free in Maze Navigation:

Advantages of Model-Based RL:

1. Sample Efficiency: The robot can simulate trajectories 'in its head' using the known model,
without physically moving. This requires far fewer real-world interactions.

2. Planning: The agent can evaluate the consequences of actions many steps ahead,
enabling more informed decisions at each junction.

3. Imagined Experience: The model allows generation of synthetic training data to
supplement real experience.

Challenges:

1. Model Accuracy: Even small errors in the model compound over many planning steps,
leading to inaccurate predictions and poor decisions.

2. Scalability: For a large maze with complex dynamics, building an accurate model may
itself be intractable.

3. Model Bias: If the model is wrong, the agent may optimally solve the wrong problem.

Model-Free (TD/MC): Does not require a model but needs many real environment
interactions to learn. Better when the model is unavailable or too complex to specify.

b) UCB Exploration Term in Maze MCTS:

UCB(s,a) = Q(s,a) + c * sqrt(ln(N(s)) / N(s,a))

The exploration term c * sqrt(ln(N(s))/N(s,a)) increases when an action has been tried fewer
times (low N(s,a)). This encourages the tree search to explore paths not yet well-
characterized, preventing premature convergence to a local optimum (e.g., the first found
path that may not be optimal).

If c=0 (pure exploitation): The algorithm always selects the action with the highest current
Q(s,a) estimate. In the maze, this could cause it to repeatedly explore the same branch that
happens to have a good initial estimate, missing better paths in unexplored corridors. The
tree search degenerates into a greedy search with no exploration guarantee.

c) MuZero vs AlphaZero and Application:

AlphaZero: Requires a KNOWN environment model (perfect rules of the game). It uses the
true game dynamics for MCTS planning. Not directly applicable when dynamics are
unknown.

MuZero: Learns a LATENT model of the environment dynamics from experience. Instead of
using a given model, it trains three networks: a representation function (encoding states), a
dynamics function (predicting next state and reward), and a prediction function (policy and
value). MCTS planning is done in the learned latent space.

MuZero can thus plan effectively even when the environment rules are not explicitly provided
— it learns them from interaction.

Critical Application: Video games like Atari, where the physics engine and reward dynamics
are not explicitly programmed into the agent. MuZero can learn these dynamics purely from
pixel observations and plan using the learned model, achieving superhuman performance
without any given model of the game rules.

Source: Study Material: Lectures 14-15, Pages 4-15 (Model-Based RL, MCTS, AlphaZero, MuZero)

TOPIC 9: Imitation Learning (Behavioral Cloning and DAGGER)

QUESTION 15 [10 Marks] — Imitation Learning | Behavioral Cloning |
Distributional Shift

Scenario: A recycling robot learns sorting policies from expert demonstrations. The robot
operates in states based on Battery Level: {High (H), Low (L)}. Actions: {Search (Se),
Recharge (Re), Wait (W)}. Expert policy: pi_expert(H)=Search, pi_expert(L)=Recharge.  The
agent is trained via behavioral cloning and develops agent policy: pi_agent(H)=Search,
pi_agent(L)=Wait.  a) The agent rolls out episode: (H, Se, +1, L) -> (L, W, 0, L) -> (L, W, 0, L)
-> (L, W, 0, L)... Compute the behavioral cloning loss after 4 steps. What problem does this
illustrate? [4 Marks] b) Explain DAGGER (Dataset Aggregation) and how it addresses the
problem identified in (a). Use the recycling robot to illustrate. [4 Marks] c) Compare
Behavioral Cloning and DAGGER on the dimensions of: data collection, compounding error,
and convergence guarantee. [2 Marks]

MODEL ANSWER

a) Behavioral Cloning Loss and Distributional Shift:

Loss L(theta) = (1/T) * sum_t [ 1(pi_expert(State_t) != pi_agent(State_t)) ]

Step 1: State H. pi_expert(H)=Se, pi_agent(H)=Se. Match -> loss contribution = 0

Step 2: State L. pi_expert(L)=Re, pi_agent(L)=W. Mismatch -> loss contribution = 1

Step 3: State L. Mismatch (agent stuck in Wait). loss = 1

Step 4: State L. Mismatch. loss = 1

Total Loss after 4 steps: L = (0+1+1+1)/4 = 0.75

Problem - Distributional Shift (Compounding Error): Behavioral cloning trains on expert state
distributions. But once the agent deviates from the expert trajectory (e.g., by waiting instead
of recharging at Low), it enters states the expert never demonstrated. Without training data
for these states, errors compound. The agent stays stuck in Low battery state indefinitely, a
pattern never seen in expert data. This is the covariate shift problem — the training and
execution distributions diverge.

b) DAGGER Solution:

DAGGER (Dataset Aggregation) iteratively collects new training data from states the AGENT
visits (not just expert states), and labels them with EXPERT actions.

Algorithm steps:

1. Train initial policy pi_1 from expert demonstrations using supervised learning.

2. Rollout: Execute a mixture policy pi_mix = beta * pi_expert + (1-beta) * pi_agent. This
visits states the agent actually reaches.

3. Query expert: For every state visited in the rollout, ask the expert what action should be
taken.

4. Aggregate dataset: Add (state, expert_action) pairs from the rollout to the existing dataset.

5. Retrain policy on the aggregated dataset.

6. Repeat, gradually reducing beta.

Recycling Robot Example: DAGGER rollout visits Low battery state (which the expert never
visits in a well-functioning robot). The expert labels Low state with 'Recharge'. This state-
action pair is added to the dataset. After retraining, pi_agent(L)=Re, eliminating the stuck-in-
Wait problem.

c) Behavioral Cloning vs DAGGER:

Data Collection: BC collects data ONLY from expert trajectories (offline). DAGGER collects
data from states the AGENT visits (online, iterative).

Compounding Error: BC suffers severely from compounding error due to distributional shift.
DAGGER explicitly addresses this by training on agent-visited states.

Convergence Guarantee: BC has no formal guarantee for long rollouts. DAGGER provides a
theoretical guarantee of sublinear regret — the performance gap between agent and expert
shrinks as more iterations are run, under mild assumptions.

Source: Study Material: Lectures 14-15, Pages (Behavioral Cloning, DAGGER, Recycling Robot Example)

MIXED TOPIC PRACTICE QUESTIONS

QUESTION 16 [10 Marks] — Mixed | MDP + TD + Policy Iteration | Smart Grid

Scenario: A smart electricity grid management system operates as an MDP. States: {Low-
Demand (LD), Peak-Demand (PD), Critical (CR)}. Actions: {Normal (N), Boost (B),
Emergency (E)}. Gamma=0.8.  Transition probabilities and rewards: LD+N->LD
(p=0.7,r=+2), LD+N->PD (p=0.3,r=+1) LD+B->PD (p=1.0,r=+3) PD+N->PD (p=0.5,r=+1),
PD+N->CR (p=0.5,r=-2) PD+B->LD (p=0.6,r=+4), PD+B->PD (p=0.4,r=+2) CR+N->CR
(p=1.0,r=-5) CR+E->PD (p=1.0,r=-1)  V(LD)=3, V(PD)=5, V(CR)=-2 (current estimates).
Current policy pi: pi(N|LD)=1, pi(N|PD)=1, pi(E|CR)=1.  a) Write and evaluate Bellman
expectation equations for V_pi(LD) and V_pi(PD) using current estimates. [3 Marks] b) Using
policy improvement, determine if the policy should change at state PD. Compute Q_pi(PD,N)
and Q_pi(PD,B). [4 Marks] c) After one SARSA update with alpha=0.5, compute the updated
Q(PD, N) given the transition (PD, N, -2, CR) where the next action taken is E. [3 Marks]

MODEL ANSWER

a) Bellman Expectation Equations:

V_pi(LD) = sum P(s'|LD,N) * [R + gamma * V(s')]

= P(LD|LD,N)*[2+0.8*V(LD)] + P(PD|LD,N)*[1+0.8*V(PD)]

= 0.7*[2+0.8*3] + 0.3*[1+0.8*5]

= 0.7*[2+2.4] + 0.3*[1+4.0]

= 0.7*4.4 + 0.3*5.0 = 3.08 + 1.5 = 4.58

V_pi(PD) = P(PD|PD,N)*[1+0.8*V(PD)] + P(CR|PD,N)*[-2+0.8*V(CR)]

= 0.5*[1+0.8*5] + 0.5*[-2+0.8*(-2)]

= 0.5*[1+4.0] + 0.5*[-2-1.6]

= 0.5*5.0 + 0.5*(-3.6) = 2.5 - 1.8 = 0.7

b) Policy Improvement at PD:

Q_pi(PD, N) = V_pi(PD) computed above = 0.7 [from Bellman; or directly:] 0.7

Q_pi(PD, B) = P(LD|PD,B)*[4+0.8*V(LD)] + P(PD|PD,B)*[2+0.8*V(PD)]

= 0.6*[4+0.8*3] + 0.4*[2+0.8*5]

= 0.6*[4+2.4] + 0.4*[2+4.0]

= 0.6*6.4 + 0.4*6.0 = 3.84 + 2.4 = 6.24

Q_pi(PD, B) = 6.24 >> Q_pi(PD, N) = 0.7

Policy SHOULD change: pi_1(B|PD) = 1.0 (switch from Normal to Boost at Peak
Demand)

c) SARSA Update Q(PD, N):

SARSA: Q(St, At) <- Q(St, At) + alpha * [R + gamma * Q(St+1, At+1) - Q(St, At)]

Transition: (PD, N, -2, CR, E)

Assuming Q(PD,N) current = 0.7 (from Bellman), Q(CR,E) = 0 (or initial estimate)

Q(PD,N) <- 0.7 + 0.5 * [-2 + 0.8*0 - 0.7]

= 0.7 + 0.5 * [-2 - 0.7]

= 0.7 + 0.5 * (-2.7) = 0.7 - 1.35 = -0.65

The SARSA update significantly reduces Q(PD,N) because transitioning to Critical state with
negative reward confirms that Normal action at Peak Demand is poor.

Source: Study Material: Lectures 3-9 (MDP Bellman, Policy Iteration, SARSA)

QUESTION 17 [10 Marks] — Mixed | Function Approximation + Policy Gradient |
Coarse Coding

Scenario: An AI tutor platform assigns tasks of difficulty {Easy (E), Hard (H)} to learners
based on their state {Novice (N), Intermediate (I), Expert (Ex)} and engagement {Active (A),
Passive (P)}.  Coarse coding features: F1=1 if learner is Intermediate or Expert; F2=1 if
Passive; F3=1 if Intermediate AND Passive.  States observed: S1=(I,P), S2=(N,A)  a)
Compute feature vectors phi(S1) and phi(S2) using the coarse coding rules above. [2 Marks]
b) Using theta^T_H = [0.3, 0.2, 0.1] for Hard task and theta^T_E = [0, 0, 0] for Easy task,
compute pi(H|S1) and pi(E|S1) using softmax. [3 Marks] c) Observation at t0: (S1=(I,P),
action=H, S2=(I,P), reward=+3). Baseline=1. Perform a REINFORCE-with-baseline policy
gradient update for theta_H with alpha=0.05. [3 Marks] d) Explain the role of the Actor vs
Critic in A2C applied to the AI tutor scenario. [2 Marks]

MODEL ANSWER

a) Feature Vectors:

Rules: F1=1 if (Intermediate OR Expert); F2=1 if Passive; F3=1 if (Intermediate AND
Passive)

S1 = (Intermediate, Passive):

F1=1 (Intermediate), F2=1 (Passive), F3=1 (Intermediate AND Passive)

phi(S1) = [1, 1, 1]^T

S2 = (Novice, Active):

F1=0 (Novice), F2=0 (Active), F3=0

phi(S2) = [0, 0, 0]^T

b) Softmax Policy at S1:

h(H|S1) = theta_H^T . phi(S1) = [0.3, 0.2, 0.1] . [1,1,1] = 0.3+0.2+0.1 = 0.6

h(E|S1) = theta_E^T . phi(S1) = [0,0,0] . [1,1,1] = 0.0

pi(H|S1) = exp(0.6) / (exp(0.6) + exp(0.0)) = 1.8221 / (1.8221 + 1.0) = 1.8221 / 2.8221 =
0.6456

pi(E|S1) = 1.0 / 2.8221 = 0.3544

c) REINFORCE with Baseline Update:

G = +3 (return), b = 1 (baseline)

Advantage = G - b = 3 - 1 = 2

Gradient of log pi(H|S1): grad = (1 - pi(H|S1)) * phi(S1) = (1 - 0.6456) * [1,1,1]^T = 0.3544 *
[1,1,1]^T

Update: theta_H_new = theta_H_old + alpha * (G-b) * grad

= [0.3, 0.2, 0.1]^T + 0.05 * 2 * 0.3544 * [1,1,1]^T

= [0.3, 0.2, 0.1]^T + [0.03544, 0.03544, 0.03544]^T

= [0.3354, 0.2354, 0.1354]^T

Since reward (+3) > baseline (1), Hard task is reinforced at the (Intermediate, Passive) state.

d) Actor vs Critic in A2C for AI Tutor:

Actor (Policy Network theta): Decides WHICH task difficulty to assign (Easy or Hard) based
on learner state. Outputs action probabilities pi(H|s) and pi(E|s). Learns by updating theta to
increase probability of actions with positive advantage.

Critic (Value Network w): Estimates the expected future reward (learning progress) from the
current learner state: V_w(s). This estimate serves as the baseline for advantage
computation. The critic tells the actor how good or bad the current state is relative to the
average, guiding more stable and faster policy updates.

Source: Study Material: Question 3 sample paper; Lecture Notes on Function Approximation, Policy Gradient, Actor-Critic

QUESTION 18 [10 Marks] — Mixed | TD + Exploration | Non-Stationary Bandit |
RL Comparison

Scenario: A clinical decision support system uses RL to recommend between 3 treatments:
Drug A (DA), Drug B (DB), Therapy (T). Patient response changes over time (non-stationary
environment). The system has been running for 10 time steps with the following record:  DA:
selected 4 times, rewards: [+1, -1, +1, +1], Q_avg(DA)=0.5 DB: selected 3 times, rewards:
[+1, +1, -1], Q_avg(DB)=0.333 T: selected 3 times, rewards: [-1, +1, +1], Q_avg(T)=0.333  a)
At time step 11, compute UCB scores for DA, DB, T using c=1.0 and sample averages.
Which treatment is selected? [3 Marks] b) The system switches to a non-stationary Q update
with alpha=0.3. Given Q_prev(T)=0.333 and the next observation R(T)=+1, compute
Q_new(T). Compare this updated value to the sample average approach. [3 Marks] c) Justify
why TD-based approaches (SARSA/Q-learning) are generally preferred over Monte Carlo
methods in this clinical scenario and over Dynamic Programming in any real-world medical
AI. [4 Marks]

MODEL ANSWER

a) UCB Score at t=11 (c=1.0):

UCB(a) = Q(a) + c * sqrt(ln(t) / N(a)), t=10, ln(10)=2.3026

UCB(DA) = 0.5 + 1.0 * sqrt(2.3026/4) = 0.5 + sqrt(0.5757) = 0.5 + 0.7588 = 1.2588

UCB(DB) = 0.333 + 1.0 * sqrt(2.3026/3) = 0.333 + sqrt(0.7675) = 0.333 + 0.8761 = 1.2091

UCB(T) = 0.333 + 1.0 * sqrt(2.3026/3) = 0.333 + 0.8761 = 1.2091

Selected: Drug A (DA) with UCB = 1.2588

DA wins because it has been tried more often (higher N=4 means lower exploration bonus),
but its high Q-value of 0.5 compensates. DB and T tie at 1.2091.

b) Non-Stationary Q Update for T:

Non-stationary update: Q_new(T) = Q_old(T) + alpha * (R - Q_old(T))

= 0.333 + 0.3 * (1 - 0.333) = 0.333 + 0.3 * 0.667 = 0.333 + 0.200 = 0.533

Sample average update: Q_new = (3*0.333 + 1) / 4 = (1.0 + 1) / 4 = 0.5

Non-stationary gives Q(T) = 0.533 vs sample average 0.500.

Non-stationary weights recent reward (+1) more heavily, giving a higher estimate. This is
appropriate in a clinical setting where patient response patterns may shift over time (e.g.,
due to tolerance, comorbidities, or seasonal factors).

c) Justification for TD over MC and DP:

TD vs Monte Carlo:

In clinical settings, patient episodes may be VERY LONG (chronic disease management).
MC would require waiting for the full treatment episode to terminate before updating values
— impractical for months-long treatments. TD updates happen after each visit/prescription,
enabling real-time learning.

TD has lower variance than MC (bootstrap from one-step), important for clinical data which is
noisy and limited. Delayed feedback (patient outcome after weeks) makes MC's full-episode
requirement infeasible.

TD vs Dynamic Programming:

DP requires a COMPLETE MODEL of the environment — i.e., P(outcome | patient state,
treatment) for all states. In medical AI, this transition model is unknown and cannot be
specified accurately due to patient heterogeneity.

DP also requires sweeping all states, which is computationally intractable for the high-
dimensional patient state space (lab values, age, diagnosis codes, etc.).

TD is MODEL-FREE and ONLINE — it learns from real patient data without requiring a pre-
specified model, making it uniquely suitable for real-world clinical decision support.

Source: Study Material: Lectures 1-9, All Topics (Bandit, TD, MC, DP comparison)

Summary: Topics and Question Mapping

Topic

Key Concepts

Q#

Q1

Q2

Q3

Q4

Q5

Q6

Q7

Q8

Q9

K-Armed Bandit

K-Armed Bandit

MDP

Dynamic Programming

Monte Carlo

Monte Carlo

TD Learning

TD Learning

Function Approx

Q10

DQN / DDQN

Q11

Policy Gradient

Q12

Actor-Critic

Q13

MCTS / AlphaGo

Q14

Model-Based RL

Q15

Imitation Learning

UCB, Sample Avg, Non-
Stationary

Epsilon-greedy, Gradient
Bandit, Softmax

Bellman Expectation,
Bellman Optimality, Policy

Policy Eval, Policy
Improvement, Value
Iteration

First-Visit MC, Importance
Sampling, Off-Policy

Every-Visit MC, On-Policy
vs Off-Policy, MC Control

SARSA, Q-Learning, TD
Error, On vs Off Policy

Expected SARSA, Double
Q-Learning, Max Bias

Linear FA, Coarse Coding,
Semi-Gradient TD

DQN, Double DQN,
Experience Replay, Target
Net

REINFORCE, Baseline,
Softmax Policy

A2C, TD Error, Online
Updates, Variance

UCB in MCTS, 4 Phases,
AlphaZero Training Data

MCTS, MuZero, Model vs
Model-Free

Behavioral Cloning,
DAGGER, Distributional
Shift

Pages (Study
Material)

Lec 1-3, pp.19-46

Lec 1-3, pp.29-57

Lec 3-5, pp.21-32

Lec 3-5, pp.42-50

Lec 6-8, pp.7-40

Lec 6-8, pp.7-30

Lec 9, pp.3-20

Notes pp.80-90

Notes pp.18-49

Lec 12-13, pp.46-
49

Lec Notes PG

Lec Notes A2C

Lec 14-15, pp.3-30

Lec 14-15, pp.4-15

Lec 14-15,
pp.11219

Q16

Q17

Mixed

Mixed

MDP + TD + Policy Iteration  All Lectures

Coarse Coding + Policy
Gradient + A2C

All Lectures

Q18

Mixed

Bandit + TD + DP
Comparison

All Lectures

End of Practice Question Bank — All Topics Covered
AIMLCZG512 | Deep Reinforcement Learning | BITS Pilani

