Deep Reinforcement Learning
2022-23 Second Semester, M.Tech (AIML)

2025-56 First

Session #2-3:
Multi-armed Bandits

Instructors - DRL Course

1

Agenda for the class

• Recap
• k-armed Bandit Problem & its significance
• Action-Value Methods

Sample Average Method & Incremental Implementation

• Non-stationary Problem
•

Initial Values & Action Selection

Acknowledgements: Some of the slides were adopted with permission from the course CSCE-689 (Texas A&M University) by Prof.  Guni Sharon

2

K-armed Bandit Problem

Problem
•
• After each choice of actions you receive a numerical reward

You are faced repeatedly with a choice among k different options, or actions

Reward is chosen from a stationary probability distribution that depends on the selected

action

• Objective : to maximize the expected total reward over some time period

3

K-armed Bandit Problem

Problem
•
• After each choice of actions you receive a numerical reward

You are faced repeatedly with a choice among k different options, or actions

Reward is chosen from a stationary probability distribution that depends on the selected

action

• Objective : to maximize the expected total reward over some time period

4

K-armed Bandit Problem

Problem
•
• After each choice of actions you receive a numerical reward

You are faced repeatedly with a choice among k different options, or actions

Reward is chosen from a stationary probability distribution that depends on the selected

action

• Objective : to maximize the expected total reward over some time period

Strategy:
● Identify the best lever(s)
● Keep pulling the identified ones
Questions:
● How do we define the best ones?
● What are the best levers?

5

K-armed Bandit Problem

Problem
•
• After each choice of actions you receive a numerical reward

You are faced repeatedly with a choice among k different options, or actions

Reward is chosen from a stationary probability distribution that depends on the selected

action

• Objective : to maximize the expected total reward over some time period

Strategy:
● Identify the best lever(s)
● Keep pulling the identified ones
Questions:
● How do we define the best ones?
● What are the best levers?

6

K-armed Bandit Problem

Problem
•
• After each choice of actions you receive a numerical reward

You are faced repeatedly with a choice among k different options, or actions

Reward is chosen from a stationary probability distribution that depends on the selected

action

• Objective : to maximize the expected total reward over some time period

● Expected Mean Reward for  each

action selected
→ call it Value of the action

7

K-armed Bandit Problem

• At
• Qt (a)
• q*(a)

- action selected on time step t
- estimated value of action a at time step t
- value of an arbitrary action a

Note: If you knew the value of each action, then it would be trivial to solve the k -armed bandit
problem: you would always select the action with highest value :-)

8

What are problems whose solutions are modelled as MAB?

9

10

                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        11

K-armed Bandit Problem

12

K-armed Bandit Problem

Keep pulling the levers;  update the estimate of action values;

13

K-armed Bandit Problem

14

K-armed Bandit Problem

1. How to maintain the estimate of expected rewards for each action?

Average the rewards actually received !!!

1. How to use the estimate in selecting the right action?

Greedy Action Selection

15

K-armed Bandit Problem

2. How to use the estimate in selecting the right action?

Greedy Action Selection

Actions which are inferior by the value estimate upto time t, could be indeed better than
the greedy action at t !!!

3. Exploration vs. Exploitation?

ε-Greedy Action Selection / near-greedy action selection
Behave greedily most of the time; Once in a while, with small probability 𝛆 select randomly
from among all the actions with equal probability, independently of the action-value estimates.

16

K-armed Bandit Problem

17

K-armed Bandit Problem

Greedy Action

18

K-armed Bandit Problem

Action to Explore

19

K-armed Bandit Problem

ε-Greedy Action Selection / near-greedy action selection

epsilon = 0.05 // small value to control exploration
def get_action():

if random.random() > epsilon:
return argmaxa(Q(a))

else:

return random.choice(A)

● In the limit as the number of steps increases, every action will be sampled by ε-greedy action

selection an infinite number of times. This ensures that all the Qt (a) converge to q* (a).

● Easy to implement / optimize for epsilon / yields good results

20

Ex-1: In ε-greedy action selection, for the case of two actions and ε
= 0.5, what is the probability that the greedy action is selected?

21

Ex-1: In ε-greedy action selection, for the case of two actions and ε
= 0.5, what is the probability that the greedy action is selected?

p (greedy action)

= p (greedy action AND greedy selection ) + p (greedy action AND random selection )
= p (greedy action | greedy selection ) p ( greedy selection )

+ p (greedy action | random selection ) p (random selection )

=  p (greedy action | greedy selection ) (1-𝛆) + p (greedy action | random selection ) (𝛆)
= p (greedy action | greedy selection ) (0.5) + p (greedy action | random selection ) (0.5)
= (1) (0.5) + (0.5) (0.5)
= 0.5 + 0.25
= 0.75

22

10-armed Testbed

Example:
• A set of 2000 randomly generated k -armed

bandit problems with k = 10

• Action values were selected according to a
normal (Gaussian) distribution with mean 0
and variance 1.

• While selecting action At at time step t, the
actual reward, Rt , was selected from a
normal distribution with mean q*(At ) and
variance 1

