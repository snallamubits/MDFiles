AIMLC ZG512 - Deep Reinforcement Learning  | Review and Practice Questions

Session #2-3:Multi-armed Bandits

(1)  Explain how the feedbacks considered in RL is evaluative not instructive, with an example.
(2)  Why do you say, Multi-armed bandit is RL problem in non-associative setting? Explain.
(3)  Provide one applications which can be modelled as Multi-armed bandit? Why do you think this

modelling is appropriate?

(4)  If the action value is constant for all the actions, do you need to explore? Why or why not.
(5)  Tabulate approaches we have learned to balance exploration and exploitation with your remark

on their application.

(6)  What will be your choice of ε, ( as used in ε-greedy), for each of the following case:

(a)  Deterministic rewards
(b)  Reward distribution with lesser variance
(c)  Reward distributions with larger variance

Explain the reasons for your choice.

(7)  In ε-greedy action selection with four actions (a,b,c,d; assume a is greedy action)  and ε=0.4, what

is the probability that greedy action and non-greedy actions are selected.

(8)  Consider the general form of the update rule that updates the estimate of action values:

NewEstimate = OldEstimate + StepSize [ Target - OldEstimate ]

Comment on how the following choice adresses (i)  non-stationarity and (ii) higher reward
variance,

(a)  Step size is 1/n for each update, where n is the current timestep
(b)  Step size is constant [0 ≤ ꭤ ≤ 1 ] for each update

(9)  Effect of exploration due to setting optimistic initial values is temporary. Why? When would you

use this hack?

(10) Try the following exercises from RL, Sutton & Barto, Second Ed.

(a)  Exercise 2.2, 2.3

(11)  Try to understand the problem statement in exercise 2.7 ( of RL, Sutton & Barto, Second Ed. ),

while the analysis as required is not required.

(12) Explain how policy-based methods and value based methods are different?
(13) Write any two approaches (need not be the only ones discussed in the classes)  you can use to

maintain the estimate of action values?

(14) How does UCB differ from ε-greedy? Explain.
(15) Given a problem, what factors will you consider in choosing the right ε for ε-greedy action

selection?

Happy Learning!

Readings Required:  Sections 2.1-2.7 of Sutton & Barto, Ed-2

Note: The review questions are posted to help students to perform a self-assessment on the key take-aways from
the sessions. These are not to be treated as sample questions / pool of questions for written exams. Certain
questions will require some additional preparation beyond the class coverage.

