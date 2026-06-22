Deep Reinforcement Learning
2022-23 Second Semester, M.Tech (AIML)

2025-56 First

Session #2-3:
Multi-armed Bandits

Session Faculty : Dr. Sangeetha Viswanathan

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

Acknowledgements: Some of the slides were adopted with permission from the course CSCE-689  (Texas A&M University) by Prof.  Guni Sharon

2

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