• One Run : Apply a method for 1000 time
steps to one of the bandit problems
• Perform 2000 runs, each run with a
different bandit problem, to get an
algorithms average behavior

An example bandit problem from the 10-armed testbed

24

Average performance of 𝛆-greedy action-value methods on
the 10-armed testbed

25

Average performance of 𝛆-greedy action-value methods on
the 10-armed testbed

26

Ex-2:

Consider a k -armed bandit problem with k = 4 actions, denoted 1, 2, 3, and 4.

Consider applying to this problem a bandit algorithm using 𝛆-greedy action selection, sample-
average action-value estimates, and initial estimates of Q1 (a) = 0, for all a.

Suppose the initial sequence of actions and rewards is A1 = 1, R1 = 1, A2 = 2, R2 = 1, A3 = 2, R3 = 2,
A4 = 2, R4 = 2, A5 = 3, R5 = 0.

On some of these time steps the 𝛆 case may have occurred, causing an action to be selected at
random.

On which time steps did this definitely occur? On which time steps could this possibly have
occurred?

27

Incremental Implementation

• Efficient approach to

compute the estimate of
action-value;

• Given Qn and the nth
reward, Rn , the new
average of all n rewards can
be computed as follows

28

Incremental Implementation

Note:
● StepSize decreases with each update
● We use 𝛂 or 𝛂t(a) to denote step size (constant /

varies with each step)

Discussion:

Const vs. Variable step size?

29

Bandit Algorithm with Incremental Update/ 𝛆-greedy
selection

30

Discussion on Exploration vs. Exploitation

1) What if the reward variance is
a. larger, say 10 instead of 1?
b. zero ? [ deterministic ]

2)  What if the bandit task is non-stationary? [ that is, the true values of the
actions changed over time]

31

Non-stationary Problem

• Most RL problems are non-stationary !
• Give more weight to recent rewards than to long-past rewards !!!

32

Non-stationary Problem

• Most RL problems are non-stationary !
• Give more weight to recent rewards than to long-past rewards !!!

Exponential recency-weighted average

33

Optimistic Initial Values

• All the above discussed methods are biased by their initial estimates

•

•

•

•

For sample average method the bias disappears once all actions have been selected at
least once

For methods with constant α, the bias is permanent, though decreasing over time

Initial action values can also be used as a simple way of encouraging exploration.

In 10 armed testbed, set initial estimate to +5 rather than 0.

This can encourage action-value methods to explore.

Whichever actions are initially selected, the reward is less than the starting estimates;

the learner switches to other actions, being disappointed with the rewards it is receiving.

The result is that all actions are tried several times before the value estimates converge.

34

Optimistic Initial Values

Caution:
Optimistic Initial Values can
only be considered as a simple
trick that can be quite effective
on stationary problems, but it is
far
from being a generally
useful approach to encouraging
exploration.

how in

Question:
non-
Explain
stationary
the
optimistic initial values will fail
(to explore adequately).

the
scenario

The effect of optimistic initial action-value estimates on the 10-armed testbed.
Both methods used a constant step-size parameter, 𝛂 = 0.1

35

Upper-Confidence-Bound Action Selection

• 𝛆-greedy action selection forces the non-greedy actions to be tried,
Indiscriminately, with no preference for those that are nearly greedy or particularly uncertain

•

It would be better to select among the non-greedy actions
according to their potential for actually being optimal

Take into account both how close their estimates are to being maximal and the uncertainties

in those estimates.

36

Upper-Confidence-Bound Action Selection

● Each time a is selected the uncertainty is presumably reduced
● Each time an action other than a is selected, t increases but Nt(a) does not; because t appears in the numerator, the

uncertainty estimate increases.

● Actions with lower value estimates, or that have already been selected frequently, will be selected with decreasing

frequency over time

Action Value at time t for a

Confidence Level

Measure of Uncertainty

37

Upper-Confidence-Bound Action Selection

UCB often performs well, as shown here, but is more difficult than "-greedy to extend beyond bandits to the more
general reinforcement learning settings

Policy-based algorithms

•

39

Softmax function

•

40

Softmax function

•

41

Gradient ascend

•

?

42

Update Rule

On each step, after selecting action A t and receiving the reward Rt ,
Update the action preferences :

43

44

What did we learn?

• Problem: choose the action that results in highest expected reward
• Assumptions: 1. actions’ expected reward is unknown, 2. we are

confronted with the same problem over and over, 3. we are able to
observe an action’s outcome once chosen

• Approach: learn the actions’ expected reward through exploration
(value based) or learn a policy directly (policy based), exploit learnt
knowledge to choose best action

• Methods: 1. greedy + initializing estimates optimistically, 2. epsilon-
greedy, 3. Upper-Confidence-Bounds, 4. gradient ascend + soft-max

45

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

46

Required Readings

1. Chapter-2 of Introduction to Reinforcement Learning,2nd Ed.,  Sutton &

Barto

2. A Survey on Practical Applications of Multi-Armed and Contextual Bandits,

Djallel Bouneffouf , Irina Rish [https://arxiv.org/pdf/1904.10040.pdf]

47

Thank you !

48

