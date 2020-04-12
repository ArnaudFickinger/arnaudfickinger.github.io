---
title: "Gibbard's Theorem and Inverse Reinforcement Learning"
date: 2020-04-04
permalink: /posts/2020/04/gibbard-theorem-and-irl/
tags:
  - research
---


# Abstract

> Can we call it IRL for social robots? Or artificial social choice theory, or social choice theory for robots, then 2 parts: strategy-proofness of IRL, fairness of multi agent systems (a paper already talk avbout the fact that ressouce are usually given to the most performant)

In this post I will show that when an IRL system aggregates demonstrations from multiple humans, the best response trajectory for a self-interested human
is not the expert trajectory. 

# Motivation
* Most machine Learning algorithm are built with the assumption that the distribution of the data won't change
between training and execution. Recently efficient meta learning have been built to enable an efficient work on out-of-distibution
data, but the tasks remain similar. When we think about humans, it's hard to think about any stationary distribution. Each human has
his unique preferences, beliefs and decision-maker mechanism, and each human is repeatedly evolving. Moreover human are decision-maker 
and will change their behavior in presence of a robot. It's necessary to think about multi-agent methods when
treating human data: 

* Rethink MA(I)RL for social... Firstly IRL is manipulable, then MARL no fair. Human Compatible IRL/RL.

> Look at literature about social robots

Social choice theory is the branch of Economics modeling and analyzing collective decision-making
from the perspective of aggregating individual preferences. For example it is concerned with the 
design of fair voting systems. It is closely related to mechanism design, a branch of Game Theory
that is concerned with designing games where strategic players are incentivized to act truthfully. 
An important theorem lying at the intersection of both disciplines is the following: *any non-dictatorial
voting scheme with at least three possible outcomes is subject to individual manipulation*. In other words,
knowing the preferences of the others and adapting yours in consequence might change the outcome
in your advantage. 

In Inverse Reinforcement Learning, preferences are not shared directly to the system. Instead, the 
system observes a states-actions trajectory and compute a reward function such that the observed trajectory 
would have been produced by an optimal policy under that reward. For complex tasks, a lot of trajectories are 
aggregated in order to compute a good estimate of the reward function. Yet it is always assumed that the 
trajectories can be explained by the same reward function. In light of the issue in social 
choice theory discussed above, the question we want to answer is: *if an IRL system aims to compute the collective
preferences of two individuals by aggregating their two trajectories, does the expert trajectory remain the best response
of each individual?*


# Meeting with tom (10-11)

## Manifesto for Multi-Agent Inverse Reinforcement Learning: Why should we avoid Inverse Reinforcement Learning to understand human values?

* Game: how does the payoffs and competition change when the robot is present? How does it perturbe the behavior of both humans? Theory+Experiment

* Besides alleviating reward engineering, a longer term and more conceptual purpose of Inverse Reinforcement Learning 
is to learn about human values. The idea is that it's hard for a human to quantify their values and preferences, and IRL propose to 
learn this by itself by observing their behaviors. Yet a possible loophole is that it assumes that the observed behavior truthfully express 
the values and preferences. Thinking about manipulation voting [OTHER EXAMLE], it appear as a big assumption. 

