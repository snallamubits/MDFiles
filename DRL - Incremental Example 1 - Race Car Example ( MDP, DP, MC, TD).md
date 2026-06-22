DEEP REINFORCEMENT
LEARNING
Incremental Example

DRL Team

BITS Pilani WILP

The instructors is gratefully acknowledging the
authors who made their course materials
freely available online.

This deck is designed by BITS WILP faculty team of
course Deep Reinforcement Learning

BITS PILANI WILP

Deep Reinforcement Learning

2

TABLE OF CONTENTS

1

2

3

4

MDP

DP
MC

TD

BITS PILANI WILP

Deep Reinforcement Learning

3

Problem Definition

Race Car Laps
A race car completes laps while managing engine temperature and speed decisions. Here each step is a
segment of a lap in the track where the car learns to trades off lap time against overheating risk. The
more the lap the car completes it performance betters. Car shuts down only when its engine get
overheated (optional terminal state).

Key Characteristics:

The agent must act under uncertainty —

percepts are local, and the agent must reason about hidden dangers

Assume there is no fuel constraints or No.of.Laps to complete!

At every time step the next potential engine temperature

depends on the current engine state not the past history

BITS PILANI WILP

Deep Reinforcement Learning

4

MARKOV DECISION PROCESS FORMALIZATION (Simplified)

1

2

3

4

(F)
}

BITS PILANI WILP

Deep Reinforcement Learning

5

5

6

7

TABLE OF CONTENTS

1

2

3

4

MDP

DP
MC

TD

BITS PILANI WILP

Deep Reinforcement Learning

6

Dynamic Programming

Scenario
In a modified Race car, there is a training track where agent is given a known map and
risk factors(dynamics) in advance. Agent knows exactly where it is and its action how
actions result in engine state change (KNOWN MODEL).

With full knowledge, the agent can compute optimal policies by trying through all states.

(1)

BITS PILANI WILP

Deep Reinforcement Learning

7

Dynamic Programming

1 Given

• P(s` | s, a) , R(s, a, s`) , P(s`, r | s, a)

2 To find

• Policy π

3 Solution

• Policy Iteration (PI): Prefer this in a relatively smaller state space where intermediate
termination provides explicit interpretable policy
• Value Iteration (VI): Prefer this in a relatively larger state space where fast convergence to
optimal policy is obtained at the end

4

Idea

• PI : One Step Look ahead 🡪 Evaluate 🡪 Improve
• VI : One Step Look ahead 🡪 Control

VI can be thought of truncated PI where evaluation is done fully before improvement.

BITS PILANI WILP

Deep Reinforcement Learning

8

Dynamic Programming Solution

Value Iteration Algorithm

Dynamic Programming – Value Iteration

Cool

Go Slow

Go Fast

ɵ = 0.01

0             0             0 ……..

Cool

cool          warm

(F)
}

+1                         +2                +2
1.0                        0.5               0.5

BITS PILANI WILP

Deep Reinforcement Learning

10

Synchronous Updates

Dynamic Programming – Value Iteration

Cool

Go Slow

Go Fast

ɵ = 0.01

0             0             0 ……..

Cool

cool          warm

+1                         +2                +2
1.0                        0.5               0.5

BITS PILANI WILP

Deep Reinforcement Learning

11

Synchronous Updates

Dynamic Programming – Value Iteration

Cool

Go Slow

Go Fast

ɵ = 0.01

0             0             0 ……..

2             1             0……….

Cool

cool          warm

• Below is done only for state : “Cool”. Repeat this for
all the states “Warm”, “Overheated” per iteration

+1                         +2                +2
1.0                        0.5               0.5

BITS PILANI WILP

Deep Reinforcement Learning

12

Synchronous Updates

Dynamic Programming – Value Iteration

Cool

Go Slow

Go Fast

ɵ = 0.01

Cool

cool          warm

0             0             0 ……..

2             1             0……….

3.35

2.35        0 ………

• Below is done only for state : “Cool”. Repeat this for
all the states “Warm”, “Overheated” per iteration

+1                         +2                +2
1.0                        0.5               0.5

BITS PILANI WILP

Deep Reinforcement Learning

13

Synchronous Updates

Dynamic Programming – Value Iteration

Cool

Go Slow

Go Fast

ɵ = 0.01

Cool

cool          warm

0             0             0 ……..

2             1             0……….

3.35

2.35        0 ………

…….

V49

~15.41

~14.41        0

+1                         +2                +2
1.0                        0.5               0.5

• ∆ = ~0.009 less than threshold ɵ = 0.01
• Algorithm converges slowly. Without ɵ converges ~208th
• Can faster convergence possible ?  Yes via
Asynchronous Value Updates. Idea is to use the
recent values V(S`) even within the same iteration !
One iteration is shown in next slide

Synchronous Updates

BITS PILANI WILP

Deep Reinforcement Learning

14

Dynamic Programming – Value Iteration

Cool

Go Slow

Go Fast

ɵ = 0.01

0             0             0 ……..

2

Cool

cool          warm

• Below is done only for state : “Cool”. In this same
iteration while updating the V(Warm) use recent value
of V(Cool) = 2 not 0 .

+1                         +2                +2
1.0                        0.5               0.5

BITS PILANI WILP

Deep Reinforcement Learning

15

Asynchronous Updates

Dynamic Programming – Value Iteration

Cool

Go Slow

Go Fast

ɵ = 0.01

0             0             0 ……..

2             1.9

0

Cool

cool          warm

• Below is done only for state : “Cool”. In this same
iteration while updating the V(Warm) use recent value
of V(Cool) = 2 .

+1                         +2                +2
1.0                        0.5               0.5

BITS PILANI WILP

Deep Reinforcement Learning

16

Asynchronous Updates

Dynamic Programming – Value Iteration

Cool

Go Slow

Go Fast

ɵ = 0.01

0             0             0 ……..

2             1.9
0……….

3.75

3.54        0 ………

…….

V40

~15.44

~14.44        0

Cool

cool          warm

+1                         +2                +2
1.0                        0.5               0.5

• ∆ = ~0.008 less than threshold ɵ = 0.01
• Algorithm converges fast. Without ɵ converges at ~157th
iteration!

BITS PILANI WILP

Deep Reinforcement Learning

17

Asynchronous Updates

Dynamic Programming – Value Iteration

Cool

Go Slow

Go Fast

ɵ = 0.01

0             0             0 ……..

2             1.9
0……….

3.75

3.54        0 ………

…….

V40

~15.44

~14.44        0

State

Cool

Warm

Best Action

Fast

Slow

Overheated

-

Cool

cool          warm

+1                         +2                +2
1.0                        0.5               0.5

• After convergence extract the
policy by choosing the action
that lead to the converged
maximum value here from
V40th iteration

Asynchronous Updates

BITS PILANI WILP

Deep Reinforcement Learning

DEEP LEARNING

18

Dynamic Programming Solution

In many cases, sometimes
policies
to
converge faster than value!

observed

is

So why wait for entire value
updates?

Policy Iteration Algorithm

Dynamic Programming

1 Given

