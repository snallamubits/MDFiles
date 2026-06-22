Markov Decision Processes– Solution

1) Invent a simple Markov decision process (MDP) with the following properties:
a) it has a goal state, b) its immediate action costs are all positive, c) all of its
actions can result with some probability in the start state, and d) the optimal
policy without discounting diﬀers from the optimal policy with discounting and
a discount factor of 0.9. Prove d) using value iteration.

Answer:

With no discount factor, action a1 is preferred over action a2 in state s1:

i
a1
a2
a3

0
0
0
0
0

State1

State2
State3

3

2

1

4
100 100.09 100.10009 100.1001001
101.18909
90 101.079
11.10010009
11.09
11
0
0
0

101.179
11.10009
0

. . .

With discount factor = 0.9, action a2 is preferred over action a1 in state s1:

i
a1
a2
a3

0
0
0
0
0

State1

State2
State3

2
100.081

3
100.089974

4
1
100
100.0900476
90 99.9711 100.0529011 100.0610432
11.09004761
11.08997399
11
0
0
0

11.081
0

. . .

2) Consider the following problem (with thanks to V. Conitzer): Consider a rover
that operates on a slope and uses solar panels to recharge. It can be in one of
three states: high, medium and low on the slope. If it spins its wheels, it climbs
the slope in each time step (from low to medium or from medium to high) or
stays high. If it does not spin its wheels, it slides down the slope in each time
step (from high to medium or from medium to low) or stays low. Spinning its
wheels uses one unit of energy per time step. Being high or medium on the
slope gains three units of energy per time step via the solar panels, while being

S3S1S2a1a2a30.0010.9990.9990.9990.0010.0019010011low on the slope does not gain any energy per time step. The robot wants to
gain as much energy as possible.

a) Draw the MDP graphically. b) Solve the MDP using value iteration with a
discount factor of 0.8. c) Describe the optimal policy.

Answer:

where L = low, M = medium and H = high.

Starting with 0 as initial values, value iteration calculates the following:

ITR
1
2
3
4
5
6
7
8
9
10
...
20
...
28
29

L
spin
-1.00
1.40*
2.52*
4.06*
4.77*
5.76*
6.21*
6.84*
7.14*
7.54*

don’t
0.00*
0.00
1.12
2.02
3.24
3.82
4.60
4.97
5.47
5.71

M
don’t
spin
3.00*
2.00
3.00
4.40*
4.12
6.32*
5.02
7.22*
6.24
8.44*
6.82
9.02*
9.80*
7.60
10.17* 7.97
10.67* 8.47
10.91* 8.71

H
spin
2.00
4.40
6.32
7.22
8.44
9.02
9.80
10.17
10.67
10.91

don’t
3.00*
5.40*
6.52*
8.06*
8.77*
9.76*
10.21*
10.84*
11.14*
11.54*

8.64*

6.88

12.08* 9.88

12.08

12.64*

8.76*
8.76*

7.00
7.00

12.20* 10.00
12.20* 10.00

12.20
12.20

12.76*
12.76*

At each iteration, the value of a state is the value of the maximizing action
in that state (since we are trying to maximize energy) and is marked with an
asterisk. For instance, in iteration 4, the value of L, v4(L), is computed as
follows:

v4(L, spin) = 0.8 × v3(M ) − 1 = 0.8 × 6.32 − 1 ∼ 4.06
v4(L, don(cid:48)t) = 0.8 × v3(L) + 0 = 0.8 × 2.52 ∼ 2.02
v4(L) = max(v4(L, spin), v4(L, don(cid:48)t)) = 4.06
The optimal policy is to spin when the rover is low or medium on the slope and
not to spin when it is high on the slope.

HLMP(Z | Y) = 0.5P(Z | Y) = 0.5spindon‘t spin0spin2spindon‘t spindon‘t spin2-133Now answer the three questions above for the following variant of the robot
problem: If it spins its wheels, it climbs the slope in each time step (from low
to medium or from medium to high) or stays high, all with probability 0.3. It
stays where it is with probability 0.7. If it does not spin its wheels, it slides
down the slope to low with probability 0.4 and stays where it is with probability
0.6. Everything else remains unchanged from the previous problem.

Answer:

Starting with 0 as initial values, value iteration calculates the following:

ITR
1
2
3
4
5
6
7
8
9
10
...
20
...
30
31
32

L
spin
-1.00
-0.28
0.07*
0.37*
0.75*
1.14*
1.49*
1.80*
2.06*
2.27*

don’t
0.00*
0.00*
0.00
0.05
0.30
0.60
0.91
1.19
1.44
1.65

M
spin
2.00
4.40
5.55*
6.44*
7.15*
7.72*
8.18*
8.54*
8.83*
9.07*

don’t
3.00*
4.44*
5.13
5.69
6.21
6.67
7.07
7.40
7.68
7.90

H
spin
2.00
4.40
5.55*
6.44*
7.15*
7.72*
8.18*
8.54*
8.83*
9.07*

