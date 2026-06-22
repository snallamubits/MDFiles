Birla Institute of Technology & Science, Pilani
Work Integrated Learning Programmes Division
Second Semester 2022-2023
Mid-Semester Test (EC-2 Regular)

Course No. : AIMLCZG512
Nature of Exam : Closed Book Weightage : 30% No. of Pages = 2 ;
Duration : 2 Hours;

Course Title: Deep Reinforcement Learning
No. Of Questions = 5;
Date of Exam: 28-07-2024 (EN)

Note to Students:

1. Answer all the questions.
2. Write your name and sign at the end of all the pages.
3. Assumptions made if any, should be stated clearly at the beginning of your answer.

Q1) [Write the answer in an A4 Sheet, Scan & Upload]

(a) In what ways a Unsupervised Learning and Reinforment Learning are different? [2.0 M]
(b) How are model based and model free reinforcement algorithms differ? What are scenarios
when these approaches are appropriate? [scenarios in not more than three statements] [2.0
M]

(c) Write any one use-case (application) from your workplace which can be modeled as a RL
problem suitable to be solved by dynamic programming approach. Your answer should
have all
identify the use case sitable to be solved by dynamic
programming approach. [vague description of application will be penalized]. [2.0 M]

the elements that

[2.0 + 2.0 +2.0 = 6.0 Marks]

Q2) [Write the answer in A4 Sheet, Scan & Upload]

(a) In the image below is a representation of the game that you are about to play. There are 5
states: A, B, C, D, and the goal state. The goal state, when reached, gives 100 points as
reward. Treat this as the value of being in the Goal State. The immediate rewards while
transitioning is mentioned in the edges. Assume the values of states are initialized to 0.
Assume that the each outgoing actions from the states are equiprobable. Assume we are
using asynchronous value iteration with a decay (γ) of 0.9. Show the value of each state
after one iteration, if the states are considered in the order D, A, C, B. What will be the
policy at state B after this iteration.

Q3) [Write the answer in A4 Sheet, Scan & Upload]

(a) In the gridworld example, rewards are positive for goals, negative for running into the edge
of the world, and zero the rest of the time. Are the signs of these rewards important, or only
the intervals between them? Explain. [2.0 M].

(b) Consider a k-armed bandit problem with k = 5 actions, denoted 1, 2, 3, 4 and 5. Consider
applying to this problem a bandit algorithm using 𝞮-greedy action selection, sample-average

[ 6 Marks]

Page (1/2)

action-value estimates, and initial estimates of Q1(a) = 4, for all a. Suppose the initial
sequence of actions and rewards is A1 = 1, R1 = 2, A2 = 2, R2 = 2, A3 = 5, R3 = 1, A4 = 2, R4
= 1, A5 = 4, R5 = 1, A5 = 3, R5 = 5. On some of these time steps the 𝞮-case may have
occurred, causing an action to be selected at random.

(i)
(ii)

On which time steps did this definitely occur? Why? [2 M].
On which time steps could this possibly have occurred? Why? [2 M].

[2.0 + 4 = 6 Marks]

Q4) [Write the answer in A4 Sheet, Scan & Upload]

(a) Devise one example task of your own that fit into the MDP framework, identifying for each
its states, actions, and rewards. Make the examples as different from each other as
possible. [1 M] .

(b) Write a recursive expression that can be used to evaluate q𝝅(s,a) ? What is the significance

of the recursive nature of q𝝅(s,a)? [2 M].
(c) Consider the continuing MDP shown below.

The only decision to be made is that in the top state, where two actions are available, left
and right. The numbers show the rewards that are received deterministically after each
action. There are exactly two deterministic policies, 𝝅left and 𝝅right .

(i) What policy is optimal if 𝛾= 0.7? [1.5 M]. Explain
(ii) What policy is optimal if 𝛾= 0.5 ?[1.5 M]. Explain

[1.0 + 2.0+ 3.0 = 6 Marks]

Q5) [Write the answer in A4 Sheet, Scan & Upload]

Consider the following episodes as experienced by an agent following a policy 𝝅 with states
{A,B,C,T} in which T is terminal state and actions {x,y,z}. The episodes are written using the
representation { state - action - reward- nextState … } order, and the number in red within
the bracket is the immediate reward.

E1: C - x - ( 0 ) - A - x - (+10) - C - x - (+2) - B - y - (+12) - C - x - (+ 20 ) - T
E2: A - x - (+10) - C - x - (+2) - B - y - (+12) - B - y - (+12) - C - x - (+ 20 ) - T
E3: C - x - (+2) - B - y - (+12) - C - x - (+ 20 ) - T

Assuming the initial Q𝝿(s,a) are all 0’s, compute the revised Q𝝿(s,a) using on-policy
ﬁrst-visit MC control algorithm for ε-soft policies for one iteration only [4 M]. Assume the 𝛄 =
0.9. Write down the revised policy. [2 M].

[ 6 Marks]

Page (2/2)