• P(s` | s, a) , R(s, a, s`) , P(s`, r | s, a)

2 To find

• Policy π

3 Solution

• Policy Iteration (PI): Prefer this in a relatively smaller state space where intermediate
termination provides explicit interpretable policy
• Value Iteration (VI): Prefer this in a relatively larger state space where fast convergence to
optimal policy is obtained at the end

4

Idea

• PI : One Step Look ahead 🡪 Evaluate 🡪 Improve
• VI : One Step Look ahead 🡪 Control

🡨 Number of state sweeps (updates) can be
controlled if required (similar to mini-batch
/stochastic processing). Evaluate & Improve
steps are alternatively are done .

VI can be thought of truncated PI where evaluation is done fully before improvement.

BITS PILANI WILP

Deep Reinforcement Learning

20

Dynamic Programming – Policy Iteration

ɵ = 0.01

0             0             0 ……..

Cool

Go Slow
Go Fast

Cool

cool          warm

+1                         +2                +2
1.0                        0.5               0.5

π0

State

Cool

Warm

Best Action

Slow

Slow

Overheated

-

We will use asynchronous for
updates in this example. Note
that even though above backup
diagram depicts all possible
transition, this algorithm
computes value from only one of
the action as given by the
initialized policy at the start of
every iteration!!!

BITS PILANI WILP

Deep Reinforcement Learning

21

Dynamic Programming – Policy Iteration
Policy Evaluation Starts

ɵ = 0.01

0             0             0 ……..

1             1.45        0……….

Cool

Go Slow
Go Fast

Cool

cool          warm

• The value uses the initialized policy to select only one
action GREEDILY. Hence below cancelled equations
differentiated PI vs VI

This slide show what change from
Value iteration to Policy iteration
+1                         +2                +2
algorithm in the Evaluation step!.
1.0                        0.5               0.5
Since only action needs to be
assessed, MAX of all actions outcome
is no longer required in this PE cycle!

BITS PILANI WILP

Deep Reinforcement Learning

22

Dynamic Programming – Policy Iteration
Policy Evaluation Completes

ɵ = 0.01

Cool

Go Slow

Go Fast

Cool

cool          warm

0             0             0 ……..

1

1.45        0……….

1.9           2.51

0……….

V225

•

•

•

+1                         +2                +2
1.0                        0.5               0.5

0

~ 10

~10
In PE, either synchronous or asynchronous value
updates can be followed
If Threshold of 0.01 is applied then approx., at 46th
iteration algorithm converges
Assume that Asynchronous method is used &
Thresholding is not applied. In this case at approx., near
225th iteration values converge

BITS PILANI WILP

Deep Reinforcement Learning

23

Dynamic Programming – Policy Iteration
Policy Improvement

ɵ = 0.01

Cool

Go Slow
Fast

Go

Cool

cool          warm

0             0             0 ……..

1

1.45        0……….

1.9           2.51

0……….

V225

~10

~ 10

0

+1                         +2                +2
1.0                        0.5               0.5

After PE is done, PI starts where the last value
from PE is used to find the next best action. In
this PI phase all actions are analysed and best
action that MAXimises the value is chosen to
update the policy

BITS PILANI WILP

Deep Reinforcement Learning

24

Dynamic Programming – Policy Iteration
Policy Improvement

ɵ = 0.01

Cool

Go Slow
Fast

Go

Cool

cool          warm

0             0             0 ……..

1

1.45        0……….

1.9           2.51

0……….

V225

~10

~ 10

0

+1                         +2                +2
1.0                        0.5               0.5

After PE is done, PI starts where the last value
from PE is used to find the next best action. In
this PI phase all actions are analysed and best
action that MAXimises the value is chosen to
update the policy

BITS PILANI WILP

Deep Reinforcement Learning

25

Dynamic Programming – Policy Iteration
Policy Improvement Completes

ɵ = 0.01

Cool

Go Slow
Go Fast

Cool

cool          warm

0             0             0 ……..

1

1.45        0……….

1.9           2.51

0……….

V225

~10

~ 10

0

+1                         +2                +2
1.0                        0.5               0.5

π1

State

Cool

Warm

Best Action

Fast

Slow

Overheated

-

BITS PILANI WILP

Deep Reinforcement Learning

26

Dynamic Programming – Policy Iteration
Continue another cycle of PE🡪PI

ɵ = 0.01

10             10             0 ……..

Cool

Go Slow
Go Fast

Cool

cool          warm

+1                         +2                +2
1.0                        0.5               0.5

π1

State

Cool

Warm

Best Action

Fast

Slow

Overheated

-

cycle
of
converges

this

After
algorithm
with values :
V(cool) = 15.5
V(Warm) = 14.5

BITS PILANI WILP

Deep Reinforcement Learning

27

Dynamic Programming - Policy Iteration

1 Observation

• Policy iteration consists of two simultaneous, interacting processes,
one making the value function consistent with the current policy (policy
evaluation), and the other making the policy greedy with respect to the
current value function (policy improvement).
• In policy iteration,
before the other begins, but this is not really necessary.

these two processes alternate, each completing

Solution : GPI Generalized Policy Iteration

• Generalized policy iteration (GPI) to refer to the general idea of letting
policy-evaluation
interact,
independent of the granularity and other details of the two processes.
Almost all reinforcement learning methods are well described as GPI.

improvement

processes

policy

and

Idea (Do this as an exercise for given problem)

• In one cycle perform only one iteration of Policy Evaluation (ie.,Value
Updates) without waiting for convergence immediately follow by Policy
Improvement.

BITS PILANI WILP

Deep Reinforcement Learning

28

TABLE OF CONTENTS

1

2

3

4

MDP

DP
MC

TD

BITS PILANI WILP

Deep Reinforcement Learning

29

Problem Definition

Race Car Laps
In a modified Race car, there is a training track where agent is given a known (sometimes incomplete)
map and risk factors(dynamics) may not be known in advance. Agent knows exactly where it is but its
actions impact on the engine state change is difficult to predict (UNKNOWN MODEL).

With partial knowledge, the agent can compute optimal policies by trying through random experiments
(Sampling). Car shuts down when its engine get overheated (optional terminal state) or Car stops once
the predefined no.of.laps are completed.

Key Characteristics:

The agent must act under uncertainty —

percepts are local, and the agent must reason about hidden dangers

Assume there are fuel constraints or/and No.of.Laps to complete!

At every time step there is no way clear indication of

Impact of next potential engine temperature depending on the

current engine state. The entire past changes might lead to any

possible state change. Hence immediate reward is not always available.

BITS PILANI WILP

Deep Reinforcement Learning

32

MARKOV DECISION PROCESS FORMALIZATION (Reduced)

1

States (S)

• S = (Cool(C), Warm(W), Overheated(O)) #Engine Temperature

• Finite State MDP

2

Actions (A)

• A = {Go Slow(S), Go Fast(F)}

3

4

Rewards (R) and/or State Transition Probabilities (P)

may be non-stationary

Policy still needs estimation of V(S) , Q(S,A) i.e., MDP components but its is
not a necessity that the process is expected to follow a Markov Property!!

BITS PILANI WILP

Deep Reinforcement Learning

33

5

6

7

Monte Carlo Methods

1 Given

• S, A, optionally R(s, a, s`)

2 To find

• Policy π

3 Solution

• Sample Episodes
• Compute estimates of the value by discounted returns

✔ Simple average
✔ Weighted average
✔ Normalized weighted average

4

Idea

• On Policy :

• Generate Sample/Experience 🡪 Evaluate using Return 🡪 Improve

• Off Policy :

• Refer to Sample/Experience generated by another reference(behavior) policy  🡪

Evaluate using Return 🡪 Improve

BITS PILANI WILP

Deep Reinforcement Learning

34

Monte Carlo Method

On Policy Control Algorithm