don’t
3.00*
4.44*
5.13
5.69
6.21
6.67
7.07
7.40
7.68
7.90

3.08*

2.45

9.90*

8.72

9.90*

8.72

3.17*
3.17*
3.17*

2.53
2.54
2.54

9.99*
9.99*
9.99*

8.81
8.81
8.81

9.99*
9.99*
9.99*

8.81
8.81
8.81

In this variant, in iteration 4, the value of L, v4(L), is computed as follows:
v4(L, spin) = 0.8 × (0.3 × v3(M ) + 0.7 × v3(L)) − 1
= 0.8 × (0.3 × 5.55 + 0.7 × 0.07) − 1 ∼ 0.37
v4(L, don(cid:48)t) = 0.8 × v3(L) + 0 = 0.8 × 0.07 = 0.056
v4(L) = max(v4(L, spin), v4(L, don(cid:48)t)) = 0.37
The optimal policy is to spin, wherever the rover is on the slope.

HLMP(Z | Y) = 0.5P(Z | Y) = 0.5spinspinspindon‘t spindon‘t spin2323-10.70.70.30.30.40.40.60.6don‘t spin03) Consider the following problem (with thanks to V. Conitzer): Consider a rover
that operates on a slope. It can be in one of four states: top, high, medium and
low on the slope. If it spins its wheels slowly, it climbs the slope in each time
step (from low to medium or from medium to high or from high to top) with
probability 0.3. It slides down the slope to low with probability 0.7. If it spins
its wheels rapidly, it climbs the slope in each time step (from low to medium or
from medium to high or from high to top) with probability 0.5. It slides down
the slope to low with probability 0.5.

Spinning its wheels slowly uses one unit of energy per time step. Spinning its
wheels rapidly uses two units of energy per time step. The rover is low on the
slope and aims to reach the top with minimum expected energy consumptions.

a) Draw the MDP graphically. b) Solve the MDP using undiscounted value
iteration (that is, value iteration with a discount factor of 1). c) Describe the
optimal policy.

Answer:

where L = low, M = medium H = high, and T = top.

Starting with 0 as initial values, value iteration calculates the following:

L

M

H

ITR
1
2
3
4
5
6
7
8
9
...
196

slowly rapidly slowly rapidly slowly rapidly
1.00*
2.00*
3.00*
3.97*
4.93*
5.86*
6.78*
7.68*
8.54*

1.00*
1.70*
2.40*
3.10*
3.78*
4.45*
5.10
5.75
6.37

1.00*
2.00*
2.91*
3.82*
4.71*
5.58*
6.44*
7.22*
7.99*

2.00
2.50
3.00
3.50
3.99
4.46
4.93*
5.39*
5.84*

2.00
3.00
3.85
4.70
5.54
6.35
7.16
7.85
8.53

2.00
3.00
4.00
4.96
5.90
6.82
7.72
8.61
9.45

25.33* 25.67

23.13

22.00* 18.73

14.67*

LMHT(1)slowly  0.3(2)rapidly  0.50.70.70.70.50.50.5(2)rapidly   0.5(2)rapidly   0.5(1)slowly  0.3(1)slowly   0.3197
198
199

25.33* 25.67
25.33* 25.67
25.33* 25.67

23.13
23.13
23.13

22.00* 18.73
22.00* 18.73
22.00* 18.73

14.67*
14.67*
14.67*

At each iteration, the value of a state is the value of the minimizing action in
that state (since we are trying to minimize cost). For instance, in iteration 4,
the value of L, v4(L), is computed as follows:
v4(L, slowly) = 0.3 × v3(M ) + 0.7 × v3(L) + 1 (cid:39) 3.97
v4(L, rapidly) = 0.5 × v3(M ) + 0.5 × v3(L) + 2 (cid:39) 4.96
v4(L) = min(v4(L, slowly), v4(L, rapidly)) = 3.97
The optimal policy is to spin slowly in the low state and to spin rapidly in the
other states.

Here’s a sample C code for this value iteration.

#include <s t d i o . h>
#define min ( x , y )

( ( ( x)<(y ) ? ( x ) : ( y ) ) )

main ( )
{

int i t e r a t i o n = 0 ;
f l o a t l = 0 . 0 ;
f l o a t m = 0 . 0 ;
f l o a t h = 0 . 0 ;
f l o a t t = 0 . 0 ;
f l o a t l s l o w ,

l r a p i d , m slow , m rapid , h slow , h r a p i d ;

while ( 1 )

{

l s l o w = 1 + 0 . 7 ∗ l + 0 . 3 ∗m;
l r a p i d = 2 + 0 . 5 ∗ l + 0 . 5 ∗m;
m slow = 1 + 0 . 7 ∗ l + 0 . 3 ∗ h ;
m rapid = 2 + 0 . 5 ∗ l + 0 . 5 ∗ h ;
h s l o w = 1 + 0 . 7 ∗ l + 0 . 3 ∗ t ;
h r a p i d = 2 + 0 . 5 ∗ l + 0 . 5 ∗ t ;

p r i n t f ( ”%d : ” , ++i t e r a t i o n ) ;
p r i n t f ( ”%.2 f %.2 f ” ,
l r a p i d ) ;
l s l o w ,
p r i n t f ( ”%.2 f %.2 f ” , m slow , m rapid ) ;
p r i n t f ( ”%.2 f %.2 f \n” , h slow , h r a p i d ) ;
l = min ( l s l o w , l r a p i d ) ;
m = min ( m slow , m rapid ) ;
h = min ( h slow , h r a p i d ) ;

}

}

