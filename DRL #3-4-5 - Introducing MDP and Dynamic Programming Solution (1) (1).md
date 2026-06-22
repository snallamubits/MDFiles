Deep Reinforcement Learning
2024-25 Second Semester, M.Tech (AIML)

Session #3-4-5:
Markov Decision Processes ,
Dynamic Programming Solutions

Session Instructor – Dr. Sangeetha Viswanathan

1

Agenda for the class

• Agent-Environment Interface  (Sequential Decision Problem)
• MDP

Defining MDP,
Rewards,
Returns, Policy &  Value Function,
Optimal Policy and Value Functions

• Approaches to solve MDP

Acknowledgements: Some of the slides were adopted with permission from the course CSCE-689 (Texas A&M University) by Prof.  Guni Sharon

2

Quick Recap

3

Exponentially Weighted Decay of Rewards

Non-stationary rewards: tracking a moving target by trusting recent experience most

Unrolling the recursion

T H E   U P D A T E   R U L E

Qn+1 = Qn + α [ Rn − Qn ]

R E W R I T E   A S   A   B L E N D ,   T H E N   S U B S T I T U T E   Q ₙ   I N T O   I T S E L F
Qn+1 = αRn + (1−α)·Qn
= αRn + α(1−α)Rn−1 + (1−α)2·Qn−1
= αRn + α(1−α)Rn−1 + α(1−α)2Rn−2 + (1−α)3·Qn−2

⋮ each step shrinks the leftover Q-term by another (1−α)

U N R O L L   A L L   T H E   W A Y   D O W N   T O   Q ₁     — C L O S E D   F O R M

Qn+1 = (1−α)nQ1 + Σ α(1−α)n−iRi

W E I G H T   O N   T H E   R E W A R D   i   S T E P S   B A C K

wi = α(1−α)n−i

older rewards (bigger n−i)
decay geometrically; weights sum to 1

Step-by-step working  (α = ½)

Rewards in order:  R₁=10, R₂=0, R₃=8, R₄=4 ·   Q₁ = 0

1

2

3

4

N E W   R E W A R D     R ₁   =   1 0
Q₂ = Q₁ + ½(R₁−Q₁) = 0 + ½(10−0) =

N E W   R E W A R D     R ₂   =   0
Q₃ = Q₂ + ½(R₂−Q₂) = 5 + ½(0−5) =

N E W   R E W A R D     R ₃   =   8
Q₄ = Q₃ + ½(R₃−Q₃) = 2.5 + ½(8−2.5) =

N E W   R E W A R D     R ₄   =   4
Q₅ = Q₄ + ½(R₄−Q₄) = 5.25 + ½(4−5.25) =

Weight each reward ends up carrying  (α = ½)

5.000

2.500

5.250

4.625

0.0625

R₁

0.125

R₂

0.25

R₃

0.50

R₄

Cross-check:  (1−α)⁴Q₁ + .0625(10) + .125(0) + .25(8) + .50(4) = 4.625 — the closed form and the step-by-step updates agree.

A different scenario

● Associative vs. Non-associative tasks ?
● Policy: A mapping from situations to the
actions that are best in those situations
● (discuss) How do we extend the solution for
non-associative task to an associative task?
○ Approach: Extend the solutions to non-stationary task to

non-associative tasks
■ Works, if the true action values changes slowly

○ What if the context switching between the situations are

made explicit?
■ How?
■ Need Special approaches !!!

5

6

Agent-Environment Interface

● Agent - Learner & the decision

maker

● Environment - Everything

outside the agent

● Interaction:

○ Agent performs an action
○ Environment responds by

■ presenting a new situation

(change in state)

■ presents numerical reward

● Objective (of the interaction):

○ Maximize the return

(cumulative rewards) over time

Note:

● Interaction occurs in discrete time steps

7

Grid World Example

● A maze-like problem

○ The agent lives in a grid
○ Walls block the agent’s path

● Noisy movement: actions do not always go as planned

○ 80% of the time, the action North takes the agent North

(if there is no wall there)

○ 10% of the time, North takes the agent West; 10% East
○ If there is a wall in the direction the agent would have

been taken, the agent stays put

● The agent receives rewards each time step

○ -0.1 per step (battery loss)
○ +1 if arriving at (4,3) ; -1 for arriving at (4,2) ;1 for arriving

at (2,2)

● Goal: maximize accumulated rewards

8

Markov Decision Processes

● An MDP is defined by
○ A set of states
○ A set of actions
○ State-transition probabilities

■ Probability of arriving to  after performing  at
■ Also called the model dynamics

○ A reward function

■ The utility gained from arriving to  after

performing  at

■ Sometimes just  or even

○ A start state
○ Maybe a terminal state

9

Markov Decision Processes

Model Dynamics

State-transition probabilities