Monte Carlo

Ꜫ = 0.2
γ = 0.6

0              0          0

0            0             0

Q0

Q1

Q2

π0

State

Cool

Warm

Best
Action

Slow

Fast

Overheated

-

P(F)

P(S)

0.4

0.6

-

0.6

0.4

-

BITS PILANI WILP

Deep Reinforcement Learning

36

First Visit Policy Evaluation

Monte Carlo

Ꜫ = 0.2
γ = 0.6

0              0          0

0            0             0

Q0

Q1

Q2

Episode 1: C, F, 2, W, S, 1, C, F, 2, W, F, -10, O
G=0

π0

State

Cool

Warm

Best
Action

Slow

Fast

Overheated

-

P(F)

P(S)

0.4

0.6

-

0.6

0.4

-

BITS PILANI WILP

Deep Reinforcement Learning

37

First Visit Policy Evaluation

Monte Carlo

Ꜫ = 0.2
γ = 0.6

0              0          0

0            0             0

-4 ,1.16   0       -10

-1.4

0             0

Q0

Q1

Q2

Episode 1: C, F, 2, W, S, 1, C, F, 2, W, F, -10, O
G=0

t=3: G3 = -10
t=2: G2 = 2 + (0.6)(-10) = -4  #Not used in First Visit
t=1: G1 = 1+ (0.6*2) + (0.6*0.6*-10) = -1.4
t=0: G0 = 2+ (0.6*1) + (0.6*0.6*2) + (0.6*0.6*0.6-10) = 1.16

π0

State

Cool

Warm

Best
Action

Slow

Fast

Overheated

-

P(F)

P(S)

0.4

0.6

-

0.6

0.4

-

BITS PILANI WILP

Deep Reinforcement Learning

38

First Visit Policy Evaluation

Monte Carlo

Ꜫ = 0.2
γ = 0.6

0              0          0

0            0             0

-4 ,1.16   0       -10

-1.4

0             0

Q0

Q1

Q2

Episode 1: C, F, 2, W, S, 1, C, F, 2, W, F, -10, O
G=0

Episode 1:

t=3: G3 = -10
t=2: G2 = 2 + (0.6)(-10) = -4  #Not used in First Visit
t=1: G1 = 1+ (0.6*2) + (0.6*0.6*-10) = -1.4
t=0: G0 = 2+ (0.6*1) + (0.6*0.6*2) + (0.6*0.6*0.6-10) = 1.16

t=3: Q(W, F) = -10
t=2: Q(C, F) =  -4
t=1: Q(W, S) = -1.4
t=0: Q(C, F) =  1.16

π0

State

Cool

Warm

Best
Action

Slow

Fast

Overheated

-

P(F)

P(S)

0.4

0.6

-

0.6

0.4

-

BITS PILANI WILP

Deep Reinforcement Learning

39

First Visit Policy Evaluation

Monte Carlo

Ꜫ = 0.2
γ = 0.6

0              0          0

0            0             0

1.16

0       -10

-1.4

0             0

Q0

Q1

Q2

Episode 1: C, F, 2, W, S, 1, C, F, 2, W, F, -10, O
G=0

Episode 1:

t=3: G3 = -10
t=2: G2 = 2 + (0.6)(-10) = -4  #Not used in First Visit
t=1: G1 = 1+ (0.6*2) + (0.6*0.6*-10) = -1.4
t=0: G0 = 2+ (0.6*1) + (0.6*0.6*2) + (0.6*0.6*0.6-10) = 1.16

t=3: Q(W, F) = -10
t=2: Q(C, F) =  -4
t=1: Q(W, S) = -1.4
t=0: Q(C, F) =  1.16

π1

State

Cool

Warm

Best
Action

Slow

Slow

Overheated

-

P(F)

P(S)

0.2

0.2

-

0.8

0.8

-

BITS PILANI WILP

Deep Reinforcement Learning

40

Policy Improvement

Monte Carlo

Ꜫ = 0.2
γ = 0.6

0              0          0

0            0             0

1.16

0       -10

-1.4

0             0

Q0

Q1

Q2

Episode 1: C, F, 2, W, S, 1, C, F, 2, W, F, -10, O
G=0

Episode 1:

t=3: G3 = -10
t=2: G2 = 2 + (0.6)(-10) = -4  #Not used in First Visit
t=1: G1 = 1+ (0.6*2) + (0.6*0.6*-10) = -1.4
t=0: G0 = 2+ (0.6*1) + (0.6*0.6*2) + (0.6*0.6*0.6-10) = 1.16

t=3: Q(W, F) = -10
t=2: Q(C, F) =  -4
t=1: Q(W, S) = -1.4
t=0: Q(C, F) =  1.16

Episode 2: C, S, 1, C, F, 2, W, F, -10, O
G=0
t=2: G2 = -10
t=1: G1 = 2 + (0.6)(-10) = -4
t=0: G0 = 1+ (0.6*2) + (0.6*0.6*-10) = -1.4

π1

State

Cool

Warm

Best
Action

Slow

Slow

Overheated

-

P(F)

P(S)

0.2

0.2

-

0.8

0.8

-

Policy Evaluation

BITS PILANI WILP

Deep Reinforcement Learning

41

Monte Carlo

Ꜫ = 0.2
γ = 0.6

Q0

Q1

Q2

0              0          0

0            0             0

1.16

0       -10

-1.4

0             0

-1.42    -1.4

-10

0

0             0

Episode 1: C, F, 2, W, S, 1, C, F, 2, W, F, -10, O
G=0

Episode 1:

t=3: G3 = -10
t=2: G2 = 2 + (0.6)(-10) = -4  #Not used in First Visit
t=1: G1 = 1+ (0.6*2) + (0.6*0.6*-10) = -1.4
t=0: G0 = 2+ (0.6*1) + (0.6*0.6*2) + (0.6*0.6*0.6-10) = 1.16

t=3: Q(W, F) = -10
t=2: Q(C, F) =  -4
t=1: Q(W, S) = -1.4
t=0: Q(C, F) =  1.16

π1

State

Cool

Warm

Best
Action

Slow

Slow

Overheated

-

P(F)

P(S)

0.2

0.2

-

0.8

0.8

-

Episode 2: C, S, 1, C, F, 2, W, F, -10, O
G=0
t=2: G2 = -10
t=1: G1 = 2 + (0.6)(-10) = -4
t=0: G0 = 1+ (0.6*2) + (0.6*0.6*-10) = -1.4

BITS PILANI WILP

Episode 2:

t=2: Q(W, F) = -10
t=1: Q(C, F) =  avg(1.16,-4) = -1.42
t=0: Q(C, S) = -1.4
Deep Reinforcement Learning

Policy PE & PI

42

Monte Carlo

Ꜫ = 0.2
γ = 0.6

Q0

Q1

Q2

0              0          0

0            0             0

1.16

0       -10

-1.4

0             0

-1.42    -1.4

-10

0

0             0

Episode 3: C, S, 1, C, S, 1, C, F, 2, W, F, -10, O
G=0

Episode 3:

π1

State

Cool

Warm

Best
Action

Slow

Slow

Overheated

-

P(F)

P(S)

0.2

0.2

-

0.8

0.8

-

t=3: G3 = -10
t=2: G2 = 2 + (0.6)(-10) = -4
t=1: G1 = 1+ (0.6*2) + (0.6*0.6*-10) = -1.4
t=0: G0 = 1+ (0.6*1) + (0.6*0.6*2) + (0.6*0.6*0.6-10) = 0.16

