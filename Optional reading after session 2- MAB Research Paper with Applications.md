9
1
0
2

r
p
A
2

]

G
L
.
s
c
[

1
v
0
4
0
0
1
.
4
0
9
1
:
v
i
X
r
a

A Survey on Practical Applications of Multi-Armed and Contextual Bandits

Djallel Bouneffouf1, Irina Rish2
1,2IBM Thomas J. Watson Research Center, Yorktown Heights, NY USA
{dbouneffouf, Irish }@us.ibm.com

Abstract

In recent years, multi-armed bandit (MAB)
framework has attracted a lot of attention in
various applications, from recommender sys-
tems and information retrieval to healthcare
and ﬁnance, due to its stellar performance
combined with certain attractive properties,
such as learning from less feedback. The
multi-armed bandit ﬁeld is currently ﬂourish-
ing, as novel problem settings and algorithms
motivated by various practical applications are
being introduced, building on top of the clas-
sical bandit problem. This article aims to pro-
vide a comprehensive review of top recent de-
velopments in multiple real-life applications of
the multi-armed bandit. Speciﬁcally, we intro-
duce a taxonomy of common MAB-based ap-
plications and summarize state-of-art for each
of those domains. Furthermore, we identify
important current trends and provide new per-
spectives pertaining to the future of this excit-
ing and fast-growing ﬁeld.

1 Introduction
Sequential decision-making problems, where at each
in time an agent must choose the best ac-
point
tion out of several alternatives, are frequently en-
countered in various practical applications,
from
trials [Durand et al., 2018]
clinical
to recommender
[Mary et al., 2015] and anomaly detection
systems
[Ding et al., 2019]. Often,
there is a side informa-
tion, or context, associated with each action (e.g., a
user’s proﬁle), and the feedback, or reward, is limited
to the chosen option. For example, in clinical trials
[Durand et al., 2018; Bastani and Bayati, 2015] the con-
text is the patient’s medical record (e.g. health condition,
family history, etc.), the actions correspond to the treat-
ment options being compared, and the reward represents
the outcome of the proposed treatment (e.g., success or
failure). An important aspect affecting the long-term

success in such settings is ﬁnding a good trade-off be-
tween exploration (e.g., trying a new drug) and exploita-
tion (choosing the known drug).

This inherent exploration vs. exploitation trade-off ex-
ists in many sequential decision problems, and is tra-
ditionally formulated as the multi-armed bandit (MAB)
problem, stated as follows: given K possible actions,
or “arms”, each associated with a ﬁxed but unknown
reward probability distribution [Lai and Robbins, 1985;
Auer et al., 2002], at each iteration (time point) an agent
selects an arm to play and receives a reward, sampled
from the respective arm’s probability distribution inde-
pendently from the previous actions. The task of an agent
is to learn how to choose its actions so that the cumulative
rewards over time is maximized. Different solutions have
been proposed for this problem, based on a stochastic
formulation [Lai and Robbins, 1985; Auer et al., 2002;
Bouneffouf and F´eraud, 2016] and a Bayesian formu-
lation [Agrawal and Goyal, 2012]; however, these ap-
proaches did not take into account the context, or side
information available to the agent.

A particularly useful version of the MAB is the con-
textual multi-arm bandit (CMAB), or simply the con-
textual bandit problem, where at each iteration, before
choosing an arm, the agent observes an N -dimensional
context, or feature vector. The agent uses this con-
text, along with the rewards of the arms played in the
past, to choose which arm to play in the current itera-
tion. Over time, the agent’s aim is to collect enough
information about the relationship between the context
vectors and rewards, so that it can predict the next
the current context
best arm to play by looking at
[Langford and Zhang, 2008; Agrawal and Goyal, 2013].
Different algorithms were proposed for the general case,
including LINUCB [Li et al., 2010], Neural Bandit
[Allesiardo et al., 2014] and Contextual Thompson Sam-
pling (CTS) [Agrawal and Goyal, 2013], where a linear
dependency is typically assumed between the expected
reward of an action and its context.

We will now provide an extensive overview includ-
ing various applications of the bandit framework, both

in real-life problem setting arising in multiple practi-
cal domains (healthcare, computer network routing, ﬁ-
nance, and beyond), as well as in computer science and
machine-learning in particular, where bandit approaches
can help improve hyperparameter tuning and other im-
portant algorithmic choices in supervised learning, active
learning and reinforcement learning.

2 Real-Life Applications of Bandit
As a general mathematical framework, the stochastic
multi-armed bandit setting addresses the primary difﬁ-
culty in sequential decision-making under uncertainty,
namely, the exploration versus exploitation dilemma, and
therefore provides a natural formalism for most real-life
online decision making problems.

2.1 Healthcare
Clinical trials. Collecting data for assessing treatment
effectiveness on animal models during the full range of
disease stages can be difﬁcult when using conventional
random treatment allocation procedures, since poor treat-
ments can cause deterioration of subject’s health. Au-
thors in [Durand et al., 2018] aim to design an adaptive
allocation strategy to improve the efﬁciency of data col-
lection by allocating more samples for exploring promis-
ing treatments. They cast this application as a contex-
tual bandit problem and introduce a practical algorithm
for exploration vs. exploitation in this framework. The
work relies on sub-sampling to compare treatment op-
tions using an equivalent amount of information. Pre-
cisely, they extend the sub-sampling strategy to contex-
tual bandit setting g by applying sub-sampling within
Gaussian Process regression.

Warfarin is the most widely used oral anticoagulant
agent in the world; however, dosing it correctly remains
a signiﬁcant challenge, as the appropriate dose can be
highly variable among individuals due to various clin-
ical, demographic and genetic factors. Physicians cur-
rently follow a ﬁxed-dose strategy: they start patients on
5mg/day (the appropriate dose for the majority of pa-
tients) and slowly adjust the dose over the course of a
few weeks by tracking the patients anti-coagulation lev-
els. However, an incorrect initial dosage can result in
highly adverse consequences such as stroke (if the initial
dose is too low) or internal bleeding (if the initial dose
is too high). Thus, authors in [Bastani and Bayati, 2015]
tackle the problem of learning and assigning an appropri-
ate initial dosage to patients by modeling the problem as
a multi-armed bandit with high-dimensional covariates,
and propose a novel and efﬁcient bandit algorithm based
on the LASSO estimator.

Brain and behavior modeling. Drawing an inspira-
tion from behavioral studies of human decision making
in both healthy controls and patients with different men-
tal disorders, authors in [Bouneffouf et al., 2017a] pro-
pose a general parametric framework for multi-armed

bandit problem which extends the standard Thompson
Sampling approach to incorporate reward processing bi-
ases associated with several neurological and psychiatric
conditions, including Parkinson’s and Alzheimer’s dis-
eases, attention-deﬁcit/hyperactivity disorder (ADHD),
addiction, and chronic pain. They demonstrate empir-
ically, from the behavioral modeling perspective, that
their parametric framework can be viewed as a ﬁrst step
towards a unifying computational model capturing re-
ward processing abnormalities across multiple mental
conditions.

2.2 Finance
In recent years, sequential portfolio selection has been a
focus of increasing interest at the intersection of the ma-
chine learning and quantitative ﬁnance. The trade-off be-
tween exploration and exploitation, with the goal of max-
imizing cumulative reward, is a natural formulation of
the portfolio choice problems. In [Shen et al., 2015], the
authors proposed a bandit algorithm for making online
portfolio choices via exploiting correlations among mul-
tiple arms. By constructing orthogonal portfolios from
multiple assets and integrating their approach with the
upper-conﬁdence-bound bandit framework, the authors
derive the optimal portfolio strategy representing a com-
bination of passive and active investments according to
a risk-adjusted reward function. In [Huo and Fu, 2017],
the authors incorporate risk-awareness into the classic
multi-armed bandit setting and introduce a novel algo-
rithm for portfolio construction. Through ﬁltering as-
sets based on the topological structure of ﬁnancial mar-
ket and combining the optimal multi-armed bandit policy
with the minimization of a coherent risk measure, they
achieve a balance between risk and return.

2.3 Dynamic Pricing
Online retailer companies are often faced with the dy-
namic pricing problem:
the company must decide on
real-time prices for each of its multiple products. The
company can run price experiments (make frequent price
changes) to learn about demand and maximize long-run
proﬁts. The authors in [Misra et al., 2018] propose a dy-
namic price experimentation policy, where the company
has only incomplete demand information. For this gen-
eral setting, authors derive a pricing algorithm that bal-
learning for fu-
ances earning an immediate proﬁt vs.
ture proﬁts. The approach combines multi-armed ban-
dit with partial identiﬁcation of consumer demand from
economic theory. Similar to [Misra et al., 2018], au-
thors in [Mueller et al., 2018] consider high-dimensional
dynamic multi-product pricing with an evolving low-
dimensional linear demand model. They show that the
revenue maximization problem reduces to an online ban-
dit convex optimization with side information given by
the observed demands. The approach applies a ban-
dit convex optimization algorithm in a projected low-

2

dimensional space spanned by the latent product fea-
tures, while simultaneously learning this span via online
singular value decomposition of a carefully-crafted ma-
trix containing the observed demands.

2.4 Recommender Systems
Recommender systems are frequently used in various ap-
plication to predict user preferences. However, they also
face the exploration-exploitation dilemma when mak-
ing a recommendation, since they need to exploit their
knowledge about the previously chosen items the user
is interested in, while also exploring new items the
user may like. Authors in [Zhou et al., 2017] approach
this challenge using multi-armed bandit setting, espe-
cially for large-scale recommender systems that have re-
ally large or inﬁnite number of items. They propose
two large-scale bandit approaches in situations when
no prior information is available. Continuous explo-
ration in their approaches can address the cold start prob-
lem in recommender systems. In context-aware recom-
mender systems, most existing approaches focus on rec-
ommending relevant items to users, taking into account
contextual information, such as time, location, or so-
cial aspects. However, none of those approaches has
considered the problem of users content evolution.
In
[Bouneffouf et al., 2012] authors introduce an algorithm
that takes this dynamics into account. It is based on dy-
namic exploration/exploitation and can adaptively bal-
ance the two aspects, deciding which situation is most
relevant for exploration or exploitation.
In this sense,
[Bouneffouf, 2014] propose to study the ”freshness” of
the user’s content through the bandit problem. They
introduce in this paper an algorithm named Freshness-
Aware Thompson Sampling that manages the recom-
mendation of fresh document according to the user’s risk
of the situation.

Inﬂuence Maximization

2.5
Autors in [Vaswani et al., 2017] consider inﬂuence max-
imization (IM) in social networks, which is the problem
of maximizing the number of users that become aware of
a product by selecting a set of seed users to expose the
product to. They propose a novel parametrization that
not only makes the framework agnostic to the underlying
diffusion model, but also statistically efﬁcient to learn
from data. They give a corresponding monotone, sub-
modular surrogate function, and show that it is a good
approximation to the original IM objective. They also
consider the case of a new marketer looking to exploit an
existing social network, while simultaneously learning
the factors governing information propagation. For this,
they develop a LinUCB-based bandit algorithm. Authors
in [Wen et al., 2017] also study the online inﬂuence max-
imization problem in social networks but under the inde-
pendent cascade model. Speciﬁcally, they try to learn the
set of best seeds or inﬂuencers in a social network online

while repeatedly interacting with it. They address the
challenges of combinatorial action space, since the num-
ber of feasible inﬂuencer sets grows exponentially with
the maximum number of inﬂuencers, and limited feed-
back, since only the inﬂuenced portion of the network is
observed. They propose and analyze IMLinUCB, a com-
putationally efﬁcient UCB-based algorithm.

Information Retrieval

2.6
Authors in [Losada et al., 2017] argue that Informa-
tion Retrieval iterative selection process can be natu-
rally modeled as a contextual bandit problem. Cast-
ing document judging as a multi-armed bandit problem
leads to highly effective adjudication methods. Under
this bandit allocation framework, they consider station-
ary and non-stationary models and propose seven new
document adjudication methods (ﬁve stationary meth-
ods and two non-stationary variants). This comparative
study includes existing methods designed for pooling-
based evaluation and existing methods designed for
metasearch.
In mobile information retrieval, authors
in [Bouneffouf et al., 2013] introduce an algorithm that
tackles this dilemma in Context-Based Information Re-
It is based on dynamic explo-
trieval (CBIR) area.
ration/exploitation and can adaptively balance the two
aspects by deciding which users situation is most relevant
for exploration or exploitation. Within a deliberately de-
signed online framework they conduct evaluations with
mobile users.

2.7 Dialogue Systems
Dialogue response selection. Dialogue response selec-
tion is an important step towards natural response gen-
eration in conversational agents. Existing work on con-
versational models mainly focuses on ofﬂine supervised
learning using a large set of context-response pairs. In
[Liu et al., 2018] authors focus on online learning of re-
sponse selection in dialog systems. They propose a con-
textual multi-armed bandit model with a nonlinear re-
ward function that uses distributed representation of text
for online response selection. A bidirectional LSTM is
used to produce the distributed representations of dialog
context and responses, which serve as the input to a con-
textual bandit. They propose a customized Thompson
sampling method that is applied to a polynomial feature
space in approximating the reward.

Pro-activity dialogue systems. An objective of pro-
activity in dialogue systems is to enhance the usabil-
ity of conversational agents by enabling them to initi-
ate conversation on their own. While dialogue systems
have become increasingly popular during the last cou-
ple of years, current task-oriented dialogue systems are
still mainly reactive, as users tend to initiate conversa-
tions. Authors of [Silander and others, 2018] propose to
introduce the paradigm of contextual bandits as frame-
work for proactive dialog systems. Contextual bandits

3

have been the model of choice for the problem of reward
maximization with partial feedback since they ﬁt well
to the task description, they also explore the notion of
memory into this paradigm, where they propose two dif-
ferentiable memory models that act as parts of the para-
metric reward estimation function. The ﬁrst one, Con-
volutional Selective Memory Networks, uses a selection
of past interactions as part of the decision support. The
second model, called Contextual Attentive Memory Net-
work, implements a differentiable attention mechanism
over the past interactions of the agent. The goal is to gen-
eralize the classic model of contextual bandits to settings
where temporal information needs to be incorporated and
leveraged in a learnable manner.

Multi-domain dialogue systems. Building multi-
domain dialogue agents is a challenging task and an open
problem in modern AI. Within the domain of dialogue,
the ability to orchestrate multiple independently trained
dialog agents, or skills, to create a uniﬁed system is of
In [Upadhyay et al., 2018], the
particular signiﬁcance.
authors study the task of online posterior dialogue or-
chestration, where they deﬁne posterior orchestration as
the task of selecting a subset of skills which most ap-
propriately answers a user input using features extracted
from both the user input and the individual skills. To
account for the various costs associated with extracting
skill features, they consider online posterior orchestra-
tion under a skill execution budget. This setting is for-
malized as Context-Attentive Bandit with Observations,
a variant of context-attentive bandits, and evaluate it on
simulated non-conversational and proprietary conversa-
tional datasets.

2.8 Anomaly Detection

Performing anomaly detection on attributed networks
concerns with ﬁnding nodes whose behaviors deviate
signiﬁcantly from the majority of nodes. Authors in
[Ding et al., 2019] investigate the problem of anomaly
detection in an interactive setting by allowing the sys-
tem to proactively communicate with the human expert
in making a limited number of queries about ground
truth anomalies. Their objective is to maximize the
true anomalies presented to the human expert after a
given budget is used up. Along with this line, they
formulate the problem through the principled multi-
armed bandit framework and develop a novel collabo-
rative contextual bandit algorithm, that explicitly mod-
els the nodal attributes and node dependencies seam-
lessly in a joint framework, and handles the exploration-
exploitation dilemma when querying anomalies of dif-
ferent types. Credit card transactions predicted to be
fraudulent by automated detection systems are typically
handed over to human experts for veriﬁcation. To limit
costs,
it is standard practice to select only the most
suspicious transactions for investigation. Authors in
[Soemers et al., 2018] claim that a trade-off between ex-

ploration and exploitation is imperative to enable adap-
tation to changes in behavior. Exploration consists of
the selection and investigation of transactions with the
purpose of improving predictive models, and exploita-
tion consists of investigating transactions detected to be
suspicious. Modeling the detection of fraudulent trans-
actions as rewarding, they use an incremental regression
tree learner to create clusters of transactions with simi-
lar expected rewards. This enables the use of a contex-
tual multi-armed bandit (CMAB) algorithm to provide
the exploration/exploitation trade-off.

2.9 Telecommunication
In [Boldrini et al., 2018], a multi-armed bandit model
was used to describe the problem of best wireless net-
work selection by a multi-Radio Access Technology
(multi-RAT) device, with the goal of maximizing the
quality perceived by the ﬁnal user. The proposed model
extends the classical MAB model in a twofold manner.
First, it foresees two different actions: to measure and
to use; second, it allows actions to span over multiple
time steps. Two new algorithms designed to take advan-
tage of the higher ﬂexibility provided by the muMAB
model are also introduced. The ﬁrst one, referred to
as measure-use-UCB1 is derived from the UCB1 algo-
rithm, while the second one, referred to as Measure with
Logarithmic Interval, is appositely designed for the new
model so to take advantage of the new measure action,
while aggressively using the best arm. The authors in
[Kerkouche et al., 2018] demonstrate the possibility to
optimize the performance of the Long Range Wide Area
Network technology. Authors suggest that nodes use
multi-armed bandit algorithms, to select the communica-
tion parameters (spreading factor and emission power).
Evaluations show that such learning methods allow to
manage the trade-off between energy consumption and
packet loss much better than an Adaptive Data Rate algo-
rithm adapting spreading factors and transmission pow-
ers on the basis of Signal to Interference and Noise Ratio
values.

2.10 Bandit in Real-Life Applications:
Summary and Future Directions

Table 1: Bandit for Real Life Application
Non-
Non-
stationary
stationary
CMAB
MAB

CMAB

MAB

Healthcare
Finance
Dynamic pricing
Recommendr system
Maximization
Dialogue system
Telecomunication
Anomaly detection

√
√

√
√ √
√

√
√

√

√

√

√

Table 1 provides a summary of bandit problem for-

4

mulations used in each of the above domain applica-
tions. We see that, for example, non-stationary bandit
was not used in healthcare applications, since perhaps
there was no signiﬁcant change assumed to happen in
the environment in the process of making the treatment
decision, i.e. no transition in the state of the the patient;
such transition, if it occurred, would be better modeled
using reinforcement learning rather than non-stationary
bandit. There are clearly other domains where the non-
stationary bandit is a more appropriate setting, but it
looks like this setting was not yet much investigated in
healthcare domain. For example, anomaly detection, is
a domain where non-stationary contextual bandit could
be used, since in this setting the anomaly could be adver-
sarial, which means that any bandit applied to this set-
ting should have some kind of drift condition, in-order to
adapt to new type of attack. Another observation is that
none of the existing work tried to develop an algorithm
that could solve these different tasks at the same time, or
apply the knowledge obtained in one domain to another
domain, thus opening a direction of research on multi-
task and transfer learning in bandit setting. Furthermore,
given an online nature of bandit problem, continuous, or
lifelong learning would be a natural next step, adapting
the model learned in the previous tasks to the new one,
while still remembering how to perform earlier task, thus
avoiding the problem of ”catastrophic forgetting”.

3 Bandit for Better Machine Learning
In this section we are describing how bandit algorithms
could be used to improve other algorithms, e.g. various
machine-learning techniques.

3.1 Algorithm Selection
Algorithm selection is typically based on models of al-
gorithm performance, learned during a separate ofﬂine
training sequence, which can be prohibitively expen-
sive. In recent work, they adopted an online approach,
in which a performance model is iteratively updated and
used to guide selection on a sequence of problem in-
stances. The resulting exploration-exploitation trade-off
was represented as a bandit problem with expert ad-
vice, using an existing solver for this game, but this re-
quired using an arbitrary bound on algorithm runtimes,
thus invalidating the optimal regret of the solver.
In
[Gagliolo and Schmidhuber, 2010], a simpler framework
was proposed for representing algorithm selection as a
bandit problem, using partial information and an un-
known bound on losses.

3.2 Hyperparameter Optimization
Performance of machine learning algorithms depends
critically on identifying a good set of hyperparame-
ters. While recent approaches use Bayesian optimization
to adaptively select optimal hyperparameter conﬁgura-
tions, they rather focus on speeding up random search

through adaptive resource allocation and early-stopping.
[Li et al., 2016] formulated hyperparameter optimiza-
tion as a pure-exploration non-stochastic inﬁnite-armed
bandit problem where a predeﬁned resources, such as it-
erations, data samples, or features are allocated to ran-
domly sampled conﬁgurations. This work introduced a
novel algorithm, Hyperband, for this framework and an-
alyze its theoretical properties, providing several desir-
able guarantees. Furthermore, Hyperband wascmpared
with popular Bayesian optimization methods on a suite
of hyperparameter optimization problems;
it was ob-
served that Hyperband can provide more than an order-
of-magnitude speedup over its competitors on a variety
of deep-learning and kernel-based learning problems.

3.3 Feature Selection

In a classical online supervised learning the true label of
a sample is always revealed to the classiﬁer, unlike in a
bandit setting were any wrong classiﬁcation resuls into
zero reward, and only the single correct classiﬁcation
yields reward 1. The authors of [Wang et al., 2014] in-
vestigate the problem of Online Feature Selection, where
the aim is to make accurate predictions using only a
small number of active features using epsilon greedy
algorithm. The authors of [Bouneffouf et al., 2017b]
tackle the online feature selection problem by addressing
the combinatorial optimization problem in the stochastic
bandit setting with bandit feedback, utilizing the Thomp-
son Sampling algorithm.

3.4 Bandit for Active Learning

Labelling all training examples in supervised classiﬁca-
tion setting can be costly. Active learning strategies solve
this problem by selecting the most useful unlabelled ex-
amples to obtain the label for, and to train a predictive
model. The choice of examples to label can be seen
as a dilemma between the exploration and the exploita-
tion over the input space. In [Bouneffouf et al., 2014], a
novel active learning strategy manages this compromise
by modelling the active learning problem as a contex-
tual bandit problem. they propose a sequential algorithm
named Active Thompson Sampling (ATS), which, in
each round, assigns a sampling distribution on the pool,
samples one point from this distribution, and queries
the oracle for this sample point label. The authors of
[Ganti and Gray, 2013] also propose a multi-armed ban-
dit inspired, pool-based active learning algorithm for the
problem of binary classiﬁcation. They utilize ideas such
as lower conﬁdence bounds, and self-concordant regular-
ization from the multi-armed bandit literature to design
their proposed algorithm. In each round, the proposed
algorithm assigns a sampling distribution on the pool,
samples one point from this distribution, and queries the
oracle for the label of this sampled point.

5

3.5 Clustering

[Sublime and Lefebvre, 2018] considers collaborative
clustering, which is machine-learning paradigm con-
cerned with the unsupervised analysis of complex multi-
view data using several algorithms working together.
Well-known applications of collaborative clustering in-
clude multiview clustering and distributed data cluster-
ing, where several algorithms exchange information in
order to mutually improve each others. One of the key
issue with multi-view and collaborative clustering is to
assess which collaborations are going to be beneﬁcial or
detrimental. Many solutions have been proposed for this
problem, and all of them conclude that, unless two mod-
els are very close, it is difﬁcult to predict in advance the
result of a collaboration. To address this problem, the
authors of [Sublime and Lefebvre, 2018] propose a col-
laborative peer to peer clustering algorithm based on the
principle of non stochastic multi-arm bandits to assess
in real time which algorithms or views can bring useful
information.

3.6 Reinforcement learning

Autonomous cyber-physical systems play a large role in
our lives. To ensure that agents behave in ways aligned
with the values of the societies in which they operate,
we must develop techniques that allow these agents to
not only maximize their reward in an environment, but
also to learn and follow the implicit constraints assumed
by the society. In [Noothigattu et al., 2018], the authors
study a setting where an agent can observe traces of be-
havior of members of the society but has no access to
the explicit set of constraints that give rise to the ob-
served behavior. Instead, inverse reinforcement learning
is used to learn such constraints, that are then combined
with a possibly orthogonal value function through the
use of a contextual bandit-based orchestrator that picks a
contextually-appropriate choice between the two policies
(constraint-based and environment reward-based) when
taking actions. The contextual bandit orchestrator al-
lows the agent to mix policies in novel ways, taking the
best actions from either a reward maximizing or con-
strained policy. The [Laroche and F´eraud, 2017] tackles
the problem of online RL algorithm selection. A meta-
algorithm is given for input a portfolio constituted of sev-
eral off-policy RL algorithms. It then determines at the
beginning of each new trajectory, which algorithm in the
portfolio is in control of the behaviour during the next
trajectory, in order to maximise the return. A novel meta-
algorithm, called Epochal Stochastic Bandit Algorithm
Selection. Its principle is to freeze the policy updates at
each epoch, and to leave a rebooted stochastic bandit in
charge of the algorithm selection.

3.7 Bandit for Machine Learning:

Table 2: Bandit in Machine Learning

Algorithm Slection
Parameter Optimization
Features Selection
Active Learning
Clustering
Reinforcement learning

MAB

Non-
stationary
MAB
√

CMAB

Non-
stationary
CMAB

√
√ √
√
√
√ √

√

√

Summary and Future Directions

Table 2 summarizes the types of bandit problems used to
solve the machine-learning problems mentioned above.
We see, for example, that contextual bandit was not used
in feature selection or hyperparameter optimization. This
observation could point into a direction for future work,
where side information could be employed in feature se-
lection. Also, non-stationary bandit was rarely consid-
ered in these problem settings, which is also suggest-
ing possible extensions of current work. For instance,
the non-stationary contextual bandit could be useful in
the non-stationary feature selection setting, where ﬁnd-
ing the right features is time-dependent and context-
dependent when the environment keeps changing. Our
main observation is also that each technique is solving
just one machine learning problem at a time; thus, the
question is whether a bandit setting and algoritms can
be developed to solve multiple machine learning prob-
lems simultaneously, and whether transfer and continual
learning can be achieved in this setting. One solution
could be to model all these problems in a combinatorial
bandit framework, where the bandit algorithm would ﬁnd
the optimal solution for each problem at each iteration;
thus, combinatorial bandit could be further used as a tool
for advancing automated machine learning.

4 Conclusions

In this article, we reviewed some of the most notable re-
cent work on applications of multi-armed bandit and con-
textual bandit, both in real-life domains and in automated
machine learning. We summarized, in an organized way
(Tables 1 and 2), various existing applications, by types
of bandit settings used, and discussed the advantages of
using bandit techniques in each domain. We brieﬂy out-
lines of several important open problems and promising
future extensions.

In summary, the bandit framework, including both
multi-arm and contextual bandit, is currently very ac-
tive and promising research areas, and there are multiple
novel techniques and applications emerging each year.
We hope our survey can help the reader better under-
stand some key aspects of this exciting ﬁeld and get a
better perspective on its notable advancements and future
promises.

6

References
[Agrawal and Goyal, 2012] Shipra Agrawal and Navin
Goyal. Analysis of thompson sampling for the multi-
In COLT 2012 - The 25th
armed bandit problem.
Annual Conference on Learning Theory, June 25-27,
2012, Edinburgh, Scotland, pages 39.1–39.26, 2012.
[Agrawal and Goyal, 2013] Shipra Agrawal and Navin
Goyal. Thompson sampling for contextual bandits
In ICML (3), pages 127–135,
with linear payoffs.
2013.

[Allesiardo et al., 2014] Robin Allesiardo, Rapha¨el
F´eraud, and Djallel Bouneffouf. A neural networks
committee for the contextual bandit problem.
In
Neural Information Processing - 21st International
Conference,
ICONIP 2014, Kuching, Malaysia,
November 3-6, 2014. Proceedings, Part I, pages
374–381, 2014.

[Auer et al., 2002] Peter Auer, Nicol`o Cesa-Bianchi,
and Paul Fischer. Finite-time analysis of the mul-
tiarmed bandit problem. Machine Learning, 47(2-
3):235–256, 2002.

[Bastani and Bayati, 2015] Hamsa

Mohsen Bayati.
high-dimensional covariates.
2661896, 2015.

Bastani

and
Online decision-making with
Available at SSRN

[Boldrini et al., 2018] Stefano

Luca
De Nardis, Giuseppe Caso, Mai Le,
Jocelyn
Fiorina, and Maria-Gabriella Di Benedetto. mumab:
A multi-armed bandit model for wireless network
selection. Algorithms, 11(2):13, 2018.

Boldrini,

[Bouneffouf and F´eraud, 2016] Djallel Bouneffouf and
Rapha¨el F´eraud. Multi-armed bandit problem with
known trend. Neurocomputing, 205:16–21, 2016.
[Bouneffouf et al., 2012] Djallel Bouneffouf, Amel
Bouzeghoub, and Alda Lopes Ganc¸arski.
A
contextual-bandit algorithm for mobile context-aware
In International Conference
recommender system.
on Neural Information Processing, pages 324–331.
Springer, 2012.

[Bouneffouf et al., 2013] Djallel Bouneffouf, Amel
Bouzeghoub, and Alda Lopes Ganc¸arski. Contextual
bandits for context-based information retrieval.
In
Information
International Conference on Neural
Processing, pages 35–42. Springer, 2013.

[Bouneffouf et al., 2014] Djallel Bouneffouf, Romain
Laroche, Tanguy Urvoy, Raphael F´eraud, and Robin
Allesiardo. Contextual bandit for active learning: Ac-
tive thompson sampling. In International Conference
on Neural Information Processing, pages 405–412.
Springer, 2014.

[Bouneffouf et al., 2017a] Djallel Bouneffouf,

Rish, and Guillermo A Cecchi.

Irina
Bandit models

of human behavior: Reward processing in mental
disorders. In AGI, pages 237–248. Springer, 2017.

[Bouneffouf et al., 2017b] Djallel Bouneffouf,

Irina
Rish, Guillermo A. Cecchi, and Rapha¨el F´eraud.
Context attentive bandits: Contextual bandit with
In IJCAI 2017, Melbourne,
restricted context.
Australia, August 19-25, 2017, pages 1468–1475,
2017.

[Bouneffouf, 2014] Djallel Bouneffouf.

Freshness-
aware thompson sampling. In International Confer-
ence on Neural Information Processing, pages 373–
380. Springer, 2014.

[Ding et al., 2019] Kaize Ding, Jundong Li, and Huan
Liu. Interactive anomaly detection on attributed net-
works. In Proceedings of the Twelfth ACM Interna-
tional Conference on Web Search and Data Mining,
WSDM ’19, pages 357–365, New York, NY, USA,
2019. ACM.

[Durand et al., 2018] Audrey Durand, Charis Achilleos,
Demetris Iacovides, Katerina Strati, Georgios D Mit-
sis, and Joelle Pineau. Contextual bandits for adapting
treatment in a mouse model of de novo carcinogene-
sis. In Machine Learning for Healthcare Conference,
pages 67–82, 2018.

[Gagliolo and Schmidhuber, 2010] Matteo Gagliolo and
J¨urgen Schmidhuber. Algorithm selection as a bandit
problem with unbounded losses. In Learning and In-
telligent Optimization, 4th International Conference,
LION 4, Venice, Italy, January 18-22, 2010. Selected
Papers, pages 82–96, 2010.

[Ganti and Gray, 2013] Ravi Ganti and Alexander G
Gray. Building bridges: Viewing active learning
arXiv preprint
from the multi-armed bandit lens.
arXiv:1309.6830, 2013.

[Huo and Fu, 2017] Xiaoguang Huo and Feng Fu. Risk-
aware multi-armed bandit problem with application
to portfolio selection. Royal Society open science,
4(11):171377, 2017.

[Kerkouche et al., 2018] Raouf

Kerkouche,

R´eda
Alami, Rapha¨el F´eraud, Nad`ege Varsier, and Patrick
Maill´e. Node-based optimization of lora transmis-
In ICT
sions with multi-armed bandit algorithms.
2018, Saint Malo, France, June 26-28, 2018, pages
521–526, 2018.

[Lai and Robbins, 1985] T. L. Lai and Herbert Robbins.
Asymptotically efﬁcient adaptive allocation rules. Ad-
vances in Applied Mathematics, 6(1):4–22, 1985.
[Langford and Zhang, 2008] John Langford and Tong
Zhang. The epoch-greedy algorithm for multi-armed
In Advances in neu-
bandits with side information.
ral information processing systems, pages 817–824,
2008.

7

Adapting to concept drift in credit card transaction
data streams using contextual bandits and decision
trees. In AAAI, 2018.

[Sublime and Lefebvre, 2018] J´er´emie Sublime

and
Sylvain Lefebvre. Collaborative clustering through
constrained networks using bandit optimization.
In 2018 International Joint Conference on Neural
Networks, IJCNN 2018, Rio de Janeiro, Brazil, July
8-13, 2018, pages 1–8, 2018.

[Upadhyay et al., 2018] Sohini Upadhyay, Mayank
Agarwal, Djallel Bounneffouf,
and Yasaman
Khazaeni. A bandit approach to posterior dialog
orchestration under a budget. 2018.

[Vaswani et al., 2017] Sharan Vaswani, Branislav Kve-
ton, Zheng Wen, Mohammad Ghavamzadeh, Laks VS
Lakshmanan, and Mark Schmidt. Model-independent
online learning for inﬂuence maximization. In Pro-
ceedings of the 34th International Conference on Ma-
chine Learning-Volume 70, pages 3530–3539. JMLR.
org, 2017.

[Wang et al., 2014] Jialei Wang, Peilin Zhao, Steven CH
Hoi, and Rong Jin. Online feature selection and its
applications. IEEE Transactions on Knowledge and
Data Engineering, 26(3):698–710, 2014.

[Wen et al., 2017] Zheng Wen, Branislav Kveton,
Michal Valko, and Sharan Vaswani. Online inﬂuence
independent cascade model
maximization under
In Advances in neural
with semi-bandit feedback.
information processing systems, pages 3022–3032,
2017.

[Zhou et al., 2017] Qian Zhou, XiaoFang Zhang, Jin
Xu, and Bin Liang. Large-scale bandit approaches
In International Confer-
for recommender systems.
ence on Neural Information Processing, pages 811–
821. Springer, 2017.

[Laroche and F´eraud, 2017] Romain

Rapha¨el F´eraud.
policy reinforcement learning algorithm.
abs/1701.08810, 2017.

Laroche

and
Algorithm selection of off-
CoRR,

[Li et al., 2010] Lihong Li, Wei Chu, John Langford,
and Robert E. Schapire. A contextual-bandit approach
to personalized news article recommendation. CoRR,
2010.

[Li et al., 2016] Lisha Li, Kevin Jamieson, Giulia
DeSalvo, Afshin Rostamizadeh, and Ameet Tal-
walkar. Hyperband: A novel bandit-based approach
arXiv preprint
to hyperparameter optimization.
arXiv:1603.06560, 2016.

[Liu et al., 2018] Bing Liu, Tong Yu, Ian Lane, and
Ole J. Mengshoel. Customized nonlinear bandits for
online response selection in neural conversation mod-
els. In AAAI, 2018, pages 5245–5252, 2018.

[Losada et al., 2017] David E Losada, Javier Parapar,
and Alvaro Barreiro. Multi-armed bandits for adju-
dicating documents in pooling-based evaluation of in-
formation retrieval systems. Information Processing
& Management, 53(5):1005–1025, 2017.

[Mary et al., 2015] J´er´emie Mary, Romaric Gaudel, and
Philippe Preux. Bandits and recommender systems. In
Machine Learning, Optimization, and Big Data - First
International Workshop, MOD 2015, pages 325–336,
2015.

[Misra et al., 2018] Kanishka Misra, Eric M Schwartz,
and Jacob Abernethy. Dynamic online pricing with
incomplete information using multi-armed bandit ex-
periments. 2018.

[Mueller et al., 2018] Jonas Mueller, Vasilis Syrgkanis,
Low-rank bandit methods for
arXiv preprint

and Matt Taddy.
high-dimensional dynamic pricing.
arXiv:1801.10242, 2018.

[Noothigattu et al., 2018] Ritesh Noothigattu, Djallel
Bouneffouf, Nicholas Mattei, Rachita Chandra,
Piyush Madan, Kush Varshney, Murray Campbell,
Moninder Singh, and Francesca Rossi. Interpretable
multi-objective reinforcement learning through pol-
icy orchestration. arXiv preprint arXiv:1809.08343,
2018.

[Shen et al., 2015] Weiwei Shen, Jun Wang, Yu-Gang
Jiang, and Hongyuan Zha. Portfolio choices with
In Twenty-Fourth Inter-
orthogonal bandit learning.
national Joint Conference on Artiﬁcial Intelligence,
2015.

[Silander and others, 2018] Tomi Silander et al. Contex-
tual memory bandit for pro-active dialog engagement.
2018.

[Soemers et al., 2018] Dennis JNJ Soemers, Tim Brys,
Kurt Driessens, Mark HM Winands, and Ann Now´e.

8