Expected rewards for state–action–next-state triples

10

11

Markov Decision Processes - Discussion

● MDP framework is abstract and flexible

○ Time steps need not refer to fixed intervals of real time
○ The actions can be

■ at low-level controls or high-level decisions
■ totally mental or computational
○ States can take a wide variety of forms

■ Determined by low-level sensations or high-level and abstract (ex.

symbolic descriptions of objects in a room)

● The agent–environment boundary represents the limit of the agent’s absolute

control, not of its knowledge.
○ The boundary can be located at different places for different purposes

12

Markov Decision Processes - Discussion

● MDP framework is a considerable abstraction of the problem of goal-directed

learning from interaction.

● It proposes that whatever the details of the sensory, memory, and control
apparatus, and whatever objective one is trying to achieve, any problem of
learning goal-directed behavior can be reduced to three signals passing back
and forth between an agent and its environment:
○ one signal to represent the choices made by the agent (the actions)
○ one signal to represent the basis on which the choices are made (the

states),

○ and one signal to define the agent’s goal (the rewards).

13

MDP Formalization : Video Games

● State:

○ raw pixels

● Actions:

○ game controls

● Reward:

○ change in score

● State-transition probabilities:

○ defined by stochasticity in game evolution

Ref: Playing Atari with deep reinforcement learning”, Mnih et al., 2013

14

MDP Formalization : Traffic Signal Control

● State:

○ Current signal assignment (green, yellow,

and red assignment for each phase)
○ For each lane: number of approaching
vehicles, accumulated waiting time,
number of stopped vehicles, and average
speed of approaching vehicles

● Actions:

○ signal assignment

● Reward:

○ Reduction in traffic delay
● State-transition probabilities:

○ defined by stochasticity in approaching

demand

Ref: “Learning an Interpretable Traffic Signal Control Policy”, Ault et al., 2020

15

MDP Formalization : Recycling Robot (Detailed Ex.)

● Robot has

○ sensors for detecting cans
○ arm and gripper that can pick the cans and place in an

onboard bin;

● Runs on a rechargeable battery
● Its control system has components for interpreting sensory
information, for navigating, and for controlling the arm and
gripper

● Task for the RL Agent: Make high-level decisions about how
to search for cans based on the current charge level of the
battery

16

MDP Formalization : Recycling Robot (Detailed Ex.)

● State:

○ Assume that only two charge levels can be distinguished
○ S = {high, low}

● Actions:

○ A(high) = {search, wait}
○ A(low) = {search, wait, recharge}

● Reward:

○ Zero most of the time, except when securing a can
○ Cans are secured by searching and waiting, but rsearch > rwait

● State-transition probabilities:

○ [Next Slide]

17

MDP Formalization : Recycling Robot (Detailed Ex.)

● State-transition probabilities (contd…):

18

MDP Formalization : Recycling Robot (Detailed Ex.)

● State-transition probabilities (contd…):

19

Note on Goals & Rewards

● Reward Hypothesis:

All of what we mean by goals and purposes can be well thought of as
the maximization of the expected value of the cumulative sum of a
received scalar signal (called reward).

● The rewards we set up truly indicate what we want accomplished,

○ not the place to impart prior knowledge on how we want it to do

○ If the agent is rewarded for taking opponents pieces, the agent might fall

● Ex: Chess Playing Agent

for the opponent's trap.

● Ex: Vacuum Cleaner Agent

○ If the agent is rewarded for each unit of dirt it sucks, it can repeatedly

deposit and suck the dirt for larger reward

20

Returns & Episodes

● Goal is to maximize the expected return
● Return (Gt) is defined as some specific function of the reward

sequence

● Episodic tasks vs. Continuing tasks
● When there is a notion of final time step, say T, return can be

○ Applicable when agent-environment interaction breaks into

episodes

○ Ex: Playing Game, Trips through maze etc. [ called episodic tasks]

21

Returns & Episodes

● Generally T = ∞

○ What if the agent receive a reward

of +1 for each timestep?

○ Discounted Return:

Note:

○ Discount rate determines the present

value of future rewards

22

Returns & Episodes

● What if 𝛾is 0?
● What if 𝛾is 1?
● Computing discounted rewards incrementally

• Sum of an infinite number of terms, it is still finite if the reward is nonzero

and constant and if 𝛾< 1.
• Ex: reward is +1 constant

23

Returns & Episodes

➔ Objective:  To apply forces to a cart
moving along a track so as to keep a
pole hinged to the cart from falling over

➔ Discuss:

➔ Consider the task as episodic, that is
try/maintain balance until failure.
What could be the reward function?

➔ Repeat prev. assuming task is

continuous.

24

Ex-1

Recollect the reward function used for Gridworld as below:

○ -1 if an action takes agent off the grid
○ Exceptional reward from A and B for all actions taking agent to A’ and B’ resp.
○ 0, everywhere else

Let us add a constant c ( say 10) to the rewards of all the actions. Will it change
anything?

25

Policy

● A mapping from states to

probabilities of selecting each
possible action.
○ 𝛑 (a|s) is the probability that At

= a if St = s

● The purpose of learning is to

improve the agent's policy with its
experience

26

Defining Value Functions

State-value function for policy 𝝿

Action-value function for policy 𝝿

27

Defining Value Functions

State Value function in terms of Action-value function for policy 𝝿

Action Value function in terms of State value function for policy 𝝿

28

Bellman’s Expectation equations

Core Idea
Decomposes the value of a state into:

Immediate reward + discounted value of next state.

Turns a hard optimisation into a recursive local computation.
Foundation of all DP and TD methods.
V π(s) = [ immediate reward ] + γ × [ value of where we end up ]

Why Bellman’s
Bellman equation is a consistency condition: V must satisfy it for every state.
Solving this system (|S| equations, |S| unknowns) gives Vᵄ exactly.
To compute V π(Cool), you need:
→ All paths from Cool under π
→ Their probabilities × total returns
→ Sum infinitely many trajectories
For even 3 states × 2 actions × infinite horizon = computationally intractable!

29

Bellman’s derivation

Step 1: Start with the definition of V π(s)

V π(s) = Eπ [ Gₜ | Sₜ = s ]

Step 2: Expand return Gₜ = Rₜ₊₁ + γGₜ₊₁

V π(s) = Eπ [ Rₜ₊₁ + γGₜ₊₁ | Sₜ = s ]

Step 3: Split expectation (linearity)

V π(s) = Eπ [Rₜ₊₁ | Sₜ = s]  +  γ · Eπ [Gₜ₊₁ | Sₜ = s]

Step 4: Marginalise over actions and next states

V π(s) = Σₐ π(a|s) Σₛ' P(s'|s,a) [ R(s,a,s') + γ · V π(s') ]

30

Bellman Equation for V𝝅

Value of the start state must equal

(1) the (discounted) value of the expected next state,
plus

(1) the reward expected along the way

Backup Diagram

31

32

Understanding V𝝅(s) with Gridworld

Reward:

○ -1 if an action takes agent off the grid
○ Exceptional reward from A and B for all actions taking agent to A’ and B’ resp.
○ 0, everywhere else

Exceptional reward dynamics

State-value function for the equiprobable
random policy with 𝛾 = 0.9

33

Understanding V𝝅(s) with Gridworld

Verify V𝝅(s) using Bellman equation for this state
with 𝛾 = 0.9, and equiprobable random policy

34

Understanding V𝝅(s) with Gridworld

35

Optimal Policies and Optimal Value Functions

● 𝝿 ≥ 𝝿’ if and only if v𝝿(s)  ≥ v𝝿(s) for all s ∊ S
● There is always at least one policy that is better than or

equal to all other policies → optimal policy (denoted as 𝝿*)
○ There could be more than one optimal policy !!!

Optimal state-value function

Optimal action-value function

36

Optimal Policies and Optimal Value Functions

Bellman optimality equation - expresses that the value of a state under
an optimal policy must equal the expected return for the best action
from that state

Bellman optimality equation for V*

37

Optimal Policies and Optimal Value Functions

Bellman optimality equation - expresses that the value of a state under
an optimal policy must equal the expected return for the best action
from that state

Bellman optimality equation for q*

38

Optimal Policies and Optimal Value Functions

Bellman optimality equation - expresses that the value of a state under
an optimal policy must equal the expected return for the best action
from that state

Backup diagrams for v* and q*

39

Optimal solutions to the gridworld example

Backup diagrams for v* and q*

40

MDP - Objective

•

41

Notation

•

42

Dynamic Programming

• A collection of algorithms that use a FULL model of the MDP to

compute optimal policies.

• Key idea: use value functions to structure the search for optimal

policies.

• Requires: complete, accurate model p(s’,r|s,a). NOT applicable to

model-free RL directly.

Race car example

•

44

Race car example

•

50

Value iteration

51

Value Iteration

0             0             0

2             1             0

3.35

2.35        0

Check this computation on paper.

52

Example: Grid World

▪ A maze-like problem

The agent lives in a grid
▪
▪ Walls block the agent’s path

▪ Noisy movement: actions do not always go as planned

▪
▪
▪

80% of the time, the action North takes the agent North
10% of the time, North takes the agent West; 10% East
If there is a wall in the direction the agent would have
been taken, the agent stays put

▪

The agent receives rewards each time step
▪
▪

Small negative reward each step (battery drain)
Big rewards come at the end (good or bad)

▪ Goal: maximize sum of (discounted) rewards