t=3: Q(W, F) = -10
t=2: Q(C, F) =  avg(-4,1.16,-4) = -2.28
t=1: Q(C, S) = -1.4
t=0: Q(C, S) =  avg(0.16,-1.4)

= -0.62

BITS PILANI WILP

Deep Reinforcement Learning

43

First Visit Policy Evaluation

Monte Carlo

Ꜫ = 0.2
γ = 0.6

Q0

Q1

Q2

Q3

0              0          0

0            0             0

1.16

0       -10

-1.4

0             0

-1.42    -1.4

-10

-2.28   -0.62 -10

0

0

0             0

0             0

Episode 3:

π2

State

Cool

Warm

Best
Action

Slow

Slow

Overheated

-

P(F)

P(S)

0.2

0.2

-

0.8

0.8

-

t=3: Q(W, F) = -10
t=2: Q(C, F) =  avg(-4,1.16,-4) = -2.28
t=1: Q(C, S) = -1.4
t=0: Q(C, S) =  avg(0.16,-1.4)

= -0.62

BITS PILANI WILP

Deep Reinforcement Learning

44

After PE PI no change in π.
Policy converges towards safer actions

Monte Carlo Methods

1 Given

• S, A, optionally R(s, a, s`)

2 To find

• Policy π . This is referred to as TARGET policy

3 Solution

• Sample Episodes
• Compute estimates of the value by discounted returns

✔ Simple average
✔ Weighted average
✔ Normalized weighted average

4

Idea

• On Policy :

• Generate Sample/Experience 🡪 Evaluate using Return 🡪 Improve

• Off Policy :

• Refer to Sample/Experience generated by another reference(BEHAVIOUR) policy

🡪 Evaluate using Return 🡪 Improve

BITS PILANI WILP

Deep Reinforcement Learning

45

Monte Carlo Method

Off Policy Control Algorithm

Monte Carlo

0              0          0

0            0             0

Q

π

C

Ꜫ = 0.2
γ = 0.6

b

State

Cool

Warm

Overheated

P(F)

P(S)

0.4

0.6

-

0.6

0.4

-

BITS PILANI WILP

Deep Reinforcement Learning

47

Assume deterministic Target policy. Hence π(At | St) = 1
But the behavior policy (b) is Stochastic as defined

Monte Carlo

0              0          0

0            0             0

Q

π

C

Ep

G

W

t

At

0              0          0

0            0             0

π(St)

Ꜫ = 0.2
γ = 0.6

b

State

Cool

Warm

Overheated

P(F)

P(S)

0.4

0.6

-

0.6

0.4

-

BITS PILANI WILP

Deep Reinforcement Learning

48

Every Visit Policy Evaluation

Monte Carlo

0              0          0

0            0             0

Q

π

C

1

0

1

Ep

G

W

t

At

0              0          0

0            0             0

π(St)

Episode 1: C, F, 2, W, S, 1, C, F, 2, W, F, -10, O
G=0

Ꜫ = 0.2
γ = 0.6

b

State

Cool

Warm

Overheated

P(F)

P(S)

0.4

0.6

-

0.6

0.4

-

BITS PILANI WILP

Deep Reinforcement Learning

49

First Visit Policy Evaluation

Monte Carlo

0              0          0

0            0             0

Q

π

C

Ep

G

W

t

At

0              0          0

0            0             0

π(St)

Episode 1: C, F, 2, W, S, 1, C, F, 2, W, F, -10, O
G=0

t=3: G3 = -10

1

0

1

3

F

F

Ꜫ = 0.2
γ = 0.6

b

State

Cool

Warm

Overheated

P(F)

P(S)

0.4

0.6

-

0.6

0.4

-

BITS PILANI WILP

Deep Reinforcement Learning

50

First Visit Policy Evaluation

Monte Carlo

0              0          0

0            0             0

Q

π

C

Ep

G

W

t

At

0              0          1

0            0             0

π(St)

Episode 1: C, F, 2, W, S, 1, C, F, 2, W, F, -10, O
G=0

t=3: G3 = -10

1

-10

1

3

F

F

Ꜫ = 0.2
γ = 0.6

b

State

Cool

Warm

Overheated

P(F)

P(S)

0.4

0.6

-

0.6

0.4

-

BITS PILANI WILP

Deep Reinforcement Learning

51

Compute Return & Update the Count for Averaging

Monte Carlo

0              0       -10

0            0             0

Q

π

C

Ep

G

W

t

At

0              0          1

0            0             0

π(St)

Episode 1: C, F, 2, W, S, 1, C, F, 2, W, F, -10, O
G=0

t=3: G3 = -10

1

-10

1

3

F

F

Ꜫ = 0.2
γ = 0.6

b

State

Cool

Warm

Overheated

P(F)

P(S)

0.4

0.6

-

0.6

0.4

-

Compute the action value Q(W,F) using incremental update form adapted to perform normalized weighted average based updates. T his is
the WEIGHTED IMPORTANCE SAMPLING METHOD, which bounds the variance due to the normalizing effect!

BITS PILANI WILP

Deep Reinforcement Learning

52

Monte Carlo

0              0       -10

0            0             0

Q

π

C

Ep

G

W

t

At

0              0          1

0            0             0

π(St)

Episode 1: C, F, 2, W, S, 1, C, F, 2, W, F, -10, O
G=0

t=3: G3 = -10

1

-10

1

3

F

S

Ꜫ = 0.2
γ = 0.6

Policy
Improvement

b

State

Cool

Warm

Overheated

P(F)

P(S)

0.4

0.6

-

0.6

0.4

-

BITS PILANI WILP

Deep Reinforcement Learning

53

The best action is not the currently encountered
action in the sample!

Monte Carlo

0              0       -10

0            0             0

Q

π

C

Ep

G

W

t

At

0              0          1

0            0             0

π(St)

Episode 1: C, F, 2, W, S, 1, C, F, 2, W, F, -10, O
G=0

t=3: G3 = -10

1

-10

1

3

F

S

Ꜫ = 0.2
γ = 0.6

b

State

Cool

Warm

Overheated

P(F)

P(S)

0.4

0.6

-

0.6

0.4

-

BITS PILANI WILP

Deep Reinforcement Learning

54

Exits to the next time step without W update!

Monte Carlo

0              0       -10

0            0             0

Q

π

C

Ep

G

W

t

At

0              0          1

0            0             0

π(St)

Episode 1: C, F, 2, W, S, 1, C, F, 2, W, F, -10, O
G=0

t=3: G3 = -10
t=2: G2 = 2 + (0.6)(-10) = -4 #WILL BE used in EVERY Visit

1

-10

1

2

F

S

Ꜫ = 0.2
γ = 0.6

b

State

Cool

Warm

Overheated

P(F)

P(S)

0.4

0.6

-

0.6

0.4

-

BITS PILANI WILP

Deep Reinforcement Learning

55

Continue ……..

Monte Carlo

-4

0       -10

0            0             0

Q

π

C

Ep

G

W

t

At

1

0          1

0            0             0

π(St)

Episode 1: C, F, 2, W, S, 1, C, F, 2, W, F, -10, O
G=0

t=3: G3 = -10
t=2: G2 = 2 + (0.6)(-10) = -4

1

-4

1

2

F

S

Ꜫ = 0.2
γ = 0.6

b

State

Cool

Warm

Overheated

P(F)

P(S)

0.4

0.6

-

0.6

0.4

-

BITS PILANI WILP

Deep Reinforcement Learning

56

No change in W! Exit to next t

Monte Carlo

-4              0       -10

-1.4

0             0

Q

π

C

Ep

G

W

t

At

1              0          1

1

0             0

π(St)

Episode 1: C, F, 2, W, S, 1, C, F, 2, W, F, -10, O
G=0

t=3: G3 = -10
t=2: G2 = 2 + (0.6)(-10) = -4
t=1: G1 = 1+ (0.6*2) + (0.6*0.6*-10) = -1.4

1

-1.4

1

1

S

S

Ꜫ = 0.2
γ = 0.6

b

State

Cool

Warm

Overheated

P(F)

P(S)

0.4

0.6

-

0.6

0.4

-

BITS PILANI WILP

Deep Reinforcement Learning

57

Continue ……..

Monte Carlo

-4              0       -10

-1.4

0             0

Q

π

C

Ep

G

W

t

At

1              0          1

1

0             0

π(St)

Episode 1: C, F, 2, W, S, 1, C, F, 2, W, F, -10, O
G=0

t=3: G3 = -10
t=2: G2 = 2 + (0.6)(-10) = -4
t=1: G1 = 1+ (0.6*2) + (0.6*0.6*-10) = -1.4

Ꜫ = 0.2
γ = 0.6

W = 1/b(S|W)
= 1/0.4
=2.5

1

-1.4

2.5

1

S

S

b

State

Cool

Warm

Overheated

P(F)

P(S)

0.4

0.6

-

0.6

0.4

-

BITS PILANI WILP

Deep Reinforcement Learning

58

At t=1 the best action & current action is same
.Hence the Global Weight for WIS is updated

Monte Carlo

1

-1.4

2.5

0

F

S

-3.14          0       -10

-1.4

0             0

Q

π

C

Ep

G

W

t

At

3.5

0          1

1

0             0

π(St)

Episode 1: C, F, 2, W, S, 1, C, F, 2, W, F, -10, O
G=0

t=3: G3 = -10
t=2: G2 = 2 + (0.6)(-10) = -4
t=1: G1 = 1+ (0.6*2) + (0.6*0.6*-10) = -1.4
t=0: G0 = 2+ (0.6*1) + (0.6*0.6*2) + (0.6*0.6*0.6-10) = 1.16

Ꜫ = 0.2
γ = 0.6

b

State

Cool

Warm

Overheated

P(F)

P(S)

0.4

0.6

-

0.6

0.4

-

BITS PILANI WILP

Deep Reinforcement Learning

59

Continuing to next t=0……..
After update observe that the episode terminates

Monte Carlo

Ep

2

-3.14          0       -10

-1.4       0             0

Q

π

C

G

W

t

At

3.5              0        2

1          0             0

π(St)

Episode 1: C, F, 2, W, S, 1, C, F, 2, W, F, -10, O

Episode 2: C, S, 1, C, F, 2, W, F, -10, O
G=0
t=2: G2 = -10

0 🡪-10

1

2

F

S

Ꜫ = 0.2
γ = 0.6

b

State

Cool

Warm

Overheated

P(F)

P(S)

0.4

0.6

-

0.6

0.4

-

BITS PILANI WILP

Deep Reinforcement Learning

60

Generate new episode from “b” . Continue ……
Results of every time-step in Episode 2 is shown

Monte Carlo

Ep

2

-7.01

0       -10

-1.4       0             0

Q

π

C

G

W

t

At

4.5

0        2

1          0             0

π(St)

Episode 1: C, F, 2, W, S, 1, C, F, 2, W, F, -10, O

Episode 2: C, S, 1, C, F, 2, W, F, -10, O
G=0
t=2: G2 = -10
t=1: G1 = 2 + (0.6)(-10) = -4

-10🡪-4

1

1

F

S

Ꜫ = 0.2
γ = 0.6

b

State

Cool

Warm

Overheated

P(F)

P(S)

0.4

0.6

-

0.6

0.4

-

BITS PILANI WILP

Deep Reinforcement Learning

61

Continue ……
Results of every time-step in Episode 2 is shown

Monte Carlo

Ep

2

Ꜫ = 0.2
γ = 0.6

-7.01     -1.4

-10

-1.4       0             0

Q

π

C

G

W

t

At

4.5             1

2

1          0             0

π(St)

Episode 1: C, F, 2, W, S, 1, C, F, 2, W, F, -10, O

Episode 2: C, S, 1, C, F, 2, W, F, -10, O
G=0
t=2: G2 = -10
t=1: G1 = 2 + (0.6)(-10) = -4
t=0: G0 = 1+ (0.6*2) + (0.6*0.6*-10) = -1.4

W = 1/b(S|W)
= 1/0.6
=~1.67

-4🡪-1.4

1.67

0

S

S

b

State

Cool

Warm

Overheated

P(F)

P(S)

0.4

0.6

-

0.6

0.4

-

BITS PILANI WILP

Deep Reinforcement Learning

62

This completes processing second episode. Continue
next episode

Monte Carlo Methods

1 Given

• S, A, optionally R(s, a, s`)

