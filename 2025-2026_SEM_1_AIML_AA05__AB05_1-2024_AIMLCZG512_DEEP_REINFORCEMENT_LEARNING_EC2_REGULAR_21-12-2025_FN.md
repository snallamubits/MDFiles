Birla Institute of Technology & Science, Pilani
Work Integrated Learning Programmes Division
Second Semester 2022-2023
Mid-Semester Test (EC-2 Makeup)

    Course Title : Deep Reinforcement Learning
Course No. : AIMLCZG512
Nature of Exam : Open Book  Weightage : 30%      No. of Pages = 3 ;             No. Of Questions = 4;
     Date of Exam : 21 December, 2025 - 09:00 AM
Duration : 2 Hours;

Note to Students:

1.  Answer all the questions. All parts of a question should be answered consecutively. Each

answer should start on a fresh page.

2.  Write answers neatly in A4 paper, scan and upload.
3.  Write your name and sign at the end of all the pages.
4.  Assumptions made if any, should be stated clearly at the beginning of your answer.

Question -1
 [ 1.5 + 2+ 4 = 7.5 Marks]
A mobile health-monitoring wristband must choose among three modes each hour, based on
the current activity {resting, moderate, high}:

-  Mode A: low power, moderate accuracy
-  Mode B: medium power, high accuracy
-  Mode C: high power, very high accuracy

 The immediate benefit (reward) from each mode changes based on the user’s physical activity.
a)  State why RL (not supervised learning) fits this setting, and give a one-line distinction

between immediate reward and long-term value. [1.5 Mark]

b)  Using the same wristband scenario:

Case 1: Initially, assume the user’s activity pattern is independent of the modes chosen,
i.e., choosing Mode A or B today does not affect future rewards.
Case 2: Later, a firmware update introduces an adaptation rule: If the wristband samples
in Mode C for too long, the battery temperature rises, reducing future rewards for
power-hungry modes.
 i) Classify case 1 as a Multi-Armed Bandit (MAB) or a Finite MDP, with one justification.
[1 mark]
 ii) Classify case 2 again and justify — does the added dependency change the problem
class? [1 mark]

c)  For the MDP given below, calculate the Values of states = {resting, moderate activity,

high activity} in the same order, using synchronous Value Iteration. Actions = {mode A,
mode B} are allowed from each state. Use

Solve for 1 iteration. [4 marks]

γ  =  0. 1.

Question -2

            [2.5+2+1.5+1.5 = 7.5 marks]

In  an  ICU  environment, clinicians must periodically adjust a patient's ventilator settings
to  maintain  optimal  blood  oxygen  saturation  (SpO₂).  The  system  can  be  modeled  as  a
finite MDP where the patient’s oxygenation levels and respiratory indicators are defined
into  categories  such  as  lowO2,  highO2,  or  OptimalO2.  The  clinician-assist  AI  can
increase  pressure,  decrease  pressure,  or  maintain  settings.  With  0.4  probability,
increasing/decreasing
the  pressure  does  not  change  a  patient's  health.  Whereas
maintaining the same settings always seem to retain the patient’s condition as is. The goal
is  to  stabilize  the  patient’s  SpO₂  within  safe  clinical  thresholds  while  avoiding
over-ventilation.  Once  for  four  consecutive  recordings,  the  SpO₂  is  observed  to  be
Optimal, then the patient stabilizes.

(a)     Formulate  the  MDP.  State  the components clearly. Diagrammatically represent the
model  dynamics. Note: Assume equal likelihood for scenarios that are not explicitly
mentioned in the above use case. [2.5 Marks ]

(b)     Given below reward designs, analyse the impact on the patient’s safety in the given
setup.  Which  one  do  you  prefer  and  why?  Justify  your  answer  in  exactly  two
statement  w.r.t  i)What  behavior  each  encourage,  ii)  In  which scenario one design is
preferable over the other

Design A: For moderating from lowO2 to OptimalO2, reward = +10 is set

Design B: For moderating from OptimalO2 to HighO2, reward = -10 is set

[2 Marks ]

(c)     Is the given use case, episodic or continuous tasks? Justify your answer in no more

than 30 words. [1.5 Marks ]

(d)     If  γ = 0.01 is used, what is the impact on the patient’s stability? Justify your answer in no

more than 30 words. [1.5 Marks ]

Question -3

                    [3+1.5+1+2= 7.5 Marks]
In  an  online  pharma  platform,  a  multi-armed  bandit
that  recommends
adherence-support  interventions  for  (patients) frequent online customers based on their current state
(e.g.,  health conditions, stock of medication, risk of the ordered medicines etc., ) to improve quality
adherence and customer retention. Few observed interventions recommended for patients (customers)
in  a  digital  health  platform  include  {SMS  reminder  to  refill  medications(S),  Teleconsultation
Scheduling  with  a  doctor  (T),  Reminder about Lab Tests (R), Counselling Call by Pharmacist (C)}.
Analyze the below observations in the given order and answer the following questions sequentially.

implemented

is

(1, S, 7), (2, T, 5), (3, R, 6), (4, C, 4), (5, S, 8), (6, T, 6), (7, R, 7), (8, C, 5).

a)  Estimate the best intervention based on the listed observations. Use exponential recency weighted
average based value update only with α=0.5, to revise the Q(actions) for all the actions. Assume
for initialization. [3 Marks ]

b)  Refer  to  the  results  of  part  a)  and  illustrate  the  significance  of  α.  What  happens  if  α=1  is  set
instead? Justify answers in no more than 30 words using the given above use case for illustration.
[1.5 Marks ]

c)  What  is  the  significance  of  confidence  level  in the UCB based selection? Justify answers in no

more than 30 words using the given above use case for illustrations. [1.0 Marks ]

d)  Analyze only until the 5th time step. On some of these time steps the ε-case may have occurred,

causing an action to have been selected at random.

i)  On which time steps did this definitely occur? Why? [1.0Marks ]
ii)  On which time steps could this possibly have occurred? Why? [1.0 Marks ]

Question -4

               [2 + 2 + 3.5 = 7.5 Marks]

a)  In a model-free MDP, explain why estimating only the state value 𝑣𝜋(𝑠) is insufficient for

selecting actions during control, even if 𝑣𝜋  is estimated perfectly. [Ensure your answer is
given in 2-3 well-articulated statements; vague answers will be penalised] [2 Marks ]

b)  In a deterministic policy that always selects the same action in a state, explain in 2-3
sentences why first-visit Monte Carlo estimation may fail to reach an optimal policy?
Suggest one precise way to address this. [2 Marks]

c)  A chatbot agent operates in two states: s0

for the user engaged and s1 for the user

disengaged. It may take three actions: a1 ask an open-ended question, a2 : recommend a
resource and a3: send a fun fact.
The present Q values and the ε-soft policy are as below:

q𝝿( , )

s0

s1

a1

1

0

a2

0.5

0.5

a3

0

1

𝝿(. | .)

s0

s1

a1

0.5

0.2

a2

0.3

0.5

a3

0.2

0.3

Now consider an episode:
(s0 , a1 , r=2, s0 ) →  (s0 , a3 , r=0, s1 ) → (s1 , a2 , r=3, s1 ) → (s1 , a2 , r=−1, terminal).
Assuming γ=0.8 and computing returns using the discounted-sum formulation as per first
visit Monte-Carlo method, produce the revised value-function table and the updated
policy table at the end of this episode, clearly highlighting all changes. Show the
computation corresponding to each change [3.5 Marks]