* Utilitarism states that the best action is the one that create the greatest happiness
in the greatest number of [people](https://arxiv.org/pdf/2001.09768v1.pdf). Thus a utilitarian robot aacting
for a group of people would maximize the sum of their utilities. At first sight it sounds
like an appealing objective to motivates fair actions. Yet we can think about asymetric level of expertise.
aims to maximize global utility and appears as a fair choice. But if one human is less good as expresing 
himself, then the robot would optimize for the other [BE MORE CLEAR]

* Let's think of single-agent Inverse Reinforcement Learning. The technical purpose of IRL is that
engineering reward is hard and observing an expert to deduce a reward or a policy is easier in some cases. 
A famous example is the success of training autonomous helicopter threw [apprenticeship learning](http://www.robotics.stanford.edu/~ang/papers/ijrr10-HelicopterAerobatics.pdf).
The conceptual purpose of IRL is that for less obvious tasks, it's hard for a human to define what he wants
in terms of reward function. This problem is also studied in Economics since the problem is that human have 
hard time to externalize their preference. So instead of asking them what they want in terms of utility function or
reward function, we observe them and deduce what they want. The problem of observing a human, that is not present 
when observing an helicopter, is that his behavior does not only reflect his internal preference but also the
norms of the world he is living in. When we study a driver in isolation, we might think that the sense of the road is part of
its preference while he is just following norms (NOT A GOOD EXAMPLE, BETTER ONE?). In the contrary, when studying several humans, we might
understand that driving in the road is a game with a dual equilibrium due to a coordination problem, and 
the humans are indifferent to the sense of the road provided that they reach one of the two equilibria. 
Studying humans inside their community will enable to understand in what kind of equilibria they are in, and distinguish
their true preferences from the external influence. 

* Single Agent IRL 

* Let's think about a system that would use IRL on trajectories from multiple humans. Is it strategyproof? If now we see the 
system as part of the game, can we see emerge behaviors that would incentivize the humans to act truthfully? We can see second bid auction
as 

* Let's think about a robot inside a community of humans that would have to maximize a the utilitarian aggregation of reward,
would he end up helping the least advantaged? Maximin? Can we think of a way to understand the signal?

* An implementation of Multi Agent IRL 



* I had a very exiting meeting with Tom. He introduced me to the problem of norm. The question is does we want AI to be purely
descriptive or does we want AI to have a part of norms. Putting a norm in the AI has always a risk to make it biased. The question 
is is there a way to learn the norm? Paradoxaly, can we use a descriptive or positive approach to learn the norm? This sounds impossible
for a human because the norm is the description of all the global and he would have to extract himself to learn the norm. On a other side, we can look
back at the time and see that what they defined as a norm in the middle age is define as saddistic and marginal now. The only way to define a norm
is to have a system that extract itself of the world and learn the norm by observing the behavior. 
We can define a norm as what enable people to reach a Paretto-efficient equilibria rather than a Nash equilibria, but we still need to identify the game.
There is some methos in multi=agent inverse reinfordemtn learning that 

* We need to distinguish two types of norm: norms emerging due to the presence of coordination problem, and norm
emerging due to the presence of Pareto efficient equilibria that are not Nash equilibria. For the former case, we can think 
of languages or the sense of the road. Since in coordianation games, the Nash equilibria is condiionned by coordinated behaviors, in this case acceptance norms are reached 
naturally by self-interested agents. In the later case, we can think (look at mechanism design litterature). 


* Problem of self awareness: do we prefer to put water in India or 

* Mechanism Design: What enable Vickrey to defeat Gibbard? 

* Strategy-Proofness of IRL: Does Car should have norms? 

* Discover norm threw multi-agent IRL

* Assistance Game and Mechanism Design: discovering what enable Vickrey to alleviate Gibbard. They say constraint of utilities,
can we see that as norms? Norms make people think

# Theory

Our goal is to demonstrate that kind of result:
> The best response trajectory to a IRL system depend on the other human's trajectories. Thus an IRL mechanism is not 
> strategy-proof.

A way to prove it would be to reduce IRL to a voting mechanism, by first starting with a MAB. Another way would be to generalize Gibbard to 
utilities and then reduce IRL to cardinal utilities on features. Or we can look for results in mechanism design and see IRL as a game. 

Firstly let's formalize inverse reinforcement learning in the lense 


# Experiment

## Practical Manipulation of Inverse Reinforcement Learning

But in any case, it's useful to understand what MaxEnt IRL do in the case where features are available: given a trajectory $(s_1,a_1,...,a_{T-1},s_T)$, 
the only thing that the IRL system keep is the empirical feature count $\sum_{t=1}^{T} \phi(\tilde{s}_t)$ and the empirical initial state distribution $\rho_0$. The 
objective is:

$$ \omega^* = \max_{\omega} P(\tilde{\tau}|\omega,\rho_0) \\
P(\tilde{\tau}|\omega,\rho_0) = \frac{e^{\sum_{t=1}^{T}\phi(s_t)^T\omega}}{Z(\omega, \rho_0)} \\
Z(\omega, \rho_0) = \sum_{\tau, s_0 \sim \rho_0} e^{\sum_{t=1}^{T}\phi(s^{\tau}_t)^T\omega}$$

Assuming we have two independent trajectories, we can write the log-likelihood as:

$$L(\omega) = \sum_{i=1}^{2} \sum_{t=1}^{T}\phi(s^i_t)^T\omega - 2 \log \sum_{\tau, s_0 \sim \rho_0} e^{\sum_{t=1}^{T}\phi(s^{\tau}_t)^T\omega}$$

The Log-Sum-Exp term is convex, so our objective is convex (we maximize a linear and a concave function). Let's compute the gradient:

$$\nabla_{\omega} L(\omega) = \sum_{i=1}^{2} \sum_{t=1}^{T}\phi(s^i_t) - 2 \frac{\sum_{\tau, s_0 \sim \rho_0} e^{\sum_{t=1}^{T}\phi(s^{\tau}_t)^T\omega} \sum_{t=1}^{T}\phi(s^{\tau}_t)}{\sum_{\tau, s_0 \sim \rho_0} e^{\sum_{t=1}^{T}\phi(s^{\tau}_t)^T\omega}} \\
= \sum_{i=1}^{2} \sum_{t=1}^{T}\phi(s^i_t) - 2 \sum_{\tau, s_0 \sim \rho_0} P(\tau|\omega) \sum_{t=1}^{T}\phi(s^{\tau}_t) \\
= \sum_{i=1}^{2} \sum_{t=1}^{T}\phi(s^i_t) - 2 \sum_{s} P(s|\omega, \rho_0)\phi(s)$$ 

Where the distribution in the last term is the state visitation frequency, efficiently computable by dynamic programming:

$$P(s|\omega, \rho_0) = \sum_{t=1}^{T}P^{\pi^*(\omega)}(s_t=s|s_0 \sim \rho_0)$$

We see that the optimal solution is $\omega$ such that the expected feature count under $\omega$ matches 
the empirical feature count of the observed trajectories. Thus a human can manipulate MaxEntIRL by producing 
a trajectory such that the empirical feature count of the observed trajectories matches his own empirical feature count. 
The best response of $H_2$ to $H_1$ and the MaxEntIRL system is then:

$$\tau^*_2(\tau_1) = \min_{\tau_2} \norm{\phi(\tau_2) - (2\mathbb{E}_{\tau \sim \pi^*(w_2), s_0 \sim \rho_0}(\phi(\tau) )- \phi(\tau_1) )$$



# Related Work

Because we compute the best response to an IRL system, our work is similar to Cooperative Inverse Reinforcement Learning. 
In this work, Hadfield-Menell et al. shows that the best response trajectory to an IRL system trying to infer
the preferences of a single human is not the expert trajectory, but rather involve active teaching.

