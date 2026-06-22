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

Acknowledgements: Some of the slides were adopted with permission from the course CSCE-689  (Texas A&M University) by Prof.  Guni Sharon

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

● Reward:

○ signal assignment

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

