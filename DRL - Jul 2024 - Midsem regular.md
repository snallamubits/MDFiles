Birla Institute of Technology & Science, Pilani
Work Integrated Learning Programmes Division
Second Semester 2022-2023
Mid-Semester Test (EC-2 Regular)

Course No. : AIMLCZG512
Nature of Exam : Closed Book Weightage : 30% No. of Pages = 2 ;
Duration : 2 Hours;

Course Title:Deep Reinforcement Learning
No. Of Questions = 6;
Date of Exam: 21-07-2024 (EN)

Note to Students:

1. Answer all the questions.
2. Write your name and sign at the end of all the pages.
3. Assumptions made if any, should be stated clearly at the beginning of your answer.

Q1) [Write the answer in an A4 Sheet, Scan & Upload]
(a) How are rewards and returns connected? [1 M]
(b) Consider the RL agent

tic-tac-toe, by playing against different
randomly chosen opponents. Consider the temporal difference rule being used in this
context. Can 𝛂 be used to encourage exploration? [1 M] Why or why not? [2 M]

learning the game of

(c) Write one model-based and model-free algorithm for reinforcement learning covered in the

course so far.[1 M]

[1.0 + 3.0+ 1.0 = 5 Marks]

Q2) [Write the answer in A4 Sheet, Scan & Upload]

(a) Consider again the RL agent learning the game of tic-tac-toe by playing against different
randomly chosen opponents. It is decided that the learning algorithm does not use explicit
exploratory moves? Under this scenario, would you consider RL agent to learn the same as
as supervised learning? [One word, yes/no whose marking depends only on the correct
explanation] [0.5 M] Explain in two well articulated statements [Caution: your third and
further statements for explanation will not be evaluated ]. [2.0 M].

(b) State one situation in which an greedy action selection works better than 𝝴-greedy action

selection. [1.0 M].

(c) Write any one use-case (application) from your workplace which can be modeled as a
multi-armed bandit for its solution. Your answer should have all the elements that identify
the use case and can be modeled as a multi-armed bandit problem. [vague description of
application will be penalized]. [1.5 M]

[2.5 + 1.0 + 1.5 = 5 Marks]

Q3) [Write the answer in A4 Sheet, Scan & Upload]

(a) How do you use the following learning rule for a non-stationary MAB problem? Explain in
two well articulated statements [Caution: your third and further statements for explanation
will not be evaluated ]. [2.0 M].

(b) Consider encouraging exploration by Optimistic Initial Values and UCB. Provide one

scenario when the approach is useful and one when they are not, in a neat table as below:

Page (1/2)

When it works?

When it doesnt work?

Optimistic Initial Values

UCB

[0.5 M]

[0.5 M]

[0.5 M]

[0.5 M]

(c) What information do you need about an RL problem to find out optimal value function? [1.0

M].

[2.0 + 2.0 + 1.0 = 5 Marks]

Q4) [Write the answer in A4 Sheet, Scan & Upload]

(a) Recollect the recycling robot example whose transition diagram is as below:

Write down the expression for q𝝅(high, search), and q*(high, search). [2.0 M]. Assume the
notations introduced in the class for interpreting the transition diagram.

(b) Imagine that you are designing a robot to run a maze. You decide to give it a reward of +1
for escaping from the maze and a reward of zero at all other times. The task seems to
break down naturally into episodes—the successive runs through the maze—so you decide
to treat it as an episodic task, where the goal is to maximize expected total reward. After
running the learning agent for a while, you ﬁnd that it is showing no improvement in
escaping from the maze. What is going wrong? How to fix the situation?

[2.0 + 3.0 = 5 Marks]

Q5) [Write the answer in A4 Sheet, Scan & Upload]

Consider the following episodes as experienced by an agent following a policy 𝝅 with states
{A,B,C,T} in which T is terminal state and actions {x,y,z}. The episodes are written using the
representation { state - action - reward- nextState … } order, and the number in red within
the bracket is the immediate reward.

E1: A - x - (+10) - C - y - (+12) - C - x - ( 0 ) - T
E2: A - x - (+10) - C - x - (+2) - B - y - (+12) - C - x - (+ 20 ) - T
E3: C - x - (+2) - B - y - (+12) - C - x - (+ 20 ) - T

Assuming the initial Q𝝿(s,a) are all 0’s, compute the revised Q𝝿(s,a) using on-policy
ﬁrst-visit MC control algorithm for ε-soft policies for one iteration only [3.5 M]. Assume the 𝛄
= 0.8. Write down the revised policy. [1.5 M].

[ 5 Marks]

Page (2/2)