2 To find

• Policy π . This is referred to as TARGET policy

3 Solution

• Sample Episodes
• Compute estimates of the value by discounted returns

✔ Simple average
✔ Weighted average  (OIS : Ordinary Importance Sampling)
✔ Normalized weighted average (WIS : Weighted Importance Sampling)

Idea
• On Policy :

4

• Generate Sample/Experience 🡪 Evaluate using Return 🡪 Improve

• Off Policy :

• Refer to Sample/Experience generated by another reference(BEHAVIOUR) policy

🡪 Evaluate using Return 🡪 Improve

BITS PILANI WILP

Deep Reinforcement Learning

63

Monte Carlo

-7.01     -1.4       -10

-1.4       0             0

Q

π

C

Ep

G

W

t

At

4.5             1        2

1          0             0

π(St)

Episode 1: C, F, 2, W, S, 1, C, F, 2, W, F, -10, O

Episode 2: C, S, 1, C, F, 2, W, F, -10, O

Ꜫ = 0.2
γ = 0.6

b

State

Cool

Warm

Overheated

P(F)

P(S)

0.4

0.6

-

0.6

0.4

-

Important Note : The Ordinary Importance Sampling (OIS) is unbiased
but will produce high variance. The same given algorithm can be
adapted to perform ordinary importance sampling by changing only the
count update equation to : C(St,At) 🡪 C(St,At) + 1

BITS PILANI WILP

Deep Reinforcement Learning

64

Monte Carlo

-7.01     -1.4       -10

-1.4       0             0

Q

π

C

3

0

1

Ep

G

W

t

At

4.5             1        2

1          0             0

π(St)

Episode 1: C, F, 2, W, S, 1, C, F, 2, W, F, -10, O

Episode 2: C, S, 1, C, F, 2, W, F, -10, O

Episode 3: C, S, 1, C, S, 1, C, F, 2, W, F, -10, O

Students are advised to take this episode #3 as an exercise for practice
…………

Ꜫ = 0.2
γ = 0.6

b

State

Cool

Warm

Overheated

P(F)

P(S)

0.4

0.6

-

0.6

0.4

-

BITS PILANI WILP

Deep Reinforcement Learning

65

DP

VS

MC

s

a

s`

a`

.
.

ST

BITS PILANI WILP

Deep Reinforcement Learning

66

DP

VS

MC

s,a

s`

a`

