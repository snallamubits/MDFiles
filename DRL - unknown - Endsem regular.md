QUESTION 1:

A reinforcement learning agent helps a healthcare professional choose between two treatments
for patient recovery. At each visit, the agent selects one of the two actions: Medication(M),
Therapy (T) where medication refers to standard drug-based treatment and therapy refers to
physical rehabilitation approach. The agent assumes a Multi-Armed Bandit model where
feedback (reward) is either +1 (Successful recovery) or -1 (No improvement). The
corresponding dataset comprising 8-time steps is given below:

a) Using the UCB formula with c = 1.0, what is the maximum reward value r for which the UCB
score of "Therapy" exceeds the UCB score of "Medication" at the 9th decision point?    [4 Marks]

Note : Reward r (cid:0) Set of Integers. Use a simple sample average method.

b) Suppose the agent uses a non-stationary approach for computing Q instead of sample
averages, with α =0.5. Using Q 1 (M) =0, compute Q(M) at t =9 as a function of r.     [4 Marks]

c) Comparatively analyse the Q value update methods used in part a) vs part b) and comment
on how sensitive the agent’s treatment choice is to the value of   r     [2 Marks]

QUESTION 2:

Scenario: A mobile robot operates in a warehouse with three battery states: Low (L), Medium
(M), and High (H). At each decision point, the robot can either Continue Working (C) or Go
Recharge (R).
MDP Specification:

States: {Low (L), Medium (M), High (H)} ; Actions: {Continue, Recharge}; Discount factor:
0.9; Current value estimates: V(L) = 1, V(M) = 1, V(H) = 1.

=

State transitions :

a) The robot currently follows policy π where π(Continue | M) = 1. Write the Bellman expectation
equation for V π(M) and calculate its value using the given estimates.     [2 Marks]

b) The robot starts with the following initial policy π₀: π₀(Continue | H) = 1.0 ; π₀(Continue | M) =
1.0 ; π₀(Recharge | L) = 1.0. Given: V⁰(L) = -10, V⁰(M) = 5, V⁰(H) = 8. Determine the improved
policy π₁ at state M by computing: Q π₀(M, Continue) ; Q π₀(M, Recharge) . Should the policy at
state M change? What is the new policy π₁(a|M)?     [4 Marks]

c)The robot executes the policy π (Continue at M, Recharge at L) and generates the following

= 0.9:

episode with
Episode: (M, Continue,+1, M) →(M, Continue, +1, L) →(L,Recharge, -3,M) → (M, Continue, +1,
Terminal).
Using First-Visit Monte Carlo, calculate the estimated value V(M) from this single episode. Show
the return calculation with proper discounting.

[1 Mark]

d) The robot now uses an exploratory behaviour policy b where: b(Continue | M) = 0.7;
b(Recharge | M) = 0.3 The target policy π is deterministic: π(Continue | M) = 1.0 Consider the

following episode under behavior policy b with

= 0.9:

Episode: (M,Continue,+1,M) → (M,Recharge,-2,H) → (H, Continue, +2, Terminal ).
Calculate:

   d-1) The importance sampling ratio ρ from the first occurrence of state M until termination
   d-2) The return G from state M
   d-3) Explain how this ratio would be used in weighted importance sampling to update V(M)

[3 Marks]

QUESTION 3:

Scenario: A personalized AI tutor platform curates tasks of varied difficulty level for practice as
{Medium (M), High (H)} based on learner mastery categorized into {Weak (W), Partial (P),
Strong (S)} and motivation level observed from their usage statistics including {Engaging (E),
Disengaging (D)}.
Rewards: For the Observation At time step t0 : (S, A, S`, R) = ( S1: (P, D), H , S2 = (P, D) , +2) ,
answer the following questions sequentially.

a) Transform the states (P, D), (P, E) using the following coarse coding:
Features : (F1, F2, F3) , ϕ(S) = [F1 F2 F3] T

 b) Use the function approximator π(_ |S) = θ  Tϕ(S) to compute the probability of choosing the
difficulty level of tasks. Assume θ  T = [0.2 , 0.1 , 0.05] for High‑difficulty task (H) and θ  T = [0, 0,
0] for Medium‑difficulty task (M).
Using the given model, perform a one step policy gradient update with α=0.05 for the given
observation to reinforce the model parameters with fixed baseline value of 1.

c) Compare the agent’s behavior when α=0.05 vs α=0.7. Comment on its effect on the speed
and stability of the learner.

d) In above subpart b) what will happen if the baseline is not considered? Explain w.r.t its impact
on given scenario ie., AI tutor only.

e) Assume the Actor Critic algorithm (eg.,A2C) is chosen to be applied to the given use case.
Briefly state the role of actor vs critic w.r.t the given scenario ie., AI tutor only.

[1+4+2+1+2= 10 Marks]

QUESTION 4:

(a) During the Selection phase of Monte Carlo Tree Search, a node corresponding to state s has
two available actions, a 1 and a 2. The stored statistics are:

Compute the UCB score for both actions. Which action will be selected next? Justify numerically
[3 Marks]

(b) The company trains a value network for leaf node evaluation using Deep Q-Network (DQN)
principles. State two key techniques DQN uses to stabilize deep neural network training and
briefly explain why each addresses instability.     [2 Marks]

(c) The MCTS algorithm is inspired by AlphaGo and AlphaZero. State one key difference
between AlphaGo and AlphaZero regarding their training data. Why does this make AlphaZero
more generalizable to other domains?     [2 Marks]

(d) The company uses imitation learning with expert demonstrations of gameplay.

    (d-1) Write the loss function for behavior cloning when training policy  π θ(a|s). State one
major failure mode when the policy encounters unseen states.     [1.5 Marks]
    (d-2) How does DAGGER modify the data collection process compared to behavior cloning?
Why does this help the policy handle its own mistakes?     [1.5 Marks]