53

Value Iteration on Gridworld (k = 0 to 100)

Noise = 0.2
Discount = 0.9
Living reward = 0

54

Problems with Value Iteration

•

55

Solutions (briefly, more later…)

•

56

• Asynchronous value iteration
• In value iteration, we update every state in each iteration
• Actually, any sequences of Bellman updates will converge if every state is visited

infinitely often regardless of the visitation order

• Idea: prioritize states whose value we expect to change significantly

57

Asynchronous Value Iteration

• Which states should be prioritized for an update?

A single
update per
iteration

58

Double the work?

•

59

Issue 2: A policy cannot be easily extracted

•

60

Q-learning

•

61

Q-learning as value iteration

•

62

Issue 3: The policy often converges long
before the values
•

63

Policy Iteration

•

64

Policy Evaluation

•

65

Policy value as a Linear program

66

Policy iteration

0.7

0.8

0.9

0.7

0.6

0.4

0.6

0.5

67

Comparison

• Both value iteration and policy iteration compute the same thing (optimal

state values)

• In value iteration:

• Every iteration updates both the values and (implicitly) the policy
• We don’t track the policy, but taking the max over actions implicitly define it

• In policy iteration:

• We do several passes that update utilities with fixed policies (each pass is fast

because we consider only one action, not all of them)

• After the policy is evaluated, a new policy is chosen (slow like a value iteration

pass)

• The new policy will be better (or we’re done)

68

Issue 4: requires knowing the model and the
reward function
•

Offline optimization

Online Learning

69

Issue 5: requires discrete (finite) set of
actions
• We will explore policy gradient approaches that are suitable for

continuous actions, e.g., throttle and steering for a vehicle
• Can such approaches be relevant for discrete action spaces?

• Yes! We can always define a continues action space as a distribution over the

discreate actions (e.g., using the softmax function)

• Can we combine value-based approaches and policy gradient

approaches and get the best of both?

• Yes! Actor-critic methods

70

Issue 6: infeasible in large (or continues)
state spaces
• Most real-life problems contain very large state spaces (practically

infinite)

• It is infeasible to learn and store a value for every state
• Moreover, doing so is not useful as the chance of encountering a

state more than once is very small

• We will learn to generalize our learning to apply to unseen states
• We will use value function approximators that can generalize the

acquired knowledge and provide a value to any state (even if it was
not previously seen)

71

Generalized Policy Iteration (GPI)

GPI: Generalised Policy Iteration — the general schema of interleaving policy evaluation and improvement. Almost all RL
methods can be described as GPI.

Evaluation Process

Improvement Process

Spectrum of GPI

Makes V consistent with the CURRENT
policy π.
Applies Bellman expectation backups.
Drives V toward Vπ.
Does NOT need to converge fully
before improvement begins.

Makes π greedy w.r.t. current V.
Changes the policy, which invalidates V
again.
The two processes COMPETE — but
together converge.
Fixed point = optimal (π*, V*) for both
processes.

Policy Iter: full eval → improve.
Value Iter: 1 sweep → improve.
Async DP: update any states freely.
TD / Q-learning: model-free GPI.
Actor-Critic: parallel eval + improve.
Deep RL: approximate GPI with NNs.

PI vs VI

Aspect

Policy Iteration (PI)

Value Iteration (VI)

Evaluation depth

Bellman update

Policy update

Policy visible?

Convergence speed

Full convergence (Δ <
θ)
Σₐ π(a|s) · …
(expectation)
After full evaluation

Single Bellman sweep

max_a (…) at each
step
Implicitly each sweep

Yes — explicit at each
step
Fewer outer iterations More outer iterations

Only at end

Compute/iteration

More (full eval phase) Less (one sweep)

Best for

Race Car

Small state spaces

Large state spaces

Optimal in 3 PI steps Optimal in 23 VI steps

Summary & Bridge to Model-Free RL

Topic

Key Idea

1 MDP = { S, A, P, R, γ }

Formal framework for sequential decisions under uncertainty

2

3

4

5

Value Functions

Vπ(s) and Qπ(s,a) quantify long-term goodness

Bellman Equation

Recursive decomposition that makes computation tractable

Dynamic Programming

Solve Bellman equations when the model is KNOWN

GPI Framework

Eval

Improve alternation — unifies ALL DP methods

Next: What if we DON’T know the model?

Monte Carlo

TD Learning

Q-Learning

Learn V from complete episode returns

Learn V from one-step bootstrapped estimates

Learn Q* directly off-policy (model-free!)

GPI still applies in model-free RL — but Evaluation uses sampled experience instead of known dynamics!

Notation

•

75

Required Readings

1. Chapter-3,4 of Introduction to Reinforcement Learning,2nd Ed.,  Sutton

& Barto

76

Thank you

77