.
.

ST

BITS PILANI WILP

Deep Reinforcement Learning

67

TABLE OF CONTENTS

1

2

3

4

MDP

DP
MC

TD

BITS PILANI WILP

Deep Reinforcement Learning

68

Problem Definition

(Modified) Race Car Example
In a modified Race car, there is a training track where agent is given a known (sometimes incomplete)
map and risk factors(dynamics) may not be known in advance. Agent knows exactly where it is but its
actions impact on the engine state change is difficult to predict (UNKNOWN MODEL).

With partial knowledge, the agent can compute optimal policies by trying through random experiments
(Sampling). Car sometimes may shuts down when its engine get overheated (optional terminal state)
otherwise Race is allowed to proceed indefinitely (NO predefined no.of.laps to complete)

Key Characteristics:

The agent must act under uncertainty —

percepts are local, and the agent must reason about hidden dangers

Assume there are neither fuel constraints nor No.of.Laps to complete!

At every time step there is an indication (direct/indirect) of

Impact of next potential engine temperature depending on the

current engine state. Immediate reward is available.

BITS PILANI WILP

Deep Reinforcement Learning

69

Temporal Difference Learning Methods

1 Given

• S, A, R(s, a, s`), (optionally)P(a | s)

2 To find

• Policy π

3 Solution

• Sample Episodes
• Compute estimates of the value by discounted next state estimates (bootstrapping)

✔ Simple average
✔ Weighted average
✔ Normalized weighted average

4

Idea

• On Policy :

• Generate Sample/Experience 🡪 Evaluate using bootstrapping 🡪 Improve

• Off Policy :

• Refer to Sample/Experience generated by another reference(behavior) policy  🡪

Evaluate using bootstrapping 🡪 Improve

BITS PILANI WILP

Deep Reinforcement Learning

70

Temporal Difference Learning
Methods

Policy Evaluation (PE) Algorithm
TD(0)

TD(0)

0                      0                    0

V0

V1

V2

Episode 1: C

Important Note :
• In few textbooks/ running incremental upcoming
examples, dynamics are given so only to simulate
trajectories and show updates step by step. TD itself
doesn’t require knowing the full transition model — it
only needs sampled transitions (s,a,r,s′)  while training
from scratch ie., when policy is not known/learnt yet.
• The dynamics are provided for clarity and
reproducibility,  not because TD requires them. In
practice, TD works model-free, just like Monte
Carlo.

Ꜫ = 0.1
γ = 0.9
α  = 0.5

π

Use case : A driving policy is already learnt
which needs to be evaluated for monitoring or
certification/approval by safety engineers.

BITS PILANI WILP

Deep Reinforcement Learning

72

TD(0)

1

0                    0

V0

V1

V2

Episode 1: C, F, 2, W

Target = R+ γV(W) = 2+(0.9 * 0) = 2
TD Error = Target – Old Estimate = 2-V(C) = 2-0 = 2
Update the value : V(C) = 0 + 0.5(2) = 1

Ꜫ = 0.1
γ = 0.9
α  = 0.5

π

BITS PILANI WILP

Deep Reinforcement Learning

73

TD(0)

1                     0.95

0

V0

V1

V2

Ꜫ = 0.1
γ = 0.9
α  = 0.5

Episode 1: C, F, 2, W, S, 1, C

V(W) = 0 + 0.5 [1+ (0.9*1)-0] = 0.95

π

BITS PILANI WILP

Deep Reinforcement Learning

74

In practice, we can define an episode cutoff (e.g., after 2 or10 steps or
when Overheated occurs). If Overheated isn’t reached,  still the episode
an be programmed to end artificially. That’s how learning continues.

TD(0)

1                     0.95                  0

1.95                 2.40              1.40

V0

V1

V2

Episode 1: C, F, 2, W, S, 1, C
Episode 2: C, F, 2, C, F, 2, W, S, 1, W

t=0 : V(C) = 1 + 0.5 [2+ (0.9*1)-1] = 1.95
t=1 : V(C) = 1.95 + 0.5 [2+ (0.9*0.95)-1.95] = ~2.4

t=2 : V(W) = 0.95 + 0.5 [1+ (0.9*0.95)-0.95] = ~1.40

Ꜫ = 0.1
γ = 0.9
α  = 0.5

π

BITS PILANI WILP

Deep Reinforcement Learning

75

Continued for 1 more episode…..

Temporal Difference Learning
Methods

On Policy Control Algorithms

Temporal Difference Learning
Methods

On Policy Control Algorithms
SARSA

SARSA

0              0          0

0            0             0

Q0

Q1

Q2

Episode 1: C

Ꜫ = 0.1
γ = 0.9
α  = 0.8

π

BITS PILANI WILP

Deep Reinforcement Learning

78

Use case : A driving policy is already learnt but there are few
unforeseen changes. Policy needs to be retrained to reflect the
actual risk observed via exploration

Ꜫ = 0.1
γ = 0.9
α  = 0.8

SARSA

1.6

0          0

0            0             0

Q1

Q2

Q3

Episode 1: C, F, 2, W, S

Q(C,F) = 0 + 0.8 [2+ (0.9*0)-0] = 1.6

π

From State “C” & “W”, Action “F” & “S” are derived
respectively  by applying  E-greedy on current policy  from
Q values learnt till now.
In the shown time step : (S,A,R,S,A) = (C,F,2,W,S)

BITS PILANI WILP

Deep Reinforcement Learning

79

SARSA

1.6           0          0

1.95

0           0

Q1

Q2

Q3

Ꜫ = 0.1
γ = 0.9
α  = 0.8

Episode 1: C, F, 2, W, S, 1, C , F

Q(W,S) = 0 + 0.6 [1+ (0.9*1.6)-0] = ~1.95

π

BITS PILANI WILP

Deep Reinforcement Learning

80

Terminating episode 1 after 2 steps. In practice, we can define an episode
cutoff (e.g., after 2 or10 steps or when Overheated occurs). If Overheated isn’t
reached,  still the episode an be programmed to end artificially. That’s how learning
continues.

SARSA

1.6          0          0

1.95            0

3.62          0          -8

1.32            0

Q1

Q2

Q3

Episode 1: C, F, 2, W, S, 1, C , F
Episode 2: C, F, 2, C, F, 2, W, S, 1, W , S, 1, W , F, -10, O

t=0 : Q(C,F) = 1.6 + 0.8 [2+ (0.9*1)-1.6] = 3.07
t=1 : Q(C,F) = 3.07 + 0.8 [2+ (0.9*1.95)-3.07] = ~3.62
t=2 : Q(W,S) = 1.95 + 0.8 [1+ (0.9*1.95)-1.95] = ~2.59
t=3 : Q(W,S) = 2.59 + 0.8 [1+ (0.9*0)-2.59] = ~1.32
t=4 : Q(W,F) = 0 + 0.8 [-10+ (0.9*0)-0] = ~-8

Ꜫ = 0.1
γ = 0.9
α  = 0.8

π

BITS PILANI WILP

Deep Reinforcement Learning

81

SARSA

Q1

Q2

Q3

Q4

1.6          0          0

1.95            0

3.62          0          -8

1.32

0

3.62          0       6.48     -4.69

0

3.62          0       6.48     +4.47

0

Episode 1: C, F, 2, W, S, 1, C , F
Episode 2: C, F, 2, C, F, 2, W, S, 1, W , S, 1, W , F, -10, O

Episode 3: W, S, +1, W, F, +10, O
t=0 : Q(W,S)  = 1.32 + 0.8 [1+ (0.9*-8)-1.32] = -4.69
t=1 : Q(W,F) = -8 + 0.8 [10+ (0.9*0)+8] = ~+6.4

Episode 4: W, S, +1, W, F
t=0 : Q(W,S) = -4.69 + 0.8 [1+ (0.9*6.4)+4.69] = ~+4.47

Ꜫ = 0.1
γ = 0.9
α  = 0.8

Continued for two more episodes….
Observe the  difference in value updates w.r.t Q(W,S)
between successive time steps in episodes 3 & 4.
At the worst case on larger learning rate eg., 0.8 the pull
is even larger
This large pull is an effect of the VARIANCE produced
Solution to tackle : Expected SARSA

π

BITS PILANI WILP

Deep Reinforcement Learning

82

Temporal Difference Learning
Methods

On Policy Control Algorithms
Expected SARSA

Expected SARSA

0              0          0

0            0             0

Q0

Q1

Q2

Episode 1: C

Ꜫ = 0.1
γ = 0.9
α  = 0.8

π

BITS PILANI WILP

Deep Reinforcement Learning

84

Expected SARSA

1.6

0          0

0            0             0

Q1

Q2

Q3

Episode 1: C, F, 2, W, S

Q(C,F) = 0 + 0.8 [2+ (0.9*(0.5*Q(W,S)+0.5*Q(W,F))-0] = 1.6

Ꜫ = 0.1
γ = 0.9
α  = 0.8

Important note from TextBook:
In these results Expected Sarsa was used on-policy, but in general it might use a
policy different from the target policy to generate behavior, in which case
it becomes an off-policy algorithm. For example, suppose the target is the greedy
policy while behavior is more exploratory; then Expected Sarsa is exactly Q-
learning.

π

Actions “F” & “S` are derived by applying E-greedy on policy from state “C” &“W”, For above highlighted
timestep:  (S,A,R,S) = (C,F,2,W)
During bootstrapping the expected values are used.
For simplicity in this episode its assumed that all actions are equiprobable for state “W”

BITS PILANI WILP

Deep Reinforcement Learning

85

Expected SARSA

1.6          0          0

1.37

0           0

Q1

Q2

Q3

Ꜫ = 0.1
γ = 0.9
α  = 0.8

Episode 1: C, F, 2, W, S, 1, C , F

Q(W,S) = 0 + 0.8 [1+ (0.9*(0.5*Q(C,S)+0.5*Q(C,F)))-0] = ~1.37

π

BITS PILANI WILP

Deep Reinforcement Learning

86

Assumed that all actions are equiprobable from a state in
this episode

Expected SARSA

1.6          0          0

1.37          0           0

2.59         0        -8

1.57           0

Q1

Q2

Q3

Episode 1: C, F, 2, W, S, 1, C , F
Episode 2: C, F, 2, C, F, 2, W, S, 1, W , S, 1, W , F, -10, O

t=0 : Q(C,F) = 1.6+0.8(2+0.9(0.5*1.6+0.5*0)−1.6)=~2.496
t=1 : Q(C,F) = 2.496+0.8(2+0.9(0.5*1.37+0.5*0)−2.496)=~2.59
t=2 : Q(W,S) = 1.37+0.8(1+0.9(0.5*1.37+0.5*0)−1.37)=~1.57
t=3 : Q(W,S) = 1.57 + 0.8 [1+0.9(0.5*1.57+0.5*0)−1.57] = ~1.68
t=4 : Q(W,F) = 0 + 0.8 [-10+ (0.9*0)-0] = ~-8

Ꜫ = 0.1
γ = 0.9
α  = 0.8

π

BITS PILANI WILP

Deep Reinforcement Learning

87

Continued for one more episode….
Assumed likelihood for all the states “_” for simplicity
:P(S|_) = 0.05, P(F|_) = 0.5

Ꜫ = 0.1
γ = 0.9
α  = 0.8

Expected SARSA

Q1

Q2

Q3

Q4

1.6          0          0

1.37          0           0

2.59         0        -8

1.57

0

2.59         0        6.4      -1.14

0

2.59         0        6.4      +2.46

0

Episode 1: C, F, 2, W, S, 1, C , F
Episode 2: C, F, 2, C, F, 2, W, S, 1, W , S, 1, W , F, -10, O

Episode 3: W, S, +1, W, F, +10, O
t=0 : Q(W,S)  = 1.57 + 0.8 [1+ (0.9*((-8*0.5) + (1.57*0.5)))-1.57] = -1.14
t=1 : Q(W,F) = -8 + 0.8 [10+ (0.9*0)+8] = ~+6.4

Episode 4: W, S, +1, W, F
t=0 : Q(W,S) = -1.14 + 0.8 [1+ (0.9*((-1.14*0.5)+(6.4*0.5)))+1.14] = ~+2.46

Continued for one more episode….
Assumed likelihood for all the states “_” for simplicity
:P(S|_) = 0.05, P(F|_) = 0.5

BITS PILANI WILP

Deep Reinforcement Learning

88

Temporal Difference Learning
Methods

Off Policy Control Algorithms
Q-Learning

Q-Learning

0              0          0

0            0             0

Q0

Q1

Q2

Episode 1: C

Ꜫ = 0.1
γ = 0.9
α  = 0.8

π

BITS PILANI WILP

Deep Reinforcement Learning

90

Target Policy : Greedy (MAX) is used to evaluate /update the Q
values
Behavior Policy : ε-greedy is used to select actions based on the
policy derived from Q - Value

Q-Learning

1.6

0          0

0            0             0

Q1

Q2

Q3

Ꜫ = 0.1
γ = 0.9
α  = 0.8

Episode 1: C, F, 2, W, S

Q(C,F) = 0 + 0.8 [2+ (0.9* MAX{Q(W,S),Q(W,F)} )-0] = 1.6

π

BITS PILANI WILP

Deep Reinforcement Learning

91

Behavior Policy : ε-greedy is used to select actions based on the
policy derived from Q - Value . Here action “F” for state “C”
Target Policy : Greedy (MAX) is used to evaluate /update the Q
values.

Q-Learning

1.6           0          0

17.15

0             0

Q1

Q2

Q3

Ꜫ = 0.1
γ = 0.9
α  = 0.8

Episode 1: C, F, 2, W, S, 20, C , F

Q(W,S) = 0 + 0.8 [20+ (0.9*(MAX{Q(C,S), Q(C,F)})-0] = ~17.15

π

BITS PILANI WILP

Deep Reinforcement Learning

92

Terminating episode 1 after 2 steps. In practice, we can define an
episode cutoff (e.g., after 2 or10 steps or when Overheated occurs). If
Overheated isn’t reached,  still the episode an be programmed to end artificially.
That’s how learning continues.

Q-Learning

Q1

1.6           0          0

17.15      0             0

Q2

16.16       0        -8

11.64      0             0

Q3

Episode 1: C, F, 2, W, S, 20, C , F
Episode 2: C, F, 2, C, F, 4, W, S, -5, W , S, 1, W , F, -10, O

t=0 : Q(C,F) = 1.6+0.8(2+0.9(MAX{1.6,0})−1.6)=~3.07
t=1 : Q(C,F) = 3.07+0.8(4+0.9(MAX{0,17.15})−3.07)=~16.16
t=2 : Q(W,S) = 17.15+0.8(-5+0.9(MAX{0,17.15})−17.15)=~11.78
t=3 : Q(W,S) = 11.78 + 0.8 [1+0.9(MAX{0,11.78})−11.78] = ~11.64
t=4 : Q(W,F) = 0 + 0.8 [-10+ (0.9*0)-0] = ~-8

Ꜫ = 0.1
γ = 0.9
α  = 0.8

π

BITS PILANI WILP

Deep Reinforcement Learning

93

Target Policy : Greedy (MAX) is used to evaluate /update the Q
values
Behavior Policy : ε-greedy is used to select actions based on the
policy derived from Q - Value

Q-Learning

Q1

1.6           0          0

17.15      0             0

Q2

16.16       0        -8

11.64      0             0

Q3

Q4

Q5

Q6

16.16       0       6.4

14.71

0             0

16.16 11.39     6.4

22.50

0             0

16.16 11.39     6.4

16.70

0             0

16.16 11.39     6.4

19.37

0             0

Episode 1: C, F, 2, W, S, 20, C
Episode 2: C, F, 2, C, F, 4, W, S, -5, W , S, 1, W , F, -10, O

Episode 3: W, S, +5, W, F, +10, O
Episode 4: C, S, +1, W, S, +10, C
Episode 5: W, S, -5, W
Episode 6: W, S, +5, W

Ꜫ = 0.1
γ = 0.9
α  = 0.8

Observe the  difference in value updates w.r.t Q(W,S)
between successive time steps in episodes 3 to 6.
The true value is approx. Q(W,S) = 15
Due to MAX bias the values are overestimated and this is
more pronounced in the presence of NOISE
Sometimes this diverges from true value.
Solution to tackle : Double Q-Learning

π

** But in near-deterministic , less noisy environment , Q-learning
helps in faster convergence!

Few more episodes are completed and the results of the update
per Q(State, Action) is shown . Students are advised to practice
this.

BITS PILANI WILP

Deep Reinforcement Learning

94

Temporal Difference Learning
Methods

Off Policy Control Algorithms
Double Q-Learning

Target

Behavior

Ꜫ = 0.1
γ = 0.9
α  = 0.8

0           0         0                0

5             1        5           15

Q0

Q1

Q2

Episode 1: C

π

BITS PILANI WILP

Deep Reinforcement Learning

96

Target Policy : Q2 - Table
Behavior Policy : Q1-Table is available from other
sources/experience/logged data. Above algorithm learns to update
this as well.

Target

Behavior

Ꜫ = 0.1
γ = 0.9
α  = 0.8

Q1

5.2

0         0                0

5             1        5           15

Q2

Q3

Episode 1: C, F, 2, W, S

Q2(C,F)
= 0 + 0.8 [2+ (0.9* Q1(W, ARGMAX{Q2(W,S),Q2(W,F)})  )-0]
= 0 + 0.8 [2+ (0.9* Q1(W, F)-0]   #Here both S & F had same values hence randomly “F” is chosen
= 0 + 0.8 [2+ (0.9* 5) - 0]
= 5.2

π

BITS PILANI WILP

Deep Reinforcement Learning

97

Target Policy : Q2 - Table
Behavior Policy : Q1-Table is available from other
sources/experience/logged data. Above algorithm learns to update
this as well.

Target

Behavior

Ꜫ = 0.1
γ = 0.9
α  = 0.8

5.2          0         0           19.6

5             1        5           15

Q1

Q2

Q3

Episode 1: C, F, 2, W, S, 20, C , F

Q2(W,S) = 0 + 0.8 [20+ (0.9*(Q1(C, ARGMAX{Q2(C,S), Q2(C,F)}) )-0]
= 0 + 0.8 [20+ (0.9*(Q1(C, F) )-0]
= 0 + 0.8 [20+ (0.9*5)-0]

= ~19.6

π

BITS PILANI WILP

Deep Reinforcement Learning

98

Terminating episode 1 after 2 steps. In practice, we can define an
episode cutoff (e.g., after 2 or10 steps or when Overheated occurs). If
Overheated isn’t reached,  still the episode an be programmed to end artificially.
That’s how learning continues.

Target

Behavior

Q1

5.2          0         0           19.6

5             1        5           15

Q2

6.24        0

-8           13.74

18.3

1        5          15

Q3

Episode 1: C, F, 2, W, S, 20, C , F
Episode 2: C, F, 2, C, F, 4, W, S, -5, W , S, 1, W , F, -10, O

t=0 : Q2(C,F) = 5.2+0.8(2+0.9(Q1(C, ARGMAX{Q2(C,F), Q2(C,S)})) −5.2)=~6.24

Ꜫ = 0.1
γ = 0.9
α  = 0.8

π

For step 2 : The loop goes to Q1(S,A) where the behavior policy is updated:
t=1 : Q1(C,F) = 5+0.8(4+0.9(Q2(W, ARGMAX{ Q1(W,S) , Q1(W,F) }) )−5)
= 5+0.8(4+0.9(Q2(W, ARGMAX{ 15, 5}) )−5)
= 5+0.8(4+0.9(Q2(W, S) )−5)
= 5+0.8(4+0.9(19.6 )−5)    =~18.3

Only two time step is shown here .
Other time steps updated target policy ie., Q2 table and the
result is tabulated above.
BITS PILANI WILP

Deep Reinforcement Learning

Target Policy : Q2 - Table
Behavior Policy : Q1-Table is available from other
sources/experience/logged data. Above algorithm learns to
update this as well.

99

Target

Behavior

Q1

5.2          0         0           19.6

5             1        5           15

Q2

6.24        0        -8           13.74

18.3        1        5          15

Q3

Q4

Q5

Q6

6.24        0        9

13.74

18.3        1        5         16.89

6.24    12.9

9            15.71

18.3        1        5         15.87

6.24    12.9      9            10.57

18.3        1        5         15.87

6.24    12.9      9            13.7

18.3        1        5         15.87

Episode 1: C, F, 2, W, S, 20, C
Episode 2: C, F, 2, C, F, 4, W, S, -5, W , S, 1, W , F, -10, O

Ꜫ = 0.1
γ = 0.9
α  = 0.8

Note : Only in Episode 3
step 1 , episode 4 step 2,
the loop is simulated to
Q1(S,A) loop, where the
behavior policy is updated:

π

Episode 3: W, S, +5, W, F, +10, O
Episode 4: C, S, +1, W, S, +10, C
Episode 5: W, S, -5, W
Episode 6: W, S, +5, W

Two more episodes are completed and the results of the update
per Q(State, Action) is shown . Students are advised to practice
this.

BITS PILANI WILP

Deep Reinforcement Learning

100

Target

Behavior

Ꜫ = 0.1
γ = 0.9
α  = 0.8

Q1

5.2          0         0           19.6

5             1        5           15

Q2

6.24        0        -8           13.74

18.3        1        5          15

Q3

Q4

Q5

Q6

6.24        0        9

13.74

18.3        1        5         16.89

6.24    12.9

9            15.71

18.3        1        5         15.87

6.24    12.9      9            10.57

18.3        1        5         15.87

6.24    12.9      9            13.7

18.3        1        5         15.87

BITS PILANI WILP

Deep Reinforcement Learning

101

DP

TD

MC

s

a

s`

a`

.
.

ST

BITS PILANI WILP

Deep Reinforcement Learning

102

DP

TD

MC

s,a

s`

a`

.
.

ST

BITS PILANI WILP

Deep Reinforcement Learning

103