4) You won the lottery and they will pay you one million dollars each year for 20
years (starting this year). If the interest rate is 5 percent, how much money do
you need to get right away to be indiﬀerent between this amount of money and
the annuity?

Answer:
A million dollars we get right away is worth a million dollars to us now. A
million dollars we get in a year from now is worth γ = 1/(1 + 0.05) million
dollars to us now because, with interest, it would be (1/1.05) × 1.05 = 1 million
dollars in a year. Similarly, a million dollars we get in 19 years from now (in
the beginning of the 20th year) is worth only (1/1.05)19 ∼ 0.4 million dollars to
us now. Therefore, getting paid a million dollars each year for 20 years is worth
1 + γ + γ2 + · · · + γ19 = (1 − γ20)/(1 − γ) ∼ 0.623/0.0476 ∼ 13.08 million dollars
to us now.

5) Assume that you are trying to pick up a block from the table. You drop it
accidentally with probability 0.7 while trying to pick it up. If this happens, you
try again to pick it up. How many attempts does it take on average before you
pick up the block successfully?

Answer:
We can model this problem as an MDP as follows:

Now, we can calculate the expected cost with X = 1 + 0.7X + 0.3Y and Y = 0
(where X = on table and Y = picked up), which gives us X = 1/0.3 ∼ 3.33.

The Markov assumption is the assumption that, whenever one executes an
action in a state, the probability distribution over its outcomes is the same, no
matter how one got into the state. Is this assumption realistic here?

No. If the pickup operation does not work the ﬁrst time (e.g. because the block
is too slippery), it will likely not work the next time either.

6) Assume that you use undiscounted value iteration (that is, value iteration with
a discount factor of 1) for a Markov decision process with goal states, where
the action costs are greater than or equal to zero. Give a simple example that
shows that the values that value iteration converges to can depend on the initial
values of the states, in other words, the values that value iteration converges to
are not necessarily equal to the expected goal distances of the states.

Answer:

1pick up0.70.3on tablepicked upConsider the initial values v0(S) = 0 and v0(G) = 0. Value iteration deter-
mines the values after convergence to be v∗(S) = 0 and v∗(G) = 0, yet the (ex-
pected) goal distance of S is 1, not 0. Now consider the initial values v0(S) = 2
and v0(G) = 0. Value iteration determines the values after convergence to be
v∗(S) = 1 and v∗(G) = 0.

7) An MDP with a single goal state (S3) is given below. a) Given the expected
goal distances c(S1) = 7, c(S2) = 4.2, and c(S3) = 0, calculate the optimal
policy. b) Suppose that we want to follow a policy where we pick action a2 in
state S1 and action a3 in state S2. Calculate the expected goal distances of S1
and S2 for this policy.

Answer:
a) We use c(s, a) to denote the expected cost of reaching a goal state if one
starts in state s, executes action a and then acts according to the policy. Since
S3 is a goal state and S2 has only one available action, we only need to calculate
c(S1, a1) and c(S1, a2) in order to decide whether to execute a1 or a2 at S1.

c(S1, a1) = 0.25(1 + c(S3)) + 0.75(2 + c(S1)) = 0.25(1 + 0) + 0.75(2 + 7)) = 7

c(S1, a2) = 0.5(1 + c(S2)) + 0.5(2 + c(S1)) = 0.5(1 + 4.2) + 0.5(2 + 7)) = 7.1

Since c(S1, a1) < c(S1, a2), in the optimal policy, we execute a1 at S1.

b) Since the given policy executes a2 at S1, we simply ignore a1 during our
computation. We ﬁrst generate the following set of equations:

c(S1) = c(S1, a2) = 0.5(1 + c(S2)) + 0.5(2 + c(S1))

S0a1Ga21c(S2) = c(S2, a3) = 0.6(1 + c(S3)) + 0.4(2 + c(S1))

c(S3) = 0

Plugging c(S3) = 0 into our second equation, we get:

c(S2) = 0.6(1 + 0) + 0.4(2 + c(S1))

c(S2) = 1.4 + 0.4c(S1)

Plugging this value into our ﬁrst equation, we get:

c(S1) = 0.5(1 + 1.4 + 0.4c(S1)) + 0.5(2 + c(S1))

c(S1) = 2.2 + 0.7c(S1)

c(S1) = 2.2/0.3 = 7.33

Finally, we get:

c(S2) = 1.4 + 0.4c(S1) = 1.4 + 0.4(7.33) = 4.333

